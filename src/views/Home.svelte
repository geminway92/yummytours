<script lang="ts">
import { Confetti } from "svelte-confetti"
import {navigate} from 'svelte-routing';

let isConfetti: Boolean = false;

const toggleButton = () => {
    isConfetti = !isConfetti
    navigate("/about", {replace: true})
}
</script>
<div class="bg-special d-flex justify-content-center align-items-center">
    <div class="container-confetti">

    <Confetti x={[-5, 5]} y={[0, 0.1]} delay={[500, 2000]} infinite duration=5000 amount=200 fallDistance="100vh" />
    </div>
    
    
    <img on:click={toggleButton} src="/src/assets/logo.png" alt="">

     

</div>

<style>
.bg-special{
    background-color: #351753;
    height: 100vh;
    
}
.container-confetti{
    position: fixed;
    top: -50px;
    left: 0;
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: center;
    overflow: hidden;
    pointer-events: none;
}

img{
    border: 5px solid #dfb0a2;
    cursor: pointer;

}

</style>