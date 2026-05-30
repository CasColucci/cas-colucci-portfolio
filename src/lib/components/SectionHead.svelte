<script lang="ts">
    const { number = '00', title = 'Section Title', inverted = false } : { number?: string, title?: string, inverted?: boolean } = $props();
</script>

<div class="section-head">
    <h2 class="cardo-regular" style="color: {inverted ? 'var(--clr-dark-blue)' : 'var(--clr-white)'}">
        <span>{number}</span> {title}
    </h2>
</div>

<style>
    @font-face {
        font-family: 'geomregular';
        src: url('../../fonts/geom-variablefont_wght-webfont.woff2') format('woff2'),
            url('../../fonts/geom-variablefont_wght-webfont.woff') format('woff');
        font-weight: normal;
        font-style: normal;
    }

    .geom-regular {
        font-family: 'geomregular', sans-serif;
        font-optical-sizing: auto;
        font-weight: 400;
        font-style: normal;
    }

    .section-head {
        display: flex;
        flex-direction: column;
        align-items: center;
        font-family: 'geomregular', sans-serif;
        width: 90vw;
        margin: 0 auto;
    }
    
    h2 {
        align-self: flex-start;
        font-size: 64px;
    }

    span {
        color: var(--clr-red);
    }
</style>