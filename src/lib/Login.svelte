<script>
    let login_discord_url = import.meta.env.VITE_BACKEND_URL + '/login/discord';
    const urlParams = new URLSearchParams(window.location.search);
</script>

<style>
.login-by{
    display: flex;
    flex-direction: column;
    align-items: center;
    list-style: none;
    padding: 0;
    font-size: 2rem;
}
.login-by-btn{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 10px;
    width: 200px;
    height: 200px;
    background-color: var(--gray);
    border-radius: 10px;
    margin: 10px;
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
.login-by-btn:hover{
    transform: translateY(-3px);
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.2);
}
.login-by-btn:active{
    transform: translateY(2px);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    background-color: var(--gray);
}
a{
    text-decoration: none;
}
.discord{
    background-color: #7289DA;
    color: var(--white);
}
</style>

<div>
    <h1>Войти с помощью</h1>
    <ul class="login-by">
        <li>
            <a href={login_discord_url} class="login-by-btn discord">
                <img src="https://cdn.prod.website-files.com/6257adef93867e50d84d30e2/653714c1f22aef3b6921d63d_636e0a6ca814282eca7172c6_icon_clyde_white_RGB.svg" alt="Discrord" height="100px" />
                <span>Discord</span>
            </a>
        </li>
    </ul>
</div>