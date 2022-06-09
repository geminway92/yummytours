<script lang="ts">
import RoutesTour from "./RoutesTour.svelte";


export let params = {};

let routeList: Object[] = [];
let route: Object = {}
let widthIframe: number = 300;

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
        #output: string[] = [];
        #brochure: string = '';
        #video: string[] = [];
        
        constructor(id: string, title: string, price: number, photo: string, output: string[]){
            this.#id = id;
            this.title = title;
            this.#price = price;
            this.#photo = photo;
            this.#output = output;
            this.#brochure;
            this.#video;
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
        
        get output(){
            return this.#output;
        }

        get brochure(){
            return this.#brochure;
        }

        get video(){
            return this.#video;
        }
        
        set price(newPrice: number){
            this.#price =  newPrice;
        }

        set photo(newImg: string){
            this.#photo = newImg;
        }

        set output(newOutput: string[]){
            this.#output = newOutput;
        }

        set brochure(newBrochure){
            this.#brochure = newBrochure;
        }

        set video(newVideo){
            this.#video = newVideo;
        }

        findByID(routesList: object[] ){
            return routesList.find( route => route['title'] === this.#id)
        }
    }

    const currentRoute = new CurrentRoute(params['id'], params['id'], undefined, undefined, [])

    $:{
        if(routeList.length > 0){
            const key = ['price','photo','output','brochure','video']
            
            route = currentRoute.findByID(routeList)
            key.forEach(key => {
                currentRoute[key] = route[key]
            });
        
        }
    }

    $:{
        if(screen.width > 600){
            widthIframe = 630
        }
    }


</script>
{#if currentRoute.price}
     
<div class="m-special container w-100 d-flex flex-column align-items-center">
    <img class="rounded photo-tour" src={currentRoute.photo} alt="imagen de {currentRoute.title}">
    <h1>{currentRoute.title}</h1>
    <div class="w-75 d-flex justify-content-start align-items-center gap-2">
        <img class="svg" src="/assets/svg/euro.svg" alt="svg euro">
        <p class="m-0">Desde {currentRoute.price} €</p>
    </div>
    <div class="w-75 d-flex justify-content-start align-items-center gap-2">
        <img class="svg" src="/assets/svg/salida.svg" alt="svg salida">
        <p class="m-0">Salida: {currentRoute.output}</p>
    </div>
    

    <a class="btn btn-primary py-3 my-3" target="_black" href="{currentRoute.brochure}">Descargar Folleto</a>
    
    {#each currentRoute.video as video}
        <iframe class="m-3" width="{widthIframe}" height="315" src={video} title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    {/each}
    
</div>
{:else}
<div class="container m-special  d-flex justify-content-center align-items-center">

    <div class="spinner-border" style="width: 3rem; height: 3rem;" role="status">
        <span class="sr-only">Loading...</span>
    </div>
</div>
    
{/if}

<style>
.photo-tour{
    width: 80%;
    height: 200px;
    object-fit: cover;
}

.svg{
    width: 20px;
    height: 20px;
}


@media screen and (min-width:768px){
    img{
        height: 400px;
    }
}

</style>