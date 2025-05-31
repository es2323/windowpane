<template>
  <section id="projects" class="projects-section section-padding">
    <div class="container">
      <h2 class="section-title fade-in">projects</h2>
      
      <div class="projects-grid">
        <div 
          v-for="(project, index) in projects" 
          :key="index"
          class="project-card fade-in"
          :style="{ animationDelay: `${index * 0.1}s` }"
          @click="openProject(project.link)"
        >
          <div class="project-header">
            <div class="project-date">{{ project.date }}</div>
            <div class="project-status">{{ project.status }}</div>
          </div>
          
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            
            <div class="project-tech">
              <span 
                v-for="tech in project.technologies"
                :key="tech"
                class="tech-tag"
              >
                {{ tech }}
              </span>
            </div>
          </div>
          
          <div class="project-footer">
            <div class="project-links">
              <a 
                v-if="project.github" 
                :href="project.github" 
                target="_blank"
                class="project-link"
                @click.stop
              >
                github
              </a>
              <a 
                v-if="project.demo" 
                :href="project.demo" 
                target="_blank"
                class="project-link demo"
                @click.stop
              >
                live demo
              </a>
            </div>
          </div>
        </div>
      </div>
      
      <div class="more-projects fade-in">
        <p class="more-text">
          more projects available on 
          <a href="https://github.com/yourusername" target="_blank" class="github-link">
            github
          </a>
        </p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'projectssection',
  data() {
    return {
      projects: [
        {
          title: 'windowpane portfolio',
          description: 'a minimalist personal portfolio website built with Vue.js, featuring smooth animations and responsive design inspired by modern web aesthetics.',
          date: 'may 2025',
          status: 'design & dev',
          technologies: ['vue.js', 'css3', 'javascript'],
          github: 'https://github.com/yourusername/windowpane',
          demo: 'https://yourdomain.com',
          link: 'https://yourdomain.com'
        },
        {
          title: 'task flow manager',
          description: 'a collaborative task management application with real-time updates, built using python django backend and vue.js frontend.',
          date: 'apr 2025',
          status: 'design & dev',
          technologies: ['python', 'django', 'vue.js', 'postgresql'],
          github: 'https://github.com/yourusername/task-flow',
          demo: 'https://taskflow-demo.com',
          link: 'https://taskflow-demo.com'
        },
        {
          title: 'weather insight',
          description: 'a clean weather application that provides detailed forecasts with beautiful data visualizations and location-based insights.',
          date: 'mar 2025',
          status: 'design & dev',
          technologies: ['react', 'api integration', 'chart.js'],
          github: 'https://github.com/yourusername/weather-insight',
          demo: 'https://weather-insight-demo.com',
          link: 'https://weather-insight-demo.com'
        },
        {
          title: 'code snippet vault',
          description: 'a personal collection of reusable code snippets with syntax highlighting, search functionality, and easy sharing capabilities.',
          date: 'feb 2025',
          status: 'dev',
          technologies: ['flask', 'sqlite', 'prism.js'],
          github: 'https://github.com/yourusername/snippet-vault',
          demo: null,
          link: 'https://github.com/yourusername/snippet-vault'
        },
        {
          title: 'campus connect',
          description: 'a student networking platform for my university, connecting students through shared interests, study groups, and academic collaboration.',
          date: 'jan 2025',
          status: 'design & dev',
          technologies: ['node.js', 'express', 'mongodb', 'socket.io'],
          github: 'https://github.com/yourusername/campus-connect',
          demo: 'https://campus-connect-demo.com',
          link: 'https://campus-connect-demo.com'
        },
        {
          title: 'learning tracker',
          description: 'a personal learning dashboard to track progress across different subjects, with goal setting and achievement visualization.',
          date: 'dec 2024',
          status: 'dev',
          technologies: ['python', 'tkinter', 'sqlite'],
          github: 'https://github.com/yourusername/learning-tracker',
          demo: null,
          link: 'https://github.com/yourusername/learning-tracker'
        }
      ]
    }
  },
  mounted() {
    this.setupScrollAnimation()
  },
  methods: {
    setupScrollAnimation() {
      const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -50px 0px'
      }

      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible')
          }
        })
      }, observerOptions)

      const animatedElements = this.$el.querySelectorAll('.fade-in')
      animatedElements.forEach(el => observer.observe(el))
    },
    openProject(link) {
      if (link) {
        window.open(link, '_blank')
      }
    }
  }
}
</script>

<style scoped>
.projects-section {
  background: #f8f9fa;
  position: relative;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 300;
  color: #2c3e50;
  margin-bottom: 3rem;
  text-align: center;
}

.projects-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.project-card {
  background: white;
  border-radius: 8px;
  padding: 2rem;
  transition: all 0.3s ease;
  cursor: pointer;
  border: 2px solid transparent;
  position: relative;
  overflow: hidden;
}

.project-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  border-color: #3498db;
}

.project-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, #3498db, #2ecc71, #f39c12, #e74c3c);
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.project-card:hover::before {
  transform: scaleX(1);
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
  font-size: 0.9rem;
}

.project-date {
  color: #6c757d;
  font-weight: 500;
}

.project-status {
  color: #3498db;
  font-weight: 600;
  text-transform: lowercase;
}

.project-content {
  margin-bottom: 1.5rem;
}

.project-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #2c3e50;
  margin-bottom: 1rem;
  text-transform: lowercase;
}

.project-description {
  color: #6c757d;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  background: #e9ecef;
  color: #6c757d;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
  transition: all 0.3s ease;
}

.project-card:hover .tech-tag {
  background: #3498db;
  color: white;
}

.project-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.project-links {
  display: flex;
  gap: 1rem;
}

.project-link {
  color: #6c757d;
  font-size: 0.9rem;
  font-weight: 500;
  text-decoration: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  transition: all 0.3s ease;
  border: 1px solid #dee2e6;
}

.project-link:hover {
  color: #3498db;
  border-color: #3498db;
  transform: translateY(-1px);
}

.project-link.demo {
  background: #3498db;
  color: white;
  border-color: #3498db;
}

.project-link.demo:hover {
  background: #2980b9;
  color: white;
}

.more-projects {
  text-align: center;
  padding: 2rem 0;
}

.more-text {
  color: #6c757d;
  font-size: 1.1rem;
}

.github-link {
  color: #3498db;
  font-weight: 600;
  text-decoration: none;
  transition: color 0.3s ease;
}

.github-link:hover {
  color: #2980b9;
}

/* animation classes */
.fade-in {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease;
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

/* responsive */
@media (max-width: 768px) {
  .project-card {
    padding: 1.5rem;
  }
  
  .project-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }
  
  .project-links {
    flex-direction: column;
    gap: 0.5rem;
    width: 100%;
  }
  
  .project-link {
    text-align: center;
  }
  
  .tech-tag {
    font-size: 0.75rem;
  }
}

@media (max-width: 480px) {
  .project-card {
    padding: 1rem;
  }
  
  .project-title {
    font-size: 1.25rem;
  }
}
</style>