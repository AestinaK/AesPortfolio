
<script setup>

</script>
<template>
  <div class="home">
    <section class="hero">
      <div class="container">
        <h1>Hi, I'm <span class="highlight">Aestina Katwal</span></h1>
        <h2>.NET Developer</h2>
        <p>Building scalable web applications with .NET and modern frontend technologies</p>
        <router-link to="/projects" class="cta-button">View My Work</router-link>
      </div>
    </section>

    <section class="skills-section">
      <div class="container">
        <h2>Technical Skills</h2>
        <div class="skills-grid">
          <div class="skill-category">
            <h3>Backend</h3>
            <ul>
              <li>.NET Core / .NET 5+</li>
              <li>C#</li>
              <li>ASP.NET MVC</li>
              <li>Entity Framework</li>
              <li>SQL Server</li>
            </ul>
          </div>
          <div class="skill-category">
            <h3>Frontend</h3>
            <ul>
              <li>Vue.js</li>
              <li>JavaScript/TypeScript</li>
              <li>HTML/CSS/Sass</li>
              <li>Bootstrap/Tailwind</li>
            </ul>
          </div>
          <div class="skill-category">
            <h3>Other</h3>
            <ul>
              <li>Azure DevOps</li>
              <li>Git</li>
              <li>Docker</li>
              <li>REST APIs</li>
            </ul>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>


<style scoped lang="scss">
.home {
  .hero {
    background: linear-gradient(135deg, #42b983, #35495e);
    color: white;
    padding: 100px 0;
    text-align: center;

    .container {
      max-width: 800px;
      margin: 0 auto;
    }

    h1 {
      font-size: 3rem;
      margin-bottom: 20px;

      .highlight {
        color: #ffcc00;
      }
    }

    h2 {
      font-size: 1.8rem;
      font-weight: normal;
      margin-bottom: 20px;
    }

    p {
      font-size: 1.2rem;
      margin-bottom: 30px;
    }

    .cta-button {
      display: inline-block;
      background: white;
      color: #2c3e50;
      padding: 12px 30px;
      border-radius: 30px;
      text-decoration: none;
      font-weight: bold;
      transition: all 0.3s ease;

      &:hover {
        transform: translateY(-3px);
        box-shadow: 0 10px 20px rgba(0,0,0,0.1);
      }
    }
  }

  .skills-section {
    padding: 80px 0;

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 20px;
    }

    h2 {
      text-align: center;
      margin-bottom: 50px;
      font-size: 2rem;
    }

    .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 30px;

      .skill-category {
        background: white;
        padding: 30px;
        border-radius: 8px;
        box-shadow: 0 5px 15px rgba(0,0,0,0.05);

        h3 {
          color: #42b983;
          margin-top: 0;
          margin-bottom: 20px;
          font-size: 1.5rem;
        }

        ul {
          list-style: none;
          padding: 0;

          li {
            padding: 8px 0;
            border-bottom: 1px solid #eee;

            &:last-child {
              border-bottom: none;
            }
          }
        }
      }
    }
  }
}
</style>