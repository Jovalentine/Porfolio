<script setup lang="ts">
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { Github, Globe, ShoppingCart, Brain, Database, GraduationCap } from 'lucide-vue-next'

const sectionRef = ref<HTMLElement>()
const isVisible = ref(false)

useIntersectionObserver(sectionRef, ([{ isIntersecting }]) => {
  if (isIntersecting) {
    isVisible.value = true
  }
})

const projects = [
  {
    title: 'Digital Marketing Platform',
    description: 'A comprehensive digital marketing platform built with modern React technologies, featuring responsive design and intuitive user interface for marketing campaigns and analytics.',
    icon: ShoppingCart,
    image: 'https://images.pexels.com/photos/265087/pexels-photo-265087.jpeg?auto=compress&cs=tinysrgb&w=800',
    technologies: [
      'React',
      'TypeScript', 
      'Tailwind CSS',
      'React Router',
      'Lucide Icons',
      'Vite'
    ],
    liveDemo: 'https://digi-market-tan.vercel.app',
    sourceCode: 'https://github.com/Jovalentine/Digi-market',
    category: 'Web Development'
  },
  {
    title: 'SmartDoc Summarizer',
    description: 'An AI-powered document summarization application that uses advanced NLP models to extract key insights from documents, built with Streamlit and integrated with Firebase for authentication.',
    icon: Brain,
    image: 'https://images.pexels.com/photos/8386440/pexels-photo-8386440.jpeg?auto=compress&cs=tinysrgb&w=800',
    technologies: [
      'Streamlit',
      'Python',
      'Hugging Face Transformers',
      'Firebase Authentication',
      'Firestore',
      'BART Model'
    ],
    liveDemo: 'https://smartdoc-huunddjtfi2vkmt28eoc7e.streamlit.app/',
    sourceCode: 'https://github.com/Jovalentine/SmartDoc',
    category: 'AI/ML'
  },
  {
    title: 'CRUD Fullstack Application',
    description: 'A modern full-stack CRUD application for managing contacts, built during my training at Skill Rank company. Features complete CRUD operations with beautiful Material UI design and glassmorphism effects.',
    icon: Database,
    image: 'https://images.pexels.com/photos/574071/pexels-photo-574071.jpeg?auto=compress&cs=tinysrgb&w=800',
    technologies: [
      'React.js',
      'Node.js',
      'Express.js',
      'MongoDB Atlas',
      'Material UI',
      'Mongoose ODM',
      'Axios'
    ],
    liveDemo: 'https://main.d36xn91llc9x07.amplifyapp.com/',
    sourceCode: 'https://github.com/Jovalentine/CRUD-APP.git',
    category: 'Full Stack'
  },
  {
    title: 'Student Result Management System',
    description: 'A comprehensive web-based portal for educational institutions featuring admin and student modules, secure authentication, PDF result generation, and modern Neon/Dark UI theme.',
    icon: GraduationCap,
    image: 'https://images.pexels.com/photos/5212345/pexels-photo-5212345.jpeg?auto=compress&cs=tinysrgb&w=800',
    technologies: [
      'Python',
      'Flask',
      'MongoDB',
      'PyMongo',
      'ReportLab',
      'HTML5/CSS3',
      'Jinja2'
    ],
    liveDemo: 'https://student-result-portal-beige.vercel.app/',
    sourceCode: 'https://github.com/Jovalentine/Student-Result-Portal',
    category: 'Full Stack'
  },
  {
    title: 'Oracle Forensic System',
    description: 'An advanced AI-powered investigation portal for accident reconstruction and forensic analysis. Uses Computer Vision (YOLOv8) and Natural Language Processing (BLIP) to autonomously analyze crime scene images and surveillance footage.',
    icon: Brain,
    image: 'https://images.pexels.com/photos/5668473/pexels-photo-5668473.jpeg?auto=compress&cs=tinysrgb&w=800',
    technologies: [
      'Python',
      'Flask',
      'YOLOv8',
      'BLIP Model',
      'MongoDB Atlas',
      'Docker',
      'Computer Vision'
    ],
    liveDemo: null,
    sourceCode: 'https://github.com/Jovalentine/oracle',
    category: 'AI/ML'
  }
]

const getCategoryColor = (category: string) => {
  switch (category) {
    case 'Web Development': return 'bg-blue-100 text-blue-800'
    case 'AI/ML': return 'bg-purple-100 text-purple-800'
    case 'Full Stack': return 'bg-green-100 text-green-800'
    case 'Education': return 'bg-indigo-100 text-indigo-800'
    default: return 'bg-gray-100 text-gray-800'
  }
}
</script>

<template>
  <section id="projects" ref="sectionRef" class="py-20 bg-white">
    <div class="container-max section-padding">
      <div class="text-center mb-16">
        <h2 
          class="text-4xl md:text-5xl font-bold mb-6 transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          My <span class="gradient-text">Projects</span>
        </h2>
        <div 
          class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-700 mx-auto transition-all duration-1000 delay-200 transform"
          :class="isVisible ? 'scale-x-100 opacity-100' : 'scale-x-0 opacity-0'"
        ></div>
        <p 
          class="text-lg text-secondary-600 mt-6 max-w-2xl mx-auto transition-all duration-1000 delay-300 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          Here are some of the projects I've built that showcase my technical skills and problem-solving abilities
        </p>
      </div>

      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-7xl mx-auto">
        <div 
          v-for="(project, index) in projects" 
          :key="project.title"
          class="card overflow-hidden transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
          :style="{ transitionDelay: `${400 + index * 200}ms` }"
        >
          <!-- Project Image -->
          <div class="relative h-48 overflow-hidden">
            <img 
              :src="project.image" 
              :alt="project.title"
              class="w-full h-full object-cover transition-transform duration-300 hover:scale-110"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
            <div class="absolute top-4 left-4">
              <span :class="[getCategoryColor(project.category), 'px-3 py-1 rounded-full text-sm font-medium']">
                {{ project.category }}
              </span>
            </div>
            <div class="absolute bottom-4 left-4">
              <div class="w-12 h-12 bg-white/20 backdrop-blur-sm rounded-lg flex items-center justify-center">
                <component :is="project.icon" class="w-6 h-6 text-white" />
              </div>
            </div>
          </div>

          <!-- Project Content -->
          <div class="p-6">
            <h3 class="text-xl font-bold text-secondary-900 mb-3">{{ project.title }}</h3>
            <p class="text-secondary-700 mb-4 leading-relaxed">{{ project.description }}</p>

            <!-- Technologies -->
            <div class="mb-6">
              <h4 class="text-sm font-semibold text-secondary-900 mb-2">Technologies Used:</h4>
              <div class="flex flex-wrap gap-2">
                <span 
                  v-for="tech in project.technologies" 
                  :key="tech"
                  class="px-3 py-1 bg-primary-100 text-primary-700 rounded-full text-sm font-medium"
                >
                  {{ tech }}
                </span>
              </div>
            </div>

            <!-- Project Links -->
            <div class="flex gap-4">
              <a 
                v-if="project.liveDemo"
                :href="project.liveDemo" 
                target="_blank"
                rel="noopener noreferrer"
                class="flex-1 btn-primary text-center inline-flex items-center justify-center gap-2 text-sm"
              >
                <Globe class="w-4 h-4" />
                Live Demo
              </a>
              <div v-else class="flex-1 bg-secondary-100 text-secondary-500 text-center py-2 px-4 rounded-lg text-sm font-medium">
                Demo Coming Soon
              </div>
              
              <a 
                :href="project.sourceCode" 
                target="_blank"
                rel="noopener noreferrer"
                class="flex-1 btn-secondary text-center inline-flex items-center justify-center gap-2 text-sm"
              >
                <Github class="w-4 h-4" />
                View Code
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- Additional Info -->
      <div 
        class="mt-16 text-center transition-all duration-1000 delay-800 transform"
        :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
      >
        <div class="card p-8 max-w-4xl mx-auto">
          <h3 class="text-2xl font-bold mb-4 text-secondary-900">More Projects Coming Soon</h3>
          <p class="text-lg text-secondary-700 leading-relaxed">
            I'm constantly working on new projects and exploring emerging technologies. 
            Stay tuned for more exciting developments in web development, AI/ML, and innovative solutions!
          </p>
          <div class="mt-6">
            <a 
              href="https://github.com/Jovalentine" 
              target="_blank"
              rel="noopener noreferrer"
              class="btn-primary inline-flex items-center gap-2"
            >
              <Github class="w-5 h-5" />
              View All Projects on GitHub
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>