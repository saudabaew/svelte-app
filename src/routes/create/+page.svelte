<script>
    import { onMount } from 'svelte';

    let result = '';

    onMount(async () => {
        const res = await fetch('http://localhost:8888/create')
        result = await res.json();
    })
</script>

<h1>VM is creating...</h1>