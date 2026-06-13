<script lang="ts">
  import { onMount } from "svelte";
  import Skills from "$lib/components/Skills.svelte";
  import SectionHead from "$lib/components/SectionHead.svelte";
  import Projects from "$lib/components/Projects.svelte";

  import svelteIcon from "$lib/assets/svelte-16.svg?raw";
  import angularIcon from "$lib/assets/angular-16.svg?raw";
  import blazorIcon from "$lib/assets/blazor.svg?raw";
  import reactIcon from "$lib/assets/react-16.svg?raw";
  import mssqlIcon from "$lib/assets/database.svg?raw";
  import postgresIcon from "$lib/assets/postgresql.svg?raw";
  import dotnetIcon from "$lib/assets/dotnet.svg?raw";
  import typescriptIcon from "$lib/assets/typescript-16.svg?raw";

  import project1Img from "$lib/assets/img/bracketgame.png";

  const red = "var(--red)";

  let navOpen = $state(false);

  function toggleNav() {
    navOpen = !navOpen;
  }

  function closeNav() {
    navOpen = false;
  }

  onMount(() => {
    const sections = document.querySelectorAll("section");
    const navA = document.querySelectorAll(".navstack a");

    function updateActiveNav() {
      const viewportMid =
        (window.innerHeight || document.documentElement.clientHeight) / 4;
      let closestDist = Infinity;
      let activeSection: string | null = null;

      sections.forEach((section) => {
        const rect = section.getBoundingClientRect();
        if (
          rect.bottom < 0 ||
          rect.top >
            (window.innerHeight || document.documentElement.clientHeight)
        )
          return;
        const sectionMid = (rect.top + rect.bottom) / 2;
        const dist = Math.abs(sectionMid - viewportMid);
        if (dist < closestDist) {
          closestDist = dist;
          activeSection = section.getAttribute("id");
        }
      });

      navA.forEach((a) => {
        a.classList.remove("active");
        if (activeSection && a.getAttribute("href") === `#${activeSection}`) {
          a.classList.add("active");
        }
      });
    }

    window.addEventListener("scroll", updateActiveNav);
    window.addEventListener("resize", updateActiveNav);
    updateActiveNav();
  });
</script>

<div class="navstack">
  <button class="nav-toggle" onclick={toggleNav} aria-label="Toggle navigation">
    <svg
      class="nav-arrow"
      class:open={navOpen}
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        d="M9 18L15 12L9 6"
        stroke="var(--red)"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
      />
    </svg>
  </button>
  <nav class:open={navOpen}>
    <div class="navinner">
      <a href="#home" class="active" onclick={closeNav}>Home</a>
      <a href="#skills" onclick={closeNav}>Skills</a>
      <a href="#projects" onclick={closeNav}>Projects</a>
      <a href="#experience" onclick={closeNav}>Experience</a>
      <a href="#education" onclick={closeNav}>Education</a>
      <a href="#about" onclick={closeNav}>About</a>
      <a href="#contact" onclick={closeNav}>Contact</a>
    </div>
  </nav>
</div>

<section class="home" id="home">
  <div class="topbar">
    <div class="brand">
      <span class="dot">●</span> Cas Colucci | Portfolio
      <div>2026 · Florida, USA</div>
    </div>
  </div>
  <div class="inner">
    <div class="eyebrow">
      <span class="marker">●</span> &nbsp;Available for freelance — June 2026
    </div>
    <h1 class="geom-regular">
      <span class="red">C</span>as <span class="red">C</span>olucci
    </h1>
    <h2 class="tagline | cardo-italic">
      Full Stack Web Developer building <span class="accent"
        >durable, maintainable
      </span> software — .NET back-ends, modern front-ends, and the quiet plumbing
      in between.
    </h2>
  </div>
  <div class="lower">
    <div class="col">
      <span class="label">Currently</span>
      <span>Independent · taking on new work</span>
    </div>
    <div class="col">
      <span class="label">Stack</span>
      <span>.NET · Svelte · Postgres</span>
    </div>
  </div>
  <div class="scroll-cue">
    <span>Scroll</span>
    <div class="arrow"></div>
  </div>
</section>
<section class="skills navy" id="skills">
  <SectionHead
    number="01 - Skills"
    title="Tools of the Trade"
    meta="Daily Drivers"
  />
  <hr />
  <div class="skills-container">
    <Skills
      skill="Svelte"
      kind="Front-End Framework"
      num="01"
      iconsrc={svelteIcon}
    />
    <Skills
      skill="Angular"
      kind="Front-End Framework"
      num="02"
      iconsrc={angularIcon}
    />
    <Skills skill="Blazor" kind=".NET Web UI" num="03" iconsrc={blazorIcon} />
    <Skills
      skill="React"
      kind="Front-End Library"
      num="04"
      iconsrc={reactIcon}
    />
    <Skills
      skill="MSSQL"
      kind="Relational Database"
      num="05"
      iconsrc={mssqlIcon}
    />
    <Skills
      skill="PostgreSQL"
      kind="Relational Database"
      num="06"
      iconsrc={postgresIcon}
    />
    <Skills
      skill="C#/.NET"
      kind="Back-End Platform"
      num="07"
      iconsrc={dotnetIcon}
    />
    <Skills
      skill="TypeScript"
      kind="Typed Javascript"
      num="08"
      iconsrc={typescriptIcon}
    />
  </div>
</section>
<div class="cream-bg">
  <section class="projects" id="projects">
    <SectionHead
      number="02 - Projects"
      title="Selected Work"
      meta="A small, growing list"
      inverted={true}
    />
    <div class="projects-container">
      <Projects
        title="Golly's Bracket Game"
        tagline="Real-time, March-Madness-style bracket lobbies built with .NET, React and SignalR."
        description="A .NET and React project, utilizing PostgreSQL and Entity Framework Core for the database functions, and SignalR for real-time communication."
        projectImg={project1Img}
        modalImages={[project1Img]}
        modalDescription=""
        techStack={[
          ".NET",
          "React",
          "PostgreSQL",
          "Entity Framework Core",
          "SignalR",
        ]}
        liveLink=""
        repoLink="https://github.com/CasColucci/BracketGame"
      />
      <Projects isEmpty={true} />
    </div>
  </section>
  <section class="experience" id="experience">
    <div class="panel" aria-hidden="true"></div>
    <div class="content">
      <div class="head experience-head">
        <SectionHead
          number="03 - Experience"
          title="Where I've Shipped"
          meta="2021-present"
        />
      </div>
      <hr class="rule" />
      <div class="jobs">
        <div class="job">
          <div class="job-left-section">
            <h3 class="role">Software Engineer</h3>
            <div class="job-info">
              <span class="dates">11/24 <span class="red">-</span> 05/26</span>
              <div class="company-info">
                <span class="company">System Innovators</span>
                <span class="where">Jacksonville, FL</span>
              </div>
            </div>
          </div>
          <ul class="tech job-right-section">
            <li>C#</li>
            <li>.NET Framework</li>
            <li>Blazor</li>
            <li>Docker</li>
            <li>SQL</li>
          </ul>
        </div>
        <div class="detail">
          <ul class="points">
            <li>
              Maintained and enhanced the AMP (Admin Management Portal) within
              the iNovah enterprise revenue management system, supporting
              cashiering and payments operations for government and commercial
              clients across the United States and Canada
            </li>
            <li>
              Diagnosed and resolved long-standing production bugs in a legacy
              .NET Framework 4.8 codebase spanning 130+ interconnected projects
            </li>
            <li>
              Improved team documentation and authored transition materials
              supporting the team's migration from TFVC to Git version control
            </li>
          </ul>
        </div>
        <div class="job">
          <div class="job-left-section">
            <h3 class="role">Software Engineer</h3>
            <div class="job-info">
              <span class="dates">11/21 <span class="red">-</span> 09/24</span>
              <div class="company-info">
                <span class="company">BAM Technologies</span>
                <span class="where">Arlington, VA</span>
              </div>
            </div>
          </div>
          <ul class="tech job-right-section">
            <li>C#</li>
            <li>.NET 8</li>
            <li>Angular</li>
            <li>Entity Framework</li>
            <li>SQL</li>
          </ul>
        </div>
        <div class="detail">
          <ul class="points">
            <li>
              Built and maintained full-stack features for the MyCAA Scholarship
              platform, a nationally-deployed government application serving
              military spouses nationwide, using .NET Core 8 and Angular
            </li>
            <li>
              Designed and optimized SQL Server database queries and schema to
              support platform performance and reliability
            </li>
            <li>
              Managed CI/CD deployments via Octopus Deploy and TeamCity,
              maintaining stable production releases across environments
            </li>
            <li>
              Collaborated in a cross-functional Scrum team, conducting code
              reviews and implementing comprehensive testing practices
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</div>
<div class="triangle-divider">
  <svg
    data-name="Layer 1"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 1200 120"
    preserveAspectRatio="none"
  >
    <path d="M1200 0L0 0 598.97 114.72 1200 0z" class="shape-fill"></path>
  </svg>
</div>
<section class="education" id="education">
  <SectionHead number="04" title="Education" />
  <hr />
  <div class="school">
    <div class="school-details">
      <h3 class="school-name">Stetson University</h3>
      <h3 class="degree">Bachelor of Science | Computer Science</h3>
    </div>
    <p class="school-description">
      Computer Science Club <span class="red">-</span> Event Coordinator
    </p>
    <p class="school-description">
      Senior Project <span class="red">-</span> Bot Activity Analysis: Analyzed bot
      prevalence and engagement on social media by making a web scraper and data
      analysis program. It would gather posts from suspected bot accounts, and compare
      interactions to those by non-bot accounts, looking for trends.
    </p>
  </div>
  <div class="school">
    <div class="school-details">
      <h3 class="school-name">Daytona State College</h3>
      <h3 class="degree">Associate of Arts | Quanta-Honors College</h3>
    </div>
    <p class="school-description">
      Quanta-Honors <span class="red">-</span> Led varied, research-intensive projects
      from concept through execution, becoming skilled with seeing projects through
      from conception to completion.
    </p>
  </div>
</section>
<section class="about" id="about">
  <SectionHead
    number="05 - About"
    title="A bit about me"
    meta="The short version"
  />
</section>
<section class="contact" id="contact">
  <SectionHead number="05" title="Contact" />
  <hr />
  <div class="contact">
    <form class="contact-form" method="POST" data-netlify="true" name="contact">
      <label for="name">Name</label>
      <input type="text" id="name" name="name" placeholder="Name" required />

      <label for="email">Email</label>
      <input
        type="email"
        id="email"
        name="email"
        placeholder="Email"
        required
      />

      <label for="subject">Subject</label>
      <input
        type="text"
        id="subject"
        name="subject"
        placeholder="Subject"
        required
      />

      <label for="message">Message</label>
      <textarea
        id="message"
        name="message"
        rows="5"
        placeholder="Message"
        required
      ></textarea>

      <button type="submit">Send</button>
    </form>
  </div>
</section>
<section class="footer">
  <hr />
  <div class="links">
    <a
      href="https://github.com/cascolucci"
      aria-label="GitHub Profile"
      target="_blank"
      rel="noopener noreferrer"
    >
      <svg
        fill={red}
        width="100px"
        height="100px"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g data-name="Layer 2">
          <rect
            width="24"
            height="24"
            transform="rotate(180 12 12)"
            opacity="0"
          />
          <path
            d="M12 1A10.89 10.89 0 0 0 1 11.77 10.79 10.79 0 0 0 8.52 22c.55.1.75-.23.75-.52v-1.83c-3.06.65-3.71-1.44-3.71-1.44a2.86 2.86 0 0 0-1.22-1.58c-1-.66.08-.65.08-.65a2.31 2.31 0 0 1 1.68 1.11 2.37 2.37 0 0 0 3.2.89 2.33 2.33 0 0 1 .7-1.44c-2.44-.27-5-1.19-5-5.32a4.15 4.15 0 0 1 1.11-2.91 3.78 3.78 0 0 1 .11-2.84s.93-.29 3 1.1a10.68 10.68 0 0 1 5.5 0c2.1-1.39 3-1.1 3-1.1a3.78 3.78 0 0 1 .11 2.84A4.15 4.15 0 0 1 19 11.2c0 4.14-2.58 5.05-5 5.32a2.5 2.5 0 0 1 .75 2v2.95c0 .35.2.63.75.52A10.8 10.8 0 0 0 23 11.77 10.89 10.89 0 0 0 12 1"
            data-name="github"
          />
        </g>
      </svg>
    </a>
    <a
      href="https://www.linkedin.com/in/cassia-colucci/"
      aria-label="LinkedIn Profile"
      target="_blank"
      rel="noopener noreferrer"
    >
      <svg
        width="100px"
        height="100px"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M6.5 8C7.32843 8 8 7.32843 8 6.5C8 5.67157 7.32843 5 6.5 5C5.67157 5 5 5.67157 5 6.5C5 7.32843 5.67157 8 6.5 8Z"
          fill={red}
        />
        <path
          d="M5 10C5 9.44772 5.44772 9 6 9H7C7.55228 9 8 9.44771 8 10V18C8 18.5523 7.55228 19 7 19H6C5.44772 19 5 18.5523 5 18V10Z"
          fill={red}
        />
        <path
          d="M11 19H12C12.5523 19 13 18.5523 13 18V13.5C13 12 16 11 16 13V18.0004C16 18.5527 16.4477 19 17 19H18C18.5523 19 19 18.5523 19 18V12C19 10 17.5 9 15.5 9C13.5 9 13 10.5 13 10.5V10C13 9.44771 12.5523 9 12 9H11C10.4477 9 10 9.44772 10 10V18C10 18.5523 10.4477 19 11 19Z"
          fill={red}
        />
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M20 1C21.6569 1 23 2.34315 23 4V20C23 21.6569 21.6569 23 20 23H4C2.34315 23 1 21.6569 1 20V4C1 2.34315 2.34315 1 4 1H20ZM20 3C20.5523 3 21 3.44772 21 4V20C21 20.5523 20.5523 21 20 21H4C3.44772 21 3 20.5523 3 20V4C3 3.44772 3.44772 3 4 3H20Z"
          fill={red}
        />
      </svg>
    </a>
  </div>
  <footer>
    <p>
      Designed and built by <span class="red">C</span>as
      <span class="red">C</span>olucci <span class="red">© 2026</span>
    </p>
  </footer>
</section>

<style>
  :root {
    --experienceSectionLeftPanelWidth: 30%;
  }

  .navstack {
    position: fixed;
    right: 0;
    top: 0;
    height: 100vh;
    width: 200px;
    z-index: 50;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    justify-content: center;
    pointer-events: none;
    mix-blend-mode: difference;
  }

  /* Navigation that is sticky to right */
  nav {
    display: flex;
    flex-direction: column;

    .navinner {
      pointer-events: auto;
      padding: 24px 32px 24px 22px;
      border-left: 1px solid #ffffff20;
      display: flex;
      flex-direction: column;
      gap: 12px;
      font-family: var(--serif);
      font-style: italic;
      font-size: 17px;
    }

    a {
      color: #c8c8c8;
      text-decoration: none;
      display: flex;
      align-items: center;
      gap: 8px;
      letter-spacing: 0.01em;
      transition: color 0.2s ease;
    }

    a::before {
      content: ">";
      height: 17px;
      color: var(--red);
      opacity: 0;
      transition: opacity 0.2s ease;
      display: inline-block;
      line-height: 15px;
    }
  }

  nav a.active {
    color: var(--red);
  }
  nav a.active::before {
    opacity: 1;
  }

  .nav-toggle {
    display: none;
    pointer-events: auto;
    background-color: var(--dark-blue);
    border: 1px solid var(--red);
    border-radius: 50%;
    cursor: pointer;
    padding: 8px;
    width: 44px;
    height: 44px;
    align-items: center;
    justify-content: center;
    position: fixed;
    right: 5vw;
    top: 50%;
    transform: translateY(-50%);
    z-index: 101;
  }

  .nav-arrow {
    transition: transform 0.3s ease;
    transform: rotate(0deg);
  }

  .nav-arrow.open {
    transform: rotate(90deg);
  }

  @media (max-width: 1000px) {
    .navstack {
      mix-blend-mode: normal;
    }

    .nav-toggle {
      display: flex;
    }

    nav {
      position: fixed;
      top: 0;
      right: 0;
      height: 100vh;
      background-color: var(--dark-blue);
      border-left: 3px solid var(--red);
      padding: 80px 50px 40px 40px;
      transform: translateX(100%);
      transition: transform 0.3s ease;
      align-items: flex-start;
      gap: 0;
    }

    nav.open {
      transform: translateX(0);
    }

    nav a {
      width: 100%;
      border-bottom: 1px solid color-mix(in srgb, var(--red) 30%, transparent);
      padding: 6px 0;
      align-self: flex-start;
      font-size: 23px !important;
    }

    nav a:first-child {
      border-top: 1px solid color-mix(in srgb, var(--red) 30%, transparent);
    }
  }

  section {
    position: relative;
    padding: 140px 240px 160px 96px;
    overflow: hidden;
  }

  @media (max-width: 1000px) {
    section {
      padding: 140px 160px 96px;
    }
  }

  section.cream {
    background: var(--cream);
    color: var(--ink);
  }
  section.navy {
    background: var(--navy);
    color: var(--cream);
  }
  section.cream-alt {
    background: var(--cream-2);
    color: var(--ink);
  }

  .home {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: var(--cream);
    .topbar {
      position: absolute;
      top: 36px;
      left: 96px;
      right: 240px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-family: var(--mono);
      font-size: 11px;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      opacity: 0.55;
    }

    .topbar .brand {
      color: var(--cream);
      opacity: 1;
    }

    .topbar .brand .dot {
      color: var(--red);
      margin-right: 6px;
    }

    .inner {
      max-width: 1100px;
      margin: 0 auto;
      text-align: left;
    }

    .inner .eyebrow {
      font-family: var(--mono);
      font-size: 11px;
      letter-spacing: 0.28em;
      text-transform: uppercase;
      color: var(--cream);
      opacity: 0.55;
      margin-bottom: 28px;

      .marker {
        color: var(--red);
        opacity: 1;
      }
    }

    h1 {
      font-family: var(--display);
      font-weight: 700;
      font-size: clamp(72px, 11vw, 168px);
      line-height: 0.92;
      letter-spacing: -0.045em;
      margin: 0;
      color: var(--cream);
    }

    h2 {
      font-family: var(--serif);
      font-style: italic;
      font-weight: 400;
      letter-spacing: -0.02em;
    }

    .tagline {
      margin-top: 36px;
      font-family: var(--serif);
      font-style: italic;
      font-size: clamp(20px, 2vw, 26px);
      line-height: 1.35;
      color: var(--cream);
      opacity: 0.85;
      max-width: 640px;
    }

    .tagline .accent {
      color: var(--red);
      font-style: normal;
    }

    hr {
      width: 32%;
    }

    .lower {
      position: absolute;
      left: 96px;
      right: 240px;
      bottom: 56px;
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      gap: 24px;
      font-family: var(--mono);
      font-size: 11px;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      opacity: 0.55;
    }

    .lower .col {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }
    .lower .col .label {
      color: var(--red);
      opacity: 1;
    }
    .scroll-cue {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      bottom: 32px;
      display: flex;
      align-items: center;
      gap: 10px;
      color: var(--cream);
      opacity: 0.5;
      font-family: var(--mono);
      font-size: 10px;
      letter-spacing: 0.3em;
      text-transform: uppercase;

      .arrow {
        width: 1px;
        height: 28px;
        background: currentColor;
        position: relative;
      }

      .arrow::after {
        content: "";
        position: absolute;
        bottom: 0;
        left: -3px;
        width: 7px;
        height: 7px;
        border-right: 1px solid currentColor;
        border-bottom: 1px solid currentColor;
        transform: rotate(45deg);
        transform-origin: center;
        top: auto;
      }
    }
  }

  .red {
    color: var(--red);
  }

  hr {
    border: 1px solid var(--red);
    margin: 20px auto;
    width: 100%;
  }

  .vertical-center {
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .skills-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    background: var(--ink);
    opacity: 0.96;
    border: 1px solid #ffffff20;
  }

  .cream-bg {
    background-color: var(--cream-2);
  }

  .projects-container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 36px;
  }

  .experience {
    position: relative;
    margin: 0 auto;
    color: var(--dark-blue);
    container-type: inline-size;
  }

  .panel {
    position: absolute;
    inset: 0 auto 10% 0;
    width: var(--experienceSectionLeftPanelWidth);
    background-color: var(--dark-blue);
    z-index: 1;
  }

  .content {
    position: relative;
    z-index: 2;
    display: flex;
    flex-direction: column;
    min-height: 100%;
    padding-bottom: 10vh;
  }

  .head {
    max-width: var(--experienceSectionLeftPanelWidth);
    margin-left: 1%;
    width: 22vw;
  }

  .rule {
    width: 100%;
    border: 0;
    height: 2px;
    background-color: var(--red);
  }

  .jobs {
    flex: 1;
    display: grid;
    grid-template-columns: auto auto;
    align-items: start;
    align-content: start;
    row-gap: 3.6cqw;
    padding-top: 3cqw;
  }

  .job {
    padding: 1.8cqw 0;
  }

  .role {
    padding: 0 1.8cqw 0 3.2cqw;
    margin: 0;
    font-size: 32px;
    color: var(--white);
    font-family: var(--display);
  }

  .job-info {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 10px;
    padding: 0 3.2cqw;
    color: var(--white);
    font-family: var(--serif-italic);
    font-style: italic;
    font-size: 20px;
    width: 22vw;
  }

  .company-info {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .where {
    color: var(--red);
  }

  .tech {
    margin: 0;
    padding: 0;
    list-style: none;
    font-style: italic;
  }

  .tech li {
    position: relative;
    padding-left: 20px;
    margin-left: 3.5cqw;
    color: var(--white);
    font-family: var(--serif-italic);
    font-size: 20px;
  }

  .tech li::before {
    content: ">";
    position: absolute;
    left: 0;
    color: var(--red);
    font-weight: bold;
    font-size: 20px;
    font-family: var(--display);
  }

  .detail {
    padding: 0 3.2cqw;
  }

  .points {
    margin: 0;
    padding: 1.8cqw 0;
    list-style: none;
  }

  .points li {
    position: relative;
    padding-top: 1.8cqw;
    padding-left: 20px;
    font-size: 20px;
  }
  .points li::before {
    content: ">";
    position: absolute;
    left: 0;
    color: var(--red);
    font-weight: bold;
    font-size: 20px;
    font-family: var(--display);
  }

  .shape-fill {
    fill: var(--cream-2);
  }

  .school {
    color: var(--white);
    padding: 50px;
  }

  .school-details {
    display: flex;
    justify-content: space-between;
    width: 100%;
  }

  .school-name {
    position: relative;
    font-family: var(--display);
    font-size: 32px;
    padding-left: 25px;
  }

  .school-name::before {
    content: ">";
    position: absolute;
    left: 0;
    color: var(--red);
    font-family: var(--display);
  }

  .degree {
    color: var(--dark-blue);
    background-color: var(--yellow);
    font-size: 32px;
    font-family: var(--display);
    font-weight: 400;
    width: 60%;
    text-align-last: right;
  }

  .school-description {
    font-size: 20px;
    font-family: var(--serif);
    margin-top: 20px;
    margin-left: 25px;
  }

  .school-description::before {
    content: ">";
    color: var(--red);
    font-family: var(--display);
    margin-right: 10px;
  }

  .contact-form {
    color: var(--white);
  }

  label {
    display: block;
    margin-bottom: 5px;
    font-family: var(--display);
    font-size: 20px;
  }

  input {
    width: 50%;
    padding: 10px;
    margin-bottom: 20px;
    background-color: var(--white);
    color: var(--dark-blue);
    font-family: var(--serif);
  }

  textarea {
    width: 50%;
    padding: 10px;
    margin-bottom: 20px;
    background-color: var(--white);
    color: var(--dark-blue);
    resize: none;
  }

  .contact-form button {
    padding: 10px 20px;
    background-color: var(--red);
    color: var(--white);
    border: none;
    cursor: pointer;
    font-family: var(--display);
    display: block;
    width: 50%;
  }

  footer {
    text-align: center;
    padding: 20px 0;
    color: var(--white);
    font-family: var(--display);
    font-size: 24px;
  }

  .footer {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .links {
    display: flex;
    flex-direction: row;
  }

  .links a {
    cursor: pointer;
  }

  @media (max-width: 1300px) {
    .role {
      font-size: 28px;
      text-wrap: wrap;
      max-width: var(--experienceSectionLeftPanelWidth);
    }

    .school-details h3 {
      font-size: 28px;
    }
  }

  @media (max-width: 1122px) {
    .school-details h3 {
      font-size: 20px;
    }
  }
  @media (max-width: 960px) {
    .skills-container {
      grid-template-columns: repeat(2, 1fr);
    }
    .experience-head {
      --section-head-color: var(--dark-blue);
    }

    .panel {
      display: none;
    }

    .experience {
      position: relative;
    }

    .job {
      display: flex;
      flex-direction: row;
      background-color: var(--dark-blue);
      width: 100%;
      z-index: 1;
    }

    .tech {
      margin-top: 50px;
    }

    .jobs .role {
      max-width: 100%;
    }
    .head {
      max-width: 100%;
      width: 100%;
    }

    .jobs {
      display: flex;
      flex-direction: column;
    }

    input,
    textarea,
    .contact-form button {
      width: 100%;
    }
  }

  @media (max-width: 838px) {
    .school-details h3 {
      text-align-last: left;
    }

    .school-details {
      flex-direction: column;
    }

    .degree {
      width: 100%;
    }
  }

  @media (max-width: 700px) {
    section {
      padding: 80px 22px 88px;
    }

    .skills-container {
      grid-template-columns: 1fr;
    }
  }
</style>
