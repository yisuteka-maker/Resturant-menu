   <!DOCTYPE html>
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital QR Menu</title>
    <style>
        :root {
            --primary-color: #D32F2F;
            --bg-color: #F8F9FA;
            --card-bg: #FFFFFF;
            --text-color: #212121;
            --subtext-color: #666666;
            --border-color: #EEEEEE;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            padding-bottom: 30px;
        }

        header {
            background-color: var(--primary-color);
            color: white;
            text-align: center;
            padding: 25px 15px;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        header h1 {
            font-size: 1.8rem;
            margin-bottom: 5px;
        }

        header p {
            font-size: 0.9rem;
            opacity: 0.9;
        }

        .search-container {
            padding: 15px;
            max-width: 600px;
            margin: 0 auto;
        }

        .search-box {
            width: 100%;
            padding: 12px 20px;
            border: 2px solid var(--border-color);
            border-radius: 25px;
            font-size: 1rem;
            outline: none;
            transition: border-color 0.3s;
        }

        .search-box:focus {
            border-color: var(--primary-color);
        }

        .categories-container {
            display: flex;
            overflow-x: auto;
            padding: 10px 15px;
            gap: 10px;
            max-width: 800px;
            margin: 0 auto;
            scrollbar-width: none;
        }

        .categories-container::-webkit-scrollbar {
            display: none;
        }

        .cat-btn {
            background-color: white;
            border: 1px solid var(--border-color);
            padding: 8px 16px;
            border-radius: 20px;
            white-space: nowrap;
            cursor: pointer;
            font-weight: 600;
            color: var(--text-color);
            transition: all 0.3s ease;
        }

        .cat-btn.active, .cat-btn:hover {
            background-color: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
        }

        .menu-container {
            max-width: 800px;
            margin: 15px auto;
            padding: 0 15px;
        }

        .category-title {
            color: var(--primary-color);
            border-bottom: 2px solid var(--primary-color);
            padding-bottom: 5px;
            margin: 25px 0 15px 0;
            font-size: 1.3rem;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 15px;
        }

        .menu-card {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
            border: 1px solid var(--border-color);
        }

        .item-info h3 {
            font-size: 1rem;
            margin-bottom: 4px;
        }

        .item-info p {
            font-size: 0.85rem;
            color: var(--subtext-color);
        }

        .item-price {
            font-weight: bold;
            color: var(--primary-color);
            font-size: 1.05rem;
            white-space: nowrap;
            margin-left: 10px;
        }

        .no-result {
            text-align: center;
            padding: 40px;
            color: var(--subtext-color);
            display: none;
        }
    </style>
</head>
<body>

    <header>
        <h1>🍽️ MENU / ሜኑ</h1>
        <p>Delicious Food & Drinks / ጣፋጭ ምግቦች እና መጠጦች</p>
    </header>

    <div class="search-container">
        <input type="text" id="searchInput" class="search-box" placeholder="ምግብ ወይም መጠጥ ይፈልጉ / Search menu..." onkeyup="filterMenu()">
    </div>

    <div class="categories-container" id="categoryButtons">
        <button class="cat-btn active" onclick="filterCategory('all')">ሁሉም (All)</button>
        <button class="cat-btn" onclick="filterCategory('Breakfast')">ቁርስ (Breakfast)</button>
        <button class="cat-btn" onclick="filterCategory('SaladFruit')">ሰላጣ (Salad & Fruit)</button>
        <button class="cat-btn" onclick="filterCategory('Wrap')">ራፕ (Wrap)</button>
        <button class="cat-btn" onclick="filterCategory('Sandwich')">ሳንድዊች (Sandwich)</button>
        <button class="cat-btn" onclick="filterCategory('Burger')">በርገር (Burger)</button>
        <button class="cat-btn" onclick="filterCategory('Pizza')">ፒዛ (Pizza)</button>
        <button class="cat-btn" onclick="filterCategory('Juice')">ጁስ (Juice)</button>
        <button class="cat-btn" onclick="filterCategory('Shake')">ሼክ (Shake)</button>
        <button class="cat-btn" onclick="filterCategory('Mojito')">ሞሂቶ (Mojito)</button>
        <button class="cat-btn" onclick="filterCategory('IceOrder')">አይስ (Ice Order)</button>
        <button class="cat-btn" onclick="filterCategory('HotDrink')">የፍል መጠጥ (Hot Drink)</button>
        <button class="cat-btn" onclick="filterCategory('YogurtFrappe')">እርጎ & ፍራፑቺኖ</button>
        <button class="cat-btn" onclick="filterCategory('Extra')">ተጨማሪዎች (Extra)</button>
    </div>

    <div class="menu-container" id="menuContainer">
        <!-- Javascript የመረጃ ዝርዝሩን እዚህ ይጭነዋል -->
    </div>

    <div id="noResult" class="no-result">
        የፈለጉት ምግብ ወይም መጠጥ አልተገኘም።
    </div>

    <script>
        const menuData = [
            // Breakfast
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Avocado", am: "አቮካዶ", price: "350 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Avocado w/ Egg", am: "አቮካዶ ከእንቁላል ጋር", price: "370 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Waffle", am: "ዋፍል", price: "400 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Pancake", am: "ፓንኬክ", price: "400 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Chechebsa Normal", am: "ቸቸብሳ መደበኛ", price: "330 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Chechebsa Special", am: "ቸቸብሳ ስፔሻል", price: "400 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Avocado Toast", am: "አቮካዶ ቶስት", price: "320 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Special Fetira", am: "ስፔሻል ፈቲራ", price: "360 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Normal Fetira", am: "መደበኛ ፈቲራ", price: "260 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Omelet w/ Cheese", am: "ኡምሌት በቺዝ", price: "430 ETB" },
            { cat: "Breakfast", catName: "Breakfast / የቁርስ ምግቦች", en: "Normal Omelet", am: "መደበኛ ኡምሌት", price: "350 ETB" },

            // Salad / Fruit
            { cat: "SaladFruit", catName: "Salad & Fruit / ሰላጣ እና ፍራፍሬ", en: "Normal Salad", am: "መደበኛ ሰላጣ", price: "400 ETB" },
            { cat: "SaladFruit", catName: "Salad & Fruit / ሰላጣ እና ፍራፍሬ", en: "Special Salad", am: "ስፔሻል ሰላጣ", price: "590 ETB" },
            { cat: "SaladFruit", catName: "Salad & Fruit / ሰላጣ እና ፍራፍሬ", en: "Normal Fruit Punch", am: "መደበኛ ፍሩት ፓንች", price: "350 ETB" },
            { cat: "SaladFruit", catName: "Salad & Fruit / ሰላጣ እና ፍራፍሬ", en: "Special Fruit Punch", am: "ስፔሻል ፍሩት ፓንች", price: "450 ETB" },
            { cat: "SaladFruit", catName: "Salad & Fruit / ሰላጣ እና ፍራፍሬ", en: "Four in One", am: "ፎር ኢን ዋን (4 in 1)", price: "580 ETB" },
            { cat: "SaladFruit", catName: "Salad & Fruit / ሰላጣ እና ፍራፍሬ", en: "Waffle Fruit", am: "ዋፍል ፍሩት", price: "450 ETB" },

            // Wrap
            { cat: "Wrap", catName: "Wrap / ራፕ", en: "Chicken Wrap", am: "የዶሮ ራፕ", price: "620 ETB" },
            { cat: "Wrap", catName: "Wrap / ራፕ", en: "Beef Wrap", am: "የሬስ ራፕ", price: "570 ETB" },
            { cat: "Wrap", catName: "Wrap / ራፕ", en: "Veg Wrap", am: "የትክልት ራፕ", price: "450 ETB" },

            // Sandwich / Club
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Tuna Sandwich", am: "ቱና ሳንድዊች", price: "580 ETB" },
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Egg Sandwich", am: "የእንቁላል ሳንድዊች", price: "400 ETB" },
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Veg Sandwich", am: "የትክልት ሳንድዊች", price: "350 ETB" },
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Cheese Sandwich", am: "የቺዝ ሳንድዊች", price: "460 ETB" },
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Special Club", am: "ስፔሻል ክላብ", price: "620 ETB" },
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Beef Club", am: "የሬስ ክላብ", price: "550 ETB" },
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Chicken Club", am: "የዶሮ ክላብ", price: "590 ETB" },
            { cat: "Sandwich", catName: "Sandwich & Club / ሳንድዊች እና ክላብ", en: "Egg w/ Cheese", am: "እንቁላል ከቺዝ ጋር", price: "500 ETB" },

            // Burger
            { cat: "Burger", catName: "Burger / በርገር", en: "Special Double Burger", am: "ስፔሻል ዳብል በርገር", price: "800 ETB" },
            { cat: "Burger", catName: "Burger / በርገር", en: "Special Single Burger", am: "ስፔሻል ሲንግል በርገር", price: "680 ETB" },
            { cat: "Burger", catName: "Burger / በርገር", en: "Beef Burger", am: "የሬስ በርገር", price: "630 ETB" },
            { cat: "Burger", catName: "Burger / በርገር", en: "Cheese Burger", am: "ቺዝ በርገር", price: "650 ETB" },
            { cat: "Burger", catName: "Burger / በርገር", en: "Chicken Burger", am: "የዶሮ በርገር", price: "750 ETB" },

            // Pizza
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Tuna w/ Cheese Pizza", am: "ቱና በቺዝ ፒዛ", price: "770 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Margarita Pizza", am: "ማርጋሪታ ፒዛ", price: "700 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Meat Lover Pizza", am: "ሚት ላቨር ፒዛ", price: "770 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Special Pizza", am: "ስፔሻል ፒዛ", price: "920 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Chicken Pizza", am: "የዶሮ ፒዛ", price: "890 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Veg Pizza", am: "የትክልት ፒዛ", price: "550 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Tuna w/ Veg Pizza", am: "ቱና ከትክልት ጋር ፒዛ", price: "690 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Fasting Tuna Pizza", am: "የጾም ቱና ፒዛ", price: "650 ETB" },
            { cat: "Pizza", catName: "Pizza / ፒዛ", en: "Family Pizza", am: "ፋሚሊ ፒዛ", price: "1470 ETB" },

            // Juice
            { cat: "Juice", catName: "Juice / ጁስ", en: "Avocado Mix", am: "አቮካዶ ሚክስ", price: "M: 310 | L: 360 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Avocado", am: "አቮካዶ", price: "M: 330 | L: 370 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Mango", am: "ማንጎ", price: "M: 320 | L: 350 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Strawberry", am: "ስትሮበሪ", price: "M: 300 | L: 350 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Papaya", am: "ፓፓያ", price: "M: 250 | L: 270 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Pineapple", am: "አናናስ", price: "M: 270 | L: 300 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Watermelon", am: "ሀብሀብ", price: "M: 270 | L: 300 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Mix", am: "ሚክስ", price: "M: 250 | L: 290 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Flaxseed", am: "ተልባ", price: "M: 270 | L: 300 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Sugarcane", am: "አገዳ", price: "M: 220 | L: 240 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Lemon", am: "ሎሚ", price: "M: 220 | L: 240 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Carrot", am: "ካሮት", price: "M: 220 | L: 240 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Ginger", am: "ዝንጅብል", price: "M: 230 | L: 250 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Mango Mix", am: "ማንጎ ሚክስ", price: "M: 300 | L: 340 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Strawberry Mix", am: "ስትሮበሪ ሚክስ", price: "M: 300 | L: 340 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Orange Mix", am: "ብርቱካን ሚክስ", price: "M: 300 | L: 340 ETB" },
            { cat: "Juice", catName: "Juice / ጁስ", en: "Oat Juice", am: "የኦት (አጃ) ጁስ", price: "250 ETB" },

            // Shake
            { cat: "Shake", catName: "Shake / ሼክ", en: "Special Shake", am: "ስፔሻል ሼክ", price: "M: 300 | L: 350 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Mango Shake", am: "ማንጎ ሼክ", price: "M: 350 | L: 380 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Avocado Shake", am: "አቮካዶ ሼክ", price: "M: 350 | L: 380 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Papaya Shake", am: "ፓፓያ ሼክ", price: "M: 260 | L: 280 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Watermelon Shake", am: "ሀብሀብ ሼክ", price: "M: 260 | L: 280 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Banana Shake", am: "ሙዝ ሼክ", price: "M: 260 | L: 280 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Sugarcane Shake", am: "አገዳ ሼክ", price: "M: 260 | L: 290 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Strawberry Shake", am: "ስትሮበሪ ሼክ", price: "M: 260 | L: 380 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Chocolate Shake", am: "ቸኮሌት ሼክ", price: "420 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Oreo Shake", am: "ኦሪዮ ሼክ", price: "410 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Vanilla Shake", am: "ቫኒላ ሼክ", price: "350 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Mix Shake", am: "ሚክስ ሼክ", price: "340 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Protein Shake", am: "ፕሮቲን ሼክ", price: "480 ETB" },
            { cat: "Shake", catName: "Shake / ሼክ", en: "Family Shake", am: "ፋሚሊ ሼክ", price: "690 ETB" },

            // Mojito
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Strawberry Mojito", am: "ስትሮበሪ ሞሂቶ", price: "295 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Orange Mojito", am: "ብርቱካን ሞሂቶ", price: "295 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Kiwi Mojito", am: "ኪዊ ሞሂቶ", price: "295 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Lemon Mojito", am: "ሎሚ ሞሂቶ", price: "295 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Chocolate Mojito", am: "ቸኮሌት ሞሂቶ", price: "295 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Pineapple Mojito", am: "አናናስ ሞሂቶ", price: "300 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Special Mojito", am: "ስፔሻል ሞሂቶ", price: "300 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Avatar Mojito", am: "አቫታር ሞሂቶ", price: "300 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "King Mojito", am: "ኪንግ ሞሂቶ", price: "295 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Sky Mojito", am: "ስካይ ሞሂቶ", price: "295 ETB" },
            { cat: "Mojito", catName: "Mojito / ሞሂቶ", en: "Snuzzy Mojito", am: "ስነዚ ሞሂቶ", price: "295 ETB" },

            // Ice Order
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Iced Tea", am: "አይስ ቲ", price: "120 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Ice Latte", am: "አይስ ላቴ", price: "230 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Iced Caramel", am: "አይስ ካራሜል", price: "210 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Iced Mocha", am: "አይስ ሞካ", price: "230 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Iced Strawberry", am: "አይስ ስትሮበሪ", price: "180 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Iced Chocolate", am: "አይስ ቸኮሌት", price: "230 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Lemonade", am: "ለሞኔድ", price: "180 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Strawberry w/ Chocolate", am: "ስትሮበሪ በቸኮሌት", price: "260 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Caramel Ice Latte", am: "ካራሜል አይስ ላቴ", price: "260 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Caramel Ice Coffee", am: "ካራሜል አይስ ኮፊ", price: "280 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Ice Coffee", am: "አይስ ኮፊ", price: "240 ETB" },
            { cat: "IceOrder", catName: "Ice Drinks / የቀዝቃዛ መጠጦች", en: "Mixed Ice Latte", am: "ሚክስድ አይስ ላቴ", price: "350 ETB" },

            // Hot Drink
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Tea", am: "ሻይ", price: "70 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Coffee", am: "ቡና", price: "140 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Macchiato", am: "ማኪያቶ", price: "150 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Spice", am: "ስፓይስ", price: "90 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Espresso", am: "ኤስፕሬሶ", price: "150 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Ginger Tea", am: "የዝንጅብል ሻይ", price: "90 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Cappuccino", am: "ካፑቺኖ", price: "150 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Latte", am: "ላቴ", price: "140 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Milk", am: "ወተት", price: "140 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Hot Chocolate", am: "ሆት ቸኮሌት", price: "150 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Special Tea", am: "ስፔሻል ሻይ", price: "150 ETB" },
            { cat: "HotDrink", catName: "Hot Drinks / የፍል መጠጦች", en: "Mocha", am: "ሞካ", price: "130 ETB" },

            // Yogurt & Frappuccino
            { cat: "YogurtFrappe", catName: "Yogurt & Frappuccino", en: "Caramel Yogurt", am: "ካራሜል እርጎ", price: "310 ETB" },
            { cat: "YogurtFrappe", catName: "Yogurt & Frappuccino", en: "Fruit Yogurt", am: "የፍራፍሬ እርጎ", price: "310 ETB" },
            { cat: "YogurtFrappe", catName: "Yogurt & Frappuccino", en: "Flavored Yogurt", am: "ፍሌቨርድ እርጎ", price: "310 ETB" },
            { cat: "YogurtFrappe", catName: "Yogurt & Frappuccino", en: "Strawberry Yogurt", am: "ስትሮበሪ እርጎ", price: "310 ETB" },
            { cat: "YogurtFrappe", catName: "Yogurt & Frappuccino", en: "Chocolate Frappuccino", am: "ቸኮሌት ፍራፑቺኖ", price: "380 ETB" },
            { cat: "YogurtFrappe", catName: "Yogurt & Frappuccino", en: "Caramel Frappuccino", am: "ካራሜል ፍራፑቺኖ", price: "330 ETB" },
            { cat: "YogurtFrappe", catName: "Yogurt & Frappuccino", en: "Mocha Frappuccino", am: "ሞካ ፍራፑቺኖ", price: "350 ETB" },

            // Extras
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Extra Cheese", am: "ተጨማሪ ቺዝ", price: "80 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Extra Bread", am: "ተጨማሪ ዳቦ", price: "40 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Extra Egg", am: "ተጨማሪ እንቁላል", price: "45 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Extra Mayonnaise", am: "ተጨማሪ ማዮኔዝ", price: "80 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Extra Tuna 1/2", am: "ተጨማሪ ቱና (ግማሽ)", price: "150 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Extra Tuna", am: "ተጨማሪ ቱና", price: "270 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Juice Cup", am: "የጁስ ኮፕ", price: "25 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Coffee Cup", am: "የቡና ኮፕ", price: "20 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Burger Box", am: "የበርገር ሳጥን", price: "50 ETB" },
            { cat: "Extra", catName: "Extras & Packaging / ተጨማሪዎች", en: "Pizza Box", am: "የፒዛ ሳጥን", price: "85 ETB" }
        ];

        let currentCategory = 'all';

        function renderMenu(items) {
            const container = document.getElementById('menuContainer');
            const noResult = document.getElementById('noResult');
            container.innerHTML = '';

            if (items.length === 0) {
                noResult.style.display = 'block';
                return;
            } else {
                noResult.style.display = 'none';
            }

            // Group by category
            const grouped = {};
            items.forEach(item => {
                if (!grouped[item.catName]) {
                    grouped[item.catName] = [];
                }
                grouped[item.catName].push(item);
            });

            for (const [catName, list] of Object.entries(grouped)) {
                const catTitle = document.createElement('h2');
                catTitle.className = 'category-title';
                catTitle.innerText = catName;
                container.appendChild(catTitle);

                const grid = document.createElement('div');
                grid.className = 'menu-grid';

                list.forEach(item => {
                    const card = document.createElement('div');
                    card.className = 'menu-card';
                    card.innerHTML = `
                        <div class="item-info">
                            <h3>${item.en}</h3>
                            <p>${item.am}</p>
                        </div>
                        <div class="item-price">${item.price}</div>
                    `;
                    grid.appendChild(card);
                });

                container.appendChild(grid);
            }
        }

        function filterCategory(category) {
            currentCategory = category;
            
            // Active button style
            const buttons = document.querySelectorAll('.cat-btn');
            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            document.getElementById('searchInput').value = '';
            
            if (category === 'all') {
                renderMenu(menuData);
            } else {
                const filtered = menuData.filter(item => item.cat === category);
                renderMenu(filtered);
            }
        }

        function filterMenu() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = menuData.filter(item => {
                const matchCat = (currentCategory === 'all' || item.cat === currentCategory);
                const matchQuery = item.en.toLowerCase().includes(query) || item.am.toLowerCase().includes(query);
                return matchCat && matchQuery;
            });
            renderMenu(filtered);
        }

        // Initial render
        renderMenu(menuData);
    </script>
</body>
</html>
