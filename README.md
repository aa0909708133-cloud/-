# Y-U-G-E-F-U-R-N-I-T-U-R-E
跟家有關係的都可以找優閣
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>優閣二手傢俱行</title>

<style>
:root {
  --bg: #f9f9f9;
  --text: #333;
  --card: #ffffff;
  --border: #e0e0e0;
}

.dark {
  --bg: #1e1e1e;
  --text: #f1f1f1;
  --card: #2a2a2a;
  --border: #444;
}

body {
  font-family: "Noto Sans TC", sans-serif;
  margin: 0;
  background: var(--bg);
  color: var(--text);
}

header {
  padding: 40px 20px;
  text-align: center;
  background: var(--card);
  border-bottom: 1px solid var(--border);
}

.logo {
  font-size: 40px;
  font-weight: bold;
}

.tagline {
  font-size: 18px;
  color: #888;
}

section {
  max-width: 1100px;
  margin: auto;
  padding: 40px 20px;
}

.card {
  background: var(--card);
  border: 1px solid var(--border);
  padding: 30px;
  border-radius: 12px;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 15px;
}

.gallery-item {
  background: #eaeaea;
  height: 160px;
  border-radius: 8px;
  overflow: hidden;
  position: relative;
}

.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.price-tag {
  position: absolute;
  bottom: 5px;
  right: 5px;
  background: rgba(0,0,0,0.65);
  color: white;
  padding: 3px 7px;
  font-size: 14px;
  border-radius: 5px;
}

.category-title {
  font-weight: bold;
  margin: 25px 0 10px;
  font-size: 20px;
}

#upload-area {
  border: 2px dashed var(--border);
  padding: 20px;
  text-align: center;
  border-radius: 10px;
  margin-bottom: 25px;
}

.btn-group {
  text-align: center;
  margin-top: 15px;
}

a.btn {
  display: inline-block;
  padding: 12px 20px;
  margin: 5px;
  border-radius: 8px;
  color: white;
  text-decoration: none;
  font-weight: bold;
}

.btn-line { background: #06c755; }
.btn-messenger { background: #0084ff; }

#qrcode-page {
  display: none;
  padding: 40px 20px;
  text-align: center;
}

.qr-block {
  background: var(--card);
  padding: 20px;
  border-radius: 12px;
  margin: 15px auto;
  width: 260px;
}

footer {
  text-align: center;
  color: #777;
  padding: 20px;
}
</style>
</head>

<body>

<header>
  <!-- LOGO -->
  <div class="logo">
    <svg width="180" height="60" viewBox="0 0 300 100" xmlns="http://www.w3.org/2000/svg">
      <rect x="10" y="35" width="60" height="25" rx="5" fill="#2c3e50"/>
      <rect x="80" y="20" width="120" height="40" rx="5" fill="#34495e"/>
      <rect x="210" y="35" width="60" height="25" rx="5" fill="#2c3e50"/>
      <text x="150" y="90" font-size="28" text-anchor="middle" fill="#2c3e50" font-family="sans-serif">
        優閣二手傢俱行
      </text>
    </svg>
  </div>
  <div class="tagline">讓好傢俱找到下一個幸福的家</div>

  <!-- 按鈕：深色模式 & 管理模式 -->
  <button onclick="toggleTheme()">切換深色 / 亮色模式</button>
  <button onclick="enterAdmin()">🔐 管理模式</button>
</header>

<!-- 關於我們 -->
<section>
  <div class="card">
    <h2>關於我們</h2>
    <p>
      優閣二手傢俱行專營二手家具買賣，主打明亮、簡約、實用的家居風格。<br>
      想處理不需要的家具？想用划算的價格找到好物？都可以找我！
    </p>
  </div>
</section>

<!-- 照片上傳區 -->
<section>
  <h2>家具展示 / 自動分類與標價</h2>

  <div id="upload-area">
    <p>上傳家具照片（可多選）：</p>
    <input type="file" id="upload" accept="image/*" multiple>
    <p>
      選擇類別：
      <select id="category">
        <option value="桌子">桌子</option>
        <option value="椅子">椅子</option>
        <option value="床">床</option>
        <option value="櫃子">櫃子</option>
        <option value="其他">其他</option>
      </select>
      售價：<input type="number" id="price" placeholder="如 1200" style="width:100px;">
    </p>
  </div>

  <div class="category-title">桌子</div>
  <div class="gallery" id="桌子"></div>

  <div class="category-title">椅子</div>
  <div class="gallery" id="椅子"></div>

  <div class="category-title">床</div>
  <div class="gallery" id="床"></div>

  <div class="category-title">櫃子</div>
  <div class="gallery" id="櫃子"></div>

  <div class="category-title">其他</div>
  <div class="gallery" id="其他"></div>
</section>

<script>
/* ===================== */
/* 深色模式切換 */
function toggleTheme() {
  document.body.classList.toggle("dark");
}

/* ===================== */
/* 管理模式輸入密碼 */
function enterAdmin() {
  const pwd = prompt("請輸入管理密碼：");
  if(pwd === "588599") {
    alert("管理模式啟動！點擊照片即可刪除。");
    enableDelete();
  } else {
    alert("密碼錯誤！");
  }
}

/* ===================== */
/* 照片上傳 + 自動分類 + 標價 */
document.getElementById("upload").addEventListener("change", function (e) {
  const files = e.target.files;
  const category = document.getElementById("category").value;
  const price = document.getElementById("price").value || "未定價";
  const target = document.getElementById(category);

  Array.from(files).forEach(file => {
    const reader = new FileReader();
    reader.onload = function (event) {
      const div = document.createElement("div");
      div.className = "gallery-item";
      div.dataset.category = category;
      div.innerHTML = `
        <img src="${event.target.result}">
        <div class="price-tag">$${price}</div>
      `;
      target.appendChild(div);
    };
    reader.readAsDataURL(file);
  });
});

/* ===================== */
/* 啟用刪除照片功能（管理模式） */
function enableDelete() {
  document.querySelectorAll(".gallery-item").forEach(item => {
    item.addEventListener("click", function() {
      if(confirm("確定要刪除這張照片嗎？")) {
        item.remove();
      }
    });
  });
}
</script>
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>優閣二手傢俱行</title>

<style>
:root {
  --bg: #f9f9f9;
  --text: #333;
  --card: #ffffff;
  --border: #e0e0e0;
}

.dark {
  --bg: #1e1e1e;
  --text: #f1f1f1;
  --card: #2a2a2a;
  --border: #444;
}

body {
  font-family: "Noto Sans TC", sans-serif;
  margin: 0;
  background: var(--bg);
  color: var(--text);
}

header {
  padding: 40px 20px;
  text-align: center;
  background: var(--card);
  border-bottom: 1px solid var(--border);
}

.logo {
  font-size: 40px;
  font-weight: bold;
}

.tagline {
  font-size: 18px;
  color: #888;
}

section {
  max-width: 1100px;
  margin: auto;
  padding: 40px 20px;
}

.card {
  background: var(--card);
  border: 1px solid var(--border);
  padding: 30px;
  border-radius: 12px;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 15px;
}

.gallery-item {
  background: #eaeaea;
  height: 160px;
  border-radius: 8px;
  overflow: hidden;
  position: relative;
}

.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.price-tag {
  position: absolute;
  bottom: 5px;
  right: 5px;
  background: rgba(0,0,0,0.65);
  color: white;
  padding: 3px 7px;
  font-size: 14px;
  border-radius: 5px;
}

.category-title {
  font-weight: bold;
  margin: 25px 0 10px;
  font-size: 20px;
}

#upload-area {
  border: 2px dashed var(--border);
  padding: 20px;
  text-align: center;
  border-radius: 10px;
  margin-bottom: 25px;
}

.btn-group {
  text-align: center;
  margin-top: 15px;
}

a.btn {
  display: inline-block;
  padding: 12px 20px;
  margin: 5px;
  border-radius: 8px;
  color: white;
  text-decoration: none;
  font-weight: bold;
}

.btn-line { background: #06c755; }
.btn-messenger { background: #0084ff; }

#qrcode-page {
  display: none;
  padding: 40px 20px;
  text-align: center;
}

.qr-block {
  background: var(--card);
  padding: 20px;
  border-radius: 12px;
  margin: 15px auto;
  width: 260px;
}

footer {
  text-align: center;
  color: #777;
  padding: 20px;
}
</style>
</head>

<body>

<header>
  <!-- LOGO -->
  <div class="logo">
    <svg width="180" height="60" viewBox="0 0 300 100" xmlns="http://www.w3.org/2000/svg">
      <rect x="10" y="35" width="60" height="25" rx="5" fill="#2c3e50"/>
      <rect x="80" y="20" width="120" height="40" rx="5" fill="#34495e"/>
      <rect x="210" y="35" width="60" height="25" rx="5" fill="#2c3e50"/>
      <text x="150" y="90" font-size="28" text-anchor="middle" fill="#2c3e50" font-family="sans-serif">
        優閣二手傢俱行
      </text>
    </svg>
  </div>
  <div class="tagline">讓好傢俱找到下一個幸福的家</div>

  <!-- 按鈕：深色模式 & 管理模式 -->
  <button onclick="toggleTheme()">切換深色 / 亮色模式</button>
  <button onclick="enterAdmin()">🔐 管理模式</button>
</header>

<!-- 關於我們 -->
<section>
  <div class="card">
    <h2>關於我們</h2>
    <p>
      優閣二手傢俱行專營二手家具買賣，主打明亮、簡約、實用的家居風格。<br>
      想處理不需要的家具？想用划算的價格找到好物？都可以找我！
    </p>
  </div>
</section>

<!-- 照片上傳區 -->
<section>
  <h2>家具展示 / 自動分類與標價</h2>

  <div id="upload-area">
    <p>上傳家具照片（可多選）：</p>
    <input type="file" id="upload" accept="image/*" multiple>
    <p>
      選擇類別：
      <select id="category">
        <option value="桌子">桌子</option>
        <option value="椅子">椅子</option>
        <option value="床">床</option>
        <option value="櫃子">櫃子</option>
        <option value="其他">其他</option>
      </select>
      售價：<input type="number" id="price" placeholder="如 1200" style="width:100px;">
    </p>
  </div>

  <div class="category-title">桌子</div>
  <div class="gallery" id="桌子"></div>

  <div class="category-title">椅子</div>
  <div class="gallery" id="椅子"></div>

  <div class="category-title">床</div>
  <div class="gallery" id="床"></div>

  <div class="category-title">櫃子</div>
  <div class="gallery" id="櫃子"></div>

  <div class="category-title">其他</div>
  <div class="gallery" id="其他"></div>
</section>

<script>
/* ===================== */
/* 深色模式切換 */
function toggleTheme() {
  document.body.classList.toggle("dark");
}

/* ===================== */
/* 管理模式輸入密碼 */
function enterAdmin() {
  const pwd = prompt("請輸入管理密碼：");
  if(pwd === "588599") {
    alert("管理模式啟動！點擊照片即可刪除。");
    enableDelete();
  } else {
    alert("密碼錯誤！");
  }
}

/* ===================== */
/* 照片上傳 + 自動分類 + 標價 */
document.getElementById("upload").addEventListener("change", function (e) {
  const files = e.target.files;
  const category = document.getElementById("category").value;
  const price = document.getElementById("price").value || "未定價";
  const target = document.getElementById(category);

  Array.from(files).forEach(file => {
    const reader = new FileReader();
    reader.onload = function (event) {
      const div = document.createElement("div");
      div.className = "gallery-item";
      div.dataset.category = category;
      div.innerHTML = `
        <img src="${event.target.result}">
        <div class="price-tag">$${price}</div>
      `;
      target.appendChild(div);
    };
    reader.readAsDataURL(file);
  });
});

/* ===================== */
/* 啟用刪除照片功能（管理模式） */
function enableDelete() {
  document.querySelectorAll(".gallery-item").forEach(item => {
    item.addEventListener("click", function() {
      if(confirm("確定要刪除這張照片嗎？")) {
        item.remove();
      }
    });
  });
}
</script>
<!-- ===================== -->
<!-- Google Map -->
<!-- ===================== -->
<section>
  <div class="card">
    <h2>店家位置</h2>
    <iframe
      width="100%" height="300"
      style="border:0; border-radius: 12px;"
      src="https://www.google.com/maps?q=嘉義縣大林鎮&output=embed"
      allowfullscreen="">
    </iframe>
  </div>
</section>

<!-- ===================== -->
<!-- 聯絡方式 -->
<!-- ===================== -->
<section>
  <div class="card">
    <h2>聯絡方式</h2>

    <p><strong>LINE：</strong>fory886</p>
    <p><strong>電話：</strong>0958-253-437</p>
    <p><strong>地址：</strong>嘉義縣大林鎮</p>
    <p><strong>統一編號：</strong>94355193</p>

    <div class="btn-group">
      <a class="btn btn-line" href="https://line.me/ti/p/~fory886" target="_blank">LINE 聯絡我</a>
      <a class="btn btn-messenger" href="https://m.me/" target="_blank">Messenger 聯絡我</a>
    </div>
  </div>
</section>

<!-- ===================== -->
<!-- 收購詢問表單 -->
<!-- ===================== -->
<section>
  <div class="card">
    <h2>家具收購詢問</h2>
    <form onsubmit="alert('已送出，我們會盡快聯絡您！'); return false;">
      姓名：<br><input type="text" required><br><br>
      聯絡電話：<br><input type="text" required><br><br>
      傢俱種類：<br>
      <select>
        <option>桌子</option><option>椅子</option><option>床</option><option>櫃子</option><option>其他</option>
      </select><br><br>
      備註：<br>
      <textarea style="width:100%; height:80px;"></textarea><br><br>
      <button type="submit">送出</button>
    </form>
  </div>
</section>

<!-- ===================== -->
<!-- QR Code 名片頁面 -->
<!-- ===================== -->
<div id="qrcode-page">
  <h2>優閣二手傢俱行 • 名片</h2>

  <div class="qr-block">
    <p>LINE</p>
    <img src="https://api.qrserver.com/v1/create-qr-code/?size=230x230&data=https://line.me/ti/p/~fory886">
  </div>

  <div class="qr-block">
    <p>電話</p>
    <img src="https://api.qrserver.com/v1/create-qr-code/?size=230x230&data=tel:0958253437">
  </div>

  <button onclick="hideQR()">返回網站</button>
</div>
