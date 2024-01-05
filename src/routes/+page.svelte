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
        Hey there, <strong>I'm Sam</strong>! I tell <strong>stories</strong> and create web <strong>experiences</strong> using <strong>digital design</strong> and <strong>web development</strong>.
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
    <div class="selector">
      <h2>My Work</h2>
      <div class="projects">
        <a class="project" href="//mora.do" target="_blank">
          <h3>Morado Development</h3>
          <p>Website created for Morado Development, a web development agency in Fall of 2023.</p>
        </a>
        <a class="project" href="//designspace.vercel.app" target="_blank">
          <h3>Design Space</h3>
          <p>Artificial intelligence design thinking web app created in Winter of 2023.</p>
        </a>
        <a class="project" href="//habitual.studio" target="_blank">
          <h3>Habitual Studio</h3>
          <p>Website for Habitual Studio, a digital agency. Created in Fall of 2023.</p>
        </a>
        <div class="selection-box">
          <div class="top-dots"></div>
          <div class="bottom-dots"></div>
        </div>
      </div>
    </div>
    <div class="showcase">
      <img class="display" src="/assets/pro-display-xdr.png"/>
      <div class="screen">
        <div class="images">
          <img src="/project-screenshots/morado-1.png" alt="project screenshot"/>
          <img src="/project-screenshots/designspace-1.png" alt="project screenshot"/>
          <img src="/project-screenshots/habitual-2.png" alt="project screenshot"/>
        </div>
      </div>
    </div>
  </section>

  <section class="contact">
    <div class="wrapper">
      <h2>Let's Work Together</h2>
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