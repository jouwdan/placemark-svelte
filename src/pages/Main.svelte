<script>
  import WelcomeMenu from "../components/WelcomeMenu.svelte";
  import {getContext} from "svelte";

  const placemarkService = getContext("PlacemarkService");
  placemarkService.logout();
</script>

<WelcomeMenu/>
<div class="hero from-primary to-secondary text-primary-content -mt-[4rem] flex flex-col items-center bg-gradient-to-br pt-32 pb-48 mx-auto items-center h-96">
    <div class="text-center hero-content">
      <div class="max-w-md">
        <h1 class="text-5xl font-bold">Welcome to Placemark!</h1>
        <p class="py-6">Please sign up or log in to get started.</p>
      </div>
    </div>
  </div>