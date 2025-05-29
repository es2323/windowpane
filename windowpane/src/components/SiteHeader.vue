<template>
  <header class="main-header">
    <nav class="header-nav">
      <h1 class="site-title">
        <a href="#hero">Enosh Earnest</a>
      </h1>
      <ul class="nav-links">
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#contact">Contact</a></li>
        <li><a href="/path/to/your-resume.pdf" target="_blank" rel="noopener noreferrer">Resume</a></li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'SiteHeader' // Name of your component
}
</script>

<style scoped>
/* Styles specific to your Header component */
.main-header {
  background-color: #2c3e50; /* Dark blue/grey */
  color: white;
  padding: 1rem 0; /* Top/bottom padding, no side padding */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
}

.header-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px; /* Max width of your content */
  margin: 0 auto; /* Center the content */
  padding: 0 20px; /* Horizontal padding for smaller screens */
}

.site-title {
  margin: 0;
  font-size: 1.8rem; /* Larger font for the title */
}

.site-title a {
  color: white;
  text-decoration: none;
  transition: color 0.3s ease; /* Smooth transition for hover effect */
}

.site-title a:hover {
  color: #42b983; /* Vue green on hover */
}

.nav-links {
  list-style: none; /* Remove bullet points */
  padding: 0;
  margin: 0;
  display: flex; /* Arrange links in a row */
}

.nav-links li {
  margin-left: 30px; /* Space between navigation items */
}

.nav-links a {
  color: white;
  text-decoration: none;
  font-weight: bold;
  font-size: 1rem;
  padding: 5px 0; /* Padding for click area */
  position: relative; /* For underline effect */
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: #42b983; /* Vue green on hover */
}

/* Optional: Subtle underline effect on hover */
.nav-links a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #42b983;
  transition: width 0.3s ease-in-out;
}

.nav-links a:hover::after {
  width: 100%;
}

/* Basic Responsiveness for smaller screens */
@media (max-width: 768px) {
  .header-nav {
    flex-direction: column; /* Stack title and nav links vertically */
    text-align: center;
  }

  .site-title {
    margin-bottom: 15px; /* Space between title and nav links */
  }

  .nav-links {
    flex-wrap: wrap; /* Allow links to wrap to next line */
    justify-content: center;
  }

  .nav-links li {
    margin: 0 15px 10px 15px; /* Adjust spacing for wrapped links */
  }
}
</style>