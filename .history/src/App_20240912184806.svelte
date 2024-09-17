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
        <!-- Imagen del título -->
        <img src="./images/titulo.svg" alt="Título de Perros en Argentina" class="title-image">
    </div>

    <!-- Contenedor que agrupa el texto descriptivo y el gráfico -->
    <div class="content-container">
        <!-- Texto descriptivo -->
        <div class="description-container">
            <p class="description-text">
                En los últimos años, la cantidad de perros en Argentina ha aumentado, reflejando una creciente tendencia a tener mascotas.  
                A continuación, se presentará un gráfico que muestra cómo se ha distribuido esta población canina en términos de tamaño a lo largo de los años, diferenciando cuántos de estos perros son pequeños y cuántos son gigantes.
            </p>
        </div>

        <!-- Contenedor principal ya existente -->
        <div class="container">
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
</div>


<style>
    /* Estilos para el título */
 /* Estilos generales */
.scrollable-content {
    display: flex;
    flex-direction: column; /* Apila verticalmente el título y el contenedor desplazable */
    height: 100vh; /* Ocupa toda la altura de la pantalla */
    background-color: #1d1d1b; /* Color de fondo */
}

.title-container {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #1d1d1b;
    padding: 20px 0; /* Espacio alrededor del título */
}

.title-image {
    width: 150px; /* Ajusta el ancho según sea necesario */
    height: auto; /* Mantiene la proporción de la imagen */
}

.content-container {
    display: flex;
    flex-direction: row; /* Alinea el texto y el gráfico en una fila */
    gap: 20px; /* Espacio entre el texto y el gráfico */
    overflow-x: auto; /* Habilita el desplazamiento horizontal */
    padding: 20px; /* Espacio alrededor del contenido */
}

.description-container {
    flex: 0 0 auto; /* Ajusta el tamaño del contenedor de texto automáticamente */
    max-width: 400px; /* Ancho máximo del texto descriptivo */
}

.description-text {
    color: white; /* Color del texto */
    font-size: 16px; /* Tamaño de la fuente */
    line-height: 1.5; /* Altura de línea para mejor legibilidad */
}

.container {
    flex: 1; /* Permite que el contenedor del gráfico ocupe el espacio restante */
    display: flex;
    flex-direction: row;
    overflow-x: auto; /* Habilita el desplazamiento horizontal */
}

.chart {
    display: flex;
    gap: 20px; /* Espacio entre los elementos del gráfico */
    align-items: flex-end; /* Alinea el gráfico desde el fondo */
}

.item_wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-width: 200px;
}

.column {
    display: flex;
    justify-content: center;
    align-items: flex-end;
    position: relative;
}

.image-group {
    display: flex;
    gap: 10px;
    height: 300px; /* Fija la altura máxima del grupo de imágenes */
    position: relative;
}

.image-left, .image-right {
    display: flex;
    align-items: flex-end;
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
