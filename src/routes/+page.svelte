<script>
  import "$lib/styles/styles.scss";
  import {onMount} from 'svelte'
  import Typewriter from 'svelte-typewriter'
  import Carousel from "$lib/components/Carousel.svelte";
  import Metatags from "$lib/components/Metatags.svelte";

  let windowWidth;
  onMount(() => {
    windowWidth = window.innerWidth;
  })

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

  gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

  let smoother,
      showcaseElement;
  onMount(() => {
    if (windowWidth >= 900) { // Only use scrollSmoother if on a large enough page
      smoother = ScrollSmoother.create({
        smooth: 0.5,
        effects: true,
      });
    }
    if (windowWidth > 1000) {
      gsap.to(".showcase", {
        backgroundPosition: "-16px 800px",
        scrollTrigger: {
          start: "top bottom",
          end: "bottom top",
          scrub: true
        }
      })
      gsap.to(".hero h1", {
        top: "0.75em",
        scrollTrigger: {
          trigger: ".hero",
          start: "top top",
          end: "bottom top",
          scrub: true
        }
      })
      gsap.to(".hero-bottom", {
        y: "150%",
        scrollTrigger: {
          trigger: ".hero",
          start: "top top",
          end: "bottom top",
          scrub: true
        }
      })
    }
  });

  // Work section
  let hoveredProject = 0;
</script>

<Metatags/>

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
      <Typewriter mode="loop" interval="150" unwriteInterval="75" wordInterval="1500" delay="1000">
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
        Hey there, <strong>I'm Sam</strong>! I tell <strong>stories</strong> and craft web <strong>experiences</strong> using <strong>digital design</strong> and <strong>web development</strong>.
      </p>
      <br/>
      <p>
        Right now, I'm working with clients and agencies to create engaging and user-friendly digital presences.
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
  <section class="work" data-hovered-project={hoveredProject}>
    {#if windowWidth < 1000}
      <div class="mobile-projects">
        <h2>My Work</h2>
        <div class="projects">
          <div class="project">
            <Carousel>
              <img src="/project-screenshots/morado-1.png" alt="project screenshot"/>
              <img src="/project-screenshots/morado-2.png" alt="project screenshot"/>
              <img src="/project-screenshots/morado-3.png" alt="project screenshot"/>
            </Carousel>
            <a class="project-info" href="//mora.do" target="_blank">
              <h3>Morado Development</h3>
              <p>Website created for Morado Development, a web agency in Summer of 2023.</p>
            </a>
          </div>
          <div class="project">
            <Carousel>
              <img src="/project-screenshots/designspace-1.png" alt="project screenshot"/>
              <img src="/project-screenshots/designspace-2.png" alt="project screenshot"/>
              <img src="/project-screenshots/designspace-3.png" alt="project screenshot"/>
            </Carousel>
            <a class="project-info" href="//designspace.vercel.app" target="_blank">
              <h3>Design Space</h3>
              <p>Artificial intelligence design thinking web app created in Winter of 2023.</p>
            </a>
          </div>
          <div class="project">
            <Carousel>
              <img src="/project-screenshots/habitual-2.png" alt="project screenshot"/>
              <img src="/project-screenshots/habitual-1.png" alt="project screenshot"/>
              <img src="/project-screenshots/habitual-3.png" alt="project screenshot"/>
            </Carousel>
            <a class="project-info" href="//habitual.studio" target="_blank">
              <h3>Habitual Studio</h3>
              <p>Website for Habitual Studio, a digital agency. Created in Fall of 2023.</p>
            </a>
          </div>
        </div>
      </div>
    {:else}
      <div class="selector">
        <h2>My Work</h2>
        <div class="projects">
          <a class="project" href="//mora.do" target="_blank" on:mouseover={() => {hoveredProject = 1}} on:focus={() => {hoveredProject = 1}}>
            <h3>Morado Development</h3>
            <p>Website created for Morado Development, a web agency in Summer of 2023.</p>
          </a>
          <a class="project" href="//designspace.vercel.app" target="_blank" on:mouseover={() => {hoveredProject = 2}} on:focus={() => {hoveredProject = 2}}>
            <h3>Design Space</h3>
            <p>Artificial intelligence design thinking web app created in Winter of 2023.</p>
          </a>
          <a class="project" href="//habitual.studio" target="_blank" on:mouseover={() => {hoveredProject = 3}} on:focus={() => {hoveredProject = 3}}>
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
        <img class="display" src="/assets/pro-display-xdr.png" alt="apple pro display XDR monitor (decorational)"/>
        <div class="screen">
          <div class="images">
            <Carousel>
              <img src="/project-screenshots/morado-1.webp" alt="project screenshot"/>
              <img src="/project-screenshots/morado-2.webp" alt="project screenshot"/>
              <img src="/project-screenshots/morado-3.webp" alt="project screenshot"/>
            </Carousel>
            <Carousel>
              <img src="/project-screenshots/designspace-1.webp" alt="project screenshot"/>
              <img src="/project-screenshots/designspace-2.webp" alt="project screenshot"/>
              <img src="/project-screenshots/designspace-3.webp" alt="project screenshot"/>
            </Carousel>
            <Carousel>
              <img src="/project-screenshots/habitual-1.webp" alt="project screenshot"/>
              <img src="/project-screenshots/habitual-2.webp" alt="project screenshot"/>
              <img src="/project-screenshots/habitual-3.webp" alt="project screenshot"/>
            </Carousel>
          </div>
        </div>
      </div>
    {/if}
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

<footer class="footer">
  <div class="footer-left">
    <h3>Sam Cheng</h3>
    <a href="mailto:sam@samalander.dev" target="_blank">sam@samalander.dev</a>
  </div>
  <div class="footer-right">
    <a href="https://github.com/Samalander0/newsite2024" target="_blank">Source code for this site</a>
    <div class="footer-socials">
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
  </div>
</footer>