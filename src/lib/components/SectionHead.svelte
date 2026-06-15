<script lang="ts">
  const {
    number = "00 - Title",
    title = "Section Title",
    meta = "small blurb",
    inverted = false,
  }: {
    number?: string;
    title?: string;
    meta?: string;
    inverted?: boolean;
  } = $props();
</script>

{#if !inverted}
  <div class="section-tag blue">
    <span class="num">{number}</span>
    <span class="title">{title}</span>
    <span class="rule"></span>
    <span class="meta">{meta}</span>
  </div>
{:else}
  <div class="section-tag cream">
    <span class="num">{number}</span>
    <span class="title">{title}</span>
    <span class="rule"></span>
    <span class="meta">{meta}</span>
  </div>
{/if}

<style>
  .cream {
    color: var(--dark-blue);
  }

  .blue {
    color: var(--cream);
  }
  .section-tag {
    display: flex;
    align-items: baseline;
    gap: 22px;
    margin-bottom: 72px;
    font-family: var(--display);
    font-weight: 600;
    letter-spacing: -0.02em;
  }
  .section-tag .num {
    font-family: var(--mono);
    font-weight: 500;
    font-size: 13px;
    letter-spacing: 0.18em;
    color: var(--red);
    text-transform: uppercase;
    padding-top: 12px;
  }
  .section-tag .title {
    font-family: var(--display);
    font-weight: 700;
    font-size: 56px;
    line-height: 1;
  }
  .section-tag .rule {
    flex: 1;
    height: 1px;
    background: currentColor;
    opacity: 0.18;
    align-self: center;
  }
  .section-tag .meta {
    font-family: var(--serif);
    font-style: italic;
    font-size: 18px;
    opacity: 0.6;
    align-self: center;
  }

  @media (max-width: 640px) {
    /* section header — stack instead of side-by-side */
    .section-tag {
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 44px;
    }
    .section-tag .num {
      padding-top: 0;
      font-size: 11px;
      flex-basis: 100%;
    }
    .section-tag .title {
      font-size: 38px;
      line-height: 1;
    }
    .section-tag .rule {
      display: none;
    }
    .section-tag .meta {
      display: none;
    }
  }
</style>
