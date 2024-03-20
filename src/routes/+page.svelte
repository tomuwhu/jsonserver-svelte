<script>
    import { onMount } from 'svelte';
    var x = []
    var nextid = 0
    var newtit = ''
    const getall = () => fetch("http://localhost:3000/posts?_sort=title").then(v => v.json()).then(v => x = v).then(() => {
        nextid = Number(x.sort((a,b) => b.id - a.id)[0].id) + 1
    })
    onMount(getall)
</script>
<h1>Minimál példa</h1>
{#each x as {id, title}}
<i>{id}</i> <input id={id} bind:value={title} on:input={() => {
    fetch(`http://localhost:3000/posts/${id}`, {
        method: "PUT",
        body: JSON.stringify({id, title})
    }).then(v => v.json())
}}/> -- <button on:click={() => {
    fetch(`http://localhost:3000/posts/${id}`, {
        method: "DELETE"
    }).then(v => v.json()).then( v => {
        let x2 = []
        x.forEach(i => {
            if (i.id != v.id) x2.push(i)
        })
        x=x2
    })
}}>töröl</button>
<hr>
{/each}
<i>{nextid}</i> <input id={nextid} bind:value={newtit} on:change={() => {
    fetch(`http://localhost:3000/posts`, {
        method: "POST",
        headers: { "Content-Type": "application/json"},
        body: JSON.stringify({id: nextid.toString(), title: newtit})
    }).then(v => v.json()).then(() => {
        getall()
        newtit=''
        x = x
    })}}>
<style>
    i {
        color: gray;
    }
</style>