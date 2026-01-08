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
{"id":30,"ar_mean":7.1758,"ar_sd":1.7528,"val_mean":6.7862,"val_sd":2.1129}
{"id":51,"ar_mean":7.4025,"ar_sd":0.9944,"val_mean":1.4339,"val_sd":1.1224},
{"id":52,"ar_mean":7.2125,"ar_sd":1.3097,"val_mean":2.1500,"val_sd":1.7273},
{"id":53,"ar_mean":7.4113,"ar_sd":1.2825,"val_mean":1.3607,"val_sd":0.8462},
{"id":54,"ar_mean":6.1257,"ar_sd":1.7090,"val_mean":3.1383,"val_sd":1.6283},
{"id":55,"ar_mean":6.7062,"ar_sd":1.5845,"val_mean":2.875,"val_sd":1.5930},
{"id":56,"ar_mean":6.7044,"ar_sd":1.7009,"val_mean":2.4654,"val_sd":1.5210},
{"id":57,"ar_mean":5.9685,"ar_sd":1.8086,"val_mean":4.0062,"val_sd":1.3756},
{"id":58,"ar_mean":6.4812,"ar_sd":1.9196,"val_mean":2.7875,"val_sd":1.5636},
{"id":59,"ar_mean":6.2641,"ar_sd":2.0234,"val_mean":3.9622,"val_sd":2.1608},
{"id":60,"ar_mean":6.7610,"ar_sd":1.5404,"val_mean":3.0062,"val_sd":1.6969},
{"id":61,"ar_mean":6.7312,"ar_sd":1.6998,"val_mean":3.625,"val_sd":2.0427},
{"id":62,"ar_mean":6.1069,"ar_sd":1.8711,"val_mean":3.3899,"val_sd":1.5667},
{"id":63,"ar_mean":5.7798,"ar_sd":1.9669,"val_mean":2.0566,"val_sd":1.3228},
{"id":64,"ar_mean":6.9562,"ar_sd":1.4766,"val_mean":3.575,"val_sd":2.2333},
{"id":65,"ar_mean":6.0000,"ar_sd":1.5861,"val_mean":4.65,"val_sd":1.7562},
{"id":66,"ar_mean":5.9620,"ar_sd":2.0716,"val_mean":3.3670,"val_sd":1.4817},
{"id":67,"ar_mean":6.8238,"ar_sd":1.5852,"val_mean":1.9496,"val_sd":1.3159},
{"id":68,"ar_mean":4.8125,"ar_sd":2.1137,"val_mean":1.8562,"val_sd":1.2581},
{"id":69,"ar_mean":5.9620,"ar_sd":1.8160,"val_mean":2.9050,"val_sd":1.5752},
{"id":70,"ar_mean":7.0628,"ar_sd":1.5617,"val_mean":1.9748,"val_sd":1.4881},
{"id":71,"ar_mean":5.95,"ar_sd":2.0274,"val_mean":3.8312,"val_sd":1.6794},
{"id":72,"ar_mean":5.0822,"ar_sd":2.1502,"val_mean":2.2215,"val_sd":1.5042},
{"id":73,"ar_mean":3.9240,"ar_sd":2.0674,"val_mean":3.0886,"val_sd":1.6056},
{"id":74,"ar_mean":5.500,"ar_sd":1.7483,"val_mean":2.2062,"val_sd":1.4840},
{"id":75,"ar_mean":3.8993,"ar_sd":2.3551,"val_mean":3.8301,"val_sd":1.5393},
{"id":76,"ar_mean":4.9496,"ar_sd":2.1518,"val_mean":2.1635,"val_sd":1.4046},
{"id":77,"ar_mean":3.9125,"ar_sd":2.0631,"val_mean":3.1062,"val_sd":1.5884},
{"id":78,"ar_mean":4.2594,"ar_sd":1.9717,"val_mean":3.2658,"val_sd":1.5033},
{"id":79,"ar_mean":5.6226,"ar_sd":2.0582,"val_mean":4.1949,"val_sd":1.8297},
{"id":80,"ar_mean":4.5875,"ar_sd":2.0106,"val_mean":3.0687,"val_sd":1.6411},
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
