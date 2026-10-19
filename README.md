
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Caixa Materna - Efeito Boom Tube & Trauma Métrico</title>
    <!-- Tailwind CSS CDN -->
    <script src="[https://cdn.tailwindcss.com](https://cdn.tailwindcss.com)"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        boom: {
                            bg: '#02050a',
                            panel: 'rgba(6, 12, 22, 0.90)',
                            cyan: '#00f3ff',
                            violet: '#b026ff',
                            trauma: '#ff0055',
                            amber: '#ffaa00',
                            border: 'rgba(0, 243, 255, 0.22)'
                        }
                    },
                    fontFamily: {
                        mono: ['Consolas', 'Courier New', 'monospace'],
                        sans: ['Inter', 'Segoe UI', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <style>
        ::-webkit-scrollbar { width: 5px; height: 5px; }
        ::-webkit-scrollbar-track { background: rgba(2, 5, 10, 0.95); }
        ::-webkit-scrollbar-thumb { background: rgba(0, 243, 255, 0.3); border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(0, 243, 255, 0.7); }

        .neon-text-cyan { text-shadow: 0 0 10px rgba(0, 243, 255, 0.7); }
        .neon-text-violet { text-shadow: 0 0 10px rgba(176, 38, 255, 0.7); }
        .neon-text-trauma { text-shadow: 0 0 10px rgba(255, 0, 85, 0.8); }

        .glass-panel {
            background: rgba(6, 12, 22, 0.88);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 1px solid rgba(0, 243, 255, 0.22);
        }
        canvas { touch-action: none; }
    </style>
</head>
<body class="bg-[#02050a] text-gray-200 font-sans h-screen flex flex-col overflow-hidden select-none">

    <!-- Header Bar -->
    <header class="h-14 border-b border-boom-border bg-boom-bg flex items-center justify-between px-4 z-20 shrink-0">
        <div class="flex items-center gap-3">
            <div id="status-beacon" class="w-3.5 h-3.5 rounded-full bg-boom-cyan animate-pulse shadow-[0_0_12px_#00f3ff]"></div>
            <h1 class="font-bold text-base sm:text-lg tracking-wider text-boom-cyan neon-text-cyan uppercase">
                BOOM TUBE <span class="text-xs text-boom-violet font-mono font-normal">| TELETRANSPORTE MÉTRICO & SIMULAÇÃO DE TRAUMA</span>
            </h1>
        </div>
        <div class="flex items-center gap-3 text-xs font-mono">
            <div class="hidden sm:flex items-center gap-2 bg-black/70 px-3 py-1 rounded border border-boom-border">
                <span class="text-gray-400">REATOR HD-MHD:</span>
                <span id="hdr-reactor-status" class="text-boom-cyan font-bold">CARREGANDO</span>
            </div>
            <div class="hidden md:flex items-center gap-2 bg-black/70 px-3 py-1 rounded border border-boom-border">
                <span class="text-gray-400">SINGULARIDADE:</span>
                <span id="hdr-singularity" class="text-boom-violet font-bold">0.00 GPa</span>
            </div>
            <button id="btn-info-modal" class="bg-boom-cyan/20 hover:bg-boom-cyan/40 text-boom-cyan border border-boom-cyan px-3 py-1 rounded transition text-xs font-bold">
                Manual do Boom Tube
            </button>
        </div>
    </header>

    <!-- Main Content Workspace -->
    <div class="flex-1 grid grid-cols-1 lg:grid-cols-12 overflow-hidden relative">

        <!-- Left Controls Sidebar -->
        <aside class="lg:col-span-3 glass-panel p-4 flex flex-col gap-3 overflow-y-auto z-10 max-h-[42vh] lg:max-h-full border-r border-boom-border">
            
            <!-- Stage / Phase Navigation Selector -->
            <div class="space-y-1.5">
                <label class="text-[10px] font-mono uppercase text-gray-400 tracking-wider">Etapas do Colapso Espaço-Temporal</label>
                <div class="grid grid-cols-1 gap-1.5 font-mono text-xs">
                    <button id="btn-phase-1" onclick="setPhase(1)" class="w-full text-left p-2 rounded border border-boom-cyan bg-boom-cyan/20 text-boom-cyan font-bold transition flex items-center justify-between">
                        <span>1. Carga Reator HD-MHD</span>
                        <span class="text-[10px] bg-boom-cyan/30 px-1.5 py-0.5 rounded">0% SHIFT</span>
                    </button>
                    <button id="btn-phase-2" onclick="setPhase(2)" class="w-full text-left p-2 rounded border border-boom-border bg-black/40 text-gray-400 hover:text-boom-cyan transition flex items-center justify-between">
                        <span>2. Compressão Gravitacional</span>
                        <span class="text-[10px] bg-boom-violet/30 px-1.5 py-0.5 rounded">PLANCK</span>
                    </button>
                    <button id="btn-phase-3" onclick="setPhase(3)" class="w-full text-left p-2 rounded border border-boom-border bg-black/40 text-gray-400 hover:text-boom-violet transition flex items-center justify-between">
                        <span>3. Ponto de Canto ER=EPR</span>
                        <span class="text-[10px] bg-purple-900/50 px-1.5 py-0.5 rounded">HYPER</span>
                    </button>
                    <button id="btn-phase-4" onclick="setPhase(4)" class="w-full text-left p-2 rounded border border-boom-border bg-black/40 text-gray-400 hover:text-boom-trauma transition flex items-center justify-between">
                        <span>4. Descompressão & Trauma</span>
                        <span class="text-[10px] bg-boom-trauma/30 px-1.5 py-0.5 rounded text-boom-trauma font-bold">BOOM!</span>
                    </button>
                </div>
            </div>

            <!-- Main Trigger Fire Button -->
            <button id="btn-fire-boom" onclick="triggerBoomTube()" class="w-full bg-gradient-to-r from-boom-cyan via-boom-violet to-boom-trauma hover:from-cyan-400 hover:to-pink-600 text-black font-black text-xs p-3 rounded shadow-lg shadow-boom-cyan/20 transition transform active:scale-95 flex flex-col items-center justify-center gap-0.5 border border-white/50 tracking-wider uppercase">
                <span class="text-sm">💥 DISPARAR BOOM TUBE</span>
                <span class="text-[9.5px] font-mono font-semibold text-black/80">GERAR SINGULARIDADE MÉTRICA COM AUDIO</span>
            </button>

            <!-- Mode Scan Switcher -->
            <div class="space-y-1 bg-black/60 p-2.5 rounded border border-boom-border">
                <label class="text-[10px] font-mono uppercase text-gray-400 tracking-wider block">Modo do Scanner de Diagnóstico</label>
                <div class="grid grid-cols-2 gap-1.5 text-xs font-mono">
                    <button id="btn-view-metric" onclick="setScanView('metric')" class="p-2 rounded border border-boom-cyan bg-boom-cyan/20 text-boom-cyan font-bold transition">
                        🌐 Métrica Espaço-Tempo
                    </button>
                    <button id="btn-view-bio" onclick="setScanView('bio')" class="p-2 rounded border border-boom-border bg-black/40 text-gray-400 hover:text-boom-trauma transition">
                        🫀 Impacto Fisiológico
                    </button>
                </div>
            </div>

            <!-- HD-MHD Reactor Stability Slider -->
            <div class="space-y-2 bg-black/50 p-3 rounded border border-boom-border/80 font-mono text-xs">
                <div class="flex justify-between items-center">
                    <span class="text-gray-300 font-bold">Estabilidade HD-MHD:</span>
                    <span id="val-stability" class="text-boom-cyan font-bold">99.9999%</span>
                </div>
                <input type="range" id="slider-stability" min="999900" max="999999" value="999999" class="w-full accent-boom-cyan bg-gray-800 rounded h-1.5 cursor-pointer">
                <div class="text-[10px] text-gray-400 flex justify-between">
                    <span>99.9900% (Crítico)</span>
                    <span>99.9999% (Perfeito)</span>
                </div>
            </div>

            <!-- Console Log Window -->
            <div class="flex-1 flex flex-col min-h-[110px] bg-black/90 rounded border border-boom-border/70 p-2 font-mono text-[11px] overflow-hidden">
                <div class="text-gray-500 border-b border-gray-800 pb-1 mb-1 flex justify-between">
                    <span>> REGISTRO DO EVENTO DE TRANSPORTE</span>
                    <span id="log-clock" class="text-boom-cyan">00:00:00</span>
                </div>
                <div id="log-console" class="flex-1 overflow-y-auto space-y-1 text-gray-300 pr-1">
                    <p class="text-boom-cyan">[SISTEMA] Reator HD-MHD em espera funcional.</p>
                    <p class="text-boom-violet">[MÉTRICA] Tensor de curvatura pronto para colapso.</p>
                </div>
            </div>

        </aside>

        <!-- Center Interactive 2D Canvas Visualization -->
        <main class="lg:col-span-6 relative flex flex-col items-center justify-center bg-black overflow-hidden">
            
            <canvas id="boomCanvas" class="w-full h-full cursor-crosshair"></canvas>

            <!-- Dynamic Phase HUD Title Banner -->
            <div class="absolute top-4 left-4 pointer-events-none font-mono text-xs space-y-1 bg-black/80 p-3 rounded border border-boom-border/70 backdrop-blur-md z-10">
                <div class="text-boom-cyan font-bold flex items-center gap-2">
                    <span id="hud-status-dot" class="inline-block w-2.5 h-2.5 rounded-full bg-boom-cyan animate-ping"></span>
                    <span id="hud-phase-title">ETAPA 1: CARGA DO REATOR HD-MHD</span>
                </div>
                <div class="text-gray-400 text-[11px]" id="hud-phase-sub">Aguardando gatilho do vetor de singularidade direcionada</div>
                <div class="text-boom-violet text-[11px]">Distorção Espacial: <span id="hud-distortion-val" class="text-white">0.02 λ</span></div>
            </div>

            <!-- Shockwave Acoustic Text Banner -->
            <div id="hud-action-banner" class="hidden absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 pointer-events-none text-center z-20">
                <h2 id="hud-action-text" class="text-4xl sm:text-6xl font-black text-transparent bg-clip-text bg-gradient-to-r from-boom-cyan via-white to-boom-trauma neon-text-trauma tracking-wider uppercase animate-ping">
                    BOOM!
                </h2>
                <div class="text-xs font-mono text-boom-trauma font-bold tracking-widest mt-2 bg-black/80 px-4 py-1 rounded border border-boom-trauma inline-block">
                    DESCOMPRESSÃO MÉTRICA HIPERBÁRICA EXECUTADA
                </div>
            </div>

        </main>

        <!-- Right Scientific Telemetry & Trauma Overview -->
        <aside class="lg:col-span-3 glass-panel p-4 flex flex-col gap-3.5 overflow-y-auto z-10 max-h-[42vh] lg:max-h-full border-l border-boom-border">
            
            <h2 class="text-xs font-mono uppercase text-boom-cyan tracking-wider flex items-center gap-1 border-b border-boom-border/40 pb-2 font-bold">
                <span>📊</span> Telemetria Gravitacional & Biológica
            </h2>

            <!-- Metric Cards -->
            <div class="grid grid-cols-2 gap-2 text-xs font-mono">
                <div class="bg-black/70 p-2 rounded border border-boom-cyan/40">
                    <span class="text-gray-400 block text-[10px]">PRESSÃO COLAPSO</span>
                    <span id="tele-collapse-press" class="text-boom-cyan text-sm font-bold">0.00 GPa</span>
                </div>
                <div class="bg-black/70 p-2 rounded border border-boom-violet/40">
                    <span class="text-gray-400 block text-[10px]">TENSOR R_μν</span>
                    <span id="tele-tensor-rmu" class="text-boom-violet text-sm font-bold">0.0001 / m²</span>
                </div>
                <div class="bg-black/70 p-2 rounded border border-boom-trauma/40">
                    <span class="text-gray-400 block text-[10px]">DESCOMPENSAÇÃO</span>
                    <span id="tele-decompensation" class="text-boom-trauma text-sm font-bold">0.0%</span>
                </div>
                <div class="bg-black/70 p-2 rounded border border-boom-amber/40">
                    <span class="text-gray-400 block text-[10px]">FORÇA LABIRÍNTICA</span>
                    <span id="tele-vestibular-g" class="text-boom-amber text-sm font-bold">1.00 G</span>
                </div>
            </div>

            <!-- Trauma Progress / Stress Bars -->
            <div class="bg-black/70 p-3 rounded border border-boom-border space-y-2.5 font-mono text-xs">
                <div>
                    <div class="flex justify-between text-[11px] mb-1">
                        <span class="text-boom-trauma font-bold">STRESS CAPILAR (HEMORRAGIA)</span>
                        <span id="tele-capillary-val" class="text-boom-trauma">0.0%</span>
                    </div>
                    <div class="w-full bg-gray-900 h-2 rounded overflow-hidden p-0.5 border border-gray-800">
                        <div id="bar-capillary" class="bg-gradient-to-r from-yellow-500 to-boom-trauma h-full w-[0%] transition-all duration-300"></div>
                    </div>
                </div>

                <div>
                    <div class="flex justify-between text-[11px] mb-1">
                        <span class="text-boom-amber font-bold">DESORIENTAÇÃO TEMPORAL</span>
                        <span id="tele-temporal-val" class="text-boom-amber">0.00 ms</span>
                    </div>
                    <div class="w-full bg-gray-900 h-2 rounded overflow-hidden p-0.5 border border-gray-800">
                        <div id="bar-temporal" class="bg-gradient-to-r from-blue-500 to-boom-amber h-full w-[0%] transition-all duration-300"></div>
                    </div>
                </div>

                <div>
                    <div class="flex justify-between text-[11px] mb-1">
                        <span class="text-boom-violet font-bold">ESTABILIDADE VESTIBULAR (3 GRAVIDADES)</span>
                        <span id="tele-vestibular-val" class="text-boom-violet">100.0%</span>
                    </div>
                    <div class="w-full bg-gray-900 h-2 rounded overflow-hidden p-0.5 border border-gray-800">
                        <div id="bar-vestibular" class="bg-gradient-to-r from-boom-violet to-emerald-400 h-full w-[100%] transition-all duration-300"></div>
                    </div>
                </div>
            </div>

            <!-- Technical Narrative Description -->
            <div class="space-y-2 font-mono text-xs">
                <h3 class="text-boom-cyan font-bold text-[11px] uppercase border-b border-boom-cyan/20 pb-1">
                    🔬 Diagnóstico do Preço do Boom
                </h3>
                <div id="trauma-description-text" class="bg-black/50 p-2.5 rounded border border-gray-800 text-gray-300 text-[11px] leading-relaxed space-y-1.5">
                    <p>
                        <strong class="text-boom-cyan">Estado Normal:</strong> Reator HD-MHD em fase de indução magnética sem colapso espaço-temporal. Estabilidade do sujeito em níveis normais.
                    </p>
                </div>
            </div>

            <!-- Canvas Visual Legend -->
            <div class="bg-black/60 p-2.5 rounded border border-boom-border/40 space-y-1 text-[11px] font-mono">
                <div class="text-gray-400 mb-0.5 font-bold">Legenda de Componentes Visuais:</div>
                <div class="flex items-center gap-2">
                    <span class="w-2.5 h-2.5 rounded-full bg-boom-cyan inline-block"></span>
                    <span class="text-gray-300">Linhas Métrica Espaço-Tempo / Planck</span>
                </div>
                <div class="flex items-center gap-2">
                    <span class="w-2.5 h-2.5 rounded-full bg-boom-violet inline-block"></span>
                    <span class="text-gray-300">Fios Hiperdimensionais ER=EPR</span>
                </div>
                <div class="flex items-center gap-2">
                    <span class="w-2.5 h-2.5 rounded-full bg-boom-trauma inline-block"></span>
                    <span class="text-gray-300">Rutilação Capilar / Onda de Choque</span>
                </div>
            </div>

        </aside>

    </div>

    <!-- Tech Overview Modal -->
    <div id="info-modal" class="hidden fixed inset-0 bg-black/85 backdrop-blur-md z-50 flex items-center justify-center p-4">
        <div class="glass-panel max-w-2xl w-full p-6 rounded-lg border border-boom-cyan space-y-4 max-h-[85vh] overflow-y-auto font-mono">
            <div class="flex justify-between items-center border-b border-boom-cyan/30 pb-3">
                <h2 class="text-base sm:text-lg text-boom-cyan font-bold uppercase">Manual do Boom Tube: Física e Trauma Métrico</h2>
                <button id="close-modal-x" class="text-gray-400 hover:text-boom-trauma text-xl font-bold">&times;</button>
            </div>
            
            <div class="space-y-3 text-xs text-gray-300 leading-relaxed">
                <p>
                    No universo Hard Sci-Fi da DC Comics, o **Boom Tube** gerado pela Caixa Materna não é uma porta convencional, mas sim um rasgo métrico de alta energia no espaço-tempo.
                </p>

                <div class="bg-black/60 p-3 rounded border border-boom-border space-y-1">
                    <h4 class="text-boom-cyan font-bold">1. Compressão Gravitacional Subatômica</h4>
                    <p>O Reator HD-MHD induz uma singularidade direcionada que colapsa os átomos do indivíduo até uma escala Planckiana, permitindo a transição em dimensões superiores.</p>
                </div>

                <div class="bg-black/60 p-3 rounded border border-boom-border space-y-1">
                    <h4 class="text-boom-violet font-bold">2. Ponte ER=EPR (Einstein-Rosen / Podolsky-Rosen)</h4>
                    <p>A matéria focalizada viaja através do manifold hiperdimensional sem passar pelo espaço normal, sofrendo estabilização quântica pela Caixa Materna.</p>
                </div>

                <div class="bg-black/60 p-3 rounded border border-boom-border space-y-1">
                    <h4 class="text-boom-trauma font-bold">3. O Preço do Boom (Descompensação Métrico-Biológica)</h4>
                    <p>Pequenas flutuações de 0.00001% no reator HD-MHD geram descompressão violenta na saída. Os tecidos capilares sofrem micro-rupturas, o labirinto do ouvido interno tenta processar três vetores de gravidade simultâneos, e a mente percebe horas em apenas um nanossegundo real.</p>
                </div>
            </div>

            <div class="text-right pt-2 border-t border-boom-cyan/30">
                <button id="close-modal-btn" class="bg-boom-cyan/20 hover:bg-boom-cyan/40 text-boom-cyan border border-boom-cyan px-4 py-2 rounded text-xs font-bold transition">
                    ENTENDIDO - RETORNAR AO REATOR
                </button>
            </div>
        </div>
    </div>

    <!-- JavaScript Logic & Simulation Engine -->
    <script>
        // --- State Management ---
        const state = {
            phase: 1,                  // 1: Charge, 2: Compression, 3: ER=EPR, 4: Decompression
            scanView: 'metric',        // 'metric' or 'bio'
            stabilityRaw: 999999,      // Slider range 999900 - 999999
            stabilityPercent: 99.9999, // Calculated
            
            // Physics / Trauma Parameters
            collapsePressure: 0.0,     // GPa
            tensorRmu: 0.0001,
            decompensatePct: 0.0,      // % Trauma
            vestibularG: 1.0,          // G Force
            capillaryStress: 0.0,      // %
            temporalDesyncMs: 0.0,     // ms
            vestibularStability: 100,  // %
            
            // Canvas Animation Params
            time: 0,
            boomTriggered: false,
            shockwaveRadius: 0
        };

        // UI Text Maps
        const phaseTexts = {
            1: {
                title: "ETAPA 1: CARGA DO REATOR HD-MHD",
                sub: "Indução de fluxo magnético e preenchimento de energia do tecido local",
                doc: `<p><strong class="text-boom-cyan">Carga do Reator:</strong> O Reator Magneto-Hidrodinâmico de Alta Densidade (HD-MHD) energiza a grade de vácuo quântico, preparando o tecido espacial para a singularidade.</p>`
            },
            2: {
                title: "ETAPA 2: COMPRESSÃO MÉTRICO-GRAVITACIONAL",
                sub: "Colapso direcionado da matéria do sujeito em escala Planckiana",
                doc: `<p><strong class="text-boom-violet">Compressão Planckiana:</strong> Os átomos da massa do usuário são comprimidos por curvatura $R_{\\mu\\nu}$ extrema, mantendo a coerência da informação quântica sob alta pressão gravitacional.</p>`
            },
            3: {
                title: "ETAPA 3: PONTO DE CANTO ER=EPR",
                sub: "Trânsito hiperdimensional e estabilização de wormhole",
                doc: `<p><strong class="text-purple-400">Ponte ER=EPR:</strong> A matéria desloca-se fora do espaço tridimensional convencional, atravessando fios de emaranhamento quântico sob estabilização de campo da Caixa Materna.</p>`
            },
            4: {
                title: "ETAPA 4: DESCOMPRESSÃO & TRAUMA MÉTRICO",
                sub: "Explosão sônica hiperbárica e descompensação Fisiológica do sujeito",
                doc: `<p><strong class="text-boom-trauma">O Preço do Boom:</strong> O re-expansão súbita da matéria causa uma frente de onda de repulsão sônica ("BOOM!"). Flutuações mínimas no reator provocam descompensação vestibular e hemorragia capilar.</p>`
            }
        };

        // Canvas Setup
        const canvas = document.getElementById('boomCanvas');
        const ctx = canvas.getContext('2d');
        let width = 0;
        let height = 0;

        // Visual Particles & Subject Grid
        let gridPoints = [];
        let hyperStrings = [];
        let capillarPoints = [];

        // Web Audio Synthesizer
        let audioCtx = null;

        function initAudio() {
            if (!audioCtx) {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                audioCtx = new AudioContext();
            }
        }

        function playBoomSound() {
            try {
                initAudio();
                if (!audioCtx) return;
                const now = audioCtx.currentTime;

                // 1. High Energy Charge Sweep
                const oscCharge = audioCtx.createOscillator();
                const gainCharge = audioCtx.createGain();
                oscCharge.type = 'sawtooth';
                oscCharge.frequency.setValueAtTime(120, now);
                oscCharge.frequency.exponentialRampToValueAtTime(1400, now + 0.35);
                gainCharge.gain.setValueAtTime(0.3, now);
                gainCharge.gain.exponentialRampToValueAtTime(0.01, now + 0.35);

                oscCharge.connect(gainCharge);
                gainCharge.connect(audioCtx.destination);
                oscCharge.start(now);
                oscCharge.stop(now + 0.35);

                // 2. Heavy Sub-Bass BOOM Shockwave
                const oscBoom = audioCtx.createOscillator();
                const gainBoom = audioCtx.createGain();
                oscBoom.type = 'sine';
                oscBoom.frequency.setValueAtTime(180, now + 0.35);
                oscBoom.frequency.exponentialRampToValueAtTime(30, now + 1.2);
                
                // Volume dynamic based on trauma instability
                const boomVol = 0.5 + (100 - state.stabilityPercent) * 20;
                gainBoom.gain.setValueAtTime(Math.min(1.0, boomVol), now + 0.35);
                gainBoom.gain.exponentialRampToValueAtTime(0.001, now + 1.2);

                oscBoom.connect(gainBoom);
                gainBoom.connect(audioCtx.destination);
                oscBoom.start(now + 0.35);
                oscBoom.stop(now + 1.2);

            } catch(e) {
                console.log("Audio syntax ready.");
            }
        }

        function initEntities() {
            // Spacetime Grid
            gridPoints = [];
            const cols = 22;
            const rows = 16;
            for (let i = 0; i <= cols; i++) {
                for (let j = 0; j <= rows; j++) {
                    gridPoints.push({
                        baseX: (i / cols) * (width || 600),
                        baseY: (j / rows) * (height || 500),
                        x: (i / cols) * (width || 600),
                        y: (j / rows) * (height || 500)
                    });
                }
            }

            // Hyperdimensional Strings for ER=EPR
            hyperStrings = [];
            for (let i = 0; i < 40; i++) {
                hyperStrings.push({
                    x: Math.random() * (width || 600),
                    y: Math.random() * (height || 500),
                    length: Math.random() * 120 + 80,
                    speed: Math.random() * 8 + 4,
                    angle: (Math.random() - 0.5) * 0.2
                });
            }

            // Subject Capillars for Biological View
            capillarPoints = [];
            for (let i = 0; i < 60; i++) {
                capillarPoints.push({
                    x: (Math.random() - 0.5) * 140,
                    y: (Math.random() - 0.5) * 260,
                    stress: Math.random()
                });
            }
        }

        function handleResize() {
            const container = canvas.parentElement;
            width = container.clientWidth;
            height = container.clientHeight;
            canvas.width = width;
            canvas.height = height;

            initEntities();
        }

        window.addEventListener('resize', handleResize);

        // --- Main Render Loop ---
        function draw() {
            state.time += 0.03;

            // Clear Background
            ctx.fillStyle = '#02050a';
            ctx.fillRect(0, 0, width, height);

            // Render Scan Views
            if (state.scanView === 'metric') {
                renderSpacetimeMetricView();
            } else {
                renderBiologicalTraumaView();
            }

            // Render Shockwave Pulse if Triggered
            if (state.shockwaveRadius > 0) {
                renderBoomShockwave();
            }

            // Update Telemetry States & Progress Bars
            updateCalculationsAndTelemetry();

            requestAnimationFrame(draw);
        }

        // ==========================================
        // SCAN VIEW 1: Métrica de Espaço-Tempo
        // ==========================================
        function renderSpacetimeMetricView() {
            const centerX = width / 2;
            const centerY = height / 2;

            // Render Deformed Spacetime Grid
            ctx.strokeStyle = state.phase === 4 ? 'rgba(255, 0, 85, 0.25)' : 'rgba(0, 243, 255, 0.2)';
            ctx.lineWidth = 1;

            gridPoints.forEach(pt => {
                const dist = Math.hypot(pt.baseX - centerX, pt.baseY - centerY);
                let pullFactor = 0;

                if (state.phase === 2) {
                    pullFactor = Math.max(0, (220 - dist) / 220) * 0.7; // Gravitational compression
                } else if (state.phase === 3) {
                    pullFactor = Math.max(0, (300 - dist) / 300) * 0.9;
                } else if (state.phase === 4) {
                    pullFactor = -Math.max(0, (250 - dist) / 250) * 0.4; // Repulsive expansion
                }

                pt.x = pt.baseX + (centerX - pt.baseX) * pullFactor + Math.sin(state.time * 2 + dist * 0.02) * 2;
                pt.y = pt.baseY + (centerY - pt.baseY) * pullFactor + Math.cos(state.time * 2 + dist * 0.02) * 2;
            });

            // Draw Grid Lines
            const cols = 22;
            const rows = 16;
            for (let i = 0; i <= cols; i++) {
                ctx.beginPath();
                for (let j = 0; j <= rows; j++) {
                    const idx = i * (rows + 1) + j;
                    if (j === 0) ctx.moveTo(gridPoints[idx].x, gridPoints[idx].y);
                    else ctx.lineTo(gridPoints[idx].x, gridPoints[idx].y);
                }
                ctx.stroke();
            }

            // Render Subject Mass Centroid
            ctx.save();
            ctx.translate(centerX, centerY);

            if (state.phase === 1) {
                // HD-MHD Reactor Inductions Ring
                ctx.strokeStyle = '#00f3ff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(0, 0, 70 + Math.sin(state.time * 5) * 5, 0, Math.PI * 2);
                ctx.stroke();

                // Human Mass Outline
                drawHumanSilhouette(1.0, '#00f3ff');

            } else if (state.phase === 2) {
                // Compression to Planckian density
                const scale = Math.max(0.08, 1.0 - (state.time % 2) * 0.45);
                drawHumanSilhouette(scale, '#b026ff');

                // Singularity Event Horizon Ring
                ctx.strokeStyle = 'rgba(176, 38, 255, 0.8)';
                ctx.shadowBlur = 15;
                ctx.shadowColor = '#b026ff';
                ctx.beginPath();
                ctx.arc(0, 0, 25 * scale, 0, Math.PI * 2);
                ctx.stroke();
                ctx.shadowBlur = 0;

            } else if (state.phase === 3) {
                // ER=EPR Wormhole Hyperdimensional Strings
                hyperStrings.forEach(s => {
                    ctx.strokeStyle = 'rgba(176, 38, 255, 0.6)';
                    ctx.lineWidth = 1.5;
                    ctx.beginPath();
                    ctx.moveTo(s.x - centerX, s.y - centerY);
                    ctx.lineTo(s.x - centerX + Math.cos(s.angle) * s.length, s.y - centerY + Math.sin(s.angle) * s.length);
                    ctx.stroke();

                    s.y += s.speed;
                    if (s.y > height) s.y = 0;
                });

                drawHumanSilhouette(0.3, '#ffffff');

            } else if (state.phase === 4) {
                // Decompression Blast Out
                const decompScale = 1.0 + Math.sin(state.time * 10) * 0.15;
                drawHumanSilhouette(decompScale, '#ff0055');
            }

            ctx.restore();
        }

        // ==========================================
        // SCAN VIEW 2: Impacto Fisiológico / Biológico
        // ==========================================
        function renderBiologicalTraumaView() {
            const centerX = width / 2;
            const centerY = height / 2;

            ctx.save();
            ctx.translate(centerX, centerY);

            // Biological Human Subject Anatomical Map
            drawHumanSilhouette(1.1, 'rgba(255, 255, 255, 0.2)');

            // Capillar Stress / Hemorrhage Network
            capillarPoints.forEach(pt => {
                const isHemorrhaging = state.phase === 4 && state.stabilityPercent < 99.9995;
                
                ctx.fillStyle = isHemorrhaging ? '#ff0055' : '#00ff88';
                ctx.beginPath();
                ctx.arc(pt.x, pt.y, isHemorrhaging ? 3.5 : 1.8, 0, Math.PI * 2);
                ctx.fill();

                if (isHemorrhaging) {
                    // Vascular Micro-rupture streaks
                    ctx.strokeStyle = 'rgba(255, 0, 85, 0.6)';
                    ctx.lineWidth = 1;
                    ctx.beginPath();
                    ctx.moveTo(pt.x, pt.y);
                    ctx.lineTo(pt.x + (Math.random() - 0.5) * 12, pt.y + (Math.random() - 0.5) * 12);
                    ctx.stroke();
                }
            });

            // Vestibular Labyrinth Inner Ear Gravity Vectors (3 Overlapping Gravities)
            const earX = 0;
            const earY = -95; // Head area
            
            ctx.strokeStyle = '#ffaa00';
            ctx.lineWidth = 2;

            if (state.phase === 4) {
                // 3 Overlapping Gravity Force Arrows (Nausea & Disorientation)
                for (let g = 0; g < 3; g++) {
                    const angle = state.time * 3 + (g * Math.PI * 2 / 3);
                    const len = 35 * (state.vestibularG / 3.0);

                    ctx.beginPath();
                    ctx.moveTo(earX, earY);
                    ctx.lineTo(earX + Math.cos(angle) * len, earY + Math.sin(angle) * len);
                    ctx.stroke();

                    // Arrowhead
                    ctx.fillStyle = '#ffaa00';
                    ctx.beginPath();
                    ctx.arc(earX + Math.cos(angle) * len, earY + Math.sin(angle) * len, 3, 0, Math.PI * 2);
                    ctx.fill();
                }
            } else {
                // Standard 1G vector down
                ctx.beginPath();
                ctx.moveTo(earX, earY);
                ctx.lineTo(earX, earY + 25);
                ctx.stroke();
            }

            ctx.restore();
        }

        // Helper: Human Silhouette Generator
        function drawHumanSilhouette(scale, color) {
            ctx.save();
            ctx.scale(scale, scale);
            ctx.strokeStyle = color;
            ctx.lineWidth = 2;

            // Head
            ctx.beginPath();
            ctx.arc(0, -90, 16, 0, Math.PI * 2);
            ctx.stroke();

            // Torso & Limbs
            ctx.beginPath();
            ctx.moveTo(0, -74);
            ctx.lineTo(0, -10); // Spine

            // Arms
            ctx.moveTo(-40, -45);
            ctx.lineTo(0, -60);
            ctx.lineTo(40, -45);

            // Legs
            ctx.moveTo(0, -10);
            ctx.lineTo(-22, 65);
            ctx.moveTo(0, -10);
            ctx.lineTo(22, 65);

            ctx.stroke();
            ctx.restore();
        }

        // Shockwave Expansion Render
        function renderBoomShockwave() {
            state.shockwaveRadius += 16;
            const centerX = width / 2;
            const centerY = height / 2;

            ctx.strokeStyle = `rgba(255, 0, 85, ${Math.max(0, 1 - state.shockwaveRadius / (width * 0.6))})`;
            ctx.lineWidth = 8;
            ctx.beginPath();
            ctx.arc(centerX, centerY, state.shockwaveRadius, 0, Math.PI * 2);
            ctx.stroke();

            if (state.shockwaveRadius > width * 0.6) {
                state.shockwaveRadius = 0;
            }
        }

        // --- Phase Controls & Actions ---
        function setPhase(phaseNum) {
            state.phase = phaseNum;

            // Update Phase Buttons
            for (let i = 1; i <= 4; i++) {
                const btn = document.getElementById(`btn-phase-${i}`);
                if (i === phaseNum) {
                    const colorClass = i === 4 ? 'border-boom-trauma bg-boom-trauma/20 text-boom-trauma' : 'border-boom-cyan bg-boom-cyan/20 text-boom-cyan';
                    btn.className = `w-full text-left p-2 rounded border font-bold transition flex items-center justify-between ${colorClass}`;
                } else {
                    btn.className = 'w-full text-left p-2 rounded border border-boom-border bg-black/40 text-gray-400 hover:text-white transition flex items-center justify-between';
                }
            }

            // HUD and Text updates
            const pInfo = phaseTexts[phaseNum];
            document.getElementById('hud-phase-title').innerText = pInfo.title;
            document.getElementById('hud-phase-sub').innerText = pInfo.sub;
            document.getElementById('trauma-description-text').innerHTML = pInfo.doc;

            addLog(`[ETAPA] Fase alterada para: ${pInfo.title}`);
        }

        function triggerBoomTube() {
            setPhase(4);
            state.shockwaveRadius = 1;
            playBoomSound();

            const banner = document.getElementById('hud-action-banner');
            banner.classList.remove('hidden');
            setTimeout(() => { banner.classList.add('hidden'); }, 1800);

            addLog('💥 [BOOM TUBE] Teletransporte Métrico Disparado! Frente de choque gerada.', 'trauma');
        }

        function setScanView(viewType) {
            state.scanView = viewType;
            const btnMetric = document.getElementById('btn-view-metric');
            const btnBio = document.getElementById('btn-view-bio');

            if (viewType === 'metric') {
                btnMetric.className = 'p-2 rounded border border-boom-cyan bg-boom-cyan/20 text-boom-cyan font-bold transition';
                btnBio.className = 'p-2 rounded border border-boom-border bg-black/40 text-gray-400 hover:text-boom-trauma transition';
            } else {
                btnBio.className = 'p-2 rounded border border-boom-trauma bg-boom-trauma/20 text-boom-trauma font-bold transition';
                btnMetric.className = 'p-2 rounded border border-boom-border bg-black/40 text-gray-400 hover:text-boom-cyan transition';
            }

            addLog(`[DIAGNÓSTICO] Scanner alterado para: ${viewType === 'metric' ? 'Métrica Espaço-Tempo' : 'Impacto Fisiológico'}`);
        }

        // Telemetry Data Calculations Loop
        function updateCalculationsAndTelemetry() {
            // Stability Slider Parsing
            state.stabilityRaw = parseInt(document.getElementById('slider-stability').value);
            state.stabilityPercent = (state.stabilityRaw / 10000).toFixed(4);
            document.getElementById('val-stability').innerText = `${state.stabilityPercent}%`;

            // Instability Factor (0.0 at 99.9999%, 1.0 at 99.9900%)
            const instabilityFactor = (999999 - state.stabilityRaw) / 99;

            if (state.phase === 1) {
                state.collapsePressure = 0.05;
                state.tensorRmu = 0.0001;
                state.decompensatePct = 0.0;
                state.vestibularG = 1.0;
                state.capillaryStress = 0.0;
                state.temporalDesyncMs = 0.0;
                state.vestibularStability = 100.0;
            } else if (state.phase === 2) {
                state.collapsePressure = 845.2; // GPa Planck compression
                state.tensorRmu = 14.82;
                state.decompensatePct = (1.5 + instabilityFactor * 10).toFixed(1);
                state.vestibularG = 1.4;
                state.capillaryStress = (5.0 + instabilityFactor * 15).toFixed(1);
                state.temporalDesyncMs = (0.2 + instabilityFactor * 2).toFixed(2);
                state.vestibularStability = 95.0;
            } else if (state.phase === 3) {
                state.collapsePressure = 1290.0;
                state.tensorRmu = 98.40;
                state.decompensatePct = (4.0 + instabilityFactor * 25).toFixed(1);
                state.vestibularG = 2.1;
                state.capillaryStress = (12.0 + instabilityFactor * 30).toFixed(1);
                state.temporalDesyncMs = (1.5 + instabilityFactor * 12).toFixed(2);
                state.vestibularStability = 82.0;
            } else if (state.phase === 4) {
                // Decompression Trauma Phase
                state.collapsePressure = 12.4;
                state.tensorRmu = 0.05;
                state.decompensatePct = (15.0 + instabilityFactor * 84.0).toFixed(1);
                state.vestibularG = (2.8 + instabilityFactor * 1.2).toFixed(2); // Overlapping 3 gravities
                state.capillaryStress = (20.0 + instabilityFactor * 78.0).toFixed(1);
                state.temporalDesyncMs = (8.5 + instabilityFactor * 140.0).toFixed(1);
                state.vestibularStability = Math.max(0, 100 - (state.vestibularG * 25)).toFixed(1);
            }

            // Update UI Cards
            document.getElementById('hdr-reactor-status').innerText = state.phase === 4 ? 'DESCOMPRESSÃO' : 'OPERACIONAL';
            document.getElementById('hdr-singularity').innerText = `${state.collapsePressure} GPa`;

            document.getElementById('tele-collapse-press').innerText = `${state.collapsePressure} GPa`;
            document.getElementById('tele-tensor-rmu').innerText = `${state.tensorRmu} / m²`;
            document.getElementById('tele-decompensation').innerText = `${state.decompensatePct}%`;
            document.getElementById('tele-vestibular-g').innerText = `${state.vestibularG} G`;

            document.getElementById('tele-capillary-val').innerText = `${state.capillaryStress}%`;
            document.getElementById('bar-capillary').style.width = `${Math.min(100, state.capillaryStress)}%`;

            document.getElementById('tele-temporal-val').innerText = `${state.temporalDesyncMs} ms`;
            document.getElementById('bar-temporal').style.width = `${Math.min(100, state.temporalDesyncMs / 1.5)}%`;

            document.getElementById('tele-vestibular-val').innerText = `${state.vestibularStability}%`;
            document.getElementById('bar-vestibular').style.width = `${state.vestibularStability}%`;

            document.getElementById('hud-distortion-val').innerText = `${(state.tensorRmu * 0.1).toFixed(2)} λ`;

            // Clock update
            document.getElementById('log-clock').innerText = new Date().toTimeString().split(' ')[0];
        }

        function addLog(msg, type = 'cyan') {
            const consoleBox = document.getElementById('log-console');
            const p = document.createElement('p');

            if (type === 'trauma') p.className = 'text-boom-trauma font-bold';
            else if (type === 'violet') p.className = 'text-boom-violet font-bold';
            else p.className = 'text-boom-cyan';

            p.innerText = `${msg}`;
            consoleBox.appendChild(p);
            consoleBox.scrollTop = consoleBox.scrollHeight;
        }

        // --- Window Initialization ---
        window.onload = () => {
            handleResize();
            
            // Modal controls
            document.getElementById('btn-info-modal').addEventListener('click', () => {
                document.getElementById('info-modal').classList.remove('hidden');
            });
            const closeModal = () => document.getElementById('info-modal').classList.add('hidden');
            document.getElementById('close-modal-x').addEventListener('click', closeModal);
            document.getElementById('close-modal-btn').addEventListener('click', closeModal);

            setPhase(1);
            draw();
            addLog('[BOOM TUBE] Simulação de Teletransporte Métrico Inicializada.');
        };
    </script>
</body>
</html>
