<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<title>Mapa pobudzenia i wartościowania bodźców</title>
<script src="https://cdn.plot.ly/plotly-2.30.0.min.js"></script>

<style>
body {
    margin: 0;
    background: #111;
    color: #eee;
    font-family: Arial, sans-serif;
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
const stimuli = [
{"id":1,"ar_mean":5.9308,"ar_sd":1.8964,"val_mean":8.2893,"val_sd":1.3185},
{"id":2,"ar_mean":5.7421,"ar_sd":2.1205,"val_mean":8.3145,"val_sd":1.4804},
{"id":3,"ar_mean":4.4125,"ar_sd":2.5975,"val_mean":8.4688,"val_sd":1.1705},
{"id":4,"ar_mean":6.1572,"ar_sd":1.9890,"val_mean":8.5346,"val_sd":1.1011},
{"id":5,"ar_mean":5.0126,"ar_sd":2.1287,"val_mean":8.3396,"val_sd":1.1737},
{"id":6,"ar_mean":4.7813,"ar_sd":2.3019,"val_mean":8.2516,"val_sd":1.2626},
{"id":7,"ar_mean":4.8038,"ar_sd":2.2232,"val_mean":8.1572,"val_sd":1.4029},
{"id":8,"ar_mean":4.7421,"ar_sd":2.2340,"val_mean":8.0377,"val_sd":1.4764},
{"id":9,"ar_mean":4.9277,"ar_sd":2.2854,"val_mean":7.9748,"val_sd":1.4945},
{"id":10,"ar_mean":4.5660,"ar_sd":2.3513,"val_mean":7.9371,"val_sd":1.5422},
{"id":11,"ar_mean":4.5031,"ar_sd":2.4109,"val_mean":7.8679,"val_sd":1.5613},
{"id":12,"ar_mean":4.7358,"ar_sd":2.3624,"val_mean":7.8113,"val_sd":1.6057},
{"id":13,"ar_mean":4.8302,"ar_sd":2.3308,"val_mean":7.7547,"val_sd":1.6321},
{"id":14,"ar_mean":4.9623,"ar_sd":2.2744,"val_mean":7.6918,"val_sd":1.6643},
{"id":15,"ar_mean":5.1321,"ar_sd":2.2199,"val_mean":7.6415,"val_sd":1.7028},
{"id":16,"ar_mean":5.2579,"ar_sd":2.1832,"val_mean":7.5849,"val_sd":1.7336},
{"id":17,"ar_mean":5.3962,"ar_sd":2.1450,"val_mean":7.5220,"val_sd":1.7631},
{"id":18,"ar_mean":5.5283,"ar_sd":2.1097,"val_mean":7.4717,"val_sd":1.7936},
{"id":19,"ar_mean":5.6604,"ar_sd":2.0764,"val_mean":7.4151,"val_sd":1.8202},
{"id":20,"ar_mean":5.8050,"ar_sd":2.0412,"val_mean":7.3585,"val_sd":1.8479},
{"id":21,"ar_mean":5.9434,"ar_sd":2.0068,"val_mean":7.2956,"val_sd":1.8725},
{"id":22,"ar_mean":6.0881,"ar_sd":1.9715,"val_mean":7.2390,"val_sd":1.9008},
{"id":23,"ar_mean":6.2201,"ar_sd":1.9402,"val_mean":7.1824,"val_sd":1.9263},
{"id":24,"ar_mean":6.3522,"ar_sd":1.9116,"val_mean":7.1258,"val_sd":1.9547},
{"id":25,"ar_mean":6.4843,"ar_sd":1.8839,"val_mean":7.0692,"val_sd":1.9794},
{"id":26,"ar_mean":6.6226,"ar_sd":1.8571,"val_mean":7.0126,"val_sd":2.0069},
{"id":27,"ar_mean":6.7609,"ar_sd":1.8294,"val_mean":6.9560,"val_sd":2.0338},
{"id":28,"ar_mean":6.8992,"ar_sd":1.8031,"val_mean":6.8994,"val_sd":2.0601},
{"id":29,"ar_mean":7.0375,"ar_sd":1.7775,"val_mean":6.8428,"val_sd":2.0873},
{"id":30,"ar_mean":7.1758,"ar_sd":1.7528,"val_mean":6.7862,"val_sd":2.1129},
{"id":31,"ar_mean":2.7484,"ar_sd":2.5630,"val_mean":8.1069,"val_sd":1.3197},
{"id":32,"ar_mean":6.1823,"ar_sd":2.0027,"val_mean":8.2578,"val_sd":1.3650},
{"id":33,"ar_mean":2.1437,"ar_sd":2.5448,"val_mean":8.2875,"val_sd":1.3753},
{"id":34,"ar_mean":5.2562,"ar_sd":2.3127,"val_mean":7.7625,"val_sd":1.5233},
{"id":35,"ar_mean":5.2974,"ar_sd":2.4612,"val_mean":7.4240,"val_sd":1.8726},
{"id":36,"ar_mean":4.9430,"ar_sd":2.4682,"val_mean":8.3797,"val_sd":1.2599},
{"id":37,"ar_mean":4.7437,"ar_sd":2.6427,"val_mean":8.1250,"val_sd":1.3906},
{"id":38,"ar_mean":3.1062,"ar_sd":2.4587,"val_mean":8.4187,"val_sd":0.9280},
{"id":39,"ar_mean":4.7784,"ar_sd":2.1013,"val_mean":3.3417,"val_sd":1.7033},
{"id":40,"ar_mean":7.0314,"ar_sd":1.5443,"val_mean":1.1509,"val_sd":0.7043},
{"id":41,"ar_mean":6.3937,"ar_sd":1.5544,"val_mean":1.6562,"val_sd":1.0034},
{"id":42,"ar_mean":7.1518,"ar_sd":1.4549,"val_mean":1.7468,"val_sd":1.4582},
{"id":43,"ar_mean":5.1509,"ar_sd":2.1500,"val_mean":3.3773,"val_sd":2.0857},
{"id":44,"ar_mean":6.8625,"ar_sd":1.4729,"val_mean":1.2875,"val_sd":0.7638},
{"id":45,"ar_mean":6.3057,"ar_sd":1.7746,"val_mean":1.4683,"val_sd":1.1711},
{"id":46,"ar_mean":5.1194,"ar_sd":1.7695,"val_mean":3.2830,"val_sd":1.7141},
{"id":47,"ar_mean":5.3312,"ar_sd":1.7899,"val_mean":2.1500,"val_sd":1.3972},
{"id":48,"ar_mean":5.7421,"ar_sd":1.8698,"val_mean":1.7987,"val_sd":1.3537},
{"id":49,"ar_mean":6.3144,"ar_sd":1.5513,"val_mean":1.6037,"val_sd":1.1419},
{"id":50,"ar_mean":6.4493,"ar_sd":1.5661,"val_mean":2.4367,"val_sd":1.4734},
];

const x = [];
const y = [];
const labels = [];
const hover = [];

stimuli.forEach(d => {
    x.push(d.val_mean);
    y.push(d.ar_mean);
    labels.push(d.id.toString());
    hover.push(
        `<b>Bodziec ${d.id}</b><br>` +
        `Wartościowanie: ${d.val_mean.toFixed(2)} ± ${d.val_sd.toFixed(2)}<br>` +
        `Pobudzenie: ${d.ar_mean.toFixed(2)} ± ${d.ar_sd.toFixed(2)}`
    );
});

Plotly.newPlot("plot", [{
    x,
    y,
    mode: "markers+text",
    type: "scatter",
    text: labels,
    textposition: "middle center",
    hoverinfo: "text",
    hovertext: hover,
    marker: {
        size: 22,
        color: "#00c8ff",
        opacity: 0.85,
        line: { color: "#000", width: 1 }
    }
}], {
    title: "Dwuwymiarowa mapa bodźców eksperymentalnych",
    paper_bgcolor: "#111",
    plot_bgcolor: "#111",
    xaxis: {
        title: "Wartościowanie (średnia)",
        color: "#eee",
        zerolinecolor: "#444"
    },
    yaxis: {
        title: "Pobudzenie (średnia)",
        color: "#eee",
        zerolinecolor: "#444"
    }
}, { responsive: true });
</script>

</body>
</html>
