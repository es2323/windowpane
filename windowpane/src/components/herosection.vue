<template>
  <section class="hero-section">
        <P5AnimationBackground
      :background-color="'#222831'"
      :particle-color="'#FFFBEB'"
      :line-color="'#FFFBEB'"
    />
    <div class="container">
      <div class="two-column" :class="{ 'about-full-layout': activeSection === 'about' }">
        <div class="left-column">
          <h1>Enosh Earnest</h1>
          <p class="large-text">
            CS Undergrad & AI Explorer
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
          <div class="liminal-toggle-wrapper" @click="toggleLiminalMode">
              <svg 
  id="liminal-toggle"
  width="20" 
  height="20" 
  viewBox="0 0 338 338" 
  fill="currentColor" 
  xmlns="http://www.w3.org/2000/svg"
>
  <title>Toggle Liminal Mode</title>
  <path d="M129.7,135.3H0v24h153.7V5.2h-24V135.3z M207.8,135.1V5.4h-24v153.7H338v-24H207.8z M0,202.7h129.7v130.1h24V178.7H0V202.7z M183.9,332.6h23.9V202.9H338v-24H183.9V332.6z"/>
              </svg>
          </div>
        </div>

        <div class="right-column">
          <div v-if="activeSection === 'home'" class="content-section fade-in visible">
            <div class="home-content">
              <p class="about-para">
                Firm believer in leveraging computational mathematics to build intelligent applications, from accessibility focused mobile apps to autonomous resource allocation systems. My work thrives where mathematical rigour meets human complexity, crafting systems that amplify rather than automate judgement.<br>Based in the UK.
              </p>
            </div>
          </div>

          <div v-if="activeSection === 'projects'" class="content-section fade-in visible">
            <div v-if="!selectedProject" class="project-list-view">
              <div class="project-item" 
                  v-for="(project, index) in projects" 
                  :key="project.id" 
                  @click="showProjectDetails(project)"
                  :style="{ animationDelay: index * 0.3 + 's' }">  <h3>{{ project.title }}</h3>
                  <p class="project-short-description">{{ project.shortDescription }}</p>
              </div>
            </div>

            <div v-else class="project-detail-view">
              <button class="back-button" @click="backToProjectList()">
                ↖ Back to Projects
              </button>
              <h2>{{ selectedProject.title }}</h2>
              <p v-html="selectedProject.longDescription"></p>

              <div v-if="selectedProject.links && selectedProject.links.length > 0" class="project-links">
                <ul>
                  <li v-for="(link, index) in selectedProject.links.filter(l => l.type === 'GitHub')" :key="index">
                    <a :href="link.url" target="_blank">GitHub➚</a>
                  </li>
                </ul>
              </div>
            </div>
          </div>

          <div v-if="activeSection === 'experience'" class="content-section fade-in visible">
            <div v-if="!selectedExperience" class="experience-list-view">
              <div class="experience-item" v-for="(exp, index) in experiences" :key="exp.id" @click="showExperienceDetails(exp)" :style="{ animationDelay: index * 0.3 + 's' }">
                <h3>{{ exp.title }}</h3>
                <p class="experience-company-duration">{{ exp.company }}/ {{ exp.duration }}</p>
                <p class="experience-short-description">{{ exp.shortDescription }}</p>
              </div>
            </div>

            <div v-else class="experience-detail-view">
              <button class="back-button" @click="backToExperienceList()">
                ↖ Back to Experiences
              </button>
              <h2>{{ selectedExperience.title }}</h2>
              <p class="experience-company-duration">{{ selectedExperience.company }}/ {{ selectedExperience.duration }}</p>

              <div class="experience-description">
                <ul>
                  <li v-for="(point, index) in selectedExperience.longDescription" :key="index">{{ point }}</li>
                </ul>
              </div>

              <div v-if="selectedExperience.skills && selectedExperience.skills.length > 0" class="experience-skills">
                <h3>Skills</h3>
                <p>{{ selectedExperience.skills.join('/ ') }}</p>
              </div>
            </div>
          </div>

          <div v-if="activeSection === 'about'" class="content-section fade-in visible">
            <div class="about-content">
              <div class="about-grid">
                <div class="about-main-text">
                  <h3>Beyond the Code...</h3>   
                  <p>
                    Hi, I'm Enosh, a Computer Science student and AI enthusiast based in the rocky midlands of the UK. With a passion for computational mathematics, I specialize in crafting intelligent applications, focusing on backend development, intuitive UI/UX design, and robust database solutions, all whilst drawing on my experience across digital content creation and performance marketing.
                  </p>
                  <p>
                    <br>When I'm not immersed in code, you'll find me captivated by the intriguing liminal spaces, exploring the hidden corners of new cities, or unwinding to the smooth rhythms of jazz. I thrive on learning, building, and engaging with fellow innovators and curious minds.
                  </p>
                </div>

                <div class="about-sidebar">
                  <p>
                    <a href="/Enosh Earnest Resume.pdf" download="Enosh Earnest's Resume.pdf" class="resume-download">
                Download My Resume!
                    </a>
                  </p>
                </div>
              </div>
            </div>
          </div>

          <div v-if="activeSection === 'contact'" class="content-section fade-in visible">
            <div class="contact-content centered-links">
              <a href="mailto:enoshsolomonn@gmail.com" target="_blank">Email➚</a>
              <a href="https://www.linkedin.com/in/enosh-solomon-3370321bb/" target="_blank">LinkedIn➚</a>
              <a href="https://github.com/es2323" target="_blank">GitHub➚</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// Import the new P5AnimationBackground component
import P5AnimationBackground from './P5AnimationBackground.vue';
export default {
  name: 'HeroSection',
  components: {
    P5AnimationBackground // Register the component
  },
  

  data() {
    return {
      activeSection: 'home', // Default to home
      selectedProject: null, // Holds the currently selected project for detail view
      selectedExperience: null, // NEW: Holds the currently selected experience for detail view
      isLiminalMode: false,

      projects: [
        {
          id: 'seec',
          title: "SEEC/ May 25'",
          shortDescription: 'Public Transport app for the visually impaired/ Made for Journeo',
          longDescription: "A public transport app for the visually impaired.<br>Partnering with Journeo Plc, we developed SEEC. This voice-first mobile app uses the Google Vision API to read street signs aloud and delivers routes with 95% accuracy. The result: a tool that doesn't just give directions, but slashes navigational anxiety by 25%, empowering independent travel.",
          links: [
            { type: 'GitHub', url: 'https://github.com/es2323/SEEC' } // Placeholder
          ]
        },
        {
          id: 'snapback',
          title: "SnapBack/ May 25'",
          shortDescription: 'Web app tracking employee fatigue via cognitive games and wellness surveys',
          longDescription: "An employee fatigue monitoring platform.<br>What if you could measure team burnout with a game? That's SnapBack. This web app uses Python Flask and Pygame to turn cognitive challenges into a live measure of employee fatigue. It gives managers a real-time dashboard (loading in <150ms) to track team wellbeing, offering proactive insights long before burnout becomes a problem.",
          links: [
            { type: 'GitHub', url: 'https://github.com/es2323/SnapBack' } // Placeholder
          ]
        },
        {
          id: 'prs',
          title: "PRS/ May 25'",
          shortDescription: 'Web platform for pandemic data management',
          longDescription: 'Web platform for pandemic data management.<br>Built for public safety under pressure, this platform delivers speed and security. Using Python Flask, and combining SQL Server (for critical compliance data) with MongoDB (for dynamic field reports). With 100% password encryption and query responses under 100ms, the system gives health officials the fast, reliable, and consistent data needed for decisive action.', links: [
            { type: 'GitHub', url: 'https://github.com/es2323/Pandemic-Resilience-System-' },

          ]
        },
        {
          id: 'ssh',
          title: "SSH/ Dec 24'",
          shortDescription: 'Secure client-server system for smart home communication',
          longDescription: "Secure smart home client-server system.<br>This is a secure and high-performance communication backbone for smart homes, built with Python's asyncio library. The system uses strong AES encryption to secure every message and was stress-tested for 48 hours straight, effortlessly handling high traffic from multiple clients with near-perfect accuracy.",
          links: [
            { type: 'GitHub', url: 'https://github.com/es2323/Client_Server-' } // Placeholder

          ]
        }
      ],
      // NEW: Experience Data
      experiences: [
        {
          "id": "designer-intern",
          "title": "Designer",
          "company": "University of Derby Enterprise Centre",
          "duration": "Mar to July 24'",
          "shortDescription": "Created digital content templates, optimized CRM processes, and managed databases to enhance operational efficiency",
          "longDescription": [
            "Delivered a comprehensive operational upgrade, from front-facing content to backend data. This involved designing 13 digital templates to accelerate content creation, optimizing the CRM for 400 individuals, and refining 8 databases to boost accuracy, accessibility, and security."
          ],
          "skills": [
            "Digital Content Design",
            "Template Creation",
            "Content Creation",
            "Database Management",
            "CRM Optimization",
            "Data Normalization",
            "Process Efficiency",
            "DaVinci Resolve",
            "Microsoft Dynamics 365//"
          ]
        },
        {
          id: 'marketing-intern',
          title: 'Marketing Intern',
          company: 'Not Another Agency',
          duration: "Jan to June 23'",
          shortDescription: 'Managed social media presence, optimized performance marketing, and analyzed ad campaign performance for diverse clients',
          longDescription: [
            "Managed social media presence for up to 6 organizations across various platforms (Facebook, Instagram, Twitter, LinkedIn, YouTube, TikTok), including an NGO focused on postpartum depression.",
            "Achieved a 30% increase in follower count for a luxury villa through strategic content creation and targeted campaigns.",
            "Curated a 3x increase in ad frequency for an NGO dedicated to under-privileged youth, significantly boosting engagement and helping the organization reach a wider, more relevant audience."
          ],
          skills: ['Marketing Strategy', 'Market Research', 'Social Media Management', 'Campaign Management', 'Content Creation//']
        }
      ]
    }
  },
  methods: {
    setActiveSection(section) {
      this.activeSection = section;
      this.selectedProject = null; // Reset selected project when changing main sections
      this.selectedExperience = null; // NEW: Reset selected experience when changing main sections

    },
    showProjectDetails(project) {
      this.selectedProject = project;
    },
    backToProjectList() {
      this.selectedProject = null;
    },
    // NEW: Experience Methods
    showExperienceDetails(exp) {
      this.selectedExperience = exp;
    },
    backToExperienceList() {
      this.selectedExperience = null;
    },
    toggleLiminalMode() {
    // This flips our state variable between true and false
    this.isLiminalMode = !this.isLiminalMode;
    
    // This adds or removes a class from the main <body> tag of the page
    document.body.classList.toggle('liminal-mode-active');
  }
  }
}
</script>

<style scoped>
/* --- Hero Section Specific Styles --- */
.hero-section {
  height: 100vh;
  overflow: hidden;
  background-color: #222831; /* Main background */
  display: flex;
  align-items: center;
  padding: 20px;
  box-sizing: border-box;
  position: relative;
}

.container {
  display: flex;
  flex-grow: 1;
  width: 100%;
  background-color: transparent; /* Main background */
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  padding: 40px;
  box-sizing: border-box;
  position: relative;
  z-index: 1; 
  max-height: 100%;         /* Prevents the box from growing too tall */
  overflow-y: auto; 

  /* MODIFIED: Center the container and give it more overall width */
  max-width: 1500px;
  margin-left: auto;
  margin-right: auto;
}

.two-column {
  display: flex;
  flex-grow: 1;
  gap: 20px;
  flex-wrap: nowrap;
  width: 100%;
  align-items: stretch;
  position: relative;
  z-index: 2;
}

.left-column {
  width: 300px;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  color: #FFFBEB; /* Primary text */
}

.left-column h1 {
  font-size: 3.3rem;
  margin-bottom: 0.5rem;
  color: #FFFBEB; /* Primary text */
  text-align: left;
}

.left-column .large-text {
  font-size: 1rem;
  line-height: 1.6;
  color: #FFFBEB; /* Secondary text */
  margin-top: 0;
  text-align: left;
}

.right-column {
  flex-grow: 1;
  min-height: 400px;
  color: #FFFBEB; /* Primary text */
  display: flex;
  flex-direction: column;
  position: relative;
}

/* Common Styles for Dynamic Content Sections */
.content-section {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  animation: fadeIn 1.5s ease-in-out;
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
  color: #FFFBEB; /* Secondary text */
  max-width: 180px;
  margin-top: auto;
  margin-bottom: 100;
  margin-left: auto;
  margin-right: 0;
}

/* Main Navigation Styles */
.main-navigation {
  margin-top: 1rem;
  text-align: left;
  animation: fadeIn 1.5s ease-in-out;
  
}

.nav-item {
  display: block;
  margin-bottom: 0.8rem;
  font-size: 0.8rem;
  cursor: pointer;
  transition: all 0.2s ease;
  text-transform: capitalize;
  color: #FFFBEB; /* Primary text */
  text-align: left;
  position: relative; /* Needed for the pseudo-element */
  padding-bottom: 2px;
  
}

.nav-item::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0; /* Starts with zero width */
  height: 1px;
  background-color: #B89A6A; /* Your new accent color */
  transition: width 0.3s ease; /* Animate the width change */
}

.nav-item:hover::after {
  width: 40%; /* Expands to full width on hover */
}

.nav-item:hover {
  opacity: 0.8;
  color: #B89A6A; /* "The rest" (now matches secondary text) */
  transform: translateX(5px); 
}

.nav-item.active {
  font-weight: 700;
  opacity: 1;
  color: #FFFBEB; /* "The rest" (now matches secondary text) */
}

.project-list-view {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  text-align: left;
  animation: fadeIn 1s ease-in-out;
  max-width: 1000px;
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 0;
}

.project-list-view .project-item {
  padding-bottom: 0.5rem;
  cursor: pointer;
  
  /* FIX #1: The two 'transition' properties were combined into one. */
  transition: all 0.3s ease-out; 
  
  /* Your waterfall animation is correct */
  animation: fadeIn 0.5s ease-in-out;
  animation-fill-mode: forwards;
  opacity: 0;
}

.project-list-view .project-item:last-child {
  border-bottom: none;
}

/* FIX #2: The old hover rule is replaced by the one below, which is more specific. */
.project-list-view .project-item:hover h3 {
  color: #B89A6A; /* Your desired hover color */
}

.project-list-view .project-item h3 {
  font-size: 3.8rem;
  font-weight: 50;
  margin-bottom: 0.5rem;
  line-height: 1;
  color: #FFFBEB; /* Primary text */
  text-align: right;
  
  /* This part was perfect! It makes the color change smooth. */
  transition: color 0.3s ease;
}

.project-list-view .project-item h3 {
  font-size: 3.8rem;
  font-weight: 50;
  margin-bottom: 0.5rem;
  line-height: 1;
  color: #FFFBEB; /* Primary text */
  text-align: right;
  transition: color 0.3s ease;
}

.project-list-view .project-short-description {
  font-weight: 400;
  font-size: 0.9rem;
  color: #FFFBEB; /* Secondary text */
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
  animation: fadeIn 1s ease-in-out;

  max-width: 450px;
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 0;
}

.project-detail-view h2 {
  font-size: 3rem;
  margin-bottom: 0.5rem;
  color: #FFFBEB; /* Primary text */
  text-align: left;
}

.project-detail-view h3 {
  font-size: 1.2rem;
  margin-top: 2rem;
  margin-bottom: 0.8rem;
  color: #FFFBEB; /* Primary text */
  text-align: left;
}

.project-detail-view p {
  font-size: 0.9rem;
  line-height: 1.6;
  color: #FFFBEB; /* Secondary text */
  max-width: none;
  text-align: left;
}

.project-links ul {
  list-style: none;
  padding-left: 0;
  margin-top: 0.05rem;
  animation: fadeIn 1s ease-in-out;
}

.project-links li {
  margin-bottom: 0.5rem;
  text-align: left;
}

.project-links a {
  color: #FFFBEB; /* "The rest" */
  transition: opacity 0.2s ease;
}

.project-links a:hover {
  opacity: 0.8;
  color: #B89A6A;
   /* "The rest" */
}

.back-button {
  background: none;
  border: none;
  color: #FFFBEB; /* Primary text */
  font-size: 0.9rem;
  cursor: pointer;
  text-align: left;
  padding: 0;
  margin-bottom: 2rem;
  transition: color 1s ease;
}

.back-button:hover {
  color: #B89A6A; /* "The rest" */
}

/* NEW: Experience List View Styles */
.experience-list-view {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  text-align: left;

  max-width: 450px;
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 2000;
}

.experience-list-view .experience-item {
  padding-bottom: .5rem;
  cursor: pointer;
  transition: opacity 0.2s ease;
    /* Defines the animation that will be delayed */
  animation: fadeIn 0.5s ease-in-out;
  animation-fill-mode: forwards;
  
  /* Makes the items invisible before the animation starts */
  opacity: 0;

}

.experience-list-view .experience-item:last-child {
  border-bottom: none;
}

.experience-list-view .experience-item:hover h3 {
  
  opacity: 0.8;
  color: #B89A6A;
}

/* NEW: Big Titles for Experience List */
.experience-list-view .experience-item h3 {
  font-size: 3.80rem;
  font-weight: 50;
  margin-bottom: 0.5rem;
  line-height: 1;
  color: #FFFBEB; /* Primary text */
  text-align: right;
}

.experience-list-view .experience-company-duration {
  font-weight: 500;
  font-size: 1rem;
  color: #FFFBEB; /* Secondary text */
  margin-bottom: 0.5rem;
  text-align: right;
}

.experience-list-view .experience-short-description {
  font-weight: 400;
  font-size: 0.9rem;
  color: #B89A6A; /* Secondary text */
  line-height: 1.4;
  margin-bottom: 0;
  text-align: right;
}

/* NEW: Experience Detail View Styles */
.experience-detail-view {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  text-align: left;
  animation: fadeIn 1s ease-in-out;

  max-width: 450px;
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 0;
}

/* NEW: Big Title for Experience Detail */
.experience-detail-view h2 {
  font-size: 3rem;
  margin-bottom: 0.5rem;
  color: #FFFBEB; /* Primary text */
  text-align: left;
}

.experience-detail-view .experience-company-duration {
  font-weight: 450;
  font-size: 1.1rem;
  color: #B89A6A; /* Secondary text */
  margin-bottom: 0.0rem;
  text-align: left;
}

.experience-detail-view .experience-description ul {
  font-size: 1rem;
  line-height: 1.6;
  color: #FFFBEB; /* Secondary text */
  max-width: none;
  text-align: left;
}

.experience-detail-view .experience-description li {
  font-size: 0.9rem;
  line-height: 1.6;
  font-weight: 400;
  list-style-type: none; /* This removes the bullet point */
  padding-left: 0; 
  color: #FFFBEB; /* Primary text */
  margin-bottom: 0.5rem;
}

.experience-detail-view .experience-skills h3 {
  font-weight: 450;
  font-size: 1.1rem;
  color: #B89A6A; /* Primary text */
  margin-bottom: 0.5rem;
  text-align: left;
}

.experience-detail-view .experience-skills p {
  font-weight: 450;
  font-size: 0.9rem;
  font-weight: 400;
  line-height: 1.6;
  color: #FFFBEB; /* Secondary text */
  margin-bottom: 0;
}


/* About Styles */
.about-content {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  text-align: left;
  animation: fadeIn 1s ease-in-out;
  max-width: 400px;
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 0;
  
}
.about-content h3 {
  font-size: 3.8rem;
  font-weight: 50;
  margin-bottom: 0.5rem;
  line-height: 1;
  color: #FFFBEB; /* Primary text */
  text-align: left;
  margin-bottom: 1rem;
  
}

.about-content p {
  font-weight: 400;
  font-size: 0.9rem;
  color: #FFFBEB; /* Secondary text */
  line-height: 1.6;
  margin-bottom: 0;
  text-align: left;
}

.about-content p strong {
  color: #FFFBEB; /* Primary text */
  font-weight: 600;
  margin-top: 1rem;
}

/* Resume Download Link Styles */
.resume-download {
  display: inline-block;
  padding: 7px 10px;
  color: #B89A6A !important; /* "The rest" */
  text-decoration: none;
  border-radius: 10px;
  border: 3px solid #B89A6A; /* "The rest" */
  background-color: transparent;
  transition: all 0.2s ease;
  font-weight: 500;
  margin-top: 2rem;
}

/* This creates the TOP and LEFT border lines */
.container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 0;
  height: 0;
  box-sizing: border-box; /* Important for border calculations */
  
  /* The visible border style. Use your new accent color! */
  border-top: 1px solid #FFFBEB;
  border-left: 1px solid #FFFBEB;

  /* Apply the animation */
  animation: draw-border 1s ease-out forwards;
}

/* This creates the BOTTOM and RIGHT border lines */
.container::after {
  content: '';
  position: absolute;
  bottom: 0;
  right: 0;
  width: 0;
  height: 0;
  box-sizing: border-box;

  /* The visible border style */
  border-bottom: 1px solid #FFFBEB;
  border-right: 1px solid #FFFBEB;
  
  /* Apply the animation with a delay so it starts after the first two lines */
  animation: draw-border 1s ease-out 1s forwards;
}

.resume-download:hover {
  background-color: #222831;
  color: #222831; /* "The rest" */
  opacity: 1 !important;
  transform: translateY(-3px);
}



/* Contact Content Styles */
.contact-content.centered-links {
  display: flex;
  flex-direction: column;
  align-items: center;    /* This handles the HORIZONTAL centering */
  justify-content: center;  /* This new line handles the VERTICAL centering */
  height: 100%;             /* This is crucial, it gives the container full height */
  gap: 0.2rem;
  width: 100%;
}

/* Apply specific styles to the links for prominence and consistent formatting */
.contact-content.centered-links a {
  color: #FFFBEB; /* "The rest" */
  text-decoration: none;
  transition: opacity 01s ease;
  font-size: 0.9rem;
  font-weight: 500;
}

.contact-content.centered-links a:hover {
  opacity: 0.8;
  color: #B89A6A; 
  transform: translateY(-1px);/* "The rest" */
}

@keyframes draw-border {
  0% {
    width: 0;
    height: 0;
  }
  100% {
    width: 100%;
    height: 100%;
  }
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

.liminal-toggle-wrapper {
  margin-top: 0.2rem; /* Adds some space between the nav and the icon */
}

#liminal-toggle {
  color: #B89A6A; /* Sets the icon color to your Amber accent */
  cursor: pointer; /* Makes the mouse cursor a pointer on hover */
  transition: all 0.3s ease; /* Prepares it for hover animations */
}

/* A simple hover effect to show it's interactive */
#liminal-toggle:hover {
  opacity: 0.7;
}

/* --- Liminal Mode Easter Egg Styles --- */

/* 1. THE GLOBAL COLOR SHIFT
------------------------------------ */

/* Change all primary text to a fluorescent green */
.liminal-mode-active .left-column,
.liminal-mode-active .right-column,
.liminal-mode-active h1, .liminal-mode-active h2, .liminal-mode-active h3, .liminal-mode-active p,
.liminal-mode-active .back-button,
.liminal-mode-active .contact-content.centered-links a {
  color: #3D304C;
  transition: color 0.5s ease; /* Smooth color transition */
  
}

.liminal-mode-active .hero-section {
  background-color: #3D304C;
}

/* Change all accent/hover colors to a digital green */
.liminal-mode-active .nav-item:hover,
.liminal-mode-active .project-list-view .project-item:hover h3,
.liminal-mode-active .experience-list-view .experience-item:hover h3,
.liminal-mode-active .back-button:hover,
.liminal-mode-active .project-links a:hover,
.liminal-mode-active .contact-content.centered-links a:hover {
  color: #B2A4D4;
}

/* Change the animated border color */
.liminal-mode-active .container::before,
.liminal-mode-active .container::after {
  border-color: #B2A4D4;
  transition: border-color 0.5s ease;
}

/* Invert the resume button's hover state */
.liminal-mode-active .resume-download:hover {
  background-color: #B2A4D4; /* Fill with digital green */
  color: #1a2b20; /* Use a dark, eerie green for the text */
}


/* 2. THE ICON'S NEW STATE
------------------------------------ */

/* The icon itself glows green when Liminal Mode is on */
.liminal-mode-active #liminal-toggle {
  color: #B2A4D4;
  transform: rotate(45deg); /* Rotate it to an 'X' to signify it's active */
}

/* A more glitchy hover effect for the icon when active */
.liminal-mode-active #liminal-toggle:hover {
  opacity: 1;
  transform: rotate(45deg) scale(1.1);
}

/* --- LIMINAL MODE TEXT COLOR FIXES (V2 - More Specific) --- */

/* This specifically targets the titles in the project and experience lists */
.liminal-mode-active .project-list-view .project-item h3,
.liminal-mode-active .experience-list-view .experience-item h3 {
  color: #3D304C !important; /* Darkened Purple */
}

/* This handles the hover state for the titles in liminal mode */
.liminal-mode-active .project-list-view .project-item:hover h3,
.liminal-mode-active .experience-list-view .experience-item:hover h3 {
  color: #B2A4D4 !important; /* Royal Lavender on hover */
}

/* These are the other general text fixes for descriptions, nav, etc. */
.liminal-mode-active .nav-item,
.liminal-mode-active .nav-item.active,
.liminal-mode-active .project-short-description,
.liminal-mode-active .experience-short-description,
.liminal-mode-active .experience-company-duration,
.liminal-mode-active .large-text,
.liminal-mode-active .about-para,
.liminal-mode-active .project-detail-view p,
.liminal-mode-active .experience-description li,
.liminal-mode-active .experience-skills p {
  color: #3D304C;
}

/* And the nav hover state */
.liminal-mode-active .nav-item:hover {
  color: #B2A4D4;
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

  .project-list-view, .experience-list-view, .project-detail-view, .experience-detail-view {
    gap: 2rem;
    max-width: 100%;
    margin-left: 0;
    margin-right: 0;
  }

  .project-list-view .project-item, .experience-list-view .experience-item {
    padding-bottom: 1rem;
  }

  .project-detail-view h2, .experience-detail-view h2 {
    font-size: 1.8rem;
  }

  /* Ensure the full width layout on mobile also works for About */
  .two-column.about-full-layout {
      flex-direction: column;
      gap: 20px;
  }

  .two-column.about-full-layout .left-column,
  .two-column.about-full-layout .right-column {
      width: 100%;
      margin: 0;
  }

  /* Contact centering on mobile */
  .contact-content.centered-links {
    margin-left: 0;
    margin-top: 10%;
    align-items: center;
  }

  /* Resume and Education sections absolute positioning adjustments for mobile */
  .resume-section {
    position: static;
    top: unset;
    left: unset;
    transform: none;
    text-align: center;
    margin-top: 2rem;
    max-width: 100%;
  }

  .education-section {
    position: static;
    top: unset;
    left: unset;
    transform: none;
    text-align: center;
    margin-top: 2rem;
    max-width: 100%;
  }
}
</style>