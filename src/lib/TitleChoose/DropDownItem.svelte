<script>
  export let handleClick;
	export let TitleName;
</script>

<style>
.DropDownItem{
    padding: 5px;
    cursor: pointer;
    color: var(--white);
}
.DropDownItem:hover{
    background-color: var(--bright);
}
</style>

<span on:click={handleClick} class="DropDownItem">{TitleName}</span>
