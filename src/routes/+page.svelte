<script>
    import { onMount } from 'svelte';
    var x = []
    onMount( v => {
        fetch("http://localhost:3000/posts").then(v => v.json()).then(v => x = v).then(console.log)
    })
</script>
<h1>Minimál példa</h1>
{#each x as {title}}
{title}
<hr>
{/each}