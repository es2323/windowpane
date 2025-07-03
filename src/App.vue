<template>
  <transition name="fade">
    <div v-if="isLoading" class="preloader">
      <div class="preloader-box">
        
        <!-- The border lines are now correctly placed inside the box -->
        <span class="border-line line-top"></span>
        <span class="border-line line-right"></span>
        <span class="border-line line-bottom"></span>
        <span class="border-line line-left"></span>

        <!-- The h1 text follows the border lines -->
        <h1 class="preloader-text">
          <span class="preloader-name">Enosh Earnest</span>
          <span class="preloader-title">Portfolio</span>
        </h1>

      </div> 
    </div>
  </transition>

  <div id="app">
    <hero-section />
  </div>
</template>

// This is the script section of App.vue
<script>
import herosection from './components/herosection.vue'

export default {
  name: 'App',
  components: {
    'hero-section': herosection,
  },
  data() {
    return {
      // The preloader is visible by default
      isLoading: true 
    }
  },
  mounted() {
    // Set a timer to hide the preloader after 2 seconds
    setTimeout(() => {
      this.isLoading = false;
    }, 2000); // 2000ms = 2 seconds. You can change this value.
  }
}
</script>

<style>
/* global styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  
}

body {
  font-family: 'Neue Montreal', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
  line-height: 1.4;
  color: #f0f0f0; /* Light text color for the entire app by default */
  background-color: #0d0d0d; /* Dark background color for the entire app by default */
  font-weight: 600;
  font-feature-settings: "palt";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  min-height: 100vh;
}

/* typography */
h1 {
  font-size: clamp(2.5rem, 8vw, 6rem);
  font-weight: 5;
  line-height: 0.9;
  letter-spacing: -0.02em;
  margin-bottom: 2rem;
  color: #f0f0f0; /* Ensure headings are also light, overriding App.vue's body color if needed */

}

h2 {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  font-weight: 60;
  line-height: 1.1;
  letter-spacing: -0.01em;
  margin-bottom: 1.5rem;
  color: #f0f0f0; 

}

h3 {
  font-size: 1.25rem;
  font-weight: 500;
  line-height: 1.2;
  margin-bottom: 1rem;
  color: #f0f0f0;
}

p {
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  max-width: 65ch;
  color: #aaa;
}

.large-text {
  font-size: clamp(1.1rem, 2.5vw, 1.5rem);
  line-height: 1.5;
  font-weight: 400;
  margin-bottom: 3rem;
  max-width: 50ch;
  color: #aaa;
}

.small-text {
  font-size: 0.875rem;
  line-height: 1.5;
  color: #666;
}

a {
  color: inherit;
  text-decoration: none;
  transition: all 0.2s ease;
}

a:hover {
  opacity: 0.7;
}

/* navigation/interactive text */
.nav-item {
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.3;
  cursor: pointer;
  margin-bottom: 0.5rem;
  transition: all 0.2s ease;
  color: #f0f0f0;
}

.nav-item:hover {
  opacity: 0.6;
}

.nav-item.active {
  font-weight: 500;
  color: white;
}

/* layout utilities */
.container {
  max-width: none;
  margin: 0;
  padding: 3rem;
  height: 100vh;
}

.two-column {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  height: 100%;
  align-items: start;
}

.left-column {
  position: sticky;
  top: 3rem;
}

.right-column {
  padding-top: 2rem;
}

/* utility classes */
.text-left {
  text-align: left;
}

.fade-in {
  opacity: 0;
  transform: translateY(10px);
  transition: all 0.4s ease;
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

/* responsive */
@media (max-width: 768px) {
  .container {
    padding: 2rem 1.5rem;
  }
  
  .two-column {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .left-column {
    position: static;
  }
  
  h1 {
    margin-bottom: 1.5rem;
  }
  
  .large-text {
    margin-bottom: 2rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 1.5rem 1rem;
  }
}

@keyframes fade-up {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.preloader {
  /* Positioning to cover the entire screen */
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index: 9999; /* Ensures it's on top of everything */

  /* Use your "Digital Cathedral" background color */
  background-color: #222831;

  /* Centering the text */
  display: flex;
  justify-content: center;
  align-items: center;
}

.preloader-box {
  position: relative; /* This is the new anchor for the border animation */
  width: calc(100% - 40px);
  max-width: 1500px;  /* <-- This now matches your homepage container's size */
  height:calc(100% - 40px);
  padding: 40px;      /* <-- This also matches the homepage container's padding */
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}

.preloader-name {
  font-weight: 300; /* This makes it bold */
}

.preloader-title {
  font-weight: 100; /* This makes it a light, normal weight */
  opacity: 0.8;   /* A slightly lower opacity can look nice too */
  margin-left: 0.5em;
  color: #D87A4A;
}

.preloader-text {
  /* Use your "Parchment White" text color */
  color: #e6e1d2;
  font-size: 1.8rem; /* Adjust size as needed */
  letter-spacing: 0.5px;
  margin: 0;
}

/*
  --- Vue Transition Classes for the fade effect ---
*/
.fade-leave-active {
  transition: opacity 1s ease;
}

.fade-leave-to {
  opacity: 0;
}



.preloader-name,
.preloader-title {
  /* Common properties */
  opacity: 0;
  animation-fill-mode: forwards;
  animation-duration: 1.5s; /* How long the fade takes */
  animation-timing-function: ease-out;
}

.preloader-name {
  /* Use the new simple fade-in animation */
  animation-name: simple-fade-in;
  /* Set a more noticeable delay */
  animation-delay: 0.5s; 
}

.preloader-title {
  /* The title can still use the fade-up effect */
  animation-name: fade-up;
  /* Make it appear after the name */
  animation-delay: 0.8s;
}
/* --- NEW HIGH-PERFORMANCE BORDER ANIMATION --- */

/* Base style for all four border lines */
.border-line {
  position: absolute;
  background-color: #D87A4A; /* Your Terracotta accent color */
  transform-origin: center; /* Default origin */
}

/* Positioning and transform origin for each line */
.line-top {
  top: 0;
  left: 0;
  width: 100%;
  height: 2px;
  transform: scaleX(0); /* Starts with 0 width */
  transform-origin: left; /* Animates from left to right */
}
.line-right {
  top: 0;
  right: 0;
  width: 2px;
  height: 100%;
  transform: scaleY(0); /* Starts with 0 height */
  transform-origin: top; /* Animates from top to bottom */
}
.line-bottom {
  bottom: 0;
  left: 0;
  width: 100%;
  height: 2px;
  transform: scaleX(0);
  transform-origin: right; /* Animates from right to left */
}
.line-left {
  top: 0;
  left: 0;
  width: 2px;
  height: 100%;
  transform: scaleY(0);
  transform-origin: bottom; /* Animates from bottom to top */
}

/* Keyframe animation to scale the lines to 100% */
@keyframes scale-in {
  from { transform: scaleX(0); }
  to { transform: scaleX(1); }
}
@keyframes scale-in-y {
  from { transform: scaleY(0); }
  to { transform: scaleY(1); }
}

/* Apply the animations with a delay to create the sequential effect */
.preloader-box .line-top {
  animation: scale-in 0.5s ease-out forwards;
}
.preloader-box .line-right {
  animation: scale-in-y 0.5s ease-out 0.5s forwards;
}
.preloader-box .line-bottom {
  animation: scale-in 0.5s ease-out 1s forwards;
}
.preloader-box .line-left {
  animation: scale-in-y 0.5s ease-out 1.5s forwards;
}

@keyframes simple-fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* --- Mobile Styles for Pre-loader --- */
@media (max-width: 768px) {
  .preloader-text {
    font-size: 1.3rem;   /* Smaller font size for mobile */
    text-align: center;  /* Ensures it stays centered if it wraps to two lines */
    padding: 0 1rem;     /* Adds a little space on the sides for very narrow screens */
  }
}
</style>