<script>
  import { Router, Route } from "svelte-navigator";
  import Nav from "./components/Navbar.svelte";
  import Login from "./pages/Login.svelte";
  import Products from "./pages/Products.svelte";
  import LandingPage from "./pages/LandingPage.svelte";

</script>

<Nav />
<Router>
  <Route path="/">
    <LandingPage />
  </Route>
  <Route path="/products">
    <Products />
  </Route>
  <Route path="/login">
    <Login />
  </Route>
</Router>

<style>
</style>
