<script lang="ts">
import BaseCard from "../components/BaseCard.svelte";

fetch("../../src/assets/data/routeData.json")
    .then(res => res.json())
    .then(routes => {
        console.log(routes)
        
        routes.routes.forEach(element => {
            let route = new RouteTour(element.title, element.price)
            route.addRoute(route)
        });
       
    })


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
<div class="container d-flex justify-content-center my-2">
    <BaseCard/>
</div>
    
<style>

</style>