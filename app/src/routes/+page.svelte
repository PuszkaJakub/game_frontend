<script>
    import Screen from './Screen.svelte';
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Stu The End game" />
</svelte:head>

<section>
    <a class="how-to-play" href="/how-to-play">How to play</a>
    <Screen />
</section>

<style>
    section {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        flex: 0.6;
    }

    .how-to-play {
        color: var(--color-text);
        margin-bottom: 1rem;
    }

    .how-to-play::before {
        content: 'i';
        display: inline-block;
        font-size: 0.8em;
        font-weight: 900;
        width: 1em;
        height: 1em;
        padding: 0.2em;
        line-height: 1;
        border: 1.5px solid var(--color-text);
        border-radius: 50%;
        text-align: center;
        margin: 0 0.5em 0 0;
        position: relative;
        top: -0.05em;
    }
</style>
