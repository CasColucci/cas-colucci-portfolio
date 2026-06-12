<script lang="ts">
    const { number = '00 - Title', title = 'Section Title', meta = "small blurb", inverted = false } : { number?: string, title?: string, meta?: string, inverted?: boolean } = $props();
</script>

<div class="section-tag">
    <span class="num">{ number }</span>
    <span class="title">{ title }</span>
    <span class="rule"></span>
    <span class="meta">{ meta }</span>

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

    .section-tag {
        display: flex;
        align-items: baseline;
        gap: 22px;
        margin-bottom: 72px;
        font-family: var(--display);
        font-weight: 600;
        letter-spacing: -0.02em;
        color: var(--cream);
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

</style>