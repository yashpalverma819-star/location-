<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Permission-Based Location Tracker</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f6f8;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .card {
            background: #ffffff;
            padding: 25px;
            border-radius: 8px;
            width: 350px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            text-align: center;
        }
        button {
            padding: 10px 18px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            background: #007bff;
            color: white;
            border-radius: 5px;
        }
        button:hover {
            background: #0056b3;
        }
        .output {
            margin-top: 15px;
            font-size: 14px;
        }
    </style>
</head>
<body>

<div class="card">
    <h2>Location Tracking</h2>
    <p>This site will request permission to access your location.</p>

    <button onclick="getLocation()">Allow Location Access</button>

    <div class="output" id="output"></div>
</div>

<script>
function getLocation() {
    const output = document.getElementById("output");

    if (!navigator.geolocation) {
        output.innerHTML = "Geolocation is not supported by your browser.";
        return;
    }

    output.innerHTML = "Requesting location permission...";

    navigator.geolocation.getCurrentPosition(
        (position) => {
            const latitude = position.coords.latitude;
            const longitude = position.coords.longitude;
            const accuracy = position.coords.accuracy;

            output.innerHTML = `
                <strong>Location Access Granted</strong><br>
                Latitude: ${latitude}<br>
                Longitude: ${longitude}<br>
                Accuracy: ±${accuracy} meters
            `;
        },
        (error) => {
            switch(error.code) {
                case error.PERMISSION_DENIED:
                    output.innerHTML = "Permission denied by user.";
                    break;
                case error.POSITION_UNAVAILABLE:
                    output.innerHTML = "Location unavailable.";
                    break;
                case error.TIMEOUT:
                    output.innerHTML = "Location request timed out.";
                    break;
                default:
                    output.innerHTML = "An unknown error occurred.";
            }
        }
    );
}
</script>

</body>
</html>
