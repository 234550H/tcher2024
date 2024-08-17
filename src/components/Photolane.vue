<script setup>
import { ref } from 'vue'

defineProps({
  msg: {
    type: String,
    default: "Welcome to Memory Lane",
  },
})

const images = ref([
  'https://via.placeholder.com/200x300?text=Memory+1',
  'https://via.placeholder.com/200x300?text=Memory+2',
  'https://via.placeholder.com/200x300?text=Memory+3',
  'https://via.placeholder.com/200x300?text=Memory+4',
])
</script>

<template>
  <div class="photobook-container">
    <h1>{{ msg }}</h1>
    <div class="photobook">
      <div v-for="(image, index) in images" :key="index" class="photo">
        <img :src="image" alt="Memory photo" />
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Background and overall styling for the photobook */
.photobook-container {
  text-align: center;
  margin: 20px;
  font-family: 'Arial', sans-serif;
  background: url('https://via.placeholder.com/1920x1080?text=Textured+Background') no-repeat center center; /* Add a textured background image */
  background-size: cover;
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
}

/* Styling for the photobook */
.photobook {
  display: flex;
  overflow-x: auto; /* Use auto instead of scroll for a smoother experience */
  padding: 20px;
  gap: 20px;
  scrollbar-width: thin;
  background: rgba(255, 255, 255, 0.8); /* Semi-transparent background for a softer look */
  border: 2px solid #ccc; /* Add a border to simulate a photo album */
  border-radius: 15px;
}

/* Individual photo styling */
.photo {
  display: inline-block; /* Ensures proper spacing between images */
  border: 5px solid #ddd; /* Add a border to simulate a photo frame */
  border-radius: 15px;
  background: #fff; /* Background color for the photo area */
  padding: 5px; /* Padding inside the border */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Shadow for depth */
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.photo img {
  border-radius: 10px; /* Rounded corners for the image */
}

.photo img:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3); /* Enhanced shadow on hover */
}

h1 {
  color: #333; /* Darker color for better readability */
  margin-bottom: 20px;
  font-size: 30px; /* Larger font size for a more prominent heading */
  font-family: 'Cursive', sans-serif; /* Cursive font for a personal touch */
}

/* Scrollbar styling */
::-webkit-scrollbar {
  height: 8px;
}

::-webkit-scrollbar-thumb {
  background-color: #888;
  border-radius: 10px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1; /* Lighter background for the scrollbar track */
}
</style>
