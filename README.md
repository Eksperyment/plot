<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Przestrzenna mapa bodźców emocjonalnych</title>
    <script src="https://cdn.plot.ly/plotly-2.30.0.min.js"></script>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: #111;
            color: #eee;
        }
        #plot {
            width: 100vw;
            height: 100vh;
        }
    </style>
</head>
<body>

<div id="plot"></div>

<script>
fetch("neo4j_query_table_data_2025-12-29_entropia.csv")
    .then(res => res.text())
    .then(text => {
        const lines = text.split("\n").slice(1);

        const x = [];
        const y = [];
        const colors = [];
        const labels = [];

        lines.forEach((line, i) => {
            if (!line.trim()) return;

            const cols = line.split('","').map(c => c.replace(/"/g,''));

            const s = cols[0];
            const r = cols[1];
            const e = cols[2];

            const emotion = /dominant_emotion:\s*([a-zA-Z_]+)/.exec(s);
            const intensity = /intensity:\s*([0-9.]+)/.exec(r);
            const color = /color:\s*(#[0-9A-Fa-f]{6})/.exec(e);

            if (!emotion || !intensity) return;

            x.push(parseFloat(intensity[1]));
            y.push(i); // pseudo-przestrzeń
            colors.push(color ? color[1] : "#888");

            labels.push(
                `Emocja: ${emotion[1]}<br>` +
                `Intensywność: ${intensity[1]}`
            );
        });

        const trace = {
            x,
            y,
            mode: "markers",
            type: "scattergl",
            text: labels,
            hoverinfo: "text",
            marker: {
                size: 10,
                color: colors,
                opacity: 0.8
            }
        };

        const layout = {
            title: "Przestrzenna mapa bodźców wywołujących emocje",
            paper_bgcolor: "#111",
            plot_bgcolor: "#111",
            xaxis: {
                title: "Intensywność emocji",
                gridcolor: "#333",
                color: "#eee"
            },
            yaxis: {
                title: "Przestrzeń bodźców",
                showticklabels: false,
                gridcolor: "#222",
                color: "#eee"
            }
        };

        Plotly.newPlot("plot", [trace], layout, {responsive: true});
    });
</script>

</body>
</html>
