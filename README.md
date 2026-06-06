
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matevidadigital Pro 🤖</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;700;900&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        azul: '#0070f3', amarillo: '#FFD700', verde: '#00dc82', naranja: '#ff4d4d', rosado: '#ff007a', dark: '#0a0a0a'
                    }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Outfit', sans-serif; background: #f0f2f5; margin: 0; padding: 0; }
        .vibrant-gradient { background: linear-gradient(135deg, #0070f3 0%, #ff007a 100%); }
        .tab-btn.active { background: #0070f3; color: white; transform: scale(1.05); box-shadow: 0 10px 20px rgba(0, 112, 243, 0.3); }
        .game-card { transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); cursor: pointer; position: relative; overflow: hidden; }
        .game-card:hover { transform: translateY(-8px); }
        #timerBar { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 8px; background: #eee; z-index: 2000; }
        #timerProgress { height: 100%; background: #ff007a; width: 100%; transition: width 1s linear; }
        iframe { width: 100%; height: 100%; border: none; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
    </style>
</head>
<body class="pb-24">

    <!-- BARRA DE TIEMPO PARA JUEGOS LIMITADOS -->
    <div id="timerBar"><div id="timerProgress"></div></div>

    <!-- 1. REGISTRO MEJORADO -->
    <div id="authOverlay" class="fixed inset-0 z-[100] flex items-center justify-center vibrant-gradient p-4">
        <div class="bg-white rounded-[3rem] p-8 max-w-md w-full shadow-2xl text-center">
            <div class="text-7xl mb-4">🤖</div>
            <h2 class="text-3xl font-black text-dark mb-6 tracking-tight uppercase">Matevidadigital Pro</h2>
            
            <div id="authStep1" class="space-y-4">
                <button onclick="showEmailLogin()" class="w-full flex items-center justify-center gap-3 bg-white border-2 border-gray-100 py-4 rounded-2xl font-bold text-gray-600 hover:bg-gray-50 transition">
                    <img src="https://www.gstatic.com/images/branding/product/1x/googleg_48dp.png" class="w-6"> Continuar con Google
                </button>
                <button onclick="showEmailLogin()" class="w-full flex items-center justify-center gap-3 bg-dark text-white py-4 rounded-2xl font-bold hover:opacity-90 transition">
                    <i class="fas fa-envelope"></i> Continuar con Correo
                </button>
            </div>

            <form id="authForm" class="hidden space-y-4 mt-4">
                <input type="text" id="regName" placeholder="Tu Nombre de Usuario" required class="w-full px-6 py-4 rounded-2xl bg-gray-100 border-2 border-transparent focus:border-azul outline-none font-bold">
                <input type="email" id="regEmail" placeholder="correo@ejemplo.com" required class="w-full px-6 py-4 rounded-2xl bg-gray-100 border-2 border-transparent focus:border-azul outline-none">
                <button type="submit" class="w-full bg-azul text-white font-black py-5 rounded-2xl text-xl shadow-xl uppercase tracking-widest">ENTRAR</button>
            </form>
        </div>
    </div>

    <!-- 2. HEADER -->
    <header class="bg-white sticky top-0 z-50 px-6 py-4 border-b-2 border-gray-100 shadow-sm">
        <div class="max-w-6xl mx-auto flex justify-between items-center">
            <div class="flex items-center gap-2">
                <span class="text-3xl">🤖</span>
                <h1 class="text-xl font-black text-azul tracking-tighter">MATEVIDADIGITAL</h1>
            </div>
            <div id="profileBtn" class="flex items-center gap-3 bg-gray-100 px-4 py-1 rounded-full border-2 border-gray-200 cursor-pointer hover:border-azul transition" ondblclick="askAdmin()">
                <span id="navUserName" class="font-bold text-gray-700 text-sm">Cargando...</span>
                <div class="text-2xl">🤖</div>
            </div>
        </div>
        
        <nav class="max-w-6xl mx-auto mt-4 flex gap-2 overflow-x-auto no-scrollbar">
            <button onclick="changeTab('inicio')" id="btn-inicio" class="tab-btn active px-6 py-3 rounded-2xl font-black text-xs flex items-center gap-2"><i class="fas fa-house"></i> INICIO</button>
            <button onclick="changeTab('juegos')" id="btn-juegos" class="tab-btn bg-white text-gray-400 px-6 py-3 rounded-2xl font-black text-xs flex items-center gap-2"><i class="fas fa-gamepad"></i> JUEGOS</button>
            <button onclick="changeTab('fichas')" id="btn-fichas" class="tab-btn bg-white text-gray-400 px-6 py-3 rounded-2xl font-black text-xs flex items-center gap-2"><i class="fas fa-file-invoice"></i> FICHAS</button>
            <button onclick="changeTab('premium')" id="btn-premium" class="tab-btn bg-white text-gray-400 px-6 py-3 rounded-2xl font-black text-xs flex items-center gap-2"><i class="fas fa-crown"></i> PREMIUM</button>
        </nav>
    </header>

    <main class="max-w-6xl mx-auto p-4 sm:p-6">
        
        <!-- INICIO -->
        <section id="sec-inicio" class="tab-section h-[85vh]">
            <div class="vibrant-gradient rounded-[2.5rem] p-8 text-white shadow-xl mb-6 flex justify-between items-center overflow-hidden">
                <div class="z-10">
                    <h2 class="text-3xl font-black mb-1">¡HOLA, <span id="helloName" class="uppercase">JUAN</span>!</h2>
                    <p class="font-bold opacity-80 mb-4">¿Qué quieres aprender hoy?</p>
                    <button onclick="changeTab('juegos')" class="bg-white text-azul font-black px-6 py-3 rounded-xl shadow-lg uppercase text-sm">JUGAR AHORA</button>
                </div>
                <div class="text-9xl opacity-20 rotate-12">🤖</div>
            </div>
            <div class="h-full bg-white rounded-[2.5rem] shadow-xl overflow-hidden border-8 border-white">
                <iframe src="https://fonklexdy-cell.github.io/BIENVENIDOS/"></iframe>
            </div>
        </section>

        <!-- JUEGOS -->
        <section id="sec-juegos" class="tab-section hidden">
            <h3 class="text-2xl font-black text-dark mb-6 uppercase tracking-tighter">Zona de Desafíos</h3>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4" id="gridJuegos"></div>
        </section>

        <!-- FICHAS -->
        <section id="sec-fichas" class="tab-section hidden h-[85vh]">
            <div class="h-full bg-white rounded-[3rem] shadow-2xl overflow-hidden border-8 border-white">
                <iframe src="https://fonklexdy-cell.github.io/Recursos-Mate/"></iframe>
            </div>
        </section>

        <!-- PREMIUM -->
        <section id="sec-premium" class="tab-section hidden h-[85vh]">
            <div class="h-full bg-white rounded-[3rem] shadow-2xl overflow-hidden border-8 border-white">
                <iframe src="https://fonklexdy-cell.github.io/BilleteraMovil/"></iframe>
            </div>
        </section>
    </main>

    <!-- MODAL BLOQUEO PREMIUM -->
    <div id="premiumModal" class="fixed inset-0 z-[200] hidden flex items-center justify-center bg-dark/95 backdrop-blur-md p-6 text-center">
        <div class="bg-white rounded-[3rem] p-10 max-w-sm w-full shadow-2xl border-t-8 border-rosado">
            <div class="text-6xl mb-4">⏳</div>
            <h3 class="text-2xl font-black mb-2">TIEMPO AGOTADO</h3>
            <p class="text-gray-500 font-bold mb-8">Para jugar sin límites, activa tu cuenta Premium ahora.</p>
            <button onclick="changeTab('premium'); document.getElementById('premiumModal').classList.add('hidden')" class="w-full bg-rosado text-white font-black py-4 rounded-2xl text-lg shadow-xl uppercase">Activar Premium</button>
        </div>
    </div>

    <!-- PANEL ADMIN -->
    <div id="adminPanel" class="fixed inset-0 z-[300] hidden bg-gray-100 p-6 overflow-y-auto">
        <div class="max-w-4xl mx-auto bg-white rounded-[3rem] p-10 shadow-2xl border-4 border-azul">
            <div class="flex justify-between items-center mb-8">
                <h2 class="text-3xl font-black text-azul uppercase">Administrador 🤖</h2>
                <button onclick="toggleAdmin()" class="bg-red-500 text-white px-6 py-2 rounded-full font-bold">Cerrar</button>
            </div>
            <div class="overflow-hidden rounded-2xl border-2 border-gray-100">
                <table class="w-full text-left font-bold">
                    <thead class="bg-gray-50 border-b">
                        <tr><th class="p-6">Alumno</th><th class="p-6">Status</th><th class="p-6 text-right">Acción</th></tr>
                    </thead>
                    <tbody id="userTable"></tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        let db = JSON.parse(localStorage.getItem('mate_db')) || [];
        let session = JSON.parse(localStorage.getItem('mate_session')) || null;
        let timerId;

        const juegos = [
            { n: "Carrera Op", u: "https://brimar26.github.io/Carrera-de-Operaciones/", i: "fa-car", c: "bg-azul" },
            { n: "Tesoro", u: "https://brimar26.github.io/Tesoro-de-la-Librer-a/", i: "fa-gem", c: "bg-verde" },
            { n: "X-Tablas", u: "https://brimar26.github.io/X-tablas/", i: "fa-times", c: "bg-rosado" },
            { n: "Operaciones", u: "https://brimar26.github.io/Operaciones-Matem-ticas/", i: "fa-calculator", c: "bg-amarillo" },
            { n: "Dados Mágicos", u: "https://brimar26.github.io/DADOS-M-GICOS/", i: "fa-dice", c: "bg-indigo-500" },
            { n: "Matecarrera", u: "https://brimar26.github.io/Matecarrera/", i: "fa-flag-checkered", c: "bg-naranja" },
            { n: "La Escuela", u: "https://brimar26.github.io/La-escuela/", i: "fa-school", c: "bg-violet-600" },
            { n: "Mate Escudo", u: "https://brimar26.github.io/Mate-Escudo/", i: "fa-shield-halved", c: "bg-sky-500" },
            { n: "Ruleta Tablas", u: "https://brimar26.github.io/Ruleta-Tablas-y-Divisiones/", i: "fa-circle-dot", c: "bg-pink-400" },
            { n: "Maestro Ruleta", u: "https://brimar26.github.io/Escuela-Matematica-Ruleta/", i: "fa-chalkboard-user", c: "bg-emerald-500" },
            { n: "Multi Pro", u: "https://brimar26.github.io/Tablas-de-Multiplicar-Pro/", i: "fa-star", c: "bg-blue-600" },
            { n: "Nivel Pali", u: "https://brimar26.github.io/Nivel-Pali/", i: "fa-medal", c: "bg-red-500" },
            { n: "Desafío Total", u: "https://brimar26.github.io/Desafio-Total/", i: "fa-fire", c: "bg-orange-600" },
            { n: "El Mercado", u: "https://brimar26.github.io/El-Mercado/", i: "fa-shop", c: "bg-teal-500" },
            { n: "Espacial", u: "https://brimar26.github.io/Mate-Aventura-Espacial-/", i: "fa-rocket", c: "bg-slate-800" },
            { n: "Mate Xpress", u: "https://brimar26.github.io/Mate-Xpress/", i: "fa-bolt", c: "bg-blue-400" },
            { n: "Mensaje Secreto", u: "https://brimar26.github.io/Mensaje-Secreto/", i: "fa-user-secret", c: "bg-purple-500" },
            { n: "Tablas Mix", u: "https://brimar26.github.io/tablas-de-multiplicar/", i: "fa-list-ol", c: "bg-rose-500" },
            { n: "APP COMPLETA", u: "https://matevidadigital.base44.app", i: "fa-crown", c: "bg-dark text-amarillo" }
        ];

        window.onload = () => {
            if(session) {
                document.getElementById('authOverlay').classList.add('hidden');
                updateUI();
            }
            renderJuegos();
        };

        function showEmailLogin() {
            document.getElementById('authStep1').classList.add('hidden');
            document.getElementById('authForm').classList.remove('hidden');
        }

        document.getElementById('authForm').onsubmit = (e) => {
            e.preventDefault();
            const name = document.getElementById('regName').value;
            const email = document.getElementById('regEmail').value;
            let user = db.find(u => u.email === email);
            if(!user) {
                user = { name, email, status: 'gratis', id: Date.now() };
                db.push(user);
                localStorage.setItem('mate_db', JSON.stringify(db));
            }
            session = user;
            localStorage.setItem('mate_session', JSON.stringify(session));
            document.getElementById('authOverlay').classList.add('hidden');
            updateUI();
        };

        function updateUI() {
            document.getElementById('navUserName').innerText = session.name;
            document.getElementById('helloName').innerText = session.name;
        }

        function renderJuegos() {
            const grid = document.getElementById('gridJuegos');
            grid.innerHTML = "";
            juegos.forEach((j, index) => {
                const card = document.createElement('div');
                const isPremium = index >= 4 && session?.status === 'gratis';
                card.className = `game-card h-40 rounded-[2rem] p-6 flex flex-col items-center justify-center text-center shadow-lg border-2 border-white ${j.c}`;
                card.onclick = () => launch(j, index);
                card.innerHTML = `
                    <div class="text-4xl mb-2"><i class="fas ${j.i} text-white"></i></div>
                    <span class="text-white font-black text-xs uppercase tracking-tighter leading-none">${j.n}</span>
                    ${isPremium ? '<div class="absolute top-2 right-2 text-amarillo text-xs"><i class="fas fa-lock"></i></div>' : ''}
                `;
                grid.appendChild(card);
            });
        }

        function launch(g, index) {
            const win = window.open(g.u, '_blank');
            
            // LÓGICA DE 10 SEGUNDOS (A partir del 5to juego, índice 4)
            if(index >= 4 && session.status === 'gratis') {
                const bar = document.getElementById('timerBar');
                const progress = document.getElementById('timerProgress');
                bar.style.display = 'block';
                progress.style.width = '100%';
                
                let timeLeft = 15;
                clearInterval(timerId);
                
                timerId = setInterval(() => {
                    timeLeft--;
                    progress.style.width = (timeLeft * 10) + '%';
                    
                    if(timeLeft <= 0) {
                        clearInterval(timerId);
                        bar.style.display = 'none';
                        if(win) win.close(); // Intenta cerrar la pestaña
                        document.getElementById('premiumModal').classList.remove('hidden');
                    }
                }, 1000);
            }
        }

        function changeTab(t) {
            document.querySelectorAll('.tab-section').forEach(s => s.classList.add('hidden'));
            document.getElementById('sec-' + t).classList.remove('hidden');
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active', 'bg-white', 'text-gray-400'));
            document.getElementById('btn-' + t).classList.add('active');
        }

        function askAdmin() {
            const pass = prompt("🔐 Contraseña Admin:");
            if(pass === "PRO2024") toggleAdmin();
        }

        function toggleAdmin() {
            const p = document.getElementById('adminPanel');
            p.classList.toggle('hidden');
            if(!p.classList.contains('hidden')) renderAdmin();
        }

        function renderAdmin() {
            const tbody = document.getElementById('userTable');
            tbody.innerHTML = "";
            db.forEach(u => {
                const tr = document.createElement('tr');
                tr.className = "border-b hover:bg-gray-50 transition";
                tr.innerHTML = `
                    <td class="p-6 text-azul font-black uppercase text-sm">${u.name}</td>
                    <td class="p-6"><span class="px-3 py-1 rounded-full text-[10px] font-black uppercase ${u.status === 'premium' ? 'bg-verde/20 text-verde' : 'bg-gray-100 text-gray-400'}">${u.status}</span></td>
                    <td class="p-6 text-right"><button onclick="toggleUserStatus('${u.email}')" class="text-rosado font-black text-xs underline uppercase">Alternar</button></td>
                `;
                tbody.appendChild(tr);
            });
        }

        function toggleUserStatus(email) {
            db = db.map(u => {
                if(u.email === email) u.status = (u.status === 'gratis' ? 'premium' : 'gratis');
                return u;
            });
            localStorage.setItem('mate_db', JSON.stringify(db));
            if(session.email === email) {
                session.status = (session.status === 'gratis' ? 'premium' : 'gratis');
                localStorage.setItem('mate_session', JSON.stringify(session));
            }
            renderAdmin();
            renderJuegos();
        }
    </script>
</body>
</html>
