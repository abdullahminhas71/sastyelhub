# index.html
"My export company website"
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SEELINGS | Modern Fashion</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        * {
            font-family: 'Inter', sans-serif;
        }
        .font-serif {
            font-family: 'Playfair Display', serif;
        }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        ::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #555;
        }

        /* Glassmorphism Effects */
        .glass {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        .glass-dark {
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        /* Animations */
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }
        .animate-float {
            animation: float 3s ease-in-out infinite;
        }

        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        .slide-in {
            animation: slideIn 0.3s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .fade-in {
            animation: fadeIn 0.6s ease-out forwards;
        }

        /* Product Card Hover Effects */
        .product-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .product-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }
        .product-card:hover .product-image {
            transform: scale(1.05);
        }
        .product-image {
            transition: transform 0.5s ease;
        }

        /* Quick Add Button Animation */
        .quick-add {
            transform: translateY(100%);
            opacity: 0;
            transition: all 0.3s ease;
        }
        .product-card:hover .quick-add {
            transform: translateY(0);
            opacity: 1;
        }

        /* Loading Skeleton */
        .skeleton {
            background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
            background-size: 200% 100%;
            animation: loading 1.5s infinite;
        }
        @keyframes loading {
            0% { background-position: 200% 0; }
            100% { background-position: -200% 0; }
        }

        /* Toast Notification */
        .toast {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: #1a1a1a;
            color: white;
            padding: 16px 24px;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            z-index: 9999;
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.3s ease;
        }
        .toast.show {
            transform: translateY(0);
            opacity: 1;
        }

        /* Filter Active State */
        .filter-btn.active {
            background-color: #1a1a1a;
            color: white;
        }

        /* Mobile Menu */
        .mobile-menu {
            transform: translateX(-100%);
            transition: transform 0.3s ease;
        }
        .mobile-menu.open {
            transform: translateX(0);
        }

        /* Smooth Scroll */
        html {
            scroll-behavior: smooth;
        }

        /* Custom Selection */
        ::selection {
            background: #1a1a1a;
            color: white;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-900 antialiased overflow-x-hidden">

    <!-- Navigation -->
    <nav class="fixed w-full z-50 glass transition-all duration-300" id="navbar">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- Logo -->
                <div class="flex-shrink-0 flex items-center cursor-pointer" onclick="window.scrollTo(0,0)">
                    <span class="font-serif text-3xl font-bold tracking-tighter">SEELINGS</span>
                </div>

                <!-- Desktop Menu -->
                <div class="hidden md:flex space-x-8 items-center">
                    <a href="#new-arrivals" class="text-gray-700 hover:text-black font-medium transition">New Arrivals</a>
                    <a href="#women" class="text-gray-700 hover:text-black font-medium transition">Women</a>
                    <a href="#men" class="text-gray-700 hover:text-black font-medium transition">Men</a>
                    <a href="#accessories" class="text-gray-700 hover:text-black font-medium transition">Accessories</a>
                    <a href="#sale" class="text-red-600 hover:text-red-700 font-medium transition">Sale</a>
                </div>

                <!-- Icons -->
                <div class="flex items-center space-x-6">
                    <button class="text-gray-700 hover:text-black transition" onclick="toggleSearch()">
                        <i class="fas fa-search text-xl"></i>
                    </button>
                    <button class="text-gray-700 hover:text-black transition relative" onclick="toggleCart()">
                        <i class="fas fa-shopping-bag text-xl"></i>
                        <span id="cart-badge" class="absolute -top-2 -right-2 bg-black text-white text-xs rounded-full h-5 w-5 flex items-center justify-center opacity-0 transition-opacity">0</span>
                    </button>
                    <button class="md:hidden text-gray-700" onclick="toggleMobileMenu()">
                        <i class="fas fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Search Bar -->
        <div id="search-bar" class="hidden absolute top-full left-0 w-full glass border-t border-gray-200 p-4">
            <div class="max-w-3xl mx-auto relative">
                <input type="text" placeholder="Search for clothes, brands, or styles..." 
                       class="w-full px-6 py-3 rounded-full border border-gray-300 focus:outline-none focus:border-black transition"
                       id="search-input">
                <button class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 hover:text-black">
                    <i class="fas fa-arrow-right"></i>
                </button>
            </div>
        </div>
    </nav>

    <!-- Mobile Menu -->
    <div id="mobile-menu" class="mobile-menu fixed inset-0 z-40 bg-white pt-20 px-6 md:hidden">
        <button class="absolute top-6 right-6 text-2xl" onclick="toggleMobileMenu()">
            <i class="fas fa-times"></i>
        </button>
        <div class="flex flex-col space-y-6 text-xl">
            <a href="#new-arrivals" onclick="toggleMobileMenu()" class="border-b border-gray-100 pb-2">New Arrivals</a>
            <a href="#women" onclick="toggleMobileMenu()" class="border-b border-gray-100 pb-2">Women</a>
            <a href="#men" onclick="toggleMobileMenu()" class="border-b border-gray-100 pb-2">Men</a>
            <a href="#accessories" onclick="toggleMobileMenu()" class="border-b border-gray-100 pb-2">Accessories</a>
            <a href="#sale" onclick="toggleMobileMenu()" class="text-red-600 border-b border-gray-100 pb-2">Sale</a>
        </div>
    </div>

    <!-- Hero Section -->
    <section class="relative h-screen flex items-center justify-center overflow-hidden">
        <!-- Background Image with Overlay -->
        <div class="absolute inset-0 z-0">
            <img src="https://images.unsplash.com/photo-1469334031218-e382a71b716b?w=1920&q=80" 
                 alt="Fashion Hero" 
                 class="w-full h-full object-cover">
            <div class="absolute inset-0 bg-black/30"></div>
        </div>

        <!-- Content -->
        <div class="relative z-10 text-center text-white px-4 max-w-5xl mx-auto">
            <p class="text-sm uppercase tracking-[0.3em] mb-4 animate-fade-in" style="animation-delay: 0.1s">Spring Collection 2024</p>
            <h1 class="font-serif text-5xl md:text-7xl lg:text-8xl font-bold mb-6 leading-tight animate-fade-in" style="animation-delay: 0.2s">
                Redefine Your<br>Style
            </h1>
            <p class="text-lg md:text-xl mb-10 max-w-2xl mx-auto text-gray-200 animate-fade-in" style="animation-delay: 0.3s">
                Discover curated fashion pieces that blend contemporary design with timeless elegance. 
                Crafted for the modern individual.
            </p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center animate-fade-in" style="animation-delay: 0.4s">
                <button onclick="scrollToProducts()" class="px-8 py-4 bg-white text-black font-semibold rounded-full hover:bg-gray-100 transition transform hover:scale-105">
                    Shop Now
                </button>
                <button class="px-8 py-4 border-2 border-white text-white font-semibold rounded-full hover:bg-white hover:text-black transition">
                    View Lookbook
                </button>
            </div>
        </div>

        <!-- Scroll Indicator -->
        <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 text-white animate-bounce">
            <i class="fas fa-chevron-down text-2xl"></i>
        </div>
    </section>

    <!-- Features Bar -->
    <section class="bg-black text-white py-8">
        <div class="max-w-7xl mx-auto px-4 grid grid-cols-2 md:grid-cols-4 gap-6 text-center">
            <div class="flex flex-col items-center">
                <i class="fas fa-truck text-2xl mb-2"></i>
                <span class="text-sm font-medium">Free Shipping Over $100</span>
            </div>
            <div class="flex flex-col items-center">
                <i class="fas fa-undo text-2xl mb-2"></i>
                <span class="text-sm font-medium">30-Day Returns</span>
            </div>
            <div class="flex flex-col items-center">
                <i class="fas fa-shield-alt text-2xl mb-2"></i>
                <span class="text-sm font-medium">Secure Payment</span>
            </div>
            <div class="flex flex-col items-center">
                <i class="fas fa-headset text-2xl mb-2"></i>
                <span class="text-sm font-medium">24/7 Support</span>
            </div>
        </div>
    </section>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16" id="shop">
        
        <!-- Section Header -->
        <div class="text-center mb-12">
            <h2 class="font-serif text-4xl md:text-5xl font-bold mb-4">New Arrivals</h2>
            <p class="text-gray-600 max-w-2xl mx-auto">Explore our latest collection featuring sustainable materials and contemporary designs.</p>
        </div>

        <!-- Filters -->
        <div class="flex flex-wrap justify-center gap-3 mb-12" id="filters">
            <button class="filter-btn active px-6 py-2 rounded-full border border-gray-300 font-medium transition hover:border-black" data-category="all">All</button>
            <button class="filter-btn px-6 py-2 rounded-full border border-gray-300 font-medium transition hover:border-black" data-category="women">Women</button>
            <button class="filter-btn px-6 py-2 rounded-full border border-gray-300 font-medium transition hover:border-black" data-category="men">Men</button>
            <button class="filter-btn px-6 py-2 rounded-full border border-gray-300 font-medium transition hover:border-black" data-category="accessories">Accessories</button>
            <button class="filter-btn px-6 py-2 rounded-full border border-red-300 text-red-600 font-medium transition hover:bg-red-50" data-category="sale">Sale</button>
        </div>

        <!-- Products Grid -->
        <div id="products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
            <!-- Products will be injected here by JavaScript -->
        </div>

        <!-- Load More -->
        <div class="text-center mt-12">
            <button id="load-more" class="px-8 py-3 border-2 border-black text-black font-semibold rounded-full hover:bg-black hover:text-white transition">
                Load More Products
            </button>
        </div>
    </main>

    <!-- Featured Collection -->
    <section class="bg-gray-100 py-20">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid md:grid-cols-2 gap-12 items-center">
                <div class="relative h-[600px] overflow-hidden rounded-2xl group">
                    <img src="https://images.unsplash.com/photo-1558171813-4c088753af8f?w=800&q=80" 
                         alt="Summer Collection" 
                         class="w-full h-full object-cover transition duration-700 group-hover:scale-110">
                    <div class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent"></div>
                    <div class="absolute bottom-8 left-8 text-white">
                        <p class="text-sm uppercase tracking-wider mb-2">Limited Edition</p>
                        <h3 class="font-serif text-3xl font-bold mb-4">Summer Essentials</h3>
                        <button class="px-6 py-3 bg-white text-black rounded-full font-medium hover:bg-gray-100 transition">
                            Explore Collection
                        </button>
                    </div>
                </div>
                <div class="space-y-8">
                    <div>
                        <h3 class="font-serif text-4xl font-bold mb-4">Sustainable Fashion</h3>
                        <p class="text-gray-600 text-lg leading-relaxed">
                            Our commitment to the environment drives every decision we make. From organic cotton to recycled polyester, 
                            each piece in our collection is designed with sustainability in mind without compromising on style.
                        </p>
                    </div>
                    
                    <div class="grid grid-cols-2 gap-6">
                        <div class="bg-white p-6 rounded-xl shadow-sm">
                            <i class="fas fa-leaf text-3xl text-green-600 mb-3"></i>
                            <h4 class="font-bold mb-2">Eco Materials</h4>
                            <p class="text-sm text-gray-600">100% organic and recycled fabrics</p>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-sm">
                            <i class="fas fa-hands-helping text-3xl text-blue-600 mb-3"></i>
                            <h4 class="font-bold mb-2">Ethical Labor</h4>
                            <p class="text-sm text-gray-600">Fair wages and safe conditions</p>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-sm">
                            <i class="fas fa-recycle text-3xl text-purple-600 mb-3"></i>
                            <h4 class="font-bold mb-2">Zero Waste</h4>
                            <p class="text-sm text-gray-600">Circular production process</p>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-sm">
                            <i class="fas fa-globe text-3xl text-teal-600 mb-3"></i>
                            <h4 class="font-bold mb-2">Carbon Neutral</h4>
                            <p class="text-sm text-gray-600">Offset every shipment</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Newsletter -->
    <section class="py-20 bg-black text-white">
        <div class="max-w-4xl mx-auto px-4 text-center">
            <h2 class="font-serif text-4xl md:text-5xl font-bold mb-4">Join the Club</h2>
            <p class="text-gray-400 mb-8 text-lg">Subscribe for exclusive offers, early access to new arrivals, and styling tips.</p>
            <form class="flex flex-col sm:flex-row gap-4 max-w-lg mx-auto" onsubmit="handleSubscribe(event)">
                <input type="email" placeholder="Enter your email" required
                       class="flex-1 px-6 py-4 rounded-full bg-white/10 border border-white/20 text-white placeholder-gray-400 focus:outline-none focus:border-white transition">
                <button type="submit" class="px-8 py-4 bg-white text-black font-semibold rounded-full hover:bg-gray-200 transition">
                    Subscribe
                </button>
            </form>
            <p class="text-sm text-gray-500 mt-4">By subscribing, you agree to our Privacy Policy. Unsubscribe anytime.</p>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-50 pt-16 pb-8 border-t border-gray-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-12">
                <div>
                    <h4 class="font-bold mb-4">Shop</h4>
                    <ul class="space-y-2 text-gray-600">
                        <li><a href="#" class="hover:text-black transition">New Arrivals</a></li>
                        <li><a href="#" class="hover:text-black transition">Women</a></li>
                        <li><a href="#" class="hover:text-black transition">Men</a></li>
                        <li><a href="#" class="hover:text-black transition">Accessories</a></li>
                        <li><a href="#" class="hover:text-black transition">Sale</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-bold mb-4">Help</h4>
                    <ul class="space-y-2 text-gray-600">
                        <li><a href="#" class="hover:text-black transition">Customer Service</a></li>
                        <li><a href="#" class="hover:text-black transition">Track Order</a></li>
                        <li><a href="#" class="hover:text-black transition">Returns</a></li>
                        <li><a href="#" class="hover:text-black transition">Size Guide</a></li>
                        <li><a href="#" class="hover:text-black transition">FAQ</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-bold mb-4">Company</h4>
                    <ul class="space-y-2 text-gray-600">
                        <li><a href="#" class="hover:text-black transition">About Us</a></li>
                        <li><a href="#" class="hover:text-black transition">Careers</a></li>
                        <li><a href="#" class="hover:text-black transition">Press</a></li>
                        <li><a href="#" class="hover:text-black transition">Sustainability</a></li>
                        <li><a href="#" class="hover:text-black transition">Affiliates</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-bold mb-4">Connect</h4>
                    <div class="flex space-x-4 mb-4">
  
