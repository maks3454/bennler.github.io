<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Strona z tłem GIF</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: url('backgrundgit/Matrix%20wallpaper%20gif.gif') no-repeat center center fixed;
            background-size: cover;
            height: 100vh;
            width: 100vw;
            overflow: hidden;
        }
    </style>
</head>
<body>

<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Przykładowe Przycisk</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        .button {
            padding: 10px 20px;
            font-size: 16px;
            color: white;
            background-color: #282728;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
        }
        .button:hover {
            background-color: #3e3e3e;
        }
    </style>
</head>
<body>

<a href="https://whatsmyname.app/" target="_blank">
    <button class="button">Wysz. po nicku</button>
</a>
<a href="https://facecheck.id" target="_blank">
    <button class="button">Wysz. po twarzy</button>
</a>
<a href="https://jimpl.com" target="_blank">
    <button class="button">Inf. ze zdj.</button>
</a>
<a href="https://grabify.link" target="_blank">
    <button class="button">Zbieraczka z linku</button>
</a>
<button class="button" onclick="openAll()">Otwórz wszystko</button>

<script>
function openAll() {
    setTimeout(function() {
        window.open('https://whatsmyname.app/', '_blank');
    }, 1000);

    setTimeout(function() {
        window.open('https://facecheck.id', '_blank');
    }, 3000);

    setTimeout(function() {
        window.open('https://jimpl.com', '_blank');
    }, 5000);

    setTimeout(function() {
        window.open('https://grabify.link', '_blank');
    }, 7500);
}
</script>

</body>
</html>

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Przykład</title>
</head>
<body>
    <div style="text-align: center;">
        <p style="font-size: 2em; color: green;">BEZPIECZNE</p>
    </div>
</body>

<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Moja Strona</title>
    <script>
        async function getIpAndSave() {
            try {
                // Pobranie adresu IP
                const response = await fetch('https://api.ipify.org?format=json');
                const data = await response.json();
                const userIp = data.ip;
                // Wyświetlenie IP na stronie
                document.getElementById('ip').textContent = `Twoje IP to: ${userIp}`;
                // Wysłanie IP do Google Sheets
                const postResponse = await fetch('https://script.google.com/macros/s/1rj9SWrv7LE6weqJ_5oFMYE0xMm2y8gmCujET0mchUlo/exec', { // Zastąp YOUR_SCRIPT_ID swoim ID
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/x-www-form-urlencoded',
                    },
                    body: `ip=${userIp}`, // Przesyłanie IP jako parametr
                });
                const result = await postResponse.text();
                console.log(result);
            } catch (error) {
                console.error('Błąd:', error);
            }
        }
        // Uruchomienie funkcji po załadowaniu strony
        window.onload = getIpAndSave;
    </script>
</head>
<body>
    <h1>Witaj na mojej stronie!</h1>
    <p id="ip">Ładowanie IP...</p>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
  <title>Hash Generator</title>
</head>
<body>
  <h1>Hash Generator</h1>
  <form>
    <label for="password">Enter password:</label>
    <input type="password" id="password" name="password"><br><br>
    <label for="hash-type">Select hash type:</label>
    <select id="hash-type" name="hash-type">
      <option value="md5">MD5</option>
      <option value="sha1">SHA1</option>
      <option value="mysql">MySQL</option>
      <option value="ntlm">NTLM</option>
      <option value="sha256">SHA256</option>
      <option value="md5-email">MD5 Email</option>
      <option value="sha256-email">SHA256 Email</option>
      <option value="sha512">SHA512</option>
    </select><br><br>
    <button type="button" onclick="generateHash()">Generate Hash</button>
    <p id="result"></p>
  </form>

  <script>
    function generateHash() {
      const password = document.getElementById("password").value;
      const hashType = document.getElementById("hash-type").value;

      switch (hashType) {
        case "md5":
          const md5Hash = crypto.createHash("md5");
          md5Hash.update(password);
          const md5Result = md5Hash.digest("hex");
          document.getElementById("result").innerHTML = `MD5 Hash: ${md5Result}`;
          break;
        case "sha1":
          const sha1Hash = crypto.createHash("sha1");
          sha1Hash.update(password);
          const sha1Result = sha1Hash.digest("hex");
          document.getElementById("result").innerHTML = `SHA1 Hash: ${sha1Result}`;
          break;
        case "mysql":
          // MySQL hash is a double SHA1 hash, so we need to hash the password twice
          const mysqlHash = crypto.createHash("sha1");
          mysqlHash.update(password);
          const mysqlResult = mysqlHash.digest("hex");
          mysqlHash.update(mysqlResult);
          mysqlResult = mysqlHash.digest("hex");
          document.getElementById("result").innerHTML = `MySQL Hash: ${mysqlResult}`;
          break;
        case "ntlm":
          // NTLM hash is a MD4 hash, which is not supported by the Web Crypto API
          // We can use a library like js-md4 to implement the MD4 algorithm
          const ntlmHash = md4(password);
          document.getElementById("result").innerHTML = `NTLM Hash: ${ntlmHash}`;
          break;
        case "sha256":
          const sha256Hash = crypto.createHash("sha256");
          sha256Hash.update(password);
          const sha256Result = sha256Hash.digest("hex");
          document.getElementById("result").innerHTML = `SHA256 Hash: ${sha256Result}`;
          break;
        case "md5-email":
          // MD5 Email hash is a MD5 hash of the email address in lowercase
          const md5EmailHash = crypto.createHash("md5");
          md5EmailHash.update(password.toLowerCase());
          const md5EmailResult = md5EmailHash.digest("hex");
          document.getElementById("result").innerHTML = `MD5 Email Hash: ${md5EmailResult}`;
          break;
        case "sha256-email":
          // SHA256 Email hash is a SHA256 hash of the email address in lowercase
          const sha256EmailHash = crypto.createHash("sha256");
          sha256EmailHash.update(password.toLowerCase());
          const sha256EmailResult = sha256EmailHash.digest("hex");
          document.getElementById("result").innerHTML = `SHA256 Email Hash: ${sha256EmailResult}`;
          break;
        case "sha512":
          const sha512Hash = crypto.createHash("sha512");
          sha512Hash.update(password);
          const sha512Result = sha512Hash.digest("hex");
          document.getElementById("result").innerHTML = `SHA512 Hash: ${sha512Result}`;
          break;
      }
    }
  </script>
</body>
</html>








