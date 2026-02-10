<script setup lang="ts">
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { Code, Database, Globe, Cloud } from 'lucide-vue-next'

const sectionRef = ref<HTMLElement>()
const isVisible = ref(false)

useIntersectionObserver(sectionRef, ([{ isIntersecting }]) => {
  if (isIntersecting) {
    isVisible.value = true
  }
})

const skillCategories = [
  {
    title: 'Programming Languages',
    icon: Code,
    skills: [
      { name: 'Python', level: 80 },
      {name: 'C Basics', level: 50},
      {name: 'C++ Basics', level: 40}
    ]
  },
  {
    title: 'Web Development',
    icon: Globe,
    skills: [
      { name: 'HTML/CSS', level: 85 },
      { name:'React', level : 40}
    ]
  },
  {
    title: 'Database & Backend',
    icon: Database,
    skills: [
      { name: 'Firebase', level: 90 },
      { name: 'MySQL', level: 80 },
      { name: 'MongoDB', level: 70 },
      { name: 'REST APIs', level: 75 }
    ]
  },
  {
    title: 'Cloud & AI/ML',
    icon: Cloud,
    skills: [
      { name: 'AWS', level: 60 },
      { name: 'Machine Learning', level: 65 },
      { name: 'Git/GitHub', level: 85 },
      { name: 'VS Code', level: 90 }
    ]
  }
]
</script>

<template>
  <section id="skills" ref="sectionRef" class="py-20 bg-gradient-to-br from-secondary-50 to-white">
    <div class="container-max section-padding">
      <div class="text-center mb-16">
        <h2 
          class="text-4xl md:text-5xl font-bold mb-6 transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          My <span class="gradient-text">Skills</span>
        </h2>
        <div 
          class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-700 mx-auto transition-all duration-1000 delay-200 transform"
          :class="isVisible ? 'scale-x-100 opacity-100' : 'scale-x-0 opacity-0'"
        ></div>
        <p 
          class="text-lg text-secondary-600 mt-6 max-w-2xl mx-auto transition-all duration-1000 delay-300 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          Here are the technologies and tools I've been working with during my academic journey
        </p>
      </div>

      <div class="grid md:grid-cols-2 lg:grid-cols-2 gap-8">
        <div 
          v-for="(category, index) in skillCategories" 
          :key="category.title"
          class="card p-8 transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
          :style="{ transitionDelay: `${400 + index * 100}ms` }"
        >
          <div class="flex items-center mb-6">
            <div class="w-12 h-12 bg-primary-100 rounded-lg flex items-center justify-center mr-4">
              <component :is="category.icon" class="w-6 h-6 text-primary-600" />
            </div>
            <h3 class="text-xl font-bold text-secondary-900">{{ category.title }}</h3>
          </div>

          <div class="space-y-4">
            <div v-for="skill in category.skills" :key="skill.name" class="skill-item">
              <div class="flex items-center">
                <div class="w-3 h-3 bg-primary-500 rounded-full mr-3"></div>
                <span class="text-secondary-700 font-medium">{{ skill.name }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Additional Skills -->
      <div 
        class="mt-16 text-center transition-all duration-1000 delay-800 transform"
        :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
      >
        <h3 class="text-2xl font-bold mb-6 text-secondary-900">Additional Competencies</h3>
        <div class="flex flex-wrap justify-center gap-3">
          <span 
            v-for="skill in ['Problem Solving', 'Team Collaboration', 'Project Management', 'Technical Documentation', 'Agile Methodology', 'Code Review', 'Docker (Learning)']"
            :key="skill"
            class="px-4 py-2 bg-primary-100 text-primary-700 rounded-full text-sm font-medium hover:bg-primary-200 transition-colors duration-200"
          >
            {{ skill }}
          </span>
        </div>
      </div>
    </div>
  </section>
</template>