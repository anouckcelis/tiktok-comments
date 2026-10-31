<script setup>
import { reactive, ref, onMounted, onUnmounted } from 'vue'

const messages = reactive([])
const user = ref('')
const text = ref('')

const API_URL = 'https://lab5-p379.onrender.com/api/v1/messages/'

let refreshInterval

async function fetchMessages() {
  try {
    const response = await fetch(API_URL)

    if (!response.ok) {
      throw new Error('Berichten konden niet worden opgehaald')
    }

    const data = await response.json()
    const fetchedMessages = Array.isArray(data)
      ? data
      : data.messages || []

    // Werk de bestaande reactieve lijst bij
    messages.splice(0, messages.length, ...fetchedMessages.reverse())
  } catch (error) {
    console.error('Fout bij het ophalen:', error)
  }
}

onMounted(() => {
  // Berichten ophalen bij het openen van de component
  fetchMessages()

  // Om de 5 seconden controleren op nieuwe berichten
  refreshInterval = setInterval(fetchMessages, 5000)
})

onUnmounted(() => {
  // Stop de automatische updates wanneer de component verdwijnt
  clearInterval(refreshInterval)
})

async function addMessage() {
  if (!user.value.trim() || !text.value.trim()) return

  const newMessage = {
    user: user.value.trim(),
    text: text.value.trim()
  }

  try {
    const response = await fetch(API_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(newMessage)
    })

    if (!response.ok) {
      throw new Error('Bericht kon niet worden verstuurd')
    }

    const savedMessage = await response.json()

    // Toon het nieuwe bericht meteen
    messages.unshift(savedMessage)

    text.value = ''
  } catch (error) {
    console.error('Fout bij het versturen:', error)
  }
}
</script>

<template>
  <section class="chat">
    <h2>Comments</h2>

    <form @submit.prevent="addMessage">
      <input
        v-model="user"
        type="text"
        placeholder="Your username"
        required
      />

      <textarea
        v-model="text"
        placeholder="Write a comment..."
        required
      ></textarea>

      <button type="submit">Post comment</button>
    </form>

    <div class="messages">
      <article
        v-for="(item, index) in messages"
        :key="item._id || item.id || index"
        class="message"
      >
        <strong>{{ item.user }}</strong>
        <p>{{ item.text }}</p>
      </article>
    </div>
  </section>
</template>
