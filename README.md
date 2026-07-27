<!DOCTYPE html>
<html lang="am">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ፍቅር レストラン (Fikir Restaurant) - ሜኑ እና ማዘዣ</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-gray-50 font-sans">

    <!-- Header / Navigation -->
    <header class="bg-red-600 text-white p-4 shadow-md sticky top-0 z-50">
        <div class="container mx-auto flex justify-between items-center">
            <h1 class="text-2xl font-bold"><i class="fa-solid fa-heart"></i> ፍቅር レストラン (Fikir Restaurant)</h1>
            <div class="flex items-center gap-4">
                <button onclick="toggleCart()" class="bg-white text-red-600 px-4 py-2 rounded-lg font-semibold shadow hover:bg-gray-100">
                    🛒 ጋሪ (<span id="cart-count">0</span>)
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto p-4 md:p-8">
        <div class="text-center mb-8">
            <h2 class="text-3xl font-bold text-gray-800">እንኳን ወደ ፍቅር ምግብ ቤት በደህና መጡ!</h2>
            <p class="text-gray-600 mt-2">ጤናማ እና ጣፋጭ ምግቦች ከግል ጤና ጥቅማቸው ጋር</p>
        </div>

        <!-- Category Filter Buttons (መጠጥ እና ምግብ) -->
        <div class="flex justify-center gap-4 mb-8">
            <button onclick="filterMenu('all')" class="category-btn bg-red-600 text-white px-5 py-2 rounded-full font-semibold shadow">ሁሉንም</button>
            <button onclick="filterMenu('food')" class="category-btn bg-gray-200 text-gray-700 px-5 py-2 rounded-full font-semibold shadow hover:bg-gray-300">ምግቦች (Foods)</button>
            <button onclick="filterMenu('drink')" class="category-btn bg-gray-200 text-gray-700 px-5 py-2 rounded-full font-semibold shadow hover:bg-gray-300">መጠጦች (Drinks)</button>
        </div>

        <!-- Menu Grid -->
        <div id="menu-container" class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <!-- የምግብ ካርዶች በ JavaScript ይሞላሉ -->
        </div>
    </main>

    <!-- Food Detail Modal (የምግብ ዝርዝር፣ ጤና እና ግብዓት ማሳያ) -->
    <div id="detail-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden justify-center items-center z-50 p-4">
        <div class="bg-white rounded-2xl max-w-lg w-full p-6 relative shadow-2xl">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-gray-500 hover:text-black text-xl font-bold">✕</button>
            <img id="modal-img" src="" alt="" class="w-full h-56 object-cover rounded-xl mb-4">
            <h3 id="modal-title" class="text-2xl font-bold text-gray-800 mb-2"></h3>
            <div id="modal-stars" class="text-yellow-500 mb-2"></div>
            <p id="modal-price" class="text-red-600 font-bold text-xl mb-4"></p>
            
            <div class="bg-gray-50 p-4 rounded-xl mb-4 space-y-2">
                <p><strong><i class="fa-solid fa-list-check text-red-600"></i> ግብዓቶች (Ingredients):</strong> <span id="modal-ingredients" class="text-gray-700"></span></p>
                <p><strong><i class="fa-solid fa-shield-heart text-green-600"></i> ለጤና ያለው ጥቅም:</strong> <span id="modal-health" class="text-gray-700"></span></p>
                <p><strong><i class="fa-solid fa-eye text-blue-600"></i> የታየበት ብዛት:</strong> <span id="modal-views" class="text-gray-700"></span> ጊዜ</p>
            </div>

            <button id="modal-add-btn" class="w-full bg-red-600 text-white py-3 rounded-xl font-bold hover:bg-red-700 transition">
                ወደ ጋሪ ጨምር
            </button>
        </div>
    </div>

    <!-- Shopping Cart Sidebar -->
    <div id="cart-sidebar" class="fixed right-0 top-0 h-full w-80 md:w-96 bg-white shadow-2xl p-6 transform translate-x-full transition-transform duration-300 z-50 flex flex-col">
        <div class="flex justify-between items-center mb-4 border-b pb-2">
            <h3 class="text-xl font-bold text-gray-800">የመረጧቸው ትዕዛዞች</h3>
            <button onclick="toggleCart()" class="text-gray-500 hover:text-black text-xl font-bold">✕</button>
        </div>
        
        <!-- Table Number Selection -->
        <div class="mb-4 bg-red-50 p-3 rounded-lg">
            <label class="block text-sm font-bold text-red-700 mb-1">የጠረጴዛ ቁጥር (Table Number):</label>
            <select id="table-number" class="w-full border border-red-300 rounded-lg p-2 bg-white font-semibold">
                <option value="1">ጠረጴዛ 1 (Table 1)</option>
                <option value="2">ጠረጴዛ 2 (Table 2)</option>
                <option value="3">ጠረጴዛ 3 (Table 3)</option>
                <option value="4">ጠረጴዛ 4 (Table 4)</option>
                <option value="VIP">ቪአይፒ ጠረጴዛ (VIP Table)</option>
            </select>
        </div>

        <div id="cart-items" class="flex-grow overflow-y-auto space-y-4">
            <!-- የተመረጡ ምግቦች እዚህ ይገባሉ -->
        </div>
        <div class="border-t pt-4 mt-4">
            <div class="flex justify-between font-bold text-lg mb-4">
                <span>አጠቃላይ ዋጋ:</span>
                <span id="total-price">0 ብር</span>
            </div>
            <button onclick="checkout()" class="w-full bg-green-600 text-white py-3 rounded-lg font-bold hover:bg-green-700 shadow">
                አሁን አዝዝ (Start Order)
            </button>
        </div>
    </div>

    <!-- JavaScript ሎጂክ -->
    <script>
        // የምግብ እና መጠጥ የውሂብቤዝ (Database with Views, Stars, Ingredients, and Health Benefits)
        const menuItems = [
            { 
                id: 1, 
                name: "ዶሮ ወጥ (Doro Wat)", 
                category: "food", 
                price: 450, 
                rating: 5, 
                views: 342, 
                ingredients: "ዶሮ፣ ቀይ ሽንኩርት፣ በርበሬ፣ ንጹህ ቅቤ፣ እንቁላል እና ቅመማ ቅመም", 
                health: "ለሰውነት ከፍተኛ ፕሮቲን ይሰጣል፤ ጉልበትንና በሽታ የመከላከል አቅምን ያጠናክራል።",
                image: "https://images.unsplash.com/photo-1541544741938-0af808871cc0?w=500" 
            },
            { 
                id: 2, 
                name: "ክትፎ (Kitfo)", 
                category: "food", 
                price: 500, 
                rating: 4.8, 
                views: 512, 
                ingredients: "ጥሬ ስጋ (የተቀጠቀጠ)፣ይህም ሚጥሚጣና ቀለል ያለ ኮሰረ የተጨመረበት ንጹህ ቅቤ", 
                health: "ብረት (Iron) እና ቫይታሚን B12 በውስጡ ስለያዘ ለደም ማነስ እጅግ ጠቃሚ ነው።",
                image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500" 
            },
            { 
                id: 3, 
                name: "ልዩ የፍሩት ጁስ (Special Fruit Juice)", 
                category: "drink", 
                price: 150, 
                rating: 4.9, 
                views: 280, 
                ingredients: "አቮካዶ፣ ማንጎ፣ ፓፓያ እና እንጆሪ ተደባልቆ የሚዘጋጅ", 
                health: "በተፈጥሮ ቫይታሚኖች የበለፀገ በመሆኑ ቆዳን ያጸዳል፣ ለሰውነት አዲስ ጉልበት ይሰጣል።",
                image: "https://images.unsplash.com/photo-1556881286-fc6915169721?w=500" 
            },
            { 
                id: 4, 
                name: "የጾም ፍያስ (Fasting Combo)", 
                category: "food", 
                price: 300, 
                rating: 4.6, 
                views: 195, 
                ingredients: "ሽንፈፍ፣ የምስር ወጥ፣ አተር ክክ፣ እና የተለያዩ የአትክልት saldat", 
                health: "በፋይበር እና በዕፅዋት ፕሮቲን የበለፀገ በመሆኑ ለልብ ጤንነት እና ለክብደት መቀነስ ይረዳል።",
                image: "https://images.unsplash.com/photo-1540420773420-3366772f4999?w=500" 
            },
            { 
                id: 5, 
                name: "ባህላዊ ጀበና ቡና (Traditional Coffee)", 
                category: "drink", 
                price: 50, 
                rating: 5, 
                views: 670, 
                ingredients: "የተጠበሰ የቡና ፍሬ እና ውሃ", 
                health: "አዕምሮን ያነቃቃል፣ የትኩረት ማዕከልን ይጨምራል እንዲሁም የፀረ-ኦክሳይድ (Antioxidant) ምንጭ ነው።",
                image: "https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?w=500" 
            }
        ];

        let cart = [];

        // ስታር ሪቪው በ HTML ፎርማት ለመፍጠር
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

        // ሜኑዎችን ማሳየት (በምድብ ማጣራት)
        function filterMenu(category) {
            // የቡተኖችን ከለር መቀየር
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('bg-red-600', 'text-white');
                btn.classList.add('bg-gray-200', 'text-gray-700');
            });
            event.target.classList.remove('bg-gray-200', 'text-gray-700');
            event.target.classList.add('bg-red-600', 'text-white');

            const filtered = category === 'all' ? menuItems : menuItems.filter(item => item.category === category);
            const container = document.getElementById('menu-container');
            
            container.innerHTML = filtered.map(item => `
                <div class="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition flex flex-col justify-between">
                    <div>
                        <img src="${item.image}" alt="${item.name}" class="w-full h-48 object-cover cursor-pointer" onclick="openDetail(${item.id})">
                        <div class="p-4">
                            <div class="flex justify-between items-start mb-1">
                                <h3 onclick="openDetail(${item.id})" class="text-xl font-semibold text-gray-800 cursor-pointer hover:text-red-600">${item.name}</h3>
                                <span class="text-xs bg-gray-100 text-gray-600 px-2 py-1 rounded"><i class="fa-solid fa-eye"></i> ${item.views}</span>
                            </div>
                            <div class="mb-2">${renderStars(item.rating)}</div>
                            <p class="text-red-600 font-bold text-lg">${item.price} ብር</p>
                        </div>
                    </div>
                    <div class="p-4 pt-0 flex gap-2">
                        <button onclick="openDetail(${item.id})" class="w-1/2 bg-gray-100 text-gray-700 py-2 rounded-lg font-semibold hover:bg-gray-200 transition text-sm">
                            ዝርዝር ማየት
                        </button>
                        <button onclick="addToCart(${item.id})" class="w-1/2 bg-red-600 text-white py-2 rounded-lg font-semibold hover:bg-red-700 transition text-sm">
                            አዝዝ
                        </button>
                    </div>
                </div>
            `).join('');
        }

        // የምግብ ዝርዝር መመልከቻ (Modal) መክፈት እና Views ቁጥር መጨመር
        function openDetail(id) {
            const item = menuItems.find(p => p.id === id);
            item.views += 1; // ሲታይ የቪው ቁጥር ይጨምራል

            document.getElementById('modal-img').src = item.image;
            document.getElementById('modal-title').innerText = item.name;
            document.getElementById('modal-stars').innerHTML = renderStars(item.rating);
            document.getElementById('modal-price').innerText = item.price + " ብር";
            document.getElementById('modal-ingredients').innerText = item.ingredients;
            document.getElementById('modal-health').innerText = item.health;
            document.getElementById('modal-views').innerText = item.views;
            
            document.getElementById('modal-add-btn').onclick = function() {
                addToCart(item.id);
                closeModal();
            };

            document.getElementById('detail-modal').classList.remove('hidden');
            document.getElementById('detail-modal').classList.add('flex');
            filterMenu('all'); // ቪው ሲጨምር ራሱን እንዲያድስ
        }

        function closeModal() {
            document.getElementById('detail-modal').classList.remove('flex');
            document.getElementById('detail-modal').classList.add('hidden');
        }

        // ምግብ ወደ ጋሪ መጨመር
        function addToCart(id) {
            const item = menuItems.find(p => p.id === id);
            cart.push(item);
            updateCartUI();
            toggleCart(); // ሲጨመር ጋሪው በራሱ እንዲከፈት
        }

        // የጋሪውን ገጽ ማዘመን
        function updateCartUI() {
            document.getElementById('cart-count').innerText = cart.length;
            const container = document.getElementById('cart-items');
            
            if (cart.length === 0) {
                container.innerHTML = "<p class='text-gray-500 text-center py-8'>ጋሪዎ ባዶ ነው</p>";
                document.getElementById('total-price').innerText = "0 ብር";
                return;
            }

            let total = 0;
            container.innerHTML = cart.map((item, index) => {
                total += item.price;
                return `
                    <div class="flex justify-between items-center border-b pb-2">
                        <div>
                            <h4 class="font-semibold text-sm">${item.name}</h4>
                            <p class="text-xs text-red-600 font-bold">${item.price} ብር</p>
                        </div>
                        <button onclick="removeFromCart(${index})" class="text-red-500 text-xs font-bold hover:underline">አጥፋ</button>
                    </div>
                `;
            }).join('');

            document.getElementById('total-price').innerText = total + " ብር";
        }

        // ከጋሪ ማጥፋት
        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        // ጋሪውን መክፈት/ዝጋ ማድረግ
        function toggleCart() {
            const sidebar = document.getElementById('cart-sidebar');
            sidebar.classList.toggle('translate-x-full');
        }

        // ትዕዛዝ ማጠናቀቅ (Start Order with Table Number)
        function checkout() {
            if (cart.length === 0) {
                alert("እባክዎ መጀመሪያ ምግብ ወይም መጠጥ ይምረጡ!");
                return;
            }
            const tableNum = document.getElementById('table-number').value;
            alert(`ትዕዛዝዎ በተሳካ ሁኔታ ለ ${tableNum}ኛ ጠረጴዛ አስተናጋጅ ተልኳል! እናመሰግናለን።`);
            cart = [];
            updateCartUI();
            toggleCart();
        }

        // ሲጀምር ሁሉንም ሜኑ ማሳየት
        filterMenu('all');
    </script>
</body>
</html>
