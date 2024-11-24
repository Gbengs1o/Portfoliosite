<template>
    <div class="min-h-screen bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900 text-white p-4">
      <!-- Background effects -->
      <div class="absolute inset-0 overflow-hidden">
        <div class="absolute top-0 right-0 w-96 h-96 bg-emerald-500/10 rounded-full blur-3xl animate-pulse"></div>
        <div class="absolute bottom-0 left-0 w-96 h-96 bg-emerald-500/10 rounded-full blur-3xl animate-pulse"></div>
      </div>
  
      <!-- Main chat container -->
      <div class="relative max-w-4xl mx-auto h-[85vh] flex flex-col rounded-2xl backdrop-blur-sm bg-gray-900/50 border border-emerald-500/20">
        <!-- Chat header with settings -->
        <div class="p-4 border-b border-emerald-500/20 flex justify-between items-center">
          <h2 class="text-2xl font-bold bg-gradient-to-r from-white via-emerald-300 to-emerald-500 bg-clip-text text-transparent">
            AI Assistant
          </h2>
          <div class="flex items-center space-x-3">
            <button 
              @click="toggleTheme"
              class="p-2 rounded-full bg-emerald-500/20 hover:bg-emerald-500/30 transition-all"
            >
              <component :is="isDarkMode ? SunIcon : MoonIcon" class="w-5 h-5 text-emerald-400"/>
            </button>
            <button 
              @click="clearChat"
              class="p-2 rounded-full bg-emerald-500/20 hover:bg-emerald-500/30 transition-all"
            >
              <TrashIcon class="w-5 h-5 text-emerald-400"/>
            </button>
          </div>
        </div>
  
        <!-- Messages container with typing indicator -->
        <div class="flex-1 overflow-y-auto p-4 space-y-4" ref="messagesContainer">
          <div v-for="(message, index) in messages" 
               :key="index" 
               :class="['message-wrapper', message.role === 'user' ? 'justify-end' : 'justify-start']"
               class="flex w-full">
            <div :class="[
              'max-w-[80%] rounded-2xl p-3 space-y-2',
              message.role === 'user' 
                ? 'bg-emerald-500/20 border border-emerald-500/30' 
                : 'bg-gray-800/80 border border-gray-700'
            ]">
              <div class="flex items-start space-x-2">
                <div class="w-8 h-8 rounded-full bg-emerald-500/20 flex items-center justify-center">
                  <component :is="message.role === 'user' ? UserIcon : BotIcon" class="w-5 h-5 text-emerald-400"/>
                </div>
                <div class="flex-1">
                  <p class="text-gray-100">{{ message.content }}</p>
                  <span class="text-xs text-gray-400">{{ formatTimestamp(message.timestamp) }}</span>
                </div>
              </div>
              
              <!-- Audio player with enhanced visualization -->
              <div v-if="message.audio" class="flex items-center space-x-2 mt-2">
                <button @click="toggleAudio(message)" 
                        class="p-2 rounded-full bg-emerald-500/20 hover:bg-emerald-500/30 transition-all">
                  <component :is="message.isPlaying ? PauseIcon : PlayIcon" 
                            class="w-4 h-4 text-emerald-400"/>
                </button>
                <!-- Enhanced audio waveform visualization -->
                <div class="h-8 flex items-center space-x-0.5 flex-1">
                  <div v-for="i in 40" :key="i"
                       :class="[
                         'w-0.5 rounded-full transition-all duration-200',
                         message.isPlaying ? 'bg-emerald-400' : 'bg-emerald-400/60',
                         message.isPlaying ? `h-${Math.floor(Math.random() * 6 + 2)}` : 'h-2'
                       ]">
                  </div>
                </div>
                <!-- Audio duration -->
                <span class="text-xs text-gray-400">{{ formatDuration(message.audioDuration) }}</span>
              </div>
            </div>
          </div>
          <!-- Typing indicator -->
          <div v-if="isTyping" class="flex items-center space-x-2 text-emerald-400">
            <div class="typing-dot"></div>
            <div class="typing-dot animation-delay-200"></div>
            <div class="typing-dot animation-delay-400"></div>
          </div>
        </div>
  
        <!-- Enhanced input area -->
        <div class="p-4 border-t border-emerald-500/20 space-y-3">
          <div class="relative">
            <textarea 
              v-model="newMessage" 
              @keyup.enter.exact="sendMessage"
              @keyup.enter.shift.exact="newMessage += '\n'"
              placeholder="Type a message... (Shift + Enter for new line)"
              :disabled="isRecording"
              class="w-full bg-gray-800/50 border border-emerald-500/20 rounded-xl p-3 text-white placeholder-gray-400 focus:outline-none focus:border-emerald-500/50 transition-all resize-none pr-12"
              :rows="textareaRows"
              @input="adjustTextareaHeight"
            ></textarea>
            <div class="absolute right-3 bottom-3">
              <button 
                v-if="newMessage.trim()"
                @click="sendMessage"
                class="p-2 rounded-full bg-emerald-500 hover:bg-emerald-600 transition-all"
              >
                <SendIcon class="w-4 h-4 text-white"/>
              </button>
            </div>
          </div>
          
          <div class="flex justify-between items-center">
            <!-- Recording indicator with timer -->
            <div v-if="isRecording" class="flex items-center space-x-2 text-emerald-400">
              <div class="w-2 h-2 rounded-full bg-red-500 animate-pulse"></div>
              <span>Recording... {{ formatRecordingTime }}</span>
            </div>
            
            <!-- Action buttons -->
            <div class="flex space-x-3">
              <button 
                @click="toggleRecording"
                :class="[
                  'flex items-center space-x-2 px-4 py-2 rounded-xl transition-all',
                  isRecording 
                    ? 'bg-red-500/20 text-red-400 hover:bg-red-500/30'
                    : 'bg-emerald-500/20 text-emerald-400 hover:bg-emerald-500/30'
                ]"
              >
                <component :is="isRecording ? StopCircleIcon : MicIcon" class="w-5 h-5"/>
                <span>{{ isRecording ? 'Stop' : 'Voice' }}</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed, onMounted, watch } from 'vue';
  import axios from 'axios';
  import { 
    Mic as MicIcon,
    StopCircle as StopCircleIcon,
    Play as PlayIcon,
    Pause as PauseIcon,
    Send as SendIcon,
    Sun as SunIcon,
    Moon as MoonIcon,
    Trash as TrashIcon,
    User as UserIcon,
    Bot as BotIcon
  } from 'lucide-vue-next';
  
  const messages = ref([]);
  const newMessage = ref('');
  const isRecording = ref(false);
  const mediaRecorder = ref(null);
  const messagesContainer = ref(null);
  const recordingStartTime = ref(null);
  const recordingTimer = ref(null);
  const isTyping = ref(false);
  const isDarkMode = ref(true);
  const textareaRows = ref(1);
  
  // Computed property for recording time display
  const formatRecordingTime = computed(() => {
    if (!recordingStartTime.value) return '00:00';
    const elapsed = Math.floor((Date.now() - recordingStartTime.value) / 1000);
    const minutes = Math.floor(elapsed / 60).toString().padStart(2, '0');
    const seconds = (elapsed % 60).toString().padStart(2, '0');
    return `${minutes}:${seconds}`;
  });
  
  // Watch for changes in messages to scroll to bottom
  watch(messages, () => {
    scrollToBottom();
  }, { deep: true });
  
  const scrollToBottom = () => {
    setTimeout(() => {
      if (messagesContainer.value) {
        messagesContainer.value.scrollTop = messagesContainer.value.scrollHeight;
      }
    }, 100);
  };
  
  const adjustTextareaHeight = () => {
    const lines = newMessage.value.split('\n').length;
    textareaRows.value = Math.min(Math.max(1, lines), 5);
  };
  
  const formatTimestamp = (timestamp) => {
    if (!timestamp) return '';
    const date = new Date(timestamp);
    return date.toLocaleTimeString(undefined, { 
      hour: '2-digit', 
      minute: '2-digit'
    });
  };
  
  const formatDuration = (duration) => {
    if (!duration) return '00:00';
    const minutes = Math.floor(duration / 60).toString().padStart(2, '0');
    const seconds = Math.floor(duration % 60).toString().padStart(2, '0');
    return `${minutes}:${seconds}`;
  };
  
  const toggleTheme = () => {
    isDarkMode.value = !isDarkMode.value;
    // Add theme switching logic here
  };
  
  const clearChat = () => {
    if (confirm('Are you sure you want to clear all messages?')) {
      messages.value = [];
    }
  };
  
  const sendMessage = async (event) => {
    if (event) event.preventDefault();
    if (!newMessage.value.trim() || isRecording.value) return;
  
    try {
      // Add user message
      messages.value.push({
        role: 'user',
        content: newMessage.value,
        timestamp: new Date()
      });
  
      // Set typing indicator
      isTyping.value = true;
  
      // Send to backend
      const response = await axios.post('https://portfolio-backend-1-smcg.onrender.com/api/chat', {
        text: newMessage.value
      });
  
      // Clear typing indicator
      isTyping.value = false;
  
      // Add AI response
      messages.value.push({
        role: 'assistant',
        content: response.data.message,
        audio: response.data.audio,
        timestamp: new Date(),
        audioDuration: response.data.audioDuration
      });
  
      newMessage.value = '';
      textareaRows.value = 1;
      scrollToBottom();
    } catch (error) {
      console.error('Error sending message:', error);
      isTyping.value = false;
      messages.value.push({
        role: 'assistant',
        content: 'Sorry, there was an error processing your message.',
        timestamp: new Date()
      });
    }
  };
  
  // ... Rest of the existing code (toggleRecording, createWavBlob, writeString, sendAudioMessage, toggleAudio) ...
  
  // Enhanced cleanup
  onMounted(() => {
    return () => {
      if (recordingTimer.value) {
        clearInterval(recordingTimer.value);
      }
      messages.value.forEach(message => {
        if (message.audioElement) {
          message.audioElement.pause();
          message.audioElement = null;
        }
      });
    };
  });
  </script>
  
  <style scoped>
  /* Existing styles */
  ::-webkit-scrollbar {
    width: 8px;
  }
  
  ::-webkit-scrollbar-track {
    background: transparent;
  }
  
  ::-webkit-scrollbar-thumb {
    background: rgba(16, 185, 129, 0.2);
    border-radius: 4px;
  }
  
  ::-webkit-scrollbar-thumb:hover {
    background: rgba(16, 185, 129, 0.4);
  }
  
  /* Enhanced animations */
  .typing-dot {
    @apply w-2 h-2 bg-emerald-400 rounded-full;
    animation: bounce 1s infinite;
  }
  
  .animation-delay-200 {
    animation-delay: 0.2s;
  }
  
  .animation-delay-400 {
    animation-delay: 0.4s;
  }
  
  @keyframes bounce {
    0%, 80%, 100% { transform: translateY(0); }
    40% { transform: translateY(-6px); }
  }
  
  .message-wrapper {
    animation: slideIn 0.3s ease-out;
  }
  
  @keyframes slideIn {
    from {
      opacity: 0;
      transform: translateY(10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  /* Theme transitions */
  * {
    @apply transition-colors duration-200;
  }
  </style>