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
      // This array will hold our wave objects. It's declared at the top level.
      let waves = [];

      // This class defines a single, undulating wave layer.
      class Wave {
        constructor(y, amplitude, period, speed) {
          this.y = y;
          this.amplitude = amplitude;
          this.period = period;
          this.speed = speed;
          this.phase = p.random(p.TWO_PI);
          this.swell_phase = p.random(p.TWO_PI);
          this.swell_speed = p.random(0.007, 0.03);
          this.swell_amplitude = p.random(5, 30);
        }

        update() {
          this.phase += this.speed;
          this.swell_phase += this.swell_speed;
        }

        draw(waveColor) {
          let y_offset = p.sin(this.swell_phase) * this.swell_amplitude;
          p.beginShape();
          p.noStroke();
          p.fill(waveColor);
          p.vertex(0, p.height);
          for (let x = 0; x <= p.width; x += 10) {
            let angle = this.phase + (x / this.period) * p.TWO_PI;
            let waveY = this.y + y_offset + p.sin(angle) * this.amplitude;
            p.vertex(x, waveY);
          }
          p.vertex(p.width, p.height);
          p.endShape(p.CLOSE);
        }
      }

      // SETUP runs once at the start.
      p.setup = () => {
        const container = this.$refs.canvasContainer;
        p.createCanvas(container.clientWidth, container.clientHeight);
        p.frameRate(30);

        waves = []; // Clear the array just in case

        const waveCount = 3;
        for (let i = 0; i < waveCount; i++) {
          let y = p.height - p.height * 0.12 + (i * 20);
          let amplitude = p.random(15, 8);
          let period = p.random(500, 500);
          let speed = p.random(0.02, 0.02);
          waves.push(new Wave(y, amplitude, period, speed));
        }
      };

      // DRAW runs on every frame.
      p.draw = () => {
        const isLiminal = document.body.classList.contains('liminal-mode-active');

        if (isLiminal) {
          p.background(255, 251, 235); // Liminal: Light Cream
        } else {
          p.background(this.backgroundColor); // Default: Dark Charcoal
        }

        const defaultColors = ['#205781FF', '#4F959D', '#98D2C0'];
        const liminalColors = ['#B2A4D455', '#B2A4D488', '#B2A4D4'];

        for (let i = 0; i < waves.length; i++) {
          waves[i].update();
          let colorToUse = isLiminal ? liminalColors[i] : defaultColors[i];
          waves[i].draw(colorToUse);
        }
      };

      // WINDOWRESIZED runs when the browser window changes size.
      p.windowResized = () => {
        const container = this.$refs.canvasContainer;
        p.resizeCanvas(container.clientWidth, container.clientHeight);
        // We re-run setup to recalculate wave positions for the new size
        p.setup();
      };
    }
  }

// ... don't forget the closing brace for the export default
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