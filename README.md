<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Portfolio von Matthias Prie - IT-Systemintegration, Hardware Enthusiast & Streamer.">
    <title>Portfolio | Matthias Prie</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');

        :root {
            --matrix-primary: #00ff41; 
            --matrix-dim: #008f11;
            --matrix-bg: #0d0208;
        }

        body {
            background-color: black;
            color: var(--matrix-primary);
            font-family: 'Share Tech Mono', monospace;
            margin: 0;
            overflow-x: hidden;
            user-select: none; 
        }

        /* Matrix Rain Canvas */
        #matrix-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.8; 
        }

        .scanlines {
            position: fixed;
            inset: 0;
            background: linear-gradient(to bottom, transparent 50%, rgba(0,0,0,0.2) 50%);
            background-size: 100% 4px;
            z-index: 50;
            pointer-events: none;
        }

        /* Scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #000; }
        ::-webkit-scrollbar-thumb { background: var(--matrix-dim); border: 1px solid var(--matrix-primary); }

        /* Effekte */
        .glitch-hover:hover {
            text-shadow: 2px 0 #fff, -2px 0 var(--matrix-primary);
            animation: glitch 0.5s infinite;
        }

        @keyframes glitch {
            0% { transform: translate(0) }
            20% { transform: translate(-2px, 2px) }
            40% { transform: translate(-2px, -2px) }
            60% { transform: translate(2px, 2px) }
            80% { transform: translate(2px, -2px) }
            100% { transform: translate(0) }
        }

        .cyber-box {
            background: rgba(0, 0, 0, 0.85);
            border: 1px solid var(--matrix-dim);
            box-shadow: 0 0 10px rgba(0, 255, 65, 0.1);
            transition: all 0.3s ease;
        }

        .cyber-box:hover {
            border-color: var(--matrix-primary);
            box-shadow: 0 0 20px var(--matrix-primary);
        }

        .cyber-box-interactive { cursor: pointer; }
        .cyber-box-interactive:hover { transform: translateY(-2px); }

        .typing-cursor::after {
            content: '█';
            animation: blink 1s step-end infinite;
        }
        @keyframes blink { 50% { opacity: 0; } }

        .nav-btn.active {
            background-color: var(--matrix-primary);
            color: black;
            font-weight: bold;
        }
        
        /* Animation Classes */
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .animate-fade-in { animation: fadeIn 0.5s ease-out forwards; }
        
        /* Skill Bar Animation */
        @keyframes fillBar { from { width: 0; } }
        .skill-fill { animation: fillBar 1.5s ease-out forwards; }

        /* Timeline Styles */
        .timeline-line {
            position: absolute;
            left: 19px;
            top: 10px;
            bottom: 0;
            width: 2px;
            background: var(--matrix-dim);
        }
        .timeline-dot {
            width: 40px;
            height: 40px;
            border: 2px solid var(--matrix-primary);
            background: black;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 10;
            position: relative;
        }

        /* Security Styles */
        .security-blur { filter: blur(15px) grayscale(100%); transition: filter 0.2s; }
        .watermark-overlay {
            position: absolute; inset: 0; pointer-events: none; z-index: 20;
            background-image: url("data:image/svg+xml,%3Csvg width='200' height='200' xmlns='http://www.w3.org/2000/svg'%3E%3Ctext x='30' y='100' font-family='monospace' font-size='20' fill='rgba(128, 128, 128, 0.2)' transform='rotate(-45 30 100)'%3EPROTECTED VIEW%3C/text%3E%3C/svg%3E");
        }
        
        /* Server Blink Animation */
        @keyframes blink-led { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
        .led-blink { animation: blink-led 2s infinite; }
        .led-blink-fast { animation: blink-led 0.5s infinite; }
    </style>
</head>

<body class="antialiased min-h-screen flex flex-col" oncontextmenu="return false;">

    <canvas id="matrix-canvas"></canvas>
    <div class="scanlines"></div>

    <!-- IMPRESSUM MODAL -->
    <div id="impressum-modal" class="fixed inset-0 z-[100] hidden bg-black/95 flex items-center justify-center p-4">
        <div class="w-full max-w-2xl cyber-box p-6 relative overflow-y-auto max-h-[80vh]">
            <button onclick="document.getElementById('impressum-modal').classList.add('hidden')" class="absolute top-4 right-4 text-white hover:text-red-500">[X]</button>
            <h2 class="text-2xl font-bold mb-4 border-b border-gray-700 pb-2">Impressum & Datenschutz</h2>
            
            <div class="space-y-6 text-sm text-gray-300">
                <!-- Impressum -->
                <div>
                    <h3 class="text-lg font-bold text-white mb-2">Impressum</h3>
                    <p><strong>Angaben gemäß § 5 TMG:</strong><br>
                    Matthias Prie<br>
                    Bismarckstr. 10a<br>
                    24837 Schleswig</p>
                    
                    <p class="mt-2"><strong>Kontakt:</strong><br>
                    E-Mail: <a href="mailto:matthiasprie@gmail.com" class="text-green-400 hover:underline">matthiasprie@gmail.com</a><br>
                    Tel: 0152 276 381 05</p>

                    <p class="mt-2"><strong>Inhaltlich Verantwortlicher:</strong><br>
                    Matthias Prie (Adresse wie oben)</p>
                </div>

                <!-- Datenschutz -->
                <div>
                    <h3 class="text-lg font-bold text-white mb-2">Datenschutzerklärung</h3>
                    <p><strong>Allgemeiner Hinweis:</strong><br>
                    Wir nehmen den Schutz Ihrer persönlichen Daten sehr ernst. Diese Webseite dient rein als Portfolio und erhebt keine personenbezogenen Daten (keine Cookies, kein Tracking, keine Analytics).</p>
                    
                    <p class="mt-2"><strong>Hosting:</strong><br>
                    Beim Aufruf dieser Webseite werden durch den Provider automatisch Informationen in sogenannten Server-Log-Dateien erhoben (z.B. Browsertyp, Uhrzeit). Diese Daten sind technisch notwendig und nicht bestimmten Personen zuordenbar.</p>

                    <p class="mt-2"><strong>Externe Links:</strong><br>
                    Diese Seite enthält Links zu externen Webseiten (Twitch, YouTube, TikTok). Beim Klicken auf diese Links verlassen Sie dieses Angebot und es gelten die Datenschutzbestimmungen der jeweiligen Anbieter.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- PDF VIEWER MODAL (Security) -->
    <div id="pdf-modal" class="fixed inset-0 z-[100] hidden bg-black/95 flex items-center justify-center p-4 select-none">
        <div id="security-warning" class="absolute inset-0 z-[120] hidden bg-black flex flex-col items-center justify-center text-red-500 font-bold text-2xl text-center">
            <i data-lucide="shield-alert" class="w-24 h-24 mb-4 animate-pulse"></i>
            <div>SECURITY VIOLATION DETECTED</div>
        </div>

        <div class="w-full h-full max-w-6xl flex flex-col cyber-box bg-black relative">
            <div class="flex justify-between items-center p-2 border-b border-current bg-white/5">
                <div class="flex items-center gap-2">
                    <i id="secure-icon" data-lucide="file-text" class="w-4 h-4"></i>
                    <span id="modal-title" class="text-xs md:text-sm font-bold tracking-widest">> DOCUMENT_VIEWER.EXE</span>
                </div>
                <button onclick="closePDF()" class="hover:bg-red-600 hover:text-white px-3 py-1 transition-colors uppercase text-xs font-bold border border-current">
                    [X] CLOSE
                </button>
            </div>
            <div class="flex-grow relative bg-white">
                 <!-- Watermark Layer (Pointer events durchlässig damit Scrollen geht) -->
                 <div id="watermark" class="watermark-overlay hidden"></div>
                 
                 <!-- HILFE TEXT IM HINTERGRUND -->
                 <div class="absolute inset-0 -z-10 flex flex-col items-center justify-center text-center p-8 bg-gray-900 text-green-400">
                    <i data-lucide="help-circle" class="w-16 h-16 mb-4"></i>
                    <h3 class="text-xl font-bold mb-2">Lade Datei...</h3>
                    <p class="mb-4">Wenn hier nichts erscheint, prüfe bitte den Dateinamen:</p>
                    <div id="filename-debug" class="bg-black border border-green-500 px-4 py-2 font-mono text-lg select-all">
                        DATEINAME_HIER
                    </div>
                    <p class="text-xs text-gray-400 mt-4">Tipp: Die Datei muss im gleichen Ordner liegen.</p>
                 </div>

                 <!-- IFRAME FÜR PDF -->
                 <iframe id="pdf-frame" src="" class="w-full h-full absolute inset-0 border-0"></iframe>
            </div>
        </div>
    </div>

    <!-- MAIN CONTAINER -->
    <div class="relative z-10 flex-grow container mx-auto px-4 py-8 max-w-5xl">
        
        <header class="mb-12 text-center border-b border-green-900 pb-4">
            <h1 class="text-4xl md:text-6xl font-bold mb-2 glitch-hover cursor-default">MATTHIAS_PRIE</h1>
            <p class="text-xl opacity-80 typing-cursor" id="typewriter"></p>
        </header>

        <nav class="flex flex-wrap justify-center gap-4 mb-10">
            <button onclick="showSection('home')" class="nav-btn active cyber-box px-6 py-2 uppercase tracking-wider hover:bg-white/10 transition-colors flex items-center gap-2"><i data-lucide="terminal" class="w-4 h-4"></i> Home</button>
            <button onclick="showSection('about')" class="nav-btn cyber-box px-6 py-2 uppercase tracking-wider hover:bg-white/10 transition-colors flex items-center gap-2"><i data-lucide="history" class="w-4 h-4"></i> Werdegang</button>
            <button onclick="showSection('homelab')" class="nav-btn cyber-box px-6 py-2 uppercase tracking-wider hover:bg-white/10 transition-colors flex items-center gap-2 text-[#00ff41] border border-[#00ff41] shadow-[0_0_5px_#00ff41]"><i data-lucide="server" class="w-4 h-4"></i> Home Lab</button>
            <button onclick="showSection('thesis')" class="nav-btn cyber-box px-6 py-2 uppercase tracking-wider hover:bg-white/10 transition-colors flex items-center gap-2 border-current"><i data-lucide="shield-check" class="w-4 h-4"></i> Projektarbeit</button>
            <button onclick="showSection('projects')" class="nav-btn cyber-box px-6 py-2 uppercase tracking-wider hover:bg-white/10 transition-colors flex items-center gap-2"><i data-lucide="code" class="w-4 h-4"></i> Projekte</button>
            <button onclick="showSection('certificates')" class="nav-btn cyber-box px-6 py-2 uppercase tracking-wider hover:bg-white/10 transition-colors flex items-center gap-2"><i data-lucide="file-check" class="w-4 h-4"></i> Zertifikate</button>
        </nav>

        <main class="relative min-h-[400px]">
            
            <!-- HOME -->
            <section id="home" class="content-section space-y-6 animate-fade-in">
                <div class="cyber-box p-8 flex flex-col md:flex-row items-center gap-8">
                    <!-- BILD CONTAINER -->
                    <div class="w-32 h-32 md:w-48 md:h-48 border-2 border-current rounded-full overflow-hidden shrink-0 shadow-[0_0_15px_currentColor] relative group">
                        <!-- PLATZHALTER BILD -->
                        <img src="https://images.unsplash.com/photo-1526374965328-7f61d4dc18c5?w=500&h=500&fit=crop" 
                             alt="Matthias Prie" 
                             class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110">
                        
                        <!-- Overlay Text (Hover) -->
                        <div class="absolute inset-0 bg-black/50 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity">
                            <span class="text-xs font-bold bg-black px-2 py-1 border border-green-500">ADMIN</span>
                        </div>
                    </div>
                    
                    <div>
                        <h2 class="text-3xl font-bold mb-4">> System Identity: Active</h2>
                        <p class="text-lg leading-relaxed opacity-90">
                            <strong>Base:</strong> Schleswig | <strong>Spawn:</strong> 19.10.1988<br><br>
                            Willkommen im Netzwerk. Vom Schlachter zum Systemintegrator. Ich verbinde Handwerks-Disziplin mit IT-Leidenschaft.
                            Erfahrung seit dem ersten Pentium, geschliffen in World of Warcraft, professionalisiert in der Systemintegration.
                        </p>
                        <div class="mt-6 flex flex-wrap gap-4 justify-center md:justify-start">
                            <a href="https://www.twitch.tv/ultiweapen" target="_blank" class="px-4 py-2 border border-current hover:bg-green-500 hover:text-black transition-colors flex items-center gap-2"><i data-lucide="twitch"></i> Ultiweapen</a>
                            <a href="https://www.youtube.com/@Ultiweapen" target="_blank" class="px-4 py-2 border border-current hover:bg-red-600 hover:text-white transition-colors flex items-center gap-2"><i data-lucide="youtube"></i> YouTube</a>
                            <a href="https://www.tiktok.com/@Ultiweapen" target="_blank" class="px-4 py-2 border border-current hover:bg-pink-600 hover:text-white transition-colors flex items-center gap-2"><i data-lucide="film"></i> TikTok</a>
                        </div>
                    </div>
                </div>
            </section>

            <!-- ABOUT / WERDEGANG / RIG -->
            <section id="about" class="content-section hidden space-y-8 animate-fade-in">
                <!-- Werdegang Timeline -->
                <div class="cyber-box p-8">
                    <h2 class="text-2xl font-bold mb-6 border-b border-gray-700 pb-2 flex items-center gap-2">
                        <i data-lucide="git-branch"></i> Werdegang & Experience Log
                    </h2>
                    <div class="relative pl-2">
                        <div class="timeline-line"></div>

                        <!-- 2025 Start -->
                        <div class="flex gap-6 mb-8 relative">
                            <div class="timeline-dot shrink-0 text-black font-bold bg-[#00ff41] shadow-[0_0_10px_#00ff41]"><i data-lucide="cpu" class="w-5 h-5"></i></div>
                            <div>
                                <span class="text-xs bg-green-900/40 border border-green-800 px-2 py-1 text-green-300">2025 - Heute</span>
                                <h3 class="text-xl font-bold mt-2">IT-Systemintegration (Ausbildung/Umschulung)</h3>
                                <p class="text-sm opacity-80 mt-1">Professioneller Einstieg in die IT bei Tertia. Fokus auf Netzwerktechnik (TQ2 Zertifiziert), Systemadministration und moderne Bürokommunikation.</p>
                            </div>
                        </div>

                        <div class="flex gap-6 mb-8 relative">
                            <div class="timeline-dot shrink-0"><i data-lucide="file-spreadsheet" class="w-5 h-5"></i></div>
                            <div>
                                <span class="text-xs bg-gray-900 border border-gray-800 px-2 py-1 opacity-70">2024</span>
                                <h3 class="text-xl font-bold mt-2">Fachkraft für Bürokommunikation (IT)</h3>
                                <p class="text-sm opacity-80 mt-1">Schwerpunkt MS-Office und digitale Prozesse. Brücke zwischen Verwaltung und IT-Infrastruktur.</p>
                            </div>
                        </div>

                        <div class="flex gap-6 mb-8 relative">
                            <div class="timeline-dot shrink-0"><i data-lucide="swords" class="w-5 h-5"></i></div>
                            <div>
                                <span class="text-xs bg-gray-900 border border-gray-800 px-2 py-1 opacity-70">2000 - Heute</span>
                                <h3 class="text-xl font-bold mt-2">Die "Grind" Ära (Gaming & Streaming)</h3>
                                <p class="text-sm opacity-80 mt-1">Vom Unreal Tournament 99 Reflex-Training bis zum Rang 14 (High Warlord/Grand Marshal) in WoW Classic. Leidenschaft für Competitive Gaming.</p>
                            </div>
                        </div>

                        <div class="flex gap-6 relative">
                            <div class="timeline-dot shrink-0"><i data-lucide="hammer" class="w-5 h-5"></i></div>
                            <div>
                                <span class="text-xs bg-gray-900 border border-gray-800 px-2 py-1 opacity-70">Origin</span>
                                <h3 class="text-xl font-bold mt-2">Handwerk (Gelernter Schlachter)</h3>
                                <p class="text-sm opacity-80 mt-1">Der Start ins Berufsleben. Hier habe ich Disziplin, Ausdauer und präzises Arbeiten gelernt – Skills, die ich heute in die IT übertrage.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Info Grid: Skills & Rig -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="cyber-box p-6">
                        <h3 class="text-lg font-bold mb-4 flex items-center gap-2"><i data-lucide="bar-chart-2"></i> Skill Matrix</h3>
                        <div class="space-y-4">
                            <div><div class="flex justify-between text-xs mb-1"><span>Hardware Assembly & Modding</span><span>95%</span></div><div class="h-2 bg-gray-900 border border-gray-800"><div class="h-full bg-[#00ff41] skill-fill" style="width: 95%"></div></div></div>
                            <div><div class="flex justify-between text-xs mb-1"><span>Windows Administration</span><span>90%</span></div><div class="h-2 bg-gray-900 border border-gray-800"><div class="h-full bg-[#00ff41] skill-fill" style="width: 90%"></div></div></div>
                            <div><div class="flex justify-between text-xs mb-1"><span>Netzwerktechnik (Cisco/Routing)</span><span>75%</span></div><div class="h-2 bg-gray-900 border border-gray-800"><div class="h-full bg-[#00ff41] skill-fill" style="width: 75%"></div></div></div>
                            <div><div class="flex justify-between text-xs mb-1"><span>Web Development</span><span>Loading...</span></div><div class="h-2 bg-gray-900 border border-gray-800"><div class="h-full bg-[#00ff41] skill-fill animate-pulse" style="width: 40%"></div></div></div>
                        </div>
                    </div>
                    <div class="cyber-box p-6 relative overflow-hidden h-full flex flex-col">
                        <div class="absolute -right-4 -top-4 text-green-900 opacity-20"><i data-lucide="monitor" class="w-40 h-40"></i></div>
                        <h3 class="text-lg font-bold mb-4 flex items-center gap-2 relative z-10"><i data-lucide="hard-drive"></i> Hardware Status</h3>
                        <div class="mb-4 border-b border-green-900 pb-4 relative z-10">
                            <h4 class="text-sm font-bold text-[#00ff41] mb-2">> ACTIVE SYSTEM</h4>
                            <div class="flex items-center gap-3 bg-green-900/10 p-2 border border-green-900">
                                <i data-lucide="gamepad-2" class="w-8 h-8 text-white"></i>
                                <div><p class="font-bold">Xbox Series X</p><p class="text-xs text-gray-400">Main Gaming Platform</p></div>
                            </div>
                        </div>
                        <div class="relative z-10 flex-grow">
                            <h4 class="text-sm font-bold text-yellow-500 mb-2 flex justify-between items-center"><span>> PROJECT: HIGH_END_RIG</span><span class="animate-pulse text-xs border border-yellow-600 px-1 text-yellow-500">[SAVING...]</span></h4>
                            <div class="text-xs text-gray-300 space-y-2 font-mono overflow-y-auto max-h-[220px] pr-2 scrollbar-thin scrollbar-thumb-green-900">
                                <div class="flex justify-between border-b border-gray-800 pb-1 hover:bg-gray-900/50"><span class="opacity-60">CPU</span><span class="text-right font-bold">Ryzen 9 9900X</span></div>
                                <div class="flex justify-between border-b border-gray-800 pb-1 hover:bg-gray-900/50"><span class="opacity-60">GPU</span><span class="text-right font-bold text-[#00ff41]">RTX 5080 Gaming OC</span></div>
                                <div class="flex justify-between border-b border-gray-800 pb-1 hover:bg-gray-900/50"><span class="opacity-60">RAM</span><span class="text-right">64GB Corsair 6000MHz</span></div>
                                <div class="flex justify-between border-b border-gray-800 pb-1 hover:bg-gray-900/50"><span class="opacity-60">SSD</span><span class="text-right">2TB 990 EVO+</span></div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- SECTION: HOME LAB -->
            <section id="homelab" class="content-section hidden space-y-6 animate-fade-in">
                <div class="cyber-box p-8 border-t-2 border-[#00ff41]">
                    <div class="flex items-center justify-between mb-6">
                        <h2 class="text-2xl font-bold flex items-center gap-2"><i data-lucide="server"></i> Home Lab & Infrastructure</h2>
                        <span class="text-xs bg-green-900 px-2 py-1 rounded text-white animate-pulse">STATUS: ACTIVE</span>
                    </div>
                    
                    <p class="mb-8 text-gray-300 leading-relaxed">
                        Mein privates Rechenzentrum. Hier teste ich Enterprise-Umgebungen, Sicherheitskonzepte und neue Betriebssysteme unter Realbedingungen.
                    </p>

                    <!-- Server Nodes Grid -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                        
                        <!-- Node 1: Windows Domain -->
                        <div class="cyber-box p-4 bg-black border border-green-800 relative overflow-hidden group hover:bg-green-900/10">
                            <div class="absolute top-2 right-2 w-2 h-2 rounded-full bg-blue-500 led-blink"></div>
                            <i data-lucide="layout-grid" class="w-10 h-10 mb-4 text-blue-500"></i>
                            <h3 class="font-bold text-lg mb-1">Windows Domain</h3>
                            <p class="text-xs text-gray-400 mb-2">AD / DNS / DHCP</p>
                            <ul class="text-xs font-mono text-green-300 space-y-1">
                                <li>> Win Server 2019 - 2025</li>
                                <li>> Active Directory Config</li>
                                <li>> Client Management</li>
                            </ul>
                        </div>

                        <!-- Node 2: Security / OPNsense -->
                        <div class="cyber-box p-4 bg-black border border-green-800 relative overflow-hidden group hover:bg-green-900/10">
                            <div class="absolute top-2 right-2 w-2 h-2 rounded-full bg-red-500 led-blink-fast"></div>
                            <i data-lucide="shield-check" class="w-10 h-10 mb-4 text-red-500"></i>
                            <h3 class="font-bold text-lg mb-1">Network Security</h3>
                            <p class="text-xs text-gray-400 mb-2">VM-Based Firewall</p>
                            <ul class="text-xs font-mono text-green-300 space-y-1">
                                <li>> OPNsense Gateway</li>
                                <li>> WLAN Segregation</li>
                                <li>> Intrusion Detection</li>
                            </ul>
                        </div>

                        <!-- Node 3: Storage / Fileserver -->
                        <div class="cyber-box p-4 bg-black border border-green-800 relative overflow-hidden group hover:bg-green-900/10">
                            <div class="absolute top-2 right-2 w-2 h-2 rounded-full bg-yellow-500 led-blink"></div>
                            <i data-lucide="hard-drive" class="w-10 h-10 mb-4 text-yellow-400"></i>
                            <h3 class="font-bold text-lg mb-1">Data Exchange</h3>
                            <p class="text-xs text-gray-400 mb-2">Custom Fileserver</p>
                            <ul class="text-xs font-mono text-green-300 space-y-1">
                                <li>> 100GB Data Pool</li>
                                <li>> Link: VM <-> Acer 314</li>
                                <li>> Protocol: SMB/NFS</li>
                            </ul>
                        </div>
                    </div>

                    <!-- OS ARSENAL (Terminal View) -->
                    <div class="cyber-box p-0 overflow-hidden">
                        <div class="bg-gray-900 px-4 py-2 border-b border-green-800 flex items-center gap-2">
                            <div class="w-3 h-3 rounded-full bg-red-500"></div>
                            <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                            <div class="w-3 h-3 rounded-full bg-green-500"></div>
                            <span class="text-xs font-mono ml-2 text-gray-400">user@admin-rig:~/installed_systems</span>
                        </div>
                        <div class="p-4 font-mono text-xs md:text-sm h-48 overflow-y-auto scrollbar-thin scrollbar-thumb-green-700">
                            <div class="mb-2 text-green-500">
                                <span class="text-blue-400">➜</span> <span class="text-yellow-400">~</span> cat os_experience_log.txt
                            </div>
                            
                            <!-- Server List -->
                            <div class="mb-4">
                                <h4 class="text-white underline mb-1"># SERVER & INFRASTRUCTURE</h4>
                                <p class="text-gray-400">
                                    [X] Microsoft Windows Server 2019 / 2022 / <span class="text-[#00ff41]">2025 (Preview)</span><br>
                                    [X] Ubuntu Server LTS<br>
                                    [X] Zentyal Server (Small Business)<br>
                                    [X] Fedora Server
                                </p>
                            </div>

                            <!-- Linux Distros -->
                            <div class="mb-4">
                                <h4 class="text-white underline mb-1"># LINUX DISTRIBUTIONS (TESTED/DAILY)</h4>
                                <div class="grid grid-cols-2 md:grid-cols-3 gap-2 text-gray-400">
                                    <span>> Ubuntu Desktop</span>
                                    <span>> Zorin OS</span>
                                    <span>> CachyOS (Arch)</span>
                                    <span>> Garuda Linux</span>
                                    <span>> Nobara (Gaming)</span>
                                    <span>> Fedora (Gnome)</span>
                                    <span>> Elementary OS</span>
                                    <span>> <span class="text-red-400">Kali Linux</span></span>
                                    <span>> <span class="text-yellow-400">Qubes OS</span></span>
                                    <span>> Arch Linux</span>
                                </div>
                            </div>

                            <!-- Clients -->
                            <div>
                                <h4 class="text-white underline mb-1"># CLIENT SYSTEMS</h4>
                                <p class="text-gray-400">
                                    [X] Windows 10 / 11 (All Editions)<br>
                                    [X] ChromeOS (Acer Chromebook 314 Integration)
                                </p>
                            </div>
                            
                            <div class="mt-4 animate-pulse">
                                <span class="text-green-500">➜</span> <span class="text-yellow-400">~</span> <span class="typing-cursor">_</span>
                            </div>
                        </div>
                    </div>

                </div>
            </section>

            <!-- THESIS (SECURE) -->
            <section id="thesis" class="content-section hidden space-y-6 animate-fade-in">
                <div class="cyber-box p-8 border-2 border-red-500/50 bg-red-900/10">
                    <div class="flex items-center gap-4 mb-6 border-b border-red-500/50 pb-4">
                        <i data-lucide="lock" class="w-12 h-12 text-red-500 animate-pulse"></i>
                        <div>
                            <h2 class="text-2xl font-bold text-red-500">SECURE ARCHIVE: PROJEKTARBEITEN</h2>
                            <p class="text-xs text-red-300">View-Only Protocol Active. Copying Disabled.</p>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 gap-6">
                        <div onclick="openPDF('Projektarbeit.pdf', true)" class="cyber-box cyber-box-interactive p-6 flex flex-col md:flex-row items-center gap-6 border border-red-500 hover:bg-red-900/20 group">
                            <i data-lucide="file-lock" class="w-12 h-12 text-red-500"></i>
                            <div class="flex-grow">
                                <h3 class="text-xl font-bold text-red-400">IHK Projektarbeit (2025)</h3>
                                <p class="text-sm text-gray-400">Betriebliche Dokumentation: Systemintegration</p>
                            </div>
                            <button class="px-6 py-2 border border-red-500 text-red-500 font-bold hover:bg-red-500 hover:text-black transition-all">SECURE VIEW</button>
                        </div>
                    </div>
                </div>
            </section>

            <!-- PROJECTS -->
            <section id="projects" class="content-section hidden space-y-6 animate-fade-in">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="cyber-box p-6 flex flex-col">
                        <div class="h-40 bg-white/5 border border-current mb-4 flex items-center justify-center"><i data-lucide="monitor-play" class="w-12 h-12 opacity-50"></i></div>
                        <h3 class="text-xl font-bold mb-2">Streaming Setup 2.0</h3>
                        <p class="text-sm opacity-80 mb-4">Dual-PC Config, Custom Loop Wasserkühlung.</p>
                        <a href="#" class="text-center py-2 border border-dashed border-current hover:bg-white/10 transition-colors">> Details</a>
                    </div>
                    <div class="cyber-box p-6 flex flex-col">
                        <div class="h-40 bg-white/5 border border-current mb-4 flex items-center justify-center"><i data-lucide="gamepad-2" class="w-12 h-12 opacity-50"></i></div>
                        <h3 class="text-xl font-bold mb-2">Xbox Event</h3>
                        <p class="text-sm opacity-80 mb-4">Community Turnier Organisation.</p>
                        <a href="#" class="text-center py-2 border border-dashed border-current hover:bg-white/10 transition-colors">> Details</a>
                    </div>
                </div>
            </section>

            <!-- CERTIFICATES -->
            <section id="certificates" class="content-section hidden space-y-6 animate-fade-in">
                <div class="cyber-box p-4 mb-6 border border-yellow-600/50 bg-yellow-900/10 text-center text-yellow-500 text-sm">
                    <i data-lucide="info" class="inline w-4 h-4 mr-2"></i> Klicke auf ein Zertifikat für die Vorschau.
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <!-- TQ 2 -->
                    <div onclick="openPDF('TQ2 Zertifikat.pdf', false)" class="cyber-box cyber-box-interactive p-4 flex items-center gap-4 border border-current hover:bg-white/5">
                        <i data-lucide="network" class="w-10 h-10"></i>
                        <div><h4 class="font-bold">TQ 2: IT-Netzwerke</h4><p class="text-xs opacity-70">TERTIA (2025)</p></div>
                    </div>
                    
                    <!-- NEU: TQ 3 -->
                    <div onclick="openPDF('TQ3 Zertifikat.pdf', false)" class="cyber-box cyber-box-interactive p-4 flex items-center gap-4 border border-current hover:bg-white/5">
                        <i data-lucide="server" class="w-10 h-10 text-blue-400"></i>
                        <div><h4 class="font-bold">TQ 3: IT-Administration</h4><p class="text-xs opacity-70">IT-Systeme administrieren</p></div>
                    </div>

                    <!-- Bürokomm -->
                    <div onclick="openPDF('Zertifikat Prie-1.pdf', false)" class="cyber-box cyber-box-interactive p-4 flex items-center gap-4 border border-current hover:bg-white/5">
                        <i data-lucide="file-spreadsheet" class="w-10 h-10"></i>
                        <div><h4 class="font-bold">Bürokommunikation IT</h4><p class="text-xs opacity-70">MS-Office (2024)</p></div>
                    </div>
                </div>
            </section>

        </main>

        <footer class="mt-12 text-center text-xs opacity-60 border-t border-gray-800 pt-4 pb-8">
            <p>&copy; 2026 Matthias Prie | <span class="animate-pulse">SYSTEM ONLINE</span></p>
            <div class="mt-2 space-x-4">
                <button onclick="document.getElementById('impressum-modal').classList.remove('hidden')" class="hover:text-white underline">Impressum & Datenschutz</button>
            </div>
        </footer>
    </div>

    <script>
        lucide.createIcons();
        let isSecureMode = false;
        
        // --- MATRIX RAIN ---
        const canvas = document.getElementById('matrix-canvas');
        const ctx = canvas.getContext('2d');
        
        function resizeCanvas() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        const chars = 'アァカサタナハマヤャラワガザダ0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ';
        const fontSize = 16;
        const columns = canvas.width / fontSize;
        const drops = Array(Math.floor(columns)).fill(1);

        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#0F0';
            ctx.font = fontSize + 'px monospace';

            for(let i = 0; i < drops.length; i++) {
                const text = chars.charAt(Math.floor(Math.random() * chars.length));
                ctx.fillText(text, i*fontSize, drops[i]*fontSize);
                if(drops[i]*fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
                drops[i]++;
            }
        }
        setInterval(drawMatrix, 30);

        // --- PDF LOGIC ---
        function openPDF(filename, secure) {
            isSecureMode = secure;
            const modal = document.getElementById('pdf-modal');
            const frame = document.getElementById('pdf-frame');
            const watermark = document.getElementById('watermark');
            const title = document.getElementById('modal-title');
            const icon = document.getElementById('secure-icon');
            const debugText = document.getElementById('filename-debug');

            // Set debug filename
            debugText.innerText = filename;

            // Scroll-Fix: 'scrollbar=0' entfernt, damit scrollen möglich ist
            frame.src = filename + (secure ? "#toolbar=0&navpanes=0&view=FitH" : "");
            
            modal.classList.remove('hidden');
            document.body.style.overflow = 'hidden';

            if (secure) {
                watermark.classList.remove('hidden');
                title.innerText = "> RESTRICTED_VIEWER // EYES_ONLY";
                title.classList.add('text-red-500');
                icon.classList.add('text-red-500');
                window.addEventListener('blur', blurWindow);
                window.addEventListener('focus', unblurWindow);
            } else {
                watermark.classList.add('hidden');
                title.innerText = "> DOCUMENT_VIEWER.EXE";
                title.classList.remove('text-red-500');
                icon.classList.remove('text-red-500');
                window.removeEventListener('blur', blurWindow);
            }
        }

        function closePDF() {
            document.getElementById('pdf-modal').classList.add('hidden');
            setTimeout(() => { document.getElementById('pdf-frame').src = ""; }, 300);
            document.body.style.overflow = 'auto';
            window.removeEventListener('blur', blurWindow);
            unblurWindow();
        }

        function blurWindow() { if(isSecureMode) document.getElementById('security-warning').classList.remove('hidden'); }
        function unblurWindow() { document.getElementById('security-warning').classList.add('hidden'); }

        // --- GENERAL UI ---
        const textToType = "IT-Systemintegration | Hardware Enthusiast | Gamer | Schleswig";
        let typeIdx = 0;
        function typeWriter() {
            if (typeIdx < textToType.length) {
                document.getElementById('typewriter').innerHTML += textToType.charAt(typeIdx);
                typeIdx++;
                setTimeout(typeWriter, 50);
            }
        }
        setTimeout(typeWriter, 800);

        function showSection(id) {
            document.querySelectorAll('.content-section').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById(id).classList.remove('hidden');
            
            // Re-trigger animations
            if(id === 'about') {
                const bars = document.querySelectorAll('.skill-fill');
                bars.forEach(bar => {
                    bar.style.animation = 'none';
                    bar.offsetHeight; /* trigger reflow */
                    bar.style.animation = null; 
                });
            }
            
            // Set active button
            const btns = document.getElementsByTagName('button');
            for (let btn of btns) {
                if(btn.getAttribute('onclick') && btn.getAttribute('onclick').includes(id)) btn.classList.add('active');
            }
        }
    </script>
</body>
</html>
