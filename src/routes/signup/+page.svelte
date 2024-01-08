<script>
    import axios from 'axios'

    let username = ''
    let passwrord = ''

    let isSignedUp = false; 

    function toggle() {
        try {
            axios.post('http://localhost:3000/users/signup', {
                user: username,
                pass: passwrord
            })
        } catch {
            console.log('error')
        }

        isSignedUp = true;
    }
</script>

<main>
    <div class="wrapper">
        <div class="center">
            <div class="loginTextDiv">
                <h1 class="login">Signup</h1>
                <form class="loginDiv">
                    <label class="usernamePassword" for="user">Username</label>
                    <input id="user" type="text" class="input" bind:value={username}>
                    <label class="usernamePassword" for="pass">Password</label>
                    <input type="password" class="input input-password" id="pass" bind:value={passwrord}>
                    <button on:click={toggle} class="loginButton">Signup</button>
                </form>
            </div>
            {#if isSignedUp}
                <h1 class="no-account">Signed up? <a href="/signup">Login here!</a></h1>
            {/if}
        </div>
    </div>
    <div>
    </div>

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

    .no-account {
        color: white;
        font-size: 15px;
    }

</style>