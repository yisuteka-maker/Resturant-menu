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
am: { name: "የባህል ቡና", desc: "በጀበና የፈላ ጥሩ መዓዛ ያለው ትኩስ የሀበሻ ባህላዊ ቡና።" },en: { name: "Traditional Coffee", desc: "Freshly brewed traditional Ethiopian coffee with a rich aroma." }}];// የትርጉም ቃላት ማከማቻconst translations = {am: {headerTitle: "ሜኑ", langBtn: "English", searchPlaceholder: "ይፈልጉ...",navMenu: "ሜኑ", navOrders: "ትዕዛዞች", cartTitle: "የእርስዎ ጋሪ",tableLabel: "የጠረጴዛ ቁጥር:", tablePlaceholder: "ምሳሌ: 4",totalText: "ጠቅላላ ድምር:", orderBtn: "በትዕዛዝ ወደ ቴሌግራም ላክ",addCart: "ወደ ጋሪ ጨምር", added: "ተጨምሯል!"},en: {headerTitle: "Menu", langBtn: "አማርኛ", searchPlaceholder: "Search...",navMenu: "Menu", navOrders: "Orders", cartTitle: "Your Cart",tableLabel: "Table Number:", tablePlaceholder: "e.g., 4",totalText: "Total:", orderBtn: "Send Order via Telegram",addCart: "Add to Cart", added: "Added!"}};let currentLang = 'am';let currentCategory = 'all';let cart = [];// ገጹ ሲከፈት መጀመሪያ የሚሰሩ ነገሮችdocument.addEventListener("DOMContentLoaded", () => {renderMenu();updateUI();});// የቋንቋ መቀየሪያ ፈንክሽንfunction toggleLanguage() {currentLang = currentLang === 'am' ? 'en' : 'am';updateUI();renderMenu();}function updateUI() {const trans = translations[currentLang];document.getElementById("header-title").innerText = trans.headerTitle;document.getElementById("lang-btn-text").innerText = trans.langBtn;document.getElementById("search-input").placeholder = trans.searchPlaceholder;document.getElementById("nav-menu").innerText = trans.navMenu;document.getElementById("nav-orders").innerText = trans.navOrders;document.getElementById("cart-sidebar-title").innerText = trans.cartTitle;document.getElementById("table-label").innerText = trans.tableLabel;document.getElementById("table-number").placeholder = trans.tablePlaceholder;document.getElementById("total-text").innerText = trans.totalText;document.getElementById("order-btn-text").innerText = trans.orderBtn;document.getElementById("modal-add-btn").innerText = trans.addCart;document.querySelectorAll(".cat-btn").forEach(btn => {btn.innerText = currentLang === 'am' ? btn.getAttribute("data-am") : btn.getAttribute("data-en");});}// ምግቦችን በስክሪን ላይ ማሳያfunction renderMenu(items = menuData) {const container = document.getElementById("menu-container");container.innerHTML = "";const filtered = items.filter(item => currentCategory === 'all' || item.category === currentCategory);filtered.forEach(item => {const localized = item[currentLang];const card = document.createElement("div");card.className = "bg-white border border-gray-100 rounded-2xl p-2.5 shadow-sm hover:shadow-md transition flex flex-col cursor-pointer";card.setAttribute("onclick", openModal(${item.id}));card.innerHTML = <img src="${item.image}" alt="${localized.name}" class="w-full h-28 object-cover rounded-xl mb-2"> <h4 class="font-bold text-sm text-gray-900 line-clamp-1">${localized.name}</h4> <p class="text-[11px] text-gray-400 line-clamp-1 mb-2">${localized.desc}</p> <div class="flex justify-between items-center mt-auto"> <span class="text-emerald-800 font-bold text-sm">${item.price} ETB</span> <button onclick="event.stopPropagation(); addToCart(${item.id})" class="bg-emerald-50 text-emerald-900 w-7 h-7 rounded-full flex items-center justify-center hover:bg-emerald-800 hover:text-white transition"> <i class="fa-solid fa-plus text-xs"></i> </button> </div>;container.appendChild(card);});}// የምግብ አይነቶችን መለያ (Fasting, Breakfast...)function filterMenu(category) {currentCategory = category;document.querySelectorAll(".cat-btn").forEach(btn => {btn.classList.remove("bg-emerald-900", "text-white", "shadow");btn.classList.add("bg-gray-100", "text-gray-600");});const activeBtn = Array.from(document.querySelectorAll(".cat-btn")).find(btn => btn.getAttribute("onclick").includes('${category}'));if(activeBtn) {activeBtn.classList.remove("bg-gray-100", "text-gray-600");activeBtn.classList.add("bg-emerald-900", "text-white", "shadow");}renderMenu();}// ምግብ መፈለጊያfunction searchMenu() {const query = document.getElementById("search-input").value.toLowerCase();const filtered = menuData.filter(item => {return item.am.name.includes(query) || item.en.name.toLowerCase().includes(query);});renderMenu(filtered);}// ምግብ ሲነካ በሰፊው ማሳያ (Modal)function openModal(id) {const item = menuData.find(i => i.id === id);const localized = item[currentLang];document.getElementById("modal-img").src = item.image;document.getElementById("modal-title").innerText = localized.name;document.getElementById("modal-price").innerText = ${item.price} ETB;document.getElementById("modal-desc").innerText = localized.desc;document.getElementById("modal-time").innerText = item.time;document.getElementById("modal-stars").innerText = item.stars;const addBtn = document.getElementById("modal-add-btn");addBtn.onclick = () => {addToCart(item.id);addBtn.innerText = translations[currentLang].added;setTimeout(() => { closeModal(); updateUI(); }, 500);};document.getElementById("detail-modal").classList.remove("hidden");document.getElementById("detail-modal").classList.add("flex");}function closeModal() {document.getElementById("detail-modal").classList.remove("flex");document.getElementById("detail-modal").classList.add("hidden");}// የጋሪ ስራዎች (Cart Operations)function toggleCart() {document.getElementById("cart-sidebar").classList.toggle("translate-x-full");}function addToCart(id) {const existing = cart.find(i => i.id === id);if(existing) {existing.quantity++;} else {const item = menuData.find(i => i.id === id);cart.push({...item, quantity: 1});}updateCartUI();}function changeQuantity(id, amount) {const item = cart.find(i => i.id === id);if(item) {item.quantity += amount;if(item.quantity <= 0) cart = cart.filter(i => i.id !== id);}updateCartUI();}function updateCartUI() {const container = document.getElementById("cart-items");container.innerHTML = "";let total = 0;let count = 0;cart.forEach(item => {total += item.price * item.quantity;count += item.quantity;const localized = item[currentLang];const row = document.createElement("div");row.className = "flex items-center justify-between bg-gray-50 p-2.5 rounded-xl border border-gray-100";row.innerHTML = <div class="flex items-center gap-2 max-w-[60%]"> <img src="${item.image}" class="w-12 h-12 object-cover rounded-lg"> <div> <h4 class="text-xs font-bold text-gray-900 line-clamp-1">${localized.name}</h4> <span class="text-[11px] text-emerald-800 font-semibold">${item.price} ETB</span> </div> </div> <div class="flex items-center gap-2 bg-white border border-gray-200 px-2 py-1 rounded-lg"> <button onclick="changeQuantity(${item.id}, -1)" class="text-gray-500 font-bold text-xs">-</button> <span class="text-xs font-bold w-4 text-center">${item.quantity}</span> <button onclick="changeQuantity(${item.id}, 1)" class="text-emerald-800 font-bold text-xs">+</button> </div>;container.appendChild(row);});document.getElementById("cart-count").innerText = count;document.getElementById("total-price").innerText = ${total.toFixed(2)} ETB;}// ማዘዣውን ወደ ቴሌግራም መላኪያfunction checkout() {if(cart.length === 0) {alert(currentLang === 'am' ? "እባክዎ መጀመሪያ ምግብ ይምረጡ!" : "Your cart is empty!");return;}const table = document.getElementById("table-number").value.trim();if(!table) {alert(currentLang === 'am' ? "እባክዎ የጠረጴዛ ቁጥር ያስገቡ!" : "Please enter your Table Number!");return;}let text = 🔔 **አዲስ ትዕዛዝ ከ ፍቅር ሬስቶራንት**\n\n;text += 🪑 **ጠረጴዛ ቁጥር:** ${table}\n;text += -------------------------\n;let total = 0;cart.forEach(item => {text += • ${item[currentLang].name} x${item.quantity} - ${item.price * item.quantity} ETB\n;total += item.price * item.quantity;});text += -------------------------\n;text += 💰 **አጠቃላይ ድምር:** ${total} ETB;// ወደ ቴሌግራም መተግበሪያ በቀጥታ መላኪያ ሊንክwindow.open(https://t.me{encodeURIComponent(text)}, '_blank');}
