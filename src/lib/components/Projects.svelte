<script lang="ts">
  const {
    id = "id",
    title = "Project Title",
    tagline = "Project Tagline",
    description = "Project Description",
    projectImg = "",
    modalImages = [] as string[],
    modalDescription = "",
    techStack = [] as string[],
    liveLink = "",
    repoLink = "",
    year = "2026",
    isEmpty = false,
  }: {
    id?: string;
    title?: string;
    tagline?: string;
    description?: string;
    projectImg?: string;
    modalImages?: string[];
    modalDescription?: string;
    techStack?: string[];
    liveLink?: string;
    repoLink?: string;
    year?: string;
    isEmpty?: boolean;
  } = $props();

  let modalOpen = $state(false);

  function openModal() {
    modalOpen = true;
  }
  function closeModal() {
    modalOpen = false;
  }

  function onKeydown(e: KeyboardEvent) {
    if (e.key === "Escape") closeModal();
  }
</script>

<svelte:window onkeydown={onKeydown} />

{#if isEmpty}
  <div class="proj-card empty">
    <div class="label">More on the way</div>
    <div class="sub">Currently in build — client work, summer 2026</div>
  </div>
{:else}
  <button class="proj-card" onclick={openModal}>
    <div class="proj-thumb">
      <img src={projectImg} alt="{title} image" />
    </div>
    <div class="proj-body">
      <h3>{title}</h3>
      <div class="proj-tags">
        {#if techStack.length > 0}
          {#each techStack as tech}
            <span class="tag">{tech}</span>
          {/each}
        {/if}
        <span class="tag">{year}</span>
      </div>
      <p>{tagline}</p>
      <span class="proj-cta">
        Read case study <span class="arrow">→</span>
      </span>
    </div>
  </button>

  {#if modalOpen}
    <div class="modal-backdrop" onclick={closeModal} role="presentation">
      <div
        class="modal"
        onclick={(e) => e.stopPropagation()}
        role="dialog"
        aria-modal="true"
        aria-label={title}
      >
        <button class="close-btn" onclick={closeModal} aria-label="Close">
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M18 6L6 18M6 6L18 18"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
            />
          </svg>
        </button>
        <div class="modal-num">Project · {year}</div>

        <h2 class="modal-title">{title}</h2>
        <div class="modal-sub">{tagline}</div>

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
              <li class="tag">{tech}</li>
            {/each}
          </ul>
        {/if}

        <p class="modal-description">{modalDescription || description}</p>

        {#if liveLink || repoLink}
          <div class="modal-links">
            {#if liveLink}
              <a href={liveLink} target="_blank" rel="noopener noreferrer"
                >Live Site →
              </a>
            {/if}
            {#if repoLink}
              <a href={repoLink} target="_blank" rel="noopener noreferrer"
                >Repository →</a
              >
            {/if}
          </div>
        {/if}
      </div>
    </div>
  {/if}
{/if}

<style>
  .proj-card {
    background: var(--cream);
    color: var(--ink);
    border: 1px solid #1c314420;
    padding: 0;
    text-align: left;
    display: flex;
    flex-direction: column;
    position: relative;
    overflow: hidden;
    transition:
      transform 0.22s ease,
      border-color 0.22s ease;
  }

  .proj-card:hover {
    border-color: var(--red);
    transform: translateY(-3px);
  }

  .proj-thumb {
    height: 240px;
    background: var(--cream-2);
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border-bottom: 1px solid #1c314420;
  }

  .proj-body {
    padding: 28px 32px 32px;

    h3 {
      font-family: var(--display);
      font-weight: 600;
      font-size: 28px;
      letter-spacing: -0.02em;
      margin: 0 0 12px;
    }

    p {
      font-family: var(--serif);
      font-size: 16px;
      line-height: 1.5;
      margin: 0 0 22px;
      color: var(--ink);
      opacity: 0.85;
    }
  }

  .proj-tags {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-bottom: 18px;
  }

  .tag {
    background: transparent;
    color: var(--muted);
    font-family: var(--mono);
    font-size: 10px;
    padding: 3px 8px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    border: 1px solid #1c314430;
  }

  .proj-cta {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--red);
    display: inline-flex;
    align-items: center;
    gap: 8px;

    .arrow {
      transition: transform 0.2s ease;
      display: inline-block;
    }
  }

  .proj-card:hover .proj-cta .arrow {
    transform: translateX(4px);
  }

  .proj-card.empty {
    background: transparent;
    border: 1px dashed #1c314440;
    justify-content: center;
    align-items: center;
    min-height: 460px;
    color: var(--muted);
    cursor: default;
  }
  .proj-card.empty:hover {
    transform: none;
    border-color: #1c314440;
  }
  .proj-card.empty .label {
    font-family: var(--display);
    font-weight: 600;
    font-size: 22px;
    letter-spacing: -0.01em;
    color: var(--ink);
  }
  .proj-card.empty .sub {
    font-family: var(--serif);
    font-style: italic;
    font-size: 15px;
    margin-top: 6px;
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
    animation: fadeIn 0.18s ease;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  .modal {
    background: var(--cream);
    color: var(--ink);
    max-width: 720px;
    width: 100%;
    max-height: 85vh;
    overflow: auto;
    padding: 40px 44px 44px;
    border: 1px solid var(--ink);
    position: relative;
  }

  .close-btn {
    position: absolute;
    top: 14px;
    right: 18px;
    background: none;
    border: none;
    color: var(--muted);
    font-family: var(--mono);
    font-size: 22px;
    line-height: 1;
    transition: color 0.18s ease;
  }

  .close-btn:hover {
    color: var(--red);
  }

  .modal-num {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 10px;
  }

  .modal-title {
    font-family: var(--display);
    font-weight: 700;
    font-size: 36px;
    letter-spacing: -0.025em;
    margin: 0 0 8px;
  }

  .modal-sub {
    font-family: var(--serif);
    font-style: italic;
    font-size: 17px;
    color: var(--muted);
    margin-bottom: 24px;
    padding-bottom: 20px;
    border-bottom: 1px solid #1c314420;
  }

  .modal-images {
    margin-top: 0;
    border: 1px solid #1c314420;
    padding: 32px;
    background: var(--cream-2);
    display: flex;
    justify-content: center;

    img {
      flex: 1 1 200px;
      max-width: 100%;
      height: 380px;
      object-fit: cover;
    }
  }

  .modal-tech {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    list-style: none;
    padding: 0;
    margin: 24px 0 18px;
  }

  .modal-description {
    font-family: var(--serif);
    font-size: 17px;
    line-height: 1.55;
    color: var(--ink);
    opacity: 0.9;
  }

  .modal-links {
    margin-top: 22px;
    font-family: var(--mono);
    font-size: 12px;
    letter-spacing: 0.16em;
    text-transform: uppercase;

    a {
      color: var(--red);
      text-decoration: none;
      border-bottom: 1px solid var(--red);
      padding-bottom: 2px;
    }
  }
</style>
