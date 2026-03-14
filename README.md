# Sa_nails_art
salon de uñas
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>sa.nails_art - Folleto Digital Interactivo</title>
    <!-- Tailwind CSS para el diseño base -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Fuentes de Google -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Dancing+Script:wght@700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-pink: #fce4ec;
            --accent-pink: #f06292;
            --dark-pink: #ad1457;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #fdf2f8 0%, #fce4ec 50%, #fbcfe8 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: 2rem 1rem;
            margin: 0;
            overflow-y: auto;
            position: relative;
        }

        /* Decoración: Emojis flotantes */
        .floating-emoji {
            position: fixed;
            pointer-events: none;
            z-index: 0;
            font-size: 1.5rem;
            animation: float 15s linear infinite;
            opacity: 0.4;
        }

        @keyframes float {
            0% { transform: translateY(110vh) rotate(0deg); }
            100% { transform: translateY(-10vh) rotate(360deg); }
        }

        /* Estilo Glassmorphism */
        .glass-card {
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border-radius: 2rem;
            border: 1px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 10px 40px 0 rgba(240, 98, 146, 0.15);
            width: 100%;
            max-width: 450px;
            padding: 2.5rem 1.5rem;
            margin-bottom: 2rem;
            animation: fadeIn 0.8s ease-out;
            position: relative;
            z-index: 10;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(15px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .title-font {
            font-family: 'Dancing Script', cursive;
            color: var(--dark-pink);
        }

        .btn-option {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: 2px solid transparent;
            width: 100%;
            text-align: left;
            background-color: rgba(255, 255, 255, 0.6);
        }

        .btn-option:hover {
            transform: translateY(-2px);
            background-color: white;
            box-shadow: 0 4px 12px rgba(240, 98, 146, 0.1);
        }

        .step-container {
            display: none;
        }

        .step-container.active {
            display: block;
            animation: slideIn 0.4s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: scale(0.98); }
            to { opacity: 1; transform: scale(1); }
        }

        /* Indicadores de progreso */
        .progress-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: #e2e8f0;
            transition: all 0.3s;
        }

        .progress-dot.active {
            background-color: var(--accent-pink);
            width: 24px;
        }

        /* Contador para retiro */
        .counter-btn {
            width: 50px;
            height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: white;
            border-radius: 15px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            font-size: 1.5rem;
            color: var(--accent-pink);
            transition: all 0.2s;
        }

        .counter-btn:active {
            transform: scale(0.9);
            background-color: var(--primary-pink);
        }

        /* Navegación Volver */
        .back-nav {
            position: absolute;
            top: 1.5rem;
            left: 1.5rem;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s;
        }
        
        .back-nav.visible {
            opacity: 1;
            pointer-events: auto;
        }
    </style>
</head>
<body>

    <!-- Contenedor para los emojis flotantes -->
    <div id="emoji-container"></div>

    <div class="glass-card">
        <!-- Botón Volver -->
        <button id="globalBackBtn" onclick="goBack()" class="back-nav text-pink-500 flex items-center gap-1 font-medium text-sm hover:underline">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
            </svg>
            Volver
        </button>

        <!-- Cabecera -->
        <header class="text-center mt-4 mb-8">
            <h1 class="text-4xl title-font mb-1">sa.nails_art</h1>
            <p class="text-gray-500 text-sm italic">Calculá el precio de tu servicio ✨</p>
        </header>

        <!-- Indicador de pasos -->
        <div class="flex justify-center space-x-2 mb-8" id="progressBar">
            <div class="progress-dot active"></div>
            <div class="progress-dot"></div>
            <div class="progress-dot"></div>
            <div class="progress-dot"></div>
        </div>

        <!-- PASO 1: Técnica -->
        <div class="step-container active" id="step1">
            <h2 class="text-lg font-semibold text-gray-700 mb-4 text-center">1. Elegí la técnica 💅</h2>
            <div class="grid grid-cols-1 gap-3">
                <button onclick="selectStep1('Acrílico')" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>Acrílico</span>
                    <span class="text-pink-400">→</span>
                </button>
                <button onclick="selectStep1('Semipermanente')" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>Semipermanente</span>
                    <span class="text-pink-400">→</span>
                </button>
                <button onclick="selectStep1('Capping')" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>Capping</span>
                    <span class="text-pink-400">→</span>
                </button>
                <button onclick="selectStep1('Retiro')" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>Retiro</span>
                    <span class="text-pink-400">→</span>
                </button>
            </div>
        </div>

        <!-- PASO 2: Opciones Dinámicas -->
        <div class="step-container" id="step2">
            <h2 class="text-lg font-semibold text-gray-700 mb-4 text-center" id="step2Title">2. Elegí el detalle 📏</h2>
            <div id="step2Options" class="grid grid-cols-1 gap-3"></div>
        </div>

        <!-- PASO 3: Adicionales -->
        <div class="step-container" id="step3">
            <h2 class="text-lg font-semibold text-gray-700 mb-4 text-center">3. ¿Algún adicional? 🌸</h2>
            <div class="grid grid-cols-1 gap-3">
                <button onclick="selectStep3('Servicio base', 0)" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>1️⃣ Servicio base</span>
                    <span class="text-gray-400">$0</span>
                </button>
                <button onclick="selectStep3('Retoque', 1000)" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>2️⃣ Retoque</span>
                    <span class="text-pink-400">+$1.000</span>
                </button>
                <button onclick="selectStep3('Retiro trabajo mío', 2000)" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>3️⃣ Retiro (mi trabajo)</span>
                    <span class="text-pink-400">+$2.000</span>
                </button>
                <button onclick="selectStep3('Retiro otro lugar', 5000)" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>4️⃣ Retiro (otro lugar)</span>
                    <span class="text-pink-400">+$5.000</span>
                </button>
            </div>
        </div>

        <!-- PASO 4: Diseño -->
        <div class="step-container" id="step4">
            <h2 class="text-lg font-semibold text-gray-700 mb-4 text-center">4. Elegí tu diseño 🎨</h2>
            <div class="grid grid-cols-1 gap-3">
                <button onclick="finishCalculation('Clásico', 1000)" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>💅 Clásico</span>
                    <span class="text-gray-400">+$1.000</span>
                </button>
                <button onclick="finishCalculation('Solo esmalte', 1500)" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>💅 Solo esmalte</span>
                    <span class="text-gray-400">+$1.500</span>
                </button>
                <button onclick="finishCalculation('Personalizado', 6000)" class="btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm">
                    <span>👑 Personalizado</span>
                    <span class="text-gray-400">+$6.000</span>
                </button>
            </div>
        </div>

        <!-- PASO ESPECIAL: Contador para Retiro -->
        <div class="step-container" id="stepCounter">
            <h2 class="text-lg font-semibold text-gray-700 mb-4 text-center">Cantidad de uñas a retirar</h2>
            <div class="flex items-center justify-center space-x-8 my-10">
                <button onclick="updateUñas(-1)" class="counter-btn font-bold">-</button>
                <span id="uñasValue" class="text-5xl font-bold text-gray-700 w-16 text-center">10</span>
                <button onclick="updateUñas(1)" class="counter-btn font-bold">+</button>
            </div>
            <button onclick="calculateRetiro()" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-semibold py-4 rounded-2xl shadow-lg transition-colors">
                Continuar
            </button>
        </div>

        <!-- RESULTADO FINAL -->
        <div class="step-container" id="stepResult">
            <div class="mb-6 text-center">
                <div class="text-gray-400 text-xs uppercase tracking-widest mb-2">Total Estimado</div>
                <div class="text-5xl font-bold text-pink-600 mb-4" id="totalPrice">$0</div>
                <div id="breakdown" class="text-sm text-gray-600 bg-white/40 p-5 rounded-2xl text-left border border-white/60 space-y-1"></div>
            </div>

            <div class="space-y-3">
                <!-- Botón Agendar Cita -->
                <a href="https://calendar.app.google/r8PVFaNYKqZASr91A" target="_blank" class="block w-full bg-pink-500 hover:bg-pink-600 text-white text-center font-semibold py-4 rounded-2xl shadow-lg shadow-pink-100 transition-all transform hover:-translate-y-1">
                    📅 Agendar cita
                </a>
                <!-- Botón WhatsApp -->
                <a href="https://wa.me/541171446016" target="_blank" class="block w-full bg-white text-pink-600 text-center font-semibold py-4 rounded-2xl border-2 border-pink-100 hover:border-pink-200 transition-all">
                    💬 Más información por WhatsApp
                </a>
            </div>

            <button onclick="restart()" class="w-full mt-6 text-xs text-pink-400 uppercase tracking-widest hover:underline text-center">Reiniciar cálculo</button>
        </div>

        <!-- Footer -->
        <footer class="mt-10 pt-6 border-t border-pink-100 text-center">
            <p class="text-gray-500 text-sm font-medium">✨ Agenda tu cita con nosotros ✨</p>
            <p class="text-pink-500 font-bold text-lg">@sa.nails_art</p>
        </footer>
    </div>

    <script>
        // Estado de la aplicación
        let currentStepId = 'step1';
        let stepHistory = ['step1'];
        let selection = {
            tecnica: '',
            basePrice: 0,
            detalle: '',
            adicional: '',
            adicionalPrice: 0,
            diseno: '',
            disenoPrice: 0,
            uñas: 10
        };

        // Generar emojis flotantes al azar
        function initEmojis() {
            const container = document.getElementById('emoji-container');
            const emojis = ['💅', '✨', '💎', '🌸', '💖'];
            for (let i = 0; i < 15; i++) {
                const el = document.createElement('div');
                el.className = 'floating-emoji';
                el.innerText = emojis[Math.floor(Math.random() * emojis.length)];
                el.style.left = Math.random() * 90 + 'vw';
                el.style.animationDelay = Math.random() * 15 + 's';
                el.style.animationDuration = (Math.random() * 8 + 10) + 's';
                container.appendChild(el);
            }
        }

        // Navegación entre pasos
        function showStep(stepId) {
            document.querySelectorAll('.step-container').forEach(el => el.classList.remove('active'));
            document.getElementById(stepId).classList.add('active');
            currentStepId = stepId;
            
            // Guardar en historial si es un avance
            if (stepHistory[stepHistory.length - 1] !== stepId) {
                stepHistory.push(stepId);
            }

            // Visibilidad del botón Volver
            const backBtn = document.getElementById('globalBackBtn');
            if (stepId === 'step1') {
                backBtn.classList.remove('visible');
            } else {
                backBtn.classList.add('visible');
            }

            // Actualizar bolitas de progreso
            const dots = document.querySelectorAll('.progress-dot');
            dots.forEach(dot => dot.classList.remove('active'));
            
            if(stepId === 'step1') dots[0].classList.add('active');
            else if(stepId === 'step2' || stepId === 'stepCounter') dots[1].classList.add('active');
            else if(stepId === 'step3') dots[2].classList.add('active');
            else if(stepId === 'step4' || stepId === 'stepResult') dots[3].classList.add('active');

            // Scroll automático arriba
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function goBack() {
            if (stepHistory.length > 1) {
                stepHistory.pop(); // Elimina el paso actual
                const prev = stepHistory.pop(); // Obtiene y quita el anterior para re-insertarlo al llamar showStep
                showStep(prev);
            }
        }

        // Selección Técnica
        function selectStep1(tecnica) {
            selection.tecnica = tecnica;
            const step2Options = document.getElementById('step2Options');
            const step2Title = document.getElementById('step2Title');
            step2Options.innerHTML = '';

            if (tecnica === 'Acrílico') {
                step2Title.innerText = '2. Elegí el largo 📏';
                addOption(step2Options, 'Largo 1-2', 18000, 'step3');
                addOption(step2Options, 'Largo 3-4', 21000, 'step3');
            } else if (tecnica === 'Semipermanente') {
                step2Title.innerText = '2. ¿Manos o pies? 👣';
                addOption(step2Options, 'Manos', 12000, 'step3');
                addOption(step2Options, 'Pies', 15000, 'step3');
            } else if (tecnica === 'Capping') {
                step2Title.innerText = '2. Servicio Capping ✨';
                addOption(step2Options, 'Natural', 14000, 'step3');
            } else if (tecnica === 'Retiro') {
                step2Title.innerText = '2. Tipo de retiro 🗑️';
                addOption(step2Options, 'Acrílico', 1500, 'stepCounter');
                addOption(step2Options, 'Semipermanente', 1000, 'stepCounter');
            }
            showStep('step2');
        }

        function addOption(container, label, price, next) {
            const btn = document.createElement('button');
            btn.className = 'btn-option p-4 rounded-2xl text-gray-700 flex justify-between items-center shadow-sm';
            const priceLabel = selection.tecnica === 'Retiro' ? '$' + price + ' c/u' : '$' + price.toLocaleString();
            btn.innerHTML = `<span>${label}</span> <span class="text-pink-400 font-semibold">${priceLabel}</span>`;
            btn.onclick = () => {
                selection.detalle = label;
                selection.basePrice = price;
                showStep(next);
            };
            container.appendChild(btn);
        }

        // Funciones para Retiro (Contador)
        function updateUñas(val) {
            selection.uñas = Math.max(1, Math.min(20, selection.uñas + val));
            document.getElementById('uñasValue').innerText = selection.uñas;
        }

        function calculateRetiro() {
            const total = selection.basePrice * selection.uñas;
            document.getElementById('totalPrice').innerText = `$${total.toLocaleString()}`;
            document.getElementById('breakdown').innerHTML = `
                <div class="flex justify-between"><span>Retiro ${selection.detalle}</span> <span>$${selection.basePrice.toLocaleString()} c/u</span></div>
                <div class="flex justify-between font-bold text-pink-600 pt-2 border-t border-pink-100"><span>Cantidad</span> <span>${selection.uñas} uñas</span></div>
            `;
            showStep('stepResult');
        }

        // Funciones para Adicionales y Diseño
        function selectStep3(adicional, price) {
            selection.adicional = adicional;
            selection.adicionalPrice = price;
            showStep('step4');
        }

        function finishCalculation(diseno, price) {
            selection.diseno = diseno;
            selection.disenoPrice = price;

            const total = selection.basePrice + selection.adicionalPrice + selection.disenoPrice;
            document.getElementById('totalPrice').innerText = `$${total.toLocaleString()}`;

            const breakdown = document.getElementById('breakdown');
            breakdown.innerHTML = `
                <div class="flex justify-between"><span>Base: ${selection.tecnica} (${selection.detalle})</span> <span>$${selection.basePrice.toLocaleString()}</span></div>
                <div class="flex justify-between"><span>Adicional: ${selection.adicional}</span> <span>+$${selection.adicionalPrice.toLocaleString()}</span></div>
                <div class="flex justify-between font-bold text-pink-600 pt-2 border-t border-pink-100"><span>Diseño: ${selection.diseno}</span> <span>+$${selection.disenoPrice.toLocaleString()}</span></div>
            `;

            showStep('stepResult');
        }

        // Reinicio
        function restart() {
            selection = { tecnica: '', basePrice: 0, detalle: '', adicional: '', adicionalPrice: 0, diseno: '', disenoPrice: 0, uñas: 10 };
            stepHistory = ['step1'];
            document.getElementById('uñasValue').innerText = 10;
            showStep('step1');
        }

        // Ejecutar al cargar
        window.onload = initEmojis;
    </script>
</body>
</html>
