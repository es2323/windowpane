<template>
  <div id="app">
    <hero-section />
    <about-section />
    <projects-section />
    <contact-section />
    <site-footer />
  </div>
</template>

<script>
import herosection from './components/herosection.vue'

export default {
  name: 'app',
  components: {
    'hero-section': herosection,
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
</style>