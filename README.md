<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>LUXURA - Fine Dining & Order System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&family=Playfair+Display:ital,wght@0,600;1,400&display=swap');
        
        * { box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
        .font-serif-luxury { font-family: 'Playfair Display', serif; }
        body { background-color: #030712; margin: 0; padding: 0; overflow-x: hidden; color: #f3f4f6; }
        
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

        .glass-header {
            background: rgba(15, 23, 42, 0.85);
            backdrop-filter: blur(16px);
            border-bottom: 1px solid rgba(212, 175, 55, 0.2);
        }

        .luxury-btn-gold {
            background: linear-gradient(135deg, #d97706 0%, #b45309 50%, #78350f 100%);
            box-shadow: 0 8px 20px -4px rgba(217, 119, 6, 0.5);
        }

        .luxury-btn-gold:active { transform: scale(0.95); }

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
        <header class="p-3.5 glass-header text-white flex justify-between items-center z-20 shrink-0 sticky top-0">
            <div class="flex items-center gap-2.5">
                <div class="w-9 h-9 rounded-2xl bg-gradient-to-tr from-amber-400 via-amber-600 to-amber-700 flex items-center justify-center text-slate-950 font-black shadow-lg shadow-amber-500/20">
                    <i class="fa-solid fa-crown text-sm"></i>
                </div>
                <div>
                    <h1 class="text-sm font-extrabold tracking-tight text-amber-100 font-serif-luxury leading-none">LUXURA</h1>
                    <span class="text-[8px] text-amber-400/90 font-medium tracking-widest uppercase">Fine Dining & Lounge</span>
                </div>
            </div>

            <div class="flex items-center gap-1.5">
                <!-- Profile / Admin Dashboard Button 👤 -->
                <button onclick="handleAdminButtonClick()" id="admin-profile-btn" class="bg-slate-800 hover:bg-slate-700 text-amber-400 border border-amber-500/30 w-8 h-8 rounded-xl text-xs font-bold transition flex items-center justify-center active:scale-95" title="Admin Dashboard">
                    <i class="fa-solid fa-user-shield"></i>
                </button>

                <!-- Payment Waiter Call Button 💳 -->
                <button onclick="openPaymentWaiterModal()" class="bg-emerald-600/90 hover:bg-emerald-600 text-white border border-emerald-400/40 px-2.5 py-1.5 rounded-xl text-[11px] font-bold transition flex items-center gap-1 shadow-lg active:scale-95">
                    <i class="fa-solid fa-credit-card text-xs"></i>
                    <span>ክፍያ</span>
                </button>

                <!-- Call Waiter Quick Button 🛎️ -->
                <button onclick="openCallWaiterModal()" class="bg-rose-600/90 hover:bg-rose-600 text-white border border-rose-400/40 px-2.5 py-1.5 rounded-xl text-[11px] font-bold transition flex items-center gap-1 shadow-lg active:scale-95 animate-pulse">
                    <i class="fa-solid fa-bell text-xs"></i>
                    <span>አስተናጋጅ</span>
                </button>

                <!-- Cart Button -->
                <button onclick="toggleCart()" class="luxury-btn-gold text-slate-950 p-2 rounded-xl transition relative active:scale-95 flex items-center justify-center font-bold">
                    <i class="fa-solid fa-bag-shopping text-sm"></i>
                    <span id="cart-count" class="absolute -top-1.5 -right-1.5 bg-rose-600 text-white text-[9px] w-4 h-4 rounded-full flex items-center justify-center font-black ring-2 ring-slate-900 shadow-md">0</span>
                </button>
            </div>
        </header>

        <!-- Admin Active Mode Indicator Banner -->
        <div id="admin-banner" class="hidden bg-amber-500/20 border-b border-amber-500/40 text-amber-300 px-4 py-1.5 flex justify-between items-center text-[11px] font-bold">
            <span class="flex items-center gap-1.5"><i class="fa-solid fa-lock-open text-amber-400"></i> Admin Panel Active</span>
            <button onclick="logoutAdmin()" class="bg-rose-600 text-white px-2 py-0.5 rounded-lg text-[10px] hover:bg-rose-700 transition">Logout</button>
        </div>

        <!-- Scrollable Main Content -->
        <main class="flex-grow overflow-y-auto p-4 space-y-4 pb-28">

            <!-- Search Bar -->
            <div class="relative">
                <i class="fa-solid fa-magnifying-glass absolute left-4 top-3.5 text-amber-500/60 text-sm"></i>
                <input type="text" id="search-input" oninput="searchMenu()" placeholder="የሚወዱትን ምግብ ይፈልጉ..." class="w-full bg-slate-800/80 text-amber-100 placeholder-slate-400 pl-11 pr-4 py-3 rounded-2xl text-xs font-medium border border-amber-500/20 focus:outline-none focus:ring-2 focus:ring-amber-500/50 shadow-inner transition">
            </div>

            <!-- Categories Filter -->
            <div class="flex gap-2 overflow-x-auto no-scrollbar pb-1">
                <button onclick="filterMenu('all')" data-cat="all" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-gradient-to-r from-amber-500 to-amber-700 text-slate-950 shadow-lg border border-amber-400/40 whitespace-nowrap transition-all duration-300">ሁሉም</button>
                <button onclick="filterMenu('habesha')" data-cat="habesha" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">የሀበሻ</button>
                <button onclick="filterMenu('western')" data-cat="western" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">የውጭ</button>
                <button onclick="filterMenu('fasting')" data-cat="fasting" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">ጾም</button>
                <button onclick="filterMenu('drink')" data-cat="drink" class="cat-btn px-4 py-2 rounded-2xl text-xs font-bold bg-slate-800/80 text-slate-300 border border-slate-700 whitespace-nowrap hover:bg-slate-800 transition-all duration-300">መጠጥና ዴዘርት</button>
            </div>

            <!-- Food Items Grid -->
            <div id="menu-container" class="grid grid-cols-1 gap-3.5"></div>
        </main>

        <!-- Bottom Navigation -->
        <nav class="absolute bottom-0 left-0 right-0 bg-slate-950/95 backdrop-blur-xl border-t border-amber-500/20 py-3 px-6 flex justify-around items-center text-slate-400 z-20 shrink-0">
            <button onclick="filterMenu('all')" class="text-amber-400 flex flex-col items-center text-xs font-bold w-1/3 transition transform active:scale-95">
                <i class="fa-solid fa-utensils text-lg mb-1"></i>
                <span>ሜኑ</span>
            </button>
            <button onclick="openPaymentWaiterModal()" class="text-emerald-400 hover:text-emerald-300 flex flex-col items-center text-xs font-bold w-1/3 transition transform active:scale-95">
                <i class="fa-solid fa-credit-card text-lg mb-1"></i>
                <span>ክፍያ መጠየቂያ</span>
            </button>
            <button onclick="toggleCart()" class="hover:text-amber-400 flex flex-col items-center text-xs font-semibold w-1/3 transition transform active:scale-95">
                <i class="fa-solid fa-receipt text-lg mb-1"></i>
                <span>ትዕዛዞች</span>
            </button>
        </nav>
    </div>

    <!-- 👤 ADMIN LOGIN MODAL -->
    <div id="admin-login-modal" class="fixed inset-0 bg-slate-950/85 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-amber-500/30 rounded-3xl max-w-sm w-full p-6 text-center shadow-2xl relative">
            <button onclick="closeAdminLoginModal()" class="absolute right-4 top-4 w-8 h-8 bg-slate-800 text-slate-400 rounded-full flex items-center justify-center font-bold">✕</button>
            <div class="w-14 h-14 bg-amber-500/10 text-amber-400 rounded-full flex items-center justify-center text-2xl mx-auto mb-3 border border-amber-500/30">
                <i class="fa-solid fa-user-shield"></i>
            </div>
            <h3 class="text-lg font-black text-amber-100 mb-1">Admin Login</h3>
            <p class="text-xs text-slate-400 mb-4">ወደ አድሚን ዳሽቦርድ ለመግባት መረጃ ያስገቡ።</p>

            <div class="space-y-3 mb-4 text-left">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 mb-1">Username:</label>
                    <input type="text" id="admin-username" placeholder="Admin" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 mb-1">Password:</label>
                    <input type="password" id="admin-password" placeholder="••••••••" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
            </div>

            <p id="admin-error-msg" class="text-rose-500 text-xs font-bold hidden mb-3"></p>

            <button onclick="loginAdmin()" class="w-full luxury-btn-gold text-slate-950 font-black py-3 rounded-xl text-xs shadow-lg transition flex items-center justify-center gap-2 active:scale-95">
                <i class="fa-solid fa-right-to-bracket"></i>
                <span>ግባ (Login)</span>
            </button>
        </div>
    </div>

    <!-- 📊 ADMIN DASHBOARD MODAL (ANALYTICS & MENU MANAGEMENT) -->
    <div id="admin-dashboard-modal" class="fixed inset-0 bg-slate-950/85 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-amber-500/30 rounded-3xl max-w-md w-full p-5 shadow-2xl relative max-h-[90vh] flex flex-col">
            <div class="flex justify-between items-center mb-4 border-b border-slate-800 pb-3">
                <h3 class="text-base font-black text-amber-100 flex items-center gap-2">
                    <i class="fa-solid fa-chart-line text-amber-400"></i> Admin Panel
                </h3>
                <button onclick="closeAdminDashboardModal()" class="w-8 h-8 bg-slate-800 text-slate-400 rounded-full flex items-center justify-center font-bold">✕</button>
            </div>

            <!-- Dashboard Navigation Tabs (2 Choices) -->
            <div class="flex bg-slate-800 p-1 rounded-2xl mb-4 shrink-0">
                <button onclick="switchAdminTab('analytics')" id="tab-btn-analytics" class="w-1/2 py-2 rounded-xl text-xs font-bold text-slate-950 bg-amber-500 transition">📊 1. አናሊቲክስ (Analytics)</button>
                <button onclick="switchAdminTab('menu')" id="tab-btn-menu" class="w-1/2 py-2 rounded-xl text-xs font-bold text-slate-400 transition">🍽️ 2. ሜኑ አስተካክል (Menu)</button>
            </div>

            <!-- TAB 1: ANALYTICS CONTENT -->
            <div id="tab-content-analytics" class="space-y-3 overflow-y-auto pr-1">
                <div class="grid grid-cols-2 gap-3">
                    <div class="bg-slate-800/80 p-3.5 rounded-2xl border border-amber-500/20 text-center">
                        <i class="fa-solid fa-users text-2xl text-amber-400 mb-1"></i>
                        <h4 class="text-[10px] uppercase font-bold text-slate-400">የጎብኚዎች ብዛት</h4>
                        <p id="stat-visitors" class="text-xl font-black text-amber-100">0</p>
                    </div>
                    <div class="bg-slate-800/80 p-3.5 rounded-2xl border border-emerald-500/20 text-center">
                        <i class="fa-solid fa-cart-check text-2xl text-emerald-400 mb-1"></i>
                        <h4 class="text-[10px] uppercase font-bold text-slate-400">የትዕዛዝ ብዛት</h4>
                        <p id="stat-orders" class="text-xl font-black text-emerald-300">0</p>
                    </div>
                </div>

                <div class="bg-slate-800/80 p-4 rounded-2xl border border-slate-700">
                    <h5 class="text-xs font-bold text-slate-300 mb-2 flex items-center justify-between">
                        <span>💰 አጠቃላይ የትዕዛዝ ዋጋ ድምር</span>
                        <span id="stat-revenue" class="text-amber-400 font-extrabold text-sm">0.00 ETB</span>
                    </h5>
                    <p class="text-[11px] text-slate-400 leading-relaxed">ይህ መረጃ በሲስተሙ ላይ የሚደረጉ የደንበኞችን እንቅስቃሴ በቋሚነት (Persistently) ይይዛል።</p>
                </div>
            </div>

            <!-- TAB 2: MENU MANAGEMENT CONTENT -->
            <div id="tab-content-menu" class="hidden overflow-y-auto space-y-3 pr-1 flex-grow">
                <!-- 1. ADD NEW ITEM BUTTON -->
                <button onclick="openAddItemModal()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-extrabold py-2.5 rounded-xl text-xs transition flex items-center justify-center gap-2 shadow-lg">
                    <i class="fa-solid fa-plus-circle text-sm"></i>
                    <span>1. አዲስ የምግብ/መጠጥ አይነት ጨምር (Add Item)</span>
                </button>

                <p class="text-[11px] text-slate-400 font-bold border-b border-slate-800 pb-1">ያሉ ምግቦች ዝርዝር (ለመቀየር ወይም ለመሰረዝ):</p>

                <!-- List of items with EDIT & DELETE buttons -->
                <div id="admin-items-list" class="space-y-2"></div>
            </div>
        </div>
    </div>

    <!-- ➕ 1. ADD NEW FOOD/DRINK ITEM MODAL -->
    <div id="add-item-modal" class="fixed inset-0 bg-slate-950/85 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-emerald-500/30 rounded-3xl max-w-sm w-full p-5 shadow-2xl relative">
            <button onclick="closeAddItemModal()" class="absolute right-4 top-4 w-8 h-8 bg-slate-800 text-slate-400 rounded-full flex items-center justify-center font-bold">✕</button>
            <h3 class="text-base font-black text-emerald-400 mb-3 flex items-center gap-2">
                <i class="fa-solid fa-folder-plus"></i> አዲስ ምግብ መዝግብ
            </h3>

            <div class="space-y-2.5 text-left mb-4">
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 mb-1">የምግብ/መጠጥ ስም:</label>
                    <input type="text" id="add-name" placeholder="ምሳሌ: የዶሮ ጥብስ" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3 py-2 rounded-xl text-xs font-semibold focus:outline-none">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 mb-1">ምድብ (Category):</label>
                    <select id="add-category" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3 py-2 rounded-xl text-xs font-semibold focus:outline-none">
                        <option value="habesha">የሀበሻ (Habesha)</option>
                        <option value="western">የውጭ (International)</option>
                        <option value="fasting">ጾም (Fasting)</option>
                        <option value="drink">መጠጥና ዴዘርት (Drink/Dessert)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 mb-1">ዋጋ (ETB):</label>
                    <input type="number" id="add-price" placeholder="450" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3 py-2 rounded-xl text-xs font-semibold focus:outline-none">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 mb-1">የምስል አድራሻ (Image URL):</label>
                    <input type="text" id="add-image" placeholder="https://images.unsplash.com/..." class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3 py-2 rounded-xl text-xs font-semibold focus:outline-none">
                </div>
            </div>

            <button onclick="saveNewItem()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-black py-3 rounded-xl text-xs shadow-lg transition flex items-center justify-center gap-2">
                <i class="fa-solid fa-check"></i>
                <span>አዲሱን ምግብ መዝግብ (Save)</span>
            </button>
        </div>
    </div>

    <!-- ✏️ 3. EDIT ITEM DETAILS MODAL -->
    <div id="edit-item-modal" class="fixed inset-0 bg-slate-950/85 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-amber-500/30 rounded-3xl max-w-sm w-full p-5 shadow-2xl relative">
            <button onclick="closeEditModal()" class="absolute right-4 top-4 w-8 h-8 bg-slate-800 text-slate-400 rounded-full flex items-center justify-center font-bold">✕</button>
            <h3 class="text-base font-black text-amber-100 mb-3 flex items-center gap-2">
                <i class="fa-solid fa-pen-to-square text-amber-400"></i> የምግብ መረጃ ማስተካከያ
            </h3>

            <input type="hidden" id="edit-item-id">

            <div class="space-y-2.5 text-left mb-4">
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 mb-1">የምግብ ስም:</label>
                    <input type="text" id="edit-item-name" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3 py-2 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 mb-1">ዋጋ (ETB):</label>
                    <input type="number" id="edit-item-price" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3 py-2 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 mb-1">የምስል አድራሻ (Image URL):</label>
                    <input type="text" id="edit-item-image" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3 py-2 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
            </div>

            <button onclick="saveItemEdits()" class="w-full luxury-btn-gold text-slate-950 font-black py-3 rounded-xl text-xs shadow-lg transition flex items-center justify-center gap-2 active:scale-95">
                <i class="fa-solid fa-floppy-disk"></i>
                <span>ለውጦችን መዝግብ (Save Changes)</span>
            </button>
        </div>
    </div>

    <!-- 💳 CALL WAITER FOR PAYMENT MODAL -->
    <div id="payment-waiter-modal" class="fixed inset-0 bg-slate-950/85 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-emerald-500/30 rounded-3xl max-w-sm w-full p-6 text-center shadow-2xl relative">
            <button onclick="closePaymentWaiterModal()" class="absolute right-4 top-4 w-8 h-8 bg-slate-800 text-slate-400 rounded-full flex items-center justify-center font-bold">✕</button>
            <div class="w-14 h-14 bg-emerald-500/10 text-emerald-400 rounded-full flex items-center justify-center text-2xl mx-auto mb-3 border border-emerald-500/30">
                💳
            </div>
            <h3 class="text-base font-black text-amber-100 mb-1">አስተናጋጅ ጥራ ለክፍያ</h3>
            <p class="text-xs text-slate-400 mb-4">እባክዎ የጠረጴዛዎን ቁጥር እና የክፍያ መንገድ ይምረጡ።</p>

            <div class="space-y-3 text-left mb-4">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 mb-1">የጠረጴዛ ቁጥር (Table #):</label>
                    <input type="number" id="pay-table-num" placeholder="ለምሳሌ: 5" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3.5 py-2.5 rounded-xl text-xs text-center font-bold focus:outline-none focus:ring-2 focus:ring-emerald-500">
                </div>

                <div>
                    <label class="block text-[11px] font-bold text-slate-300 mb-1">የክፍያ መንገድ (Payment Method):</label>
                    <div class="grid grid-cols-2 gap-2">
                        <label class="bg-slate-800 p-2.5 rounded-xl border border-slate-700 flex items-center gap-2 cursor-pointer text-xs font-bold text-slate-200">
                            <input type="radio" name="pay_method" value="ካሽ (Cash)" checked class="accent-emerald-500">
                            <span>💵 ካሽ (Cash)</span>
                        </label>
                        <label class="bg-slate-800 p-2.5 rounded-xl border border-slate-700 flex items-center gap-2 cursor-pointer text-xs font-bold text-slate-200">
                            <input type="radio" name="pay_method" value="ባንክ ሂሳብ (Bank)" class="accent-emerald-500">
                            <span>🏦 ባንክ (Bank)</span>
                        </label>
                    </div>
                </div>
            </div>

            <button onclick="sendPaymentCall()" id="pay-send-btn" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-black py-3 rounded-xl text-xs shadow-lg transition flex items-center justify-center gap-2 active:scale-95">
                <i class="fa-solid fa-paper-plane"></i>
                <span>ለክፍያ ጥሪ ላክ</span>
            </button>
        </div>
    </div>

    <!-- Call Regular Waiter Modal 🛎️ -->
    <div id="call-waiter-modal" class="fixed inset-0 bg-slate-950/85 hidden justify-center items-center z-50 p-4 backdrop-blur-md">
        <div class="bg-slate-900 border border-rose-500/30 rounded-3xl max-w-sm w-full p-6 text-center shadow-2xl relative">
            <button onclick="closeCallWaiterModal()" class="absolute right-4 top-4 w-8 h-8 bg-slate-800 text-slate-400 rounded-full flex items-center justify-center font-bold">✕</button>
            <div class="w-14 h-14 bg-rose-500/10 text-rose-400 rounded-full flex items-center justify-center text-2xl mx-auto mb-3 border border-rose-500/30">🛎️</div>
            <h3 class="text-base font-black text-amber-100 mb-1">አስተናጋጅ መጠራት ይፈልጋሉ?</h3>
            <p class="text-xs text-slate-400 mb-4">የጠረጴዛዎን ቁጥር ያስገቡ፤ አስተናጋጅ ወዲያውኑ ይመጣል።</p>
            
            <input type="number" id="waiter-table-num" placeholder="የጠረጴዛ ቁጥር (ለምሳሌ: 3)" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-4 py-2.5 rounded-xl text-xs text-center font-bold mb-4 focus:outline-none focus:ring-2 focus:ring-rose-500">

            <button onclick="sendWaiterCall()" id="waiter-send-btn" class="w-full bg-rose-600 hover:bg-rose-700 text-white font-black py-3 rounded-xl text-xs shadow-lg transition flex items-center justify-center gap-2 active:scale-95">
                <i class="fa-solid fa-paper-plane"></i>
                <span>አስተናጋጅ አሁኑኑ ጥራ</span>
            </button>
        </div>
    </div>

    <!-- Shopping Cart Sidebar -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-full sm:w-80 bg-slate-900 border-l border-amber-500/20 shadow-2xl p-5 transform translate-x-full transition-transform duration-300 z-50 flex flex-col">
        <div class="flex justify-between items-center mb-4 border-b border-slate-800 pb-3">
            <h3 class="text-base font-extrabold text-amber-100">የመረጧቸው እቃዎች</h3>
            <button onclick="toggleCart()" class="w-8 h-8 rounded-full bg-slate-800 text-slate-300 font-bold text-sm flex items-center justify-center">✕</button>
        </div>

        <div class="mb-3">
            <label class="block text-xs font-bold text-slate-300 mb-1">የጠረጴዛ ቁጥር (Table Number):</label>
            <input type="number" id="table-number" placeholder="ምሳሌ: 4" class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
        </div>

        <div class="mb-3">
            <label class="block text-xs font-bold text-slate-300 mb-1">ልዩ ማስታወሻ (Special Note):</label>
            <input type="text" id="order-note" placeholder="ለምሳሌ: ያለ በርበሬ ይሁን..." class="w-full bg-slate-800 border border-slate-700 text-amber-100 px-3.5 py-2.5 rounded-xl text-xs font-semibold focus:outline-none focus:ring-2 focus:ring-amber-500">
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-2.5 pr-1"></div>

        <div class="border-t border-slate-800 pt-4 mt-2">
            <div class="flex justify-between font-extrabold text-sm mb-4">
                <span class="text-slate-400">አጠቃላይ ዋጋ:</span>
                <span id="total-price" class="text-amber-400 text-base">0.00 ETB</span>
            </div>
            <button id="checkout-btn" onclick="checkout()" class="w-full luxury-btn-gold text-slate-950 py-3.5 rounded-2xl font-extrabold shadow-xl transition text-xs flex items-center justify-center gap-2 active:scale-95">
                <i class="fa-brands fa-telegram text-base"></i>
                <span>ትዕዛዝ በቦት ላክ</span>
            </button>
            <p id="order-status" class="text-center text-xs mt-2 hidden font-bold"></p>
        </div>
    </div>

    <!-- JavaScript Engine -->
    <script>
        // Telegram Configuration
        const BOT_TOKEN = "8752629354:AAEwRCOv5_SR4ynYGFZLgBD_b999E2SEpyA";
        const CHAT_ID = "-1004466655656";

        let isAdminLoggedIn = false;

        // Analytics Tracking Logic
        let visitorsCount = parseInt(localStorage.getItem('analytics_visitors') || '0');
        let ordersCount = parseInt(localStorage.getItem('analytics_orders') || '0');
        let totalRevenue = parseFloat(localStorage.getItem('analytics_revenue') || '0.0');

        // Increment visitor count on app load
        if (!sessionStorage.getItem('visited')) {
            visitorsCount++;
            sessionStorage.setItem('visited', 'true');
            localStorage.setItem('analytics_visitors', visitorsCount);
        }

        // Initial Default Menu Items
        const defaultMenuItems = [
            { id: 1, name: "ልዩ ዶሮ ወጥ", category: "habesha", price: 650.00, image: "https://images.unsplash.com/photo-1541544741938-0af808871cc0?w=600" },
            { id: 2, name: "ክትፎ ስፔሻል", category: "habesha", price: 720.00, image: "https://images.unsplash.com/photo-1544025162-d76694265947?w=600" },
            { id: 3, name: "የበሬ ቁልቋል ጥብስ", category: "habesha", price: 580.00, image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=600" },
            { id: 4, name: "ልዩ የጾም በያይነት", category: "fasting", price: 380.00, image: "https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=600" },
            { id: 5, name: "ዋግዩ ቺዝ በርገር", category: "western", price: 680.00, image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=600" },
            { id: 6, name: "ስፔሻል አቮካዶ ማንጎ", category: "drink", price: 180.00, image: "https://images.unsplash.com/photo-1556881286-fc6915169721?w=600" }
        ];

        let menuItems = JSON.parse(localStorage.getItem('luxury_menu_items')) || defaultMenuItems;
        let cart = [];
        let currentFilter = 'all';

        // 👤 ADMIN LOGIN & DASHBOARD SYSTEM
        function handleAdminButtonClick() {
            if (isAdminLoggedIn) {
                openAdminDashboardModal();
            } else {
                openAdminLoginModal();
            }
        }

        function openAdminLoginModal() {
            document.getElementById('admin-error-msg').classList.add('hidden');
            document.getElementById('admin-login-modal').classList.remove('hidden');
            document.getElementById('admin-login-modal').classList.add('flex');
        }

        function closeAdminLoginModal() {
            document.getElementById('admin-login-modal').classList.remove('flex');
            document.getElementById('admin-login-modal').classList.add('hidden');
        }

        function loginAdmin() {
            const user = document.getElementById('admin-username').value.trim();
            const pass = document.getElementById('admin-password').value.trim();
            const errEl = document.getElementById('admin-error-msg');

            if (user === "Admin" && pass === "yisu@1234") {
                isAdminLoggedIn = true;
                closeAdminLoginModal();
                document.getElementById('admin-banner').classList.remove('hidden');
                document.getElementById('admin-profile-btn').classList.add('bg-amber-500', 'text-slate-950');
                openAdminDashboardModal();
            } else {
                errEl.innerText = "ስህተት፡ የተሳሳተ Username ወይም Password!";
                errEl.classList.remove('hidden');
            }
        }

        function logoutAdmin() {
            isAdminLoggedIn = false;
            document.getElementById('admin-banner').classList.add('hidden');
            document.getElementById('admin-profile-btn').classList.remove('bg-amber-500', 'text-slate-950');
            filterMenu(currentFilter);
        }

        function openAdminDashboardModal() {
            updateAnalyticsUI();
            renderAdminItemsList();
            document.getElementById('admin-dashboard-modal').classList.remove('hidden');
            document.getElementById('admin-dashboard-modal').classList.add('flex');
        }

        function closeAdminDashboardModal() {
            document.getElementById('admin-dashboard-modal').classList.remove('flex');
            document.getElementById('admin-dashboard-modal').classList.add('hidden');
        }

        function switchAdminTab(tab) {
            const btnAnalytics = document.getElementById('tab-btn-analytics');
            const btnMenu = document.getElementById('tab-btn-menu');
            const contentAnalytics = document.getElementById('tab-content-analytics');
            const contentMenu = document.getElementById('tab-content-menu');

            if (tab === 'analytics') {
                btnAnalytics.className = "w-1/2 py-2 rounded-xl text-xs font-bold text-slate-950 bg-amber-500 transition";
                btnMenu.className = "w-1/2 py-2 rounded-xl text-xs font-bold text-slate-400 transition";
                contentAnalytics.classList.remove('hidden');
                contentMenu.classList.add('hidden');
            } else {
                btnMenu.className = "w-1/2 py-2 rounded-xl text-xs font-bold text-slate-950 bg-amber-500 transition";
                btnAnalytics.className = "w-1/2 py-2 rounded-xl text-xs font-bold text-slate-400 transition";
                contentMenu.classList.remove('hidden');
                contentAnalytics.classList.add('hidden');
            }
        }

        function updateAnalyticsUI() {
            document.getElementById('stat-visitors').innerText = visitorsCount;
            document.getElementById('stat-orders').innerText = ordersCount;
            document.getElementById('stat-revenue').innerText = totalRevenue.toFixed(2) + " ETB";
        }

        // ➕ 1. ADD NEW ITEM LOGIC
        function openAddItemModal() {
            document.getElementById('add-item-modal').classList.remove('hidden');
            document.getElementById('add-item-modal').classList.add('flex');
        }

        function closeAddItemModal() {
            document.getElementById('add-item-modal').classList.remove('flex');
            document.getElementById('add-item-modal').classList.add('hidden');
        }

        function saveNewItem() {
            const name = document.getElementById('add-name').value.trim();
            const category = document.getElementById('add-category').value;
            const price = parseFloat(document.getElementById('add-price').value);
            const image = document.getElementById('add-image').value.trim();

            if (!name || isNaN(price) || !image) {
                alert("እባክዎ መረጃዎችን በትክክል ይሙሉ!");
                return;
            }

            const newItem = {
                id: Date.now(),
                name: name,
                category: category,
                price: price,
                image: image
            };

            menuItems.push(newItem);
            localStorage.setItem('luxury_menu_items', JSON.stringify(menuItems));

            closeAddItemModal();
            renderAdminItemsList();
            filterMenu(currentFilter);
            alert("አዲስ ምግብ በስኬት ተጨምሯል! ✅");
        }

        // 🗑️ 2. DELETE ITEM LOGIC
        function deleteItem(id) {
            if (confirm("እርግጠኛ ነዎት ይህን ምግብ ከስርዓቱ መሰረዝ ይፈልጋሉ?")) {
                menuItems = menuItems.filter(item => item.id !== id);
                localStorage.setItem('luxury_menu_items', JSON.stringify(menuItems));
                renderAdminItemsList();
                filterMenu(currentFilter);
            }
        }

        // ✏️ 3. EDIT ITEM LOGIC
        function openEditModal(id) {
            const item = menuItems.find(p => p.id === id);
            if (!item) return;

            document.getElementById('edit-item-id').value = item.id;
            document.getElementById('edit-item-name').value = item.name;
            document.getElementById('edit-item-price').value = item.price;
            document.getElementById('edit-item-image').value = item.image;

            document.getElementById('edit-item-modal').classList.remove('hidden');
            document.getElementById('edit-item-modal').classList.add('flex');
        }

        function closeEditModal() {
            document.getElementById('edit-item-modal').classList.remove('flex');
            document.getElementById('edit-item-modal').classList.add('hidden');
        }

        function saveItemEdits() {
            const id = parseInt(document.getElementById('edit-item-id').value);
            const name = document.getElementById('edit-item-name').value.trim();
            const price = parseFloat(document.getElementById('edit-item-price').value);
            const image = document.getElementById('edit-item-image').value.trim();

            const itemIndex = menuItems.findIndex(p => p.id === id);
            if (itemIndex !== -1) {
                menuItems[itemIndex].name = name;
                menuItems[itemIndex].price = price;
                menuItems[itemIndex].image = image;

                localStorage.setItem('luxury_menu_items', JSON.stringify(menuItems));

                closeEditModal();
                renderAdminItemsList();
                filterMenu(currentFilter);
                alert("የምግቡ መረጃ በስኬት ተስተካክሏል! ✅");
            }
        }

        function renderAdminItemsList() {
            const listEl = document.getElementById('admin-items-list');
            listEl.innerHTML = menuItems.map(item => `
                <div class="bg-slate-800 p-2.5 rounded-2xl border border-slate-700 flex justify-between items-center text-xs">
                    <div class="flex items-center gap-2">
                        <img src="${item.image}" class="w-10 h-10 object-cover rounded-xl border border-slate-600">
                        <div>
                            <h5 class="font-bold text-amber-100">${item.name}</h5>
                            <p class="text-amber-400 font-extrabold text-[11px]">${item.price.toFixed(2)} ETB</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-1.5">
                        <button onclick="openEditModal(${item.id})" class="bg-amber-500 text-slate-950 px-2.5 py-1 rounded-xl font-bold text-[10px] hover:bg-amber-400">✏️ ኤዲት</button>
                        <button onclick="deleteItem(${item.id})" class="bg-rose-600 text-white px-2 py-1 rounded-xl font-bold text-[10px] hover:bg-rose-700">🗑️ ሰርዝ</button>
                    </div>
                </div>
            `).join('');
        }

        // 💳 CALL WAITER FOR PAYMENT LOGIC
        function openPaymentWaiterModal() {
            document.getElementById('payment-waiter-modal').classList.remove('hidden');
            document.getElementById('payment-waiter-modal').classList.add('flex');
        }

        function closePaymentWaiterModal() {
            document.getElementById('payment-waiter-modal').classList.remove('flex');
            document.getElementById('payment-waiter-modal').classList.add('hidden');
        }

        async function sendPaymentCall() {
            const tableNum = document.getElementById('pay-table-num').value.trim();
            const payMethod = document.querySelector('input[name="pay_method"]:checked').value;

            if (!tableNum) {
                alert("እባክዎ የጠረጴዛ ቁጥር ያስገቡ!");
                return;
            }

            const sendBtn = document.getElementById('pay-send-btn');
            sendBtn.disabled = true;
            sendBtn.innerHTML = `<span class="spinner mr-1.5"></span> ጥሪ በመላክ ላይ...`;

            let message = `💳 <b>የክፍያ አስተናጋጅ ጥሪ / PAYMENT WAITER NEEDED!</b>\n\n`;
            message += `📍 <b>ጠረጴዛ / Table #:</b> ${tableNum}\n`;
            message += `💵 <b>የክፍያ መንገድ:</b> ${payMethod}\n`;
            message += `⏰ <b>ሰዓት:</b> ${new Date().toLocaleTimeString()}`;

            const formData = new FormData();
            formData.append('chat_id', CHAT_ID);
            formData.append('text', message);
            formData.append('parse_mode', 'HTML');

            try {
                let res = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, { method: 'POST', body: formData });
                let data = await res.json();
                if (data.ok) {
                    alert(`💳 ጥሪዎ ደርሷል! አስተናጋጅ የ${payMethod} ክፍያ ለመቀበል ወደ ጠረጴዛዎ እየመጣ ነው።`);
                    closePaymentWaiterModal();
                    document.getElementById('pay-table-num').value = '';
                } else {
                    alert("ጥሪ መላክ አልተቻለም።");
                }
            } catch (e) {
                alert("የኢንተርኔት ግንኙነትዎን ያረጋግጡ።");
            } finally {
                sendBtn.disabled = false;
                sendBtn.innerHTML = `<i class="fa-solid fa-paper-plane"></i> <span>ለክፍያ ጥሪ ላክ</span>`;
            }
        }

        // Regular Waiter Call Modal Logic
        function openCallWaiterModal() {
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
                alert("እባክዎ የጠረጴዛ ቁጥር ያስገቡ!");
                return;
            }

            const sendBtn = document.getElementById('waiter-send-btn');
            sendBtn.disabled = true;

            let message = `🛎️ <b>አስተናጋጅ ጥሪ / WAITER NEEDED!</b>\n\n`;
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
                }
            } catch (e) {
                alert("የኢንተርኔት ግንኙነትዎን ያረጋግጡ።");
            } finally {
                sendBtn.disabled = false;
            }
        }

        // Menu Filtering & Rendering
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
            const filtered = menuItems.filter(item => item.name.toLowerCase().includes(query));
            renderGrid(filtered);
        }

        function renderGrid(items) {
            const container = document.getElementById('menu-container');
            container.innerHTML = items.map(item => `
                <div class="bg-slate-800/60 rounded-3xl p-3 shadow-md border border-amber-500/10 flex items-center justify-between gap-3.5">
                    <div class="flex items-center gap-3">
                        <img src="${item.image}" alt="" class="w-16 h-16 object-cover rounded-2xl border border-slate-700">
                        <div>
                            <h4 class="font-extrabold text-xs text-amber-100">${item.name}</h4>
                            <div class="text-amber-400 font-black text-xs mt-1">${item.price.toFixed(2)} ETB</div>
                        </div>
                    </div>
                    <button onclick="addToCart(${item.id})" class="luxury-btn-gold text-slate-950 w-9 h-9 rounded-2xl font-black shadow-md flex items-center justify-center active:scale-95">
                        <i class="fa-solid fa-plus text-xs"></i>
                    </button>
                </div>
            `).join('');
        }

        // Shopping Cart Logic
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
                container.innerHTML = `<p class='text-slate-500 text-center py-10 text-xs font-semibold'>ጋሪዎ ባዶ ነው</p>`;
                document.getElementById('total-price').innerText = "0.00 ETB";
                return;
            }

            let total = 0;
            container.innerHTML = cart.map((item, index) => {
                total += item.price * item.qty;
                return `
                    <div class="flex justify-between items-center bg-slate-800/80 p-3 rounded-2xl border border-slate-700">
                        <div>
                            <h5 class="font-bold text-xs text-amber-100">${item.name}</h5>
                            <p class="text-[11px] text-amber-400 font-extrabold">${(item.price * item.qty).toFixed(2)} ETB</p>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="changeQty(${index}, -1)" class="w-6 h-6 bg-slate-700 text-slate-200 rounded-lg font-bold text-xs flex items-center justify-center">-</button>
                            <span class="text-xs font-black text-amber-300">${item.qty}</span>
                            <button onclick="changeQty(${index}, 1)" class="w-6 h-6 bg-amber-500 text-slate-950 rounded-lg font-bold text-xs flex items-center justify-center">+</button>
                        </div>
                    </div>
                `;
            }).join('');

            document.getElementById('total-price').innerText = total.toFixed(2) + " ETB";
        }

        function toggleCart() {
            document.getElementById('cart-sidebar').classList.toggle('translate-x-full');
        }

        // Checkout Order Logic
        async function checkout() {
            if (cart.length === 0) {
                alert("እባክዎ መጀመሪያ ምግብ ይምረጡ!");
                return;
            }

            const tableNum = document.getElementById('table-number').value.trim();
            if (!tableNum) {
                alert("እባክዎ የጠረጴዛ ቁጥር ያስገቡ!");
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
                message += `${index + 1}. ${item.name} (${item.qty}x) - ${itemTotal.toFixed(2)} ETB\n`;
            });

            message += `-----------------------------\n`;
            message += `💰 <b>አጠቃላይ ዋጋ / Total:</b> ${total.toFixed(2)} ETB`;

            const checkoutBtn = document.getElementById('checkout-btn');
            checkoutBtn.disabled = true;

            const formData = new FormData();
            formData.append('chat_id', CHAT_ID);
            formData.append('text', message);
            formData.append('parse_mode', 'HTML');

            try {
                let response = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, { method: 'POST', body: formData });
                let data = await response.json();

                if (data.ok) {
                    alert("ትዕዛዝዎ ወደ አስተናጋጆች በተሳካ ሁኔታ ተልኳል! 🎉");

                    // Track Analytics Data
                    ordersCount++;
                    totalRevenue += total;
                    localStorage.setItem('analytics_orders', ordersCount);
                    localStorage.setItem('analytics_revenue', totalRevenue);

                    cart = [];
                    updateCartUI();
                    document.getElementById('order-note').value = '';
                    document.getElementById('table-number').value = '';
                    setTimeout(() => toggleCart(), 800);
                } else {
                    alert("ትዕዛዝ መላክ አልተቻለም።");
                }
            } catch (error) {
                alert("የኢንተርኔት ግንኙነትዎን ያረጋግጡ።");
            } finally {
                checkoutBtn.disabled = false;
            }
        }

        // Initialize Menu
        filterMenu('all');
        updateCartUI();
    </script>
</body>
</html>
