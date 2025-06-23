<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Retro Emulador Web</title>
  <style>
    body {
      background-color: #1e1e1e;
      color: white;
      font-family: sans-serif;
      text-align: center;
      padding: 20px;
    }
    canvas {
      border: 4px solid #555;
      margin-top: 20px;
    }
    select, input {
      margin: 10px;
      padding: 10px;
    }
  </style>
</head>
<body>
  <h1>🎮 Emulador de Consolas Retro</h1>

  <label for="consoleSelect">Selecciona consola:</label>
  <select id="consoleSelect">
    <option value="nes">NES</option>
    <option value="snes">SNES</option>
    <!-- Puedes agregar más -->
  </select>

  <br>
  <input type="file" id="romInput" accept=".nes,.smc">
  <br>

  <canvas id="screen" width="256" height="240"></canvas>

  <script src="js/jsnes.min.js"></script>
  <script src="js/snes9x.js"></script>
  <script src="js/emulators.js"></script>
</body>
</html>const canvas = document.getElementById('screen');
const ctx = canvas.getContext('2d');
const consoleSelect = document.getElementById('consoleSelect');
const romInput = document.getElementById('romInput');

let currentEmulator = null;

function loadNES(romData) {
  const nes = new jsnes.NES({
    onFrame: function (frameBuffer) {
      const imageData = ctx.getImageData(0, 0, 256, 240);
      for (let i = 0; i < frameBuffer.length; i++) {
        const pixel = frameBuffer[i];
        imageData.data[i * 4 + 0] = (pixel >> 16) & 0xFF;
        imageData.data[i * 4 + 1] = (pixel >> 8) & 0xFF;
        imageData.data[i * 4 + 2] = pixel & 0xFF;
        imageData.data[i * 4 + 3] = 0xFF;
      }
      ctx.putImageData(imageData, 0, 0);
    }
  });
  nes.loadROM(romData);
  nes.start();
  currentEmulator = nes;
}

// SNES
function loadSNES(romData) {
  // Aquí iría la lógica de snes9x (necesita WebAssembly y configuración especial)
  alert("Soporte para SNES aún en desarrollo. (Aquí iría snes9x.js)");
}

romInput.addEventListener('change', function () {
  const file = this.files[0];
  const reader = new FileReader();
  reader.onload = function () {
    const romData = reader.result;
    const selected = consoleSelect.value;
    if (selected === 'nes') {
      loadNES(romData);
    } else if (selected === 'snes') {
      loadSNES(romData);
    }
  };
  reader.readAsBinaryString(file);
});const canvas = document.getElementById('screen');
const ctx = canvas.getContext('2d');
const consoleSelect = document.getElementById('consoleSelect');
const romInput = document.getElementById('romInput');

let currentEmulator = null;

function loadNES(romData) {
  const nes = new jsnes.NES({
    onFrame: function (frameBuffer) {
      const imageData = ctx.getImageData(0, 0, 256, 240);
      for (let i = 0; i < frameBuffer.length; i++) {
        const pixel = frameBuffer[i];
        imageData.data[i * 4 + 0] = (pixel >> 16) & 0xFF;
        imageData.data[i * 4 + 1] = (pixel >> 8) & 0xFF;
        imageData.data[i * 4 + 2] = pixel & 0xFF;
        imageData.data[i * 4 + 3] = 0xFF;
      }
      ctx.putImageData(imageData, 0, 0);
    }
  });
  nes.loadROM(romData);
  nes.start();
  currentEmulator = nes;
}

// SNES
function loadSNES(romData) {
  // Aquí iría la lógica de snes9x (necesita WebAssembly y configuración especial)
  alert("Soporte para SNES aún en desarrollo. (Aquí iría snes9x.js)");
}

romInput.addEventListener('change', function () {
  const file = this.files[0];
  const reader = new FileReader();
  reader.onload = function () {
    const romData = reader.result;
    const selected = consoleSelect.value;
    if (selected === 'nes') {
      loadNES(romData);
    } else if (selected === 'snes') {
      loadSNES(romData);
    }
  };
  reader.readAsBinaryString(file);
});const canvas = document.getElementById('screen');
const ctx = canvas.getContext('2d');
const consoleSelect = document.getElementById('consoleSelect');
const romInput = document.getElementById('romInput');

let currentEmulator = null;

function loadNES(romData) {
  const nes = new jsnes.NES({
    onFrame: function (frameBuffer) {
      const imageData = ctx.getImageData(0, 0, 256, 240);
      for (let i = 0; i < frameBuffer.length; i++) {
        const pixel = frameBuffer[i];
        imageData.data[i * 4 + 0] = (pixel >> 16) & 0xFF;
        imageData.data[i * 4 + 1] = (pixel >> 8) & 0xFF;
        imageData.data[i * 4 + 2] = pixel & 0xFF;
        imageData.data[i * 4 + 3] = 0xFF;
      }
      ctx.putImageData(imageData, 0, 0);
    }
  });
  nes.loadROM(romData);
  nes.start();
  currentEmulator = nes;
}

// SNES
function loadSNES(romData) {
  // Aquí iría la lógica de snes9x (necesita WebAssembly y configuración especial)
  alert("Soporte para SNES aún en desarrollo. (Aquí iría snes9x.js)");
}

romInput.addEventListener('change', function () {
  const file = this.files[0];
  const reader = new FileReader();
  reader.onload = function () {
    const romData = reader.result;
    const selected = consoleSelect.value;
    if (selected === 'nes') {
      loadNES(romData);
    } else if (selected === 'snes') {
      loadSNES(romData);
    }
  };
  reader.readAsBinaryString(file);
});