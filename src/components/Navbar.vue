<script setup lang="ts">
import { ref, computed } from 'vue'
import { Menu, X } from 'lucide-vue-next'

interface Props {
  scrollY: number
}

const props = defineProps<Props>()
const isMenuOpen = ref(false)

const isScrolled = computed(() => props.scrollY > 50)

const navItems = [
  { name: 'Home', href: '#home' },
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
  isMenuOpen.value = false
}
</script>

<template>
  <nav 
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="isScrolled ? 'bg-white/95 backdrop-blur-md shadow-lg' : 'bg-transparent'"
  >
    <div class="container-max section-padding">
      <div class="flex items-center justify-between h-16">
        <!-- Logo -->
        <div class="flex-shrink-0">
          <h1 class="text-xl font-bold gradient-text">Francis Johan M</h1>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden md:block">
          <div class="ml-10 flex items-baseline space-x-8">
            <button
              v-for="item in navItems"
              :key="item.name"
              @click="scrollToSection(item.href)"
              class="text-secondary-700 hover:text-primary-600 px-3 py-2 text-sm font-medium transition-colors duration-200 hover:scale-105 transform"
            >
              {{ item.name }}
            </button>
          </div>
        </div>

        <!-- Mobile menu button -->
        <div class="md:hidden">
          <button
            @click="isMenuOpen = !isMenuOpen"
            class="text-secondary-700 hover:text-primary-600 p-2 rounded-md transition-colors duration-200"
          >
            <Menu v-if="!isMenuOpen" class="h-6 w-6" />
            <X v-else class="h-6 w-6" />
          </button>
        </div>
      </div>

      <!-- Mobile Navigation -->
      <div 
        v-if="isMenuOpen"
        class="md:hidden absolute top-16 left-0 right-0 bg-white/95 backdrop-blur-md shadow-lg border-t border-secondary-200"
      >
        <div class="px-2 pt-2 pb-3 space-y-1">
          <button
            v-for="item in navItems"
            :key="item.name"
            @click="scrollToSection(item.href)"
            class="text-secondary-700 hover:text-primary-600 block px-3 py-2 text-base font-medium w-full text-left transition-colors duration-200"
          >
            {{ item.name }}
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>