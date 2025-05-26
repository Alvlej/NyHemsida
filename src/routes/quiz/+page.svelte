<script>
    import {base} from '$app/paths';

</script>

<main>

<div class = "ruta"> 
    <a href="{base}\spela">
        <p class = "spel">Spela</p>
    </a>

</div>

</main>



<style>



main{
    background-image: url("https://t3.ftcdn.net/jpg/03/00/27/36/360_F_300273615_iYVmicXE77f8waxfq9HxVll7R28Vl2CJ.jpg");
    background-size: cover;
    width: 100vw;
    height: 100vh;
    font-weight:600;
}
.spela{
    display: flex;
    font-size: xx-large;

    
}

.ruta{
    background-color: green;
    border-radius: 5px;
    justify-self: center;
    align-self: center;
    height: 100px;
    width: 200px;
    

    
    
}
.spel{
    text-align: center;
    font-size: 70px;
    color: white;
    font-weight: 800;
    padding-top: 30px;
}
</style>