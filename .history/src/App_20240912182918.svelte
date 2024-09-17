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

 
    // Script para desplazar horizontalmente con la rueda del ratón, usando requestAnimationFrame
    function handleWheel(event) {
        if (event.deltaY !== 0) {
            event.preventDefault();
            scrollAmount += event.deltaY * 8;  // Aumentamos la velocidad de scroll multiplicando por 5
            requestAnimationFrame(() => {
                document.querySelector('.scrollable-content').scrollLeft += scrollAmount;
            });
        }
    }

    // Esperar hasta que el DOM esté cargado para añadir el evento
    document.addEventListener('DOMContentLoaded', () => {
        document.addEventListener('wheel', handleWheel);
    });
</script>

<!-- Añadimos el nuevo título -->
<div class="scrollable-content">
    <div class="title-container">
        <img src="./images/titulo.svg" class="title-image">
    </div>

    <!-- Contenedor principal ya existente -->
    <div class="container">
        <!-- Todo tu código existente para las imágenes -->
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
    </div>
</div>

<style>
    /* Estilos para el título */
    .scrollable-content {
    display: flex;
    flex-direction: row;
    justify-content: flex-start; /* Para que el contenido siga desplazándose desde el inicio */
    align-items: center; /* Centra el contenido verticalmente */
    overflow-x: auto; /* Habilita el desplazamiento horizontal */
    height: 100vh; /* Ocupa toda la altura de la pantalla */
    background-color: #1d1d1b; /* Color de fondo */
    transform: translateY(-50px); /* Mueve todo el contenido 50px hacia arriba */
    padding-left: 50px; /* Mantiene un pequeño espacio a la izquierda */
}


.title-container {
    flex: 0 0 100vw; /* Ocupa el ancho completo de la pantalla */
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #1d1d1b;
}

.title-image {
    width: 150px; /* Ajusta el ancho según sea necesario */
    height: auto; /* Mantiene la proporción de la imagen */
}


    /* El contenido desplazable */
    .container {
    display: flex;
    flex-direction: row;
    gap: 50px;
    align-items: flex-end; /* Asegura que todo el contenido se alinee al final (parte inferior) */
    padding-left: 50px;
}

.chart {
    display: flex;
    justify-content: space-between;
    align-items: flex-end; /* Alinea todo el contenido desde la parte inferior */
    gap: 50px;
}

.item_wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end; /* Asegura que todo el contenido se mantenga alineado al fondo */
    min-width: 200px;
}

    .column {
        display: flex;
        justify-content: center;
        align-items: end;
        position: relative;
    }

    .image-group {
    display: flex;
    justify-content: space-between;
    align-items: flex-end; /* Asegura que las imágenes estén alineadas desde la parte inferior */
    gap: 10px;
    height: 300px; /* Fija la altura máxima del grupo de imágenes */
    position: relative; /* Esto permitirá que los números se ubiquen encima de las imágenes correctamente */
}

.image-left, .image-right {
    display: flex;
    align-items: flex-end; /* Alinea las imágenes al fondo */
    position: relative;
}

.label-a, .label-b {
    position: absolute;
    top: -20px;
    left: 50%;
    transform: translateX(-50%);
    font-weight: bold;
    font-size: 14px;
}

.label-a {
    color: #f190b8; /* Amarillo para serie_a */
}

.label-b {
    color: #a6cff0; /* Naranja para serie_b */
}

    .year {
        margin-top: 10px;
        color: white;
        text-align: center;
    }
</style>
