<script lang="ts">
  import { Router, Link, Route } from "svelte-routing";

  import Home from "./views/Home.svelte";
  import About from "./views/About.svelte";
  import RoutesTour from "./views/RoutesTour.svelte";
  import Meta from './lib/Meta.svelte';

  let isActiveMenu: boolean = false;

  const metadata = {
		title: 'Yummy Tours',
		description: 'Somos una empresa de rutas gastronomicas por españa que fusiona gastronomia y cultura al mejor precio y con experiencias unicas en el sector , nuestra idea de negocio  surge de la necesidadde mezclar estos dos mundos que nos apasionan y crear una agencia dedicada exclusivamente para ello  , descubre que te ofrecemos en nuestra oficina de benalmadena o si lo prefieres en esta web , en la app o en nuestras redes , atrevete a saborear españa con nsostros y no te errepentiras',
		image: 'https://res.cloudinary.com/ddn278n2q/image/upload/v1654635403/meta-img/v6lkixqrchkl0q9glnea.jpg',
		imageAlt: 'Yummy Tours Logo',
		url:'https://yummytours.netlify.app'
	}

  const showMenu = () => {
  isActiveMenu = !isActiveMenu;
  console.log(isActiveMenu)
 }
</script>

<div>
  <Meta {metadata}/>
<Router>
  <nav class="navbar navbar-expand-lg bg-light fixed-top shadow-sm">
    <div class="container-fluid">
      <button on:click={showMenu} class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" class:show="{ isActiveMenu }" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <Link to="/" class="nav-link" aria-current="page">Inicio</Link>
          <Link to="/about" class="nav-link">Acerca</Link>
          <Link to="/route-tour" class="nav-link">Rutas</Link>
  
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
