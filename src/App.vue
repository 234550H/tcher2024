<script setup>
import { ref } from 'vue'
import confetti from 'canvas-confetti'
import PhotoLane from './components/Photolane.vue'

const showCover = ref(false)
const logoClicked = ref(false)
const buttonVisible = ref(true) // Controls button visibility
const namePromptVisible = ref(false) // Controls input box visibility
const userName = ref('') // Stores user input

function handleLogoClick() {
  logoClicked.value = true
  buttonVisible.value = false // Hide the button when clicked
  namePromptVisible.value = true // Show the input box

  // Trigger confetti effect
  confetti({
    particleCount: 200,  // Increased particle count for a more intense effect
    spread: 120,         // Wider spread
    origin: { y: 0.6 },  // Position from where the confetti originates
    colors: ['#ff0', '#f0f', '#0ff', '#f00'], // Color palette for the confetti
    disableForReducedMotion: true // Respect reduced motion settings if enabled
  })
}

function handleNameSubmit() {
  if (userName.value.trim()) {
    showCover.value = true // Show PhotoLane if name is entered
    namePromptVisible.value = false // Hide the input box
  }
}
</script>

<template>
  <div class="memory-background">
    <div class="photo-frame-container" v-if="buttonVisible" @click="handleLogoClick">
      <div class="photo-frame" :class="{ 'clicked': logoClicked }">
        <div class="chalkboard">
          <div class="chalk">
            <span>Click me</span>
          </div>
        </div>
      </div>
    </div>
    <div v-if="namePromptVisible" class="name-prompt">
      <input v-model="userName" type="text" placeholder="Enter your name" />
      <button @click="handleNameSubmit">Submit</button>
    </div>
    <PhotoLane v-if="showCover" />
    <footer class="footer">
      <b>Coded by Qi Fang</b>
      <p>Behalf of (Hui Xin, Renee, Yang Zhe, Ryan)</p>
    </footer>
  </div>
</template>

<style scoped>
/* Background styling */
.memory-background {
  width: 100vw; /* Use viewport width for full width */
  height: 100vh; /* Use viewport height for full height */
  display: flex;
  flex-direction: column; /* Column layout to stack items vertically */
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden; /* Hide overflow to avoid scrollbars */
  background: linear-gradient(135deg, #00aaff, #009952); /* Ocean blue gradient */
}

/* Photo Frame Styling */
.photo-frame-container {
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.photo-frame {
  width: 250px; /* Adjust size for better visibility */
  height: 200px;
  background: radial-gradient(circle, #e0e5e6, #d3bd18); /* Vintage gradient color */
  border-radius: 20px; /* Rounded corners */
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative; /* Position relative for absolute positioning of footer */
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3); /* Enhanced shadow for depth */
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background-clip: padding-box;
}

.photo-frame.clicked {
  animation: rotate-scale 1s ease forwards;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4); /* Increased shadow on click */
}

.chalkboard {
  width: 180px; /* Wider for better proportion */
  height: 120px;
  background: #ffffff; /* Light vintage background */
  border-radius: 12px; /* Rounded corners */
  display: flex;
  flex-direction: column; /* Stack chalkboard content vertically */
  justify-content: center;
  align-items: center;
  color: black;
  font-family: 'Dancing Script', cursive; /* Updated cursive font */
  font-size: 22px;
  text-align: center;
  border: 2px solid #a1887f; /* Subtle border for a chalkboard look */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Light shadow */
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
  background-color: #ff5722; /* Lively orange color */
  color: white;
  cursor: pointer;
  font-family: 'Dancing Script', cursive; /* Updated cursive font */
}

.name-prompt button:hover {
  background-color: #e64a19; /* Darker shade for hover effect */
}

/* Footer Styling */
.footer {
  position: absolute;
  bottom: 10px; /* Position footer at the bottom of the viewport */
  left: 50%;
  transform: translateX(-50%);
  width: auto; /* Adjust width based on content */
  text-align: center; /* Center text */
  padding: 5px; /* Padding for spacing */
  color: #5d4037; /* Match the chalkboard color */
  font-size: 12px; /* Smaller font size */
  font-family: 'Dancing Script', cursive; /* Updated cursive font */
  background-color: rgba(255, 255, 255, 0.8); /* Semi-transparent background to make text readable */
  border-radius: 8px; /* Rounded corners for the footer */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Light shadow */
}

@keyframes rotate-scale {
  0% {
    transform: rotate(0deg) scale(1);
  }
  50% {
    transform: rotate(360deg) scale(1.2);
  }
  100% {
    transform: rotate(720deg) scale(1);
  }
}

@keyframes chalk-draw {
  0%, 100% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(-5px);
  }
}
</style>
