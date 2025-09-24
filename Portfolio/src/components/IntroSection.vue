<template>
  <section class="intro-section">
    <div class="card">
      <!-- Profile Image -->
      <img
        src="/public/my-photo.JPG"
        alt="Profile"
        class="profile-img"
      />

      <!-- Short Intro About Me -->
      <div class="content">
        <h1 ref="typedText" class="typing-text"></h1>
        <p>
          I’m a passionate
          <span class="highlight">IT Student</span>
          at Ateneo de Zamboanga University, crafting modern, interactive, and responsive websites.
        </p>

      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const typedText = ref(null)
const introText = "Hi, I’m Katrina Perez."

onMounted(() => {
  let i = 0
  const speed = 100 // typing speed in ms (for typing animation)

  function typeWriter() {
    if (i < introText.length) {
      typedText.value.innerHTML += introText.charAt(i)
      i++
      setTimeout(typeWriter, speed)
    } else {
      //Keep cursor blinking for 2 seconds, then hide
      setTimeout(() => {
        typedText.value.classList.add('done')
      }, 2000)
    }
  }

  typeWriter()
})
</script>

<style scoped>
.intro-section {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  padding: 0;
}

/* Card container */
.card {
  display: flex;
  align-items: center;
  gap: 2.5rem;
  background: white;
  border-radius: 16px;
  padding: 3rem 4rem;
  box-shadow: 0 12px 36px rgba(0, 0, 0, 0.15);
  transform: translateY(-30%);
}

/* Profile image */
.profile-img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.15);
}

/* Text content */
.content h1 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #2c3e50;
  margin-bottom: 0.75rem;
  white-space: pre;
  display: inline-block; 
}

/* Typing cursor effect */
.typing-text::after {
  content: '';
  display: inline-block;
  width: 3px;
  height: 1em;
  background-color: #42b883;
  margin-left: 2px;
  vertical-align: text-bottom;
  animation: blink 0.8s steps(1) infinite;
}

.typing-text.done::after {
  display: none; 
}

@keyframes blink {
  0%, 50%, 100% { background-color: #42b883; }
  25%, 75% { background-color: transparent; }
}

.content p {
  font-size: 1.1rem;
  color: #555;
  max-width: 450px;
  margin-bottom: 1.75rem;
}

.highlight {
  color: #42b883;
  font-weight: 600;
}

/* Buttons */
.buttons {
  display: flex;
  gap: 1.2rem;
}

.btn {
  display: inline-block;
  text-decoration: none;
  padding: 0.7rem 1.6rem;
  border-radius: 999px;
  border: none;
  cursor: pointer;
  font-weight: 500;
  background: #f5f5f5;
  color: #333;
  transition: all 0.3s ease;
  text-align: center;
}

.btn.primary {
  background: #555;
  color: white;
}

.btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}
</style>
