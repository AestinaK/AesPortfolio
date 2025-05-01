<template>
  <div class="about-page">
    <!-- Animated background elements -->
    <div class="decor-circle circle-1"></div>
    <div class="decor-circle circle-2"></div>
    <div class="decor-blob"></div>

    <div class="content-container">
      <!-- Profile section with floating effect -->
      <div class="profile-section" @mousemove="handleParallax">
        <div class="profile-image" ref="profileImage">
          <img src="../assets/profile.jpg" alt="aestina" />
        </div>
        <div class="profile-glow"></div>
      </div>

      <!-- Main content with typewriter effect -->
      <div class="text-content">
        <h1 class="title">
          <span class="greeting">Hello!</span>
          <Typewriter
              :texts="['I\'m Aestina Katwal', 'A .NET Developer', 'A Problem Solver']"
              :speed="100"
          />
        </h1>

        <div class="bio-section">
          <p class="lead-text">
            With <span class="highlight">{{ yearsOfExperience }}+ years</span> crafting robust solutions on the .NET platform
          </p>

          <div class="animated-border-box">
            <p>
              I specialize in building scalable web applications with
              <span class="tech-highlight">C#</span>,
              <span class="tech-highlight">ASP.NET Core</span>, and
              <span class="tech-highlight">Vue.js</span>.
              My passion lies in creating efficient, maintainable code that delivers exceptional user experiences.
            </p>
          </div>
        </div>

        <!-- Skill matrix -->
        <div class="skills-matrix">
          <div
              v-for="(skill, index) in skills"
              :key="index"
              class="skill-item"
              :style="`--skill-level: ${skill.level}`"
          >
            <div class="skill-name">{{ skill.name }}</div>
            <div class="skill-bar">
              <div class="skill-level"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Floating action button -->
      <button class="floating-cta" @click="downloadResume">
        <span>Download Resume</span>
        <svg viewBox="0 0 24 24"><path d="M19 9h-4V3H9v6H5l7 7 7-7zM5 18v2h14v-2H5z"/></svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import Typewriter from '../components/Typewriter.vue'

// Parallax effect for profile image
const profileImage = ref(null)
const handleParallax = (e) => {
  if (profileImage.value) {
    const x = (e.clientX / window.innerWidth) * 20 - 10
    const y = (e.clientY / window.innerHeight) * 20 - 10
    profileImage.value.style.transform = `translate(${x}px, ${y}px)`
  }
}

// Calculate years of experience
const startYear = 2021
const yearsOfExperience = computed(() => new Date().getFullYear() - startYear)

// Skills data
const skills = ref([
  { name: 'C# / .NET', level: 90 },
  { name: 'ASP.NET Core', level: 85 },
  {name:'Javascript',level: 80},
  { name: 'Vue.js', level: 80 },
  { name: 'SQL Server', level: 75 },
  { name: 'Posgresql', level: 75 },
  { name: 'Docker', level: 65 }
])

const downloadResume = () => {
  // Method 1: Direct public folder access (recommended)
  const fileUrl = '/documents/AeljinaKatwal.pdf'
  const link = document.createElement('a')
  link.href = fileUrl
  link.download = 'AeljinaKatwal.pdf' // Custom filename for download
  link.target = '_blank' // Open in new tab as fallback
  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)

}
</script>

<style scoped lang="scss">
.about-page {
  min-height: 100vh;
  width: 100%;
  position: relative;
  overflow: hidden;
  background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
  color: white;
  padding: 1rem 1rem;
  display: flex;
  align-items: center;
  justify-content: center;

  // Decorative elements
  .decor-circle {
    position: absolute;
    border-radius: 50%;
    filter: blur(60px);
    opacity: 0.15;

    &.circle-1 {
      width: 300px;
      height: 300px;
      background: #42b983;
      top: -50px;
      left: -50px;
      animation: float 12s ease-in-out infinite;
    }

    &.circle-2 {
      width: 500px;
      height: 500px;
      background: #ff6b6b;
      bottom: -100px;
      right: -100px;
      animation: float 8s ease-in-out infinite reverse;
    }
  }

  .decor-blob {
    position: absolute;
    width: 600px;
    height: 600px;
    background: rgba(66, 185, 131, 0.05);
    border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    animation: morph 15s ease-in-out infinite;
  }

  .content-container {
    position: relative;
    z-index: 2;
    max-width: 1200px;
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 1.5fr;
    gap: 4rem;
    align-items: center;
  }

  .profile-section {
    position: relative;
    width: 350px;
    height: 450px;
    margin: 0 auto;

    .profile-image {
      width: 100%;
      height: 100%;
      border-radius: 20px;
      overflow: hidden;
      border: 3px solid rgba(255, 255, 255, 0.1);
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
      transition: transform 0.1s ease-out;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }

    .profile-glow {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border-radius: 20px;
      background: radial-gradient(circle at center, rgba(66, 185, 131, 0.4) 0%, transparent 70%);
      z-index: -1;
      animation: pulse 4s ease-in-out infinite;
    }
  }

  .text-content {
    .title {
      font-size: 3.5rem;
      margin-bottom: 1.5rem;
      line-height: 1.2;

      .greeting {
        display: block;
        font-size: 2rem;
        color: #42b983;
        margin-bottom: 0.5rem;
      }
    }

    .lead-text {
      font-size: 1.5rem;
      margin-bottom: 2rem;

      .highlight {
        color: #42b983;
        font-weight: bold;
      }
    }

    .animated-border-box {
      .animated-border-box {
        position: relative;
        padding: 2rem;
        margin-bottom: 3rem;
        border-radius: 10px;
        background:
            linear-gradient(rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0.05)),
            linear-gradient(45deg, #42b983, #2c5364);
        background-origin: border-box;
        background-clip: padding-box, border-box;
        border: 2px solid transparent;
        backdrop-filter: blur(10px);
      }


      .tech-highlight {
        color: #42b983;
        font-weight: 500;
      }
    }
  }

  .skills-matrix {
    display: grid;
    gap: 1rem;

    .skill-item {
      display: grid;
      grid-template-columns: 120px 1fr;
      align-items: center;
      gap: 1rem;

      .skill-name {
        font-weight: 500;
      }

      .skill-bar {
        height: 8px;
        background: rgba(255, 255, 255, 0.1);
        border-radius: 4px;
        overflow: hidden;

        .skill-level {
          height: 100%;
          width: calc(var(--skill-level) * 1%);
          background: linear-gradient(90deg, #42b983, #2c5364);
          border-radius: 4px;
          position: relative;

          &::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(90deg,
                rgba(255,255,255,0.3) 0%,
                rgba(255,255,255,0) 100%);
          }
        }
      }
    }
  }

  .floating-cta {
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    background: linear-gradient(135deg, #42b983, #2c5364);
    color: white;
    border: none;
    padding: 1rem 1.5rem;
    border-radius: 50px;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease;
    z-index: 10;

    &:hover {
      transform: translateY(-5px);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
    }

    svg {
      width: 20px;
      height: 20px;
      fill: currentColor;
    }
  }
}

// Animations
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}

@keyframes pulse {
  0%, 100% { opacity: 0.6; transform: scale(1); }
  50% { opacity: 0.3; transform: scale(1.05); }
}

@keyframes morph {
  0% { border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%; }
  50% { border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%; }
  100% { border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%; }
}

// Responsive adjustments
@media (max-width: 1024px) {
  .content-container {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .profile-section {
    margin-bottom: 3rem;
  }

  .skills-matrix {
    grid-template-columns: 1fr;

    .skill-item {
      grid-template-columns: 1fr;
      text-align: left;
    }
  }
}
</style>