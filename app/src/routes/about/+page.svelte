<script>
    import {onMount} from 'svelte';
    import MarkdownRenderer from './MarkdownRenderer.svelte';
    let markdownContent = '';

    onMount(async () => {
        const response = await fetch('./ABOUT.md');
        markdownContent = await response.text();
    });
</script>

<svelte:head>
    <title>About</title>
    <meta name="description" content="About Stu The End game" />
</svelte:head>

<div class="text-column markdown">
    <h1>About this app</h1>
    <MarkdownRenderer {markdownContent} />
</div>

<style>
</style>
