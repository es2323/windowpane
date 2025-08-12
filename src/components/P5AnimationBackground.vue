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
    },
    particleColor: {
      type: String,
      default: '#FFFFFF'
    },
    lineColor: {
      type: String,
      default: '#B89A6A'
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
      let bubbles = [];
      let liminalStartFrame = 0;
      let wasLiminalLastFrame = false;

      // This class defines a single, undulating wave layer.
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
          this.original_swell_amplitude = p.random(5, 10); // Store the original
          this.swell_amplitude = this.original_swell_amplitude;
        }

        // Replace the entire update() method with this new version
        update(isLiminal) {
          // This part still makes the wave scroll horizontally
          this.phase += this.speed;
          this.swell_phase += this.swell_speed;
          let targetY;
          if (isLiminal) {
            // In Liminal Mode, the target is the top of the screen.
            // We subtract the original Y from the full height to get its distance from the top,
            // preserving the layered spacing.
            targetY = p.height - this.original_y + 150;
          } else {
            // In Default Mode, the target is its original home position.
            targetY = this.original_y;
          }

          // On every frame, smoothly move (lerp) towards the target position.
          this.y = p.lerp(this.y, targetY, 0.02);
          // --- DYNAMIC AMPLITUDE LOGIC ---
          let targetSwellAmplitude;
          if (isLiminal) {
            // In Liminal Mode, let's make the waves taller and more dramatic
                  targetSwellAmplitude = this.original_swell_amplitude * 7.5; // Much bigger swell
          } else {
            // In Default Mode, return to the original amplitude
            targetSwellAmplitude = this.original_swell_amplitude;
          }
          // Smoothly transition the current amplitude towards the target
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

      class Bubble {
        constructor() {
          // Start at the bottom center, with a little horizontal randomness
          this.x = p.random(p.width * 0.1, p.width * 0.7);
          this.y = p.height + 10; // Start just off-screen at the bottom
          
          this.radius = p.random(2, 8);
          this.ySpeed = p.random(1, 3); // How fast it rises
          
          // Each bubble gets its own wobble pattern
          this.wobblePhase = p.random(p.TWO_PI);
        }

        update() {
          this.y -= this.ySpeed; // Move up
    
          // Add a gentle side-to-side wobble using sin()
          this.x += p.sin(this.wobblePhase) * 0.5;
          this.wobblePhase += 0.05;
        }

        draw(bubbleColor) {
          const baseColor = p.color(bubbleColor);

          // Use a semi-transparent version for the inside of the bubble
          p.fill(
            p.red(baseColor),
            p.green(baseColor),
            p.blue(baseColor),
            255 // Opacity for the fill (0-255)
          );

          // Use a solid version for the outline
          p.stroke(baseColor);
          p.strokeWeight(0.5); // The thickness of the outline
          
          p.ellipse(this.x, this.y, this.radius * 2);
        }

        // A check to see if the bubble should be removed
        isOffscreen(surfaceY) {
          // We remove the bubble if it rises above the "surface" (the lowest wave)
          return this.y < (surfaceY - this.radius);
        }
      }

      // SETUP runs once at the start.
      p.setup = () => {
        const container = this.$refs.canvasContainer;
        p.createCanvas(container.clientWidth, container.clientHeight);
        p.frameRate(30);

        waves = []; 
        bubbles = [];

        const waveCount = 3;
        for (let i = 0; i < waveCount; i++) {
          let y = p.height - p.height * 0.12 + (i * 20);
          let amplitude = p.random(8, 15);
          let period = p.random(500, 500);
          let speed = p.random(0.02, 0.02);
          waves.push(new Wave(y, amplitude, period, speed));
        }
      };

      // DRAW runs on every frame.
      p.draw = () => {
        const isLiminal = document.body.classList.contains('liminal-mode-active');

        if (isLiminal) {
          p.background(255, 170, 51); 
        } else {
          p.background(this.backgroundColor);
        }
        
        // --- BUBBLE ANIMATION WITH TIMER ---

        // First, check if we have JUST switched into liminal mode this frame
        if (isLiminal && !wasLiminalLastFrame) {
          liminalStartFrame = p.frameCount; // If so, start the timer
        }

        if (isLiminal) {
          // You can easily change the delay here (in seconds)
          const delayInSeconds = 1;
          const frameDelay = delayInSeconds * 30; // Assuming 30fps

          // Only start creating and drawing bubbles AFTER the delay has passed
          if (p.frameCount > liminalStartFrame + frameDelay) {
            
            // This is your existing bubble code, now nested inside the timer check
            if (p.frameCount % 8 === 0) {
              bubbles.push(new Bubble());
            }

            let lowestWaveY = p.height;
            for (const wave of waves) {
              if (wave.y < lowestWaveY) {
                lowestWaveY = wave.y;
              }
            }

            for (let i = bubbles.length - 1; i >= 0; i--) {
              let bubble = bubbles[i];
              bubble.update();
              bubble.draw('#123458');
              if (bubble.isOffscreen(lowestWaveY)) {
                bubbles.splice(i, 1);
              }
            }
          }
        } else {
          bubbles = []; // Clear bubbles when not in liminal mode
        }

          wasLiminalLastFrame = isLiminal;
  // --- END OF BUBBLE ANIMATION BLOCK ---



        // FIX #4: Updated color arrays to match the new wave count
        const defaultColors = ['#205781', '#4F959D', '#98D2C0'];
        const underwaterColors = ['#54779280', '#54779280', '#94B4C180'];

        for (let i = 0; i < waves.length; i++) {
         let wave = waves[i];
          wave.update(isLiminal);

          // --- NEW COLOR BLENDING LOGIC ---
          let topTargetY = p.height - wave.original_y;

          // Calculate the wave's progress from bottom to top (a value from 0.0 to 1.0)
          // The 'true' at the end constrains the value, preventing weird color flashes
          let progress = p.map(wave.y, wave.original_y, topTargetY, 0, 1, true);

          // Create p5.Color objects from your hex codes
          let fromColor = p.color(defaultColors[i]);
          let toColor = p.color(underwaterColors[i]);

          // Blend the two colors based on the wave's vertical progress
          let blendedColor = p.lerpColor(fromColor, toColor, progress);

          // Draw the wave with the smoothly blended color
          wave.draw(blendedColor);
        }
      };

      p.windowResized = () => {
        const container = this.$refs.canvasContainer;
        p.resizeCanvas(container.clientWidth, container.clientHeight);
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