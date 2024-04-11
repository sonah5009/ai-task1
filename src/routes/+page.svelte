<script>
    import { onMount } from 'svelte';
    import { read, utils, writeFileXLSX } from 'xlsx';

    /* the component state is an array of presidents */
    let pres = [];
    onMount(async () => {
    const file = 'src/lib/task1.xlsx'; // Path to your local XLSX file
    const data = await fetch(file);
    const arrayBuffer = await data.arrayBuffer();
    const wb = read(arrayBuffer);
    const ws = wb.Sheets[wb.SheetNames[0]];
    pres = utils.sheet_to_json(ws);
});

    /* get state data and export to XLSX */
    function exportFile() {
        const ws = utils.json_to_sheet(pres);
        const wb = utils.book_new();
        utils.book_append_sheet(wb, ws, "Data");
        writeFileXLSX(wb, "suna_task1.xlsx");
    }
</script>
<h1>Submission: Block End-to-End Machine LearningAssignment</h1>
<p>This is excel.</p>
<table>
    <thead>
    <tr>
        <th>Data_Preprocessing</th>
        <th>Models</th>
        <th>Performance_Metrics</th>
        <th>Description</th>
    </tr>
</thead>
    <tbody>
    {#each pres as p}
    <tr>
      <td>{p.Data_Preprocessing}</td>
      <td>{p.Models}</td>
      <td>{p.Performance_Metrics}</td>
      <td>{p.Description}</td>
    </tr>{/each}
    </tbody><tfoot><td colSpan={4}>
    <button on:click={exportFile}>Export XLSX</button>
    </td></tfoot></table>
