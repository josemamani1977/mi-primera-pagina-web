<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Transcriptor de Audio</title>
<style>
    body {
        font-family: Arial, sans-serif;
        max-width: 800px;
        margin: 20px auto;
        padding: 20px;
        background: #f2f2f2;
    }
    #time {
        font-size: 20px;
        margin-top: 10px;
        font-weight: bold;
    }
    textarea {
        width: 100%;
        height: 200px;
        margin-top: 20px;
        font-size: 16px;
        padding: 10px;
    }
    .controls-extra {
        margin: 15px 0;
    }
    .controls-extra button {
        padding: 8px 15px;
        margin-right: 10px;
        font-size: 16px;
        cursor: pointer;
    }
</style>
</head>
<body>

<h2>🎧 Transcriptor de Audio</h2>

<input type="file" id="audioFile" accept="audio/*">
<br><br>

<audio id="player" controls></audio>

<div class="controls-extra">
    <button id="back10">⏪ Retroceder 10s</button>
    <button id="forward10">⏩ Avanzar 10s</button>
</div>

<div id="time">Tiempo: 0:00</div>

<textarea id="transcription" placeholder="Escribe aquí la transcripción..."></textarea>

<script>
    const fileInput = document.getElementById("audioFile");
    const player = document.getElementById("player");
    const timeDisplay = document.getElementById("time");

    // Cargar audio seleccionado
    fileInput.addEventListener("change", function () {
        const file = this.files[0];
        player.src = URL.createObjectURL(file);
        player.load();
    });

    // Botón retroceder 10 segundos
    document.getElementById("back10").addEventListener("click", () => {
        player.currentTime = Math.max(0, player.currentTime - 10);
    });

    // Botón avanzar 10 segundos
    document.getElementById("forward10").addEventListener("click", () => {
        player.currentTime = Math.min(player.duration, player.currentTime + 10);
    });

    // Actualizar el tiempo cada 200 ms
    player.addEventListener("timeupdate", () => {
        const seconds = Math.floor(player.currentTime);
        const minutes = Math.floor(seconds / 60);
        const sec = seconds % 60;

        timeDisplay.textContent =
            `Tiempo: ${minutes}:${sec.toString().padStart(2, "0")}`;
    });
</script>

</body>
</html>
