<script>
    import {getContext, onMount} from 'svelte'
  
    const placemarkService = getContext("PlacemarkService");
    let restaurantsList = [];
  
    onMount(async () => {
      restaurantsList = await placemarkService.getRestaurants();
    });
  </script>

{#each restaurantsList as restaurant}
<div class="card w-72 bg-base-100 shadow-xl p-10 m-2">
  <a href="/restaurant/{restaurant._id}">
  <div class="box box-link-hover-shadow">
      <h2 class="text-2xl font-bold">
      {restaurant.name}
      </h2>
      <span class="badge my-2">{restaurant.category}</span>
      <span class="badge badge-primary my-2">{restaurant.cuisine}</span>
      <p>
      {restaurant.description}
      </p>
  </div>
  </a>
</div>
{/each}