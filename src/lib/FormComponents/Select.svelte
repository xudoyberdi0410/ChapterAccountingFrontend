<script>
    export let options = [];
    export let role = '';
</script>

<style>
select{
    border-radius: 5px;
    border: 2px solid var(--gray);
    background-color: var(--gray);
    padding: 5px 10px;
    color: var(--white);
}
</style>

<select bind:value={role} required>
    <option value="" disabled selected>Выберите роль</option>
    {#each options as option}
        <option value={option}>{option}</option>
    {/each}
</select>