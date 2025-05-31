<template>
  <section class="hero-section">
    <div class="container">
      <div class="two-column">
        <!-- Left Column: Name, Description, Navigation -->
        <div class="left-column">
          <h1>Your Name</h1>
          <p class="large-text">
            Born in 1994 in Your City, Country. I believe web design can be more diverse and inspiring. With a mission to present the possibilities of web design, I am pursuing new expressions through experiments and thoughts.
          </p>
          
          <nav class="main-navigation">
            <div 
              class="nav-item" 
              :class="{ active: activeSection === 'projects' }"
              @click="setActiveSection('projects')"
            >
              projects
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

        <!-- Right Column: Dynamic Content -->
        <div class="right-column">
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
  name: 'herosection',
  data() {
    return {
      activeSection: 'projects', // Default to projects
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
.hero-section {
  min-height: 100vh;
  background-color: #faf9f7;
}

.main-navigation {
  margin-top: 3rem;
}

.nav-item {
  display: block;
  margin-bottom: 0.8rem;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.nav-item:hover {
  opacity: 0.6;
}

.nav-item.active {
  font-weight: 500;
  opacity: 1;
}

.content-section {
  animation: fadeIn 0.4s ease-in-out;
}

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

.project-list {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.project-item {
  border-bottom: 1px solid #e5e5e5;
  padding-bottom: 1.5rem;
}

.project-item:last-child {
  border-bottom: none;
}

.project-item h3 {
  font-size: 1.25rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
  line-height: 1.2;
}

.project-meta {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  font-size: 0.9rem;
  color: #666;
  line-height: 1.4;
}

.project-date {
  font-weight: 500;
}

.about-content h3,
.contact-content h3 {
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 0.8rem;
  margin-top: 2rem;
}

.about-content h3:first-child,
.contact-content h3:first-child {
  margin-top: 0;
}

.about-content p,
.contact-content p {
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  max-width: none;
}

.contact-content a {
  color: #1a1a1a;
  text-decoration: none;
  transition: opacity 0.2s ease;
}

.contact-content a:hover {
  opacity: 0.6;
}

/* Mobile responsiveness */
@media (max-width: 768px) {
  .main-navigation {
    margin-top: 2rem;
    margin-bottom: 2rem;
  }
  
  .project-list {
    gap: 2rem;
  }
  
  .project-item {
    padding-bottom: 1rem;
  }
}
</style>