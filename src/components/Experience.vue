<script setup lang="ts">
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { GraduationCap, Award, BookOpen, Users, FileText, Briefcase, Lightbulb } from 'lucide-vue-next'

const sectionRef = ref<HTMLElement>()
const isVisible = ref(false)

useIntersectionObserver(sectionRef, ([{ isIntersecting }]) => {
  if (isIntersecting) {
    isVisible.value = true
  }
})

const experiences = [
  {
    title: 'Software Engineer Intern',
    organization: 'Skillrank',
    period: 'Jul 2025 - Aug 2025',
    type: 'Internship',
    icon: Briefcase,
    description: 'Remote internship focused on automating manual processes using cutting-edge technologies including AWS services and Large Language Models.',
    achievements: [
      'Automated manual data entry process for vehicles (new, rental, pre-owned)',
      'Leveraged AWS services for scalable cloud solutions',
      'Implemented Large Language Models (LLMs) for intelligent automation',
      'Worked remotely with international team in Delaware, United States',
      'Gained hands-on experience with enterprise-level automation'
    ]
  },
  {
    title: 'Patent Holder',
    organization: 'Animal Sound Based Audiometry Testing System',
    period: 'Mar 29, 2024',
    type: 'Patent',
    icon: Lightbulb,
    description: 'Innovative patent for improving audiometry testing using animal sounds, particularly beneficial for pediatric testing.',
    achievements: [
      'Patent Number: IN 202441022012',
      'Developed innovative solution for audiometry testing',
      'Focused on child-friendly testing methodology',
      'Addressed challenges in pediatric hearing assessment',
      'Contributed to healthcare technology advancement'
    ]
  },
  {
    title: 'Published Researcher',
    organization: 'International Journal of Scientific Research and Engineering Development',
    period: 'May 2, 2025',
    type: 'Publication',
    icon: FileText,
    description: 'Published research paper on AI-powered document summarization using advanced NLP models.',
    achievements: [
      'Paper: "SmartDoc Summariser AI"',
      'Presented BART model implementation for document summarization',
      'Covered PDF, DOCX, and TXT file processing capabilities',
      'Demonstrated practical AI application in document management',
      'Contributed to academic research in NLP field'
    ]
  },
  {
    title: 'Final Year Engineering Student',
    organization: 'Francis Xavier Engineering College',
    period: '2022 - 2026',
    type: 'Education',
    icon: GraduationCap,
    description: 'Pursuing Bachelor\'s degree in Engineering with focus on practical applications and project-based learning.',
    achievements: [
      'Maintained strong academic performance',
      'Completed multiple technical projects',
      'Active participation in college events',
      'Developed leadership and teamwork skills'
    ]
  },
  {
    title: 'Workshop Participant',
    organization: 'Various Technical Workshops',
    period: '2022 - 2024',
    type: 'Learning',
    icon: BookOpen,
    description: 'Actively participated in technical workshops and training programs to enhance skills.',
    achievements: [
      'Completed workshops on modern web technologies',
      'Gained hands-on experience with industry tools',
      'Networked with industry professionals',
      'Applied learnings to academic projects'
    ]
  },
  {
    title: 'Academic Achievements',
    organization: 'Francis Xavier Engineering College',
    period: '2022 - 2026',
    type: 'Recognition',
    icon: Award,
    description: 'Recognition for academic excellence and contribution to college activities.',
    achievements: [
      'Consistent academic performance',
      'Active participation in technical events',
      'Contribution to college technical magazine',
      'Peer recognition for project work'
    ]
  }
]

const getIconColor = (type: string) => {
  switch (type) {
    case 'Education': return 'text-blue-600'
    case 'Leadership': return 'text-green-600'
    case 'Learning': return 'text-purple-600'
    case 'Recognition': return 'text-orange-600'
    default: return 'text-primary-600'
  }
}

const getBgColor = (type: string) => {
  switch (type) {
    case 'Internship': return 'bg-indigo-100'
    case 'Patent': return 'bg-yellow-100'
    case 'Publication': return 'bg-red-100'
    case 'Education': return 'bg-blue-100'
    case 'Leadership': return 'bg-green-100'
    case 'Learning': return 'bg-purple-100'
    case 'Recognition': return 'bg-orange-100'
    default: return 'bg-primary-100'
  }
}
</script>

<template>
  <section id="experience" ref="sectionRef" class="py-20 bg-gradient-to-br from-secondary-50 to-white">
    <div class="container-max section-padding">
      <div class="text-center mb-16">
        <h2 
          class="text-4xl md:text-5xl font-bold mb-6 transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          My <span class="gradient-text">Journey</span>
        </h2>
        <div 
          class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-700 mx-auto transition-all duration-1000 delay-200 transform"
          :class="isVisible ? 'scale-x-100 opacity-100' : 'scale-x-0 opacity-0'"
        ></div>
        <p 
          class="text-lg text-secondary-600 mt-6 max-w-2xl mx-auto transition-all duration-1000 delay-300 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          My academic journey and experiences that have shaped my technical skills and professional growth
        </p>
      </div>

      <div class="relative">
        <!-- Timeline Line -->
        <div class="absolute left-8 top-0 bottom-0 w-0.5 bg-gradient-to-b from-primary-500 to-primary-700 hidden md:block"></div>

        <div class="space-y-12">
          <div 
            v-for="(experience, index) in experiences" 
            :key="experience.title"
            class="relative transition-all duration-1000 transform"
            :class="isVisible ? 'translate-x-0 opacity-100' : 'translate-x-10 opacity-0'"
            :style="{ transitionDelay: `${400 + index * 200}ms` }"
          >
            <!-- Timeline Dot -->
            <div class="absolute left-6 w-4 h-4 bg-primary-600 rounded-full border-4 border-white shadow-lg hidden md:block"></div>

            <!-- Content Card -->
            <div class="md:ml-20">
              <div class="card p-8">
                <div class="flex items-start justify-between mb-6">
                  <div class="flex items-center">
                    <div :class="[getBgColor(experience.type), 'w-12 h-12 rounded-lg flex items-center justify-center mr-4']">
                      <component :is="experience.icon" :class="[getIconColor(experience.type), 'w-6 h-6']" />
                    </div>
                    <div>
                      <h3 class="text-xl font-bold text-secondary-900">{{ experience.title }}</h3>
                      <p class="text-primary-600 font-medium">{{ experience.organization }}</p>
                    </div>
                  </div>
                  <span class="text-sm text-secondary-500 bg-secondary-100 px-3 py-1 rounded-full">
                    {{ experience.period }}
                  </span>
                </div>

                <p class="text-secondary-700 mb-6 leading-relaxed">
                  {{ experience.description }}
                </p>

                <div>
                  <h4 class="font-semibold text-secondary-900 mb-3">Key Highlights:</h4>
                  <ul class="space-y-2">
                    <li 
                      v-for="achievement in experience.achievements" 
                      :key="achievement"
                      class="flex items-start"
                    >
                      <div class="w-2 h-2 bg-primary-600 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                      <span class="text-secondary-700">{{ achievement }}</span>
                    </li>
                  </ul>
                </div>

                <!-- Special action for Published Researcher -->
                <div v-if="experience.type === 'Publication'" class="mt-6 pt-6 border-t border-secondary-200">
                  <div class="flex flex-col sm:flex-row gap-4">
                    <a 
                      href="https://www.ijsred.com/volume8/issue2/IJSRED-V8I2P436.pdf"
                      target="_blank"
                      rel="noopener noreferrer"
                      class="btn-primary inline-flex items-center justify-center gap-2 text-sm"
                    >
                      <FileText class="w-4 h-4" />
                      View Article
                    </a>
                    <div class="flex flex-col text-sm text-secondary-600">
                      <span><strong>Paper ID:</strong> IJSRED-V8I2P436</span>
                      <span><strong>Pages:</strong> 3008-3015</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Future Goals -->
      <div 
        class="mt-16 text-center transition-all duration-1000 delay-1000 transform"
        :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
      >
        <div class="card p-8 max-w-4xl mx-auto">
          <h3 class="text-2xl font-bold mb-4 text-secondary-900">Looking Forward</h3>
          <p class="text-lg text-secondary-700 leading-relaxed">
            As I approach graduation, I'm excited to transition from academic learning to professional contribution. 
            I'm seeking opportunities where I can apply my technical skills, continue learning, and make a meaningful 
            impact in the technology industry. My goal is to join a dynamic team where I can grow as a professional 
            while contributing to innovative projects.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>