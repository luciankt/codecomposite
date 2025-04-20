<script setup>
import { ref } from 'vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faSun, faMoon } from '@fortawesome/free-solid-svg-icons';

library.add(faSun, faMoon);

const isDarkMode = ref(false);
const email = ref('');
const successMessage = ref('');
const visibleLogos = ref([]);

const techLogos = ref([
  { src: new URL('./assets/logo1.png', import.meta.url).href, alt: 'Google' },
  { src: new URL('./assets/logo2.png', import.meta.url).href, alt: 'NVIDIA' },
  { src: new URL('./assets/logo3.png', import.meta.url).href, alt: 'Microsoft' },
  { src: new URL('./assets/logo4.png', import.meta.url).href, alt: 'Anthropic' },
  { src: new URL('./assets/logo5.png', import.meta.url).href, alt: 'OpenAI' },
  { src: new URL('./assets/logo6.png', import.meta.url).href, alt: 'Meta' },
  { src: new URL('./assets/logo7.png', import.meta.url).href, alt: 'Amazon' },
  { src: new URL('./assets/logo8.png', import.meta.url).href, alt: 'Apple' },
  { src: new URL('./assets/logo9.png', import.meta.url).href, alt: 'IBM' },
  { src: new URL('./assets/logo10.png', import.meta.url).href, alt: 'Tesla' },
  { src: new URL('./assets/logo11.png', import.meta.url).href, alt: 'CreateX' },
]);

const rotateLogos = () => {
  const firstLogo = techLogos.value.shift(); // Remove the first logo
  techLogos.value.push(firstLogo); // Add it to the end
  visibleLogos.value = techLogos.value.slice(0, 3); // Update visible logos
};

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  document.documentElement.classList.toggle('dark-mode', isDarkMode.value);
};

const handleSignup = () => {
  if (email.value) {
    successMessage.value = 'Thank you for signing up!';
    email.value = '';
    setTimeout(() => {
      successMessage.value = '';
    }, 3000);
  }
};
</script>

<template>
  <header>
    <h1>CodeComposite</h1>
    <p class="tagline">Revolutionizing video editing for developers and creators.</p>
    <button class="dark-mode-toggle" @click="toggleDarkMode">
      <font-awesome-icon v-if="isDarkMode" icon="sun" style="color: white;" />
      <font-awesome-icon v-else icon="moon" style="color: black;" />
    </button>
    <div class="logo">
      <img src="./assets/logo.png" alt="CodeComposite Logo" />
    </div>
  </header>

  <main>
    <section class="features">
      <h2>Features</h2>
      <ul>
        <li>Code-based video editing for precision and flexibility.</li>
        <li>Import multimedia and your data for dynamic visualizations.</li>
        <li>Real-time previews and rendering.</li>
      </ul>
    </section>
    
    <section class="carousel">
      <div class="carousel-container">
        <div class="carousel-item">
          <video autoplay muted loop>
            <source src="./assets/video1.mp4" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
        </div>
        <div class="carousel-item">
          <video autoplay muted loop>
            <source src="./assets/video1.mp4" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
        </div>
        <div class="carousel-item">
          <video autoplay muted loop>
            <source src="./assets/video1.mp4" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
        </div>
      </div>
    </section>

    <section class="investment">

      <h2>Investment Funding</h2>
        <p>We are <s>proud</s> to announce that CodeComposite has secured $0 in seed funding to revolutionize video editing for developers and creators.</p>
        <p>See some of the companies we admire:</p>
        <section class="tech-carousel">
        <div class="tech-carousel-container">
            <div
              class="tech-carousel-item"
              v-for="(logo, index) in techLogos"
              :key="index"
            >
              <img :src="logo.src" :alt="logo.alt" />
            </div>
            <!-- Duplicate the logos for seamless looping -->
            <div
              class="tech-carousel-item"
              v-for="(logo, index) in techLogos"
              :key="'duplicate-' + index"
            >
              <img :src="logo.src" :alt="logo.alt" />
            </div>
          </div>
      </section>
    </section>

    <section class="cta">
      <h2>Join Our Mailing List</h2>
      <p>Stay updated with the latest features and updates.</p>
      <form @submit.prevent="handleSignup" class="email-signup-form">
        <input type="email" v-model="email" placeholder="Enter your email" required />
        <button type="submit" class="cta-button">Sign Up</button>
      </form>
      <p v-if="successMessage" class="success-message">{{ successMessage }}</p>
    </section>
  </main>
</template>

<style>
html {
  --background-color: #f0f0f0;
  --text-color: #333;
}

html.dark-mode {
  --background-color: #121212;
  --text-color: #ffffff;
  --header-background: #1e1e1e;
  --cta-background: #004d40;
}

body {
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: var(--background-color);
  color: var(--text-color);
  transition: background-color 0.5s, color 0.5s; 
}

header {
  text-align: center;
  padding: 1rem;
  background-color: var(--header-background);
  position: relative;
  color: var(--text-color);
  transition: background-color 0.5s, color 0.5s; 
}

.logo img {
  width: 200px;
  height: auto;
  margin-bottom: 1rem;
  animation: float 3s ease-in-out infinite, shadow-pulse 3s ease-in-out infinite;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

@keyframes shadow-pulse {
  0%, 100% {
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  50% {
    box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
  }
}

.tagline {
  font-size: 1.2rem;
  color: var(--text-color);
}

.dark-mode-toggle {
  position: fixed; 
  top: 1rem; 
  right: 1rem; 
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  z-index: 1000; 
}

.features {
  padding: 1rem;
  color: var(--text-color);
}

.features h2 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.features ul {
  list-style: none;
  padding: 0;
}

.features li {
  margin-bottom: 0.5rem;
}

.cta {
  text-align: center;
  padding: 1rem;
  background-color: var(--cta-background);
  color: var(--text-color);

}

.cta-button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  color: white;
  background-color: #00796b;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.carousel-container {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  gap: 1rem;
  padding: 1rem 0;
  scrollbar-width: none; 
  scroll-behavior: smooth; 
  justify-content: center; 
}

.carousel-container::-webkit-scrollbar {
  display: none; 
}

.carousel-item {
  flex: 0 0 80%; 
  max-width: 600px; 
  scroll-snap-align: center;
  border: 1px solid #ddd;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #fff; 
}

.carousel-item video {
  width: 100%;
  height: auto;
  display: block;
}

@media (min-width: 768px) {
  .carousel-container {
    gap: 2rem; 
  }

  .carousel-item {
    flex: 0 0 60%; 
  }
}

@media (min-width: 1024px) {
  .carousel-item {
    flex: 0 0 50%; 
  }
}
.email-signup-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  margin-top: 1rem;
}

.email-signup-form input[type="email"] {
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 100%;
  max-width: 300px;
  box-sizing: border-box;
}

.email-signup-form button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  color: white;
  background-color: #00796b;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.email-signup-form button:hover {
  background-color: #005f56;
}
.success-message {
  margin-top: 1rem;
  color: #00796b;
  font-size: 1rem;
  font-weight: bold;
  text-align: center;
}

.investment {
  color: var(--text-color);
  background-color: var(--background-color);
  padding: 1rem;
}

.tech-carousel {
  margin-top: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden; /* Hide overflowing logos */
  padding: 1rem 0;
  width: 100%;
  background-color: var(--background-color);
  color: var(--text-color);
}
.tech-carousel {
  margin-top: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden; /* Hide overflowing logos */
  padding: 1rem 0;
  width: 100%;
}

.tech-carousel-container {
  display: flex;
  gap: 1rem;
  animation: scroll 20s linear infinite; /* Smooth scrolling animation */
}

.tech-carousel-item {
  flex: 0 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 0.5rem;
  background-color: #fff;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.tech-carousel-item img {
  max-width: 100px;
  max-height: 50px;
  object-fit: contain;
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%); /* Move halfway to loop seamlessly */
  }
}
</style>