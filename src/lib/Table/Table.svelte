<script>
  import axios from "axios";
  import { onMount } from "svelte";

  const data_url = import.meta.env.VITE_BACKEND_URL + "/api/chapters";
  let page = 1;
  let per_page = 20;
  let chapter_list = [];

  if (window.location.search) {
    const urlParams = new URLSearchParams(window.location.search);
    page = parseInt(urlParams.get("page"));
  }

  async function get_data() {
    let params = {
      page: page,
      per_page: per_page,
    };
    let headers = {
      Authorization: "Bearer " + localStorage.getItem("access_token"),
    };
    let response = await axios.get(data_url, {
      params: params,
      headers: headers,
    });
    return response.data; // Make sure to return the data part of the response
  }

  onMount(async () => {
    chapter_list = await get_data(); // Assign the fetched data to chapter_list
  });
</script>

<table>
  <thead>
    <tr>
      <th>Номер главы</th>
      <th>Роль</th>
      <th>Тайтл</th>
      <th>Сделал</th>
    </tr>
  </thead>
  <tbody>
    {#each chapter_list as chapter}
      <tr>
        <td>{chapter.chapter}</td>
        <td>{chapter.role}</td>
        <td>{chapter.title}</td>
        <td>{chapter.worker}</td>
      </tr>
    {/each}
  </tbody>
</table>

<style>
  table {
    width: 100%; /* таблица будет занимать всю ширину */
    border-collapse: collapse; /* убирает промежутки между ячейками */
    border: 1px soid var(--bright); /* граница таблицы */
    border-radius: 5px; /* закругляет углы таблицы */
  }

  th,
  td {
    padding: 10px; /* добавляет отступы в ячейках */
    border-bottom: 1px solid var(--bright); /* граница между строками */
    text-align: center; /* центрирует текст в ячейках */
  }

  th {
    background-color: var(--bright); /* светлый фон для заголовков */
    border-top: none;
  }
  td:first-child, th:first-child {
    border-left: none;
    width: 10%;
  }
</style>
