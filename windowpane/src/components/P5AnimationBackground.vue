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

    p.draw = () => {
      p.background(this.backgroundColor);

      for (let particle of particles) {
        particle.update();
        particle.draw();
      }
      
      for (let i = 0; i < particles.length; i++) {
        for (let j = i + 1; j < particles.length; j++) {
          
          // --- OPTIMIZATION 2: Use squared distance to avoid slow square roots ---
          const dx = particles[i].pos.x - particles[j].pos.x;
          const dy = particles[i].pos.y - particles[j].pos.y;
          const d_squared = dx * dx + dy * dy;

          if (d_squared < connectDistance_squared) {
            const d = Math.sqrt(d_squared); // Only calculate sqrt when we absolutely need it
            const alpha = p.map(d, 0, connectDistance, 255, 0);
            const lineColorWithAlpha = p.color(this.lineColor);
            lineColorWithAlpha.setAlpha(alpha);
            p.strokeWeight(0.2);
            p.stroke(lineColorWithAlpha);
            p.line(particles[i].pos.x, particles[i].pos.y, particles[j].pos.x, particles[j].pos.y);
          }
        }
      }
      // The mouse connection part is already efficient enough and doesn't need changes.
      for (let particle of particles) {
          const d = p.dist(p.mouseX, p.mouseY, particle.pos.x, particle.pos.y);
          if (d < connectDistance + 20) {
            const alpha = p.map(d, 0, connectDistance + 30, 200, 0);
            const lineColorWithAlpha = p.color(this.lineColor);
            lineColorWithAlpha.setAlpha(alpha);
            p.strokeWeight(0.2);
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
  z-index: 0; /* Changed from -1 to 0, ensure hero-section content has z-index: 1 */
}
</style>