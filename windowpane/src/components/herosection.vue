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
              <p v-html="selectedProject.longDescription"></p>
              
              <div v-if="selectedProject.links && selectedProject.links.length > 0" class="project-links">
                <ul>
                  <li v-for="(link, index) in selectedProject.links.filter(l => l.type === 'GitHub')" :key="index">
                    <a :href="link.url" target="_blank">GitHub</a>
                  </li>
                </ul>
              </div>

              </div>
          </div>
          <div v-if="activeSection === 'experience'" class="content-section fade-in visible">
            <div v-if="!selectedExperience" class="experience-list-view">
              <div class="experience-item" v-for="exp in experiences" :key="exp.id" @click="showExperienceDetails(exp)">
                <h3>{{ exp.title }}</h3>
                <p class="experience-company-duration">{{ exp.company }} | {{ exp.duration }}</p>
                <p class="experience-short-description">{{ exp.shortDescription }}</p>
              </div>
            </div>

            <div v-else class="experience-detail-view">
              <button class="back-button" @click="backToExperienceList()">
                &larr; Back to Experience
              </button>
              <h2>{{ selectedExperience.title }}</h2>
              <p class="experience-company-duration">{{ selectedExperience.company }} | {{ selectedExperience.duration }}</p>
              
              <div class="experience-description">
                <ul>
                  <li v-for="(point, index) in selectedExperience.longDescription" :key="index">{{ point }}</li>
                </ul>
              </div>

              <div v-if="selectedExperience.skills && selectedExperience.skills.length > 0" class="experience-skills">
                <h3>Skills</h3>
                <p>{{ selectedExperience.skills.join(', ') }}</p>
              </div>
            </div>
          </div>

          <div v-if="activeSection === 'about'" class="content-section fade-in visible">
            <div class="about-content">
              <h3>Beyond the Code</h3>
              <p>
                Hi! I'm Enosh, a Computer Science student and AI enthusiast based in the rocky midlands of the UK. With a passion for computational mathematics, I specialize in crafting intelligent applications, focusing on backend development, intuitive UI/UX design, and robust database solutions, all whilst drawing on my experience across digital content creation and performance marketing.              </p>
              <p>
                When I'm not immersed in code, you'll find me captivated by the intriguing aesthetics of liminal spaces, exploring the hidden corners of new cities, or unwinding to the smooth rhythms of jazz. I thrive on learning, building, and engaging with fellow innovators and curious minds.              </p>
            </div>

              <div class="resume-section">
                <p>
                  <a href="/Enosh_Earnest_Resume.pdf" download="Enosh_Earnest_Resume.pdf" class="resume-download">
                    Download My Resume!
                  </a>
                </p>
              </div>

            <!-- Separate Education section positioned at center bottom -->
              <div class="education-section">
                <h3>Education</h3>
                <p>
                  <strong>University of Derby</strong><br>
                  BSc (Honours) in Computer Science<br>Expected: Sep 2026<br>    
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
      selectedExperience: null, // NEW: Holds the currently selected experience for detail view


      projects: [
        {
          id: 'seec',
          title: "SEEC/ May 25'",
          shortDescription: 'Public Transport app for the visually impaired (Made for Journeo)',
          longDescription: 'A Public Transport App for the Visually Impaired.<br><br>SEEC is a voice-controlled mobile application built for Journeo Plc using React Native (Expo), Node.js, and Express.js. It seamlessly integrates Google Maps/Directions API and real-time location tracking via Expo Location, achieving a remarkable 95% accuracy in route generation and 90% adherence to turn-by-turn guidance. The app also features an advanced image-to-text capability using Google Vision API, providing 98% OCR accuracy to convert physical signs into audible formats. User acceptance testing demonstrated a 30% improvement in ease of following transit instructions and a 25% reduction in reported navigational anxiety, thanks to its dynamic voice feedback system.',
          links: [
            { type: 'GitHub', url: 'https://github.com/es2323/SEEC' } // Placeholder
          ]
        },
        {
          id: 'snapback',
          title: "SnapBack/ May 25'",
          shortDescription: 'Web app tracking employee fatigue via cognitive games and wellness surveys',
          longDescription: 'An Employee Fatigue Monitoring Platform.<br><br>Uncover the power of real-time insights with SnapBack, developed with Python Flask and SQLite. This innovative, role-based web app features distinct dashboards for employees, managers, and HR, integrating fatigue scoring from 4 engaging cognitive games (engineered using Pygame) and daily wellness surveys. It accurately tracks real-time fatigue for 25+ users across 3 teams, logging over 500+ session metrics like reaction time and accuracy. Managers gain immediate insights with Chart.js analytics, offering dynamic SQL joins and threshold-based alerts, all with dashboard render times under 150 ms and 100% session log retention.',
          links: [
            { type: 'GitHub', url: 'https://github.com/es2323/SnapBack' } // Placeholder
          ]
        },
        {
          id: 'prs',
          title: "PRS/ May 25'",
          shortDescription: 'Web platform for pandemic data management',
          longDescription: 'Web Platform for pandemic data management.<br><br>Dive into a world where public safety meets cutting-edge technology. This secure, role-based web platform, meticulously engineered with Python Flask, leverages a hybrid data architecture combining SQL Server for compliance-critical data and MongoDB Atlas for dynamic, semi-structured information. With over 20+ endpoints and 3 intuitive dashboards, it powers 500+ dynamic data operations across structured and unstructured sources, all while maintaining sub-100 ms query response times under load. It boasts 100% password encryption compliance using PBKDF2 via Werkzeug and significantly boosts error handling and data consistency by approximately 80%, ensuring robust pandemic response management.',          links: [
            { type: 'GitHub', url: 'https://github.com/enosh-earnest/prs' }, 
            
          ]
        },
        {
          id: 'ssh',
          title: "SSH/ Dec 24'",
          shortDescription: 'Secure client-server system for smart home communication',
          longDescription: 'Secure Smart Home Client-Server System.<br><br>Experience the next generation of secure smart home connectivity with this high-performance client-server system built with Python, asyncio, and SQLite. Engineered for robust communication, it utilizes AES-CBC encryption and Diffie-Hellman key exchange, handling 10+ concurrent clients and encrypting 500+ messages with zero errors. Advanced features like 30-second idle disconnection and a heartbeat mechanism ensure 98% reliability in maintaining active client-server communication, even under extensive testing, processing over 100 client requests per second with 99.9% accuracy during 48-hour stress tests.',
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
      "duration": "Mar 2024 – July 2024",
      "shortDescription": "Created digital content templates, optimized CRM processes, and managed databases to enhance operational efficiency.",
      "longDescription": [
        "Created an average of 13 new digital content templates for various platforms (newsletters, chats, LinkedIn feeds, presentations), significantly streamlining future content creation efforts.",
        "Optimized CRM records for up to 400 individuals, enhancing data organization and efficiency for smoother client management processes.",
        "Refined and updated 8 databases to ensure accuracy, consistency, and data normalization, improving user-friendliness, accessibility options, and encryption."
      ],
      "skills": [
        "Digital Content Design/",
        "Template Creation",
        "Content Creation",
        "Database Management",
        "CRM Optimization",
        "Data Normalization",
        "Process Efficiency",
        "DaVinci Resolve",
        "Canva",
        "MS Excel",
        "Microsoft Dynamics 365"
      ]
    },
        {
          id: 'marketing-intern',
          title: 'Marketing Intern',
          company: 'Not Another Agency',
          duration: 'Jan 2023 – June 2023',
          shortDescription: 'Managed social media presence, optimized performance marketing, and analyzed ad campaign performance for diverse clients.',
          longDescription: [
        "Managed social media presence for up to 6 organizations across various platforms (Facebook, Instagram, Twitter, LinkedIn, YouTube, TikTok), including an NGO focused on postpartum depression.",
        "Achieved a 30% increase in follower count for a luxury villa through strategic content creation and targeted campaigns.",
        "Curated a 3x increase in ad frequency for an NGO dedicated to under-privileged youth, significantly boosting engagement and helping the organization reach a wider, more relevant audience."
      ],
          skills: ['Marketing Strategy', 'Market Research', 'Social Media Management', 'Campaign Management', 'Content Creation']
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
    }
  }
}
</script>

<style scoped>
/* --- Hero Section Specific Styles --- */
.hero-section {
  min-height: 100vh;
  background-color: #161616;
  display: flex;
  align-items: center;
  padding: 20px;
  box-sizing: border-box;
}

.container {
  display: flex;
  flex-grow: 1;
  width: 100%;
  background-color: #000000;
  border: 1px solid #acacac;
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
  color: #ffffff;
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
  position: relative; 
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
  font-weight: 50;
  margin-bottom: 0.5rem;
  line-height: 1;
  color: #f0f0f0;
  text-align: right;
}

.project-list-view .project-short-description {
  font-weight: 400;
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
  font-size: 3rem;
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
  font-size: 0.9rem;
  line-height: 1.6;
  color: #aaa;
  max-width: none;
  text-align: left;
}

.project-links ul {
  list-style: none;
  padding-left: 0;
  margin-top: 0.05rem;
}

.project-links li {
  margin-bottom: 0.5rem;
  text-align: left;
}

.project-links a {
  color: #3058f5;
  transition: opacity 0.2s ease;
}

.project-links a:hover {
  opacity: 0.8;
  color: white;
}

.back-button {
  background: none;
  border: none;
  color: #ffffff;
  font-size: 0.9rem;
  cursor: pointer;
  text-align: left;
  padding: 0;
  margin-bottom: 2rem;
  transition: color 0.2s ease;
}

.back-button:hover {
  color: white;
}


/* NEW: Experience List View Styles */
.experience-list-view {
  display: flex;
  flex-direction: column;
  gap: 2.5rem; /* Space between experience items */
  text-align: left;

  /* Positioning: Same as projects to be "center right" */
  max-width: 450px; /* Constrain width */
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 2000;
}

.experience-list-view .experience-item {
  padding-bottom: .5rem;
  cursor: pointer;
  transition: opacity 0.2s ease;
}

.experience-list-view .experience-item:last-child {
  border-bottom: none;
}

.experience-list-view .experience-item:hover {
  opacity: 0.7;
}

/* NEW: Big Titles for Experience List */
.experience-list-view .experience-item h3 {
  font-size: 3.80rem; /* Larger font size for main titles */
  font-weight: 50;
  margin-bottom: 0.5rem;
  line-height: 1;
  color: #f0f0f0;
  text-align: right;
}

.experience-list-view .experience-company-duration {
  font-weight: 500;
  font-size: 1rem;
  color: #ffffff;
  margin-bottom: 0.5rem;
  text-align: right;
}

.experience-list-view .experience-short-description {
  font-weight: 400;
  font-size: 0.9rem;
  color: #ffffff;
  line-height: 1.4;
  margin-bottom: 0;
  text-align: right;
}

/* NEW: Experience Detail View Styles */
.experience-detail-view {
  display: flex;
  flex-direction: column;
  gap: 1.5rem; /* Spacing between elements in detail view */
  text-align: left;

  /* Positioning: Same as projects to be "center right" */
  max-width: 450px; /* Apply similar width constraint */
  margin-top: auto;
  margin-bottom: auto;
  margin-left: auto;
  margin-right: 0;
}

/* NEW: Big Title for Experience Detail */
.experience-detail-view h2 {
  font-size: 3rem;
  margin-bottom: 0.5rem;
  color: #f0f0f0;
  text-align: left;
}

.experience-detail-view .experience-company-duration {
  font-weight: 450;
  font-size: 1.2rem;
  color: #ffffff;
  margin-bottom: 0.05rem;
  text-align: left;
}

.experience-detail-view .experience-description ul {
  font-size: 1rem;
  line-height: 1.6;
  color: #aaa;
  max-width: none;
  text-align: left;
}

.experience-detail-view .experience-description li {
  font-weight: 600;
  font-size: 0.85rem;
  line-height: 1.6;
  color: #ffffff;
  margin-bottom: 0.5rem;
}

.experience-detail-view .experience-skills h3 {
  font-weight: 450;
  font-size: 1.2rem;
  color: #ffffff;
  margin-bottom: 0.5rem;
  text-align: left;
}

.experience-detail-view .experience-skills p {
  font-weight: 450;
  font-size: 0.85rem;
  line-height: 1.6;
  color: #ffffff;
  margin-bottom: 0;
}


/* About Styles */
.about-content {
  max-width: 600px;
  margin-top: auto;
  margin-bottom: 10;
  margin-left: 200;
  margin-right: 100;
  text-align: left;
}
.about-content h3 {
  font-size: 2.0rem; /* Larger font size for main titles */
  font-weight: 50;
  margin-bottom: 0.5rem;
  margin-top: 2rem;
  line-height: 1;
  color: #f0f0f0;
  text-align: left;
}


.about-content h3:first-child {
  margin-top: 0;
}

.about-content p {
  font-size: 0.9rem;
  line-height: 1.6;
  color: #ffffff;
  margin-bottom: 1.5rem;
}

.about-content p strong {
  color: #ffffff;
  font-weight: 600;
}

/* Resume Download Link Styles */
.resume-download {
  display: inline-block;
  padding: 7px 10px;
  background-color: #8a8383;
  color: white !important;
  text-decoration: none;
  border-radius: 10px;
  border-color: #f0f0f0;
  transition: all 0.2s ease;
  font-weight: 500;
}

.resume-download:hover {
  background-color: #4068ff;
  opacity: 1 !important;
  transform: translateY(-1px);
}

/* NEW: Resume section positioned at center */
.resume-section {
  position: absolute;
  top: 35%;
  left: 82%;
  transform: translateX(-50%);
  text-align: left;
  max-width: 400px;
}


.resume-section p {
  font-size: 0.9rem;
  line-height: 1.6;
  color: #aaa; /* Or #ffffff if preferred for the download link context */
  margin-bottom: 0;
  text-align: left;
}


/* Education section positioned at center bottom */
.education-section {
  position: absolute;
  top: 1%;
  left: 55%;
  transform: translate(-50%, -50%); /* Centering trick */
  text-align: left;
  max-width: 300px; /* Adjust as needed */
}

.education-section h3 {
  font-size: 2.0rem; /* Larger font size for main titles */
  font-weight: 50;
  margin-bottom: 0.5rem;
  margin-top: 2rem;
  line-height: 1;
  color: #f0f0f0;
  text-align: left;
}

.education-section p {
  font-size: 0.9rem;
  line-height: 1.6;
  color: #aaa;
  margin-bottom: 0;
}

.education-section p strong {
  color: #ffffff;
  font-weight: 600;
}

/* Contact Content Styles */
.contact-content h3 {
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 0.8rem;
  margin-top: 2rem;
  color: #f0f0f0;
  text-align: left;
}

.contact-content h3:first-child {
  margin-top: 0;
}

.contact-content p {
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  max-width: none;
  color: #aaa;
  text-align: left;
}

/*Contact Section Styling */
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

  .project-list-view, .experience-list-view, .project-detail-view, .experience-detail-view {
    gap: 2rem;
    max-width: 100%; /* Ensure it takes full width on mobile */
    margin-left: 0;
    margin-right: 0;
  }

  .project-list-view .project-item, .experience-list-view .experience-item {
    padding-bottom: 1rem;
  }

  .project-detail-view h2, .experience-detail-view h2 {
    font-size: 1.8rem;
  }
}
</style>