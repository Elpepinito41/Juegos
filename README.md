<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Retro NES Emulator</title>
  <style>
    body {
      background: #111;
      color: white;
      text-align: center;
      font-family: sans-serif;
    }
    canvas {
      border: 4px solid #555;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>🎮 Retro NES Emulator</h1>
  <input type="file" id="romLoader" accept=".nes">
  <br><br>
  <canvas id="nes-canvas" width="256" height="240"></canvas>

  <script src="https://unpkg.com/jsnes/dist/jsnes.min.js"></script>
  <script>
    const canvas = document.getElementById('nes-canvas');
    const ctx = canvas.getContext('2d');
    const imageData = ctx.getImageData(0, 0, 256, 240);

    const nes = new jsnes.NES({
      onFrame: function (frameBuffer) {
        for (let i = 0; i < frameBuffer.length; i++) {
          imageData.data[i * 4 + 0] = (frameBuffer[i] >> 16) & 0xFF;
          imageData.data[i * 4 + 1] = (frameBuffer[i] >> 8) & 0xFF;
          imageData.data[i * 4 + 2] = frameBuffer[i] & 0xFF;
          imageData.data[i * 4 + 3] = 0xFF;
        }
        ctx.putImageData(imageData, 0, 0);
      },
      onStatusUpdate: console.log,
      onAudioSample: function () {},
    });

    document.getElementById('romLoader').addEventListener('change', function(e) {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function () {
          nes.loadROM(reader.result);
          nes.start();
        };
        reader.readAsBinaryString(file);
      }
    });
  </script>
</body>
</html>