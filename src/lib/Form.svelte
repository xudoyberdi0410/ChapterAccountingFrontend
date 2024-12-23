<script>
    import axios from 'axios';
    import { onMount } from 'svelte';
    

    import TitleChoose from './TitleChoose/TitleChoose.svelte';
    import FormButton from './FormComponents/Button.svelte';
    import Select from './FormComponents/Select.svelte';
    import Counter from './FormComponents/Counter.svelte';

    const BACKEND_URL = import.meta.env.VITE_BACKEND_URL

    let chapter, inputValue, role

    let roles = []
    let titles = []

    async function get_roles() {
        const token = localStorage.getItem('access_token');
        
        if (!token) {
            console.error("No access token found");
            return;
        }
        let headers = {
            "Authorization": "Bearer " + token
        }
        const response = await axios.get(BACKEND_URL + '/api/roles', {headers: headers})
        return response.data
    }

    async function get_titles() {
        const token = localStorage.getItem('access_token');
        if (!token) {
            console.error("No access token found");
            return;
        }
        let headers = {
            "Authorization": "Bearer " + token
        }
        const response = await axios.get(BACKEND_URL + '/api/manga_list', {headers: headers})
        console.log(response.data);
        
        return response.data
    }
    async function add_record(){
        let form_data = {
            title: inputValue,
            chapter: chapter,
            role: role,
        }
        let headers = {
            "Authorization": "Bearer " + localStorage.getItem('access_token')
        }
        await axios.post(BACKEND_URL + '/api/add', form_data, {headers: headers})
    }

    onMount(async () => {
        roles = await get_roles()
        titles = await get_titles()
    })
</script>

<form action="/" method="post" class="add_record_form" on:submit|preventDefault={add_record}>
    <TitleChoose title_list={titles} bind:inputValue/>
    <Counter bind:chapter />
    <Select options={roles} bind:role/>
    <FormButton text="Добавить" onclick={add_record}/>
</form>

<style>
.add_record_form{
    display: flex;
    flex-direction: row;
    gap: 10px;
    justify-content: center;
}
</style>