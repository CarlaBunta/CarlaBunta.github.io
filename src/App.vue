<template>
  <div>
    <!-- Loading Screen -->
    <div v-if="loading" class="loading-screen">
      <div class="loading-text">Welcome</div>
    </div>

    <!-- Navigation Bar -->
    <nav>
      <ul>
        <li><a href="#hero" @click.prevent="scrollToSection('#hero')">Home</a></li>
        <li><a href="#about" @click.prevent="scrollToSection('#about')">About</a></li>
        <li><a href="#skills" @click.prevent="scrollToSection('#skills')">Skills</a></li>
        <li><a href="#projects" @click.prevent="scrollToSection('#projects')">Projects</a></li>
        <li><a href="#contact" @click.prevent="scrollToSection('#contact')">Contact</a></li>
      </ul>
    </nav>

    <!-- Sections -->
    <section id="hero">
      <h1>Carla Bunta</h1>
      <p>Web Developer | UI/UX Designer | Graphic Designer | Frontend Developer</p>
    </section>

    <section id="about">
      <h2>About Me</h2>
      <p>With a strong foundation in Computer Science and a passion for blending technology with aesthetics, I specialize in crafting seamless, visually engaging user experiences. My expertise spans frontend development, UI/UX design, and motion graphics, where I transform ideas into intuitive and dynamic interfaces.

        As a project manager, I have led teams in building innovative frontend solutions, ensuring efficiency from concept to execution. My experience in developing interactive web applications with Vue.js, HTML, and CSS has sharpened my ability to create fluid, user-centric designs. Additionally, my proficiency in GSAP animations and graphic design allows me to bring a creative edge to every project, making interfaces not only functional but also visually captivating.

        I thrive in dynamic environments where creativity meets technology, always eager to push boundaries and refine my craft. If you're looking for someone who can bridge the gap between technical precision and artistic vision, let's build something amazing together.</p>
    </section>

    <section id="skills">
      <h2>Skills</h2>
      <div class="skills-container">
        <div class="skill-item">HTML5</div>
        <div class="skill-item">CSS3</div>
        <div class="skill-item">JavaScript</div>
        <div class="skill-item">Vue.js</div>
        <div class="skill-item">GSAP Animations</div>
        <div class="skill-item">Graphic Design</div>
      </div>
    </section>

    <section id="projects">
      <h2>Projects</h2>
      <div class="projects-grid">
        <div class="project-card" v-for="project in projects" :key="project.id">
          <h3>{{ project.name }}</h3>
          <p>{{ project.description }}</p>
          <a :href="project.link">View Project</a>
        </div>
      </div>
    </section>

    <section id="contact">
      <h2>Contact Me</h2>
      <p>Email: your.email@example.com</p>
      <p>LinkedIn: your-linkedin-profile</p>
      <p>GitHub: your-github-profile</p>
    </section>
  </div>
</template>

<script>
  import gsap from "gsap";
  import ScrollTrigger from "gsap/ScrollTrigger";

  export default {
    data() {
      return {
        loading: true,
        skills: ["HTML5", "CSS3", "JavaScript", "Vue.js"],
        projects: [
          { id: 1, name: "Project 1", description: "Project description goes here", link: "#" },
        ],
      };
    },
    mounted() {
      gsap.registerPlugin(ScrollTrigger);
      this.initializeAnimations();
    },
    methods: {
      initializeAnimations() {
        window.addEventListener("load", () => {
          gsap.to(".loading-screen", {
            opacity: 0,
            duration: 1,
            onComplete: () => {
              this.loading = false;
            },
          });
        });

        gsap.utils.toArray("section").forEach((section) => {
          gsap.to(section, {
            opacity: 1,
            y: 0,
            duration: 1,
            scrollTrigger: {
              trigger: section,
              start: "top center",
            },
          });
        });

        gsap.from(".skill-item", {
          opacity: 0,
          y: 50,
          stagger: 0.1,
          scrollTrigger: {
            trigger: ".skills-container",
            start: "top center",
          },
        });

        gsap.from(".project-card", {
          opacity: 0,
          y: 50,
          stagger: 0.2,
          scrollTrigger: {
            trigger: ".projects-grid",
            start: "top center",
          },
        });
      },
      scrollToSection(id) {
        document.querySelector(id).scrollIntoView({ behavior: "smooth" });
      },
    },
  };
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'Arial', sans-serif;
    line-height: 1.6;
    color: #333;
  }

  nav {
    background: #2c3e50;
    padding: 1rem;
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 1000;
  }

  nav ul {
    display: flex;
    justify-content: flex-end;
    list-style: none;
  }

  nav ul li a {
    color: white;
    text-decoration: none;
    padding: 0.5rem 1rem;
    transition: color 0.3s ease;
  }

  nav ul li a:hover {
    color: #3498db;
  }

  section {
    padding: 5rem 2rem;
    min-height: 100vh;
    opacity: 0;
  }

  #hero {
    background: #3498db;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    padding: 2rem 0;
  }

  .project-card {
    border: 1px solid #ddd;
    padding: 1rem;
    border-radius: 8px;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: pointer;
  }

  .project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  }

  .skills-container {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    padding: 2rem 0;
  }

  .skill-item {
    background: #f0f0f0;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    transition: transform 0.3s ease, background 0.3s ease;
  }

  .skill-item:hover {
    transform: scale(1.1);
    background: #3498db;
    color: white;
  }

  .loading-screen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #2c3e50;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 2000;
  }

  .loading-text {
    color: white;
    font-size: 2rem;
  }
</style>
