<template>
  <section id="about" class="about-section section-padding">
    <div class="container">
      <div class="about-grid">
        <div class="about-content">
          <h2 class="section-title">about me</h2>
          
          <div class="about-text">
            <p class="intro-text">
              i'm an undergraduate student passionate about creating digital experiences 
              that matter. currently studying computer science while exploring the 
              intersection of technology and creativity.
            </p>
            
            <p>
              my journey in programming started with curiosity about how websites work, 
              and has evolved into a deep appreciation for clean code, thoughtful design, 
              and meaningful user experiences.
            </p>
            
            <p>
              when i'm not coding, you'll find me reading about emerging technologies, 
              experimenting with new frameworks, or working on personal projects that 
              challenge me to grow as a developer.
            </p>
          </div>

          <div class="skills-grid">
            <div class="skill-category">
              <h3>frontend</h3>
              <ul>
                <li>vue.js</li>
                <li>react</li>
                <li>javascript</li>
                <li>html & css</li>
                <li>tailwind</li>
              </ul>
            </div>
            
            <div class="skill-category">
              <h3>backend</h3>
              <ul>
                <li>python</li>
                <li>django</li>
                <li>flask</li>
                <li>node.js</li>
                <li>postgresql</li>
              </ul>
            </div>
            
            <div class="skill-category">
              <h3>tools</h3>
              <ul>
                <li>git</li>
                <li>vs code</li>
                <li>figma</li>
                <li>linux</li>
                <li>docker</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="about-visual">
          <div class="profile-card">
            <div class="card-header">
              <div class="card-dots">
                <span class="dot red"></span>
                <span class="dot yellow"></span>
                <span class="dot green"></span>
              </div>
              <span class="card-title">enosh.dev</span>
            </div>
            <div class="card-content">
              <div class="code-lines">
                <div class="code-line">
                  <span class="keyword">const</span> 
                  <span class="variable">developer</span> = {
                </div>
                <div class="code-line indent">
                  <span class="property">name</span>: 
                  <span class="string">'enosh earnest'</span>,
                </div>
                <div class="code-line indent">
                  <span class="property">role</span>: 
                  <span class="string">'student & developer'</span>,
                </div>
                <div class="code-line indent">
                  <span class="property">location</span>: 
                  <span class="string">'india'</span>,
                </div>
                <div class="code-line indent">
                  <span class="property">passion</span>: 
                  <span class="string">'creating'</span>,
                </div>
                <div class="code-line">};</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'aboutsection',
  mounted() {
    this.setupScrollAnimation()
  },
  methods: {
    setupScrollAnimation() {
      const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -100px 0px'
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
    }
  }
}
</script>

<style scoped>
.about-section {
  background: #fff;
  position: relative;
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 300;
  color: #2c3e50;
  margin-bottom: 2rem;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease;
}

.about-content {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease 0.2s;
}

.intro-text {
  font-size: 1.2rem;
  line-height: 1.6;
  color: #2c3e50;
  margin-bottom: 1.5rem;
  font-weight: 500;
}

.about-text p {
  color: #6c757d;
  line-height: 1.7;
  margin-bottom: 1.2rem;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.skill-category h3 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #2c3e50;
  margin-bottom: 1rem;
  text-transform: lowercase;
}

.skill-category ul {
  list-style: none;
  padding: 0;
}

.skill-category li {
  color: #6c757d;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
  position: relative;
  padding-left: 1rem;
}

.skill-category li::before {
  content: '→';
  position: absolute;
  left: 0;
  color: #3498db;
  font-weight: bold;
}

.about-visual {
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease 0.4s;
}

.profile-card {
  width: 100%;
  max-width: 400px;
  background: #1e1e1e;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  font-family: 'Monaco', 'Menlo', monospace;
}

.card-header {
  background: #2d2d2d;
  padding: 1rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.card-dots {
  display: flex;
  gap: 0.5rem;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.dot.red { background: #ff5f57; }
.dot.yellow { background: #ffbd2e; }
.dot.green { background: #28ca42; }

.card-title {
  color: #fff;
  font-size: 0.9rem;
}

.card-content {
  padding: 1.5rem;
  background: #1e1e1e;
}

.code-lines {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.code-line {
  font-size: 0.9rem;
  line-height: 1.4;
}

.code-line.indent {
  padding-left: 2rem;
}

.keyword {
  color: #c678dd;
}

.variable {
  color: #e06c75;
}

.property {
  color: #56b6c2;
}

.string {
  color: #98c379;
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

.visible .section-title,
.visible .about-content,
.visible .about-visual {
  opacity: 1;
  transform: translateY(0);
}

/* responsive */
@media (max-width: 968px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
  
  .about-visual {
    order: -1;
  }
}

@media (max-width: 768px) {
  .skills-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
    margin-top: 2rem;
  }
  
  .profile-card {
    max-width: 100%;
  }
  
  .code-line {
    font-size: 0.8rem;
  }
}
</style>