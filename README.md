
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> (Fikir Restaurant) - Menu</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { background-color: #f4f7f6; }
    </style>
</head>
<body class="font-sans text-gray-800">

    <!-- Header / Navigation (Dark Green Theme) -->
    <header class="bg-emerald-900 text-white p-4 shadow-md sticky top-0 z-50">
        <div class="container mx-auto flex justify-between items-center">
            <h1 id="site-title" class="text-xl md:text-2xl font-bold">
                <i class="fa-solid fa-heart text-red-400"></i> ፍቅር レストラン (Fikir Restaurant)
            </h1>
            <div class="flex items-center gap-4">
                <!-- Language Switcher Button -->
                <button onclick="toggleLanguage()" class="bg-emerald-800 text-white px-3 py-1.5 rounded-lg text-sm font-semibold border border-emerald-700 hover:bg-emerald-700 transition">
                    🌐 <span id="lang-btn-text">English</span>
                </button>
                <!-- Cart Button -->
                <button onclick="toggleCart()" class="bg-white text-emerald-900 px-4 py-2 rounded-lg font-semibold shadow hover:bg-gray-100 transition">
                    🛒 <span id="cart-text">ጋሪ</span> (<span id="cart-count">0</span>)
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto p-4 md:p-8">
        <div class="text-center mb-8">
            <h2 id="main-heading" class="text-3xl font-bold text-emerald-900">እንኳን ወደ ፍቅር ምግብ ቤት በደህና መጡ!</h2>
            <p id="main-subheading" class="text-gray-600 mt-2">ጤናማ እና ጣፋጭ ምግቦችና መጠጦች</p>
        </div>

        <!-- Category Filter Buttons (Habesha, Ferenj, Hot, Cold) -->
        <div class="flex flex-wrap justify-center gap-3 mb-8">
            <button onclick="filterMenu('all')" class="category-btn bg-emerald-900 text-white px-5 py-2 rounded-full font-semibold shadow transition" data-am="ሁሉንም" data-en="All">ሁሉንም</button>
            <button onclick="filterMenu('habesha')" class="category-btn bg-white text-emerald-900 border border-emerald-900 px-5 py-2 rounded-full font-semibold shadow hover:bg-emerald-50 transition" data-am="ሀባሻ (Habesha)" data-en="Habesha">ሀባሻ (Habesha)</button>
            <button onclick="filterMenu('ferenj')" class="category-btn bg-white text-emerald-900 border border-emerald-900 px-5 py-2 rounded-full font-semibold shadow hover:bg-emerald-50 transition" data-am="ፈረንጅ (Ferenj)" data-en="Ferenj">ፈረንጅ (Ferenj)</button>
            <button onclick="filterMenu('hot')" class="category-btn bg-white text-emerald-900 border border-emerald-900 px-5 py-2 rounded-full font-semibold shadow hover:bg-emerald-50 transition" data-am="ሙቅ (Hot)" data-en="Hot">ሙቅ (Hot)</button>
            <button onclick="filterMenu('cold')" class="category-btn bg-white text-emerald-900 border border-emerald-900 px-5 py-2 rounded-full font-semibold shadow hover:bg-emerald-50 transition" data-am="ቀዝቃዛ (Cold)" data-en="Cold">ቀዝቃዛ (Cold)</button>
        </div>

        <!-- Menu Grid -->
        <div id="menu-container" class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <!-- የምግብ ካርዶች በ JavaScript ይሞላሉ -->
        </div>
    </main>

    <!-- Food Detail Modal -->
    <div id="detail-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden justify-center items-center z-50 p-4">
        <div class="bg-white rounded-2xl max-w-lg w-full p-6 relative shadow-2xl border-t-4 border-emerald-900">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-gray-500 hover:text-black text-xl font-bold">✕</button>
            <img id="modal-img" src="" alt="" class="w-full h-56 object-cover rounded-xl mb-4">
            <h3 id="modal-title" class="text-2xl font-bold text-gray-800 mb-2"></h3>
            <div id="modal-stars" class="text-yellow-500 mb-2"></div>
            <p id="modal-price" class="text-emerald-900 font-bold text-xl mb-4"></p>
            
            <div class="bg-emerald-50 p-4 rounded-xl mb-4 space-y-2 border border-emerald-100">
                <p><strong><i class="fa-solid fa-list-check text-emerald-900"></i> <span class="ing-label">ግብዓቶች</span>:</strong> <span id="modal-ingredients" class="text-gray-700"></span></p>
                <p><strong><i class="fa-solid fa-shield-heart text-green-700"></i> <span class="health-label">ለጤና ያለው ጥቅም</span>:</strong> <span id="modal-health" class="text-gray-700"></span></p>
                <p><strong><i class="fa-solid fa-eye text-blue-600"></i> <span class="views-label">የታየበት ብዛት</span>:</strong> <span id="modal-views" class="text-gray-700"></span></p>
            </div>

            <button id="modal-add-btn" class="w-full bg-emerald-900 text-white py-3 rounded-xl font-bold hover:bg-emerald-800 transition">
                ወደ ጋሪ ጨምር
            </button>
        </div>
    </div>

    <!-- Shopping Cart Sidebar (Dark Green Accents) -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-80 md:w-96 bg-white shadow-2xl p-6 transform translate-x-full transition-transform duration-300 z-50 flex flex-col border-l border-gray-200">
        <div class="flex justify-between items-center mb-4 border-b pb-2">
            <h3 id="cart-title" class="text-xl font-bold text-emerald-900">የመረጧቸው ትዕዛዞች</h3>
            <button onclick="toggleCart()" class="text-gray-500 hover:text-black text-xl font-bold">✕</button>
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-4">
            <!-- የተመረጡ ምግቦች እዚህ ይገባሉ -->
        </div>
        <div class="border-t pt-4 mt-4">
            <div class="flex justify-between font-bold text-lg mb-4">
                <span id="total-text">አጠቃላይ ዋጋ:</span>
                <span id="total-price" class="text-emerald-900">0 ብር</span>
            </div>
            <!-- አሁን አዝዝ (Start Order) - በቀጥታ ወደ ጂሜይል ይልካል -->
            <button onclick="checkout()" class="w-full bg-emerald-900 text-white py-3 rounded-lg font-bold hover:bg-emerald-800 shadow transition">
                <span id="order-btn-text">አሁን አዝዝ (Start Order)</span>
            </button>
        </div>
    </div>

    <!-- JavaScript ሎጂክ (ቋንቋ እና ሲስተም) -->
    <script>
        let currentLang = 'am'; // ነባሪ ቋንቋ አማርኛ

        const translations = {
            am: {
                title: "ፍቅር レストラン (Fikir Restaurant)",
                welcome: "እንኳን ወደ ፍቅር ምግብ ቤት በደህና መጡ!",
                sub: "ጤናማ እና ጣፋጭ ምግቦችና መጠጦች",
                cart: "ጋሪ",
                cartTitle: "የመረጧቸው ትዕዛዞች",
                total: "አጠቃላይ ዋጋ:",
                orderBtn: "አሁን አዝዝ (Start Order)",
                details: "ዝርዝር ማየት",
                add: "አዝዝ",
                addToCart: "ወደ ጋሪ ጨምር",
                emptyCart: "ጋሪዎ ባዶ ነው",
                ingredients: "ግብዓቶች",
                health: "ለጤና ያለው ጥቅም",
                views: "የታየበት ብዛት",
                times: "ጊዜ",
                birr: "ብር"
            },
            en: {
                title: "Fikir Restaurant",
                welcome: "Welcome to Fikir Restaurant!",
                sub: "Healthy and Delicious Foods & Drinks",
                cart: "Cart",
                cartTitle: "Your Ordered Items",
                total: "Total Price:",
                orderBtn: "Start Order",
                details: "View Details",
                add: "Order",
                addToCart: "Add to Cart",
                emptyCart: "Your cart is empty",
                ingredients: "Ingredients",
                health: "Health Benefits",
                views: "Views",
                times: "times",
                birr: "ETB"
            }
        };

        const menuItems = [
            { 
                id: 1, 
                name: { am: "ዶሮ ወጥ", en: "Doro Wat" }, 
                category: "habesha", 
                price: 450, 
                rating: 5, 
                views: 342, 
                ingredients: { am: "ዶሮ፣ ቀይ ሽንኩርት፣ በርበሬ፣ ንጹህ ቅቤ፣ እንቁላል", en: "Chicken, red onion, berbere, purified butter, egg" }, 
                health: { am: "ለሰውነት ከፍተኛ ፕሮቲን ይሰጣል፤ ጉልበትን ያጠናክራል።", en: "Provides high protein and boosts energy." },
                image: "https://images.unsplash.com/photo-1541544741938-0af808871cc0?w=500" 
            },
            { 
                id: 2, 
                name: { am: "ክትፎ", en: "Kitfo" }, 
                category: "habesha", 
                price: 500, 
                rating: 4.8, 
                views: 512, 
                ingredients: { am: "ጥሬ ስጋ (የተቀጠቀጠ)፣ ሚጥሚጣ፣ ንጹህ ቅቤ", en: "Minced raw beef, mitmita, spiced butter" }, 
                health: { am: "ብረት (Iron) በውስጡ ስለያዘ ለደም ማነስ ጠቃሚ ነው።", en: "Rich in iron, helpful for blood health." },
                image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" 
            },
            { 
                id: 3, 
                name: { am: "ፒዛ (Pizza)", en: "Classic Pizza" }, 
                category: "ferenj", 
                price: 600, 
                rating: 4.9, 
                views: 410, 
                ingredients: { am: "ዱቄት፣ ቺዝ፣ トマト ሾርባ፣ ስጋ ወይም አትክልት", en: "Flour, cheese, tomato sauce, meat or vegetables" }, 
                health: { am: "ፈጣን ጉልበት ይሰጣል፣ በካልሲየም የበለፀገ ነው።", en: "Provides quick energy, rich in calcium." },
                image: "https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500" 
            },
            { 
                id: 4, 
                name: { am: "ሙቅ ሻይ (Hot Tea)", en: "Hot Tea" }, 
                category: "hot", 
                price: 30, 
                rating: 4.7, 
                views: 220, 
                ingredients: { am: "ጥቁር ሻይ ቅጠል፣ ሩዝ ወይም ከርፋና ውሃ", en: "Black tea leaves, spices, hot water" }, 
                health: { am: "አዕምሮን ያዝናናል፣ ሰውነትን ያሞቃል።", en: "Relaxes the mind, warms up the body." },
                image: "https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500" 
            },
            { 
                id: 5, 
                name: { am: "ቀዝቃዛ ፍሩት ጁስ", en: "Cold Fruit Juice" }, 
                category: "cold", 
                price: 150, 
                rating: 4.9, 
                views: 280, 
                ingredients: { am: "አቮካዶ፣ ማንጎ፣ ፓፓያ እና በረዶ", en: "Avocado, mango, papaya and ice" }, 
                health: { am: "በተፈጥሮ ቫይታሚኖች የበለፀገ በመሆኑ ቆዳን ያጸዳል።", en: "Rich in natural vitamins, clears the skin." },
                image: "https://images.unsplash.com/photo-1556881286-fc6915169721?w=500" 
            }
        ];

        let cart = [];
        let currentFilter = 'all';

        // ቋንቋ መቀየሪያ ተግባር
        function toggleLanguage() {
            currentLang = currentLang === 'am' ? 'en' : 'am';
            document.getElementById('lang-btn-text').innerText = currentLang === 'am' ? 'English' : 'አማርኛ';
            
            document.getElementById('main-heading').innerText = translations[currentLang].welcome;
            document.getElementById('main-subheading').innerText = translations[currentLang].sub;
            document.getElementById('cart-text').innerText = translations[currentLang].cart;
            document.getElementById('cart-title').innerText = translations[currentLang].cartTitle;
            document.getElementById('total-text').innerText = translations[currentLang].total;
            document.getElementById('order-btn-text').innerText = translations[currentLang].orderBtn;
            
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.innerText = btn.getAttribute(`data-${currentLang}`);
            });

            filterMenu(currentFilter);
            updateCartUI();
        }

        function renderStars(rating) {
            let starsHTML = "";
            for (let i = 1; i <= 5; i++) {
                if (i <= Math.floor(rating)) {
                    starsHTML += '<i class="fa-solid fa-star"></i>';
                } else {
                    starsHTML += '<i class="fa-regular fa-star"></i>';
                }
            }
            return `${starsHTML} <span class="text-sm text-gray-600 ml-1">(${rating})</span>`;
        }

        function filterMenu(category) {
            currentFilter = category;
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('bg-emerald-900', 'text-white');
                btn.classList.add('bg-white', 'text-emerald-900', 'border', 'border-emerald-900');
            });
            event && event.target && event.target.classList.remove('bg-white', 'text-emerald-900');
            event && event.target && event.target.classList.add('bg-emerald-900', 'text-white');

            const filtered = category === 'all' ? menuItems : menuItems.filter(item => item.category === category);
            const container = document.getElementById('menu-container');
            
            container.innerHTML = filtered.map(item => `
                <div class="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition flex flex-col justify-between border border-gray-100">
                    <div>
                        <img src="${item.image}" alt="${item.name[currentLang]}" class="w-full h-48 object-cover cursor-pointer" onclick="openDetail(${item.id})">
                        <div class="p-4">
                            <div class="flex justify-between items-start mb-1">
                                <h3 onclick="openDetail(${item.id})" class="text-xl font-semibold text-gray-800 cursor-pointer hover:text-emerald-900">${item.name[currentLang]}</h3>
                                <span class="text-xs bg-emerald-50 text-emerald-800 px-2 py-1 rounded border border-emerald-200"><i class="fa-solid fa-eye"></i> ${item.views}</span>
                            </div>
                            <div class="mb-2">${renderStars(item.rating)}</div>
                            <p class="text-emerald-900 font-bold text-lg">${item.price} ${translations[currentLang].birr}</p>
                        </div>
                    </div>
                    <div class="p-4 pt-0 flex gap-2">
                        <button onclick="openDetail(${item.id})" class="w-1/2 bg-gray-100 text-gray-700 py-2 rounded-lg font-semibold hover:bg-gray-200 transition text-sm">
                            ${translations[currentLang].details}
                        </button>
                        <button onclick="addToCart(${item.id})" class="w-1/2 bg-emerald-900 text-white py-2 rounded-lg font-semibold hover:bg-emerald-800 transition text-sm">
                            ${translations[currentLang].add}
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function openDetail(id) {
            const item = menuItems.find(p => p.id === id);
            item.views += 1;

            document.getElementById('modal-img').src = item.image;
            document.getElementById('modal-title').innerText = item.name[currentLang];
            document.getElementById('modal-stars').innerHTML = renderStars(item.rating);
            document.getElementById('modal-price').innerText = item.price + " " + translations[currentLang].birr;
            document.getElementById('modal-ingredients').innerText = item.ingredients[currentLang];
            document.getElementById('modal-health').innerText = item.health[currentLang];
            document.getElementById('modal-views').innerText = item.views + " " + translations[currentLang].times;
            
            document.querySelector('.ing-label').innerText = currentLang === 'am' ? 'ግብዓቶች' : 'Ingredients';
            document.querySelector('.health-label').innerText = currentLang === 'am' ? 'ለጤና ያለው ጥቅም' : 'Health Benefits';
            document.querySelector('.views-label').innerText = currentLang === 'am' ? 'የታየበት ብዛት' : 'Total Views';
            document.getElementById('modal-add-btn').innerText = translations[currentLang].addToCart;

            document.getElementById('modal-add-btn').onclick = function() {
                addToCart(item.id);
                closeModal();
            };

            document.getElementById('detail-modal').classList.remove('hidden');
            document.getElementById('detail-modal').classList.add('flex');
            filterMenu(currentFilter);
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
                container.innerHTML = `<p class='text-gray-500 text-center py-8'>${translations[currentLang].emptyCart}</p>`;
                document.getElementById('total-price').innerText = "0 " + translations[currentLang].birr;
                return;
            }

            let total = 0;
            container.innerHTML = cart.map((item, index) => {
                total += item.price;
                return `
                    <div class="flex justify-between items-center border-b pb-2">
                        <div>
                            <h4 class="font-semibold text-sm">${item.name[currentLang]}</h4>
                            <p class="text-xs text-emerald-900 font-bold">${item.price} ${translations[currentLang].birr}</p>
                        </div>
                        <button onclick="removeFromCart(${index})" class="text-red-500 text-xs font-bold hover:underline">✕</button>
                    </div>
                `;
            }).join('');

            document.getElementById('total-price').innerText = total + " " + translations[currentLang].birr;
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        function toggleCart() {
            const sidebar = document.getElementById('cart-sidebar');
            sidebar.classList.toggle('translate-x-full');
        }

        // ትዕዛዙን በቀጥታ ወደ ጂሜይል (yisuteka@gmail.com) መላኪያ ሎጂክ
        function checkout() {
            if (cart.length === 0) {
                alert(currentLang === 'am' ? "እባክዎ መጀመሪያ ምግብ ወይም መጠጥ ይምረጡ!" : "Please select food or drinks first!");
                return;
            }

            const emailTo = "yisuteka@gmail.com";
            const emailSubject = currentLang === 'am' ? "አዲስ የምግብ ትዕዛዝ - ፍቅር ምግብ ቤት" : "New Food Order - Fikir Restaurant";
            
            let emailBody = currentLang === 'am' ? "ሰላም! የሚከተሉትን ምግቦች አዘዛለሁ:%0A%0A" : "Hello! I would like to order the following items:%0A%0A";
            let total = 0;

            cart.forEach((item, index) => {
                emailBody += `${index + 1}. ${item.name[currentLang]} - ${item.price} ${translations[currentLang].birr}%0A`;
                total += item.price;
            });

            emailBody += `%0A---------------------------------%0A`;
            emailBody += `${translations[currentLang].total} ${total} ${translations[currentLang].birr}`;

            const mailtoUrl = `mailto:${emailTo}?subject=${encodeURIComponent(emailSubject)}&body=${emailBody}`;
            window.location.href = mailtoUrl;

            cart = [];
            updateCartUI();
            toggleCart();
        }

        // ሲጀምር ሁሉንም ማሳየት
        filterMenu('all');
    </script>
</body>
</html>
