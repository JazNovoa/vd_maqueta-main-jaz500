<script>
    // Tu código permanece igual...
</script>

<!-- Añadimos el nuevo título -->
<div class="scrollable-content">
    <div class="title-container">
        <h1>Perros en Argentina</h1>
        <h2>¿GIGANTE / pequeño?</h2>
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
        overflow-x: scroll; /* Desplazamiento horizontal habilitado */
        height: 100vh; /* La altura ocupará toda la pantalla */
        background-color: #312783;
    }

    .title-container {
        flex: 0 0 100vw; /* Ocupa el ancho completo de la pantalla */
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: #312783;
    }

    .title-container h1 {
        font-size: 24px;
        font-weight: normal;
        text-transform: uppercase;
        margin-bottom: 10px;
        color: white;
    }

    .title-container h2 {
        font-size: 48px;
        font-weight: bold;
        text-transform: uppercase;
        margin-top: 0;
        color: white;
    }

    /* El contenido desplazable */
    .container {
        display: flex;
        flex-direction: row;
        gap: 50px; /* Separación entre el título y el contenido */
        min-width: 100vw; /* El contenedor ocupa al menos el ancho de la pantalla */
    }

    .chart {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
        gap: 50px; /* Más espacio entre los elementos */
    }

    .item_wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        min-width: 200px;
        margin-right: 20px;
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
        align-items: flex-end;
        gap: 10px;
    }

    .image-left, .image-right {
        object-fit: contain;
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
        color: #f6e81d;
    }

    .label-b {
        color: #e94e1b;
    }

    .year {
        margin-top: 10px;
        color: white;
        text-align: center;
    }
</style>
