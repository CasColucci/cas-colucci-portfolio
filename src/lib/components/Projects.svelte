<script lang="ts">
    const { title = 'Project Title', description = 'Project Description', link = '#', projectImg = ''} : { title?: string, description?: string, link?: string, projectImg?: string } = $props();
</script>

<div class="project">
    <img src="{projectImg}" alt="{title} image" />
    <h3 class="cardo-regular">{title}</h3>
    <p class="cardo-regular">{description}</p>
    <a href="{link}" class="cardo-regular">View Project</a>
</div>

<style>
    .project {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        color: var(--clr-white);
        width: 345px;

        img {
            width: 345px;
            height: auto;
            outline: 2px solid var(--clr-red);
        }

        h3 {
            font-size: 32px;
            color: var(--clr-red);
            font-family: 'geomregular', sans-serif;
        }

        p {
            color: var(--clr-dark-blue);
            font-family: 'cardo-regular', serif;
            font-size: 20px;
        }

        a {
            align-self: center;
            color: var(--clr-yellow);
            text-shadow: 1px 1px 0 var(--clr-dark-blue);
            text-decoration: underline;
            font-size: 20px;
        }
    }
</style>