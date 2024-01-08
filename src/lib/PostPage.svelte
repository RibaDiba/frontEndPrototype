<script>
  import axios from "axios";
  import { onMount } from "svelte";

  export let user;
  let imageArray = [];
  let titleArray = [];
  let buttonPressed = false;
  let count = 0;
  let title = "";

  async function getImages() {
    try {
      const res = await axios.get("http://localhost:3000/images/");
      const response = res.data.images;

      imageArray = [];
      titleArray = [];

      response.forEach((object) => {
        if (user == object.user) {
          imageArray.push(object.request.uploadUrl);
          titleArray.push(object.title);
        }
      });

      console.log(imageArray);
    } catch (error) {
      console.error("Error fetching images:", error.message);
    }

    console.log(imageArray[0]);
    buttonPressed = !buttonPressed;
  }

  function countInc() {
    count++;
  }

  onMount(() => {
    getImages();
  });

  let fileInput;
  let file;

  const handleFileChange = () => {
    file = fileInput.files[0];
  };

  const handleSubmit = async (event) => {
    event.preventDefault();

    const formData = {
      image: file,
      user: user,
      title: title,
    };

    console.log(formData);

    try {
      const response = await axios.post(
        "http://localhost:3000/images/",
        formData,
        {
          headers: {
            "Content-Type": "multipart/form-data",
          },
        }
      );

      console.log("File uploaded successfully.", response.data);
      // Handle success
    } catch (error) {
      console.error("An error occurred during file upload:", error);
      // Handle error
    }
  };
</script>

<main>
  {#each imageArray as imageUrl (imageUrl)}
    <div class="i-hate-css">
      <div class="wrapper">
        <div class="textwrap">
          <h1 class="text">{titleArray[count]}</h1>
        </div>
        <img alt="test" src={imageUrl} class="images" />
      </div>
    </div>
  {/each}

  <form on:submit={handleSubmit} class="form">
    <label for="fileInput" class="formComp">Choose a file:</label>
    <input
      type="file"
      id="fileInput"
      accept="image/*"
      bind:this={fileInput}
      on:change={handleFileChange}
      class="formComp"
    />
    <input type="text" bind:value={title} />
    <div class="i-hate-css">
      <button type="submit" class="choose">Upload</button>
    </div>
  </form>
</main>

<style>
  .choose {
    background-color: white;
    font-size: 30px;
    border: 4px solid whtite;
    border-radius: 10px;
  }

  .form {
    display: flex;
    justify-content: center;
  }

  .formComp {
    margin: 10px;
    font-size: 20px;
    color: white;
  }

  .textwrap {
    display: flex;
    justify-content: center;
    background-color: white;
  }

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

  .text {
    text-align: center;
    background-color: azure;
    margin: 0;
    max-width: 700px;
  }
</style>
