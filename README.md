<!DOCTYPE html>
<html lang="am">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Eroshake Juice - Digital Menu</title>
  <style>
    :root {
      --primary-blue: #0284c7;     /* Bright Blue */
      --dark-blue: #0c4a6e;        /* Dark Navy Blue */
      --light-blue: #f0f9ff;       /* Very Light Blue Tint */
      --accent-blue: #38bdf8;      /* Accent Ice Blue */
      --bg-color: #f8fafc;         /* Clean Soft White Background */
      --card-bg: #ffffff;         /* Pure White Cards */
      --text-dark: #0f172a;       /* Dark Text */
      --text-muted: #64748b;      /* Muted Subtitles */
      --border-color: #e2e8f0;    /* Light Border */
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, sans-serif;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-dark);
      padding-bottom: 2rem;
    }

    /* Header & Navigation */
    header {
      background-color: var(--card-bg);
      padding: 1.25rem 1rem 1rem 1rem;
      position: sticky;
      top: 0;
      z-index: 100;
      border-bottom: 2px solid var(--light-blue);
      box-shadow: 0 4px 6px -1px rgba(2, 132, 199, 0.08);
    }

    .header-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 600px;
      margin: 0 auto 1.2rem auto;
    }

    .brand-name {
      font-size: 1.5rem;
      font-weight: 800;
      color: var(--primary-blue);
      letter-spacing: -0.5px;
    }

    .lang-btn {
      background-color: var(--light-blue);
      color: var(--primary-blue);
      border: 1px solid #bae6fd;
      padding: 0.4rem 0.9rem;
      border-radius: 20px;
      font-weight: 700;
      font-size: 0.85rem;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .lang-btn:hover {
      background-color: var(--primary-blue);
      color: white;
    }

    /* Category Buttons */
    .category-tabs {
      display: flex;
      justify-content: flex-start;
      gap: 0.5rem;
      overflow-x: auto;
      padding-bottom: 0.25rem;
      max-width: 600px;
      margin: 0 auto;
      scrollbar-width: none; /* Hide scrollbar Firefox */
    }
    
    .category-tabs::-webkit-scrollbar {
      display: none; /* Hide scrollbar Chrome/Safari */
    }

    .tab-btn {
      background: var(--light-blue);
      border: 1px solid #bae6fd;
      color: var(--dark-blue);
      padding: 0.5rem 1.1rem;
      border-radius: 20px;
      cursor: pointer;
      font-weight: 600;
      font-size: 0.9rem;
      white-space: nowrap;
      transition: all 0.2s ease;
    }

    .tab-btn.active, .tab-btn:hover {
      background-color: var(--primary-blue);
      color: #ffffff;
      border-color: var(--primary-blue);
      box-shadow: 0 2px 8px rgba(2, 132, 199, 0.25);
    }

    /* Menu Container */
    .menu-container {
      max-width: 600px;
      margin: 1.5rem auto;
      padding: 0 1rem;
    }

    .section-title {
      font-size: 1.25rem;
      color: var(--dark-blue);
      margin-bottom: 1rem;
      padding-bottom: 0.3rem;
      border-bottom: 3px solid var(--accent-blue);
      display: inline-block;
    }

    /* Menu Item Card */
    .menu-item {
      background-color: var(--card-bg);
      border: 1px solid var(--border-color);
      border-radius: 14px;
      padding: 0.85rem;
      margin-bottom: 1rem;
      display: flex;
      align-items: center;
      gap: 1rem;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .menu-item:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 12px rgba(2, 132, 199, 0.08);
    }

    .item-img {
      width: 85px;
      height: 85px;
      border-radius: 10px;
      object-fit: cover;
      background-color: var(--light-blue);
    }

    .item-info {
      flex: 1;
    }

    .item-name {
      font-size: 1.05rem;
      font-weight: 700;
      color: var(--text-dark);
      margin-bottom: 0.25rem;
    }

    .item-desc {
      font-size: 0.85rem;
      color: var(--text-muted);
      margin-bottom: 0.5rem;
      line-height: 1.3;
    }

    .item-price {
      font-size: 1rem;
      font-weight: 800;
      color: var(--primary-blue);
    }

    .hidden {
      display: none;
    }
  </style>
</head>
<body>

  <header>
    <div class="header-top">
      <div class="brand-name">Eroshake Juice</div>
      <button class="lang-btn" id="langBtn" onclick="toggleLanguage()">English</button>
    </div>
    
    <div class="category-tabs">
      <button class="tab-btn active" data-cat="all" onclick="filterMenu('all')">ሁሉም</button>
      <button class="tab-btn" data-cat="juices" onclick="filterMenu('juices')">ጁሶች</button>
      <button class="tab-btn" data-cat="shakes" onclick="filterMenu('shakes')">ሼኮች</button>
      <button class="tab-btn" data-cat="snacks" onclick="filterMenu('snacks')">ስናኮች</button>
    </div>
  </header>

  <div class="menu-container">
    
    <!-- Juices Section -->
    <div class="menu-category" id="juices">
      <h2 class="section-title" data-en="Fresh Juices" data-am="ትኩስ ጁሶች">ትኩስ ጁሶች</h2>
      
      <div class="menu-item">
        <img src="https://images.unsplash.com/photo-1613478223719-2ab802602423?w=200" alt="Avocado Juice" class="item-img">
        <div class="item-info">
          <div class="item-name" data-en="Special Avocado Juice" data-am="ስፔሻል የአቮካዶ ጁስ">ስፔሻል የአቮካዶ ጁስ</div>
          <div class="item-desc" data-en="Fresh avocado layered with vimto & honey" data-am="በቪምቶ እና በማር ያሸበረቀ ትኩስ አቮካዶ">በቪምቶ እና በማር ያሸበረቀ ትኩስ አቮካዶ</div>
          <div class="item-price">120 ETB</div>
        </div>
      </div>

      <div class="menu-item">
        <img src="https://images.unsplash.com/photo-1553530666-ba11a7da3888?w=200" alt="Mango Juice" class="item-img">
        <div class="item-info">
          <div class="item-name" data-en="Mango Spris Juice" data-am="የማንጎ ስፕሪስ ጁስ">የማንጎ ስፕሪስ ጁስ</div>
          <div class="item-desc" data-en="Pure mango blended with papaya and lime" data-am="ከትኩስ ፓፓያ እና ሎሚ ጋር የተቀላቀለ ማንጎ">ከትኩስ ፓፓያ እና ሎሚ ጋር የተቀላቀለ ማንጎ</div>
          <div class="item-price">110 ETB</div>
        </div>
      </div>
    </div>

    <!-- Shakes Section -->
    <div class="menu-category" id="shakes">
      <h2 class="section-title" data-en="Special Shakes" data-am="ስፔሻል ሼኮች">ስፔሻል ሼኮች</h2>
      
      <div class="menu-item">
        <img src="https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=200" alt="Chocolate Shake" class="item-img">
        <div class="item-info">
          <div class="item-name" data-en="Oreo Milkshake" data-am="ኦሪዮ ሚልክሼክ">ኦሪዮ ሚልክሼክ</div>
          <div class="item-desc" data-en="Creamy vanilla ice cream blended with Oreo" data-am="ከቫኒላ አይስክሬም እና ኦሪዮ ብስክሌት ጋር የተመታ">ከቫኒላ አይስክሬም እና ኦሪዮ ብስክሌት ጋር የተመታ</div>
          <div class="item-price">180 ETB</div>
        </div>
      </div>
    </div>

    <!-- Snacks Section -->
    <div class="menu-category" id="snacks">
      <h2 class="section-title" data-en="Snacks & Burgers" data-am="ስናክ እና በርገር">ስናክ እና በርገር</h2>
      
      <div class="menu-item">
        <img src="https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=200" alt="Special Burger" class="item-img">
        <div class="item-info">
          <div class="item-name" data-en="Eroshake Beef Burger" data-am="ኢሮሼክ የስጋ በርገር">ኢሮሼክ የስጋ በርገር</div>
          <div class="item-desc" data-en="Juicy beef patty with cheese, lettuce & fries" data-am="የስጋ ፓቲ ከቺዝ፣ ሰላጣ እና ድንች ጥብስ ጋር">የስጋ ፓቲ ከቺዝ፣ ሰላጣ እና ድንች ጥብስ ጋር</div>
          <div class="item-price">260 ETB</div>
        </div>
      </div>
    </div>

  </div>

  <script>
    let currentLang = 'am';

    function toggleLanguage() {
      currentLang = currentLang === 'am' ? 'en' : 'am';
      const langBtn = document.getElementById('langBtn');
      
      langBtn.textContent = currentLang === 'am' ? 'English' : 'አማርኛ';

      // Update elements with data attributes
      const elements = document.querySelectorAll('[data-en]');
      elements.forEach(el => {
        el.textContent = el.getAttribute(`data-${currentLang}`);
      });

      // Update Category Tab Names
      const catBtns = document.querySelectorAll('.tab-btn');
      const catTexts = {
        am: { all: 'ሁሉም', juices: 'ጁሶች', shakes: 'ሼኮች', snacks: 'ስናኮች' },
        en: { all: 'All', juices: 'Juices', shakes: 'Shakes', snacks: 'Snacks' }
      };

      catBtns.forEach(btn => {
        const cat = btn.getAttribute('data-cat');
        btn.textContent = catTexts[currentLang][cat];
      });
    }

    function filterMenu(category) {
      const buttons = document.querySelectorAll('.tab-btn');
      buttons.forEach(btn => btn.classList.remove('active'));
      
      // Highlight selected tab
      event.target.classList.add('active');

      const categories = document.querySelectorAll('.menu-category');
      categories.forEach(cat => {
        if (category === 'all' || cat.id === category) {
          cat.classList.remove('hidden');
        } else {
          cat.classList.add('hidden');
        }
      });
    }
  </script>

</body>
</html>
