<script>
    import {marked} from 'marked';
    export let markdownContent = '';
</script>

<div class="markdown">
    {@html marked(markdownContent)}
</div>
