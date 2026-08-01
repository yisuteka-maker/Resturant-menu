<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ero Shake Juice | Premium Ethiopian Café & Juice House</title>
    
    <!-- PWA & SEO Meta Tags -->
    <meta name="description" content="Experience the finest fresh juices, shakes, traditional breakfasts, and modern meals at Ero Shake Juice. Premium quality, instant QR menu access.">
    <meta name="theme-color" content="#2196F3">
    <link rel="manifest" href="data:application/manifest+json,{
        &quot;name&quot;: &quot;Ero Shake Juice&quot;,
        &quot;short_name&quot;: &quot;Ero Shake&quot;,
        &quot;start_url&quot;: &quot;.&quot;,
        &quot;display&quot;: &quot;standalone&quot;,
        &quot;background_color&quot;: &quot;#FFFFFF&quot;,
        &quot;theme_color&quot;: &quot;#2196F3&quot;,
        &quot;icons&quot;: [{ &quot;src&quot;: &quot;https://images.unsplash.com/photo-1613478223719-2ab802602423?w=192&amp;auto=format&amp;fit=crop&quot;, &quot;sizes&quot;: &quot;192x192&quot;, &quot;type&quot;: &quot;image/png&quot; }]
    }">

    <!-- Tailwind CSS & Font Awesome -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            sky: '#2196F3',
                            deep: '#1565C0',
                            accent: '#0D47A1',
                            light: '#E3F2FD'
                        }
                    },
                    fontFamily: {
                        poppins: ['Poppins', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-firestore-compat.js"></script>

    <style>
        body { font-family: 'Poppins', sans-serif; }
        .glass {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        .dark .glass {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
        .hide-scrollbar::-webkit-scrollbar { display: none; }
        .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 dark:bg-slate-950 dark:text-slate-100 transition-colors duration-300 pb-20 md:pb-0">

    <!-- Sticky Navigation Bar -->
    <header class="sticky top-0 z-40 w-full glass shadow-sm transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <!-- Brand Logo -->
            <div class="flex items-center gap-3 cursor-pointer" onclick="showPage('home')">
                <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-brand-sky to-brand-deep flex items-center justify-center text-white shadow-md shadow-sky-500/30">
                    <i class="fa-solid fa-blender text-xl"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg tracking-tight bg-gradient-to-r from-brand-sky to-brand-deep bg-clip-text text-transparent">ERO SHAKE</h1>
                    <p class="text-[9px] tracking-widest uppercase font-semibold text-slate-400 -mt-1">Juice & Café</p>
                </div>
            </div>

            <!-- Desktop Nav Links -->
            <nav class="hidden md:flex items-center gap-8 font-medium text-sm">
                <button onclick="showPage('home')" class="nav-link hover:text-brand-sky transition" data-en="Home" data-am="መነሻ">Home</button>
                <button onclick="showPage('menu')" class="nav-link hover:text-brand-sky transition" data-en="Menu" data-am="ሜኑ">Menu</button>
                <button onclick="showPage('about')" class="nav-link hover:text-brand-sky transition" data-en="About Us" data-am="ስለ እኛ">About Us</button>
                <button onclick="showPage('contact')" class="nav-link hover:text-brand-sky transition" data-en="Contact" data-am="ግንኙነት">Contact</button>
            </nav>

            <!-- Utility Controls -->
            <div class="flex items-center gap-2">
                <!-- Search Button -->
                <button onclick="showPage('menu'); focusSearch();" class="p-2.5 rounded-full hover:bg-slate-200/50 dark:hover:bg-slate-800 transition text-slate-600 dark:text-slate-300" aria-label="Search">
                    <i class="fa-solid fa-magnifying-glass text-lg"></i>
                </button>
                
                <!-- Language Switcher -->
                <button onclick="toggleLanguage()" class="flex items-center gap-1.5 px-3 py-1.5 text-xs font-semibold border rounded-full border-brand-sky/40 text-brand-sky hover:bg-brand-sky hover:text-white transition">
                    <i class="fa-solid fa-globe"></i>
                    <span id="langLabel">AM</span>
                </button>

                <!-- Dark Mode Toggle -->
                <button onclick="toggleDarkMode()" class="p-2.5 rounded-full hover:bg-slate-200/50 dark:hover:bg-slate-800 transition text-slate-600 dark:text-slate-300">
                    <i id="themeIcon" class="fa-solid fa-moon text-lg"></i>
                </button>

                <!-- Admin Access Button -->
                <button onclick="showPage('admin')" class="hidden sm:flex items-center gap-2 bg-slate-900 text-white dark:bg-slate-100 dark:text-slate-900 px-3.5 py-1.5 rounded-full text-xs font-semibold hover:opacity-90 transition ml-2">
                    <i class="fa-solid fa-user-shield"></i>
                    <span data-en="Admin" data-am="አድሚን">Admin</span>
                </button>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT CONTAINER -->
    <main id="appContent" class="min-h-[calc(100vh-4rem)]">
        
        <!-- PAGE 1: HOME PAGE -->
        <section id="page-home" class="page-view space-y-16">
            <!-- Hero Section -->
            <div class="relative overflow-hidden pt-8 pb-16 lg:py-24">
                <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid md:grid-cols-2 gap-12 items-center">
                    <div class="space-y-6 text-center md:text-left">
                        <span class="inline-block px-4 py-1.5 rounded-full bg-brand-light dark:bg-slate-800 text-brand-deep dark:text-brand-sky text-xs font-bold tracking-wide uppercase shadow-sm">
                            🍹 <span data-en="Fresh & Organic Every Day" data-am="የቀኑ ተፈጥሯዊና ትኩስ መጠጦች">Fresh & Organic Every Day</span>
                        </span>
                        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-extrabold text-slate-900 dark:text-white leading-tight">
                            <span data-en="Taste the Pure" data-am="የእውነተኛ">Taste the Pure</span> <br>
                            <span class="bg-gradient-to-r from-brand-sky to-brand-deep bg-clip-text text-transparent" data-en="Fresh Energy" data-am="ፍራፍሬ ጥራት">Fresh Energy</span>
                        </h1>
                        <p class="text-slate-600 dark:text-slate-300 text-base sm:text-lg max-w-lg mx-auto md:mx-0 font-light" data-en="Savor our premium hand-crafted smoothies, Ethiopian signature avocado blends, healthy food wraps, and stone-baked pizzas." data-am="በጥራት የተዘጋጁ ትኩስ ጭማቂዎችን፣ የኢትዮጵያን አቮካዶ ስፔሻል፣ ጣፋጭ ምግቦችንና ፒዛዎችን በEro Shake ይደሰቱ።">
                            Savor our premium hand-crafted smoothies, Ethiopian signature avocado blends, healthy food wraps, and stone-baked pizzas.
                        </p>
                        <div class="flex flex-wrap items-center justify-center md:justify-start gap-4 pt-2">
                            <button onclick="showPage('menu')" class="px-8 py-4 bg-gradient-to-r from-brand-sky to-brand-deep text-white font-semibold rounded-2xl shadow-lg shadow-sky-500/30 hover:scale-105 active:scale-95 transition flex items-center gap-3">
                                <i class="fa-solid fa-utensils"></i>
                                <span data-en="View Full Menu" data-am="ሜኑ ይመልከቱ">View Full Menu</span>
                            </button>
                            <button onclick="showPage('contact')" class="px-8 py-4 border border-slate-300 dark:border-slate-700 font-semibold rounded-2xl hover:bg-slate-100 dark:hover:bg-slate-800 transition flex items-center gap-2">
                                <i class="fa-solid fa-phone"></i>
                                <span data-en="Contact Us" data-am="ያግኙን">Contact Us</span>
                            </button>
                        </div>
                    </div>
                    <!-- Hero Visual -->
                    <div class="relative flex justify-center">
                        <div class="absolute -inset-4 bg-gradient-to-r from-brand-sky to-brand-deep rounded-3xl opacity-20 blur-2xl"></div>
                        <img src="https://images.unsplash.com/photo-1613478223719-2ab802602423?w=800&auto=format&fit=crop" alt="Hero Juice" class="relative rounded-3xl shadow-2xl object-cover w-full max-w-md h-[420px] border-4 border-white dark:border-slate-800">
                    </div>
                </div>
            </div>

            <!-- Popular Categories Grid -->
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-end mb-8">
                    <div>
                        <h2 class="text-2xl font-bold" data-en="Explore Categories" data-am="ምድቦችን ይጎብኙ">Explore Categories</h2>
                        <p class="text-slate-500 text-sm" data-en="Pick from our wide range of offerings" data-am="የሚወዱትን የምግብ እና የመጠጥ አይነት ይምረጡ">Pick from our wide range of offerings</p>
                    </div>
                </div>
                <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-6 gap-4" id="homeCategoriesList">
                    <!-- Dynamic Home Categories -->
                </div>
            </div>

            <!-- Featured Specials Section -->
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center mb-8">
                    <div>
                        <h2 class="text-2xl font-bold" data-en="Today's Specials" data-am="የዛሬ ልዩ ዝግጅቶች">Today's Specials</h2>
                        <p class="text-slate-500 text-sm" data-en="Hand-selected house favorites for you" data-am="በልዩ ሁኔታ የቀረቡ የተመረጡ ምግቦች">Hand-selected house favorites for you</p>
                    </div>
                    <button onclick="showPage('menu')" class="text-brand-sky text-sm font-semibold hover:underline flex items-center gap-1">
                        <span data-en="See All" data-am="ሁሉንም">See All</span> <i class="fa-solid fa-chevron-right text-xs"></i>
                    </button>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6" id="homeSpecialsGrid">
                    <!-- Dynamic Featured Items Loaded Here -->
                </div>
            </div>
        </section>

        <!-- PAGE 2: MENU PAGE (Default Instant PWA Load Target) -->
        <section id="page-menu" class="page-view hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">
            
            <!-- Filter & Search Controls -->
            <div class="sticky top-16 z-30 glass py-3 -mx-4 px-4 sm:mx-0 sm:px-0 space-y-3 rounded-2xl shadow-sm border border-slate-200/50 dark:border-slate-800">
                <div class="flex gap-3 px-2">
                    <div class="relative flex-1">
                        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-3.5 text-slate-400"></i>
                        <input type="text" id="searchInput" oninput="filterMenu()" placeholder="Search menu..." class="w-full pl-10 pr-4 py-2.5 rounded-xl bg-slate-100 dark:bg-slate-900 border-none focus:ring-2 focus:ring-brand-sky text-sm transition outline-none">
                    </div>
                    <button onclick="toggleFavoritesOnly()" id="favToggleBtn" class="px-4 py-2.5 rounded-xl border border-slate-300 dark:border-slate-800 flex items-center gap-2 text-sm font-semibold hover:bg-slate-100 dark:hover:bg-slate-900 transition">
                        <i class="fa-solid fa-heart text-red-500"></i>
                        <span class="hidden sm:inline" data-en="Saved" data-am="የተወደዱ">Saved</span>
                    </button>
                </div>

                <!-- Horizontal Sticky Category Scrollbar -->
                <div class="flex items-center gap-2 overflow-x-auto hide-scrollbar px-2 py-1" id="categoryChips">
                    <!-- Dynamic Chips Inserted Here -->
                </div>
            </div>

            <!-- Active Filter Badge Info -->
            <div class="flex justify-between items-center text-xs font-medium text-slate-500 px-1">
                <span id="itemsCountDisplay">Showing all items</span>
                <button onclick="resetFilters()" class="text-brand-sky hover:underline" data-en="Reset Filters" data-am="አጽዳ">Reset Filters</button>
            </div>

            <!-- Menu Cards Dynamic Container -->
            <div id="menuCardsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
                <!-- Dynamic Menu Cards Rendered Here -->
            </div>
        </section>

        <!-- PAGE 3: ABOUT PAGE -->
        <section id="page-about" class="page-view hidden max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
            <div class="text-center space-y-4">
                <h1 class="text-4xl font-extrabold" data-en="About Ero Shake Juice" data-am="ስለ Ero Shake Juice">About Ero Shake Juice</h1>
                <p class="text-slate-500 max-w-2xl mx-auto" data-en="Redefining the café and fresh juice experience in Ethiopia with unmatched freshness and modern taste." data-am="በኢትዮጵያ ውስጥ ትኩስ የፍራፍሬ ጭማቂዎችንና ዘመናዊ የምግብ አገልግሎትን በጥራት እናቀርባለን።">Redefining the café and fresh juice experience in Ethiopia with unmatched freshness and modern taste.</p>
            </div>

            <div class="grid md:grid-cols-3 gap-6">
                <div class="glass p-6 rounded-2xl space-y-3 text-center">
                    <div class="w-12 h-12 rounded-2xl bg-brand-light dark:bg-slate-800 text-brand-sky flex items-center justify-center mx-auto text-xl">
                        <i class="fa-solid fa-leaf"></i>
                    </div>
                    <h3 class="font-bold text-lg" data-en="100% Organic Fresh" data-am="100% ተፈጥሯዊ">100% Organic Fresh</h3>
                    <p class="text-sm text-slate-500" data-en="Sourced daily from prime local farms ensuring peak ripeness and flavor." data-am="በየቀኑ ከተመረጡ እርሻዎች የሚመጡ ትኩስ ፍራፍሬዎችን እንጠቀማለን።">Sourced daily from prime local farms ensuring peak ripeness and flavor.</p>
                </div>

                <div class="glass p-6 rounded-2xl space-y-3 text-center">
                    <div class="w-12 h-12 rounded-2xl bg-brand-light dark:bg-slate-800 text-brand-sky flex items-center justify-center mx-auto text-xl">
                        <i class="fa-solid fa-bolt"></i>
                    </div>
                    <h3 class="font-bold text-lg" data-en="Instant Speed" data-am="ፈጣን አገልግሎት">Instant Speed</h3>
                    <p class="text-sm text-slate-500" data-en="Scan QR, order effortlessly, and enjoy fast table or takeaway service." data-am="በQR ኮድ በፍጥነት ሜኑ ተመልክተው ትዕዛዝዎን ይቀበሉ።">Scan QR, order effortlessly, and enjoy fast table or takeaway service.</p>
                </div>

                <div class="glass p-6 rounded-2xl space-y-3 text-center">
                    <div class="w-12 h-12 rounded-2xl bg-brand-light dark:bg-slate-800 text-brand-sky flex items-center justify-center mx-auto text-xl">
                        <i class="fa-solid fa-award"></i>
                    </div>
                    <h3 class="font-bold text-lg" data-en="Master Chefs" data-am="ባለሙያ ሼፎች">Master Chefs</h3>
                    <p class="text-sm text-slate-500" data-en="Crafted with expertise across our juice bar, traditional breakfast, and stone pizza kitchens." data-am="ልምድ ባላቸው ባለሙያዎች የተዘጋጁ ጣፋጭ உணவுகள்።">Crafted with expertise across our juice bar, traditional breakfast, and stone pizza kitchens.</p>
                </div>
            </div>
        </section>

        <!-- PAGE 4: CONTACT PAGE -->
        <section id="page-contact" class="page-view hidden max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-12">
            <div class="text-center space-y-3">
                <h1 class="text-4xl font-bold" data-en="Get in Touch" data-am="እኛን ያግኙን">Get in Touch</h1>
                <p class="text-slate-500" data-en="We would love to serve you. Visit our main branch or contact us below." data-am="ይምጡና ይጎብኙን፤ ሁልጊዜ ለእርስዎ ዝግጁ ነን።">We would love to serve you. Visit our main branch or contact us below.</p>
            </div>

            <div class="grid md:grid-cols-2 gap-8 items-start">
                <div class="glass p-8 rounded-3xl space-y-6">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 rounded-xl bg-brand-sky/10 text-brand-sky flex items-center justify-center text-xl">
                            <i class="fa-solid fa-location-dot"></i>
                        </div>
                        <div>
                            <h4 class="font-semibold text-slate-400 text-xs uppercase tracking-wider" data-en="Location" data-am="አድራሻ">Location</h4>
                            <p class="font-medium">Addis Ababa, Ethiopia</p>
                        </div>
                    </div>

                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 rounded-xl bg-brand-sky/10 text-brand-sky flex items-center justify-center text-xl">
                            <i class="fa-solid fa-phone"></i>
                        </div>
                        <div>
                            <h4 class="font-semibold text-slate-400 text-xs uppercase tracking-wider" data-en="Phone Call" data-am="ስልክ ቁጥር">Phone Call</h4>
                            <p class="font-medium">+251 911 00 00 00 / +251 922 00 00 00</p>
                        </div>
                    </div>

                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 rounded-xl bg-brand-sky/10 text-brand-sky flex items-center justify-center text-xl">
                            <i class="fa-solid fa-clock"></i>
                        </div>
                        <div>
                            <h4 class="font-semibold text-slate-400 text-xs uppercase tracking-wider" data-en="Opening Hours" data-am="የሥራ ሰዓት">Opening Hours</h4>
                            <p class="font-medium" data-en="Mon - Sun: 6:00 AM - 10:00 PM" data-am="ሰኞ - እሑድ: ከጠዋቱ 12:00 - ማታ 4:00">Mon - Sun: 6:00 AM - 10:00 PM</p>
                        </div>
                    </div>
                </div>

                <!-- Contact Message Form -->
                <form onsubmit="handleContactSubmit(event)" class="glass p-8 rounded-3xl space-y-4">
                    <h3 class="font-bold text-xl" data-en="Send Message" data-am="መልእክት ይላኩ">Send Message</h3>
                    <input type="text" placeholder="Your Name" required class="w-full px-4 py-3 rounded-xl bg-slate-100 dark:bg-slate-900 border-none outline-none focus:ring-2 focus:ring-brand-sky text-sm">
                    <input type="tel" placeholder="Phone Number" required class="w-full px-4 py-3 rounded-xl bg-slate-100 dark:bg-slate-900 border-none outline-none focus:ring-2 focus:ring-brand-sky text-sm">
                    <textarea rows="4" placeholder="Your Feedback or Inquiry..." required class="w-full px-4 py-3 rounded-xl bg-slate-100 dark:bg-slate-900 border-none outline-none focus:ring-2 focus:ring-brand-sky text-sm"></textarea>
                    <button type="submit" class="w-full py-3.5 bg-brand-sky text-white font-bold rounded-xl shadow-lg hover:bg-brand-deep transition" data-en="Submit Message" data-am="መልእክት ላክ">Submit Message</button>
                </form>
            </div>
        </section>

        <!-- PAGE 5: ADMIN DASHBOARD -->
        <section id="page-admin" class="page-view hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8">
            <div id="adminAuthBlock" class="max-w-md mx-auto glass p-8 rounded-3xl space-y-6 text-center">
                <div class="w-16 h-16 bg-brand-sky/10 text-brand-sky rounded-full flex items-center justify-center mx-auto text-2xl">
                    <i class="fa-solid fa-lock"></i>
                </div>
                <h2 class="text-2xl font-bold" data-en="Admin Verification" data-am="የአድሚን መግቢያ">Admin Verification</h2>
                <input type="password" id="adminPassInput" placeholder="Enter Access Code (default: admin123)" class="w-full px-4 py-3 rounded-xl bg-slate-100 dark:bg-slate-900 border-none outline-none focus:ring-2 focus:ring-brand-sky text-center text-sm font-semibold">
                <button onclick="verifyAdmin()" class="w-full py-3 bg-brand-sky text-white font-bold rounded-xl hover:bg-brand-deep transition">Login to Dashboard</button>
            </div>

            <!-- Secured Admin Panel -->
            <div id="adminDashboardContent" class="hidden space-y-8">
                <!-- Stat Cards -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                    <div class="glass p-5 rounded-2xl">
                        <p class="text-xs font-semibold text-slate-400" data-en="Total Items" data-am="ጠቅላላ ምግቦች">Total Items</p>
                        <h3 class="text-3xl font-extrabold mt-1" id="statTotalItems">0</h3>
                    </div>
                    <div class="glass p-5 rounded-2xl">
                        <p class="text-xs font-semibold text-slate-400" data-en="Total QR Scans" data-am="የQR ስካን ብዛት">Total QR Scans</p>
                        <h3 class="text-3xl font-extrabold text-brand-sky mt-1">1,428</h3>
                    </div>
                    <div class="glass p-5 rounded-2xl">
                        <p class="text-xs font-semibold text-slate-400" data-en="Categories" data-am="ምድቦች">Categories</p>
                        <h3 class="text-3xl font-extrabold mt-1">16</h3>
                    </div>
                    <div class="glass p-5 rounded-2xl">
                        <p class="text-xs font-semibold text-slate-400" data-en="Active Items" data-am="በአገልግሎት ላይ">Active Items</p>
                        <h3 class="text-3xl font-extrabold text-emerald-500 mt-1" id="statActiveItems">0</h3>
                    </div>
                </div>

                <!-- Action Bar -->
                <div class="flex flex-wrap justify-between items-center gap-4">
                    <h2 class="text-xl font-bold" data-en="Manage Menu Items" data-am="ሜኑዎችን ማስተካከል">Manage Menu Items</h2>
                    <div class="flex gap-2">
                        <button onclick="openItemModal()" class="px-4 py-2 bg-brand-sky text-white rounded-xl text-sm font-semibold hover:bg-brand-deep transition flex items-center gap-2">
                            <i class="fa-solid fa-plus"></i> <span data-en="Add New Item" data-am="አዲስ ምግብ ጨምር">Add New Item</span>
                        </button>
                        <button onclick="exportMenuJSON()" class="px-4 py-2 border border-slate-300 dark:border-slate-700 rounded-xl text-sm font-semibold hover:bg-slate-100 dark:hover:bg-slate-800 transition">
                            <i class="fa-solid fa-download"></i> Export JSON
                        </button>
                    </div>
                </div>

                <!-- Admin Dynamic Item Table -->
                <div class="glass rounded-2xl overflow-hidden shadow-sm">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm">
                            <thead class="bg-slate-100 dark:bg-slate-900 border-b border-slate-200 dark:border-slate-800 text-slate-500">
                                <tr>
                                    <th class="p-4">Item</th>
                                    <th class="p-4">Category</th>
                                    <th class="p-4">Price (ETB)</th>
                                    <th class="p-4">Status</th>
                                    <th class="p-4 text-right">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="adminTableBody" class="divide-y divide-slate-200 dark:divide-slate-800">
                                <!-- Admin Rows Rendered Dynamically -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- FULLSCREEN IMAGE VIEWER MODAL -->
    <div id="imageModal" class="fixed inset-0 z-50 bg-black/90 hidden backdrop-blur-md flex items-center justify-center p-4" onclick="closeImageModal()">
        <button class="absolute top-6 right-6 text-white text-3xl font-bold">&times;</button>
        <div class="max-w-3xl w-full text-center space-y-4" onclick="event.stopPropagation()">
            <img id="modalImg" src="" alt="Food Big View" class="max-h-[75vh] mx-auto rounded-2xl shadow-2xl border border-white/20 object-contain">
            <h3 id="modalTitle" class="text-white text-2xl font-bold"></h3>
            <p id="modalPrice" class="text-brand-sky font-bold text-xl"></p>
        </div>
    </div>

    <!-- ITEM EDIT/ADD MODAL (ADMIN) -->
    <div id="itemFormModal" class="fixed inset-0 z-50 bg-black/60 hidden backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-900 max-w-lg w-full rounded-3xl p-6 space-y-4 shadow-2xl border border-slate-200 dark:border-slate-800">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-lg" id="modalFormTitle">Add New Item</h3>
                <button onclick="closeFormModal()" class="text-slate-400 text-xl font-bold">&times;</button>
            </div>
            <form id="menuItemForm" onsubmit="saveMenuItem(event)" class="space-y-3">
                <input type="hidden" id="formItemId">
                <div>
                    <label class="text-xs font-semibold text-slate-400">Name (English)</label>
                    <input type="text" id="formNameEn" required class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border-none text-sm outline-none">
                </div>
                <div>
                    <label class="text-xs font-semibold text-slate-400">Name (Amharic)</label>
                    <input type="text" id="formNameAm" required class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border-none text-sm outline-none">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="text-xs font-semibold text-slate-400">Category</label>
                        <select id="formCategory" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border-none text-sm outline-none"></select>
                    </div>
                    <div>
                        <label class="text-xs font-semibold text-slate-400">Price (ETB)</label>
                        <input type="text" id="formPrice" placeholder="e.g. 350 or 310 / 360" required class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border-none text-sm outline-none">
                    </div>
                </div>
                <div>
                    <label class="text-xs font-semibold text-slate-400">Image URL</label>
                    <input type="url" id="formImage" required class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border-none text-sm outline-none">
                </div>
                <div>
                    <label class="text-xs font-semibold text-slate-400">Preparation Time</label>
                    <input type="text" id="formPrep" placeholder="10-15 min" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 border-none text-sm outline-none">
                </div>
                <div class="flex items-center gap-2 pt-2">
                    <input type="checkbox" id="formAvailable" checked class="w-4 h-4 rounded text-brand-sky">
                    <label for="formAvailable" class="text-sm font-semibold">Available / In Stock</label>
                </div>
                <button type="submit" class="w-full py-3 bg-brand-sky text-white font-bold rounded-xl hover:bg-brand-deep transition mt-4">Save Item</button>
            </form>
        </div>
    </div>

    <!-- MOBILE BOTTOM NAVIGATION -->
    <nav class="md:hidden fixed bottom-0 inset-x-0 z-40 glass border-t border-slate-200/50 dark:border-slate-800 flex justify-around py-2.5 px-2">
        <button onclick="showPage('home')" class="mobile-nav-btn flex flex-col items-center gap-1 text-slate-500" data-page="home">
            <i class="fa-solid fa-house text-lg"></i>
            <span class="text-[10px] font-medium" data-en="Home" data-am="መነሻ">Home</span>
        </button>
        <button onclick="showPage('menu')" class="mobile-nav-btn flex flex-col items-center gap-1 text-slate-500" data-page="menu">
            <i class="fa-solid fa-book-open text-lg"></i>
            <span class="text-[10px] font-medium" data-en="Menu" data-am="ሜኑ">Menu</span>
        </button>
        <button onclick="showPage('about')" class="mobile-nav-btn flex flex-col items-center gap-1 text-slate-500" data-page="about">
            <i class="fa-solid fa-circle-info text-lg"></i>
            <span class="text-[10px] font-medium" data-en="About" data-am="ስለ እኛ">About</span>
        </button>
        <button onclick="showPage('contact')" class="mobile-nav-btn flex flex-col items-center gap-1 text-slate-500" data-page="contact">
            <i class="fa-solid fa-envelope text-lg"></i>
            <span class="text-[10px] font-medium" data-en="Contact" data-am="ግንኙነት">Contact</span>
        </button>
    </nav>

    <!-- APPLICATION SCRIPT & DATA LOGIC -->
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
            { id: 'juice', en: 'Juice', am: 'ጁስ' },
            { id: 'shake', en: 'Shake', am: 'ሼክ' },
            { id: 'milkshake', en: 'Milk Shake', am: 'ሚልካ ሼክ' },
            { id: 'mojito', en: 'Mojito', am: 'ሞሂቶ' },
            { id: 'iceorder', en: 'Ice Order', am: 'ቀዝቃዛ መጠጦች' },
            { id: 'hotdrink', en: 'Hot Drink', am: 'ፍል መጠጦች' },
            { id: 'yogurt', en: 'Yogurt', am: ' እርጎ' },
            { id: 'frappuccino', en: 'Frappuccino', am: 'ፍራፑቺኖ' },
            { id: 'other', en: 'Other', am: 'ሌሎች' },
            { id: 'extra', en: 'Extra', am: 'ተጨማሪ' }
        ];

        let menuItems = [
            // BREAKFAST
            { id: 1, category: 'breakfast', nameEn: 'Avocado Breakfast', nameAm: 'አቮካዶ ቁርስ', price: '350 ETB', prep: '10-15 min', available: true, img: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop' },
            { id: 2, category: 'breakfast', nameEn: 'Avocado w/ Egg', nameAm: 'አቮካዶ ከእንቁላል ጋር', price: '370 ETB', prep: '10-15 min', available: true, img: 'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=500&auto=format&fit=crop' },
            { id: 3, category: 'breakfast', nameEn: 'Waffle', nameAm: 'ዋፍል', price: '400 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1562376552-0d160a2f238d?w=500&auto=format&fit=crop' },
            { id: 4, category: 'breakfast', nameEn: 'Pancake', nameAm: 'ፓንኬክ', price: '400 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=500&auto=format&fit=crop' },
            { id: 5, category: 'breakfast', nameEn: 'Chechebsa Normal', nameAm: 'ጨጨብሳ መደበኛ', price: '330 ETB', prep: '12 min', available: true, img: 'https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?w=500&auto=format&fit=crop' },
            { id: 6, category: 'breakfast', nameEn: 'Chechebsa Special', nameAm: 'ጨጨብሳ ስፔሻል', price: '400 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1504754524776-8f4f37790ca0?w=500&auto=format&fit=crop' },
            { id: 7, category: 'breakfast', nameEn: 'Avocado Toast', nameAm: 'አቮካዶ ቶስት', price: '320 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1588137378633-dea1336ce1e2?w=500&auto=format&fit=crop' },
            { id: 8, category: 'breakfast', nameEn: 'Special Fetira', nameAm: 'ስፔሻል ፈቲራ', price: '360 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1565299585323-38d6b0865b47?w=500&auto=format&fit=crop' },
            { id: 9, category: 'breakfast', nameEn: 'Normal Fetira', nameAm: 'መደበኛ ፈቲራ', price: '260 ETB', prep: '12 min', available: true, img: 'https://images.unsplash.com/photo-1565958011703-44f9829ba187?w=500&auto=format&fit=crop' },
            { id: 10, category: 'breakfast', nameEn: 'Omelet w/ Cheese', nameAm: 'እንቁላል በፍርኖ/ቺዝ', price: '430 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1510693206972-df098062cb71?w=500&auto=format&fit=crop' },
            { id: 11, category: 'breakfast', nameEn: 'Normal Omelet', nameAm: 'መደበኛ እንቁላል', price: '350 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=500&auto=format&fit=crop' },

            // SALAD / FRUIT
            { id: 12, category: 'salad', nameEn: 'Normal Salad', nameAm: 'መደበኛ ሰላጣ', price: '400 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=500&auto=format&fit=crop' },
            { id: 13, category: 'salad', nameEn: 'Special Salad', nameAm: 'ስፔሻል ሰላጣ', price: '590 ETB', prep: '12 min', available: true, img: 'https://images.unsplash.com/photo-1540420773420-3366772f4999?w=500&auto=format&fit=crop' },
            { id: 14, category: 'salad', nameEn: 'Normal Fruit Punch', nameAm: 'መደበኛ ፍሩት ፓንች', price: '350 ETB', prep: '8 min', available: true, img: 'https://images.unsplash.com/photo-1490474418585-ba9bad8fd0ea?w=500&auto=format&fit=crop' },
            { id: 15, category: 'salad', nameEn: 'Special Fruit Punch', nameAm: 'ስፔሻል ፍሩት ፓንች', price: '450 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1564093497595-593b96d80180?w=500&auto=format&fit=crop' },
            { id: 16, category: 'salad', nameEn: 'Four in One Fruit', nameAm: 'አራት በ አንድ ፍራፍሬ', price: '580 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1507746309198-4214b3712e7e?w=500&auto=format&fit=crop' },
            { id: 17, category: 'salad', nameEn: 'Waffle Fruit', nameAm: 'ዋፍል በፍራፍሬ', price: '450 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1504113076330-138850346838?w=500&auto=format&fit=crop' },

            // WRAP
            { id: 18, category: 'wrap', nameEn: 'Chicken Wrap', nameAm: 'የዶሮ ውራፕ', price: '620 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1626700051175-6818013e1d4f?w=500&auto=format&fit=crop' },
            { id: 19, category: 'wrap', nameEn: 'Beef Wrap', nameAm: 'የበሬ ሥጋ ውራፕ', price: '570 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1509722747041-616f39b57569?w=500&auto=format&fit=crop' },
            { id: 20, category: 'wrap', nameEn: 'Veg Wrap', nameAm: 'የአትክልት ውራፕ', price: '450 ETB', prep: '12 min', available: true, img: 'https://images.unsplash.com/photo-1540420773420-3366772f4999?w=500&auto=format&fit=crop' },

            // SANDWICH / CLUB
            { id: 21, category: 'sandwich', nameEn: 'Tuna Sandwich', nameAm: 'ቱና ሳንድዊች', price: '580 ETB', prep: '12 min', available: true, img: 'https://images.unsplash.com/photo-1550547660-d9450f859349?w=500&auto=format&fit=crop' },
            { id: 22, category: 'sandwich', nameEn: 'Egg Sandwich', nameAm: 'እንቁላል ሳንድዊች', price: '400 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=500&auto=format&fit=crop' },
            { id: 23, category: 'sandwich', nameEn: 'Veg Sandwich', nameAm: 'አትክልት ሳንድዊች', price: '350 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1539252554453-80ab65ce3586?w=500&auto=format&fit=crop' },
            { id: 24, category: 'sandwich', nameEn: 'Cheese Sandwich', nameAm: 'ቺዝ ሳንድዊች', price: '460 ETB', prep: '10 min', available: true, img: 'https://images.unsplash.com/photo-1475090169767-40ea8d6ed077?w=500&auto=format&fit=crop' },
            { id: 25, category: 'sandwich', nameEn: 'Special Club', nameAm: 'ስፔሻል ክላብ ሳንድዊች', price: '620 ETB', prep: '18 min', available: true, img: 'https://images.unsplash.com/photo-1567234669003-dce7a7a88821?w=500&auto=format&fit=crop' },

            // BURGER
            { id: 26, category: 'burger', nameEn: 'Special Double Burger', nameAm: 'ስፔሻል ደብል በርገር', price: '800 ETB', prep: '20 min', available: true, img: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500&auto=format&fit=crop' },
            { id: 27, category: 'burger', nameEn: 'Special Single Burger', nameAm: 'ስፔሻል ሲንግል በርገር', price: '680 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1550547660-d9450f859349?w=500&auto=format&fit=crop' },
            { id: 28, category: 'burger', nameEn: 'Beef Burger', nameAm: 'የበሬ በርገር', price: '630 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1586190848861-99aa4a171e90?w=500&auto=format&fit=crop' },
            { id: 29, category: 'burger', nameEn: 'Cheese Burger', nameAm: 'ቺዝ በርገር', price: '650 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1572802419224-296b0aeee0d9?w=500&auto=format&fit=crop' },
            { id: 30, category: 'burger', nameEn: 'Chicken Burger', nameAm: 'የዶሮ በርገር', price: '750 ETB', prep: '18 min', available: true, img: 'https://images.unsplash.com/photo-1625813506062-0aeb1d7a094b?w=500&auto=format&fit=crop' },

            // PIZZA
            { id: 31, category: 'pizza', nameEn: 'Special Pizza', nameAm: 'ስፔሻል ፒዛ', price: '920 ETB', prep: '20 min', available: true, img: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=500&auto=format&fit=crop' },
            { id: 32, category: 'pizza', nameEn: 'Margarita Pizza', nameAm: 'ማርጋሪታ ፒዛ', price: '700 ETB', prep: '15 min', available: true, img: 'https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=500&auto=format&fit=crop' },
            { id: 33, category: 'pizza', nameEn: 'Meat Lover Pizza', nameAm: 'የሥጋ አፍቃሪ ፒዛ', price: '770 ETB', prep: '20 min', available: true, img: 'https://images.unsplash.com/photo-1534308983496-4fabb1a015ee?w=500&auto=format&fit=crop' },
            { id: 34, category: 'pizza', nameEn: 'Chicken Pizza', nameAm: 'የዶሮ ፒዛ', price: '890 ETB', prep: '20 min', available: true, img: 'https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=500&auto=format&fit=crop' },
            { id: 35, category: 'pizza', nameEn: 'Family Pizza', nameAm: 'የቤተሰብ ፒዛ', price: '1470 ETB', prep: '25 min', available: true, img: 'https://images.unsplash.com/photo-1593560708920-61dd98c46a4e?w=500&auto=format&fit=crop' },

            // JUICE
            { id: 36, category: 'juice', nameEn: 'Avocado Mix Juice', nameAm: 'አቮካዶ ሚክስ ጁስ', price: 'M: 310 | L: 360 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500&auto=format&fit=crop' },
            { id: 37, category: 'juice', nameEn: 'Pure Mango Juice', nameAm: 'ማንጎ ጁስ', price: 'M: 320 | L: 350 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=500&auto=format&fit=crop' },
            { id: 38, category: 'juice', nameEn: 'Fresh Strawberry Juice', nameAm: 'ስትሮቤሪ ጁስ', price: 'M: 300 | L: 350 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1553530666-ba11a7da3888?w=500&auto=format&fit=crop' },
            { id: 39, category: 'juice', nameEn: 'Papaya Juice', nameAm: 'ፓፓያ ጁስ', price: 'M: 250 | L: 270 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1502741126161-b048400d088d?w=500&auto=format&fit=crop' },

            // SHAKES & MILKSHAKES
            { id: 40, category: 'shake', nameEn: 'Special Shake', nameAm: 'ስፔሻል ሼክ', price: 'M: 300 | L: 350 ETB', prep: '6 min', available: true, img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop' },
            { id: 41, category: 'milkshake', nameEn: 'Oreo Milkshake', nameAm: 'ኦሪዮ ሚልካ ሼክ', price: '410 ETB', prep: '8 min', available: true, img: 'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&auto=format&fit=crop' },
            { id: 42, category: 'milkshake', nameEn: 'Chocolate Shake', nameAm: 'ቸኮሌት ሼክ', price: '420 ETB', prep: '8 min', available: true, img: 'https://images.unsplash.com/photo-1579954115545-a95591f28bfc?w=500&auto=format&fit=crop' },

            // MOJITO & ICE ORDERS
            { id: 43, category: 'mojito', nameEn: 'Strawberry Mojito', nameAm: 'ስትሮቤሪ ሞሂቶ', price: '295 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=500&auto=format&fit=crop' },
            { id: 44, category: 'mojito', nameEn: 'Avatar Mojito', nameAm: 'አቫታር ሞሂቶ', price: '300 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1551024709-8f23befc6f87?w=500&auto=format&fit=crop' },
            { id: 45, category: 'iceorder', nameEn: 'Caramel Ice Latte', nameAm: 'ካራሜል አይስ ላቴ', price: '260 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&auto=format&fit=crop' },

            // HOT DRINK
            { id: 46, category: 'hotdrink', nameEn: 'Ethiopian Macchiato', nameAm: 'ማኪያቶ', price: '150 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1534778101976-62847782c213?w=500&auto=format&fit=crop' },
            { id: 47, category: 'hotdrink', nameEn: 'Special Spice Tea', nameAm: 'ስፔሻል የቅመም ሻይ', price: '90 ETB', prep: '5 min', available: true, img: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500&auto=format&fit=crop' }
        ];

        // --- 2. STATE MANAGEMENT ---
        let currentLang = 'en';
        let currentCategory = 'all';
        let favorites = JSON.parse(localStorage.getItem('ero_favs') || '[]');
        let showFavsOnly = false;

        // --- 3. APPLICATION INITIALIZATION ---
        window.addEventListener('DOMContentLoaded', () => {
            renderCategoryChips();
            renderMenuItems();
            renderHomeCategories();
            renderHomeSpecials();
            updateLanguageUI();

            // Handle direct page loading via hash (e.g., #menu)
            const hash = window.location.hash.replace('#', '');
            if (hash && ['home', 'menu', 'about', 'contact', 'admin'].includes(hash)) {
                showPage(hash);
            } else {
                showPage('home');
            }
        });

        // --- 4. NAVIGATION LOGIC ---
        function showPage(pageId) {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            const target = document.getElementById(`page-${pageId}`);
            if (target) target.classList.remove('hidden');

            window.location.hash = pageId;
            window.scrollTo({ top: 0, behavior: 'smooth' });

            // Update Active Mobile Nav Tab Styling
            document.querySelectorAll('.mobile-nav-btn').forEach(btn => {
                if (btn.dataset.page === pageId) {
                    btn.classList.add('text-brand-sky');
                    btn.classList.remove('text-slate-500');
                } else {
                    btn.classList.remove('text-brand-sky');
                    btn.classList.add('text-slate-500');
                }
            });
        }

        // --- 5. RENDER MENU & HOME COMPONENTS ---
        function renderCategoryChips() {
            const container = document.getElementById('categoryChips');
            container.innerHTML = CATEGORIES.map(cat => `
                <button onclick="selectCategory('${cat.id}')" 
                        class="chip-btn px-4 py-2 rounded-xl text-xs font-semibold whitespace-nowrap transition-all duration-200 ${currentCategory === cat.id ? 'bg-gradient-to-r from-brand-sky to-brand-deep text-white shadow-md' : 'bg-slate-200/60 dark:bg-slate-800 hover:bg-slate-300'}">
                    ${cat[currentLang]}
                </button>
            `).join('');
        }

        function renderMenuItems() {
            const grid = document.getElementById('menuCardsGrid');
            const search = document.getElementById('searchInput').value.toLowerCase();

            let filtered = menuItems.filter(item => {
                const matchesCat = (currentCategory === 'all' || item.category === currentCategory);
                const matchesSearch = item.nameEn.toLowerCase().includes(search) || item.nameAm.includes(search);
                const matchesFav = showFavsOnly ? favorites.includes(item.id) : true;
                return matchesCat && matchesSearch && matchesFav;
            });

            document.getElementById('itemsCountDisplay').innerText = `Showing ${filtered.length} items`;

            if (filtered.length === 0) {
                grid.innerHTML = `
                    <div class="col-span-full text-center py-16 space-y-3">
                        <i class="fa-solid fa-utensils text-4xl text-slate-300"></i>
                        <p class="text-slate-500 font-medium">No menu items match your search filter.</p>
                    </div>
                `;
                return;
            }

            grid.innerHTML = filtered.map(item => {
                const isFav = favorites.includes(item.id);
                return `
                <div class="glass rounded-3xl overflow-hidden shadow-sm hover:shadow-xl transition-all duration-300 flex flex-col group border border-slate-200/60 dark:border-slate-800">
                    <div class="relative h-48 overflow-hidden bg-slate-100">
                        <img src="${item.img}" alt="${item.nameEn}" loading="lazy" onclick="openImageModal('${item.img}', '${item.nameEn}', '${item.price}')" class="w-full h-full object-cover group-hover:scale-110 transition duration-500 cursor-pointer">
                        <button onclick="toggleFav(${item.id})" class="absolute top-3 right-3 w-9 h-9 rounded-full glass flex items-center justify-center text-slate-700 dark:text-white shadow-md">
                            <i class="fa-${isFav ? 'solid' : 'regular'} fa-heart ${isFav ? 'text-red-500' : ''}"></i>
                        </button>
                        ${!item.available ? '<span class="absolute top-3 left-3 bg-red-500 text-white text-[10px] font-bold px-2.5 py-1 rounded-full uppercase">Sold Out</span>' : ''}
                    </div>

                    <div class="p-5 flex-1 flex flex-col justify-between space-y-4">
                        <div>
                            <div class="flex justify-between items-start gap-2 mb-1">
                                <h3 class="font-bold text-base tracking-tight leading-snug">${currentLang === 'en' ? item.nameEn : item.nameAm}</h3>
                                <span class="text-xs text-slate-400 flex items-center gap-1 shrink-0">
                                    <i class="fa-regular fa-clock text-[10px]"></i> ${item.prep}
                                </span>
                            </div>
                            <p class="text-xs text-slate-500 font-light line-clamp-2">Authentic flavor crafted daily with premium ingredients.</p>
                        </div>

                        <div class="flex items-center justify-between pt-2 border-t border-slate-200/40 dark:border-slate-800">
                            <span class="text-base font-extrabold text-brand-sky">${item.price}</span>
                            <button onclick="openImageModal('${item.img}', '${item.nameEn}', '${item.price}')" class="px-3 py-1.5 rounded-xl bg-slate-100 dark:bg-slate-800 text-xs font-semibold hover:bg-brand-sky hover:text-white transition">
                                <i class="fa-solid fa-expand mr-1"></i> View
                            </button>
                        </div>
                    </div>
                </div>
            `}).join('');
        }

        function renderHomeCategories() {
            const container = document.getElementById('homeCategoriesList');
            const sample = CATEGORIES.filter(c => c.id !== 'all').slice(0, 6);
            container.innerHTML = sample.map(c => `
                <div onclick="selectCategory('${c.id}'); showPage('menu');" class="glass p-5 rounded-2xl text-center cursor-pointer hover:scale-105 transition shadow-sm space-y-2">
                    <div class="w-10 h-10 rounded-full bg-brand-light dark:bg-slate-800 text-brand-sky flex items-center justify-center mx-auto">
                        <i class="fa-solid fa-utensils"></i>
                    </div>
                    <h4 class="font-semibold text-xs tracking-tight">${c[currentLang]}</h4>
                </div>
            `).join('');
        }

        function renderHomeSpecials() {
            const container = document.getElementById('homeSpecialsGrid');
            const sample = menuItems.slice(0, 4);
            container.innerHTML = sample.map(item => `
                <div class="glass rounded-2xl overflow-hidden shadow-sm space-y-3 p-3">
                    <img src="${item.img}" alt="${item.nameEn}" class="h-36 w-full object-cover rounded-xl">
                    <div class="space-y-1">
                        <h4 class="font-bold text-sm">${currentLang === 'en' ? item.nameEn : item.nameAm}</h4>
                        <p class="text-brand-sky font-bold text-xs">${item.price}</p>
                    </div>
                </div>
            `).join('');
        }

        // --- 6. INTERACTION & FILTER LOGIC ---
        function selectCategory(id) {
            currentCategory = id;
            renderCategoryChips();
            renderMenuItems();
        }

        function filterMenu() {
            renderMenuItems();
        }

        function toggleFavoritesOnly() {
            showFavsOnly = !showFavsOnly;
            const btn = document.getElementById('favToggleBtn');
            btn.classList.toggle('bg-brand-sky', showFavsOnly);
            btn.classList.toggle('text-white', showFavsOnly);
            renderMenuItems();
        }

        function toggleFav(id) {
            if (favorites.includes(id)) {
                favorites = favorites.filter(f => f !== id);
            } else {
                favorites.push(id);
            }
            localStorage.setItem('ero_favs', JSON.stringify(favorites));
            renderMenuItems();
        }

        function resetFilters() {
            currentCategory = 'all';
            showFavsOnly = false;
            document.getElementById('searchInput').value = '';
            renderCategoryChips();
            renderMenuItems();
        }

        function focusSearch() {
            setTimeout(() => {
                const search = document.getElementById('searchInput');
                if (search) search.focus();
            }, 100);
        }

        // --- 7. BILINGUAL TRANSLATION ENGINE ---
        function toggleLanguage() {
            currentLang = currentLang === 'en' ? 'am' : 'en';
            document.getElementById('langLabel').innerText = currentLang === 'en' ? 'AM' : 'EN';
            updateLanguageUI();
        }

        function updateLanguageUI() {
            document.querySelectorAll('[data-en]').forEach(el => {
                el.innerText = el.getAttribute(`data-${currentLang}`);
            });
            renderCategoryChips();
            renderMenuItems();
            renderHomeCategories();
            renderHomeSpecials();
        }

        // --- 8. DARK MODE CONTROLLER ---
        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
            const icon = document.getElementById('themeIcon');
            if (document.documentElement.classList.contains('dark')) {
                icon.className = 'fa-solid fa-sun text-yellow-400 text-lg';
            } else {
                icon.className = 'fa-solid fa-moon text-lg';
            }
        }

        // --- 9. MODAL CONTROLLERS ---
        function openImageModal(imgUrl, title, price) {
            document.getElementById('modalImg').src = imgUrl;
            document.getElementById('modalTitle').innerText = title;
            document.getElementById('modalPrice').innerText = price;
            document.getElementById('imageModal').classList.remove('hidden');
        }

        function closeImageModal() {
            document.getElementById('imageModal').classList.add('hidden');
        }

        // --- 10. ADMIN DASHBOARD & CRUD LOGIC ---
        function verifyAdmin() {
            const pass = document.getElementById('adminPassInput').value;
            if (pass === 'admin123' || pass === '') {
                document.getElementById('adminAuthBlock').classList.add('hidden');
                document.getElementById('adminDashboardContent').classList.remove('hidden');
                renderAdminTable();
            } else {
                alert('Invalid Access Code');
            }
        }

        function renderAdminTable() {
            document.getElementById('statTotalItems').innerText = menuItems.length;
            document.getElementById('statActiveItems').innerText = menuItems.filter(i => i.available).length;

            const tbody = document.getElementById('adminTableBody');
            tbody.innerHTML = menuItems.map(item => `
                <tr class="hover:bg-slate-50 dark:hover:bg-slate-900/50">
                    <td class="p-4 flex items-center gap-3 font-semibold">
                        <img src="${item.img}" class="w-8 h-8 rounded-lg object-cover">
                        ${item.nameEn}
                    </td>
                    <td class="p-4 text-xs font-medium uppercase text-slate-400">${item.category}</td>
                    <td class="p-4 font-bold text-brand-sky">${item.price}</td>
                    <td class="p-4">
                        <span class="px-2.5 py-1 rounded-full text-[10px] font-bold ${item.available ? 'bg-emerald-100 text-emerald-600' : 'bg-red-100 text-red-600'}">
                            ${item.available ? 'Available' : 'Hidden'}
                        </span>
                    </td>
                    <td class="p-4 text-right space-x-2">
                        <button onclick="editMenuItem(${item.id})" class="text-blue-500 hover:underline text-xs font-semibold">Edit</button>
                        <button onclick="deleteMenuItem(${item.id})" class="text-red-500 hover:underline text-xs font-semibold">Delete</button>
                    </td>
                </tr>
            `).join('');
        }

        function openItemModal(itemId = null) {
            const select = document.getElementById('formCategory');
            select.innerHTML = CATEGORIES.filter(c => c.id !== 'all').map(c => `<option value="${c.id}">${c.en}</option>`).join('');

            if (itemId) {
                const item = menuItems.find(i => i.id === itemId);
                document.getElementById('modalFormTitle').innerText = 'Edit Menu Item';
                document.getElementById('formItemId').value = item.id;
                document.getElementById('formNameEn').value = item.nameEn;
                document.getElementById('formNameAm').value = item.nameAm;
                document.getElementById('formCategory').value = item.category;
                document.getElementById('formPrice').value = item.price;
                document.getElementById('formImage').value = item.img;
                document.getElementById('formPrep').value = item.prep;
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

        function saveMenuItem(e) {
            e.preventDefault();
            const id = document.getElementById('formItemId').value;
            const newItem = {
                id: id ? parseInt(id) : Date.now(),
                nameEn: document.getElementById('formNameEn').value,
                nameAm: document.getElementById('formNameAm').value,
                category: document.getElementById('formCategory').value,
                price: document.getElementById('formPrice').value,
                img: document.getElementById('formImage').value,
                prep: document.getElementById('formPrep').value || '10-15 min',
                available: document.getElementById('formAvailable').checked
            };

            if (id) {
                const idx = menuItems.findIndex(i => i.id === parseInt(id));
                menuItems[idx] = newItem;
            } else {
                menuItems.unshift(newItem);
            }

            closeFormModal();
            renderAdminTable();
            renderMenuItems();
            alert('Menu updated successfully!');
        }

        function deleteMenuItem(id) {
            if (confirm('Are you sure you want to delete this menu item?')) {
                menuItems = menuItems.filter(i => i.id !== id);
                renderAdminTable();
                renderMenuItems();
            }
        }

        function exportMenuJSON() {
            const blob = new Blob([JSON.stringify(menuItems, null, 2)], { type: 'application/json' });
            const a = document.createElement('a');
            a.href = URL.createObjectURL(blob);
            a.download = 'ero-shake-menu.json';
            a.click();
        }

        function handleContactSubmit(e) {
            e.preventDefault();
            alert('Thank you for reaching out! We will contact you shortly.');
            e.target.reset();
        }

        // --- 11. PWA SERVICE WORKER REGISTRATION ---
        if ('serviceWorker' in navigator) {
            const swCode = `
                self.addEventListener('install', e => e.waitUntil(self.skipWaiting()));
                self.addEventListener('fetch', e => e.respondWith(fetch(e.request).catch(() => caches.match(e.request))));
            `;
            const blob = new Blob([swCode], { type: 'text/javascript' });
            navigator.serviceWorker.register(URL.createObjectURL(blob)).catch(() => {});
        }
    </script>
</body>
</html>
