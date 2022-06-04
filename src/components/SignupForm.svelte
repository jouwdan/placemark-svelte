<script>
    import {push} from "svelte-spa-router";
    import {getContext} from "svelte";

    const placemarkService = getContext("PlacemarkService");

    let firstName = "";
    let lastName = "";
    let email= "";
    let password = "";
    let errorMessage = "";

    async function signup() {
        let success = await placemarkService.signup(firstName, lastName, email, password)
        if (success) {
            push("/login");
        } else {
            firstName = "";
            lastName = "";
            email = "";
            password = "";
            errorMessage = "Error Registering";
        }
    }
  </script>

<form on:submit|preventDefault={signup}>
    <div class="card-body">
        {#if errorMessage}
        <div class="alert shadow-lg alert-error">
            <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
            <span>{errorMessage}</span>
          </div>
        {/if}
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