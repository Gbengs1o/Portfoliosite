<script setup>
import { ref, onMounted } from 'vue'
import { 
  Code2, 
  Smartphone, 
  Brain, 
  Wrench,
  GraduationCap,
  User,
  Globe
} from 'lucide-vue-next'

const sections = ref([])
const skillsVisible = ref(false)
const currentImageIndex = ref(0)
const isTransitioning = ref(false)

// Add your image URLs here
const profileImages = [
  '/public/pics1.jpg', // Replace with your actual image URLs
  '/public/pic2.jpg',
  '/public/pic3.jpg',
  '/public/pic4.jpg'
]

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('show')
        if (entry.target.classList.contains('skills-section')) {
          skillsVisible.value = true
        }
      }
    })
  }, { threshold: 0.1 })

  sections.value = document.querySelectorAll('.section-fade')
  sections.value.forEach(section => observer.observe(section))

  // Start the image rotation
  setInterval(() => {
    isTransitioning.value = true
    setTimeout(() => {
      currentImageIndex.value = (currentImageIndex.value + 1) % profileImages.length
      isTransitioning.value = false
    }, 300) // Half the transition time to ensure smooth animation
  }, 3000)
})

const skills = [
  {
    title: 'Frontend Development',
    icon: Code2,
    color: 'text-blue-400',
    bgColor: 'from-blue-500/20 to-blue-600/20',
    items: [
      { name: 'Vue.js', level: 60 },
      { name: 'Next.js', level: 80 },
      { name: 'React.js', level: 90 },
      { name: 'Tailwind CSS', level: 95 },
      { name: 'JavaScript/TypeScript', level: 88 }
    ]
  },
  {
    title: 'Mobile Development',
    icon: Smartphone,
    color: 'text-purple-400',
    bgColor: 'from-purple-500/20 to-purple-600/20',
    items: [
      { name: 'React Native/Expo', level: 85 },
      { name: 'Kotlin (Android)', level: 75 },
      { name: 'Kotlin (Java)', level: 45 },
      { name: 'Mobile Frontend Development', level: 90 }
    ]
  },
  {
    title: 'Backend & AI',
    icon: Brain,
    color: 'text-green-400',
    bgColor: 'from-green-500/20 to-green-600/20',
    items: [
      { name: 'Python', level: 56 },
      { name: 'Node.js', level: 78 },
      { name: 'Generative AI', level: 85 },
      { name: 'AI Chatbot', level: 85 },
      { name: 'TensorFlow', level: 80 },
      { name: 'Flask/Django', level: 88 }
    ]
  },
  {
    title: 'Other Skills',
    icon: Wrench,
    color: 'text-orange-400',
    bgColor: 'from-orange-500/20 to-orange-600/20',
    items: [
      { name: 'WordPress Development', level: 95 },
      { name: 'Git/Version Control', level: 90 },
      { name: 'API Development', level: 85 },
      { name: 'Cloud Services (AWS/GCP)', level: 82 }
    ]
  }
]
</script>

<template>
  <div class="min-h-screen bg-[#0a0c1b] text-white overflow-hidden">
    <div class="absolute inset-0 bg-gradient-to-br from-emerald-500/10 via-blue-500/5 to-purple-500/10" />
    
    <!-- Animated background particles -->
    <div class="absolute inset-0 opacity-20">
      <div v-for="i in 50" :key="i" 
           class="particle absolute rounded-full bg-white"
           :style="{
             left: `${Math.random() * 100}%`,
             top: `${Math.random() * 100}%`,
             width: `${Math.random() * 3}px`,
             height: `${Math.random() * 3}px`,
             animationDelay: `${Math.random() * 2}s`,
             animationDuration: `${Math.random() * 3 + 2}s`
           }" />
    </div>

    <div class="container mx-auto px-4 sm:px-6 py-16 sm:py-24 relative">
      <div class="max-w-5xl mx-auto">
        <!-- Header Section -->
        <div class="text-center mb-20 space-y-6 section-fade">
          <!-- Profile Image Carousel -->
          <div class="relative w-48 h-48 mx-auto mb-8">
            <div 
              class="absolute inset-0 rounded-full overflow-hidden floating-image"
              :class="{ 'fade-out': isTransitioning }"
            >
              <img 
                :src="profileImages[currentImageIndex]" 
                alt="Profile picture"
                class="w-full h-full object-cover"
              />
              <!-- Gradient border -->
              <div class="absolute inset-0 rounded-full border-4 border-transparent bg-gradient-to-r from-emerald-400 via-blue-400 to-purple-400 opacity-75" style="mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0); mask-composite: exclude;" />
            </div>
          </div>

          <h1 class="text-5xl sm:text-6xl font-bold bg-gradient-to-r from-emerald-400 via-blue-400 to-purple-400 bg-clip-text text-transparent">
            About Me
          </h1>
          <p class="text-xl text-gray-400 max-w-2xl mx-auto">
            Bridging the gap between biotechnology and software development
          </p>
          <div class="flex justify-center gap-4 pt-4">
            <a href="/projects" class="px-6 py-3 rounded-full bg-gradient-to-r from-emerald-500 to-blue-500 hover:from-emerald-600 hover:to-blue-600 transition-all duration-300 shadow-lg hover:shadow-emerald-500/25">
              View Projects
            </a>
            <a href="/contact" class="px-6 py-3 rounded-full border border-gray-700 hover:border-emerald-500 transition-all duration-300">
              Contact Me
            </a>
          </div>
        </div>

        <!-- Rest of the content remains the same -->
        <!-- ... (previous sections) ... -->









          <!-- Main Content -->
          <div class="space-y-16">
          <!-- Background Section -->
          <section class="section-fade backdrop-blur-xl bg-white/5 rounded-3xl p-8 sm:p-10 shadow-2xl hover:shadow-emerald-500/10 transition-all duration-500 border border-white/10">
            <div class="flex items-start gap-6">
              <div class="hidden sm:flex items-center justify-center w-16 h-16 rounded-2xl bg-gradient-to-br from-emerald-500/20 to-blue-500/20 flex-shrink-0">
                <Globe class="w-8 h-8 text-emerald-400" />
              </div>
              <div>
                <h2 class="text-3xl font-bold mb-6 text-emerald-400">Background</h2>
                <p class="text-lg leading-relaxed text-gray-300">
                  I have always loved technology from a very young age. It didn't matter that I chose to study biotechnology because it bridges the gap between the research world and the technological or innovative world. During my 100-level days, I got myself a laptop and became a self-taught programmer. Ever since then, I’ve engaged in several projects and have continued to improve steadily.
                </p>
              </div>
            </div>
          </section>

          <!-- Skills Grid -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <template v-for="(skill, index) in skills" :key="index">
              <section class="section-fade skills-section backdrop-blur-xl bg-white/5 rounded-3xl p-8 shadow-2xl hover:shadow-emerald-500/10 transition-all duration-500 border border-white/10 transform hover:-translate-y-1">
                <div class="flex items-start gap-6">
                  <div class="hidden sm:flex items-center justify-center w-14 h-14 rounded-2xl bg-gradient-to-br" :class="skill.bgColor">
                    <component :is="skill.icon" class="w-7 h-7" :class="skill.color" />
                  </div>
                  <div class="flex-1">
                    <h3 class="text-2xl font-bold mb-6" :class="skill.color">{{ skill.title }}</h3>
                    <ul class="space-y-6">
                      <li v-for="(item, itemIndex) in skill.items" 
                          :key="itemIndex"
                          class="space-y-2">
                        <div class="flex justify-between text-gray-300">
                          <span>{{ item.name }}</span>
                          <span class="text-sm" :class="skill.color">{{ item.level }}%</span>
                        </div>
                        <div class="h-2 bg-gray-700/50 rounded-full overflow-hidden">
                          <div 
                            class="h-full rounded-full transition-all duration-1000 ease-out"
                            :class="`bg-gradient-to-r ${skill.color.replace('text', 'from')}-500 ${skill.color.replace('text', 'to')}-600`"
                            :style="{
                              width: skillsVisible ? `${item.level}%` : '0%'
                            }"
                          />
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
              </section>
            </template>
          </div>

          <!-- Education Section -->
          <section class="section-fade backdrop-blur-xl bg-white/5 rounded-3xl p-8 sm:p-10 shadow-2xl hover:shadow-emerald-500/10 transition-all duration-500 border border-white/10">
            <div class="flex items-start gap-6">
              <div class="hidden sm:flex items-center justify-center w-16 h-16 rounded-2xl bg-gradient-to-br from-emerald-500/20 to-blue-500/20">
                <GraduationCap class="w-8 h-8 text-emerald-400" />
              </div>
              <div class="flex-1">
                <h2 class="text-3xl font-bold mb-8 text-emerald-400">Education & Certifications</h2>
                <div class="space-y-8">
                  <div class="relative pl-8 before:absolute before:left-0 before:top-0 before:bottom-0 before:w-1 before:bg-gradient-to-b before:from-emerald-400 before:to-blue-400 before:rounded-full">
                    <h3 class="text-2xl font-bold text-white">Federal University of Technology, Akure (FUTA)</h3>
                    <p class="text-lg text-gray-400 mt-2">B.Tech in Biotechnology</p>
                  </div>
                  
                </div>
              </div>
            </div>
          </section>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.section-fade {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s ease-out;
}

.section-fade.show {
  opacity: 1;
  transform: translateY(0);
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.particle {
  animation: float linear infinite;
}

.floating-image {
  animation: float 3s ease-in-out infinite;
  transition: opacity 0.3s ease-in-out;
}

.fade-out {
  opacity: 0;
}
</style>