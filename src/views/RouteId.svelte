<script lang="ts">
import RoutesTour from "./RoutesTour.svelte";


export let params = {};

let routeList: Object[] =  [];


fetch("/public/assets/data/routeData.json")
    .then(res => res.json())
    .then(routeData => {
        
        routeList = routeData.routes;

        const currentRoute = new CurrentRoute(params['id'], params['id'])
        currentRoute.price = currentRoute.findByID()['price']
        

        console.log(currentRoute)
        

    })


    class CurrentRoute {
        #id: String = '';
        title: String = '';
        #price: number = 0;
        
        constructor(id: string, title: string, price?: number){
            this.#id = id;
            this.title = title;
            this.#price = price;
        }

        get id(){
            return this.#id
        }

        get price(){
            return this.#price;
        }
        
        set price(newPrice: number){
            this.#price =  newPrice;
        }

        findByID(){
            return routeList.find( route => route['title'] === this.#id)
        }
    }

</script>

<div class="m-special">

    <h1>ROUTE</h1>
    <p>{params['id']}</p>
</div>