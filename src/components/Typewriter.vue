<template>
  <span class="typewriter-text">{{ displayedText }}</span>
  <span class="typewriter-cursor">|</span>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const props = defineProps({
  texts: {
    type: Array,
    required: true,
    default: () => ['Default Text']
  },
  speed: {
    type: Number,
    default: 100 // milliseconds per character
  },
  pause: {
    type: Number,
    default: 2000 // milliseconds between phrases
  },
  eraseSpeed: {
    type: Number,
    default: 50 // milliseconds per character when erasing
  }
})

const displayedText = ref('')
const currentIndex = ref(0)
const isTyping = ref(true)
let timeoutId = null

const typeText = () => {
  const currentText = props.texts[currentIndex.value]

  if (isTyping.value) {
    // Typing logic
    if (displayedText.value.length < currentText.length) {
      displayedText.value = currentText.substring(0, displayedText.value.length + 1)
      timeoutId = setTimeout(typeText, props.speed)
    } else {
      // Switch to erasing after pause
      isTyping.value = false
      timeoutId = setTimeout(typeText, props.pause)
    }
  } else {
    // Erasing logic
    if (displayedText.value.length > 0) {
      displayedText.value = displayedText.value.substring(0, displayedText.value.length - 1)
      timeoutId = setTimeout(typeText, props.eraseSpeed)
    } else {
      // Move to next text and start typing again
      isTyping.value = true
      currentIndex.value = (currentIndex.value + 1) % props.texts.length
      timeoutId = setTimeout(typeText, props.speed)
    }
  }
}

onMounted(() => {
  typeText() // Start the animation
})

onBeforeUnmount(() => {
  clearTimeout(timeoutId) // Clean up on unmount
})
</script>

<style scoped>
.typewriter-text {
  color: white;
  font-weight: bold;
}

.typewriter-cursor {
  animation: blink 1s step-end infinite;
  color: #42b983;
  font-weight: bold;
}

@keyframes blink {
  from, to { opacity: 1; }
  50% { opacity: 0; }
}
</style>