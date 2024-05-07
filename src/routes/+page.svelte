<script>
    import { onMount } from 'svelte';
    import { read, utils, writeFileXLSX } from 'xlsx';

    /* the component state is an array of presidents */
    const src = '/src/lib/task1_excel.png'; // Path to your task1_excel.png file


    /* get state data and export to XLSX */
    function exportFile() {
        const ws = utils.json_to_sheet(sheet);
        const wb = utils.book_new();
        utils.book_append_sheet(wb, ws, "Data");
        writeFileXLSX(wb, "suna_task1.xlsx");
    }
</script>
<h1>Submission: Block End-to-End Machine LearningAssignment</h1>

<img {src} alt="excel image" width="100%"/>