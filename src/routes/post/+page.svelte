<script>
    import PostPage from '../../lib/PostPage.svelte';

    let login = false;
    let loginFailed = false; 
    let userName ="";
    let password = ""

    import axios from 'axios';

    function toggle() {
        userName = userName;

    }

    function get() {
        axios.get('http://localhost:3000/users')
        .then(res => {
            userName = res.data.user;
            console.log(res)
        })
    }

    function submitHandler() {
        axios.post('http://localhost:3000/users/login', {
            user: userName,
            pass: password
        }).then(res => {
            if (res.data.message == 'Sucessfully Logged In') {
                login = true
            } else {
                loginFailed = true
            }
        })
    }
</script>

<main>
    <a href="/">
        <button class="goBack">Go Back</button>
    </a>

    {#if login}
        <PostPage user={userName}/>
    {/if}
    {#if !login}
        <div class="wrapper">
            <div class="center">
                <div class="loginTextDiv">
                    <h1 class="login">Login</h1>
                    <form class="loginDiv">
                        <label class="usernamePassword" for="user">Username</label>
                        <input id="user" type="text" class="input" bind:value={userName}>
                        <label class="usernamePassword" for="pass">Password</label>
                        <input type="password" class="input input-password" id="pass" bind:value={password}>
                        <button on:click={submitHandler} class="loginButton">Login</button>
                    </form>
                </div>
            </div>
            <h1 class="no-account">Dont have an Account? <a href="/signup">Sign Up here!</a></h1>
        </div>
        <div>
            
        </div>
    {/if}    
    
</main>

<style>
    .usernamePassword {
        color: white;
        margin-bottom: 10px;
    }
    .login {
        color: white;
    }

    .wrapper {
        display: flex;
        justify-content: center;
        flex-direction: column;
        align-items: center;
    }

    .loginDiv {
        display: flex;
        justify-content: center;
        flex-direction: column;
        max-width: 300px;
    }

    .loginTextDiv {
        display: flex;
        justify-content: center;
        flex-direction: column;
    }

    .center {
        display: flex;
        justify-content: center;
        margin-top: 20vh;
        border: 4px solid #03122b;
        border-radius: 10px;
        max-width: 500px;
        padding: 85px;
        padding-top: 50px;
        padding-bottom: 50px;
    }

    .loginButton {
        transition: .4s;
        background-color: blue;
        color: white;
        border-radius: 4px;
        border: 4px solid blue;
        margin-top: 20px;
    }

    .loginButton:hover {
        background-color: white;
        border: 4px solid white;
        color: black;
    }

    .input {
        transition: .4s;
        margin-bottom: 40px;
        padding: 10px;
        background-color: #071630;
        border: solid 2px #3CBC8D;
        border-radius: 8px;
        color: white;
    }

    .input-password {
        margin-bottom: 10px;
    }

    .goBack {
        transition: .4s;
        background-color: #3f664a;
        color: white;
        border-radius: 4px;
        border: 1px solid #3f664a;
        margin: 10px;
        padding: 10px;
    }

    .goBack:hover {
        color: white;
        background-color: #223331;
        border: 1px solid #3f664a;
    }

    .no-account {
        color: white;
        font-size: 15px;
    }

</style>