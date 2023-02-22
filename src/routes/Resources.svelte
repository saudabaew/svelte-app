<script>
    import { onMount } from 'svelte';

    let result = []

    onMount(async () => {
        const res = await fetch('http://localhost:8888/resources')
        result = await res.json()
    })
</script>

{#if result.length > 0}
    <table class="content-table buyside">
        <tr>
            <th>ID</th>
            <th>CPU</th>
            <th>Maxcpu</th>
            <th>Mem</th>
            <th>Maxmem</th>
            <th>Disk</th>
            <th>Maxdisk</th>
            <th>Uptime</th>
            <th>Status</th>
        </tr>
        {#each result as data}
            <tr>
                <td>{data.id}</td>
                <td>{data.cpu}</td>
                <td>{data.maxcpu}</td>
                <td>{(data.mem / 1000000000).toFixed(2)}</td>
                <td>{(data.maxmem / 1000000000).toFixed(2)}</td>
                <td>{(data.disk / 1000000000).toFixed(2)}</td>
                <td>{(data.maxdisk / 1000000000).toFixed(2)}</td>
                <td>{data.uptime}</td>
                <td>{data.status}</td>
            </tr>
        {/each}
    </table>
{/if}

<style>
    table {
        width: 100%;
        margin-bottom: 20px;
        border: 1px solid #dddddd;
        empty-cells: hide;
        border-collapse: collapse;
    }

    th {
        font-weight: bold;
        padding: 5px;
        background: #efefef;
        border: 1px solid #dddddd;
    }

    td {
        border: 1px solid #dddddd;
        padding: 5px;
        word-wrap: break-word;
    }
</style>