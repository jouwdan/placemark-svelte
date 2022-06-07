<script>
    import {getContext, onMount} from "svelte";
    import {push} from "svelte-spa-router";
    import Menu from "../components/Menu.svelte";
    import RestaurantMap from "../components/RestaurantMap.svelte";
    
    export let params = {};
    let restaurant = {};
    let imageFile;

  const placemarkService = getContext("PlacemarkService");

    onMount(async () => {
      restaurant = await placemarkService.getRestaurantById(params.id);
    });

    let fileInput;
    let files;
    let uploadComplete = "";
    let deleteComplete = "";

    function getBase64(image) {
        const reader = new FileReader();
        reader.readAsDataURL(image);
        reader.onload = e => {
            fileInput = e.target.result;
        };
    };

    async function imageUpload() {
      try {
        const id = params.id;
        var data = new FormData();
        data.append('data', fileInput)
        if (data) {
          console.log(data);
          let success = await placemarkService.uploadImage(id, data);
          if (success) {
            push("/restaurant/" + id);
            uploadComplete = "true";
          }
        }
        push("/restaurant/" + id);
        uploadComplete = "true";
      } catch (err) {
        console.log(err);
      }
    };

    async function deleteImage() {
      try {
        const id = params.id;
        let success = await placemarkService.deleteImage(id);
        if (success) {
          push("/restaurant/" + id);
          deleteComplete = "true";
        }
      } catch (err) {
        console.log(err);
      }
    }
</script>

<Menu/>
<div
  class="hero from-primary to-secondary text-primary-content -mt-[4rem] flex flex-col items-center bg-gradient-to-br p-16">
  <div class="hero-content w-full">
    <h1 class="text-5xl font-bold p-12">{restaurant.name}</h1>
  </div>
</div>

<div class="container mx-auto mt-4 flex flex-wrap justify-center">
  <div class="card w-full text-center bg-base-100 shadow-xl p-10 m-2">
    <p class="text-lg">
      <span class="font-bold">{restaurant.name}</span> is a
      <span class="badge my-2">{restaurant.category}</span> restaurant that serves
      <span class="badge badge-primary my-2">{restaurant.cuisine}</span> cuisine.<br>
      Their decription is: <br> {restaurant.description} <br>
    </p>
  </div>
</div>

<div class="container mx-auto mt-4 flex flex-wrap justify-center">
{#if restaurant.latitude}
  <div class="card w-1/3 text-center bg-base-100 shadow-xl p-10 m-2">
    <RestaurantMap latitude="{restaurant.latitude}" longitude="{restaurant.longitude}"/>
  </div>
{/if}
{#if restaurant.img}
  <div class="card w-1/2 text-center bg-base-100 shadow-xl p-10 m-2">
    <img src="{restaurant.img}" alt="{restaurant.name}">
    <form on:submit|preventDefault={deleteImage} enctype="multipart/form-data"><br>
      <div class="card-actions justify-end">
    <button class="btn gap-2" type="submit"><svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
      Delete Image</button>
      </div>
    </form>
    {#if deleteComplete}
  <div class="success shadow-lg alert-success">
    <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
    <span>Image Deleted</span>
  </div>
  {/if}
  </div>
{/if}
{#if !restaurant.img}
<div class="card w-1/2 text-center bg-base-100 shadow-xl p-10 m-2">
  <p class="text-lg">
    <span class="font-bold">Have an image to upload of {restaurant.name}?</span>
  </p>
  <br>
  {#if files}
    <img id="fileInput" src={fileInput} alt="fileInput"/>
  {/if}
  <div class="flex justify-center">
    <form on:submit|preventDefault={imageUpload} enctype="multipart/form-data">
    <div id="file-select" class="file has-name is-fullwidth">
      <label class="file-label">
        <input type="file" bind:files bind:this={fileInput} on:change={() => getBase64(files[0])} class="file-input" name="imagefile" accept="image/png, image/jpeg">
        <span class="file-cta">
          <span class="file-icon">
            <i class="fas fa-upload"></i>
          </span>
         </span>
        <span class="file-name"></span>
      </label>
      <button class="btn" type="submit">Upload</button>
    </div>
  </form>
  </div>
  {#if uploadComplete}
  <div class="success shadow-lg alert-success">
    <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
    <span>Upload Complete</span>
  </div>
  {/if}
</div>
{/if}
</div>