<!DOCTYPE html>
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>የኢትዮጵያ ሬስቶራንት ሜኑ</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f8f9fa;
            color: #333;
        }

        header {
            background: #2c1d11;
            color: white;
            text-align: center;
            padding: 40px 20px;
        }

        .container {
            max-width: 1100px;
            margin: 30px auto;
            padding: 0 20px;
        }

        /* ምድቦች ማሳያ ቁልፎች (Categories Filter) */
        .category-filters {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding-bottom: 15px;
            margin-bottom: 25px;
        }

        .filter-btn {
            background: white;
            border: 1px solid #ddd;
            padding: 8px 18px;
            border-radius: 20px;
            cursor: pointer;
            white-space: nowrap;
            font-weight: 500;
            color: #555;
        }

        .filter-btn.active, .filter-btn:hover {
            background: #b85d00;
            color: white;
            border-color: #b85d00;
        }

        .menu-category h2 {
            font-size: 1.8rem;
            color: #2c1d11;
            margin-bottom: 20px;
            border-left: 5px solid #b85d00;
            padding-left: 10px;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .menu-item {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            position: relative;
        }

        .menu-item img {
            width: 100%;
            height: 160px;
            object-fit: cover;
        }

        /* የጾም/የፍስክ መለያ ባጅ (Tag) */
        .badge {
            position: absolute;
            top: 10px;
            right: 10px;
            padding: 5px 12px;
            font-size: 0.8rem;
            font-weight: bold;
            border-radius: 20px;
            color: white;
        }

        .badge.fasting {
            background-color: #2e7d32; /* አረንጓዴ ለጾም */
        }

        .badge.non-fasting {
            background-color: #c62828; /* ቀይ ለፍስክ */
        }

        .item-details {
            padding: 15px;
        }

        .item-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }

        .item-header h3 {
            font-size: 1.1rem;
            color: #222;
        }

        .price {
            font-size: 1rem;
            font-weight: bold;
            color: #b85d00;
        }

        .item-description {
            font-size: 0.9rem;
            color: #666;
            margin-bottom: 15px;
        }

        .add-btn {
            width: 100%;
            background-color: #b85d00;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }

        .add-btn:hover {
            background-color: #964a00;
        }
    </style>
</head>
<body>

    <header>
        <h1>ባህላዊ የኢትዮጵያ ሬስቶራንት</h1>
        <p>ልዩ የጾም እና የፍስክ ምግቦች በታላቅ  ጣዕም</p>
    </header>

    <div class="container">
        <!-- የምድብ ማጣሪያዎች (Category Buttons) -->
        <div class="category-filters">
            <button class="filter-btn active">ሁሉም (All)</button>
            <button class="filter-btn">ቁርስ</button>
            <button class="filter-btn">የጾም ምግቦች</button>
            <button class="filter-btn">የፍስክ ምግቦች</button>
            <button class="filter-btn">መጠጦች</button>
        </div>

        <!-- የጾም ምግቦች ክፍል -->
        <div class="menu-category">
            <h2>የጾም ምግቦች (Fasting Menu)</h2>
            <div class="menu-grid">
                
                <div class="menu-item">
                    <span class="badge fasting">የጾም</span>
                    <img src="https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&w=600&q=80" alt="ሽሮ ወጥ">
                    <div class="item-details">
                        <div class="item-header">
                            <h3>የሐበሻ ሽሮ ወጥ</h3>
                            <span class="price">250 ብር</span>
                        </div>
                        <p class="item-description">በየነጭ ሽንኩርት እና ቅመም የተከተፈ ድንቅ የጓሮ ሽሮ ከ እንጀራ ጋር።</p>
                        <button class="add-btn">ወደ ከርት ጨምር</button>
                    </div>
                </div>

                <div class="menu-item">
                    <span class="badge fasting">የጾም</span>
                    <img src="https://images.unsplash.com/photo-1512621776951-a57141f2eefd?auto=format&fit=crop&w=600&q=80" alt="atkilt">
                    <div class="item-details">
                        <div class="item-header">
                            <h3>አታክልት ወጥ</h3>
                            <span class="price">220 ብር</span>
                        </div>
                        <p class="item-description">ድንች፣ ካሮት እና ጎመን በቅቤ-አልባ ዘይትና μጋ የተጠበሰ።</p>
                        <button class="add-btn">ወደ ከርት ጨምር</button>
                    </div>
                </div>

            </div>
        </div>

        <!-- የፍስክ ምግቦች ክፍል -->
        <div class="menu-category">
            <h2>የፍስክ ምግቦች (Non-Fasting Menu)</h2>
            <div class="menu-grid">
                
                <div class="menu-item">
                    <span class="badge non-fasting">የፍስክ</span>
                    <img src="https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=600&q=80" alt="ጥብስ">
                    <div class="item-details">
                        <div class="item-header">
                            <h3>ልዩ የበሬ ጥብስ</h3>
                            <span class="price">650 ብር</span>
                        </div>
                        <p class="item-description">ለስላሳ ስጋ ከነጭ ሽንኩርት፣ ሮዝማሪ እና አረንጓዴ ፔፐር ጋር የተጠበሰ።</p>
                        <button class="add-btn">ወደ ከርት ጨምር</button>
                    </div>
                </div>

                <div class="menu-item">
                    <span class="badge non-fasting">የፍስክ</span>
                    <img src="https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&w=600&q=80" alt="ዶሮ ወጥ">
                    <div class="item-details">
                        <div class="item-header">
                            <h3>ባህላዊ የዶሮ ወጥ</h3>
                            <span class="price">700 ብር</span>
                        </div>
                        <p class="item-description">በቀይ ሽንኩርት፣ በርበሬ፣ ቂቤ እና ሙሉ እንቁላል የተሰራ።</p>
                        <button class="add-btn">ወደ ከርት ጨምር</button>
                    </div>
                </div>

            </div>
        </div>

    </div>

</body>
</html>
