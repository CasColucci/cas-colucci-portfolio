<script lang="ts">
  const {
    skill = "Skill",
    kind = "Kind",
    num = "00",
    iconsrc,
  }: {
    skill?: string;
    kind?: string;
    num?: string;
    iconsrc?: string;
  } = $props();
</script>

<div class="skill-card">
  <div class="num">{num}/08</div>
  {#if iconsrc}
    <div class="skill-icon">{@html iconsrc}</div>
  {/if}
  <div>
    <div class="name">{skill}</div>
    <div class="kind">{kind}</div>
  </div>
</div>

<style>
  .skill-card {
    background: var(--dark-blue);
    color: var(--cream);
    padding: 36px 28px 28px;
    position: relative;
    transition: background 0.2s ease;
    min-height: 200px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    p {
      font-family: var(--display);
      font-weight: 600;
      font-size: 26px;
      letter-spacing: -0.02em;
      margin-top: 32px;
      margin-bottom: 4px;
    }
  }

  .skill-card:hover {
    background: var(--dark-blue2);
  }

  .skill-icon {
    width: 114px;
    height: 114px;
    color: var(--red);
    margin: auto;
  }

  .skill-icon svg {
    width: 100%;
    height: 100%;
  }

  .num {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 0.18em;
    margin-bottom: auto;
  }

  .name {
    font-family: var(--display);
    font-weight: 600;
    font-size: 26px;
    letter-spacing: -0.02em;
    margin-top: 32px;
    margin-bottom: 4px;
  }

  .kind {
    font-family: var(--serif);
    font-style: italic;
    font-size: 14px;
    color: var(--muted);
  }
</style>
