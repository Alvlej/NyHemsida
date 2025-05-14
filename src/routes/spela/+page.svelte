<script>
	import { filter } from "@skeletonlabs/skeleton";


    let frågor = [{fråga: "Vilket av alternativen är världens snabbaste bil?", svar: "Koenigsegg Agera RS" , alternativ: ["Lamborghini huracán", "Pagani huayra", "Koenigsegg Agera RS", "Bugatti Chiron"]},
                {fråga: "Vilket bilmärke har fyra ringar i sin logga?", svar: "Audi" , alternativ: ["BMW", "Audi", "Volkswagen", "Mercedes"]},
                {fråga: "Vilket bilmärke har en logotyp med en tjur?", svar: "Lamborghini" , alternativ: ["Lamborghini", "Porsche", "Ferrari", "Maserati"]}
                ,{fråga: "Vilken bil är känd som 'The Godfather'?", svar: "Cadillac" , alternativ: ["Cadillac", "Chevrolet", "Ford", "Buick"]},
                {fråga: "Vilket bilmärke tillverkar modellen “911”?", svar: "Porsche" , alternativ: ["Mercedes-Benz", "Volvo", "Ford", "Porsche"]},
                {fråga: "vilken bil har mest hästkrafter i världen?", svar: "Koenigsegg Gemera HV8" , alternativ: ["Koenigsegg Gemera HV8", "Lamborghini huracan SVJ", "Ferrari Laferrari", "Bugatti Chiron",]},
                {fråga: "Vilket bilmärke tillverkar modellen “911”?", svar: "Porsche" , alternativ: ["Mercedes-Benz", "Volvo", "Ford", "Porsche"]},
                {fråga: "Vilket land är känd för att tillvärka driftsäkra bilar”?", svar: "Japan" , alternativ: ["Japan", "USA", "Sverige", "Italien"]},
                {fråga: "Vilket land har flest invånare i världen?", svar: "Indien" , alternativ: ["Ryssland", "USA", "Kina", "Indien"]},
                {fråga: "Hur många olika smaker har Nocco producerat?", svar: "40" , alternativ: ["10", "25", "30", "40"]},
                {fråga: "Vilken är världens mest sålda bil genom tiderna?", svar: "Toyota Corolla" , alternativ: ["Honda Civic", "Toyota Corolla", "Lamborginhi Urus", "Mercedes-Benz G63",]},
                {fråga: "Vilket är max HCP i golf?", svar: "54" , alternativ: ["42", "52", "31", "54",]},
                {fråga: "vilken är den mäst köpta pizzan i världen?", svar: "Vesuvio" , alternativ: ["Havaii", "Kebabpizza", "Margherita", "Vesuvio",]},

]

    let priser = [{pris:"1 000 000", ratt:false},
                {pris:"500 000", ratt:false},
                {pris:"250 000", ratt:false},
                {pris:"100 000", ratt:false},
                {pris:"50 000", ratt:false},
                {pris:"25 000", ratt:false},
                {pris:"10 000", ratt:false},
                {pris:"5 000", ratt:false},
                {pris:"1 000", ratt:false}];

            

    let fråga = frågor[0];
    

    function kontrolleraSvar(alt) {
        if (alt == fråga.svar) {
            for (let i = priser.length; i > 0; i--) {
                if (priser[i-1].ratt == false) {
                    priser[i-1].ratt = true;
                    priser = priser
                    console.log(priser)
                    break;
                }
            }
        }
    
        else {
            alert("Fel svar!");
            for (let i = 0; i < priser.length; i++) {
                if (priser[i].ratt == true) {
                    priser[i].ratt = false;
                    priser = priser
                    console.log(priser)
                    break;
                }
            }
        }

        if (priser.filter(pris => pris.ratt == true).length >=9) {
            alert("Grattis du har vunnit 1 000 000 kr!");
        }

        nyFråga()
    }

    function nyFråga() {
        let randomIndex = Math.floor(Math.random() * frågor.length);
        fråga = frågor[randomIndex];
    }

    import { onMount } from "svelte";

    let timeLeft = 30; 
    let timer;

   
    onMount(() => {
        startTimer();
    });

    function startTimer() {
        timer = setInterval(() => {
            if (timeLeft > 0) {
                timeLeft--;
            } else {
                clearInterval(timer);
                alert("Tiden är slut!");
                nyFråga();   
            }
        }, 1000); 
    }

    function resetTimer() {
        clearInterval(timer);
        timeLeft = 30; 
        startTimer();
    }

    function andra(){

    }

</script>

<div class="timer">
    Tid kvar: {timeLeft} sekunder
</div>

<div class = "andrachansen">
    
    <img src="https://images.vexels.com/media/users/3/129190/isolated/preview/c3e00e75d5fb9997379e299db384f34c-50-percent-orange-ring-infographic.png" alt="Andra chansen"/>

</div>

<div class = "container">
    <div class= "fråga">{fråga.fråga}</div>
    <div class="svarsAlt">
        {#each fråga.alternativ as alt}
            <div class = "box"on:click={() => kontrolleraSvar(alt)}>
                <p>{alt}</p>
            </div>
        {/each}
    </div>
</div>

<ul class = "score">
    {#each priser as pris}
        <li class:correct = {pris.ratt}>💰{pris.pris} kr</li>
    {/each}
</ul>

<div class="backdrop">
    <img alt="" src ="https://thumbs.dreamstime.com/b/modern-quiz-show-stage-interior-bright-spotlights-illuminate-circular-dais-large-digital-screen-displays-questions-colorful-348791856.jpg">
</div>

<style>
     
    .backdrop{
    background-size: cover;
    position: fixed;
    top: 0;
    left: 0;
    z-index: -1;
    filter: blur(3px);
    }



.svarsAlt{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
}

.container {
    display: grid;
    grid-template-rows: 1fr 3fr;
    width: 50vw;
    height: 70vh;
    background-color: rgba(255, 255, 255, 0.8);
    margin: auto;
    border-radius: 20px;
    font-size: larger;
    font-weight: 800;
        
    
    
    
}

.backdrop img{
    width: 100vw;
    height: 100vh;
    }

    .box{
    width: 300px;
    height: 100px;
    background-color: darkblue;
    margin: auto;
    margin-top: 20%;
    border-radius: 20px;
    text-align: center;
    

  
}
.box:hover{
        transform: scale(1.05);

     }
    .box{ width: 100%; border-radius: 20px; border: 2px solid darkgoldenrod;background-color: darkblue;box-shadow: 4px 8px 0px rgba(0,0,0,0.10);}
    .box { flex-grow:2; transition: 1000ms flex; }
    

.fråga{
    background-color: orange;
    height: 150px;
    font-weight: 800;
    font-size: xx-large;
    text-align: center;
    padding-top: 20px;
    border-radius: 20px;
}
.score{
    height: 800px;
    width: 300px;
    background-color:darkblue;
    margin-left: 80%;
    margin-top: -40%;
    border-radius: 20px;
    padding: 50px;
    font-size: xx-large;
}

li {
    padding-bottom: 60px;
    color: white;
    font-size: x-large;
    font-weight: 800;
    
}
.correct {
    color: greenyellow;
    font-size: xx-large;
    font-weight: 1000;
}

.timer {
        font-size: 1.5rem;
        font-weight: bold;
        color: white;
        position: fixed;
        text-align: center;
        margin-top: 20px;
    }
.andrachansen{
    width: 100px;
    height: 100px;
    background-color: white;
    position: absolute;
    margin-top: 10%;
    margin-left: 5%;
    border-radius: 50%;
    
    
    
}

</style>

