# Qr-nova-scanner
QR-Nova


<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>QR-Code Scanner</title>
  <style>
    body {
      margin:0;
      font-family: 'Inter', Arial, sans-serif;
      display:flex;
      flex-direction:column;
      align-items:center;
      justify-content:center;
      height:100vh;
      background:#ffffff;
      color:#0072ff;
      text-align:center;
    }
    video {
      width:90%;
      max-width:400px;
      border-radius:16px;
      border:2px solid #0072ff;
      margin-bottom:20px;
    }
    input {
      width:90%;
      max-width:400px;
      padding:10px;
      font-size:16px;
      border:2px solid #0072ff;
      border-radius:12px;
      text-align:center;
      color:#0072ff;
      margin-bottom:10px;
    }
    button {
      padding:10px 20px;
      font-size:16px;
      background:#0072ff;
      color:white;
      border:none;
      border-radius:12px;
      cursor:pointer;
      margin-top:10px;
    }
  </style>
</head>
<body>

<h1>QR-Code Scanner</h1>
<video id="preview" autoplay></video>
<input type="text" id="qrResult" placeholder="Hier erscheint der Link" readonly>
<button id="copyBtn">Link kopieren</button>

<script src="https://cdn.jsdelivr.net/npm/qr-scanner@1.4.2/qr-scanner.min.js"></script>
<script>
  const video = document.getElementById('preview');
  const resultInput = document.getElementById('qrResult');
  const copyBtn = document.getElementById('copyBtn');

  const scanner = new QrScanner(video, result => {
    resultInput.value = result;
  }, { highlightScanRegion: true, highlightCodeOutline: true });

  QrScanner.hasCamera().then(hasCamera => {
    if(hasCamera){
      scanner.start().catch(err => alert('Kamera konnte nicht gestartet werden. Bitte HTTPS prüfen oder Berechtigungen erlauben.'));
    } else {
      alert('Keine Kamera gefunden.');
    }
  });

  copyBtn.addEventListener('click', () => {
    resultInput.select();
    navigator.clipboard.writeText(resultInput.value);
    alert('Link kopiert!');
  });
</script>

</body>
</html>
