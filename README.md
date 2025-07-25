
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>ferdes.ai v5.1 beta - Launcher Cerdas & Fitur Lengkap</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" />
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;600;700&display=swap" rel="stylesheet" />
  <style>
    body {
      font-family: "Outfit", sans-serif;
      background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
      padding: 40px;
      color: #222;
      transition: background 0.3s, color 0.3s;
    }
    body.dark {
      background: linear-gradient(135deg, #1e1e2f 0%, #121217 100%);
      color: #eee;
    }
    .logo {
      font-size: 40px;
      font-weight: 900;
      color: #ffffff;
      text-shadow: 0 0 10px #00f2fe, 0 0 20px #4facfe;
      text-align: center;
      margin-bottom: 12px;
      cursor: default;
      user-select: none;
      transition: text-shadow 0.4s ease;
    }
    .logo:hover {
      text-shadow: 0 0 15px #00f2fe, 0 0 30px #4facfe, 0 0 40px #00f2fe;
    }
    .section-box {
      max-width: 760px;
      margin: 30px auto;
      background: rgba(255 255 255 / 0.9);
      padding: 25px;
      border-radius: 20px;
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
      transition: background 0.3s, color 0.3s;
    }
    body.dark .section-box {
      background: rgba(34 34 34 / 0.9);
      color: #eee;
      box-shadow: 0 15px 30px rgba(0, 255, 255, 0.2);
    }
    .form-control {
      border-radius: 30px;
      padding: 18px;
      font-size: 18px;
    }
    .btn-round {
      border-radius: 30px;
      padding: 10px 25px;
      position: relative;
    }
    .btn-toggle-theme {
      position: fixed;
      top: 15px;
      right: 15px;
      background: #00f2fe;
      border: none;
      color: #222;
      border-radius: 50px;
      padding: 10px 20px;
      font-weight: 700;
      cursor: pointer;
      z-index: 9999;
      transition: background 0.3s, color 0.3s;
    }
    .btn-toggle-theme:hover {
      background: #4facfe;
      color: #fff;
    }
    .chat-message {
      margin-bottom: 12px;
      opacity: 1; /* Langsung muncul tanpa delay */
      position: relative;
      padding-right: 60px;
    }
    .chat-user { font-weight: 600; color: #007bff; }
    .chat-bot { font-weight: 600; color: #28a745; }
    .copy-chat-btn {
      position: absolute;
      right: 10px;
      top: 50%;
      transform: translateY(-50%);
      font-size: 12px;
      padding: 4px 8px;
      border: none;
      border-radius: 12px;
      background-color: #28a745;
      color: white;
      cursor: pointer;
      opacity: 0.7;
      transition: opacity 0.3s;
    }
    .copy-chat-btn:hover {
      opacity: 1;
    }
    .loading-spinner {
      border: 3px solid #f3f3f3;
      border-top: 3px solid #007bff;
      border-radius: 50%;
      width: 16px;
      height: 16px;
      animation: spin 1s linear infinite;
      position: absolute;
      right: 15px;
      top: 50%;
      transform: translateY(-50%);
      display: none;
    }
    .btn-loading .loading-spinner { display: inline-block; }
    .btn-loading .btn-text { visibility: hidden; }
    @keyframes spin {
      0% { transform: translateY(-50%) rotate(0deg); }
      100% { transform: translateY(-50%) rotate(360deg); }
    }
  </style>
</head>
<body>
  <button class="btn-toggle-theme" id="toggleTheme">🌙 Dark Mode</button>
  <div class="text-center mb-4">
    <div class="logo">ferdes.ai</div>
    <p class="text-white-50">Versi 5.1 Beta - Launcher Cerdas & Fitur Lengkap</p>
  </div>
  <div class="section-box">
    <h5>Cari Instan 🔍</h5>
    <form id="searchForm">
      <div class="input-group">
        <input type="text" class="form-control" id="query" placeholder="Cari sesuatu..." autocomplete="off" />
        <select class="form-select" id="engine">
          <option value="google">Google</option>
          <option value="bing">Bing</option>
          <option value="youtube">YouTube</option>
          <option value="tiktok">TikTok</option>
          <option value="wikipedia">Wikipedia</option>
        </select>
        <button class="btn btn-primary btn-round" type="submit">Cari</button>
      </div>
    </form>
  </div>
  <div class="section-box">
    <h5>Riwayat Pencarian</h5>
    <ul id="historyList" class="list-group"></ul>
    <button class="btn btn-sm btn-outline-danger mt-3" id="clearHistory">Hapus Riwayat</button>
  </div>
  <div class="section-box">
    <h5>Chat AI</h5>
    <div id="chatDisplay" style="max-height: 300px; overflow-y: auto; margin-bottom: 15px"></div>
    <div class="input-group">
      <input type="text" class="form-control" id="chatInput" placeholder="Tulis pertanyaan atau ngobrol..." autocomplete="off" />
      <button class="btn btn-success" id="sendChat">Kirim</button>
    </div>
  </div>
  <div class="section-box">
    <h5>Fitur Serba Bisa</h5>
    <div class="mb-3">
      <label for="videoUrl" class="form-label">Download Video (YT, TikTok, IG)</label>
      <input type="text" id="videoUrl" class="form-control" placeholder="Masukkan link..." />
      <button class="btn btn-primary btn-round mt-2 w-100" id="downloadVideoBtn">
        <span class="btn-text">Download MP4</span>
        <div class="loading-spinner"></div>
      </button>
    </div>
    <div class="mb-3">
      <label for="audioUrl" class="form-label">Download MP3</label>
      <input type="text" id="audioUrl" class="form-control" placeholder="Masukkan link..." />
      <button class="btn btn-success btn-round mt-2 w-100" id="downloadAudioBtn">
        <span class="btn-text">Download MP3</span>
        <div class="loading-spinner"></div>
      </button>
    </div>
    <div class="mb-3">
      <label for="imageInput" class="form-label">Hapus Background Gambar</label>
      <input type="file" id="imageInput" class="form-control" accept="image/*" />
      <button class="btn btn-warning btn-round mt-2 w-100" id="removeBgBtn">
        <span class="btn-text">Hapus BG</span>
        <div class="loading-spinner"></div>
      </button>
      <div id="outputImage" class="text-center mt-3"></div>
    </div>
  </div>

  <script>
    const engines = {
      google: "https://www.google.com/search?q=",
      bing: "https://www.bing.com/search?q=",
      youtube: "https://www.youtube.com/results?search_query=",
      tiktok: "https://www.tiktok.com/search?q=",
      wikipedia: "https://id.wikipedia.org/wiki/",
    };

    const form = document.getElementById("searchForm");
    const query = document.getElementById("query");
    const engine = document.getElementById("engine");
    const historyList = document.getElementById("historyList");
    const clearHistory = document.getElementById("clearHistory");
    const chatDisplay = document.getElementById("chatDisplay");
    const chatInput = document.getElementById("chatInput");
    const sendChat = document.getElementById("sendChat");
    const toggleThemeBtn = document.getElementById("toggleTheme");

    toggleThemeBtn.onclick = () => {
      document.body.classList.toggle("dark");
      toggleThemeBtn.textContent = document.body.classList.contains("dark") ? "☀️ Light Mode" : "🌙 Dark Mode";
      localStorage.setItem("theme", document.body.classList.contains("dark") ? "dark" : "light");
    };
    if (localStorage.getItem("theme") === "dark") {
      document.body.classList.add("dark");
      toggleThemeBtn.textContent = "☀️ Light Mode";
    }

    form.onsubmit = (e) => {
      e.preventDefault();
      const q = query.value.trim();
      if (!q) return;
      const url = engines[engine.value] + encodeURIComponent(q);
      window.open(url, "_blank");
      saveHistory(q);
      query.value = "";
    };

    function saveHistory(text) {
      let hist = JSON.parse(localStorage.getItem("ferdesHistory") || "[]");
      if (!hist.includes(text)) {
        hist.unshift(text);
        if (hist.length > 10) hist.pop();
        localStorage.setItem("ferdesHistory", JSON.stringify(hist));
      }
      renderHistory();
    }
    function renderHistory() {
      let hist = JSON.parse(localStorage.getItem("ferdesHistory") || "[]");
      historyList.innerHTML = "";
      hist.forEach((item) => {
        const li = document.createElement("li");
        li.className = "list-group-item d-flex justify-content-between align-items-center";
        li.textContent = item;
        const copyBtn = document.createElement("button");
        copyBtn.className = "btn btn-sm btn-outline-primary btn-copy";
        copyBtn.textContent = "Copy Link";
        copyBtn.onclick = () => {
          const url = engines[engine.value] + encodeURIComponent(item);
          navigator.clipboard.writeText(url);
          copyBtn.textContent = "Copied!";
          setTimeout(() => (copyBtn.textContent = "Copy Link"), 1500);
        };
        li.appendChild(copyBtn);
        historyList.appendChild(li);
      });
    }
    clearHistory.onclick = () => {
      localStorage.removeItem("ferdesHistory");
      renderHistory();
    };
    renderHistory();

    sendChat.onclick = () => sendMessage();
    chatInput.addEventListener("keypress", (e) => { if (e.key === "Enter") { e.preventDefault(); sendMessage(); } });
    function sendMessage() {
      const msg = chatInput.value.trim();
      if (!msg) return;
      chatInput.value = "";
      appendMessage("Kamu", msg, "chat-user");
      setTimeout(() => {
        appendMessage("ferdes.ai", generateAdvancedResponse(msg), "chat-bot");
      }, 800);
    }
    function appendMessage(sender, msg, cls) {
      const div = document.createElement("div");
      div.className = "chat-message";
      div.innerHTML = `<div class="${cls}">${sender}</div><div>${msg}</div>`;

      if (cls === "chat-bot") {
        const copyBtn = document.createElement("button");
        copyBtn.className = "copy-chat-btn";
        copyBtn.textContent = "Copy";
        copyBtn.title = "Salin jawaban";
        copyBtn.onclick = () => {
          navigator.clipboard.writeText(msg);
          copyBtn.textContent = "Copied!";
          setTimeout(() => (copyBtn.textContent = "Copy"), 1500);
        };
        div.appendChild(copyBtn);
      }

      chatDisplay.appendChild(div);

      // Scroll ke bawah dengan delay supaya chat muncul dan terlihat
      setTimeout(() => {
        chatDisplay.scrollTop = chatDisplay.scrollHeight;
      }, 100);
    }
    function generateAdvancedResponse(input) {
      input = input.toLowerCase();
      if (input.includes("rumus luas lingkaran")) return "Luas = π × r²";
      if (input.includes("presiden pertama")) return "Ir. Soekarno";
      if (input.includes("siapa kamu")) return "Aku ferdes.ai, AI buatan lokal!";
      if (input.includes("hai") || input.includes("halo")) return "Hai juga! Ada yang bisa aku bantu?";
      return "Maaf, aku belum ngerti penuh. Coba tanya hal lain 😉";
    }

    const downloadVideoBtn = document.getElementById("downloadVideoBtn");
    const downloadAudioBtn = document.getElementById("downloadAudioBtn");
    const removeBgBtn = document.getElementById("removeBgBtn");
    const videoUrl = document.getElementById("videoUrl");
    const audioUrl = document.getElementById("audioUrl");
    const imageInput = document.getElementById("imageInput");
    const outputImage = document.getElementById("outputImage");
    function simulateLoading(button, callback) {
      button.classList.add("btn-loading");
      setTimeout(() => {
        button.classList.remove("btn-loading");
        callback();
      }, 2000);
    }
    downloadVideoBtn.onclick = () => {
      const url = videoUrl.value.trim();
      if (!url) return alert("Masukkan link video dulu!");
      simulateLoading(downloadVideoBtn, () => alert("Fitur masih dalam pengembangan."));
    };
    downloadAudioBtn.onclick = () => {
      const url = audioUrl.value.trim();
      if (!url) return alert("Masukkan link audio dulu!");
      simulateLoading(downloadAudioBtn, () => alert("Fitur masih dalam pengembangan."));
    };
    removeBgBtn.onclick = () => {
      if (!imageInput.files.length) return alert("Pilih gambar dulu!");
      simulateLoading(removeBgBtn, () => alert("Fitur masih dalam pengembangan."));
    };
  </script>
</body>
</html>
