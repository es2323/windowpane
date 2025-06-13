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
  methods: {
    sketch(p) {
      let particles = [];
      // Adjust particle count for screen size for performance
      const numParticles = window.innerWidth > 768 ? 120 : 40;
      const connectDistance = 120;

      // The Particle class is defined inside the sketch to have access to 'p'
      class Particle {
        constructor() {
          this.pos = p.createVector(p.random(p.width), p.random(p.height));
          this.vel = p.createVector(p.random(-0.5, 0.5), p.random(-0.5, 0.5));
          this.size = 2;
        }

        update() {
          this.pos.add(this.vel);
          this.edges();
        }

        draw() {
          p.noStroke();
          // Use the prop passed from the parent component
          p.fill(this.particleColor);
          p.circle(this.pos.x, this.pos.y, this.size);
        }

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
        
        // Connect particles to each other
        for (let i = 0; i < particles.length; i++) {
          for (let j = i + 1; j < particles.length; j++) {
            const d = p.dist(particles[i].pos.x, particles[i].pos.y, particles[j].pos.x, particles[j].pos.y);
            if (d < connectDistance) {
              const alpha = p.map(d, 0, connectDistance, 255, 0);
              const lineColorWithAlpha = p.color(this.lineColor);
              lineColorWithAlpha.setAlpha(alpha);
              p.stroke(lineColorWithAlpha);
              p.line(particles[i].pos.x, particles[i].pos.y, particles[j].pos.x, particles[j].pos.y);
            }
          }
        }

        // Connect particles to the mouse
        for (let particle of particles) {
            const d = p.dist(p.mouseX, p.mouseY, particle.pos.x, particle.pos.y);
            if (d < connectDistance + 30) { // Slightly larger radius for mouse
              const alpha = p.map(d, 0, connectDistance + 30, 200, 0);
              const lineColorWithAlpha = p.color(this.lineColor);
              lineColorWithAlpha.setAlpha(alpha);
              p.stroke(lineColorWithAlpha);
              p.line(p.mouseX, p.mouseY, particle.pos.x, particle.pos.y);
            }
        }
      };

      // Handle window resize
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