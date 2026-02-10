<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { GraduationCap, MapPin, Calendar, Target } from 'lucide-vue-next'

const sectionRef = ref<HTMLElement>()
const isVisible = ref(false)

useIntersectionObserver(sectionRef, ([{ isIntersecting }]) => {
  if (isIntersecting) {
    isVisible.value = true
  }
})
</script>

<template>
  <section id="about" ref="sectionRef" class="py-20 bg-white">
    <div class="container-max section-padding">
      <div class="text-center mb-16">
        <h2 
          class="text-4xl md:text-5xl font-bold mb-6 transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          About <span class="gradient-text">Me</span>
        </h2>
        <div 
          class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-700 mx-auto transition-all duration-1000 delay-200 transform"
          :class="isVisible ? 'scale-x-100 opacity-100' : 'scale-x-0 opacity-0'"
        ></div>
      </div>

      <div class="grid lg:grid-cols-2 gap-12 items-center">
        <!-- Content -->
        <div 
          class="transition-all duration-1000 delay-300 transform"
          :class="isVisible ? 'translate-x-0 opacity-100' : '-translate-x-10 opacity-0'"
        >
          <h3 class="text-2xl md:text-3xl font-bold mb-6 text-secondary-900">
            Passionate Engineering Student Ready to Make an Impact
          </h3>
          
          <p class="text-lg text-secondary-700 mb-6 leading-relaxed">
            As a final year engineering student at Francis Xavier Engineering College, I'm passionate about 
            leveraging technology to solve real-world problems. My academic journey has equipped me with 
            strong analytical skills and a deep understanding of engineering principles.
          </p>
          
          <p class="text-lg text-secondary-700 mb-8 leading-relaxed">
            I'm actively seeking opportunities to apply my knowledge in a professional environment, 
            contribute to innovative projects, and continue learning from industry experts. My goal is 
            to become a valuable team member who can drive technological advancement and create meaningful solutions.
          </p>

          <!-- Info Cards -->
          <div class="grid sm:grid-cols-2 gap-4">
            <div class="card p-6">
              <div class="flex items-center mb-3">
                <GraduationCap class="w-6 h-6 text-primary-600 mr-3" />
                <h4 class="font-semibold text-secondary-900">Education</h4>
              </div>
              <p class="text-secondary-700">Final Year Engineering</p>
              <p class="text-sm text-secondary-500">Francis Xavier Engineering College</p>
            </div>

            <div class="card p-6">
              <div class="flex items-center mb-3">
                <MapPin class="w-6 h-6 text-primary-600 mr-3" />
                <h4 class="font-semibold text-secondary-900">Location</h4>
              </div>
              <p class="text-secondary-700">Tirunelveli</p>
              <p class="text-sm text-secondary-500">Tamil Nadu, India</p>
            </div>

            <div class="card p-6">
              <div class="flex items-center mb-3">
                <Calendar class="w-6 h-6 text-primary-600 mr-3" />
                <h4 class="font-semibold text-secondary-900">Status</h4>
              </div>
              <p class="text-secondary-700">Final Year Student</p>
              <p class="text-sm text-secondary-500">Graduating Soon</p>
            </div>

            <div class="card p-6">
              <div class="flex items-center mb-3">
                <Target class="w-6 h-6 text-primary-600 mr-3" />
                <h4 class="font-semibold text-secondary-900">Goal</h4>
              </div>
              <p class="text-secondary-700">Career Opportunities</p>
              <p class="text-sm text-secondary-500">Ready to Contribute</p>
            </div>
          </div>
        </div>

        <!-- Image/Visual -->
        <div 
          class="transition-all duration-1000 delay-500 transform"
          :class="isVisible ? 'translate-x-0 opacity-100' : 'translate-x-10 opacity-0'"
        >
          <div class="relative">
            <div class="aspect-square rounded-2xl bg-gradient-to-br from-primary-500 to-primary-700 p-8 shadow-2xl">
              <div class="w-full h-full rounded-xl bg-white/10 backdrop-blur-sm flex items-center justify-center">
                <div class="text-center text-white">
                  <GraduationCap class="w-24 h-24 mx-auto mb-4 opacity-80" />
                  <h4 class="text-2xl font-bold mb-2">Engineering Excellence</h4>
                  <p class="text-lg opacity-90">Building Tomorrow's Solutions</p>
                </div>
              </div>
            </div>
            
            <!-- Floating Elements -->
            <div class="absolute -top-4 -right-4 w-20 h-20 bg-primary-200 rounded-full opacity-60 animate-bounce-slow"></div>
            <div class="absolute -bottom-4 -left-4 w-16 h-16 bg-primary-300 rounded-full opacity-40 animate-bounce-slow" style="animation-delay: 1s;"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>