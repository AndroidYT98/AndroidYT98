<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>AndroidYT DNS - Dark Mode</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700&display=swap');

    body {
      background: #0a0a0a;
      font-family: 'Orbitron', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      color: #eee;
      margin: 0;
      padding: 0;
      direction: rtl;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      padding: 40px 20px;
    }

    .container {
      background: #111;
      max-width: 900px;
      width: 100%;
      border-radius: 20px;
      padding: 40px 50px;
      box-shadow:
        0 0 10px #ff0000,
        0 0 20px #ff0000,
        0 0 30px #ff0000;
      user-select: none;
    }

    h1 {
      font-size: 48px;
      text-align: center;
      color: #ff1a1a;
      margin-bottom: 40px;
      text-shadow:
        0 0 5px #ff0000,
        0 0 10px #ff0000;
    }

    .buttons {
      text-align: center;
      margin-bottom: 35px;
    }

    button {
      background: #220000;
      color: #ff1a1a;
      border: 2px solid #ff1a1a;
      border-radius: 12px;
      font-size: 22px;
      padding: 14px 28px;
      margin: 0 12px;
      cursor: pointer;
      transition: all 0.3s ease;
      font-weight: 700;
      box-shadow:
        0 0 5px #ff1a1a;
    }

    button:hover {
      background: #ff1a1a;
      color: #111;
      box-shadow:
        0 0 15px #ff4d4d,
        0 0 30px #ff4d4d;
    }

    .dns-list {
      display: flex;
      flex-direction: column;
      gap: 22px;
    }

    .dns-item {
      background: #1a1a1a;
      border: 2px solid #ff1a1a;
      border-radius: 16px;
      padding: 20px 28px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow:
        0 0 8px #ff1a1a;
      font-size: 20px;
      line-height: 1.3;
    }

    .dns-info {
      max-width: 70%;
      color: #eee;
      font-weight: 700;
    }

    .dns-info em {
      display: block;
      margin-top: 8px;
      color: #ff6666;
      font-weight: 600;
      font-size: 18px;
      text-shadow: 0 0 4px #ff3333;
    }

    .copy-btn {
      background: #330000;
      border: 1.5px solid #ff1a1a;
      color: #ff1a1a;
      font-size: 16px;
      font-weight: 700;
      padding: 10px 16px;
      border-radius: 12px;
      cursor: pointer;
      box-shadow:
        0 0 6px #ff1a1a;
      transition: all 0.3s ease;
      user-select: none;
      margin-left: 12px;
    }

    .copy-btn:hover {
      background: #ff1a1a;
      color: #111;
      box-shadow:
        0 0 20px #ff6666,
        0 0 40px #ff6666;
    }

    @media (max-width: 650px) {
      .dns-item {
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
      }
      .dns-info {
        max-width: 100%;
      }
      .copy-btn {
        margin-left: 0;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>AndroidYT DNS</h1>
    <div class="buttons">
      <button onclick="generateDNS()">Generate DNS</button>
      <button onclick="generateDNS()">Regenerate DNS</button>
    </div>
    <div id="dnsList" class="dns-list"></div>
  </div>

  <script>
    function rand(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function generateIPv4() {
      return `23.${rand(0, 255)}.${rand(0, 255)}.${rand(1, 254)}`;
    }

    function generateIPv6() {
      const parts = [];
      for (let i = 0; i < 8; i++) {
        parts.push(Math.floor(Math.random() * 0xffff).toString(16));
      }
      return parts.join(':');
    }

    function generateDNS() {
      const dnsList = document.getElementById("dnsList");
      dnsList.innerHTML = '';
      for (let i = 0; i < 10; i++) {
        const ipv4 = generateIPv4();
        const ipv6 = generateIPv6();
        const dnsItem = document.createElement('div');
        dnsItem.className = 'dns-item';
        dnsItem.innerHTML = `
          <div class="dns-info">
            <strong>IPv4:</strong> ${ipv4} <br />
            <strong>IPv6:</strong> ${ipv6} <br />
            <em>پینگ پایین | ثبت سریع | بدون لگ</em>
          </div>
          <div>
            <button class="copy-btn" onclick="copyToClipboard('${ipv4}')">Copy IPv4</button>
            <button class="copy-btn" onclick="copyToClipboard('${ipv6}')">Copy IPv6</button>
          </div>
        `;
        dnsList.appendChild(dnsItem);
      }
    }

    function copyToClipboard(text) {
      navigator.clipboard.writeText(text).then(() => {
        alert('کپی شد: ' + text);
      });
    }
  </script>
</body>
</html>
