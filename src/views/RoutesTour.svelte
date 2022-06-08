<script lang="ts">
import { navigate } from "svelte-routing";

import BaseCard from "../components/BaseCard.svelte";

fetch("assets/data/routeData.json")
    .then(res => res.json())
    .then(routes => {
        routesArray = routes.routes;
        
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

let goRoute = (id: string) => {
     navigate(`/route/${id}`, {replace: true})
}
 
</script>
<div class="container w-75 d-flex flex-wrap justify-content-center m-special align-content-center gap-5 ">

        {#if routesArray}
        {#each routesArray as route}
        <div class="row">

            <div class="col">
                <BaseCard widthProp="300px"  {goRoute} photo={route['photo']} title={route['title']} subtitle={route['price']} textInfo={route['location']} />
            </div>
        </div>

        {/each}
        {/if}
</div>
    
<style>

</style>