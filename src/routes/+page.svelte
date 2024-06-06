
<style>
    :global(body) {
       size: 210mm 297mm;
    }
    table { page-break-inside:auto ; border:1px solid black }
    tr    { page-break-inside:avoid; page-break-after:auto }
    thead { display:table-header-group }
    tfoot { display:table-footer-group }
    .divfooter {
        display: fixed;
        bottom: 0mm;
    }
    @page:left {
       content:"test"
    }
    
</style>
<script>
    //@ts-ignore
	import saveAs from "file-saver";
	import { asBlob } from "html-docx-js-typescript";

    let rows = Array.from({length: 500}, (_, i) => i);

	async function docx() {
        const html = document.getElementById("print")?.innerHTML ??""
        const docx = await asBlob(html);
        console.log(docx)
        saveAs(docx, "test.docx")
	}
</script>
<button onclick={docx}>test</button>
<div id="print">
    <h1>Blandet tekst på siden</h1>
    tekst der skal løbe ud over kanten zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz zzzzzzzzzzzzzzzzzzzzzzzzzz zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz zzzzzzzzzzzzzzzzzzzzzzz

    <table>
        <thead>
            <tr><th>Header</th></tr>
        </thead>
        <tbody>
            {#each rows as row}
                <tr><td>{row}</td></tr>
            {/each}
    </tbody>
    </table>
    <div class="divfooter">
        <p>Footer tekst</p>
    </div>
</div>
