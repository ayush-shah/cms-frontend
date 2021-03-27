<script>
  import { Router, Route } from "svelte-navigator";
  import Nav from "./components/Navbar.svelte";
  import Login from "./pages/Login.svelte";
  import Products from "./pages/Products.svelte";
  import LandingPage from "./pages/LandingPage.svelte";
  import DetailedProduct from "./pages/DetailedProduct.svelte";

</script>

<Nav />
<Router>
  <Route path="/product/:id" component={DetailedProduct} />
  <Route path="/products" component={Products} />
  <Route path="/login" component={Login} />
  <Route path="/" component={LandingPage} />
</Router>

<style>
</style>
