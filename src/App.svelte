<script lang="ts">
  import { Router, Link, Route, navigate } from "svelte-routing";

  import Home from "./views/Home.svelte";
  import About from "./views/About.svelte";
  import RoutesTour from "./views/RoutesTour.svelte";
import { onMount } from "svelte";

let linkActive: string = '/'
let isActiveMenu: boolean = false;


 
 $:{
   console.log(linkActive)
   console.log(linkActive)
   console.log(linkActive)

 }

 const goRoute = ( selector ) => {
   return linkActive = selector;
   console.log('selector', selector)
   
 }

 const showMenu = () => {
  isActiveMenu = !isActiveMenu;
  console.log(isActiveMenu)
 }
</script>

<div>
  
<Router>
  <nav class="navbar navbar-expand-lg bg-light fixed-top shadow-sm">
    <div class="container-fluid">
      <button on:click={showMenu} class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" class:show="{ isActiveMenu }" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <Link to="/" class="nav-link" on:click={goRoute("/")} aria-current="page">Inicio</Link>
          <Link to="/about" class="nav-link" on:click={goRoute("/about")}>Acerca</Link>
          <Link to="/route-tour" class="nav-link" on:click={goRoute("router-tour")}>Rutas</Link>
  
        </div>
    </div>
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
