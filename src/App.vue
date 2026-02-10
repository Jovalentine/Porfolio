<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useScroll } from '@vueuse/core'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Experience from './components/Experience.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'

const { y } = useScroll(window)
const isLoaded = ref(false)

onMounted(() => {
  setTimeout(() => {
    isLoaded.value = true
  }, 100)
})
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-secondary-50 to-white">
    <Navbar :scroll-y="y" />
    
    <main class="transition-opacity duration-1000" :class="{ 'opacity-100': isLoaded, 'opacity-0': !isLoaded }">
      <Hero />
      <About />
      <Skills />
      <Projects />
      <Experience />
      <Contact />
    </main>
    
    <Footer />
  </div>
</template>