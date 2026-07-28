<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ፍቅር ሬስቶራንት - Luxury Dining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        * { box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; }
        body { background-color: #0f172a; margin: 0; padding: 0; overflow-x: hidden; }
        
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

        .glass-card {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.4);
        }

        .luxury-gradient-btn {
            background: linear-gradient(135deg, #064e3b 0%, #047857 50%, #065f46 100%);
            box-shadow: 0 10px 25px -5px rgba(4, 120, 87, 0.4);
        }

        .luxury-gradient-btn:hover {
            background: linear-gradient(135deg, #022c22 0%, #065f46 50%, #047857 100%);
            transform: translateY(-2px);
            box-shadow: 0 15px 30px -5px rgba(4, 120, 87, 0.6);
        }

        .gold-glow {
            box-shadow: 0 0 15px rgba(245, 158, 11, 0.3);
        }

        .pulse-alarm {
            animation: pulse-red 1.5s infinite;
        }

        @keyframes pulse-red {
            0% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(239, 68, 68, 0); }
            100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); }
        }

        .spinner {
            border: 2px solid #f3f3f3;
            border-top: 2px solid #ffffff;
            border-radius: 50%;
            width: 16px;
            height: 16px;
            animation: spin 0.8s linear infinite;
            display: inline-block;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body class="bg-slate-900 text-slate-800 flex justify-center items-center min-h-screen p-0 sm:p-4">

    <!-- Mobile Frame Container -->
    <div class="w-full max-w-md bg-slate-50 shadow-2xl overflow-hidden relative flex flex-col h-screen sm:h-[92vh] sm:rounded-[40px] border border-slate-700/50">

        <!-- Top Luxury Header -->
        <header class="p-4 bg-slate-900 text-white flex justify-between items-center border-b border-slate-800 z-10 shrink-0 shadow-md">
            <div class="flex items-center gap-2">
                <div class="w-9 h-9 rounded-2xl bg-gradient-to-tr from-amber-400 to-amber-600 flex items-center justify-center font-black text-slate-950 shadow-md">
                    <i class="fa-solid fa-crown text-sm"></i>
                </div>
                <div>
                    <h1 class="text-base font-extrabold tracking-tight text-white leading-none">ፍቅር ሬስቶራንት</h1>
                    <span class="text-[10px] text-amber-400 font-medium tracking-wider uppercase">Luxury Menu</span>
                </div>
            </div>

            <div class="flex items-center gap-2">
                <button onclick="toggleLanguage()" class="bg-slate-800 hover:bg-slate-700 text-amber-400 border border-amber-400/30 px-3 py-1.5 rounded-xl text-xs font-bold transition flex items-center gap-1.5 shadow-sm active:scale-95">
                    <i class="fa-solid fa-globe text-amber-400"></i>
                    <span id="lang-btn-text">English</span>
                </button>

                <button onclick="toggleCart()" class="luxury-gradient-btn text-white p-2.5 rounded-xl shadow-lg transition relative active:scale-95 flex items-center justify-center">
                    <i class="fa-solid fa-bag-shopping text-base"></i>
                    <span id="cart-count" class="absolute -top-1.5 -right-1.5 bg-rose-500 text-white text-[10px] w-5 h-5 rounded-full flex items-center justify-center font-black ring-2 ring-slate-900 shadow-md">0</span>
                </button>
            </div>
        </header>

        <!-- Live Order Delay Tracking Banner -->
        <div id="live-order-banner" class="hidden bg-gradient-to-r from-amber-500 to-orange-600 text-slate-950 px-4 py-2 flex justify-between items-center text-xs font-bold shadow-inner cursor-pointer" onclick="openActiveOrderModal()">
            <div class="flex items-center gap-2">
                <span class="w-2 h-2 rounded-full bg-rose-900 animate-ping"></span>
                <span id="active-order-status-text">ትዕዛዝዎ በመዘጋጀት ላይ ነው...</span>
            </div>
            <div class="bg-slate-950 text-amber-400 px-2.5 py-0.5 rounded-lg text-[11px] font-mono" id="active-order-timer">15:00</div>
        </div>

        <!-- Main Body Content -->
        <main class="flex-grow overflow-y-auto p-4 space-y-4 pb-28">

            <!-- Search Bar -->
            <div class="relative">
                <i class="fa-solid fa-magnifying-glass absolute left-4 top-3.5 text-slate-400 text-sm"></i>
                <input type="text" id="search-input" oninput="searchMenu()" placeholder="የሚወዱትን ምግብ ይፈልጉ..." class="w-full bg-white pl-11 pr-4 py-3 rounded-2xl text-xs font-semibold border border-slate-200 focus:outline-none focus:ring-2 focus:ring-emerald-600 shadow-sm transition">
            </div>

            <!-- Categories Slider -->
            <div class="flex gap-2.5 overflow-x-auto no-scrollbar pb-1">
                <button onclick="filterMenu('all')" data-cat="all" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-900 text-amber-400 shadow-lg border border-slate-800 whitespace-nowrap transition-all duration-300">ሁሉም</button>
                <button onclick="filterMenu('fasting')" data-cat="fasting" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-white text-slate-600 border border-slate-200 whitespace-nowrap hover:bg-slate-100 transition-all duration-300">ጾም</button>
                <button onclick="filterMenu('non-fasting')" data-cat="non-fasting" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-white text-slate-600 border border-slate-200 whitespace-nowrap hover:bg-slate-100 transition-all duration-300">ፍስክ</button>
                <button onclick="filterMenu('breakfast')" data-cat="breakfast" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-white text-slate-600 border border-slate-200 whitespace-nowrap hover:bg-slate-100 transition-all duration-300">ቁርስ</button>
                <button onclick="filterMenu('drink')" data-cat="drink" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-white text-slate-600 border border-slate-200 whitespace-nowrap hover:bg-slate-100 transition-all duration-300">መጠጥ</button>
            </div>

            <!-- Menu Grid -->
            <div id="menu-container" class="grid grid-cols-1 gap-3.5"></div>
        </main>

        <!-- Bottom Navigation -->
        <nav class="absolute bottom-0 left-0 right-0 bg-slate-900/95 backdrop-blur-md border-t border-slate-800 py-3 px-6 flex justify-around items-center text-slate-400 z-20 shrink-0">
            <button onclick="filterMenu('all')" class="text-amber-400 flex flex-col items-center text-xs font-bold w-1/2 transition transform active:scale-95">
                <i class="fa-solid fa-utensils text-lg mb-1"></i>
                <span id="nav-menu">ሜኑ</span>
            </button>
            <button onclick="toggleCart()" class="hover:text-amber-400 flex flex-col items-center text-xs font-semibold w-1/2 transition transform active:scale-95">
                <i class="fa-solid fa-receipt text-lg mb-1"></i>
                <span id="nav-orders">ትዕዛዞች</span>
            </button>
        </nav>
    </div>

    <!-- Food Detail Modal -->
    <div id="detail-modal" class="fixed inset-0 bg-slate-950/75 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-white rounded-3xl max-w-sm w-full p-5 relative shadow-2xl flex flex-col max-h-[85vh] overflow-y-auto border border-slate-100">
            <div class="flex justify-between items-center mb-3">
                <button onclick="closeModal()" class="w-9 h-9 bg-slate-100 rounded-full flex items-center justify-center text-slate-600 font-bold hover:bg-slate-200 transition"><i class="fa-solid fa-xmark"></i></button>
                <div class="w-9 h-9 bg-amber-50 text-amber-600 rounded-full flex items-center justify-center font-bold"><i class="fa-solid fa-heart"></i></div>
            </div>
            <img id="modal-img" src="" alt="" class="w-full h-52 object-cover rounded-2xl mb-4 shadow-md">

            <div class="flex justify-between items-start mb-2">
                <h3 id="modal-title" class="text-lg font-black text-slate-900 leading-snug"></h3>
                <div class="text-emerald-700 font-extrabold text-lg" id="modal-price"></div>
            </div>

            <div class="flex items-center gap-4 text-xs font-semibold text-slate-500 mb-3">
                <span><i class="fa-regular fa-clock text-emerald-700"></i> <span id="modal-time">15 ደቂቃ</span></span>
                <span id="modal-stars" class="text-amber-400">★★★★★</span>
            </div>

            <p id="modal-desc" class="text-xs text-slate-600 leading-relaxed mb-5 bg-slate-50 p-3.5 rounded-2xl border border-slate-100"></p>

            <div class="mt-auto pt-2">
                <button id="modal-add-btn" class="w-full luxury-gradient-btn text-white py-3.5 rounded-2xl font-extrabold shadow-lg transition text-xs flex items-center justify-center gap-2">
                    <i class="fa-solid fa-cart-plus"></i>
                    <span>ወደ ጋሪ ጨምር</span>
                </button>
            </div>
        </div>
    </div>

    <!-- Active Delayed Order Alert Modal 🚨 -->
    <div id="delay-alert-modal" class="fixed inset-0 bg-slate-950/80 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-white rounded-3xl max-w-sm w-full p-6 text-center shadow-2xl border-2 border-rose-500 pulse-alarm relative">
            <div class="w-16 h-16 bg-rose-100 text-rose-600 rounded-full flex items-center justify-center text-3xl mx-auto mb-3">
                🚨
            </div>
            <h3 class="text-lg font-black text-slate-900 mb-1" id="delay-alert-title">ትዕዛዝዎ ዘግይቷል!</h3>
            <p class="text-xs text-slate-600 mb-4" id="delay-alert-msg">ትዕዛዝዎ ከተሰጠው ዝግጅት ጊዜ በላይ ወስዷል። እባክዎ ለአስተናጋጆች ጥሪ ይላኩ።</p>
            
            <div class="space-y-2">
                <button onclick="sendUrgentDelayNotification()" id="urgent-btn" class="w-full bg-rose-600 hover:bg-rose-700 text-white font-extrabold py-3 rounded-xl text-xs shadow-lg transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-bell"></i>
                    <span>ለአስተናጋጅ አሁኑኑ ጥሪ ላክ!</span>
                </button>
                <button onclick="closeDelayModal()" class="w-full bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold py-2.5 rounded-xl text-xs transition">
                    ዝጋ (Dismiss)
                </button>
            </div>
        </div>
    </div>

    <!-- Shopping Cart Sidebar -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-full sm:w-80 bg-white shadow-2xl p-5 transform translate-x-full transition-transform duration-300 z-50 flex flex-col border-l border-slate-200">
        <div class="flex justify-between items-center mb-4 border-b border-slate-100 pb-3">
            <h3 class="text-base font-extrabold text-slate-900" id="cart-sidebar-title">የመረጧቸው እቃዎች</h3>
            <button onclick="toggleCart()" class="w-8 h-8 rounded-full bg-slate-100 text-slate-600 font-bold text-sm flex items-center justify-center hover:bg-slate-200">✕</button>
        </div>

        <div class="mb-3">
            <label class="block text-xs font-bold text-slate-700 mb-1" id="table-label">የጠረጴዛ ቁጥር (Table Number):</label>
            <input type="number" id="table-number" placeholder="ምሳሌ: 4" class="w-full bg-slate-50 border border-slate-200 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-600">
        </div>

        <div class="mb-3">
            <label class="block text-xs font-bold text-slate-700 mb-1" id="note-label">ልዩ ማስታወሻ (Special Note):</label>
            <input type="text" id="order-note" placeholder="ለምሳሌ: ያለ በርበሬ ይሁን..." class="w-full bg-slate-50 border border-slate-200 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-600">
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-2.5 pr-1"></div>

        <div class="border-t border-slate-100 pt-4 mt-2">
            <div class="flex justify-between font-extrabold text-sm mb-4">
                <span id="total-text" class="text-slate-700">አጠቃላይ ዋጋ:</span>
                <span id="total-price" class="text-emerald-700 text-base">0.00 ETB</span>
            </div>
            <button id="checkout-btn" onclick="checkout()" class="w-full luxury-gradient-btn text-white py-3.5 rounded-2xl font-extrabold shadow-xl transition text-xs flex items-center justify-center gap-2">
                <i class="fa-brands fa-telegram text-base"></i>
                <span id="order-btn-text">ትዕዛዝ በቦት ላክ</span>
            </button>
            <p id="order-status" class="text-center text-xs mt-2 hidden font-bold"></p>
        </div>
    </div>

    <!-- JavaScript Engine -->
    <script>
        let currentLang = 'am';

        // ቴሌግራም ቦት እና ግሩፕ ID
        const BOT_TOKEN = "8752629354:AAEwRCOv5_SR4ynYGFZLgBD_b999E2SEpyA";
        const CHAT_ID = "-1004466655656";

        let activeOrder = JSON.parse(localStorage.getItem('luxury_active_order') || 'null');

        const translations = {
            en: {
                headerTitle: "Menu", searchPlaceholder: "Search luxury meals...", navMenu: "Menu", navOrders: "Orders",
                addToCart: "Add to Cart", cartTitle: "Your Selected Items",
                tableLabel: "Table Number:", noteLabel: "Special Note:", totalText: "Total:",
                orderBtn: "Send Order via Bot", emptyCart: "Your cart is empty",
                sending: "Sending order...", sent: "Order sent to group successfully! 🎉", failed: "Could not send. Check connection.",
                enterTableAlert: "Please enter your Table Number!", selectItemsAlert: "Please select items first!",
                delayTitle: "Order Delayed! 🚨", delayMsg: "Your order is taking longer than expected. Click below to alert the staff immediately.",
                delaySent: "Urgent alert sent to staff! 🚨",
                categories: { all: "All", fasting: "Fasting", "non-fasting": "Non-Fasting", breakfast: "Breakfast", drink: "Drinks" }
            },
            am: {
                headerTitle: "ምግብ ዝርዝር", searchPlaceholder: "የሚወዱትን ምግብ ይፈልጉ...", navMenu: "ሜኑ", navOrders: "ትዕዛዞች",
                addToCart: "ወደ ጋሪ ጨምር", cartTitle: "የመረጧቸው እቃዎች",
                tableLabel: "የጠረጴዛ ቁጥር (Table Number):", noteLabel: "ልዩ ማስታወሻ (Special Note):", totalText: "አጠቃላይ ዋጋ:",
                orderBtn: "ትዕዛዝ በቦት ላክ", emptyCart: "ጋሪዎ ባዶ ነው",
                sending: "ትዕዛዝዎ በመላክ ላይ...", sent: "ትዕዛዝዎ ወደ ግሩፑ በተሳካ ሁኔታ ተልኳል! 🎉", failed: "ትዕዛዙ አልተላከም። እባክዎ እንደገና ይሞክሩ።",
                enterTableAlert: "እባክዎ የጠረጴዛ ቁጥር ያስገቡ!", selectItemsAlert: "እባክዎ መጀመሪያ ምግብ ይምረጡ!",
                delayTitle: "ትዕዛዝዎ ዘግይቷል! 🚨", delayMsg: "ትዕዛዝዎ ከተሰጠው ዝግጅት ጊዜ በላይ ወስዷል። ለአስተናጋጆች አሁኑኑ ጥሪ ይላኩ።",
                delaySent: "ለአስተናጋጆች አስቸኳይ ጥሪ ተልኳል! 🚨",
                categories: { all: "ሁሉም", fasting: "ጾም", "non-fasting": "ፍስክ", breakfast: "ቁርስ", drink: "መጠጥ" }
            }
        };

        const menuItems = [
            { id: 1, name: { am: "የጾም ፍርፍር", en: "Fasting Firfir" }, category: "fasting", price: 150.00, time: "15 min", desc: { am: "በዘይት፣ ሽንኩርት እና በርበሬ የተዘጋጀ ጣፋጭ የጾም ፍርፍር።", en: "Delicious fasting firfir prepared with oil, onions, and berbere." }, image: "https://images.unsplash.com/photo-1541544741938-0af808871cc0?w=500" },
            { id: 2, name: { am: "ዶሮ ወጥ (ፍስክ)", en: "Doro Wat (Non-Fasting)" }, category: "non-fasting", price: 450.00, time: "30 min", desc: { am: "በንጹህ ቅቤ፣ ዶሮ እና እንቁላል የተዘጋጀ ባህላዊ የፍስክ ወጥ።", en: "Traditional non-fasting chicken stew prepared with spiced butter and eggs." }, image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" },
            { id: 3, name: { am: "ክትፎ ስፔሻል", en: "Special Kitfo" }, category: "non-fasting", price: 500.00, time: "25 min", desc: { am: "የተፈጨ የቀቀለ ስጋ ከሚጥሚጣ እና ንጹህ ቅቤ ጋር።", en: "Minced raw/cooked lean beef seasoned with mitmita and spiced butter." }, image: "https://images.unsplash.com/photo-1544025162-d76694265947?w=500" },
            { id: 4, name: { am: "የጾም በያይነት", en: "Fasting Beyaynetu" }, category: "fasting", price: 250.00, time: "20 min", desc: { am: "ልዩ ልዩ የጾም አትክልት ወጦች በምርጥ እንጀራ።", en: "Assorted vegetarian stews served on injera." }, image: "https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=500" },
            { id: 5, name: { am: "ጥብስ ፍርፍር", en: "Tibs Firfir" }, category: "non-fasting", price: 380.00, time: "20 min", desc: { am: "ከተጠበሰ ስጋ እና ከቀቀለ እንጀራ ጋር የሚዘጋጅ።", en: "Tender beef chunks sautéed and mixed with shredded injera." }, image: "https://images.unsplash.com/photo-1565299585323-38d6b0865b47?w=500" },
            { id: 6, name: { am: "ሽሮ ወጥ", en: "Shiro Wat" }, category: "fasting", price: 130.00, time: "15 min", desc: { am: "በልዩ ቅመም የተፈጨ ሽሮ ከበርበሬ ጋር።", en: "Traditional thick chickpea flour stew." }, image: "https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=500" },
            { id: 7, name: { am: "ቺዝ በርገር", en: "Cheese Burger" }, category: "non-fasting", price: 350.00, time: "15 min", desc: { am: "ጭማቂ የበሬ ስጋ ፓቲ ከቺዝ እና ሰላጣ ጋር።", en: "Juicy beef patty with melted cheese and fresh lettuce." }, image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500" },
            { id: 8, name: { am: "ፔፔሮኒ ፒዛ", en: "Pepperoni Pizza" }, category: "non-fasting", price: 650.00, time: "25 min", desc: { am: "ትኩስ ሞዞሬላ ቺዝ እና ፔፔሮኒ የተጨመረበት ጣፋጭ ፒዛ።", en: "Classic pizza topped with mozzarella cheese and pepperoni." }, image: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500" },
            { id: 9, name: { am: "ስፓጌቲ ቦሎኛዝ", en: "Spaghetti Bolognese" }, category: "non-fasting", price: 320.00, time: "20 min", desc: { am: "ጣፋጭ የጣሊያን ስፓጌቲ ከስጋ ሶስ ጋር።", en: "Classic Italian pasta served with rich meat sauce." }, image: "https://images.unsplash.com/photo-1621996346565-e3d5d6281298?w=500" },
            { id: 10, name: { am: "ክለብ ሳንድዊች", en: "Club Sandwich" }, category: "breakfast", price: 220.00, time: "10 min", desc: { am: "በዶሮ ስጋ፣ እንቁላል እና ቲማቲም የተሞላ ባለ ሶስት ሽፋን ሳንድዊች።", en: "Triple-layer sandwich with chicken, egg, and fresh veggies." }, image: "https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=500" },
            { id: 11, name: { am: "እንቁላል ሳንድዊች", en: "Egg Sandwich" }, category: "breakfast", price: 90.00, time: "10 min", desc: { am: "ትኩስ ዳቦ እና የተጠበሰ እንቁላል ለቁርስ።", en: "Fresh toasted bread served with fried egg." }, image: "https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500" },
            { id: 12, name: { am: "አቮካዶ ጁስ", en: "Avocado Juice" }, category: "drink", price: 120.00, time: "10 min", desc: { am: "ከተፈጥሮ አቮካዶ የተሰራ ንጹህ የጾም ጁስ።", en: "Fresh and pure fasting avocado juice." }, image: "https://images.unsplash.com/photo-1556881286-fc6915169721?w=500" },
            { id: 13, name: { am: "ማንጎ ጁስ", en: "Mango Juice" }, category: "drink", price: 110.00, time: "10 min", desc: { am: "ትኩስ የማንጎ ፍሬ የተጨመቀ ጤናማ መጠጥ።", en: "Freshly squeezed sweet mango juice." }, image: "https://images.unsplash.com/photo-1546173159-315724a31696?w=500" },
            { id: 14, name: { am: "የተጠበሰ ድንች (French Fries)", en: "French Fries" }, category: "fasting", price: 130.00, time: "10 min", desc: { am: "ወርቃማ እና ጥርት ያለ የተጠበሰ ድንች።", en: "Crispy golden french fries." }, image: "https://images.unsplash.com/photo-1573080496219-bb080dd4f877?w=500" }
        ];

        let cart = [];
        let currentFilter = 'all';

        // 🔊 Alert Sound Synth
        function playBeepSound() {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(880, ctx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(440, ctx.currentTime + 0.6);
                gain.gain.setValueAtTime(0.3, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.6);
                osc.connect(gain);
                gain.connect(ctx.destination);
                osc.start();
                osc.stop(ctx.currentTime + 0.6);
            } catch(e){}
        }

        function toggleLanguage() {
            currentLang = currentLang === 'am' ? 'en' : 'am';
            document.getElementById('lang-btn-text').innerText = currentLang === 'am' ? 'English' : 'አማርኛ';
            document.getElementById('search-input').placeholder = translations[currentLang].searchPlaceholder;
            document.getElementById('nav-menu').innerText = translations[currentLang].navMenu;
            document.getElementById('nav-orders').innerText = translations[currentLang].navOrders;
            document.getElementById('cart-sidebar-title').innerText = translations[currentLang].cartTitle;
            document.getElementById('table-label').innerText = translations[currentLang].tableLabel;
            document.getElementById('note-label').innerText = translations[currentLang].noteLabel;
            document.getElementById('total-text').innerText = translations[currentLang].totalText;
            document.getElementById('order-btn-text').innerText = translations[currentLang].orderBtn;

            document.querySelectorAll('.cat-btn').forEach(btn => {
                const catKey = btn.getAttribute('data-cat');
                if (catKey && translations[currentLang].categories[catKey]) {
                    btn.innerText = translations[currentLang].categories[catKey];
                }
            });

            filterMenu(currentFilter);
            updateCartUI();
        }

        function filterMenu(category) {
            currentFilter = category;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                btn.classList.remove('bg-slate-900', 'text-amber-400', 'shadow-lg');
                btn.classList.add('bg-white', 'text-slate-600');
            });
            const activeBtn = document.querySelector(`.cat-btn[data-cat="${category}"]`);
            if (activeBtn) {
                activeBtn.classList.add('bg-slate-900', 'text-amber-400', 'shadow-lg');
                activeBtn.classList.remove('bg-white', 'text-slate-600');
            }
            const filtered = category === 'all' ? menuItems : menuItems.filter(item => item.category === category);
            renderGrid(filtered);
        }

        function searchMenu() {
            const query = document.getElementById('search-input').value.toLowerCase();
            const filtered = menuItems.filter(item =>
                item.name.en.toLowerCase().includes(query) || item.name.am.toLowerCase().includes(query)
            );
            renderGrid(filtered);
        }

        function renderGrid(items) {
            const container = document.getElementById('menu-container');
            container.innerHTML = items.map(item => `
                <div onclick="openDetail(${item.id})" class="bg-white rounded-3xl p-3 shadow-sm hover:shadow-xl transition-all duration-300 cursor-pointer flex items-center gap-3.5 border border-slate-100 hover:border-amber-200 active:scale-[0.98] group">
                    <div class="relative overflow-hidden rounded-2xl w-20 h-20 shrink-0">
                        <img src="${item.image}" alt="" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500">
                    </div>
                    <div class="flex-grow">
                        <h4 class="font-extrabold text-xs text-slate-900 line-clamp-1">${item.name[currentLang]}</h4>
                        <p class="text-[11px] text-slate-500 line-clamp-1 my-1">${item.desc[currentLang]}</p>
                        <div class="text-emerald-700 font-black text-xs">${item.price.toFixed(2)} ETB</div>
                    </div>
                    <button onclick="event.stopPropagation(); addToCart(${item.id})" class="luxury-gradient-btn text-white w-9 h-9 rounded-2xl font-bold shadow-md hover:scale-105 transition shrink-0 flex items-center justify-center active:scale-95">
                        <i class="fa-solid fa-plus text-xs"></i>
                    </button>
                </div>
            `).join('');
        }

        function openDetail(id) {
            const item = menuItems.find(p => p.id === id);
            document.getElementById('modal-img').src = item.image;
            document.getElementById('modal-title').innerText = item.name[currentLang];
            document.getElementById('modal-price').innerText = item.price.toFixed(2) + " ETB";
            document.getElementById('modal-time').innerText = item.time;
            document.getElementById('modal-desc').innerText = item.desc[currentLang];

            document.getElementById('modal-add-btn').onclick = function() {
                addToCart(item.id);
                closeModal();
            };
            document.getElementById('detail-modal').classList.remove('hidden');
            document.getElementById('detail-modal').classList.add('flex');
        }

        function closeModal() {
            document.getElementById('detail-modal').classList.remove('flex');
            document.getElementById('detail-modal').classList.add('hidden');
        }

        function addToCart(id) {
            const item = menuItems.find(p => p.id === id);
            const existing = cart.find(p => p.id === id);
            if (existing) {
                existing.qty += 1;
            } else {
                cart.push({ ...item, qty: 1 });
            }
            updateCartUI();
            toggleCart();
        }

        function changeQty(index, delta) {
            cart[index].qty += delta;
            if (cart[index].qty <= 0) cart.splice(index, 1);
            updateCartUI();
        }

        function updateCartUI() {
            const totalCount = cart.reduce((sum, item) => sum + item.qty, 0);
            document.getElementById('cart-count').innerText = totalCount;
            const container = document.getElementById('cart-items');

            if (cart.length === 0) {
                container.innerHTML = `<p class='text-slate-400 text-center py-10 text-xs font-semibold'>${translations[currentLang].emptyCart}</p>`;
                document.getElementById('total-price').innerText = "0.00 ETB";
                return;
            }

            let total = 0;
            container.innerHTML = cart.map((item, index) => {
                total += item.price * item.qty;
                return `
                    <div class="flex justify-between items-center bg-slate-50 p-3 rounded-2xl border border-slate-100">
                        <div>
                            <h5 class="font-bold text-xs text-slate-900">${item.name[currentLang]}</h5>
                            <p class="text-[11px] text-emerald-700 font-extrabold">${(item.price * item.qty).toFixed(2)} ETB</p>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="changeQty(${index}, -1)" class="w-6 h-6 bg-slate-200 rounded-lg font-bold text-xs flex items-center justify-center hover:bg-slate-300">-</button>
                            <span class="text-xs font-black">${item.qty}</span>
                            <button onclick="changeQty(${index}, 1)" class="w-6 h-6 bg-emerald-700 text-white rounded-lg font-bold text-xs flex items-center justify-center hover:bg-emerald-800">+</button>
                        </div>
                    </div>
                `;
            }).join('');

            document.getElementById('total-price').innerText = total.toFixed(2) + " ETB";
        }

        function toggleCart() {
            document.getElementById('cart-sidebar').classList.toggle('translate-x-full');
        }

        function setStatus(text, colorClass, showSpinner = false) {
            const el = document.getElementById('order-status');
            el.innerHTML = showSpinner ? `<span class="spinner mr-1.5"></span> ${text}` : text;
            el.className = `text-center text-xs mt-2 ${colorClass}`;
            el.classList.remove('hidden');
        }

        // 🔥 Order Checkout Function
        async function checkout() {
            if (cart.length === 0) {
                alert(translations[currentLang].selectItemsAlert);
                return;
            }

            const tableNum = document.getElementById('table-number').value.trim();
            if (!tableNum) {
                alert(translations[currentLang].enterTableAlert);
                return;
            }

            const note = document.getElementById('order-note').value.trim();
            const orderId = Math.floor(1000 + Math.random() * 9000);

            let total = 0;
            let message = `🛒 <b>አዲስ ትዕዛዝ / NEW LUXURY ORDER #${orderId}</b>\n\n`;
            message += `📍 <b>ጠረጴዛ / Table #:</b> ${tableNum}\n`;
            if (note) message += `📝 <b>ማስታወሻ / Note:</b> ${note}\n`;
            message += `-----------------------------\n`;

            cart.forEach((item, index) => {
                let itemTotal = item.price * item.qty;
                total += itemTotal;
                message += `${index + 1}. ${item.name.am} (${item.qty}x) - ${itemTotal.toFixed(2)} ETB\n`;
            });

            message += `-----------------------------\n`;
            message += `💰 <b>አጠቃላይ ዋጋ / Total:</b> ${total.toFixed(2)} ETB`;

            const checkoutBtn = document.getElementById('checkout-btn');
            checkoutBtn.disabled = true;
            checkoutBtn.classList.add('opacity-60', 'cursor-not-allowed');
            setStatus(translations[currentLang].sending, 'text-slate-500 font-semibold', true);

            const formData = new FormData();
            formData.append('chat_id', CHAT_ID);
            formData.append('text', message);
            formData.append('parse_mode', 'HTML');

            try {
                let response = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
                    method: 'POST',
                    body: formData
                });

                let data = await response.json();

                if (data.ok) {
                    setStatus(translations[currentLang].sent, 'text-emerald-700 font-extrabold', false);
                    alert(translations[currentLang].sent);

                    // 🚨 Start Live Delay Tracking Timer (Set for 15 Minutes = 900 seconds)
                    activeOrder = {
                        id: orderId,
                        table: tableNum,
                        startTime: Date.now(),
                        maxSeconds: 900, // 15 Min timer (ለሙከራ መቀነስ ይቻላል)
                        alerted: false
                    };
                    localStorage.setItem('luxury_active_order', JSON.stringify(activeOrder));
                    startDelayTracker();

                    cart = [];
                    updateCartUI();
                    document.getElementById('order-note').value = '';
                    document.getElementById('table-number').value = '';
                    setTimeout(() => toggleCart(), 1200);
                } else {
                    setStatus(`እገዳ፡ ${data.description || 'ለግሩፑ መላክ አልተቻለም'}`, 'text-rose-600 font-bold', false);
                    alert(`የቴሌግራም ስህተት፡ ${data.description}`);
                }
            } catch (error) {
                setStatus(translations[currentLang].failed, 'text-rose-600 font-bold', false);
                alert("የኢንተርኔት ግንኙነት ችግር አጋጥሟል።");
            } finally {
                checkoutBtn.disabled = false;
                checkoutBtn.classList.remove('opacity-60', 'cursor-not-allowed');
            }
        }

        // ⏱ Live Order Tracker & Automatic Delay Alert Engine
        let trackerInterval = null;

        function startDelayTracker() {
            if (!activeOrder) return;
            const banner = document.getElementById('live-order-banner');
            banner.classList.remove('hidden');

            if (trackerInterval) clearInterval(trackerInterval);

            trackerInterval = setInterval(() => {
                const elapsedSeconds = Math.floor((Date.now() - activeOrder.startTime) / 1000);
                const remainingSeconds = activeOrder.maxSeconds - elapsedSeconds;

                if (remainingSeconds > 0) {
                    const mins = Math.floor(remainingSeconds / 60);
                    const secs = remainingSeconds % 60;
                    document.getElementById('active-order-timer').innerText = `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
                } else {
                    // 🚨 Order Timer Expired -> Trigger Automatic Delay Sound & Modal
                    document.getElementById('active-order-timer').innerText = "00:00 - DELAYED!";
                    document.getElementById('active-order-status-text').innerText = "🚨 ትዕዛዝዎ ዘግይቷል!";

                    if (!activeOrder.alerted) {
                        activeOrder.alerted = true;
                        localStorage.setItem('luxury_active_order', JSON.stringify(activeOrder));
                        playBeepSound();
                        triggerDelayAlertModal();
                    }
                }
            }, 1000);
        }

        function triggerDelayAlertModal() {
            document.getElementById('delay-alert-title').innerText = translations[currentLang].delayTitle;
            document.getElementById('delay-alert-msg').innerText = translations[currentLang].delayMsg;
            document.getElementById('delay-alert-modal').classList.remove('hidden');
            document.getElementById('delay-alert-modal').classList.add('flex');
        }

        function closeDelayModal() {
            document.getElementById('delay-alert-modal').classList.remove('flex');
            document.getElementById('delay-alert-modal').classList.add('hidden');
        }

        // 🚨 Send Urgent Delay Notification to Telegram Waiter Group
        async function sendUrgentDelayNotification() {
            if (!activeOrder) return;

            const urgentBtn = document.getElementById('urgent-btn');
            urgentBtn.disabled = true;
            urgentBtn.innerText = "ጥሪ በመላክ ላይ...";

            let urgentMsg = `🚨 <b>አስቸኳይ/URGENT: የትዕዛዝ መዘግየት ማስጠንቀቂያ!</b>\n\n`;
            urgentMsg += `📍 <b>ጠረጴዛ / Table #:</b> ${activeOrder.table}\n`;
            urgentMsg += `🆔 <b>ትዕዛዝ #:</b> #${activeOrder.id}\n`;
            urgentMsg += `⚠️ ደንበኛው ትዕዛዙ እንደዘገየበት ገልጿል። እባክዎ አሁኑኑ ያረጋግጡ!`;

            const formData = new FormData();
            formData.append('chat_id', CHAT_ID);
            formData.append('text', urgentMsg);
            formData.append('parse_mode', 'HTML');

            try {
                let res = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, { method: 'POST', body: formData });
                let data = await res.json();
                if (data.ok) {
                    alert(translations[currentLang].delaySent);
                    closeDelayModal();
                } else {
                    alert("ጥሪ መላክ አልተቻለም።");
                }
            } catch(e) {
                alert("የኢንተርኔት ግንኙነት ችግር።");
            } finally {
                urgentBtn.disabled = false;
                urgentBtn.innerText = "ለአስተናጋጅ አሁኑኑ ጥሪ ላክ!";
            }
        }

        // Initialize Page
        filterMenu('all');
        updateCartUI();
        if (activeOrder) startDelayTracker();
    </script>
</body>
</html>
