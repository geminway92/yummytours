<script>
export let title;
export let subtitle;
export let photo;
export let textInfo;
export let goRoute;
export let widthProp;

</script>


<div on:click={goRoute(title)} class="card mx-2 shadow-lg" style="width: {widthProp};">
    <img class="h-50 " src={photo} alt="">
    
    <div class="container w-100 position-absolute bottom-0  p-3 d-flex flex-column">
        <h1 class="fs-4">{title}</h1>
        <p>{textInfo}</p>
        <hr>
        <p class="text-center">Desde: {subtitle}€</p>
    </div>
    
</div>

<style>
img {
    object-fit: cover;
    border-radius: 1rem 1rem 0 0;
}    
.card{
    border-radius: 1rem ;
    cursor: pointer;
    transition: .5s;
    height: 400px;
}

.card:hover{
    transform: scale(1.05);
}

</style>