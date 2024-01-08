<script>
    import { onMount } from "svelte";
    import axios from "axios";

    let imageArray = []

    onMount(() => {
        getImages()
    })

    async function getImages() {
      try {
        const res = await axios.get('http://localhost:3000/images/');
        const response = res.data.images;

        imageArray = []
  
        response.forEach((object) => {
          imageArray.push(object.request.uploadUrl)
        });
  
      console.log(imageArray);
      } catch (error) {
        console.error("Error fetching images:", error.message);
      }
    }

</script>

<main>

    <a href="/">
        <button>Go Back</button>
    </a>

    <h1 class="title">Here are all the images (not just uploaded from your user)</h1>

    {#each imageArray as imageUrl (imageUrl)}
        <div class="i-hate-css">
          <div class="wrapper">
            <div class="textwrap">
            </div>
            <img alt="test" src={imageUrl} class="images"/>
          </div>
        </div>
      {/each}

</main>

<style>
     .i-hate-css {
      display: flex;
      justify-content: center;
    }

    .images {
      max-width: 700px;
      margin: 75px;
      border: 10px solid azure;
      border-radius: 10px;
      margin-top: 0;
      margin-left: 0;
      margin-right: 0;
    }

    .wrapper {
      display: flex;
      flex-direction: column;
      justify-content: center;
      text-align: center;
      background-color: #03122b;
    }

    .title {
        color: white;
        text-align: center;

    }
</style>