<script>
    import Menu from "../components/Menu.svelte";
    import PlacemarkMap from "../components/PlacemarkMap.svelte";
</script>

<Menu/>
<div class="hero from-primary to-secondary text-primary-content -mt-[4rem] flex flex-col items-center bg-gradient-to-br p-16">
    <div class="hero-content w-full">
      <h1 class="text-5xl font-bold p-12">Map of Placemarks</h1>
    </div>
  </div>
  
  <div class="container mx-auto mt-4">
    <div class="card bg-base-100 shadow-xl p-10">
      <PlacemarkMap/>
    </div>
  </div>