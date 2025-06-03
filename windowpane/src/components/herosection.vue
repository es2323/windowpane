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
            <div v-if="!selectedProject" class="project-list-view">
              <div class="project-item" v-for="project in projects" :key="project.id" @click="showProjectDetails(project)">
                <h3>{{ project.title }}</h3>
                <p class="project-short-description">{{ project.shortDescription }}</p>
              </div>
            </div>

            <div v-else class="project-detail-view">
              <button class="back-button" @click="backToProjectList()">
                &larr; Back to Projects
              </button>
              <h2>{{ selectedProject.title }}</h2>
              <p>{{ selectedProject.longDescription }}</p>
              
              <div v-if="selectedProject.links && selectedProject.links.length > 0" class="project-links">
                <h3>Links</h3>
                <ul>
                  <li v-for="(link, index) in selectedProject.links" :key="index">
                    <a :href="link.url" target="_blank">{{ link.type }}</a>
                  </li>
                </ul>
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
      selectedProject: null, // Holds the currently selected project for detail view

      projects: [
        {
          id: 'prs',
          title: 'PRS',
          shortDescription: 'Web platform for real-time pandemic data management.',
          longDescription: 'PRS (Performance Reporting System) is a robust application designed to provide instantaneous insights into complex system performance. It leverages advanced data visualization techniques and real-time data streaming to help identify bottlenecks and optimize operations. Developed using [Technologies like Python, Flask, React, D3.js].',
          links: [
            { type: 'GitHub Repo', url: 'https://github.com/enosh-earnest/prs' }, // Placeholder
            { type: 'Live Demo', url: '#' } // Placeholder
          ]
        },
        {
          id: 'seec',
          title: 'SEEC',
          shortDescription: 'Public Transport app for the visually impaired',
          longDescription: 'SEEC (Secure Email Encryption Client) is a desktop application focused on enhancing email privacy through end-to-end encryption. It integrates seamlessly with popular email services and employs [Encryption standard, e.g., AES-256, RSA] to protect sensitive communications. Built with [Technologies like Electron, Node.js, OpenSSL].',
          links: [
            { type: 'GitHub Repo', url: 'https://github.com/enosh-earnest/seec' } // Placeholder
          ]
        },
        {
          id: 'snapback',
          title: 'SnapBack',
          shortDescription: 'Web app tracking employee fatigue through cognitive games and wellness surveys.',
          longDescription: 'SnapBack is an intuitive mobile application designed to help users track and revert progress on tasks with ease. Ideal for managing personal projects or small team workflows, it features a unique "snap-to-previous-state" functionality. Developed for [Platform, e.g., iOS/Android] using [Technologies like React Native, Firebase].',
          links: [
            { type: 'App Store', url: '#' }, // Placeholder
            { type: 'Google Play', url: '#' } // Placeholder
          ]
        },
        {
          id: 'ssh',
          title: 'SSH',
          shortDescription: ' secure client-server system for smart home communication.',
          longDescription: 'SSH (Smart Home Hub) is a centralized control system for various smart home devices, designed for ease of use and interoperability. It provides a unified interface for managing lighting, climate, security, and entertainment systems, offering both local and remote access. Implemented with [Technologies like Raspberry Pi, Home Assistant, MQTT].',
          links: [
            { type: 'GitHub Repo', url: 'https://github.com/enosh-earnest/ssh' } // Placeholder
          ]
        }
      ]
    }
  },
  methods: {
    setActiveSection(section) {
      this.activeSection = section;
      this.selectedProject = null; // Reset selected project when changing main sections
    },
    showProjectDetails(project) {
      this.selectedProject = project;
    },
    backToProjectList() {
      this.selectedProject = null;
    }
  }
}
</script>

<style scoped>
/* --- Hero Section Specific Styles --- */
.hero-section {
  min-height: 100vh;
  background-color: #0d0d0d;
  display: flex;
  align-items: center;
  padding: 20px;
  box-sizing: border-box;
}

.container {
  display: flex;
  flex-grow: 1;
  width: 100%;
  background-color: #1a1a1a;
  border: 1px solid #333;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
  padding: 40px;
  box-sizing: border-box;

  /* MODIFIED: Center the container and give it more overall width */
  max-width: 1500px; /* Increased overall width for content */
  margin-left: auto; /* Center the container horizontally */
  margin-right: auto; /* Center the container horizontally */
}

.two-column {
  display: flex;
  flex-grow: 1;
  gap: 20px; /* This reduced gap helps in softening the "diving line" effect */
  flex-wrap: nowrap;
  width: 100%;
  align-items: stretch;
}

.left-column {
  /* MODIFIED: Make left column wider for name/nav */
  width: 300px; /* Adjust this value (e.g., 250px-350px) to your preference */
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  color: #f0f0f0;
}

.left-column h1 {
  font-size: 3rem;
  margin-bottom: 0.5rem;
  color: #f0f0f0;
  text-align: left;
}

.left-column .large-text {
  font-size: 0.9rem;
  line-height: 1.6;
  color: #aaa;
  margin-top: 0;
  text-align: left;
}

.right-column {
  flex-grow: 1; /* Allows the right column to take up the remaining space */
  min-height: 400px;
  color: #f0f0f0;
  display: flex;
  flex-direction: column;
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
  justify-content: flex-end; /* Keeps content at the bottom */
  padding-bottom: 10px;
}

/* MODIFIED: .about-para for true "bottom left" within its space */
.about-para {
  font-size: 0.8rem;
  line-height: 1.5;
  color: #aaa;
  max-width: 180px; /* Constrain width to allow it to be pushed right */
  margin-top: auto;    /* Pushes content to the center vertically */
  margin-bottom: 100; /* Pushes content to the center vertically */
  margin-left: auto;   /* Pushes content to the right horizontally */
  margin-right: 0;     /* Aligns flush right within its parent */
}

/* Main Navigation Styles */
.main-navigation {
  margin-top: 1rem;
  text-align: left;
}

.nav-item {
  display: block;
  margin-bottom: 0.8rem;
  font-size: 0.8rem;
  cursor: pointer;
  transition: all 0.2s ease;
  text-transform: capitalize;
  color: #f0f0f0;
  text-align: left;
}

.nav-item:hover {
  opacity: 0.6;
}

.nav-item.active {
  font-weight: 700;
  opacity: 1;
  color: white;
}

/* Project List Styles (List View) */
.project-list-view {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  text-align: left;

  /* NEW: Positioning for "center right" */
  max-width: 1000px; /* Constrain width to allow it to be pushed right */
  margin-top: auto;    /* Pushes content to the center vertically */
  margin-bottom: auto; /* Pushes content to the center vertically */
  margin-left: auto;   /* Pushes content to the right horizontally */
  margin-right: 0;     /* Aligns flush right within its parent */
}

.project-list-view .project-item {
  /* REMOVED: border-bottom: 1px solid #333; */ /* This horizontal line was removed */
  padding-bottom: 0.5rem;
  cursor: pointer;
  transition: opacity 0.2s ease;
}

.project-list-view .project-item:last-child {
  border-bottom: none; /* This rule is now redundant as no border is applied above */
}

.project-list-view .project-item:hover {
  opacity: 0.7;
}

.project-list-view .project-item h3 {
  font-size: 3.8rem;
  font-weight: 100;
  margin-bottom: 0.5rem;
  line-height: 1;
  color: #f0f0f0;
  text-align: right;
}

.project-list-view .project-short-description {
  font-size: 0.9rem;
  color: #ffffff;
  line-height: 1.4;
  margin-bottom: 0;
  text-align: right;
}

/* Project Detail View */
.project-detail-view {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  text-align: left;

  /* NEW: Positioning for "center right" similar to project list */
  max-width: 450px; /* Apply similar width constraint */
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 0;
}

.project-detail-view h2 {
  font-size: 2rem;
  margin-bottom: 0.5rem;
  color: #f0f0f0;
  text-align: left;
}

.project-detail-view h3 {
  font-size: 1.2rem;
  margin-top: 2rem;
  margin-bottom: 0.8rem;
  color: #f0f0f0;
  text-align: left;
}

.project-detail-view p {
  font-size: 1rem;
  line-height: 1.6;
  color: #aaa;
  max-width: none;
  text-align: left;
}

.project-links ul {
  list-style: none;
  padding-left: 0;
  margin-top: 0.5rem;
}

.project-links li {
  margin-bottom: 0.5rem;
  text-align: left;
}

.project-links a {
  color: #f0f0f0;
  text-decoration: underline;
  transition: opacity 0.2s ease;
}

.project-links a:hover {
  opacity: 0.8;
  color: white;
}

.back-button {
  background: none;
  border: none;
  color: #aaa;
  font-size: 1rem;
  cursor: pointer;
  text-align: left;
  padding: 0;
  margin-bottom: 2rem;
  transition: color 0.2s ease;
}

.back-button:hover {
  color: white;
}


/* Experience Content Styles */
.experience-content {
  /* No specific text-align needed here if parent is left-aligned */
}

/* About and Contact Content Styles */
.about-content h3,
.contact-content h3,
.experience-content h3 {
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 0.8rem;
  margin-top: 2rem;
  color: #f0f0f0;
  text-align: left;
}

.about-content h3:first-child,
.contact-content h3:first-child,
.experience-content h3:first-child {
  margin-top: 0;
}

.about-content p,
.contact-content p,
.experience-content p {
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  max-width: none;
  color: #aaa;
  text-align: left;
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
    max-width: 100%;
    margin-left: 0;
    margin-right: 0;
  }
  .two-column {
    flex-direction: column;
    gap: 20px;
    flex-wrap: wrap;
  }
  .left-column {
    width: auto;
    flex-shrink: 1;
    max-width: 100%;
  }
  .right-column {
    min-height: unset;
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

  .home-content {
    justify-content: flex-start;
    padding-bottom: 0;
  }
  .about-para {
    margin-left: 0;
    text-align: left;
    max-width: 100%;
  }

  .project-list-view {
    gap: 2rem;
  }

  .project-list-view .project-item {
    padding-bottom: 1rem;
  }

  .project-detail-view h2 {
    font-size: 1.8rem;
  }
}
</style>