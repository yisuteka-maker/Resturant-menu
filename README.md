<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ero Shake - Menu & Refreshments</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            sky: '#0284c7',
                            light: '#f0f9ff',
                            dark: '#0c4a6e'
                        }
                    }
                }
            }
        }
    </script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .glass {
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }
        .dark .glass {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }
    </style>
</head>
<body class="bg-slate-50 dark:bg-slate-950 text-slate-800 dark:text-slate-100 min-h-screen pb-20 md:pb-0 transition-colors duration-300">

    <header class="sticky top-0 z-40 glass border-b border-slate-200/60 dark:border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3 cursor-pointer" onclick="showPage('home')">
                <div class="w-10 h-10 rounded-2xl bg-brand-sky text-white flex items-center justify-center text-xl font-black shadow-lg shadow-sky-500/30">
                    E
                </div>
                <div>
                    <h1 class="font-extrabold text-lg tracking-tight leading-none text-slate-900 dark:text-white">ERO SHAKE</h1>
                    <p class="text-[10px] text-slate-400 font-medium tracking-wider uppercase">Menu & Drinks</p>
                </div>
            </div>

            <nav class="hidden md:flex items-center gap-6 text-sm font-semibold">
                <button onclick="showPage('home')" class="hover:text-brand-sky transition" data-en="Home" data-am="መነሻ">Home</button>
                <button onclick="showPage('menu')" class="hover:text-brand-sky transition" data-en="Menu" data-am="ሜኑ">Menu</button>
                <button onclick="showPage('contact')" class="hover:text-brand-sky transition" data-en="Contact" data-am="አድራሻ">Contact</button>
                <button onclick="showPage('admin')" class="hover:text-brand-sky transition" data-en="Admin" data-am="አስተዳዳሪ">Admin</button>
            </nav>

            <div class="flex items-center gap-2">
                <button onclick="toggleLanguage()" class="px-3 py-1.5 rounded-xl bg-slate-200/60 dark:bg-slate-800 text-xs font-bold hover:bg-slate-300 dark:hover:bg-slate-700 transition">
                    <span id="langLabel">AM</span>
                </button>
                <button onclick="toggleDarkMode()" class="p-2.5 rounded-xl bg-slate-200/60 dark:bg-slate-800 hover:bg-slate-300 dark:hover:bg-slate-700 transition">
                    <i id="themeIcon" class="fa-solid fa-moon text-lg"></i>
                </button>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">

        <section id="page-home" class="page-view space-y-10">
            <div class="relative rounded-3xl overflow-hidden bg-gradient-to-r from-sky-600 to-blue-700 text-white p-8 sm:p-12 shadow-xl shadow-sky-500/10">
                <div class="relative z-10 max-w-xl space-y-4">
                    <span class="px-3 py-1 rounded-full bg-white/20 text-xs font-bold tracking-wide uppercase backdrop-blur-md" data-en="Fresh & Delicious" data-am="ትኩስ እና ጣፋጭ">Fresh & Delicious</span>
                    <h2 class="text-3xl sm:text-5xl font-black leading-tight" data-en="Taste The Freshness At Ero Shake" data-am="የተለየ ጣዕምን በኤሮ ሼክ ይለማመዱ">Taste The Freshness At Ero Shake</h2>
                    <p class="text-sky-100 text-sm sm:text-base" data-en="Explore our wide variety of fresh juices, milkshakes, pizzas, burgers, and breakfast specials." data-am="የተለያዩ የጁስ፣ የሚልካ ሼክ፣ የፒዛ፣ የበርገር እና የቁርስ አማራጮችን እኛ ዘንድ ያግኙ።">Explore our wide variety of fresh juices, milkshakes, pizzas, burgers, and breakfast specials.</p>
                    <div class="pt-2">
                        <button onclick="showPage('menu')" class="px-6 py-3 bg-white text-brand-sky rounded-2xl font-bold shadow-lg hover:bg-sky-50 transition" data-en="Explore Full Menu" data-am="ሙሉ ሜኑ ይመልከቱ">Explore Full Menu</button>
                    </div>
                </div>
            </div>

            <div>
                <h3 class="text-xl font-bold mb-4" data-en="Popular Categories" data-am="ታዋቂ ምድቦች">Popular Categories</h3>
                <div id="homeCategoriesList" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-3"></div>
            </div>

            <div>
                <h3 class="text-xl font-bold mb-4" data-en="Featured Items" data-am="ተመራጭ ማዕዶች">Featured Items</h3>
                <div id="homeSpecialsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6"></div>
            </div>
        </section>

        <section id="page-menu" class="page-view hidden space-y-6">
            <div class="flex flex-col sm:flex-row gap-3 items-center justify-between">
                <div class="relative w-full sm:w-80">
                    <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-slate-400"></i>
                    <input type="text" id="searchInput" oninput="renderMenuItems()" placeholder="Search menu..." class="w-full pl-11 pr-4 py-3 rounded-2xl bg-slate-200/50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-sky">
                </div>
                <div class="flex items-center gap-2 w-full sm:w-auto">
                    <button id="favToggleBtn" onclick="toggleFavoritesOnly()" class="px-4 py-3 rounded-2xl bg-slate-200/50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-xs font-bold flex items-center gap-2 hover:bg-slate-300 dark:hover:bg-slate-800 transition">
                        <i class="fa-solid fa-heart text-red-500"></i> <span data-en="Favorites" data-am="የወደዷቸው">Favorites</span>
                    </button>
                    <button onclick="resetFilters()" class="px-4 py-3 rounded-2xl bg-slate-200/50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-xs font-bold hover:bg-slate-300 dark:hover:bg-slate-800 transition" data-en="Reset" data-am="እንደገና">Reset</button>
                </div>
            </div>

            <div id="categoryChips" class="flex gap-2 overflow-x-auto pb-2 scrollbar-none"></div>

            <p id="itemsCountDisplay" class="text-xs font-semibold text-slate-400"></p>

            <div id="menuCardsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6"></div>
        </section>

        <section id="page-contact" class="page-view hidden space-y-6">
            <div class="max-w-2xl mx-auto glass p-8 rounded-3xl border border-slate-200/50 dark:border-slate-800 space-y-6">
                <h2 class="text-2xl font-bold" data-en="Contact Us" data-am="ያግኙን">Contact Us</h2>
                <div class="space-y-4 text-sm">
                    <div class="flex items-center gap-4">
                        <div class="w-10 h-10 rounded-xl bg-sky-100 dark:bg-slate-800 text-brand-sky flex items-center justify-center text-lg"><i class="fa-solid fa-location-dot"></i></div>
                        <div>
                            <p class="font-bold">Location</p>
                            <p class="text-slate-400">Addis Ababa, Ethiopia</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-4">
                        <div class="w-10 h-10 rounded-xl bg-sky-100 dark:bg-slate-800 text-brand-sky flex items-center justify-center text-lg"><i class="fa-solid fa-phone"></i></div>
                        <div>
                            <p class="font-bold">Phone</p>
                            <p class="text-slate-400">+251 900 000 000</p>
                        </div>
                    </div>
                </div>

                <form onsubmit="handleContactSubmit(event)" class="space-y-4 pt-4 border-t border-slate-200/50 dark:border-slate-800">
                    <input type="text" placeholder="Your Name" required class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-sky">
                    <textarea placeholder="Message" rows="4" required class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-sky"></textarea>
                    <button type="submit" class="w-full py-3 bg-brand-sky text-white font-bold rounded-xl shadow-lg hover:bg-sky-600 transition">Send Message</button>
                </form>
            </div>
        </section>

        <section id="page-admin" class="page-view hidden space-y-6">
            <div id="adminAuthBlock" class="max-w-md mx-auto glass p-8 rounded-3xl border border-slate-200/50 dark:border-slate-800 text-center space-y-4">
                <i class="fa-solid fa-lock text-3xl text-brand-sky"></i>
                <h2 class="text-xl font-bold">Admin Login</h2>
                <input type="password" id="adminPassInput" placeholder="Password (default: admin)" class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-sm text-center focus:outline-none focus:ring-2 focus:ring-brand-sky">
                <button onclick="verifyAdmin()" class="w-full py-3 bg-brand-sky text-white font-bold rounded-xl shadow-lg hover:bg-sky-600 transition">Login</button>
            </div>

            <div id="adminDashboardContent" class="hidden space-y-6">
                <div class="flex flex-col sm:flex-row items-center justify-between gap-4">
                    <h2 class="text-2xl font-bold">Menu Management</h2>
                    <div class="flex items-center gap-2">
                        <button onclick="openItemModal()" class="px-4 py-2 bg-brand-sky text-white text-xs font-bold rounded-xl hover:bg-sky-600 transition"><i class="fa-solid fa-plus mr-2"></i>Add Item</button>
                        <button onclick="exportMenuJSON()" class="px-4 py-2 bg-slate-200 dark:bg-slate-800 text-xs font-bold rounded-xl hover:bg-slate-300 dark:hover:bg-slate-700 transition"><i class="fa-solid fa-download mr-2"></i>Export JSON</button>
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div class="glass p-4 rounded-2xl border border-slate-200/50 dark:border-slate-800">
                        <p class="text-xs text-slate-400 font-bold">Total Items</p>
                        <p id="statTotalItems" class="text-2xl font-black text-brand-sky">0</p>
                    </div>
                    <div class="glass p-4 rounded-2xl border border-slate-200/50 dark:border-slate-800">
                        <p class="text-xs text-slate-400 font-bold">Active Items</p>
                        <p id="statActiveItems" class="text-2xl font-black text-emerald-500">0</p>
                    </div>
                </div>

                <div class="glass rounded-3xl overflow-hidden border border-slate-200/50 dark:border-slate-800">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm">
                            <thead class="bg-slate-100 dark:bg-slate-900 text-slate-400 text-xs uppercase">
                                <tr>
                                    <th class="p-4">Item</th>
                                    <th class="p-4">Category</th>
                                    <th class="p-4">Price (ETB)</th>
                                    <th class="p-4">Status</th>
                                    <th class="p-4 text-right">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="adminTableBody" class="divide-y divide-slate-200/50 dark:divide-slate-800"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <nav class="md:hidden fixed bottom-0 left-0 right-0 glass border-t border-slate-200/60 dark:border-slate-800 flex justify-around py-3 z-40">
        <button onclick="showPage('home')" class="mobile-nav-btn text-brand-sky flex flex-col items-center gap-1 text-[10px] font-bold" data-page="home">
            <i class="fa-solid fa-house text-lg"></i>
            <span data-en="Home" data-am="መነሻ">Home</span>
        </button>
        <button onclick="showPage('menu')" class="mobile-nav-btn text-slate-500 flex flex-col items-center gap-1 text-[10px] font-bold" data-page="menu">
            <i class="fa-solid fa-utensils text-lg"></i>
            <span data-en="Menu" data-am="ሜኑ">Menu</span>
        </button>
        <button onclick="showPage('contact')" class="mobile-nav-btn text-slate-500 flex flex-col items-center gap-1 text-[10px] font-bold" data-page="contact">
            <i class="fa-solid fa-envelope text-lg"></i>
            <span data-en="Contact" data-am="አድራሻ">Contact</span>
        </button>
        <button onclick="showPage('admin')" class="mobile-nav-btn text-slate-500 flex flex-col items-center gap-1 text-[10px] font-bold" data-page="admin">
            <i class="fa-solid fa-user-shield text-lg"></i>
            <span data-en="Admin" data-am="አስተዳዳሪ">Admin</span>
        </button>
    </nav>

    <div id="imageModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm hidden flex items-center justify-center p-4" onclick="closeImageModal()">
        <div class="relative max-w-lg w-full bg-white dark:bg-slate-900 rounded-3xl overflow-hidden shadow-2xl space-y-4 p-4" onclick="event.stopPropagation()">
            <img id="modalImg" src="" class="w-full h-64 object-cover rounded-2xl">
            <div class="flex items-center justify-between gap-3 px-2">
                <h3 id="modalTitle" class="font-bold text-lg break-words min-w-0"></h3>
                <p id="modalPrice" class="text-brand-sky font-black text-lg whitespace-nowrap"></p>
            </div>
            <button onclick="closeImageModal()" class="w-full py-2.5 bg-slate-200 dark:bg-slate-800 font-bold text-xs rounded-xl hover:bg-slate-300 dark:hover:bg-slate-700 transition">Close</button>
        </div>
    </div>

    <div id="itemFormModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="max-w-md w-full bg-white dark:bg-slate-900 rounded-3xl p-6 space-y-4 shadow-2xl">
            <h3 id="modalFormTitle" class="font-bold text-lg">Add New Item</h3>
            <form id="menuItemForm" onsubmit="saveMenuItem(event)" class="space-y-3">
                <input type="hidden" id="formItemId">
                <input type="text" id="formNameEn" placeholder="Name (English)" required class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs">
                <input type="text" id="formNameAm" placeholder="Name (Amharic)" required class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs">
                <select id="formCategory" class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs capitalize"></select>
                <input type="text" id="formPrice" placeholder="Price (ETB)" required class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs">
                <input type="url" id="formImage" placeholder="Image URL" required class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs">
                <input type="text" id="formPrep" placeholder="Prep Time (e.g. 10 min)" class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs">
                <label class="flex items-center gap-2 text-xs font-semibold cursor-pointer">
                    <input type="checkbox" id="formAvailable" checked class="rounded text-brand-sky focus:ring-brand-sky">
                    <span>Available / In Stock</span>
                </label>
                <div class="flex gap-2 pt-2">
                    <button type="button" onclick="closeFormModal()" class="w-1/2 py-2.5 bg-slate-200 dark:bg-slate-800 font-bold text-xs rounded-xl">Cancel</button>
                    <button type="submit" class="w-1/2 py-2.5 bg-brand-sky text-white font-bold text-xs rounded-xl shadow-md hover:bg-sky-600">Save Item</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // እባክዎን እነዚህን በራስዎ የ GitHub አካውንት እና Repository ስም ይተኩ
        const GITHUB_USER = "YOUR_GITHUB_USERNAME";
        const GITHUB_REPO = "YOUR_REPOSITORY_NAME";
        const GITHUB_BASE_URL = `https://raw.githubusercontent.com/${GITHUB_USER}/${GITHUB_REPO}/main/`;

        const CATEGORIES = [
            { id: 'all', en: 'All Items', am: 'ሁሉም' },
            { id: 'breakfast', en: 'Breakfast', am: 'ቁርስ' },
            { id: 'salad', en: 'Salad / Fruit', am: 'ሰላጣ እና ፍራፍሬ' },
            { id: 'wrap', en: 'Wrap', am: 'ውራፕ' },
            { id: 'sandwich', en: 'Sandwich / Club', am: 'ሳንድዊች' },
            { id: 'burger', en: 'Burger', am: 'በርገር' },
            { id: 'pizza', en: 'Pizza', am: 'ፒዛ' },
            { id: 'extra', en: 'Extra', am: 'ተጨማሪዎች' },
            { id: 'juice', en: 'Juice', am: 'ጁስ' },
            { id: 'shake', en: 'Shake', am: 'ሼክ' },
            { id: 'milkshake', en: 'Milk Shake', am: 'ሚልካ ሼክ' },
            { id: 'mojito', en: 'Mojito', am: 'ሞሂቶ' },
            { id: 'iceorder', en: 'Ice Order', am: 'ቀዝቃዛ መጠጦች' },
            { id: 'hotdrink', en: 'Hot Drink', am: 'ፍል መጠጦች' },
            { id: 'yogurt', en: 'Yogurt', am: 'እርጎ' },
            { id: 'frappuccino', en: 'Frappuccino', am: 'ፍራፑቺኖ' },
            { id: 'other', en: 'Other', am: 'ሌሎች' }
        ];

        let initialMenuItems = [
            { id: 'b1', category: 'breakfast', nameEn: 'Avocado', nameAm: 'አቮካዶ', price: '350', image: GITHUB_BASE_URL + 'avocado%20.jpg', prep: '10 min', available: true },
            { id: 'b2', category: 'breakfast', nameEn: 'Avocado w/ Egg', nameAm: 'አቮካዶ ከእንቁላል ጋር', price: '370', image: GITHUB_BASE_URL + 'avocado%20toste.jpg', prep: '10 min', available: true },
            { id: 'b3', category: 'breakfast', nameEn: 'Waffle', nameAm: 'ዋፍል', price: '400', image: GITHUB_BASE_URL + 'waffle%20.jpg', prep: '15 min', available: true },
            { id: 'b4', category: 'breakfast', nameEn: 'Pancake', nameAm: 'ፓንኬክ', price: '400', image: GITHUB_BASE_URL + 'pan%20cake%20.jpg', prep: '15 min', available: true },
            { id: 'b5', category: 'breakfast', nameEn: 'Chechebsa Normal', nameAm: 'ጨጨብሳ', price: '330', image: GITHUB_BASE_URL + 'normal%20chchbsa%20.jpg', prep: '15 min', available: true },
            { id: 'b6', category: 'breakfast', nameEn: 'Chechebsa Special', nameAm: 'ስፔሻል ጨጨብሳ', price: '400', image: GITHUB_BASE_URL + 'spacial%20chchbsa%20.jpg', prep: '15 min', available: true },
            { id: 'b7', category: 'breakfast', nameEn: 'Avocado Toast', nameAm: 'አቮካዶ ቶስት', price: '320', image: GITHUB_BASE_URL + 'avocado%20toste.jpg', prep: '10 min', available: true },
            { id: 'b8', category: 'breakfast', nameEn: 'Special Fetira', nameAm: 'ስፔሻል ፈቲራ', price: '360', image: GITHUB_BASE_URL + 'spacial%20fetira.jpg', prep: '15 min', available: true },
            { id: 'b9', category: 'breakfast', nameEn: 'Normal Fetira', nameAm: 'ፈቲራ', price: '260', image: GITHUB_BASE_URL + 'normal%20fetira%20.jpg', prep: '15 min', available: true },
            { id: 'b10', category: 'breakfast', nameEn: 'Omelet w/ Cheese', nameAm: 'ኦምሌት ከቺዝ ጋር', price: '430', image: GITHUB_BASE_URL + 'omlet%20with%20cheese%20.jpg', prep: '10 min', available: true },
            { id: 'b11', category: 'breakfast', nameEn: 'Normal Omelet', nameAm: 'ኦምሌት', price: '350', image: GITHUB_BASE_URL + 'omlet.jpg', prep: '10 min', available: true },
            { id: 'sl1', category: 'salad', nameEn: 'Normal Salad', nameAm: 'ሰላጣ', price: '400', image: GITHUB_BASE_URL + 'normal%20salad%20.jpg', prep: '10 min', available: true },
            { id: 'sl2', category: 'salad', nameEn: 'Special Salad', nameAm: 'ስፔሻል ሰላጣ', price: '590', image: GITHUB_BASE_URL + 'spacial%20salad.jpg', prep: '12 min', available: true },
            { id: 'sl3', category: 'salad', nameEn: 'Normal Fruit Punch', nameAm: 'ፍሩት ፓንች', price: '350', image: GITHUB_BASE_URL + 'normal%20fruit%20punch.jpg', prep: '10 min', available: true },
            { id: 'sl4', category: 'salad', nameEn: 'Special Fruit Punch', nameAm: 'ስፔሻል ፍሩት ፓንች', price: '450', image: GITHUB_BASE_URL + 'special%20fruit%20punch.jpg', prep: '10 min', available: true },
            { id: 'w1', category: 'wrap', nameEn: 'Chicken Wrap', nameAm: 'የዶሮ ውራፕ', price: '620', image: GITHUB_BASE_URL + 'beff%20wrap.jpg', prep: '15 min', available: true },
            { id: 'w2', category: 'wrap', nameEn: 'Beef Wrap', nameAm: 'የስጋ ውራፕ', price: '570', image: GITHUB_BASE_URL + 'beff%20wrap.jpg', prep: '15 min', available: true },
            { id: 'w3', category: 'wrap', nameEn: 'Veg Wrap', nameAm: 'የአትክልት ውራፕ', price: '450', image: GITHUB_BASE_URL + 'veg%20wrap%20.jpg', prep: '10 min', available: true },
            { id: 'sw2', category: 'sandwich', nameEn: 'Egg Sandwich', nameAm: 'እንቁላል ሳንድዊች', price: '400', image: GITHUB_BASE_URL + 'egg%20sandwich%20.jpg', prep: '10 min', available: true },
            { id: 'sw3', category: 'sandwich', nameEn: 'Veg Sandwich', nameAm: 'የአትክልት ሳንድዊች', price: '350', image: GITHUB_BASE_URL + 'veg%20sandwich%20.jpg', prep: '10 min', available: true },
            { id: 'sw4', category: 'sandwich', nameEn: 'Cheese Sandwich', nameAm: 'ቺዝ ሳንድዊች', price: '460', image: GITHUB_BASE_URL + 'cheese%20sandwich%20.jpg', prep: '10 min', available: true },
            { id: 'sw5', category: 'sandwich', nameEn: 'Special Club', nameAm: 'ስፔሻል ክለብ ሳንድዊች', price: '620', image: GITHUB_BASE_URL + 'spacial%20club.jpg', prep: '15 min', available: true },
            { id: 'sw6', category: 'sandwich', nameEn: 'Beef Club', nameAm: 'ቢፍ ክለብ ሳንድዊች', price: '550', image: GITHUB_BASE_URL + 'beef%20club%20.jpg', prep: '15 min', available: true },
            { id: 'sw7', category: 'sandwich', nameEn: 'Chicken Club', nameAm: 'ቺከን ክለብ ሳንድዊች', price: '590', image: GITHUB_BASE_URL + 'chicken%20club.jpg', prep: '15 min', available: true },
            { id: 'sw8', category: 'sandwich', nameEn: 'Egg w/ Cheese', nameAm: 'እንቁላል ከቺዝ ጋር', price: '500', image: GITHUB_BASE_URL + 'egg%20with%20cheese.jpg', prep: '10 min', available: true },
            { id: 'bg1', category: 'burger', nameEn: 'Special Double Burger', nameAm: 'ስፔሻል ዳብል በርገር', price: '800', image: GITHUB_BASE_URL + 'spacial%20Burger%20.jpg', prep: '20 min', available: true },
            { id: 'bg2', category: 'burger', nameEn: 'Special Single Burger', nameAm: 'ስፔሻል ሲንግል በርገር', price: '680', image: GITHUB_BASE_URL + 'spacial%20single%20Burger%20.jpg', prep: '15 min', available: true },
            { id: 'bg3', category: 'burger', nameEn: 'Beef Burger', nameAm: 'ቢፍ በርገር', price: '630', image: GITHUB_BASE_URL + 'beef%20burger%20.jpg', prep: '15 min', available: true },
            { id: 'bg4', category: 'burger', nameEn: 'Cheese Burger', nameAm: 'ቺዝ በርገር', price: '650', image: GITHUB_BASE_URL + 'cheese%20burger%20.jpg', prep: '15 min', available: true },
            { id: 'bg5', category: 'burger', nameEn: 'Chicken Burger', nameAm: 'ቺከን በርገር', price: '750', image: GITHUB_BASE_URL + 'chicken%20burger%20.jpg', prep: '15 min', available: true },
            { id: 'ot1', category: 'other', nameEn: 'Oat Juice', nameAm: 'የአሜካራ/ኦት ጁስ', price: '250', image: GITHUB_BASE_URL + 'oat%20juice%20.jpg', prep: '5 min', available: true },
            { id: 'ot2', category: 'other', nameEn: 'Detox', nameAm: 'ዲቶክስ', price: '110', image: GITHUB_BASE_URL + 'detox.jpg', prep: '5 min', available: true },
            { id: 'ot3', category: 'other', nameEn: 'Mint', nameAm: 'ናና (ሚንት)', price: '230', image: GITHUB_BASE_URL + 'mint.jpg', prep: '5 min', available: true }
        ];

        let menuItems = JSON.parse(localStorage.getItem('ero_menu_items')) || initialMenuItems;
        let activeCategory = 'all';
        let currentLang = localStorage.getItem('ero_lang') || 'en';
        let favorites = JSON.parse(localStorage.getItem('ero_favorites')) || [];
        let showFavsOnly = false;

        function saveState() {
            localStorage.setItem('ero_menu_items', JSON.stringify(menuItems));
        }

        function escAttr(str) {
            return String(str)
                .replace(/&/g, '&amp;')
                .replace(/'/g, '&#39;')
                .replace(/"/g, '&quot;');
        }

        document.addEventListener('DOMContentLoaded', () => {
            initTheme();
            renderCategoryChips();
            renderHomeCategories();
            renderHomeSpecials();
            renderMenuItems();
            applyLanguage();
            updateStats();
            populateCategoryDropdown();
        });

        function showPage(pageId) {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            const targetPage = document.getElementById(`page-${pageId}`);
            if (targetPage) targetPage.classList.remove('hidden');

            document.querySelectorAll('.mobile-nav-btn').forEach(btn => {
                const isActive = btn.dataset.page === pageId;
                btn.classList.toggle('text-brand-sky', isActive);
                btn.classList.toggle('text-slate-500', !isActive);
            });

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function renderCategoryChips() {
            const container = document.getElementById('categoryChips');
            if (!container) return;
            container.innerHTML = CATEGORIES.map(cat => `
                <button onclick="selectCategory('${cat.id}')" 
                        class="chip-btn px-4 py-2 rounded-xl text-xs font-semibold whitespace-nowrap transition-all duration-200 ${activeCategory === cat.id ? 'bg-brand-sky text-white shadow-md shadow-sky-500/20' : 'bg-slate-200/60 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-300 dark:hover:bg-slate-700'}">
                    ${cat[currentLang]}
                </button>
            `).join('');
        }

        function selectCategory(catId) {
            activeCategory = catId;
            renderCategoryChips();
            renderMenuItems();
        }

        function renderHomeCategories() {
            const container = document.getElementById('homeCategoriesList');
            if (!container) return;
            const displayCats = CATEGORIES.filter(c => c.id !== 'all').slice(0, 6);
            container.innerHTML = displayCats.map(cat => `
                <div onclick="showPage('menu'); selectCategory('${cat.id}');" class="glass p-4 rounded-2xl text-center cursor-pointer hover:scale-105 transition-all shadow-sm group border border-slate-200/50 dark:border-slate-800 min-w-0">
                    <div class="w-12 h-12 rounded-xl bg-brand-light dark:bg-slate-800 text-brand-sky flex items-center justify-center mx-auto text-xl mb-2 group-hover:bg-brand-sky group-hover:text-white transition">
                        <i class="fa-solid fa-utensils"></i>
                    </div>
                    <h4 class="font-bold text-xs sm:text-sm text-slate-800 dark:text-slate-100 break-words">${cat[currentLang]}</h4>
                </div>
            `).join('');
        }

        function renderHomeSpecials() {
            const container = document.getElementById('homeSpecialsGrid');
            if (!container) return;
            const specials = menuItems.slice(0, 4);
            container.innerHTML = specials.map(item => createCardHTML(item)).join('');
        }

        function renderMenuItems() {
            const container = document.getElementById('menuCardsGrid');
            if (!container) return;

            const searchVal = document.getElementById('searchInput')?.value.toLowerCase() || '';

            const filtered = menuItems.filter(item => {
                const matchesCat = activeCategory === 'all' || item.category === activeCategory;
                const matchesSearch = item.nameEn.toLowerCase().includes(searchVal) || item.nameAm.includes(searchVal);
                const matchesFav = !showFavsOnly || favorites.includes(item.id);
                return matchesCat && matchesSearch && matchesFav;
            });

            document.getElementById('itemsCountDisplay').innerText = `Showing ${filtered.length} of ${menuItems.length} items`;

            if (filtered.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full text-center py-12 space-y-3">
                        <i class="fa-solid fa-cookie-bite text-4xl text-slate-300"></i>
                        <p class="text-slate-400 font-medium text-sm">No menu items found.</p>
                    </div>
                `;
                return;
            }

            container.innerHTML = filtered.map(item => createCardHTML(item)).join('');
        }

        function createCardHTML(item) {
            const isFav = favorites.includes(item.id);
            const name = currentLang === 'am' ? item.nameAm : item.nameEn;
            return `
                <div class="glass rounded-3xl overflow-hidden shadow-sm hover:shadow-xl transition-all duration-300 flex flex-col justify-between group border border-slate-200/50 dark:border-slate-800 min-w-0">
                    <div class="relative overflow-hidden cursor-pointer aspect-[4/3]" onclick="openImageModal('${escAttr(item.image)}', '${escAttr(name)}', '${escAttr(item.price)}')">
                        <img src="${item.image}" alt="${name}" class="absolute inset-0 w-full h-full object-cover group-hover:scale-105 transition duration-500">
                        <button onclick="event.stopPropagation(); toggleFavorite('${escAttr(item.id)}')" class="absolute top-3 right-3 w-9 h-9 rounded-full glass flex items-center justify-center text-slate-400 hover:text-red-500 transition shadow-md">
                            <i class="${isFav ? 'fa-solid text-red-500' : 'fa-regular'} fa-heart"></i>
                        </button>
                        ${!item.available ? '<span class="absolute bottom-3 left-3 px-2.5 py-1 rounded-full bg-red-500/80 backdrop-blur-md text-white text-[10px] font-bold tracking-wider uppercase">Out of Stock</span>' : ''}
                    </div>
                    <div class="p-5 space-y-3 flex-1 flex flex-col justify-between min-w-0">
                        <div class="min-w-0">
                            <div class="flex justify-between items-start gap-2 min-w-0">
                                <h3 class="font-bold text-base text-slate-800 dark:text-white leading-snug break-words min-w-0">${name}</h3>
                            </div>
                            <p class="text-xs text-slate-400 mt-1"><i class="fa-regular fa-clock mr-1"></i>${item.prep || '10-15 min'}</p>
                        </div>
                        <div class="flex items-center justify-between gap-2 pt-2 border-t border-slate-200/40 dark:border-slate-800 min-w-0">
                            <div class="min-w-0">
                                <span class="text-xs text-slate-400 font-medium">Price</span>
                                <p class="text-brand-sky font-extrabold text-base">${item.price} ETB</p>
                            </div>
                        </div>
                    </div>
                </div>
            `;
        }

        function toggleFavorite(id) {
            if (favorites.includes(id)) {
                favorites = favorites.filter(fId => fId !== id);
            } else {
                favorites.push(id);
            }
            localStorage.setItem('ero_favorites', JSON.stringify(favorites));
            renderMenuItems();
            renderHomeSpecials();
        }

        function toggleFavoritesOnly() {
            showFavsOnly = !showFavsOnly;
            const btn = document.getElementById('favToggleBtn');
            btn.classList.toggle('bg-brand-sky', showFavsOnly);
            btn.classList.toggle('text-white', showFavsOnly);
            renderMenuItems();
        }

        function resetFilters() {
            document.getElementById('searchInput').value = '';
            showFavsOnly = false;
            activeCategory = 'all';
            const btn = document.getElementById('favToggleBtn');
            btn.classList.remove('bg-brand-sky', 'text-white');
            renderCategoryChips();
            renderMenuItems();
        }

        function toggleLanguage() {
            currentLang = currentLang === 'en' ? 'am' : 'en';
            localStorage.setItem('ero_lang', currentLang);
            applyLanguage();
            renderCategoryChips();
            renderHomeCategories();
            renderHomeSpecials();
            renderMenuItems();
        }

        function applyLanguage() {
            document.getElementById('langLabel').innerText = currentLang === 'en' ? 'AM' : 'EN';
            document.querySelectorAll('[data-en]').forEach(el => {
                el.innerText = currentLang === 'am' ? el.dataset.am : el.dataset.en;
            });
        }

        function initTheme() {
            if (localStorage.getItem('ero_theme') === 'dark' || (!('ero_theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark');
                document.getElementById('themeIcon').className = 'fa-solid fa-sun text-amber-400 text-lg';
            } else {
                document.documentElement.classList.remove('dark');
                document.getElementById('themeIcon').className = 'fa-solid fa-moon text-lg';
            }
        }

        function toggleDarkMode() {
            const isDark = document.documentElement.classList.toggle('dark');
            localStorage.setItem('ero_theme', isDark ? 'dark' : 'light');
            document.getElementById('themeIcon').className = isDark ? 'fa-solid fa-sun text-amber-400 text-lg' : 'fa-solid fa-moon text-lg';
        }

        function openImageModal(img, title, price) {
            document.getElementById('modalImg').src = img;
            document.getElementById('modalTitle').innerText = title;
            document.getElementById('modalPrice').innerText = price + ' ETB';
            document.getElementById('imageModal').classList.remove('hidden');
        }

        function closeImageModal() {
            document.getElementById('imageModal').classList.add('hidden');
        }

        function verifyAdmin() {
            const pass = document.getElementById('adminPassInput').value;
            if (pass === 'admin' || pass === '1234') {
                document.getElementById('adminAuthBlock').classList.add('hidden');
                document.getElementById('adminDashboardContent').classList.remove('hidden');
                renderAdminTable();
            } else {
                alert('የተሳሳተ የይለፍ ቃል (Incorrect password)');
            }
        }

        function renderAdminTable() {
            const tbody = document.getElementById('adminTableBody');
            if (!tbody) return;

            tbody.innerHTML = menuItems.map(item => `
                <tr class="hover:bg-slate-100/50 dark:hover:bg-slate-900/50 transition">
                    <td class="p-4 flex items-center gap-3">
                        <img src="${item.image}" class="w-10 h-10 rounded-xl object-cover">
                        <div>
                            <p class="font-bold text-xs">${item.nameEn}</p>
                            <p class="text-[10px] text-slate-400">${item.nameAm}</p>
                        </div>
                    </td>
                    <td class="p-4 text-xs font-semibold capitalize">${item.category}</td>
                    <td class="p-4">
                        <input type="text" value="${item.price}" onchange="updateItemPrice('${item.id}', this.value)" class="w-20 p-1.5 rounded-lg bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs font-bold text-brand-sky">
                    </td>
                    <td class="p-4">
                        <button onclick="toggleAvailability('${item.id}')" class="px-2.5 py-1 rounded-full text-[10px] font-bold ${item.available ? 'bg-emerald-100 dark:bg-emerald-950 text-emerald-600' : 'bg-red-100 dark:bg-red-950 text-red-500'}">
                            ${item.available ? 'In Stock' : 'Out of Stock'}
                        </button>
                    </td>
                    <td class="p-4 text-right space-x-2">
                        <button onclick="editItem('${item.id}')" class="text-brand-sky hover:underline text-xs"><i class="fa-solid fa-pen-to-square"></i></button>
                        <button onclick="deleteItem('${item.id}')" class="text-red-500 hover:underline text-xs"><i class="fa-solid fa-trash"></i></button>
                    </td>
                </tr>
            `).join('');

            updateStats();
        }

        function updateItemPrice(id, newPrice) {
            const item = menuItems.find(i => i.id === id);
            if (item) {
                item.price = newPrice;
                saveState();
                renderMenuItems();
                renderHomeSpecials();
            }
        }

        function toggleAvailability(id) {
            const item = menuItems.find(i => i.id === id);
            if (item) {
                item.available = !item.available;
                saveState();
                renderAdminTable();
                renderMenuItems();
            }
        }

        function deleteItem(id) {
            if (confirm('Are you sure you want to delete this item?')) {
                menuItems = menuItems.filter(i => i.id !== id);
                saveState();
                renderAdminTable();
                renderMenuItems();
                renderHomeSpecials();
            }
        }

        function updateStats() {
            document.getElementById('statTotalItems').innerText = menuItems.length;
            document.getElementById('statActiveItems').innerText = menuItems.filter(i => i.available).length;
        }

        function populateCategoryDropdown() {
            const select = document.getElementById('formCategory');
            if (!select) return;
            select.innerHTML = CATEGORIES.filter(c => c.id !== 'all').map(c => `
                <option value="${c.id}">${c.en} (${c.am})</option>
            `).join('');
        }

        function openItemModal(itemId = null) {
            const modal = document.getElementById('itemFormModal');
            document.getElementById('menuItemForm').reset();
            document.getElementById('formItemId').value = '';
            document.getElementById('modalFormTitle').innerText = itemId ? 'Edit Item' : 'Add New Item';

            if (itemId) {
                const item = menuItems.find(i => i.id === itemId);
                if (item) {
                    document.getElementById('formItemId').value = item.id;
                    document.getElementById('formNameEn').value = item.nameEn;
                    document.getElementById('formNameAm').value = item.nameAm;
                    document.getElementById('formCategory').value = item.category;
                    document.getElementById('formPrice').value = item.price;
                    document.getElementById('formImage').value = item.image;
                    document.getElementById('formPrep').value = item.prep || '';
                    document.getElementById('formAvailable').checked = item.available;
                }
            }
            modal.classList.remove('hidden');
        }

        function closeFormModal() {
            document.getElementById('itemFormModal').classList.add('hidden');
        }

        function editItem(id) {
            openItemModal(id);
        }

        function saveMenuItem(event) {
            event.preventDefault();
            const id = document.getElementById('formItemId').value || 'item_' + Date.now();
            const newItem = {
                id: id,
                nameEn: document.getElementById('formNameEn').value,
                nameAm: document.getElementById('formNameAm').value,
                category: document.getElementById('formCategory').value,
                price: document.getElementById('formPrice').value,
                image: document.getElementById('formImage').value,
                prep: document.getElementById('formPrep').value || '10-15 min',
                available: document.getElementById('formAvailable').checked
            };

            const index = menuItems.findIndex(i => i.id === id);
            if (index > -1) {
                menuItems[index] = newItem;
            } else {
                menuItems.push(newItem);
            }

            saveState();
            closeFormModal();
            renderAdminTable();
            renderMenuItems();
            renderHomeSpecials();
        }

        function exportMenuJSON() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(menuItems, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", "ero_shake_menu.json");
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
        }

        function handleContactSubmit(event) {
            event.preventDefault();
            alert('መልዕክትዎ በስኬት ተልኳል! እናመሰግናለን። (Message sent successfully!)');
            event.target.reset();
        }
    </script>
</body>
</html>
