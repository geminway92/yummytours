<script lang="ts">
import RoutesTour from "./RoutesTour.svelte";


export let params = {};

let routeList: Object[] = [];

fetch("/assets/data/routeData.json")
    .then(res => res.json())
    .then(routeData => {
        routeList = routeData['routes']
    })
    .catch(err => console.log(err));


    class CurrentRoute {
        #id: String = '';
        title: String = '';
        #price: number = 0;
        #photo: string = '';
        
        constructor(id: string, title: string, price: number, photo: string){
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

        findByID(routesList ){
            console.log(routesList, 'que trae')
            return routesList.find( route => route['title'] === this.#id)
        }
    }

    const currentRoute = new CurrentRoute(params['id'], params['id'], undefined, undefined)

    $:{
        if(routeList.length > 0){
            currentRoute.price = currentRoute.findByID(routeList)['price']
            currentRoute.photo = currentRoute.findByID(routeList)['photo']
            console.log(currentRoute)
        
        }
    }
    
        

</script>
{#if routeList}
     
<div class="m-special container w-100 d-flex flex-column align-items-center">
    <img src={currentRoute.photo} alt="imagen de {currentRoute.title}">
    <h1>{currentRoute.title}</h1>
    <p>Desde {currentRoute.price}</p>
</div>
{/if}