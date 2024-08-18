<script setup>
import { ref, onMounted } from 'vue'
import confetti from 'canvas-confetti'
import PhotoLane from './components/Photolane.vue'
import '../src/assets/lovestory.mp3'

const showCover = ref(false)
const logoClicked = ref(false)
const buttonVisible = ref(true)
const namePromptVisible = ref(false)
const userName = ref('')
const nameError = ref('')
const isMuted = ref(false)
let audio = null

const allowedNames = ['4T1', 'Ms koh', 'Mrs seow', 'Mdm jam', 'Mdm jamaliah']

function handleLogoClick() {
  logoClicked.value = true
  buttonVisible.value = false
  namePromptVisible.value = true

  confetti({
    particleCount: 200,
    spread: 120,
    origin: { y: 0.6 },
    colors: ['#ff0', '#f0f', '#0ff', '#f00'],
    disableForReducedMotion: true
  })

  if (audio) {
    audio.play().catch((error) => {
      console.error('Playback failed:', error)
    })
  }
}

function handleNameSubmit() {
  if (allowedNames.includes(userName.value.trim())) {
    showCover.value = true
    namePromptVisible.value = false
  } else {
    nameError.value = "Please enter a valid name from the list.";
  }
}

function toggleMute() {
  isMuted.value = !isMuted.value
  if (audio) {
    audio.muted = isMuted.value
  }
}

onMounted(() => {
  audio = new Audio('../src/assets/lovestory.mp3')
  audio.loop = true
  audio.volume = 0.7
})
</script>

<template>
  <div class="memory-background">
    <h1 :class="{ 'hidden-title': showCover }">Teacher's Special Gift 2024</h1>
    <div class="photo-frame-container" v-if="buttonVisible" @click="handleLogoClick">
      <div class="photo-frame" :class="{ 'clicked': logoClicked }">
        <div class="chalkboard">
          <div class="chalk">
            <span>⭐</span>
          </div>
        </div>
      </div>
    </div>
    <div v-if="namePromptVisible" class="name-prompt">
      <input v-model="userName" type="text" placeholder="Enter your name" />
      <p v-if="nameError" class="error-message">{{ nameError }}</p>
      <button @click="handleNameSubmit">Submit</button>
    </div>
    <PhotoLane v-if="showCover" :photoSet="userName" />
    <footer class="footer">
      <b>Coded by Qi Fang</b>
      <br>
      <b>Behalf of (Hui Xin, Renee, Yang Zhe, Ryan)</b>
    </footer>
    <button class="mute-toggle" @click="toggleMute">
      {{ isMuted ? 'Unmute' : 'Mute' }}
    </button>
  </div>
</template>

<style scoped>
/* Global Styles */
.memory-background {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  background-color: black;
}

/* Title Styling */
h1 {
  position: absolute;
  top: 5%;
  color: white;
  text-align: center;
  width: 100%;
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.hidden-title {
  opacity: 0;
  transform: translateY(-50px);
}

/* Photo Frame Styling */
.photo-frame-container {
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.photo-frame {
  width: 150px;
  height: 150px;
  background: transparent;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.photo-frame-container:hover .photo-frame {
  box-shadow: 0 0 15px rgba(192, 2, 97, 0.6);
}

.chalkboard {
  width: 100px;
  height: 100px;
  background: transparent;
  display: flex;
  justify-content: center;
  align-items: center;
  color: gold;
  font-size: 64px;
  text-align: center;
  transition: color 0.3s ease, box-shadow 0.3s ease;
  box-shadow: 0 0 20px gold;
}

.photo-frame-container:hover .chalkboard {
  color: #ff5722;
  box-shadow: 0 0 30px #ff5722;
}

.photo-frame.clicked {
  animation: rotate-scale 1s ease forwards;
}

.chalk {
  animation: chalk-draw 2s ease infinite;
}

/* Input and Button Styling */
.name-prompt {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #fff;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.name-prompt input {
  padding: 12px;
  font-size: 18px;
  border: 2px solid #ccc;
  border-radius: 8px;
  width: 250px;
}

.name-prompt button {
  padding: 12px 24px;
  font-size: 18px;
  border: none;
  border-radius: 8px;
  background-color: #000;
  color: white;
  cursor: pointer;
  font-family: 'Dancing Script', cursive;
}

.name-prompt button:hover {
  background-color: #dbb131;
}

/* Error Message Styling */
.error-message {
  color: red;
  font-size: 17px;
  margin-top: 10px;
}

/* Footer Styling */
.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  padding: 15px;
  color: white;
  font-size: 16px;
  font-family: 'Dancing Script', cursive;
  background: linear-gradient(135deg, rgba(0,0,0,0.8), rgba(0,0,0,0.6));
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
  width: 80%;
  max-width: 300px;
  z-index: 1000;
  text-align: left;
}

/* Mute Toggle Button */
.mute-toggle {
  position: absolute;
  bottom: 20px;
  right: 20px;
  background-color: #ffffff;
  border: none;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
  font-family: 'Dancing Script', cursive;
  font-size: 16px;
}

.mute-toggle:hover {
  background-color: #f0f0f0;
}

/* Responsive Styles */
@media (max-width: 1024px) {
  .photo-frame {
    width: 130px;
    height: 130px;
  }

  .chalkboard {
    width: 90px;
    height: 90px;
    font-size: 56px;
  }

  .name-prompt {
    width: 70%;
    padding: 15px;
  }

  .name-prompt input {
    width: 220px;
  }

  .name-prompt button {
    padding: 10px 20px;
    font-size: 16px;
  }

  .footer {
    font-size: 14px;
    padding: 12px;
    width: 75%;
  }

  .mute-toggle {
    bottom: 40px;
    right: 15px;
    font-size: 15px;
  }
}

@media (max-width: 768px) {
  .photo-frame {
    width: 120px;
    height: 120px;
  }

  .chalkboard {
    width: 80px;
    height: 80px;
    font-size: 48px;
  }

  .name-prompt {
    width: 80%;
    padding: 15px;
  }

  .name-prompt input {
    width: 200px;
  }

  .name-prompt button {
    padding: 10px 20px;
    font-size: 16px;
  }

  .footer {
    font-size: 12px;
    padding: 10px;
    width: 90%;
  }

  .mute-toggle {
    bottom: 30px;
    right: 10px;
    font-size: 14px;
  }
}

@media (max-width: 480px) {
  .photo-frame {
    width: 100px;
    height: 100px;
  }

  .chalkboard {
    width: 60px;
    height: 60px;
    font-size: 36px;
  }

  .name-prompt {
    width: 90%;
    padding: 10px;
  }

  .name-prompt input {
    width: 180px;
  }

  .name-prompt button {
    padding: 8px 16px;
    font-size: 14px;
  }

  .footer {
    font-size: 10px;
    padding: 8px;
    width: 95%;
    bottom: 0;
  }

  .mute-toggle {
    bottom: 20px;
    right: 5px;
    font-size: 12px;
  }
}

/* Animations */
@keyframes rotate-scale {
  from {
    transform: scale(0) rotate(0deg);
  }
  to {
    transform: scale(1) rotate(360deg);
  }
}

@keyframes chalk-draw {
  0% {
    transform: translateY(0);
    opacity: 1;
  }
  50% {
    transform: translateY(-10px);
    opacity: 0.5;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}


</style>
