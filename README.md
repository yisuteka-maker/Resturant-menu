<!DOCTYPE html>
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ፍቅር ሬስቶራንት (Fikir Restaurant)</title>
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

    <div class="w-full max-w-md bg-white shadow-xl overflow-hidden relative flex flex-col h-screen sm:h-[90vh] sm:rounded-[35px]">

        <!-- Header -->
        <header class="p-4 bg-white flex justify-between items-center border-b border-gray-100 z-10 shrink-0">
            <h1 class="text-xl font-bold text-gray-900" id="header-title">ምግብ ዝርዝር</h1>
            <div class="flex items-center gap-2">
                <button onclick="toggleLanguage()" class="bg-emerald-800 text-white px-2.5 py-1 rounded-lg text-xs font-semibold shadow hover:bg-emerald-700 transition">
                    🌐 <span id="lang-btn-text">English</span>
                </button>
                <button onclick="toggleCart()" class="bg-emerald-800 text-white p-2.5 rounded-full shadow hover:bg-emerald-700 transition relative">
                    <i class="fa-solid fa-bag-shopping"></i>
                    <span id="cart-count" class="absolute -top-1 -right-1 bg-red-500 text-white text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold">0</span>
                </button>
            </div>
        </header>

        <!-- Main Area -->
        <main class="flex-grow overflow-y-auto p-4 space-y-4 pb-24">
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

            <!-- Menu Vertical List -->
            <div id="menu-container" class="grid grid-cols-1 gap-3"></div>
        </main>

        <!-- Bottom Nav -->
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

    <!-- Shopping Cart Sidebar -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-full sm:w-80 bg-white shadow-2xl p-5 transform translate-x-full transition-transform duration-300 z-50 flex flex-col border-l border-gray-200">
        <div class="flex justify-between items-center mb-4 border-b pb-3">
            <h3 class="text-lg font-bold text-gray-900" id="cart-sidebar-title">የመረጧቸው እቃዎች</h3>
            <button onclick="toggleCart()" class="text-gray-400 hover:text-black font-bold text-xl px-2">✕</button>
        </div>

        <div class="mb-3">
            <label class="block text-xs font-semibold text-gray-600 mb-1" id="table-label">የጠረጴዛ ቁጥር (Table Number):</label>
            <input type="number" id="table-number" placeholder="ምሳሌ: 4" class="w-full bg-gray-100 border border-gray-200 px-3 py-2 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-emerald-800">
        </div>

        <div class="mb-3">
            <label class="block text-xs font-semibold text-gray-600 mb-1" id="note-label">ልዩ ማስታወሻ (Special Note):</label>
            <input type="text" id="order-note" placeholder="ለምሳሌ: ያለ በርበሬ ይሁን..." class="w-full bg-gray-100 border border-gray-200 px-3 py-2 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-emerald-800">
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-3 pr-1"></div>

        <div class="border-t pt-4 mt-2">
            <div class="flex justify-between font-bold text-base mb-4">
                <span id="total-text">አጠቃላይ ዋጋ:</span>
                <span id="total-price" class="text-emerald-900">0.00 ETB</span>
            </div>
            <button id="checkout-btn" onclick="checkout()" class="w-full bg-[#114b3e] text-white py-3 rounded-xl font-bold hover:bg-emerald-950 shadow transition text-sm flex items-center justify-center gap-2">
                <i class="fa-brands fa-telegram text-lg"></i>
                <span id="order-btn-text">ትዕዛዝ በቦት ላክ</span>
            </button>
            <p id="order-status" class="text-center text-xs mt-2 hidden"></p>
        </div>
    </div>

    <script>
        let currentLang = 'am';

        // 1. የቦት Token እና የGroup ID
        const BOT_TOKEN = "8752629354:AAHcNjUDff1NTP-_3RNUPqWAX1eFatfznKuU";
        const CHAT_ID = "-1004466655656"; // የርሶ የቴሌግራም ግሩፕ ID

        // የBackend URL ካለዎት እዚህ ያስገቡ (ለምሳሌ: http://localhost:3000/api/order)
        // ባዶ ከተወው በቀጥታ ወደ ቴሌግራም ግሩፕ ይልካል
        const BACKEND_API_URL = ""; 

        const translations = {
            en: {
                headerTitle: "Menu", searchPlaceholder: "Search...", navMenu: "Menu", navOrders: "Orders",
                addToCart: "Add to cart", orderBtnLabel: "Order", cartTitle: "Your Cart",
                tableLabel: "Table Number:", noteLabel: "Special Note:", totalText: "Total:",
                orderBtn: "Send Order via Bot", emptyCart: "Your cart is empty",
                sending: "Sending your order...", sent: "Order sent to group!", failed: "Could not send. Opening Telegram instead...",
                categories: { all: "All", fasting: "Fasting", "non-fasting": "Non-Fasting", breakfast: "Breakfast", drink: "Drinks" }
            },
            am: {
                headerTitle: "ምግብ ዝርዝር", searchPlaceholder: "ይፈልጉ...", navMenu: "ሜኑ", navOrders: "ትዕዛዞች",
                addToCart: "ወደ ጋሪ ጨምር", orderBtnLabel: "አዝዝ", cartTitle: "የመረጧቸው እቃዎች",
                tableLabel: "የጠረጴዛ ቁጥር (Table Number):", noteLabel: "ልዩ ማስታወሻ (Special Note):", totalText: "አጠቃላይ ዋጋ:",
                orderBtn: "ትዕዛዝ በቦት ላክ", emptyCart: "ጋሪዎ ባዶ ነው",
                sending: "ትዕዛዝዎ በመላክ ላይ...", sent: "ትዕዛዝዎ ወደ ግሩፑ ተልኳል!", failed: "ትዕዛዙ አልተላከም። ቴሌግራም በመክፈት ላይ...",
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

        function toggleLanguage() {
            currentLang = currentLang === 'am' ? 'en' : 'am';
            document.getElementById('lang-btn-text').innerText = currentLang === 'am' ? 'English' : 'አማርኛ';
            document.getElementById('header-title').innerText = translations[currentLang].headerTitle;
            document.getElementById('search-input').placeholder = translations[currentLang].searchPlaceholder;
            document.getElementById('nav-menu').innerText = translations[currentLang].navMenu;
            document.getElementById('nav-orders').innerText = translations[currentLang].navOrders;
            document.getElementById('cart-sidebar-title').innerText = translations[currentLang].cartTitle;
            document.getElementById('table-label').innerText = translations[currentLang].tableLabel;
            document.getElementById('note-label').innerText = translations[currentLang].noteLabel;
            document.getElementById('total-text').innerText = translations[currentLang].totalText;
            document.getElementById('order-btn-text').innerText = translations[currentLang].orderBtn;
            document.getElementById('modal-add-btn').innerText = translations[currentLang].addToCart;

            filterMenu(currentFilter);
            updateCartUI();
        }

        function filterMenu(category) {
            currentFilter = category;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                btn.classList.remove('bg-emerald-900', 'text-white', 'shadow');
                btn.classList.add('bg-gray-100', 'text-gray-600');
            });
            const activeBtn = document.querySelector(`.cat-btn[onclick="filterMenu('${category}')"]`);
            if (activeBtn) {
                activeBtn.classList.add('bg-emerald-900', 'text-white', 'shadow');
                activeBtn.classList.remove('bg-gray-100', 'text-gray-600');
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
                <div onclick="openDetail(${item.id})" class="bg-gray-50 rounded-2xl p-3 shadow-sm hover:shadow-md transition cursor-pointer flex items-center gap-3 border border-gray-100">
                    <img src="${item.image}" alt="" class="w-20 h-20 object-cover rounded-xl shrink-0">
                    <div class="flex-grow">
                        <h4 class="font-bold text-sm text-gray-900 line-clamp-1">${item.name[currentLang]}</h4>
                        <p class="text-[11px] text-gray-500 line-clamp-1 my-0.5">${item.desc[currentLang]}</p>
                        <div class="text-emerald-900 font-extrabold text-xs">${item.price.toFixed(2)} ETB</div>
                    </div>
                    <button onclick="event.stopPropagation(); addToCart(${item.id})" class="bg-[#114b3e] text-white px-3.5 py-2.5 rounded-xl font-bold text-xs shadow hover:bg-emerald-950 transition shrink-0 flex items-center justify-center">
                        <i class="fa-solid fa-plus"></i>
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
            if (cart[index].qty <= 0) {
                cart.splice(index, 1);
            }
            updateCartUI();
        }

        function updateCartUI() {
            const totalCount = cart.reduce((sum, item) => sum + item.qty, 0);
            document.getElementById('cart-count').innerText = totalCount;
            const container = document.getElementById('cart-items');

            if (cart.length === 0) {
                container.innerHTML = `<p class='text-gray-400 text-center py-8 text-xs'>${translations[currentLang].emptyCart}</p>`;
                document.getElementById('total-price').innerText = "0.00 ETB";
                return;
            }

            let total = 0;
            container.innerHTML = cart.map((item, index) => {
                total += item.price * item.qty;
                return `
                    <div class="flex justify-between items-center bg-gray-50 p-2.5 rounded-xl border border-gray-100">
                        <div>
                            <h5 class="font-semibold text-xs text-gray-900">${item.name[currentLang]}</h5>
                            <p class="text-[11px] text-emerald-900 font-bold">${(item.price * item.qty).toFixed(2)} ETB</p>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="changeQty(${index}, -1)" class="w-6 h-6 bg-gray-200 rounded-full font-bold text-xs flex items-center justify-center">-</button>
                            <span class="text-xs font-bold">${item.qty}</span>
                            <button onclick="changeQty(${index}, 1)" class="w-6 h-6 bg-emerald-800 text-white rounded-full font-bold text-xs flex items-center justify-center">+</button>
                        </div>
                    </div>
                `;
            }).join('');

            document.getElementById('total-price').innerText = total.toFixed(2) + " ETB";
        }

        function toggleCart() {
            document.getElementById('cart-sidebar').classList.toggle('translate-x-full');
        }

        function setStatus(text, colorClass) {
            const el = document.getElementById('order-status');
            el.innerText = text;
            el.className = `text-center text-xs mt-2 ${colorClass}`;
            el.classList.remove('hidden');
        }

        async function checkout() {
            if (cart.length === 0) {
                alert(currentLang === 'am' ? "እባክዎ መጀመሪያ እቃ ይምረጡ!" : "Please select items first!");
                return;
            }

            const tableNum = document.getElementById('table-number').value.trim();
            if (!tableNum) {
                alert(currentLang === 'am' ? "እባክዎ የጠረጴዛ ቁጥር ያስገቡ!" : "Please enter your table number!");
                return;
            }

            const note = document.getElementById('order-note').value.trim();
            const orderId = Math.floor(1000 + Math.random() * 9000); // Random Order ID

            let itemsSummary = cart.map(i => `${i.name.am} (${i.qty}x)`).join(", ");
            let total = cart.reduce((sum, i) => sum + (i.price * i.qty), 0);

            const checkoutBtn = document.getElementById('checkout-btn');
            checkoutBtn.disabled = true;
            checkoutBtn.classList.add('opacity-60', 'cursor-not-allowed');
            setStatus(translations[currentLang].sending, 'text-gray-500');

            // Backend ካለ ወደ Backend ይልካል (15 Min Alert Timer እንዲሰራ)
            if (BACKEND_API_URL) {
                try {
                    let res = await fetch(BACKEND_API_URL, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({
                            orderId: orderId,
                            tableNumber: tableNum,
                            items: itemsSummary + (note ? ` | ማስታወሻ: ${note}` : ''),
                            alertMinutes: 15
                        })
                    });
                    if (res.ok) {
                        finishCheckout();
                        return;
                    }
                } catch (e) {
                    console.log("Backend offline, falling back to direct Telegram call...");
                }
            }

            // Backend ከሌለ በቀጥታ በTelegram API ይልካል
            let message = `🛒 <b>አዲስ ትዕዛዝ / NEW ORDER #${orderId}</b>\n\n`;
            message += `📍 <b>ጠረጴዛ / Table #:</b> ${tableNum}\n`;
            if (note) message += `📝 <b>ማስታወሻ / Note:</b> ${note}\n`;
            message += `-----------------------------\n`;

            cart.forEach((item, index) => {
                let itemTotal = item.price * item.qty;
                message += `${index + 1}. ${item.name.am} (${item.qty}x) - ${itemTotal.toFixed(2)} ETB\n`;
            });

            message += `-----------------------------\n`;
            message += `💰 <b>አጠቃላይ ዋጋ / Total:</b> ${total.toFixed(2)} ETB`;

            const url = `https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`;

            try {
                let response = await fetch(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        chat_id: CHAT_ID,
                        text: message,
                        parse_mode: 'HTML'
                    })
                });

                const data = await response.json();

                if (response.ok && data.ok) {
                    finishCheckout();
                } else {
                    throw new Error(data.description || "Telegram API error");
                }
            } catch (error) {
                console.error("Telegram send failed:", error);
                setStatus(translations[currentLang].failed, 'text-red-600');
                const encodedMessage = encodeURIComponent(message);
                window.open(`https://t.me/share/url?url=${encodedMessage}`, '_blank');
            } finally {
                checkoutBtn.disabled = false;
                checkoutBtn.classList.remove('opacity-60', 'cursor-not-allowed');
            }
        }

        function finishCheckout() {
            setStatus(translations[currentLang].sent, 'text-emerald-700');
            alert(currentLang === 'am' ? "ትዕዛዝዎ በተሳካ ሁኔታ ተልኳል!" : "Order sent successfully!");
            cart = [];
            updateCartUI();
            document.getElementById('order-note').value = '';
            document.getElementById('table-number').value = '';
            toggleCart();
        }

        filterMenu('all');
        updateCartUI();
    </script>
</body>
</html>
