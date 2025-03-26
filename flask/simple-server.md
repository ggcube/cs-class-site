# 🖥️ Flask 簡易伺服器教學

## 課程目標
- 架設簡單的本地伺服器
- 讓同學能透過區網訪問

## 程式碼範例
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, 這是我的伺服器！"

app.run(host="0.0.0.0", port=5000)
```
