<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ero Shake - Menu & Refreshments</title>
    <!-- Tailwind CSS CDN -->
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
    <!-- FontAwesome Icons -->
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

    <!-- HEADER / NAVIGATION -->
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

            <!-- DESKTOP NAV -->
            <nav class="hidden md:flex items-center gap-6 text-sm font-semibold">
                <button onclick="showPage('home')" class="hover:text-brand-sky transition" data-en="Home" data-am="መነሻ">Home</button>
                <button onclick="showPage('menu')" class="hover:text-brand-sky transition" data-en="Menu" data-am="ሜኑ">Menu</button>
                <button onclick="showPage('contact')" class="hover:text-brand-sky transition" data-en="Contact" data-am="አድራሻ">Contact</button>
                <button onclick="showPage('admin')" class="hover:text-brand-sky transition" data-en="Admin" data-am="አስተዳዳሪ">Admin</button>
            </nav>

            <!-- UTILITY BUTTONS -->
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

    <!-- MAIN CONTENT CONTAINERS -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">

        <!-- PAGE 1: HOME -->
        <section id="page-home" class="page-view space-y-10">
            <!-- HERO -->
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

            <!-- QUICK CATEGORIES -->
            <div>
                <h3 class="text-xl font-bold mb-4" data-en="Popular Categories" data-am="ታዋቂ ምድቦች">Popular Categories</h3>
                <div id="homeCategoriesList" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-3"></div>
            </div>

            <!-- SPECIALS GRID -->
            <div>
                <h3 class="text-xl font-bold mb-4" data-en="Featured Items" data-am="ተመራጭ ማዕዶች">Featured Items</h3>
                <div id="homeSpecialsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6"></div>
            </div>
        </section>

        <!-- PAGE 2: MENU -->
        <section id="page-menu" class="page-view hidden space-y-6">
            <!-- SEARCH & FILTERS -->
            <div class="flex flex-col sm:flex-row gap-3 items-center justify-between">
                <div class="relative w-full sm:w-80">
                    <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-slate-400"></i>
                    <input type="text" id="searchInput" oninput="filterMenu()" placeholder="Search menu..." class="w-full pl-11 pr-4 py-3 rounded-2xl bg-slate-200/50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-sky">
                </div>
                <div class="flex items-center gap-2 w-full sm:w-auto">
                    <button id="favToggleBtn" onclick="toggleFavoritesOnly()" class="px-4 py-3 rounded-2xl bg-slate-200/50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-xs font-bold flex items-center gap-2 hover:bg-slate-300 dark:hover:bg-slate-800 transition">
                        <i class="fa-solid fa-heart text-red-500"></i> <span data-en="Favorites" data-am="የወደዷቸው">Favorites</span>
                    </button>
                    <button onclick="resetFilters()" class="px-4 py-3 rounded-2xl bg-slate-200/50 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-xs font-bold hover:bg-slate-300 dark:hover:bg-slate-800 transition" data-en="Reset" data-am="እንደገና">Reset</button>
                </div>
            </div>

            <!-- CATEGORY CHIPS -->
            <div id="categoryChips" class="flex gap-2 overflow-x-auto pb-2 scrollbar-none"></div>

            <!-- ITEM COUNT DISPLAY -->
            <p id="itemsCountDisplay" class="text-xs font-semibold text-slate-400"></p>

            <!-- MENU ITEMS GRID -->
            <div id="menuCardsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6"></div>
        </section>

        <!-- PAGE 3: CONTACT -->
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

        <!-- PAGE 4: ADMIN -->
        <section id="page-admin" class="page-view hidden space-y-6">
            <!-- LOGIN BLOCK -->
            <div id="adminAuthBlock" class="max-w-md mx-auto glass p-8 rounded-3xl border border-slate-200/50 dark:border-slate-800 text-center space-y-4">
                <i class="fa-solid fa-lock text-3xl text-brand-sky"></i>
                <h2 class="text-xl font-bold">Admin Login</h2>
                <input type="password" id="adminPassInput" placeholder="Password (admin123)" class="w-full p-3 rounded-xl bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-sm text-center focus:outline-none focus:ring-2 focus:ring-brand-sky">
                <button onclick="verifyAdmin()" class="w-full py-3 bg-brand-sky text-white font-bold rounded-xl shadow-lg hover:bg-sky-600 transition">Login</button>
            </div>

            <!-- DASHBOARD CONTENT (HIDDEN UNTIL AUTH) -->
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
                                    <th class="p-4">Price</th>
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

    <!-- MOBILE NAVIGATION BOTTOM BAR -->
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

    <!-- IMAGE MODAL -->
    <div id="imageModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm hidden flex items-center justify-center p-4" onclick="closeImageModal()">
        <div class="relative max-w-lg w-full bg-white dark:bg-slate-900 rounded-3xl overflow-hidden shadow-2xl space-y-4 p-4" onclick="event.stopPropagation()">
            <img id="modalImg" src="" class="w-full h-64 object-cover rounded-2xl">
            <div class="flex items-center justify-between px-2">
                <h3 id="modalTitle" class="font-bold text-lg"></h3>
                <p id="modalPrice" class="text-brand-sky font-black text-lg"></p>
            </div>
            <button onclick="closeImageModal()" class="w-full py-2.5 bg-slate-200 dark:bg-slate-800 font-bold text-xs rounded-xl hover:bg-slate-300 dark:hover:bg-slate-700 transition">Close</button>
        </div>
    </div>

    <!-- ITEM FORM MODAL (ADMIN) -->
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

    <!-- JAVASCRIPT CODE -->
    <script>
        // --- 1. MENU CATEGORIES & COMPLETE DATASET WITH UNIQUE IMAGES ---
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
            // BREAKFAST
            { id: 'b1', category: 'breakfast', nameEn: 'Avocado', nameAm: 'አቮካዶ', price: '350', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'b2', category: 'breakfast', nameEn: 'Avocado w/ Egg', nameAm: 'አቮካዶ ከእንቁላል ጋር', price: '370', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'b3', category: 'breakfast', nameEn: 'Waffle', nameAm: 'ዋፍል', price: '400', image: 'https://images.unsplash.com/photo-1562376552-0d160a2f238d?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'b4', category: 'breakfast', nameEn: 'Pancake', nameAm: 'ፓንኬክ', price: '400', image: 'https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'b5', category: 'breakfast', nameEn: 'Chechebsa Normal', nameAm: 'ጨጨብሳ', price: '330', image: 'https://images.unsplash.com/photo-1600891964092-4316c288032e?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'b6', category: 'breakfast', nameEn: 'Chechebsa Special', nameAm: 'ስፔሻል ጨጨብሳ', price: '400', image: 'https://images.unsplash.com/photo-1600891964092-4316c288032e?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'b7', category: 'breakfast', nameEn: 'Avocado Toast', nameAm: 'አቮካዶ ቶስት', price: '320', image: 'https://images.unsplash.com/photo-1588137378633-dea1336ce1e2?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'b8', category: 'breakfast', nameEn: 'Special Fetira', nameAm: 'ስፔሻል ፈቲራ', price: '360', image: 'https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'b9', category: 'breakfast', nameEn: 'Normal Fetira', nameAm: 'ፈቲራ', price: '260', image: 'https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'b10', category: 'breakfast', nameEn: 'Omelet w/ Cheese', nameAm: 'ኦምሌት ከቺዝ ጋር', price: '430', image: 'https://images.unsplash.com/photo-1510693206972-df098062cb71?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'b11', category: 'breakfast', nameEn: 'Normal Omelet', nameAm: 'ኦምሌት', price: '350', image: 'https://images.unsplash.com/photo-1510693206972-df098062cb71?w=500&auto=format&fit=crop', prep: '10 min', available: true },

            // SALAD / FRUIT
            { id: 'sl1', category: 'salad', nameEn: 'Normal Salad', nameAm: 'ሰላጣ', price: '400', image: 'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'sl2', category: 'salad', nameEn: 'Special Salad', nameAm: 'ስፔሻል ሰላጣ', price: '590', image: 'https://images.unsplash.com/photo-1540420773420-3366772f4999?w=500&auto=format&fit=crop', prep: '12 min', available: true },
            { id: 'sl3', category: 'salad', nameEn: 'Normal Fruit Punch', nameAm: 'ፍሩት ፓንች', price: '350', image: 'https://images.unsplash.com/photo-1519996529931-28324d5a630e?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'sl4', category: 'salad', nameEn: 'Special Fruit Punch', nameAm: 'ስፔሻል ፍሩት ፓንች', price: '450', image: 'https://images.unsplash.com/photo-1490474418585-ba9bad8fd0ea?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'sl5', category: 'salad', nameEn: 'Four in One', nameAm: 'ፎር ኢን ዋን', price: '580', image: 'https://images.unsplash.com/photo-1565958011703-44f9829ba187?w=500&auto=format&fit=crop', prep: '12 min', available: true },
            { id: 'sl6', category: 'salad', nameEn: 'Waffle Fruit', nameAm: 'ዋፍል ፍሩት', price: '450', image: 'https://images.unsplash.com/photo-1562376552-0d160a2f238d?w=500&auto=format&fit=crop', prep: '15 min', available: true },

            // WRAP
            { id: 'w1', category: 'wrap', nameEn: 'Chicken Wrap', nameAm: 'የዶሮ ውራፕ', price: '620', image: 'https://images.unsplash.com/photo-1626700051175-6818013e1d4f?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'w2', category: 'wrap', nameEn: 'Beef Wrap', nameAm: 'የስጋ ውራፕ', price: '570', image: 'https://images.unsplash.com/photo-1565299585323-38d6b0865b47?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'w3', category: 'wrap', nameEn: 'Veg Wrap', nameAm: 'የአትክልት ውራፕ', price: '450', image: 'https://images.unsplash.com/photo-1540420773420-3366772f4999?w=500&auto=format&fit=crop', prep: '10 min', available: true },

            // SANDWICH / CLUB
            { id: 'sw1', category: 'sandwich', nameEn: 'Tuna Sandwich', nameAm: 'ቱና ሳንድዊች', price: '580', image: 'https://images.unsplash.com/photo-1509722747041-616f39b57569?w=500&auto=format&fit=crop', prep: '12 min', available: true },
            { id: 'sw2', category: 'sandwich', nameEn: 'Egg Sandwich', nameAm: 'እንቁላል ሳንድዊች', price: '400', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'sw3', category: 'sandwich', nameEn: 'Veg Sandwich', nameAm: 'የአትክልት ሳንድዊች', price: '350', image: 'https://images.unsplash.com/photo-1540420773420-3366772f4999?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'sw4', category: 'sandwich', nameEn: 'Cheese Sandwich', nameAm: 'ቺዝ ሳንድዊች', price: '460', image: 'https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=500&auto=format&fit=crop', prep: '10 min', available: true },
            { id: 'sw5', category: 'sandwich', nameEn: 'Special Club', nameAm: 'ስፔሻል ክለብ ሳንድዊች', price: '620', image: 'https://images.unsplash.com/photo-1567234669003-dce7a7a88721?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'sw6', category: 'sandwich', nameEn: 'Beef Club', nameAm: 'ቢፍ ክለብ ሳንድዊች', price: '550', image: 'https://images.unsplash.com/photo-1567234669003-dce7a7a88721?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'sw7', category: 'sandwich', nameEn: 'Chicken Club', nameAm: 'ቺከን ክለብ ሳንድዊች', price: '590', image: 'https://images.unsplash.com/photo-1567234669003-dce7a7a88721?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'sw8', category: 'sandwich', nameEn: 'Egg w/ Cheese', nameAm: 'እንቁላል ከቺዝ ጋር', price: '500', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop', prep: '10 min', available: true },

            // BURGER
            { id: 'bg1', category: 'burger', nameEn: 'Special Double Burger', nameAm: 'ስፔሻል ዳብል በርገር', price: '800', image: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500&auto=format&fit=crop', prep: '20 min', available: true },
            { id: 'bg2', category: 'burger', nameEn: 'Special Single Burger', nameAm: 'ስፔሻል ሲንግል በርገር', price: '680', image: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'bg3', category: 'burger', nameEn: 'Beef Burger', nameAm: 'ቢፍ በርገር', price: '630', image: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'bg4', category: 'burger', nameEn: 'Cheese Burger', nameAm: 'ቺዝ በርገር', price: '650', image: 'https://images.unsplash.com/photo-1550547660-d9450f859349?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'bg5', category: 'burger', nameEn: 'Chicken Burger', nameAm: 'ቺከን በርገር', price: '750', image: 'https://images.unsplash.com/photo-1615297928064-24977384d0da?w=500&auto=format&fit=crop', prep: '15 min', available: true },

            // PIZZA
            { id: 'pz1', category: 'pizza', nameEn: 'Tuna w/ Cheese Pizza', nameAm: 'ቱና ከቺዝ ፒዛ', price: '770', image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&auto=format&fit=crop', prep: '20 min', available: true },
            { id: 'pz2', category: 'pizza', nameEn: 'Margarita Pizza', nameAm: 'ማርጋሪታ ፒዛ', price: '700', image: 'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'pz3', category: 'pizza', nameEn: 'Meat Lover Pizza', nameAm: 'ሜት ላቨር ፒዛ', price: '770', image: 'https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=500&auto=format&fit=crop', prep: '20 min', available: true },
            { id: 'pz4', category: 'pizza', nameEn: 'Special Pizza', nameAm: 'ስፔሻል ፒዛ', price: '920', image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&auto=format&fit=crop', prep: '20 min', available: true },
            { id: 'pz5', category: 'pizza', nameEn: 'Chicken Pizza', nameAm: 'ቺከን ፒዛ', price: '890', image: 'https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=500&auto=format&fit=crop', prep: '20 min', available: true },
            { id: 'pz6', category: 'pizza', nameEn: 'Veg Pizza', nameAm: 'የአትክልት ፒዛ', price: '550', image: 'https://images.unsplash.com/photo-1571407970349-bc81e7e96d47?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'pz7', category: 'pizza', nameEn: 'Tuna w/ Veg Pizza', nameAm: 'ቱና ከአትክልት ፒዛ', price: '690', image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&auto=format&fit=crop', prep: '20 min', available: true },
            { id: 'pz8', category: 'pizza', nameEn: 'Fasting Tuna Pizza', nameAm: 'የጾም ቱና ፒዛ', price: '650', image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&auto=format&fit=crop', prep: '15 min', available: true },
            { id: 'pz9', category: 'pizza', nameEn: 'Family Pizza', nameAm: 'ፋሚሊ ፒዛ', price: '1470', image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&auto=format&fit=crop', prep: '25 min', available: true },

            // EXTRA
            { id: 'ex1', category: 'extra', nameEn: 'Extra Cheese', nameAm: 'ተጨማሪ ቺዝ', price: '80', image: 'https://images.unsplash.com/photo-1552767059-ce182ead8c1b?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex2', category: 'extra', nameEn: 'Extra Bread', nameAm: 'ተጨማሪ ዳቦ', price: '40', image: 'https://images.unsplash.com/photo-1509440159596-0249088772ff?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex3', category: 'extra', nameEn: 'Extra Egg', nameAm: 'ተጨማሪ እንቁላል', price: '45', image: 'https://images.unsplash.com/photo-1516467508483-a7212febe31a?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'ex4', category: 'extra', nameEn: 'Extra Mayonnaise', nameAm: 'ተጨማሪ ማዮኔዝ', price: '80', image: 'https://images.unsplash.com/photo-1585238342024-78d387f4a707?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex5', category: 'extra', nameEn: 'Juice Cup', nameAm: 'የጁስ ብርጭቆ', price: '25', image: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex6', category: 'extra', nameEn: 'Burger Box', nameAm: 'የበርገር ሳጥን', price: '50', image: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex7', category: 'extra', nameEn: 'Pizza Box', nameAm: 'የፒዛ ሳጥን', price: '85', image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex8', category: 'extra', nameEn: 'Extra Tuna 1/2', nameAm: 'ተጨማሪ ቱና 1/2', price: '150', image: 'https://images.unsplash.com/photo-1509722747041-616f39b57569?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex9', category: 'extra', nameEn: 'Extra Tuna', nameAm: 'ተጨማሪ ቱና', price: '270', image: 'https://images.unsplash.com/photo-1509722747041-616f39b57569?w=500&auto=format&fit=crop', prep: 'Instant', available: true },
            { id: 'ex10', category: 'extra', nameEn: 'Coffee Cup', nameAm: 'የቡና ብርጭቆ', price: '20', image: 'https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?w=500&auto=format&fit=crop', prep: 'Instant', available: true },

            // JUICE
            { id: 'j1', category: 'juice', nameEn: 'Avocado Mix', nameAm: 'አቮካዶ ሚክስ', price: '310 / 360', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j2', category: 'juice', nameEn: 'Avocado', nameAm: 'አቮካዶ ጁስ', price: '330 / 370', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j3', category: 'juice', nameEn: 'Mango', nameAm: 'ማንጎ ጁስ', price: '320 / 350', image: 'https://images.unsplash.com/photo-1553279768-865429fa0078?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j4', category: 'juice', nameEn: 'Strawberry', nameAm: 'ስትሮቤሪ ጁስ', price: '300 / 350', image: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j5', category: 'juice', nameEn: 'Papaya', nameAm: 'ፓፓያ ጁስ', price: '250 / 270', image: 'https://images.unsplash.com/photo-1517256064527-09c73fc73e38?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j6', category: 'juice', nameEn: 'Pineapple', nameAm: 'አናናስ ጁስ', price: '270 / 300', image: 'https://images.unsplash.com/photo-1550258987-190a2d41a8ba?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j7', category: 'juice', nameEn: 'Watermelon', nameAm: 'ሐብሐብ ጁስ', price: '270 / 300', image: 'https://images.unsplash.com/photo-1587049352847-81a56d773cae?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j8', category: 'juice', nameEn: 'Mix Juice', nameAm: 'ሚክስ ጁስ', price: '250 / 290', image: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j9', category: 'juice', nameEn: 'Flaxseed Juice', nameAm: 'የተልባ ጁስ', price: '270 / 300', image: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j10', category: 'juice', nameEn: 'Sugarcane Juice', nameAm: 'የሸንኮራ አገዳ ጁስ', price: '220 / 240', image: 'https://images.unsplash.com/photo-1534353473418-4cfa6c56fd38?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j11', category: 'juice', nameEn: 'Lemon Juice', nameAm: 'ሎሚ ጁስ', price: '220 / 240', image: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j12', category: 'juice', nameEn: 'Carrot Juice', nameAm: 'ካሮት ጁስ', price: '220 / 240', image: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j13', category: 'juice', nameEn: 'Ginger Juice', nameAm: 'ዝንጅብል ጁስ', price: '230 / 250', image: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j14', category: 'juice', nameEn: 'Mango Mix', nameAm: 'ማንጎ ሚክስ', price: '300 / 340', image: 'https://images.unsplash.com/photo-1553279768-865429fa0078?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j15', category: 'juice', nameEn: 'Strawberry Mix', nameAm: 'ስትሮቤሪ ሚክስ', price: '300 / 340', image: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'j16', category: 'juice', nameEn: 'Orange Mix', nameAm: 'ብርትኳን ሚክስ', price: '300 / 340', image: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=500&auto=format&fit=crop', prep: '5 min', available: true },

            // SHAKE
            { id: 'sk1', category: 'shake', nameEn: 'Special Shake', nameAm: 'ስፔሻል ሼክ', price: '300 / 350', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'sk2', category: 'shake', nameEn: 'Mango Shake', nameAm: 'ማንጎ ሼክ', price: '350 / 380', image: 'https://images.unsplash.com/photo-1553279768-865429fa0078?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'sk3', category: 'shake', nameEn: 'Avocado Shake', nameAm: 'አቮካዶ ሼክ', price: '350 / 380', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'sk4', category: 'shake', nameEn: 'Papaya Shake', nameAm: 'ፓፓያ ሼክ', price: '260 / 280', image: 'https://images.unsplash.com/photo-1517256064527-09c73fc73e38?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'sk5', category: 'shake', nameEn: 'Watermelon Shake', nameAm: 'ሐብሐብ ሼክ', price: '260 / 280', image: 'https://images.unsplash.com/photo-1587049352847-81a56d773cae?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'sk6', category: 'shake', nameEn: 'Banana Shake', nameAm: 'ሙዝ ሼክ', price: '260 / 280', image: 'https://images.unsplash.com/photo-1528825871115-3581a5387919?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'sk7', category: 'shake', nameEn: 'Sugarcane Shake', nameAm: 'የሸንኮራ አገዳ ሼክ', price: '260 / 290', image: 'https://images.unsplash.com/photo-1534353473418-4cfa6c56fd38?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'sk8', category: 'shake', nameEn: 'Strawberry Shake', nameAm: 'ስትሮቤሪ ሼክ', price: '260 / 380', image: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500&auto=format&fit=crop', prep: '8 min', available: true },

            // MILK SHAKE
            { id: 'ms1', category: 'milkshake', nameEn: 'Chocolate Shake', nameAm: 'ቾኮሌት ሚልካ ሼክ', price: '420', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'ms2', category: 'milkshake', nameEn: 'Oreo Shake', nameAm: 'ኦሪዮ ሚልካ ሼክ', price: '410', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'ms3', category: 'milkshake', nameEn: 'Vanilla Shake', nameAm: 'ቫኒላ ሚልካ ሼክ', price: '350', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'ms4', category: 'milkshake', nameEn: 'Mix Shake', nameAm: 'ሚክስ ሚልካ ሼክ', price: '340', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'ms5', category: 'milkshake', nameEn: 'Protein Shake', nameAm: 'ፕሮቲን ሼክ', price: '480', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'ms6', category: 'milkshake', nameEn: 'Family Shake', nameAm: 'ፋሚሊ ሼክ', price: '690', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '10 min', available: true },

            // MOJITO
            { id: 'mj1', category: 'mojito', nameEn: 'Strawberry Mojito', nameAm: 'ስትሮቤሪ ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj2', category: 'mojito', nameEn: 'Orange Mojito', nameAm: 'ኦሬንጅ ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj3', category: 'mojito', nameEn: 'Kiwi Mojito', nameAm: 'ኪዊ ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj4', category: 'mojito', nameEn: 'Lemon Mojito', nameAm: 'ሌመን ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj5', category: 'mojito', nameEn: 'Chocolate Mojito', nameAm: 'ቾኮሌት ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj6', category: 'mojito', nameEn: 'Pineapple Mojito', nameAm: 'አናናስ ሞሂቶ', price: '300', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj7', category: 'mojito', nameEn: 'Special Mojito', nameAm: 'ስፔሻል ሞሂቶ', price: '300', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj8', category: 'mojito', nameEn: 'Avatar Mojito', nameAm: 'አቫታር ሞሂቶ', price: '300', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj9', category: 'mojito', nameEn: 'King Mojito', nameAm: 'ኪንግ ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj10', category: 'mojito', nameEn: 'Sky Mojito', nameAm: 'ስካይ ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'mj11', category: 'mojito', nameEn: 'Snuzzy Mojito', nameAm: 'ስነዚ ሞሂቶ', price: '295', image: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop', prep: '5 min', available: true },

            // ICE ORDER
            { id: 'io1', category: 'iceorder', nameEn: 'Iced Tea', nameAm: 'አይስድ ቲ', price: '120', image: 'https://images.unsplash.com/photo-1556679343-c7306c1976bc?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io2', category: 'iceorder', nameEn: 'Ice Latte', nameAm: 'አይስ ላቴ', price: '230', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io3', category: 'iceorder', nameEn: 'Iced Caramel', nameAm: 'አይስ ካራሜል', price: '210', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io4', category: 'iceorder', nameEn: 'Iced Mocha', nameAm: 'አይስ ሞካ', price: '230', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io5', category: 'iceorder', nameEn: 'Iced Strawberry', nameAm: 'አይስ ስትሮቤሪ', price: '180', image: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io6', category: 'iceorder', nameEn: 'Iced Chocolate', nameAm: 'አይስ ቾኮሌት', price: '230', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io7', category: 'iceorder', nameEn: 'Lemonade', nameAm: 'ሌሞኔድ', price: '180', image: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io8', category: 'iceorder', nameEn: 'Strawberry w/ Chocolate', nameAm: 'ስትሮቤሪ ከቾኮሌት ጋር', price: '260', image: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io9', category: 'iceorder', nameEn: 'Caramel Ice Latte', nameAm: 'ካራሜል አይስ ላቴ', price: '260', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io10', category: 'iceorder', nameEn: 'Caramel Ice Coffee', nameAm: 'ካራሜል አይስ ቡና', price: '280', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io11', category: 'iceorder', nameEn: 'Ice Coffee', nameAm: 'አይስ ቡና', price: '240', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'io12', category: 'iceorder', nameEn: 'Mixed Ice Latte', nameAm: 'ሚክስድ አይስ ላቴ', price: '350', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },

            // HOT DRINK
            { id: 'hd1', category: 'hotdrink', nameEn: 'Tea', nameAm: 'ሻይ', price: '70', image: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500&auto=format&fit=crop', prep: '3 min', available: true },
            { id: 'hd2', category: 'hotdrink', nameEn: 'Coffee', nameAm: 'ቡና', price: '140', image: 'https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd3', category: 'hotdrink', nameEn: 'Macchiato', nameAm: 'ማኪያቶ', price: '150', image: 'https://images.unsplash.com/photo-1485808191679-5f86510681a2?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd4', category: 'hotdrink', nameEn: 'Spice Tea', nameAm: 'የቅመም ሻይ', price: '90', image: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd5', category: 'hotdrink', nameEn: 'Espresso', nameAm: 'ኤስፕሬሶ', price: '150', image: 'https://images.unsplash.com/photo-1510591509098-f4fdc6d0ff04?w=500&auto=format&fit=crop', prep: '3 min', available: true },
            { id: 'hd6', category: 'hotdrink', nameEn: 'Ginger Tea', nameAm: 'የዝንጅብል ሻይ', price: '90', image: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd7', category: 'hotdrink', nameEn: 'Cappuccino', nameAm: 'ካፑቺኖ', price: '150', image: 'https://images.unsplash.com/photo-1534778101976-62847782c213?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd8', category: 'hotdrink', nameEn: 'Latte', nameAm: 'ላቴ', price: '140', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd9', category: 'hotdrink', nameEn: 'Milk', nameAm: 'ወተት', price: '140', image: 'https://images.unsplash.com/photo-1550583724-b2692b85b150?w=500&auto=format&fit=crop', prep: '3 min', available: true },
            { id: 'hd10', category: 'hotdrink', nameEn: 'Hot Chocolate', nameAm: 'ሆት ቾኮሌት', price: '150', image: 'https://images.unsplash.com/photo-1542990253-0d0f5be5f0ed?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd11', category: 'hotdrink', nameEn: 'Special Tea', nameAm: 'ስፔሻል ሻይ', price: '150', image: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'hd12', category: 'hotdrink', nameEn: 'Mocha', nameAm: 'ሞካ', price: '130', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop', prep: '5 min', available: true },

            // YOGURT
            { id: 'yg1', category: 'yogurt', nameEn: 'Caramel Yogurt', nameAm: 'ካራሜል እርጎ', price: '310', image: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'yg2', category: 'yogurt', nameEn: 'Fruit Yogurt', nameAm: 'ፍሩት እርጎ', price: '310', image: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'yg3', category: 'yogurt', nameEn: 'Flavored Yogurt', nameAm: 'ፍላቨርድ እርጎ', price: '310', image: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'yg4', category: 'yogurt', nameEn: 'Strawberry Yogurt', nameAm: 'ስትሮቤሪ እርጎ', price: '310', image: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=500&auto=format&fit=crop', prep: '5 min', available: true },

            // FRAPPUCCINO
            { id: 'fp1', category: 'frappuccino', nameEn: 'Chocolate Frappuccino', nameAm: 'ቾኮሌት ፍራፑቺኖ', price: '380', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'fp2', category: 'frappuccino', nameEn: 'Caramel Frappuccino', nameAm: 'ካራሜል ፍራፑቺኖ', price: '330', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },
            { id: 'fp3', category: 'frappuccino', nameEn: 'Mocha Frappuccino', nameAm: 'ሞካ ፍራፑቺኖ', price: '350', image: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop', prep: '8 min', available: true },

            // OTHER
            { id: 'ot1', category: 'other', nameEn: 'Oat Juice', nameAm: 'የአሜካራ/ኦት ጁስ', price: '250', image: 'https://images.unsplash.com/photo-1613478223719-2ab802602423?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'ot2', category: 'other', nameEn: 'Detox', nameAm: 'ዲቶክስ', price: '110', image: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=500&auto=format&fit=crop', prep: '5 min', available: true },
            { id: 'ot3', category: 'other', nameEn: 'Mint', nameAm: 'ናና (ሚንት)', price: '230', image: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=500&auto=format&fit=crop', prep: '5 min', available: true }
        ];

        // --- 2. STATE MANAGEMENT ---
        let menuItems = JSON.parse(localStorage.getItem('ero_menu_items')) || initialMenuItems;
        let activeCategory = 'all';
        let currentLang = localStorage.getItem('ero_lang') || 'en';
        let favorites = JSON.parse(localStorage.getItem('ero_favorites')) || [];
        let showFavsOnly = false;
        let isAdminLoggedIn = false;

        // --- 3. APPLICATION INITIALIZATION ---
        document.addEventListener('DOMContentLoaded', () => {
            initTheme();
            renderCategoryChips();
            renderHomeCategories();
            renderHomeSpecials();
            renderMenuItems();
            applyLanguage();
            updateStats();
        });

        // --- 4. NAVIGATION SYSTEM ---
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

        // --- 5. RENDER MENU & DYNAMIC UI ---
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

        function renderHomeCategories() {
            const container = document.getElementById('homeCategoriesList');
            if (!container) return;
            const displayCats = CATEGORIES.filter(c => c.id !== 'all').slice(0, 6);
            container.innerHTML = displayCats.map(cat => `
                <div onclick="showPage('menu'); selectCategory('${cat.id}');" class="glass p-4 rounded-2xl text-center cursor-pointer hover:scale-105 transition-all shadow-sm group border border-slate-200/50 dark:border-slate-800">
                    <div class="w-12 h-12 rounded-xl bg-brand-light dark:bg-slate-800 text-brand-sky flex items-center justify-center mx-auto text-xl mb-2 group-hover:bg-brand-sky group-hover:text-white transition">
                        <i class="fa-solid fa-utensils"></i>
                    </div>
                    <h4 class="font-bold text-xs sm:text-sm text-slate-800 dark:text-slate-100">${cat[currentLang]}</h4>
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
                <div class="glass rounded-3xl overflow-hidden shadow-sm hover:shadow-xl transition-all duration-300 flex flex-col justify-between group border border-slate-200/50 dark:border-slate-800">
                    <div class="relative overflow-hidden cursor-pointer" onclick="openImageModal('${item.image}', '${name}', '${item.price}')">
                        <img src="${item.image}" alt="${name}" class="w-full h-48 object-cover group-hover:scale-105 transition duration-500">
                        <button onclick="event.stopPropagation(); toggleFavorite('${item.id}')" class="absolute top-3 right-3 w-9 h-9 rounded-full glass flex items-center justify-center text-slate-400 hover:text-red-500 transition shadow-md">
                            <i class="${isFav ? 'fa-solid text-red-500' : 'fa-regular'} fa-heart"></i>
                        </button>
                        ${!item.available ? '<span class="absolute bottom-3 left-3 px-2.5 py-1 rounded-full bg-red-500/80 backdrop-blur-md text-white text-[10px] font-bold tracking-wider uppercase">Out of Stock</span>' : ''}
                    </div>
                    <div class="p-5 space-y-3 flex-1 flex flex-col justify-between">
                        <div>
                            <div class="flex justify-between items-start gap-2">
                                <h3 class="font-bold text-base text-slate-800 dark:text-white leading-snug">${name}</h3>
                            </div>
                            <p class="text-xs text-slate-400 mt-1"><i class="fa-regular fa-clock mr-1"></i>${item.prep || '10-15 min'}</p>
                        </div>
                        <div class="flex items-center justify-between pt-2 border-t border-slate-200/40 dark:border-slate-800">
                            <div>
                                <span class="text-xs text-slate-400 font-medium">Price</span>
                                <p class="text-brand-sky font-extrabold text-base leading-tight">${item.price} <span class="text-[10px] font-normal text-slate-500">ETB</span></p>
                            </div>
                        </div>
                    </div>
                </div>
            `;
        }

        // --- 6. FILTERING & CONTROLS ---
        function selectCategory(catId) {
            activeCategory = catId;
            renderCategoryChips();
            renderMenuItems();
        }

        function filterMenu() {
            renderMenuItems();
        }

        function toggleFavoritesOnly() {
            showFavsOnly = !showFavsOnly;
            const btn = document.getElementById('favToggleBtn');
            if (btn) btn.classList.toggle('bg-red-50', showFavsOnly);
            renderMenuItems();
        }

        function toggleFavorite(itemId) {
            if (favorites.includes(itemId)) {
                favorites = favorites.filter(id => id !== itemId);
            } else {
                favorites.push(itemId);
            }
            localStorage.setItem('ero_favorites', JSON.stringify(favorites));
            renderMenuItems();
            renderHomeSpecials();
        }

        function resetFilters() {
            activeCategory = 'all';
            showFavsOnly = false;
            document.getElementById('searchInput').value = '';
            renderCategoryChips();
            renderMenuItems();
        }

        // --- 7. LANGUAGE SWITCHER ---
        function toggleLanguage() {
            currentLang = currentLang === 'en' ? 'am' : 'en';
            localStorage.setItem('ero_lang', currentLang);
            document.getElementById('langLabel').innerText = currentLang === 'en' ? 'AM' : 'EN';
            applyLanguage();
            renderCategoryChips();
            renderHomeCategories();
            renderHomeSpecials();
            renderMenuItems();
            if (isAdminLoggedIn) renderAdminTable();
        }

        function applyLanguage() {
            document.querySelectorAll('[data-en]').forEach(el => {
                if (el.dataset[currentLang]) {
                    el.innerText = el.dataset[currentLang];
                }
            });
        }

        // --- 8. THEME TOGGLE (DARK MODE) ---
        function toggleDarkMode() {
            const isDark = document.documentElement.classList.toggle('dark');
            localStorage.setItem('ero_theme', isDark ? 'dark' : 'light');
            updateThemeIcon(isDark);
        }

        function initTheme() {
            const savedTheme = localStorage.getItem('ero_theme');
            const isDark = savedTheme === 'dark' || (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches);
            if (isDark) document.documentElement.classList.add('dark');
            updateThemeIcon(isDark);
        }

        function updateThemeIcon(isDark) {
            const icon = document.getElementById('themeIcon');
            if (icon) icon.className = isDark ? 'fa-solid fa-sun text-lg text-amber-400' : 'fa-solid fa-moon text-lg';
        }

        // --- 9. MODALS (IMAGE VIEWER & FORMS) ---
        function openImageModal(imgUrl, title, price) {
            document.getElementById('modalImg').src = imgUrl;
            document.getElementById('modalTitle').innerText = title;
            document.getElementById('modalPrice').innerText = price + ' ETB';
            document.getElementById('imageModal').classList.remove('hidden');
        }

        function closeImageModal() {
            document.getElementById('imageModal').classList.add('hidden');
        }

        // --- 10. ADMIN DASHBOARD & MANAGEMENT ---
        function verifyAdmin() {
            const pass = document.getElementById('adminPassInput').value;
            if (pass === 'admin123' || pass === 'ero2026') {
                isAdminLoggedIn = true;
                document.getElementById('adminAuthBlock').classList.add('hidden');
                document.getElementById('adminDashboardContent').classList.remove('hidden');
                renderAdminTable();
                populateCategorySelect();
            } else {
                alert('Incorrect password!');
            }
        }

        function updateStats() {
            document.getElementById('statTotalItems').innerText = menuItems.length;
            document.getElementById('statActiveItems').innerText = menuItems.filter(i => i.available).length;
        }

        function renderAdminTable() {
            const tbody = document.getElementById('adminTableBody');
            if (!tbody) return;
            tbody.innerHTML = menuItems.map(item => `
                <tr class="hover:bg-slate-50 dark:hover:bg-slate-900/50 transition">
                    <td class="p-4 font-semibold flex items-center gap-3">
                        <img src="${item.image}" class="w-10 h-10 rounded-xl object-cover">
                        <div>
                            <p>${item.nameEn}</p>
                            <p class="text-xs text-slate-400 font-normal">${item.nameAm}</p>
                        </div>
                    </td>
                    <td class="p-4 capitalize text-slate-500">${item.category}</td>
                    <td class="p-4 font-bold text-brand-sky">${item.price} ETB</td>
                    <td class="p-4">
                        <span class="px-2.5 py-1 rounded-full text-xs font-semibold ${item.available ? 'bg-emerald-100 dark:bg-emerald-900/40 text-emerald-600' : 'bg-red-100 dark:bg-red-900/40 text-red-600'}">
                            ${item.available ? 'Active' : 'Out of Stock'}
                        </span>
                    </td>
                    <td class="p-4 text-right space-x-2">
                        <button onclick="editMenuItem('${item.id}')" class="p-2 text-slate-400 hover:text-brand-sky transition"><i class="fa-solid fa-pen"></i></button>
                        <button onclick="deleteMenuItem('${item.id}')" class="p-2 text-slate-400 hover:text-red-500 transition"><i class="fa-solid fa-trash"></i></button>
                    </td>
                </tr>
            `).join('');
            updateStats();
        }

        function populateCategorySelect() {
            const select = document.getElementById('formCategory');
            if (!select) return;
            select.innerHTML = CATEGORIES.filter(c => c.id !== 'all').map(c => `<option value="${c.id}">${c.en}</option>`).join('');
        }

        function openItemModal(itemId = null) {
            populateCategorySelect();
            if (itemId) {
                const item = menuItems.find(i => i.id === itemId);
                document.getElementById('modalFormTitle').innerText = 'Edit Item';
                document.getElementById('formItemId').value = item.id;
                document.getElementById('formNameEn').value = item.nameEn;
                document.getElementById('formNameAm').value = item.nameAm;
                document.getElementById('formCategory').value = item.category;
                document.getElementById('formPrice').value = item.price;
                document.getElementById('formImage').value = item.image;
                document.getElementById('formPrep').value = item.prep || '';
                document.getElementById('formAvailable').checked = item.available;
            } else {
                document.getElementById('modalFormTitle').innerText = 'Add New Item';
                document.getElementById('menuItemForm').reset();
                document.getElementById('formItemId').value = '';
            }
            document.getElementById('itemFormModal').classList.remove('hidden');
        }

        function closeFormModal() {
            document.getElementById('itemFormModal').classList.add('hidden');
        }

        function saveMenuItem(event) {
            event.preventDefault();
            const id = document.getElementById('formItemId').value;
            const newItem = {
                id: id || 'item_' + Date.now(),
                category: document.getElementById('formCategory').value,
                nameEn: document.getElementById('formNameEn').value,
                nameAm: document.getElementById('formNameAm').value,
                price: document.getElementById('formPrice').value,
                image: document.getElementById('formImage').value,
                prep: document.getElementById('formPrep').value || '10-15 min',
                available: document.getElementById('formAvailable').checked
            };

            if (id) {
                const index = menuItems.findIndex(i => i.id === id);
                menuItems[index] = newItem;
            } else {
                menuItems.push(newItem);
            }

            localStorage.setItem('ero_menu_items', JSON.stringify(menuItems));
            renderMenuItems();
            renderHomeSpecials();
            renderAdminTable();
            closeFormModal();
        }

        function editMenuItem(id) {
            openItemModal(id);
        }

        function deleteMenuItem(id) {
            if (confirm('Are you sure you want to delete this menu item?')) {
                menuItems = menuItems.filter(i => i.id !== id);
                localStorage.setItem('ero_menu_items', JSON.stringify(menuItems));
                renderMenuItems();
                renderHomeSpecials();
                renderAdminTable();
            }
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

        function handleContactSubmit(e) {
            e.preventDefault();
            alert(currentLang === 'am' ? 'መልእክትዎ በትክክል ተልኳል! እናመሰግናለን።' : 'Thank you! Your message has been sent.');
            e.target.reset();
        }
    </script>
</body>
</html>
