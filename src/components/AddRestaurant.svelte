<script>
    import {push} from "svelte-spa-router";
    import {getContext} from "svelte";

    const placemarkService = getContext("PlacemarkService");

    let name = "";
    let description = "";
    let category = "";
    let latitude = "";
    let longitude = "";
    let errorMessage = "";

    async function addRestaurant() {
        let success = await placemarkService.addRestaurant(name, description, category, latitude, longitude)
        if (success) {
            push("/login");
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
    <div class="form-control">
        <label class="label" for="Name">Restaurant Name</label>
        <input class="input input-bordered" type="text" placeholder="Name" name="name">
        <label class="label" for="description">Description</label>
        <input class="input input-bordered" type="text" placeholder="Description" name="description">
        <label class="label" for="category">Category</label>
        <select class="select select-bordered" name="category">
            <option disabled selected>Select One</option>
            <option>Fine Dining</option>
            <option>Casual Dining</option>
            <option>Fast Casual</option>
            <option>Fast Food</option>
            <option>Cafe</option>
            <option>Buffet</option>
            <option>Pub</option>
        </select>
        <label class="label" for="cuisine">Cuisine</label>
        <select class="select select-bordered" name="cuisine">
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
        </select>
        <label class="label" for="location">Location</label>
        <div class="flex">
        <input class="input input-bordered flex-1 mr-2" type="text" placeholder="Latitude" name="latitude">
        <input class="input input-bordered flex-1" type="text" placeholder="Longitude" name="longitude">
        </div>
        <br>
        <button class="btn btn-neutral">Add Restaurant</button>
    </div>
</form>