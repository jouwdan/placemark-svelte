<script>
  import Main from "./pages/Main.svelte"
  import Login from "./pages/Login.svelte"
  import Signup from "./pages/Signup.svelte"
  import Dashboard from "./pages/Dashboard.svelte"

  import Router from "svelte-spa-router";

  let routes = {
    "/": Main,
    "/main": Main,
    "/logout": Main,
    "/login": Login,
    "/signup": Signup,
    "/dashboard": Dashboard
  }
</script>

<Router {routes}/>