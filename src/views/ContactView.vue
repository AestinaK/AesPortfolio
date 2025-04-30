<template>
  <div class="contact-page">
    <!-- Shared decorative elements -->
    <div class="decor-circle circle-1"></div>
    <div class="decor-circle circle-2"></div>
    <div class="decor-blob"></div>

    <div class="content-container">
      <!-- Left side - Contact form -->
      <div class="contact-form-container">
        <h1 class="title">
          <span class="greeting">Get In Touch</span>
          <Typewriter
              :texts="['Let\'s Collaborate', 'Contact Me', 'Build Something Amazing']"
              :speed="100"
          />
        </h1>

        <form @submit.prevent="handleSubmit" class="contact-form">
          <div class="form-group floating">
            <input
                v-model="form.name"
                type="text"
                id="name"
                required
                @focus="activateFloatLabel('name')"
                @blur="checkFloatLabel('name')"
            >
            <label for="name" :class="{ active: floatLabels.name }">Your Name</label>
            <div class="underline"></div>
          </div>

          <div class="form-group floating">
            <input
                v-model="form.email"
                type="email"
                id="email"
                required
                @focus="activateFloatLabel('email')"
                @blur="checkFloatLabel('email')"
            >
            <label for="email" :class="{ active: floatLabels.email }">Email Address</label>
            <div class="underline"></div>
          </div>

          <div class="form-group floating">
            <textarea
                v-model="form.message"
                id="message"
                required
                @focus="activateFloatLabel('message')"
                @blur="checkFloatLabel('message')"
            ></textarea>
            <label for="message" :class="{ active: floatLabels.message }">Your Message</label>
            <div class="underline"></div>
          </div>

          <button type="submit" class="submit-btn">
            <span>Send Message</span>
            <svg viewBox="0 0 24 24">
              <path d="M2.01 21L23 12 2.01 3 2 10l15 2-15 2z"/>
            </svg>
          </button>
        </form>
      </div>

      <!-- Right side - Contact info -->
      <div class="contact-info">
        <div class="info-card glow-card">
          <div class="icon-container">
            <svg viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
          </div>
          <h3>Email</h3>
          <a href="mailto:your.email@example.com">your.email@example.com</a>
        </div>

        <div class="info-card glow-card">
          <div class="icon-container">
            <svg viewBox="0 0 24 24"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/></svg>
          </div>
          <h3>Location</h3>
          <p>City, Country</p>
        </div>

        <div class="info-card glow-card">
          <div class="icon-container">
            <svg viewBox="0 0 24 24"><path d="M20.01 15.38c-1.23 0-2.42-.2-3.53-.56-.35-.12-.74-.03-1.01.24l-1.57 1.97c-2.83-1.35-5.48-3.9-6.89-6.83l1.95-1.66c.27-.28.35-.67.24-1.02-.37-1.11-.56-2.3-.56-3.53 0-.54-.45-.99-.99-.99H4.19C3.65 3 3 3.24 3 3.99 3 13.28 10.73 21 20.01 21c.71 0 .99-.63.99-1.18v-3.45c0-.54-.45-.99-.99-.99z"/></svg>
          </div>
          <h3>Phone</h3>
          <a href="tel:+1234567890">+1 (234) 567-890</a>
        </div>

        <div class="social-links">
          <a v-for="social in socials" :key="social.name" :href="social.url" class="social-icon" target="_blank">
            <component :is="social.icon" />
          </a>
        </div>
      </div>
    </div>

    <!-- Floating decoration -->
    <div class="floating-dots"></div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Typewriter from '../components/Typewriter.vue'
import GithubIcon from '../components/icons/GithubIcon.vue'
import LinkedInIcon from '../components/icons/LinkedInIcon.vue'
import TwitterIcon from '../components/icons/TwitterIcon.vue'

// Form handling
const form = ref({
  name: '',
  email: '',
  message: ''
})

const floatLabels = ref({
  name: false,
  email: false,
  message: false
})

const activateFloatLabel = (field) => {
  floatLabels.value[field] = true
}

const checkFloatLabel = (field) => {
  if (!form.value[field]) {
    floatLabels.value[field] = false
  }
}

const handleSubmit = () => {
  // Handle form submission
  console.log('Form submitted:', form.value)
  // Reset form
  form.value = { name: '', email: '', message: '' }
  Object.keys(floatLabels.value).forEach(key => {
    floatLabels.value[key] = false
  })
}

// Social links
const socials = ref([
  { name: 'github', url: 'https://github.com/yourusername', icon: GithubIcon },
  { name: 'linkedin', url: 'https://linkedin.com/in/yourusername', icon: LinkedInIcon },
  { name: 'twitter', url: 'https://twitter.com/yourusername', icon: TwitterIcon }
])
</script>

<style scoped lang="scss">
.contact-page {
  @extend .about-page; // Shares the same base styles

  .content-container {
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: flex-start;
  }

  .title {
    margin-bottom: 2.5rem;

    .greeting {
      color: #42b983;
    }
  }

  .contact-form {
    display: grid;
    gap: 2rem;

    .form-group {
      position: relative;

      &.floating {
        label {
          position: absolute;
          left: 0;
          top: 0;
          pointer-events: none;
          transition: all 0.3s ease;
          color: rgba(255, 255, 255, 0.7);

          &.active {
            transform: translateY(-25px);
            font-size: 0.9rem;
            color: #42b983;
          }
        }
      }

      input, textarea {
        width: 100%;
        background: transparent;
        border: none;
        border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        color: white;
        padding: 10px 0;
        font-size: 1.1rem;

        &:focus {
          outline: none;

          & ~ .underline {
            width: 100%;
          }
        }
      }

      textarea {
        min-height: 120px;
        resize: vertical;
      }

      .underline {
        position: absolute;
        bottom: 0;
        left: 0;
        height: 2px;
        width: 0;
        background: #42b983;
        transition: width 0.3s ease;
      }
    }

    .submit-btn {
      background: linear-gradient(135deg, #42b983, #2c5364);
      color: white;
      border: none;
      padding: 1rem 2rem;
      border-radius: 50px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;
      cursor: pointer;
      font-size: 1.1rem;
      transition: all 0.3s ease;
      margin-top: 1rem;

      &:hover {
        transform: translateY(-3px);
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);

        svg {
          transform: translateX(5px);
        }
      }

      svg {
        width: 20px;
        height: 20px;
        fill: currentColor;
        transition: transform 0.3s ease;
      }
    }
  }

  .contact-info {
    display: grid;
    gap: 2rem;
    position: sticky;
    top: 2rem;
  }

  .info-card {
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    border-radius: 15px;
    padding: 2rem;
    transition: transform 0.3s ease;

    &:hover {
      transform: translateY(-5px);
    }

    .icon-container {
      width: 50px;
      height: 50px;
      background: rgba(66, 185, 131, 0.1);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 1rem;

      svg {
        width: 24px;
        height: 24px;
        fill: #42b983;
      }
    }

    h3 {
      color: #42b983;
      margin-bottom: 0.5rem;
    }

    a, p {
      color: rgba(255, 255, 255, 0.8);
      transition: color 0.2s ease;

      &:hover {
        color: white;
      }
    }
  }

  .social-links {
    display: flex;
    gap: 1.5rem;
    justify-content: center;
    margin-top: 1rem;

    .social-icon {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.1);
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.3s ease;

      &:hover {
        background: #42b983;
        transform: translateY(-3px);

        :deep(svg) {
          fill: white;
        }
      }

      :deep(svg) {
        width: 20px;
        height: 20px;
        fill: rgba(255, 255, 255, 0.7);
        transition: fill 0.3s ease;
      }
    }
  }

  .floating-dots {
    position: absolute;
    width: 200px;
    height: 200px;
    background-image: radial-gradient(#42b983 2px, transparent 2px);
    background-size: 20px 20px;
    opacity: 0.1;
    bottom: 10%;
    right: 10%;
    animation: float 8s ease-in-out infinite;
  }
}

// Responsive adjustments
@media (max-width: 1024px) {
  .content-container {
    grid-template-columns: 1fr !important;
  }

  .contact-info {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    margin-top: 3rem;
    position: static !important;
  }
}
</style>