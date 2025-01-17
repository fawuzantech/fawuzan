<script>
  import { onMount } from 'svelte';

  let isLoading = true;  // Controls whether the loading screen is visible
  let audio;

  onMount(() => {
    // Play the boot sound immediately when the page loads
    audio = new Audio('/boot-sound.mp3'); // Replace with the path to your boot sound

    // Ensure audio is ready to play
    audio.oncanplaythrough = () => {
      // Start playing the sound
      audio.play().then(() => {
        // After the audio finishes, hide the loading screen
        setTimeout(() => {
          isLoading = false; // Hide the loading screen after the sound duration
        }, audio.duration * 1000);  // Duration is in seconds, multiply by 1000 to convert to milliseconds
      }).catch((error) => {
        console.error("Error playing audio:", error); // Handle any errors
      });
    };
  });

  const photo = "/f15e92.jpg"; // Replace with the path to your profile photo

  const projects = [
    {
      title: "Project Alpha",
      description: "Full-stack application with real-time updates",
      tech: ["React", "Node.js", "Socket.IO"],
      image: "/placeholder-project1.jpg"
    },
    {
      title: "Project Beta",
      description: "AI-powered game analytics dashboard",
      tech: ["Python", "TensorFlow", "Vue.js"],
      image: "/placeholder-project2.jpg"
    }
  ];

  const skills = [
    { name: "Frontend", level: 92 },
    { name: "Backend", level: 88 },
    { name: "DevOps", level: 85 },
    { name: "Game Development", level: 90 }
  ];
</script>

<style>
  :global(body) {
    margin: 0;
    background-color: #0A0A0A;
    color: #E2E2E2;
    font-family: 'Tachyon', sans-serif;
  }

  .loading-screen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #000;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 1000;
    animation: fadeOut 1s forwards 2s; /* Fade out effect after the timeout */
  }

  @keyframes fadeOut {
    to {
      opacity: 0;
      visibility: hidden;
    }
  }

  .rog-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
  }

  .profile {
    display: flex;
    align-items: center;
    gap: 2rem;
    margin: 2rem 0;
    background: rgba(255, 255, 255, 0.05);
    padding: 2rem;
    border-radius: 10px;
    border: 2px solid #ff0000;
    box-shadow: 0 0 15px rgba(255, 0, 0, 0.3);
  }

  .profile-photo {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    border: 3px solid #ff0000;
    object-fit: cover;
    box-shadow: 0 0 10px rgba(255, 0, 0, 0.5);
  }

  .profile-intro {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  .profile-intro h1 {
    margin: 0;
  }

  .profile-intro .subtitle {
    font-size: 1.2rem;
    color: #ccc;
  }

  .hero {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
    overflow: hidden;
  }

  .hero::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(45deg, #ff0000 0%, #000 100%);
    opacity: 0.1;
    z-index: -1;
  }

  .glitch-text {
    font-size: 4rem;
    font-weight: bold;
    text-transform: uppercase;
    color: #fff;
    text-shadow: 
      2px 2px #ff0000,
      -2px -2px #00ff00;
    animation: glitch 1s infinite;
  }

  .project-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-top: 4rem;
  }

  .project-card {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid #ff0000;
    padding: 1.5rem;
    border-radius: 8px;
    transition: transform 0.3s ease;
  }

  .project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 0 20px rgba(255, 0, 0, 0.3);
  }

  .skill-bar {
    width: 100%;
    height: 20px;
    background: rgba(255, 255, 255, 0.1);
    margin: 1rem 0;
    position: relative;
    border-radius: 10px;
    overflow: hidden;
  }

  .skill-progress {
    height: 100%;
    background: linear-gradient(90deg, #ff0000, #ff6b6b);
    position: absolute;
    transition: width 1s ease;
  }

  @keyframes glitch {
    0% { transform: translate(0); }
    20% { transform: translate(-2px, 2px); }
    40% { transform: translate(-2px, -2px); }
    60% { transform: translate(2px, 2px); }
    80% { transform: translate(2px, -2px); }
    100% { transform: translate(0); }
  }
</style>

{#if isLoading}
  <div class="loading-screen">
    <div class="glitch-text">INITIALIZING...</div>
  </div>
{/if}

<main class="rog-container">
  <section class="profile">
    <img src="{photo}" alt="Your Photo" class="profile-photo" />
    <div class="profile-intro">
      <h1 class="glitch-text">[IbrahimFawuzan]</h1>
      <p class="subtitle">SOFTWARE ENGINEER & GAMING ENTHUSIAST</p>
    </div>
  </section>

  <section id="projects">
    <h2 class="glitch-text">PROJECTS</h2>
    <div class="project-grid">
      {#each projects as project}
        <div class="project-card">
          <h3>{project.title}</h3>
          <p>{project.description}</p>
          <div class="tech-stack">
            {#each project.tech as tech}
              <span class="tech-tag">{tech}</span>
            {/each}
          </div>
        </div>
      {/each}
    </div>
  </section>
  
  <section id="skills">
    <h2 class="glitch-text">SKILL MATRIX</h2>
    {#each skills as skill}
      <div class="skill-container">
        <h3>{skill.name}</h3>
        <div class="skill-bar">
          <div 
            class="skill-progress" 
            style="width: {skill.level}%"
          ></div>
        </div>
      </div>
    {/each}
  </section>
</main>
