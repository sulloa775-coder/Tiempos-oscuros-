<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Transformers Tiempos Oscuros</title>
    <style>
        body { background-color: #000; color: #fff; font-family: 'Segoe UI', sans-serif; margin: 0; }
        header { background-color: #1a0000; padding: 20px; text-align: center; border-bottom: 3px solid #ff0000; }
        .marquee-container { background-color: #000; color: #ff0000; padding: 10px; overflow: hidden; border-bottom: 1px solid #333; }
        .marquee-text { display: inline-block; animation: moveText 15s linear infinite; font-weight: bold; }
        @keyframes moveText { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .container { padding: 20px; max-width: 1000px; margin: auto; }
        .upload-section { background: #111; padding: 20px; border: 1px solid #333; margin-bottom: 20px; border-radius: 8px; }
        #video-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 20px; margin-top: 20px; }
        .video-card { background: #1a0000; padding: 15px; border-radius: 8px; border: 1px solid #440000; text-align: center; }
        video { width: 100%; border-radius: 4px; }
        .actions { margin-top: 10px; }
        button { background: #ff0000; color: white; border: none; padding: 8px 12px; cursor: pointer; border-radius: 4px; margin: 2px; font-size: 12px; }
        input { padding: 8px; margin: 5px; border-radius: 4px; border: none; }
    </style>
</head>
<body>

<header><h1>Transformers Tiempos Oscuros</h1></header>
<div class="marquee-container">
    <div class="marquee-text">Bienvenid@, Aquí subiré todos los avances de mi serie, espero lo disfrutes <3</div>
</div>

<div class="container">
    <div class="upload-section">
        <input type="text" id="videoTitle" placeholder="Título del video">
        <input type="file" id="videoFile" accept="video/*">
        <button onclick="uploadVideo()">Publicar Video</button>
    </div>
    <div id="video-grid"></div>
</div>

<script>
    const CLAVE = "etepepe90#";

    function uploadVideo() {
        const file = document.getElementById('videoFile').files[0];
        const title = document.getElementById('videoTitle').value || "Sin título";
        
        if (!file) return alert("Selecciona un video.");
        if (prompt("Clave de administrador:") !== CLAVE) return alert("Acceso denegado.");

        const grid = document.getElementById('video-grid');
        const div = document.createElement('div');
        div.className = 'video-card';
        div.innerHTML = `
            <h3>${title}</h3>
            <video src="${URL.createObjectURL(file)}" controls></video>
            <div class="actions">
                <button onclick="reemplazar(this)">Reemplazar</button>
                <button onclick="borrar(this)">Borrar</button>
            </div>
        `;
        grid.appendChild(div);
        document.getElementById('videoFile').value = "";
    }

    function borrar(btn) {
        if (prompt("Introduce la clave para borrar:") === CLAVE) {
            btn.closest('.video-card').remove();
        } else {
            alert("Clave incorrecta.");
        }
    }

    function reemplazar(btn) {
        if (prompt("Introduce la clave para reemplazar:") === CLAVE) {
            const newFile = document.createElement('input');
            newFile.type = 'file';
            newFile.accept = 'video/*';
            newFile.onchange = (e) => {
                const video = btn.closest('.video-card').querySelector('video');
                video.src = URL.createObjectURL(e.target.files[0]);
            };
            newFile.click();
        } else {
            alert("Clave incorrecta.");
        }
    }
</script>

</body>
</html>
