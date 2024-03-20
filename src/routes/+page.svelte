<script>
    import { onMount } from 'svelte';
    var x = {title: ''}
    onMount( v => {
        fetch("http://localhost:3000/posts/2").then(v => v.json()).then(v => x = v).then(console.log)
    })
</script>
<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
{x.title}