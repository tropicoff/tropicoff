<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ethan ROSSIGNOL | Développeur Hacker</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Major+Mono+Display&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Share Tech Mono', monospace;
            background-color: #000;
            color: #e2e2e2;
            overflow-x: hidden;
        }
        
        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: radial-gradient(circle at center, #1a0535 0%, #000 70%);
            opacity: 0.8;
        }
        
        .matrix-particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #9d4dff;
            border-radius: 50%;
            box-shadow: 0 0 5px #9d4dff, 0 0 10px #9d4dff;
        }
        
        .glitch {
            position: relative;
        }
        
        .glitch::before, .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: transparent;
        }
        
        .glitch::before {
            left: 2px;
            text-shadow: -2px 0 #ff00c1;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim 5s infinite linear alternate-reverse;
        }
        
        .glitch::after {
            left: -2px;
            text-shadow: -2px 0 #00fff9, 2px 2px #ff00c1;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim2 5s infinite linear alternate-reverse;
        }
        
        @keyframes glitch-anim {
            0% { clip: rect(31px, 9999px, 94px, 0); }
            10% { clip: rect(112px, 9999px, 76px, 0); }
            20% { clip: rect(85px, 9999px, 77px, 0); }
            30% { clip: rect(27px, 9999px, 97px, 0); }
            40% { clip: rect(64px, 9999px, 98px, 0); }
            50% { clip: rect(61px, 9999px, 85px, 0); }
            60% { clip: rect(99px, 9999px, 114px, 0); }
            70% { clip: rect(34px, 9999px, 115px, 0); }
            80% { clip: rect(98px, 9999px, 129px, 0); }
            90% { clip: rect(43px, 9999px, 96px, 0); }
            100% { clip: rect(82px, 9999px, 64px, 0); }
        }
        
        @keyframes glitch-anim2 {
            0% { clip: rect(65px, 9999px, 119px, 0); }
            10% { clip: rect(66px, 9999px, 101px, 0); }
            20% { clip: rect(76px, 9999px, 69px, 0); }
            30% { clip: rect(81px, 9999px, 84px, 0); }
            40% { clip: rect(28px, 9999px, 84px, 0); }
            50% { clip: rect(40px, 9999px, 78px, 0); }
            60% { clip: rect(95px, 9999px, 79px, 0); }
            70% { clip: rect(91px, 9999px, 105px, 0); }
            80% { clip: rect(98px, 9999px, 93px, 0); }
            90% { clip: rect(93px, 9999px, 96px, 0); }
            100% { clip: rect(106px, 9999px, 115px, 0); }
        }
        
        .fade-in {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        
        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }
        
        .blink {
            animation: blink 1s infinite;
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .terminal {
            border: 1px solid #9d4dff;
            border-radius: 5px;
            background-color: rgba(0, 0, 0, 0.7);
            box-shadow: 0 0 10px #9d4dff;
            padding: 15px;
            position: relative;
            overflow: hidden;
        }
        
        .terminal::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 25px;
            background: linear-gradient(90deg, #9d4dff, #6a00f4);
            opacity: 0.3;
        }
        
        .terminal-header {
            position: absolute;
            top: 5px;
            left: 10px;
            font-size: 0.8rem;
            color: #9d4dff;
        }
        
        .social-icon {
            transition: all 0.3s ease;
        }
        
        .social-icon:hover {
            transform: translateY(-3px);
            filter: drop-shadow(0 0 5px #9d4dff);
        }
        
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #000;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 9999;
        }
        
        .loading-text {
            color: #9d4dff;
            font-size: 1.5rem;
            margin-top: 20px;
            text-align: center;
        }
        
        .progress-bar {
            width: 80%;
            max-width: 300px;
            height: 3px;
            background-color: #1a0535;
            margin-top: 20px;
            overflow: hidden;
            border-radius: 3px;
        }
        
        .progress {
            height: 100%;
            width: 0;
            background-color: #9d4dff;
            transition: width 0.1s linear;
        }
        
        .code-line {
            color: #9d4dff;
            font-family: 'Share Tech Mono', monospace;
            white-space: nowrap;
            overflow: hidden;
            border-right: 2px solid #9d4dff;
            animation: typing 3.5s steps(40, end), blink-caret 0.75s step-end infinite;
        }
        
        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }
        
        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: #9d4dff }
        }
    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loading-screen" id="loadingScreen">
        <div class="terminal w-4/5 max-w-md">
            <div class="terminal-header">SYSTEM BOOT</div>
            <div class="mt-8 mb-4">
                <div class="code-line">Initializing system...</div>
                <div class="code-line">Loading core modules...</div>
                <div class="code-line">Establishing secure connection...</div>
                <div class="code-line">Welcome to ETHAN_ROSSIGNOL.exe</div>
            </div>
            <div class="progress-bar">
                <div class="progress" id="progressBar"></div>
            </div>
            <div class="loading-text blink">ACCESS GRANTED</div>
        </div>
    </div>

    <!-- Matrix Background -->
    <div class="matrix-bg" id="matrixBg"></div>

    <!-- Main Content -->
    <div class="container mx-auto px-4 py-12 relative" style="min-height: 100vh;">
        <!-- Hero Section -->
        <section class="min-h-screen flex flex-col justify-center items-center text-center">
            <h1 class="glitch text-5xl md:text-7xl font-bold mb-6 text-purple-400" data-text="ETHAN ROSSIGNOL">
                ETHAN ROSSIGNOL
            </h1>
            <p class="text-xl md:text-2xl text-purple-300 mb-8">Développeur Passionné • Hacker Créatif • Tech Enthousiaste</p>
            
            <div class="terminal w-full max-w-md mt-8 fade-in">
                <div class="terminal-header">BIO_15s.exe</div>
                <p class="text-left py-4 px-2">
                    > Je m'appelle Ethan Rossignol, j'ai 15 ans et je suis développeur passionné. Je fais partie de Trolix, un groupe de jeunes créateurs tech avec qui je développe des outils, logiciels et systèmes qu'on aurait adoré avoir plus jeunes. Mon projet principal : Lixie, un assistant vocal entièrement fait maison.
                </p>
                <div class="flex justify-center space-x-4 py-4">
                    <a href="https://www.instagram.com/ethan_rossignol_?igsh=N3BmMDI4aHc4NWJm&utm_source=qr" target="_blank" class="social-icon">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#9d4dff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                            <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                            <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
                        </svg>
                    </a>
                    <a href="https://t.snapchat.com/nv5w1MnO" target="_blank" class="social-icon">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#9d4dff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <path d="M22 12.5c0 5.8-4.7 10.5-10.5 10.5S1 18.3 1 12.5 5.7 2 11.5 2c2.9 0 5.5 1.2 7.4 3.1"></path>
                            <path d="M7.5 11.5c0-2.2 1.8-4 4-4s4 1.8 4 4-1.8 4-4 4-4-1.8-4-4z"></path>
                        </svg>
                    </a>
                </div>
            </div>
            
            <div class="absolute bottom-10 left-0 right-0 text-center">
                <p class="text-purple-400 blink">↓ SCROLL DOWN ↓</p>
            </div>
        </section>

        <!-- About Section -->
        <section class="min-h-screen flex flex-col justify-center py-20">
            <div class="terminal w-full max-w-3xl mx-auto fade-in">
                <div class="terminal-header">ABOUT_ME.txt</div>
                <div class="text-left py-4 px-2 space-y-4">
                    <p>> Je suis Ethan Rossignol, développeur autodidacte de 15 ans et passionné de tech depuis toujours.</p>
                    <p>> J'aime bidouiller, créer des outils informatiques, tester la sécurité des réseaux, et imaginer des projets que j'aurais rêvé utiliser plus jeune. Je fais partie de Trolix, un collectif de jeunes développeurs avec qui je partage cette passion de créer librement, selon nos idées et nos envies.</p>
                    <p>> Avec Trolix, on bosse sur des projets comme :</p>
                    <ul class="list-disc list-inside pl-4 text-purple-300">
                        <li>des logiciels de pentest pour tester nos réseaux,</li>
                        <li>des systèmes Linux personnalisés,</li>
                        <li>des interfaces web interactives et immersives,</li>
                        <li>des assistants IA ou clés USB bootables customisées.</li>
                    </ul>
                    <p>> De mon côté, je développe Lixie, un assistant vocal avec une interface animée, une vraie personnalité et des fonctions stylées.</p>
                    <p>> Ce projet représente bien ce que j'aime : mélanger technique, créativité, IA et design pour créer des expériences originales.</p>
                    <p>> Mon univers, c'est un mélange de style hacker, d'ambiance violet + noir, de nébuleuses animées et d'interfaces fluides pensées pour les utilisateurs mobiles ou tactiles.</p>
                    <p>> Pour moi, coder ce n'est pas juste écrire des lignes : c'est construire quelque chose de vivant, utile, et surtout qui me ressemble.</p>
                </div>
            </div>
        </section>

        <!-- Projects Section -->
        <section class="min-h-screen flex flex-col justify-center py-20">
            <h2 class="text-3xl md:text-4xl font-bold mb-12 text-center text-purple-400 fade-in">MES PROJETS</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 max-w-4xl mx-auto">
                <div class="terminal fade-in">
                    <div class="terminal-header">LIXIE.exe</div>
                    <div class="p-4">
                        <h3 class="text-xl text-purple-300 mb-2">Assistant Vocal</h3>
                        <p class="text-sm">Un assistant vocal avec personnalité, interface animée et fonctions customisées.</p>
                        <div class="mt-4 h-32 bg-gradient-to-br from-purple-900 to-black flex items-center justify-center">
                            <span class="text-purple-400">[DEMO COMING SOON]</span>
                        </div>
                    </div>
                </div>
                
                <div class="terminal fade-in">
                    <div class="terminal-header">TROLIX_OS</div>
                    <div class="p-4">
                        <h3 class="text-xl text-purple-300 mb-2">Système Linux</h3>
                        <p class="text-sm">Distribution Linux personnalisée pour les développeurs et hackers.</p>
                        <div class="mt-4 h-32 bg-gradient-to-br from-purple-900 to-black flex items-center justify-center">
                            <span class="text-purple-400">[WIP]</span>
                        </div>
                    </div>
                </div>
                
                <div class="terminal fade-in">
                    <div class="terminal-header">NET_SCANNER</div>
                    <div class="p-4">
                        <h3 class="text-xl text-purple-300 mb-2">Outil Pentest</h3>
                        <p class="text-sm">Scanner réseau pour tester la sécurité des systèmes.</p>
                        <div class="mt-4 h-32 bg-gradient-to-br from-purple-900 to-black flex items-center justify-center">
                            <span class="text-purple-400">[PRIVATE]</span>
                        </div>
                    </div>
                </div>
                
                <div class="terminal fade-in">
                    <div class="terminal-header">COMING_SOON</div>
                    <div class="p-4">
                        <h3 class="text-xl text-purple-300 mb-2">Projet Secret</h3>
                        <p class="text-sm">Un nouveau projet en développement... Stay tuned!</p>
                        <div class="mt-4 h-32 bg-gradient-to-br from-purple-900 to-black flex items-center justify-center">
                            <span class="text-purple-400 blink">[TOP SECRET]</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Footer -->
        <footer class="py-12 text-center fade-in">
            <div class="terminal w-full max-w-md mx-auto">
                <div class="terminal-header">CONTACT.exe</div>
                <div class="p-4">
                    <p class="mb-4">Pour toute collaboration ou discussion tech :</p>
                    <div class="flex justify-center space-x-6">
                        <a href="https://www.instagram.com/ethan_rossignol_?igsh=N3BmMDI4aHc4NWJm&utm_source=qr" target="_blank" class="social-icon">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#9d4dff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
                            </svg>
                        </a>
                        <a href="https://t.snapchat.com/nv5w1MnO" target="_blank" class="social-icon">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#9d4dff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M22 12.5c0 5.8-4.7 10.5-10.5 10.5S1 18.3 1 12.5 5.7 2 11.5 2c2.9 0 5.5 1.2 7.4 3.1"></path>
                                <path d="M7.5 11.5c0-2.2 1.8-4 4-4s4 1.8 4 4-1.8 4-4 4-4-1.8-4-4z"></path>
                            </svg>
                        </a>
                    </div>
                    <p class="mt-6 text-sm text-purple-300">© 2023 ETHAN ROSSIGNOL | Tous droits réservés</p>
                </div>
            </div>
        </footer>
    </div>

    <script>
        // Loading Screen Animation
        document.addEventListener('DOMContentLoaded', function() {
            const loadingScreen = document.getElementById('loadingScreen');
            const progressBar = document.getElementById('progressBar');
            const matrixBg = document.getElementById('matrixBg');
            
            // Simulate loading progress
            let progress = 0;
            const interval = setInterval(() => {
                progress += 1;
                progressBar.style.width = progress + '%';
                
                if (progress >= 100) {
                    clearInterval(interval);
                    setTimeout(() => {
                        loadingScreen.style.opacity = '0';
                        setTimeout(() => {
                            loadingScreen.style.display = 'none';
                            createMatrixParticles();
                        }, 500);
                    }, 300);
                }
            }, 30);
            
            // Create matrix particles
            function createMatrixParticles() {
                const particleCount = Math.floor(window.innerWidth / 10);
                
                for (let i = 0; i < particleCount; i++) {
                    const particle = document.createElement('div');
                    particle.classList.add('matrix-particle');
                    
                    // Random position
                    const posX = Math.random() * window.innerWidth;
                    const posY = Math.random() * window.innerHeight;
                    const size = Math.random() * 3 + 1;
                    const opacity = Math.random() * 0.5 + 0.1;
                    
                    particle.style.left = posX + 'px';
                    particle.style.top = posY + 'px';
                    particle.style.width = size + 'px';
                    particle.style.height = size + 'px';
                    particle.style.opacity = opacity;
                    
                    // Animation
                    const duration = Math.random() * 10 + 5;
                    const delay = Math.random() * 5;
                    
                    particle.style.animation = `float ${duration}s linear ${delay}s infinite`;
                    
                    matrixBg.appendChild(particle);
                    
                    // Keyframes for floating animation
                    const style = document.createElement('style');
                    style.innerHTML = `
                        @keyframes float {
                            0% {
                                transform: translateY(0) translateX(0);
                                opacity: ${opacity};
                            }
                            50% {
                                transform: translateY(${Math.random() * 100 - 50}px) translateX(${Math.random() * 20 - 10}px);
                                opacity: ${Math.random() * 0.5 + 0.1};
                            }
                            100% {
                                transform: translateY(${Math.random() * 100 - 50}px) translateX(${Math.random() * 20 - 10}px);
                                opacity: 0;
                            }
                        }
                    `;
                    document.head.appendChild(style);
                }
            }
            
            // Scroll reveal animation
            const fadeElements = document.querySelectorAll('.fade-in');
            
            function checkScroll() {
                fadeElements.forEach(element => {
                    const elementTop = element.getBoundingClientRect().top;
                    const windowHeight = window.innerHeight;
                    
                    if (elementTop < windowHeight - 100) {
                        element.classList.add('visible');
                    }
                });
            }
            
            // Initial check
            checkScroll();
            
            // Check on scroll
            window.addEventListener('scroll', checkScroll);
            
            // Terminal cursor effect
            const terminals = document.querySelectorAll('.terminal');
            terminals.forEach(terminal => {
                terminal.addEventListener('mousemove', (e) => {
                    const rect = terminal.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    
                    terminal.style.setProperty('--x', `${x}px`);
                    terminal.style.setProperty('--y', `${y}px`);
                    
                    const glow = document.createElement('div');
                    glow.classList.add('glow-effect');
                    glow.style.left = x + 'px';
                    glow.style.top = y + 'px';
                    
                    terminal.appendChild(glow);
                    
                    setTimeout(() => {
                        glow.remove();
                    }, 500);
                });
            });
        });
    </script>
</body>
</html>
