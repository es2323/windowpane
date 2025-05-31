<template>
  <section id="contact" class="contact-section section-padding">
    <div class="container">
      <div class="contact-grid">
        <div class="contact-info">
          <h2 class="section-title fade-in">let's connect</h2>
          
          <div class="contact-text fade-in">
            <p class="intro-text">
              i'm always interested in new opportunities, 
              collaborations, and meaningful conversations.
            </p>
            
            <p>
              whether you have a project in mind, want to discuss technology, 
              or just want to say hello, i'd love to hear from you.
            </p>
          </div>

          <div class="contact-methods fade-in">
            <div class="contact-method">
              <div class="method-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                  <polyline points="22,6 12,13 2,6"/>
                </svg>
              </div>
              <div class="method-content">
                <h3>email</h3>
                <a href="mailto:your.email@example.com" class="contact-link">
                  your.email@example.com
                </a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
                  <rect x="2" y="9" width="4" height="12"/>
                  <circle cx="4" cy="4" r="2"/>
                </svg>
              </div>
              <div class="method-content">
                <h3>linkedin</h3>
                <a href="https://linkedin.com/in/yourprofile" target="_blank" class="contact-link">
                  /in/enosh-earnest
                </a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/>
                </svg>
              </div>
              <div class="method-content">
                <h3>github</h3>
                <a href="https://github.com/yourusername" target="_blank" class="contact-link">
                  /yourusername
                </a>
              </div>
            </div>
          </div>
        </div>

        <div class="contact-form-container fade-in">
          <form @submit.prevent="submitForm" class="contact-form">
            <div class="form-group">
              <label for="name">name</label>
              <input 
                type="text" 
                id="name" 
                v-model="form.name" 
                required
                :class="{ 'error': errors.name }"
              >
              <span v-if="errors.name" class="error-message">{{ errors.name }}</span>
            </div>

            <div class="form-group">
              <label for="email">email</label>
              <input 
                type="email" 
                id="email" 
                v-model="form.email" 
                required
                :class="{ 'error': errors.email }"
              >
              <span v-if="errors.email" class="error-message">{{ errors.email }}</span>
            </div>

            <div class="form-group">
              <label for="subject">subject</label>
              <input 
                type="text" 
                id="subject" 
                v-model="form.subject" 
                required
                :class="{ 'error': errors.subject }"
              >
              <span v-if="errors.subject" class="error-message">{{ errors.subject }}</span>
            </div>

            <div class="form-group">
              <label for="message">message</label>
              <textarea 
                id="message" 
                v-model="form.message" 
                rows="5" 
                required
                :class="{ 'error': errors.message }"
              ></textarea>
              <span v-if="errors.message" class="error-message">{{ errors.message }}</span>
            </div>

            <button 
              type="submit" 
              class="submit-btn"
              :disabled="isSubmitting"
              :class="{ 'submitting': isSubmitting, 'success': submitSuccess }"
            >
              <span v-if="!isSubmitting && !submitSuccess">send message</span>
              <span v-if="isSubmitting">sending...</span>
              <span v-if="submitSuccess">message sent!</span>
            </button>

            <p v-if="submitMessage" class="submit-message" :class="submitSuccess ? 'success' : 'error'">
              {{ submitMessage }}
            </p>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'contactsection',
  data() {
    return {
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      errors: {},
      isSubmitting: false,
      submitSuccess: false,
      submitMessage: ''
    }
  },
  mounted() {
    this.setupScrollAnimation()
  },
  methods: {
    setupScrollAnimation() {
      const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -50px 0px'
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
    },
    
    validateForm() {
      this.errors = {}
      
      if (!this.form.name.trim()) {
        this.errors.name = 'name is required'
      }
      
      if (!this.form.email.trim()) {
        this.errors.email = 'email is required'
      } else if (!this.isValidEmail(this.form.email)) {
        this.errors.email = 'please enter a valid email'
      }
      
      if (!this.form.subject.trim()) {
        this.errors.subject = 'subject is required'
      }
      
      if (!this.form.message.trim()) {
        this.errors.message = 'message is required'
      } else if (this.form.message.trim().length < 10) {
        this.errors.message = 'message must be at least 10 characters'
      }
      
      return Object.keys(this.errors).length === 0
    },
    
    isValidEmail(email) {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      return emailRegex.test(email)
    },
    
    async submitForm() {
      if (!this.validateForm()) {
        return
      }
      
      this.isSubmitting = true
      this.submitMessage = ''
      
      try {
        // simulate api call
        await new Promise(resolve => setTimeout(resolve, 2000))
        
        // in a real app, you would send the form data to your backend
        console.log('form submitted:', this.form)
        
        this.submitSuccess = true
        this.submitMessage = 'thank you for your message! i\'ll get back to you soon.'
        
        // reset form after success
        setTimeout(() => {
          this.resetForm()
        }, 3000)
        
      } catch (error) {
        this.submitSuccess = false
        this.submitMessage = 'sorry, there was an error sending your message. please try again.'
      } finally {
        this.isSubmitting = false
      }
    },
    
    resetForm() {
      this.form = {
        name: '',
        email: '',
        subject: '',
        message: ''
      }
      this.submitSuccess = false
      this.submitMessage = ''
      this.errors = {}
    }
  }
}
</script>

<style scoped>
.contact-section {
  background: #fff;
  position: relative;
}

.contact-grid {
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
}

.intro-text {
  font-size: 1.2rem;
  line-height: 1.6;
  color: #2c3e50;
  margin-bottom: 1.5rem;
  font-weight: 500;
}

.contact-text p {
  color: #6c757d;
  line-height: 1.7;
  margin-bottom: 1.2rem;
}

.contact-methods {
  margin-top: 3rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.method-icon {
  width: 48px;
  height: 48px;
  background: #f8f9fa;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #3498db;
  transition: all 0.3s ease;
}

.method-icon svg {
  width: 24px;
  height: 24px;
}

.contact-method:hover .method-icon {
  background: #3498db;
  color: white;
  transform: translateY(-2px);
}

.method-content h3 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #2c3e50;
  margin-bottom: 0.25rem;
  text-transform: lowercase;
}

.contact-link {
  color: #6c757d;
  text-decoration: none;
  font-size: 0.95rem;
  transition: color 0.3s ease;
}

.contact-link:hover {
  color: #3498db;
}

.contact-form {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 12px;
  border: 1px solid #e9ecef;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  color: #2c3e50;
  font-size: 0.9rem;
  text-transform: lowercase;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background: white;
  font-family: inherit;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

.form-group input.error,
.form-group textarea.error {
  border-color: #e74c3c;
}

.error-message {
  display: block;
  color: #e74c3c;
  font-size: 0.8rem;
  margin-top: 0.5rem;
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

.submit-btn {
  width: 100%;
  padding: 1rem;
  background: #3498db;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-transform: lowercase;
  letter-spacing: 0.5px;
}

.submit-btn:hover:not(:disabled) {
  background: #2980b9;
  transform: translateY(-1px);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

.submit-btn.submitting {
  background: #95a5a6;
}

.submit-btn.success {
  background: #27ae60;
}

.submit-message {
  margin-top: 1rem;
  padding: 0.75rem;
  border-radius: 8px;
  font-size: 0.9rem;
  text-align: center;
}

.submit-message.success {
  background: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.submit-message.error {
  background: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
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

/* responsive */
@media (max-width: 968px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}

@media (max-width: 768px) {
  .contact-methods {
    margin-top: 2rem;
    gap: 1.5rem;
  }
  
  .contact-form {
    padding: 1.5rem;
  }
  
  .form-group {
    margin-bottom: 1.25rem;
  }
}

@media (max-width: 480px) {
  .contact-method {
    gap: 0.75rem;
  }
  
  .method-icon {
    width: 40px;
    height: 40px;
  }
  
  .method-icon svg {
    width: 20px;
    height: 20px;
  }
  
  .contact-form {
    padding: 1rem;
  }
}
</style>