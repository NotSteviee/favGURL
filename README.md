<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Favorite Girl</title>

  <!-- Cute Font -->
  <link href="https://fonts.cdnfonts.com/css/little-orion" rel="stylesheet" />

  <!-- Confetti Script -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>

  <style>
    body {
      font-family: 'Little Orion', cursive;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      height: 100vh;
      margin: 0;
      background-color: #B57EDC;
      color: white;
      transition: background-color 1s ease;
    }

    .container {
      text-align: center;
      padding: 20px;
      border: 6px solid black;
      border-radius: 10px;
      background-color: #8A5D99;
      transition: background-color 1s ease, border 1s ease;
    }

    h1 {
      font-size: 2rem;
    }

    button {
      border: 2px solid white;
      padding: 10px 20px;
      font-size: 16px;
      margin: 10px;
      cursor: pointer;
      border-radius: 8px;
      background-color: #f44336;
      color: white;
      font-family: 'Little Orion', cursive;
      transition: all 0.3s ease;
    }

    button:hover {
      filter: brightness(1.1);
    }

    .yes {
      background-color: #4CAF50;
    }

    .rgb {
      animation: rgbFlash 1s infinite;
    }

    @keyframes rgbFlash {
      0%   { background-color: red; }
      25%  { background-color: orange; }
      50%  { background-color: lime; }
      75%  { background-color: cyan; }
      100% { background-color: violet; }
    }

    #finalMessage {
      margin-top: 30px;
      font-size: 2rem;
      display: none;
    }

    #finalGif {
      margin-top: 20px;
      display: none;
      margin-left: auto;
      margin-right: auto;
      box-shadow: 0 0 20px 5px white;
      border-radius: 10px;
      width: 300px;
    }

    audio {
      display: none;
    }

    /* Mobile Responsive Styling */
    @media (max-width: 600px) {
      h1 {
        font-size: 1.5rem;
      }

      button {
        font-size: 14px;
        padding: 8px 16px;
      }

      .container {
        width: 90%;
        padding: 15px;
      }

      #finalGif {
        width: 90%;
        max-width: 300px;
      }

      #finalMessage {
        font-size: 1.5rem;
      }
    }
  </style>
</head>
<body>

  <!-- Using your Vocaroo link -->
  <audio id="backgroundAudio">
    <source src="https://voca.ro/1fL4Dvdgg3Y4.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <div class="container">
    <h1 id="mainText">Do u wanna be my favorite girl??</h1>
    <button class="yes" onclick="respond('Yes')">Yes</button>
    <button class="no" id="noButton" onclick="changeNoText()">No</button>
    <div id="finalMessage"></div>
    <img id="finalGif" src="https://media.giphy.com/media/xTiTnHvXHHxOTcdmxO/giphy.gif">
  </div>

  <script>
    let noClicks = 0;
    const noButton = document.getElementById("noButton");
    const mainText = document.getElementById("mainText");
    const finalMessage = document.getElementById("finalMessage");
    const finalGif = document.getElementById("finalGif");
    const audio = document.getElementById("backgroundAudio");
    const container = document.querySelector(".container");

    const noTextChanges = [
      "No",
      "U sure?",
      "Really??",
      "Think about it",
      "Wooaah",
      "Nahhh u can't",
      "There's no other option",
      "Ok fine",
      "Duuuuh",
      "YESShhh!!"
    ];

    function playAudio() {
      if (audio.paused) {
        audio.play().catch(e => {
          console.log("Audio play blocked until interaction.");
        });
      }
    }

    function respond(answer) {
      playAudio();
      finalMessage.style.display = "block";
      finalMessage.innerText = "YOU WERE ALR MY FAV GURRLL!";
      setTimeout(() => {
        finalMessage.style.display = "none";
      }, 5000);
    }

    function changeNoText() {
      if (noClicks < noTextChanges.length - 1) {
        noClicks++;
        noButton.innerText = noTextChanges[noClicks];

        let newSize = 16 + noClicks * 4;
        noButton.style.fontSize = newSize + "px";
        noButton.style.padding = (10 + noClicks * 2) + "px " + (20 + noClicks * 4) + "px";

        if (noTextChanges[noClicks] === "Duuuuh") {
          noButton.classList.add("rgb");

          // Activate dark mode
          document.body.style.backgroundColor = "black";
          container.style.backgroundColor = "black";
          container.style.border = "6px solid white";
        }
      } else {
        noButton.innerText = "YESShhh!!";
        noButton.classList.add("rgb");

        finalMessage.style.display = "block";
        finalMessage.innerText = "Awwwwwww! THATSSS maaaa GAAALLLLL!";
        finalGif.style.display = "block";

        confetti({
          particleCount: 150,
          spread: 100,
          origin: { y: 0.6 }
        });

        setTimeout(() => {
          finalMessage.style.display = "none";
        }, 5000);
      }
    }

    document.body.addEventListener('click', playAudio);
  </script>
</body>
</html>
