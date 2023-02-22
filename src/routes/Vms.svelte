<script>
    import { onMount } from 'svelte';

    let result = []

    onMount(async () => {
        // const res = await fetch('http://pve-test.develop.newdv.ru:8888/vms')
        const res = await fetch('http://localhost:8888/vms')
        result = await res.json()
    })
</script>


{#if result.length > 0}
    <table class="content-table buyside">
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Node</th>
            <th>CPU</th>
            <th>Memory</th>
            <th>Disk</th>
            <th>Status</th>
        </tr>
        {#each result as data}
            <tr>
                <td><a href="{data.vmid}">{data.vmid}</a></td>
                <td>{data.name}</td>
                <td>{data.node}</td>
                <td>{data.maxcpu}</td>
                <td>{(data.maxmem / 1000000000).toFixed(2)}</td>
                <td>{(data.maxdisk / 1000000000).toFixed(2)}</td>
                <td>{data.status}</td>
            </tr>
        {/each}
    </table>
    <form action="templates">
        <input type="submit" value="CREATE NEW" />
    </form>
    {:else}
    <h1>
        There is not templates
    </h1>
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