<script setup>
import { onMounted, ref } from 'vue'
import api from '@/api/axios'

const items = ref([])
const isLoading = ref(false)
const errorMessage = ref('')

async function loadDemo() {
  isLoading.value = true
  errorMessage.value = ''

  try {
    const response = await api.get('/demo')

    if (!Array.isArray(response.data) || !response.data.every((item) => typeof item === 'string')) {
      throw new Error('API cần trả về một danh sách JSON gồm các chuỗi.')
    }

    items.value = response.data
  } catch (error) {
    items.value = []

    if (error.response) {
      errorMessage.value = `Backend trả về lỗi HTTP ${error.response.status}.`
    } else if (error.code === 'ECONNABORTED') {
      errorMessage.value = 'Yêu cầu đã hết thời gian chờ. Vui lòng thử lại.'
    } else if (error.message === 'API cần trả về một danh sách JSON gồm các chuỗi.') {
      errorMessage.value = error.message
    } else {
      errorMessage.value =
        'Không thể kết nối đến backend. Hãy kiểm tra Spring Boot tại http://localhost:8080.'
    }
  } finally {
    isLoading.value = false
  }
}

onMounted(loadDemo)
</script>

<template>
  <section class="page-container demo-page">
    <p class="eyebrow">TÍCH HỢP BACKEND</p>
    <div class="page-heading">
      <div>
        <h1>Danh sách dữ liệu</h1>
        <p class="page-description">Dữ liệu được tải từ endpoint <code>GET /api/demo</code>.</p>
      </div>
      <button class="button button-secondary" type="button" :disabled="isLoading" @click="loadDemo">
        {{ isLoading ? 'Đang tải...' : 'Tải lại' }}
      </button>
    </div>

    <div v-if="isLoading" class="status-card" role="status">
      <span class="loader" aria-hidden="true"></span>
      Đang tải dữ liệu từ Spring Boot...
    </div>

    <div v-else-if="errorMessage" class="status-card status-error" role="alert">
      <div>
        <strong>Chưa tải được dữ liệu</strong>
        <p>{{ errorMessage }}</p>
      </div>
      <button class="button button-secondary" type="button" @click="loadDemo">Thử lại</button>
    </div>

    <div v-else-if="items.length === 0" class="status-card">
      Backend đã phản hồi nhưng danh sách hiện đang trống.
    </div>

    <ul v-else class="data-list">
      <li v-for="(item, index) in items" :key="`${index}-${item}`">
        <span class="list-index">{{ String(index + 1).padStart(2, '0') }}</span>
        <span>{{ item }}</span>
      </li>
    </ul>

    <p class="api-note">
      Đảm bảo backend đang chạy và có endpoint <code>GET /api/demo</code> trả về JSON dạng mảng.
    </p>
  </section>
</template>
