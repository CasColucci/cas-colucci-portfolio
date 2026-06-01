<script lang="ts">
    import { onMount } from 'svelte';
    import Skills from '$lib/components/Skills.svelte';
    import SectionHead from '$lib/components/SectionHead.svelte';
    import Projects from '$lib/components/Projects.svelte';

    import svelteIcon from '$lib/assets/svelte-16.svg?raw';
    import angularIcon from '$lib/assets/angular-16.svg?raw';
    import blazorIcon from '$lib/assets/blazor.svg?raw';
    import reactIcon from '$lib/assets/react-16.svg?raw';
    import mssqlIcon from '$lib/assets/database.svg?raw';
    import postgresIcon from '$lib/assets/postgresql.svg?raw';
    import dotnetIcon from '$lib/assets/dotnet.svg?raw';
    import typescriptIcon from '$lib/assets/typescript-16.svg?raw';

    import project1Img from '$lib/assets/img/bracketgame.png';
    
    const red = 'var(--clr-red)';

    onMount(() => {
        const sections = document.querySelectorAll('section');
        const navA = document.querySelectorAll('.navstack a');

        function updateActiveNav() {
            let maxVisibleArea = 0;
            let activeSection : string | null = null;

            sections.forEach((section) => {
                const visibleArea = getVisibleArea(section);
                if(visibleArea > maxVisibleArea) {
                    maxVisibleArea = visibleArea;
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

        function getVisibleArea(element: Element): number {
            const rect = element.getBoundingClientRect();
            const windowHeight = window.innerHeight || document.documentElement.clientHeight;
            const windowWidth = window.innerWidth || document.documentElement.clientWidth;
            const visibleHeight = Math.min(rect.bottom, windowHeight) - Math.max(rect.top, 0);
            const visibleWidth = Math.min(rect.right, windowWidth) - Math.max(rect.left, 0);
            return visibleHeight * visibleWidth;
        }

        window.addEventListener('scroll', updateActiveNav);
        window.addEventListener('resize', updateActiveNav);
    });
</script>

<div class="index">
    <div class="navstack | vertical-center">
        <nav class="">
            <a href="#home" class="active">Home</a>
            <a href="#skills">Skills</a>
            <a href="#projects">Projects</a>
            <a href="#experience">Experience</a>
            <a href="#education">Education</a>
            <a href="#contact">Contact</a>
        </nav>
    </div>
    <section class="home" id="home">
        <h1 class="geom-regular"><span class="red">C</span>as <span class="red">C</span>olucci</h1>
        <hr>
        <h2 class="cardo-italic">Full Stack Web Developer</h2>
        <svg id="arrows" width="12" height="55" viewBox="0 0 12 55" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path id="toparrow" d="M5.7735 55L11.547 45H-4.29153e-06L5.7735 55Z" fill="{red}"/>
            <path id="midarrow" d="M5.7735 32L11.547 22H-4.29153e-06L5.7735 32Z" fill="{red}"/>
            <path id="bottomarrow" d="M5.7735 10L11.547 0H-4.29153e-06L5.7735 10Z" fill="{red}"/>
        </svg>

    </section> 
    <section class="skills" id="skills">
        <SectionHead number="01" title="Skills" />
        <hr>
        <div class="skills-container">
            <Skills skill="Svelte" iconsrc={svelteIcon} />
            <Skills skill="Angular" iconsrc={angularIcon} />
            <Skills skill="Blazor" iconsrc={blazorIcon} />
            <Skills skill="React" iconsrc={reactIcon} />
            <Skills skill="MSSQL" iconsrc={mssqlIcon} />
            <Skills skill="PostgreSQL" iconsrc={postgresIcon} />
            <Skills skill="C#/.NET" iconsrc={dotnetIcon} />
            <Skills skill="TypeScript" iconsrc={typescriptIcon} />
        </div>
    </section>
    <div class="white-bg">
        <section class="projects" id="projects">
            <SectionHead number="02" title="Projects" inverted={true} />
            <hr>
            <div class="projects-container">
                <Projects title="Golly's Bracket Game" 
                description="A .NET and React project, utilizing PostgreSQL and Entity Framework Core for the 
                database functions, and SignalR for real-time communication." 
                link="/project1" projectImg={project1Img} />
            </div>
        </section>
        <section class="experience" id="experience">
            <div class="panel" aria-hidden="true"></div>
            <div class="content">
                <div class="head">
                    <SectionHead number="03" title="Experience" />
                </div>
                <hr class="rule">
                <div class="jobs">
                    <div class="job">
                        <h3 class="role">Software Engineer</h3>
                        <div class="job-info">
                            <span class="dates">11/24 <span class="red">-</span> 05/26</span>
                            <div class="company-info">
                                <span class="company">System Innovators</span>
                                <span class="where">Jacksonville, FL</span>
                            </div>
                        </div>
                        <ul class="tech">
                            <li>C#</li>
                            <li>.NET Framework</li>
                            <li>Blazor</li>
                            <li>Docker</li>
                            <li>SQL</li>
                        </ul>
                    </div>
                    <div class="detail">
                        <ul class="points">
                            <li>Maintained and enhanced the AMP (Admin Management Portal) within the iNovah enterprise revenue management system, supporting cashiering and payments operations for government and commercial clients across the United States and Canada</li>
                            <li>Diagnosed and resolved long-standing production bugs in a legacy .NET Framework 4.8 codebase spanning 130+ interconnected projects</li>
                            <li>Improved team documentation and authored transition materials supporting the team's migration from TFVC to Git version control</li>
                        </ul>
                    </div>
                    <div class="job">
                        <h3 class="role">Software Engineer</h3>
                        <div class="job-info">
                            <span class="dates">11/21 <span class="red">-</span> 09/24</span>
                            <div class="company-info">
                                <span class="company">BAM Technologies</span>
                                <span class="where">Arlington, VA</span>
                            </div>
                        </div>
                        <ul class="tech">
                            <li>C#</li>
                            <li>.NET 8</li>
                            <li>Angular</li>
                            <li>Entity Framework</li>
                            <li>SQL</li>
                        </ul>
                    </div>
                    <div class="detail">
                        <ul class="points">
                            <li>Built and maintained full-stack features for the MyCAA Scholarship platform, a nationally-deployed government application serving military spouses nationwide, using .NET Core 8 and Angular</li>
                            <li>Designed and optimized SQL Server database queries and schema to support platform performance and reliability</li>
                            <li>Managed CI/CD deployments via Octopus Deploy and TeamCity, maintaining stable production releases across environments</li>
                            <li>Collaborated in a cross-functional Scrum team, conducting code reviews and implementing comprehensive testing practices</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>
    </div>
    <div class="triangle-divider">
        <svg data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 120" preserveAspectRatio="none">
            <path d="M1200 0L0 0 598.97 114.72 1200 0z" class="shape-fill"></path>
        </svg>
    </div>
    <section class="education" id="education">
        <SectionHead number="04" title="Education" />
        <hr>
    </section>
    <section class="contact" id="contact">
        <SectionHead number="05" title="Contact" />
        <hr>
    </section>
    <footer>
        <hr>
        <p class="cardo-italic">Designed and built by Cas Colucci</p>
    </footer>
</div>

<style>
    :root {
        --experienceSectionLeftPanelWidth: 30%;
    }
    @font-face {
        font-family: 'cardoitalic';
        src: url('../fonts/cardo-italic-webfont.woff2') format('woff2'),
                url('../fonts/cardo-italic-webfont.woff') format('woff');
        font-weight: normal;
        font-style: italic;
    }

    @font-face {
        font-family: 'cardoregular';
        src: url('../fonts/cardo-regular-webfont.woff2') format('woff2'),
            url('../fonts/cardo-regular-webfont.woff') format('woff');
        font-weight: normal;
        font-style: normal;
    }

    @font-face {
        font-family: 'geomregular';
        src: url('../fonts/geom-variablefont_wght-webfont.woff2') format('woff2'),
            url('../fonts/geom-variablefont_wght-webfont.woff') format('woff');
        font-weight: normal;
        font-style: normal;
    }

    .geom-regular {
        font-family: 'geomregular', sans-serif;
        font-optical-sizing: auto;
        font-weight: 400;
        font-style: normal;
    }

    .cardo-regular {
        font-family: 'cardoregular', serif;
        font-optical-sizing: auto;
        font-weight: 400;
        font-style: normal;
    }

    .cardo-italic {
        font-family: 'cardoitalic', serif;
        font-optical-sizing: auto;
        font-weight: 400;
        font-style: italic;
    }

    /* Navigation that is sticky to right */
    .navstack {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 60px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        padding: 0 5vw;
        a {
            color: var(--clr-yellow);
            text-shadow: 1px 1px 0 var(--clr-dark-blue);
        }
    }

    nav {
        display: flex;
        align-items: center;
        position: fixed;
        gap: 20px;
        flex-direction: column;
        a {
            display: flex;
            align-items: center;
            color: var(--clr-white);
            text-decoration: none;
            font-family: 'cardo-italic', serif;
            font-size: 20px;
            align-self: flex-end;
            transition: color 0.3s ease, font-size 0.3s ease, font-family 0.3s ease;
            line-height: 2.5rem;
        }
        .active {
            color: var(--clr-red);
            font-size: 23px;
            font-family: 'cardo-regular', serif;
        }
        .active::after {
            content: '';
            display: inline-block;
            width: 50px;
            height: 2px;
            background-color: var(--clr-red);
            margin-left: 5px;
        }

        a::after {
            content: '';
            display: inline-block;
            width: 20px;
            height: 2px;
            background-color: var(--clr-yellow);
            margin-left: 5px;
            transition: width 0.3s ease;
        }
        
        a:hover {
            color: var(--clr-red);
            font-size: 24px;
            font-family: 'cardo-regular', serif;
        }

        a:hover::after {
            background-color: var(--clr-red);  
            width: 50px;
        }

    } 

    section {
        width: 90vw;
        margin: 0 auto 10vh;
    }

    .home {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        h1 {
            color: var(--clr-white);
            text-align: center;
            font-size: 96px;
        }

        h2 {
            color: var(--clr-white);
            text-align: center;
            font-size: 36px;
        }

        hr {
            width: 420px;
        }

    }

    .red {
        color: var(--clr-red);
    }

    hr {
        border: 1px solid var(--clr-red);
        margin: 20px auto;
        width: 100%;
    }

    .vertical-center {
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    #arrows {
        position: absolute;
        margin-top: 50vh;
    }

    #toparrow {
        opacity: 0;
        animation: fadeIn 1s ease-in-out 1s forwards, translateY 1s ease-in-out 1s forwards;
    }

    #midarrow {
        opacity: 0;
        animation: fadeIn 1s ease-in-out 1.5s forwards, translateY 1s ease-in-out 1.5s forwards;
    }

    #bottomarrow {
        opacity: 0;
        animation: fadeIn 1s ease-in-out 2s forwards, translateY 1s ease-in-out 2s forwards;
    }

    @keyframes fadeIn {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    @keyframes translateY {
        from {
            transform: translateY(20px);
        }
        to {
            transform: translateY(0);
        }
    }

    .skills-container {
        display: flex;
        flex-wrap: wrap;
        gap: 50px;
        justify-content: center;
        margin: 0 auto 10vh;
    }

    .white-bg {
        background-color: var(--clr-white);
    }

    .projects-container {
        display: flex;
        flex-direction: row;
        gap: 2rem;
        margin: 0 auto 10vh;
        padding: 0 5vw;
    }

    .experience {
        position: relative;
        margin: 0 auto;
        color: var(--clr-dark-blue);
        container-type: inline-size;
    }

    .panel {
        position: absolute;
        inset: 0 auto 10% 0;
        width: var(--experienceSectionLeftPanelWidth);
        background-color: var(--clr-dark-blue);
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
        background-color: var(--clr-red);
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
        color: var(--clr-white);
        font-family: 'geomregular', sans-serif;
    }

    .job-info {
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        gap: 10px;
        padding: 0 3.2cqw;
        color: var(--clr-white);
        font-family: 'cardo-italic', serif;
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
        color: var(--clr-red);
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
        color: var(--clr-white);
        font-family: 'cardo-italic', serif;
        font-size: 20px;
    }

    .tech li::before {
        content: '>';
        position: absolute;
        left: 0;
        color: var(--clr-red);
        font-weight: bold;
        font-size: 20px;
        font-family: 'geomregular', sans-serif;
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
        content: '>';
        position: absolute;
        left: 0;
        color: var(--clr-red);
        font-weight: bold;
        font-size: 20px;
        font-family: 'geomregular', sans-serif;
    }


    .shape-fill {
        fill: var(--clr-white);
    }

    /* Responsive adjustments */
    @media (min-width: 1600px) {
        section {
            width:70vw;
        }
    }
</style>