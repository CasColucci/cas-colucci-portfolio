<script lang="ts">
    const {
        title = 'Project Title',
        description = 'Project Description',
        projectImg = '',
        modalImages = [] as string[],
        modalDescription = '',
        techStack = [] as string[],
        liveLink = '',
        repoLink = '',
    } : {
        title?: string,
        description?: string,
        projectImg?: string,
        modalImages?: string[],
        modalDescription?: string,
        techStack?: string[],
        liveLink?: string,
        repoLink?: string,
    } = $props();

    let modalOpen = $state(false);

    function openModal() { modalOpen = true; }
    function closeModal() { modalOpen = false; }

    function onKeydown(e: KeyboardEvent) {
        if (e.key === 'Escape') closeModal();
    }
</script>

<svelte:window onkeydown={onKeydown} />

<div class="project">
    <img src={projectImg} alt="{title} image" />
    <h3>{title}</h3>
    <p>{description}</p>
    <button class="view-btn" onclick={openModal}>View Project</button>
</div>

{#if modalOpen}
<div class="modal-backdrop" onclick={closeModal} role="presentation">
    <div class="modal" onclick={(e) => e.stopPropagation()} role="dialog" aria-modal="true" aria-label={title}>
        <button class="close-btn" onclick={closeModal} aria-label="Close">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M18 6L6 18M6 6L18 18" stroke="var(--red)" stroke-width="2" stroke-linecap="round"/>
            </svg>
        </button>

        <div class="modal-inner">
            <h2 class="modal-title">{title}</h2>
            <hr class="modal-rule">

            {#if modalImages.length > 0}
            <div class="modal-images">
                {#each modalImages as img}
                    <img src={img} alt="{title} screenshot" />
                {/each}
            </div>
            {/if}

            {#if techStack.length > 0}
            <ul class="modal-tech">
                {#each techStack as tech}
                    <li>{tech}</li>
                {/each}
            </ul>
            {/if}

            <p class="modal-description">{modalDescription || description}</p>

            {#if liveLink || repoLink}
            <div class="modal-links">
                {#if liveLink}
                    <a href={liveLink} target="_blank" rel="noopener noreferrer">Live Site</a>
                {/if}
                {#if repoLink}
                    <a href={repoLink} target="_blank" rel="noopener noreferrer">Repository</a>
                {/if}
            </div>
            {/if}
        </div>
    </div>
</div>
{/if}

<style>
    @font-face {
        font-family: 'geomregular';
        src: url('../../fonts/geom-variablefont_wght-webfont.woff2') format('woff2'),
            url('../../fonts/geom-variablefont_wght-webfont.woff') format('woff');
        font-weight: normal;
        font-style: normal;
    }

    @font-face {
        font-family: 'cardoregular';
        src: url('../../fonts/cardo-regular-webfont.woff2') format('woff2'),
            url('../../fonts/cardo-regular-webfont.woff') format('woff');
        font-weight: normal;
        font-style: normal;
    }

    .project {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        color: var(--white);
        width: 345px;

        img {
            width: 345px;
            height: auto;
            outline: 2px solid var(--red);
        }

        h3 {
            font-size: 32px;
            color: var(--red);
            font-family: 'geomregular', sans-serif;
        }

        p {
            color: var(--dark-blue);
            font-family: 'cardoregular', serif;
            font-size: 20px;
        }
    }

    .view-btn {
        align-self: center;
        background: none;
        border: none;
        color: var(--yellow);
        text-shadow: 1px 1px 0 var(--dark-blue);
        text-decoration: underline;
        font-size: 20px;
        cursor: pointer;
        font-family: 'cardoregular', serif;
        width: auto;
        padding: 0;
    }

    .view-btn:hover {
        color: var(--red);
        text-shadow: none;
    }

    /* Modal */
    .modal-backdrop {
        position: fixed;
        inset: 0;
        background-color: color-mix(in srgb, var(--dark-blue) 85%, transparent);
        z-index: 200;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 2rem;
    }

    .modal {
        background-color: var(--dark-blue);
        border-left: 3px solid var(--red);
        max-width: 800px;
        width: 100%;
        max-height: 85vh;
        overflow-y: auto;
        position: relative;
    }

    .modal-inner {
        padding: 1.5rem 2rem 2rem;
    }

    .close-btn {
        position: sticky;
        top: 0.75rem;
        float: right;
        background: none;
        border: none;
        cursor: pointer;
        padding: 4px;
        width: auto;
        z-index: 1;
        margin: 0.75rem 0.75rem 0 0;
    }

    .modal-title {
        font-family: 'geomregular', sans-serif;
        font-size: 36px;
        color: var(--white);
        margin-bottom: 0.25rem;
    }

    .modal-rule {
        border: none;
        height: 2px;
        background-color: var(--red);
        margin: 0 0 1rem 0;
        width: 100%;
    }

    .modal-images {
        display: flex;
        flex-wrap: wrap;
        gap: 0.75rem;
        margin-bottom: 1rem;

        img {
            flex: 1 1 200px;
            max-width: 100%;
            height: 380px;
            outline: 2px solid var(--red);
            object-fit: cover;
        }
    }

    .modal-tech {
        display: flex;
        flex-wrap: wrap;
        gap: 0.4rem;
        list-style: none;
        padding: 0;
        margin: 0 0 1rem 0;

        li {
            font-family: 'geomregular', sans-serif;
            font-size: 13px;
            color: var(--dark-blue);
            background-color: var(--yellow);
            padding: 1px 8px;
        }
    }

    .modal-description {
        font-family: 'cardoregular', serif;
        font-size: 18px;
        color: var(--white);
        line-height: 1.6;
        margin-bottom: 1.25rem;
    }

    .modal-links {
        display: flex;
        gap: 1.5rem;

        a {
            font-family: 'geomregular', sans-serif;
            font-size: 16px;
            color: var(--yellow);
            text-decoration: underline;
            position: relative;
            padding-left: 18px;
        }

        a::before {
            content: '>';
            position: absolute;
            left: 0;
            color: var(--red);
            font-family: 'geomregular', sans-serif;
        }

        a:hover {
            color: var(--red);
        }
    }
</style>
