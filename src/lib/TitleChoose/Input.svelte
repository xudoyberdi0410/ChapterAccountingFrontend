<script>
export let inputValue = "";

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


<input type="text" placeholder="Тайтл..." autocomplete="off" id="searchInput" bind:value={inputValue} on:input on:focus on:blur/>