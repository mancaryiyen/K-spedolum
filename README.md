<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Küspe Depo Takip Sistemi</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
            color: #333;
        }
        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        .silo-status {
            margin: 10px;
            display: flex;
            justify-content: space-between;
            width: 80%;
        }
        .status-indicator {
            height: 25px;
            width: 25px;
            border-radius: 50%;
        }
        .start-button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        .countdown {
            font-size: 20px;
            margin-top: 20px;
        }
        .alert {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Küspe Depo Takip Sistemi</h1>
    <div class="silo-status">
        <div>Silo 1 <span class="status-indicator" style="background-color: red;"></span></div>
        <div>Silo 2 <span class="status-indicator" style="background-color: green;"></span></div>
        <!-- Diğer silolar buraya eklenebilir -->
    </div>

    <button class="start-button" onclick="startTime()">Dolum Başlat</button>
    <div class="countdown">
        <p>Geçen Süre: <span id="timer">00:00</span></p>
        <p id="max-time-alert" class="alert" style="display: none;">Maksimum süre aşıldı!</p>
    </div>
</div>

<script>
    let startTime = null;
    let timerInterval = null;

    function startTime() {
        if (timerInterval !== null) {
            clearInterval(timerInterval); // Önceki zamanlayıcıyı temizle
        }

        startTime = Date.now(); // Zamanı başlat
        timerInterval = setInterval(updateTimer, 1000); // 1 saniyede bir güncellemeyi başlat
    }

    function updateTimer() {
        let elapsed = Date.now() - startTime; // Geçen süreyi hesapla
        let hours = Math.floor(elapsed / (1000 * 60 * 60)); // Saat hesapla
        let minutes = Math.floor((elapsed % (1000 * 60 * 60)) / (1000 * 60)); // Dakika hesapla

        document.getElementById("timer").innerText = formatTime(hours, minutes); // Zamanı ekrana yazdır

        if (hours >= 1 && minutes >= 30) { // Maksimum süreyi kontrol et
            document.getElementById("max-time-alert").style.display = "block"; // Uyarı göster
        }
    }

    function formatTime(hours, minutes) {
        return `${padTime(hours)}:${padTime(minutes)}`; // Saat ve dakikayı düzgün formatta göster
    }

    function padTime(time) {
        return time < 10 ? '0' + time : time; // Saat ve dakikayı 2 haneli yap
    }
</script>

</body>
</html>
