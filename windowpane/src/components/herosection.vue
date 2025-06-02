<template>
  <section class="hero-section">
    <div class="container">
      <div class="two-column">
        <div class="left-column">
          <h1>Enosh Earnest</h1>
          <p class="large-text">
            CS Undergrad & AI Aficionado 
          </p>

          <nav class="main-navigation">
            <div
              class="nav-item"
              :class="{ active: activeSection === 'home' }"
              @click="setActiveSection('home')"
            >
              home
            </div>
            <div
              class="nav-item"
              :class="{ active: activeSection === 'projects' }"
              @click="setActiveSection('projects')"
            >
              projects
            </div>
            <div
              class="nav-item"
              :class="{ active: activeSection === 'experience' }"
              @click="setActiveSection('experience')"
            >
              experience
            </div>
            <div
              class="nav-item"
              :class="{ active: activeSection === 'about' }"
              @click="setActiveSection('about')"
            >
              about
            </div>
            <div
              class="nav-item"
              :class="{ active: activeSection === 'contact' }"
              @click="setActiveSection('contact')"
            >
              contact
            </div>
          </nav>
        </div>

        <div class="right-column">
          <div v-if="activeSection === 'home'" class="content-section fade-in visible">
            <div class="home-content">
              <p class="about-para">
                Firm believer in leveraging computational mathematics to build intelligent applications—from accessibility focused mobile apps to autonomous resource allocation systems. My work thrives where mathematical rigour meets human complexity, crafting systems that amplify rather than automate judgement. Based in the UK. 
              </p>
            </div>
          </div>

          <div v-if="activeSection === 'projects'" class="content-section fade-in visible">
            <div class="project-list">
              <div class="project-item" v-for="project in projects" :key="project.id">
                <h3>{{ project.title }}</h3>
                <div class="project-meta">
                  <span class="project-date">{{ project.date }}</span>
                  <span class="project-role">{{ project.role }}</span>
                  <span v-if="project.collaborator" class="project-collaborator">
                    {{ project.collaborator }}
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div v-if="activeSection === 'experience'" class="content-section fade-in visible">
            <div class="experience-content">
              <h3>Professional Experience</h3>
              <p>
                List your internships, part-time jobs, academic roles, etc. here.
                Include dates, company/institution names, and brief descriptions of your responsibilities and achievements.
              </p>
              <h3>Skills Gained</h3>
              <p>Highlight specific technologies, methodologies, or soft skills developed.</p>
              </div>
          </div>

          <div v-if="activeSection === 'about'" class="content-section fade-in visible">
            <div class="about-content">
              <h3>Background</h3>
              <p>
                I'm a web designer and developer focused on creating unique digital experiences.
                I specialize in WebGL, Three.js, and experimental web technologies.
              </p>

              <h3>Skills</h3>
              <p>
                Frontend Development, WebGL/GLSL, Three.js, Vue.js, Creative Coding,
                UI/UX Design, Motion Graphics
              </p>

              <h3>Awards</h3>
              <p>
                - Awwwards Site of the Day<br>
                - Independent Designer of the Year Nominee
              </p>
            </div>
          </div>

          <div v-if="activeSection === 'contact'" class="content-section fade-in visible">
            <div class="contact-content">
              <h3>Get in Touch</h3>
              <p>
                <a href="mailto:your@email.com">your@email.com</a>
              </p>

              <h3>Social</h3>
              <p>
                <a href="#" target="_blank">Twitter</a><br>
                <a href="#" target="_blank">GitHub</a><br>
                <a href="#" target="_blank">Instagram</a>
              </p>

              <h3>Location</h3>
              <p>Your City, Country</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',
  data() {
    return {
      activeSection: 'home', // Default to home
      projects: [
        {
          id: 1,
          title: 'Project Alpha',
          date: 'Apr.2025',
          role: 'Design & Dev'
        },
        {
          id: 2,
          title: 'Creative Portfolio',
          date: 'Mar.2025',
          role: 'Dev',
          collaborator: 'Design: Jane Doe'
        },
        {
          id: 3,
          title: 'Interactive Experience',
          date: 'Feb.2025',
          role: 'Design & Dev'
        },
        {
          id: 4,
          title: 'Brand Website',
          date: 'Jan.2025',
          role: 'Frontend Dev',
          collaborator: 'Design: Studio XYZ'
        },
        {
          id: 5,
          title: 'WebGL Experiment',
          date: 'Dec.2024',
          role: 'Design & Dev'
        }
      ]
    }
  },
  methods: {
    setActiveSection(section) {
      this.activeSection = section
    }
  }
}
</script>

<style scoped>
/* REMOVED: All body and global font-family rules from here. They are now assumed to be in App.vue */

/* --- Hero Section Specific Styles --- */
.hero-section {
  min-height: 100vh; /* Ensures it takes at least the full viewport height */
  background-color: #0d0d0d; /* Specific background for hero section */
  display: flex; /* Make hero-section a flex container */
  align-items: center; /* Vertically centers the content (container) within the viewport */
  padding: 20px; /* This creates the "little room outside" around the main content box */
  box-sizing: border-box; /* Include padding in element's total width/height */
}

.container {
  display: flex; /* Make container a flex container */
  flex-grow: 1; /* Allows it to grow to fill hero-section's height */
  width: 100%; /* Ensures it takes full width within hero-section's padding */
  background-color: #1a1a1a; /* Slightly lighter dark for the 'box' effect */
  border: 1px solid #333; /* Border for the 'box' */
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.5); /* Subtle shadow for depth */
  margin: 0; /* No auto margin needed, padding handles spacing */
  padding: 40px; /* Internal padding within the bordered box */
  box-sizing: border-box; /* Include padding in element's total width/height */
}

.two-column {
  display: flex;
  flex-grow: 1; /* Allows it to grow to fill container's height */
  justify-content: space-between;
  gap: 40px; /* Space between columns */
  flex-wrap: nowrap; /* Prevent wrapping by default on large screens */
  width: 100%; /* Ensures it takes full width of container */
  align-items: stretch; /* Ensures flex children (left/right columns) stretch to fill height */
}

.left-column {
  flex: 1; /* Allows the left column to grow */
  min-width: 250px; /* Adjusted minimum width for left column */
  max-width: 350px; /* Max width to control its size */
  display: flex; /* Make it a flex container */
  flex-direction: column; /* Stack content vertically */
  padding-right: 20px; /* Add some space to the right of left column */
  color: #f0f0f0; /* Light text color for left column content */
}

.left-column h1 {
  font-size: 2.5rem; /* Specific font size for this h1 */
  margin-bottom: 0.5rem;
  color: #f0f0f0; /* Ensure title is light */
}

.left-column .large-text {
  font-size: 0.9rem; /* Specific font size for this large-text */
  line-height: 1.6;
  color: #aaa; /* Slightly subdued text */
  margin-top: 0;
}

.right-column {
  flex: 2; /* Allows the right column to grow more than the left */
  display: flex; /* Make it a flex container */
  flex-direction: column; /* Stack content vertically */
  min-height: 400px; /* Gives it a minimum height for visual balance if content is short */
  color: #f0f0f0; /* Light text color for right column content */
}

/* Common Styles for Dynamic Content Sections */
.content-section {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  animation: fadeIn 0.4s ease-in-out;
}

/* Specific Styles for Home Content & About Paragraph */
.home-content {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding-bottom: 10px;
}

.about-para {
  font-size: 0.8rem;
  line-height: 1.5;
  color: #aaa;
  max-width: 200px;
  margin-bottom: 0;
  margin-left: auto;
  text-align: left;
  padding-right: 10px;
}

/* Main Navigation Styles */
.main-navigation {
  margin-top: 1rem;
}

.nav-item {
  display: block;
  margin-bottom: 0.8rem;
  font-size: 1rem; /* Adjusted from 1.1rem */
  cursor: pointer;
  transition: all 0.2s ease;
  text-transform: capitalize;
  color: #f0f0f0; /* Ensure nav items are light */
}

.nav-item:hover {
  opacity: 0.6;
}

.nav-item.active {
  font-weight: 500;
  opacity: 1;
  color: white;
}

/* Project List Styles */
.project-list {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.project-item {
  border-bottom: 1px solid #333;
  padding-bottom: 1.5rem;
}

.project-item:last-child {
  border-bottom: none;
}

.project-item h3 {
  font-size: 1.25rem; /* Specific font size for this h3 */
  font-weight: 500;
  margin-bottom: 0.5rem;
  line-height: 1.2;
  color: #f0f0f0;
}

.project-meta {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  font-size: 0.9rem;
  color: #aaa;
  line-height: 1.4;
}

.project-date {
  font-weight: 500;
}

/* NEW: Experience Content Styles (inherits most styles but can be customized) */
.experience-content {
  /* Add specific styles here if needed, or it will inherit from global p/h3 */
}

/* About and Contact Content Styles */
.about-content h3,
.contact-content h3,
.experience-content h3 { /* Added experience-content h3 here */
  font-size: 1.1rem; /* Specific font size for these h3s */
  font-weight: 500;
  margin-bottom: 0.8rem;
  margin-top: 2rem;
  color: #f0f0f0;
}

.about-content h3:first-child,
.contact-content h3:first-child,
.experience-content h3:first-child { /* Added experience-content h3 here */
  margin-top: 0;
}

.about-content p,
.contact-content p,
.experience-content p { /* Added experience-content p here */
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  max-width: none;
  color: #aaa;
}

.contact-content a {
  color: #f0f0f0;
  text-decoration: none;
  transition: opacity 0.2s ease;
}

.contact-content a:hover {
  opacity: 0.6;
  color: white;
}

/* Fade-in Animation */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* --- Mobile Responsiveness --- */
@media (max-width: 768px) {
  .hero-section {
    padding: 10px;
  }
  .container {
    padding: 20px;
    flex-direction: column;
  }
  .two-column {
    flex-direction: column;
    gap: 20px;
    flex-wrap: wrap;
  }
  .left-column, .right-column {
    min-width: unset;
    max-width: 100%;
    min-height: unset;
    padding-left: 0;
    padding-right: 0;
    align-items: flex-start;
  }

  .left-column h1, .left-column .large-text {
    text-align: left;
  }
  
  .main-navigation {
    margin-top: 2rem;
    margin-bottom: 2rem;
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
  }

  .nav-item {
    margin-bottom: 0;
  }

  /* Adjust home content for mobile */
  .home-content {
    justify-content: flex-start;
    padding-bottom: 0;
  }
  .about-para {
    margin-left: 0;
    text-align: left;
    max-width: 100%;
  }

  .project-list {
    gap: 2rem;
  }

  .project-item {
    padding-bottom: 1rem;
  }
}
</style>