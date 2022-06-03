<script>
    import WelcomeMenu from "../components/WelcomeMenu.svelte"

    import {push} from "svelte-spa-router";

    let firstName = "";
    let lastName = "";
    let email= "";
    let password = "";

    async function signup() {
        push("/");
    }
  </script>
  
  <WelcomeMenu/>
  <div class="hero from-primary to-secondary text-primary-content -mt-[4rem] flex flex-col items-center bg-gradient-to-br p-16">
    <div class="hero-content w-full">
      <h1 class="text-5xl font-bold p-12">Sign Up To Placemark</h1>
    </div>
  </div>
  <div class="flex justify-center p-12">
    <div class="card flex-shrink-0 w-full max-w-sm shadow-2xl bg-base-100">
      <form on:submit|preventDefault={signup}>
        <div class="card-body">
            <div class="form-control">
                <label for="firstname" class="label">First Name</label>
                <input bind:value={firstName} id="firstname" class="input input-bordered w-full" type="text" placeholder="Enter first name" name="firstName">
              </div>
              <div class="form-control">
                <label for="lastname" class="label">Last Name </label>
                <input bind:value={lastName}  id="lastname" class="input input-bordered w-full" type="text" placeholder="Enter last name" name="lastName">
              </div>
          <div class="form-control">
            <label class="label" for="email">Email Address</label>
                <input bind:value={email}  class="input input-bordered w-full" id="email" name="email"placeholder="Enter Email" type="text">
          </div>
          <div class="form-control">
            <label class="label" for="password">Password</label>
            <input bind:value={password}  class="input input-bordered w-full" id="password" name="password" placeholder="Enter Password" type="password">
          </div>
          <div class="form-control mt-6 justify-center">
            <button class="btn btn-neutral">Sign Up</button>
          </div>
        </div>
      </form>
    </div>
  </div>