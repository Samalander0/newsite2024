<script>
  import "$lib/styles/styles.scss";
  import {onMount} from 'svelte'
  import Typewriter from 'svelte-typewriter'

  // Get time for time display
  import dayjs from "dayjs"
  import utc from "dayjs/plugin/utc"
  import timezone from "dayjs/plugin/timezone"

  dayjs.extend(utc);
  dayjs.extend(timezone);

  let time = dayjs().tz("America/Los_Angeles").format("hh:mm A");
  setInterval(() => {
    time = dayjs().tz("America/Los_Angeles").format("hh:mm A");
  }, 5000);

  // GSAP
  import { gsap } from "gsap/dist/gsap";
  import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
  import { ScrollSmoother } from "$lib/gsap/src/ScrollSmoother";
  import { Flip } from "$lib/gsap/src/Flip";
  import { Draggable } from "$lib/gsap/src/Draggable";

  gsap.registerPlugin(ScrollTrigger, ScrollSmoother, Flip, Draggable);

  let smoother;
  onMount(() => {
    if (window.innerWidth >= 900) { // Only use scrollSmoother if on a large enough page
      smoother = ScrollSmoother.create({
        smooth: 0.5,
        effects: true,
      });
    }
  });

  // Project Windows
  let project1 = {open: false, opened: false, element: null, imageSlider: {element: null, container: null}},
      project2 = {open: false, opened: false, element: null, imageSlider: {element: null, container: null}},
      project3 = {open: false, opened: false, element: null, imageSlider: {element: null, container: null}};
  let cooldown = false;

  // Animate opening/closing
  function cancelCooldown() {cooldown = false}

  function findOpenProject(projects) {
    for (let i = 0; i < projects.length; i++) {
      if (projects[i].open) {
        return projects[i];
      }
    }
  }

  function closeAllProjects() {
    let project = findOpenProject([project1, project2, project3])

    getProjectsState(project)

    project.element.classList.add("closed");
    project.open = false;

    animateProjects()

    allProjectsClosed = !(project1.open || project2.open || project3.open);
  }

  let allProjectsClosed = !(project1.open || project2.open || project3.open);

  function toggleProject(project, value) {
    if (!cooldown && value) {
      getProjectsState(project)
      project.element.classList.remove("closed")
      project.open = true;
      animateProjects()

      cooldown = true;
      setTimeout(cancelCooldown, 1000); // After 1 second, set cooldown to false

      // Create the image slider
      if (!project.opened) { //need to do this after delay
        setTimeout(() => {
          const widthOfImages = project.imageSlider.element.getElementsByTagName('*').length * 632 - 32;
          const maxScrollDistance = project.imageSlider.container.getBoundingClientRect().width - widthOfImages;
          Draggable.create(project.imageSlider.element, {
            type: "x",
            bounds: {
              maxX: maxScrollDistance, 
              minX: 0
            }
          })
        }, 500)
        project.opened = true
      }
    } else if (!cooldown && !value) {
      getProjectsState(project)
      project.element.classList.add("closed")
      project.open = false;
      animateProjects()

      cooldown = true;
      setInterval(cancelCooldown, 1000); // After 1 second, set cooldown to false
    }

    allProjectsClosed = !(project1.open || project2.open || project3.open);
  }

  let flipState;
  function getProjectsState(project) {
    flipState = Flip.getState(project.element);
  }
  function animateProjects() {
    Flip.from(flipState, {
      duration: 0.5,
      ease: "power2.out",
    })
  }
</script>

<nav>
  <h2>Sam Cheng</h2>
  <div class="nav-socials">
    <a href="https://github.com/samalander0" target="_blank">
      <img src="/assets/github-white.svg" alt="github"/>
    </a>
    <a href="https://www.linkedin.com/in/samalander/" target="_blank">
      <img src="/assets/linkedin-white.svg" alt="linkedin"/>
    </a>
    <a href="https://twitter.com/samaland3r" target="_blank">
      <img src="/assets/twitter-white.svg" alt="github"/>
    </a>
    <a href="https://discord.com/users/588480933108121618" target="_blank">
      <img src="/assets/discord-white.svg" alt="discord"/>
    </a>
  </div>
</nav>

<header class="hero">
  <h1>
    Sam is a 
    <span class="selected" style="--cursor-color: #0019FF; --cursor-width: 0.1em;">
      <div class="selected-bottom-dots"></div>
      <Typewriter mode="loop" interval="150" unwriteInterval="75" wordInterval="2500">
        <span>Designer</span>
        <span>Developer</span>
        <span>Student</span>
        <span>Maker</span>
      </Typewriter>
    </span>
  </h1>

  <div class="hero-bottom">
    <div class="hero-about">
      <p>
        Hey there! <strong>I'm Sam</strong>, and I create web <strong>experiences</strong> and tell <strong>stories</strong> using <strong>digital design</strong> and <strong>web development</strong>.
      </p>
      <br/>
      <p>
        Right now, I'm working with clients and agencies to tell meaningful stories online.
      </p>
    </div>
    <div class="hero-skills">
      <div class="skill-category">
        <p><strong>Design</strong></p>
        <p>
          Figma<br/>
          AdobeXD<br/>
        </p>
      </div>
      <br/>
      <div class="skill-category">
        <p><strong>Development</strong></p>
        <p>
          Svelte & React<br/>
          CSS/HTML/JS<br/>
          GSAP<br/>
        </p>
      </div>
    </div>
    <div class="hero-time-and-scroll">
      <p class="hero-time">
        <strong>{time} San Francisco</strong><br/>
        Scroll for more
      </p>
      <div class="hero-scroll">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
  </div>
</header>

<main>
  <section class="work">
    <h2 class="title">
      <span class="title-group">
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
      </span>
      <span class="title-group">
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
      </span>
      <span class="title-group">
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
      </span>
      <span class="title-group">
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
        <span>My Work</span>
        <img src="/assets/star.svg" alt="star"/>
      </span>
    </h2>
    <div class="projects">
      <button id="background" disabled={allProjectsClosed} on:click={closeAllProjects}></button>
      <div id="project1" class="project closed" on:click={() => {toggleProject(project1, true)}} bind:this={project1.element}>
        <div class="project-top-bar">
          <button on:click={() => {toggleProject(project1, false)}}></button>
          <button on:click={() => {toggleProject(project1, false)}}></button>
          <button on:click={() => {toggleProject(project1, true)}}></button>
        </div>
        <div class="project-content">
          <h3>Habitual</h3>
          <div class="tags">
            <span>Web Design</span>
            <span>Web Development</span>
          </div>
          <div class="images" bind:this={project1.imageSlider.container}>
            <div class="wrapper" bind:this={project1.imageSlider.element}>
              <img src="/project-screenshots/habitual-1.png"/>
              <img src="/project-screenshots/habitual-2.png"/>
              <img src="/project-screenshots/habitual-3.png"/>
            </div>
          </div>
          <div class="text">
            <p>
              <a href="https://www.habitual.studio/" target="_blank">Habitual</a> is a design, development, and marketing agency that I got the chance to create a website for in Fall 2023. They wanted to establish a strong brand presence and bring a sense of authenticity and uniqueness to their agency.
            </p>
          </div>
        </div>
      </div>
      <div id="project2" class="project closed" on:click={() => {toggleProject(project2, true)}} bind:this={project2.element}>
        <div class="project-top-bar">
          <button on:click={() => {toggleProject(project2, false)}}></button>
          <button on:click={() => {toggleProject(project2, false)}}></button>
          <button on:click={() => {toggleProject(project2, true)}}></button>
        </div>
        <div class="project-content">
          <h3>Design Space</h3>
          <div class="tags">
            <span>Web Design</span>
            <span>Web Development</span>
            <span>Artificial Intelligence</span>
          </div>
          <div class="images" bind:this={project2.imageSlider.container}>
            <div class="wrapper" bind:this={project2.imageSlider.element}>
              <img src="/project-screenshots/designspace-1.png"/>
              <img src="/project-screenshots/designspace-2.png"/>
              <img src="/project-screenshots/designspace-3.png"/>
            </div>
          </div>
          <div class="text">
            <p>
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
            </p>
          </div>
        </div>
      </div>
      <div id="project3" class="project closed" on:click={() => {toggleProject(project3, true)}} bind:this={project3.element}>
        <div class="project-top-bar">
          <button on:click={() => {toggleProject(project3, false)}}></button>
          <button on:click={() => {toggleProject(project3, false)}}></button>
          <button on:click={() => {toggleProject(project3, true)}}></button>
        </div>
        <div class="project-content">
          <h3>Morado Development</h3>
          <div class="tags">
            <span>Web Design</span>
            <span>Web Development</span>
          </div>
          <div class="images" bind:this={project3.imageSlider.container}>
            <div class="wrapper" bind:this={project3.imageSlider.element}>
              <img src="/project-screenshots/morado-1.png"/>
              <img src="/project-screenshots/morado-2.png"/>
              <img src="/project-screenshots/morado-3.png"/>
              <img src="/project-screenshots/morado-4.png"/>
            </div>
          </div>
          <div class="text">
            <p>
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section class="contact">
    <div class="wrapper">
      <h2>Say Hello</h2>
      <div class="contact-content">
        <div class="content-left">
          <div class="content-category">
            <p><strong>Contact</strong></p>
            <p>
              <a href="mailto:sam@samalander.dev" target="_blank">sam@samalander.dev</a><br/>
              <a href="https://discord.com/users/588480933108121618" target="_blank">@samaland3r (Discord)</a>
            </p>
          </div>
          <div class="content-category">
            <p><strong>Location</strong></p>
            <p>Currently based in Silicon Valley, CA</p>
          </div>
          <div class="content-category">
            <p><strong>Links</strong></p>
            <p>
              <a href="https://github.com/samalander0" target="_blank">Github</a><br/>
              <a href="https://www.linkedin.com/in/samalander/" target="_blank">LinkedIn</a><br/>
              <a href="https://twitter.com/samaland3r" target="_blank">Twitter</a>
            </p>
          </div>
        </div>
        <form class="contact-form" acceptCharset="utf-8" action="https://formsubmit.co/contact@samalander.dev" method="post">
          <div class="group">
            <div class="field">
              <label for="your-name">Name</label>
              <input type="text" name="name" id="your-name" placeholder="Name" autocomplete="name" required/>
            </div>
            <div class="field">
              <label for="your-email">Email</label>
              <input type="email" name="email" id="your-email" placeholder="Email" autocomplete="email" required/>
            </div>
          </div>
          <div class="field">
            <label for="message">Message</label>
            <textarea name="message" id="message" placeholder="Message" required/>
          </div>
          <input type="submit" value="Submit"/>
          <input type="hidden" name="_next" value="https://www.samalander.dev">
        </form>
      </div>
    </div>
  </section>
</main>