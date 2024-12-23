<script>
  import axios from "axios";
  import { onMount } from "svelte";

    let username, profile_img, user_id
    async function get_user_data(){
        try{
            let data = await axios.get(import.meta.env.VITE_BACKEND_URL + '/api/user_data', {
                headers: {
                    "Authorization": "Bearer " + localStorage.getItem('access_token')
                }
            })
            return data
        } catch {
            window.location.href = import.meta.env.VITE_BACKEND_URL + '/login/discord'
        }
    }
    onMount(async () => {
        let data = await get_user_data()
        console.log(data);
        
        username = data.data.username
        profile_img = data.data.avatar
        user_id = data.data.user_id
    })

    function logout(){
        localStorage.removeItem('access_token');
        window.location.href = '/';
    }
</script>

<header>
    <a href="/" aria-label="Home" class="logo-link">
        <span class="logo">Chapter Accounting</span>
    </a>
    <nav>    
        <span id="username_label">{username}</span>

        <div class="avatar" style="background-image: url(&quot;//cdn.discordapp.com/avatars/{user_id}/{profile_img}&quot;);"></div>
        <button class="log-out-btn" id="log_out_btn" on:click={logout}>
            Log Out
        </button>
    </nav>

</header>

<style>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem 2rem;
    }
    .logo-link{
        text-decoration: none;
        color: var(--bright);
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        font-size: 1.5rem;
        position: relative;
    }
    .logo-link::after{
        content: "";
        position: absolute;
        width: 0;
        height: 2px;
        background-color: var(--bright);
        bottom: 0;
        left: 0;
        transition: all 0.3s;
    }
    .logo-link:hover::after{
        width: 100%;
    }

    nav{
        display: flex;
        align-items: center;
        gap: 1rem;
        padding: 0.5rem 1rem;
        border-radius: 5px;
        background-color: var(--gray);
    }

    #log_out_btn{
        background-color: var(--bright);
        color: var(--dark);
        border: none;
        padding: 0.5rem 1rem;
        border-radius: 5px;
        cursor: pointer;
    }
    .hidden{
        display: none;
    }
    .avatar{
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background-size: cover;
        background-position: center;
    }
</style>