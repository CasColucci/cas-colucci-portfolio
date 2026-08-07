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

  const EXPERIENCE = [
    {
      company: "System Innovators",
      place: "Jacksonville, FL",
      dates: "Nov 2024 — May 2026",
      duration: "1 yr 6 mo",
      role: "Software Engineer",
      stack: ["C#", ".NET Framework", "Blazor", "SQL Server"],
      bullets: [
        "Maintained and enhanced the AMP (Admin Management Portal) within the iNovah enterprise revenue management system, supporting cashiering and payments operations for government and commercial clients across the United States and Canada.",
        "Diagnosed and resolved long-standing production bugs in a legacy .NET Framework 4.8 codebase spanning 130+ interconnected projects.",
        "Improved team documentation and authored transition materials supporting the team's migration from TFVC to Git version control.",
      ],
    },
    {
      company: "BAM Technologies",
      place: "Arlington, VA",
      dates: "Nov 2021 — Sep 2024",
      duration: "2 yr 10 mo",
      role: "Software Engineer",
      stack: ["C#", ".NET 8", "Angular", "Entity Framework", "SQL Server"],
      bullets: [
        "Built and maintained full-stack features for the MyCAA Scholarship platform, a nationally-deployed government application serving military spouses, using .NET Core 8 and Angular.",
        "Designed and optimized SQL Server queries and schema to support platform performance and reliability.",
        "Managed CI/CD deployments via Octopus Deploy and TeamCity, maintaining stable production releases across environments.",
        "Collaborated in a cross-functional Scrum team, conducting code reviews and implementing comprehensive testing practices.",
      ],
    },
  ];

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
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
  </svg>
</button>
<div class="navstack">
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
      <span class="marker">●</span> &nbsp;Available for freelance — August 2026
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
<section class="skills dark-blue" id="skills">
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
  <section class="jobs dark-blue" id="experience">
    <SectionHead
      number="03 - Experience"
      title="Where I've Shipped"
      meta="2021-present"
    />
    <div class="jobs">
      {#each EXPERIENCE as x}
        <div class="xp-row">
          <div class="date">
            {x.dates}
            <span class="dur">{x.duration}</span>
          </div>
          <div class="role-block">
            <div class="head">
              <h3>{x.company}</h3>
              <div class="place">{x.place}</div>
            </div>
            <div class="role-title">{x.role}</div>
            <div class="stack">
              {#each x.stack as chip}
                <span class="chip">{chip}</span>
              {/each}
            </div>
            <ul>
              {#each x.bullets as bullet}
                <li>{bullet}</li>
              {/each}
            </ul>
          </div>
        </div>
      {/each}
    </div>
  </section>
</div>
<section class="education cream-alt" id="education">
  <SectionHead
    number="04 - Education"
    title="School & Study"
    meta="Florida"
    inverted={true}
  />
  <div class="schools">
    <div class="school">
      <div class="degree">B.S. | Computer Science</div>
      <h3 class="school-name">Stetson University</h3>
      <div class="where">DeLand, FL</div>
      <ul>
        <li class="school-description">
          Computer Science Club <span class="red">-</span> Event Coordinator
        </li>
        <li class="school-description">
          Senior project on bot activity analysis <span class="red">-</span> a web
          scraper and data pipeline comparing engagement patterns between suspected
          bot and non-bot accounts on social media.
        </li>
      </ul>
    </div>
    <div class="school">
      <div class="degree">A.A. | Quanta-Honors College</div>
      <h3 class="school-name">Daytona State College</h3>
      <div class="where">Daytona Beach, FL</div>
      <ul>
        <li class="school-description">
          Quanta-Honors <span class="red">-</span> Led varied, research-intensive
          projects from concept through execution, becoming skilled with seeing projects
          through from conception to completion.
        </li>
      </ul>
    </div>
  </div>
</section>
<section class="about" id="about">
  <SectionHead
    number="05 - About"
    title="A bit about me"
    meta="The short version"
  />
  <div class="about-grid">
    <div class="about-body">
      <p>
        I'm a full-stack developer specializing in C#/.NET, with five years of
        experience across legacy enterprise systems and custom client work built
        from scratch. At my core, I'm a puzzle solver — I spend my time trying
        to logic my way through a problem, and I care a lot about making the
        right shaped thing for the space.
      </p>
      <p>
        That shows up in how I write code. Good software, to me, strikes a
        balance: general enough to be reused when it makes sense, specific
        enough to actually do the job. It should be readable, logical, and
        satisfying to look at. I've spent a lot of my career inside a
        large-scale .NET codebase in the payments domain, which gave me a lot of
        practice writing code that the next developer can actually work with —
        not just code that works today.
      </p>
      <p>
        Outside of development, I'm a maker in other ways too: games, <a
          class="quiet-link"
          href="http://zegollygosh.com"
        >
          writing</a
        >, creative projects. It's the same instinct, just different materials.
      </p>
    </div>

    <aside class="about-side">
      <div class="about-fact">
        <div class="label">Based</div>
        <div class="value">Florida, USA</div>
      </div>
      <div class="about-fact">
        <div class="label">Working</div>
        <div class="value">Remote · UTC−5</div>
      </div>
      <div class="about-fact">
        <div class="label">Status</div>
        <div class="value">Booking new work</div>
      </div>
      <div class="about-fact">
        <div class="label">Writing</div>
        <div class="value">
          <a class="quiet-link" href="http://zegollygosh.com">zegollygosh.com</a
          >
        </div>
      </div>
    </aside>
  </div>
</section>
<section
  data-section="contact"
  data-screen-label="Contact"
  class="cream"
  id="contact"
>
  <SectionHead
    number="05 - Contact"
    title="Let's Talk!"
    meta="Normally replies within a day"
    inverted={true}
  />

  <div class="contact-wrap">
    <div class="contact-blurb">
      <h3>
        Got something<br />
        that needs <span class="ital">building?</span>
      </h3>
      <p>
        I take on freelance full-stack work. Front-end designs, back-end
        systems, database design, and the unglamorous middle bits that keep apps
        running quietly.
      </p>
      <div class="info">
        <a href="mailto:cas@cascolucci.com">
          <span class="label">Email</span>
          <svg
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M4 7.00005L10.2 11.65C11.2667 12.45 12.7333 12.45 13.8 11.65L20 7"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <rect
              x="3"
              y="5"
              width="18"
              height="14"
              rx="2"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
            />
          </svg> <span>cas@cascolucci.com</span>
        </a>
        <a href="http://github.com/cascolucci">
          <span class="label">GitHub</span>
          <svg
            fill="currentColor"
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
          </svg> <span>github.com/cascolucci</span>
        </a>
        <a href="#">
          <span class="label">LinkedIn</span>
          <svg
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M6.5 8C7.32843 8 8 7.32843 8 6.5C8 5.67157 7.32843 5 6.5 5C5.67157 5 5 5.67157 5 6.5C5 7.32843 5.67157 8 6.5 8Z"
              fill="currentColor"
            />
            <path
              d="M5 10C5 9.44772 5.44772 9 6 9H7C7.55228 9 8 9.44771 8 10V18C8 18.5523 7.55228 19 7 19H6C5.44772 19 5 18.5523 5 18V10Z"
              fill="currentColor"
            />
            <path
              d="M11 19H12C12.5523 19 13 18.5523 13 18V13.5C13 12 16 11 16 13V18.0004C16 18.5527 16.4477 19 17 19H18C18.5523 19 19 18.5523 19 18V12C19 10 17.5 9 15.5 9C13.5 9 13 10.5 13 10.5V10C13 9.44771 12.5523 9 12 9H11C10.4477 9 10 9.44772 10 10V18C10 18.5523 10.4477 19 11 19Z"
              fill="currentColor"
            />
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M20 1C21.6569 1 23 2.34315 23 4V20C23 21.6569 21.6569 23 20 23H4C2.34315 23 1 21.6569 1 20V4C1 2.34315 2.34315 1 4 1H20ZM20 3C20.5523 3 21 3.44772 21 4V20C21 20.5523 20.5523 21 20 21H4C3.44772 21 3 20.5523 3 20V4C3 3.44772 3.44772 3 4 3H20Z"
              fill="currentColor"
            />
          </svg> <span>linkedin.com/in/cascolucci</span>
        </a>
      </div>
    </div>

    <form class="contact-form" method="POST" data-netlify="true" name="contact">
      <div class="field">
        <label>Name</label>
        <input type="text" required placeholder="Your name" />
      </div>
      <div class="field">
        <label>Email</label>
        <input type="email" required placeholder="you@company.com" />
      </div>
      <div class="field">
        <label>Subject</label>
        <input type="text" required placeholder="What's the project?" />
      </div>
      <div class="field">
        <label>Message</label>
        <textarea rows={5} required placeholder="Tell me about it…" />
      </div>
      <button class="submit" type="submit">Submit</button>
    </form>
  </div>
</section>
<footer>
  <div class="footer-wrap">
    <div class="signoff">
      <span class="period">C</span>as <span class="period">C</span>olucci
    </div>
    <div class="footer-social">
      <a href="http://github.com/cascolucci" aria-label="GitHub">
        <svg
          fill="currentColor"
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
        aria-label="LinkedIn"
        ><svg
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M6.5 8C7.32843 8 8 7.32843 8 6.5C8 5.67157 7.32843 5 6.5 5C5.67157 5 5 5.67157 5 6.5C5 7.32843 5.67157 8 6.5 8Z"
            fill="currentColor"
          />
          <path
            d="M5 10C5 9.44772 5.44772 9 6 9H7C7.55228 9 8 9.44771 8 10V18C8 18.5523 7.55228 19 7 19H6C5.44772 19 5 18.5523 5 18V10Z"
            fill="currentColor"
          />
          <path
            d="M11 19H12C12.5523 19 13 18.5523 13 18V13.5C13 12 16 11 16 13V18.0004C16 18.5527 16.4477 19 17 19H18C18.5523 19 19 18.5523 19 18V12C19 10 17.5 9 15.5 9C13.5 9 13 10.5 13 10.5V10C13 9.44771 12.5523 9 12 9H11C10.4477 9 10 9.44772 10 10V18C10 18.5523 10.4477 19 11 19Z"
            fill="currentColor"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M20 1C21.6569 1 23 2.34315 23 4V20C23 21.6569 21.6569 23 20 23H4C2.34315 23 1 21.6569 1 20V4C1 2.34315 2.34315 1 4 1H20ZM20 3C20.5523 3 21 3.44772 21 4V20C21 20.5523 20.5523 21 20 21H4C3.44772 21 3 20.5523 3 20V4C3 3.44772 3.44772 3 4 3H20Z"
            fill="currentColor"
          />
        </svg></a
      >
      <a href="mailto:cas@cascolucci.com" aria-label="Email"
        ><svg
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M4 7.00005L10.2 11.65C11.2667 12.45 12.7333 12.45 13.8 11.65L20 7"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
          <rect
            x="3"
            y="5"
            width="18"
            height="14"
            rx="2"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
          />
        </svg></a
      >
    </div>
  </div>
  <div class="copyright">
    <span>© 2026 Cas Colucci</span>
    <span>Designed &amp; built by Cas</span>
  </div>
</footer>

<style>
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
    background-color: transparent;
    border: 1px solid var(--red);
    color: var(--red);
    mix-blend-mode: difference;
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
  section.dark-blue {
    background: var(--dark-blue);
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

  .jobs {
    display: flex;
    flex-direction: column;
  }

  .xp-row {
    display: grid;
    grid-template-columns: 220px 1fr;
    gap: 56px;
    padding: 44px 0;
    border-top: 1px solid #ffffff18;
  }
  .xp-row:last-child {
    border-bottom: 1px solid #ffffff18;
  }
  .xp-row .date {
    font-family: var(--mono);
    font-size: 13px;
    letter-spacing: 0.04em;
    color: var(--cream);
  }
  .xp-row .date .dur {
    display: block;
    margin-top: 8px;
    font-size: 11px;
    color: #ffffff60;
    letter-spacing: 0.16em;
    text-transform: uppercase;
  }
  .xp-row .role-block .head {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    gap: 24px;
    margin-bottom: 6px;
  }
  .xp-row .role-block h3 {
    font-family: var(--display);
    font-weight: 600;
    font-size: 30px;
    letter-spacing: -0.02em;
    margin: 0;
    color: var(--cream);
  }
  .xp-row .role-block .place {
    font-family: var(--serif);
    font-style: italic;
    font-size: 16px;
    color: #ffffff70;
    text-align: right;
    white-space: nowrap;
  }
  .xp-row .role-block .role-title {
    font-family: var(--serif);
    font-style: italic;
    font-size: 18px;
    color: var(--red);
    margin-bottom: 18px;
  }
  .xp-row .role-block .stack {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-bottom: 20px;
  }
  .xp-row .role-block .stack .chip {
    font-family: var(--mono);
    font-size: 10px;
    padding: 3px 8px;
    border-color: #ffffff25;
    color: #ffffff85;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }
  .xp-row ul {
    margin: 0;
    padding: 0;
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 14px;
    max-width: 760px;
  }
  .xp-row li {
    font-family: var(--serif);
    font-size: 17px;
    line-height: 1.55;
    position: relative;
    padding-left: 22px;
    color: var(--cream);
    opacity: 0.92;
  }
  .xp-row li::before {
    content: "";
    position: absolute;
    left: 0;
    top: 12px;
    width: 8px;
    height: 1px;
    background: var(--red);
  }

  .schools {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 36px;
  }

  .school {
    background: var(--cream);
    border: 1px solid #1c314420;
    padding: 40px 36px 36px;
    position: relative;
  }

  .school-name {
    font-family: var(--display);
    font-weight: 600;
    font-size: 28px;
    letter-spacing: -0.02em;
    margin: 0 0 4px;
    color: var(--ink);
  }

  .degree {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 16px;
  }

  .school-description {
    font-size: 20px;
    font-family: var(--serif);
    margin-top: 20px;
    margin-left: 25px;
  }

  .school .where {
    font-family: var(--serif);
    font-style: italic;
    font-size: 16px;
    color: var(--muted);
    margin-bottom: 20px;
    padding-bottom: 20px;
    border-bottom: 1px solid #1c314420;
  }

  .school ul {
    padding: 0;
    margin: 0;
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 14px;
  }

  .school li {
    font-family: var(--serif);
    font-size: 16px;
    line-height: 1.55;
    padding-left: 22px;
    position: relative;
    color: var(--ink);
  }

  .school li::before {
    content: "";
    position: absolute;
    left: 0;
    top: 12px;
    width: 8px;
    height: 1px;
    background: var(--red);
  }

  .about-grid {
    display: grid;
    grid-template-columns: 1.4fr 1fr;
    gap: 96px;
    align-items: start;
  }

  .about-side {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--red);
    padding-top: 14px;
  }

  .about-body p {
    font-family: var(--serif);
    font-size: 19px;
    line-height: 1.55;
    margin: 0 0 22px;
    color: var(--cream);
    opacity: 0.88;
    max-width: 620px;
  }

  .about-body em {
    font-style: italic;
    color: var(--cream);
    opacity: 1;
    border-bottom: 1px solid var(--red);
    padding-bottom: 1px;
  }

  .quiet-link {
    color: inherit;
    text-decoration: none;
    border-bottom: 1px solid currentColor;
    opacity: 0.85;
    transition:
      opacity 0.18s ease,
      color 0.18s ease;
    padding-bottom: 1px;
  }

  .quiet-link:hover {
    color: var(--red);
    opacity: 1;
    border-bottom-color: var(--red);
  }

  .about-body p:last-child {
    margin-bottom: 0;
  }

  .about-side {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    background: #ffffff15;
    border: 1px solid #ffffff18;
  }

  .about-fact {
    background: var(--navy);
    padding: 22px 24px 24px;
  }

  .about-fact .label {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 10px;
  }

  .about-fact .value {
    font-family: var(--display);
    font-weight: 500;
    font-size: 17px;
    letter-spacing: -0.01em;
    color: var(--cream);
  }

  .about-fact .value a {
    color: inherit;
  }

  .info svg {
    width: 16px;
    height: 16px;
  }

  /* ------- contact ------- */
  .contact-wrap {
    display: grid;
    grid-template-columns: 1.1fr 1fr;
    gap: 96px;
    align-items: start;
  }
  .contact-blurb h3 {
    font-family: var(--display);
    font-weight: 700;
    font-size: clamp(44px, 5vw, 76px);
    line-height: 0.95;
    letter-spacing: -0.035em;
    margin: 0 0 28px;
  }
  .contact-blurb h3 .ital {
    font-family: var(--serif);
    font-style: italic;
    font-weight: 400;
    color: var(--red);
    letter-spacing: -0.02em;
  }
  .contact-blurb p {
    font-family: var(--serif);
    font-size: 18px;
    line-height: 1.5;
    margin: 0 0 32px;
    max-width: 440px;
    color: var(--ink);
    opacity: 0.85;
  }
  .contact-blurb .info {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }
  .contact-blurb .info a {
    display: grid;
    grid-template-columns: 72px 20px auto;
    gap: 14px;
    align-items: center;
    color: var(--ink);
    text-decoration: none;
    font-family: var(--mono);
    font-size: 13px;
    padding: 10px 0;
    border-bottom: 1px solid #1c314415;
    transition: color 0.18s ease;
  }
  .contact-blurb .info a:hover {
    color: var(--red);
  }
  .contact-blurb .info .label {
    color: var(--red);
    font-size: 10px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
  }

  .contact-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
  .field {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
  .field label {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
  }
  .field input,
  .field textarea {
    font: inherit;
    font-family: var(--serif);
    font-size: 17px;
    padding: 12px 0;
    background: transparent;
    border: none;
    border-bottom: 1px solid #1c314430;
    color: var(--ink);
    outline: none;
    transition: border-color 0.2s ease;
    resize: vertical;
  }
  .field input:focus,
  .field textarea:focus {
    border-bottom-color: var(--red);
  }
  .submit {
    background: var(--ink);
    color: var(--cream);
    border: none;
    padding: 18px 22px;
    font-family: var(--display);
    font-weight: 600;
    font-size: 15px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    margin-top: 12px;
    align-self: flex-start;
    transition: background 0.18s ease;
    display: inline-flex;
    align-items: center;
    gap: 12px;
    min-width: 220px;
    justify-content: center;
  }
  .submit:hover {
    background: var(--red);
  }

  footer {
    background: var(--navy);
    color: var(--cream);
    padding: 80px 240px 56px 96px;
  }
  .footer-wrap {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 24px;
    padding-bottom: 48px;
    border-bottom: 1px solid #ffffff15;
  }
  .footer-wrap .signoff {
    font-family: var(--display);
    font-weight: 700;
    font-size: clamp(36px, 4.5vw, 72px);
    letter-spacing: -0.035em;
    line-height: 1;
  }
  .footer-wrap .signoff .period {
    color: var(--red);
  }
  .footer-social {
    display: flex;
    gap: 18px;
  }
  .footer-social a {
    width: 44px;
    height: 44px;
    border-radius: 50%;
    border: 1px solid #ffffff30;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--cream);
    text-decoration: none;
    opacity: 0.7;
    transition:
      opacity 0.2s ease,
      border-color 0.2s ease,
      color 0.2s ease;
  }
  .footer-social a:hover {
    opacity: 1;
    border-color: var(--red);
    color: var(--red);
  }
  .copyright {
    margin-top: 32px;
    display: flex;
    justify-content: space-between;
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    opacity: 0.5;
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

  /* ============================================================
   RESPONSIVE — TABLET (≤ 960px)
   ============================================================ */
  @media (max-width: 960px) {
    /* the fixed topnav owns the brand now — hide the hero's own duplicate */
    .home .topbar {
      display: none;
    }

    /* section paddings shrink and lose the 240px right gutter */
    section {
      padding: 96px 56px 100px;
    }
    .home {
      padding: 110px 56px 80px;
    }
    .home .lower {
      left: 56px;
      right: 56px;
      bottom: 44px;
    }
    footer {
      padding: 64px 56px 48px;
    }

    /* skills — 2 columns */
    .skills-container {
      grid-template-columns: repeat(2, 1fr);
    }

    /* projects — 1 column */
    .projects-container {
      grid-template-columns: 1fr;
      gap: 28px;
    }

    .schools {
      grid-template-columns: 1fr;
      gap: 24px;
    }

    /* experience — stack the date above the role block */
    .xp-row {
      grid-template-columns: 1fr;
      gap: 24px;
    }
    .xp-row .date {
      padding-top: 0;
    }
    .xp-row .role-block .head {
      flex-direction: column;
      align-items: flex-start;
      gap: 4px;
    }
    .xp-row .role-block .place {
      text-align: left;
      white-space: normal;
    }

    /* education — 1 column */
    .jobs {
      grid-template-columns: 1fr;
      gap: 24px;
    }

    /* about — stack body + side */
    .about-grid {
      grid-template-columns: 1fr;
      gap: 48px;
    }

    /* contact — stack */
    .contact-wrap {
      grid-template-columns: 1fr;
      gap: 56px;
    }

    /* footer */
    .footer-wrap {
      flex-direction: column;
      align-items: flex-start;
      gap: 28px;
    }
    .copyright {
      flex-direction: column;
      gap: 8px;
    }
  }

  /* ============================================================
   RESPONSIVE — PHONE (≤ 640px)
   ============================================================ */
  @media (max-width: 640px) {
    section {
      padding: 80px 22px 88px;
    }
    .home {
      padding: 80px 22px 100px;
      min-height: auto;
      padding-top: 110px;
    }
    /* topbar already hidden at the 960px breakpoint */
    .scroll-cue {
      display: none;
    }

    /* hero lower row gets a hairline above the stacked currently/stack cols */
    .home .lower {
      position: static;
      left: auto;
      right: auto;
      bottom: auto;
      margin-top: 40px;
      padding-top: 28px;
      border-top: 1px solid #ffffff20;
      flex-direction: column;
      align-items: flex-start;
      gap: 18px;
    }

    .home .tagline {
      font-size: 17px;
      margin-top: 24px;
    }
    .home h1 {
      font-size: clamp(56px, 14vw, 88px);
      line-height: 0.94;
    }
    .home .eyebrow {
      margin-bottom: 22px;
      font-size: 10px;
      letter-spacing: 0.22em;
    }

    /* skills — single column on phone, name+kind left, number right */
    .skills-container {
      grid-template-columns: 1fr;
    }

    /* experience */
    .xp-row {
      padding: 32px 0;
      gap: 18px;
    }
    .xp-row .role-block h3 {
      font-size: 24px;
    }
    .xp-row li {
      font-size: 15px;
    }
    .xp-row .role-block .stack {
      gap: 6px;
    }

    /* education */
    .school {
      padding: 28px 24px 24px;
    }
    .school h3 {
      font-size: 22px;
    }

    /* about */
    .about-body p {
      font-size: 16px;
    }
    .about-side {
      grid-template-columns: 1fr;
    }

    /* contact */
    .contact-blurb h3 {
      font-size: 40px;
      line-height: 1;
    }
    .contact-blurb p {
      font-size: 16px;
    }
    .contact-blurb .info a {
      grid-template-columns: 56px 18px auto;
      gap: 10px;
      font-size: 12px;
    }
    .submit {
      width: 100%;
      min-width: 0;
    }

    /* footer */
    footer {
      padding: 56px 22px 40px;
    }
    .footer-wrap .signoff {
      font-size: 38px;
    }
  }
</style>
