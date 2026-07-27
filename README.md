
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ፍቅር レストラン (Fikir Restaurant)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
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
            <h1 class="text-xl font-bold text-gray-900" id="header-title">Menu</h1>
            <div class="flex items-center gap-2">
                <!-- Language Switcher Button -->
                <button onclick="toggleLanguage()" class="bg-emerald-800 text-white px-2.5 py-1 rounded-lg text-xs font-semibold shadow hover:bg-emerald-700 transition">
                    🌐 <span id="lang-btn-text">አማርኛ</span>
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
                <input type="text" id="search-input" oninput="searchMenu()" placeholder="Search..." class="w-full bg-gray-100 pl-10 pr-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-emerald-800">
            </div>

            <!-- Categories -->
            <div class="flex gap-2 overflow-x-auto no-scrollbar pb-1">
                <button onclick="filterMenu('all')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-emerald-900 text-white whitespace-nowrap shadow" data-am="ሁሉም" data-en="All">All</button>
                <button onclick="filterMenu('fasting')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="ጾም" data-en="Fasting">Fasting</button>
                <button onclick="filterMenu('non-fasting')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="ፍስክ" data-en="Non-Fasting">Non-Fasting</button>
                <button onclick="filterMenu('breakfast')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="ቁርስ" data-en="Breakfast">Breakfast</button>
                <button onclick="filterMenu('drink')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-gray-100 text-gray-600 whitespace-nowrap hover:bg-gray-200" data-am="መጠጥ" data-en="Drinks">Drinks</button>
            </div>

            <!-- Menu Grid -->
            <div id="menu-container" class="grid grid-cols-2 gap-3">
                <!-- JS በኩል ይሞላል -->
            </div>
        </main>

        <!-- Bottom Navigation Bar -->
        <nav class="absolute bottom-0 left-0 right-0 bg-white border-t border-gray-200 py-3 px-6 flex justify-around items-center text-gray-400 z-20 shrink-0">
            <button onclick="filterMenu('all')" class="text-emerald-900 flex flex-col items-center text-xs font-bold"><i class="fa-solid fa-utensils text-lg"></i><span id="nav-menu">Menu</span></button>
            <button onclick="alert(currentLang === 'am' ? 'ተወዳጅ ምግቦችዎ' : 'Your Favorites')" class="hover:text-emerald-900 flex flex-col items-center text-xs"><i class="fa-regular fa-heart text-lg"></i><span id="nav-fav">Favorite</span></button>
            <button onclick="toggleCart()" class="hover:text-emerald-900 flex flex-col items-center text-xs"><i class="fa-regular fa-file-lines text-lg"></i><span id="nav-orders">Orders</span></button>
            <button onclick="alert(currentLang === 'am' ? 'የተጠቃሚ መለያ' : 'User Profile')" class="hover:text-emerald-900 flex flex-col items-center text-xs"><i class="fa-regular fa-user text-lg"></i><span id="nav-profile">Profile</span></button>
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
                    Add to cart
                </button>
            </div>
        </div>
    </div>

    <!-- Shopping Cart & Orders Sidebar -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-full sm:w-80 bg-white shadow-2xl p-5 transform translate-x-full transition-transform duration-300 z-50 flex flex-col border-l border-gray-200">
        <div class="flex justify-between items-center mb-4 border-b pb-3">
            <h3 class="text-lg font-bold text-gray-900" id="cart-sidebar-title">Your Cart</h3>
            <button onclick="toggleCart()" class="text-gray-400 hover:text-black font-bold text-xl px-2">✕</button>
        </div>

        <!-- Table Number Input -->
        <div class="mb-3">
            <label class="block text-xs font-semibold text-gray-600 mb-1" id="table-label">የጠረጴዛ ቁጥር (Table Number):</label>
            <input type="number" id="table-number" placeholder="ምሳሌ: 4" class="w-full bg-gray-100 border border-gray-200 px-3 py-2 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-emerald-800">
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-3 pr-1">
            <!-- እቃዎች እዚህ ይገባሉ -->
        </div>

        <div class="border-t pt-4 mt-2">
            <div class="flex justify-between font-bold text-base mb-4">
                <span id="total-text">Total:</span>
                <span id="total-price" class="text-emerald-900">0.00 ETB</span>
            </div>
            <button onclick="checkout()" class="w-full bg-[#114b3e] text-white py-3 rounded-xl font-bold hover:bg-emerald-950 shadow transition text-sm">
                <span id="order-btn-text">Send Order via Telegram</span>
            </button>
        </div>
    </div>

    <!-- JavaScript Logic -->
    <script>
        let currentLang = 'am';

        const translations = {
            en: {
                headerTitle: "Menu",
                searchPlaceholder: "Search...",
                navMenu: "Menu",
                navFav: "Favorite",
                navOrders: "Orders",
                navProfile: "Profile",
                addToCart: "Add to cart",
                cartTitle: "Your Cart",
                tableLabel: "Table Number:",
                totalText: "Total:",
                orderBtn: "Send Order via Telegram",
                emptyCart: "Your cart is empty",
                categories: { all: "All", fasting: "Fasting", "non-fasting": "Non-Fasting", breakfast: "Breakfast", drink: "Drinks" }
            },
            am: {
                headerTitle: "ምግብ ዝርዝር",
                searchPlaceholder: "ይፈልጉ...",
                navMenu: "ሜኑ",
                navFav: "ተወዳጅ",
                navOrders: "ትዕዛዞች",
                navProfile: "መለያ",
                addToCart: "ወደ ጋሪ ጨምር",
                cartTitle: "የመረጧቸው እቃዎች",
                tableLabel: "የጠረጴዛ ቁጥር (Table Number):",
                totalText: "አጠቃላይ ዋጋ:",
                orderBtn: "ትዕዛዝ በቴሌግራም ላክ",
                emptyCart: "ጋሪዎ ባዶ ነው",
                categories: { all: "ሁሉም", fasting: "ጾም", "non-fasting": "ፍስክ", breakfast: "ቁርስ", drink: "መጠጥ" }
            }
        };

        const menuItems = [
            { 
                id: 1, 
                name: { am: "የጾም ፍርፍር", en: "Fasting Firfir" }, 
                category: "fasting", 
                price: 150.00, 
                rating: 5, 
                time: "15 min",
                desc: { 
                    am: "በዘይት፣ ሽንኩርት እና በርበሬ የተዘጋጀ ጣፋጭ የጾም ፍርፍር።", 
                    en: "Delicious fasting firfir prepared with oil, onions, and berbere." 
                },
                image: "https://images.unsplash.com/photo-1541544741938-0af808871cc0?w=500" 
            },
            { 
                id: 2, 
                name: { am: "ዶሮ ወጥ (ፍስክ)", en: "Doro Wat (Non-Fasting)" }, 
                category: "non-fasting", 
                price: 450.00, 
                rating: 5, 
                time: "30 min",
                desc: { 
                    am: "በንጹህ ቅቤ፣ ዶሮ እና እንቁላል የተዘጋጀ ባህላዊ የፍስክ ወጥ።", 
                    en: "Traditional non-fasting chicken stew prepared with spiced butter and eggs." 
                },
                image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" 
            },
            { 
                id: 3, 
                name: { am: "አቮካዶ ጁስ (ጾም)", en: "Avocado Juice (Fasting)" }, 
                category: "fasting", 
                price: 120.00, 
                rating: 5, 
                time: "10 min",
                desc: { 
                    am: "ከተፈጥሮ አቮካዶ የተሰራ ንጹህ የጾም ጁስ።", 
                    en: "Fresh and pure fasting avocado juice." 
                },
                image: "https://images.unsplash.com/photo-1556881286-fc6915169721?w=500" 
            },
            { 
                id: 4, 
                name: { am: "እንቁላል ሳዊች (ፍስክ)", en: "Egg Sandwich" }, 
                category: "breakfast", 
                price: 90.00, 
                rating: 5, 
                time: "10 min",
                desc: { 
                    am: "ትኩስ ዳቦ እና የተጠበሰ እንቁላል ለቁርስ።", 
                    en: "Fresh toasted bread served with fried egg." 
                },
                image: "https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500" 
            }
        ];

        let cart = [];
        let currentFilter = 'all';

        function toggleLanguage() {
            currentLang = currentLang === 'am' ? 'en' : 'am';
            document.getElementById('lang-btn-text').innerText = currentLang === 'am' ? 'English' : 'አማርኛ';
            
            document.getElementById('header-title').innerText = translations[currentLang].headerTitle;
            document.getElementById('search-input').placeholder = translations[currentLang].searchPlaceholder;
            document.getElementById('nav-menu').innerText = translations[currentLang].navMenu;
            document.getElementById('nav-fav').innerText = translations[currentLang].navFav;
            document.getElementById('nav-orders').innerText = translations[currentLang].navOrders;
            document.getElementById('nav-profile').innerText = translations[currentLang].navProfile;
            document.getElementById('cart-sidebar-title').innerText = translations[currentLang].cartTitle;
            document.getElementById('table-label').innerText = translations[currentLang].tableLabel;
            document.getElementById('total-text').innerText = translations[currentLang].totalText;
            document.getElementById('order-btn-text').innerText = translations[currentLang].orderBtn;
            document.getElementById('modal-add-btn').innerText = translations[currentLang].addToCart;

            const catButtons = document.querySelectorAll('.cat-btn');
            catButtons.forEach(btn => {
                const catKey = btn.getAttribute('onclick').match(/'([^']+)'/)[1];
                btn.innerText = translations[currentLang].categories[catKey];
            });

            filterMenu(currentFilter);
            updateCartUI();
        }

        function filterMenu(category) {
            currentFilter = category;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                btn.classList.remove('bg-emerald-900', 'text-white', 'shadow');
                btn.classList.add('bg-gray-100', 'text-gray-600');
            });
            event && event.target.classList.remove('bg-gray-100', 'text-gray-600');
            event && event.target.classList.add('bg-emerald-900', 'text-white', 'shadow');

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
                <div onclick="openDetail(${item.id})" class="bg-gray-50 rounded-2xl p-2.5 shadow-sm hover:shadow-md transition cursor-pointer flex flex-col justify-between border border-gray-100">
                    <div>
                        <img src="${item.image}" alt="" class="w-full h-28 object-cover rounded-xl mb-2">
                        <h4 class="font-bold text-xs text-gray-900 line-clamp-1">${item.name[currentLang]}</h4>
                        <div class="text-yellow-500 text-[10px] my-0.5">★★★★★</div>
                    </div>
                    <div class="flex justify-between items-center mt-2">
                        <span class="text-emerald-900 font-extrabold text-xs">${item.price.toFixed(2)} ETB</span>
                        <button onclick="event.stopPropagation(); addToCart(${item.id})" class="w-6 h-6 bg-emerald-900 text-white rounded-full flex items-center justify-center text-[10px] shadow hover:bg-emerald-800"><i class="fa-solid fa-plus"></i></button>
                    </div>
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
            cart.push(item);
            updateCartUI();
            toggleCart();
        }

        function updateCartUI() {
            document.getElementById('cart-count').innerText = cart.length;
            const container = document.getElementById('cart-items');
            
            if (cart.length === 0) {
                container.innerHTML = `<p class='text-gray-400 text-center py-8 text-xs'>${translations[currentLang].emptyCart}</p>`;
                document.getElementById('total-price').innerText = "0.00 ETB";
                return;
            }

            let total = 0;
            container.innerHTML = cart.map((item, index) => {
                total += item.price;
                return `
                    <div class="flex justify-between items-center bg-gray-50 p-2.5 rounded-xl border border-gray-100">
                        <div>
                            <h5 class="font-semibold text-xs text-gray-900">${item.name[currentLang]}</h5>
                            <p class="text-[11px] text-emerald-900 font-bold">${item.price.toFixed(2)} ETB</p>
                        </div>
                        <button onclick="removeFromCart(${index})" class="text-red-400 text-xs font-bold px-2 py-1 hover:text-red-600">✕</button>
                    </div>
                `;
            }).join('');

            document.getElementById('total-price').innerText = total.toFixed(2) + " ETB";
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        function toggleCart() {
            const sidebar = document.getElementById('cart-sidebar');
            sidebar.classList.toggle('translate-x-full');
        }

        function checkout() {
            if (cart.length === 0) {
                alert(currentLang === 'am' ? "እባክዎ መጀመሪያ እቃ ይምረጡ!" : "Please select items first!");
                return;
            }

            const tableNum = document.getElementById('table-number').value.trim();
            if (!tableNum) {
                alert(currentLang === 'am' ? "እባክዎ የጠረጴዛ ቁጥር ያስገቡ!" : "Please enter your table number!");
                return;
            }

            const telegramUsername = "lanyisu";
            let message = currentLang === 'am' ? `ሰላም! ከጠረጴዛ ቁጥር ${tableNum} የተላከ አዲስ ትዕዛዝ:\n\n` : `Hello! New order from Table #${tableNum}:\n\n`;
            let total = 0;

            cart.forEach((item, index) => {
                message += `${index + 1}. ${item.name[currentLang]} - ${item.price.toFixed(2)} ETB\n`;
                total += item.price;
            });

            message += `\n---------------------\n`;
            message += `Table Number / የጠረጴዛ ቁጥር: ${tableNum}\n`;
            message += `${translations[currentLang].totalText} ${total.toFixed(2)} ETB`;

            const telegramUrl = `https://t.me/${telegramUsername}?text=${encodeURIComponent(message)}`;
            window.open(telegramUrl, '_blank');

            cart = [];
            updateCartUI();
            toggleCart();
        }

        filterMenu('all');
    </script>
</body>
</html>
