<template>
  <section class="about-section">
    <div class="card">
      <!-- About Me -->
      <div class="about">
        <h2>About Me</h2>
        <h3>My Hobbies</h3>
        <p>
          Beyond coding, I am a landscape photography enthusiast, 
          I always admire the beauty of nature even if I just see it in photos.
          I also enjoy playing mobile video games such as Mobile Legends: Bang Bang and Call of Duty: Mobile.
          These hobbies fuel my drained energy throughout the busy days.
          A fun fact about me is that I am planning to include skiing and paragliding 
          to my hobbies in the future.
        </p>
      </div>

      <!-- Skills -->
      <div class="skills">
        <h2>My Skills</h2>
        <ul>
          <li>
            <span>Vue.js</span>
            <div class="bar"><div class="fill" style="width: 30%"></div></div>
          </li>
          <li>
            <span>Tailwind CSS</span>
            <div class="bar"><div class="fill" style="width: 65%"></div></div>
          </li>
          <li>
            <span>PHP</span>
            <div class="bar"><div class="fill" style="width: 45%"></div></div>
          </li>
          <li>
            <span>Data Analytics</span>
            <div class="bar"><div class="fill" style="width: 35%"></div></div>
          </li>
          <li>
            <span>Testing</span>
            <div class="bar"><div class="fill" style="width: 60%"></div></div>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script setup>
// no JS needed
</script>

<style scoped>
.about-section {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 5rem 1rem;
  background: linear-gradient(135deg, #f8f9ff, #fef9ff);
}

.card {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  max-width: 1200px;
  width: 100%;
  padding: 4rem;
  border-radius: 25px;
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(25px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.about h2,
.skills h2 {
  font-size: 2rem;
  font-weight: 700;
  color: #2c3e50;
  margin-bottom: 1rem;
}

.about h3 {
  font-size: 1.4rem;
  font-weight: 600;
  color: #6c63ff;
  margin-bottom: 0.5rem;
}

.about p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #555;
}

.skills ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.skills li {
  margin-bottom: 1.5rem;
}

.skills span {
  display: block;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: #333;
}

.bar {
  width: 100%;
  height: 10px;
  background: rgba(0, 0, 0, 0.05);
  border-radius: 10px;
  overflow: hidden;
}

.fill {
  height: 100%;
  background: linear-gradient(90deg, #6c63ff, #42b883);
  border-radius: 10px;
}

@media (max-width: 900px) {
  .card {
    grid-template-columns: 1fr;
    gap: 3rem;
    padding: 3rem;
  }
}

/*Tablet screen size CSS*/
@media (max-width: 1024px) {
  .card {
    gap: 2.5rem;
    padding: 3rem;
  }
  .about h2,
  .skills h2 { font-size: 1.8rem; }
  .about p { font-size: 1.05rem; }
}

/*Mobile layout CSS*/
@media (max-width: 680px) {
  .about-section {
    padding: 3.5rem 1rem;
  }
  .card {
    padding: 1.5rem 1.25rem;
    gap: 2rem;
    border-radius: 18px;
  }
  .about h2,
  .skills h2 { font-size: 1.5rem; }
  .about h3 { font-size: 1.15rem; }
  .about p {
    font-size: 0.98rem;
    line-height: 1.7;
  }
  .skills li { margin-bottom: 1.1rem; }
  .bar { height: 8px; }
}
</style>
