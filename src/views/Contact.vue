<template>
  <!-- Previous code remains the same until the Social Links section -->
  <div class="min-h-screen bg-gradient-to-br from-gray-900 to-gray-800 text-gray-100">
    <div class="container mx-auto px-6 py-24">
      <div class="max-w-4xl mx-auto">
        <!-- Header Section remains the same -->
        <div class="text-center mb-16">
          <h2 class="text-5xl font-bold mb-4 bg-gradient-to-r from-emerald-400 to-teal-500 bg-clip-text text-transparent">
            Get In Touch
          </h2>
          <p class="text-gray-400 max-w-2xl mx-auto">
            Have a question or want to work together? Drop me a message and I'll get back to you as soon as possible.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
          <!-- Contact Information Card -->
          <div class="bg-gray-800/40 backdrop-blur-sm rounded-2xl p-8 shadow-xl border border-gray-700">
            <h3 class="text-2xl font-bold mb-8 text-emerald-400">Contact Information</h3>
            
            <div class="space-y-6">
              <!-- Email -->
              <div class="flex items-center space-x-4 group">
                <div class="w-12 h-12 rounded-full bg-emerald-400/10 flex items-center justify-center">
                  <i class="fas fa-envelope text-emerald-400 text-xl group-hover:scale-110 transition-transform"></i>
                </div>
                <div>
                  <p class="text-sm text-gray-400">Email</p>
                  <a href="mailto:davidogunkoya80@gmail.com" 
                     class="hover:text-emerald-400 transition-colors">
                     davidogunkoya80@gmail.com
                  </a>
                </div>
              </div>

              <!-- WhatsApp -->
              <div class="flex items-center space-x-4 group">
                <div class="w-12 h-12 rounded-full bg-emerald-400/10 flex items-center justify-center">
                  <i class="fab fa-whatsapp text-emerald-400 text-xl group-hover:scale-110 transition-transform"></i>
                </div>
                <div>
                  <p class="text-sm text-gray-400">WhatsApp</p>
                  <a href="https://wa.me/2348050488519" 
                     target="_blank"
                     class="hover:text-emerald-400 transition-colors">
                    +234 805 048 8519
                  </a>
                </div>
              </div>

              <!-- Location -->
              <div class="flex items-center space-x-4 group">
                <div class="w-12 h-12 rounded-full bg-emerald-400/10 flex items-center justify-center">
                  <i class="fas fa-map-marker-alt text-emerald-400 text-xl group-hover:scale-110 transition-transform"></i>
                </div>
                <div>
                  <p class="text-sm text-gray-400">Location</p>
                  <span>No1 Kudayisi street Ibadan, Nigeria</span>
                </div>
              </div>
            </div>

            <!-- Updated Social Links with Labels -->
            <div class="mt-12">
              <h4 class="font-bold mb-6 text-lg">Connect With Me</h4>
              <div class="flex space-x-8 justify-center">
                <!-- WhatsApp -->
                <a href="https://wa.me/2348050488519" target="_blank" class="group text-center">
                  <div class="w-12 h-12 rounded-full bg-gray-700/50 flex items-center justify-center hover:bg-emerald-400/20 transition-colors mb-2 mx-auto">
                    <i class="fab fa-whatsapp text-xl group-hover:text-emerald-400 transition-colors"></i>
                  </div>
                  <span class="text-sm text-gray-400 group-hover:text-emerald-400 transition-colors">WhatsApp</span>
                </a>
                <!-- Email -->
                <a href="mailto:davidogunkoya80@gmail.com" class="group text-center">
                  <div class="w-12 h-12 rounded-full bg-gray-700/50 flex items-center justify-center hover:bg-emerald-400/20 transition-colors mb-2 mx-auto">
                    <i class="fas fa-envelope text-xl group-hover:text-emerald-400 transition-colors"></i>
                  </div>
                  <span class="text-sm text-gray-400 group-hover:text-emerald-400 transition-colors">Email</span>
                </a>
                <!-- LinkedIn -->
                <a href="https://www.linkedin.com/in/david-ogunkoya-aa31991b7/" target="_blank" class="group text-center">
                  <div class="w-12 h-12 rounded-full bg-gray-700/50 flex items-center justify-center hover:bg-emerald-400/20 transition-colors mb-2 mx-auto">
                    <i class="fab fa-linkedin text-xl group-hover:text-emerald-400 transition-colors"></i>
                  </div>
                  <span class="text-sm text-gray-400 group-hover:text-emerald-400 transition-colors">LinkedIn</span>
                </a>
              </div>
            </div>
          </div>

          <!-- Contact Form Card remains the same -->
          <form @submit.prevent="submitForm" 
                class="bg-gray-800/40 backdrop-blur-sm rounded-2xl p-8 shadow-xl border border-gray-700">
            <div class="space-y-6">
              <div class="relative">
                <label class="block text-sm text-gray-400 mb-2">Full Name</label>
                <input 
                  type="text" 
                  v-model="form.name" 
                  required
                  placeholder="John Doe"
                  class="w-full px-4 py-3 bg-gray-900/50 rounded-lg border border-gray-700 focus:ring-2 focus:ring-emerald-400 focus:border-transparent transition-all placeholder-gray-500">
              </div>

              <div class="relative">
                <label class="block text-sm text-gray-400 mb-2">Email Address</label>
                <input 
                  type="email" 
                  v-model="form.email" 
                  required
                  placeholder="john@example.com"
                  class="w-full px-4 py-3 bg-gray-900/50 rounded-lg border border-gray-700 focus:ring-2 focus:ring-emerald-400 focus:border-transparent transition-all placeholder-gray-500">
              </div>

              <div class="relative">
                <label class="block text-sm text-gray-400 mb-2">Message</label>
                <textarea 
                  v-model="form.message" 
                  required 
                  rows="4"
                  placeholder="Your message here..."
                  class="w-full px-4 py-3 bg-gray-900/50 rounded-lg border border-gray-700 focus:ring-2 focus:ring-emerald-400 focus:border-transparent transition-all placeholder-gray-500"></textarea>
              </div>

              <button 
                type="submit" 
                class="w-full py-4 bg-gradient-to-r from-emerald-500 to-teal-500 hover:from-emerald-600 hover:to-teal-600 rounded-lg transition-all transform hover:scale-[1.02] focus:scale-[0.98] font-medium">
                <span class="flex items-center justify-center space-x-2">
                  <span>Send Message</span>
                  <i class="fas fa-paper-plane"></i>
                </span>
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContactPage',
  data() {
    return {
      form: {
        name: '',
        email: '',
        message: ''
      }
    }
  },
  methods: {
    async submitForm() {
      try {
        // Show loading state
        this.$emit('loading', true)
        
        // Simulated API call - replace with your actual API endpoint
        await new Promise(resolve => setTimeout(resolve, 1000))
        
        console.log('Form submitted:', this.form)
        
        // Reset form
        this.form = {
          name: '',
          email: '',
          message: ''
        }
        
        // Show success message
        alert('Message sent successfully!')
      } catch (error) {
        console.error('Error submitting form:', error)
        alert('There was an error sending your message. Please try again.')
      } finally {
        this.$emit('loading', false)
      }
    }
  }
}
</script>