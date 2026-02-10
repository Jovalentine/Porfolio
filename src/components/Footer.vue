<script setup lang="ts">
import { Heart, Github, Linkedin, Mail } from 'lucide-vue-next'

const currentYear = new Date().getFullYear()

const socialLinks = [
  {
    icon: Github,
    name: 'GitHub',
    url: 'https://github.com/Jovalentine',
    color: 'hover:text-gray-900'
  },
  {
    icon: Linkedin,
    name: 'LinkedIn',
    url: 'https://www.linkedin.com/in/francis-johan-6ba329321',
    color: 'hover:text-blue-600'
  },
  {
    icon: Mail,
    name: 'Email',
    url: 'mailto:joeseno040@gmail.com',
    color: 'hover:text-red-600'
  }
]

const quickLinks = [
  { name: 'About', href: '#about' },
  { name: 'Skills', href: '#skills' },
  { name: 'Projects', href: '#projects' },
  { name: 'Experience', href: '#experience' },
  { name: 'Contact', href: '#contact' }
]

const scrollToSection = (href: string) => {
  const element = document.querySelector(href)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="bg-secondary-900 text-white">
    <div class="container-max section-padding py-12">
      <div class="grid md:grid-cols-3 gap-8">
        <!-- Brand Section -->
        <div>
          <h3 class="text-2xl font-bold gradient-text mb-4">Francis Johan M</h3>
          <p class="text-secondary-300 mb-6 leading-relaxed">
            Final year engineering student passionate about technology and innovation. 
            Ready to contribute to meaningful projects and grow in the tech industry.
          </p>
          <div class="flex space-x-4">
            <a 
              v-for="social in socialLinks" 
              :key="social.name"
              :href="social.url"
              :target="social.url.startsWith('http') ? '_blank' : undefined"
              :rel="social.url.startsWith('http') ? 'noopener noreferrer' : undefined"
              :class="['text-secondary-400 transition-all duration-200 transform hover:scale-110', social.color]"
              :aria-label="social.name"
            >
              <component :is="social.icon" class="w-6 h-6" />
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div>
          <h4 class="text-lg font-semibold mb-4">Quick Links</h4>
          <ul class="space-y-2">
            <li v-for="link in quickLinks" :key="link.name">
              <button
                @click="scrollToSection(link.href)"
                class="text-secondary-300 hover:text-white transition-colors duration-200 text-left"
              >
                {{ link.name }}
              </button>
            </li>
          </ul>
        </div>

        <!-- Contact Info -->
        <div>
          <h4 class="text-lg font-semibold mb-4">Get In Touch</h4>
          <div class="space-y-2 text-secondary-300">
            <p>📧 joeseno040@gmail.com</p>
            <p>📱 +91 9500210559</p>
            <p>📍 Tirunelveli, Tamil Nadu, India</p>
          </div>
          <div class="mt-6">
            <button
              @click="scrollToSection('#contact')"
              class="btn-primary text-sm"
            >
              Let's Connect
            </button>
          </div>
        </div>
      </div>

      <!-- Bottom Section -->
      <div class="border-t border-secondary-800 mt-12 pt-8">
        <div class="flex flex-col md:flex-row justify-between items-center">
          <p class="text-secondary-400 text-sm mb-4 md:mb-0">
            © {{ currentYear }} Francis Johan M. Made with 
            <Heart class="w-4 h-4 inline text-red-500 mx-1" />
            using Vue.js & Tailwind CSS
          </p>
          
          <button
            @click="scrollToTop"
            class="text-secondary-400 hover:text-white transition-colors duration-200 text-sm"
          >
            Back to Top ↑
          </button>
        </div>
      </div>
    </div>
  </footer>
</template>