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
    default: 100
  },
  pause: {
    type: Number,
    default: 2000
  },
  eraseSpeed: {
    type: Number,
    default: 50
  }
})

const displayedText = ref('')
const currentIndex = ref(0)
const isTyping = ref(true)
let timeoutId = null

const typeText = () => {
  const currentText = props.texts[currentIndex.value]

  if (isTyping.value) {
    if (displayedText.value.length < currentText.length) {
      displayedText.value = currentText.substring(0, displayedText.value.length + 1)
      timeoutId = setTimeout(typeText, props.speed)
    } else {
      isTyping.value = false
      timeoutId = setTimeout(typeText, props.pause)
    }
  } else {
    if (displayedText.value.length > 0) {
      displayedText.value = displayedText.value.substring(0, displayedText.value.length - 1)
      timeoutId = setTimeout(typeText, props.eraseSpeed)
    } else {
      isTyping.value = true
      currentIndex.value = (currentIndex.value + 1) % props.texts.length
      timeoutId = setTimeout(typeText, props.speed)
    }
  }
}

onMounted(() => {
  typeText()
})

onBeforeUnmount(() => {
  clearTimeout(timeoutId)
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

@media(max-width: 768px) {
  .typewriter-text {
    font-size: 30px;
  }
}

</style>