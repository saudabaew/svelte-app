<script>
    import {onMount} from 'svelte';

    let template = '';
    let soft = [];
    let disk = 2;
    let vmName = '';

    let app = [
        'Postgres',
        'Kafka',
        'Docker'
    ];
    let result = []

    onMount(async () => {
        const res = await fetch('http://localhost:8888/templates')
        result = await res.json()
    })

    async function doPost() {
        const formData = new FormData();
        formData.append('template', template);
        formData.append('vmName', vmName);
        formData.append('disk', disk);
        // await fetch('http://pve-test.develop.newdv.ru:8888/create', {
        await fetch('http://localhost:8888/create', {
            method: 'POST',
            body: formData
        })
    }

</script>

<form method="post">
    {#if result.length > 0}
        <h1>Select template</h1>
        <table class="content-table buyside">
            <tr>
                <th></th>
                <th>ID</th>
                <th>Name</th>
                <th>Description</th>
            </tr>
            {#each result as data, i}
                <tr>
                    <td>
                        <input name="template" type=radio bind:group={template} value="{data.name}">
                    </td>
                    <td>
                        {data.vmid}
                    </td>
                    <td>
                        {data.name}
                    </td>
                    <td>
                        {data.description}
                    </td>
                </tr>
            {/each}
        </table>


        <h2>Add software</h2>
        {#each app as a}
            <p>
                <label>
                    <input name="soft" type=checkbox bind:group={soft} value={a}>
                    {a}
                </label>
            </p>
        {/each}


        <h2>Disk size</h2>
        <p>
            <label>
                <input name="disk" type=number bind:value={disk} min=2 max=10>
                <input name="disk" type=range bind:value={disk} min=2 max=10>
            </label>
        </p>

        <p>
            <input bind:value={vmName} placeholder="enter vm name">
        </p>

        <form action="/">
            <input type="submit" on:click={doPost} value="START"/>
        </form>
    {/if}
</form>

<style>
    label {
        width: 100%;
        margin-bottom: 20px;
        border: 1px solid #dddddd;
        empty-cells: hide;
        border-collapse: collapse;
        font-weight: bold;
        padding: 5px;
        background: #efefef;
    }

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