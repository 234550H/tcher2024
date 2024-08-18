<template>
  <div class="photo-lane-container">
    <h1 class="main-title">#ThrowbackPics</h1>
    <h2 class="photo-lane-title">{{ photoSet }}</h2>
    
    <div class="photo-lane">
      <div v-for="photo in photos" :key="photo" class="photo-item" @click="openLightbox(photo)">
        <img :src="photo" alt="Memory Photo" />
      </div>
    </div>

    <!-- Lightbox Modal -->
    <div v-if="showLightbox" class="lightbox" @click="closeLightbox">
      <img :src="zoomedPhoto" alt="Zoomed Photo" class="lightbox-img" />
    </div>

    <!-- Special Message Container -->
    <div class="special-message-container">
      <p class="special-message">{{ specialMessage }}</p>
      <div class="profile-placeholders">
        <div v-for="(profile, index) in profilePlaceholders" :key="index" class="profile-placeholder" @click="openProfileMessage(index)">
          <img :src="profile.image" alt="Profile Placeholder" class="profile-img" />
          <p class="profile-message">{{ profile.message }}</p>
        </div>
      </div>
    </div>

    <!-- Profile Message Modal with Animated Border -->
    <div v-if="showProfileMessage" class="profile-message-modal" @click="closeProfileMessage">
      <div class="profile-message-content animated-border">
        <p>{{ selectedProfileMessage }}</p>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'

// Import photos
import photo1 from '../assets/images/4T1/classphoto1.jpg'
import photo2 from '../assets/images/4T1/classphoto2.jpg'
import photo3 from '../assets/images/4T1/classphoto3.jpg'
import photo4 from '../assets/images/4T1/classphoto4.jpg'
import photo6 from '../assets/images/4T1/ph5.jpg'

import ryan from '../assets/images/profile/ryan.jpeg'
import Hx from '../assets/images/profile/huixin.jpeg'
import renee from '../assets/images/profile/renee.jpeg'
import yz from '../assets/images/profile/yz.jpeg'
import qf from '../assets/images/profile/qf.jpg'

import koh1 from '../assets/images/Mskoh/ph1.jpg'
import koh2 from '../assets/images/Mskoh/ph2.jpg'
import koh3 from '../assets/images/Mskoh/ph3.jpg'
import koh4 from '../assets/images/Mskoh/ph4.jpg'
import koh5 from '../assets/images/Mskoh/ph5.jpg'

import so1 from '../assets/images/Mrsseow/sp1.jpg'
import so2 from '../assets/images/Mrsseow/sp2.jpg'

import jam1 from '../assets/images/jam/jam1.jpg'
import jam2 from '../assets/images/jam/jam2.jpg'
import jam3 from '../assets/images/jam/jam3.jpg'
import jam4 from '../assets/images/jam/jam4.jpg'

// Define props and reactive variables
const props = defineProps({
  photoSet: String
})

const photos = ref([])
const zoomedPhoto = ref(null)
const showLightbox = ref(false)
const showProfileMessage = ref(false)
const selectedProfileMessage = ref('')

// Special messages for photo sets
const specialMessages = {
  '4T1': '4T1 short-pics',
  'Ms koh': 'Tap on the profile below to see message',
  'Mrs seow': 'Tap on the profile below to see message',
  'Mdm jam': 'Tap on the profile below to see message',
  'Mdm jamaliah': 'Tap on the profile below to see message',
  default: 'Just a little gift '
}

const specialMessage = ref(specialMessages[props.photoSet] || specialMessages.default)

// Define profile placeholders and messages
const profilePlaceholders = ref([
  {
    image: ryan,
    message: 'Message - Ryan',
    profileMessage: 'Hello! I remember the times where i needed help with my subjects,i will ask questions.Thank you for being my teacher and i am happy to have you as my teacher given all the wonderful memories in class that had happened! Stay Safe ,Stay strong & 我爱你 Happy teachers day!!'
  },
  {
    image: Hx,
    message: 'Message - Hui Xin',
    profileMessage: 'hiiii 👋🏻 firstly, thank you for teaching me & i am grateful to have you as my teacher during my time in secondary school 😙❤ may your passion for teaching continue to ignite the minds of many ✨ happy teacher dayyy! 👩🏻‍🏫💐💖'
  },
  {
    image: renee,
    message: 'Message - Renee',
    profileMessage: 'Hello! 👋 Happy Teachers Day! Even though its been nearly four years since you last taught us, thank you for being a teacher to me and our rowdy/chaotic class, haha. And just know that not only me but us, students will always remember the effort you put in to guide us in many ways other than teaching and will treasure the memories you created with us. Once again, thank you so much! And I wish you a very Happy Teachers Day!! (≧▽≦)🙌✨'
  },
  {
    image: yz,
    message: 'Message - Yang Zhe',
    profileMessage: 'Happy teachers day !! Its been a long time since we have last met :D, just wanted to say thank you for making the lessons more fun and engaging, wishing you a year ahead full of happiness and achievement ^^/'
  },
  {
    image: qf,
    message: 'Message - Qi Fang',
    profileMessage: 'Hello!! Certainly time flies! Sometimes we will recall all the funny and how we sleep in class during your lessons ! Haha. But those were the most enjoyable lessons that we have than current lessons that we have. Continue to stay in contact! And happy teachers day 🫡💐 Stay passionate for teaching, the journey is certainly not easy,Happy teachers day!'
  }
])

// Set the photos based on the photoSet prop
onMounted(() => {
  switch (props.photoSet) {
    case '4T1':
      photos.value = [photo1, photo2, photo3, photo4, photo6]
      break
    case 'Ms koh':
      photos.value = [koh1, koh2, koh3, koh4, koh5]
      break
    case 'Mrs seow':
      photos.value = [so1, so2]
      break
    case 'Mdm jam':
    case 'Mdm jamaliah':
      photos.value = [jam1, jam2, jam3, jam4]
      break
    default:
      photos.value = []
      break
  }
})

// Function to open the lightbox with the clicked photo
function openLightbox(photo) {
  zoomedPhoto.value = photo
  showLightbox.value = true
}

// Function to close the lightbox
function closeLightbox() {
  showLightbox.value = false
}

// Function to open the profile message modal
function openProfileMessage(index) {
  selectedProfileMessage.value = profilePlaceholders.value[index].profileMessage
  showProfileMessage.value = true
}

// Function to close the profile message modal
function closeProfileMessage() {
  showProfileMessage.value = false
}
</script>

<style scoped>
/* Container styles */
.photo-lane-container {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 1200px;
  margin: 0 auto;
  margin-top: 70px;
  text-align: center;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: auto;
}

.main-title {
  font-size: 2rem;
  color: #333;
  margin-bottom: 15px;
  font-weight: bold;
}

.photo-lane-title {
  font-size: 1.5rem;
  color: #666;
  margin-bottom: 20px;
}

/* Photo lane styles */
.photo-lane {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 10px;
  width: 100%;
}

.photo-item {
  width: 100%;
  height: auto;
  aspect-ratio: 3/2;
  display: flex;
  justify-content: center;
  align-items: flex-start; /* Align items to the top */
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
  background-color: #fff;
}

.photo-item:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.photo-item img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ensure the image covers the container */
  object-position: top; /* Align the image to the top */
}

/* Special message container styles */
.special-message-container {
  margin-top: 20px;
  text-align: center;
  width: 100%;
}

.special-message {
  font-size: 1.2rem;
  color: rgb(0, 0, 0);
font-weight: bold;
  margin-bottom: 20px;
}

/* Profile placeholders styles */
.profile-placeholders {
  display: flex;
  justify-content: center;
  gap: 15px;
  flex-wrap: wrap;
}

.profile-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
}

.profile-img {
  width: 90px; /* Increase size here */
  height: 90px; /* Increase size here */
  border-radius: 50%;
  object-fit: cover;
  background-color: #ddd;
  margin-bottom: 8px;
}

.profile-message {
  font-size: 0.875rem;
  color: #000000;
font-weight: 600;
}

/* Responsive styles */
/* Container styles */
.photo-lane-container {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 1200px;
  margin: 70px auto 0; /* Adjust margin to provide space from the top */
  text-align: center;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: auto;
  overflow: auto; /* Allow scrolling if content overflows */
}

/* Ensure body and html can scroll */
html, body {
  height: 100%;
  margin: 0;
  padding: 0;
  overflow: auto; /* Allow scrolling */
}

/* Special message container styles */
.special-message-container {
  margin-top: 20px;
  text-align: center;
  width: 100%;
}

/* Responsive styles */
@media (max-width: 768px) {
  .photo-lane {
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  }

  .profile-img {
    width: 70px; /* Adjust size for mobile */
    height: 70px; /* Adjust size for mobile */
  }

  /* Position buttons below the photo-lane content */
  .mute-toggle, .about-us-toggle {
    width: calc(60% - 30px); /* Full width minus margin */
    padding: 12px;
    font-size: 16px;
    position: fixed; /* Fixed positioning for visibility */
    right: 20px;
    border-radius: 10px;
    z-index: 1000; /* Ensure buttons are above other content */
  }

  .about-us-toggle {
    bottom: 120px; /* Positioned above the mute-toggle */
    background-color: #a90000;
    color: white;
  }

  .mute-toggle {
    bottom: 60px; /* Positioned at the bottom of the viewport */
    background-color: #a90000;
    color: white;
  }
}

/* Lightbox styles */
.lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.lightbox-img {
  max-width: 90%;
  max-height: 80%;
}

/* Profile message modal styles */
.profile-message-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.profile-message-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  width: 80%;
  max-width: 600px;
  text-align: center;
}

.animated-border {
  border: 2px solid #00aaff;
  border-radius: 8px;
  animation: borderAnimation 1.5s infinite;
}

@keyframes borderAnimation {
  0% {
    border-color: #00aaff;
  }
  50% {
    border-color: #ff6600;
  }
  100% {
    border-color: #00aaff;
  }
}


</style>
