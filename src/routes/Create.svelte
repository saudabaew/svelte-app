<script>
    let foo = 'baz'
    let bar = 'qux'
    let result = null

    async function doPost () {
        // const res = await fetch('http://pve-test.develop.newdv.ru:8888/create', {
        const res = await fetch('http://localhost:8888/create', {
            method: 'POST',
            body: JSON.stringify({
                foo,
                bar
            })
        })

        const json = await res.json()
        result = JSON.stringify(json)
    }
</script>


<input bind:value={foo} />
<input bind:value={bar} />
<button type="button" on:click={doPost}>
    Post it.
</button>
<p>
    Result:
</p>
<pre>
{result}
</pre>