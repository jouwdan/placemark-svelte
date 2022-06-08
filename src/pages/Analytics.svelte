<script>
    import Menu from "../components/Menu.svelte";
    import Chart from 'svelte-frappe-charts';
    import {getContext, onMount} from "svelte";

    const placemarkService = getContext("PlacemarkService");
    let restaurantsList = [];

    let cuisines = ["Irish", "Italian", "Chinese", "Indian", "Thai", "Mexican", "French", "Seafood", "Steakhouse", "Deli"];
    let categories = ["Fine Dining", "Casual Dining", "Fast Casual", "Fast Food", "Cafe", "Buffet", "Pub"]

    let cuisineChart = {
        labels: cuisines,
        datasets: [{
            values: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
        }]
    };

    let categoryChart = {
        labels: categories,
        datasets: [{
            values: [0, 0, 0, 0, 0, 0, 0]
        }]
    };

    onMount(async () => {
        restaurantsList = await placemarkService.getRestaurants();
        restaurantsList.forEach(restaurant => {
            cuisines.forEach(cuisine => {
                if(restaurant.cuisine == cuisine) {
                    let cuisineIndex = cuisines.indexOf(cuisine);
                    cuisineChart.datasets[0].values[cuisineIndex]++;
                }
            });
            categories.forEach(category => {
                if(restaurant.category == category) {
                    let categoryIndex = categories.indexOf(category);
                    categoryChart.datasets[0].values[categoryIndex]++;
                }
            })
        })
        console.log(cuisineChart)
    });
</script>

<Menu/>
<div class="hero from-primary to-secondary text-primary-content -mt-[4rem] flex flex-col items-center bg-gradient-to-br p-16">
    <div class="hero-content w-full">
      <h1 class="text-5xl font-bold p-12">Placemark Analytics</h1>
    </div>
  </div>
  
  <div class="container mx-auto mt-4">
    <div class="card bg-base-100 shadow-xl p-10 mb-2">
        <h2 class="text-2xl mx-auto">Restaurants by Cuisine</h2>
        <Chart data={cuisineChart} type="pie" maxSlices="10" />
    </div>
    <div class="card bg-base-100 shadow-xl p-10">
        <h2 class="text-2xl mx-auto">Restaurants by Category</h2>
        <Chart data={categoryChart} type="bar" />
    </div>
  </div>