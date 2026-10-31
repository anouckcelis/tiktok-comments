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
  <iframe
    src="https://www.tiktok.com/player/v1/7702793187370241313"
    title="DisneyNouckie TikTok-video"
    allow="fullscreen"
    allowfullscreen
  ></iframe>
      </div>
      </section>

      <aside class="sidebar">
        <section class="video-description">
            <h2>DisneyNouckie</h2>
            <p>Sharing a little Disney magic ✨</p>
        </section>

        <Chat />
      </aside>
    </main>
  </div>
</template>