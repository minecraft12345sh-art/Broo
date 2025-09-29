<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hồ Việt Trung Piano</title>
  <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      background: #111;
      color: white;
      font-family: sans-serif;
    }
    h1 {
      margin-bottom: 20px;
    }
    .piano {
      display: flex;
    }
    .key {
      width: 60px;
      height: 200px;
      border: 1px solid #000;
      background: white;
      margin: 1px;
      cursor: pointer;
      display: flex;
      align-items: flex-end;
      justify-content: center;
      font-size: 12px;
      user-select: none;
    }
    .key.black {
      width: 40px;
      height: 120px;
      background: black;
      color: white;
      margin-left: -20px;
      margin-right: -20px;
      z-index: 2;
      position: relative;
    }
  </style>
</head>
<body>
  <h1>🎹 Hồ Việt Trung Piano</h1>
  <div class="piano">
    <div class="key" data-note="261.63">C</div>
    <div class="key black" data-note="277.18">C#</div>
    <div class="key" data-note="293.66">D</div>
    <div class="key black" data-note="311.13">D#</div>
    <div class="key" data-note="329.63">E</div>
    <div class="key" data-note="349.23">F</div>
    <div class="key black" data-note="369.99">F#</div>
    <div class="key" data-note="392.00">G</div>
    <div class="key black" data-note="415.30">G#</div>
    <div class="key" data-note="440.00">A</div>
    <div class="key black" data-note="466.16">A#</div>
    <div class="key" data-note="493.88">B</div>
  </div>

  <script>
    function playNote(frequency) {
      const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
      const oscillator = audioCtx.createOscillator();
      const gainNode = audioCtx.createGain();

      oscillator.type = 'sine';
      oscillator.frequency.setValueAtTime(frequency, audioCtx.currentTime);

      oscillator.connect(gainNode);
      gainNode.connect(audioCtx.destination);

      gainNode.gain.setValueAtTime(0.2, audioCtx.currentTime);
      oscillator.start();
      oscillator.stop(audioCtx.currentTime + 1);
    }

    document.querySelectorAll('.key').forEach(key => {
      key.addEventListener('click', () => {
        const frequency = parseFloat(key.dataset.note);
        playNote(frequency);
      });
    });
  </script>
</body>
</html>
