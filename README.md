<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>👑 REG KUCHOK V1 👑</title>
  <style>
    body {
      background-color: #000;
      color: #fff;
      font-family: 'Arial', sans-serif;
      text-align: center;
    }
    .panel {
      margin: 50px auto;
      padding: 20px;
      width: 90%;
      max-width: 400px;
      background: url('https://www.transparenttextures.com/patterns/cubes.png'), #111;
      border-radius: 10px;
      box-shadow: 0 0 15px #0000FF;
    }
    h1 {
      color: #0000FF;
      font-size: 24px;
      margin-bottom: 20px;
    }
    .switch-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: #222;
      margin: 10px 0;
      padding: 10px;
      border-radius: 5px;
    }
    .switch-label {
      color: white;
      font-size: 16px;
    }
    .switch {
      position: relative;
      display: inline-block;
      width: 50px;
      height: 24px;
    }
    .switch input {
      opacity: 0;
      width: 0;
      height: 0;
    }
    .slider {
      position: absolute;
      cursor: pointer;
      top: 0; left: 0;
      right: 0; bottom: 0;
      background-color: #ccc;
      transition: .4s;
      border-radius: 24px;
    }
    .slider:before {
      position: absolute;
      content: "";
      height: 18px;
      width: 18px;
      left: 3px;
      bottom: 3px;
      background-color: white;
      transition: .4s;
      border-radius: 50%;
    }
    input:checked + .slider {
      background-color: #0000FF;
    }
    input:checked + .slider:before {
      transform: translateX(26px);
    }
    .btn {
      background: blue;
      color: white;
      padding: 10px 20px;
      margin: 10px 5px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      display: block;
      width: 100%;
      max-width: 300px;
      margin-left: auto;
      margin-right: auto;
    }
    .btn:hover {
      background: darkblue;
    }
    .status-message {
      color: #0000FF;
      font-size: 14px;
      margin-top: 10px;
      min-height: 20px;
    }
  </style>
</head>
<body>
  <div class="panel">
    <h1>REG PANEL👑</h1>
    <div class="switch-container">
      <span class="switch-label">REG Aimbot Pro 👑:</span>
      <label class="switch">
        <input type="checkbox" id="switch1" onchange="handleSwitchChange()">
        <span class="slider"></span>
      </label>
    </div>
    <div class="switch-container">
      <span class="switch-label"> Game boot 🔥🥶:</span>
      <label class="switch">
        <input type="checkbox" id="switch2" onchange="handleSwitchChange()">
        <span class="slider"></span>
      </label>
    </div>
    <div class="switch-container">
      <span class="switch-label">กันแบน กันดำ⚫⚫  :</span>
      <label class="switch">
        <input type="checkbox" id="switch3" onchange="handleSwitchChange()">
        <span class="slider"></span>
      </label>
    </div>
    <div class="status-message" id="statusMessage"></div>
    <button class="btn" onclick="downloadPlist();">
      ดาวน์โหลด .plist
    </button>
    <button class="btn" onclick="window.location.href='intent://#Intent;package=com.dts.freefireth;scheme=freefire;end';">
      เปิด Free Fire
    </button>
    <button class="btn" onclick="window.location.href='intent://#Intent;package=com.dts.freefiremax;scheme=freefiremax;end';">
      เปิด Free Fire MAX
    </button>
  </div>

  <script>
    // รายชื่อโดเมนที่จะบล็อก
    const blockedDomains = [
      "gin.freefiremobile.com", "ffarena.championship.garena.com", "creditappeal.ind.freefiremobile.com",
      "creditappeal.sea.freefiremobile.com", "gamesecurity.us.freefiremobile.com", "gamesecurity.sea.freefiremobile.com",
      "ff.garena.co.id", "ffsupport.garena.com", "rankguide.freefireindiamobile.com", "rankguide.us.freefiremobile.com",
      "rankguide.sea.freefiremobile.com", "ffguide.garena.com", "freefire.diamond.170.com.garenanow.grtc.dr.ff.com.garenanow.org",
      "cocoapods.firebasecore.com", "apple.compilers.llvm.clang.1_0.com", "185753624591-uavl56vk7f7ep2cudd1je4lh83orj2hh.apps.googleusercontent.com",
      "185753624591-qvie83hnchh8n0nbnq2neheti7r16c5m.apps.googleusercontent.com", "free-fire-8cd39.appspot.com", "free-fire-8cd39.firebaseio.com",
      "h7xxrov9lb.cloudflare-gateway.com", "com.dts.freefireth.unitywebviewactivity", "com.dts.freefireth", "garena.vn",
      "hotro.ff.garena.vn", "measurement.com", "app-measurement.com", "gcdsdk.appsflyer.com", "crashlytics.com",
      "crashlyrics.com", "firebase-settings.crashlytics.com", "skadsdkless.appsflyer.com", "conversions.appsflyer.com",
      "inapps.appsflyer.com", "attr.appsflyer.com", "launches.appsflyer.com", "cdn-settings.appsflyersdk.com",
      "squadpass.sea.garena.vn", "quandoan.ff.garena.vn", "yomost.ff.garena.vn", "akamaihd.net", "garenanow.com",
      "akamaiedge.net", "garena.com", "hocal.com", "appsflyer.com", "gopapi.io", "akamai.net", "1e100.net",
      "appsflyersdk.com", "ff.garena.vn", "na-gin.freefiremobile.com", "ff.sdk.grtc.garenanow.com", "ff.dr.grtc.garenanow.com",
      "listdl.com", "addr.arpa", "catchingnow.com", "analytics.com", "bc.googleusercontent.com", "mcdn.garenanow.com",
      "sea.freefiremobile.com", "ff.garena.com", "freefiremobile.com", "security-checker.com", "ffim.ff.garena.com",
      "api-spring2020.ffim.ff.garena.com", "ffmlseason3.ff.garena.com", "api-ffmlseason3.ff.garena.com", "heaven.ff.garena.com",
      "auctionhouse.ff.garena.com", "api.heaven.ff.garena.com", "midnight.ff.garena.com", "api-midnight.ff.garena.com",
      "api.anniversary2.ff.garena.com", "api-changefate3.ff.garena.com", "changefate3.ff.garena.com", "api.changefate3.ff.garena.com",
      "myproxyserver.com", "evice-check.garena.com", "anti-cheat.garena.com", "ip-detection.garena.com", "api.garena.com",
      "game.garena.com", "anticheat.garena.com", "token.garena.com", "anti.garena.com", "checker.garena.com",
      "guard.garena.com", "fraudulent.garena.com", "alert.garena.com", "dl.listdl.com", "dl.aw.freefiremobile.com",
      "dl.gmc.freefiremobile.com", "dl.cvs.freefiremobile.com", "cvs.freefiremobile.com", "dl.ctlin.freefiremobile.com",
      "dl.ctl.freefiremobile.com", "common.freefiremobile.com", "vnevent.ggblueshark.com", "dl.cdn.freefiremobile.com",
      "dl.castle.freefiremobile.com", "firebaselogging.googleapis.com", "rslw0r-launches.appsflyersdk.com", "grin.freefiremobile.com",
      "csoversea.stronghold.freefiremobile.com", "dl.dir.freefiremobile.com", "clientbp.ggblueshark.com", "anti-bot.garena.com",
      "anti-cheat-service.ff-garena.com", "anti-fraud.ff-garena.com", "anti-fraud.garena.com", "anti-fraudulent.garena.com",
      "anti-hack.garena.com", "audit.garena.com", "auth-check.garena.com", "security.garena.com", "cheat-detection.garena.com",
      "cheat-monitor.garena.com", "cheat-prevention.ff-garena.com", "cheat-analysis.garena.com", "cheat-detection-service-logs.garena.com",
      "cheat-detection-monitoring.garena.com", "cheat-prevention-logs.garena.com", "fraud-detection-system.garena.com",
      "fraud-monitoring-service.garena.com", "game-integrity-logs.garena.com", "exploit-detection.ff-garena.com",
      "ff-security.garena.com", "telemetry.garena.com", "analytics.garena.com", "activity-log.garena.com"
    ];

    // ฟังก์ชันสร้าง .plist พื้นฐาน
    function generateBasicPlist() {
      return `<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>PayloadDisplayName</key>
<string>Kuchok 🇧🇷</string>
<key>PayloadOrganization</key>
<string>encrypted-dns.party</string>
<key>PayloadDescription</key>
<string>botão trick é uma ferramenta que ajuda na fluidez do capa e auxílio na hora de atirar Regedit 100% De feita e configurada para o botãotrick @BLACKXITFF</string>
<key>ConsentText</key>
<dict>
<key>default</key>
<string>Privacy policy: https://mullvad.net/help/privacy-policy</string>
</dict>
<key>PayloadIdentifier</key>
<string>eaaa03ba-ffea-4eba-9150-8521f8a860bb</string>
<key>PayloadScope</key>
<string>User</string>
<key>PayloadType</key>
<string>Configuration</string>
<key>PayloadUUID</key>
<string>5879b00f-1359-41b7-a694-f435598a97c4</string>
<key>PayloadVersion</key>
<integer>1</integer>
<key>PayloadContent</key>
<array>
</array>
</dict>
</plist>`;
    }

    // ฟังก์ชันสร้าง DNS Settings
    function generateDNSSettings() {
      return `<dict>
<key>DNSSettings</key>
<dict>
<key>DNSProtocol</key>
<string>HTTPS</string>
<key>ServerAddresses</key>
<array>
<string>194.242.2.2</string>
<string>193.19.108.2</string>
<string>2a07:e340::2</string>
</array>
<key>ServerURL</key>
<string>https://doh.mullvad.net/dns-query</string>
</dict>
<key>PayloadType</key>
<string>com.apple.dnsSettings.managed</string>
<key>PayloadIdentifier</key>
<string>eadf8a3b-7082-4c30-96bb-0ebddb439e6b</string>
<key>PayloadUUID</key>
<string>9c8aa1d5-c018-4fcc-83b1-b796ac48d149</string>
<key>PayloadDisplayName</key>
<string>REGEBOTÃOTRICK🔴99%HS</string>
<key>PayloadVersion</key>
<integer>1</integer>
</dict>`;
    }

    // ฟังก์ชันสร้าง OnDemandRules
    function generateOnDemandRules() {
      return `<key>OnDemandRules</key>
<array>
<dict>
<key>Action</key>
<string>Connect</string>
<key>InterfaceTypeMatch</key>
<string>Cellular</string>
</dict>
<dict>
<key>Action</key>
<string>Connect</string>
<key>URLStringProbe</key>
<string>http://captive.apple.com/hotspot-detect.html</string>
</dict>
</array>`;
    }

    // ฟังก์ชันสร้าง Proxy Settings สำหรับบล็อกโดเมน
    function generateProxySettings() {
      let proxyConfig = `<dict>
<key>ProxyType</key>
<string>Manual</string>
<key>HTTPProxy</key>
<string>127.0.0.1</string>
<key>HTTPPort</key>
<integer>8080</integer>
<key>HTTPSProxy</key>
<string>127.0.0.1</string>
<key>HTTPSPort</key>
<integer>8080</integer>
<key>ExceptionsList</key>
<array>`;
      
      blockedDomains.forEach(domain => {
        proxyConfig += `\n<string>${domain}</string>`;
      });
      
      proxyConfig += `\n</array>
<key>PayloadType</key>
<string>com.apple.proxy.http.https</string>
<key>PayloadIdentifier</key>
<string>proxy-block-domains</string>
<key>PayloadUUID</key>
<string>12345678-1234-1234-1234-123456789012</string>
<key>PayloadDisplayName</key>
<string>Block Domains Configuration</string>
<key>PayloadVersion</key>
<integer>1</integer>
</dict>`;
      
      return proxyConfig;
    }

    // ฟังก์ชันสร้าง .plist ที่สมบูรณ์
    function generateCompletePlist() {
      let plist = `<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>PayloadDisplayName</key>
<string>Kuchok 🇧🇷</string>
<key>PayloadOrganization</key>
<string>encrypted-dns.party</string>
<key>PayloadDescription</key>
<string>botão trick é uma ferramenta que ajuda na fluidez do capa e auxílio na hora de atirar Regedit 100% De feita e configurada para o botãotrick @BLACKXITFF</string>
<key>ConsentText</key>
<dict>
<key>default</key>
<string>Privacy policy: https://mullvad.net/help/privacy-policy</string>
</dict>
<key>PayloadIdentifier</key>
<string>eaaa03ba-ffea-4eba-9150-8521f8a860bb</string>
<key>PayloadScope</key>
<string>User</string>
<key>PayloadType</key>
<string>Configuration</string>
<key>PayloadUUID</key>
<string>5879b00f-1359-41b7-a694-f435598a97c4</string>
<key>PayloadVersion</key>
<integer>1</integer>
<key>PayloadContent</key>
<array>`;

      const switch1 = document.getElementById('switch1').checked;
      const switch2 = document.getElementById('switch2').checked;
      const switch3 = document.getElementById('switch3').checked;

      if (switch1) {
        plist += `\n${generateDNSSettings()}`;
      }

      if (switch3) {
        plist += `\n${generateProxySettings()}`;
      }

      plist += `\n</array>`;

      if (switch2) {
        plist += `\n${generateOnDemandRules()}`;
      }

      plist += `\n</dict>
</plist>`;

      return plist;
    }

    // ฟังก์ชันจัดการการเปลี่ยนแปลงของสวิตช์
    function handleSwitchChange() {
      const switch1 = document.getElementById('switch1').checked;
      const switch2 = document.getElementById('switch2').checked;
      const switch3 = document.getElementById('switch3').checked;
      const statusMessage = document.getElementById('statusMessage');

      let status = [];
      if (switch1) status.push('✓ REG Aimbot 🔥');
      if (switch2) status.push('✓ Game boot 🥶');
      if (switch3) status.push('✓ กันแบน ดำ⚫');

      if (status.length === 0) {
        statusMessage.textContent = '✗ ไม่มีการตั้งค่า';
        statusMessage.style.color = '#FF0000';
      } else {
        statusMessage.textContent = status.join(' | ');
        statusMessage.style.color = '#00FF00';
      }
    }

    // ฟังก์ชันดาวน์โหลด .plist
    function downloadPlist() {
      const plistContent = generateCompletePlist();
      
      // สร้าง Blob จากข้อมูล
      const blob = new Blob([plistContent], { type: 'application/x-plist' });
      
      // สร้าง URL จาก Blob
      const url = window.URL.createObjectURL(blob);
      
      // สร้างลิงก์ดาวน์โหลด
      const link = document.createElement('a');
      link.href = url;
      link.download = 'Kuchok.plist';
      
      // เรียกใช้งานดาวน์โหลด
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
      
      // ปล่อย URL
      window.URL.revokeObjectURL(url);
    }
  </script>
</body>
</html>

