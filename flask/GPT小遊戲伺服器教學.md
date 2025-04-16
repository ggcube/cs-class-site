# 🐍 貪食蛇遊戲伺服器教學

## 🎯 課程目標
- 在本地區網環境中建立小遊戲伺服器
- 使用 Flask 架設靜態 HTML 遊戲頁面
- 學生透過瀏覽器連線即可遊玩「貪食蛇」

---

## 📁 專案資料夾結構
```
snake-game-server/
├── app.py                    ← Flask 主程式
├── static/
│   └── snake.html            ← 遊戲主頁面（HTML + JS）
└── templates/
    └── index.html            ← 首頁（遊戲入口）
```

---

## 🧱 Flask 主程式：`app.py`
```python
from flask import Flask, send_from_directory, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/snake")
def snake():
    return send_from_directory("static", "snake.html")

app.run(host="0.0.0.0", port=5000)
```

---

## 🖥️ 首頁：`templates/index.html`
```html
<!DOCTYPE html>
<html>
<head>
  <title>遊戲首頁</title>
</head>
<body>
  <h1>🎮 小遊戲伺服器</h1>
  <a href="/snake">點這裡玩貪食蛇</a>
</body>
</html>
```

---

## 🐍 遊戲頁面：`static/snake.html`
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>貪食蛇 Snake Game</title>
  <style>
    canvas { background: #000; display: block; margin: 20px auto; }
    body { text-align: center; font-family: sans-serif; }
  </style>
</head>
<body>
  <h1>🐍 貪食蛇遊戲</h1>
  <canvas id="game" width="400" height="400"></canvas>
  <script>
    const canvas = document.getElementById("game");
    const ctx = canvas.getContext("2d");
    const box = 20;
    let snake = [{ x: 200, y: 200 }];
    let direction = "RIGHT";
    let food = {
      x: Math.floor(Math.random() * 20) * box,
      y: Math.floor(Math.random() * 20) * box
    };

    document.addEventListener("keydown", e => {
      if (e.key === "ArrowUp" && direction !== "DOWN") direction = "UP";
      if (e.key === "ArrowDown" && direction !== "UP") direction = "DOWN";
      if (e.key === "ArrowLeft" && direction !== "RIGHT") direction = "LEFT";
      if (e.key === "ArrowRight" && direction !== "LEFT") direction = "RIGHT";
    });

    function resetGame() {
      snake = [{ x: 200, y: 200 }];
      direction = "RIGHT";
      food = {
        x: Math.floor(Math.random() * 20) * box,
        y: Math.floor(Math.random() * 20) * box
      };
    }

    function draw() {
      ctx.clearRect(0, 0, 400, 400);
      for (let i = 0; i < snake.length; i++) {
        ctx.fillStyle = i === 0 ? "lime" : "green";
        ctx.fillRect(snake[i].x, snake[i].y, box, box);
      }
      ctx.fillStyle = "red";
      ctx.fillRect(food.x, food.y, box, box);

      let headX = snake[0].x;
      let headY = snake[0].y;
      if (direction === "LEFT") headX -= box;
      if (direction === "RIGHT") headX += box;
      if (direction === "UP") headY -= box;
      if (direction === "DOWN") headY += box;

      if (
        headX < 0 || headY < 0 || headX >= 400 || headY >= 400 ||
        snake.some(seg => seg.x === headX && seg.y === headY)
      ) {
        alert("Game Over! 分數：" + (snake.length - 1));
        resetGame();
        return;
      }

      let newHead = { x: headX, y: headY };
      if (headX === food.x && headY === food.y) {
        food = {
          x: Math.floor(Math.random() * 20) * box,
          y: Math.floor(Math.random() * 20) * box
        };
      } else {
        snake.pop();
      }
      snake.unshift(newHead);
    }
    setInterval(draw, 100);
  </script>
</body>
</html>
```

---

## 🔗 學生連線方式
請學生在瀏覽器輸入：
```
http://你的IP位址:5000/snake
```
（例如：http://192.168.0.10:5000/snake）

---

## 🔐 防火牆設定
請務必開放 TCP port 5000，否則學生無法連線。
可參考 Flask 防火牆設定教學課程。

---

## 💡 延伸挑戰
- 增加分數顯示 / 最高分記錄
- 增加加速功能、障礙物
- 支援手機操作
- 改寫成「多人連線」對戰版（需 Socket）

---

## GPT生成提示詞
幫我用純 HTML + JavaScript 寫一個簡單的「貪食蛇」遊戲，請把程式包在單一 snake.html 檔案中，包含 canvas 畫面、遊戲邏輯與鍵盤操作，使用 <script> 內嵌方式，不需要額外連結外部 JS 或 CSS。請確保可以直接在瀏覽器中開啟並執行。

---


祝你成為區網遊戲伺服器大師！

