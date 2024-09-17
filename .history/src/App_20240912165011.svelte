<script>
    import * as d3 from "d3";
    
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
    ];

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
    ];

    let serie_a = [21, 33, 42, 54, 63, 71, 77, 84, 92, 98];
    let serie_b = [23, 35, 45, 56, 50, 43, 38, 32, 28, 25];
    let años = [2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023];
    
    let altura_a = d3
        .scaleLinear()
        .domain([0, d3.max(serie_a)])
        .range([0, 300]);

    let altura_b = d3
        .scaleLinear()
        .domain([0, d3.max(serie_a)])
        .range([0, 300]);  

    function getImage(index) {
        return images1[index];
    }

    function preload(index) {
        return images2[index];
    }
</script>

    <div class="chart">
        {#each serie_a as num_1, i}
            <div class="item_wrapper">
                <div class="column">
                    <div class="image-group">
                        <div class="image-left">
                            <p class="label-b">{serie_b[i]}</p> <!-- Texto de serie_b -->
                            <img src={preload(i)} alt="imagen2" style="height: {altura_b(serie_b[i])}px;">
                        </div>
                        <div class="image-right">
                            <p class="label-a">{num_1}</p> <!-- Texto de serie_a -->
                            <img src={getImage(i)} alt="imagen1" style="height: {altura_a(num_1)}px;">
                        </div>
                    </div>
                </div>
                <div class="year">{años[i]}</div>
            </div>
        {/each}
    </div>

<style>
    :global(body) {
        background-color: #312783; 
        font-family: 'Noto Sans JP', sans-serif; /* Aplica la tipografía a todo el cuerpo */
        overflow-x: hidden; /* Evita el desplazamiento horizontal en el cuerpo */
    }

    .container {
        display: flex;
        flex-direction: row;
        overflow-x: auto; /* Habilita el desplazamiento horizontal */
        white-space: nowrap; /* Evita el ajuste de línea */
        width: 100vw; /* Asegura que el contenedor ocupe todo el ancho de la ventana */
    }

    .chart {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
        margin: 20px 0;
        gap: 50px; /* Más espacio entre los elementos */
    }

    .item_wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-right: 20px;
        min-width: 200px; /* Asegura que cada item tenga un ancho mínimo */
    }

    .column {
        display: flex;
        justify-content: center;
        align-items: end;
        position: relative; /* Necesario para posicionar los números */
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
        position: relative; /* Necesario para que los textos estén sobre las imágenes */
    }

    .label-a {
        position: absolute;
        top: -20px; /* Ajusta este valor según sea necesario */
        left: 50%;
        transform: translateX(-50%);
        color: #f6e81d; /* Color amarillo para serie_a */
        font-weight: bold;
        font-size: 14px;
    }

    .label-b {
        position: absolute;
        top: -20px; /* Ajusta este valor según sea necesario */
        left: 50%;
        transform: translateX(-50%);
        color: #e94e1b; /* Color naranja para serie_b */
        font-weight: bold;
        font-size: 14px;
    }

    .year {
        margin-top: 10px;
        color: white;
        text-align: center;
    }

   
</style>
