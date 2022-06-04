<script>
    import WelcomeMenu from "../components/WelcomeMenu.svelte";
    import SignupForm from "../components/SignupForm.svelte";
  </script>
  
  <WelcomeMenu/>
  <div class="hero from-primary to-secondary text-primary-content -mt-[4rem] flex flex-col items-center bg-gradient-to-br p-16">
    <div class="hero-content w-full">
      <h1 class="text-5xl font-bold p-12">Sign Up To Placemark</h1>
    </div>
  </div>
  <div class="flex justify-center p-12">
    <div class="card flex-shrink-0 w-full max-w-sm shadow-2xl bg-base-100">
      <SignupForm/>
    </div>
  </div>