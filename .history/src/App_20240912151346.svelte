<!-- Script JS -->
<script>
    import * as d3 from "d3"
    let images2 = [
        "./images/perrogrande1.svg", 
        "./images/perrogrande9.svg", 
        "./images/perrogrande7.svg", 
        "./images/perrogrande10.svg", 
        "./images/perrogrande2.svg", 
        "./images/perrogrande3.svg", 
        "./images/perrogrande4.svg", 
        "./images/perrogrande5.svg", 
        "./images/perrogrande8.svg", 
        "./images/perrogrande6.svg",
    ]

    let images1 = [
        "./images/perrochico1.svg", 
        "./images/perrochico8.svg", 
        "./images/perrochico2.svg", 
        "./images/perrochico3.svg", 
        "./images/perrochico10.svg", 
        "./images/perrochico4.svg", 
        "./images/perrochico7.svg", 
        "./images/perrochico5.svg", 
        "./images/perrochico6.svg", 
        "./images/perrochico9.svg",
    ]

    let serie_a = [21, 33, 42, 54, 63, 71, 77, 84, 92, 98]
    let serie_b = [23, 35, 45, 56, 50, 43, 38, 32, 28, 25]
    let años = [2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023]
    
    let altura_a = d3
        .scaleLinear()
        .domain([0, d3.max(serie_a)])
        .range([0, 300])

    let altura_b = d3
        .scaleLinear()
        .domain([0, d3.max(serie_a)])
        .range([0, 300])  

    function getImage(index) {
        return images1[index] 
    }

    function preload(index) {
        return images2[index]
    }
    
</script>

<!-- Estructura contenido HTML -->   


<div class=titulos>
<h1 id="titulo"> <strong>¿GIGANTE</strong></h1>
<h1 id="titulo2"><strong>PEQUEÑO?</strong></h1>
<h2 id="subtitulo"> Cantidad de perros pequeños y gigantes por año </h2>
</div>    


<div class="chart">


<!--<div class= "container_2">
    {#each serie_b as num_2, i}
        <div class="item_wrapper">
            <p class="num2">{num_2}</p>
            <div class="column2" style="height: {altura(num_2)}px; background-image: url({preload(i)}]">
                <img src={preload(i)} alt="imagen" class="image-column2">
            </div>
        </div>
    {/each}
    </div>-->

    <div class="container_1">
        {#each serie_a as num_1, i}
            <div class="item_wrapper">
                <div class="num1"><p>{num_1}</p></div>
                <div class="num2"><p>{serie_b[i]}</p></div>
                <div class="column">
                    <div class="image-group">
                        <!-- images2 usa `altura_b` y serie_b -->
                        <div class="image-left"><img src={preload(i)} alt="imagen2" style="height: {altura_b(serie_b[i])}px;"></div>
                        <!-- images1 usa `altura_a` y serie_a -->
                        <div class="image-right"><img src={getImage(i)} alt="imagen1" style="height: {altura_a(num_1)}px;"></div>
                    </div>
                </div>


            </div>

        {/each}
    </div>


<div class= "años">
    {#each años as año, i}
    <p>{años[i]}</p>

    {/each}
</div>
<!--<div class="num2">
    {#each serie_b as num_2}
    <p>{num_2}</p>
        
    {/each}

</div>    

</div> -->

<div class="chart-wrapper">
    <div class="flourish-embed" data-src="story/2601108"><script src="https://public.flourish.studio/resources/embed.js"></script><noscript><img src="https://public.flourish.studio/story/2601108/thumbnail" width="100%" alt="visualization" /></noscript></div>
</div> 


</div>


<!-- Estilos CSS -->
<style>
   .chart {
    display: flex;

   }

    .container_1 {
        display: flex;
        justify-content: space-between;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 20px;
        margin-top: 10px;
        gap: 8px;
        align-items: end;
        
          
    }

    /*.container_2 {
        display: flex;
        justify-content: space-between;
        width: 1920px;
        height: 1080px;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 20px;
        margin-top: 10px;

        gap: 69px;


    }*/

    /*.container_3 {
        display: flex;
        width: 1920px;
        height: 85px;
        font-size: 21px;
        margin-left: 40px;
        margin-top: 330px;
        margin-bottom: 100px;
        justify-content: space-between;
        align-items: flex-end;
        color: white;
        position: absolute;
        gap: 180px;
    }*/

    .item_wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        /*justify-content: flex-end;
        margin-bottom: 40px;
        margin-left: 20px;
        align-items: end;
        gap: 10px;*/
    }

    .column {
        display: flex;
        justify-content: center;
        align-items: end;
        margin-bottom: 700px;
    }

    .image-group {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
        gap: 10px;
        
    }

    .image-left, .image-right {
        width: auto;
        object-fit: contain;
    }

    .image-right{
        margin-right: 10px;   
    }

    .image-left{
        margin-left: 20px;
    }

    .num1, .num2, .años {
        text-align: center;
        margin: 10px 0;
    }

    .num1{
        color: #f6e81d;
        margin-left: 60px;
        margin-top: 50px;
        position: absolute;
    }

    .num2{
        color: #e94e1b;
        margin-right: 70px;
        margin-top: 50px;
        
    }

    .años{
        display: flex;
        flex-direction: row;
        gap: 200px;
        margin-top: 420px;
        margin-left: 47px;
        color: white;
        position: absolute;
    }

    
    /*.num1 {
        display: flex;
        font-size: 21px;
        margin: 0;
        margin-bottom: 1000px;
        color: #f6e81d;
        position: absolute;
        gap: 50px;
        margin-right: 30px;
    }
    
    .num2{
        display: flex;
        font-size: 21px;
        margin: 0;
        margin-bottom: 1000px;
        margin-left: 10px;
        color: #e94e1b;
        position: absolute;
        gap: 50px;
        margin-right: 40px;
    }*/
    
    
    .chart-wrapper {
        width: 1100px;
        height: 550px;
        margin: auto;
        margin-top: 500px;
        margin-bottom: 10px;
    }
    
    .flourish-embed{
        display: flex;
        justify-content: flex-start;
        

    }

    .titulos {
        display: flex;
        width: 100%;
        height: 85px;
        margin-bottom: 0px;

    }


    #titulo{ 
        width: 100%;
        height: 70px;
        text-align: left;
        font-size: 40px;
        margin-bottom: 0;
        color: #e94e1b;
        position:absolute;
        margin-left: 60px;
        
    }

    #subtitulo {
        width: 100%;
        height: 70px;
        text-align: left;
        font-size: 20px;
        color: white;
        margin-top: 50px;
        margin-left: 40px;
    }

    #titulo2 {
        width: 1024px;
        height: 70px;
        text-align: left;
        font-size: 40px;
        margin-bottom: 0;
        color: #f6e81d;
        position: absolute;
        margin-left: 260px;

    }

    :global(body) {
        background-color: #312783; 
    }
   

    
</style>
