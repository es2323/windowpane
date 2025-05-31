<template>
  <section id="hero" class="hero-section">
    <div class="hero-container">
      <div class="hero-content">
        <div class="hero-intro">
          <h1 class="hero-title">
            <span class="title-line">born in</span>
            <span class="title-line highlight">{{ currentYear - 2003 }}</span>
            <span class="title-line">years old</span>
            <span class="title-line">in india.</span>
          </h1>
        </div>
        
        <div class="hero-statement">
          <p class="statement-text">
            i believe
            <br />
            <strong>code can be more</strong>
            <br />
            <strong>creative and impactful.</strong>
          </p>
          
          <p class="mission-text">
            with a mission
            <br />
            to present
            <br />
            the possibilities
            <br />
            of web development,
            <br />
            i am pursuing
            <br />
            new expressions
            <br />
            through experiments
            <br />
            and learning.
          </p>
        </div>
      </div>

      <div class="hero-visual">
        <div class="floating-elements">
          <div class="element element-1"></div>
          <div class="element element-2"></div>
          <div class="element element-3"></div>
          <div class="element element-4"></div>
        </div>
      </div>
    </div>

    <div class="scroll-indicator">
      <div class="scroll-line"></div>
      <span class="scroll-text">scroll</span>
    </div>
  </section>
</template>

<script>
export default {
  name: 'herosection',
  data() {
    return {
      currentYear: new Date().getFullYear()
    }
  },
  mounted() {
    this.animateElements()
  },
  methods: {
    animateElements() {
      const elements = document.querySelectorAll('.element')
      elements.forEach((el, index) => {
        el.style.animationDelay = `${index * 0.5}s`
      })
    }
  }
}
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding: 6rem 0 4rem;
  background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
  overflow: hidden;
}

.hero-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.hero-content {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.hero-title {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 300;
  line-height: 1.1;
  color: #2c3e50;
}

.title-line {
  display: block;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease-out forwards;
}

.title-line:nth-child(1) { animation-delay: 0.1s; }
.title-line:nth-child(2) { animation-delay: 0.2s; }
.title-line:nth-child(3) { animation-delay: 0.3s; }
.title-line:nth-child(4) { animation-delay: 0.4s; }

.highlight {
  font-weight: 700;
  color: #3498db;
}

.hero-statement {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.statement-text {
  font-size: clamp(1.2rem, 3vw, 1.5rem);
  line-height: 1.4;
  color: #2c3e50;
  opacity: 0;
  transform: translateY(20px);
  animation: fadeInUp 0.8s ease-out 0.5s forwards;
}

.mission-text {
  font-size: 1rem;
  line-height: 1.6;
  color: #6c757d;
  opacity: 0;
  transform: translateY(20px);
  animation: fadeInUp 0.8s ease-out 0.7s forwards;
}

.hero-visual {
  position: relative;
  height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.floating-elements {
  position: relative;
  width: 100%;
  height: 100%;
}

.element {
  position: absolute;
  border-radius: 50%;
  opacity: 0;
  animation: float 6s ease-in-out infinite, fadeIn 1s ease-out forwards;
}

.element-1 {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, #3498db, #2980b9);
  top: 20%;
  left: 20%;
  animation-delay: 0s;
}

.element-2 {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #e74c3c, #c0392b);
  top: 60%;
  right: 30%;
  animation-delay: 1s;
}

.element-3 {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #f39c12, #e67e22);
  bottom: 30%;
  left: 10%;
  animation-delay: 2s;
}

.element-4 {
  width: 100px;
  height: 100px;
  background: linear-gradient(135deg, #9b59b6, #8e44ad);
  top: 10%;
  right: 10%;
  animation-delay: 3s;
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  opacity: 0;
  animation: fadeIn 1s ease-out 1.5s forwards;
}

.scroll-line {
  width: 1px;
  height: 30px;
  background: #6c757d;
  animation: scrollLine 2s ease-in-out infinite;
}

.scroll-text {
  font-size: 0.8rem;
  color: #6c757d;
  font-weight: 500;
  letter-spacing: 2px;
  text-transform: uppercase;
}

/* animations */
@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  25% {
    transform: translateY(-10px) rotate(5deg);
  }
  50% {
    transform: translateY(-20px) rotate(0deg);
  }
  75% {
    transform: translateY(-10px) rotate(-5deg);
  }
}

@keyframes scrollLine {
  0% {
    transform: scaleY(0);
    transform-origin: top;
  }
  50% {
    transform: scaleY(1);
    transform-origin: top;
  }
  100% {
    transform: scaleY(0);
    transform-origin: bottom;
  }
}

/* responsive */
@media (max-width: 968px) {
  .hero-container {
    grid-template-columns: 1fr;
    gap: 2rem;
    text-align: center;
  }
  
  .hero-visual {
    height: 300px;
  }
}

@media (max-width: 768px) {
  .hero-section {
    padding: 5rem 0 3rem;
  }
  
  .hero-container {
    padding: 0 1rem;
  }
  
  .hero-visual {
    height: 200px;
  }
  
  .element-1 { width: 60px; height: 60px; }
  .element-2 { width: 45px; height: 45px; }
  .element-3 { width: 30px; height: 30px; }
  .element-4 { width: 75px; height: 75px; }
}
</style>