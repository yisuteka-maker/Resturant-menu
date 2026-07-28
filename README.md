<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>LUXURA - International & Traditional Fine Dining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&family=Playfair+Display:ital,wght@0,600;1,400&display=swap');
        
        * { box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
        .font-serif-luxury { font-family: 'Playfair Display', serif; }
        body { background-color: #030712; margin: 0; padding: 0; overflow-x: hidden; color: #f3f4f6; }
        
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

        /* Luxury Glassmorphism & Micro-animations */
        .glass-header {
            background: rgba(15, 23, 42, 0.85);
            backdrop-filter: blur(16px);
            border-bottom: 1px solid rgba(212, 175, 55, 0.2);
        }

        .gold-border-glow {
            border: 1px solid rgba(245, 158, 11, 0.3);
            box-shadow: 0 0 20px rgba(245, 158, 11, 0.1);
        }

        .luxury-btn-gold {
            background: linear-gradient(135deg, #d97706 0%, #b45309 50%, #78350f 100%);
            box-shadow: 0 8px 20px -4px rgba(217, 119, 6, 0.5);
        }

        .luxury-btn-gold:active {
            transform: scale(0.95);
            box-shadow: 0 4px 10px -2px rgba(217, 119, 6, 0.7);
        }

        .luxury-btn-emerald {
            background: linear-gradient(135deg, #059669 0%, #047857 50%, #064e3b 100%);
            box-shadow: 0 8px 20px -4px rgba(5, 150, 105, 0.4);
        }

        .luxury-btn-emerald:active { transform: scale(0.95); }

        .pulse-alarm { animation: pulse-red 1.5s infinite; }
        @keyframes pulse-red {
            0% { box-shadow: 0 0 0 0 rgba(225, 29, 72, 0.7); }
            70% { box-shadow: 0 0 0 16px rgba(225, 29, 72, 0); }
            100% { box-shadow: 0 0 0 0 rgba(225, 29, 72, 0); }
        }

        .spinner {
            border: 2px solid #f3f3f3;
            border-top: 2px solid #d97706;
            border-radius: 50%;
            width: 16px;
            height: 16px;
            animation: spin 0.8s linear infinite;
            display: inline-block;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body class="bg-slate-950 flex justify-center items-center min-h-screen p-0 sm:p-4">

    <!-- Main App Container -->
    <div class="w-full max-w-md bg-slate-900 shadow-2xl overflow-hidden relative flex flex-col h-screen sm:h-[92vh] sm:rounded-[44px] border border-amber-500/20">

        <!-- Luxury Header -->
        <header class="p-4 glass-header text-white flex justify-between items-center z-20 shrink-0 sticky top-0">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-2xl bg-gradient-to-tr from-amber-400 via-amber-600 to-amber-700 flex items-center justify-center text-slate-950 font-black shadow-lg shadow-amber-500/20">
                    <i class="fa-solid fa-crown text-base"></i>
                </div>
                <div>
                    <h1 class="text-base font-extrabold tracking-tight text-amber-100 font-serif-luxury leading-none">LUXURA</h1>
                    <span class="text-[9px] text-amber-400/90 font-medium tracking-widest uppercase">Fine Dining & Lounge</span>
                </div>
            </div>

            <div class="flex items-center gap-2">
                <!-- Call Waiter Quick Button 🛎️ -->
                <button onclick="openCallWaiterModal()" class="bg-rose-600/90 hover:bg-rose-600 text-white border border-rose-400/40 px-3 py-1.5 rounded-xl text-xs font-bold transition flex items-center gap-1.5 shadow-lg active:scale-95 animate-pulse">
                    <i class="fa-solid fa-bell text-xs"></i>
                    <span id="call-waiter-btn-text">አስተናጋጅ</span>
                </button>

                <!-- Language Toggle -->
                <button onclick="toggleLanguage()" class="bg-slate-800 hover:bg-slate-700 text-amber-400 border border-amber-500/30 px-2.5 py-1.5 rounded-xl text-xs font-bold transition flex items-center gap-1 active:scale-95">
                    <i class="fa-solid fa-globe"></i>
                    <span id="lang-btn-text">EN</span>
                </button>

                <!-- Cart Button -->
                <button onclick="toggleCart()" class="luxury-btn-gold text-slate-950 p-2.5 rounded-xl transition relative active:scale-95 flex items-center justify-center font-bold">
                    <i class="fa-solid fa-bag-shopping text-base"></i>
                    <span id="cart-count" class="absolute -top-1.5 -right-1.5 bg-rose-600 text-white text-[10px] w-5 h-5 rounded-full flex items-center justify-center font-black ring-2 ring-slate-900 shadow-md">0</span>
                </button>
            </div>
        </header>

        <!-- Live Order Delay Tracking Banner -->
        <div id="live-order-banner" class="hidden bg-gradient-to-r from-amber-600 to-orange-600 text-slate-950 px-4 py-2 flex justify-between items-center text-xs font-bold shadow-inner cursor-pointer" onclick="triggerDelayAlertModal()">
            <div class="flex items-center gap-2">
                <span class="w-2 h-2 rounded-full bg-slate-950 animate-ping"></span>
                <span id="active-order-status-text">ትዕዛዝዎ በመዘጋጀት ላይ ነው...</span>
            </div>
            <div class="bg-slate-950 text-amber-400 px-2.5 py-0.5 rounded-lg text-[11px] font-mono" id="active-order-timer">15:00</div>
        </div>

        <!-- Scrollable Body -->
        <main class="flex-grow overflow-y-auto p-4 space-y-4 pb-28">

            <!-- Search Bar -->
            <div class="relative">
                <i class="fa-solid fa-magnifying-glass absolute left-4 top-3.5 text-amber-500/60 text-sm"></i>
                <input type="text" id="search-input" oninput="searchMenu()" placeholder="የሚወዱትን ምግብ ይፈልጉ..." class="w-full bg-slate-800/80 text-amber-100 placeholder-slate-400 pl-11 pr-4 py-3 rounded-2xl text-xs font-medium border border-amber-500/20 focus:outline-none focus:ring-2 focus:ring-amber-500/50 shadow-inner transition">
            </div>

            <!-- Luxury Categories Filter -->
            <div class="flex gap-2 overflow-x-auto no-scrollbar pb-1">
                <button onclick="filterMenu('all')" data-cat="all" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-gradient-to-r from-amber-500 to-amber-700 text-slate-950 shadow-lg border border-amber-400/40 whitespace-nowrap transition-all duration-300">ሁሉም</button>
                <button onclick="filterMenu('habesha')" data-cat="habesha" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">የሀበሻ</button>
                <button onclick="filterMenu('western')" data-cat="western" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">የውጭ (International)</button>
                <button onclick="filterMenu('fasting')" data-cat="fasting" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">ጾም</button>
                <button onclick="filterMenu('breakfast')" data-cat="breakfast" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">ቁርስ</button>
                <button onclick="filterMenu('drink')" data-cat="drink" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">መጠጥና ዴዘርት</button>
            </div>

            <!-- Food Items Grid -->
            <div id="menu-container" class="grid grid-cols-1 gap-3.5"></div>
        </main>

        <!-- Bottom Navigation -->
        <nav class="absolute bottom-0 left-0 right-0 bg-slate-950/95 backdrop-blur-xl border-t border-amber-500/20 py-3 px-6 flex justify-around items-center text-slate-400 z-20 shrink-0">
            <button onclick="filterMenu('all')" class="text-amber-400 flex flex-col items-center text-xs font-bold w-1/3 transition transform active:scale-95">
                <i class="fa-solid fa-utensils text-lg mb-1"></i>
                <span id="nav-menu">ሜኑ</span>
            </button>
            <button onclick="openCallWaiterModal()" class="text-rose-400 hover:text-rose-300 flex flex-col items-center text-xs font-bold w-1/3 transition transform active:scale-95">
                <i class="fa-solid fa-bell text-lg mb-1"></i>
                <span>አስተናጋጅ ጥራ</span>
            </button>
            <button onclick="toggleCart()" class="hover:text-amber-400 flex flex-col items-center text-xs font-semibold w-1/3 transition transform active:scale-95">
                <i class="fa-solid fa-receipt text-lg mb-1"></i>
                <span id="nav-orders">ትዕዛዞች</span>
            </button>
        </nav>
    </div>

    <!-- Call Waiter Modal 🛎️ -->
    <div id="call-waiter-modal" class="fixed inset-0 bg-slate-950/85 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-amber-500/30 rounded-3xl max-w-sm w-full p-6 text-center shadow-2xl relative">
            <button onclick="closeCallWaiterModal()" class="absolute right-4 top-4 w-8 h-8 bg-slate-800 text-slate-400 rounded-full flex items-center justify-center font-bold">✕</button>
            <div class="w-16 h-16 bg-amber-500/10 text-amber-400 rounded-full flex items-center justify-center text-3xl mx-auto mb-3 border border-amber-500/30">
                🛎️
            </div>
            <h3 class="text-lg font-black text-amber-100 mb-1" id="waiter-modal-title">አስተናጋጅ መጠራት ይፈልጋሉ?</h3>
            <p class="text-xs text-slate-400 mb-4" id="waiter-modal-desc">እባክዎ የጠረጴዛዎን ቁጥር ያስገቡ፤ አስተናጋጅ ወዲያውኑ ወደ እርሶ ይመጣል።</p>
            
            <input type="number" id="waiter-table-num" placeholder="የጠረጴዛ ቁጥር (ለምሳሌ: 5)" class="w-full bg-slate-800 border border-amber-500/30 text-amber-100 px-4 py-3 rounded-2xl text-xs text-center font-bold mb-4 focus:outline-none focus:ring-2 focus:ring-amber-500">

            <button onclick="sendWaiterCall()" id="waiter-send-btn" class="w-full luxury-btn-gold text-slate-950 font-black py-3.5 rounded-2xl text-xs shadow-lg transition flex items-center justify-center gap-2 active:scale-95">
                <i class="fa-solid fa-paper-plane"></i>
                <span>አስተናጋጅ አሁኑኑ ጥራ</span>
            </button>
        </div>
    </div>

    <!-- Food Detail Modal -->
    <div id="detail-modal" class="fixed inset-0 bg-slate-950/80 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-amber-500/30 rounded-3xl max-w-sm w-full p-5 relative shadow-2xl flex flex-col max-h-[85vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-3">
                <button onclick="closeModal()" class="w-9 h-9 bg-slate-800 text-slate-300 rounded-full flex items-center justify-center font-bold hover:bg-slate-700 transition"><i class="fa-solid fa-xmark"></i></button>
                <div class="w-9 h-9 bg-amber-500/10 text-amber-400 rounded-full flex items-center justify-center font-bold border border-amber-500/20"><i class="fa-solid fa-crown text-xs"></i></div>
            </div>
            <img id="modal-img" src="" alt="" class="w-full h-52 object-cover rounded-2xl mb-4 shadow-lg border border-slate-800">

            <div class="flex justify-between items-start mb-2">
                <h3 id="modal-title" class="text-lg font-black text-amber-100 leading-snug"></h3>
                <div class="text-amber-400 font-extrabold text-lg" id="modal-price"></div>
            </div>

            <div class="flex items-center gap-4 text-xs font-semibold text-slate-400 mb-3">
                <span><i class="fa-regular fa-clock text-amber-400"></i> <span id="modal-time">15 min</span></span>
                <span id="modal-stars" class="text-amber-400">★★★★★</span>
            </div>

            <p id="modal-desc" class="text-xs text-slate-300 leading-relaxed mb-5 bg-slate-800/60 p-3.5 rounded-2xl border border-slate-800"></p>

            <div class="mt-auto pt-2">
                <button id="modal-add-btn" class="w-full luxury-btn-gold text-slate-950 py-3.5 rounded-2xl font-extrabold shadow-lg transition text-xs flex items-center justify-center gap-2">
                    <i class="fa-solid fa-cart-plus"></i>
                    <span>ወደ ጋሪ ጨምር</span>
                </button>
            </div>
        </div>
    </div>

    <!-- Active Delayed Order Alert Modal 🚨 -->
    <div id="delay-alert-modal" class="fixed inset-0 bg-slate-950/90 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 rounded-3xl max-w-sm w-full p-6 text-center shadow-2xl border-2 border-rose-600 pulse-alarm relative">
            <div class="w-16 h-16 bg-rose-500/10 text-rose-500 rounded-full flex items-center justify-center text-3xl mx-auto mb-3 border border-rose-500/30">
                🚨
            </div>
            <h3 class="text-lg font-black text-white mb-1" id="delay-alert-title">ትዕዛዝዎ ዘግይቷል!</h3>
            <p class="text-xs text-slate-400 mb-4" id="delay-alert-msg">ትዕዛዝዎ ከተሰጠው ዝግጅት ጊዜ በላይ ወስዷል። እባክዎ ለአስተናጋጆች ጥሪ ይላኩ።</p>
            
            <div class="space-y-2">
                <button onclick="sendUrgentDelayNotification()" id="urgent-btn" class="w-full bg-rose-600 hover:bg-rose-700 text-white font-extrabold py-3.5 rounded-2xl text-xs shadow-lg transition flex items-center justify-center gap-2 active:scale-95">
                    <i class="fa-solid fa-bell"></i>
                    <span>ለአስተናጋጅ አሁኑኑ ጥሪ ላክ!</span>
                </button>
                <button onclick="closeDelayModal()" class="w-full bg-slate-800 text-slate-300 font-bold py-2.5 rounded-xl text-xs transition">
                    ዝጋ (Dismiss)
                </button>
            </div>
        </div>
    </div>

    <!-- Shopping Cart Sidebar -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-full sm:w-80 bg-slate-900 border-l border-amber-500/20 shadow-2xl p-5 transform translate-x-full transition-transform duration-300 z-50 flex flex-col">
        <div class="flex justify-between items-center mb-4 border-b border-slate-800 pb-3">
            <h3 class="text-base font-extrabold text-amber-100" id="cart-sidebar-title">የመረጧቸው እቃዎች</h3>
            <button onclick="toggleCart()" class="w-8 h-8 rounded-full bg-slate-800 text-slate-300 font-bold text-sm flex items-center justify-center hover:bg-slate-700">✕</button>
        </div>

        <div class="mb-3">
            <label class="block text-xs font-bold text-slate-300 mb-1" id="table-label">የጠረጴዛ ቁጥር (Table Number):</label>
            <input type="number" id="table-number" placeholder="ምሳሌ: 4" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
        </div>

        <div class="mb-3">
            <label class="block text-xs font-bold text-slate-300 mb-1" id="note-label">ልዩ ማስታወሻ (Special Note):</label>
            <input type="text" id="order-note" placeholder="ለምሳሌ: ያለ በርበሬ ይሁን..." class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-2.5 pr-1"></div>

        <div class="border-t border-slate-800 pt-4 mt-2">
            <div class="flex justify-between font-extrabold text-sm mb-4">
                <span id="total-text" class="text-slate-400">አጠቃላይ ዋጋ:</span>
                <span id="total-price" class="text-amber-400 text-base">0.00 ETB</span>
            </div>
            <button id="checkout-btn" onclick="checkout()" class="w-full luxury-btn-gold text-slate-950 py-3.5 rounded-2xl font-extrabold shadow-xl transition text-xs flex items-center justify-center gap-2 active:scale-95">
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
                headerTitle: "LUXURA", searchPlaceholder: "Search luxury habesha & international meals...", navMenu: "Menu", navOrders: "Orders",
                addToCart: "Add to Cart", cartTitle: "Your Order Bag",
                tableLabel: "Table Number:", noteLabel: "Special Request:", totalText: "Total Amount:",
                orderBtn: "Send Order to Kitchen", emptyCart: "Your bag is empty",
                sending: "Transmitting order...", sent: "Order sent to kitchen! 🎉", failed: "Could not send. Check internet.",
                enterTableAlert: "Please enter your Table Number!", selectItemsAlert: "Please select items first!",
                delayTitle: "Order Delayed! 🚨", delayMsg: "Your order is taking longer than expected. Tap below to alert staff immediately.",
                delaySent: "Urgent alert sent to staff! 🚨", callWaiterBtn: "Call Waiter",
                waiterTitle: "Call Waiter Service", waiterDesc: "Enter table number to summon your personal waiter.",
                categories: { all: "All", habesha: "Habesha Special", western: "International", fasting: "Fasting", breakfast: "Breakfast", drink: "Drinks & Desserts" }
            },
            am: {
                headerTitle: "LUXURA", searchPlaceholder: "የሚወዱትን የሀበሻ እና የውጭ ምግብ ይፈልጉ...", navMenu: "ሜኑ", navOrders: "ትዕዛዞች",
                addToCart: "ወደ ጋሪ ጨምር", cartTitle: "የመረጧቸው እቃዎች",
                tableLabel: "የጠረጴዛ ቁጥር (Table Number):", noteLabel: "ልዩ ማስታወሻ (Special Note):", totalText: "አጠቃላይ ዋጋ:",
                orderBtn: "ትዕዛዝ በቦት ላክ", emptyCart: "ጋሪዎ ባዶ ነው",
                sending: "ትዕዛዝዎ በመላክ ላይ...", sent: "ትዕዛዝዎ ወደ አስተናጋጆች በተሳካ ሁኔታ ተልኳል! 🎉", failed: "ትዕዛዙ አልተላከም። እባክዎ እንደገና ይሞክሩ።",
                enterTableAlert: "እባክዎ የጠረጴዛ ቁጥር ያስገቡ!", selectItemsAlert: "እባክዎ መጀመሪያ ምግብ ይምረጡ!",
                delayTitle: "ትዕዛዝዎ ዘግይቷል! 🚨", delayMsg: "ትዕዛዝዎ ከተሰጠው ዝግጅት ጊዜ በላይ ወስዷል። ለአስተናጋጆች አሁኑኑ ጥሪ ይላኩ።",
                delaySent: "ለአስተናጋጆች አስቸኳይ ጥሪ ተልኳል! 🚨", callWaiterBtn: "አስተናጋጅ",
                waiterTitle: "አስተናጋጅ መጠራት ይፈልጋሉ?", waiterDesc: "እባክዎ የጠረጴዛዎን ቁጥር ያስገቡ፤ አስተናጋጅ ወዲያውኑ ይመጣል።",
                categories: { all: "ሁሉም", habesha: "የሀበሻ", western: "የውጭ (International)", fasting: "ጾም", breakfast: "ቁርስ", drink: "መጠጥና ዴዘርት" }
            }
        };

        // 🍽️ Expanded International & Habesha Luxury Menu
        const menuItems = [
            // --- HABESHA SPECIALS ---
            { id: 1, name: { am: "ልዩ ዶሮ ወጥ", en: "Royal Doro Wat" }, category: "habesha", price: 650.00, time: "25 min", desc: { am: "በንጹህ አገር ቤት ቅቤ፣ በሀበሻ እንቁላል እና በዶሮ ስጋ የተዘጋጀ ባህላዊ የፍስክ ወጥ።", en: "Traditional Ethiopian chicken stew cooked in purified spiced butter and rich berbere sauce." }, image: "https://images.unsplash.com/photo-1541544741938-0af808871cc0?w=600" },
            { id: 2, name: { am: "ክትፎ ስፔሻል (በአይብና ጎመን)", en: "Special Beef Kitfo" }, category: "habesha", price: 720.00, time: "20 min", desc: { am: "የተፈጨ ለስላሳ የበሬ ስጋ ከሚጥሚጣ፣ ንጹህ ቅቤ፣ አይብ እና ጎመን ጋር።", en: "Minced prime lean beef seasoned with mitmita, clarified butter, served with cottage cheese & greens." }, image: "https://images.unsplash.com/photo-1544025162-d76694265947?w=600" },
            { id: 3, name: { am: "የበሬ ቁልቋል ጥብስ", en: "Sizzling Ribeye Tibs" }, category: "habesha", price: 580.00, time: "20 min", desc: { am: "በትኩስ የሸክላ ድስት ላይ ከሽንኩርት፣ ቃሪያ እና ቅቤ ጋር የተጠበሰ የበሬ ስጋ።", en: "Tender ribeye beef strips sautéed with onions, rosemary, and green peppers on a hot sizzler." }, image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=600" },
            { id: 4, name: { am: "ልዩ የጾም በያይነት", en: "Royal Fasting Combo" }, category: "fasting", price: 380.00, time: "15 min", desc: { am: "የተለያዩ 9 አይነት የጾም ወጦች፣ አትክልቶች እና ሽሮ በምርጥ እንጀራ።", en: "Deluxe vegetarian platter featuring 9 distinct spiced lentil, chickpea, and vegetable dishes." }, image: "https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=600" },
            { id: 5, name: { am: "ጥብስ ፍርፍር ከእንቁላል ጋር", en: "Special Tibs Firfir" }, category: "habesha", price: 420.00, time: "15 min", desc: { am: "በተጠበሰ የበሬ ስጋ እና በቃሪያ የተዘጋጀ ጣፋጭ ፍርፍር።", en: "Shredded injera sautéed in rich spicy berbere sauce mixed with prime beef chunks." }, image: "https://images.unsplash.com/photo-1565299585323-38d6b0865b47?w=600" },
            { id: 6, name: { am: "የበግ ዱሌት ስፔሻል", en: "Special Lamb Dulet" }, category: "habesha", price: 390.00, time: "15 min", desc: { am: "በጥንቃቄ የተከተፈ የበግ ስጋ፣ ጨጓራ እና ከבד ከሚጥሚጣና ቅቤ ጋር።", en: "Finely minced lamb tripe, liver, and lean meat seasoned with mitmita and butter." }, image: "https://images.unsplash.com/photo-1603048588665-791ca8aea617?w=600" },

            // --- WESTERN & INTERNATIONAL ---
            { id: 7, name: { am: "ዋግዩ ቺዝ በርገር (Wagyu Burger)", en: "Luxury Wagyu Cheeseburger" }, category: "western", price: 680.00, time: "20 min", desc: { am: "ጭማቂ የዋግዩ ስጋ፣ የተቀለጠ ቸዳር ቺዝ እና የፈረንሳይ ድንች።", en: "Grilled Wagyu beef patty with melted cheddar cheese, caramelized onions, served with fries." }, image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=600" },
            { id: 8, name: { am: "ትራፍል ፔፔሮኒ ፒዛ (Truffle Pizza)", en: "Truffle Pepperoni Pizza" }, category: "western", price: 850.00, time: "25 min", desc: { am: "በትኩስ ሞዞሬላ ቺዝ፣ ፔፔሮኒ እና ትራፍል ኦይል የተሰራ የጣሊያን ፒዛ።", en: "Wood-fired pizza topped with mozzarella, spicy pepperoni slices, and infused truffle oil." }, image: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=600" },
            { id: 9, name: { am: "ግሪልድ ሳልመን ስቴክ (Grilled Salmon)", en: "Atlantic Grilled Salmon" }, category: "western", price: 1100.00, time: "25 min", desc: { am: "በእሳት የተጠበሰ የሳልመን አሳ ከአትክልትና ሌመን ባተር ሶስ ጋር።", en: "Pan-seared Atlantic salmon fillet served with steamed asparagus and lemon-butter sauce." }, image: "https://images.unsplash.com/photo-1467003909585-2f8a72700288?w=600" },
            { id: 10, name: { am: "ፌቱቺኒ አልፍሬዶ (Fettuccine Alfredo)", en: "Creamy Chicken Alfredo" }, category: "western", price: 540.00, time: "20 min", desc: { am: "በክሬሚ ቺዝ ሶስ እና በጥበስ የዶሮ ስጋ የተዘጋጀ የጣሊያን ፓስታ።", en: "Fettuccine pasta tossed in rich parmesan cream sauce topped with grilled chicken breast." }, image: "https://images.unsplash.com/photo-1621996346565-e3d5d6281298?w=600" },
            { id: 11, name: { am: "ክለብ ሳንድዊች ከድንች ጋር", en: "Luxury Club Sandwich" }, category: "breakfast", price: 340.00, time: "15 min", desc: { am: "ባለ 3 ፎቅ ሳንድዊች በዶሮ ስጋ፣ ቼዳር ቺዝ እና እንቁላል።", en: "Triple-decker sandwich layered with chicken, bacon, fried egg, lettuce, tomato, served with fries." }, image: "https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=600" },

            // --- DRINKS & DESSERTS ---
            { id: 12, name: { am: "ቲራሚሱ ዴዘርት (Tiramisu)", en: "Classic Italian Tiramisu" }, category: "drink", price: 290.00, time: "10 min", desc: { am: "በካፑቺኖ እና በማስካርፖኔ ቺዝ የተሰራ የጣሊያን ጣፋጭ ዴዘርት።", en: "Traditional Italian dessert made with espresso-soaked ladyfingers and mascarpone cream." }, image: "https://images.unsplash.com/photo-1571877227200-a0d98ea607e9?w=600" },
            { id: 13, name: { am: "ስፔሻል አቮካዶ ማንጎ ስሙዚ", en: "Luxury Mango Avocado Layer" }, category: "drink", price: 180.00, time: "10 min", desc: { am: "ከትኩስ አቮካዶ እና ማንጎ የተዘጋጀ ተፈጥሯዊ ጁስ።", en: "Freshly blended layered avocado and mango smoothie topped with honey and nuts." }, image: "https://images.unsplash.com/photo-1556881286-fc6915169721?w=600" },
            { id: 14, name: { am: "ኢስፕሬሶ ካፑቺኖ", en: "Double Shot Cappuccino" }, category: "drink", price: 120.00, time: "5 min", desc: { am: "በጥራት ከተቆላ የሀበሻ ቡና የተሰራ ትኩስ ካፑቺኖ።", en: "Rich double espresso topped with steamed milk froth." }, image: "https://images.unsplash.com/photo-1534778101976-62847782c213?w=600" }
        ];

        let cart = [];
        let currentFilter = 'all';

        function toggleLanguage() {
            currentLang = currentLang === 'am' ? 'en' : 'am';
            document.getElementById('lang-btn-text').innerText = currentLang === 'am' ? 'EN' : 'አማርኛ';
            document.getElementById('search-input').placeholder = translations[currentLang].searchPlaceholder;
            document.getElementById('nav-menu').innerText = translations[currentLang].navMenu;
            document.getElementById('nav-orders').innerText = translations[currentLang].navOrders;
            document.getElementById('cart-sidebar-title').innerText = translations[currentLang].cartTitle;
            document.getElementById('table-label').innerText = translations[currentLang].tableLabel;
            document.getElementById('note-label').innerText = translations[currentLang].noteLabel;
            document.getElementById('total-text').innerText = translations[currentLang].totalText;
            document.getElementById('order-btn-text').innerText = translations[currentLang].orderBtn;
            document.getElementById('call-waiter-btn-text').innerText = translations[currentLang].callWaiterBtn;

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
                btn.classList.remove('bg-gradient-to-r', 'from-amber-500', 'to-amber-700', 'text-slate-950', 'shadow-lg');
                btn.classList.add('bg-slate-800/80', 'text-slate-300');
            });
            const activeBtn = document.querySelector(`.cat-btn[data-cat="${category}"]`);
            if (activeBtn) {
                activeBtn.classList.add('bg-gradient-to-r', 'from-amber-500', 'to-amber-700', 'text-slate-950', 'shadow-lg');
                activeBtn.classList.remove('bg-slate-800/80', 'text-slate-300');
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
                <div onclick="openDetail(${item.id})" class="bg-slate-800/60 rounded-3xl p-3 shadow-md hover:shadow-xl transition-all duration-300 cursor-pointer flex items-center gap-3.5 border border-amber-500/10 hover:border-amber-500/40 active:scale-[0.98] group">
                    <div class="relative overflow-hidden rounded-2xl w-20 h-20 shrink-0 border border-slate-700">
                        <img src="${item.image}" alt="" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500">
                    </div>
                    <div class="flex-grow">
                        <h4 class="font-extrabold text-xs text-amber-100 line-clamp-1">${item.name[currentLang]}</h4>
                        <p class="text-[11px] text-slate-400 line-clamp-1 my-1">${item.desc[currentLang]}</p>
                        <div class="text-amber-400 font-black text-xs">${item.price.toFixed(2)} ETB</div>
                    </div>
                    <button onclick="event.stopPropagation(); addToCart(${item.id})" class="luxury-btn-gold text-slate-950 w-9 h-9 rounded-2xl font-black shadow-md hover:scale-105 transition shrink-0 flex items-center justify-center active:scale-95">
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
                container.innerHTML = `<p class='text-slate-500 text-center py-10 text-xs font-semibold'>${translations[currentLang].emptyCart}</p>`;
                document.getElementById('total-price').innerText = "0.00 ETB";
                return;
            }

            let total = 0;
            container.innerHTML = cart.map((item, index) => {
                total += item.price * item.qty;
                return `
                    <div class="flex justify-between items-center bg-slate-800/80 p-3 rounded-2xl border border-slate-700">
                        <div>
                            <h5 class="font-bold text-xs text-amber-100">${item.name[currentLang]}</h5>
                            <p class="text-[11px] text-amber-400 font-extrabold">${(item.price * item.qty).toFixed(2)} ETB</p>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="changeQty(${index}, -1)" class="w-6 h-6 bg-slate-700 text-slate-200 rounded-lg font-bold text-xs flex items-center justify-center active:scale-90">-</button>
                            <span class="text-xs font-black text-amber-300">${item.qty}</span>
                            <button onclick="changeQty(${index}, 1)" class="w-6 h-6 bg-amber-500 text-slate-950 rounded-lg font-bold text-xs flex items-center justify-center active:scale-90">+</button>
                        </div>
                    </div>
                `;
            }).join('');

            document.getElementById('total-price').innerText = total.toFixed(2) + " ETB";
        }

        function toggleCart() {
            document.getElementById('cart-sidebar').classList.toggle('translate-x-full');
        }

        // 🛎️ Call Waiter Modal Logic
        function openCallWaiterModal() {
            document.getElementById('waiter-modal-title').innerText = translations[currentLang].waiterTitle;
            document.getElementById('waiter-modal-desc').innerText = translations[currentLang].waiterDesc;
            document.getElementById('call-waiter-modal').classList.remove('hidden');
            document.getElementById('call-waiter-modal').classList.add('flex');
        }

        function closeCallWaiterModal() {
            document.getElementById('call-waiter-modal').classList.remove('flex');
            document.getElementById('call-waiter-modal').classList.add('hidden');
        }

        async function sendWaiterCall() {
            const tableNum = document.getElementById('waiter-table-num').value.trim();
            if (!tableNum) {
                alert(translations[currentLang].enterTableAlert);
                return;
            }

            const sendBtn = document.getElementById('waiter-send-btn');
            sendBtn.disabled = true;
            sendBtn.innerHTML = `<span class="spinner mr-1.5"></span> የመልእክት ጥሪ በመላክ ላይ...`;

            let message = `🛎️ <b>አስቸኳይ አስተናጋጅ ጥሪ / WAITER NEEDED!</b>\n\n`;
            message += `📍 <b>ጠረጴዛ / Table #:</b> ${tableNum}\n`;
            message += `⏰ <b>ሰዓት:</b> ${new Date().toLocaleTimeString()}`;

            const formData = new FormData();
            formData.append('chat_id', CHAT_ID);
            formData.append('text', message);
            formData.append('parse_mode', 'HTML');

            try {
                let res = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, { method: 'POST', body: formData });
                let data = await res.json();
                if (data.ok) {
                    alert("🛎️ አስተናጋጁ ጥሪው ደርሶታል! በአጭር ጊዜ ውስጥ ወደ ጠረጴዛዎ ይመጣል።");
                    closeCallWaiterModal();
                    document.getElementById('waiter-table-num').value = '';
                } else {
                    alert("ጥሪ መላክ አልተቻለም።");
                }
            } catch (e) {
                alert("የኢንተርኔት ግንኙነትዎን ያረጋግጡ።");
            } finally {
                sendBtn.disabled = false;
                sendBtn.innerHTML = `<i class="fa-solid fa-paper-plane"></i> <span>አስተናጋጅ አሁኑኑ ጥራ</span>`;
            }
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
            setStatus(translations[currentLang].sending, 'text-amber-400 font-semibold', true);

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
                    setStatus(translations[currentLang].sent, 'text-emerald-400 font-extrabold', false);
                    alert(translations[currentLang].sent);

                    // 🚨 Start Live Delay Tracking Timer (Set for 15 Minutes = 900 seconds)
                    activeOrder = {
                        id: orderId,
                        table: tableNum,
                        startTime: Date.now(),
                        maxSeconds: 900,
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
                    setStatus(`እገዳ፡ ${data.description}`, 'text-rose-500 font-bold', false);
                }
            } catch (error) {
                setStatus(translations[currentLang].failed, 'text-rose-500 font-bold', false);
            } finally {
                checkoutBtn.disabled = false;
                checkoutBtn.classList.remove('opacity-60', 'cursor-not-allowed');
            }
        }

        // ⏱ Live Order Tracker Engine
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
                    document.getElementById('active-order-timer').innerText = "00:00 - DELAYED!";
                    document.getElementById('active-order-status-text').innerText = "🚨 ትዕዛዝዎ ዘግይቷል!";

                    if (!activeOrder.alerted) {
                        activeOrder.alerted = true;
                        localStorage.setItem('luxury_active_order', JSON.stringify(activeOrder));
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

        async function sendUrgentDelayNotification() {
            if (!activeOrder) return;

            const urgentBtn = document.getElementById('urgent-btn');
            urgentBtn.disabled = true;

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
                }
            } catch(e) {
                alert("የኢንተርኔት ግንኙነት ችግር።");
            } finally {
                urgentBtn.disabled = false;
            }
        }

        // Initialize Page
        filterMenu('all');
        updateCartUI();
        if (activeOrder) startDelayTracker();
    </script>
</body>
</html>
