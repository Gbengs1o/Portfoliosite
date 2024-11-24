<template>
    <div class="min-h-screen bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900 text-white overflow-hidden">
      <!-- Enhanced animated background -->
      <div class="absolute inset-0 overflow-hidden">
        <div class="absolute top-0 right-0 w-96 h-96 bg-emerald-500/10 rounded-full blur-3xl animate-pulse"></div>
        <div class="absolute bottom-0 left-0 w-96 h-96 bg-emerald-500/10 rounded-full blur-3xl animate-pulse"></div>
        <div class="absolute top-1/2 left-1/4 w-64 h-64 bg-blue-500/10 rounded-full blur-3xl animate-pulse"></div>
        <!-- Animated particles -->
        <div class="particles absolute inset-0"></div>
      </div>
  
      <!-- Main content with improved layout -->
      <div class="relative min-h-screen flex items-center justify-center">
        <div class="container mx-auto px-6 py-12">
          <div class="text-center space-y-8">
            <!-- Enhanced name section with 3D effect -->




            <div class="transform hover:scale-105 transition-transform duration-300">
              <h1 class="text-2xl md:text-7xl font-bold mb-4 animate-gradient bg-gradient-to-r from-white via-emerald-300 to-emerald-500 bg-clip-text text-transparent">
                Ogunkoya Oluwagbenga David
              </h1>
              <div class="h-1 w-32 mx-auto bg-gradient-to-r from-emerald-500 to-blue-500 rounded-full"></div>
            </div>

            
  
            <!-- Role with typewriter effect -->
            <h2 class="text-2xl md:text-4xl font-semibold text-emerald-400 mb-8 typewriter">
              <span class="typing-text">Full-Stack Developer & AI Specialist</span>
            </h2>
  
            <!-- Enhanced description with better typography -->
            <p class="text-xl mb-12 max-w-2xl mx-auto text-gray-300 leading-relaxed font-light">
              Crafting exceptional digital experiences through innovative solutions in web development,
              mobile apps, and artificial intelligence. Turning complex challenges into elegant solutions.
            </p>
  
            <!-- Skills section -->
            <div class="flex flex-wrap justify-center gap-4 mb-12">
              <span v-for="skill in skills" :key="skill" 
                    class="px-4 py-2 bg-emerald-500/10 rounded-full text-emerald-300 border border-emerald-500/20
                           hover:bg-emerald-500/20 transition-all duration-300 transform hover:scale-105">
                {{ skill }}
              </span>
            </div>
  
            <!-- Enhanced CTA buttons -->
            <div class="flex flex-col sm:flex-row justify-center items-center space-y-4 sm:space-y-0 sm:space-x-6">
              <router-link to="/projects"
                class="group px-8 py-3 bg-gradient-to-r from-emerald-500 to-emerald-600 rounded-full 
                       transition-all duration-300 flex items-center space-x-2 transform hover:scale-105
                       hover:shadow-lg hover:shadow-emerald-500/25">
                <span>View My Work</span>
                <ChevronRight class="w-4 h-4 group-hover:translate-x-1 transition-transform" />
              </router-link>
  
              <router-link to="/contact"
                class="group px-8 py-3 border-2 border-emerald-500 rounded-full
                       transition-all duration-300 transform hover:scale-105
                       hover:bg-emerald-500/20 hover:shadow-lg hover:shadow-emerald-500/25">
                <span>Get In Touch</span>
              </router-link>
            </div>
  
            <!-- Enhanced social links with tooltips -->
            <div class="mt-16 flex justify-center space-x-8">
              <a v-for="(social, index) in socials" :key="index"
                 :href="social.href"
                 class="group relative p-3 rounded-full hover:bg-emerald-500/20 transition-all duration-300"
                 target="_blank"
                 rel="noopener noreferrer">
                <component :is="social.icon"
                          class="w-6 h-6 text-emerald-400 group-hover:text-emerald-300 transition-colors" />
                <span class="absolute -bottom-8 left-1/2 transform -translate-x-1/2 
                           opacity-0 group-hover:opacity-100 transition-opacity duration-300
                           text-sm text-emerald-300">
                  {{ social.name }}
                </span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { Github, Linkedin, Twitter, ChevronRight, TicketIcon, ChartAreaIcon, MessageCircleCodeIcon, VideotapeIcon, VideoIcon } from 'lucide-vue-next';
  
  const skills = [
    'Vue.js', 'Next.js','React', 'Angular', 'Node.js', 'Python', 'AI/ML', 'Android Studio', 'AI promting'
  ];
  
  const socials = [
    { 
      icon: Github, 
      href: 'https://github.com/Gbengs1o',
      name: 'GitHub'
    },
    { 
      icon: Linkedin, 
      href: 'https://www.linkedin.com/in/david-ogunkoya-aa31991b7/',
      name: 'LinkedIn'
    },
    { 
      icon: VideoIcon, 
      href: 'https://www.tiktok.com/@.dovekings?_t=8p5D50dlykw&_r=1',
      name: 'TikTok'
    },
    {
      icon: MessageCircleCodeIcon, 
      href: 'https://api.whatsapp.com/send?phone=2348050488519&text=To%20Dovekings%20(Your%20Message)',
      name: 'Whatsapp'
    }
  ];
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
  
  /* Typewriter effect */
  .typing-text {
    border-right: 2px solid #6ee7b7;
    white-space: nowrap;
    overflow: hidden;
    animation: typing 3.5s steps(40, end),
               blink-caret 0.75s step-end infinite;
  }
  
  @keyframes typing {
    from { width: 0 }
    to { width: 100% }
  }
  
  @keyframes blink-caret {
    from, to { border-color: transparent }
    50% { border-color: #6ee7b7 }
  }
  
  /* Particle animation */
  .particles {
    background-image: radial-gradient(circle, #6ee7b7 1px, transparent 1px);
    background-size: 50px 50px;
    animation: particleFlow 20s linear infinite;
    opacity: 0.1;
  }
  
  @keyframes particleFlow {
    0% { transform: translateY(0); }
    100% { transform: translateY(-50px); }
  }
  
  /* Smooth transitions */
  * {
    transition: all 0.3s ease-in-out;
  }
  </style>