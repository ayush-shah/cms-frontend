<script>
    import { Router, Link } from "svelte-navigator";
</script>

<nav>
  <div class="topnav padding-layout">Shop at 10% discount</div>
  <ul class="padding-layout">
    <Router>
      <li class="logo"><Link class="link" to="/">Logo Here</Link></li>
      <li><Link class="link" to="/">Home</Link></li>
      <li><Link class="link" to="/products">Products</Link></li>
      <li><Link class="link" to="/login">Login / Register</Link></li>
    </Router>
  </ul>
</nav>

<style scoped>
  nav {
    height: 75px;
    display: flex;
    position: relative;
    flex-flow: column wrap;
  }
  nav .topnav {
    height: 35%;
    background: #222831;
    color: #eeeeee;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 13px;
  }
  nav ul {
    display: flex;
    height: 65%;
    background: #393e46;
    color: #eeeeee;
    flex-flow: row wrap;
    align-content: center;
  }
  nav ul li {
    list-style: none;
    margin: 0 15px;
  }
  nav ul li.logo {
    margin: 0 auto 0 0 !important;
  }
  .padding-layout {
    padding: 0 5vw;
  }
</style>
