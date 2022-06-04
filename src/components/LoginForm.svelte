<script>
    import {push} from "svelte-spa-router";
    import {getContext} from "svelte";

    let email= "";
    let password = "";
    let errorMessage = "";

    const placemarkService = getContext("PlacemarkService");

    async function login() {
        let success = await placemarkService.login(email, password)
        if (success) {
            push("/dashboard");
        } else {
            email = "";
            password = "";
            errorMessage = "Invalid Credentials";
        }
    }
</script>

<form on:submit|preventDefault={login}>
    <div class="card-body">
        {#if errorMessage}
        <div class="alert shadow-lg alert-error">
            <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current flex-shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
            <span>{errorMessage}</span>
          </div>
        {/if}
        <div class="form-control">
            <label class="label" for="email">Email Address</label>
                <input bind:value={email}  class="input input-bordered w-full" id="email" name="email"placeholder="Enter Email" type="text">
          </div>
          <div class="form-control">
            <label class="label" for="password">Password</label>
            <input bind:value={password}  class="input input-bordered w-full" id="password" name="password" placeholder="Enter Password" type="password">
          </div>
      <div class="form-control mt-6">
        <button class="btn btn-neutral">Login</button>
      </div>
    </div>
  </form>