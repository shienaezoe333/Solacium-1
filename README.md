<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Solacium - Relaxing Bubble Pop</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@300;400;500;600;700&family=Nunito:wght@400;600;700;800&display=swap');

        :root {
            /* Palette Swatches from Design Chart */
            --color-zircon: #F4F8FB;
            --color-fungreen: #007A33;
            --color-conifer: #99E344;
            --color-pictonblue: #45B2E8;
            --color-mariner: #1E66C4;
            
            /* Dynamic Theme Variables */
            --theme-primary: #1E66C4;
            --theme-secondary: #45B2E8;
            --theme-accent: #99E344;
            --theme-header-1: #3A90E8;
            --theme-header-2: #1562C1;
            --theme-header-3: #0D47A1;
            --theme-tint: rgba(69, 178, 232, 0.15);
            --theme-glow: rgba(69, 178, 232, 0.35);
        }

        body {
            font-family: 'Nunito', sans-serif;
            user-select: none;
            overflow: hidden;
            touch-action: manipulation;
        }

        .font-brand {
            font-family: 'Fredoka', cursive;
        }

        /* Aero Glass UI styling with dynamic theme variables */
        .aero-window {
            background: rgba(255, 255, 255, 0.92);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 2px solid rgba(255, 255, 255, 0.9);
            box-shadow: 0 15px 35px rgba(0, 30, 80, 0.25), inset 0 1px 0 rgba(255, 255, 255, 0.9);
            border-radius: 12px;
        }

        .aero-header {
            background: linear-gradient(180deg, var(--theme-header-1) 0%, var(--theme-header-2) 50%, var(--theme-header-3) 100%);
            border-top-left-radius: 9px;
            border-top-right-radius: 9px;
            color: white;
            text-shadow: 0 1px 2px rgba(0,0,0,0.5);
            box-shadow: inset 0 1px 1px rgba(255,255,255,0.6);
            transition: background 0.4s ease;
        }

        /* Glossy Bubble Button Styling */
        .bubble-btn {
            background: radial-gradient(circle at 30% 30%, rgba(255,255,255,0.98) 0%, rgba(255,255,255,0.45) 30%, var(--theme-secondary) 70%, var(--theme-primary) 100%);
            box-shadow: inset -5px -5px 12px rgba(0, 0, 0, 0.15), inset 5px 5px 12px rgba(255, 255, 255, 0.85), 0 8px 20px var(--theme-glow);
            border: 1px solid rgba(255, 255, 255, 0.8);
            transition: transform 0.15s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease, background 0.4s ease;
            backdrop-filter: blur(4px);
        }

        .bubble-btn:hover {
            transform: scale(1.06);
            box-shadow: inset -5px -5px 12px rgba(0, 0, 0, 0.1), inset 5px 5px 15px rgba(255, 255, 255, 0.98), 0 12px 25px var(--theme-glow);
        }

        .bubble-btn:active {
            transform: scale(0.95);
        }

        /* Custom Shiny Glass Bubble Buttons matching provided images */
        .shiny-bubble-btn {
            position: relative;
            background: radial-gradient(circle at 35% 35%, rgba(255, 255, 255, 0.95) 0%, rgba(240, 248, 255, 0.85) 45%, rgba(210, 238, 255, 0.6) 75%, rgba(180, 220, 255, 0.4) 100%);
            border: 2px solid rgba(255, 255, 255, 0.9);
            box-shadow: inset -4px -4px 10px rgba(67, 142, 230, 0.25), inset 4px 4px 10px rgba(255, 255, 255, 1), 0 6px 16px rgba(30, 102, 196, 0.25);
            border-radius: 50%;
            cursor: pointer;
            transition: transform 0.15s ease, box-shadow 0.2s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            color: #1E66C4;
        }

        .shiny-bubble-btn::before {
            content: '';
            position: absolute;
            top: 6%;
            left: 15%;
            width: 35%;
            height: 25%;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.95);
            filter: blur(1px);
            transform: rotate(-35deg);
            pointer-events: none;
        }

        /* Iridescent rainbow edge glare */
        .shiny-bubble-btn::after {
            content: '';
            position: absolute;
            inset: -2px;
            border-radius: 50%;
            background: conic-gradient(from 45deg, transparent 0%, rgba(255, 180, 220, 0.4) 20%, rgba(160, 220, 255, 0.6) 40%, rgba(180, 255, 200, 0.4) 60%, rgba(255, 230, 160, 0.4) 80%, transparent 100%);
            mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            padding: 2px;
            pointer-events: none;
        }

        .shiny-bubble-btn:hover {
            transform: scale(1.08);
            box-shadow: inset -4px -4px 10px rgba(67, 142, 230, 0.15), inset 4px 4px 12px rgba(255, 255, 255, 1), 0 8px 22px rgba(30, 102, 196, 0.35);
        }

        .shiny-bubble-btn:active {
            transform: scale(0.95);
        }

        /* Interactive Game Bubbles - Uniform and less colorful */
        .pop-bubble {
            position: relative;
            width: 64px;
            height: 64px;
            background: radial-gradient(circle at 32% 32%, rgba(255,255,255,0.95) 0%, rgba(255,255,255,0.5) 30%, rgba(180, 225, 250, 0.6) 70%, rgba(100, 170, 230, 0.75) 100%);
            box-shadow: inset -3px -3px 8px rgba(20, 60, 100, 0.15), inset 3px 3px 8px rgba(255, 255, 255, 0.9), 0 4px 10px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.75);
            border-radius: 50%;
            cursor: pointer;
            transition: transform 0.1s ease-out, opacity 0.2s ease, filter 0.2s ease;
            flex-shrink: 0;
        }

        .pop-bubble::before {
            content: '';
            position: absolute;
            top: 12%;
            left: 18%;
            width: 28%;
            height: 20%;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.85);
            filter: blur(1px);
            transform: rotate(-30deg);
        }

        .pop-bubble::after {
            content: '';
            position: absolute;
            bottom: 15%;
            right: 20%;
            width: 16%;
            height: 12%;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.6);
            filter: blur(1px);
        }

        .pop-bubble:hover {
            transform: scale(1.06);
            filter: brightness(1.05);
        }

        /* Popping Animation */
        @keyframes pop-out {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.3); opacity: 0.8; }
            100% { transform: scale(1.6); opacity: 0; }
        }

        .popping {
            animation: pop-out 0.22s forwards ease-out;
            pointer-events: none;
        }

        /* Custom Scrollbars */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(0,0,0,0.05);
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb {
            background: var(--theme-secondary);
            border-radius: 4px;
        }

        /* Landscape Canvas Background */
        .bg-hills {
            background: linear-gradient(180deg, #3DA4FF 0%, #A0E0FF 45%, #C2F0FF 60%, #76CF20 60%, #4FA311 80%, #2E7305 100%);
        }

        .sun-burst {
            position: absolute;
            top: -100px;
            left: -100px;
            width: 500px;
            height: 500px;
            background: radial-gradient(circle, rgba(255,255,255,0.85) 0%, rgba(255,255,210,0.4) 35%, rgba(255,255,255,0) 70%);
            pointer-events: none;
        }

        /* Retro OS Button Styles */
        .os-btn {
            background: linear-gradient(180deg, #FFFFFF 0%, #E3E8EC 50%, #C2CEDA 100%);
            border: 1px solid #708090;
            box-shadow: inset 0 1px 0 #FFFFFF, 0 2px 4px rgba(0,0,0,0.15);
            color: #1A2B3C;
            font-weight: bold;
            border-radius: 6px;
            transition: all 0.15s;
        }
        .os-btn:hover {
            background: linear-gradient(180deg, #FFFFFF 0%, #EAF3FD 50%, #B2D1F5 100%);
            border-color: var(--theme-primary);
        }
        .os-btn:active {
            background: linear-gradient(180deg, #9FB3C8 0%, #DCE3EA 100%);
            box-shadow: inset 0 2px 3px rgba(0,0,0,0.2);
        }
        .os-btn-active {
            background: linear-gradient(180deg, var(--theme-header-1) 0%, var(--theme-header-2) 100%) !important;
            color: white !important;
            border-color: var(--theme-header-3) !important;
        }

        /* Color Swatch Ring Indicator */
        .swatch-selected {
            ring: 3px solid #1E66C4;
            transform: scale(1.15);
        }
    </style>
</head>
<body class="w-screen h-screen relative select-none overflow-hidden">
    <!-- Background Canvas Container -->
    <div id="bgContainer" class="absolute inset-0 bg-hills transition-all duration-700 ease-in-out">
        <!-- Sun effect -->
        <div class="sun-burst"></div>
        <!-- Animated Background Canvas for floating ambient bubbles -->
        <canvas id="ambientCanvas" class="absolute inset-0 w-full h-full pointer-events-none"></canvas>
    </div>

    <!-- Tint Layer (controlled via Settings) -->
    <div id="tintOverlay" class="absolute inset-0 pointer-events-none transition-colors duration-500" style="background-color: var(--theme-tint);"></div>

    <!-- ================= START PAGE ================= -->
    <div id="startPage" class="absolute inset-0 flex flex-col justify-between p-6 z-10 transition-opacity duration-500">
        <!-- Top Info Header -->
        <div class="w-full flex justify-between items-center max-w-5xl mx-auto pt-2">
            <div class="aero-window px-4 py-1.5 flex items-center gap-2 text-xs font-semibold text-slate-700 shadow-sm">
                <i class="fa-solid fa-droplet text-sky-500"></i>
                <span>Solacium Relaxation Suite v2.0</span>
            </div>
            
            <!-- Top Right Quick Controls -->
            <div class="flex gap-3">
                <button onclick="openHelp()" class="shiny-bubble-btn w-12 h-12 text-2xl font-bold" title="Help">
                    <i class="fa-solid fa-question"></i>
                </button>
                <button onclick="openSettings()" class="shiny-bubble-btn w-12 h-12 text-2xl font-bold" title="Settings">
                    <i class="fa-solid fa-gear"></i>
                </button>
            </div>
        </div>

        <!-- Center Solacium Title & Hero Bubble Buttons -->
        <div class="flex flex-col items-center justify-center my-auto text-center relative w-full max-w-3xl mx-auto">
            <h1 class="font-brand text-6xl md:text-8xl text-white drop-shadow-[0_4px_12px_rgba(0,60,140,0.6)] tracking-wide mb-2">
                solacium
            </h1>
            <p class="text-sky-100 text-base md:text-xl font-medium drop-shadow-[0_2px_4px_rgba(0,0,0,0.4)] mb-10">
                Unwind. Pop bubbles. Release stress.
            </p>

            <!-- Main Proceed Bubble Button -->
            <div class="relative flex items-center justify-center gap-12">
                <!-- Setting > Side Bubble -->
                <button onclick="openSettings()" class="bubble-btn w-28 h-28 rounded-full flex items-center justify-center text-slate-800 font-bold text-sm hover:scale-110">
                    <span class="font-brand text-lg text-slate-800">Setting &gt;</span>
                </button>

                <!-- Proceed > Hero Bubble -->
                <button onclick="startGame()" class="bubble-btn w-44 h-44 rounded-full flex flex-col items-center justify-center gap-1 text-slate-800 font-bold group cursor-pointer shadow-2xl">
                    <span class="font-brand text-2xl text-slate-900 group-hover:scale-110 transition-transform">Proceed &gt;</span>
                    <span class="text-[11px] text-slate-700 font-bold bg-white/60 px-3 py-0.5 rounded-full shadow-xs">Tap to Play</span>
                </button>
            </div>
        </div>

        <!-- Bottom Bar -->
        <div class="w-full max-w-md mx-auto pb-4 text-center">
            <div class="aero-window py-2 px-6 rounded-full inline-block text-xs font-semibold text-slate-600 shadow-md">
                ✨ Tip: Pop bubbles smoothly to create tranquil soundscapes.
            </div>
        </div>
    </div>

    <!-- ================= GAME PLAY SCREEN ================= -->
    <div id="gamePage" class="absolute inset-0 flex flex-col justify-between p-4 md:p-6 z-10 hidden opacity-0 transition-opacity duration-500">
        <!-- Top Navigation Bar -->
        <div class="w-full flex justify-between items-center max-w-6xl mx-auto">
            <!-- Home Button -->
            <button onclick="goToHome()" class="shiny-bubble-btn px-5 py-2.5 rounded-full flex items-center gap-2 font-bold text-sm shadow-md">
                <i class="fa-solid fa-house text-lg"></i>
                <span class="hidden sm:inline">Home</span>
            </button>

            <!-- Top Right Controls (Reset, Help, Settings) -->
            <div class="flex items-center gap-3">
                <button onclick="resetBubbles()" class="shiny-bubble-btn px-5 py-2.5 rounded-full flex items-center gap-2 font-bold text-sm shadow-md" title="Resets the bubbles">
                    <i class="fa-solid fa-rotate-right text-lg"></i>
                    <span>Reset</span>
                </button>
                <button onclick="openHelp()" class="shiny-bubble-btn w-12 h-12 text-2xl font-bold" title="Help">
                    <i class="fa-solid fa-question"></i>
                </button>
                <button onclick="openSettings()" class="shiny-bubble-btn w-12 h-12 text-2xl font-bold" title="Settings">
                    <i class="fa-solid fa-gear"></i>
                </button>
            </div>
        </div>

        <!-- Center Interactive Game Grid Area -->
        <div class="flex-1 w-full max-w-5xl mx-auto my-4 relative flex items-center justify-center">
            <!-- Bubble Matrix Container -->
            <div id="bubbleGrid" class="w-full h-full max-h-[600px] bg-white/10 backdrop-blur-sm rounded-3xl p-4 border border-white/30 shadow-2xl grid grid-cols-5 sm:grid-cols-6 md:grid-cols-8 gap-3 sm:gap-4 place-items-center overflow-y-auto">
                <!-- Dynamic Bubbles Injected via JS -->
            </div>
        </div>
    </div>

    <!-- ================= SETTINGS POPUP MODAL ================= -->
    <div id="settingsModal" class="fixed inset-0 bg-black/30 backdrop-blur-xs flex items-center justify-center z-50 hidden opacity-0 transition-opacity duration-300">
        <div class="aero-window w-[92%] max-w-md overflow-hidden transform scale-95 transition-transform duration-300" id="settingsBox">
            <!-- Header Bar -->
            <div class="aero-header px-4 py-2.5 flex justify-between items-center">
                <div class="flex items-center gap-2 text-sm font-bold">
                    <i class="fa-solid fa-sliders"></i>
                    <span>SETTINGS</span>
                </div>
                <!-- Standard OS Modal Controls -->
                <div class="flex items-center gap-1">
                    <button class="w-5 h-5 bg-sky-200/30 text-white rounded text-xs hover:bg-sky-200/50 flex items-center justify-center">_</button>
                    <button class="w-5 h-5 bg-sky-200/30 text-white rounded text-xs hover:bg-sky-200/50 flex items-center justify-center">□</button>
                    <button onclick="closeSettings()" class="w-5 h-5 bg-red-500 hover:bg-red-600 text-white rounded text-xs font-bold flex items-center justify-center">✕</button>
                </div>
            </div>

            <!-- Settings Content -->
            <div class="p-6 space-y-6 text-slate-800 text-sm">
                <!-- Volume Controls -->
                <div class="space-y-2">
                    <div class="flex justify-between font-bold text-slate-700">
                        <label class="flex items-center gap-2">
                            <i class="fa-solid fa-volume-high text-sky-600"></i> Volume
                        </label>
                        <span id="volValueText" class="text-xs text-sky-600 font-bold">70%</span>
                    </div>
                    <div class="flex items-center gap-3">
                        <i class="fa-solid fa-volume-xmark text-slate-400"></i>
                        <input type="range" id="volumeSlider" min="0" max="100" value="70" oninput="updateVolume(this.value)" class="w-full accent-sky-500 h-2 bg-slate-200 rounded-lg appearance-none cursor-pointer">
                        <i class="fa-solid fa-volume-high text-sky-600"></i>
                    </div>
                </div>

                <!-- SFX Toggle -->
                <div class="flex items-center justify-between border-t border-slate-200 pt-4">
                    <span class="font-bold text-slate-700 flex items-center gap-2">
                        <i class="fa-solid fa-toggle-on text-emerald-600"></i> SFX Audio
                    </span>
                    <label class="relative inline-flex items-center cursor-pointer">
                        <input type="checkbox" id="sfxToggle" checked onchange="toggleSFX(this.checked)" class="sr-only peer">
                        <div class="w-11 h-6 bg-gray-300 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-emerald-500"></div>
                    </label>
                </div>

                <!-- Color Theme Tint Selector Swatches -->
                <div class="border-t border-slate-200 pt-4 space-y-2">
                    <label class="font-bold text-slate-700 block">Tint Color Overlay Theme</label>
                    <div class="flex items-center justify-between gap-1 pt-1">
                        <!-- Swatches matching screenshot: Orange, Red, Purple, Dark Blue, Light Blue, Green, Yellow, Pink -->
                        <button onclick="setThemeColor('orange', this)" class="swatch-btn w-6 h-6 rounded-full bg-orange-500 border-2 border-white shadow-sm" title="Orange"></button>
                        <button onclick="setThemeColor('red', this)" class="swatch-btn w-6 h-6 rounded-full bg-red-600 border-2 border-white shadow-sm" title="Red"></button>
                        <button onclick="setThemeColor('purple', this)" class="swatch-btn w-6 h-6 rounded-full bg-purple-700 border-2 border-white shadow-sm" title="Purple"></button>
                        <button onclick="setThemeColor('blue', this)" class="swatch-btn w-6 h-6 rounded-full bg-blue-600 border-2 border-white shadow-sm ring-2 ring-sky-500 transform scale-110" title="Dark Blue"></button>
                        <button onclick="setThemeColor('cyan', this)" class="swatch-btn w-6 h-6 rounded-full bg-sky-400 border-2 border-white shadow-sm" title="Light Blue"></button>
                        <button onclick="setThemeColor('green', this)" class="swatch-btn w-6 h-6 rounded-full bg-lime-500 border-2 border-white shadow-sm" title="Green"></button>
                        <button onclick="setThemeColor('yellow', this)" class="swatch-btn w-6 h-6 rounded-full bg-yellow-400 border-2 border-white shadow-sm" title="Yellow"></button>
                        <button onclick="setThemeColor('pink', this)" class="swatch-btn w-6 h-6 rounded-full bg-pink-400 border-2 border-white shadow-sm" title="Pink"></button>
                    </div>
                </div>

                <!-- Quick Navigation to Sub Settings Modals -->
                <div class="border-t border-slate-200 pt-4 flex gap-2">
                    <button onclick="openBackgroundModal()" class="os-btn flex-1 py-2 px-2 text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-image text-sky-600"></i>
                        <span>Background</span>
                    </button>
                    <button onclick="openBGMModal()" class="os-btn flex-1 py-2 px-2 text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-compact-disc text-emerald-600"></i>
                        <span>BGM</span>
                    </button>
                    <button onclick="openSFXModal()" class="os-btn flex-1 py-2 px-2 text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-music text-purple-600"></i>
                        <span>SFX Choice</span>
                    </button>
                </div>
            </div>

            <!-- Footer Close -->
            <div class="bg-slate-100 px-6 py-3 border-t border-slate-200 flex justify-end">
                <button onclick="closeSettings()" class="os-btn px-6 py-1.5 text-xs font-bold">OK</button>
            </div>
        </div>
    </div>

    <!-- ================= BACKGROUND MUSIC OPTIONS MODAL ================= -->
    <div id="bgmModal" class="fixed inset-0 bg-black/30 backdrop-blur-xs flex items-center justify-center z-50 hidden opacity-0 transition-opacity duration-300">
        <div class="aero-window w-[92%] max-w-sm overflow-hidden transform scale-95 transition-transform duration-300">
            <!-- Header -->
            <div class="aero-header px-4 py-2.5 flex justify-between items-center">
                <div class="flex items-center gap-2 text-sm font-bold">
                    <i class="fa-solid fa-music"></i>
                    <span>BACKGROUND MUSIC OPTIONS</span>
                </div>
                <button onclick="closeBGMModal()" class="w-5 h-5 bg-red-500 hover:bg-red-600 text-white rounded text-xs font-bold flex items-center justify-center">✕</button>
            </div>

            <!-- Content matching flow chart choices -->
            <div class="p-5 space-y-3">
                <p class="text-xs text-slate-600 font-semibold">Select the background music</p>
                
                <div class="grid grid-cols-3 gap-2">
                    <button onclick="selectBGMTrack('none', this)" class="bgm-btn os-btn os-btn-active py-2.5 px-2 text-xs flex items-center justify-center font-bold">
                        None
                    </button>
                    <button onclick="selectBGMTrack('calm', this)" class="bgm-btn os-btn py-2.5 px-2 text-xs flex items-center justify-center font-bold">
                        Calm
                    </button>
                    <button onclick="selectBGMTrack('cute', this)" class="bgm-btn os-btn py-2.5 px-2 text-xs flex items-center justify-center font-bold">
                        Cute
                    </button>
                    <button onclick="selectBGMTrack('soft', this)" class="bgm-btn os-btn py-2.5 px-2 text-xs flex items-center justify-center font-bold">
                        Soft
                    </button>
                    <button onclick="selectBGMTrack('soothing', this)" class="bgm-btn os-btn py-2.5 px-2 text-xs flex items-center justify-center font-bold">
                        Soothing
                    </button>
                    <button onclick="selectBGMTrack('chillhop', this)" class="bgm-btn os-btn py-2.5 px-2 text-xs flex items-center justify-center font-bold">
                        Chill hop
                    </button>
                </div>
            </div>

            <!-- Footer -->
            <div class="bg-slate-100 px-5 py-3 border-t border-slate-200 flex justify-end">
                <button onclick="closeBGMModal()" class="os-btn px-5 py-1 text-xs">Apply</button>
            </div>
        </div>
    </div>

    <!-- ================= BACKGROUND SELECTION MODAL ================= -->
    <div id="bgModal" class="fixed inset-0 bg-black/30 backdrop-blur-xs flex items-center justify-center z-50 hidden opacity-0 transition-opacity duration-300">
        <div class="aero-window w-[92%] max-w-lg overflow-hidden transform scale-95 transition-transform duration-300">
            <!-- Header -->
            <div class="aero-header px-4 py-2.5 flex justify-between items-center">
                <div class="flex items-center gap-2 text-sm font-bold">
                    <i class="fa-solid fa-image"></i>
                    <span>BACKGROUNDS</span>
                </div>
                <button onclick="closeBackgroundModal()" class="w-5 h-5 bg-red-500 hover:bg-red-600 text-white rounded text-xs font-bold flex items-center justify-center">✕</button>
            </div>

            <!-- Content Grid -->
            <div class="p-5 space-y-3">
                <p class="text-xs text-slate-600 font-semibold">Select a picture to change the background:</p>
                <div class="grid grid-cols-3 gap-3">
                    <!-- Wallpaper 1 -->
                    <button onclick="changeBackground('hills', this)" class="bg-card group border-2 border-sky-500 rounded-lg overflow-hidden p-1 bg-white hover:shadow-md transition-all">
                        <div class="h-20 rounded bg-gradient-to-b from-sky-400 via-sky-200 to-emerald-500 relative flex items-end justify-center pb-1">
                            <span class="text-[10px] font-bold text-white drop-shadow">Wallpaper 1</span>
                        </div>
                    </button>
                    <!-- Wallpaper 2 -->
                    <button onclick="changeBackground('sunset', this)" class="bg-card group border-2 border-transparent hover:border-sky-400 rounded-lg overflow-hidden p-1 bg-white hover:shadow-md transition-all">
                        <div class="h-20 rounded bg-gradient-to-b from-amber-500 via-rose-400 to-purple-800 relative flex items-end justify-center pb-1">
                            <span class="text-[10px] font-bold text-white drop-shadow">Wallpaper 2</span>
                        </div>
                    </button>
                    <!-- Wallpaper 3 -->
                    <button onclick="changeBackground('ocean', this)" class="bg-card group border-2 border-transparent hover:border-sky-400 rounded-lg overflow-hidden p-1 bg-white hover:shadow-md transition-all">
                        <div class="h-20 rounded bg-gradient-to-b from-cyan-400 via-blue-600 to-indigo-900 relative flex items-end justify-center pb-1">
                            <span class="text-[10px] font-bold text-white drop-shadow">Wallpaper 3</span>
                        </div>
                    </button>
                    <!-- Wallpaper 4 -->
                    <button onclick="changeBackground('clouds', this)" class="bg-card group border-2 border-transparent hover:border-sky-400 rounded-lg overflow-hidden p-1 bg-white hover:shadow-md transition-all">
                        <div class="h-20 rounded bg-gradient-to-b from-sky-300 via-indigo-200 to-slate-300 relative flex items-end justify-center pb-1">
                            <span class="text-[10px] font-bold text-slate-700 drop-shadow">Wallpaper 4</span>
                        </div>
                    </button>
                    <!-- Wallpaper 5 -->
                    <button onclick="changeBackground('space', this)" class="bg-card group border-2 border-transparent hover:border-sky-400 rounded-lg overflow-hidden p-1 bg-white hover:shadow-md transition-all">
                        <div class="h-20 rounded bg-gradient-to-b from-indigo-950 via-purple-900 to-slate-900 relative flex items-end justify-center pb-1">
                            <span class="text-[10px] font-bold text-purple-200 drop-shadow">Wallpaper 5</span>
                        </div>
                    </button>
                    <!-- Wallpaper 6 -->
                    <button onclick="changeBackground('mint', this)" class="bg-card group border-2 border-transparent hover:border-sky-400 rounded-lg overflow-hidden p-1 bg-white hover:shadow-md transition-all">
                        <div class="h-20 rounded bg-gradient-to-b from-emerald-300 via-teal-400 to-cyan-600 relative flex items-end justify-center pb-1">
                            <span class="text-[10px] font-bold text-white drop-shadow">Wallpaper 6</span>
                        </div>
                    </button>
                </div>
            </div>

            <!-- Footer -->
            <div class="bg-slate-100 px-5 py-3 border-t border-slate-200 flex justify-end">
                <button onclick="closeBackgroundModal()" class="os-btn px-5 py-1 text-xs">Done</button>
            </div>
        </div>
    </div>

    <!-- ================= SFX CHOICE MODAL ================= -->
    <div id="sfxModal" class="fixed inset-0 bg-black/30 backdrop-blur-xs flex items-center justify-center z-50 hidden opacity-0 transition-opacity duration-300">
        <div class="aero-window w-[92%] max-w-sm overflow-hidden transform scale-95 transition-transform duration-300">
            <!-- Header -->
            <div class="aero-header px-4 py-2.5 flex justify-between items-center">
                <div class="flex items-center gap-2 text-sm font-bold">
                    <i class="fa-solid fa-music"></i>
                    <span>SFX CHOICE</span>
                </div>
                <button onclick="closeSFXModal()" class="w-5 h-5 bg-red-500 hover:bg-red-600 text-white rounded text-xs font-bold flex items-center justify-center">✕</button>
            </div>

            <!-- Content matching flow chart choices -->
            <div class="p-5 space-y-3">
                <p class="text-xs text-slate-600 font-semibold">Select the sound effect that plays when popping the bubbles:</p>
                
                <div class="grid grid-cols-3 gap-2">
                    <button onclick="selectSoundEffect('default', this)" class="sfx-btn os-btn os-btn-active py-2 px-2 text-xs flex items-center justify-center">
                        Default Pop
                    </button>
                    <button onclick="selectSoundEffect('bruh', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        Bruh
                    </button>
                    <button onclick="selectSoundEffect('getout', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        Get Out
                    </button>
                    <button onclick="selectSoundEffect('fart', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        Fart #1
                    </button>
                    <button onclick="selectSoundEffect('vineboom', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        Vine Boom
                    </button>
                    <button onclick="selectSoundEffect('sixseven', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        Six Seven
                    </button>
                    <button onclick="selectSoundEffect('fahhh', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        FAHHH
                    </button>
                    <button onclick="selectSoundEffect('heehee', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        Hee Hee
                    </button>
                    <button onclick="selectSoundEffect('verity', this)" class="sfx-btn os-btn py-2 px-2 text-xs flex items-center justify-center">
                        verity
                    </button>
                </div>
            </div>

            <!-- Footer -->
            <div class="bg-slate-100 px-5 py-3 border-t border-slate-200 flex justify-end">
                <button onclick="closeSFXModal()" class="os-btn px-5 py-1 text-xs">Apply</button>
            </div>
        </div>
    </div>

    <!-- ================= HELP POPUP MODAL ================= -->
    <div id="helpModal" class="fixed inset-0 bg-black/30 backdrop-blur-xs flex items-center justify-center z-50 hidden opacity-0 transition-opacity duration-300">
        <div class="aero-window w-[92%] max-w-md overflow-hidden transform scale-95 transition-transform duration-300">
            <!-- Header -->
            <div class="aero-header px-4 py-2.5 flex justify-between items-center">
                <div class="flex items-center gap-2 text-sm font-bold">
                    <i class="fa-solid fa-circle-question"></i>
                    <span>HELP</span>
                </div>
                <button onclick="closeHelp()" class="w-5 h-5 bg-red-500 hover:bg-red-600 text-white rounded text-xs font-bold flex items-center justify-center">✕</button>
            </div>

            <!-- Help Body Text matching chart layout -->
            <div class="p-6 text-slate-800 text-sm leading-relaxed space-y-4">
                <div class="bg-sky-50 border border-sky-200 p-4 rounded-xl text-xs text-sky-900 leading-relaxed shadow-inner">
                    Welcome to <strong>Solacium!</strong> In this game, you pop bubbles. To start the game, press the <strong>proceed button</strong>. To change the volume, music, sounds, color theme, and wallpaper, click the <strong>setting button</strong>.
                </div>
            </div>

            <!-- Footer Close Button -->
            <div class="bg-slate-100 px-6 py-3 border-t border-slate-200 flex justify-end">
                <button onclick="closeHelp()" class="os-btn px-6 py-1.5 text-xs font-bold">Close</button>
            </div>
        </div>
    </div>

    <script>
        /* ================= DYNAMIC THEME COLOR SWITCHER ================= */
        const themePresets = {
            orange: {
                primary: '#EA580C',
                secondary: '#FB923C',
                accent: '#FBBF24',
                header1: '#FB923C',
                header2: '#EA580C',
                header3: '#9A3412',
                tint: 'rgba(249, 115, 22, 0.20)',
                glow: 'rgba(249, 115, 22, 0.40)'
            },
            red: {
                primary: '#DC2626',
                secondary: '#F87171',
                accent: '#FDE047',
                header1: '#EF4444',
                header2: '#DC2626',
                header3: '#991B1B',
                tint: 'rgba(239, 68, 68, 0.20)',
                glow: 'rgba(239, 68, 68, 0.40)'
            },
            purple: {
                primary: '#6D28D9',
                secondary: '#A855F7',
                accent: '#F472B6',
                header1: '#9333EA',
                header2: '#6D28D9',
                header3: '#4C1D95',
                tint: 'rgba(147, 51, 234, 0.20)',
                glow: 'rgba(147, 51, 234, 0.40)'
            },
            blue: {
                primary: '#1D4ED8',
                secondary: '#3B82F6',
                accent: '#60A5FA',
                header1: '#3B82F6',
                header2: '#1D4ED8',
                header3: '#1E3A8A',
                tint: 'rgba(37, 99, 235, 0.20)',
                glow: 'rgba(37, 99, 235, 0.40)'
            },
            cyan: {
                primary: '#0284C7',
                secondary: '#38BDF8',
                accent: '#34D399',
                header1: '#38BDF8',
                header2: '#0284C7',
                header3: '#0369A1',
                tint: 'rgba(56, 189, 248, 0.20)',
                glow: 'rgba(56, 189, 248, 0.40)'
            },
            green: {
                primary: '#65A30D',
                secondary: '#84CC16',
                accent: '#FACC15',
                header1: '#84CC16',
                header2: '#65A30D',
                header3: '#3F6212',
                tint: 'rgba(132, 204, 22, 0.20)',
                glow: 'rgba(132, 204, 22, 0.40)'
            },
            yellow: {
                primary: '#CA8A04',
                secondary: '#EAB308',
                accent: '#FDE047',
                header1: '#FACC15',
                header2: '#CA8A04',
                header3: '#854D0E',
                tint: 'rgba(234, 179, 8, 0.20)',
                glow: 'rgba(234, 179, 8, 0.40)'
            },
            pink: {
                primary: '#DB2777',
                secondary: '#F472B6',
                accent: '#FBCFE8',
                header1: '#EC4899',
                header2: '#DB2777',
                header3: '#831843',
                tint: 'rgba(236, 72, 153, 0.20)',
                glow: 'rgba(236, 72, 153, 0.40)'
            }
        };

        function setThemeColor(colorKey, btn) {
            const theme = themePresets[colorKey];
            if (!theme) return;

            // Update Root CSS Variables
            const root = document.documentElement;
            root.style.setProperty('--theme-primary', theme.primary);
            root.style.setProperty('--theme-secondary', theme.secondary);
            root.style.setProperty('--theme-accent', theme.accent);
            root.style.setProperty('--theme-header-1', theme.header1);
            root.style.setProperty('--theme-header-2', theme.header2);
            root.style.setProperty('--theme-header-3', theme.header3);
            root.style.setProperty('--theme-tint', theme.tint);
            root.style.setProperty('--theme-glow', theme.glow);

            // Highlight chosen button swatch
            document.querySelectorAll('.swatch-btn').forEach(b => {
                b.classList.remove('ring-2', 'ring-sky-500', 'transform', 'scale-110');
            });
            if (btn) {
                btn.classList.add('ring-2', 'ring-sky-500', 'transform', 'scale-110');
            }
        }

        /* ================= AUDIO & SFX ADJUSTMENTS ================= */
        function updateVolume(val) {
            soundVolume = val / 100;
            document.getElementById('volValueText').innerText = `${val}%`;
            if (masterGain) {
                masterGain.gain.value = soundVolume;
            }
        }

        function toggleSFX(enabled) {
            soundEnabled = enabled;
        }

        function selectSoundEffect(sfxKey, btn) {
            currentSFX = sfxKey;
            document.querySelectorAll('.sfx-btn').forEach(b => b.classList.remove('os-btn-active'));
            if (btn) btn.classList.add('os-btn-active');
            playPopSound(150);
        }

        function changeBackground(theme, btn) {
            const bgContainer = document.getElementById('bgContainer');
            
            bgContainer.className = 'absolute inset-0 transition-all duration-700 ease-in-out ';

            if (theme === 'hills') {
                bgContainer.className += 'bg-hills';
            } else if (theme === 'sunset') {
                bgContainer.className += 'bg-gradient-to-b from-amber-500 via-rose-500 to-purple-900';
            } else if (theme === 'ocean') {
                bgContainer.className += 'bg-gradient-to-b from-cyan-400 via-blue-600 to-indigo-950';
            } else if (theme === 'clouds') {
                bgContainer.className += 'bg-gradient-to-b from-sky-300 via-indigo-200 to-slate-400';
            } else if (theme === 'space') {
                bgContainer.className += 'bg-gradient-to-b from-slate-950 via-purple-950 to-indigo-950';
            } else if (theme === 'mint') {
                bgContainer.className += 'bg-gradient-to-b from-emerald-300 via-teal-500 to-cyan-700';
            }

            document.querySelectorAll('.bg-card').forEach(b => b.classList.replace('border-sky-500', 'border-transparent'));
            if (btn) btn.classList.replace('border-transparent', 'border-sky-500');
        }

        window.onload = function() {
            initAudio();
            initCanvas();
            initBubbleGrid();
            animateCanvas();
        };

        /* ================= AUDIO SYNTHESIZER & SFX ================= */
        let audioCtx = null;
        let masterGain = null;
        let bgmGain = null;
        let soundVolume = 0.7;
        let soundEnabled = true;
        let currentSFX = 'default';
        let currentBGM = 'none';
        let bgmTimer = null;
        let bgmStep = 0;

        function initAudio() {
            try {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                if (AudioContext && !audioCtx) {
                    audioCtx = new AudioContext();
                    masterGain = audioCtx.createGain();
                    masterGain.gain.value = soundVolume;
                    masterGain.connect(audioCtx.destination);

                    bgmGain = audioCtx.createGain();
                    bgmGain.gain.value = 0.35; // Comfortable BGM level
                    bgmGain.connect(masterGain);
                }
            } catch (e) {
                console.warn('Web Audio API not supported', e);
            }
        }

        /* ================= BACKGROUND MUSIC SYNTHESIZER ================= */
        const bgmNotes = {
            calm: [261.63, 329.63, 392.00, 523.25, 392.00, 329.63], // C major arpeggio
            cute: [523.25, 659.25, 783.99, 659.25, 880.00, 783.99], // Upbeat high melody
            soft: [220.00, 277.18, 329.63, 440.00, 329.63, 277.18], // A major soft warmth
            soothing: [174.61, 220.00, 261.63, 349.23, 261.63, 220.00], // F major deep ambient
            chillhop: [146.83, 220.00, 261.63, 293.66, 349.23, 293.66] // D minor chill loop
        };

        function selectBGMTrack(trackKey, btn) {
            currentBGM = trackKey;
            document.querySelectorAll('.bgm-btn').forEach(b => b.classList.remove('os-btn-active'));
            if (btn) btn.classList.add('os-btn-active');
            
            stopBGM();
            if (trackKey !== 'none') {
                startBGM(trackKey);
            }
        }

        function stopBGM() {
            if (bgmTimer) {
                clearInterval(bgmTimer);
                bgmTimer = null;
            }
        }

        function startBGM(trackKey) {
            if (!soundEnabled) return;
            if (!audioCtx) initAudio();
            if (audioCtx && audioCtx.state === 'suspended') {
                audioCtx.resume();
            }

            bgmStep = 0;
            const notes = bgmNotes[trackKey] || bgmNotes.calm;
            const interval = trackKey === 'cute' ? 350 : trackKey === 'chillhop' ? 450 : 600;

            bgmTimer = setInterval(() => {
                if (!soundEnabled || currentBGM === 'none' || !audioCtx) return;

                const freq = notes[bgmStep % notes.length];
                const now = audioCtx.currentTime;

                const osc = audioCtx.createOscillator();
                const noteGain = audioCtx.createGain();

                osc.type = trackKey === 'cute' ? 'triangle' : trackKey === 'chillhop' ? 'sawtooth' : 'sine';
                osc.frequency.setValueAtTime(freq, now);

                const attack = 0.08;
                const release = interval / 1000 * 0.8;

                noteGain.gain.setValueAtTime(0, now);
                noteGain.gain.linearRampToValueAtTime(0.2, now + attack);
                noteGain.gain.exponentialRampToValueAtTime(0.001, now + attack + release);

                osc.connect(noteGain);
                noteGain.connect(bgmGain);

                osc.start(now);
                osc.stop(now + attack + release + 0.05);

                bgmStep++;
            }, interval);
        }

        function updateVolume(val) {
            soundVolume = val / 100;
            document.getElementById('volValueText').innerText = `${val}%`;
            if (masterGain) {
                masterGain.gain.value = soundVolume;
            }
        }

        function toggleSFX(enabled) {
            soundEnabled = enabled;
            if (!enabled) {
                stopBGM();
            } else if (currentBGM !== 'none') {
                startBGM(currentBGM);
            }
        }

        function playPopSound(freqOffset = 0) {
            if (!soundEnabled) return;
            if (!audioCtx) initAudio();
            if (audioCtx && audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
            if (!audioCtx) return;

            const now = audioCtx.currentTime;

            if (currentSFX === 'bruh') {
                // Low pitched synth tone mimicking "bruh" vocal pitch drop
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(140 + freqOffset, now);
                osc.frequency.exponentialRampToValueAtTime(70, now + 0.35);
                gain.gain.setValueAtTime(0.4 * soundVolume, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.35);
                osc.connect(gain);
                gain.connect(masterGain);
                osc.start(now);
                osc.stop(now + 0.36);
            } else if (currentSFX === 'getout') {
                // Staccato dual pulse
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'square';
                osc.frequency.setValueAtTime(320, now);
                osc.frequency.setValueAtTime(220, now + 0.1);
                gain.gain.setValueAtTime(0.3 * soundVolume, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.25);
                osc.connect(gain);
                gain.connect(masterGain);
                osc.start(now);
                osc.stop(now + 0.26);
            } else if (currentSFX === 'fart') {
                // Low noise / frequency wobble sweep
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(90, now);
                osc.frequency.linearRampToValueAtTime(45, now + 0.3);
                gain.gain.setValueAtTime(0.5 * soundVolume, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
                osc.connect(gain);
                gain.connect(masterGain);
                osc.start(now);
                osc.stop(now + 0.31);
           } else if (currentSFX === 'vineboom') {
    const boom = new Audio(
        'https://www.myinstants.com/media/sounds/vine-boom.mp3'
    );

    boom.volume = soundVolume;
    boom.play().catch(err => {
        console.error('Failed to play Vine Boom:', err);
    });
}
            } else if (currentSFX === 'sixseven') {
                // Two upbeat tones
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(523.25, now); // C5
                osc.frequency.setValueAtTime(659.25, now + 0.1); // E5
                gain.gain.setValueAtTime(0.3 * soundVolume, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.25);
                osc.connect(gain);
                gain.connect(masterGain);
                osc.start(now);
                osc.stop(now + 0.26);
            } else if (currentSFX === 'fahhh') {
                // High airy chirp sweep
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(800, now);
                osc.frequency.exponentialRampToValueAtTime(250, now + 0.4);
                gain.gain.setValueAtTime(0.4 * soundVolume, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.4);
                osc.connect(gain);
                gain.connect(masterGain);
                osc.start(now);
                osc.stop(now + 0.41);
            } else if (currentSFX === 'heehee') {
                // Double high pitched chirp
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(1050, now);
                osc.frequency.setValueAtTime(1300, now + 0.08);
                gain.gain.setValueAtTime(0.35 * soundVolume, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.22);
                osc.connect(gain);
                gain.connect(masterGain);
                osc.start(now);
                osc.stop(now + 0.23);
            } else if (currentSFX === 'verity') {
                // Harmonic arpeggiated chime
                const freqs = [523.25, 659.25, 783.99];
                freqs.forEach((f, idx) => {
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(f, now + idx * 0.05);
                    gain.gain.setValueAtTime(0.2 * soundVolume, now + idx * 0.05);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + idx * 0.05 + 0.3);
                    osc.connect(gain);
                    gain.connect(masterGain);
                    osc.start(now + idx * 0.05);
                    osc.stop(now + idx * 0.05 + 0.31);
                });
            } else {
                // Default Bubble Pop
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(400 + Math.random() * 200, now);
                osc.frequency.exponentialRampToValueAtTime(800 + Math.random() * 300, now + 0.08);
                gain.gain.setValueAtTime(0.4 * soundVolume, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.08);
                osc.connect(gain);
                gain.connect(masterGain);
                osc.start(now);
                osc.stop(now + 0.09);
            }
        }

        /* ================= AMBIENT CANVAS BUBBLE PHYSICS ================= */
        let canvas, ctx;
        let ambientBubbles = [];

        function initCanvas() {
            canvas = document.getElementById('ambientCanvas');
            if (!canvas) return;
            ctx = canvas.getContext('2d');
            resizeCanvas();
            window.addEventListener('resize', resizeCanvas);

            ambientBubbles = [];
            for (let i = 0; i < 25; i++) {
                ambientBubbles.push(createAmbientBubble());
            }
        }

        function resizeCanvas() {
            if (!canvas) return;
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }

        function createAmbientBubble() {
            return {
                x: Math.random() * (canvas ? canvas.width : window.innerWidth),
                y: (canvas ? canvas.height : window.innerHeight) + Math.random() * 100,
                radius: 12 + Math.random() * 28,
                speedY: 0.5 + Math.random() * 1.2,
                wobble: Math.random() * Math.PI * 2,
                wobbleSpeed: 0.02 + Math.random() * 0.03,
                opacity: 0.2 + Math.random() * 0.4
            };
        }

        function animateCanvas() {
            if (canvas && ctx) {
                ctx.clearRect(0, 0, canvas.width, canvas.height);

                ambientBubbles.forEach((b) => {
                    b.y -= b.speedY;
                    b.wobble += b.wobbleSpeed;
                    const curX = b.x + Math.sin(b.wobble) * 15;

                    if (b.y + b.radius < -20) {
                        Object.assign(b, createAmbientBubble());
                    }

                    // Render floating bubble
                    ctx.save();
                    ctx.beginPath();
                    ctx.arc(curX, b.y, b.radius, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(255, 255, 255, ${b.opacity * 0.3})`;
                    ctx.fill();

                    ctx.strokeStyle = `rgba(255, 255, 255, ${b.opacity * 0.7})`;
                    ctx.lineWidth = 1.5;
                    ctx.stroke();

                    // Bubble glint
                    ctx.beginPath();
                    ctx.arc(curX - b.radius * 0.3, b.y - b.radius * 0.3, b.radius * 0.25, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(255, 255, 255, ${b.opacity * 0.8})`;
                    ctx.fill();
                    ctx.restore();
                });
            }
            requestAnimationFrame(animateCanvas);
        }

        /* ================= GAME PAGE BUBBLE GRID ================= */
        const BUBBLE_COUNT = 32; // Exactly 32 uniform bubbles

        function initBubbleGrid() {
            const grid = document.getElementById('bubbleGrid');
            if (!grid) return;
            grid.innerHTML = '';

            for (let i = 0; i < BUBBLE_COUNT; i++) {
                const bubble = document.createElement('div');
                bubble.className = 'pop-bubble';
                bubble.setAttribute('role', 'button');
                bubble.setAttribute('aria-label', 'Pop Bubble');
                bubble.addEventListener('click', (e) => popBubble(e.currentTarget));
                grid.appendChild(bubble);
            }
        }

        function popBubble(el) {
            if (el.classList.contains('popping') || el.style.visibility === 'hidden') return;

            el.classList.add('popping');
            playPopSound();

            setTimeout(() => {
                el.style.visibility = 'hidden';
                el.classList.remove('popping');
            }, 200);
        }

        function resetBubbles() {
            const bubbles = document.querySelectorAll('.pop-bubble');
            bubbles.forEach((b) => {
                b.style.visibility = 'visible';
                b.classList.remove('popping');
            });
            playPopSound(50);
        }

        /* ================= NAVIGATION & MODAL CONTROLS ================= */
        function startGame() {
            if (!audioCtx) initAudio();
            const startPage = document.getElementById('startPage');
            const gamePage = document.getElementById('gamePage');

            startPage.classList.add('opacity-0');
            setTimeout(() => {
                startPage.classList.add('hidden');
                gamePage.classList.remove('hidden');
                setTimeout(() => gamePage.classList.remove('opacity-0'), 50);
            }, 500);
        }

        function goToHome() {
            const startPage = document.getElementById('startPage');
            const gamePage = document.getElementById('gamePage');

            gamePage.classList.add('opacity-0');
            setTimeout(() => {
                gamePage.classList.add('hidden');
                startPage.classList.remove('hidden');
                setTimeout(() => startPage.classList.remove('opacity-0'), 50);
            }, 500);
        }

        function openModal(id) {
            const modal = document.getElementById(id);
            if (!modal) return;
            modal.classList.remove('hidden');
            setTimeout(() => modal.classList.remove('opacity-0'), 10);
        }

        function closeModal(id) {
            const modal = document.getElementById(id);
            if (!modal) return;
            modal.classList.add('opacity-0');
            setTimeout(() => modal.classList.add('hidden'), 300);
        }

        function openSettings() { openModal('settingsModal'); }
        function closeSettings() { closeModal('settingsModal'); }

        function openBackgroundModal() { openModal('bgModal'); }
        function closeBackgroundModal() { closeModal('bgModal'); }

        function openSFXModal() { openModal('sfxModal'); }
        function closeSFXModal() { closeModal('sfxModal'); }

        function openBGMModal() { openModal('bgmModal'); }
        function closeBGMModal() { closeModal('bgmModal'); }

        function openHelp() { openModal('helpModal'); }
        function closeHelp() { closeModal('helpModal'); }
    </script>
</body>
</html>
