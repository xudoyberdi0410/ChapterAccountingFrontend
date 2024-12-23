<script>
    import DropDownItem from "./DropDownItem.svelte";
    import Input from "./Input.svelte";
    import { onMount } from 'svelte';
  
    export let title_list = [];
  
    let isActive = false;
  
    export let inputValue = '';
    let filteredItems = [];
  
    function handleInput() {
      filteredItems = title_list.filter(item => item.toLowerCase().includes(inputValue.toLowerCase()));
    }
  
    function DropDownItemClicked(e) {
      inputValue = e.target.innerText;
      isActive = false; // Закрываем список после выбора элемента
    }
  
    function handleClickOutside(event) {
      // Закрываем список, если клик был не по компоненту
      if (!event.target.closest('.dropdown-container')) {
        isActive = false;
      }
    }
  
    // Добавляем глобальный обработчик кликов
    onMount(() => {
      document.addEventListener('click', handleClickOutside);
      return () => {
        document.removeEventListener('click', handleClickOutside);
      };
    });
  </script>
  
  <style>
  .hidden {
    display: none !important;
  }
  .dropdown-container {
    position: relative;
    display: inline-block;
  }
  .DropDownItems {
    position: absolute;
    background-color: var(--gray);
    border: 2px solid var(--gray);
    border-radius: 5px;
    padding: 5px;
    z-index: 1;
    width: 100%;
    display: flex;
    flex-direction: column;
  }
  </style>
  
  <div class="dropdown-container">
    <Input
      bind:inputValue
      on:input={handleInput}
      on:focus={() => { isActive = true; }}
    />
    <div class="DropDownItems {isActive ? '' : 'hidden'}">
      {#if filteredItems.length > 0}
        {#each filteredItems as item}
          <DropDownItem TitleName={item} handleClick={DropDownItemClicked} />
        {/each}
      {:else}
        {#each title_list as item}
          <DropDownItem TitleName={item} handleClick={DropDownItemClicked} />
        {/each}
      {/if}
    </div>
  </div>
  