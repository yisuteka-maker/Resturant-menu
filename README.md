<!DOCTYPE html>
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ፍቅር レストラン (Fikir Restaurant)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cloudflare.com">
    <style>
        * { box-sizing: border-box; }
        body { background-color: #f3f4f6; margin: 0; padding: 0; overflow-x: hidden; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="font-sans text-gray-800 flex justify-center items-center min-h-screen">

    <!-- Mobile Full Screen / App Container -->
    <div class="w-full max-w-md bg-white shadow-xl overflow-hidden relative flex flex-col h-screen sm:h-[90vh] sm:rounded-[35px]">
        
        <!-- Header -->
        <header class="p-4 bg-white flex justify-between items-center border-b border-gray-100 z-10 shrink-0">
            <h1 class="text-xl font-bold text-gray-900" id="header-title">ሜኑ (Menu)</h1>
            <div class="flex items-center gap-2">
                <!-- Language Switcher Button -->
                <button onclick="toggleLanguage()" class="bg-emerald-800 text-white px-2.5 py-1 rounded-lg text-xs font-semibold shadow hover:bg-emerald-700 transition">
                    🌐 <span id="lang-btn-text">English</span>
                </button>
                <!-- Cart Button -->
                <button onclick="toggleCart()" class="bg-emerald-800 text-white p-2.5 rounded-full shadow hover:bg-emerald-700 transition relative">
                    <i class="fa-solid fa-bag-shopping"></i>
                    <span id="cart-count" class="absolute -top-1 -right-1 bg-red-500 text-white text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold">0</span>
                </button>
            </div>
        </header>

        <!-- Main Scrollable Area -->
        <main class="flex-grow overflow-y-auto p-4 space-y-4 pb-24">
            <!-- Search Bar -->
            <div class="relative">
                <i class="fa-solid fa-magnifying-glass absolute left-3 top-3.5 text-gray-400"></i>
                <input type="text" id="search-input" oninput="searchMenu()" placeholder="ይፈልጉ..." class="w-full bg-gray-100 pl-10 pr-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-emerald-800">
            </div>

            <!-- Categories -->
            <div class="flex gap-2 overflow-x-auto no-scrollbar pb-1">
                <button onclick="filterMenu('all')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-emerald-900 text-white whitespace-nowrap shadow" data-am="ሁሉም" data-en="All">ሁሉም</button>
                <button onclick="filterMenu('fasting')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="ጾም" data-en="Fasting">ጾም</button>
                <button onclick="filterMenu('non-fasting')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="ፍስክ" data-en="Non-Fasting">ፍስክ</button>
                <button onclick="filterMenu('breakfast')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="ቁርስ" data-en="Breakfast">ቁርስ</button>
                <button onclick="filterMenu('drink')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="መጠጥ" data-en="Drinks">መጠጥ</button>
            </div>

            <!-- Menu Grid -->
            <div id="menu-container" class="grid grid-cols-2 gap-3">
                <!-- ጃቫስክሪፕት በቪው እዚህ ይሞላል -->
            </div>
        </main>

        <!-- Bottom Navigation Bar -->
        <nav class="absolute bottom-0 left-0 right-0 bg-white border-t border-gray-200 py-3 px-6 flex justify-around items-center text-gray-400 z-20 shrink-0">
            <button onclick="filterMenu('all')" class="text-emerald-900 flex flex-col items-center text-xs font-bold w-1/2">
                <i class="fa-solid fa-utensils text-lg"></i>
                <span id="nav-menu">ሜኑ</span>
            </button>
            <button onclick="toggleCart()" class="hover:text-emerald-900 flex flex-col items-center text-xs w-1/2">
                <i class="fa-regular fa-file-lines text-lg"></i>
                <span id="nav-orders">ትዕዛዞች</span>
            </button>
        </nav>
    </div>

    <!-- Food Detail Modal -->
    <div id="detail-modal" class="fixed inset-0 bg-black bg-opacity-60 hidden justify-center items-center z-50 p-4">
        <div class="bg-white rounded-3xl max-w-sm w-full p-5 relative shadow-2xl flex flex-col max-h-[85vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-3">
                <button onclick="closeModal()" class="w-8 h-8 bg-gray-100 rounded-full flex items-center justify-center text-gray-600 font-bold"><i class="fa-solid fa-arrow-left"></i></button>
                <button class="w-8 h-8 bg-emerald-50 text-emerald-900 rounded-full flex items-center justify-center"><i class="fa-solid fa-bag-shopping"></i></button>
            </div>
            <img id="modal-img" src="" alt="" class="w-full h-48 object-cover rounded-2xl mb-4 shadow-md">
            
            <div class="flex justify-between items-start mb-2">
                <h3 id="modal-title" class="text-xl font-bold text-gray-900"></h3>
                <div class="text-emerald-800 font-bold text-lg" id="modal-price"></div>
            </div>

            <div class="flex items-center gap-4 text-xs text-gray-500 mb-3">
                <span><i class="fa-regular fa-clock text-emerald-800"></i> <span id="modal-time">20 min</span></span>
                <span id="modal-stars" class="text-yellow-500">★★★★★</span>
            </div>

            <p id="modal-desc" class="text-xs text-gray-600 leading-relaxed mb-4 bg-gray-50 p-3 rounded-xl"></p>

            <div class="mt-auto pt-2">
                <button id="modal-add-btn" class="w-full bg-[#114b3e] text-white py-3 rounded-xl font-bold hover:bg-emerald-950 transition shadow-lg text-sm">
                    ወደ ጋሪ ጨምር
                </button>
            </div>
        </div>
    </div>

    <!-- Shopping Cart & Orders Sidebar -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-full sm:w-80 bg-white shadow-2xl p-5 transform translate-x-full transition-transform duration-300 z-50 flex flex-col border-l border-gray-200">
        <div class="flex justify-between items-center mb-4 border-b pb-3">
            <h3 class="text-lg font-bold text-gray-900" id="cart-sidebar-title">የእርስዎ ጋሪ</h3>
            <button onclick="toggleCart()" class="text-gray-400 hover:text-black font-bold text-xl px-2">✕</button>
        </div>

        <!-- Table Number Input -->
        <div class="mb-3">
            <label class="block text-xs font-semibold text-gray-600 mb-1" id="table-label">የጠረጴዛ ቁጥር (Table Number):</label>
            <input type="number" id="table-number" placeholder="ምሳሌ: 4" class="w-full bg-gray-100 border border-gray-200 px-3 py-2 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-emerald-800">
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-3 pr-1">
            <!-- የታዘዙ ምግቦች እዚህ ይገባሉ -->
        </div>

        <div class="border-t pt-4 mt-2">
            <div class="flex justify-between font-bold text-base mb-4">
                <span id="total-text">ጠቅላላ ድምር:</span>
                <span id="total-price" class="text-emerald-900">0.00 ETB</span>
            </div>
            <button onclick="checkout()" class="w-full bg-[#114b3e] text-white py-3 rounded-xl font-bold hover:bg-emerald-950 shadow transition text-sm">
                <span id="order-btn-text">በትዕዛዝ ወደ ቴሌግራም ላክ</span>
            </button>
        </div>
    </div>

    <!-- ጃቫስክሪፕት (JavaScript Logic) -->
    <script>
        // የሜኑ መረጃዎች (የናሙና ምግቦች)
        const menuData = [
            {
                id: 1, category: "fasting", stars: "★★★★★", time: "15 min", price: 250,
                image: "https://unsplash.com",
                am: { name: "ልዩ በያይነቱ", desc: "የተለያዩ የምስር፣ የክክ፣ የሽሮ ወጥ እና አትክልቶች ድብልቅ ከባህላዊ እንጀራ ጋር።" },
                en: { name: "Special Beyaynetu", desc: "A combination of various lentil stews, shiro, and vegetables served with Injera." }
            },
            {
                id: 2, category: "non-fasting", stars: "★★★★★", time: "20 min", price: 480,
                image: "https://unsplash.com",
                am: { name: "ልዩ ክትፎ", desc: "በጥንቃቄ የተከተፈ ቀይ ስጋ በንጥር ቅቤ፣ በሚጥሚጣ እና አይብ የቀረበ።" },
                en: { name: "Special Kitfo", desc: "Finely minced lean beef, seasoned with mitmita and herbed clarified butter." }
            },
            {
                id: 3, category: "breakfast", stars: "★★★★☆", time: "15 min", price: 220,
                image: "https://unsplash.com",
                am: { name: "እንቁላል ፍርፍር", desc: "በሽንኩርት፣ ቃሪያ እና ቲማቲም የተጠበሰ እንቁላል በዳቦ ወይም በኮረንቲ የቀረበ።" },
                en: { name: "Scrambled Eggs", desc: "Scrambled eggs cooked with onions, green peppers, and tomatoes." }
            },
            {
                id: 4, category: "drink", stars: "★★★★★", time: "5 min", price: 70,
                image: "https://unsplash.com",
                am: { name: "የባህል ቡና", desc: "በጀበና የፈላ ጥሩ መዓዛ ያለው ትኩስ የሀበሻ ባህላዊ ቡና።" },

