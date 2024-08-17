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
    <h1 style="color: white; text-align: center;">Teacher's Special Gift 2024</h1>
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
      <b style="font-size: 15px;">Coded by Qi Fang</b>
      <br>
      <b style="font-size: 15px;">Behalf of (Hui Xin, Renee, Yang Zhe, Ryan)</b>
    </footer>
    <button class="mute-toggle" @click="toggleMute">
      {{ isMuted ? 'Unmute' : 'Mute' }}
    </button>
  </div>
</template>

<style scoped>
/* Background styling for different devices */
.memory-background {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  background-color: black; /* Set background color to black */
}

/* Title Styling */
h1 {
  position: absolute;
  top: 5%; /* Position it higher on the page */
  color: white;
  text-align: center;
  width: 100%;
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.hidden-title {
  opacity: 0;
  transform: translateY(-50px); /* Move it up smoothly when hidden */
}

/* Photo Frame Styling */
.photo-frame-container {
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.photo-frame {
  width: 150px; /* Adjust size for the star icon */
  height: 150px;
  background: transparent; /* No background */
  border-radius: 50%; /* Make it circular */
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.photo-frame-container:hover .photo-frame {
  box-shadow: 0 0 15px rgba(192, 2, 97, 0.6); /* Glowing effect for the circle on hover */
}

.chalkboard {
  width: 100px; /* Smaller size for the star icon */
  height: 100px;
  background: transparent; /* No background */
  display: flex;
  justify-content: center;
  align-items: center;
  color: gold; /* Default color for the star */
  font-size: 64px; /* Larger font size for the star icon */
  text-align: center;
  transition: color 0.3s ease, box-shadow 0.3s ease; /* Smooth transition for color and glow */
  box-shadow: 0 0 20px gold; /* Glowing effect for the star */
}

.photo-frame-container:hover .chalkboard {
  color: #ff5722; /* Change star color on hover */
  box-shadow: 0 0 30px #ff5722; /* Increase the glow effect on hover */
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
  background: #fff; /* White background for input box */
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Subtle shadow */
}

.name-prompt input {
  padding: 12px;
  font-size: 18px;
  border: 2px solid #ccc;
  border-radius: 8px;
  width: 250px; /* Adjust width as needed */
}

.name-prompt button {
  padding: 12px 24px;
  font-size: 18px;
  border: none;
  border-radius: 8px;
  background-color: #000000; /* Background color for the button */
  color: white;
  cursor: pointer;
  font-family: 'Dancing Script', cursive; /* Updated cursive font */
}

.name-prompt button:hover {
  background-color: #dbb131; /* Darker shade for hover effect */
}

/* Error Message Styling */
.error-message {
  color: red; /* Red color for error text */
  font-size: 17px; /* Smaller font size */
  margin-top: 10px; /* Slight adjustment for spacing */
}

/* Footer Styling */
.footer {
  position: absolute;
  bottom: 20px; /* Move the footer up by 60px */
  left: 80%;
  transform: translateX(-50%);
  text-align: left;
  padding: 5px;
  color: white;
  font-size: 12px;
  font-family: 'Dancing Script', cursive;
  background-color: rgba(10, 14, 231, 0.8);
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.mute-toggle {
  position: absolute;
  bottom: 50px;
  left: 10px;
  padding: 10px 20px;
  background-color: #000;
  color: #fff;
  border: 2px solid;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-family: 'Dancing Script', cursive;
}

.mute-toggle:hover {
  background-color: #333;
}

@keyframes rotate-scale {
  0% {
    transform: rotate(0deg) scale(1);
  }
  50% {
    transform: rotate(180deg) scale(1.1);
  }
  100% {
    transform: rotate(360deg) scale(1);
  }
}

@keyframes chalk-draw {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}
</style>
