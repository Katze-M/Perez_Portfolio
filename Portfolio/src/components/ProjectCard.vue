<template>
  <div class="project-card">
    <div class="project-image" :style="{ backgroundImage: `url(${image})` }">
      <div class="overlay"></div>
    </div>
    <div class="project-content">
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
      <!-- Link opens the image in a new tab -->
      <a :href="image" target="_blank" class="project-link">
        View Project
        <span class="arrow">→</span>
      </a>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  description: String,
  image: String
})
</script>

<style scoped>
.project-card {
  display: flex;
  flex-direction: column;
  border-radius: 12px;
  overflow: hidden;
  background: #fff;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.2);
}

.project-image {
  position: relative;
  width: 100%;
  aspect-ratio: 16/9;
  background-position: center;
  background-size: cover;
}

.overlay {
  position: absolute;
  inset: 0;
  background: rgba(255,255,255,0);
}

.project-content {
  padding: 20px;
  display: flex;
  flex-direction: column;
}

.project-content h3 {
  margin: 0 0 10px;
  font-size: 1.25rem;
  color: #1a1a1a;
}

.project-content p {
  flex-grow: 1;
  margin: 0 0 15px;
  font-size: 0.9rem;
  color: #555;
}

.project-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  color: #1a1a1a;
  border: 1px solid rgba(0,0,0,0.2);
  border-radius: 8px;
  padding: 8px 16px;
  transition: all 0.3s ease;
}

.project-link:hover {
  background-color: #1a1a1a;
  color: #fff;
}

.arrow {
  margin-left: 8px;
  font-size: 1rem;
}
</style>
