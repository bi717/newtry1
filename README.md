<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>美麗媽的秘製食譜</title>

  <!-- 引用可愛字體 -->
 "Patrick Hand"

  <style>
    /* 密碼錯誤時的畫面 */
    body.locked {
      background-color: #000;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: "Noto Sans TC", sans-serif;
      font-size: 24px;
      margin: 0;
    }

    /* 正常模式下的網站樣式 */
    body {
      font-family: 'Noto Sans TC', sans-serif;
      background:#FFE0AC
      background-size: cover;
      margin: 0;
      padding: 20px;
      color: #333;
    }

    h1 {
      font-family: 'ZCOOL KuaiLe', cursive;
      font-size: 36px;
      color: #FF6F61;
      text-align: center;
      margin-bottom: 30px;
    }

    .buttons {
      text-align: center;
      margin-bottom: 20px;
    }
    .buttons button {
      background-color: #FFB6B9;
      color: white;
      border: none;
      border-radius: 25px;
      padding: 10px 20px;
      margin: 5px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s, transform 0.2s;
      box-shadow: 2px 2px 5px rgba(0,0,0,0.1);
    }
    .buttons button:hover {
      background-color: #FF9AA2;
      transform: scale(1.05);
    }

    /* 搜尋框 */
    #searchInput {
      display: block;
      margin: 20px auto;
      padding: 10px;
      width: 80%;
      max-width: 400px;
      border-radius: 25px;
      border: 1px solid #ccc;
      font-size: 16px;
    }

    .recipe {
      background-color: rgba(255, 255, 255, 0.9);
      padding: 20px;
      margin-bottom: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    .recipe h2 {
      margin-top: 0;
      color: #FF6F61;
      font-size: 24px;
    }
    .section-title {
      font-weight: bold;
      margin-top: 10px;
      margin-bottom: 5px;
      color: #555;
    }
    ul, ol {
      margin-top: 5px;
      padding-left: 20px;
    }

    /* 夜間模式樣式 */
    body.dark-mode {
      background: #222;
      color: #eee;
    }
    body.dark-mode .recipe {
      background: #333;
    }
    body.dark-mode button {
      background-color: #666;
    }
    body.dark-mode #searchInput {
      background-color: #444;
      color: #eee;
    }
  </style>
</head>

<body>

<!-- 密碼保護（有完整註解） -->
<script>
// 啟動密碼保護功能
var password = prompt("請輸入密碼才能進入網站：");

// 判斷密碼
if (password !== "mylovelyrecipe") { // ←這裡自訂密碼
  // 密碼錯誤時，顯示錯誤畫面
  document.body.className = "locked";
  document.body.innerHTML = "密碼錯誤！請重新整理再試。";
}
</script>

<h1>美麗媽的秘製食譜 ❤︎</h1>

<div class="buttons">
  <button onclick="filterRecipes('全部')">全部</button>
  <button onclick="filterRecipes('家常菜')">家常菜</button>
  <button onclick="filterRecipes('甜點')">甜點</button>
  <button onclick="filterRecipes('麵包／早餐')">麵包／早餐</button>
  <button onclick="filterRecipes('鹹的')">鹹的</button>
  <button onclick="filterRecipes('肉類')">肉類</button>
  <button onclick="filterRecipes('其他')">其他</button>
  <button onclick="toggleDarkMode()">夜間模式</button> <!-- 新增夜間模式按鈕 -->
</div>

<input type="text" id="searchInput" placeholder="搜尋食譜..." oninput="searchRecipes()">

<div id="recipes">

  <div class="recipe" data-category="家常菜 肉類">
    <h2>滷肉飯</h2>
    <div class="section-title">食材：</div>
    <ul>
      <li>絞肉 300g</li>
      <li>醬油 2大匙</li>
      <li>糖 1小匙</li>
      <li>米酒 1大匙</li>
      <li>洋蔥 半顆</li>
    </ul>
    <div class="section-title">步驟：</div>
    <ol>
      <li>炒香洋蔥。</li>
      <li>加入絞肉煸炒。</li>
      <li>加調味料煮滾，小火燉30分鐘。</li>
      <li>淋在白飯上即可享用！</li>
    </ol>
  </div>

  <div class="recipe" data-category="甜點 麵包／早餐">
    <h2>法式吐司</h2>
    <div class="section-title">食材：</div>
    <ul>
      <li>吐司 2片</li>
      <li>蛋 1顆</li>
      <li>牛奶 50ml</li>
      <li>糖 1大匙</li>
    </ul>
    <div class="section-title">步驟：</div>
    <ol>
      <li>將蛋、牛奶、糖打散。</li>
      <li>吐司浸泡均勻。</li>
      <li>小火煎到兩面金黃。</li>
    </ol>
  </div>

  <!-- 可以在這裡繼續新增更多食譜 -->

</div>

<script>
// 分類按鈕功能
function filterRecipes(category) {
  const recipes = document.querySelectorAll('.recipe');
  recipes.forEach(recipe => {
    const categories = recipe.getAttribute('data-category').split(' ');
    if (category === '全部' || categories.includes(category)) {
      recipe.style.display = 'block';
    } else {
      recipe.style.display = 'none';
    }
  });
}

// 搜尋功能
function searchRecipes() {
  const keyword = document.getElementById('searchInput').value.toLowerCase();
  const recipes = document.querySelectorAll('.recipe');
  recipes.forEach(recipe => {
    const title = recipe.querySelector('h2').innerText.toLowerCase();
    if (title.includes(keyword)) {
      recipe.style.display = 'block';
    } else {
      recipe.style.display = 'none';
    }
  });
}

// 夜間模式切換
function toggleDarkMode() {
  document.body.classList.toggle('dark-mode');
}
</script>

</body>
</html>
