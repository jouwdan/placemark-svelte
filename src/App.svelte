<script>
  import {setContext} from "svelte";
  import {PlacemarkService} from "./services/PlacemarkService";

  import Main from "./pages/Main.svelte"
  import Login from "./pages/Login.svelte"
  import Signup from "./pages/Signup.svelte"
  import Dashboard from "./pages/Dashboard.svelte"
  import Restaurant from "./pages/Restaurant.svelte"

  import Router from "svelte-spa-router";

  setContext("PlacemarkService", new PlacemarkService("http://localhost:4000"));

  let routes = {
    "/": Main,
    "/main": Main,
    "/logout": Main,
    "/login": Login,
    "/signup": Signup,
    "/dashboard": Dashboard,
    "/restaurant/:id": Restaurant
  }
</script>

<Router {routes}/>