<script setup lang="ts">
import { ChevronDown, Download, Github, Linkedin, Mail } from 'lucide-vue-next'
import { onMounted, ref } from 'vue'

const isVisible = ref(false)

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)
})

const scrollToAbout = () => {
  const element = document.querySelector('#about')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <section id="home" class="min-h-screen flex items-center justify-center relative overflow-hidden">
    <div class="absolute inset-0 opacity-5">
      <div class="absolute inset-0 bg-gradient-to-r from-primary-600 to-primary-800"></div>
      <svg class="absolute inset-0 w-full h-full" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
            <path d="M 40 0 L 0 0 0 40" fill="none" stroke="currentColor" stroke-width="1"/>
          </pattern>
        </defs>
        <rect width="100%" height="100%" fill="url(#grid)" />
      </svg>
    </div>

    <div class="container-max section-padding relative z-10">
      <div class="text-center">
        <div 
          class="mb-8 transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          <div class="w-32 h-32 mx-auto rounded-full bg-gradient-to-r from-primary-500 to-primary-700 p-1 shadow-2xl">
            <div class="w-full h-full rounded-full bg-secondary-200 flex items-center justify-center">
              <span class="text-4xl font-bold text-primary-600">FJ</span>
            </div>
          </div>
        </div>

        <div 
          class="transition-all duration-1000 delay-300 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          <h1 class="text-5xl md:text-7xl font-bold mb-6">
            <span class="gradient-text">Francis Johan M</span>
          </h1>
          
          <p class="text-lg md:text-xl text-secondary-700 font-medium max-w-3xl mx-auto leading-relaxed mb-12">
            Software & AI Engineer passionate about leveraging machine learning and full-stack development to solve complex, real-world problems.
          </p>

          <div class="flex flex-col sm:flex-row gap-4 justify-center mb-16">
            <a 
              href="./Resume.pdf" 
              download="Francis_Johan_M_Resume.pdf"
              class="btn-primary inline-flex items-center gap-2"
            >
              <Download class="w-5 h-5" />
              Download Resume
            </a>
            <a 
              href="mailto:joeseno040@gmail.com"
              class="btn-secondary inline-flex items-center gap-2"
            >
              <Mail class="w-5 h-5" />
              Get In Touch
            </a>
          </div>

          <div class="flex justify-center space-x-6 mb-16">
            <a 
              href="https://github.com/Jovalentine" 
              target="_blank"
              rel="noopener noreferrer"
              class="text-secondary-600 hover:text-primary-600 transition-colors duration-200 transform hover:scale-110"
              aria-label="GitHub"
            >
              <Github class="w-6 h-6" />
            </a>
            <a 
              href="https://www.linkedin.com/in/francis-johan-6ba329321" 
              target="_blank"
              rel="noopener noreferrer"
              class="text-secondary-600 hover:text-primary-600 transition-colors duration-200 transform hover:scale-110"
              aria-label="LinkedIn"
            >
              <Linkedin class="w-6 h-6" />
            </a>
            <a 
              href="mailto:joeseno040@gmail.com" 
              class="text-secondary-600 hover:text-primary-600 transition-colors duration-200 transform hover:scale-110"
              aria-label="Email"
            >
              <Mail class="w-6 h-6" />
            </a>
          </div>
        </div>

        <div 
          class="absolute bottom-8 left-1/2 transform -translate-x-1/2 transition-all duration-1000 delay-700"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          <button 
            @click="scrollToAbout"
            class="text-secondary-400 hover:text-primary-600 transition-colors duration-200 animate-bounce-slow"
          >
            <ChevronDown class="w-8 h-8" />
          </button>
        </div>
      </div>
    </div>
  </section>
</template>