<template>
    <div class="min-h-screen bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900 text-white">
      <!-- Background elements -->
      <div class="absolute inset-0 overflow-hidden">
        <div class="absolute top-20 right-20 w-96 h-96 bg-emerald-500/5 rounded-full blur-3xl animate-pulse"></div>
        <div class="absolute bottom-20 left-20 w-96 h-96 bg-blue-500/5 rounded-full blur-3xl animate-pulse"></div>
      </div>
  
      <div class="container mx-auto px-6 py-24 relative">
        <!-- Enhanced header section -->
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold mb-6 bg-gradient-to-r from-white via-emerald-300 to-emerald-500 bg-clip-text text-transparent animate-gradient">
            Featured Projects
          </h2>
          <div class="h-1 w-24 mx-auto bg-gradient-to-r from-emerald-500 to-blue-500 rounded-full"></div>
          <p class="text-gray-300 mt-6 max-w-2xl mx-auto">
            Explore my latest work in web development, mobile applications, and artificial intelligence.
          </p>
        </div>
  
        <!-- Project filters -->
        <div class="flex flex-wrap justify-center gap-4 mb-12">
          <button v-for="category in categories" 
                  :key="category"
                  @click="filterCategory = category"
                  :class="[
                    'px-4 py-2 rounded-full transition-all duration-300 text-sm',
                    filterCategory === category 
                      ? 'bg-emerald-500 text-white' 
                      : 'bg-emerald-500/10 text-emerald-300 hover:bg-emerald-500/20'
                  ]">
            {{ category }}
          </button>
        </div>
  
        <!-- Enhanced projects grid -->
        <TransitionGroup 
          tag="div"
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
          name="projects"
        >
          <div v-for="project in filteredProjects" 
               :key="project.id"
               class="group relative bg-gray-800/50 backdrop-blur-sm rounded-xl overflow-hidden
                      transform transition-all duration-500 hover:scale-105 hover:shadow-xl
                      hover:shadow-emerald-500/10">
            <!-- Project image with overlay -->
            <div class="relative overflow-hidden h-48">
              <img :src="project.image" 
                   :alt="project.title" 
                   class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110">
              <div class="absolute inset-0 bg-gradient-to-t from-gray-900/90 to-transparent"></div>
            </div>
  
            <!-- Project content -->
            <div class="p-6">
              <h3 class="text-xl font-bold mb-3 text-white group-hover:text-emerald-400 transition-colors">
                {{ project.title }}
              </h3>
              <p class="text-gray-300 mb-4 line-clamp-3">{{ project.description }}</p>
  
              <!-- Technologies -->
              <div class="flex flex-wrap gap-2 mb-6">
                <span v-for="tech in project.technologies" 
                      :key="tech"
                      class="px-3 py-1 bg-emerald-500/10 text-emerald-400 rounded-full text-sm
                             transform transition-all duration-300 hover:scale-105 hover:bg-emerald-500/20">
                  {{ tech }}
                </span>
              </div>
  
              <!-- Project links -->
              <div class="flex justify-between items-center">
                <a :href="project.link" 
                   target="_blank"
                   class="inline-flex items-center space-x-2 text-emerald-400 hover:text-emerald-300 
                          transition-colors group/link">
                  <span>View Project</span>
                  <ArrowRight class="w-4 h-4 transform transition-transform group-hover/link:translate-x-1" />
                </a>
  
                <!-- GitHub link -->
                <a :href="project.github" 
                   target="_blank"
                   class="p-2 rounded-full hover:bg-emerald-500/20 transition-colors">
                  <Github class="w-5 h-5 text-emerald-400" />
                </a>
              </div>
  
              <!-- Project status badge -->
              <div class="absolute top-4 right-4 px-3 py-1 rounded-full text-xs font-medium"
                   :class="{
                     'bg-green-500/20 text-green-400': project.status === 'Completed',
                     'bg-yellow-500/20 text-yellow-400': project.status === 'In Progress',
                     'bg-blue-500/20 text-blue-400': project.status === 'Featured'
                   }">
                {{ project.status }}
              </div>
            </div>
          </div>
        </TransitionGroup>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  import { Github, ArrowRight } from 'lucide-vue-next'
  
  const filterCategory = ref('All')
  
  const categories = ['All', 'Web', 'Mobile', 'AI/ML']
  
  const projects = [
    {
      id: 1,
      title: 'AI-Powered Education platform',
      description: 'This is also another startup of mine where the goal is simple use the advancements in technology for example AI to increase learning among student. Helping them with subjects and topics they dont understand.',
      image: '/public/foreface.jpg',
      technologies: ['AndroidStudio', 'ReactNative', 'Next.js', 'Node.js'],
      link: 'https://getin2school.vercel.app/',
      github: 'https://github.com/Gbengs1o',
      category: 'Web',
      status: 'Featured'
    },
    {
      id: 2,
      title: 'DoveKings',
      description: 'This is a start up of Mine with the goal of utilizing AI and other technologies to 2x the rate and efficiency to which things will be done in various fields.',
      image: '/public/dk.png',
      technologies: ['React Native', 'Expo', 'Firebase', 'Stripe'],
      link: 'https://dovekings.com/',
      github: 'https://github.com/Gbengs1o',
      category: 'Web',
      status: 'Completed continuous update every week'
    },
    {
      id: 3,
      title: 'Alive',
      description: 'This is a project aimed to making sites and other technologies for example mobile apps more intelligent in other for them to achieve their goals better in both my projects above you i have implemented advanced chatbot that can navigate through site ages and more this is all thans to the Alive project.',
      image: '/public/4.jpeg',
      technologies: ['Vue.js', 'reac.js', 'Next.js', 'Node.js'],
      link: '#',
      github: 'https://github.com/Gbengs1o',
      category: 'AI/ML',
      status: 'In Progress'
    },
    {
    id: 4,
      title: 'Educate',
      description: 'This is part of the getin2school project where mobile apps are being developed with the aim to hel students significantly boost their academics.',
      image: '/public/2.jpeg',
      technologies: ['ReactNative','Android Studio'],
      link: 'https://getin2school.vercel.app/collection/',
      github: 'https://github.com/Gbengs1o',
      category: 'Mobile',
      status: 'In Progress'
    },


    {
    id: 5,
      title: 'FastTrack',
      description: 'A project that incorporates ai workflow and can help Developers code 10X faster',
      image: '/public/ft.jpeg',
      technologies: ['ReactNative','python'],
      link: '#',
      github: 'https://github.com/Gbengs1o',
      category: 'AI/ML',
      status: 'In Progress'
    }




  ]
  
  const filteredProjects = computed(() => {
    if (filterCategory.value === 'All') return projects
    return projects.filter(project => project.category === filterCategory.value)
  })
  </script>
  
  <style scoped>
  /* Gradient animation */
  @keyframes gradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  .animate-gradient {
    background-size: 200% auto;
    animation: gradient 8s linear infinite;
  }
  
  /* Projects transition group animations */
  .projects-enter-active,
  .projects-leave-active {
    transition: all 0.5s ease;
  }
  
  .projects-enter-from,
  .projects-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }
  
  /* Hover animations */
  .group:hover .group-hover\:scale-110 {
    transform: scale(1.1);
  }
  
  /* Line clamp for descriptions */
  .line-clamp-3 {
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  </style>