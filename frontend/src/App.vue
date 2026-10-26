<template>
  <div class="app-shell">
    <header class="site-header">
      <RouterLink class="brand" to="/" aria-label="HTQT Frontend - Trang chủ">
        <span class="brand-mark">H</span>
        <span>HTQT <span class="brand-light">Frontend</span></span>
      </RouterLink>

      <nav class="main-nav" aria-label="Điều hướng chính">
        <RouterLink to="/">Trang chủ</RouterLink>
        <RouterLink to="/demo">Kết nối API</RouterLink>
      </nav>
    </header>

    <main>
      <RouterView />
    </main>

    <footer class="site-footer">
      Vue 3 · Vite <span aria-hidden="true">·</span> Frontend cho HTQT
    </footer>
  </div>
</template>
