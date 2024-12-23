<script>
  import { onMount } from 'svelte';
  // import { Router, Link, Route } from "svelte-routing";

  import Header from "./lib/Header.svelte";
  import Form from "./lib/Form.svelte";
  import Login from "./lib/Login.svelte";
  import Table from "./lib/Table/Table.svelte";

  // export let url = ''

  onMount(() => {
    // check params for access_token
    if (window.location.search.includes('access_token')){
      const urlParams = new URLSearchParams(window.location.search)
      const access_token = urlParams.get('access_token')
      localStorage.setItem('access_token', access_token)
      document.location.href="/"
    }
    if (!localStorage.getItem('access_token')){
      window.location.href = import.meta.env.VITE_BACKEND_URL + '/login/discord';
    }
  })
</script>

<main>
  <div class="container">
    <Header />
    <Form />
    <br>
    <Table />
  </div>
</main>

<style>
</style>
