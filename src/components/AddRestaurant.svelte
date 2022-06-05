<script>
    import {push} from "svelte-spa-router";
    import {getContext} from "svelte";

    const placemarkService = getContext("PlacemarkService");

    let name = "";
    let description = "";
    let category = "";
    let cuisine = "";
    let latitude = "";
    let longitude = "";
    let errorMessage = "";

    async function addRestaurant() {
        let success = await placemarkService.addRestaurant(name, description, category, cuisine, latitude, longitude)
        if (success) {
            push("/dashboard");
        } else {
            name = "";
            description = "";
            category = "";
            latitude = "";
            longitude = "";
            errorMessage = "Error Adding Restaurant";
        }
    }
</script>

<form on:submit|preventDefault={addRestaurant}>
    {#if errorMessage}
    <div class="alert shadow-lg alert-error">
        <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
        <span>{errorMessage}</span>
    </div>
    {/if}
    <div class="form-control">
        <label class="label" for="Name">Restaurant Name</label>
        <input bind:value={name} class="input input-bordered" type="text" placeholder="Name" name="name">
        </div>

    <div class="form-control">
        <label class="label" for="description">Description</label>
        <input bind:value={description} class="input input-bordered" type="text" placeholder="Description" name="description">
        </div>
        
    <div class="form-control">
        <label class="label" for="category">Category</label>
        <select bind:value={category} class="select select-bordered" name="category">
            <option disabled selected>Select One</option>
            <option>Fine Dining</option>
            <option>Casual Dining</option>
            <option>Fast Casual</option>
            <option>Fast Food</option>
            <option>Cafe</option>
            <option>Buffet</option>
            <option>Pub</option>
        </select></div>
        
    <div class="form-control"><label class="label" for="cuisine">Cuisine</label>
        <select bind:value={cuisine} class="select select-bordered" name="cuisine">
            <option disabled selected>Select One</option>
            <option>Irish</option>
            <option>Italian</option>
            <option>Chinese</option>
            <option>Indian</option>
            <option>Thai</option>
            <option>Mexican</option>
            <option>French</option>
            <option>Seafood</option>
            <option>Steakhouse</option>
            <option>Deli</option>
        </select></div>

    <div class="form-control">
        <label class="label" for="location">Location</label>
        <div class="flex">
        <input bind:value={latitude} class="input input-bordered flex-1 mr-2" type="text" placeholder="Latitude" name="latitude">
        <input bind:value={longitude} class="input input-bordered flex-1" type="text" placeholder="Longitude" name="longitude">
        </div>
        <div class="form-control mt-6 justify-center">
        <button class="btn btn-neutral">Add Restaurant</button>
        </div>
    </div>
</form>