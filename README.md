# coloer-picker
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Random Color Picker</title>
<style>
  body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background: #1e1e24;
    font-family: 'Segoe UI', Arial, sans-serif;
  }

  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 320px;
  }

  h1 {
    color: white;
    font-size: 26px;
    margin-bottom: 20px;
  }

  #preview {
    width: 220px;
    height: 140px;
    border-radius: 10px;
    border: 2px solid #444;
    background: #7db4e6;
    transition: background 0.15s ease;
  }

  #hexLabel {
    color: white;
    font-family: Consolas, monospace;
    font-size: 22px;
    font-weight: bold;
    margin-top: 18px;
  }

  #rgbLabel {
    color: #aaaaaa;
    font-family: Consolas, monospace;
    font-size: 14px;
    margin-top: 4px;
    margin-bottom: 20px;
  }

  .buttons {
    display: flex;
    gap: 12px;
  }

  button {
    padding: 12px 22px;
    font-size: 15px;
    font-weight: bold;
    border: none;
    border-radius: 6px;
    background: #3a3a44;
    color: white;
    cursor: pointer;
  }

  button:hover {
    background: #4a4a56;
  }

  #copiedLabel {
    color: #7dff9a;
    font-size: 13px;
    margin-top: 14px;
    height: 16px;
  }
</style>
</head>
<body>

  <div class="card">
    <h1>Random Color</h1>
    <div id="preview"></div>
    <div id="hexLabel">#7DB4E6</div>
    <div id="rgbLabel">rgb(125, 180, 230)</div>
    <div class="buttons">
      <button onclick="randomize()">Randomize</button>
      <button onclick="copyHex()">Copy Hex</button>
    </div>
    <div id="copiedLabel"></div>
  </div>

  <script>
    let currentHex = "#7DB4E6";

    function randomize() {
      const r = Math.floor(Math.random() * 256);
      const g = Math.floor(Math.random() * 256);
      const b = Math.floor(Math.random() * 256);

      currentHex = "#" + [r, g, b]
        .map(v => v.toString(16).padStart(2, "0").toUpperCase())
        .join("");

      document.getElementById("preview").style.background = currentHex;
      document.getElementById("hexLabel").textContent = currentHex;
      document.getElementById("rgbLabel").textContent = `rgb(${r}, ${g}, ${b})`;
      document.getElementById("copiedLabel").textContent = "";
    }

    function copyHex() {
      navigator.clipboard.writeText(currentHex).then(() => {
        document.getElementById("copiedLabel").textContent = `Copied ${currentHex} to clipboard!`;
      });
    }

    // spacebar rerolls too
    document.addEventListener("keydown", (e) => {
      if (e.code === "Space") {
        e.preventDefault();
        randomize();
      }
    });

    randomize();
  </script>

</body>
</html>
