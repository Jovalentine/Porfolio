<script setup lang="ts">
import { ref, reactive } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { Mail, Phone, MapPin, Send, Github, Linkedin, MessageCircle, CheckCircle, X } from 'lucide-vue-next'
import emailjs from '@emailjs/browser'

const sectionRef = ref<HTMLElement>()
const isVisible = ref(false)
const isSubmitting = ref(false)
const showSuccess = ref(false) // Controls the popup visibility
const formRef = ref<HTMLFormElement>() // Reference to the HTML form

useIntersectionObserver(sectionRef, ([{ isIntersecting }]) => {
  if (isIntersecting) {
    isVisible.value = true
  }
})

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const handleSubmit = async () => {
  if (!formRef.value) return

  isSubmitting.value = true
  
  try {
    // -----------------------------------------------------------
    // TODO: Replace these with your actual EmailJS credentials
    // Sign up at https://www.emailjs.com/ to get them (It's free)
    // -----------------------------------------------------------
    const serviceID = 'service_ik6hrk9'
    const templateID = 'template_e1ttsaw'
    const publicKey = '7UN9_rLav1DBelG2Y'

    // Sends the form data directly to your email
    await emailjs.sendForm(serviceID, templateID, formRef.value, publicKey)
    
    // Show the success popup with animation
    showSuccess.value = true
    
    // Reset form fields
    Object.keys(form).forEach(key => {
      form[key as keyof typeof form] = ''
    })
    
  } catch (error) {
    console.error('EmailJS Error:', error)
    alert('Failed to send message. Please check your internet or try again later.')
  } finally {
    isSubmitting.value = false
  }
}

// Contact Info Data
const contactInfo = [
  {
    icon: Mail,
    title: 'Email',
    value: 'joeseno040@gmail.com',
    link: 'mailto:joeseno040@gmail.com'
  },
  {
    icon: Phone,
    title: 'Phone',
    value: '+91 9500210559',
    link: 'tel:+919500210559'
  },
  {
    icon: MapPin,
    title: 'Location',
    value: 'Tirunelveli, Tamil Nadu, India',
    link: '#'
  }
]

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
</script>

<template>
  <section id="contact" ref="sectionRef" class="py-20 bg-white relative">
    <div class="container-max section-padding">
      <div class="text-center mb-16">
        <h2 
          class="text-4xl md:text-5xl font-bold mb-6 transition-all duration-1000 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          Get In <span class="gradient-text">Touch</span>
        </h2>
        <div 
          class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-700 mx-auto transition-all duration-1000 delay-200 transform"
          :class="isVisible ? 'scale-x-100 opacity-100' : 'scale-x-0 opacity-0'"
        ></div>
        <p 
          class="text-lg text-secondary-600 mt-6 max-w-2xl mx-auto transition-all duration-1000 delay-300 transform"
          :class="isVisible ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
        >
          I'm always open to discussing new opportunities, collaborations, or just having a chat about technology
        </p>
      </div>

      <div class="grid lg:grid-cols-2 gap-12">
        <div 
          class="transition-all duration-1000 delay-400 transform"
          :class="isVisible ? 'translate-x-0 opacity-100' : '-translate-x-10 opacity-0'"
        >
          <h3 class="text-2xl font-bold mb-8 text-secondary-900">Let's Connect</h3>
          
          <div class="space-y-6 mb-8">
            <div v-for="info in contactInfo" :key="info.title" class="flex items-center group">
              <div class="w-12 h-12 bg-primary-100 rounded-lg flex items-center justify-center mr-4 group-hover:bg-primary-200 transition-colors duration-200">
                <component :is="info.icon" class="w-6 h-6 text-primary-600" />
              </div>
              <div>
                <h4 class="font-semibold text-secondary-900">{{ info.title }}</h4>
                <a :href="info.link" class="text-secondary-600 hover:text-primary-600 transition-colors duration-200">
                  {{ info.value }}
                </a>
              </div>
            </div>
          </div>

          <div class="mb-8">
            <h4 class="font-semibold text-secondary-900 mb-4">Follow Me</h4>
            <div class="flex space-x-4">
              <a 
                v-for="social in socialLinks" 
                :key="social.name"
                :href="social.url"
                target="_blank"
                class="transition-all duration-200 transform hover:scale-110"
                :class="['text-secondary-600', social.color]"
              >
                <component :is="social.icon" class="w-6 h-6" />
              </a>
            </div>
          </div>

          <div class="card p-6 bg-gradient-to-r from-primary-50 to-primary-100">
            <div class="flex items-center mb-4">
              <MessageCircle class="w-6 h-6 text-primary-600 mr-3" />
              <h4 class="font-semibold text-secondary-900">Ready to Collaborate?</h4>
            </div>
            <p class="text-secondary-700 mb-4">
              I'm actively seeking internship and full-time opportunities. Let's discuss how I can contribute to your team!
            </p>
          </div>
        </div>

        <div 
          class="transition-all duration-1000 delay-600 transform"
          :class="isVisible ? 'translate-x-0 opacity-100' : 'translate-x-10 opacity-0'"
        >
          <div class="card p-8">
            <h3 class="text-2xl font-bold mb-6 text-secondary-900">Send a Message</h3>
            
            <form ref="formRef" @submit.prevent="handleSubmit" class="space-y-6">
              <div class="grid sm:grid-cols-2 gap-6">
                <div>
                  <label for="name" class="block text-sm font-medium text-secondary-700 mb-2">Your Name</label>
                  <input
                    id="name"
                    name="name"
                    v-model="form.name"
                    type="text"
                    required
                    class="w-full px-4 py-3 border border-secondary-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-colors duration-200"
                    placeholder="Enter your name"
                  />
                </div>
                
                <div>
                  <label for="email" class="block text-sm font-medium text-secondary-700 mb-2">Email Address</label>
                  <input
                    id="email"
                    name="email"
                    v-model="form.email"
                    type="email"
                    required
                    class="w-full px-4 py-3 border border-secondary-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-colors duration-200"
                    placeholder="Enter your email"
                  />
                </div>
              </div>

              <div>
                <label for="subject" class="block text-sm font-medium text-secondary-700 mb-2">Subject</label>
                <input
                  id="subject"
                  name="subject"
                  v-model="form.subject"
                  type="text"
                  required
                  class="w-full px-4 py-3 border border-secondary-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-colors duration-200"
                  placeholder="What's this about?"
                />
              </div>

              <div>
                <label for="message" class="block text-sm font-medium text-secondary-700 mb-2">Message</label>
                <textarea
                  id="message"
                  name="message"
                  v-model="form.message"
                  rows="5"
                  required
                  class="w-full px-4 py-3 border border-secondary-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-colors duration-200 resize-none"
                  placeholder="Tell me about your project or opportunity..."
                ></textarea>
              </div>

              <button
                type="submit"
                :disabled="isSubmitting"
                class="w-full btn-primary inline-flex items-center justify-center gap-2"
                :class="{ 'opacity-75 cursor-not-allowed': isSubmitting }"
              >
                <Send v-if="!isSubmitting" class="w-5 h-5" />
                <span v-else class="w-5 h-5 border-2 border-white border-t-transparent rounded-full animate-spin"></span>
                {{ isSubmitting ? 'Sending...' : 'Send Message' }}
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>

    <Transition name="fade">
      <div v-if="showSuccess" class="fixed inset-0 z-50 flex items-center justify-center px-4">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm" @click="showSuccess = false"></div>
        
        <div class="bg-white rounded-2xl p-8 shadow-2xl relative z-10 max-w-md w-full text-center transform transition-all animate-bounce-in">
          <button @click="showSuccess = false" class="absolute top-4 right-4 text-secondary-400 hover:text-secondary-600 transition-colors">
            <X class="w-6 h-6" />
          </button>
          
          <div class="w-20 h-20 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-6">
            <CheckCircle class="w-10 h-10 text-green-600" />
          </div>
          
          <h3 class="text-2xl font-bold text-secondary-900 mb-2">Message Sent!</h3>
          <p class="text-secondary-600 mb-8 leading-relaxed">
            Thanks for reaching out! I've received your message and will get back to you shortly.
          </p>
          
          <button @click="showSuccess = false" class="btn-primary w-full py-3 text-lg">
            Awesome!
          </button>
        </div>
      </div>
    </Transition>
  </section>
</template>

<style scoped>
/* Fade Transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Custom Bounce Animation for Modal */
@keyframes bounce-in {
  0% { transform: scale(0.8); opacity: 0; }
  50% { transform: scale(1.05); opacity: 1; }
  100% { transform: scale(1); opacity: 1; }
}

.animate-bounce-in {
  animation: bounce-in 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
}
</style>