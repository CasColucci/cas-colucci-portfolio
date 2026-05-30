<script>
    const red = 'var(--clr-red)';
</script>

<div class="index">
    <div class="navstack | vertical-center">
        <nav class="">
            <a href="#home">Home</a>
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
        <h1 class="geom-regular"><span class="red">01</span> Skills</h1>
    </section>
    <section class="projects" id="projects">
        <h1 class="geom-regular"><span class="red">02</span> Projects</h1>
    </section>
    <section class="experience" id="experience">
        <h1 class="geom-regular"><span class="red">03</span> Experience</h1>
    </section>
    <section class="education" id="education">
        <h1 class="geom-regular"><span class="red">04</span> Education</h1>
    </section>
    <section class="contact" id="contact">
        <h1 class="geom-regular"><span class="red">05</span> Contact</h1>
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
        padding: 0 10vw;
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

            .active {
                color: var(--clr-red);
                font-size: 24px;
                font-family: 'cardo-regular', serif;
            }
        }

        a::after {
            content: '';
            display: inline-block;
            width: 20px;
            height: 2px;
            background-color: var(--clr-white);
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

    svg {
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
</style>