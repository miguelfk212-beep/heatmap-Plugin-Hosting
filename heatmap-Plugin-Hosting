<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Widget de Forex Heatmap para cTrader</title>
    <style>
        /* Asegura que el widget ocupe toda la ventana sin márgenes */
        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            width: 100%;
            overflow: hidden; /* Evita barras de desplazamiento no deseadas */
            background-color: #1e1e1e; /* Color de fondo que coincide con el tema oscuro */
            font-family: Arial, sans-serif;
            color: #ffffff;
        }
        
        /* Contenedor principal */
        .main-container {
            display: flex;
            flex-direction: column;
            height: 100%;
            width: 100%;
        }
        
        /* Panel de control superior */
        .control-panel {
            background-color: #2a2a2a;
            padding: 10px;
            display: flex;
            align-items: center;
            border-bottom: 1px solid #444;
        }
        
        /* Estilo para los selectores */
        .control-group {
            margin-right: 15px;
            display: flex;
            align-items: center;
        }

        .control-group label {
            margin-right: 5px;
        }
        
        select {
            background-color: #3a3a3a;
            color: #ffffff;
            border: 1px solid #555;
            padding: 5px 10px;
            border-radius: 4px;
        }
        
        /* El contenedor donde se inyectará el widget */
        #tradingview-widget-container {
            flex-grow: 1;
            width: 100%;
            height: 100%; /* Asegura que el contenedor del widget tenga una altura definida */
        }
    </style>
</head>
<body>
    <div class="main-container">
        <!-- Panel de control superior -->
        <div class="control-panel">
            <div class="control-group">
                <label for="theme-select">Tema:</label>
                <select id="theme-select" onchange="updateHeatmap()">
                    <option value="dark">Oscuro</option>
                    <option value="light">Claro</option>
                </select>
            </div>
        </div>
        
        <!-- Este div es el ancla donde TradingView creará su widget -->
        <div id="tradingview-widget-container">
            <!-- El script de TradingView necesita esta estructura interna -->
            <div class="tradingview-widget-container__widget"></div>
        </div>
    </div>

    <script>
        /**
         * Función para actualizar el mapa de calor con el tema seleccionado.
         */
        function updateHeatmap() {
            // Obtener el valor del selector de tema
            const theme = document.getElementById('theme-select').value;

            console.log("Actualizando Heatmap con el tema:", theme);

            // 1. Obtener el contenedor principal del widget.
            const container = document.getElementById('tradingview-widget-container');
            
            // 2. Limpiar el contenido anterior de forma más robusta.
            //    Buscar y eliminar el script anterior.
            const oldScript = container.querySelector('script');
            if (oldScript) {
                container.removeChild(oldScript);
            }

            //    Buscar y eliminar el div interno del widget anterior.
            const oldWidgetDiv = container.querySelector('.tradingview-widget-container__widget');
            if (oldWidgetDiv) {
                container.removeChild(oldWidgetDiv);
            }
            
            // 3. Crear el nuevo div interno que TradingView necesita.
            const newWidgetDiv = document.createElement('div');
            newWidgetDiv.className = 'tradingview-widget-container__widget';
            container.appendChild(newWidgetDiv);
            
            // 4. Crear un nuevo elemento <script> para el widget de TradingView.
            const script = document.createElement('script');
            script.type = 'text/javascript';
            script.async = true;
            script.src = 'https://s3.tradingview.com/external-embedding/embed-widget-forex-heat-map.js';
            
            // 5. Definir la configuración del widget.
            //    Usamos la configuración por defecto de TradingView, solo cambiando el tema.
            script.innerHTML = JSON.stringify({
                "width": "100%",
                "height": "100%", // Ocupa todo el contenedor flexible
                "locale": "es",
                "colorTheme": theme,
                "dateRange": "12M", // Valor por defecto de TradingView
                "largeChartUrl": "",
                "isTransparent": false,
                "sortBy": "Change", // Valor por defecto de TradingView
                "gridSize": "large", // Valor por defecto de TradingView
                "conserveMemory": true,
                "chartType": "area"
            });
            
            // 6. Añadir el nuevo script al contenedor principal.
            container.appendChild(script);
        }

        /**
         * Función para inicializar el widget con la configuración por defecto cuando la página se carga.
         */
        function initializeWidget() {
            updateHeatmap();
        }

        // Ejecuta la función de inicialización cuando la página esté completamente cargada.
        window.onload = initializeWidget;

    </script>
</body>
</html>
