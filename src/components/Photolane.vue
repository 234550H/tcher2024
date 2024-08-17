<script setup>
import { ref, onMounted } from 'vue'

// Define photo imports
import photo1 from '../assets/images/4T1/classphoto1.jpg'
import photo2 from '../assets/images/4T1/classphoto2.jpg'
import photo3 from '../assets/images/4T1/classphoto3.jpg'
import photo4 from '../assets/images/4T1/classphoto4.jpg'
import photo6 from '../assets/images/4T1/ph5.jpg'

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

// Define special messages for each photo set
const specialMessages = {
  '4T1': 'Special memories from the 4T1 class!',
  'Ms koh': 'Ms Koh’s memorable moments captured!',
  'Mrs seow': 'Wonderful photos from Mrs Seow’s events!',
  'Mdm jam': 'Cherished times with Mdm Jamaliah!',
  'Mdm jamaliah': 'Beautiful memories with Mdm Jamaliah!',
  default: 'Enjoy these wonderful photos!'
}

const specialMessage = ref(specialMessages[props.photoSet] || specialMessages.default)

// Define profile placeholders and messages
const profilePlaceholders = Array(5).fill({
  image: '../assets/images/gift.png', // Use a default profile image
  message: 'Demo message'
})

// Define different photo sets based on the photoSet prop
onMounted(() => {
  switch (props.photoSet) {
    case '4T1':
      photos.value = [photo1, photo2, photo3, photo4, photo6]
      break
    case 'Ms koh':
      photos.value = [koh1, koh2, koh3, koh4,koh5]
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

function openLightbox(photo) {
  zoomedPhoto.value = photo
  showLightbox.value = true
}

function closeLightbox() {
  showLightbox.value = false
}
</script>

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
        <div v-for="(profile, index) in profilePlaceholders" :key="index" class="profile-placeholder">
          <img :src="profile.image" alt="Profile Placeholder" class="profile-img" />
          <p class="profile-message">{{ profile.message }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.photo-lane-container {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 1200px;
  margin: 0 auto;
  text-align: center;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: auto;
}

.main-title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: -10px;
  font-weight: bold;
}

.photo-lane-title {
  font-size: 1.75rem;
  color: #666;
  margin-bottom: 20px;
}

.photo-lane {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
}

.photo-item {
  width: 100%;
  max-width: 300px;
  height: auto;
  aspect-ratio: 3/2;
  display: flex;
  justify-content: center;
  align-items: flex-start; /* Aligns images to the top */
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
  background-color: #fff; /* Ensures a clean background */
}

.photo-item:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.photo-item img {
  width: 100%;
  height: auto;
  object-fit: cover;
  object-position: top; /* Ensures the image is aligned to the top */
}

.special-message-container {
  margin-top: 20px;
  text-align: center;
  width: 100%;
}

.special-message {
  font-size: 1.25rem;
  color: #444;
  margin-bottom: 20px;
}

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
}

.profile-img {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  object-fit: cover;
  background-color: #ddd;
  margin-bottom: 8px;
}

.profile-message {
  font-size: 0.875rem;
  color: #666;
}

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
  cursor: pointer;
}

.lightbox-img {
  max-width: 90%;
  max-height: 90%;
  border-radius: 8px;
}
</style>
