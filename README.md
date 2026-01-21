<!DOCTYPE html>
<html>
<head>
  <title>Admin Dashboard</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body { font-family: Arial; background:#eef; padding:20px; }
    h2 { text-align:center; }
    .card {
      background:white; padding:15px; border-radius:8px;
    }
    a { color:blue; font-weight:bold; }
  </style>
</head>
<body>

<h2>🧑‍💼 Admin – Mysore City Bus Stand</h2>

<div class="card" id="data">
  No alerts received.
</div>

<script>
const MYSORE_LAT = 12.2958;
const MYSORE_LON = 76.6394;

function getDistance(lat1, lon1, lat2, lon2) {
  const R = 6371;
  const dLat = (lat2-lat1) * Math.PI/180;
  const dLon = (lon2-lon1) * Math.PI/180;
  const a =
    Math.sin(dLat/2) * Math.sin(dLat/2) +
    Math.cos(lat1*Math.PI/180) * Math.cos(lat2*Math.PI/180) *
    Math.sin(dLon/2) * Math.sin(dLon/2);
  return (R * 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a))).toFixed(2);
}

let alert = localStorage.getItem("busAlert");

if (alert) {
  alert = JSON.parse(alert);

  const distance = getDistance(
    MYSORE_LAT, MYSORE_LON,
    alert.lat, alert.lon
  );

  document.getElementById("data").innerHTML = `
    <p><b>Bus Number:</b> ${alert.bus}</p>
    <p><b>Issue:</b> ${alert.issue}</p>
    <p><b>Time:</b> ${alert.time}</p>
    <p><b>Bus Distance from Mysore Bus Stand:</b> ${distance} km</p>
    <p><b>Track Bus:</b><br>
      <a href="https://www.google.com/maps?q=${alert.lat},${alert.lon}" target="_blank">
        View on Google Maps
      </a>
    </p>
  `;
}
</script>

</body>
</html># admine
