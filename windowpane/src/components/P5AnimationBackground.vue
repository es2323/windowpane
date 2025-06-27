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
      default: '#222831'
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
// This is the entire 'methods' object. Replace your old one with this.
methods: {
  sketch(p) {
    // Capture the Vue component's 'this' context to use in the sketch
    const vm = this;
    
    let waves = [];
    let fish;

    // --- CLASS DEFINITIONS ---

    class Wave {
      constructor(y, amplitude, period, speed) {
        this.y = y;
        this.original_y = y;
        this.target_y = y;
        this.amplitude = amplitude;
        this.original_amplitude = amplitude;
        this.period = period;
        this.speed = speed;
        this.phase = p.random(p.TWO_PI);
        this.swell_phase = p.random(p.TWO_PI);
        this.swell_speed = p.random(0.007, 0.03);
        this.original_swell_amplitude = p.random(5, 10);
        this.swell_amplitude = this.original_swell_amplitude;
      }

      update(isLiminal) {
        this.phase += this.speed;
        this.swell_phase += this.swell_speed;

        let targetY;
        if (isLiminal) {
          targetY = (p.height - this.original_y) + 150;
        } else {
          targetY = this.original_y;
        }
        
        this.y = p.lerp(this.y, targetY, 0.03);

        if (Math.abs(this.y - targetY) < 0.5) {
          this.y = targetY;
        }
        
        let targetSwellAmplitude;
        if (isLiminal) {
          targetSwellAmplitude = this.original_swell_amplitude * 7.5;
        } else {
          targetSwellAmplitude = this.original_swell_amplitude;
        }
        this.swell_amplitude = p.lerp(this.swell_amplitude, targetSwellAmplitude, 0.03);
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

    class Fish {
      constructor() {
        this.x = -50;
        this.y = p.random(p.height * 0.75, p.height * 0.9);
        this.speed = p.random(1, 2.5);
        this.size = 15;
      }
      update() {
        this.x += this.speed;
        if (this.x > p.width + 50) {
          this.x = -50;
          this.y = p.random(p.height * 0.7, p.height * 0.9);
          this.speed = p.random(1, 2.5);
        }
      }
      draw(fishColor) {
        p.push();
        p.translate(this.x, this.y);
        
          // --- NEW DRAWING LOGIC ---
  p.noFill();                 // IMPORTANT: We are not filling a shape.
  p.stroke(fishColor);      // Instead, we are tracing the lines with color.
  p.strokeWeight(2);        // This controls the thickness of the fish's outline.
  p.strokeCap(p.ROUND);     // Makes the line ends look softer.

  const fishWidth = this.size * 2.5;
  const fishHeight = this.size * 2;
  // This offset is the key to making the arcs cross and form a tail
  const verticalOffset = this.size * 0.15;

  // Draw the top arc, with its center slightly BELOW the midline
  p.arc(
    0, verticalOffset, 
    fishWidth, fishHeight, 
    -p.PI + 0.4, -0.4  // Start and stop angles
  );
  
  // Draw the bottom arc, with its center slightly ABOVE the midline
  p.arc(
    0, -verticalOffset,
    fishWidth, fishHeight,
    0.4, p.PI - 0.4  // Start and stop angles                  // Anchor point 2 (tail)
  );
  // --- END OF NEW LOGIC ---

  p.pop();
      }
    }

    // --- P5.JS MAIN FUNCTIONS ---

    p.setup = () => {
      const container = vm.$refs.canvasContainer;
      p.createCanvas(container.clientWidth, container.clientHeight);
      p.frameRate(30);

      waves = [];
      const waveCount = 3;
      for (let i = 0; i < waveCount; i++) {
        let y = p.height - p.height * 0.12 + (i * 20);
        let amplitude = p.random(8, 15);
        let period = p.random(500, 500);
        let speed = p.random(0.02, 0.02);
        waves.push(new Wave(y, amplitude, period, speed));
      }
      fish = new Fish();
    };

    p.draw = () => {
      const isLiminal = document.body.classList.contains('liminal-mode-active');

      if (isLiminal) {
        p.background(1, 22, 39);
      } else {
        p.background(vm.backgroundColor);
      }

      const defaultColors = ['#205781', '#4F959D', '#98D2C0'];
      const underwaterColors = ['#8E7DBE', '#A5158C', '#090040'];

      // WAVE ANIMATION
      for (let i = 0; i < waves.length; i++) {
        let wave = waves[i];
        wave.update(isLiminal);
        let topTargetY = (p.height - wave.original_y) + 150;
        let progress = p.map(wave.y, wave.original_y, topTargetY, 0, 1, true);
        let fromColor = p.color(defaultColors[i]);
        let toColor = p.color(underwaterColors[i]);
        let blendedColor = p.lerpColor(fromColor, toColor, progress);
        wave.draw(blendedColor);
      }
      
      // FISH ANIMATION
      fish.update();
      let fishColor = isLiminal ? '#B2A4D4' : '#205781';
      fish.draw(fishColor);
    };

    p.windowResized = () => {
      const container = vm.$refs.canvasContainer;
      p.resizeCanvas(container.clientWidth, container.clientHeight);
      p.setup();
    };
  }
}
}
// ... don't forget the closing brace for the export default

</script>

<style scoped>
.p5-canvas-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  /* The transition is now correctly placed in the main rule */
  transition: filter 1s ease-in-out;
}
</style>