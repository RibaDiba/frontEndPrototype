<script>
    let clicked = {ifClicked: false};

    function toggle() {
        clicked.ifClicked = !clicked.ifClicked;
    }
</script>

<main>
    {#if !clicked.ifClicked}
        <div class="center-main-button">
           <button on:click={toggle} class="main-button">Beyond Barriers</button>
        </div>
    {/if}

    {#if clicked.ifClicked} 
        <div class="center-postView">
            <a href="/post">
                <button class="post">Post</button>
            </a>
            <a href="/view">
                <button class="post">View</button>
            </a>
        </div>

        <div>
            <button on:click={toggle} class="goBack">Go Back</button>
        </div>
    {/if}
</main>

<style>
    .center-main-button {
        display: flex;
        justify-content: center;
        margin: 0px;
        margin-top: 50dvh;
    }

    .main-button {
        transition: .4s;
        color: darkslategrey;
        background-color: azure;
        border: 2px solid azure;
        border-radius: 5px;
        font-size: 40px;
        padding: 10px;
    }

    .main-button:hover {
        background-color: #071630;
        color: azure;
        padding: 15px;
        margin-bottom: 1dvh;
    }

    .center-postView {
        display: flex;
        justify-content:space-around;
        margin-top: 50vh;
    }

    .post {
        transition: .4s;
        color: darkslategrey;
        background-color: azure;
        border: 2px solid azure;
        border-radius: 5px;
        font-size: 40px;
        padding: 10px;
    }

    .post:hover {
        background-color: #071630;
        color: azure;
        padding: 15px;
        margin-bottom: 1dvh;
    }

    .goBack {
        position: absolute;
        top: 97dvh;
    }
</style>