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

        /* የምድብ ማጣሪያ አዝራሮች (Filter Buttons) */
        .category-filters {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .filter-btn {
            background: white;
            border: 1px solid #b85d00;
            padding: 10px 20px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            color: #b85d00;
            transition: all 0.3s ease;
        }

        .filter-btn.active, .filter-btn:hover {
            background: #b85d00;
            color: white;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        .menu-item {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            position: relative;
            transition: transform 0.3s ease;
        }

        .menu-item:hover {
            transform: translateY(-5px);
        }

        .menu-item img {
            width: 100%;
            height: 160px;
            object-fit: cover;
        }

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
            background-color: #2e7d32;
        }

        .badge.non-fasting {
            background-color: #c62828;
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
        <p>የጾም እና የፍስክ ምግቦች ማጣሪያ</p>
    </header>

    <div class="container">
        <!-- ማጣሪያ አዝራሮች (Filter Buttons) -->
        <div class="category-filters">
            <button class="filter-btn active" onclick="filterMenu('all')">ሁሉም</button>
            <button class="filter-btn" onclick="filterMenu('fasting')">የጾም ምግቦች</button>
            <button class="filter-btn" onclick="filterMenu('non-fasting')">የፍስክ ምግቦች</button>
        </div>

        <!-- የምግብ ዝርዝር ግሪድ -->
        <div class="menu-grid" id="menuGrid">
            
            <!-- የጾም ምግብ 1 -->
            <div class="menu-item" data-category="fasting">
                <span class="badge fasting">የጾም</span>
                <img src="shro fasting .webp" alt="የጾም ሽሮ">
                <div class="item-details">
                    <div class="item-header">
                        <h3>የሐበሻ ሽሮ ወጥ</h3>
                        <span class="price">250 ብር</span>
                    </div>
                    <p class="item-description">በነጭ ሽንኩርት እና ቅመም የተዘጋጀ ድንቅ የጓሮ ሽሮ ከ እንጀራ ጋር።</p>
                    <button class="add-btn">ወደ ከርት ጨምር</button>
                </div>
            </div>

            <!-- የጾም ምግብ 2 -->
            <div class="menu-item" data-category="fasting">
                <span class="badge fasting">የጾም</span>
                <img src="chchbsa fasting.jpeg" alt="የጾም ጨጨብሳ">
                <div class="item-details">
                    <div class="item-header">
                        <h3>የጾም ጨጨብሳ</h3>
                        <span class="price">200 ብር</span>
                    </div>
                    <p class="item-description">በቂቤ ምትክ በንጹህ ዘይት እና በርበሬ የተዘጋጀ ለስላሳ ጨጨብሳ።</p>
                    <button class="add-btn">ወደ ከርት ጨምር</button>
                </div>
            </div>

            <!-- የፍስክ ምግብ 1 -->
            <div class="menu-item" data-category="non-fasting">
                <span class="badge non-fasting">የፍስክ</span>
                <img src="shekla tbsb non fasting.jpeg" alt="ሸክላ ጥብስ">
                <div class="item-details">
                    <div class="item-header">
                        <h3>ልዩ የሸክላ ጥብስ</h3>
                        <span class="price">650 ብር</span>
                    </div>
                    <p class="item-description">በሸክላ ጣድ የተጠበሰ ለስላሳ ስጋ ከነጭ ሽንኩርት እና ሮዝማሪ ጋር።</p>
                    <button class="add-btn">ወደ ከርት ጨምር</button>
                </div>
            </div>

            <!-- የፍስክ ምግብ 2 -->
            <div class="menu-item" data-category="non-fasting">
                <span class="badge non-fasting">የፍስክ</span>
                <img src="doro wat non fasting.jpeg" alt="ዶሮ ወጥ">
                <div class="item-details">
                    <div class="item-header">
                        <h3>ባህላዊ የዶሮ ወጥ</h3>
                        <span class="price">700 ብር</span>
                    </div>
                    <p class="item-description">በቀይ ሽንኩርት፣ በርበሬ፣ ቂቤ እና ሙሉ እንቁላል የተሰራ።</p>
                    <button class="add-btn">ወደ ከርት ጨምር</button>
                </div>
            </div>

            <!-- የፍስክ ምግብ 3 -->
            <div class="menu-item" data-category="non-fasting">
                <span class="badge non-fasting">የፍስክ</span>
                <img src="spacial ktfo non fasting.jpeg" alt="ክትፎ">
                <div class="item-details">
                    <div class="item-header">
                        <h3>ልዩ የቤቱ ክትፎ</h3>
                        <span class="price">750 ብር</span>
                    </div>
                    <p class="item-description">በጥራት ስጋ፣ ሚጥሚጣ እና ቀልጦ በተሰራ ቂቤ የተዘጋጀ።</p>
                    <button class="add-btn">ወደ ከርት ጨምር</button>
                </div>
            </div>

        </div>
    </div>

    <script>
        function filterMenu(category) {
            // የአዝራሮቹን ንቁ (active) ሁኔታ መቀየር
            const buttons = document.querySelectorAll('.filter-btn');
            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            // ምግቦቹን ማጣራት
            const items = document.querySelectorAll('.menu-item');
            items.forEach(item => {
                if (category === 'all' || item.getAttribute('data-category') === category) {
                    item.style.display = 'block';
                } else {
                    item.style.display = 'none';
                }
            });
        }
    </script>

</body>
</html>
