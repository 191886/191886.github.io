<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>星空匯率換算器</title>
    <style>
        /* -------------------------------------
        // CSS 樣式：星空背景與佈局
        // ------------------------------------- */
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            color: #E0FFFF; /* 淺青色文字 */
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #000000; /* 基礎黑色 */
            /* 星空背景效果 */
            background-image: 
                radial-gradient(circle at 10% 50%, rgba(255, 255, 255, 0.6) 1px, transparent 2px),
                radial-gradient(circle at 90% 90%, rgba(255, 255, 255, 0.8) 1.5px, transparent 3px),
                radial-gradient(circle at 60% 30%, rgba(255, 255, 255, 0.4) 1px, transparent 2px);
            background-size: 2000px 2000px; /* 使星星分散 */
            animation: animateStarrySky 60s linear infinite; /* 星星移動動畫 */
        }

        /* 星星移動動畫 */
        @keyframes animateStarrySky {
            from {
                background-position: 0 0;
            }
            to {
                background-position: 2000px 2000px;
            }
        }

        .container {
            background-color: rgba(0, 0, 50, 0.8); /* 略透明的深藍色，模擬夜空中的一個區域 */
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 0 30px rgba(70, 70, 255, 0.7); /* 藍色光暈效果 */
            width: 90%;
            max-width: 450px;
            text-align: center;
        }

        h2 {
            margin-top: 0;
            color: #FFD700; /* 金色標題 */
            border-bottom: 2px solid #FFD700;
            padding-bottom: 10px;
            margin-bottom: 30px;
        }

        .input-group {
            margin-bottom: 25px;
            text-align: left;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #87CEFA; /* 淺藍色標籤 */
        }

        input[type="number"], select {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #00BFFF; /* 邊框亮藍色 */
            background-color: rgba(255, 255, 255, 0.1); /* 輸入框半透明 */
            color: #E0FFFF;
            box-sizing: border-box;
            font-size: 16px;
        }

        input[type="number"]:focus, select:focus {
            outline: none;
            border-color: #FF4500; /* 聚焦時橙紅色 */
            box-shadow: 0 0 10px rgba(255, 69, 0, 0.5);
        }

        .result {
            margin-top: 30px;
            padding: 15px;
            border: 2px solid #3CB371; /* 中綠色邊框 */
            border-radius: 8px;
            background-color: rgba(60, 179, 113, 0.2); /* 結果區塊半透明背景 */
            font-size: 1.2em;
            font-weight: bold;
            color: #ADFF2F; /* 螢光綠結果文字 */
        }
    </style>
</head>
<body>

<div class="container">
    <h2>✨ 星空匯率換算器 ✨</h2>

    <div class="input-group">
        <label for="amount">輸入金額：</label>
        <input type="number" id="amount" value="100" min="0" oninput="convertCurrency()">
    </div>

    <div class="input-group">
        <label for="currency">選擇外幣：</label>
        <select id="currency" onchange="convertCurrency()">
            <option value="USD">美元 (USD)</option>
            <option value="JPY">日圓 (JPY)</option>
            <option value="EUR">歐元 (EUR)</option>
            <option value="HKD">港幣 (HKD)</option>
            <option value="CNY">人民幣 (CNY)</option>
        </select>
    </div>

    <div class="result">
        換算結果 (新台幣 TWD)：
        <p id="result-twd">請輸入金額</p>
    </div>
</div>

<script>
    /* -------------------------------------
    // JavaScript 邏輯：匯率換算
    // ------------------------------------- */

    // 範例匯率：1 單位外幣 可換算成多少 TWD (新台幣)
    // *** 這是固定值，非即時匯率 ***
    const RATES_TO_TWD = {
        'USD': 32.00, // 1 USD = 32.00 TWD
        'JPY': 0.2200, // 1 JPY = 0.2200 TWD
        'EUR': 34.50, // 1 EUR = 34.50 TWD
        'HKD': 4.10, // 1 HKD = 4.10 TWD
        'CNY': 4.35  // 1 CNY = 4.35 TWD
    };

    /**
     * 執行匯率換算並顯示結果
     */
    function convertCurrency() {
        // 獲取輸入值
        const amountInput = document.getElementById('amount');
        const currencySelect = document.getElementById('currency');
        const resultParagraph = document.getElementById('result-twd');

        const amount = parseFloat(amountInput.value);
        const selectedCurrency = currencySelect.value;
        const rate = RATES_TO_TWD[selectedCurrency];

        // 檢查輸入是否有效
        if (isNaN(amount) || amount <= 0) {
            resultParagraph.textContent = '請輸入有效金額';
            return;
        }

        // 進行換算
        const resultTWD = amount * rate;

        // 格式化結果並顯示
        // toLocaleString('zh-TW', { style: 'currency', currency: 'TWD' }) 可以格式化為新台幣樣式
        resultParagraph.textContent = resultTWD.toFixed(2).toLocaleString('zh-TW') + ' TWD';
    }

    // 頁面載入時執行一次換算，以顯示初始結果
    window.onload = convertCurrency;
</script>

</body>
</html>
