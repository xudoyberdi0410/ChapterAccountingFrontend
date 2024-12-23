<script>
    export let text = ''
    export let onclick;
</script>

<style>
button{
    border-radius: 5px;
    border: 2px solid var(--gray);
    background-color: var(--gray);
    padding: 5px 10px;
    color: var(--white);
}
button:hover{
    background-color: var(--bright);
    border: 2px solid var(--bright);
    cursor: pointer;
}
</style>

<button class="btn btn-primary" type="submit" on:click={onclick}>
{text}
</button>