<template>
  <svg class="project-illustration" :class="type" viewBox="0 0 200 200">
    <!-- Base card background -->
    <rect width="200" height="200" rx="15" fill="rgba(255,255,255,0.05)" />

    <!-- Dynamic illustration based on project type -->
    <g v-if="type === 'web'">
      <rect x="30" y="40" width="140" height="120" rx="5" fill="#2c5364" />
      <rect x="40" y="50" width="120" height="80" fill="#0f2027" />
      <rect x="60" y="70" width="80" height="10" fill="#42b983" />
      <rect x="60" y="90" width="60" height="10" fill="#42b983" opacity="0.7" />
      <rect x="60" y="110" width="40" height="10" fill="#42b983" opacity="0.5" />
    </g>

    <g v-else-if="type === 'mobile'">
      <rect x="60" y="30" width="80" height="140" rx="10" fill="#2c5364" />
      <rect x="70" y="40" width="60" height="120" fill="#0f2027" />
      <circle cx="100" cy="60" r="15" fill="#42b983" />
      <rect x="75" y="90" width="50" height="8" fill="#42b983" />
      <rect x="75" y="105" width="30" height="8" fill="#42b983" opacity="0.7" />
    </g>

    <g v-else-if="type === 'api'">
      <path d="M30,100 Q100,30 170,100 Q100,170 30,100 Z" fill="#2c5364" />
      <path d="M50,100 Q100,50 150,100 Q100,150 50,100 Z" fill="#0f2027" />
      <circle cx="100" cy="100" r="15" fill="#42b983" />
      <path d="M100,85 L115,100 L100,115 L85,100 Z" fill="none" stroke="#42b983" stroke-width="3" />
    </g>

    <g v-else> <!-- Default design -->
      <rect x="50" y="50" width="100" height="100" rx="10" fill="#2c5364" />
      <path d="M70,70 L130,70 L130,130 L70,130 Z" fill="none" stroke="#42b983" stroke-width="4" stroke-dasharray="5 3" />
      <circle cx="100" cy="100" r="20" fill="#42b983" opacity="0.3" />
    </g>

    <!-- Glow effect -->
    <circle cx="100" cy="100" r="50" fill="#42b983" opacity="0.1" filter="blur(10px)" />
  </svg>
</template>

<script setup>
defineProps({
  type: {
    type: String,
    default: 'web',
    validator: (value) => ['web', 'mobile', 'api', 'default'].includes(value)
  }
})
</script>

<style scoped>
.project-illustration {
  width: 100%;
  height: 200px;
  transition: transform 0.3s ease;

  &.web {
    rect:nth-child(3) { animation: pulse 2s infinite alternate; }
  }

  &.mobile {
    circle { animation: bounce 2s infinite ease-in-out; }
  }

  &.api {
    path:nth-child(3) { animation: rotate 6s infinite linear; }
  }
}

@keyframes pulse {
  0% { opacity: 1; }
  100% { opacity: 0.5; }
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
</style>