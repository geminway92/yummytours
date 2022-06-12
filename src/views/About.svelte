<script lang="ts">
let widthVideo: number = 300;

$:{
        if(screen.width > 600 ){
            widthVideo = 630
        }
    }

</script>
<div class="container d-flex flex-column justify-content-center align-items-center m-special">
    <video class="my-5" src="/assets/video/Video nuestra tienda.mp4" muted controls autoplay loop width={widthVideo}></video>
    <h1>Nuestra historia</h1>
    <p>Somos YOMMYTOURS , una empresa de rutas gastronomicas por españa que fusiona gastronomia y cultura al mejor precio y con experiencias unicas en el sector , nuestra idea de negocio  surge de la necesidadde mezclar estos dos mundos que nos apasionan y crear una agencia dedicada exclusivamente para ello  , descubre que te ofrecemos en nuestra oficina de benalmadena o si lo prefieres en esta web , en la app o en nuestras redes , atrevete a saborear españa con nsostros y no te errepentiras</p>

</div>

<style>

</style>