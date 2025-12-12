# player-database
Nocturne player data base
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Player Registration</title>

<!-- Google Font -->
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">

<style>
    body {
        margin: 0;
        background: linear-gradient(135deg, #1e1e2f, #2d2d44);
        font-family: "Poppins", sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        color: white;
    }

    .container {
        background: rgba(255, 255, 255, 0.1);
        padding: 30px;
        width: 100%;
        max-width: 400px;
        backdrop-filter: blur(10px);
        border-radius: 15px;
        box-shadow: 0 0 15px rgba(0,0,0,0.4);
        animation: fadeIn 0.8s ease;
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(10px); }
        to { opacity: 1; transform: translateY(0); }
    }

    h2 {
        text-align: center;
        margin-bottom: 25px;
        font-weight: 600;
    }

    label {
        font-size: 14px;
        font-weight: 300;
        margin-top: 10px;
    }

    input, select {
        width: 100%;
        padding: 12px;
        margin-top: 5px;
        border-radius: 8px;
        border: none;
        outline: none;
        font-size: 14px;
    }

    button {
        width: 100%;
        margin-top: 20px;
        background: #28a745;
        padding: 12px;
        border: none;
        border-radius: 8px;
        color: white;
        font-size: 16px;
        cursor: pointer;
        transition: 0.25s;
    }

    button:hover {
        background: #32c255;
    }

    #status {
        text-align: center;
        margin-top: 15px;
        font-size: 14px;
    }
</style>
</head>
<body>

<div class="container">
    <h2>Player Registration</h2>

    <label>Name:</label>
    <input id="name" type="text" placeholder="Enter your name">

    <label>Level:</label>
    <input id="level" type="number" placeholder="Enter your level">

    <label>Time Played (hours):</label>
    <input id="timePlayed" type="number" placeholder="Total hours played">

    <label>Time Zone:</label>
    <select id="timeZone">
        <option value="">Select time zone</option>
        <option value="UTC-8">UTC-8</option>
        <option value="UTC-7">UTC-7</option>
        <option value="UTC-6">UTC-6</option>
        <option value="UTC-5">UTC-5</option>
        <option value="UTC-4">UTC-4</option>
        <option value="UTC-3">UTC-3</option>
        <option value="UTC">UTC</option>
        <option value="UTC+1">UTC+1</option>
        <option value="UTC+2">UTC+2</option>
        <option value="UTC+3">UTC+3</option>
        <option value="UTC+4">UTC+4</option>
        <option value="UTC+5">UTC+5</option>
        <option value="UTC+6">UTC+6</option>
        <option value="UTC+7">UTC+7</option>
        <option value="UTC+8">UTC+8</option>
        <option value="UTC+9">UTC+9</option>
        <option value="UTC+10">UTC+10</option>
        <option value="UTC+11">UTC+11</option>
        <option value="UTC+12">UTC+12</option>
    </select>

    <button onclick="submitForm()">Submit</button>

    <p id="status"></p>
</div>

<script>
const SCRIPT_URL = "YOUR_GOOGLE_SCRIPT_WEB_APP_URL";

function submitForm() {
    const name = document.getElementById("name").value;
    const level = document.getElementById("level").value;
    const timePlayed = document.getElementById("timePlayed").value;
    const timeZone = document.getElementById("timeZone").value;

    if (!name || !level || !timePlayed || !timeZone) {
        document.getElementById("status").innerHTML = "⚠ Please fill out all fields.";
        return;
    }

    fetch(SCRIPT_URL, {
        method: "POST",
        body: JSON.stringify({name, level, timePlayed, timeZone}),
        headers: {"Content-Type": "application/json"}
    })
    .then(res => res.json())
    .then(() => {
        document.getElementById("status").innerHTML = "✅ Saved successfully!";
        document.getElementById("name").value = "";
        document.getElementById("level").value = "";
        document.getElementById("timePlayed").value = "";
        document.getElementById("timeZone").value = "";
    })
    .catch(err => {
        document.getElementById("status").innerHTML = "❌ Error saving data.";
        console.error(err);
    });
}
</script>

</body>
</html>
