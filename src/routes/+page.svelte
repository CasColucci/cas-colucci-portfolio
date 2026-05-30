<script lang="ts">
    import { onMount } from 'svelte';
    import Skills from '$lib/components/Skills.svelte';
    import SectionHead from '$lib/components/SectionHead.svelte';

    import svelteIcon from '$lib/assets/svelte-16.svg?raw';
    import angularIcon from '$lib/assets/angular-16.svg?raw';
    import blazorIcon from '$lib/assets/blazor.svg?raw';
    import reactIcon from '$lib/assets/react-16.svg?raw';
    import mssqlIcon from '$lib/assets/database.svg?raw';
    import postgresIcon from '$lib/assets/postgresql.svg?raw';
    import dotnetIcon from '$lib/assets/dotnet.svg?raw';
    import typescriptIcon from '$lib/assets/typescript-16.svg?raw';
    
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
    <section class="projects | white-bg" id="projects">
        <SectionHead number="02" title="Projects" inverted={true} />
        <hr>
    </section>
    <section class="experience" id="experience">
        <SectionHead number="03" title="Experience" />
        <hr>
    </section>
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
        width: 90vw;
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
        gap: 2rem;
        justify-content: center;
        margin: 0 auto 10vh;
    }

    .white-bg {
        background-color: var(--clr-white);
    }
</style>