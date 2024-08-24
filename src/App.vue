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
const aboutUsVisible = ref(false)
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

function toggleAboutUs() {
  aboutUsVisible.value = !aboutUsVisible.value
}


</script>

<template>
  <div class="memory-background">
  <video autoplay muted loop class="background-video">
    <source src="./assets/tchsvid1.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
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
  
    <button class="about-us-toggle" @click="toggleAboutUs">About Us</button>
    
    <!-- About Us Modal -->
    <div v-if="aboutUsVisible" class="about-us-modal">
      <div class="modal-content colorful-border">
        <img src="./assets/images/profile/team.jpg" alt="Team Photo" class="team-photo" />
        <h2>About Us</h2>
        <h3>Hello Teachers!!</h3>
<p>Time files and it has been 4 years since we graduate in 2020! Your lovely good 4NT kids! 
I am sure sometimes you may wonder how have we been, how are we coping in the tertiary education, what is next, where are we right? 
So let the author of this website give you some little stories of each of us!</p>
<h3>Yang Zhe & Renee</h3>
<p>Both of them are currently in higher nitec 2 years and soon to complete before moving to poly! Coping their best to achieving and maintaining 3.0+ gpa.</p>
<h3>Hui Xin , Ryan & Qi Fang</h3>
<p>We're actually completing poly Year 2 Sem 1 as of August Month 2024. It was indeed a challenging journey at times for us to cope with stress from poly school work and working with peers that are younger than us sometimes.</p>
<h3>Final Message:</h3>
<p>
Whenever 5 of us hangout with each other,
sometimes we will recall the crazy memories that has happened during our secondary school journey and sometime we would talk about it.
The times where there are a lot of unneccssary troubles in class caused by us,
<br>
The very unique character of each group friendship in the class, or even
<br>
ahem 2 of us in this group or more sleeping in your class hahaha.
<br>
Or you have some of us who ask like stupid questions or not even paying attention,dreaming away.
#totallynotguiltyhahahaha
<br>
It is great to know and see you still teaching!
As these days we believe teaching has became even more difficult than before with the advance of technology/ Artificial intelligent and kids are a different level now in terms of handling and getting their attention.
<br>
<p>We definitely miss your classes! Even if we are going to repeat what we did back then such as sleeping in the class or dreaming away HAHA!</p>
<p>Jokes aside,we miss the teachers who will remind/chase us for homework/work , who will nag at us to study hard for upcoming exams and always letting us pass,helping us to pass. Most importantly,Looking out for us indiviually whether in our friendship/Mental health/grades being.</p>
<p>Stay safe! Do remember to rest as busy as your can be too !</p>
<b>Therefore it has been long since we ever say this:</b>
<h3>Now we would like to say</h3>
 <span class="animated-love">saranghaeyo 🫶 saya sayang awak 😊 我爱你 ✨ Aishitemasu!🌹</span>
<span class="animated-love">Happy Teachers day! Selamat hari guru ! 教师节快乐! 💝</span>
<br>
<br>
<i style="font-weight: bold;">
All 5 of us did not forget any of you teachers who have taught us simply because we just remember you in our heart! 
Although we may not contact you and talk due to our busy schedules but we definitely remember you all forever a 💯 % here.
</i>
</p>
<p>See you around in the future when chance arises,meanwhile we will work hard to acheive and further in our own adventures! All the best!</p>
<p>We will certaintly miss and remember you! Do not hestitate to contact us through our whatsapp! or even at least through our leader of our group - Qifang.</p>
<br>
<span class="animated-special">Love you all ♡</span>
<br>
<h5 style="text-align:left;">Yours Sincerely,</h5>
<h5 style="text-align: left;">Qi Fang, Hui Xin , Renee , Yang Zhe , Ryan</h5>
<br>

        <button class="close-button"  @click="toggleAboutUs">X</button>
      </div>
    </div>
  </div>


    <!-- Styled Media Player -->
    <div class="media-player-container">
      <img src="../src/assets/images/profile/team.jpg" alt="Album Cover" class="album-cover" />
      <div class="media-info">
        <h3 class="media-title">Love Story</h3>
        <audio controls loop class="audio-player">
          <source src="../src/assets/lovestory.mp3" type="audio/mpeg">
          Your browser does not support the audio element.
        </audio>
      </div>
    </div>
</template>


<style scoped>
/* Global Styles */
.media-player-container {
  position: absolute; /* Position it on top of the video */
  bottom: 20px; /* Adjust as necessary to position it above the bottom */
  left: 20px; /* Adjust as necessary to position it from the left */
  background-color: rgba(255, 255, 255, 0.7); /* Semi-transparent background */
  border-radius: 15px; /* Rounded corners */
  padding: 10px; /* Padding inside the container */
  display: flex;
  align-items: center; /* Center align content vertically */
  gap: 10px; /* Space between album cover and controls */
  z-index: 10; /* Ensure it appears above the video */
}

.album-cover {
  width: 120px; /* Set a fixed width for the album cover */
  height: 120px; /* Set a fixed height for the album cover */
  margin-right: 10px; /* Space between the album cover and buttons */
  border-radius: 5px; /* Slightly rounded corners */
  object-fit: cover; /* Ensure the image covers the area */
}

.audio-player {
  width: 350px; /* Set a fixed width for the audio player */
  height: 50px; /* Set a fixed height for the audio player */
  border-radius: 5px; /* Slightly rounded corners */
}

.play-button,
.pause-button {
  background-color: #ff6347; /* Button background color */
  color: white; /* Button text color */
  border: none; /* No border */
  border-radius: 8px; /* Rounded corners for buttons */
  padding: 8px 12px; /* Padding for buttons */
  cursor: pointer; /* Pointer cursor on hover */
  transition: background-color 0.3s ease; /* Smooth transition for hover effect */
}

.play-button:hover,
.pause-button:hover {
  background-color: #ff4500; /* Darker shade on hover */
}



/* Keyframes for color animation */
@keyframes colorChange {
  0% {
    color: #ffffff; /* White */
    text-shadow: 0 0 8px #ffffff, 0 0 16px #ffffff;
  }
  25% {
    color: #ff6347; /* Tomato (light red) */
    text-shadow: 0 0 10px #ff6347, 0 0 20px #ff6347;
  }
  50% {
    color: #00fa9a; /* Medium Spring Green */
    text-shadow: 0 0 12px #00fa9a, 0 0 24px #00fa9a;
  }
  75% {
    color: #1e90ff; /* Dodger Blue */
    text-shadow: 0 0 15px #1e90ff, 0 0 30px #1e90ff;
  }
  100% {
    color: #f0e68c; /* Khaki */
    text-shadow: 0 0 20px #f0e68c, 0 0 40px #f0e68c;
  }
}

/* Apply the animation to the span */
.animated-love {
  font-size: 24px;
  font-family: 'Arial', sans-serif;
  font-weight: bold;
  text-align: center;
  animation: colorChange 15s infinite alternate;
}

/* Apply the special color animation */
.animated-special {
  font-size: 24px;
  font-family: 'cursive';
  font-weight: bold;
  text-align: center;
  color: red;
}

.memory-background {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  background: url('./assets/tchsvid1.mp4');
  background-size: auto;
background-position: 0%;
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
z-index: 21;
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


/* Mute Toggle Button */
.mute-toggle {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background-color: white;
  color: black;
  border: none;
  padding: 12px;
  border-radius: 10px;
  cursor: pointer;
  font-family: 'Dancing Script', cursive;
  font-size: 16px;
  transition: background-color 0.3s ease;
}

.mute-toggle:hover {
  background-color: #ffea00;
}

/* About Us Button */
.about-us-toggle {
  position: fixed;
  bottom: 80px; /* Above the footer */
  right: 20px;
  background-color: white;
  color: black;
  border: none;
  padding: 12px;
  border-radius: 10px;
  cursor: pointer;
  font-family: 'Dancing Script', cursive;
  font-size: 16px;
  transition: background-color 0.3s ease;
  z-index: 1000;
}

.about-us-toggle:hover {
  background-color: #ffea00;
}

/* About Us Modal */
.about-us-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
  overflow: auto; /* Allow scrolling if content exceeds the height */
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  text-align: center;
  width: 90%;
  max-width: 600px;
  max-height: 90vh; /* Maximum height of the modal */
  overflow-y: auto; /* Enable vertical scrolling if needed */
z-index: 23;
}

/* Close Button Styling */
.close-button {
  position: absolute;
  top: 40px;
  right: 480px;
  width: 30px; /* Larger width for better touch targets */
  height: 30px; /* Larger height for better touch targets */
  background-color: #025a0e; /* Color for visibility */
  color: white;
  border: none;
  border-radius: 50%;
  font-size: 24px; /* Increase font size */
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: background-color 0.3s ease, transform 0.3s ease;
}



.close-button:focus {
  outline: none;
}

.memory-background {
  position: relative; /* Ensure child elements are positioned relative to this container */
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.background-video {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 100%;
  height: auto;
  min-height: 100%;
  min-width: 100%;
  transform: translate(-50%, -50%);
  z-index: 1; /* Lower z-index for the video */
}

h1 {
  position: relative;
  z-index: 2; /* Higher z-index for the title */
  color: white; /* Change this to your desired color */
  text-align: center; /* Center align the text */
}

.photo-frame-container {
  position: relative;
  z-index: 3; /* Higher z-index for the photo frame container */
  display: flex;
  justify-content: center; /* Center the photo frame */
  align-items: center; /* Center the photo frame vertically */
  height: 100%; /* Allow it to take the full height */
}

.chalk {
  font-size: 50px; /* Adjust size as needed */
  color: yellow; /* Change this color to your desired color */
}


@media (max-width: 768px) {
  .close-button {
    width: 35px; /* Increase size for mobile devices */
    height: 40px;
    font-size: 20px; /* Increase font size for better visibility */
right: 5px;
top:10px;
  }
}


.colorful-border {
  border: 5px solid;
  border-image-slice: 1;
  border-width: 10px;
  border-image-source: linear-gradient(45deg, red, yellow, green, blue);
  animation: border-animation 3s linear infinite;
}

.team-photo {
  width: 80%;
  height: auto;
  border-radius: 12px;
  margin-bottom: 20px;
}

@keyframes border-animation {
  0% {
    border-image-source: linear-gradient(45deg, #00ff00, #8b0000); /* Green to Dark Red */
  }
  50% {
    border-image-source: linear-gradient(45deg, #8b0000, #00ff00); /* Dark Red to Green */
  }
  100% {
    border-image-source: linear-gradient(45deg, #00ff00, #8b0000); /* Green to Dark Red */
  }
}

/* Animations */
@keyframes rotate-scale {
  0% {
    transform: rotate(0) scale(1);
  }
  50% {
    transform: rotate(360deg) scale(1.1);
  }
  100% {
    transform: rotate(720deg) scale(1);
  }
}

@keyframes chalk-draw {
  0% {
    transform: rotate(0deg) translate(0, 0);
  }
  50% {
    transform: rotate(360deg) translate(10px, 10px);
  }
  100% {
    transform: rotate(720deg) translate(0, 0);
  }
}

/* Responsive Adjustments */
@media (max-width: 768px) {
h1{
color: #000;
margin-top: 70px;

}
 .media-player-container {
    position: absolute; /* Position it on top of the video for larger screens */
    bottom: 20px; /* Adjust as necessary to position it above the bottom */
    left: 20px; /* Adjust as necessary to position it from the left */
    background-color: rgba(255, 255, 255, 0.7); /* Semi-transparent background */
    border-radius: 15px; /* Rounded corners */
    max-width: 90%; /* Allow it to take up to 90% of the viewport */
  }

.audio-player {
  width: 280px; /* Set a fixed width for the audio player */
  height: 50px; /* Set a fixed height for the audio player */
  border-radius: 5px; /* Slightly rounded corners */
}

  /* Position buttons relative to the screen width */
  .mute-toggle, .about-us-toggle {
    width: calc(35% - 80px); /* Full width minus margin */
    padding: 12px;
    font-size: 10px;
    position: fixed;
    right: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(232, 28, 28, 0.2);
    background-color: white;
    color: black;
    text-align: center;
  }

  .about-us-toggle {
    bottom: 105px; /* Positioned above the mute-toggle */
  }

  .modal-content {
    width: 90%; /* Adjust width to fit smaller screens */
    max-width: none; /* Remove max-width on small screens */
    padding: 15px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    overflow-y: auto; /* Allow scrolling inside the modal */
    position: relative; /* Ensure correct positioning */
  }

  /* Ensure body can scroll */
  body.modal-open {
    overflow: hidden; /* Prevent body scroll when modal is open */
  }

  /* Ensure content area doesn't overlap fixed elements */
  .content {
    padding-bottom: 140px; /* Space for buttons */
  }
  
  /* Ensure photolane content is not overlapped by buttons */
  .photolane {
    position: relative; /* Ensure it is positioned correctly */
    z-index: 1; /* Keep photolane above other elements but below buttons */
  }

  /* Ensure consistent margins and padding for smaller screens */
  .name-prompt {
    width: 90%; /* Adjust width for smaller screens */
    margin: 0 auto; /* Center the prompt */
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  margin-top: -20px;
  }
  
  .photo-frame {
    width: 120px; /* Adjust size for smaller screens */
    height: 120px;
  }

  .chalkboard {
    font-size: 48px; /* Adjust font size for smaller screens */
  }

}

</style>
