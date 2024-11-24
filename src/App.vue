<!-- src/App.vue -->
<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-900 to-black text-white">
    <nav 
      class="fixed w-full z-50 transition-all duration-300"
      :class="[
        scrolled ? 'bg-black/90 backdrop-blur-md py-2 shadow-lg' : 'bg-transparent py-6',
        mobileMenuOpen ? 'bg-black' : ''
      ]"
    >
      <div class="container mx-auto px-4 lg:px-6">
        <div class="flex items-center justify-between">
          <!-- Logo -->
          <router-link 
            to="/" 
            class="relative group flex items-center space-x-2"
          >
            <span class="text-2xl font-bold bg-gradient-to-r from-emerald-400 to-blue-500 bg-clip-text text-transparent">
              OOD
            </span>
            <div class="absolute -bottom-1 left-0 w-0 h-0.5 bg-emerald-400 transition-all group-hover:w-full"></div>
          </router-link>

          <!-- Desktop Navigation -->
          <div class="hidden md:flex items-center space-x-8">
            <router-link 
              v-for="item in navItems" 
              :key="item.path"
              :to="item.path"
              class="relative group py-2"
              v-slot="{ isActive }"
            >
              <span 
                class="relative z-10 transition-colors"
                :class="isActive ? 'text-emerald-400' : 'hover:text-emerald-400'"
              >
                {{ item.name }}
              </span>
              <div 
                class="absolute bottom-0 left-0 w-full h-0.5 bg-emerald-400 transform scale-x-0 group-hover:scale-x-100 transition-transform origin-left"
                :class="{ 'scale-x-100': isActive }"
              ></div>
            </router-link>
            
            <!-- Action Button -->
            <button 
              class="px-4 py-2 bg-gradient-to-r from-emerald-400 to-blue-500 rounded-lg hover:shadow-lg hover:shadow-emerald-500/20 transition-all duration-300 transform hover:-translate-y-0.5"
              @click="handleAction"
            >
              Speak to my AI Assistant
            </button>
          </div>

          <!-- Mobile Menu Button -->
          <button 
            @click="toggleMobileMenu"
            class="md:hidden relative z-50 w-10 h-10 flex items-center justify-center"
            aria-label="Toggle Menu"
          >
            <div class="relative w-6 h-6">
              <span 
                class="absolute w-full h-0.5 bg-white transform transition-all duration-300"
                :class="[
                  mobileMenuOpen ? 'rotate-45 top-3' : 'top-1',
                  'rounded-full'
                ]"
              ></span>
              <span 
                class="absolute w-full h-0.5 bg-white top-3 transform transition-all duration-300"
                :class="[
                  mobileMenuOpen ? 'opacity-0' : 'opacity-100',
                  'rounded-full'
                ]"
              ></span>
              <span 
                class="absolute w-full h-0.5 bg-white transform transition-all duration-300"
                :class="[
                  mobileMenuOpen ? '-rotate-45 top-3' : 'top-5',
                  'rounded-full'
                ]"
              ></span>
            </div>
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <transition
        enter-active-class="transition-all duration-300 ease-out"
        enter-from-class="opacity-0 transform -translate-y-4"
        enter-to-class="opacity-100 transform translate-y-0"
        leave-active-class="transition-all duration-300 ease-in"
        leave-from-class="opacity-100 transform translate-y-0"
        leave-to-class="opacity-0 transform -translate-y-4"
      >
        <div 
          v-if="mobileMenuOpen"
          class="absolute top-full left-0 w-full bg-black/95 backdrop-blur-lg md:hidden"
        >
          <div class="container mx-auto px-4 py-6 space-y-4">
            <router-link 
              v-for="item in navItems"
              :key="item.path"
              :to="item.path"
              class="block py-3 px-4 hover:bg-white/10 rounded-lg transition-colors"
              :class="{ 'text-emerald-400': $route.path === item.path }"
              @click="mobileMenuOpen = false"
            >
              {{ item.name }}
            </router-link>
            <button 
              class="w-full px-4 py-3 bg-gradient-to-r from-emerald-400 to-blue-500 rounded-lg hover:shadow-lg hover:shadow-emerald-500/20 transition-all duration-300"
              @click="handleAction"
            >
              Speak to my AI Assistant
            </button>
          </div>
        </div>
      </transition>
    </nav>

    <transition 
      name="fade" 
      mode="out-in"
      enter-active-class="transition-opacity duration-300"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition-opacity duration-300"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mobileMenuOpen: false,
      scrolled: false,
      navItems: [
        { name: 'Home', path: '/' },
        { name: 'Projects', path: '/projects' },
        { name: 'About', path: '/about' },
       
        { name: 'Contact', path: '/contact' }
      ]
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    toggleMobileMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen
      document.body.style.overflow = this.mobileMenuOpen ? 'hidden' : ''
    },
    handleScroll() {
      this.scrolled = window.scrollY > 20
    },
    handleAction() {
      // Navigate to the AI page
      this.$router.push('/ai')
      // Close mobile menu if open
      if (this.mobileMenuOpen) {
        this.mobileMenuOpen = false
        document.body.style.overflow = ''
      }
    }
  },
  watch: {
    $route() {
      this.mobileMenuOpen = false
      document.body.style.overflow = ''
    }
  }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>