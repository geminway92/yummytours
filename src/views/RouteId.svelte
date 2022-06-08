<script lang="ts">
import RoutesTour from "./RoutesTour.svelte";


export let params = {};

let routeList: Object[] =  [];

fetch("/public/assets/data/routeData.json")
    .then(res => res.json())
    .then(routeData => {
        routeList = routeData.routes;
    })


    class CurrentRoute {
        #id: String = '';
        title: String = '';
        #price: number = 0;
        #photo: string = '';
        
        constructor(id: string, title: string, price?: number, photo?: string){
            this.#id = id;
            this.title = title;
            this.#price = price;
            this.#photo = photo;
        }

        get id(){
            return this.#id
        }

        get price(){
            return this.#price;
        }

        get photo(){
            return this.#photo;
        }
        
        set price(newPrice: number){
            this.#price =  newPrice;
        }

        set photo(newImg: string){
            this.#photo = newImg;
        }

        findByID(){
            return routeList.find( route => route['title'] === this.#id)
        }
    }

    const currentRoute = new CurrentRoute(params['id'], params['id'])
    $:{
        if(routeList.length > 0){
            currentRoute.price = currentRoute.findByID()['price']
            currentRoute.photo = currentRoute.findByID()['photo']
        }
    }
    
        

</script>
{#if currentRoute}
     
<div class="m-special container w-100 d-flex flex-column align-items-center">
    <img src={currentRoute.photo} alt="">
    <h1>{currentRoute.title}</h1>
    <p>Desde {currentRoute.price}</p>
</div>
{/if}