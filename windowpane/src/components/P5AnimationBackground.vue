<template>
  <div ref="canvasContainer" class="p5-canvas-container"></div>
</template>

<script>
import p5 from 'p5';

export default {
  name: 'P5AnimationBackground',
  props: {
    backgroundColor: {
      type: String,
      default: '#000000'
    },
    particleColor: {
      type: String,
      default: '#FFFFFF'
    },
    lineColor: {
      type: String,
      default: '#FFFFFF'
    }
  },
  data() {
    return {
      p5Instance: null,
    };
  },
  mounted() {
    this.p5Instance = new p5(this.sketch, this.$refs.canvasContainer);
  },
  beforeUnmount() {
    this.p5Instance.remove();
  },
// In P5AnimationBackground.vue
methods: {
  sketch(p) {
    let particles = [];
    
    // --- OPTIMIZATION 1: Reduced particle count ---
    const numParticles = window.innerWidth > 768 ? 110 : 30;
    const connectDistance = 150;
    const connectDistance_squared = connectDistance * connectDistance; // Pre-calculate this

    class Particle {
      constructor() {
        this.pos = p.createVector(p.random(p.width), p.random(p.height));
        this.vel = p.createVector(p.random(-0.4, 0.4), p.random(-0.4, 0.4));
        this.size = 0.5;
      }
      update() { this.pos.add(this.vel); this.edges(); }
      draw() { p.noStroke(); p.fill(this.particleColor); p.circle(this.pos.x, this.pos.y, this.size); }
      edges() {
        if (this.pos.x < 0) this.pos.x = p.width;
        if (this.pos.x > p.width) this.pos.x = 0;
        if (this.pos.y < 0) this.pos.y = p.height;
        if (this.pos.y > p.height) this.pos.y = 0;
      }
    }

    p.setup = () => {
      const container = this.$refs.canvasContainer;
      p.createCanvas(container.clientWidth, container.clientHeight);
      
      // --- OPTIMIZATION 3: Set a stable frame rate ---
      p.frameRate(30); 
      
      for (let i = 0; i < numParticles; i++) {
        particles.push(new Particle());
      }
    };

    // This is inside the sketch(p) method in P5AnimationBackground.vue

p.draw = () => {
  // Check if Liminal Mode is active on every frame
  const isLiminal = document.body.classList.contains('liminal-mode-active');

  // --- 1. Set the Background ---
  if (isLiminal) {
    // In Liminal Mode, use a semi-transparent background for a "ghosting" tracer effect
    p.background (255, 251, 235); // Dark Charcoal with some transparency
  } else {
    // In normal mode, use the solid background color prop
    p.background(this.backgroundColor);
  }

  // --- 2. Set the Particle and Line Colors ---
  let particleColorToUse = this.particleColor;
  let lineColorToUse = this.lineColor;

  if (isLiminal) {
    // In Liminal Mode, override with fluorescent/digital green colors
    particleColorToUse = '#FFFBEB'; // Fluorescent Green for particles
    lineColorToUse = '#B2A4D4';     // Digital Green for lines
  }
  
  // Update and draw all particles (no changes needed here)
  for (let particle of particles) {
    particle.update();
    // We now pass the correct color into the draw method
    p.noStroke();
    p.fill(particleColorToUse);
    p.circle(particle.pos.x, particle.pos.y, particle.size);
  }
  
  // Connect particles to each other (no changes needed in the logic)
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].pos.x - particles[j].pos.x;
      const dy = particles[i].pos.y - particles[j].pos.y;
      const d_squared = dx * dx + dy * dy;

      if (d_squared < connectDistance_squared) {
        const d = Math.sqrt(d_squared);
        const alpha = p.map(d, 0, connectDistance, 255, 0);
        
        // We now use the correct color variable here
        const lineColorWithAlpha = p.color(lineColorToUse);
        lineColorWithAlpha.setAlpha(alpha);
              if (isLiminal) {
            p.strokeWeight(1.5); // <-- Use a thicker line in Liminal Mode
          } else {
            p.strokeWeight(0.2); // <-- Keep the thin line in normal mode
          }
        p.stroke(lineColorWithAlpha);
        p.line(particles[i].pos.x, particles[i].pos.y, particles[j].pos.x, particles[j].pos.y);
      }
    }
  }

  // The mouse connection part also needs to use the correct line color
  for (let particle of particles) {
      const d = p.dist(p.mouseX, p.mouseY, particle.pos.x, particle.pos.y);
      if (d < connectDistance + 30) {
        const alpha = p.map(d, 0, connectDistance + 30, 200, 0);

        // And here...
        const lineColorWithAlpha = p.color(lineColorToUse);
        lineColorWithAlpha.setAlpha(alpha);
        if (isLiminal) {
            p.strokeWeight(1); // <-- Use a thicker line in Liminal Mode
          } else {
            p.strokeWeight(0.2); // <-- Keep the thin line in normal mode
          }
        p.stroke(lineColorWithAlpha);
        p.line(p.mouseX, p.mouseY, particle.pos.x, particle.pos.y);
      }
  }
};

    p.windowResized = () => {
      const container = this.$refs.canvasContainer;
      p.resizeCanvas(container.clientWidth, container.clientHeight);
    };
  }
}
}
</script>

<style scoped>
.p5-canvas-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0; 
  .p5-canvas-container {
  transition: filter 1s ease-in-out;
}/* Changed from -1 to 0, ensure hero-section content has z-index: 1 */
}
</style>