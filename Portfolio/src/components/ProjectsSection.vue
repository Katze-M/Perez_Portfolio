<template>
  <section class="projects-section">
    <div class="projects-container">
      <!-- Header -->
      <div class="projects-header">
        <h1>Projects</h1>
        <p>
          A selection of my recent work, showcasing my skills in front-end development as well as surface-level back-end development.
        </p>
      </div>

      <!-- Projects Grid -->
      <div class="projects-grid">
        <ProjectCard
          title="OSAKnows Website"
          description="A fully functional platform for the AdZU Office Of Student Affairs, featuring about OSA page, lost and found, and FAQS section."
          image="/image.png"
        />
        <ProjectCard
          title="Data Analytics Dashboard"
          description="A data analytics dashboard analyzing the patterns and trends in AdZU Scholarships using Microsoft Excel."
          image="/image2.png"
        />
        <ProjectCard
          title="Cleaning Services Website"
          description="A simple dynamic website that has a registration and login feature with the use of PHP and MySql."
          image="/image3.png"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
import ProjectCard from './ProjectCard.vue' //imported ProjectCard component
</script>

<style scoped>
.projects-section {
  font-family: "Space Grotesk", "Noto Sans", sans-serif;
  background: linear-gradient(180deg, #ffffff 0%, #f5f7fa 100%);
  border-top: 1px solid #eaecef;
  border-bottom: 1px solid #eaecef;
  min-height: 100vh;
  padding: 60px 20px;
  box-sizing: border-box;
}

.projects-container {
  max-width: 1500px;
  margin: 0 auto;
}

.projects-header {
  margin-bottom: 40px;
  text-align: center;
}

.projects-header h1 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #2c3e50;
  margin-bottom: 10px;
}

.projects-header p {
  font-size: 1.1rem;
  color: #555;
  max-width: 700px;
  margin: 0 auto;
}

.projects-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
}

@media (min-width: 768px) {
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .projects-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.glassmorphism {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(2px);
  -webkit-backdrop-filter: blur(2px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.group:hover .glassmorphism {
  background: rgba(255, 255, 255, 0.5);
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.37);
}

/* Tablet screen size CSS */
@media (max-width: 1024px) {
  .projects-section { padding: 50px 16px; }
  .projects-header h1 { font-size: 2.2rem; }
  .projects-header p { font-size: 1.02rem; }
}

/* Mobile screen size CSS */
@media (max-width: 680px) {
  .projects-section {
    min-height: auto;
    padding: 40px 14px;
  }
  .projects-header { margin-bottom: 28px; }
  .projects-header h1 { font-size: 1.8rem; }
  .projects-header p {
    font-size: 0.98rem;
    max-width: 95%;
  }
  .projects-grid { gap: 16px; }
}
</style>
