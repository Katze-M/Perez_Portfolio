<script setup>
import { ref, onMounted } from 'vue'
import IntroSection from './components/IntroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import FooterSection from './components/FooterSection.vue'

const isMenuOpen = ref(false)
const activeSectionId = ref('intro')

onMounted(() => {
  const sections = document.querySelectorAll('.fade-section')

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible')
          if (entry.target.id) {
            activeSectionId.value = entry.target.id
          }
        } else {
          entry.target.classList.remove('visible')
        }
      })
    },
    { threshold: 0.5 }
  )

  sections.forEach((section) => observer.observe(section))

  //Observe footer as the contact section
  const contactEl = document.getElementById('contact')
  if (contactEl) {
    const contactObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            activeSectionId.value = 'contact'
          }
        })
      },
      { threshold: 0.3 }
    )
    contactObserver.observe(contactEl)
  }

  //Particle background with mouse interaction
  const canvas = document.getElementById('particles')
  if (canvas) {
    const ctx = canvas.getContext('2d')
    let width = (canvas.width = window.innerWidth)
    let height = (canvas.height = window.innerHeight)

    const particles = Array.from({ length: 100 }, () => ({
      x: Math.random() * width,
      y: Math.random() * height,
      r: Math.random() * 2 + 1,
      dx: (Math.random() - 0.5) * 1,
      dy: (Math.random() - 0.5) * 1
    }))

    //mouse tracker
    const mouse = { x: null, y: null, radius: 150 }
    window.addEventListener('mousemove', (e) => {
      mouse.x = e.x
      mouse.y = e.y
    })
    window.addEventListener('mouseout', () => {
      mouse.x = null
      mouse.y = null
    })

    function animate() {
      ctx.clearRect(0, 0, width, height)

      ctx.fillStyle = 'rgba(32,201,151,0.8)'
      particles.forEach((p) => {
        ctx.beginPath()
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2)
        ctx.fill()

        //movement
        p.x += p.dx
        p.y += p.dy
        if (p.x < 0 || p.x > width) p.dx *= -1
        if (p.y < 0 || p.y > height) p.dy *= -1

        //repel effect near mouse
        if (mouse.x && mouse.y) {
          const dx = p.x - mouse.x
          const dy = p.y - mouse.y
          const dist = Math.sqrt(dx * dx + dy * dy)
          if (dist < mouse.radius) {
            const angle = Math.atan2(dy, dx)
            const force = (mouse.radius - dist) / mouse.radius
            const move = force * 3
            p.x += Math.cos(angle) * move
            p.y += Math.sin(angle) * move
          }
        }
      })

      //connecting lines between particles
      for (let i = 0; i < particles.length; i++) {
        for (let j = i + 1; j < particles.length; j++) {
          const dx = particles[i].x - particles[j].x
          const dy = particles[i].y - particles[j].y
          const dist = Math.sqrt(dx * dx + dy * dy)
          if (dist < 120) {
            ctx.strokeStyle = `rgba(32,201,151,${1 - dist / 120})`
            ctx.lineWidth = 0.6
            ctx.beginPath()
            ctx.moveTo(particles[i].x, particles[i].y)
            ctx.lineTo(particles[j].x, particles[j].y)
            ctx.stroke()
          }
        }
      }

      //connect particles to mouse
      if (mouse.x && mouse.y) {
        particles.forEach((p) => {
          const dx = p.x - mouse.x
          const dy = p.y - mouse.y
          const dist = Math.sqrt(dx * dx + dy * dy)
          if (dist < mouse.radius) {
            ctx.strokeStyle = `rgba(32,201,151,${1 - dist / mouse.radius})`
            ctx.lineWidth = 0.8
            ctx.beginPath()
            ctx.moveTo(p.x, p.y)
            ctx.lineTo(mouse.x, mouse.y)
            ctx.stroke()
          }
        })
      }

      requestAnimationFrame(animate)
    }
    animate()

    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth
      height = canvas.height = window.innerHeight
    })
  }
})
</script>

<template>
  <div class="app-container">
    <!-- Particle canvas background -->
    <canvas id="particles"></canvas>

    <!-- Navbar -->
    <header class="navbar">
      <div class="navbar-container">
        <nav>
          <ul class="nav-links">
            <li><a :class="{ active: activeSectionId === 'intro' }" href="#intro">Home</a></li>
            <li><a :class="{ active: activeSectionId === 'about' }" href="#about">About Me</a></li>
            <li><a :class="{ active: activeSectionId === 'projects' }" href="#projects">Projects</a></li>
            <li><a :class="{ active: activeSectionId === 'contact' }" href="#contact">Contact Me</a></li>
          </ul>

          <!-- Mobile Hamburger -->
          <button class="hamburger" @click="isMenuOpen = !isMenuOpen">☰</button>

          <!-- Mobile menu -->
          <ul v-if="isMenuOpen" class="mobile-menu">
            <li><a :class="{ active: activeSectionId === 'intro' }" href="#intro" @click="isMenuOpen = false">Home</a></li>
            <li><a :class="{ active: activeSectionId === 'about' }" href="#about" @click="isMenuOpen = false">About Me</a></li>
            <li><a :class="{ active: activeSectionId === 'projects' }" href="#projects" @click="isMenuOpen = false">Projects</a></li>
            <li><a :class="{ active: activeSectionId === 'contact' }" href="#contact" @click="isMenuOpen = false">Contact Me</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <!-- Main content -->
    <main>
      <section id="intro" class="fade-section">
        <IntroSection />
      </section>

      <section id="about" class="fade-section">
        <AboutSection />
      </section>

      <section id="projects" class="fade-section">
        <ProjectsSection />
      </section>
    </main>
    <FooterSection />
  </div>
</template>

<style>
/* Global */
@import url('https://fonts.googleapis.com/css2?display=swap&family=Noto+Sans:wght@400;500;700;900&family=Space+Grotesk:wght@400;500;700');
html {
  scroll-behavior: smooth;
  scroll-padding-top: 100px;
  font-family: 'Space Grotesk', 'Noto Sans', sans-serif;
  box-sizing: border-box;
}
*, *::before, *::after { box-sizing: inherit; }
body { margin: 0; background: #f5f5f5; }

.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
}

main {
  flex: 1 0 auto;
  position: relative;
  z-index: 1;
}

/* Particles canvas */
#particles {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

/* Navbar */
.navbar {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(200, 200, 200, 0.5);
  border-radius: 12px;
  padding: 0.5rem 1.5rem;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  z-index: 10;
}
.navbar-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: fit-content;
}
.nav-links {
  display: flex;
  gap: 1.5rem;
  list-style: none;
  margin: 0;
  padding: 0;
}
.nav-links li a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  padding: 6px 12px;
  border-radius: 6px;
  transition: background 0.3s, color 0.3s;
}
.nav-links li a:hover { background: #20c997; color: white; }
.nav-links li a.active { background: #20c997; color: #fff; }

/* Hamburger */
.hamburger {
  display: none;
  font-size: 1.5rem;
  background: none;
  border: none;
  cursor: pointer;
}

/* Mobile Menu */
.mobile-menu {
  position: absolute;
  top: 100%;
  right: 0;
  background: white;
  border: 1px solid #ccc;
  border-radius: 8px;
  list-style: none;
  padding: 1rem 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.mobile-menu li a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  transition: color 0.3s, background 0.3s;
  padding: 6px 12px;
  border-radius: 6px;
}
.mobile-menu li a:hover { background: #20c997; color: white; }
.mobile-menu li a.active { background: #20c997; color: #fff; }

/* Responsive */
@media (max-width: 768px) {
  .nav-links { display: none; }
  .hamburger { display: block; }
}

/* Sections */
main section {
  padding: 6rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

/* Fade animation */
.fade-section {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s ease-out, transform 0.8s ease-out;
}
.fade-section.visible {
  opacity: 1;
  transform: translateY(0);
}
</style>
