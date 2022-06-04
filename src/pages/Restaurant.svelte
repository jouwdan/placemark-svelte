<script>
    import {getContext, onMount} from "svelte";
    import Menu from "../components/Menu.svelte";
    import RestaurantMap from "../components/RestaurantMap.svelte";
    
    export let params = {};
    let restaurant = {};

  const placemarkService = getContext("PlacemarkService");

    onMount(async () => {
      restaurant = await placemarkService.getRestaurantById(params.id);
    });
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
{#if restaurant.img}
  <div class="card w-1/2 text-center bg-base-100 shadow-xl p-10 m-2">
    <img src="{restaurant.img}" alt="{restaurant.name}">
  </div>
{/if}
{#if restaurant.latitude}
  <div class="card w-1/3 text-center bg-base-100 shadow-xl p-10 m-2">
    <RestaurantMap latitude="{restaurant.latitude}" longitude="{restaurant.longitude}"/>
  </div>
{/if}
</div>