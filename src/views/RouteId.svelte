<script lang="ts">
import RoutesTour from "./RoutesTour.svelte";


export let params = {};

let routeList: Object[] =  [];


fetch("/public/assets/data/routeData.json")
    .then(res => res.json())
    .then(routeData => {
        
        routeList = routeData.routes;
        searchRoute()
    })


    const searchRoute = () => {
        const test = routeList.filter( route => route['title'] === params['id'])
        console.log(test)
        console.log(routeList)
    }

    // class CurrentRoute {
    //     constructor(title)
    // }

</script>

<div class="m-special">

    <h1>ROUTE</h1>
    <p>{params['id']}</p>
</div>