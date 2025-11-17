<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Phantom Essence - Luxury Perfumes</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom font and base styling for a luxurious feel */
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Inter:wght300;400;600&display=swap');
        :root {
            --primary: #5a3e3e; /* Deep Red-Brown */
            --secondary: #d4af37; /* Gold */
            --bg-dark: #1f1d1d; /* Very Dark Background */
            --text-light: #f5f5f5;
        }
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-light);
            line-height: 1.6;
        }
        .header-font {
            font-family: 'Cinzel', serif;
        }
        .btn-primary {
            background-color: var(--secondary);
            color: var(--bg-dark);
            transition: all 0.3s ease;
        }
        .btn-primary:hover {
            opacity: 0.9;
            box-shadow: 0 4px 15px rgba(212, 175, 55, 0.4);
        }
        /* Custom scrollbar for better aesthetics */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #333; }
        ::-webkit-scrollbar-thumb { background: var(--primary); border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--secondary); }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'primary-dark': 'var(--primary)',
                        'gold-accent': 'var(--secondary)',
                        'bg-dark': 'var(--bg-dark)',
                        'text-light': 'var(--text-light)',
                    },
                }
            }
        }
    </script>
</head>
<body class="min-h-screen"><!-- Header & Navigation -->
<header class="bg-primary-dark p-4 shadow-xl sticky top-0 z-10">
    <div class="max-w-7xl mx-auto flex justify-between items-center">
        <h1 class="header-font text-2xl font-bold text-gold-accent tracking-widest">Phantom Essence</h1>
        <button id="cart-button" class="relative p-2 rounded-full hover:bg-[#7a5a5a] transition duration-200">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-text-light" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
            </svg>
            <span id="cart-count" class="absolute top-0 right-0 inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-bg-dark transform translate-x-1/2 -translate-y-1/2 bg-gold-accent rounded-full">0</span>
        </button>
    </div>
</header>

<!-- Main Content Area -->
<main class="p-4 md:p-8 max-w-4xl mx-auto">
    
    <!-- Application Views Container -->
    <div id="app-views">
        <!-- Products View -->
        <section id="products-view" class="view">
            <h2 class="header-font text-3xl md:text-4xl text-center mb-8 text-gold-accent">The Collection</h2>

            <!-- Shipping Policy Banner -->
            <div class="bg-[#333030] p-3 text-center rounded-lg mb-8 shadow-inner">
                <p class="text-sm font-semibold text-text-light">
                    🚚 Free Shipping all over India on orders above <span class="text-gold-accent font-bold">₹999</span>. Orders below ₹999 are charged ₹100.
                </p>
            </div>
            
            <!-- Loading Indicator - Added a prominent border to make it obvious when it's present -->
            <div id="loading-indicator" class="md:col-span-2 text-center py-10 text-gray-400 border border-dashed border-gray-600 rounded-lg">
                Loading products...
            </div>

            <div id="products-grid" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Products will be loaded here from the static JS array -->
            </div>
        </section>
        
        <!-- Checkout/Cart View -->
        <section id="checkout-view" class="view hidden">
            <h2 class="header-font text-3xl text-center mb-6 text-gold-accent">Your Cart & Checkout</h2>
            
            <!-- Dynamic Shipping Message Banner -->
            <div id="checkout-shipping-message" class="bg-[#3c3a3a] p-3 text-center rounded-xl mb-6 shadow-inner text-sm font-semibold">
                <!-- Message injected via JavaScript -->
            </div>
            
            <div id="cart-items-container" class="bg-[#282525] p-4 rounded-xl mb-6 shadow-lg">
                <p id="empty-cart-message" class="text-center text-gray-400">Your cart is empty. Add a fragrance to proceed!</p>
                <div id="cart-list" class="space-y-4">
                    <!-- Cart items will be rendered here -->
                </div>
            </div>

            <div id="checkout-summary" class="bg-[#333030] p-4 rounded-xl mb-6 shadow-lg">
                <h3 class="font-semibold text-xl border-b border-gray-600 pb-2 mb-3">Order Summary</h3>
                <div class="space-y-2 text-sm">
                    <div class="flex justify-between"><span>Subtotal:</span> <span id="subtotal-display">₹0</span></div>
                    <div class="flex justify-between"><span>Shipping:</span> <span id="shipping-display" class="text-gold-accent font-semibold">₹0</span></div>
                    <div class="flex justify-between font-bold text-lg border-t border-gold-accent/50 pt-2 mt-2"><span>Total:</span> <span id="total-display" class="text-gold-accent">₹0</span></div>
                </div>
            </div>
            
            <button id="proceed-to-address" class="btn-primary w-full p-3 text-lg rounded-xl font-bold shadow-md disabled:opacity-50" disabled>
                Proceed to Address
            </button>
            <button onclick="changeView('products-view')" class="text-sm text-gray-400 mt-4 hover:text-text-light transition duration-200">
                ← Continue Shopping
            </button>
        </section>
        
        <!-- Address Gateway View -->
        <section id="address-view" class="view hidden">
            <h2 class="header-font text-3xl text-center mb-6 text-gold-accent">Shipping Address</h2>
            <form id="address-form" class="bg-[#282525] p-6 rounded-xl shadow-2xl space-y-4">
                <input type="text" id="full-name" placeholder="Full Name" required class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                <input type="tel" id="phone-number-input" placeholder="Phone Number" required pattern="[0-9]{10}" title="Must be a 10-digit phone number" class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                <input type="text" id="address-line1" placeholder="Flat, House No., Building, Company" required class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                <input type="text" id="address-line2" placeholder="Area, Street, Sector, Village" class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                <input type="text" id="pincode" placeholder="Pincode" required pattern="[0-9]{6}" title="Must be a 6-digit Pincode" class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                <input type="text" id="city" placeholder="City" required class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                <input type="text" id="state" placeholder="State" required class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                <button type="submit" class="btn-primary w-full p-3 text-lg rounded-xl font-bold mt-6 shadow-md">
                    Continue to Payment
                </button>
            </form>
            <button onclick="changeView('checkout-view')" class="text-sm text-gray-400 mt-4 hover:text-text-light transition duration-200">
                ← Back to Cart
            </button>
        </section>

        <!-- Payment Gateway View -->
        <section id="payment-view" class="view hidden">
            <h2 class="header-font text-3xl text-center mb-6 text-gold-accent">Payment Gateway</h2>
            <div class="bg-[#282525] p-6 rounded-xl shadow-2xl space-y-6">
                <div id="final-total-summary" class="text-center mb-4 p-4 border border-gold-accent rounded-lg">
                    <p class="text-xl">Amount Due: <span id="payment-total-display" class="font-bold text-gold-accent">₹0</span></p>
                </div>

                <!-- Payment Method Selection -->
                <h3 class="font-semibold text-lg text-text-light border-b border-gray-600 pb-2">Choose Payment Method</h3>
                <div class="space-y-3">
                    <label class="block">
                        <input type="radio" name="payment-method" value="upi" checked class="text-gold-accent focus:ring-gold-accent mr-2"> UPI (BHIM, Google Pay, PhonePe, etc.)
                    </label>
                    <label class="block">
                        <input type="radio" name="payment-method" value="card" class="text-gold-accent focus:ring-gold-accent mr-2"> Credit / Debit Card
                    </label>
                </div>

                <!-- UPI/BHIM Section -->
                <div id="upi-section">
                    <h4 class="font-medium text-text-light mt-4 mb-3 border-t border-gray-600 pt-3">Pay via UPI / BHIM</h4>
                    <div class="space-y-3">
                        <button onclick="submitOrder('BHIM/UPI QR')" class="btn-primary w-full p-3 rounded-xl font-bold">Pay with BHIM / UPI App (Simulated)</button>
                        <input type="text" id="upi-id-input" placeholder="Enter UPI ID (e.g., user@bank)" class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                        <button onclick="submitOrder('UPI ID: ' + document.getElementById('upi-id-input').value)" class="btn-primary w-full p-3 rounded-xl font-bold">Pay with Entered UPI ID (Simulated)</button>
                    </div>
                </div>

                <!-- Card Section -->
                <div id="card-section" class="hidden">
                    <h4 class="font-medium text-text-light mt-4 mb-3 border-t border-gray-600 pt-3">Credit / Debit Card</h4>
                    <form id="card-form" class="space-y-3">
                        <input type="text" id="card-number" placeholder="Card Number" required pattern="[0-9\s]{13,19}" title="Enter a valid card number" class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                        <div class="flex space-x-3">
                            <input type="text" id="expiry-date" placeholder="MM/YY" required pattern="(0[1-9]|1[0-2])\/?([0-9]{2})" title="Enter MM/YY format" class="w-1/2 p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                            <input type="text" id="cvv" placeholder="CVV" required pattern="[0-9]{3,4}" title="3 or 4 digits" class="w-1/2 p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
                        </div>
                        <button type="submit" class="btn-primary w-full p-3 rounded-xl font-bold mt-4">Pay Now (Simulated)</button>
                    </form>
                </div>
            </div>
            <button onclick="changeView('address-view')" class="text-sm text-gray-400 mt-4 hover:text-text-light transition duration-200">
                ← Back to Address
            </button>
        </section>

        <!-- Confirmation/Modal Message -->
        <section id="confirmation-view" class="view hidden">
            <div class="bg-[#282525] p-8 rounded-xl shadow-2xl text-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 mx-auto text-gold-accent mb-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                <h2 class="header-font text-3xl text-gold-accent mb-3">Order Confirmed!</h2>
                <p class="text-lg text-text-light">Thank you for your purchase from Phantom Essence.</p>
                <p id="payment-method-message" class="text-sm text-gray-400 mt-2"></p>
                <p class="text-sm text-gray-400 mt-4">Your order will be shipped soon.</p>
                <button onclick="resetApp()" class="btn-primary mt-6 px-6 py-2 rounded-full font-bold">Start New Order</button>
            </div>
        </section>

    </div>
    
    <!-- Feedback Form Section -->
    <section id="feedback-form" class="mt-12 pt-8 border-t border-primary-dark/50">
        <h2 class="header-font text-3xl text-center mb-6 text-gold-accent">Share Your Feedback</h2>
        <form id="feedback-submit-form" class="max-w-md mx-auto bg-[#282525] p-6 rounded-xl shadow-2xl space-y-4">
            <p id="feedback-message" class="hidden text-center p-2 text-sm rounded-lg text-bg-dark bg-gold-accent">Thank you for your feedback!</p>
            <input type="text" placeholder="Your Name (Optional)" class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
            <input type="email" placeholder="Email (Optional)" class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light">
            <textarea placeholder="Your feedback on our perfumes or service..." rows="4" required class="w-full p-3 rounded-lg bg-[#3c3a3a] border border-primary-dark focus:ring-gold-accent focus:border-gold-accent text-text-light"></textarea>
            <button type="submit" class="btn-primary w-full p-3 rounded-xl font-bold">Submit Feedback</button>
        </form>
    </section>

</main>

<!-- Footer -->
<footer class="bg-primary-dark mt-12 p-6 text-center shadow-inner">
    <h3 class="header-font text-xl text-gold-accent mb-3">Connect With Essence</h3>
    <div class="text-sm space-y-1 text-gray-300">
        <p>
            <span class="font-semibold">Instagram:</span>
            <a href="https://instagram.com/phantom_essence" target="_blank" class="hover:text-gold-accent transition duration-200">@phantom_essence</a>
        </p>
        <p>
            <span class="font-semibold">Phone:</span>
            <a href="tel:+919876543210" class="hover:text-gold-accent transition duration-200">+91 98765 43210</a>
        </p>
        <p>
            <span class="font-semibold">Email:</span>
            <a href="mailto:contact@phantomessence.com" class="hover:text-gold-accent transition duration-200">contact@phantomessence.com</a>
        </p>
    </div>
    <p class="text-xs text-gray-500 mt-4">&copy; 2024 Phantom Essence. All rights reserved.</p>
</footer>

<!-- Firebase Script Includes (Optional - safe to include, ignores if running elsewhere) -->
<script type="module">
    // This entire module is optional for product viewing/basic cart functionality,
    // but enables persistence if run in a Firebase environment.
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
    import { getFirestore, doc, onSnapshot, setLogLevel, setDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

    // Set log level for debugging
    setLogLevel('Debug');
    
    // --- Global Firebase Variables ---
    let app, db, auth;
    let userId = null;
    let unsubscribeCart = null;

    // NOTE: If running outside of the Canvas environment, this placeholder config prevents errors.
    const PLACEHOLDER_FIREBASE_CONFIG = {
        apiKey: "AIzaSyC_PLACEHOLDER_FOR_YOUR_API_KEY",
        projectId: "your-project-id",
    };
    
    // Variables provided by the Canvas environment or fallbacks
    const APP_ID = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
    const FIREBASE_CONFIG = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : JSON.stringify(PLACEHOLDER_FIREBASE_CONFIG));
    const INITIAL_AUTH_TOKEN = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

    /**
     * Initializes Firebase and authenticates the user.
     */
    async function initializeFirebase() {
        // Guard clause to prevent initialization if config is clearly invalid/placeholder
        if (!FIREBASE_CONFIG || !FIREBASE_CONFIG.projectId || FIREBASE_CONFIG.projectId === 'your-project-id') {
            console.warn("Firebase config is placeholder. Cart persistence and Feedback saving will NOT work.");
            return;
        }

        try {
            app = initializeApp(FIREBASE_CONFIG);
            db = getFirestore(app);
            auth = getAuth(app);
            
            // Use custom token for sign-in if available, otherwise sign in anonymously
            if (INITIAL_AUTH_TOKEN) {
                await signInWithCustomToken(auth, INITIAL_AUTH_TOKEN);
            } else {
                await signInAnonymously(auth);
            }

            // Check the initial state and load data
            onAuthStateChanged(auth, (user) => {
                if (user) {
                    userId = user.uid;
                    console.log("Firebase initialized and authenticated. User ID:", userId);
                    listenToUserCart(userId);
                } else {
                    userId = crypto.randomUUID(); 
                    console.log("User signed out or failed to authenticate. Persistence disabled.");
                }
            });
            
        } catch (error) {
            console.error("Error initializing Firebase or signing in:", error);
        }
    }

    /**
     * Private Data Path: /artifacts/{appId}/users/{userId}/cart/items
     */
    function getUserCartDocRef(uid) {
        return doc(db, 'artifacts', APP_ID, 'users', uid, 'cart', 'items');
    }
    
    /**
     * Fetches and listens to the user's cart data.
     */
    function listenToUserCart(uid) {
        if (!db) return;

        if (unsubscribeCart) {
            unsubscribeCart(); 
        }
        
        const cartDocRef = getUserCartDocRef(uid);

        unsubscribeCart = onSnapshot(cartDocRef, (docSnapshot) => {
            if (docSnapshot.exists()) {
                const data = docSnapshot.data();
                try {
                    // Crucial: Update the global window.appCart object
                    window.appCart = JSON.parse(data.itemsJson || '[]'); 
                    window.updateCartUI(); 
                    console.log("Cart loaded from Firestore.");
                } catch(e) {
                    console.error("Error parsing cart data from Firestore:", e);
                }
            } else {
                window.appCart = [];
                window.updateCartUI();
                window.saveCart(); 
            }
        }, (error) => {
            console.error("Error listening to user cart:", error);
        });
    }
    
    /**
     * Saves the current cart state to Firestore.
     */
    window.saveCart = async function() {
        if (!db || !userId) {
            // If not running in a Firebase environment, this fails silently but the app still works locally.
            return;
        }

        try {
            const cartDocRef = getUserCartDocRef(userId);
            const cartData = {
                itemsJson: JSON.stringify(window.appCart),
                updatedAt: new Date().toISOString()
            };
            
            await setDoc(cartDocRef, cartData, { merge: true });
            console.log("Cart saved to Firestore.");
        } catch (e) {
            console.error("Error saving cart:", e);
        }
    }

    // --- Initialize Firebase on Load ---
    window.addEventListener('load', initializeFirebase);
</script>

<script>
    // --- Static Product Data (Ensures portability) ---
    const STATIC_PRODUCTS = [
        { id: 'Markd-30ml', name: 'Markd (30ml)', description: 'The Signature Scent', price: 450, size: '30ml', available: true, shortName: 'Markd' },
        { id: 'Markd-100ml', name: 'Markd (100ml)', description: 'The Signature Scent', price: 1199, size: '100ml', available: true, shortName: 'Markd' },
        { id: 'Cavo-30ml', name: 'Cavo (30ml)', description: 'Mysterious & Deep', price: 450, size: '30ml', available: true, shortName: 'Cavo' },
        { id: 'Cavo-100ml', name: 'Cavo (100ml)', description: 'Mysterious & Deep (Unavailable)', price: 1299, size: '100ml', available: false, shortName: 'Cavo' },
        { id: 'Omen-30ml', name: 'Omen (30ml)', description: 'Bold & Intense', price: 450, size: '30ml', available: true, shortName: 'Omen' },
        { id: 'Omen-100ml', name: 'Omen (100ml)', description: 'Bold & Intense (Unavailable)', price: 1299, size: '100ml', available: false, shortName: 'Omen' },
        { id: 'Kazza-30ml', name: 'Kazza (30ml)', description: 'Fresh & Energetic', price: 450, size: '30ml', available: true, shortName: 'Kazza' },
        { id: 'Kazza-100ml', name: 'Kazza (100ml)', description: 'Fresh & Energetic (Unavailable)', price: 1299, size: '100ml', available: false, shortName: 'Kazza' },
    ];


    // --- Global State & Constants ---
    // 'appCart' holds the local, running cart state.
    let appCart = []; 
    const SHIPPING_THRESHOLD = 999;
    const SHIPPING_COST = 100;
    let currentView = 'products-view';

    // --- Utility Functions ---

    /**
     * Renders the products grid based on the static data.
     */
    function renderProducts() {
        try {
            const grid = document.getElementById('products-grid');
            const loadingIndicator = document.getElementById('loading-indicator');
            
            // 1. Clear existing content
            grid.innerHTML = ''; 
            
            const uniqueProducts = {};

            // 2. Group products by short name
            STATIC_PRODUCTS.forEach(p => {
                if (!uniqueProducts[p.shortName]) {
                    uniqueProducts[p.shortName] = {
                        shortName: p.shortName,
                        description: p.description,
                        variants: []
                    };
                }
                uniqueProducts[p.shortName].variants.push(p);
            });

            // 3. Convert uniqueProducts object to an array for sorting
            let productArray = Object.values(uniqueProducts);

            // 4. Sort the array: Place 'Markd' at the beginning
            productArray.sort((a, b) => {
                if (a.shortName === 'Markd') return -1;
                if (b.shortName === 'Markd') return 1;
                return 0;
            });

            // 5. Generate HTML for each unique product card from the sorted array
            productArray.forEach(product => {
                const variantHTML = product.variants.map(variant => {
                    const buttonClass = variant.available ? 'btn-primary' : 'bg-gray-500 text-primary-dark opacity-50 cursor-not-allowed';
                    const buttonText = variant.available ? 'Add to Cart' : 'Coming Soon';
                    // We use the local addToCart function which is safe.
                    const buttonAction = variant.available ? `addToCart({id: '${variant.id}', name: '${variant.name}', price: ${variant.price}})` : '';
                    const displayPrice = variant.available ? `₹${variant.price.toFixed(0)}` : 'N/A';
                    
                    return `
                        <div class="flex justify-between items-center bg-[#3c3a3a] p-3 rounded-lg ${variant.available ? '' : 'opacity-50 cursor-not-allowed'}">
                            <span class="font-semibold text-lg text-gold-accent">${variant.size}</span>
                            <span class="text-text-light font-medium">${displayPrice}</span>
                            <button onclick="${buttonAction}" class="${buttonClass} px-3 py-1 text-sm rounded-full font-semibold" ${variant.available ? '' : 'disabled'}>${buttonText}</button>
                        </div>
                    `;
                }).join('');

                const cardHTML = `
                    <div id="${product.shortName.toLowerCase()}-card" class="product-card bg-[#282525] p-6 rounded-xl shadow-2xl border-2 border-primary-dark transition duration-300 hover:border-gold-accent/50">
                        <div class="flex flex-col items-center">
                            <h3 class="header-font text-2xl font-bold mb-2 text-text-light">${product.shortName}</h3>
                            <p class="text-xs italic text-gray-400 mb-4">${product.description}</p>
                            <div class="w-full space-y-3">
                                ${variantHTML}
                            </div>
                        </div>
                    </div>
                `;
                grid.insertAdjacentHTML('beforeend', cardHTML);
            });
            
            // CRITICAL FIX: Hide loading indicator *after* products are rendered
            if (loadingIndicator) {
                loadingIndicator.classList.add('hidden');
            }
            
            // Fallback for missing data
            if (grid.children.length === 0) {
                if (loadingIndicator) {
                    loadingIndicator.classList.remove('hidden'); // Show if no products rendered
                    loadingIndicator.textContent = 'Error: No products found in static list.';
                }
            }
        } catch (e) {
            console.error("Error rendering products:", e);
            // Show a detailed error message if rendering fails
            const loadingIndicator = document.getElementById('loading-indicator');
            if (loadingIndicator) {
                loadingIndicator.classList.remove('hidden');
                loadingIndicator.textContent = 'Failed to load product layout due to a JavaScript error. Check console for details.';
            }
        }
    }

    /**
     * Switches the active view/section of the application.
     * @param {string} viewId - The ID of the view to show (e.g., 'products-view').
     */
    function changeView(viewId) {
        document.querySelectorAll('.view').forEach(view => {
            view.classList.add('hidden');
        });
        document.getElementById(viewId).classList.remove('hidden');
        currentView = viewId;
        window.scrollTo(0, 0); // Scroll to top on view change
    }

    /**
     * Resets the entire application state and navigates back to the product view.
     */
    function resetApp() {
        appCart = [];
        if (typeof window.saveCart === 'function') {
            window.saveCart(); // Attempt to save empty cart to persistence layer (if available)
        }
        updateCartUI();
        changeView('products-view');
        // Reset forms
        document.getElementById('address-form').reset();
        document.getElementById('card-form').reset();
    }

    /**
     * Calculates subtotal, shipping, and grand total.
     */
    function calculateTotals() {
        const subtotal = appCart.reduce((sum, item) => sum + item.price * item.quantity, 0);
        const shipping = subtotal >= SHIPPING_THRESHOLD ? 0 : SHIPPING_COST;
        const total = subtotal + shipping;
        return { subtotal, shipping, total };
    }

    /**
     * Updates all cart displays and the proceed button state, including the dynamic shipping message.
     */
    function updateCartUI() {
        
        // Check if Firebase has loaded an external cart, otherwise use the local one
        if (typeof window.appCart !== 'undefined') {
            appCart = window.appCart; 
        }

        const { subtotal, shipping, total } = calculateTotals();
        const cartList = document.getElementById('cart-list');
        const cartCount = document.getElementById('cart-count');
        const emptyMessage = document.getElementById('empty-cart-message');
        const proceedButton = document.getElementById('proceed-to-address');
        const checkoutMessageBanner = document.getElementById('checkout-shipping-message');

        cartCount.textContent = appCart.reduce((count, item) => count + item.quantity, 0);
        cartList.innerHTML = '';
        
        if (appCart.length === 0) {
            emptyMessage.classList.remove('hidden');
            proceedButton.disabled = true;
            checkoutMessageBanner.innerHTML = 'Add items to your cart to check shipping details.';
            checkoutMessageBanner.classList.add('bg-[#3c3a3a]');
            checkoutMessageBanner.classList.remove('bg-primary-dark', 'text-gold-accent');
        } else {
            emptyMessage.classList.add('hidden');
            proceedButton.disabled = false;
            
            // Update the dynamic shipping message based on subtotal
            if (subtotal >= SHIPPING_THRESHOLD) {
                checkoutMessageBanner.innerHTML = '🎉 <span class="text-gold-accent">Congratulations!</span> You qualify for **FREE Shipping**.';
                checkoutMessageBanner.classList.remove('bg-[#3c3a3a]');
                checkoutMessageBanner.classList.add('bg-primary-dark', 'text-gold-accent'); // Highlight success
            } else {
                const amountNeeded = SHIPPING_THRESHOLD - subtotal;
                const amountDisplay = Math.ceil(amountNeeded);
                checkoutMessageBanner.innerHTML = `⚠️ Spend **₹${amountDisplay}** more to get **FREE Shipping**!`;
                checkoutMessageBanner.classList.add('bg-[#3c3a3a]');
                checkoutMessageBanner.classList.remove('bg-primary-dark', 'text-gold-accent');
            }

            // Render cart items
            appCart.forEach(item => {
                const itemElement = document.createElement('div');
                itemElement.className = 'flex justify-between items-center p-2 border-b border-gray-700 last:border-b-0';
                itemElement.innerHTML = `
                    <div class="flex-1">
                        <span class="font-medium text-text-light">${item.name}</span>
                        <span class="block text-xs text-gray-400">₹${item.price.toFixed(0)} x ${item.quantity}</span>
                    </div>
                    <div class="flex items-center space-x-2">
                        <span class="font-semibold text-gold-accent">₹${(item.price * item.quantity).toFixed(0)}</span>
                        <button onclick="updateItemQuantity('${item.id}')" class="text-red-400 hover:text-red-500 transition duration-200">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM7 9a1 1 0 000 2h6a1 1 0 100-2H7z" clip-rule="evenodd" />
                            </svg>
                        </button>
                    </div>
                `;
                cartList.appendChild(itemElement);
            });
        }

        // Update summary displays (using toFixed(0) for clean INR display)
        document.getElementById('subtotal-display').textContent = `₹${subtotal.toFixed(0)}`;
        document.getElementById('shipping-display').textContent = shipping === 0 ? 'FREE' : `₹${shipping.toFixed(0)}`;
        document.getElementById('total-display').textContent = `₹${total.toFixed(0)}`;
        document.getElementById('payment-total-display').textContent = `₹${total.toFixed(0)}`;
    }


    // --- Cart Operations ---
    
    /**
     * Adds an item to the cart or increments its quantity.
     * @param {object} product - {id, name, price}
     */
    function addToCart(product) {
        const existingItem = appCart.find(item => item.id === product.id);
        if (existingItem) {
            existingItem.quantity += 1;
        } else {
            appCart.push({ ...product, quantity: 1 });
        }
        
        if (typeof window.saveCart === 'function') {
            window.saveCart(); // Save change to persistence (if available)
        }
        updateCartUI(); 
    }

    /**
     * Decrements the quantity of an item by 1, or removes it completely if quantity is 1.
     * @param {string} id - The ID of the item to update.
     */
    function updateItemQuantity(id) {
        const itemIndex = appCart.findIndex(item => item.id === id);

        if (itemIndex > -1) {
            if (appCart[itemIndex].quantity > 1) {
                // Decrement quantity if more than 1
                appCart[itemIndex].quantity -= 1;
            } else {
                // Remove completely if quantity is 1
                appCart.splice(itemIndex, 1);
            }
        }

        if (typeof window.saveCart === 'function') {
            window.saveCart(); // Save change to persistence (if available)
        }
        updateCartUI();
    }

    // --- Event Listeners & Flow Control ---

    document.addEventListener('DOMContentLoaded', () => {
        // FIX: Use setTimeout(0) to run renderProducts AFTER all initial DOM/script loading tasks are finished.
        // This prevents a race condition where other scripts might briefly clear content.
        setTimeout(() => {
            renderProducts(); 
            updateCartUI(); 
        }, 0); 
        
        // Cart Button opens Checkout View and ensures UI is updated
        document.getElementById('cart-button').addEventListener('click', () => {
            updateCartUI(); 
            changeView('checkout-view');
        });
        
        // Proceed to Address Button
        document.getElementById('proceed-to-address').addEventListener('click', () => {
            if (appCart.length > 0) {
                changeView('address-view');
            }
        });

        // Address Form Submission
        document.getElementById('address-form').addEventListener('submit', (e) => {
            e.preventDefault();
            changeView('payment-view');
        });

        // Payment Method Switcher
        document.querySelectorAll('input[name="payment-method"]').forEach(radio => {
            radio.addEventListener('change', (e) => {
                const isCard = e.target.value === 'card';
                document.getElementById('upi-section').classList.toggle('hidden', isCard);
                document.getElementById('card-section').classList.toggle('hidden', !isCard);
            });
        });

        // Card Form Submission (Simulated)
        document.getElementById('card-form').addEventListener('submit', (e) => {
            e.preventDefault();
            submitOrder('Card (****' + document.getElementById('card-number').value.slice(-4) + ')');
        });
        
        // Feedback Form Submission (Simulated)
        document.getElementById('feedback-submit-form').addEventListener('submit', (e) => {
            e.preventDefault();
            document.getElementById('feedback-message').classList.remove('hidden');
            document.getElementById('feedback-submit-form').reset();
            
            // Hide confirmation after a delay
            setTimeout(() => {
                document.getElementById('feedback-message').classList.add('hidden');
            }, 3000);
        });

    });

    /**
     * Finalizes the order and shows the confirmation screen. (Simulated)
     * @param {string} method - The payment method used.
     */
    function submitOrder(method) {
        console.log("Order Placed. Cart:", appCart, "Method:", method);
        document.getElementById('payment-method-message').textContent = `Payment Method: ${method}`;
        
        // Clear cart and save to Firebase upon simulated order
        resetApp(); 
        
        changeView('confirmation-view');
    }

    // --- Make Functions Globally Accessible for HTML OnClick Events ---
    window.addToCart = addToCart;
    window.updateItemQuantity = updateItemQuantity;
    window.updateCartUI = updateCartUI; 
    window.changeView = changeView;
    window.resetApp = resetApp;
    window.submitOrder = submitOrder;
    // Expose cart globally for Firebase script access
    window.appCart = appCart;
</script>

</body>
</html>
