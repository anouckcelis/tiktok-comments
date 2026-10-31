<script setup>
import Chat from './components/Chat.vue'
</script>

<template>
  <div class="tiktok-page">
    <header class="topbar">
      <h1>
        <span class="tiktok-icon">♪</span>
        TikTok
      </h1>
    </header>

    <main class="layout">
      <section class="video-section">
        <div class="video-background">
          <div class="video-placeholder">
            <span class="play-button">▶</span>
            <p>Video preview</p>
          </div>
        </div>
      </section>

      <aside class="sidebar">
        <section class="video-description">
          <h2>sami2bx</h2>
          <p>No space on Metro? 🦄</p>
        </section>

        <Chat />
      </aside>
    </main>
  </div>
</template>