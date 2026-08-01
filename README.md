<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Eroshake Juice - Digital Menu</title>
  <!-- Google Fonts & FontAwesome Icons -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Noto+Sans+Ethiopic:wght@400;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

  <style>
    :root {
      --primary: #1e88e5;
      --primary-dark: #1565c0;
      --accent: #00d2ff;
      --bg: #f4f8fb;
      --card-bg: #ffffff;
      --text: #1e293b;
      --text-muted: #64748b;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Poppins', 'Noto Sans Ethiopic', sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      padding-bottom: 30px;
    }

    /* Header */
    header {
      background: linear-gradient(135deg, var(--primary-dark), var(--primary));
      color: white;
      padding: 20px 15px;
      text-align: center;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 4px 15px rgba(30, 136, 229, 0.3);
    }

    .header-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 800px;
      margin: 0 auto 15px auto;
    }

    .brand-title {
      font-size: 1.5rem;
      font-weight: 700;
      letter-spacing: 0.5px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .lang-btn {
      background: rgba(255, 255, 255, 0.2);
      border: 1px solid rgba(255, 255, 255, 0.4);
      color: white;
      padding: 6px 14px;
      border-radius: 20px;
      cursor: pointer;
      font-weight: 600;
      font-size: 0.85rem;
      transition: all 0.3s ease;
    }

    .lang-btn:hover {
      background: white;
      color: var(--primary-dark);
    }

    /* Search Box */
    .search-box {
      max-width: 800px;
      margin: 0 auto;
      position: relative;
    }

    .search-box input {
      width: 100%;
      padding: 12px 45px 12px 18px;
      border-radius: 25px;
      border: none;
      font-size: 0.95rem;
      outline: none;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }

    .search-box i {
      position: absolute;
      right: 15px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--primary);
      font-size: 1.1rem;
    }

    /* Category Navigation Bar */
    .categories-wrapper {
      background: white;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
      position: sticky;
      top: 115px;
      z-index: 99;
    }

    .categories-nav {
      display: flex;
      overflow-x: auto;
      padding: 12px 15px;
      gap: 10px;
      max-width: 800px;
      margin: 0 auto;
      scrollbar-width: none;
    }

    .categories-nav::-webkit-scrollbar {
      display: none;
    }

    .cat-pill {
      white-space: nowrap;
      padding: 8px 16px;
      border-radius: 20px;
      background: #e3f2fd;
      color: var(--primary-dark);
      font-weight: 600;
      font-size: 0.85rem;
      border: none;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .cat-pill.active {
      background: var(--primary);
      color: white;
      box-shadow: 0 3px 8px rgba(30, 136, 229, 0.4);
    }

    /* Main Container */
    .container {
      max-width: 800px;
      margin: 20px auto;
      padding: 0 15px;
    }

    /* Menu Grid */
    .menu-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
      gap: 15px;
    }

    @media (min-width: 500px) {
      .menu-grid {
        grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      }
    }

    /* Card Styling */
    .card {
      background: var(--card-bg);
      border-radius: 15px;
      overflow: hidden;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.04);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      border: 1px solid #e2e8f0;
      transition: transform 0.2s ease;
    }

    .card:active {
      transform: scale(0.98);
    }

    .card-img-container {
      width: 100%;
      height: 130px;
      background: #e2e8f0;
      overflow: hidden;
      position: relative;
    }

    .card-img-container img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .card-body {
      padding: 12px;
      display: flex;
      flex-direction: column;
      flex-grow: 1;
      justify-content: space-between;
    }

    .card-title {
      font-size: 0.95rem;
      font-weight: 600;
      color: var(--text);
      margin-bottom: 8px;
    }

    .card-price {
      font-size: 0.9rem;
      font-weight: 700;
      color: var(--primary-dark);
      background: #e3f2fd;
      padding: 4px 8px;
      border-radius: 8px;
      display: inline-block;
      width: max-content;
    }

    .no-results {
      text-align: center;
      padding: 40px 20px;
      color: var(--text-muted);
      grid-column: 1 / -1;
    }
  </style>
</head>
<body>

  <!-- Header Section -->
  <header>
    <div class="header-top">
      <div class="brand-title">
        <i class="fa-solid fa-glass-water"></i> Eroshake Juice
      </div>
      <button class="lang-btn" id="langBtn" onclick="toggleLanguage()">አማርኛ</button>
    </div>
    <div class="search-box">
      <input type="text" id="searchInput" placeholder="Search menu..." oninput="filterMenu()">
      <i class="fa-solid fa-magnifying-glass"></i>
    </div>
  </header>

  <!-- Navigation Bar -->
  <div class="categories-wrapper">
    <div class="categories-nav" id="categoryNav">
      <!-- Generated Dynamically -->
    </div>
  </div>

  <!-- Main Items Container -->
  <div class="container">
    <div class="menu-grid" id="menuGrid">
      <!-- Menu Items Generated Dynamically -->
    </div>
  </div>

  <script>
    // Language State ('en' for English, 'am' for Amharic) - Defaults to English
    let currentLang = 'en';
    let currentCategory = 'all';

    // Categories Data
    const categories = [
      { id: 'all', en: 'All Items', am: 'ሁሉም' },
      { id: 'breakfast', en: 'Breakfast', am: 'ቁርስ' },
      { id: 'salad', en: 'Salad / Fruit', am: 'ሰላጣ / ፍራፍሬ' },
      { id: 'wrap', en: 'Wrap', am: 'ራፕ' },
      { id: 'sandwich', en: 'Sandwich / Club', am: 'ሳንድዊች' },
      { id: 'burger', en: 'Burger', am: 'በርገር' },
      { id: 'pizza', en: 'Pizza', am: 'ፒዛ' },
      { id: 'extra', en: 'Extra', am: 'ተጨማሪ' },
      { id: 'juice', en: 'Juice', am: 'ጁስ' },
      { id: 'shake', en: 'Shake', am: 'ሼክ' },
      { id: 'milkshake', en: 'Milk Shake', am: 'ሚልካ ሼክ' },
      { id: 'mojito', en: 'Mojito', am: 'ሞሂቶ' },
      { id: 'iceorder', en: 'Ice Order', am: 'ቀዝቃዛ መጠጥ' },
      { id: 'hotdrink', en: 'Hot Drink', am: 'የሞቀ መጠጥ' },
      { id: 'yogurt', en: 'Yogurt', am: 'እርጎ' },
      { id: 'frappuccino', en: 'Frappuccino', am: 'ፍራፑቺኖ' },
      { id: 'other', en: 'Other', am: 'ሌሎች' }
    ];

    // Complete Menu Database with Relevant Images
    const menuData = [
      // BREAKFAST
      { cat: 'breakfast', en: 'Avocado', am: 'አቮካዶ', price: '350 ETB', img: 'https://images.unsplash.com/photo-1523049673857-eb18f1d7b578?w=400' },
      { cat: 'breakfast', en: 'Avocado w/ Egg', am: 'አቮካዶ በዕንዱላል', price: '370 ETB', img: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=400' },
      { cat: 'breakfast', en: 'Waffle', am: 'ዋፍል', price: '400 ETB', img: 'https://images.unsplash.com/photo-1562376552-0d160a2f238d?w=400' },
      { cat: 'breakfast', en: 'Pancake', am: 'ፓንኬክ', price: '400 ETB', img: 'https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=400' },
      { cat: 'breakfast', en: 'Chechebsa Normal', am: 'ጨጨብሳ መደበኛ', price: '330 ETB', img: 'https://images.unsplash.com/photo-1589301760014-d929f3979dbc?w=400' },
      { cat: 'breakfast', en: 'Chechebsa Special', am: 'ጨጨብሳ ስፔሻል', price: '400 ETB', img: 'https://images.unsplash.com/photo-1589301760014-d929f3979dbc?w=400' },
      { cat: 'breakfast', en: 'Avocado Toast', am: 'አቮካዶ ቶስት', price: '320 ETB', img: 'https://images.unsplash.com/photo-1588137378633-dea1336ce1e2?w=400' },
      { cat: 'breakfast', en: 'Special Fetira', am: 'ስፔሻል ፈቲራ', price: '360 ETB', img: 'https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?w=400' },
      { cat: 'breakfast', en: 'Normal Fetira', am: 'መደበኛ ፈቲራ', price: '260 ETB', img: 'https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?w=400' },
      { cat: 'breakfast', en: 'Omelet w/ Cheese', am: 'እንቁላል በቺዝ', price: '430 ETB', img: 'https://images.unsplash.com/photo-1510693206972-df098062cb71?w=400' },
      { cat: 'breakfast', en: 'Normal Omelet', am: 'መደበኛ እንቁላል', price: '350 ETB', img: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=400' },

      // SALAD / FRUIT
      { cat: 'salad', en: 'Normal Salad', am: 'መደበኛ ሰላጣ', price: '400 ETB', img: 'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=400' },
      { cat: 'salad', en: 'Special Salad', am: 'ስፔሻል ሰላጣ', price: '590 ETB', img: 'https://images.unsplash.com/photo-1540420773420-3366772f4999?w=400' },
      { cat: 'salad', en: 'Normal Fruit Punch', am: 'መደበኛ ፍሩት ፓንች', price: '350 ETB', img: 'https://images.unsplash.com/photo-1490474418585-ba9bad8fd0ea?w=400' },
      { cat: 'salad', en: 'Special Fruit Punch', am: 'ስፔሻል ፍሩት ፓንች', price: '450 ETB', img: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=400' },
      { cat: 'salad', en: 'Four in One', am: 'ፎር ኢን ዋን', price: '580 ETB', img: 'https://images.unsplash.com/photo-1615485290382-441e4d049cb5?w=400' },
      { cat: 'salad', en: 'Waffle Fruit', am: 'ዋፍል ፍሩት', price: '450 ETB', img: 'https://images.unsplash.com/photo-1509440159596-0249088772ff?w=400' },

      // WRAP
      { cat: 'wrap', en: 'Chicken Wrap', am: 'ዶሮ ራፕ', price: '620 ETB', img: 'https://images.unsplash.com/photo-1626700051175-6818013e1d4f?w=400' },
      { cat: 'wrap', en: 'Beef Wrap', am: 'የበሬ ሥጋ ራፕ', price: '570 ETB', img: 'https://images.unsplash.com/photo-1565299585323-38d6b0865b47?w=400' },
      { cat: 'wrap', en: 'Veg Wrap', am: 'የአትክልት ራፕ', price: '450 ETB', img: 'https://images.unsplash.com/photo-1509722747041-616f39b57569?w=400' },

      // SANDWICH / CLUB
      { cat: 'sandwich', en: 'Tuna Sandwich', am: 'ቱና ሳንድዊች', price: '580 ETB', img: 'https://images.unsplash.com/photo-1509722747041-616f39b57569?w=400' },
      { cat: 'sandwich', en: 'Egg Sandwich', am: 'እንቁላል ሳንድዊች', price: '400 ETB', img: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=400' },
      { cat: 'sandwich', en: 'Veg Sandwich', am: 'የአትክልት ሳንድዊች', price: '350 ETB', img: 'https://images.unsplash.com/photo-1539252554453-80ab65ce3586?w=400' },
      { cat: 'sandwich', en: 'Cheese Sandwich', am: 'ቺዝ ሳንድዊች', price: '460 ETB', img: 'https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=400' },
      { cat: 'sandwich', en: 'Special Club', am: 'ስፔሻል ክለብ', price: '620 ETB', img: 'https://images.unsplash.com/photo-1567234669003-dce7a7a88821?w=400' },
      { cat: 'sandwich', en: 'Beef Club', am: 'ቢፍ ክለብ', price: '550 ETB', img: 'https://images.unsplash.com/photo-1550547660-d9450f859349?w=400' },
      { cat: 'sandwich', en: 'Chicken Club', am: 'ቺከን ክለብ', price: '590 ETB', img: 'https://images.unsplash.com/photo-1603064752734-4c48eff53d05?w=400' },
      { cat: 'sandwich', en: 'Egg w/ Cheese', am: 'እንቁላል በቺዝ', price: '500 ETB', img: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=400' },

      // BURGER
      { cat: 'burger', en: 'Special Double Burger', am: 'ስፔሻል ድርብ በርገር', price: '800 ETB', img: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=400' },
      { cat: 'burger', en: 'Special Single Burger', am: 'ስፔሻል ነጠላ በርገር', price: '680 ETB', img: 'https://images.unsplash.com/photo-1586190848861-99aa4a171e90?w=400' },
      { cat: 'burger', en: 'Beef Burger', am: 'ቢፍ በርገር', price: '630 ETB', img: 'https://images.unsplash.com/photo-1550547660-d9450f859349?w=400' },
      { cat: 'burger', en: 'Cheese Burger', am: 'ቺዝ በርገር', price: '650 ETB', img: 'https://images.unsplash.com/photo-1572802419224-296b0aeee0d9?w=400' },
      { cat: 'burger', en: 'Chicken Burger', am: 'ቺከን በርገር', price: '750 ETB', img: 'https://images.unsplash.com/photo-1615297928064-24977384d0da?w=400' },

      // PIZZA
      { cat: 'pizza', en: 'Tuna w/ Cheese Pizza', am: 'ቱና በቺዝ ፒዛ', price: '770 ETB', img: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=400' },
      { cat: 'pizza', en: 'Margarita Pizza', am: 'ማርጋሪታ ፒዛ', price: '700 ETB', img: 'https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=400' },
      { cat: 'pizza', en: 'Meat Lover Pizza', am: 'ሜት ላቨር ፒዛ', price: '770 ETB', img: 'https://images.unsplash.com/photo-1534308983496-4fabb1a015ee?w=400' },
      { cat: 'pizza', en: 'Special Pizza', am: 'ስፔሻል ፒዛ', price: '920 ETB', img: 'https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=400' },
      { cat: 'pizza', en: 'Chicken Pizza', am: 'ቺከን ፒዛ', price: '890 ETB', img: 'https://images.unsplash.com/photo-1571407970349-bc81e7e96d47?w=400' },
      { cat: 'pizza', en: 'Veg Pizza', am: 'የአትክልት ፒዛ', price: '550 ETB', img: 'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=400' },
      { cat: 'pizza', en: 'Tuna w/ Veg Pizza', am: 'ቱና በአትክልት ፒዛ', price: '690 ETB', img: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=400' },
      { cat: 'pizza', en: 'Fasting Tuna Pizza', am: 'የጾም ቱና ፒዛ', price: '650 ETB', img: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=400' },
      { cat: 'pizza', en: 'Family Pizza', am: 'ፋሚሊ ፒዛ', price: '1470 ETB', img: 'https://images.unsplash.com/photo-1590947132387-155cc02f3212?w=400' },

      // EXTRA
      { cat: 'extra', en: 'Extra Cheese', am: 'ተጨማሪ ቺዝ', price: '80 ETB', img: 'https://images.unsplash.com/photo-1486297678162-eb2a19b0a32d?w=400' },
      { cat: 'extra', en: 'Extra Bread', am: 'ተጨማሪ ዳቦ', price: '40 ETB', img: 'https://images.unsplash.com/photo-1509440159596-0249088772ff?w=400' },
      { cat: 'extra', en: 'Extra Egg', am: 'ተጨማሪ እንቁላል', price: '45 ETB', img: 'https://images.unsplash.com/photo-1518569656558-1f25e69d93d7?w=400' },
      { cat: 'extra', en: 'Extra Mayonnaise', am: 'ተጨማሪ ማዮኔዝ', price: '80 ETB', img: 'https://images.unsplash.com/photo-1585238342024-78d387f4a707?w=400' },
      { cat: 'extra', en: 'Juice Cup', am: 'የጁስ ብርጭቆ', price: '25 ETB', img: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=400' },
      { cat: 'extra', en: 'Burger Box', am: 'የበርገር ሳጥን', price: '50 ETB', img: 'https://images.unsplash.com/photo-1525610553991-2bede1a236e2?w=400' },
      { cat: 'extra', en: 'Pizza Box', am: 'የፒዛ ሳጥን', price: '85 ETB', img: 'https://images.unsplash.com/photo-1590947132387-155cc02f3212?w=400' },
      { cat: 'extra', en: 'Extra Tuna 1/2', am: 'ተጨማሪ ቱና 1/2', price: '150 ETB', img: 'https://images.unsplash.com/photo-1534422298391-e4f8c172dddb?w=400' },
      { cat: 'extra', en: 'Extra Tuna', am: 'ተጨማሪ ቱና ሙሉ', price: '270 ETB', img: 'https://images.unsplash.com/photo-1534422298391-e4f8c172dddb?w=400' },
      { cat: 'extra', en: 'Coffee Cup', am: 'የቡና ብርጭቆ', price: '20 ETB', img: 'https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?w=400' },

      // JUICE
      { cat: 'juice', en: 'Avocado Mix', am: 'አቮካዶ ሚክስ', price: 'M: 310 | L: 360', img: 'https://images.unsplash.com/photo-1523049673857-eb18f1d7b578?w=400' },
      { cat: 'juice', en: 'Avocado', am: 'አቮካዶ ጁስ', price: 'M: 330 | L: 370', img: 'https://images.unsplash.com/photo-1523049673857-eb18f1d7b578?w=400' },
      { cat: 'juice', en: 'Mango', am: 'ማንጎ ጁስ', price: 'M: 320 | L: 350', img: 'https://images.unsplash.com/photo-1553279768-865429fa0078?w=400' },
      { cat: 'juice', en: 'Strawberry', am: 'ስትሮበሪ ጁስ', price: 'M: 300 | L: 350', img: 'https://images.unsplash.com/photo-1568827999250-3f658b10883d?w=400' },
      { cat: 'juice', en: 'Papaya', am: 'ፓፓያ ጁስ', price: 'M: 250 | L: 270', img: 'https://images.unsplash.com/photo-1517256064527-09c73fc73e38?w=400' },
      { cat: 'juice', en: 'Pineapple', am: 'አናናስ ጁስ', price: 'M: 270 | L: 300', img: 'https://images.unsplash.com/photo-1550258987-190a2d41a8ba?w=400' },
      { cat: 'juice', en: 'Watermelon', am: 'ሀብሀብ ጁስ', price: 'M: 270 | L: 300', img: 'https://images.unsplash.com/photo-1587049352846-4a222e784d38?w=400' },
      { cat: 'juice', en: 'Mix Juice', am: 'ሚክስ ጁስ', price: 'M: 250 | L: 290', img: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=400' },
      { cat: 'juice', en: 'Flaxseed', am: 'የተልባ ጁስ', price: 'M: 270 | L: 300', img: 'https://images.unsplash.com/photo-1505252585461-04db1eb84625?w=400' },
      { cat: 'juice', en: 'Sugarcane', am: 'የሸንኮራ አገዳ ጁስ', price: 'M: 220 | L: 240', img: 'https://images.unsplash.com/photo-1600271886742-f049cd451bba?w=400' },
      { cat: 'juice', en: 'Lemon', am: 'ሎሚ ጁስ', price: 'M: 220 | L: 240', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'juice', en: 'Carrot', am: 'ካሮት ጁስ', price: 'M: 220 | L: 240', img: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=400' },
      { cat: 'juice', en: 'Ginger', am: 'ዝንጅብል ጁስ', price: 'M: 230 | L: 250', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'juice', en: 'Mango Mix', am: 'ማንጎ ሚክስ', price: 'M: 300 | L: 340', img: 'https://images.unsplash.com/photo-1553279768-865429fa0078?w=400' },
      { cat: 'juice', en: 'Strawberry Mix', am: 'ስትሮበሪ ሚክስ', price: 'M: 300 | L: 340', img: 'https://images.unsplash.com/photo-1568827999250-3f658b10883d?w=400' },
      { cat: 'juice', en: 'Orange Mix', am: 'ብርትኳን ሚክስ', price: 'M: 300 | L: 340', img: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=400' },

      // SHAKE
      { cat: 'shake', en: 'Special Shake', am: 'ስፔሻል ሼክ', price: 'M: 300 | L: 350', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'shake', en: 'Mango Shake', am: 'ማንጎ ሼክ', price: 'M: 350 | L: 380', img: 'https://images.unsplash.com/photo-1553279768-865429fa0078?w=400' },
      { cat: 'shake', en: 'Avocado Shake', am: 'አቮካዶ ሼክ', price: 'M: 350 | L: 380', img: 'https://images.unsplash.com/photo-1523049673857-eb18f1d7b578?w=400' },
      { cat: 'shake', en: 'Papaya Shake', am: 'ፓፓያ ሼክ', price: 'M: 260 | L: 280', img: 'https://images.unsplash.com/photo-1517256064527-09c73fc73e38?w=400' },
      { cat: 'shake', en: 'Watermelon Shake', am: 'ሀብሀብ ሼክ', price: 'M: 260 | L: 280', img: 'https://images.unsplash.com/photo-1587049352846-4a222e784d38?w=400' },
      { cat: 'shake', en: 'Banana Shake', am: 'ሙዝ ሼክ', price: 'M: 260 | L: 280', img: 'https://images.unsplash.com/photo-1528825871115-3581a5387919?w=400' },
      { cat: 'shake', en: 'Sugarcane Shake', am: 'የሸንኮራ ሼክ', price: 'M: 260 | L: 290', img: 'https://images.unsplash.com/photo-1600271886742-f049cd451bba?w=400' },
      { cat: 'shake', en: 'Strawberry Shake', am: 'ስትሮበሪ ሼክ', price: 'M: 260 | L: 380', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },

      // MILK SHAKE
      { cat: 'milkshake', en: 'Chocolate Shake', am: 'ቸኮሌት ሼክ', price: '420 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'milkshake', en: 'Oreo Shake', am: 'ኦሪዮ ሼክ', price: '410 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'milkshake', en: 'Vanilla Shake', am: 'ቫኒላ ሼክ', price: '350 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'milkshake', en: 'Mix Shake', am: 'ሚክስ ሼክ', price: '340 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'milkshake', en: 'Protein Shake', am: 'ፕሮቲን ሼክ', price: '480 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'milkshake', en: 'Family Shake', am: 'ፋሚሊ ሼክ', price: '690 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },

      // MOJITO
      { cat: 'mojito', en: 'Strawberry Mojito', am: 'ስትሮበሪ ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Orange Mojito', am: 'ብርትኳን ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Kiwi Mojito', am: 'ኪዊ ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Lemon Mojito', am: 'ሎሚ ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Chocolate Mojito', am: 'ቸኮሌት ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Pineapple Mojito', am: 'አናናስ ሞሂቶ', price: '300 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Special Mojito', am: 'ስፔሻል ሞሂቶ', price: '300 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Avatar Mojito', am: 'አቫታር ሞሂቶ', price: '300 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'King Mojito', am: 'ኪንግ ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Sky Mojito', am: 'ስካይ ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'mojito', en: 'Snuzzy Mojito', am: 'ስነዚ ሞሂቶ', price: '295 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },

      // ICE ORDER
      { cat: 'iceorder', en: 'Iced Tea', am: 'አይስ ቲ', price: '120 ETB', img: 'https://images.unsplash.com/photo-1517256064527-09c73fc73e38?w=400' },
      { cat: 'iceorder', en: 'Ice Latte', am: 'አይስ ላቴ', price: '230 ETB', img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400' },
      { cat: 'iceorder', en: 'Iced Caramel', am: 'አይስ ካራሜል', price: '210 ETB', img: 'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400' },
      { cat: 'iceorder', en: 'Iced Mocha', am: 'አይስ ሞካ', price: '230 ETB', img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400' },
      { cat: 'iceorder', en: 'Iced Strawberry', am: 'አይስ ስትሮበሪ', price: '180 ETB', img: 'https://images.unsplash.com/photo-1568827999250-3f658b10883d?w=400' },
      { cat: 'iceorder', en: 'Iced Chocolate', am: 'አይስ ቸኮሌት', price: '230 ETB', img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400' },
      { cat: 'iceorder', en: 'Lemonade', am: 'ሌሞኔድ', price: '180 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'iceorder', en: 'Strawberry w/ Chocolate', am: 'ስትሮበሪ በቸኮሌት', price: '260 ETB', img: 'https://images.unsplash.com/photo-1568827999250-3f658b10883d?w=400' },
      { cat: 'iceorder', en: 'Caramel Ice Latte', am: 'ካራሜል አይስ ላቴ', price: '260 ETB', img: 'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400' },
      { cat: 'iceorder', en: 'Caramel Ice Coffee', am: 'ካራሜል አይስ ቡና', price: '280 ETB', img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400' },
      { cat: 'iceorder', en: 'Ice Coffee', am: 'አይስ ቡና', price: '240 ETB', img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400' },
      { cat: 'iceorder', en: 'Mixed Ice Latte', am: 'ሚክስድ አይስ ላቴ', price: '350 ETB', img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400' },

      // HOT DRINK
      { cat: 'hotdrink', en: 'Tea', am: 'ሻይ', price: '70 ETB', img: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=400' },
      { cat: 'hotdrink', en: 'Coffee', am: 'ቡና', price: '140 ETB', img: 'https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?w=400' },
      { cat: 'hotdrink', en: 'Macchiato', am: 'ማኪያቶ', price: '150 ETB', img: 'https://images.unsplash.com/photo-1485808191679-5f86510681a2?w=400' },
      { cat: 'hotdrink', en: 'Spice Tea', am: 'የቀመም ሻይ', price: '90 ETB', img: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=400' },
      { cat: 'hotdrink', en: 'Espresso', am: 'ኤስፕሬሶ', price: '150 ETB', img: 'https://images.unsplash.com/photo-1510591509098-f4fdc6d0ff04?w=400' },
      { cat: 'hotdrink', en: 'Ginger Tea', am: 'የዝንጅብል ሻይ', price: '90 ETB', img: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=400' },
      { cat: 'hotdrink', en: 'Cappuccino', am: 'ካፑቺኖ', price: '150 ETB', img: 'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400' },
      { cat: 'hotdrink', en: 'Latte', am: 'ላቴ', price: '140 ETB', img: 'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400' },
      { cat: 'hotdrink', en: 'Milk', am: 'ወተት', price: '140 ETB', img: 'https://images.unsplash.com/photo-1550583724-b2692b85b150?w=400' },
      { cat: 'hotdrink', en: 'Normal Tea', am: 'መደበኛ ሻይ', price: '60 ETB', img: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=400' },
      { cat: 'hotdrink', en: 'Hot Chocolate', am: 'ሆት ቸኮሌት', price: '150 ETB', img: 'https://images.unsplash.com/photo-1542990253-0d0f5be5f0ed?w=400' },
      { cat: 'hotdrink', en: 'Special Tea', am: 'ስፔሻል ሻይ', price: '150 ETB', img: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=400' },
      { cat: 'hotdrink', en: 'Mocha', am: 'ሞካ', price: '130 ETB', img: 'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400' },

      // YOGURT
      { cat: 'yogurt', en: 'Caramel Yogurt', am: 'ካራሜል እርጎ', price: '310 ETB', img: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=400' },
      { cat: 'yogurt', en: 'Fruit Yogurt', am: 'የፍራፍሬ እርጎ', price: '310 ETB', img: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=400' },
      { cat: 'yogurt', en: 'Flavored Yogurt', am: 'ፍሌቨርድ እርጎ', price: '310 ETB', img: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=400' },
      { cat: 'yogurt', en: 'Strawberry Yogurt', am: 'ስትሮበሪ እርጎ', price: '310 ETB', img: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=400' },

      // FRAPPUCCINO
      { cat: 'frappuccino', en: 'Chocolate Frappuccino', am: 'ቸኮሌት ፍራፑቺኖ', price: '380 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'frappuccino', en: 'Caramel Frappuccino', am: 'ካራሜል ፍራፑቺኖ', price: '330 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },
      { cat: 'frappuccino', en: 'Mocha Frappuccino', am: 'ሞካ ፍራፑቺኖ', price: '350 ETB', img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400' },

      // OTHER
      { cat: 'other', en: 'Oat Juice', am: 'የአጃ ጁስ', price: '250 ETB', img: 'https://images.unsplash.com/photo-1505252585461-04db1eb84625?w=400' },
      { cat: 'other', en: 'Detox', am: 'ዲቶክስ', price: '110 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' },
      { cat: 'other', en: 'Mint', am: 'ናንእና (ሚንት)', price: '230 ETB', img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=400' }
    ];

    // Render Category Buttons
    function renderCategories() {
      const navContainer = document.getElementById('categoryNav');
      navContainer.innerHTML = categories.map(cat => `
        <button class="cat-pill ${cat.id === currentCategory ? 'active' : ''}" 
                onclick="setCategory('${cat.id}')">
          ${cat[currentLang]}
        </button>
      `).join('');
    }

    // Set Active Category
    function setCategory(catId) {
      currentCategory = catId;
      renderCategories();
      filterMenu();
    }

    // Render Menu Cards
    function renderMenu(items) {
      const grid = document.getElementById('menuGrid');
      
      if (items.length === 0) {
        grid.innerHTML = `
          <div class="no-results">
            <i class="fa-solid fa-utensils" style="font-size: 2rem; margin-bottom: 10px;"></i>
            <p>${currentLang === 'en' ? 'No items found.' : 'ምንም ነገር አልተገኘም።'}</p>
          </div>`;
        return;
      }

      grid.innerHTML = items.map(item => `
        <div class="card">
          <div class="card-img-container">
            <img src="${item.img}" alt="${item.en}" loading="lazy" onerror="this.src='https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=400'">
          </div>
          <div class="card-body">
            <div class="card-title">${item[currentLang]}</div>
            <div class="card-price">${item.price}</div>
          </div>
        </div>
      `).join('');
    }

    // Dynamic Search & Category Filter
    function filterMenu() {
      const query = document.getElementById('searchInput').value.toLowerCase().trim();

      const filtered = menuData.filter(item => {
        const matchesCategory = currentCategory === 'all' || item.cat === currentCategory;
        const matchesSearch = item.en.toLowerCase().includes(query) || item.am.toLowerCase().includes(query);
        return matchesCategory && matchesSearch;
      });

      renderMenu(filtered);
    }

    // Language Switcher Function
    function toggleLanguage() {
      currentLang = currentLang === 'en' ? 'am' : 'en';
      
      // Update UI Language Elements
      document.getElementById('langBtn').innerText = currentLang === 'en' ? 'አማርኛ' : 'English';
      document.getElementById('searchInput').placeholder = currentLang === 'en' ? 'Search menu...' : 'ምግብ ወይም መጠጥ ይፈልጉ...';

      renderCategories();
      filterMenu();
    }

    // Initial Load
    renderCategories();
    filterMenu();
  </script>
</body>
</html>
