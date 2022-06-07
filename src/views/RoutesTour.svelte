<script lang="ts">
import BaseCard from "../components/BaseCard.svelte";

fetch("assets/data/routeData.json")
    .then(res => res.json())
    .then(routes => {
        // console.log(routes)
        routesArray = routes.routes;
        
        routes.routes.forEach(element => {
            let route = new RouteTour(element.title, element.price)
            route.addRoute(route)
        });
       
    })

let routesArray: object[] = [];
class RouteTour {
    #title: string = '';
    #price: number = 0;
    routes: Object[];
    constructor(title:string , price: number) {
        this.#title = title;
        this.#price = price

        this.routes = [];
        
    }

    showRoute(){
        console.log(this.#price, this.#title)
    }

    addRoute(route: Object){
        this.routes.push(route)
    }
}
const ruta2 = new RouteTour('Cádiz', 250)
ruta2.showRoute()

 
</script>
<div class="container d-flex flex-column justify-content-center m-special align-items-center gap-5 ">
    {#if routesArray}
    {#each routesArray as route}
        
         <BaseCard photo={route['photo']} title={route['title']} subtitle={route['price']} textInfo={route['location']} />
         {/each}
    {/if}
</div>
    
<style>
:global(.m-special){
    margin-top: 5rem;
}
</style>