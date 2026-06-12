<script lang="ts">
  const { skill = "Skill", iconsrc }: { skill?: string; iconsrc?: string } =
    $props();
</script>

<div class="skill">
  {#if iconsrc}
    <div class="skill-icon">{@html iconsrc}</div>
  {/if}
  <p class="cardo-regular">{skill}</p>
</div>

<style>
  .skill {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    font-family: var(--display);
    font-optical-sizing: auto;
    font-weight: 400;
    font-style: normal;
    font-size: 24px;
    color: var(--white);
  }

  .skill-icon {
    width: 114px;
    height: 114px;
    color: var(--red);
  }

  .skill-icon svg {
    width: 100%;
    height: 100%;
  }
</style>
