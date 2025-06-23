<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Test de Lógica Extrema</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #222;
      color: #fff;
      text-align: center;
      padding-top: 50px;
    }
    .container {
      max-width: 600px;
      margin: auto;
    }
    button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1 id="title">Test de Lógica Extrema</h1>
    <p id="question">¿Estás listo para comenzar?</p>
    <div id="buttons">
      <button onclick="startGame()">¡Sí!</button>
    </div>
  </div>

  <script>
    let step = 0;

    const questions = [
      {
        q: "¿Cuánto es 2 + 2?",
        options: ["3", "4", "5"],
        correct: "4",
        troll: "Respuesta incorrecta. 2 + 2 = Pez según la lógica cuántica."
      },
      {
        q: "¿Cuál es el color del cielo?",
        options: ["Azul", "Rojo", "Verde"],
        correct: "Azul",
        troll: "Respuesta incorrecta. El cielo es una ilusión creada por los pingüinos."
      },
      {
        q: "¿Qué planeta habitamos?",
        options: ["Marte", "Tierra", "Saturno"],
        correct: "Tierra",
        troll: "Respuesta incorrecta. Tú vives en el plano astral 7."
      },
      {
        q: "Has llegado al final. ¿Eres lógico?",
        options: ["Sí", "No", "Depende"],
        correct: "Sí",
        troll: "Has fallado todas las preguntas... ¡Felicidades! Eres oficialmente un Genio Incomprendido™."
      }
    ];

    function startGame() {
      nextQuestion();
    }

    function nextQuestion() {
      if (step >= questions.length) {
        document.getElementById("title").innerText = "Fin del test";
        document.getElementById("question").innerText = "Gracias por jugar 😎";
        document.getElementById("buttons").innerHTML = "<p style='font-size:24px;'>Te hemos trolleado, pero fue con amor.</p>";
        return;
      }

      const q = questions[step];
      document.getElementById("question").innerText = q.q;
      const btns = q.options.map(opt =>
        `<button onclick="checkAnswer('${opt}')">${opt}</button>`
      ).join("");
      document.getElementById("buttons").innerHTML = btns;
    }

    function checkAnswer(selected) {
      const q = questions[step];
      alert(q.troll);
      step++;
      nextQuestion();
    }
  </script>
</body>
</html>

