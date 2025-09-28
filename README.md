<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Compra Boa JF - Compare preços em tempo real e economize em Juiz de Fora</title>
    <meta name="description" content="Compare preços dos supermercados de Juiz de Fora em tempo real. Otimização de rotas, carrinho inteligente e economia garantida.">
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    
    <!-- EmailJS -->
    <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
    <style>
        .gradient-bg {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 50%, #ec4899 100%);
        }
        
        .gradient-text {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 50%, #ec4899 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .glass-effect {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }
        
        .premium-glass {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(30px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }
        
        .premium-button {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 50%, #ec4899 100%);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
        }
        
        .premium-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: left 0.6s;
        }
        
        .premium-button:hover::before {
            left: 100%;
        }
        
        .premium-button:hover {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 15px 35px rgba(79, 70, 229, 0.4);
        }
        
        .fade-in {
            animation: fadeIn 0.8s ease-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .page-section {
            display: none;
        }
        
        .page-section.active {
            display: block;
        }
        
        .nav-link.active {
            color: #667eea;
            font-weight: 600;
        }
        
        .floating-card {
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        
        .hero-pattern {
            background-image: 
                radial-gradient(circle at 25px 25px, rgba(255,255,255,.15) 2px, transparent 0), 
                radial-gradient(circle at 75px 75px, rgba(255,255,255,.15) 2px, transparent 0);
            background-size: 100px 100px;
            position: relative;
        }
        
        .hero-pattern::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, transparent 30%, rgba(79, 70, 229, 0.1) 50%, transparent 70%);
            animation: shimmer 3s ease-in-out infinite;
        }
        
        @keyframes shimmer {
            0%, 100% { transform: translateX(-100%); }
            50% { transform: translateX(100%); }
        }
        
        .interactive-map {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.1;
            pointer-events: none;
            z-index: 1;
        }
        
        .search-pulse {
            position: absolute;
            width: 4px;
            height: 4px;
            background: #4f46e5;
            border-radius: 50%;
            box-shadow: 0 0 10px #4f46e5;
            animation: searchPulse 2s ease-in-out infinite;
        }
        
        @keyframes searchPulse {
            0%, 100% { 
                transform: scale(1);
                opacity: 1;
            }
            50% { 
                transform: scale(2);
                opacity: 0.5;
            }
        }
        
        .search-line {
            position: absolute;
            height: 2px;
            background: linear-gradient(90deg, transparent, #4f46e5, transparent);
            animation: searchLine 3s ease-in-out infinite;
        }
        
        @keyframes searchLine {
            0% { 
                width: 0;
                opacity: 0;
            }
            50% { 
                width: 100px;
                opacity: 1;
            }
            100% { 
                width: 0;
                opacity: 0;
            }
        }
        
        .neon-glow {
            box-shadow: 
                0 0 5px rgba(79, 70, 229, 0.3),
                0 0 10px rgba(79, 70, 229, 0.2),
                0 0 15px rgba(79, 70, 229, 0.1);
        }
        
        .cyber-border {
            position: relative;
            border: 1px solid transparent;
            background: linear-gradient(white, white) padding-box,
                        linear-gradient(135deg, #4f46e5, #7c3aed, #ec4899) border-box;
        }
        
        .holographic {
            background: linear-gradient(45deg, 
                rgba(79, 70, 229, 0.1) 0%,
                rgba(124, 58, 237, 0.1) 25%,
                rgba(236, 72, 153, 0.1) 50%,
                rgba(79, 70, 229, 0.1) 75%,
                rgba(124, 58, 237, 0.1) 100%);
            background-size: 400% 400%;
            animation: holographicShift 4s ease-in-out infinite;
        }
        
        @keyframes holographicShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .modal.active {
            display: flex;
        }

        .comparison-interface {
            display: none;
        }

        .comparison-interface.active {
            display: block;
        }

        .cart-item {
            transition: all 0.3s ease;
        }

        .cart-item:hover {
            transform: translateX(5px);
        }

        .category-card:hover {
            transform: translateY(-5px);
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1100;
            transform: translateX(400px);
            transition: transform 0.3s ease;
        }

        .notification.show {
            transform: translateX(0);
        }

        .loading-spinner {
            border: 3px solid #f3f3f4;
            border-top: 3px solid #667eea;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .stats-counter {
            font-variant-numeric: tabular-nums;
        }

        .plan-option.selected {
            border-color: #667eea;
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
        }

        .payment-option.selected {
            border-color: #10b981;
            background: rgba(16, 185, 129, 0.1);
        }
    </style>
</head>
<body class="bg-gradient-to-br from-slate-50 to-indigo-100 min-h-screen">
    <!-- Notification System -->
    <div id="notification" class="notification bg-white rounded-lg shadow-lg p-4 max-w-sm">
        <div class="flex items-center space-x-3">
            <div id="notificationIcon" class="w-8 h-8 rounded-full flex items-center justify-center">
                <!-- Icon will be inserted here -->
            </div>
            <div>
                <div id="notificationTitle" class="font-semibold text-gray-800"></div>
                <div id="notificationMessage" class="text-sm text-gray-600"></div>
            </div>
        </div>
    </div>

    <!-- Header -->
    <header class="premium-glass sticky top-0 z-40 border-b border-white/20">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center py-4">
                <!-- Logo -->
                <div class="flex items-center space-x-3">
                    <div class="w-12 h-12 premium-button rounded-xl flex items-center justify-center">
                        <svg class="w-8 h-8 text-white" viewBox="0 0 32 32" fill="none">
                            <!-- Modern Shopping Cart with Tech Elements -->
                            <!-- Cart Base -->
                            <path d="M6 8L8.5 8.5L10.5 20.5C10.7 21.3 11.4 22 12.2 22H24C24.8 22 25.5 21.3 25.7 20.5L27 14H11" 
                                  stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                            
                            <!-- Tech Grid Pattern in Cart -->
                            <path d="M13 16H15M17 16H19M21 16H23M13 18H15M17 18H19M21 18H23" 
                                  stroke="currentColor" stroke-width="1" stroke-linecap="round" opacity="0.6"/>
                            
                            <!-- Digital Handle -->
                            <path d="M27 14C27.5 14 28 13.5 28 13V11C28 10.5 27.5 10 27 10H26" 
                                  stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                            
                            <!-- Wheels with Tech Design -->
                            <circle cx="14" cy="26" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
                            <circle cx="22" cy="26" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
                            
                            <!-- Tech Dots in Wheels -->
                            <circle cx="14" cy="26" r="0.5" fill="currentColor"/>
                            <circle cx="22" cy="26" r="0.5" fill="currentColor"/>
                            
                            <!-- Digital Signal Lines -->
                            <path d="M4 6L6 8M4 8L6 6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" opacity="0.7"/>
                            
                            <!-- Smart Badge -->
                            <circle cx="24" cy="8" r="3" fill="currentColor" opacity="0.9"/>
                            <path d="M22.5 8L23.5 9L25.5 7" stroke="white" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
                        </svg>
                    </div>
                    <div>
                        <h1 class="text-xl font-bold text-slate-800">Compra Boa JF</h1>
                        <p class="text-xs text-slate-600">Juiz de Fora</p>
                    </div>
                </div>

                <!-- Navigation Menu -->
                <nav class="hidden lg:flex items-center space-x-8">
                    <a href="#" onclick="showPage('home')" class="nav-link text-slate-700 hover:text-indigo-600 font-semibold transition-all duration-300 active">Início</a>
                    <a href="#" onclick="showPage('como-funciona')" class="nav-link text-slate-700 hover:text-indigo-600 font-semibold transition-all duration-300">Como Funciona</a>
                    <a href="#" onclick="showPage('assinatura')" class="nav-link text-slate-700 hover:text-indigo-600 font-semibold transition-all duration-300">Assinatura</a>
                    <a href="#" onclick="showPage('parceiros')" class="nav-link text-slate-700 hover:text-indigo-600 font-semibold transition-all duration-300">Parceiros</a>
                    <a href="#" onclick="showPage('contato')" class="nav-link text-slate-700 hover:text-indigo-600 font-semibold transition-all duration-300">Contato</a>
                    <a href="#" onclick="showPage('minha-conta')" id="minhaContaLink" class="nav-link text-slate-700 hover:text-indigo-600 font-semibold transition-all duration-300 hidden">Minha Conta</a>
                    
                    <!-- User Account Section -->
                    <div id="userSection" class="flex items-center space-x-3">
                        <!-- Not Logged In -->
                        <div id="notLoggedIn" class="flex items-center space-x-3">
                            <button onclick="showLoginModal()" class="text-slate-700 hover:text-indigo-600 font-semibold transition-all duration-300">
                                Entrar
                            </button>
                            <button onclick="showSignupModal()" class="premium-button text-white px-6 py-2 rounded-lg font-semibold text-sm">
                                Criar Conta
                            </button>
                        </div>
                        
                        <!-- Logged In -->
                        <div id="loggedIn" class="hidden flex items-center space-x-3">
                            <!-- Cart Icon - ALWAYS VISIBLE WHEN LOGGED IN -->
                            <div class="relative">
                                <button onclick="toggleCart()" class="bg-white border-2 border-gray-200 hover:border-indigo-300 rounded-xl p-3 transition-all duration-300 hover:shadow-lg relative group">
                                    <svg class="w-6 h-6 text-slate-700 hover:text-indigo-600 transition-colors" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4m0 0L7 13m0 0l-1.5 6M7 13l-1.5 6m0 0h9m-9 0V19a2 2 0 002 2h6a2 2 0 002-2v-1M9 19v2m6-2v2"/>
                                    </svg>
                                    <span id="cartCount" class="absolute -top-2 -right-2 bg-red-500 text-white text-xs rounded-full w-6 h-6 flex items-center justify-center font-bold shadow-lg">0</span>
                                    
                                    <!-- Tooltip -->
                                    <div class="absolute bottom-full right-0 mb-2 px-3 py-2 bg-gray-800 text-white text-xs rounded-lg opacity-0 group-hover:opacity-100 transition-opacity whitespace-nowrap shadow-lg">
                                        Carrinho de Compras
                                        <div class="absolute top-full right-3 w-0 h-0 border-l-4 border-r-4 border-t-4 border-transparent border-t-gray-800"></div>
                                    </div>
                                </button>
                            </div>
                            
                            <div class="relative group">
                                <button class="flex items-center space-x-2 text-slate-700 hover:text-indigo-600 font-semibold">
                                    <div class="w-8 h-8 bg-indigo-100 rounded-full flex items-center justify-center">
                                        <span id="userInitials" class="text-indigo-600 font-bold text-sm">U</span>
                                    </div>
                                    <span id="userName">Usuário</span>
                                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
                                    </svg>
                                </button>
                                <div class="absolute right-0 mt-2 w-48 premium-glass rounded-xl shadow-2xl opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-300 z-50">
                                    <div class="p-2">
                                        <div class="px-4 py-2 text-sm text-slate-600 border-b border-gray-200">
                                            <div>Plano: <span id="userPlan" class="font-semibold">Básico</span></div>
                                            <div class="text-xs text-gray-500">Economia: <span id="userSavings" class="font-semibold text-green-600">R$ 0,00</span></div>
                                        </div>
                                        <button onclick="showPage('dashboard')" class="block w-full text-left px-4 py-2 text-sm text-slate-700 hover:bg-white/50 rounded-lg transition-colors">Dashboard</button>
                                        <button onclick="showPage('historico')" class="block w-full text-left px-4 py-2 text-sm text-slate-700 hover:bg-white/50 rounded-lg transition-colors">Histórico</button>
                                        <button onclick="logout()" class="block w-full text-left px-4 py-2 text-sm text-slate-700 hover:bg-white/50 rounded-lg transition-colors">Sair</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </nav>

                <!-- Mobile Menu Button -->
                <button class="lg:hidden text-gray-600 hover:text-gray-900" onclick="toggleMobileMenu()">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
                    </svg>
                </button>
            </div>

            <!-- Mobile Menu -->
            <div id="mobileMenu" class="hidden lg:hidden mt-4 pb-4 border-t border-gray-200">
                <div class="flex flex-col space-y-2 mt-4">
                    <a href="#" onclick="showPage('home')" class="text-gray-700 hover:text-blue-600 font-medium py-2">Início</a>
                    <a href="#" onclick="showPage('como-funciona')" class="text-gray-700 hover:text-blue-600 font-medium py-2">Como Funciona</a>
                    <a href="#" onclick="showPage('assinatura')" class="text-gray-700 hover:text-blue-600 font-medium py-2">Assinatura</a>
                    <a href="#" onclick="showPage('parceiros')" class="text-gray-700 hover:text-blue-600 font-medium py-2">Parceiros</a>
                    <a href="#" onclick="showPage('contato')" class="text-gray-700 hover:text-blue-600 font-medium py-2">Contato</a>
                </div>
            </div>
        </div>
    </header>

    <!-- Shopping Cart Sidebar -->
    <div id="cartSidebar" class="fixed right-0 top-0 h-full w-96 bg-white shadow-2xl transform translate-x-full transition-transform duration-300 z-50">
        <div class="p-6 border-b border-gray-200">
            <div class="flex items-center justify-between">
                <h3 class="text-xl font-bold text-gray-800">Meu Carrinho</h3>
                <button onclick="toggleCart()" class="text-gray-500 hover:text-gray-700">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                    </svg>
                </button>
            </div>
        </div>
        
        <div id="cartItems" class="flex-1 overflow-y-auto p-6">
            <div id="emptyCart" class="text-center py-12">
                <svg class="w-16 h-16 text-gray-300 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4m0 0L7 13m0 0l-1.5 6M7 13l-1.5 6m0 0h9m-9 0V19a2 2 0 002 2h6a2 2 0 002-2v-1M9 19v2m6-2v2"/>
                </svg>
                <p class="text-gray-500">Seu carrinho está vazio</p>
                <p class="text-sm text-gray-400 mt-2">Adicione produtos para começar suas compras</p>
            </div>
            <div id="cartItemsList" class="space-y-4 hidden">
                <!-- Cart items will be populated here -->
            </div>
        </div>
        
        <div id="cartFooter" class="hidden border-t border-gray-200 p-6">
            <div class="space-y-4">
                <div class="flex justify-between items-center text-lg font-semibold">
                    <span>Total:</span>
                    <span id="cartTotal" class="text-green-600">R$ 0,00</span>
                </div>
                <div class="text-sm text-gray-600">
                    <span>Economia estimada: </span>
                    <span id="cartSavings" class="font-semibold text-green-600">R$ 0,00</span>
                </div>

                
                <button onclick="optimizeRoute()" class="w-full premium-button text-white py-3 rounded-lg font-semibold mb-2">
                    <svg class="w-5 h-5 inline mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-1.447-.894L15 4m0 13V4m0 0L9 7"/>
                    </svg>
                    Otimizar Rota de Compras
                </button>
                <button onclick="clearCart()" class="w-full bg-gray-200 text-gray-700 py-2 rounded-lg font-semibold text-sm hover:bg-gray-300 transition-colors">
                    Limpar Carrinho
                </button>
            </div>
        </div>
    </div>

    <!-- HOME PAGE -->
    <div id="home" class="page-section active">
        <!-- Hero Section -->
        <section class="relative overflow-hidden hero-pattern">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
                <div class="text-center fade-in">
                    <h1 class="text-5xl md:text-7xl font-bold text-slate-800 mb-8 leading-tight">
                        Compare preços em tempo real,
                        <span class="gradient-text block">economize tempo e dinheiro</span>
                    </h1>
                    <p class="text-xl md:text-2xl text-slate-600 mb-12 max-w-4xl mx-auto leading-relaxed">
                        Comparação inteligente, otimização de rotas e estratégias perfeitas para suas compras em Juiz de Fora. 
                        Economize de verdade com nossa tecnologia avançada.
                    </p>
                    
                    <div class="flex flex-col sm:flex-row gap-6 justify-center items-center mb-16">
                        <button onclick="startComparison()" class="premium-button text-white px-8 py-4 rounded-xl font-semibold text-lg shadow-lg hover:shadow-xl transition-all duration-300">
                            <svg class="w-6 h-6 inline mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
                            </svg>
                            Começar a Comparar
                        </button>
                        <button onclick="showPage('assinatura')" class="bg-white text-slate-700 px-8 py-4 rounded-xl font-semibold text-lg border-2 border-slate-200 hover:border-indigo-300 transition-all duration-300">
                            <svg class="w-6 h-6 inline mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
                            </svg>
                            Ver Planos
                        </button>
                    </div>

                    <!-- Stats -->
                    <div class="grid grid-cols-2 md:grid-cols-3 gap-8 max-w-4xl mx-auto">
                        <div class="premium-glass rounded-2xl p-6 text-center">
                            <div class="text-3xl font-bold gradient-text mb-2 stats-counter" data-target="70">70+</div>
                            <div class="text-slate-600 font-medium">Supermercados</div>
                        </div>
                        <div class="premium-glass rounded-2xl p-6 text-center">
                            <div class="text-3xl font-bold gradient-text mb-2 stats-counter" data-target="10000">10.000+</div>
                            <div class="text-slate-600 font-medium">Produtos</div>
                        </div>
                        <div class="premium-glass rounded-2xl p-6 text-center md:col-span-1 col-span-2">
                            <div class="text-3xl font-bold gradient-text mb-2">24h</div>
                            <div class="text-slate-600 font-medium">Atualização</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Features Section -->
        <section class="py-20 bg-white">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center mb-16">
                    <h2 class="text-4xl md:text-5xl font-bold text-slate-800 mb-6">
                        Por que escolher o 
                        <span class="gradient-text">Compra Boa JF?</span>
                    </h2>
                    <p class="text-xl text-slate-600 max-w-3xl mx-auto">
                        Tecnologia avançada desenvolvida especialmente para Juiz de Fora
                    </p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <div class="premium-glass rounded-2xl p-8 text-center hover:scale-105 transition-transform duration-300">
                        <div class="w-16 h-16 premium-button rounded-2xl flex items-center justify-center mx-auto mb-6">
                            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 3v2m6-2v2M9 19v2m6-2v2M5 9H3m2 6H3m18-6h-2m2 6h-2M7 19h10a2 2 0 002-2V7a2 2 0 00-2-2H7a2 2 0 00-2 2v10a2 2 0 002 2zM9 9h6v6H9V9z"/>
                            </svg>
                        </div>
                        <h3 class="text-2xl font-bold text-slate-800 mb-4">Comparação Inteligente</h3>
                        <p class="text-slate-600 leading-relaxed">
                            IA avançada que analisa preços, promoções e qualidade dos produtos em tempo real para encontrar as melhores oportunidades.
                        </p>
                    </div>

                    <div class="premium-glass rounded-2xl p-8 text-center hover:scale-105 transition-transform duration-300">
                        <div class="w-16 h-16 premium-button rounded-2xl flex items-center justify-center mx-auto mb-6">
                            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-1.447-.894L15 4m0 13V4m0 0L9 7"/>
                            </svg>
                        </div>
                        <h3 class="text-2xl font-bold text-slate-800 mb-4">Otimização de Rotas</h3>
                        <p class="text-slate-600 leading-relaxed">
                            Algoritmo exclusivo que analisa localização e melhores preços para criar rotas eficientes de compras.
                        </p>
                    </div>

                    <div class="premium-glass rounded-2xl p-8 text-center hover:scale-105 transition-transform duration-300">
                        <div class="w-16 h-16 premium-button rounded-2xl flex items-center justify-center mx-auto mb-6">
                            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
                            </svg>
                        </div>
                        <h3 class="text-2xl font-bold text-slate-800 mb-4">Estratégias Perfeitas</h3>
                        <p class="text-slate-600 leading-relaxed">
                            Sistema que aprende seus hábitos de compra e sugere estratégias personalizadas para maximizar sua economia.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Product Search Interface -->
        <section id="productSearch" class="py-20 bg-gradient-to-br from-indigo-50 to-purple-50 relative overflow-hidden">
            <!-- Interactive Map Background -->
            <div class="interactive-map">
                <svg width="100%" height="100%" viewBox="0 0 800 600" class="absolute inset-0">
                    <!-- Simplified Juiz de Fora street map -->
                    <defs>
                        <pattern id="streetPattern" patternUnits="userSpaceOnUse" width="4" height="4">
                            <rect width="4" height="4" fill="rgba(79, 70, 229, 0.05)"/>
                            <path d="M 0,4 l 4,-4 M -1,1 l 2,-2 M 3,5 l 2,-2" stroke="rgba(79, 70, 229, 0.1)" stroke-width="0.5"/>
                        </pattern>
                    </defs>
                    
                    <!-- Main streets -->
                    <path d="M50 100 L750 100" stroke="rgba(79, 70, 229, 0.2)" stroke-width="3" class="street-main"/>
                    <path d="M50 200 L750 200" stroke="rgba(79, 70, 229, 0.2)" stroke-width="3" class="street-main"/>
                    <path d="M50 300 L750 300" stroke="rgba(79, 70, 229, 0.2)" stroke-width="3" class="street-main"/>
                    <path d="M50 400 L750 400" stroke="rgba(79, 70, 229, 0.2)" stroke-width="3" class="street-main"/>
                    
                    <!-- Cross streets -->
                    <path d="M150 50 L150 550" stroke="rgba(79, 70, 229, 0.15)" stroke-width="2" class="street-cross"/>
                    <path d="M300 50 L300 550" stroke="rgba(79, 70, 229, 0.15)" stroke-width="2" class="street-cross"/>
                    <path d="M450 50 L450 550" stroke="rgba(79, 70, 229, 0.15)" stroke-width="2" class="street-cross"/>
                    <path d="M600 50 L600 550" stroke="rgba(79, 70, 229, 0.15)" stroke-width="2" class="street-cross"/>
                    
                    <!-- Store markers -->
                    <circle cx="200" cy="150" r="4" fill="rgba(79, 70, 229, 0.3)" class="store-marker">
                        <animate attributeName="r" values="4;6;4" dur="2s" repeatCount="indefinite"/>
                    </circle>
                    <circle cx="350" cy="250" r="4" fill="rgba(124, 58, 237, 0.3)" class="store-marker">
                        <animate attributeName="r" values="4;6;4" dur="2.5s" repeatCount="indefinite"/>
                    </circle>
                    <circle cx="500" cy="180" r="4" fill="rgba(236, 72, 153, 0.3)" class="store-marker">
                        <animate attributeName="r" values="4;6;4" dur="3s" repeatCount="indefinite"/>
                    </circle>
                    <circle cx="250" cy="350" r="4" fill="rgba(79, 70, 229, 0.3)" class="store-marker">
                        <animate attributeName="r" values="4;6;4" dur="2.2s" repeatCount="indefinite"/>
                    </circle>
                    
                    <!-- Search animation lines (hidden by default) -->
                    <g id="searchAnimation" style="opacity: 0;">
                        <path d="M200 150 L350 250" stroke="#4f46e5" stroke-width="2" stroke-dasharray="5,5" class="search-path">
                            <animate attributeName="stroke-dashoffset" values="0;-10" dur="1s" repeatCount="indefinite"/>
                        </path>
                        <path d="M350 250 L500 180" stroke="#7c3aed" stroke-width="2" stroke-dasharray="5,5" class="search-path">
                            <animate attributeName="stroke-dashoffset" values="0;-10" dur="1s" repeatCount="indefinite"/>
                        </path>
                        <path d="M500 180 L250 350" stroke="#ec4899" stroke-width="2" stroke-dasharray="5,5" class="search-path">
                            <animate attributeName="stroke-dashoffset" values="0;-10" dur="1s" repeatCount="indefinite"/>
                        </path>
                    </g>
                </svg>
            </div>
            
            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
                <div class="text-center mb-12">
                    <h2 class="text-4xl font-bold text-slate-800 mb-6">
                        Busque e Compare Produtos
                    </h2>
                    <p class="text-xl text-slate-600">
                        Digite o produto que você procura e veja os melhores preços em tempo real
                    </p>
                </div>

                <!-- Search Bar -->
                <div class="premium-glass rounded-2xl p-8 mb-8 neon-glow">
                    <div class="flex flex-col sm:flex-row gap-4">
                        <div class="flex-1">
                            <input 
                                type="text" 
                                id="productSearchInput"
                                placeholder="Ex: Coca-Cola 2L, Arroz 5kg, Leite integral..."
                                class="w-full px-6 py-4 text-lg border-2 border-gray-200 rounded-xl focus:border-indigo-500 focus:outline-none transition-all duration-300 cyber-border"
                                onkeypress="handleSearchKeyPress(event)"
                                onfocus="startMapAnimation()"
                                onblur="stopMapAnimation()"
                            >
                        </div>
                        <button 
                            onclick="searchProducts()"
                            class="premium-button text-white px-8 py-4 rounded-xl font-semibold text-lg whitespace-nowrap"
                        >
                            <svg class="w-6 h-6 inline mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
                            </svg>
                            Buscar
                        </button>
                    </div>
                </div>

                <!-- Product Categories -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-8">
                    <button onclick="searchByCategory('bebidas')" class="category-card premium-glass rounded-xl p-4 text-center hover:scale-105 transition-all duration-300">
                        <div class="w-12 h-12 bg-blue-100 rounded-lg mx-auto mb-3 flex items-center justify-center">
                            🥤
                        </div>
                        <span class="font-semibold text-slate-800">Bebidas</span>
                    </button>
                    <button onclick="searchByCategory('laticinios')" class="category-card premium-glass rounded-xl p-4 text-center hover:scale-105 transition-all duration-300">
                        <div class="w-12 h-12 bg-yellow-100 rounded-lg mx-auto mb-3 flex items-center justify-center">
                            🥛
                        </div>
                        <span class="font-semibold text-slate-800">Laticínios</span>
                    </button>
                    <button onclick="searchByCategory('carnes')" class="category-card premium-glass rounded-xl p-4 text-center hover:scale-105 transition-all duration-300">
                        <div class="w-12 h-12 bg-red-100 rounded-lg mx-auto mb-3 flex items-center justify-center">
                            🥩
                        </div>
                        <span class="font-semibold text-slate-800">Carnes</span>
                    </button>
                    <button onclick="searchByCategory('cereais')" class="category-card premium-glass rounded-xl p-4 text-center hover:scale-105 transition-all duration-300">
                        <div class="w-12 h-12 bg-green-100 rounded-lg mx-auto mb-3 flex items-center justify-center">
                            🌾
                        </div>
                        <span class="font-semibold text-slate-800">Cereais</span>
                    </button>
                </div>

                <!-- Search Results -->
                <div id="searchResults" class="hidden">
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-6">
                        <h3 class="text-2xl font-bold text-slate-800 mb-4 sm:mb-0">Resultados da Busca</h3>
                        <div class="flex flex-col sm:flex-row gap-3">
                            <select id="sortBy" onchange="sortProducts()" class="px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                                <option value="price">Ordenar por Preço</option>
                                <option value="distance">Ordenar por Proximidade</option>
                                <option value="savings">Ordenar por Economia</option>
                            </select>
                            <div class="text-sm text-slate-600 flex items-center">
                                <span id="resultsCount">0 produtos encontrados</span>
                            </div>
                        </div>
                    </div>
                    <div id="productList" class="space-y-4">
                        <!-- Products will be populated here -->
                    </div>
                </div>
            </div>
        </section>

        <!-- CTA Section -->
        <section class="py-20 bg-white">
            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
                <h2 class="text-4xl md:text-5xl font-bold text-slate-800 mb-6">
                    Pronto para economizar de verdade?
                </h2>
                <p class="text-xl text-slate-600 mb-8 leading-relaxed">
                    Junte-se às famílias de Juiz de Fora que já descobriram o poder da compra inteligente
                </p>
                <button onclick="showSignupModal()" class="premium-button text-white px-8 py-4 rounded-xl font-bold text-lg shadow-lg">
                    Começar Agora
                </button>
            </div>
        </section>
    </div>

    <!-- COMO FUNCIONA PAGE -->
    <div id="como-funciona" class="page-section">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Como Funciona</h1>
                <p class="text-xl text-slate-600 max-w-3xl mx-auto">
                    Descubra como nossa tecnologia revoluciona suas compras em Juiz de Fora
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-16">
                <div class="text-center">
                    <div class="w-20 h-20 premium-button rounded-full flex items-center justify-center mx-auto mb-6">
                        <span class="text-3xl text-white">1</span>
                    </div>
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">Cadastre-se</h3>
                    <p class="text-slate-600">Crie sua conta e configure suas preferências de compra</p>
                </div>
                <div class="text-center">
                    <div class="w-20 h-20 premium-button rounded-full flex items-center justify-center mx-auto mb-6">
                        <span class="text-3xl text-white">2</span>
                    </div>
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">Busque Produtos</h3>
                    <p class="text-slate-600">Digite ou escaneie produtos para comparar preços em tempo real</p>
                </div>
                <div class="text-center">
                    <div class="w-20 h-20 premium-button rounded-full flex items-center justify-center mx-auto mb-6">
                        <span class="text-3xl text-white">3</span>
                    </div>
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">Economize</h3>
                    <p class="text-slate-600">Receba rotas otimizadas e economize tempo e dinheiro</p>
                </div>
            </div>

            <div class="premium-glass rounded-2xl p-8">
                <h2 class="text-3xl font-bold text-slate-800 mb-6">Tecnologia Avançada</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div>
                        <h4 class="text-xl font-semibold text-slate-800 mb-3">🤖 Inteligência Artificial</h4>
                        <p class="text-slate-600 mb-4">Nossa IA analisa padrões de preços, promoções e qualidade dos produtos para encontrar as melhores oportunidades.</p>
                    </div>
                    <div>
                        <h4 class="text-xl font-semibold text-slate-800 mb-3">🗺️ Otimização de Rotas</h4>
                        <p class="text-slate-600 mb-4">Algoritmo exclusivo que analisa localização e melhores preços para criar rotas eficientes de compras.</p>
                    </div>
                    <div>
                        <h4 class="text-xl font-semibold text-slate-800 mb-3">📊 Análise de Dados</h4>
                        <p class="text-slate-600 mb-4">Processamos milhões de dados diariamente para garantir informações precisas e atualizadas.</p>
                    </div>
                    <div>
                        <h4 class="text-xl font-semibold text-slate-800 mb-3">🔄 Tempo Real</h4>
                        <p class="text-slate-600 mb-4">Preços atualizados a cada minuto para você sempre ter as informações mais recentes.</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- APP PAGE -->
    <div id="app" class="page-section">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Baixar App</h1>
                <p class="text-xl text-slate-600 max-w-3xl mx-auto">
                    Leve o Compra Boa JF no seu bolso e economize onde quer que esteja
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                <div>
                    <h2 class="text-3xl font-bold text-slate-800 mb-6">Recursos do App</h2>
                    <div class="space-y-6">
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Scanner de Código de Barras</h4>
                                <p class="text-slate-600">Escaneie produtos e veja preços instantaneamente</p>
                            </div>
                        </div>
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Navegação GPS</h4>
                                <p class="text-slate-600">Rotas otimizadas com navegação turn-by-turn</p>
                            </div>
                        </div>
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-5 5v-5zM4.828 7l2.586 2.586a2 2 0 002.828 0L13.828 7l2.586 2.586a2 2 0 002.828 0L22.828 7M4 4h16v13H4V4z"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Notificações Push</h4>
                                <p class="text-slate-600">Alertas de promoções e melhores preços</p>
                            </div>
                        </div>
                    </div>

                    <div class="flex flex-col sm:flex-row gap-4 mt-8">
                        <a href="#" class="flex items-center justify-center bg-black text-white px-6 py-3 rounded-lg font-semibold hover:bg-gray-800 transition-colors">
                            <svg class="w-6 h-6 mr-2" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M17.05 20.28c-.98.95-2.05.8-3.08.35-1.09-.46-2.09-.48-3.24 0-1.44.62-2.2.44-3.06-.35C2.79 15.25 3.51 7.59 9.05 7.31c1.35.07 2.29.74 3.08.8 1.18-.24 2.31-.93 3.57-.84 1.51.12 2.65.72 3.4 1.8-3.12 1.87-2.38 5.98.48 7.13-.57 1.5-1.31 2.99-2.54 4.09l.01-.01zM12.03 7.25c-.15-2.23 1.66-4.07 3.74-4.25.29 2.58-2.34 4.5-3.74 4.25z"/>
                            </svg>
                            App Store
                        </a>
                        <a href="#" class="flex items-center justify-center bg-green-600 text-white px-6 py-3 rounded-lg font-semibold hover:bg-green-700 transition-colors">
                            <svg class="w-6 h-6 mr-2" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M3,20.5V3.5C3,2.91 3.34,2.39 3.84,2.15L13.69,12L3.84,21.85C3.34,21.6 3,21.09 3,20.5M16.81,15.12L6.05,21.34L14.54,12.85L16.81,15.12M20.16,10.81C20.5,11.08 20.75,11.5 20.75,12C20.75,12.5 20.53,12.9 20.18,13.18L17.89,14.5L15.39,12L17.89,9.5L20.16,10.81M6.05,2.66L16.81,8.88L14.54,11.15L6.05,2.66Z"/>
                            </svg>
                            Google Play
                        </a>
                    </div>
                </div>

                <div class="text-center">
                    <div class="w-80 h-80 bg-gradient-to-br from-indigo-100 to-purple-100 rounded-3xl mx-auto flex items-center justify-center">
                        <div class="text-6xl">📱</div>
                    </div>
                    <p class="text-slate-600 mt-6">Disponível para iOS e Android</p>
                </div>
            </div>
        </div>
    </div>

    <!-- ASSINATURA PAGE -->
    <div id="assinatura" class="page-section">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Planos de Assinatura</h1>
                <p class="text-xl text-slate-600 max-w-3xl mx-auto">
                    Escolha o plano ideal para maximizar sua economia em Juiz de Fora
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12 max-w-4xl mx-auto">
                <!-- Plano Básico -->
                <div class="premium-glass rounded-2xl p-8 text-center hover:scale-105 transition-all duration-300">
                    <div class="mb-6">
                        <div class="w-16 h-16 bg-blue-100 rounded-2xl flex items-center justify-center mx-auto mb-4">
                            <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
                            </svg>
                        </div>
                        <h3 class="text-2xl font-bold text-slate-800 mb-2">Básico</h3>
                        <p class="text-sm text-slate-600 mb-4">Todas as funcionalidades essenciais</p>
                        <div class="text-4xl font-bold gradient-text mb-2">R$ 9,90<span class="text-lg text-slate-600">/mês</span></div>
                    </div>
                    
                    <div class="text-left mb-8 space-y-3">
                        <div class="bg-green-50 rounded-lg p-3 mb-4">
                            <h4 class="font-semibold text-green-800 mb-2">🎯 Pesquisa em Tempo Real</h4>
                            <ul class="text-sm text-green-700 space-y-1">
                                <li>• Todos os 70+ mercados cadastrados</li>
                                <li>• Preço, distância e última atualização</li>
                                <li>• Ordenação: preço, proximidade, custo-benefício</li>
                            </ul>
                        </div>
                        
                        <div class="bg-blue-50 rounded-lg p-3 mb-4">
                            <h4 class="font-semibold text-blue-800 mb-2">🏆 Ranking por Produto</h4>
                            <ul class="text-sm text-blue-700 space-y-1">
                                <li>• Badge "#1 em preço"</li>
                                <li>• "#2 em distância (750m)"</li>
                                <li>• Comparação completa entre lojas</li>
                            </ul>
                        </div>
                        
                        <div class="bg-purple-50 rounded-lg p-3 mb-4">
                            <h4 class="font-semibold text-purple-800 mb-2">🛒 Carrinho Inteligente</h4>
                            <ul class="text-sm text-purple-700 space-y-1">
                                <li>• Otimização de rotas de compras</li>
                                <li>• Menor preço total vs mais próximo</li>
                                <li>• Opção custo-benefício equilibrada</li>
                            </ul>
                        </div>
                        
                        <div class="bg-orange-50 rounded-lg p-3 mb-4">
                            <h4 class="font-semibold text-orange-800 mb-2">📊 Histórico e Alertas</h4>
                            <ul class="text-sm text-orange-700 space-y-1">
                                <li>• Curva de preço (30 dias)</li>
                                <li>• Alerta de queda de preço</li>
                                <li>• Análise de tendências</li>
                            </ul>
                        </div>
                        
                        <div class="bg-indigo-50 rounded-lg p-3 mb-4">
                            <h4 class="font-semibold text-indigo-800 mb-2">💰 Vantagens Exclusivas</h4>
                            <ul class="text-sm text-indigo-700 space-y-1">
                                <li>• Cupons de desconto exclusivos</li>
                                <li>• Cashback em parceiros</li>
                                <li>• Sistema de missões e pontos</li>
                            </ul>
                        </div>
                    </div>
                    
                    <button onclick="selectPlan('basico')" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-semibold transition-colors">
                        Escolher Básico
                    </button>
                </div>

                <!-- Plano Premium -->
                <div class="premium-glass rounded-2xl p-8 text-center border-2 border-indigo-300 relative hover:scale-105 transition-all duration-300">
                    <div class="absolute -top-4 left-1/2 transform -translate-x-1/2 bg-indigo-600 text-white px-4 py-1 rounded-full text-sm font-semibold">
                        MAIS POPULAR
                    </div>
                    <div class="mb-6">
                        <div class="w-16 h-16 bg-indigo-100 rounded-2xl flex items-center justify-center mx-auto mb-4">
                            <svg class="w-8 h-8 text-indigo-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
                            </svg>
                        </div>
                        <h3 class="text-2xl font-bold text-slate-800 mb-2">Premium</h3>
                        <p class="text-sm text-slate-600 mb-4">Tudo do Básico + Sorteio Mensal</p>
                        <div class="text-4xl font-bold gradient-text mb-2">R$ 19,90<span class="text-lg text-slate-600">/mês</span></div>
                    </div>
                    
                    <div class="text-left mb-8 space-y-3">
                        <div class="bg-green-50 rounded-lg p-3">
                            <p class="font-semibold text-green-800 text-sm">✅ Todas as funcionalidades do Básico +</p>
                        </div>
                        
                        <div class="bg-yellow-50 rounded-lg p-3 mb-4 border-2 border-yellow-300">
                            <h4 class="font-semibold text-yellow-800 mb-2">🎁 Sorteio Mensal Exclusivo</h4>
                            <ul class="text-sm text-yellow-700 space-y-1">
                                <li>• <strong>R$ 1.000 em compras</strong> todo mês</li>
                                <li>• Participação automática</li>
                                <li>• Sorteio no último dia do mês</li>
                                <li>• Válido apenas para assinantes ativos</li>
                            </ul>
                        </div>
                        
                        <div class="bg-indigo-50 rounded-lg p-3 mb-4">
                            <h4 class="font-semibold text-indigo-800 mb-2">🏆 Vantagens Premium</h4>
                            <ul class="text-sm text-indigo-700 space-y-1">
                                <li>• Suporte prioritário</li>
                                <li>• Acesso antecipado a novidades</li>
                                <li>• Relatórios de economia personalizados</li>
                            </ul>
                        </div>
                        
                        <div class="bg-pink-50 rounded-lg p-3 mb-4">
                            <h4 class="font-semibold text-pink-800 mb-2">🤝 Trocas Sugeridas Patrocinadas</h4>
                            <ul class="text-sm text-pink-700 space-y-1">
                                <li>• Melhor custo por quantidade</li>
                                <li>• Selo "Sugestão do parceiro"</li>
                                <li>• Ofertas exclusivas de marcas</li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="text-xs text-slate-500 mb-6 bg-gray-50 rounded-lg p-3">
                        <p class="font-semibold mb-1 text-yellow-700">⚠️ Importante:</p>
                        <p>A participação no sorteio mensal está condicionada à manutenção da assinatura ativa.</p>
                    </div>
                    
                    <button onclick="selectPlan('premium')" class="w-full premium-button text-white py-3 rounded-lg font-semibold">
                        Escolher Premium
                    </button>
                </div>
            </div>

            <!-- Exemplo de Carrinho Inteligente -->
            <div class="premium-glass rounded-2xl p-8 mb-12">
                <h2 class="text-3xl font-bold text-slate-800 mb-6 text-center">
                    💡 Exemplo: Carrinho Inteligente Avançado (Premium)
                </h2>
                <div class="bg-slate-50 rounded-xl p-6">
                    <div class="mb-4">
                        <h3 class="font-semibold text-slate-800 mb-2">Sua lista: 12 itens</h3>
                        <p class="text-sm text-slate-600">3 opções de compra calculadas automaticamente:</p>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="bg-green-100 rounded-lg p-4 border-2 border-green-300">
                            <div class="flex items-center mb-2">
                                <span class="bg-green-600 text-white text-xs px-2 py-1 rounded-full font-semibold mr-2">MAIS BARATO</span>
                            </div>
                            <h4 class="font-bold text-green-800">Bahamas Centro</h4>
                            <p class="text-2xl font-bold text-green-600">R$ 212,50</p>
                            <p class="text-sm text-green-700">📍 3,5 km de distância</p>
                        </div>
                        
                        <div class="bg-blue-100 rounded-lg p-4 border-2 border-blue-300">
                            <div class="flex items-center mb-2">
                                <span class="bg-blue-600 text-white text-xs px-2 py-1 rounded-full font-semibold mr-2">MAIS PRÓXIMO</span>
                            </div>
                            <h4 class="font-bold text-blue-800">Colina Gourmet</h4>
                            <p class="text-2xl font-bold text-blue-600">R$ 224,80</p>
                            <p class="text-sm text-blue-700">📍 0,9 km de distância</p>
                        </div>
                        
                        <div class="bg-purple-100 rounded-lg p-4 border-2 border-purple-300">
                            <div class="flex items-center mb-2">
                                <span class="bg-purple-600 text-white text-xs px-2 py-1 rounded-full font-semibold mr-2">CUSTO-BENEFÍCIO</span>
                            </div>
                            <h4 class="font-bold text-purple-800">Bretas + Mercearia São José</h4>
                            <p class="text-2xl font-bold text-purple-600">R$ 218,90</p>
                            <p class="text-sm text-purple-700">📍 1,2 km total</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Informações para Parceiros -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
                <div class="premium-glass rounded-2xl p-8">
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">🏪 Para Mercados/Supermercados</h3>
                    <p class="text-slate-600 leading-relaxed">
                        "Sua loja será vitrine para todos os consumidores da cidade, com destaque em filtros patrocinados e cupons. 
                        Você não paga para estar presente – e ainda pode patrocinar trocas sugeridas e selos para aumentar vendas."
                    </p>
                    <button onclick="showPage('parceiros')" class="mt-4 premium-button text-white px-6 py-2 rounded-lg font-semibold">
                        Seja Parceiro
                    </button>
                </div>
                
                <div class="premium-glass rounded-2xl p-8">
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">🏭 Para Marcas/Fornecedores</h3>
                    <p class="text-slate-600 leading-relaxed">
                        "Posicione seus produtos como a escolha inteligente ou saudável, no momento da decisão de compra. 
                        Patrocine trocas, cupons e cashback para seu público ideal."
                    </p>
                    <button onclick="showPage('contato')" class="mt-4 bg-slate-600 hover:bg-slate-700 text-white px-6 py-2 rounded-lg font-semibold transition-colors">
                        Falar Conosco
                    </button>
                </div>
            </div>

            <!-- FAQ Section -->
            <div class="bg-gradient-to-br from-slate-50 to-indigo-50 rounded-3xl p-8 mb-12">
                <div class="text-center mb-8">
                    <h2 class="text-3xl font-bold text-slate-800 mb-4">❓ Perguntas Frequentes</h2>
                    <p class="text-slate-600">Tire suas dúvidas sobre o Compra Boa JF</p>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">🌍 Como contribuímos para um mundo mais sustentável?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            O Compra Boa JF está alinhado com os <strong>Objetivos de Desenvolvimento Sustentável da ONU</strong>, especialmente:
                            <br>• <strong>ODS 12</strong> - Consumo e Produção Responsáveis: reduzimos desperdício otimizando compras
                            <br>• <strong>ODS 11</strong> - Cidades Sustentáveis: diminuímos trânsito com rotas eficientes
                            <br>• <strong>ODS 1</strong> - Erradicação da Pobreza: ajudamos famílias a economizar significativamente
                        </p>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">💰 Quanto posso economizar por mês?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            Nossos usuários economizam em média <strong>15-25% nas compras mensais</strong>. Uma família que gasta R$ 800/mês pode economizar entre R$ 120-200, pagando apenas R$ 9,90 ou R$ 19,90 pela assinatura. O retorno do investimento é garantido!
                        </p>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">🏪 Quantos supermercados estão cadastrados?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            Temos <strong>mais de 70 estabelecimentos</strong> cadastrados em Juiz de Fora, incluindo grandes redes (Extra, Zona Sul, EPA, Bahamas, Carrefour) e mercados de bairro. Atualizamos preços diariamente para garantir informações precisas.
                        </p>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">🎁 Como funciona o sorteio mensal?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            Assinantes Premium participam automaticamente do sorteio de <strong>R$ 1.000 em compras</strong> todo mês. O sorteio acontece no último dia útil do mês, e o ganhador recebe créditos para usar em qualquer estabelecimento parceiro. <strong>Importante:</strong> só participa quem mantém a assinatura ativa.
                        </p>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">📱 Preciso baixar um aplicativo?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            Não! O Compra Boa JF funciona 100% no navegador do seu celular, tablet ou computador. Basta acessar o site, fazer login e usar todas as funcionalidades. É mais prático e não ocupa espaço no seu dispositivo.
                        </p>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">🔒 Meus dados estão seguros?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            Sim! Seguimos rigorosamente a <strong>LGPD</strong> e utilizamos criptografia de ponta. Seus dados pessoais e de pagamento são protegidos com os mais altos padrões de segurança. Nunca compartilhamos informações com terceiros sem seu consentimento.
                        </p>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">⏰ Os preços são atualizados em tempo real?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            Atualizamos preços <strong>diariamente</strong> através de parcerias diretas com os estabelecimentos e verificação manual. Embora não seja "tempo real" no sentido literal, garantimos que as informações tenham no máximo 24h de defasagem.
                        </p>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-sm">
                        <h4 class="font-bold text-slate-800 mb-3">🚫 Posso cancelar quando quiser?</h4>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            <strong>Sim, sem taxas ou multas!</strong> Você pode cancelar sua assinatura a qualquer momento através do seu painel de usuário. O acesso continua até o final do período já pago. Oferecemos 7 dias de teste grátis para você experimentar sem compromisso.
                        </p>
                    </div>
                </div>
            </div>

            <div class="text-center">
                <p class="text-slate-600 mb-4">Todos os planos incluem 7 dias de teste grátis</p>
                <p class="text-sm text-slate-500">Cancele a qualquer momento • Sem taxas de cancelamento • Controle anti-fraude por CPF</p>
            </div>
        </div>
    </div>

    <!-- PARCEIROS PAGE -->
    <div id="parceiros" class="page-section">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Seja Nosso Parceiro</h1>
                <p class="text-xl text-slate-600 max-w-3xl mx-auto">
                    Conecte seu supermercado a milhares de consumidores em Juiz de Fora
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center mb-16">
                <div>
                    <h2 class="text-3xl font-bold text-slate-800 mb-6">Vantagens para Parceiros</h2>
                    <div class="space-y-6">
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Aumento de Vendas</h4>
                                <p class="text-slate-600">Atraia mais clientes com nossa base de usuários ativa</p>
                            </div>
                        </div>
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Analytics Detalhados</h4>
                                <p class="text-slate-600">Relatórios completos sobre performance e tendências</p>
                            </div>
                        </div>
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Gestão de Promoções</h4>
                                <p class="text-slate-600">Ferramentas para criar e gerenciar ofertas especiais</p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="premium-glass rounded-2xl p-8">
                    <h3 class="text-2xl font-bold text-slate-800 mb-6">Solicitar Parceria</h3>
                    <form class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Nome do Supermercado</label>
                            <input type="text" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Nome da sua empresa">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Responsável</label>
                            <input type="text" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Seu nome">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">E-mail</label>
                            <input type="email" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="seu@email.com">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Telefone</label>
                            <input type="tel" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="(32) 99999-9999">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Endereço</label>
                            <input type="text" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Endereço completo">
                        </div>
                        <button type="submit" class="w-full premium-button text-white py-3 rounded-lg font-semibold">
                            Enviar Solicitação
                        </button>
                    </form>
                </div>
            </div>

            <div class="text-center">
                <h3 class="text-2xl font-bold text-slate-800 mb-6">Nossos Parceiros Atuais</h3>
                <div class="grid grid-cols-2 md:grid-cols-5 gap-8">
                    <div class="premium-glass rounded-lg p-4 text-center">
                        <div class="text-2xl mb-2">🛒</div>
                        <p class="font-semibold text-slate-800">Zona Sul</p>
                    </div>
                    <div class="premium-glass rounded-lg p-4 text-center">
                        <div class="text-2xl mb-2">🏪</div>
                        <p class="font-semibold text-slate-800">Extra</p>
                    </div>
                    <div class="premium-glass rounded-lg p-4 text-center">
                        <div class="text-2xl mb-2">🛍️</div>
                        <p class="font-semibold text-slate-800">EPA</p>
                    </div>
                    <div class="premium-glass rounded-lg p-4 text-center">
                        <div class="text-2xl mb-2">🏬</div>
                        <p class="font-semibold text-slate-800">Bahamas</p>
                    </div>
                    <div class="premium-glass rounded-lg p-4 text-center">
                        <div class="text-2xl mb-2">🛒</div>
                        <p class="font-semibold text-slate-800">+21 outros</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- CONTATO PAGE -->
    <div id="contato" class="page-section">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Entre em Contato</h1>
                <p class="text-xl text-slate-600 max-w-3xl mx-auto">
                    Estamos aqui para ajudar você a economizar ainda mais
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
                <div>
                    <h2 class="text-3xl font-bold text-slate-800 mb-8">Fale Conosco</h2>
                    
                    <div class="space-y-6 mb-8">
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">E-mail</h4>
                                <p class="text-slate-600">contato@compraboajf.com.br</p>
                                <p class="text-slate-600">suporte@compraboajf.com.br</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Telefone</h4>
                                <p class="text-slate-600">(32) 3025-1234</p>
                                <p class="text-slate-600">(32) 99999-8888</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/>
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
                                </svg>
                            </div>
                            <div>
                                <h4 class="font-semibold text-slate-800">Endereço</h4>
                                <p class="text-slate-600">Rua Halfeld, 1234 - Centro</p>
                                <p class="text-slate-600">Juiz de Fora - MG, 36010-000</p>
                            </div>
                        </div>
                    </div>

                    <div>
                        <h3 class="text-xl font-bold text-slate-800 mb-4">Horário de Atendimento</h3>
                        <div class="space-y-2 text-slate-600">
                            <p>Segunda a Sexta: 8h às 18h</p>
                            <p>Sábado: 8h às 14h</p>
                            <p>Domingo: Fechado</p>
                        </div>
                    </div>
                </div>

                <div class="premium-glass rounded-2xl p-8">
                    <h3 class="text-2xl font-bold text-slate-800 mb-6">Envie sua Mensagem</h3>
                    <form class="space-y-4">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-slate-700 mb-2">Nome</label>
                                <input type="text" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Seu nome">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-slate-700 mb-2">E-mail</label>
                                <input type="email" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="seu@email.com">
                            </div>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Assunto</label>
                            <select class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                                <option>Suporte Técnico</option>
                                <option>Dúvidas sobre Planos</option>
                                <option>Parceria</option>
                                <option>Sugestões</option>
                                <option>Outros</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Mensagem</label>
                            <textarea rows="5" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Descreva sua dúvida ou sugestão..."></textarea>
                        </div>
                        <button type="submit" class="w-full premium-button text-white py-3 rounded-lg font-semibold">
                            Enviar Mensagem
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <!-- TERMOS PAGE -->
    <div id="termos" class="page-section">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Termos de Uso</h1>
                <p class="text-xl text-slate-600">Última atualização: Janeiro de 2024</p>
            </div>

            <div class="premium-glass rounded-2xl p-8 space-y-8">
                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">1. Aceitação dos Termos</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Ao utilizar o Compra Boa JF, você concorda com estes termos de uso. Se não concordar com qualquer parte destes termos, não utilize nossos serviços.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">2. Descrição do Serviço</h2>
                    <p class="text-slate-600 leading-relaxed">
                        O Compra Boa JF é uma plataforma de comparação de preços que permite aos usuários comparar preços de produtos em diferentes supermercados de Juiz de Fora, otimizar rotas de compras e receber alertas de promoções.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">3. Cadastro e Conta</h2>
                    <p class="text-slate-600 leading-relaxed mb-4">
                        Para utilizar nossos serviços, você deve:
                    </p>
                    <ul class="list-disc list-inside text-slate-600 space-y-2">
                        <li>Fornecer informações verdadeiras e atualizadas</li>
                        <li>Manter a segurança de sua senha</li>
                        <li>Ser responsável por todas as atividades em sua conta</li>
                        <li>Notificar-nos imediatamente sobre uso não autorizado</li>
                    </ul>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">4. Uso Aceitável</h2>
                    <p class="text-slate-600 leading-relaxed mb-4">
                        Você concorda em não:
                    </p>
                    <ul class="list-disc list-inside text-slate-600 space-y-2">
                        <li>Usar o serviço para fins ilegais ou não autorizados</li>
                        <li>Interferir ou interromper o funcionamento do serviço</li>
                        <li>Tentar acessar dados de outros usuários</li>
                        <li>Reproduzir ou distribuir conteúdo sem autorização</li>
                    </ul>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">5. Preços e Informações</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Fazemos o possível para manter as informações de preços atualizadas, mas não garantimos a precisão absoluta. Os preços podem variar e devem ser confirmados diretamente com os estabelecimentos.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">6. Pagamentos e Assinaturas</h2>
                    <p class="text-slate-600 leading-relaxed">
                        As assinaturas são cobradas mensalmente. Você pode cancelar a qualquer momento. O cancelamento será efetivo no final do período de cobrança atual.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">7. Limitação de Responsabilidade</h2>
                    <p class="text-slate-600 leading-relaxed">
                        O Compra Boa JF não se responsabiliza por danos diretos, indiretos, incidentais ou consequenciais decorrentes do uso de nossos serviços.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">8. Alterações nos Termos</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Reservamos o direito de modificar estes termos a qualquer momento. As alterações serão comunicadas através da plataforma.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">9. Contato</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Para dúvidas sobre estes termos, entre em contato conosco através do email: contato@compraboajf.com.br
                    </p>
                </section>
            </div>
        </div>
    </div>

    <!-- MINHA CONTA PAGE -->
    <div id="minha-conta" class="page-section">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Minha Conta</h1>
                <p class="text-xl text-slate-600">Gerencie sua assinatura e configurações</p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <!-- Sidebar -->
                <div class="lg:col-span-1">
                    <div class="premium-glass rounded-2xl p-6 sticky top-24">
                        <div class="text-center mb-6">
                            <div class="w-20 h-20 bg-indigo-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                <span id="userInitialsLarge" class="text-2xl font-bold text-indigo-600">U</span>
                            </div>
                            <h3 id="userNameLarge" class="text-xl font-bold text-slate-800">Usuário</h3>
                            <p id="userEmailLarge" class="text-slate-600">usuario@email.com</p>
                        </div>
                        
                        <div class="space-y-2">
                            <button onclick="showAccountSection('perfil')" class="account-tab w-full text-left px-4 py-3 rounded-lg font-semibold text-slate-700 hover:bg-white/50 transition-colors active">
                                👤 Perfil
                            </button>
                            <button onclick="showAccountSection('assinatura')" class="account-tab w-full text-left px-4 py-3 rounded-lg font-semibold text-slate-700 hover:bg-white/50 transition-colors">
                                💳 Assinatura
                            </button>
                            <button onclick="showAccountSection('historico')" class="account-tab w-full text-left px-4 py-3 rounded-lg font-semibold text-slate-700 hover:bg-white/50 transition-colors">
                                📊 Histórico
                            </button>
                            <button onclick="showAccountSection('alertas')" class="account-tab w-full text-left px-4 py-3 rounded-lg font-semibold text-slate-700 hover:bg-white/50 transition-colors">
                                🔔 Alertas
                            </button>
                            <button onclick="showAccountSection('configuracoes')" class="account-tab w-full text-left px-4 py-3 rounded-lg font-semibold text-slate-700 hover:bg-white/50 transition-colors">
                                ⚙️ Configurações
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Main Content -->
                <div class="lg:col-span-2">
                    <!-- Perfil Section -->
                    <div id="account-perfil" class="account-section">
                        <div class="premium-glass rounded-2xl p-8">
                            <h2 class="text-2xl font-bold text-slate-800 mb-6">Informações do Perfil</h2>
                            
                            <form class="space-y-6">
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                    <div>
                                        <label class="block text-sm font-medium text-slate-700 mb-2">Nome Completo</label>
                                        <input type="text" id="profileName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                                    </div>
                                    <div>
                                        <label class="block text-sm font-medium text-slate-700 mb-2">E-mail</label>
                                        <input type="email" id="profileEmail" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                                    </div>
                                </div>
                                
                                <div>
                                    <label class="block text-sm font-medium text-slate-700 mb-2">CPF</label>
                                    <input type="text" id="profileCPF" readonly class="w-full px-4 py-3 border border-gray-300 rounded-lg bg-gray-50">
                                    <p class="text-xs text-gray-500 mt-1">CPF não pode ser alterado</p>
                                </div>
                                
                                <button type="button" onclick="updateProfile()" class="premium-button text-white px-6 py-3 rounded-lg font-semibold">
                                    Salvar Alterações
                                </button>
                            </form>
                        </div>
                    </div>

                    <!-- Assinatura Section -->
                    <div id="account-assinatura" class="account-section hidden">
                        <div class="premium-glass rounded-2xl p-8">
                            <h2 class="text-2xl font-bold text-slate-800 mb-6">Minha Assinatura</h2>
                            
                            <div class="bg-gradient-to-r from-indigo-50 to-purple-50 rounded-xl p-6 mb-6">
                                <div class="flex items-center justify-between mb-4">
                                    <div>
                                        <h3 class="text-xl font-bold text-indigo-800" id="currentPlanName">Plano Premium</h3>
                                        <p class="text-indigo-600">Ativo desde Janeiro 2024</p>
                                    </div>
                                    <div class="text-right">
                                        <div class="text-2xl font-bold text-indigo-600" id="currentPlanPrice">R$ 19,90/mês</div>
                                        <div class="text-sm text-indigo-500">Próxima cobrança: 15/02/2024</div>
                                    </div>
                                </div>
                                
                                <div class="grid grid-cols-2 gap-4">
                                    <div class="text-center bg-white rounded-lg p-4">
                                        <div class="text-2xl font-bold text-green-600">R$ 156,80</div>
                                        <div class="text-sm text-gray-600">Economia Total</div>
                                    </div>
                                    <div class="text-center bg-white rounded-lg p-4">
                                        <div class="text-2xl font-bold text-blue-600">47</div>
                                        <div class="text-sm text-gray-600">Compras Otimizadas</div>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="space-y-4">
                                <button onclick="showPage('assinatura')" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-semibold transition-colors">
                                    Alterar Plano
                                </button>
                                <button onclick="cancelSubscription()" class="w-full bg-red-100 hover:bg-red-200 text-red-700 py-3 rounded-lg font-semibold transition-colors">
                                    Cancelar Assinatura
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Histórico Section -->
                    <div id="account-historico" class="account-section hidden">
                        <div class="premium-glass rounded-2xl p-8">
                            <h2 class="text-2xl font-bold text-slate-800 mb-6">Histórico de Compras</h2>
                            
                            <div class="space-y-4">
                                <div class="bg-white rounded-lg p-4 border border-gray-200">
                                    <div class="flex justify-between items-start mb-2">
                                        <div>
                                            <h4 class="font-semibold text-gray-800">Compra em Bahamas São Mateus</h4>
                                            <p class="text-sm text-gray-600">15 de Janeiro, 2024</p>
                                        </div>
                                        <div class="text-right">
                                            <div class="font-bold text-green-600">R$ 87,50</div>
                                            <div class="text-xs text-green-500">Economizou R$ 12,30</div>
                                        </div>
                                    </div>
                                    <div class="text-sm text-gray-600">
                                        8 produtos • Rota otimizada • 1 parada
                                    </div>
                                </div>
                                
                                <div class="bg-white rounded-lg p-4 border border-gray-200">
                                    <div class="flex justify-between items-start mb-2">
                                        <div>
                                            <h4 class="font-semibold text-gray-800">Compra em Extra Benfica</h4>
                                            <p class="text-sm text-gray-600">12 de Janeiro, 2024</p>
                                        </div>
                                        <div class="text-right">
                                            <div class="font-bold text-green-600">R$ 156,20</div>
                                            <div class="text-xs text-green-500">Economizou R$ 23,80</div>
                                        </div>
                                    </div>
                                    <div class="text-sm text-gray-600">
                                        15 produtos • Rota otimizada • 2 paradas
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Alertas Section -->
                    <div id="account-alertas" class="account-section hidden">
                        <div class="premium-glass rounded-2xl p-8">
                            <h2 class="text-2xl font-bold text-slate-800 mb-6">Meus Alertas de Preço</h2>
                            
                            <div class="space-y-4">
                                <div class="bg-white rounded-lg p-4 border border-gray-200">
                                    <div class="flex justify-between items-start">
                                        <div>
                                            <h4 class="font-semibold text-gray-800">Coca-Cola 2L - Marca Premium</h4>
                                            <p class="text-sm text-gray-600">Alertar quando ≤ R$ 6,50</p>
                                            <p class="text-xs text-blue-600">Preço atual: R$ 7,50</p>
                                        </div>
                                        <button onclick="removeAlert(1)" class="text-red-500 hover:text-red-700">
                                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
                                            </svg>
                                        </button>
                                    </div>
                                </div>
                                
                                <div class="bg-green-50 rounded-lg p-4 border border-green-200">
                                    <div class="flex justify-between items-start">
                                        <div>
                                            <h4 class="font-semibold text-green-800">🔔 Arroz 5kg - Marca Nacional</h4>
                                            <p class="text-sm text-green-600">ALERTA ATIVO! Preço baixou para R$ 18,90</p>
                                            <p class="text-xs text-green-500">Seu alerta: ≤ R$ 19,00</p>
                                        </div>
                                        <button onclick="viewAlert(2)" class="bg-green-600 text-white px-3 py-1 rounded text-sm font-semibold">
                                            Ver Oferta
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Configurações Section -->
                    <div id="account-configuracoes" class="account-section hidden">
                        <div class="premium-glass rounded-2xl p-8">
                            <h2 class="text-2xl font-bold text-slate-800 mb-6">Configurações</h2>
                            
                            <div class="space-y-6">
                                <div>
                                    <h3 class="text-lg font-semibold text-slate-800 mb-4">Notificações</h3>
                                    <div class="space-y-3">
                                        <label class="flex items-center">
                                            <input type="checkbox" checked class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                                            <span class="ml-3 text-slate-700">Alertas de preço por e-mail</span>
                                        </label>
                                        <label class="flex items-center">
                                            <input type="checkbox" checked class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                                            <span class="ml-3 text-slate-700">Promoções e ofertas especiais</span>
                                        </label>
                                        <label class="flex items-center">
                                            <input type="checkbox" class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                                            <span class="ml-3 text-slate-700">SMS (apenas Premium/+Saudável)</span>
                                        </label>
                                    </div>
                                </div>
                                
                                <div>
                                    <h3 class="text-lg font-semibold text-slate-800 mb-4">Privacidade</h3>
                                    <div class="space-y-3">
                                        <label class="flex items-center">
                                            <input type="checkbox" checked class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                                            <span class="ml-3 text-slate-700">Permitir análise de hábitos de compra</span>
                                        </label>
                                        <label class="flex items-center">
                                            <input type="checkbox" class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                                            <span class="ml-3 text-slate-700">Compartilhar dados para pesquisas</span>
                                        </label>
                                    </div>
                                </div>
                                
                                <button onclick="saveSettings()" class="premium-button text-white px-6 py-3 rounded-lg font-semibold">
                                    Salvar Configurações
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- PRIVACIDADE PAGE -->
    <div id="privacidade" class="page-section">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center mb-16">
                <h1 class="text-5xl font-bold text-slate-800 mb-6">Política de Privacidade</h1>
                <p class="text-xl text-slate-600">Última atualização: Janeiro de 2024</p>
            </div>

            <div class="premium-glass rounded-2xl p-8 space-y-8">
                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">1. Informações que Coletamos</h2>
                    <p class="text-slate-600 leading-relaxed mb-4">
                        Coletamos as seguintes informações:
                    </p>
                    <ul class="list-disc list-inside text-slate-600 space-y-2">
                        <li>Informações de cadastro (nome, email, telefone)</li>
                        <li>Dados de localização para otimização de rotas</li>
                        <li>Histórico de buscas e preferências de compra</li>
                        <li>Informações de uso da plataforma</li>
                    </ul>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">2. Como Usamos suas Informações</h2>
                    <p class="text-slate-600 leading-relaxed mb-4">
                        Utilizamos suas informações para:
                    </p>
                    <ul class="list-disc list-inside text-slate-600 space-y-2">
                        <li>Fornecer comparações de preços personalizadas</li>
                        <li>Otimizar rotas de compras</li>
                        <li>Enviar alertas de promoções relevantes</li>
                        <li>Melhorar nossos serviços</li>
                        <li>Comunicar atualizações importantes</li>
                    </ul>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">3. Compartilhamento de Dados</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Não vendemos, alugamos ou compartilhamos suas informações pessoais com terceiros para fins comerciais. Podemos compartilhar dados apenas quando necessário para fornecer nossos serviços ou quando exigido por lei.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">4. Segurança dos Dados</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Implementamos medidas de segurança técnicas e organizacionais para proteger suas informações contra acesso não autorizado, alteração, divulgação ou destruição.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">5. Seus Direitos</h2>
                    <p class="text-slate-600 leading-relaxed mb-4">
                        Você tem o direito de:
                    </p>
                    <ul class="list-disc list-inside text-slate-600 space-y-2">
                        <li>Acessar suas informações pessoais</li>
                        <li>Corrigir dados incorretos</li>
                        <li>Solicitar a exclusão de seus dados</li>
                        <li>Revogar consentimentos</li>
                        <li>Portabilidade de dados</li>
                    </ul>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">6. Cookies</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Utilizamos cookies para melhorar sua experiência, personalizar conteúdo e analisar o uso de nossa plataforma. Você pode gerenciar suas preferências de cookies nas configurações do navegador.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">7. Retenção de Dados</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Mantemos suas informações pelo tempo necessário para fornecer nossos serviços e cumprir obrigações legais. Dados inativos são excluídos periodicamente.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">8. Alterações na Política</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Podemos atualizar esta política periodicamente. Notificaremos sobre mudanças significativas através da plataforma ou por email.
                    </p>
                </section>

                <section>
                    <h2 class="text-2xl font-bold text-slate-800 mb-4">9. Contato</h2>
                    <p class="text-slate-600 leading-relaxed">
                        Para questões sobre privacidade, entre em contato: privacidade@compraboajf.com.br ou (32) 3025-1234.
                    </p>
                </section>
            </div>
        </div>
    </div>

    <!-- Login Modal -->
    <div id="loginModal" class="modal">
        <div class="premium-glass rounded-2xl p-8 max-w-md w-full mx-4">
            <div class="text-center mb-6">
                <h3 class="text-2xl font-bold text-slate-800 mb-2">Entrar na sua conta</h3>
                <p class="text-slate-600">Acesse sua conta para continuar economizando</p>
            </div>
            
            <form onsubmit="handleLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">E-mail</label>
                    <input type="email" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="seu@email.com">
                </div>
                <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Senha</label>
                    <input type="password" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Sua senha">
                </div>
                <div class="flex items-center justify-between">
                    <label class="flex items-center">
                        <input type="checkbox" class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                        <span class="ml-2 text-sm text-slate-600">Lembrar de mim</span>
                    </label>
                    <a href="#" class="text-sm text-indigo-600 hover:text-indigo-500">Esqueceu a senha?</a>
                </div>
                <button type="submit" class="w-full premium-button text-white py-3 rounded-lg font-semibold">
                    Entrar
                </button>
            </form>
            
            <div class="mt-6 text-center">
                <p class="text-slate-600">Não tem conta? 
                    <button onclick="showSignupModal()" class="text-indigo-600 hover:text-indigo-500 font-semibold">Criar conta</button>
                </p>
            </div>
            
            <button onclick="closeModal('loginModal')" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                </svg>
            </button>
        </div>
    </div>

    <!-- Signup Modal -->
    <div id="signupModal" class="modal">
        <div class="premium-glass rounded-2xl p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <div class="text-center mb-6">
                <h3 class="text-2xl font-bold text-slate-800 mb-2">Criar sua conta</h3>
                <p class="text-slate-600">Comece a economizar hoje mesmo com 7 dias grátis</p>
            </div>
            
            <form onsubmit="handleSignup(event)" class="space-y-6">
                <!-- Dados Pessoais -->
                <div class="bg-gray-50 rounded-xl p-6">
                    <h4 class="font-bold text-slate-800 mb-4 flex items-center">
                        <svg class="w-5 h-5 mr-2 text-indigo-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/>
                        </svg>
                        Dados Pessoais
                    </h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Nome completo *</label>
                            <input type="text" name="fullName" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Seu nome completo">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">CPF *</label>
                            <input type="text" name="cpf" required maxlength="14" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="000.000.000-00" oninput="formatCPF(this)">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">E-mail *</label>
                            <input type="email" name="email" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="seu@email.com">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Senha *</label>
                            <input type="password" name="password" required minlength="6" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Mínimo 6 caracteres">
                        </div>
                    </div>
                </div>

                <!-- Seleção de Plano -->
                <div class="bg-gradient-to-r from-indigo-50 to-purple-50 rounded-xl p-6">
                    <h4 class="font-bold text-slate-800 mb-4 flex items-center">
                        <svg class="w-5 h-5 mr-2 text-indigo-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
                        </svg>
                        Escolha seu Plano *
                    </h4>
                    <p class="text-sm text-slate-600 mb-4">Todos os planos incluem 7 dias de teste grátis. Cancele quando quiser.</p>
                    
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                        <!-- Plano Pro -->
                        <label class="cursor-pointer">
                            <input type="radio" name="selectedPlan" value="pro" required class="sr-only">
                            <div class="plan-option border-2 border-gray-200 rounded-xl p-6 hover:border-blue-300 transition-all duration-300">
                                <div class="text-center mb-4">
                                    <div class="w-16 h-16 bg-blue-100 rounded-xl flex items-center justify-center mx-auto mb-3">
                                        <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
                                        </svg>
                                    </div>
                                    <h5 class="text-2xl font-bold text-slate-800 mb-2">Pro</h5>
                                    <p class="text-sm text-slate-600 mb-4">Todas as funcionalidades essenciais</p>
                                    <div class="text-4xl font-bold text-blue-600 mb-2">R$ 9,90<span class="text-lg text-slate-600">/mês</span></div>
                                </div>
                                
                                <div class="text-left space-y-3">
                                    <div class="bg-green-50 rounded-lg p-3">
                                        <h6 class="font-semibold text-green-800 mb-2 text-sm">🎯 Pesquisa em Tempo Real</h6>
                                        <ul class="text-xs text-green-700 space-y-1">
                                            <li>• Todos os 70+ mercados cadastrados</li>
                                            <li>• Preço, distância e última atualização</li>
                                            <li>• Ordenação: preço, proximidade, custo-benefício</li>
                                        </ul>
                                    </div>
                                    
                                    <div class="bg-blue-50 rounded-lg p-3">
                                        <h6 class="font-semibold text-blue-800 mb-2 text-sm">🏆 Ranking por Produto</h6>
                                        <ul class="text-xs text-blue-700 space-y-1">
                                            <li>• Badge "#1 em preço"</li>
                                            <li>• "#2 em distância (750m)"</li>
                                            <li>• Comparação completa entre lojas</li>
                                        </ul>
                                    </div>
                                    
                                    <div class="bg-purple-50 rounded-lg p-3">
                                        <h6 class="font-semibold text-purple-800 mb-2 text-sm">🛒 Carrinho Inteligente</h6>
                                        <ul class="text-xs text-purple-700 space-y-1">
                                            <li>• Otimização de rotas de compras</li>
                                            <li>• Menor preço total vs mais próximo</li>
                                            <li>• Opção custo-benefício equilibrada</li>
                                        </ul>
                                    </div>
                                    
                                    <div class="bg-orange-50 rounded-lg p-3">
                                        <h6 class="font-semibold text-orange-800 mb-2 text-sm">📊 Histórico e Alertas</h6>
                                        <ul class="text-xs text-orange-700 space-y-1">
                                            <li>• Curva de preço (30 dias)</li>
                                            <li>• Alerta de queda de preço</li>
                                            <li>• Análise de tendências</li>
                                        </ul>
                                    </div>
                                </div>
                            </div>
                        </label>

                        <!-- Plano Premium -->
                        <label class="cursor-pointer">
                            <input type="radio" name="selectedPlan" value="premium" required class="sr-only">
                            <div class="plan-option border-2 border-gray-200 rounded-xl p-6 hover:border-indigo-300 transition-all duration-300 relative">
                                <div class="absolute -top-3 left-1/2 transform -translate-x-1/2 bg-indigo-600 text-white px-4 py-1 rounded-full text-xs font-bold">
                                    MAIS POPULAR
                                </div>
                                <div class="text-center mb-4">
                                    <div class="w-16 h-16 bg-indigo-100 rounded-xl flex items-center justify-center mx-auto mb-3">
                                        <svg class="w-8 h-8 text-indigo-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
                                        </svg>
                                    </div>
                                    <h5 class="text-2xl font-bold text-slate-800 mb-2">Premium</h5>
                                    <p class="text-sm text-slate-600 mb-4">Tudo do Pro + Sorteio Mensal</p>
                                    <div class="text-4xl font-bold text-indigo-600 mb-2">R$ 19,90<span class="text-lg text-slate-600">/mês</span></div>
                                </div>
                                
                                <div class="text-left space-y-3">
                                    <div class="bg-green-50 rounded-lg p-3">
                                        <p class="font-semibold text-green-800 text-sm">✅ Todas as funcionalidades do Pro +</p>
                                    </div>
                                    
                                    <div class="bg-yellow-50 rounded-lg p-3 border-2 border-yellow-300">
                                        <h6 class="font-semibold text-yellow-800 mb-2 text-sm">🎁 Sorteio Mensal Exclusivo</h6>
                                        <ul class="text-xs text-yellow-700 space-y-1">
                                            <li>• <strong>R$ 1.000 em compras</strong> todo mês</li>
                                            <li>• Participação automática</li>
                                            <li>• Sorteio no último dia do mês</li>
                                            <li>• Válido apenas para assinantes ativos</li>
                                        </ul>
                                    </div>
                                    
                                    <div class="bg-indigo-50 rounded-lg p-3">
                                        <h6 class="font-semibold text-indigo-800 mb-2 text-sm">🏆 Vantagens Premium</h6>
                                        <ul class="text-xs text-indigo-700 space-y-1">
                                            <li>• Suporte prioritário</li>
                                            <li>• Acesso antecipado a novidades</li>
                                            <li>• Relatórios de economia personalizados</li>
                                        </ul>
                                    </div>
                                    
                                    <div class="bg-pink-50 rounded-lg p-3">
                                        <h6 class="font-semibold text-pink-800 mb-2 text-sm">🤝 Trocas Sugeridas Patrocinadas</h6>
                                        <ul class="text-xs text-pink-700 space-y-1">
                                            <li>• Melhor custo por quantidade</li>
                                            <li>• Selo "Sugestão do parceiro"</li>
                                            <li>• Ofertas exclusivas de marcas</li>
                                        </ul>
                                    </div>
                                    
                                    <div class="text-xs text-slate-500 bg-gray-50 rounded-lg p-3">
                                        <p class="font-semibold mb-1 text-yellow-700">⚠️ Importante:</p>
                                        <p>A participação no sorteio mensal está condicionada à manutenção da assinatura ativa.</p>
                                    </div>
                                </div>
                            </div>
                        </label>


                    </div>
                </div>

                <!-- Forma de Pagamento -->
                <div class="bg-green-50 rounded-xl p-6">
                    <h4 class="font-bold text-slate-800 mb-4 flex items-center">
                        <svg class="w-5 h-5 mr-2 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z"/>
                        </svg>
                        Forma de Pagamento *
                    </h4>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                        <label class="cursor-pointer">
                            <input type="radio" name="paymentMethod" value="credit" required class="sr-only">
                            <div class="payment-option border-2 border-gray-200 rounded-xl p-4 hover:border-green-300 transition-all duration-300">
                                <div class="flex items-center space-x-3">
                                    <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center">
                                        <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z"/>
                                        </svg>
                                    </div>
                                    <div>
                                        <h5 class="font-semibold text-slate-800">Cartão de Crédito</h5>
                                        <p class="text-sm text-slate-600">Cobrança mensal automática</p>
                                        <p class="text-xs text-green-600 font-semibold">Mais prático</p>
                                    </div>
                                </div>
                            </div>
                        </label>

                        <label class="cursor-pointer">
                            <input type="radio" name="paymentMethod" value="pix" required class="sr-only">
                            <div class="payment-option border-2 border-gray-200 rounded-xl p-4 hover:border-green-300 transition-all duration-300">
                                <div class="flex items-center space-x-3">
                                    <div class="w-12 h-12 bg-green-100 rounded-xl flex items-center justify-center">
                                        <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"/>
                                        </svg>
                                    </div>
                                    <div>
                                        <h5 class="font-semibold text-slate-800">PIX</h5>
                                        <p class="text-sm text-slate-600">Pagamento mensal via PIX</p>
                                        <p class="text-xs text-green-600 font-semibold">Sem taxas</p>
                                    </div>
                                </div>
                            </div>
                        </label>
                    </div>

                    <!-- Campos do Cartão (aparecem quando cartão é selecionado) -->
                    <div id="creditCardFields" class="hidden space-y-4">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-slate-700 mb-2">Número do Cartão</label>
                                <input type="text" name="cardNumber" maxlength="19" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent" placeholder="0000 0000 0000 0000" oninput="formatCardNumber(this)">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-slate-700 mb-2">Nome no Cartão</label>
                                <input type="text" name="cardName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent" placeholder="Como está no cartão">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-slate-700 mb-2">Validade</label>
                                <input type="text" name="cardExpiry" maxlength="5" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent" placeholder="MM/AA" oninput="formatExpiry(this)">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-slate-700 mb-2">CVV</label>
                                <input type="text" name="cardCVV" maxlength="4" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent" placeholder="000">
                            </div>
                        </div>
                    </div>

                    <!-- Informação PIX -->
                    <div id="pixInfo" class="hidden bg-green-100 rounded-lg p-4">
                        <div class="flex items-center space-x-2 mb-2">
                            <svg class="w-5 h-5 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
                            </svg>
                            <h5 class="font-semibold text-green-800">Como funciona o PIX</h5>
                        </div>
                        <p class="text-sm text-green-700">
                            Todo mês você receberá um e-mail com o código PIX para pagamento. 
                            Você tem 5 dias para efetuar o pagamento e manter sua assinatura ativa.
                        </p>
                    </div>
                </div>

                <!-- Resumo da Assinatura -->
                <div id="subscriptionSummary" class="bg-slate-50 rounded-xl p-6">
                    <h4 class="font-bold text-slate-800 mb-4">📋 Resumo da Assinatura</h4>
                    <div class="space-y-2 text-sm">
                        <div class="flex justify-between">
                            <span class="text-slate-600">Plano selecionado:</span>
                            <span id="selectedPlanName" class="font-semibold text-slate-800">Selecione um plano</span>
                        </div>
                        <div class="flex justify-between">
                            <span class="text-slate-600">Valor mensal:</span>
                            <span id="selectedPlanPrice" class="font-semibold text-slate-800">R$ 0,00</span>
                        </div>
                        <div class="flex justify-between">
                            <span class="text-slate-600">Teste grátis:</span>
                            <span class="font-semibold text-green-600">7 dias</span>
                        </div>
                        <div class="flex justify-between">
                            <span class="text-slate-600">Primeira cobrança:</span>
                            <span id="firstBilling" class="font-semibold text-slate-800">-</span>
                        </div>
                        <hr class="my-3">
                        <div class="flex justify-between text-lg">
                            <span class="font-bold text-slate-800">Hoje você paga:</span>
                            <span class="font-bold text-green-600">R$ 0,00</span>
                        </div>
                    </div>
                </div>

                <!-- Termos -->
                <div>
                    <label class="flex items-start">
                        <input type="checkbox" required class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500 mt-1">
                        <span class="ml-2 text-sm text-slate-600">
                            Aceito os <a href="#" onclick="showPage('termos')" class="text-indigo-600 hover:text-indigo-500 font-semibold">termos de uso</a>, 
                            <a href="#" onclick="showPage('privacidade')" class="text-indigo-600 hover:text-indigo-500 font-semibold">política de privacidade</a> 
                            e autorizo a cobrança automática conforme o plano escolhido.
                        </span>
                    </label>
                </div>

                <button type="submit" class="w-full premium-button text-white py-4 rounded-lg font-bold text-lg">
                    🎉 Começar Teste Grátis de 7 Dias
                </button>
            </form>
            
            <div class="mt-6 text-center">
                <p class="text-slate-600">Já tem conta? 
                    <button onclick="showLoginModal()" class="text-indigo-600 hover:text-indigo-500 font-semibold">Entrar</button>
                </p>
                <p class="text-xs text-slate-500 mt-2">
                    🔒 Seus dados estão seguros. Cancele quando quiser sem taxas.
                </p>
            </div>
            
            <button onclick="closeModal('signupModal')" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                </svg>
            </button>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-slate-800 text-white py-12">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <div class="flex items-center space-x-3 mb-4">
                        <div class="w-10 h-10 premium-button rounded-lg flex items-center justify-center">
                            <svg class="w-6 h-6 text-white" viewBox="0 0 32 32" fill="none">
                                <!-- Modern Shopping Cart with Tech Elements -->
                                <!-- Cart Base -->
                                <path d="M6 8L8.5 8.5L10.5 20.5C10.7 21.3 11.4 22 12.2 22H24C24.8 22 25.5 21.3 25.7 20.5L27 14H11" 
                                      stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                
                                <!-- Tech Grid Pattern in Cart -->
                                <path d="M13 16H15M17 16H19M21 16H23M13 18H15M17 18H19M21 18H23" 
                                      stroke="currentColor" stroke-width="1" stroke-linecap="round" opacity="0.6"/>
                                
                                <!-- Digital Handle -->
                                <path d="M27 14C27.5 14 28 13.5 28 13V11C28 10.5 27.5 10 27 10H26" 
                                      stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                                
                                <!-- Wheels with Tech Design -->
                                <circle cx="14" cy="26" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
                                <circle cx="22" cy="26" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
                                
                                <!-- Tech Dots in Wheels -->
                                <circle cx="14" cy="26" r="0.5" fill="currentColor"/>
                                <circle cx="22" cy="26" r="0.5" fill="currentColor"/>
                                
                                <!-- Digital Signal Lines -->
                                <path d="M4 6L6 8M4 8L6 6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" opacity="0.7"/>
                                
                                <!-- Smart Badge -->
                                <circle cx="24" cy="8" r="3" fill="currentColor" opacity="0.9"/>
                                <path d="M22.5 8L23.5 9L25.5 7" stroke="white" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
                            </svg>
                        </div>
                        <div>
                            <h3 class="font-bold text-lg">Compra Boa JF</h3>
                            <p class="text-sm text-gray-400">Juiz de Fora</p>
                        </div>
                    </div>
                    <p class="text-gray-400 text-sm leading-relaxed">
                        Compare preços em tempo real, economize tempo e dinheiro com nossa tecnologia avançada.
                    </p>
                </div>
                
                <div>
                    <h4 class="font-semibold mb-4">Produto</h4>
                    <ul class="space-y-2 text-sm text-gray-400">
                        <li><a href="#" onclick="showPage('como-funciona')" class="hover:text-white transition-colors">Como Funciona</a></li>
                        <li><a href="#" onclick="showPage('assinatura')" class="hover:text-white transition-colors">Planos</a></li>
                        <li><a href="#" onclick="showPage('parceiros')" class="hover:text-white transition-colors">Seja Parceiro</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="font-semibold mb-4">Suporte</h4>
                    <ul class="space-y-2 text-sm text-gray-400">
                        <li><a href="#" onclick="showPage('contato')" class="hover:text-white transition-colors">Contato</a></li>
                        <li><a href="#" onclick="showPage('assinatura')" class="hover:text-white transition-colors">FAQ</a></li>
                        <li><a href="#" class="hover:text-white transition-colors">Status</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="font-semibold mb-4">Legal</h4>
                    <ul class="space-y-2 text-sm text-gray-400">
                        <li><a href="#" onclick="showPage('termos')" class="hover:text-white transition-colors">Termos de Uso</a></li>
                        <li><a href="#" onclick="showPage('privacidade')" class="hover:text-white transition-colors">Política de Privacidade</a></li>
                        <li><a href="#" class="hover:text-white transition-colors">LGPD</a></li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-gray-700 mt-8 pt-8 text-center text-sm text-gray-400">
                <p>&copy; 2024 Compra Boa JF. Todos os direitos reservados. Desenvolvido com ❤️ em Juiz de Fora.</p>
            </div>
        </div>
    </footer>

    <script>
        // Firebase Configuration (DEMO MODE - Simulação sem Firebase real)
        const firebaseConfig = {
            // Configuração será adicionada quando você configurar o Firebase
            demo: true
        };

        // Demo Firebase simulation
        const auth = {
            createUserWithEmailAndPassword: (email, password) => {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve({
                            user: {
                                uid: 'demo_' + Date.now(),
                                email: email
                            }
                        });
                    }, 1000);
                });
            },
            signInWithEmailAndPassword: (email, password) => {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        // Simulate login check
                        const savedUsers = JSON.parse(localStorage.getItem('demoUsers') || '[]');
                        const user = savedUsers.find(u => u.email === email && u.password === password);
                        
                        if (user) {
                            resolve({
                                user: {
                                    uid: user.uid,
                                    email: user.email
                                }
                            });
                        } else {
                            reject({ code: 'auth/user-not-found' });
                        }
                    }, 1000);
                });
            },
            signOut: () => {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        currentUser = null;
                        isLoggedIn = false;
                        resolve();
                    }, 500);
                });
            },
            onAuthStateChanged: (callback) => {
                // Simulate auth state
                setTimeout(() => {
                    const savedUser = JSON.parse(localStorage.getItem('currentDemoUser') || 'null');
                    callback(savedUser);
                }, 100);
            }
        };

        const db = {
            collection: (name) => ({
                doc: (id) => ({
                    set: (data) => {
                        return new Promise((resolve) => {
                            setTimeout(() => {
                                // Save to localStorage for demo
                                const key = `demo_${name}_${id}`;
                                localStorage.setItem(key, JSON.stringify(data));
                                resolve();
                            }, 500);
                        });
                    },
                    get: () => {
                        return new Promise((resolve) => {
                            setTimeout(() => {
                                const key = `demo_${name}_${id}`;
                                const data = localStorage.getItem(key);
                                resolve({
                                    exists: !!data,
                                    data: () => data ? JSON.parse(data) : null
                                });
                            }, 300);
                        });
                    },
                    update: (data) => {
                        return new Promise((resolve) => {
                            setTimeout(() => {
                                const key = `demo_${name}_${id}`;
                                const existing = localStorage.getItem(key);
                                if (existing) {
                                    const updated = { ...JSON.parse(existing), ...data };
                                    localStorage.setItem(key, JSON.stringify(updated));
                                }
                                resolve();
                            }, 300);
                        });
                    }
                }),
                add: (data) => {
                    return new Promise((resolve) => {
                        setTimeout(() => {
                            const id = 'demo_' + Date.now();
                            const key = `demo_${name}_${id}`;
                            localStorage.setItem(key, JSON.stringify(data));
                            resolve({ id });
                        }, 300);
                    });
                }
            })
        };

        // EmailJS Configuration (DEMO MODE)
        const emailjs = {
            init: () => {},
            send: (serviceId, templateId, params) => {
                return new Promise((resolve) => {
                    console.log('📧 Email simulado enviado:', params);
                    setTimeout(resolve, 1000);
                });
            }
        };

        // Global variables
        let currentUser = null;
        let cart = [];
        let isLoggedIn = false;
        let userSubscription = null;
        let mapAnimationInterval = null;

        // Page navigation
        function showPage(pageId) {
            // Hide all pages
            document.querySelectorAll('.page-section').forEach(page => {
                page.classList.remove('active');
            });
            
            // Show selected page
            const targetPage = document.getElementById(pageId);
            if (targetPage) {
                targetPage.classList.add('active');
            }
            
            // Update navigation
            document.querySelectorAll('.nav-link').forEach(link => {
                link.classList.remove('active');
            });
            
            // Find and activate the corresponding nav link
            const navLink = document.querySelector(`[onclick="showPage('${pageId}')"]`);
            if (navLink) {
                navLink.classList.add('active');
            }
            
            // Close mobile menu if open
            document.getElementById('mobileMenu').classList.add('hidden');
            
            // Close any open modals
            closeAllModals();
            
            // Scroll to top
            window.scrollTo(0, 0);
        }

        // Mobile menu toggle
        function toggleMobileMenu() {
            const mobileMenu = document.getElementById('mobileMenu');
            mobileMenu.classList.toggle('hidden');
        }

        // Modal functions
        function showLoginModal() {
            closeAllModals();
            document.getElementById('loginModal').classList.add('active');
        }

        function showSignupModal() {
            closeAllModals();
            document.getElementById('signupModal').classList.add('active');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
        }

        function closeAllModals() {
            document.querySelectorAll('.modal').forEach(modal => {
                modal.classList.remove('active');
            });
        }

        // Authentication Functions
        async function handleLogin(event) {
            event.preventDefault();
            const email = event.target.querySelector('input[type="email"]').value;
            const password = event.target.querySelector('input[type="password"]').value;
            
            showNotification('Entrando...', 'Verificando suas credenciais', 'info');
            
            try {
                const userCredential = await auth.signInWithEmailAndPassword(email, password);
                const user = userCredential.user;
                
                // Get user data from demo database
                const userDoc = await db.collection('users').doc(user.uid).get();
                if (userDoc.exists) {
                    const userData = userDoc.data();
                    
                    // Set current user in localStorage
                    localStorage.setItem('currentDemoUser', JSON.stringify({
                        uid: user.uid,
                        email: user.email
                    }));
                    
                    currentUser = {
                        uid: user.uid,
                        name: userData.fullName,
                        email: user.email,
                        plan: userData.selectedPlan || 'Pro',
                        paymentMethod: userData.paymentMethod,
                        createdAt: userData.createdAt,
                        savings: userData.totalSavings || 0,
                        isTrialActive: userData.isTrialActive || false,
                        trialEndsAt: userData.trialEndsAt
                    };
                    
                    isLoggedIn = true;
                    updateUserInterface();
                    closeModal('loginModal');
                    showNotification('Bem-vindo!', `Olá, ${currentUser.name}!`, 'success');
                    
                    // Load user's cart if exists
                    loadUserCart();
                } else {
                    throw { code: 'auth/user-not-found' };
                }
            } catch (error) {
                console.error('Login error:', error);
                let errorMessage = 'Erro ao fazer login';
                
                switch(error.code) {
                    case 'auth/user-not-found':
                        errorMessage = 'Usuário não encontrado';
                        break;
                    case 'auth/wrong-password':
                        errorMessage = 'Senha incorreta';
                        break;
                    case 'auth/invalid-email':
                        errorMessage = 'Email inválido';
                        break;
                    case 'auth/too-many-requests':
                        errorMessage = 'Muitas tentativas. Tente novamente mais tarde';
                        break;
                }
                
                showNotification('Erro', errorMessage, 'error');
            }
        }

        async function handleSignup(event) {
            event.preventDefault();
            const formData = new FormData(event.target);
            
            const name = formData.get('fullName');
            const cpf = formData.get('cpf');
            const email = formData.get('email');
            const password = formData.get('password');
            const selectedPlan = formData.get('selectedPlan');
            const paymentMethod = formData.get('paymentMethod');
            
            // Validate required fields
            if (!name || !cpf || !email || !password || !selectedPlan || !paymentMethod) {
                showNotification('Erro', 'Preencha todos os campos obrigatórios', 'error');
                return;
            }
            
            // Validate CPF format
            if (!isValidCPF(cpf)) {
                showNotification('Erro', 'CPF inválido. Verifique o formato.', 'error');
                return;
            }
            
            // If credit card is selected, validate card fields
            if (paymentMethod === 'credit') {
                const cardNumber = formData.get('cardNumber');
                const cardName = formData.get('cardName');
                const cardExpiry = formData.get('cardExpiry');
                const cardCVV = formData.get('cardCVV');
                
                if (!cardNumber || !cardName || !cardExpiry || !cardCVV) {
                    showNotification('Erro', 'Preencha todos os dados do cartão', 'error');
                    return;
                }
            }
            
            showNotification('Criando conta...', 'Processando seus dados', 'info');
            
            try {
                // Check if email already exists in demo mode
                const savedUsers = JSON.parse(localStorage.getItem('demoUsers') || '[]');
                if (savedUsers.find(u => u.email === email)) {
                    throw { code: 'auth/email-already-in-use' };
                }
                
                // Create user in Demo Auth
                const userCredential = await auth.createUserWithEmailAndPassword(email, password);
                const user = userCredential.user;
                
                const planNames = {
                    'pro': 'Pro',
                    'premium': 'Premium',
                    'saudavel': '+Saudável'
                };
                
                const planPrices = {
                    'pro': 9.90,
                    'premium': 19.90,
                    'saudavel': 29.90
                };
                
                // Prepare user data
                const userData = {
                    uid: user.uid,
                    fullName: name,
                    cpf: cpf,
                    email: email,
                    password: password, // Only for demo mode
                    selectedPlan: planNames[selectedPlan],
                    planPrice: planPrices[selectedPlan],
                    paymentMethod: paymentMethod,
                    isTrialActive: true,
                    trialEndsAt: new Date(Date.now() + 7 * 24 * 60 * 60 * 1000),
                    createdAt: new Date(),
                    totalSavings: 0,
                    status: 'trial',
                    lastLogin: new Date()
                };
                
                // Add payment method details if credit card
                if (paymentMethod === 'credit') {
                    userData.cardDetails = {
                        cardNumber: formData.get('cardNumber').replace(/\s/g, '').slice(-4), // Only last 4 digits
                        cardName: formData.get('cardName'),
                        cardExpiry: formData.get('cardExpiry')
                    };
                }
                
                // Save user data to demo database
                await db.collection('users').doc(user.uid).set(userData);
                
                // Save to demo users list
                savedUsers.push(userData);
                localStorage.setItem('demoUsers', JSON.stringify(savedUsers));
                
                // Set current user in localStorage
                localStorage.setItem('currentDemoUser', JSON.stringify({
                    uid: user.uid,
                    email: user.email
                }));
                
                // Update current user
                currentUser = {
                    uid: user.uid,
                    name: name,
                    email: email,
                    plan: planNames[selectedPlan],
                    paymentMethod: paymentMethod,
                    savings: 0,
                    isTrialActive: true,
                    trialEndsAt: userData.trialEndsAt,
                    createdAt: userData.createdAt
                };
                
                isLoggedIn = true;
                updateUserInterface();
                closeModal('signupModal');
                
                // Send welcome email (simulated)
                await sendWelcomeEmail(email, name, planNames[selectedPlan]);
                
                showNotification('Bem-vindo!', `Conta criada com sucesso! Plano ${planNames[selectedPlan]} ativo por 7 dias grátis.`, 'success');
                
                // Show trial information
                setTimeout(() => {
                    showNotification('Teste Grátis Ativo!', 'Aproveite 7 dias para testar todas as funcionalidades', 'info');
                }, 2000);
                
                // Log signup event for analytics
                await logUserEvent('signup', {
                    plan: selectedPlan,
                    paymentMethod: paymentMethod
                });
                
            } catch (error) {
                console.error('Signup error:', error);
                let errorMessage = 'Erro ao criar conta';
                
                switch(error.code) {
                    case 'auth/email-already-in-use':
                        errorMessage = 'Este email já está em uso';
                        break;
                    case 'auth/weak-password':
                        errorMessage = 'Senha muito fraca. Use pelo menos 6 caracteres';
                        break;
                    case 'auth/invalid-email':
                        errorMessage = 'Email inválido';
                        break;
                }
                
                showNotification('Erro', errorMessage, 'error');
            }
        }

        async function logout() {
            try {
                await auth.signOut();
                
                // Clear localStorage
                localStorage.removeItem('currentDemoUser');
                
                currentUser = null;
                isLoggedIn = false;
                cart = [];
                updateUserInterface();
                updateCartDisplay();
                showNotification('Até logo!', 'Logout realizado com sucesso', 'info');
            } catch (error) {
                console.error('Logout error:', error);
                showNotification('Erro', 'Erro ao fazer logout', 'error');
            }
        }

        // Email Functions
        async function sendWelcomeEmail(email, name, plan) {
            try {
                const templateParams = {
                    to_email: email,
                    to_name: name,
                    plan_name: plan,
                    trial_days: 7,
                    company_name: 'Compra Boa JF'
                };

                await emailjs.send('YOUR_SERVICE_ID', 'welcome_template', templateParams);
                console.log('Welcome email sent successfully');
            } catch (error) {
                console.error('Error sending welcome email:', error);
            }
        }

        async function sendPaymentConfirmationEmail(email, name, plan, amount) {
            try {
                const templateParams = {
                    to_email: email,
                    to_name: name,
                    plan_name: plan,
                    amount: amount,
                    company_name: 'Compra Boa JF'
                };

                await emailjs.send('YOUR_SERVICE_ID', 'payment_confirmation_template', templateParams);
                console.log('Payment confirmation email sent successfully');
            } catch (error) {
                console.error('Error sending payment confirmation email:', error);
            }
        }

        // Analytics Functions
        async function logUserEvent(eventType, eventData = {}) {
            try {
                if (currentUser) {
                    await db.collection('analytics').add({
                        userId: currentUser.uid,
                        eventType: eventType,
                        eventData: eventData,
                        timestamp: new Date(),
                        userAgent: navigator.userAgent,
                        url: window.location.href
                    });
                }
            } catch (error) {
                console.error('Error logging event:', error);
            }
        }

        // Cart Functions with Firebase
        async function loadUserCart() {
            if (!currentUser) return;
            
            try {
                const cartDoc = await db.collection('carts').doc(currentUser.uid).get();
                if (cartDoc.exists) {
                    cart = cartDoc.data().items || [];
                    updateCartDisplay();
                }
            } catch (error) {
                console.error('Error loading cart:', error);
            }
        }

        async function saveUserCart() {
            if (!currentUser) return;
            
            try {
                await db.collection('carts').doc(currentUser.uid).set({
                    items: cart,
                    updatedAt: new Date()
                });
            } catch (error) {
                console.error('Error saving cart:', error);
            }
        }

        // Auth State Observer
        auth.onAuthStateChanged(async (user) => {
            if (user) {
                // User is signed in
                try {
                    const userDoc = await db.collection('users').doc(user.uid).get();
                    if (userDoc.exists) {
                        const userData = userDoc.data();
                        currentUser = {
                            uid: user.uid,
                            name: userData.fullName,
                            email: user.email,
                            plan: userData.selectedPlan || 'Pro',
                            paymentMethod: userData.paymentMethod,
                            createdAt: userData.createdAt,
                            savings: userData.totalSavings || 0,
                            isTrialActive: userData.isTrialActive || false,
                            trialEndsAt: userData.trialEndsAt
                        };
                        
                        isLoggedIn = true;
                        updateUserInterface();
                        loadUserCart();
                        
                        // Update last login
                        await db.collection('users').doc(user.uid).update({
                            lastLogin: new Date()
                        });
                    }
                } catch (error) {
                    console.error('Error loading user data:', error);
                }
            } else {
                // User is signed out
                currentUser = null;
                isLoggedIn = false;
                cart = [];
                updateUserInterface();
                updateCartDisplay();
            }
        });

        function updateUserInterface() {
            const notLoggedIn = document.getElementById('notLoggedIn');
            const loggedIn = document.getElementById('loggedIn');
            const minhaContaLink = document.getElementById('minhaContaLink');
            const cartCount = document.getElementById('cartCount');
            
            console.log('🔧 updateUserInterface called');
            console.log('isLoggedIn:', isLoggedIn);
            console.log('currentUser:', currentUser);
            
            if (isLoggedIn && currentUser) {
                console.log('✅ User is logged in, showing elements');
                
                // Show logged in elements
                if (notLoggedIn) notLoggedIn.classList.add('hidden');
                if (loggedIn) {
                    loggedIn.classList.remove('hidden');
                    loggedIn.style.display = 'flex';
                }
                
                // FORCE SHOW "Minha Conta" link
                if (minhaContaLink) {
                    minhaContaLink.classList.remove('hidden');
                    minhaContaLink.style.display = 'block';
                    minhaContaLink.style.visibility = 'visible';
                    console.log('✅ Minha Conta link shown');
                }
                
                // FORCE SHOW cart icon and count - MULTIPLE WAYS
                if (cartCount) {
                    cartCount.classList.remove('hidden');
                    cartCount.style.display = 'flex';
                    cartCount.style.visibility = 'visible';
                    cartCount.style.opacity = '1';
                    cartCount.textContent = cart.length;
                    
                    // Also force show the parent cart button
                    const cartButton = cartCount.closest('button');
                    if (cartButton) {
                        cartButton.classList.remove('hidden');
                        cartButton.style.display = 'block';
                        cartButton.style.visibility = 'visible';
                    }
                    
                    // Force show the entire cart container
                    const cartContainer = cartCount.closest('.relative');
                    if (cartContainer) {
                        cartContainer.classList.remove('hidden');
                        cartContainer.style.display = 'block';
                        cartContainer.style.visibility = 'visible';
                    }
                    
                    console.log('✅ Cart icon forced to show with count:', cart.length);
                }
                
                // Update user info in header
                const userName = document.getElementById('userName');
                const userInitials = document.getElementById('userInitials');
                const userPlan = document.getElementById('userPlan');
                const userSavings = document.getElementById('userSavings');
                
                if (userName) userName.textContent = currentUser.name;
                if (userInitials) userInitials.textContent = currentUser.name.charAt(0).toUpperCase();
                if (userPlan) userPlan.textContent = currentUser.plan;
                if (userSavings) userSavings.textContent = `R$ ${currentUser.savings.toFixed(2)}`;
                
                // Update user info in Minha Conta page
                const userNameLarge = document.getElementById('userNameLarge');
                const userEmailLarge = document.getElementById('userEmailLarge');
                const userInitialsLarge = document.getElementById('userInitialsLarge');
                
                if (userNameLarge) userNameLarge.textContent = currentUser.name;
                if (userEmailLarge) userEmailLarge.textContent = currentUser.email;
                if (userInitialsLarge) userInitialsLarge.textContent = currentUser.name.charAt(0).toUpperCase();
                
                // Update profile form fields
                const profileName = document.getElementById('profileName');
                const profileEmail = document.getElementById('profileEmail');
                const profileCPF = document.getElementById('profileCPF');
                
                if (profileName) profileName.value = currentUser.name;
                if (profileEmail) profileEmail.value = currentUser.email;
                if (profileCPF) profileCPF.value = currentUser.cpf || '000.000.000-00';
                
                // Update subscription info
                const currentPlanName = document.getElementById('currentPlanName');
                const currentPlanPrice = document.getElementById('currentPlanPrice');
                
                if (currentPlanName) currentPlanName.textContent = `Plano ${currentUser.plan}`;
                if (currentPlanPrice) {
                    const prices = { 'Pro': 9.90, 'Premium': 19.90, '+Saudável': 29.90 };
                    currentPlanPrice.textContent = `R$ ${prices[currentUser.plan] || 9.90}/mês`;
                }
                
                // Update cart display
                updateCartDisplay();

            } else {
                console.log('❌ User not logged in, hiding elements');
                if (notLoggedIn) notLoggedIn.classList.remove('hidden');
                if (loggedIn) loggedIn.classList.add('hidden');
                if (minhaContaLink) minhaContaLink.classList.add('hidden');
                
                // Hide cart when not logged in
                if (cartCount) {
                    cartCount.classList.add('hidden');
                    cartCount.style.display = 'none';
                }
            }
        }

        // Product search
        function startComparison() {
            if (!isLoggedIn) {
                showSignupModal();
                return;
            }
            
            // Scroll to search section
            document.getElementById('productSearch').scrollIntoView({ behavior: 'smooth' });
            document.getElementById('productSearchInput').focus();
        }

        function handleSearchKeyPress(event) {
            if (event.key === 'Enter') {
                searchProducts();
            }
        }

        function searchProducts() {
            if (!isLoggedIn) {
                showSignupModal();
                return;
            }
            
            const query = document.getElementById('productSearchInput').value.trim();
            if (!query) {
                showNotification('Atenção', 'Digite um produto para buscar', 'warning');
                return;
            }
            
            // Show loading
            showNotification('Buscando...', 'Procurando os melhores preços', 'info');
            
            // Simulate search - cart stays open if it was open
            setTimeout(() => {
                displaySearchResults(query);
                // Maintain cart state after search
                if (isCartOpen) {
                    openCart();
                }
            }, 1500);
        }

        function searchByCategory(category) {
            if (!isLoggedIn) {
                showSignupModal();
                return;
            }
            
            const categoryNames = {
                'bebidas': 'Bebidas',
                'laticinios': 'Laticínios',
                'carnes': 'Carnes',
                'cereais': 'Cereais'
            };
            
            document.getElementById('productSearchInput').value = categoryNames[category];
            
            // Remember cart state before search
            const wasCartOpen = isCartOpen;
            
            searchProducts();
            
            // Restore cart state after search
            setTimeout(() => {
                if (wasCartOpen) {
                    openCart();
                }
            }, 1600);
        }

        function displaySearchResults(query) {
            const resultsContainer = document.getElementById('searchResults');
            const resultsCount = document.getElementById('resultsCount');
            
            // Generate sample products based on query
            currentProducts = generateSampleProducts(query);
            
            // Update results count
            resultsCount.textContent = `${currentProducts.length} produtos encontrados`;
            
            // Reset sort to price by default
            document.getElementById('sortBy').value = 'price';
            
            // Sort and display products
            sortProducts();
            
            resultsContainer.classList.remove('hidden');
            resultsContainer.scrollIntoView({ behavior: 'smooth' });
        }

        function sortProducts() {
            const sortBy = document.getElementById('sortBy').value;
            const productList = document.getElementById('productList');
            
            // Create a copy to sort
            let sortedProducts = [...currentProducts];
            
            // Regular sorting
            switch(sortBy) {
                case 'price':
                    sortedProducts.sort((a, b) => a.price - b.price);
                    break;
                case 'distance':
                    sortedProducts.sort((a, b) => a.distanceKm - b.distanceKm);
                    break;
                case 'savings':
                    sortedProducts.sort((a, b) => b.savings - a.savings);
                    break;
            }
            
            // Calculate rankings for all criteria
            const priceRanking = [...currentProducts].sort((a, b) => a.price - b.price);
            const distanceRanking = [...currentProducts].sort((a, b) => a.distanceKm - b.distanceKm);
            const savingsRanking = [...currentProducts].sort((a, b) => b.savings - a.savings);
            
            // Clear product list
            productList.innerHTML = '';
            
            // Create product cards with ranking information
            sortedProducts.forEach((product, index) => {
                const priceRank = priceRanking.findIndex(p => p.name === product.name) + 1;
                const distanceRank = distanceRanking.findIndex(p => p.name === product.name) + 1;
                const savingsRank = savingsRanking.findIndex(p => p.name === product.name) + 1;
                
                const productCard = createProductCard(product, {
                    currentSort: sortBy,
                    currentRank: index + 1,
                    priceRank: priceRank,
                    distanceRank: distanceRank,
                    savingsRank: savingsRank,
                    totalProducts: currentProducts.length,
                    cheapestPrice: priceRanking[0].price,
                    closestDistance: distanceRanking[0].distanceKm
                });
                productList.appendChild(productCard);
            });
        }

        // Global variable to store current products
        let currentProducts = [];

        function generateSampleProducts(query) {
            const brands = ['Premium', 'Nacional', 'Popular', 'Especial', 'Gourmet', 'Econômica'];
            
            const products = [
                {
                    name: `${query} - Marca Premium`,
                    store: 'Zona Sul Cascatinha',
                    price: 7.50,
                    originalPrice: 8.90,
                    distanceKm: 2.1,
                    distance: '2.1km',
                    brand: 'Premium'
                },
                {
                    name: `${query} - Marca Nacional`,
                    store: 'Extra Benfica',
                    price: 9.89,
                    originalPrice: 11.20,
                    distanceKm: 1.8,
                    distance: '1.8km',
                    brand: 'Nacional'
                },
                {
                    name: `${query} - Marca Popular`,
                    store: 'EPA Centro',
                    price: 8.20,
                    originalPrice: 9.50,
                    distanceKm: 3.2,
                    distance: '3.2km',
                    brand: 'Popular'
                },
                {
                    name: `${query} - Marca Especial`,
                    store: 'Bahamas São Mateus',
                    price: 8.90,
                    originalPrice: 10.50,
                    distanceKm: 4.5,
                    distance: '4.5km',
                    brand: 'Especial'
                },
                {
                    name: `${query} - Marca Gourmet`,
                    store: 'Carrefour Shopping',
                    price: 9.10,
                    originalPrice: 10.80,
                    distanceKm: 1.2,
                    distance: '1.2km',
                    brand: 'Gourmet'
                },
                {
                    name: `${query} - Marca Econômica`,
                    store: 'Atacadão Benfica',
                    price: 6.50,
                    originalPrice: 7.90,
                    distanceKm: 5.8,
                    distance: '5.8km',
                    brand: 'Econômica'
                }
            ];
            
            // Calculate savings for each product
            products.forEach(product => {
                product.savings = product.originalPrice - product.price;
                product.savingsPercent = ((product.savings / product.originalPrice) * 100);
            });
            
            return products;
        }

        function createProductCard(product, rankings) {
            const card = document.createElement('div');
            card.className = 'premium-glass rounded-xl p-6 hover:scale-102 transition-all duration-300';
            
            const savings = product.savings;
            const savingsPercent = product.savingsPercent.toFixed(0);
            
            // Determine primary badge based on current sort
            let primaryBadge = '';
            let badgeColor = '';
            
            if (rankings.currentSort === 'price') {
                if (rankings.currentRank === 1) {
                    primaryBadge = 'MELHOR PREÇO';
                    badgeColor = 'green';
                } else if (rankings.currentRank === 2) {
                    primaryBadge = '2º MELHOR PREÇO';
                    badgeColor = 'blue';
                } else {
                    primaryBadge = `${rankings.currentRank}º PREÇO`;
                    badgeColor = 'gray';
                }
            } else if (rankings.currentSort === 'distance') {
                if (rankings.currentRank === 1) {
                    primaryBadge = 'MAIS PRÓXIMO';
                    badgeColor = 'green';
                } else if (rankings.currentRank === 2) {
                    primaryBadge = '2º MAIS PRÓXIMO';
                    badgeColor = 'blue';
                } else {
                    primaryBadge = `${rankings.currentRank}º PROXIMIDADE`;
                    badgeColor = 'gray';
                }
            } else if (rankings.currentSort === 'savings') {
                if (rankings.currentRank === 1) {
                    primaryBadge = 'MAIOR ECONOMIA';
                    badgeColor = 'green';
                } else if (rankings.currentRank === 2) {
                    primaryBadge = '2ª MAIOR ECONOMIA';
                    badgeColor = 'blue';
                } else {
                    primaryBadge = `${rankings.currentRank}º ECONOMIA`;
                    badgeColor = 'gray';
                }
            }
            

            
            // Generate secondary ranking info
            let secondaryInfo = '';
            if (rankings.currentSort === 'price') {
                secondaryInfo = `
                    <div class="flex items-center space-x-4 text-sm text-slate-600 mb-2">
                        <span class="flex items-center">
                            <svg class="w-4 h-4 mr-1 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/>
                            </svg>
                            ${rankings.distanceRank}º em proximidade
                        </span>
                        <span class="flex items-center">
                            <svg class="w-4 h-4 mr-1 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"/>
                            </svg>
                            ${rankings.savingsRank}º em economia
                        </span>
                    </div>
                `;
            } else if (rankings.currentSort === 'distance') {
                const priceDifference = (product.price - rankings.cheapestPrice).toFixed(2);
                secondaryInfo = `
                    <div class="flex items-center space-x-4 text-sm text-slate-600 mb-2">
                        <span class="flex items-center">
                            <svg class="w-4 h-4 mr-1 text-red-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"/>
                            </svg>
                            ${rankings.priceRank}º em preço
                        </span>
                        <span class="text-orange-600">
                            ${priceDifference > 0 ? `+R$ ${priceDifference}` : 'Melhor preço'} vs mais barato
                        </span>
                    </div>
                `;
            } else if (rankings.currentSort === 'savings') {
                secondaryInfo = `
                    <div class="flex items-center space-x-4 text-sm text-slate-600 mb-2">
                        <span class="flex items-center">
                            <svg class="w-4 h-4 mr-1 text-red-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"/>
                            </svg>
                            ${rankings.priceRank}º em preço
                        </span>
                        <span class="flex items-center">
                            <svg class="w-4 h-4 mr-1 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/>
                            </svg>
                            ${rankings.distanceRank}º em proximidade
                        </span>
                    </div>
                `;
            }
            
            card.innerHTML = `
                <div class="flex justify-between items-start">
                    <div class="flex-1">
                        <h4 class="font-bold text-lg text-slate-800 mb-2">${product.name}</h4>
                        <p class="text-slate-600 mb-3">${product.store} • ${product.distance}</p>
                        
                        <div class="flex items-center flex-wrap gap-2 mb-3">
                            <span class="bg-${badgeColor}-100 text-${badgeColor}-800 text-xs px-3 py-1 rounded-full font-semibold">
                                ${primaryBadge}
                            </span>
                            <span class="text-sm text-slate-500">Economia: ${savingsPercent}%</span>
                        </div>
                        

                        
                        ${secondaryInfo}
                        
                        <div class="flex items-center space-x-2">
                            <span class="text-2xl font-bold text-green-600">R$ ${product.price.toFixed(2)}</span>
                            <span class="text-sm text-gray-500 line-through">R$ ${product.originalPrice.toFixed(2)}</span>
                        </div>
                    </div>
                    <div class="text-right">
                        <button onclick="addToCart('${product.name}', ${product.price}, '${product.store}')" 
                                class="premium-button text-white px-6 py-2 rounded-lg font-semibold mb-2 hover:scale-105 transition-transform">
                            <svg class="w-4 h-4 inline mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"/>
                            </svg>
                            Adicionar
                        </button>
                        
                        <div class="flex space-x-1 mb-2">
                            <button onclick="showPriceHistory('${product.name}', ${product.price})" 
                                    class="bg-blue-100 text-blue-700 px-3 py-1 rounded text-xs font-semibold hover:bg-blue-200 transition-colors">
                                📊 Histórico
                            </button>
                            <button onclick="setPriceAlert('${product.name}', ${product.price})" 
                                    class="bg-yellow-100 text-yellow-700 px-3 py-1 rounded text-xs font-semibold hover:bg-yellow-200 transition-colors">
                                🔔 Alerta
                            </button>
                        </div>
                        
                        <div class="text-xs text-slate-500">
                            Economize R$ ${savings.toFixed(2)}
                        </div>
                    </div>
                </div>
            `;
            
            return card;
        }

        // Cart functions
        async function addToCart(name, price, store) {
            if (!isLoggedIn) {
                showSignupModal();
                return;
            }
            
            const item = {
                id: Date.now(),
                name: name,
                price: price,
                store: store,
                quantity: 1,
                originalPrice: price * 1.15, // Simulate original price
                hasPromotion: Math.random() > 0.7,
                cashbackEligible: currentUser && currentUser.plan === 'Premium',
                addedAt: new Date()
            };
            
            cart.push(item);
            updateCartDisplay();
            
            // Save cart to Firebase
            await saveUserCart();
            
            // Log add to cart event
            await logUserEvent('add_to_cart', {
                productName: name,
                price: price,
                store: store
            });
            
            // Keep cart open if it was already open, or open it if it's the first item
            if (!isCartOpen || cart.length === 1) {
                openCart();
            }
            
            // Show plan-specific features
            if (currentUser) {
                if (currentUser.plan === 'Pro') {
                    showNotification('Adicionado!', `${name} foi adicionado ao carrinho`, 'success');
                } else if (currentUser.plan === 'Premium') {
                    const cashback = item.cashbackEligible ? (price * 0.05).toFixed(2) : '0.00';
                    showNotification('Adicionado + Cashback!', `${name} adicionado. Cashback: R$ ${cashback}`, 'success');
                }
            }
            
            // Check for suggested substitutions (Premium only)
            if (currentUser && currentUser.plan === 'Premium') {
                setTimeout(() => {
                    checkForSubstitutions(item);
                }, 1000);
            }
        }

        function checkForSubstitutions(item) {
            // Simulate finding better alternatives
            const alternatives = [
                {
                    name: item.name.replace('Premium', 'Econômica').replace('Nacional', 'Popular'),
                    price: item.price * 0.85,
                    store: 'Atacadão Benfica',
                    savings: item.price * 0.15,
                    reason: 'Melhor preço'
                },
                {
                    name: item.name.replace('Premium', 'Light').replace('Nacional', 'Integral'),
                    price: item.price * 1.05,
                    store: item.store,
                    savings: 0,
                    reason: 'Mais saudável',
                    healthier: true
                }
            ];
            
            const suggestion = alternatives[Math.floor(Math.random() * alternatives.length)];
            
            if (suggestion.savings > 0 || suggestion.healthier) {
                showSubstitutionModal(item, suggestion);
            }
        }

        function showSubstitutionModal(originalItem, suggestion) {
            let modal = document.getElementById('substitutionModal');
            if (!modal) {
                modal = document.createElement('div');
                modal.id = 'substitutionModal';
                modal.className = 'modal';
                document.body.appendChild(modal);
            }
            
            const isHealthierSuggestion = suggestion.healthier;
            const savingsText = suggestion.savings > 0 ? `Economize R$ ${suggestion.savings.toFixed(2)}` : '';
            const healthText = isHealthierSuggestion ? '🥗 Opção mais saudável' : '';
            
            modal.innerHTML = `
                <div class="premium-glass rounded-2xl p-8 max-w-md w-full mx-4">
                    <div class="text-center mb-6">
                        <div class="w-16 h-16 ${isHealthierSuggestion ? 'bg-green-100' : 'bg-blue-100'} rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl">${isHealthierSuggestion ? '🥗' : '💰'}</span>
                        </div>
                        <h3 class="text-2xl font-bold text-slate-800 mb-2">Sugestão do Parceiro</h3>
                        <p class="text-slate-600">Encontramos uma alternativa interessante!</p>
                    </div>
                    
                    <div class="space-y-4 mb-6">
                        <div class="bg-gray-50 rounded-lg p-4">
                            <h4 class="font-semibold text-gray-800 mb-2">Produto Atual:</h4>
                            <p class="text-gray-700">${originalItem.name}</p>
                            <p class="text-lg font-bold text-gray-600">R$ ${originalItem.price.toFixed(2)}</p>
                        </div>
                        
                        <div class="text-center">
                            <svg class="w-8 h-8 text-gray-400 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m0 0l7-7"/>
                            </svg>
                        </div>
                        
                        <div class="bg-${isHealthierSuggestion ? 'green' : 'blue'}-50 rounded-lg p-4 border-2 border-${isHealthierSuggestion ? 'green' : 'blue'}-200">
                            <h4 class="font-semibold text-${isHealthierSuggestion ? 'green' : 'blue'}-800 mb-2">Sugestão:</h4>
                            <p class="text-${isHealthierSuggestion ? 'green' : 'blue'}-700">${suggestion.name}</p>
                            <p class="text-lg font-bold text-${isHealthierSuggestion ? 'green' : 'blue'}-600">R$ ${suggestion.price.toFixed(2)}</p>
                            <p class="text-sm text-${isHealthierSuggestion ? 'green' : 'blue'}-600 mt-2">${suggestion.store}</p>
                            ${savingsText ? `<p class="text-sm font-semibold text-green-600 mt-1">${savingsText}</p>` : ''}
                            ${healthText ? `<p class="text-sm font-semibold text-green-600 mt-1">${healthText}</p>` : ''}
                        </div>
                    </div>
                    
                    <div class="flex space-x-3">
                        <button onclick="closeModal('substitutionModal')" class="flex-1 bg-gray-200 text-gray-700 py-3 rounded-lg font-semibold hover:bg-gray-300 transition-colors">
                            Manter Original
                        </button>
                        <button onclick="acceptSubstitution('${originalItem.id}', '${suggestion.name}', ${suggestion.price}, '${suggestion.store}')" class="flex-1 bg-${isHealthierSuggestion ? 'green' : 'blue'}-600 hover:bg-${isHealthierSuggestion ? 'green' : 'blue'}-700 text-white py-3 rounded-lg font-semibold transition-colors">
                            Trocar
                        </button>
                    </div>
                    
                    <button onclick="closeModal('substitutionModal')" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                        </svg>
                    </button>
                </div>
            `;
            
            modal.classList.add('active');
        }

        function acceptSubstitution(originalItemId, newName, newPrice, newStore) {
            // Find and replace the item in cart
            const itemIndex = cart.findIndex(item => item.id == originalItemId);
            if (itemIndex !== -1) {
                cart[itemIndex].name = newName;
                cart[itemIndex].price = newPrice;
                cart[itemIndex].store = newStore;
                updateCartDisplay();
                
                showNotification('Troca Realizada!', 'Produto substituído com sucesso', 'success');
                
                // Add mission points for Premium/+Saudável users
                if (currentUser && (currentUser.plan === 'Premium' || currentUser.plan === '+Saudável')) {
                    setTimeout(() => {
                        showNotification('Pontos Ganhos!', '+25 pontos de missão pela troca inteligente', 'info');
                    }, 1500);
                }
            }
            
            closeModal('substitutionModal');
        }

        function removeFromCart(itemId) {
            cart = cart.filter(item => item.id !== itemId);
            updateCartDisplay();
        }

        function updateCartDisplay() {
            const cartCount = document.getElementById('cartCount');
            const emptyCart = document.getElementById('emptyCart');
            const cartItemsList = document.getElementById('cartItemsList');
            const cartFooter = document.getElementById('cartFooter');
            const cartTotal = document.getElementById('cartTotal');
            const cartSavings = document.getElementById('cartSavings');
            
            console.log('🛒 updateCartDisplay called');
            console.log('isLoggedIn:', isLoggedIn);
            console.log('cart length:', cart.length);
            
            // FORCE SHOW cart icon when user is logged in
            if (isLoggedIn && currentUser && cartCount) {
                console.log('✅ Forcing cart visibility');
                
                // FORCE show cart count badge ALWAYS - MULTIPLE METHODS
                cartCount.classList.remove('hidden');
                cartCount.style.display = 'flex !important';
                cartCount.style.visibility = 'visible !important';
                cartCount.style.opacity = '1 !important';
                cartCount.textContent = cart.length;
                
                // Force show all parent elements too
                let parent = cartCount.parentElement;
                while (parent && parent !== document.body) {
                    parent.classList.remove('hidden');
                    parent.style.display = parent.tagName === 'BUTTON' ? 'block' : 'flex';
                    parent.style.visibility = 'visible';
                    parent = parent.parentElement;
                }
                
                console.log('✅ Cart count set to:', cart.length);
                
                if (cart.length === 0) {
                    if (emptyCart) emptyCart.classList.remove('hidden');
                    if (cartItemsList) cartItemsList.classList.add('hidden');
                    if (cartFooter) cartFooter.classList.add('hidden');
                } else {
                    if (emptyCart) emptyCart.classList.add('hidden');
                    if (cartItemsList) cartItemsList.classList.remove('hidden');
                    if (cartFooter) cartFooter.classList.remove('hidden');
                    
                    // Update cart items
                    if (cartItemsList) {
                        cartItemsList.innerHTML = '';
                        let total = 0;
                        let totalSavings = 0;
                        
                        cart.forEach(item => {
                            total += item.price * item.quantity;
                            totalSavings += (item.price * 0.15) * item.quantity; // Assume 15% savings
                            
                            const itemElement = document.createElement('div');
                            itemElement.className = 'cart-item bg-gray-50 rounded-lg p-4';
                            itemElement.innerHTML = `
                                <div class="flex justify-between items-start">
                                    <div class="flex-1">
                                        <h5 class="font-semibold text-gray-800">${item.name}</h5>
                                        <p class="text-sm text-gray-600">${item.store}</p>
                                        <p class="text-lg font-bold text-green-600 mt-1">R$ ${item.price.toFixed(2)}</p>
                                    </div>
                                    <button onclick="removeFromCart(${item.id})" class="text-red-500 hover:text-red-700">
                                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
                                        </svg>
                                    </button>
                                </div>
                            `;
                            cartItemsList.appendChild(itemElement);
                        });
                        
                        if (cartTotal) cartTotal.textContent = `R$ ${total.toFixed(2)}`;
                        if (cartSavings) cartSavings.textContent = `R$ ${totalSavings.toFixed(2)}`;
                    }
                }
            } else {
                console.log('❌ Hiding cart - user not logged in');
                // Hide cart when not logged in
                if (cartCount) {
                    cartCount.classList.add('hidden');
                    cartCount.style.display = 'none';
                }
            }
        }

        let isCartOpen = false;

        function toggleCart() {
            const cartSidebar = document.getElementById('cartSidebar');
            isCartOpen = !isCartOpen;
            
            if (isCartOpen) {
                cartSidebar.classList.remove('translate-x-full');
            } else {
                cartSidebar.classList.add('translate-x-full');
            }
        }

        function openCart() {
            const cartSidebar = document.getElementById('cartSidebar');
            isCartOpen = true;
            cartSidebar.classList.remove('translate-x-full');
        }

        function closeCart() {
            const cartSidebar = document.getElementById('cartSidebar');
            isCartOpen = false;
            cartSidebar.classList.add('translate-x-full');
        }

        function clearCart() {
            cart = [];
            updateCartDisplay();
            showNotification('Carrinho limpo', 'Todos os itens foram removidos', 'info');
        }

        function optimizeRoute() {
            if (cart.length === 0) {
                showNotification('Carrinho vazio', 'Adicione produtos para otimizar a rota', 'warning');
                return;
            }
            
            if (!currentUser || currentUser.plan === 'Básico') {
                showNotification('Upgrade Necessário', 'Funcionalidade disponível nos planos Pro, Premium e +Saudável', 'warning');
                showPage('assinatura');
                return;
            }
            
            showNotification('Otimizando...', 'Calculando a melhor rota e verificando disponibilidade', 'info');
            
            setTimeout(() => {
                // Check for unavailable items before showing modal
                const tourData = generateDetailedTour();
                const unavailableItems = tourData.unavailableItemsSummary || [];
                
                if (unavailableItems.length > 0) {
                    showNotification('Atenção!', `${unavailableItems.length} produto${unavailableItems.length > 1 ? 's' : ''} indisponível${unavailableItems.length > 1 ? 'is' : ''} detectado${unavailableItems.length > 1 ? 's' : ''}`, 'warning');
                }
                
                showRouteOptimizationModal();
            }, 2000);
        }

        function showRouteOptimizationModal() {
            // Create modal if it doesn't exist
            let modal = document.getElementById('routeOptimizationModal');
            if (!modal) {
                modal = document.createElement('div');
                modal.id = 'routeOptimizationModal';
                modal.className = 'modal';
                document.body.appendChild(modal);
            }
            
            const routeOptions = generateRouteOptions();
            
            modal.innerHTML = `
                <div class="premium-glass rounded-2xl p-8 max-w-4xl w-full mx-4 max-h-[90vh] overflow-y-auto">
                    <div class="text-center mb-6">
                        <h3 class="text-3xl font-bold text-slate-800 mb-2">🗺️ Carrinho Inteligente Avançado</h3>
                        <p class="text-slate-600">Escolha a melhor estratégia para suas compras</p>
                    </div>
                    
                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
                        ${routeOptions.map((option, index) => `
                            <div class="bg-white rounded-xl p-6 border-2 ${index === 0 ? 'border-green-300 bg-green-50' : index === 1 ? 'border-blue-300 bg-blue-50' : 'border-purple-300 bg-purple-50'} hover:scale-105 transition-all duration-300 cursor-pointer" onclick="selectRouteOption(${index})">
                                <div class="text-center mb-4">
                                    <div class="w-16 h-16 ${index === 0 ? 'bg-green-100' : index === 1 ? 'bg-blue-100' : 'bg-purple-100'} rounded-full flex items-center justify-center mx-auto mb-3">
                                        <span class="text-2xl">${option.icon}</span>
                                    </div>
                                    <h4 class="text-lg font-bold ${index === 0 ? 'text-green-800' : index === 1 ? 'text-blue-800' : 'text-purple-800'} mb-1">${option.title}</h4>
                                    <p class="text-xs ${index === 0 ? 'text-green-600' : index === 1 ? 'text-blue-600' : 'text-purple-600'} mb-3">${option.subtitle}</p>
                                    <div class="text-3xl font-bold ${index === 0 ? 'text-green-600' : index === 1 ? 'text-blue-600' : 'text-purple-600'} mb-2">R$ ${option.totalPrice.toFixed(2)}</div>
                                </div>
                                
                                <div class="bg-white rounded-lg p-3 mb-4 border border-gray-200">
                                    <p class="text-xs text-gray-700 mb-2 font-semibold">${option.explanation}</p>
                                    <div class="space-y-2">
                                        <div class="flex items-center text-xs text-gray-600">
                                            <span class="w-2 h-2 bg-green-500 rounded-full mr-2"></span>
                                            <span class="flex-1">${option.stores[0].name}</span>
                                        </div>
                                        <div class="text-xs text-gray-500 ml-4">
                                            📍 ${option.stores[0].distance} • ${option.stores[0].items} produtos
                                        </div>
                                        <div class="text-xs text-gray-500 ml-4">
                                            ${option.stores[0].address}
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="bg-${index === 0 ? 'green' : index === 1 ? 'blue' : 'purple'}-50 rounded-lg p-3 mb-4">
                                    <p class="text-xs ${index === 0 ? 'text-green-700' : index === 1 ? 'text-blue-700' : 'text-purple-700'}">${option.details}</p>
                                </div>
                                
                                <div class="flex justify-between text-xs text-gray-600 mb-4">
                                    <span>Economia: <strong class="text-green-600">R$ ${option.savings.toFixed(2)}</strong></span>
                                    <span>100% disponível</span>
                                </div>
                                
                                <button class="w-full ${index === 0 ? 'bg-green-600 hover:bg-green-700' : index === 1 ? 'bg-blue-600 hover:bg-blue-700' : 'bg-purple-600 hover:bg-purple-700'} text-white py-3 rounded-lg font-semibold transition-colors text-sm">
                                    ✅ Escolher Esta Opção
                                </button>
                            </div>
                        `).join('')}
                    </div>
                    
                    <div class="bg-gray-50 rounded-xl p-6 mb-6">
                        <h4 class="font-bold text-gray-800 mb-4">🎯 Tour de Compras Detalhado - Opção Custo-Benefício</h4>
                        <div class="bg-blue-50 rounded-lg p-3 mb-4 border-l-4 border-blue-400">
                            <p class="text-sm text-blue-800">
                                <strong>💡 Como funciona:</strong> O tour indica apenas os produtos <strong>MAIS BARATOS</strong> disponíveis em cada mercado. 
                                Você vai direto ao que interessa - os melhores preços de cada loja!
                            </p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                            ${generateDetailedTour().map(stop => `
                                <div class="bg-white rounded-lg p-4 border border-gray-200">
                                    <div class="flex items-center mb-3">
                                        <div class="w-8 h-8 bg-purple-100 rounded-full flex items-center justify-center mr-3">
                                            <span class="text-sm font-bold text-purple-600">${stop.order}</span>
                                        </div>
                                        <div>
                                            <h5 class="font-semibold text-gray-800">${stop.store}</h5>
                                            <p class="text-xs text-gray-600">${stop.address} • ${stop.distance}</p>
                                        </div>
                                    </div>
                                    
                                    <!-- Available Items -->
                                    <div class="space-y-2 mb-3">
                                        ${stop.items.map(item => `
                                            <div class="flex justify-between items-center text-sm">
                                                <span class="text-gray-700 flex items-center">
                                                    <span class="w-2 h-2 bg-green-500 rounded-full mr-2"></span>
                                                    ${item.name}
                                                </span>
                                                <span class="font-semibold text-green-600">R$ ${item.price.toFixed(2)}</span>
                                            </div>
                                        `).join('')}
                                    </div>
                                    
                                    <!-- Unavailable Items -->
                                    ${stop.unavailableItems.length > 0 ? `
                                        <div class="bg-red-50 rounded-lg p-3 mb-3">
                                            <h6 class="text-xs font-semibold text-red-800 mb-2 flex items-center">
                                                <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L3.732 16.5c-.77.833.192 2.5 1.732 2.5z"/>
                                                </svg>
                                                PRODUTOS INDISPONÍVEIS
                                            </h6>
                                            <div class="space-y-1">
                                                ${stop.unavailableItems.map(item => `
                                                    <div class="text-xs text-red-700 flex items-center">
                                                        <span class="w-2 h-2 bg-red-500 rounded-full mr-2"></span>
                                                        ${item.name}
                                                    </div>
                                                `).join('')}
                                            </div>
                                        </div>
                                    ` : ''}
                                    
                                    <div class="border-t mt-3 pt-3 flex justify-between items-center">
                                        <span class="text-sm font-semibold text-gray-800">Subtotal:</span>
                                        <span class="font-bold text-purple-600">R$ ${stop.subtotal.toFixed(2)}</span>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                        
                        <!-- Global Unavailable Items Warning -->
                        ${(() => {
                            const tourData = generateDetailedTour();
                            const totalUnavailable = tourData.unavailableItemsSummary || [];
                            return totalUnavailable.length > 0 ? `
                                <div class="bg-orange-50 border-l-4 border-orange-400 p-4 rounded-lg">
                                    <div class="flex items-center mb-2">
                                        <svg class="w-5 h-5 text-orange-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L3.732 16.5c-.77.833.192 2.5 1.732 2.5z"/>
                                        </svg>
                                        <h5 class="font-bold text-orange-800">⚠️ ATENÇÃO: Produtos Indisponíveis Detectados</h5>
                                    </div>
                                    <p class="text-sm text-orange-700 mb-3">
                                        <strong>${totalUnavailable.length} produto${totalUnavailable.length > 1 ? 's' : ''}</strong> da sua lista não ${totalUnavailable.length > 1 ? 'estão' : 'está'} disponível${totalUnavailable.length > 1 ? 'is' : ''} nos mercados selecionados:
                                    </p>
                                    <div class="grid grid-cols-1 md:grid-cols-2 gap-2 mb-3">
                                        ${totalUnavailable.map(item => `
                                            <div class="text-sm text-orange-800 bg-orange-100 rounded px-3 py-1">
                                                <strong>${item.name}</strong> - ${item.store}
                                            </div>
                                        `).join('')}
                                    </div>
                                    <div class="text-sm text-orange-700">
                                        <p class="mb-2"><strong>💡 Sugestões:</strong></p>
                                        <ul class="list-disc list-inside space-y-1 text-xs">
                                            <li>Ligue antes para confirmar disponibilidade</li>
                                            <li>Considere produtos similares disponíveis</li>
                                            <li>Visite outros mercados próximos para estes itens</li>
                                            <li>Configure alertas para quando voltarem ao estoque</li>
                                        </ul>
                                    </div>
                                </div>
                            ` : '';
                        })()}
                    </div>
                    
                    ${currentUser && currentUser.plan === 'Premium' ? `
                        <div class="bg-gradient-to-r from-indigo-50 to-purple-50 rounded-xl p-6 mb-6">
                            <h4 class="font-bold text-indigo-800 mb-4">✨ Funcionalidades Premium Ativas</h4>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <div class="flex items-center space-x-3">
                                    <div class="w-8 h-8 bg-indigo-100 rounded-full flex items-center justify-center">
                                        <span class="text-indigo-600">🎯</span>
                                    </div>
                                    <div>
                                        <p class="font-semibold text-indigo-800">Trocas Sugeridas</p>
                                        <p class="text-xs text-indigo-600">2 sugestões encontradas</p>
                                    </div>
                                </div>
                                <div class="flex items-center space-x-3">
                                    <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center">
                                        <span class="text-green-600">💰</span>
                                    </div>
                                    <div>
                                        <p class="font-semibold text-green-800">Cashback Disponível</p>
                                        <p class="text-xs text-green-600">R$ 3,20 em cashback</p>
                                    </div>
                                </div>
                                <div class="flex items-center space-x-3">
                                    <div class="w-8 h-8 bg-yellow-100 rounded-full flex items-center justify-center">
                                        <span class="text-yellow-600">🎫</span>
                                    </div>
                                    <div>
                                        <p class="font-semibold text-yellow-800">Cupons Exclusivos</p>
                                        <p class="text-xs text-yellow-600">3 cupons aplicáveis</p>
                                    </div>
                                </div>
                                <div class="flex items-center space-x-3">
                                    <div class="w-8 h-8 bg-purple-100 rounded-full flex items-center justify-center">
                                        <span class="text-purple-600">🏆</span>
                                    </div>
                                    <div>
                                        <p class="font-semibold text-purple-800">Pontos de Missão</p>
                                        <p class="text-xs text-purple-600">+150 pontos nesta compra</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    ` : ''}
                    
                    <div class="flex justify-between items-center">
                        <button onclick="closeModal('routeOptimizationModal')" class="bg-gray-200 text-gray-700 px-6 py-3 rounded-lg font-semibold hover:bg-gray-300 transition-colors">
                            Fechar
                        </button>
                        <button onclick="startShopping()" class="premium-button text-white px-8 py-3 rounded-lg font-semibold">
                            <svg class="w-5 h-5 inline mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-1.447-.894L15 4m0 13V4m0 0L9 7"/>
                            </svg>
                            Iniciar Compras
                        </button>
                    </div>
                    
                    <button onclick="closeModal('routeOptimizationModal')" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                        </svg>
                    </button>
                </div>
            `;
            
            modal.classList.add('active');
        }

        function generateRouteOptions() {
            const cartTotal = cart.reduce((sum, item) => sum + item.price, 0);
            const cartOptimizationMode = document.getElementById('cartOptimizationMode')?.value || 'balanced';
            
            // Base options
            let options = [
                {
                    title: "TUDO MAIS BARATO",
                    subtitle: "Onde sua lista COMPLETA sai mais barata",
                    icon: "💰",
                    totalPrice: cartTotal * 0.82,
                    totalDistance: 0,
                    estimatedTime: "Uma parada só",
                    savings: cartTotal * 0.18,
                    storesCount: 1,
                    explanation: "Encontramos UM supermercado onde TODOS os seus produtos custam menos no total",
                    stores: [
                        { name: "Bahamas São Mateus", items: cart.length, address: "Rua São Mateus, 450", distance: "30m de você" }
                    ],
                    details: "Mesmo alguns produtos individuais custando mais, o TOTAL da sua compra sai mais barato aqui."
                },
                {
                    title: "TUDO MAIS PERTO", 
                    subtitle: "Mais próximo que tem TUDO disponível",
                    icon: "📍",
                    totalPrice: cartTotal * 0.96,
                    totalDistance: 0,
                    estimatedTime: "Uma parada só",
                    savings: cartTotal * 0.04,
                    storesCount: 1,
                    explanation: "O estabelecimento mais próximo que tem 100% dos seus produtos em estoque",
                    stores: [
                        { name: "Mercearia do Seu João", items: cart.length, address: "Rua São Mateus, 123", distance: "50m de você" }
                    ],
                    details: "Pode custar um pouco mais, mas você economiza tempo e combustível."
                },
                {
                    title: "MELHOR CUSTO-BENEFÍCIO",
                    subtitle: "Equilibrio entre preço e distância",
                    icon: "⚖️",
                    totalPrice: cartTotal * 0.89,
                    totalDistance: 0,
                    estimatedTime: "Uma parada só",
                    savings: cartTotal * 0.11,
                    storesCount: 1,
                    explanation: "Boa economia sem ir muito longe - tem tudo que você precisa",
                    stores: [
                        { name: "Mercado Itamar Franco", items: cart.length, address: "Av. Itamar Franco, 234", distance: "120m de você" }
                    ],
                    details: "Preços competitivos e bem pertinho. A escolha mais equilibrada."
                }
            ];
            

            
            return options;
        }

        function generateDetailedTour() {
            // Simulate a detailed tour based on cart items with product availability
            const allItems = [...cart];
            const stores = [];
            let unavailableItems = [];
            
            // Store 1: Extra Benfica
            const store1Items = allItems.slice(0, Math.ceil(allItems.length / 2));
            // Simulate some items not being available (20% chance per item)
            const store1Available = store1Items.filter(() => Math.random() > 0.2);
            const store1Unavailable = store1Items.filter(item => !store1Available.includes(item));
            unavailableItems.push(...store1Unavailable.map(item => ({...item, store: "Extra Benfica"})));
            
            stores.push({
                order: 1,
                store: "Extra Benfica",
                address: "Av. Barão do Rio Branco, 1234",
                distance: "1.2 km",
                items: store1Available.map(item => ({
                    name: item.name,
                    price: item.price * 0.9,
                    available: true
                })),
                unavailableItems: store1Unavailable.map(item => ({
                    name: item.name,
                    available: false
                })),
                subtotal: 0
            });
            
            // Store 2: Bahamas São Mateus
            const remainingItems = allItems.filter(item => !store1Available.includes(item) && !store1Unavailable.includes(item));
            const store2Items = remainingItems.slice(0, Math.ceil(remainingItems.length * 0.7));
            const store2Available = store2Items.filter(() => Math.random() > 0.15);
            const store2Unavailable = store2Items.filter(item => !store2Available.includes(item));
            unavailableItems.push(...store2Unavailable.map(item => ({...item, store: "Bahamas São Mateus"})));
            
            stores.push({
                order: 2,
                store: "Bahamas São Mateus",
                address: "Rua São Mateus, 567",
                distance: "2.1 km do anterior",
                items: store2Available.map(item => ({
                    name: item.name,
                    price: item.price * 0.85,
                    available: true
                })),
                unavailableItems: store2Unavailable.map(item => ({
                    name: item.name,
                    available: false
                })),
                subtotal: 0
            });
            
            // Store 3: Mercearia do Bairro (gets remaining items)
            const finalItems = allItems.filter(item => 
                !store1Available.includes(item) && !store1Unavailable.includes(item) &&
                !store2Available.includes(item) && !store2Unavailable.includes(item)
            );
            
            stores.push({
                order: 3,
                store: "Mercearia do Bairro",
                address: "Rua das Flores, 89",
                distance: "0.8 km do anterior",
                items: finalItems.map(item => ({
                    name: item.name,
                    price: item.price * 0.95,
                    available: true
                })),
                unavailableItems: [],
                subtotal: 0
            });
            
            // Calculate subtotals
            stores.forEach(store => {
                store.subtotal = store.items.reduce((sum, item) => sum + item.price, 0);
            });
            
            // Add unavailable items summary
            stores.unavailableItemsSummary = unavailableItems;
            
            return stores;
        }

        function selectRouteOption(optionIndex) {
            const options = ['Mais Barato', 'Mais Próximo', 'Custo-Benefício'];
            showNotification('Rota Selecionada!', `Você escolheu a opção "${options[optionIndex]}"`, 'success');
            
            setTimeout(() => {
                closeModal('routeOptimizationModal');
                showRouteDetailsModal();
            }, 1500);
        }

        function showRouteDetailsModal() {
            let modal = document.getElementById('routeDetailsModal');
            if (!modal) {
                modal = document.createElement('div');
                modal.id = 'routeDetailsModal';
                modal.className = 'modal';
                document.body.appendChild(modal);
            }
            
            // Get the selected route option (simplified to one store)
            const selectedStore = {
                name: "Bahamas São Mateus",
                address: "Rua São Mateus, 450 - São Mateus, Juiz de Fora - MG",
                distance: "30m de você",
                items: cart.length,
                total: cart.reduce((sum, item) => sum + item.price * 0.82, 0)
            };
            
            modal.innerHTML = `
                <div class="premium-glass rounded-2xl p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
                    <div class="text-center mb-6">
                        <h3 class="text-2xl font-bold text-slate-800 mb-2">🗺️ Sua Compra Otimizada</h3>
                        <p class="text-slate-600">Um só lugar, todos os produtos</p>
                    </div>
                    
                    <div class="bg-white rounded-lg p-6 border border-gray-200 mb-6">
                        <div class="flex items-center justify-between mb-4">
                            <div class="flex items-center">
                                <div class="w-12 h-12 bg-green-100 rounded-full flex items-center justify-center mr-4">
                                    <span class="text-2xl">🏪</span>
                                </div>
                                <div>
                                    <h4 class="text-xl font-bold text-gray-800">${selectedStore.name}</h4>
                                    <p class="text-gray-600">${selectedStore.address}</p>
                                    <p class="text-sm text-blue-600 font-semibold">${selectedStore.distance}</p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="grid grid-cols-2 gap-4 mb-4">
                            <div class="text-center bg-green-50 rounded-lg p-3">
                                <div class="text-2xl font-bold text-green-600">${selectedStore.items}</div>
                                <div class="text-sm text-green-700">Produtos Disponíveis</div>
                            </div>
                            <div class="text-center bg-blue-50 rounded-lg p-3">
                                <div class="text-2xl font-bold text-blue-600">R$ ${selectedStore.total.toFixed(2)}</div>
                                <div class="text-sm text-blue-700">Total da Compra</div>
                            </div>
                        </div>
                        
                        <div class="flex space-x-3">
                            <button onclick="copyAddress('${selectedStore.address}')" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3 rounded-lg font-semibold transition-colors">
                                📋 Copiar Endereço
                            </button>
                            <button onclick="openInMaps('${selectedStore.name}', '${selectedStore.address}')" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-semibold transition-colors">
                                🗺️ Abrir no Maps
                            </button>
                        </div>
                    </div>
                    
                    <div class="bg-blue-50 rounded-lg p-4 mb-6">
                        <h4 class="font-semibold text-blue-800 mb-2">📱 Como usar a navegação:</h4>
                        <div class="text-sm text-blue-700 space-y-1">
                            <p>• <strong>Copiar Endereço:</strong> Cola no Waze, Google Maps ou Apple Maps</p>
                            <p>• <strong>Abrir no Maps:</strong> Abre diretamente no Google Maps (nova aba)</p>
                            <p>• <strong>Dica:</strong> Ligue antes para confirmar horário de funcionamento</p>
                        </div>
                    </div>
                    
                    <div class="bg-green-50 rounded-lg p-4 mb-6">
                        <h4 class="font-semibold text-green-800 mb-2">✅ Sua Lista de Compras:</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-2">
                            ${cart.map(item => `
                                <div class="flex justify-between items-center text-sm">
                                    <span class="text-gray-700">${item.name}</span>
                                    <span class="font-semibold text-green-600">R$ ${(item.price * 0.89).toFixed(2)}</span>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                    
                    <div class="flex justify-between items-center">
                        <button onclick="closeModal('routeDetailsModal')" class="bg-gray-200 text-gray-700 px-6 py-3 rounded-lg font-semibold hover:bg-gray-300 transition-colors">
                            Fechar
                        </button>
                        <button onclick="openInMaps('${selectedStore.name}', '${selectedStore.address}'); closeModal('routeDetailsModal')" class="premium-button text-white px-6 py-3 rounded-lg font-semibold">
                            🚗 Ir às Compras
                        </button>
                    </div>
                    
                    <button onclick="closeModal('routeDetailsModal')" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                        </svg>
                    </button>
                </div>
            `;
            
            modal.classList.add('active');
        }

        function copyAddress(address) {
            if (navigator.clipboard) {
                navigator.clipboard.writeText(address).then(() => {
                    showNotification('Copiado!', 'Endereço copiado para a área de transferência', 'success');
                }).catch(() => {
                    showNotification('Erro', 'Não foi possível copiar o endereço', 'error');
                });
            } else {
                // Fallback for older browsers
                const textArea = document.createElement('textarea');
                textArea.value = address;
                document.body.appendChild(textArea);
                textArea.select();
                try {
                    document.execCommand('copy');
                    showNotification('Copiado!', 'Endereço copiado para a área de transferência', 'success');
                } catch (err) {
                    showNotification('Erro', 'Não foi possível copiar o endereço', 'error');
                }
                document.body.removeChild(textArea);
            }
        }

        function openInMaps(storeName, address) {
            const query = encodeURIComponent(`${storeName}, ${address}, Juiz de Fora, MG`);
            const mapsUrl = `https://www.google.com/maps/search/?api=1&query=${query}`;
            
            // Try to open in new tab
            const newWindow = window.open(mapsUrl, '_blank');
            
            if (newWindow) {
                showNotification('Abrindo Maps', `Navegando para ${storeName}`, 'info');
            } else {
                // If popup blocked, show alternative
                showNotification('Popup Bloqueado', 'Copie o endereço e cole no seu app de navegação', 'warning');
                copyAddress(address);
            }
        }

        function openAllInMaps() {
            const tourStops = generateDetailedTour();
            let allAddresses = tourStops.map(stop => `${stop.store}: ${stop.address}`).join('\n');
            
            // Copy all addresses
            if (navigator.clipboard) {
                navigator.clipboard.writeText(allAddresses).then(() => {
                    showNotification('Todos os Endereços Copiados!', 'Cole no seu app de navegação favorito', 'success');
                });
            }
            
            // Try to open first location in Maps
            if (tourStops.length > 0) {
                const firstStop = tourStops[0];
                openInMaps(firstStop.store, firstStop.address);
            }
            
            closeModal('routeDetailsModal');
        }

        function startShopping() {
            closeModal('routeOptimizationModal');
            showNotification('Rota Salva!', 'Você pode copiar os endereços ou abrir no Google Maps', 'success');
            
            // Show route details modal
            setTimeout(() => {
                showRouteDetailsModal();
            }, 1500);
            
            // Simulate updating user savings
            if (currentUser) {
                const estimatedSavings = cart.reduce((sum, item) => sum + item.price * 0.15, 0);
                currentUser.savings += estimatedSavings;
                updateUserInterface();
            }
        }

        // Notification system
        function showNotification(title, message, type = 'info') {
            const notification = document.getElementById('notification');
            const icon = document.getElementById('notificationIcon');
            const titleEl = document.getElementById('notificationTitle');
            const messageEl = document.getElementById('notificationMessage');
            
            // Set content
            titleEl.textContent = title;
            messageEl.textContent = message;
            
            // Set icon and color based on type
            const colors = {
                success: 'bg-green-100 text-green-600',
                error: 'bg-red-100 text-red-600',
                warning: 'bg-yellow-100 text-yellow-600',
                info: 'bg-blue-100 text-blue-600'
            };
            
            const icons = {
                success: '✓',
                error: '✕',
                warning: '⚠',
                info: 'ℹ'
            };
            
            icon.className = `w-8 h-8 rounded-full flex items-center justify-center ${colors[type]}`;
            icon.textContent = icons[type];
            
            // Show notification
            notification.classList.add('show');
            
            // Hide after 3 seconds
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // Plan selection and payment simulation
        async function selectPlan(planType) {
            if (!isLoggedIn) {
                showSignupModal();
                return;
            }
            
            const planNames = {
                'pro': 'Pro',
                'premium': 'Premium',
                'saudavel': '+Saudável'
            };
            
            const planPrices = {
                'pro': 9.90,
                'premium': 19.90,
                'saudavel': 29.90
            };
            
            // Show payment processing modal
            showPaymentProcessingModal(planNames[planType], planPrices[planType]);
        }

        function showPaymentProcessingModal(planName, planPrice) {
            let modal = document.getElementById('paymentProcessingModal');
            if (!modal) {
                modal = document.createElement('div');
                modal.id = 'paymentProcessingModal';
                modal.className = 'modal';
                document.body.appendChild(modal);
            }
            
            modal.innerHTML = `
                <div class="premium-glass rounded-2xl p-8 max-w-md w-full mx-4">
                    <div class="text-center">
                        <div id="processingStep1" class="step-content">
                            <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                <div class="loading-spinner"></div>
                            </div>
                            <h3 class="text-2xl font-bold text-slate-800 mb-2">Processando Pagamento</h3>
                            <p class="text-slate-600 mb-4">Plano ${planName} - R$ ${planPrice.toFixed(2)}/mês</p>
                            <p class="text-sm text-slate-500">Validando dados do cartão...</p>
                        </div>
                        
                        <div id="processingStep2" class="step-content hidden">
                            <div class="w-16 h-16 bg-yellow-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                <div class="loading-spinner"></div>
                            </div>
                            <h3 class="text-2xl font-bold text-slate-800 mb-2">Autorizando Transação</h3>
                            <p class="text-slate-600 mb-4">Comunicando com o banco...</p>
                            <p class="text-sm text-slate-500">Aguarde alguns segundos</p>
                        </div>
                        
                        <div id="processingStep3" class="step-content hidden">
                            <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                <svg class="w-8 h-8 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
                                </svg>
                            </div>
                            <h3 class="text-2xl font-bold text-green-800 mb-2">Pagamento Aprovado!</h3>
                            <p class="text-green-600 mb-4">Plano ${planName} ativado com sucesso</p>
                            <p class="text-sm text-slate-500">Você receberá um email de confirmação</p>
                            
                            <button onclick="closePaymentModal()" class="mt-6 premium-button text-white px-8 py-3 rounded-lg font-semibold">
                                Continuar
                            </button>
                        </div>
                    </div>
                </div>
            `;
            
            modal.classList.add('active');
            
            // Simulate payment processing steps
            setTimeout(() => {
                document.getElementById('processingStep1').classList.add('hidden');
                document.getElementById('processingStep2').classList.remove('hidden');
            }, 2000);
            
            setTimeout(async () => {
                document.getElementById('processingStep2').classList.add('hidden');
                document.getElementById('processingStep3').classList.remove('hidden');
                
                // Update user plan in Firebase
                if (currentUser) {
                    try {
                        await db.collection('users').doc(currentUser.uid).update({
                            selectedPlan: planName,
                            planPrice: planPrice,
                            paymentStatus: 'active',
                            lastPayment: new Date(),
                            nextBilling: new Date(Date.now() + 30 * 24 * 60 * 60 * 1000) // 30 days from now
                        });
                        
                        // Update current user object
                        currentUser.plan = planName;
                        updateUserInterface();
                        
                        // Log payment event
                        await logUserEvent('payment_processed', {
                            plan: planName,
                            amount: planPrice,
                            paymentMethod: currentUser.paymentMethod || 'credit'
                        });
                        
                        // Send payment confirmation email
                        await sendPaymentConfirmationEmail(currentUser.email, currentUser.name, planName, planPrice);
                        
                    } catch (error) {
                        console.error('Error updating user plan:', error);
                    }
                }
            }, 4000);
        }

        function closePaymentModal() {
            const modal = document.getElementById('paymentProcessingModal');
            if (modal) {
                modal.classList.remove('active');
                showNotification('Plano Ativado!', 'Aproveite todas as funcionalidades premium', 'success');
            }
        }

        // Price history and alerts
        function showPriceHistory(productName, currentPrice) {
            if (!isLoggedIn) {
                showSignupModal();
                return;
            }
            
            if (!currentUser || currentUser.plan === 'Básico') {
                showNotification('Upgrade Necessário', 'Histórico de preços disponível nos planos Pro, Premium e +Saudável', 'warning');
                showPage('assinatura');
                return;
            }
            
            let modal = document.getElementById('priceHistoryModal');
            if (!modal) {
                modal = document.createElement('div');
                modal.id = 'priceHistoryModal';
                modal.className = 'modal';
                document.body.appendChild(modal);
            }
            
            // Generate sample price history
            const priceHistory = generatePriceHistory(currentPrice);
            const minPrice = Math.min(...priceHistory.map(p => p.price));
            const maxPrice = Math.max(...priceHistory.map(p => p.price));
            const avgPrice = priceHistory.reduce((sum, p) => sum + p.price, 0) / priceHistory.length;
            
            modal.innerHTML = `
                <div class="premium-glass rounded-2xl p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
                    <div class="text-center mb-6">
                        <h3 class="text-2xl font-bold text-slate-800 mb-2">📊 Histórico de Preços</h3>
                        <p class="text-slate-600">${productName}</p>
                        <p class="text-sm text-slate-500">Últimos 30 dias</p>
                    </div>
                    
                    <div class="grid grid-cols-3 gap-4 mb-6">
                        <div class="text-center bg-green-50 rounded-lg p-4">
                            <div class="text-2xl font-bold text-green-600">R$ ${minPrice.toFixed(2)}</div>
                            <div class="text-sm text-green-700">Menor Preço</div>
                        </div>
                        <div class="text-center bg-blue-50 rounded-lg p-4">
                            <div class="text-2xl font-bold text-blue-600">R$ ${avgPrice.toFixed(2)}</div>
                            <div class="text-sm text-blue-700">Preço Médio</div>
                        </div>
                        <div class="text-center bg-red-50 rounded-lg p-4">
                            <div class="text-2xl font-bold text-red-600">R$ ${maxPrice.toFixed(2)}</div>
                            <div class="text-sm text-red-700">Maior Preço</div>
                        </div>
                    </div>
                    
                    <div class="bg-gray-50 rounded-lg p-4 mb-6">
                        <h4 class="font-semibold text-gray-800 mb-4">Curva de Preços</h4>
                        <div class="space-y-2">
                            ${priceHistory.map((entry, index) => {
                                const barWidth = ((entry.price - minPrice) / (maxPrice - minPrice)) * 100;
                                const isCurrentPrice = Math.abs(entry.price - currentPrice) < 0.01;
                                return `
                                    <div class="flex items-center space-x-3">
                                        <div class="w-16 text-xs text-gray-600">${entry.date}</div>
                                        <div class="flex-1 bg-gray-200 rounded-full h-4 relative">
                                            <div class="bg-${isCurrentPrice ? 'blue' : entry.price === minPrice ? 'green' : entry.price === maxPrice ? 'red' : 'gray'}-500 h-4 rounded-full transition-all duration-300" style="width: ${Math.max(barWidth, 5)}%"></div>
                                        </div>
                                        <div class="w-20 text-sm font-semibold text-gray-800">R$ ${entry.price.toFixed(2)}</div>
                                        <div class="w-24 text-xs text-gray-600">${entry.store}</div>
                                    </div>
                                `;
                            }).join('')}
                        </div>
                    </div>
                    
                    <div class="bg-blue-50 rounded-lg p-4 mb-6">
                        <h4 class="font-semibold text-blue-800 mb-2">💡 Análise Inteligente</h4>
                        <div class="text-sm text-blue-700 space-y-1">
                            <p>• Preço atual está ${currentPrice < avgPrice ? 'abaixo' : 'acima'} da média (${((currentPrice - avgPrice) / avgPrice * 100).toFixed(1)}%)</p>
                            <p>• ${currentPrice === minPrice ? 'Este é o menor preço registrado!' : `Você pode economizar R$ ${(currentPrice - minPrice).toFixed(2)} comprando no menor preço`}</p>
                            <p>• Melhor dia para comprar: ${priceHistory.find(p => p.price === minPrice)?.date}</p>
                        </div>
                    </div>
                    
                    <div class="flex justify-between items-center">
                        <button onclick="closeModal('priceHistoryModal')" class="bg-gray-200 text-gray-700 px-6 py-3 rounded-lg font-semibold hover:bg-gray-300 transition-colors">
                            Fechar
                        </button>
                        <button onclick="setPriceAlert('${productName}', ${currentPrice}); closeModal('priceHistoryModal')" class="bg-yellow-600 hover:bg-yellow-700 text-white px-6 py-3 rounded-lg font-semibold transition-colors">
                            🔔 Criar Alerta
                        </button>
                    </div>
                    
                    <button onclick="closeModal('priceHistoryModal')" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                        </svg>
                    </button>
                </div>
            `;
            
            modal.classList.add('active');
        }

        function generatePriceHistory(currentPrice) {
            const history = [];
            const stores = ['Zona Sul', 'Extra', 'EPA', 'Bahamas', 'Carrefour'];
            
            for (let i = 29; i >= 0; i--) {
                const date = new Date();
                date.setDate(date.getDate() - i);
                const dateStr = date.toLocaleDateString('pt-BR', { day: '2-digit', month: '2-digit' });
                
                // Generate price variation around current price
                const variation = (Math.random() - 0.5) * 0.4; // ±20% variation
                const price = currentPrice * (1 + variation);
                const store = stores[Math.floor(Math.random() * stores.length)];
                
                history.push({
                    date: dateStr,
                    price: Math.max(price, 0.5), // Minimum price
                    store: store
                });
            }
            
            return history;
        }

        function setPriceAlert(productName, currentPrice) {
            if (!isLoggedIn) {
                showSignupModal();
                return;
            }
            
            if (!currentUser || currentUser.plan === 'Básico') {
                showNotification('Upgrade Necessário', 'Alertas de preço disponíveis nos planos Pro, Premium e +Saudável', 'warning');
                showPage('assinatura');
                return;
            }
            
            let modal = document.getElementById('priceAlertModal');
            if (!modal) {
                modal = document.createElement('div');
                modal.id = 'priceAlertModal';
                modal.className = 'modal';
                document.body.appendChild(modal);
            }
            
            const suggestedPrice = (currentPrice * 0.9).toFixed(2); // 10% below current price
            
            modal.innerHTML = `
                <div class="premium-glass rounded-2xl p-8 max-w-md w-full mx-4">
                    <div class="text-center mb-6">
                        <div class="w-16 h-16 bg-yellow-100 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl">🔔</span>
                        </div>
                        <h3 class="text-2xl font-bold text-slate-800 mb-2">Criar Alerta de Preço</h3>
                        <p class="text-slate-600">${productName}</p>
                        <p class="text-sm text-slate-500">Preço atual: R$ ${currentPrice.toFixed(2)}</p>
                    </div>
                    
                    <div class="space-y-4 mb-6">
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Avisar quando o preço for igual ou menor que:</label>
                            <div class="relative">
                                <span class="absolute left-3 top-3 text-gray-500">R$</span>
                                <input type="number" id="alertPrice" value="${suggestedPrice}" step="0.01" min="0.01" 
                                       class="w-full pl-8 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-500 focus:border-transparent">
                            </div>
                        </div>
                        
                        <div class="bg-yellow-50 rounded-lg p-4">
                            <h4 class="font-semibold text-yellow-800 mb-2">💡 Sugestão Inteligente</h4>
                            <p class="text-sm text-yellow-700">
                                Baseado no histórico, recomendamos alertar quando o preço for R$ ${suggestedPrice} ou menos 
                                (economia de R$ ${(currentPrice - parseFloat(suggestedPrice)).toFixed(2)}).
                            </p>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Como você quer ser notificado?</label>
                            <div class="space-y-2">
                                <label class="flex items-center">
                                    <input type="checkbox" checked class="rounded border-gray-300 text-yellow-600 focus:ring-yellow-500">
                                    <span class="ml-2 text-sm text-slate-700">Notificação no app</span>
                                </label>
                                <label class="flex items-center">
                                    <input type="checkbox" checked class="rounded border-gray-300 text-yellow-600 focus:ring-yellow-500">
                                    <span class="ml-2 text-sm text-slate-700">E-mail</span>
                                </label>
                                <label class="flex items-center">
                                    <input type="checkbox" class="rounded border-gray-300 text-yellow-600 focus:ring-yellow-500">
                                    <span class="ml-2 text-sm text-slate-700">SMS (Premium/+Saudável)</span>
                                </label>
                            </div>
                        </div>
                    </div>
                    
                    <div class="flex space-x-3">
                        <button onclick="closeModal('priceAlertModal')" class="flex-1 bg-gray-200 text-gray-700 py-3 rounded-lg font-semibold hover:bg-gray-300 transition-colors">
                            Cancelar
                        </button>
                        <button onclick="createPriceAlert('${productName}', ${currentPrice})" class="flex-1 bg-yellow-600 hover:bg-yellow-700 text-white py-3 rounded-lg font-semibold transition-colors">
                            Criar Alerta
                        </button>
                    </div>
                    
                    <button onclick="closeModal('priceAlertModal')" class="absolute top-4 right-4 text-gray-400 hover:text-gray-600">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                        </svg>
                    </button>
                </div>
            `;
            
            modal.classList.add('active');
        }

        function createPriceAlert(productName, currentPrice) {
            const alertPrice = document.getElementById('alertPrice').value;
            
            if (!alertPrice || parseFloat(alertPrice) <= 0) {
                showNotification('Erro', 'Digite um preço válido para o alerta', 'error');
                return;
            }
            
            closeModal('priceAlertModal');
            showNotification('Alerta Criado!', `Você será notificado quando ${productName} custar R$ ${parseFloat(alertPrice).toFixed(2)} ou menos`, 'success');
            
            // Simulate alert triggering after some time
            setTimeout(() => {
                if (Math.random() > 0.7) { // 30% chance of alert
                    showNotification('🔔 Alerta de Preço!', `${productName} está em promoção por R$ ${(parseFloat(alertPrice) - 0.50).toFixed(2)}!`, 'success');
                }
            }, 10000); // 10 seconds
        }

        // Form formatting functions
        function formatCPF(input) {
            let value = input.value.replace(/\D/g, '');
            value = value.replace(/(\d{3})(\d)/, '$1.$2');
            value = value.replace(/(\d{3})(\d)/, '$1.$2');
            value = value.replace(/(\d{3})(\d{1,2})$/, '$1-$2');
            input.value = value;
        }

        function formatCardNumber(input) {
            let value = input.value.replace(/\D/g, '');
            value = value.replace(/(\d{4})(?=\d)/g, '$1 ');
            input.value = value;
        }

        function formatExpiry(input) {
            let value = input.value.replace(/\D/g, '');
            value = value.replace(/(\d{2})(\d)/, '$1/$2');
            input.value = value;
        }

        function isValidCPF(cpf) {
            cpf = cpf.replace(/\D/g, '');
            if (cpf.length !== 11) return false;
            
            // Check for known invalid patterns
            if (/^(\d)\1{10}$/.test(cpf)) return false;
            
            // Validate check digits
            let sum = 0;
            for (let i = 0; i < 9; i++) {
                sum += parseInt(cpf.charAt(i)) * (10 - i);
            }
            let remainder = (sum * 10) % 11;
            if (remainder === 10 || remainder === 11) remainder = 0;
            if (remainder !== parseInt(cpf.charAt(9))) return false;
            
            sum = 0;
            for (let i = 0; i < 10; i++) {
                sum += parseInt(cpf.charAt(i)) * (11 - i);
            }
            remainder = (sum * 10) % 11;
            if (remainder === 10 || remainder === 11) remainder = 0;
            if (remainder !== parseInt(cpf.charAt(10))) return false;
            
            return true;
        }

        // Plan and payment selection handlers
        function handlePlanSelection() {
            const planRadios = document.querySelectorAll('input[name="selectedPlan"]');
            const planOptions = document.querySelectorAll('.plan-option');
            const selectedPlanName = document.getElementById('selectedPlanName');
            const selectedPlanPrice = document.getElementById('selectedPlanPrice');
            const firstBilling = document.getElementById('firstBilling');
            
            planRadios.forEach((radio, index) => {
                radio.addEventListener('change', function() {
                    // Remove selected class from all options
                    planOptions.forEach(option => option.classList.remove('selected'));
                    
                    // Add selected class to chosen option
                    if (this.checked) {
                        planOptions[index].classList.add('selected');
                        
                        const planData = {
                            'pro': { name: 'Pro', price: 'R$ 9,90' },
                            'premium': { name: 'Premium', price: 'R$ 19,90' },
                            'saudavel': { name: '+Saudável', price: 'R$ 29,90' }
                        };
                        
                        const plan = planData[this.value];
                        selectedPlanName.textContent = plan.name;
                        selectedPlanPrice.textContent = plan.price;
                        
                        // Calculate first billing date (7 days from now)
                        const firstBillingDate = new Date();
                        firstBillingDate.setDate(firstBillingDate.getDate() + 7);
                        firstBilling.textContent = firstBillingDate.toLocaleDateString('pt-BR');
                    }
                });
            });
        }

        function handlePaymentSelection() {
            const paymentRadios = document.querySelectorAll('input[name="paymentMethod"]');
            const paymentOptions = document.querySelectorAll('.payment-option');
            const creditCardFields = document.getElementById('creditCardFields');
            const pixInfo = document.getElementById('pixInfo');
            
            paymentRadios.forEach((radio, index) => {
                radio.addEventListener('change', function() {
                    // Remove selected class from all options
                    paymentOptions.forEach(option => option.classList.remove('selected'));
                    
                    // Add selected class to chosen option
                    if (this.checked) {
                        paymentOptions[index].classList.add('selected');
                        
                        if (this.value === 'credit') {
                            creditCardFields.classList.remove('hidden');
                            pixInfo.classList.add('hidden');
                            
                            // Make card fields required
                            const cardInputs = creditCardFields.querySelectorAll('input');
                            cardInputs.forEach(input => input.required = true);
                        } else {
                            creditCardFields.classList.add('hidden');
                            pixInfo.classList.remove('hidden');
                            
                            // Remove required from card fields
                            const cardInputs = creditCardFields.querySelectorAll('input');
                            cardInputs.forEach(input => input.required = false);
                        }
                    }
                });
            });
        }

        // Map animation functions
        function startMapAnimation() {
            const searchAnimation = document.getElementById('searchAnimation');
            if (searchAnimation) {
                searchAnimation.style.opacity = '1';
                
                // Create pulsing search effect
                mapAnimationInterval = setInterval(() => {
                    const stores = document.querySelectorAll('.store-marker');
                    stores.forEach((store, index) => {
                        setTimeout(() => {
                            store.style.transform = 'scale(1.5)';
                            store.style.opacity = '0.8';
                            setTimeout(() => {
                                store.style.transform = 'scale(1)';
                                store.style.opacity = '0.3';
                            }, 300);
                        }, index * 200);
                    });
                }, 2000);
            }
        }

        function stopMapAnimation() {
            const searchAnimation = document.getElementById('searchAnimation');
            if (searchAnimation) {
                searchAnimation.style.opacity = '0';
            }
            
            if (mapAnimationInterval) {
                clearInterval(mapAnimationInterval);
                mapAnimationInterval = null;
            }
            
            // Reset store markers
            const stores = document.querySelectorAll('.store-marker');
            stores.forEach(store => {
                store.style.transform = 'scale(1)';
                store.style.opacity = '0.3';
            });
        }

        // Account section functions
        function showAccountSection(sectionName) {
            // Hide all account sections
            document.querySelectorAll('.account-section').forEach(section => {
                section.classList.add('hidden');
            });
            
            // Show selected section
            const targetSection = document.getElementById(`account-${sectionName}`);
            if (targetSection) {
                targetSection.classList.remove('hidden');
            }
            
            // Update tab active state
            document.querySelectorAll('.account-tab').forEach(tab => {
                tab.classList.remove('active', 'bg-white/50');
            });
            
            // Find and activate the corresponding tab
            const activeTab = document.querySelector(`[onclick="showAccountSection('${sectionName}')"]`);
            if (activeTab) {
                activeTab.classList.add('active', 'bg-white/50');
            }
        }

        function updateProfile() {
            const name = document.getElementById('profileName').value;
            const email = document.getElementById('profileEmail').value;
            
            if (!name || !email) {
                showNotification('Erro', 'Preencha todos os campos obrigatórios', 'error');
                return;
            }
            
            // Update current user
            if (currentUser) {
                currentUser.name = name;
                currentUser.email = email;
                updateUserInterface();
                showNotification('Perfil Atualizado!', 'Suas informações foram salvas com sucesso', 'success');
            }
        }

        function cancelSubscription() {
            if (confirm('Tem certeza que deseja cancelar sua assinatura? Você perderá acesso às funcionalidades premium.')) {
                showNotification('Assinatura Cancelada', 'Sua assinatura será cancelada no final do período atual', 'info');
            }
        }

        function removeAlert(alertId) {
            if (confirm('Deseja remover este alerta de preço?')) {
                showNotification('Alerta Removido', 'O alerta foi removido com sucesso', 'success');
            }
        }

        function viewAlert(alertId) {
            showNotification('Oferta Encontrada!', 'Redirecionando para a melhor oferta...', 'success');
        }

        function saveSettings() {
            showNotification('Configurações Salvas!', 'Suas preferências foram atualizadas', 'success');
        }

        // TEST LOGIN FUNCTION - REMOVE IN PRODUCTION
        function testLogin() {
            currentUser = {
                uid: 'test_user_123',
                name: 'João Silva',
                email: 'joao@teste.com',
                plan: 'Premium',
                paymentMethod: 'credit',
                createdAt: new Date(),
                savings: 156.80,
                isTrialActive: false,
                trialEndsAt: null,
                cpf: '123.456.789-00'
            };
            
            isLoggedIn = true;
            cart = []; // Start with empty cart
            
            updateUserInterface();
            updateCartDisplay();
            
            showNotification('Login de Teste!', 'Usuário João Silva logado com sucesso', 'success');
            
            console.log('TEST LOGIN ACTIVATED');
            console.log('Current User:', currentUser);
            console.log('Is Logged In:', isLoggedIn);
        }

        // Initialize page
        document.addEventListener('DOMContentLoaded', function() {
            // Close modals when clicking outside
            document.querySelectorAll('.modal').forEach(modal => {
                modal.addEventListener('click', function(e) {
                    if (e.target === modal) {
                        modal.classList.remove('active');
                    }
                });
            });
            
            // Initialize user interface
            updateUserInterface();
            updateCartDisplay();
            
            // Initialize form handlers
            handlePlanSelection();
            handlePaymentSelection();
            
            // AUTO TEST LOGIN - REMOVE IN PRODUCTION
            setTimeout(() => {
                testLogin();
            }, 1000);
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9715399a442c6d7b',t:'MTc1NTU2MDA5OS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
