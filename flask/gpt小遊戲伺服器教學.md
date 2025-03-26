# 🧠 GPT 小遊戲伺服器教學

## 🎯 課程目標
- 學會使用 Flask 架設區網內部的遊戲伺服器
- 使用 GPT 協助生成 HTML + JS 小遊戲
- 讓同學在電腦教室中，透過瀏覽器連線體驗互動式遊戲

---

## 🧰 準備工具
- 安裝 Python 3
- 安裝 Flask 套件：
```bash
pip install flask
```
- 使用 VSCode 或記事本

---

## 📁 專案結構
```
gpt-game-server/
├── app.py                ← Flask 主程式
├── static/
│   └── game.html         ← GPT 產生的小遊戲頁面
└── templates/
    └── index.html        ← 首頁（列出可玩遊戲）
```

---

## 🖥️ Flask 主程式：`app.py`

```python
from flask import Flask, send_from_directory, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/game")
def game():
    return send_from_directory("static", "game.html")

app.run(host="0.0.0.0", port=5000)
```

---

## 🌐 建立遊戲畫面：`static/game.html`

```html
<!DOCTYPE html>
<html>
<head>
  <title>單字配對遊戲</title>
</head>
<body>
  <h2>請點選對應的中英文</h2>
  <ul id="wordList"></ul>
  <script>
    const words = [
      { en: "apple", zh: "蘋果" },
      { en: "cat", zh: "貓" },
      { en: "book", zh: "書" }
    ];
    // 這裡可補上 GPT 生成的互動邏輯
  </script>
</body>
</html>
```

---

## 📃 建立首頁：`templates/index.html`

```html
<!DOCTYPE html>
<html>
<head>
  <title>GPT 小遊戲首頁</title>
</head>
<body>
  <h1>歡迎來玩 GPT 小遊戲</h1>
  <a href="/game">進入單字配對遊戲</a>
</body>
</html>
```

---

## 🛠️ 啟動伺服器

1. 打開命令提示字元或 VSCode Terminal
2. 進入資料夾後輸入：
```bash
python app.py
```
3. 出現以下訊息表示成功：
```
Running on http://0.0.0.0:5000/
```

---

## 🤝 學生如何連線
請學生打開瀏覽器，輸入你的 IP，例如：
```
http://192.168.0.10:5000/game
```
即可進入 GPT 遊戲！

---

## 🔐 防火牆設定（Windows）
記得開放 5000 port，步驟如下：
1. 開啟「防火牆與進階安全性」
2. 建立新的輸入規則
3. 開啟 TCP 的 5000 port
4. 設定為允許內部連線

---

## 💡 延伸挑戰
- 將遊戲改成數學題、猜數字、圖形配對等
- 每組同學製作不同 GPT 小遊戲在區網互訪
- 加入倒數計時、分數累積、排行榜等功能

---

祝大家玩得開心也學得開心！
