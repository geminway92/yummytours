<script lang="ts">
  import { Router, Link, Route } from "svelte-routing";

  import Home from "./views/Home.svelte";
  import About from "./views/About.svelte";
import RoutesTour from "./views/RoutesTour.svelte";
</script>

<div >
<Router>
  <nav>
    <Link to="/">Home</Link>
    <Link to="/about">About</Link>
    <Link to="/route-tour">Rutas</Link>
  </nav>
  
    <Route path="/">
      <Home />
    </Route>
    <Route path="/about">
      <About />
    </Route>
    <Route path="/route-tour">
      <RoutesTour/>
    </Route>
  </Router>
</div>
  
<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    /* background-color: #351753; */
    height: 100;
  }
  
</style>
