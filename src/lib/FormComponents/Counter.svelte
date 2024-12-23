<script>
    export let chapter;
</script>

<style>
    input{
        border-radius: 5px;
        border: 2px solid var(--gray);
        background-color: var(--gray);
        padding: 5px 10px;
        color: var(--white);
    }
    input:focus{
        outline: none;
        border: 2px solid var(--bright);
    }
</style>

<input type="number" name="chapter_number" id="chapter_number" placeholder="Глава" required bind:value={chapter}/>