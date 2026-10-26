<template>
  <section class="page-container home-page">
    <div class="hero">
      <p class="eyebrow">HTQT · FRONTEND</p>
      <h1>Xin chào Vue.js</h1>
      <p class="hero-copy">
        Giao diện Vue 3 đã sẵn sàng. Bạn có thể bắt đầu phát triển frontend và kết nối với
        Spring Boot API.
      </p>
      <RouterLink class="button button-primary" to="/demo">
        Thử kết nối API
        <span aria-hidden="true">→</span>
      </RouterLink>
    </div>

    <div class="feature-grid">
      <article class="feature-card">
        <span class="feature-number">01</span>
        <h2>Vue 3 + Vite</h2>
        <p>Phát triển giao diện nhanh với Vue 3, Vite và cấu hình alias <code>@</code>.</p>
      </article>
      <article class="feature-card">
        <span class="feature-number">02</span>
        <h2>Điều hướng</h2>
        <p>Vue Router đã được thiết lập với trang chủ và màn hình kiểm tra API.</p>
      </article>
      <article class="feature-card">
        <span class="feature-number">03</span>
        <h2>Spring Boot</h2>
        <p>Proxy chuyển tiếp yêu cầu <code>/api</code> đến backend tại <code>localhost:8080</code>.</p>
      </article>
    </div>
  </section>
</template>
