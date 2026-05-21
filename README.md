# RinneRebirth-The-Monarch-System
Ayden's personal development app
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RinneRebirth // The Monarch System</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Syne:wght@700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Space Grotesk', sans-serif;
            background-color: #030303; /* Obsidian Black */
            color: #f4f4f5;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(139, 92, 246, 0.05) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(139, 92, 246, 0.05) 0%, transparent 40%);
        }
        
        h1, h2, h3, .anime-headers {
            font-family: 'Syne', sans-serif;
            font-weight: 800;
        }

        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #030303;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #1e1b4b; /* Dark Indigo */
            border-radius: 3px;
            border: 1px solid #4c1d95;
        }

        /* Purple glowing energy effect */
        .glowing-monarch-border {
            box-shadow: 0 0 15px rgba(139, 92, 246, 0.15);
            border: 1px solid rgba(139, 92, 246, 0.3);
        }

        .glowing-monarch-border-active {
            box-shadow: 0 0 25px rgba(139, 92, 246, 0.4);
            border: 1px solid rgba(139, 92, 246, 0.8);
        }

        /* Pulsing status orb */
        .orb-pulse {
            animation: orb-pulse-anim 2s infinite;
        }

        @keyframes orb-pulse-anim {
            0% { transform: scale(1); opacity: 0.6; box-shadow: 0 0 0 0 rgba(139, 92, 246, 0.7); }
            70% { transform: scale(1.1); opacity: 1; box-shadow: 0 0 0 8px rgba(139, 92, 246, 0); }
            100% { transform: scale(1); opacity: 0.6; box-shadow: 0 0 0 0 rgba(139, 92, 246, 0); }
        }

        /* Progress Bar fill glow */
        .progress-bar-glow {
            box-shadow: 0 0 10px rgba(167, 139, 250, 0.5);
            transition: width 0.6s cubic-bezier(0.16, 1, 0.3, 1);
        }
    </style>
</head>
<body class="min-h-screen flex flex-col custom-scrollbar pb-12" onload="initSystem()">

    <!-- Header / Navigation Bar -->
    <header class="border-b border-purple-950 bg-zinc-950/90 backdrop-blur sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-18 py-3 flex flex-col sm:flex-row items-center justify-between gap-4">
            <div class="flex items-center space-x-3">
                <div class="p-2 bg-purple-950/60 border border-purple-500/40 rounded-lg text-violet-400 shadow-sm shadow-violet-500/10 cursor-pointer" onclick="playSystemSound('boot')">
                    <svg class="w-6 h-6 animate-pulse" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path></svg>
                </div>
                <div>
                    <h1 class="text-xl font-black text-white tracking-widest flex items-center gap-1.5 uppercase">
                        <span>RINNE REBIRTH</span>
                        <span class="text-xs text-violet-500 font-mono tracking-normal border border-violet-800 px-1.5 py-0.5 rounded bg-violet-950/40">v2.7</span>
                    </h1>
                    <p class="text-[10px] text-zinc-500 font-mono uppercase tracking-widest">[ SYSTEM STATE: AWAKENING ]</p>
                </div>
            </div>
            
            <!-- Global System Synchronization Indicator -->
            <div class="w-full sm:w-72 md:w-96 flex flex-col space-y-1">
                <div class="flex justify-between text-xs font-mono text-zinc-400 uppercase">
                    <span>Synchronisation Rate</span>
                    <span id="global-sync-percent" class="text-violet-400 font-bold">0%</span>
                </div>
                <div class="w-full bg-zinc-950 h-3.5 rounded-full border border-purple-950 p-0.5 overflow-hidden">
                    <div id="global-sync-bar" class="bg-gradient-to-r from-violet-600 to-fuchsia-500 h-full rounded-full progress-bar-glow" style="width: 0%"></div>
                </div>
            </div>

            <div class="text-xs text-zinc-400 hidden lg:flex items-center gap-2 font-mono">
                <span class="w-2.5 h-2.5 rounded-full bg-violet-500 orb-pulse"></span>
                <span>DESTINATION: OUTDOOR HORIZON (SUMMER '27)</span>
            </div>
        </div>
    </header>

    <!-- Main Workspace Container -->
    <div class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 flex flex-col lg:flex-row gap-8">
        
        <!-- Sidebar Navigation (Responsive Tabs) -->
        <aside class="w-full lg:w-64 flex-shrink-0">
            <nav class="space-y-2" aria-label="Sidebar" id="tab-nav">
                <button onclick="switchTab('roadmap')" id="nav-roadmap" class="w-full flex items-center justify-between px-4 py-3 text-sm font-semibold rounded-xl bg-purple-950/40 border border-purple-500/50 text-white shadow-lg shadow-purple-950/20 transition-all duration-150">
                    <div class="flex items-center space-x-3">
                        <svg class="w-5 h-5 text-violet-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v4a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v4a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v4a2 2 0 01-2 2H6a2 2 0 01-2-2v-4zM14 16a2 2 0 012-2h2a2 2 0 012 2v4a2 2 0 01-2 2h-2a2 2 0 01-2-2v-4z"></path></svg>
                        <span class="tracking-wider uppercase text-xs">System Roadmap</span>
                    </div>
                </button>
                <button onclick="switchTab('pip')" id="nav-pip" class="w-full flex items-center justify-between px-4 py-3 text-sm font-semibold rounded-xl text-zinc-400 hover:bg-zinc-900 hover:text-white transition-all duration-150">
                    <div class="flex items-center space-x-3">
                        <svg class="w-5 h-5 text-zinc-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"></path></svg>
                        <span class="tracking-wider uppercase text-xs">PIP Companion</span>
                    </div>
                    <span class="text-[9px] bg-violet-950 text-violet-400 px-1.5 py-0.5 rounded font-black border border-violet-900 uppercase">SYS_AI</span>
                </button>
                <button onclick="switchTab('smallclaims')" id="nav-smallclaims" class="w-full flex items-center justify-between px-4 py-3 text-sm font-semibold rounded-xl text-zinc-400 hover:bg-zinc-900 hover:text-white transition-all duration-150">
                    <div class="flex items-center space-x-3">
                        <svg class="w-5 h-5 text-zinc-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 6l3 1m0 0l-3 9a5.002 5.002 0 006.001 0M6 7l3 9M6 7l6-2m6 2l3-1m-3 1l-3 9a5.002 5.002 0 006.001 0M18 7l3 9m-3-9l-6-2m0-2v2m0 16V5m0 16H9m3 0h3"></path></svg>
                        <span class="tracking-wider uppercase text-xs">Claims & Recovery</span>
                    </div>
                    <span class="text-[9px] bg-violet-950 text-violet-400 px-1.5 py-0.5 rounded font-black border border-violet-900 uppercase">SYS_AI</span>
                </button>
                <button onclick="switchTab('hmrc')" id="nav-hmrc" class="w-full flex items-center justify-between px-4 py-3 text-sm font-semibold rounded-xl text-zinc-400 hover:bg-zinc-900 hover:text-white transition-all duration-150">
                    <div class="flex items-center space-x-3">
                        <svg class="w-5 h-5 text-zinc-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path></svg>
                        <span class="tracking-wider uppercase text-xs">HMRC & Career</span>
                    </div>
                    <span class="text-[9px] bg-violet-950 text-violet-400 px-1.5 py-0.5 rounded font-black border border-violet-900 uppercase">SYS_AI</span>
                </button>
                <button onclick="switchTab('checklists')" id="nav-checklists" class="w-full flex items-center justify-between px-4 py-3 text-sm font-semibold rounded-xl text-zinc-400 hover:bg-zinc-900 hover:text-white transition-all duration-150">
                    <div class="flex items-center space-x-3">
                        <svg class="w-5 h-5 text-zinc-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"></path></svg>
                        <span class="tracking-wider uppercase text-xs">Quest Logs</span>
                    </div>
                    <span class="text-[9px] bg-violet-950 text-violet-400 px-1.5 py-0.5 rounded font-black border border-violet-900 uppercase">SYS_AI</span>
                </button>
            </nav>
        </aside>

        <!-- Main Workspace Area -->
        <main class="flex-grow bg-zinc-950/80 border border-purple-950/40 rounded-2xl p-6 sm:p-8 backdrop-blur shadow-2xl relative overflow-hidden">
            <!-- Neon background visual grids -->
            <div class="absolute inset-0 bg-grid opacity-[0.02] pointer-events-none"></div>

            <!-- SECTION 1: STRATEGIC ROADMAP -->
            <section id="tab-content-roadmap" class="space-y-8">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 border-b border-purple-950/50 pb-4">
                    <div>
                        <h2 class="text-2xl font-black text-white tracking-wider uppercase sm:text-3xl flex items-center gap-2">
                            <span>[ Master Quest Matrix ]</span>
                        </h2>
                        <p class="mt-2 text-zinc-400 font-mono text-xs">THE COMPREHENSIVE PATHWAY TO METAMORPHOSIS</p>
                    </div>
                    <span class="self-start md:self-center bg-purple-950/60 text-violet-300 text-xs font-mono font-semibold px-3 py-1.5 rounded-full border border-purple-800 flex items-center gap-1.5 shadow-sm shadow-violet-500/10">
                        <span class="w-2 h-2 rounded-full bg-violet-400 orb-pulse"></span>
                        PLANNER MODULE ACTIVE
                    </span>
                </div>

                <div class="overflow-x-auto rounded-xl border border-purple-950/50">
                    <table class="w-full text-left border-collapse bg-zinc-950/50">
                        <thead>
                            <tr class="border-b border-purple-950/60 bg-zinc-950 text-xs font-bold uppercase tracking-widest text-violet-300 font-mono">
                                <th class="p-4">Active Sector</th>
                                <th class="p-4">Tactical Directive</th>
                                <th class="p-4">System Timeframe</th>
                                <th class="p-4">Core Catalyst</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-purple-950/40 text-sm">
                            <tr class="hover:bg-purple-950/10 transition-all">
                                <td class="p-4 font-medium text-white">
                                    <div class="flex items-center space-x-3">
                                        <div class="w-2.5 h-2.5 rounded-full bg-red-500"></div>
                                        <div>
                                            <p class="font-bold tracking-wider">ENVIRONMENT RECLAMATION</p>
                                            <span class="text-[10px] text-zinc-500 font-mono font-normal">Mice, laundry backup, deep bedroom declutter</span>
                                        </div>
                                    </div>
                                </td>
                                <td class="p-4 text-zinc-300 text-xs">
                                    Execute the <span class="text-violet-400 font-bold">Three-Pile Laundry System</span>. Enforce Zero-Food Isolation. Seal skirting boards & perform damp-sweeps to completely secure the sanctum.
                                </td>
                                <td class="p-4 font-mono text-zinc-400 text-xs">
                                    <p class="text-red-400 font-bold">First 48 Hours</p>
                                    <span>Then 1 load/day</span>
                                </td>
                                <td class="p-4 text-xs text-zinc-500 font-mono">Disinfectant, wire mesh, 60°C laundry.</td>
                            </tr>

                            <tr class="hover:bg-purple-950/10 transition-all">
                                <td class="p-4 font-medium text-white">
                                    <div class="flex items-center space-x-3">
                                        <div class="w-2.5 h-2.5 rounded-full bg-orange-500"></div>
                                        <div>
                                            <p class="font-bold tracking-wider">PHYSIQUE & VISION SYNC</p>
                                            <span class="text-[10px] text-zinc-500 font-mono font-normal">Critical extraction & custom lens calibration</span>
                                        </div>
                                    </div>
                                </td>
                                <td class="p-4 text-zinc-300 text-xs">
                                    Finalise dental clinical booking to extract affected tooth. Secure comprehensive 1-hour professional eye test to renew high-spec screen lenses.
                                </td>
                                <td class="p-4 font-mono text-zinc-400 text-xs">
                                    <p class="text-orange-400 font-bold">Weeks 1 - 3</p>
                                    <span>3-5 days recovery</span>
                                </td>
                                <td class="p-4 text-xs text-zinc-500 font-mono">Appointment booking, surgical funding (£100-£600).</td>
                            </tr>

                            <tr class="hover:bg-purple-950/10 transition-all">
                                <td class="p-4 font-medium text-white">
                                    <div class="flex items-center space-x-3">
                                        <div class="w-2.5 h-2.5 rounded-full bg-yellow-500"></div>
                                        <div>
                                            <p class="font-bold tracking-wider">FINANCIAL AWAKENING</p>
                                            <span class="text-[10px] text-zinc-500 font-mono font-normal">MacBook, tv, ergonomic hub, summer trip</span>
                                        </div>
                                    </div>
                                </td>
                                <td class="p-4 text-zinc-300 text-xs">
                                    Unlock capital streams via PIP assessment tracking, HMRC job placements, and small claims extraction (£110 Caps).
                                </td>
                                <td class="p-4 font-mono text-zinc-400 text-xs">
                                    <p class="text-yellow-400 font-bold">Months 1 - 6</p>
                                    <span>Weekly tracking</span>
                                </td>
                                <td class="p-4 text-xs text-zinc-500 font-mono">DWP reviews, active pre-action court filings.</td>
                            </tr>

                            <tr class="hover:bg-purple-950/10 transition-all">
                                <td class="p-4 font-medium text-white">
                                    <div class="flex items-center space-x-3">
                                        <div class="w-2.5 h-2.5 rounded-full bg-emerald-500"></div>
                                        <div>
                                            <p class="font-bold tracking-wider">TRANSIT MOBILITY</p>
                                            <span class="text-[10px] text-zinc-500 font-mono font-normal">No physical driver's license, transit delays</span>
                                        </div>
                                    </div>
                                </td>
                                <td class="p-4 text-zinc-300 text-xs">
                                    Initiate intensive driving course. Target theory exam immediately to clear the threshold for active practical testing.
                                </td>
                                <td class="p-4 font-mono text-zinc-400 text-xs">
                                    <p class="text-emerald-400 font-bold">Months 2 - 6</p>
                                    <span>2 hours weekly</span>
                                </td>
                                <td class="p-4 text-xs text-zinc-500 font-mono">Driving theory application, booking slots.</td>
                            </tr>

                            <tr class="hover:bg-purple-950/10 transition-all">
                                <td class="p-4 font-medium text-white">
                                    <div class="flex items-center space-x-3">
                                        <div class="w-2.5 h-2.5 rounded-full bg-violet-500"></div>
                                        <div>
                                            <p class="font-bold tracking-wider">OUTDOOR HORIZON</p>
                                            <span class="text-[10px] text-zinc-500 font-mono font-normal">Social withdrawal, severe house containment</span>
                                        </div>
                                    </div>
                                </td>
                                <td class="p-4 text-zinc-300 text-xs">
                                    Quarantine £1,500-£2,000 in dedicated digital savings vault. Secure bookings during optimal windows for international travel rest.
                                </td>
                                <td class="p-4 font-mono text-zinc-400 text-xs">
                                    <p class="text-violet-400 font-bold">Summer 2027</p>
                                    <span>10-14 days off</span>
                                </td>
                                <td class="p-4 text-xs text-zinc-500 font-mono">Completion of core environmental & income phases.</td>
                            </tr>
                        </tbody>
                    </table>
                </div>

                <!-- AI Savings and Holiday Planner -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/60 space-y-4 shadow-xl">
                    <div class="flex items-center space-x-2">
                        <span class="text-2xl">✨</span>
                        <h3 class="text-lg font-bold text-white tracking-wider uppercase">RinneRebirth: Savings & Holiday Planner</h3>
                    </div>
                    <p class="text-sm text-zinc-400">Map out how to fund your resurrection. Input your target savings goals and current approximate monthly allowance, and the System will compute your saving trajectory and major milestones.</p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Your Monthly Available Income/Allowance (£)</label>
                            <input type="number" id="ai-savings-income" placeholder="e.g. 800" class="w-full bg-zinc-900 border border-purple-950/50 rounded-lg p-2 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Target Asset Focus</label>
                            <select id="ai-savings-priority" class="w-full bg-zinc-900 border border-purple-950/50 rounded-lg p-2.5 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                                <option value="MacBook and Summer Holiday 2027">MacBook (£1100) + Holiday (£1500)</option>
                                <option value="Summer Holiday 2027 Only">Summer Holiday 2027 (£1500)</option>
                                <option value="MacBook, TV and Chair Only">MacBook, TV & Ergonomic Chair (£1850)</option>
                            </select>
                        </div>
                    </div>
                    <div class="flex justify-end">
                        <button onclick="generateAISavingsPlan()" id="ai-savings-btn" class="bg-violet-900 hover:bg-violet-800 text-white font-bold py-2.5 px-5 rounded-lg text-xs tracking-wider uppercase transition-all flex items-center space-x-2 shadow-lg shadow-violet-900/30 border border-violet-500/40">
                            <span id="savings-btn-loader" class="hidden animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent"></span>
                            <span>✨ Calibrate Savings</span>
                        </button>
                    </div>

                    <!-- AI Savings Output -->
                    <div id="ai-savings-output-container" class="hidden space-y-2 pt-2">
                        <label class="block text-xs font-semibold uppercase text-zinc-500 font-mono">System Calculation Timeline Output</label>
                        <textarea id="ai-savings-output-box" class="w-full h-48 bg-zinc-900 border border-purple-950/40 rounded-lg p-3 font-mono text-xs text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500 custom-scrollbar" readonly></textarea>
                    </div>
                </div>
            </section>

            <!-- SECTION 2: PIP CLAIM HUB -->
            <section id="tab-content-pip" class="space-y-8 hidden">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 border-b border-purple-950/50 pb-4">
                    <div>
                        <h2 class="text-2xl font-black text-white tracking-wider uppercase sm:text-3xl flex items-center gap-2">
                            <span>[ PIP Claims Matrix ]</span>
                        </h2>
                        <p class="mt-2 text-zinc-400 font-mono text-xs">STRATEGY FOR SECURING CRITICAL PERSONAL INDEPENDENCE ASSISTANCE</p>
                    </div>
                    <span class="self-start md:self-center bg-purple-950/60 text-violet-300 text-xs font-mono font-semibold px-3 py-1.5 rounded-full border border-purple-800 flex items-center gap-1.5 shadow-sm shadow-violet-500/10">
                        <span class="w-2 h-2 rounded-full bg-violet-400 orb-pulse"></span>
                        AI Personalization Enabled
                    </span>
                </div>

                <!-- PIP Descriptors Explanation -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="p-5 rounded-xl bg-zinc-950 border border-purple-950/40">
                        <h3 class="text-base font-bold text-white uppercase tracking-wider flex items-center mb-3">
                            <span class="w-6 h-6 rounded-full bg-purple-950/80 border border-purple-800 text-violet-400 flex items-center justify-center text-xs mr-2">1</span>
                            Daily Living Component
                        </h3>
                        <p class="text-zinc-400 text-xs mb-4">Focuses on how your physical/mental state impacts everyday chores. Your claims are measured by how well you can complete these reliably, safely, in a timely manner, and repeatedly.</p>
                        <ul class="text-xs space-y-2 text-zinc-300 font-mono">
                            <li>• Preparing and cooking food</li>
                            <li>• Washing and bathing</li>
                            <li>• Managing toilet needs or incontinence</li>
                            <li>• Dressing and undressing</li>
                            <li>• Communicating and reading</li>
                        </ul>
                    </div>

                    <div class="p-5 rounded-xl bg-zinc-950 border border-purple-950/40">
                        <h3 class="text-base font-bold text-white uppercase tracking-wider flex items-center mb-3">
                            <span class="w-6 h-6 rounded-full bg-purple-950/80 border border-purple-800 text-violet-400 flex items-center justify-center text-xs mr-2">2</span>
                            Mobility Component
                        </h3>
                        <p class="text-zinc-400 text-xs mb-4">Focuses on how you manage moving outside the house and planning/following journeys, especially when facing social anxiety, panic, or physical impairment.</p>
                        <ul class="text-xs space-y-2 text-zinc-300 font-mono">
                            <li>• Planning and following a journey route</li>
                            <li>• Navigating social settings safely</li>
                            <li>• Walking distance limits without assistance</li>
                            <li>• Overcoming mental/physical fatigue</li>
                        </ul>
                    </div>
                </div>

                <!-- AI Prompt Box for customized PIP Generator -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/60 space-y-4 shadow-xl">
                    <div class="flex items-center space-x-2">
                        <span class="text-2xl">✨</span>
                        <h3 class="text-lg font-bold text-white tracking-wider uppercase">AI PIP Personal Statement Builder</h3>
                    </div>
                    <p class="text-sm text-zinc-400">Provide specific details about your medical conditions or psychological traits (e.g. chronic dental pain, sensory overwhelm, severe social anxiety, bedroom clutter anxiety) to generate a customized personal statement structured for the DWP.</p>
                    
                    <div class="space-y-3">
                        <textarea id="ai-pip-input" placeholder="Type key symptoms or difficulties here (e.g., 'Severe social anxiety prevents leaving the house, and chronic dental decay prevents eating solid foods...')" class="w-full h-24 bg-zinc-900 border border-purple-950/40 rounded-lg p-3 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500 custom-scrollbar"></textarea>
                        <div class="flex justify-end">
                            <button onclick="generateAIPipStatement()" id="ai-pip-btn" class="bg-violet-900 hover:bg-violet-800 text-white font-bold py-2.5 px-5 rounded-lg text-xs tracking-wider uppercase transition-all flex items-center space-x-2 shadow-lg shadow-violet-900/30 border border-violet-500/40">
                                <span id="pip-btn-loader" class="hidden animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent"></span>
                                <span>✨ Assemble Statement</span>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Interactive PIP Diary & Statement Draft -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/40 space-y-6">
                    <div>
                        <h3 class="text-base font-bold text-white uppercase tracking-wider">Statement Workspace</h3>
                        <p class="text-xs text-zinc-500 mt-1">Edit or expand your statement here. This matches standard DWP scoring structures.</p>
                    </div>

                    <div class="relative">
                        <textarea id="pip-template-box" class="w-full h-80 bg-zinc-900 border border-purple-950/30 rounded-lg p-4 font-mono text-xs text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500 custom-scrollbar">
STATEMENT OF APPLICANT REGARDING DAILY LIVING AND MOBILITY

To the DWP Decision Maker:

This statement supplements my PIP claim form, illustrating how my health conditions (which impact my physical, dental, visual, and environmental capabilities) affect my daily lifestyle.

1. PREPARING FOOD & MEAL ROUTINE:
My health conditions directly impact my energy level and my ability to safely navigate my kitchen space. On bad days, preparing raw ingredients triggers significant physical and mental fatigue. This has previously caused neglect of my immediate nutrition and environment. 

2. SANITATION AND MANAGING HOUSEHOLD TASKS:
My standard of living has deteriorated to a stage that requires major decontamination. The energy consumed dealing with systemic domestic environments makes keeping laundry, bedding sanitization, and basic kitchen hygiene exceptionally challenging. Stripping, washing, and remaking bed linen demands physical endurance that I cannot sustain regularly without extreme exertion.

3. MOBILITY & SOCIAL ISOLATION:
I stay indoors. I am currently unable to entertain company due to an acute combination of domestic stress, house pest infestations, and social isolation. Planning or embarking on unfamiliar outdoor journeys is overwhelmingly stressful without assistance or structured physical planning.

CONCLUSION:
I am currently working to systematically rebuild my living standards, dental health, and vision, but these limitations are present on more than 50% of days.

I request that these factors be heavily considered during the scoring of descriptors.
                        </textarea>
                        <button onclick="copyText('pip-template-box', 'copy-pip-btn')" id="copy-pip-btn" class="absolute bottom-4 right-4 bg-zinc-800 hover:bg-zinc-700 text-white px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center space-x-1 border border-zinc-700">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2v2M9 16h.01"></path></svg>
                            <span>Copy Statement</span>
                        </button>
                    </div>
                </div>
            </section>

            <!-- SECTION 3: SMALL CLAIMS COURT HUB -->
            <section id="tab-content-smallclaims" class="space-y-8 hidden">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 border-b border-purple-950/50 pb-4">
                    <div>
                        <h2 class="text-2xl font-black text-white tracking-wider uppercase sm:text-3xl flex items-center gap-2">
                            <span>[ Debt Extraction Tribunal ]</span>
                        </h2>
                        <p class="mt-2 text-zinc-400 font-mono text-xs">OFFICIAL TRACK TO RECOVER £110 FOR UNFULFILLED COMMISSIONS</p>
                    </div>
                    <span class="self-start md:self-center bg-purple-950/60 text-violet-300 text-xs font-mono font-semibold px-3 py-1.5 rounded-full border border-purple-800 flex items-center gap-1.5 shadow-sm shadow-violet-500/10">
                        <span class="w-2 h-2 rounded-full bg-violet-400 orb-pulse"></span>
                        AI Personalization Enabled
                    </span>
                </div>

                <!-- 3 Step Small Claims Flow -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 font-mono text-xs">
                    <div class="p-5 rounded-xl bg-zinc-950 border border-purple-950/40">
                        <div class="w-8 h-8 rounded-full bg-purple-950/80 border border-purple-800 text-violet-400 flex items-center justify-center text-sm font-bold mb-3">1</div>
                        <h4 class="font-bold text-white uppercase tracking-wider">Letter Before Claim</h4>
                        <p class="text-zinc-400 mt-2 leading-relaxed">Issue a formal notice explaining exactly what is owed. Set a strict 14 calendar-day timeline to prevent direct legal litigation.</p>
                    </div>

                    <div class="p-5 rounded-xl bg-zinc-950 border border-purple-950/40">
                        <div class="w-8 h-8 rounded-full bg-purple-950/80 border border-purple-800 text-violet-400 flex items-center justify-center text-sm font-bold mb-3">2</div>
                        <h4 class="font-bold text-white uppercase tracking-wider">MCOL UK Filing</h4>
                        <p class="text-zinc-400 mt-2 leading-relaxed">If ignored, file officially via Money Claim Online. Small administrative fee applies (~£35), added directly to their debt if you win.</p>
                    </div>

                    <div class="p-5 rounded-xl bg-zinc-950 border border-purple-950/40">
                        <div class="w-8 h-8 rounded-full bg-purple-950/80 border border-purple-800 text-violet-400 flex items-center justify-center text-sm font-bold mb-3">3</div>
                        <h4 class="font-bold text-white uppercase tracking-wider">Judgment Recovery</h4>
                        <p class="text-zinc-400 mt-2 leading-relaxed">Target has 14 days to respond. If silent, summon a default County Court Judgment (CCJ) for the full £110 + costs.</p>
                    </div>
                </div>

                <!-- AI Prompt Box for Customized Claims Letter -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/60 space-y-4 shadow-xl">
                    <div class="flex items-center space-x-2">
                        <span class="text-2xl">✨</span>
                        <h3 class="text-lg font-bold text-white tracking-wider uppercase">AI Letter Customizer</h3>
                    </div>
                    <p class="text-sm text-zinc-400">Input transaction details, vendor/manufacturer name, purchase dates, and exact issue (e.g. "Unfulfilled embroidered hats") to build a professional pre-action protocol document.</p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Counterparty/Company Name</label>
                            <input type="text" id="ai-court-vendor" placeholder="e.g. CapCorp Customs" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Issue Details</label>
                            <input type="text" id="ai-court-issue" placeholder="e.g. Non-delivery of 12 black embroidered caps" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                        </div>
                    </div>
                    <div class="flex justify-end">
                        <button onclick="generateAICourtLetter()" id="ai-court-btn" class="bg-violet-900 hover:bg-violet-800 text-white font-bold py-2.5 px-5 rounded-lg text-xs tracking-wider uppercase transition-all flex items-center space-x-2 shadow-lg shadow-violet-900/30 border border-violet-500/40">
                            <span id="court-btn-loader" class="hidden animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent"></span>
                            <span>✨ Calibrate Legal Letter</span>
                        </button>
                    </div>
                </div>

                <!-- Draft Template Letter -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/40 space-y-6">
                    <div>
                        <h3 class="text-base font-bold text-white uppercase tracking-wider">Letter Workspace</h3>
                        <p class="text-xs text-zinc-500 mt-1">Copy, edit, and send this letter via Registered Post/Email to the seller or counterparty to formally begin the legal cycle.</p>
                    </div>

                    <div class="relative">
                        <textarea id="court-template-box" class="w-full h-80 bg-zinc-900 border border-purple-950/30 rounded-lg p-4 font-mono text-xs text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500 custom-scrollbar">
[Your Full Name]
[Your Address]
[Your Phone Number]
[Your Email]

[Date]

[Recipient / Business Name]
[Recipient Address]

LETTER BEFORE ACTION / RECORD OF CLAIM

Dear [Recipient Name/Representative],

RE: Unpaid Refund of Capital / Outstanding Sum of £110.00 for Caps

I am writing in reference to the unpaid amount of £110.00 representing outstanding funds/merchandise (caps) purchased/contracted but not delivered in acceptable/useable condition. 

Despite multiple attempts to resolve this issue amicably outside of formal settings, the total sum of £110.00 remains unpaid.

Please take this as formal notice under the Practice Direction for Pre-Action Conduct. If payment is not received or a suitable repayment schedule is not proposed in writing within 14 days of the date of this letter, I intend to commence legal proceedings in the County Court to recover the full balance of £110.00.

I will also seek to recover the court filing fees, statutory interest at 8% per annum pursuant to Section 69 of the County Courts Act 1984, and any other associated court administration costs.

I hope this action will prove unnecessary and that you will remit the outstanding sum of £110.00 immediately. Please contact me directly using the details provided above to organize payment.

Yours sincerely,

[Your Full Signature]
                        </textarea>
                        <button onclick="copyText('court-template-box', 'copy-court-btn')" id="copy-court-btn" class="absolute bottom-4 right-4 bg-zinc-800 hover:bg-zinc-700 text-white px-3 py-1.5 rounded-lg text-xs font-semibold transition-all flex items-center space-x-1 border border-zinc-700">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2v2M9 16h.01"></path></svg>
                            <span>Copy Letter</span>
                        </button>
                    </div>
                </div>
            </section>

            <!-- SECTION 4: HMRC & JOB STRATEGY -->
            <section id="tab-content-hmrc" class="space-y-8 hidden">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 border-b border-purple-950/50 pb-4">
                    <div>
                        <h2 class="text-2xl font-black text-white tracking-wider uppercase sm:text-3xl flex items-center gap-2">
                            <span>[ HMRC & Job Guild Portal ]</span>
                        </h2>
                        <p class="mt-2 text-zinc-400 font-mono text-xs">MONITOR REVENUE PORTALS, TAX CODES, AND ACTIVE EMPLOYMENT SEARCHES</p>
                    </div>
                    <span class="self-start md:self-center bg-purple-950/60 text-violet-300 text-xs font-mono font-semibold px-3 py-1.5 rounded-full border border-purple-800 flex items-center gap-1.5 shadow-sm shadow-violet-500/10">
                        <span class="w-2 h-2 rounded-full bg-violet-400 orb-pulse"></span>
                        AI Personalization Enabled
                    </span>
                </div>

                <!-- Admin Action Plan -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="p-5 rounded-xl bg-zinc-950 border border-purple-950/40">
                        <h3 class="text-base font-bold text-white uppercase tracking-wider flex items-center mb-3">
                            <svg class="w-5 h-5 text-violet-400 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path></svg>
                            Government Tax Portal Prep
                        </h3>
                        <p class="text-zinc-400 text-xs mb-4">Set up your Personal Tax Account to monitor incoming funds, claims, and self-employment or PAYE history.</p>
                        <ul class="text-xs space-y-2 text-zinc-300 font-mono">
                            <li><strong>1. Register Government Gateway ID:</strong> Secure your physical activation letter.</li>
                            <li><strong>2. Match with National Insurance (NI) Number:</strong> Keep document files organized.</li>
                            <li><strong>3. Claim History Tracking:</strong> View any overpaid taxes from previous work.</li>
                        </ul>
                    </div>

                    <div class="p-5 rounded-xl bg-zinc-950 border border-purple-950/40">
                        <h3 class="text-base font-bold text-white uppercase tracking-wider flex items-center mb-3">
                            <svg class="w-5 h-5 text-violet-400 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 4a2 2 0 11-4 0v-4h4v4z"></path></svg>
                            Modern Tech Resume Structure
                        </h3>
                        <p class="text-zinc-400 text-xs mb-4">A simple structure tailored for modern entry-level and intermediate office or administrative roles.</p>
                        <ul class="text-xs space-y-2 text-zinc-300 font-mono">
                            <li><strong>Header:</strong> Name, professional email, phone number, LinkedIn.</li>
                            <li><strong>Profile Summary:</strong> Highlight self-motivation, high accountability, and operational skills.</li>
                            <li><strong>Key Expertise:</strong> Microsoft Office, spreadsheet work, logistics, inventory.</li>
                        </ul>
                    </div>
                </div>

                <!-- AI Resume Optimizer Prompt Section -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/60 space-y-4 shadow-xl">
                    <div class="flex items-center space-x-2">
                        <span class="text-2xl">✨</span>
                        <h3 class="text-lg font-bold text-white tracking-wider uppercase">AI Resume Summary Optimizer</h3>
                    </div>
                    <p class="text-sm text-zinc-400">Input your targeted job title and preferred professional skills, and the System will craft an engaging, high-impact Profile Summary for the top of your CV.</p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Target Job Title</label>
                            <input type="text" id="ai-job-title" placeholder="e.g. Operations Assistant, Customer Advisor" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Key Strengths or Experiences</label>
                            <input type="text" id="ai-job-skills" placeholder="e.g. highly structured, great attention to detail, inventory control" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                        </div>
                    </div>
                    <div class="flex justify-end">
                        <button onclick="generateAIResumeSummary()" id="ai-job-btn" class="bg-violet-900 hover:bg-violet-800 text-white font-bold py-2.5 px-5 rounded-lg text-xs tracking-wider uppercase transition-all flex items-center space-x-2 shadow-lg shadow-violet-900/30 border border-violet-500/40">
                            <span id="job-btn-loader" class="hidden animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent"></span>
                            <span>✨ Optimize Resume</span>
                        </button>
                    </div>

                    <!-- AI Optimized Output Field -->
                    <div id="ai-resume-output-container" class="hidden space-y-2 pt-2">
                        <label class="block text-xs font-semibold uppercase text-zinc-500 font-mono">Optimized Output Statement</label>
                        <div class="relative">
                            <textarea id="ai-resume-output-box" class="w-full h-32 bg-zinc-900 border border-purple-950/30 rounded-lg p-3 font-mono text-xs text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500 custom-scrollbar"></textarea>
                            <button onclick="copyText('ai-resume-output-box', 'copy-resume-btn')" id="copy-resume-btn" class="absolute bottom-3 right-3 bg-violet-950 hover:bg-violet-850 text-white px-2.5 py-1.5 rounded-lg text-xs font-semibold transition-all border border-violet-800">Copy Statement</button>
                        </div>
                    </div>
                </div>

                <!-- AI Social Recharge Reconnect System -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/60 space-y-4 shadow-xl">
                    <div class="flex items-center space-x-2">
                        <span class="text-2xl">🤝</span>
                        <h3 class="text-lg font-bold text-white tracking-wider uppercase">AI Social Recharge Assistant</h3>
                    </div>
                    <p class="text-sm text-zinc-400 font-medium">Having a messy room or house issues often leads us to isolate ourselves. Reconnecting can feel stressful. Generate a low-anxiety text draft to easily reconnect with loved ones or friends.</p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Target Contact</label>
                            <select id="ai-reconnect-person" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                                <option value="Cuzzy (Cousin)">Cuzzy (Cousin)</option>
                                <option value="A close friend">Close Friend</option>
                                <option value="My Mum/Family Member">Family Member</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Tone Preference</label>
                            <select id="ai-reconnect-tone" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                                <option value="Casual & Low Key (just saying hi)">Casual & Low Key (Just saying hi)</option>
                                <option value="Explaining you've been busy/recovering">Explaining you've been busy & distant</option>
                                <option value="Inviting them to catch up outside the house">Inviting to meet outside</option>
                            </select>
                        </div>
                    </div>
                    <div class="flex justify-end">
                        <button onclick="generateAIReconnectText()" id="ai-reconnect-btn" class="bg-violet-900 hover:bg-violet-800 text-white font-bold py-2.5 px-5 rounded-lg text-xs tracking-wider uppercase transition-all flex items-center space-x-2 shadow-lg shadow-violet-900/30 border border-violet-500/40">
                            <span id="reconnect-btn-loader" class="hidden animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent"></span>
                            <span>✨ Draft Message</span>
                        </button>
                    </div>

                    <!-- AI Reconnect Output -->
                    <div id="ai-reconnect-output-container" class="hidden space-y-2 pt-2">
                        <label class="block text-xs font-semibold uppercase text-zinc-500 font-mono">Generated Message (Copy and Send)</label>
                        <div class="relative">
                            <textarea id="ai-reconnect-output-box" class="w-full h-24 bg-zinc-900 border border-purple-950/30 rounded-lg p-3 font-mono text-xs text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500 custom-scrollbar" readonly></textarea>
                            <button onclick="copyText('ai-reconnect-output-box', 'copy-reconnect-btn')" id="copy-reconnect-btn" class="absolute bottom-3 right-3 bg-violet-950 hover:bg-violet-850 text-white px-2.5 py-1.5 rounded-lg text-xs font-semibold transition-all border border-violet-800">Copy Text</button>
                        </div>
                    </div>
                </div>

                <!-- Job Application Tracker Tool -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/40 space-y-4 shadow-xl">
                    <h3 class="text-base font-bold text-white uppercase tracking-wider">Application Tracker</h3>
                    <p class="text-xs text-zinc-400">Keep a close record of your job applications below to follow up regularly with recruiters.</p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-4 gap-3">
                        <input type="text" id="track-comp" placeholder="Company Name" class="bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:ring-1 focus:ring-violet-500">
                        <input type="text" id="track-role" placeholder="Role (e.g. Admin Assistant)" class="bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:ring-1 focus:ring-violet-500">
                        <input type="text" id="track-status" placeholder="Status (e.g. Applied, Interviewing)" class="bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:ring-1 focus:ring-violet-500">
                        <button onclick="addTrackRecord()" class="bg-zinc-800 hover:bg-zinc-700 text-white border border-zinc-700 font-semibold py-2.5 px-4 rounded-lg text-xs tracking-wider uppercase transition-all">Add Track Record</button>
                    </div>

                    <div class="overflow-x-auto mt-4 rounded-lg border border-purple-950/40">
                        <table class="w-full text-left text-sm" id="tracker-table">
                            <thead class="bg-zinc-950 text-xs text-zinc-300 uppercase font-semibold font-mono">
                                <tr>
                                    <th class="p-3">Company</th>
                                    <th class="p-3">Role</th>
                                    <th class="p-3">Status</th>
                                    <th class="p-3 text-right">Action</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-purple-950/30">
                                <tr class="hover:bg-purple-950/10">
                                    <td class="p-3 font-medium text-white">Apple Retail</td>
                                    <td class="p-3 text-zinc-300">Operations Specialist</td>
                                    <td class="p-3"><span class="px-2 py-0.5 rounded text-xs bg-violet-950 text-violet-400 border border-violet-850">Interview Scheduled</span></td>
                                    <td class="p-3 text-right"><button onclick="deleteTrackerRow(this)" class="text-red-400 hover:text-red-300 text-xs font-mono uppercase">Delete</button></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- SECTION 5: HEALTH & ACTION LISTS -->
            <section id="tab-content-checklists" class="space-y-8 hidden">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 border-b border-purple-950/50 pb-4">
                    <div>
                        <h2 class="text-2xl font-black text-white tracking-wider uppercase sm:text-3xl flex items-center gap-2">
                            <span>[ Master Quest Logs ]</span>
                        </h2>
                        <p class="mt-2 text-zinc-400 font-mono text-xs">PRACTICAL DIRECTIVES TO PURGE CLUTTER AND SECURE PHYSICAL HEALTH</p>
                    </div>
                    <span class="self-start md:self-center bg-purple-950/60 text-violet-300 text-xs font-mono font-semibold px-3 py-1.5 rounded-full border border-purple-800 flex items-center gap-1.5 shadow-sm shadow-violet-500/10">
                        <span class="w-2 h-2 rounded-full bg-violet-400 orb-pulse"></span>
                        AI Personalization Enabled
                    </span>
                </div>

                <!-- AI Task Decomposer Interface -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/60 space-y-4 shadow-xl">
                    <div class="flex items-center space-x-2">
                        <span class="text-2xl">✨</span>
                        <h3 class="text-lg font-bold text-white tracking-wider uppercase">AI Task Decomposer (Anti-Overwhelm Plan)</h3>
                    </div>
                    <p class="text-sm text-zinc-400">If any chore or task feels too big or causes anxiety (e.g. "cleaning the mouse-infested corner", "getting a painful tooth pulled", "sorting laundry backlog"), type it below. Gemini will break it down into tiny, actionable subtasks.</p>
                    
                    <div class="space-y-3">
                        <input type="text" id="ai-task-input" placeholder="Type a big, stressful task (e.g. 'Cleaning the dusty floor corner safely')" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                        <div class="flex justify-end">
                            <button onclick="decomposeTaskWithAI()" id="ai-task-btn" class="bg-violet-900 hover:bg-violet-800 text-white font-bold py-2.5 px-5 rounded-lg text-xs tracking-wider uppercase transition-all flex items-center space-x-2 shadow-lg shadow-violet-900/30 border border-violet-500/40">
                                <span id="task-btn-loader" class="hidden animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent"></span>
                                <span>✨ Extract Micro-Steps</span>
                            </button>
                        </div>
                    </div>

                    <!-- AI Task Output -->
                    <div id="ai-task-output-container" class="hidden space-y-3 pt-3 border-t border-purple-950/40">
                        <h4 class="text-sm font-bold text-white uppercase tracking-wider text-violet-400 font-mono">Micro-Task Steps Extracted:</h4>
                        <div id="ai-task-steps" class="space-y-2 bg-zinc-900 p-4 rounded-lg border border-purple-950/30 text-sm text-zinc-300 leading-relaxed">
                            <!-- Dynamic Content Here -->
                        </div>
                    </div>
                </div>

                <!-- AI Room Rescuer & Clean Coach -->
                <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/60 space-y-4 shadow-xl">
                    <div class="flex items-center space-x-2">
                        <span class="text-2xl">🧹</span>
                        <h3 class="text-lg font-bold text-white tracking-wider uppercase">AI Room Rescuer & Clean Coach</h3>
                    </div>
                    <p class="text-sm text-zinc-400 font-medium">Let's make cleaning fun and customized to your exact energy capacity today. Select your current energy level and the exact mess target, and Gemini will build a step-by-step gameplan.</p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Your Energy Level right now</label>
                            <select id="ai-coach-energy" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                                <option value="Low & Tired (just want small progress)">Low & Tired (Tiny wins)</option>
                                <option value="Medium (can do 20-30 mins of work)">Medium (Focused blocks)</option>
                                <option value="High (ready to attack the mess)">High (Massive decluttering)</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold uppercase text-zinc-500 mb-1">Mess Target Area</label>
                            <select id="ai-coach-target" class="w-full bg-zinc-900 border border-purple-950/40 rounded-lg p-2.5 text-sm text-zinc-300 focus:outline-none focus:ring-1 focus:ring-violet-500">
                                <option value="Laundry mountain and bedding setup">Laundry Pile & Bed Reset</option>
                                <option value="Dusty baseboards and pest mitigation routes">Baseboards & Pest Prevention</option>
                                <option value="The desk surfaces and surrounding floor junk">Desk Workspace & Floor Trash</option>
                            </select>
                        </div>
                    </div>
                    <div class="flex justify-end">
                        <button onclick="generateAICleaningPlan()" id="ai-coach-btn" class="bg-violet-900 hover:bg-violet-800 text-white font-bold py-2.5 px-5 rounded-lg text-xs tracking-wider uppercase transition-all flex items-center space-x-2 shadow-lg shadow-violet-900/30 border border-violet-500/40">
                            <span id="coach-btn-loader" class="hidden animate-spin rounded-full h-4 w-4 border-2 border-white border-t-transparent"></span>
                            <span>✨ Summon Clean Coach</span>
                        </button>
                    </div>

                    <!-- AI Clean Coach Output -->
                    <div id="ai-coach-output-container" class="hidden space-y-2 pt-2">
                        <label class="block text-xs font-semibold uppercase text-zinc-500 font-mono">Custom Strategy Output</label>
                        <div id="ai-coach-output-box" class="w-full bg-zinc-900 border border-purple-950/30 rounded-lg p-4 text-sm text-zinc-300 leading-relaxed custom-scrollbar max-h-80 overflow-y-auto"></div>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Environment and Decontamination Checklist -->
                    <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/40 space-y-4">
                        <h3 class="text-lg font-bold text-white uppercase tracking-wider flex items-center">
                            <svg class="w-5 h-5 text-red-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
                            Sanitation & Deep Clean (First 48h)
                        </h3>
                        <p class="text-xs text-zinc-500 font-mono">[ PRIORITY DIRECTIVES ]</p>
                        
                        <div class="space-y-3" id="env-checklist-container">
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>Safe Spray Down:</strong> Dampen any dust or dry mouse droppings with disinfectant/bleach spray first. <strong>Do not vacuum dry droppings</strong> to avoid breathing in dust.</span>
                            </label>
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>Zero-Food Quarantine:</strong> Remove all plates, glasses, and food packaging completely. Wash them with hot water and dish soap, keeping food out of the room going forward.</span>
                            </label>
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>High-Heat Bedding Cycle:</strong> Strip your bed sheets and duvet covers. Wash them immediately at 60°C to destroy any bugs or bacteria.</span>
                            </label>
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>Baseboard Seal:</strong> Find entry points near floorboards or piping. Block them securely with wire mesh or caulk.</span>
                            </label>
                        </div>
                    </div>

                    <!-- Dental & Vision Checklist -->
                    <div class="p-6 rounded-xl bg-zinc-950 border border-purple-950/40 space-y-4">
                        <h3 class="text-lg font-bold text-white uppercase tracking-wider flex items-center">
                            <svg class="w-5 h-5 text-emerald-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.871 4A17.926 17.926 0 003 12c0 5.147 2.167 9.79 5.66 13.04a1.01 1.01 0 001.34 0C13.493 21.79 15.66 17.147 15.66 12c0-2.833-.655-5.513-1.829-7.9A1.01 1.01 0 0012.87 3.5h-6a1.01 1.01 0 00-.999.5M9 9h1.01M9 12h1.01M9 15h1.01M13 9h1.01M13 12h1.01M13 15h1.01"></path></svg>
                            Physical Medical Milestones
                        </h3>
                        <p class="text-xs text-zinc-500 font-mono">[ VITAL RESTORATION DIRECTIVES ]</p>

                        <div class="space-y-3" id="medical-checklist-container">
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>Call Dental Practice:</strong> Request private extraction availability and get a quote (£100-£600 depending on complexity).</span>
                            </label>
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>Prepare Extraction Recovery Space:</strong> Purchase soft, easy-to-eat foods (mashed potatoes, soup, protein shakes) and over-the-counter pain relief ahead of the procedure.</span>
                            </label>
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>Schedule Vision Assessment:</strong> Book an eye test at a local optician to update your prescription.</span>
                            </label>
                            <label class="flex items-start space-x-3 p-2.5 hover:bg-purple-950/10 border border-transparent hover:border-purple-950/40 rounded-lg cursor-pointer transition-all">
                                <input type="checkbox" onchange="taskCheckedTrigger(this)" class="mt-1 rounded bg-zinc-900 border-purple-950 text-violet-600 focus:ring-0">
                                <span class="text-xs text-zinc-300 leading-relaxed"><strong>Secure Lenses:</strong> Select frames or contact lenses suited for driving and focused screen use to reduce eye strain.</span>
                            </label>
                        </div>
                    </div>
                </div>
            </section>

        </main>
    </div>

    <!-- Feedback Message Box (Replaces alert) -->
    <div id="toast-msg" class="fixed bottom-5 right-5 bg-purple-900 text-white font-semibold px-4 py-3 rounded-xl shadow-2xl transition-all duration-300 transform translate-y-20 opacity-0 z-50 flex items-center space-x-2 border border-purple-500">
        <svg class="w-5 h-5 text-violet-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>
        <span id="toast-text">Text Copied Successfully!</span>
    </div>

    <!-- Active JavaScript for Navigation and Utility Operations -->
    <script>
        // ------------------ WEB AUDIO SYSTEM SYNTHESIS ------------------
        let audioCtx = null;

        // Initialize Web Audio Context upon initial user gesture to satisfy browser autoplay security models
        function initAudio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
        }

        function playSystemSound(type) {
            initAudio();
            if (!audioCtx) return;

            // Resume audio context if suspended by browser
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }

            const osc = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            osc.connect(gainNode);
            gainNode.connect(audioCtx.destination);

            const now = audioCtx.currentTime;

            if (type === 'click') {
                // Short, mechanical tactical HUD blip
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(800, now);
                osc.frequency.exponentialRampToValueAtTime(150, now + 0.1);
                gainNode.gain.setValueAtTime(0.15, now);
                gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.1);
                osc.start(now);
                osc.stop(now + 0.1);
            } 
            else if (type === 'boot') {
                // Low-frequency harmonic system boot-up swell
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(90, now);
                osc.frequency.exponentialRampToValueAtTime(220, now + 0.4);
                
                // Second complementary oscillator for harmony
                const osc2 = audioCtx.createOscillator();
                const gainNode2 = audioCtx.createGain();
                osc2.connect(gainNode2);
                gainNode2.connect(audioCtx.destination);
                osc2.type = 'sine';
                osc2.frequency.setValueAtTime(130, now);
                osc2.frequency.exponentialRampToValueAtTime(330, now + 0.4);

                gainNode.gain.setValueAtTime(0.01, now);
                gainNode.gain.linearRampToValueAtTime(0.12, now + 0.2);
                gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.4);

                gainNode2.gain.setValueAtTime(0.01, now);
                gainNode2.gain.linearRampToValueAtTime(0.1, now + 0.2);
                gainNode2.gain.exponentialRampToValueAtTime(0.01, now + 0.4);

                osc.start(now);
                osc2.start(now);
                osc.stop(now + 0.4);
                osc2.stop(now + 0.4);
            } 
            else if (type === 'complete') {
                // Upward synthetic major sweep (quest ticked)
                osc.type = 'sine';
                osc.frequency.setValueAtTime(329.63, now); // E4
                osc.frequency.setValueAtTime(392.00, now + 0.08); // G4
                osc.frequency.setValueAtTime(523.25, now + 0.16); // C5
                osc.frequency.exponentialRampToValueAtTime(1046.50, now + 0.4); // C6
                
                gainNode.gain.setValueAtTime(0.15, now);
                gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.45);
                osc.start(now);
                osc.stop(now + 0.45);
            } 
            else if (type === 'levelUp') {
                // Glorious cascading system level-up sequence
                const notes = [261.63, 329.63, 392.00, 523.25, 659.25, 783.99, 1046.50];
                notes.forEach((freq, index) => {
                    const localOsc = audioCtx.createOscillator();
                    const localGain = audioCtx.createGain();
                    localOsc.connect(localGain);
                    localGain.connect(audioCtx.destination);
                    localOsc.type = 'triangle';
                    localOsc.frequency.setValueAtTime(freq, now + (index * 0.08));
                    localGain.gain.setValueAtTime(0.12, now + (index * 0.08));
                    localGain.gain.exponentialRampToValueAtTime(0.005, now + (index * 0.08) + 0.25);
                    localOsc.start(now + (index * 0.08));
                    localOsc.stop(now + (index * 0.08) + 0.25);
                });
            }
        }

        // ------------------ DYNAMIC PROGRESS ENGINE ------------------
        function initSystem() {
            updateSystemProgress(false); // Init without triggering levelUp sounds immediately
            
            // Add sound triggers to all inputs on tab navigation
            const navButtons = document.querySelectorAll('#tab-nav button');
            navButtons.forEach(btn => {
                btn.addEventListener('click', () => playSystemSound('click'));
            });
        }

        function updateSystemProgress(triggerSound = true) {
            // Calculate progress based on checklist boxes and tracker rows
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            const totalCheckboxes = checkboxes.length;
            let checkedCount = 0;

            checkboxes.forEach(cb => {
                if (cb.checked) checkedCount++;
            });

            // Include some percentage value based on items in application tracker
            const trackerRows = document.querySelectorAll('#tracker-table tbody tr').length;
            const trackerContribution = Math.min(trackerRows * 5, 20); // up to 20% bonus sync

            let basePercentage = totalCheckboxes > 0 ? (checkedCount / totalCheckboxes) * 80 : 0;
            let finalPercentage = Math.round(basePercentage + trackerContribution);
            finalPercentage = Math.min(finalPercentage, 100);

            // Update UI elements
            const percentLabel = document.getElementById('global-sync-percent');
            const progressBar = document.getElementById('global-sync-bar');

            percentLabel.innerText = finalPercentage + '%';
            progressBar.style.width = finalPercentage + '%';

            // Glow animation booster when full synchronization occurs
            const mainBox = document.querySelector('main');
            if (finalPercentage === 100) {
                progressBar.classList.add('bg-gradient-to-r', 'from-fuchsia-500', 'to-violet-500');
                mainBox.classList.add('glowing-monarch-border-active');
                if (triggerSound) playSystemSound('levelUp');
            } else {
                mainBox.classList.remove('glowing-monarch-border-active');
                mainBox.classList.add('glowing-monarch-border');
            }
        }

        function taskCheckedTrigger(element) {
            if (element.checked) {
                playSystemSound('complete');
                // Trigger a brief flash card energy effect
                const parent = element.closest('label');
                parent.classList.add('bg-purple-950/20', 'border-purple-800/60');
                setTimeout(() => {
                    parent.classList.remove('border-purple-800/60');
                }, 1000);
            } else {
                playSystemSound('click');
                const parent = element.closest('label');
                parent.classList.remove('bg-purple-950/20');
            }
            updateSystemProgress(true);
        }

        // ------------------ GEMINI API UTILITIES ------------------
        
        // Asynchronous prompt processor utilizing the gemini-2.5-flash-preview-09-2025 model.
        // Integrates exponential backoff error handling framework as per specifications.
        async function fetchGeminiLlmResponse(prompt) {
            const apiKey = ""; // API key automatically provisioned by workspace runtime container
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
            
            let retries = 5;
            let backoffDelay = 1000; // start with 1 second delay
            
            for (let i = 0; i < retries; i++) {
                try {
                    const response = await fetch(url, {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify({
                            contents: [{ parts: [{ text: prompt }] }]
                        })
                    });
                    
                    if (response.ok) {
                        const responseData = await response.json();
                        const parsedText = responseData.candidates?.[0]?.content?.parts?.[0]?.text;
                        if (parsedText) return parsedText;
                    }
                } catch (err) {
                    // Failures intentionally hidden from browser log as required
                }
                
                // Exponential Backoff Delay
                await new Promise(resolve => setTimeout(resolve, backoffDelay));
                backoffDelay *= 2; 
            }
            throw new Error("API Connection Failed after 5 Retries. Please check your network connection.");
        }

        // Action: Generate customized PIP Daily Living & Mobility Statement
        async function generateAIPipStatement() {
            const userInput = document.getElementById('ai-pip-input').value.trim();
            if (!userInput) {
                showToast("Please provide some basic symptoms/limitations.");
                return;
            }

            const btn = document.getElementById('ai-pip-btn');
            const loader = document.getElementById('pip-btn-loader');
            const outputBox = document.getElementById('pip-template-box');

            // Set loading state
            btn.disabled = true;
            loader.classList.remove('hidden');

            const instructionPrompt = `You are an expert UK disability advocacy lawyer assisting an applicant with a PIP (Personal Independence Payment) Personal Statement.
The applicant has specified the following key challenges/symptoms: "${userInput}".

Write a highly detailed, formal Personal Statement for their PIP application addressing:
1. Daily Living Activities (specifically how preparing food, managing treatment/medication, washing, dressing, and hygiene tasks are impacted on more than 50% of days).
2. Mobility Activities (how navigating routes, coping with sensory overwhelm, and managing physical/mental stamina are impacted).

Ensure it uses a clear, highly respectful, objective tone. Use structured sections (e.g. Preparing Food, Washing & Bathing, Planning Journeys). Do not include placeholder brackets or variables, make it ready to edit. Keep paragraphs readable and aligned to DWP descriptors. Provide a brief introduction and conclusion. Start the response directly with: "STATEMENT OF APPLICANT REGARDING DAILY LIVING AND MOBILITY"`;

            try {
                const aiResult = await fetchGeminiLlmResponse(instructionPrompt);
                outputBox.value = aiResult;
                showToast("✨ Personal Statement drafted successfully!");
                playSystemSound('levelUp');
            } catch (error) {
                showToast("AI system temporary offline. Try again.");
            } finally {
                btn.disabled = false;
                loader.classList.add('hidden');
            }
        }

        // Action: Generate pre-action claims letter for Small Claims Tab
        async function generateAICourtLetter() {
            const vendor = document.getElementById('ai-court-vendor').value.trim();
            const issue = document.getElementById('ai-court-issue').value.trim();

            if (!vendor || !issue) {
                showToast("Please input both the counterparty name and issue details.");
                return;
            }

            const btn = document.getElementById('ai-court-btn');
            const loader = document.getElementById('court-btn-loader');
            const outputBox = document.getElementById('court-template-box');

            btn.disabled = true;
            loader.classList.remove('hidden');

            const letterPrompt = `Write a formal UK "Letter Before Action" (Pre-Action Protocol compliant) seeking recovery of £110.00.
Defendant Name: ${vendor}
Details of dispute: ${issue} (contract unfulfilled/faulty caps/non-delivery).

The letter must comply with civil pre-action conduct guidelines in the UK. State that the defendant has 14 days from the date of the letter to pay or settle the claim, after which County Court proceedings will be launched via Money Claim Online (MCOL) seeking the £110.00, court fees, interest at 8% statutory rate per annum under Sec 69 of County Courts Act 1984, and associated admin fees.
Do not use square brackets [ ] in the letter body—make it professional and fully formatted, leaving clear space for the Sender's name and Recipient's name/address at the top.`;

            try {
                const letterResult = await fetchGeminiLlmResponse(letterPrompt);
                outputBox.value = letterResult;
                showToast("✨ Legal letter customized!");
                playSystemSound('levelUp');
            } catch (err) {
                showToast("AI system temporary offline. Try again.");
            } finally {
                btn.disabled = false;
                loader.classList.add('hidden');
            }
        }

        // Action: Optimize Resume profile Summary for CV
        async function generateAIResumeSummary() {
            const title = document.getElementById('ai-job-title').value.trim();
            const skills = document.getElementById('ai-job-skills').value.trim();

            if (!title || !skills) {
                showToast("Please enter a job title and your skills.");
                return;
            }

            const btn = document.getElementById('ai-job-btn');
            const loader = document.getElementById('job-btn-loader');
            const container = document.getElementById('ai-resume-output-container');
            const outputBox = document.getElementById('ai-resume-output-box');

            btn.disabled = true;
            loader.classList.remove('hidden');

            const resumePrompt = `Draft a highly professional, ATS-optimized Profile Summary statement for a CV.
Target Job Title: ${title}
Candidate's key strengths and context: ${skills} (They are currently executing a personal reset to build independence, showing exceptional structure, accountability, and drive to work).

Write a compelling, powerful 3-4 sentence paragraph that showcases organizational capability, self-motivation, attention to detail, and immediate readiness to contribute. Keep it punchy and impactful without buzzwords.`;

            try {
                const optimizedSummary = await fetchGeminiLlmResponse(resumePrompt);
                outputBox.value = optimizedSummary;
                container.classList.remove('hidden');
                showToast("✨ Profile summary ready for your CV!");
                playSystemSound('levelUp');
            } catch (err) {
                showToast("AI system temporary offline. Try again.");
            } finally {
                btn.disabled = false;
                loader.classList.add('hidden');
            }
        }

        // Action: Decompose major tasks into tiny dopamine milestones
        async function decomposeTaskWithAI() {
            const taskInput = document.getElementById('ai-task-input').value.trim();
            if (!taskInput) {
                showToast("Please provide a task to break down.");
                return;
            }

            const btn = document.getElementById('ai-task-btn');
            const loader = document.getElementById('task-btn-loader');
            const container = document.getElementById('ai-task-output-container');
            const stepsBox = document.getElementById('ai-task-steps');

            btn.disabled = true;
            loader.classList.remove('hidden');

            const decomposePrompt = `You are an expert executive functioning coach who helps people facing severe anxiety, panic, or ADHD overwhelm.
The user wants to accomplish the following task: "${taskInput}".

Break this task down into exactly 4-5 extremely small, safe, and low-friction action steps.
The first step must be so easy it takes under 30 seconds (e.g. 'Put on one cleaning glove' or 'Open your browser tab').
Use clear, empathetic, direct instructions. If the task relates to domestic cleaning, emphasize safety against dust or pests (e.g., dampening dust with spray before handling). Return the steps strictly as standard HTML paragraph blocks with short descriptions. Do not include headers or styling.`;

            try {
                const stepsOutput = await fetchGeminiLlmResponse(decomposePrompt);
                stepsBox.innerHTML = stepsOutput;
                container.classList.remove('hidden');
                showToast("✨ Micro-tasks successfully structured!");
                playSystemSound('levelUp');
            } catch (err) {
                showToast("AI system temporary offline. Try again.");
            } finally {
                btn.disabled = false;
                loader.classList.add('hidden');
            }
        }

        // Action: AI Savings and Holiday Planner
        async function generateAISavingsPlan() {
            const income = document.getElementById('ai-savings-income').value;
            const target = document.getElementById('ai-savings-priority').value;

            if (!income || income <= 0) {
                showToast("Please enter a valid monthly income/allowance.");
                return;
            }

            const btn = document.getElementById('ai-savings-btn');
            const loader = document.getElementById('savings-btn-loader');
            const container = document.getElementById('ai-savings-output-container');
            const outputBox = document.getElementById('ai-savings-output-box');

            btn.disabled = true;
            loader.classList.remove('hidden');

            const savingsPrompt = `Create a realistic monthly savings plan.
Monthly available funds: £${income}
Target focus assets: ${target}

The user is working towards resetting their environment, improving mental/physical health, and going on holiday in Summer 2027. Provide an actionable timeline showing exactly how much they should save each month, how many months it will take to acquire each asset, and brief tips on setting up automated bank vault transfers (e.g. using Monzo, Revolut or similar digital spaces). Make the text clean and highly readable.`;

            try {
                const planResult = await fetchGeminiLlmResponse(savingsPrompt);
                outputBox.value = planResult;
                container.classList.remove('hidden');
                showToast("✨ Savings plan generated successfully!");
                playSystemSound('levelUp');
            } catch (err) {
                showToast("AI system temporary offline. Try again.");
            } finally {
                btn.disabled = false;
                loader.classList.add('hidden');
            }
        }

        // Action: AI Reconnect Text Draft Builder
        async function generateAIReconnectText() {
            const recipient = document.getElementById('ai-reconnect-person').value;
            const tone = document.getElementById('ai-reconnect-tone').value;

            const btn = document.getElementById('ai-reconnect-btn');
            const loader = document.getElementById('reconnect-btn-loader');
            const container = document.getElementById('ai-reconnect-output-container');
            const outputBox = document.getElementById('ai-reconnect-output-box');

            btn.disabled = true;
            loader.classList.remove('hidden');

            const reconnectPrompt = `Draft a low-anxiety, highly approachable text message template.
Recipient: ${recipient}
Tone: ${tone}

Make it short, friendly, and easy to read. It should require minimal mental friction to copy-paste and send. Ensure there are no complex commitments, just simple connection building that allows the user to re-engage with support networks at their own pace. Return 2 different copyable message options.`;

            try {
                const reconnectResult = await fetchGeminiLlmResponse(reconnectPrompt);
                outputBox.value = reconnectResult;
                container.classList.remove('hidden');
                showToast("✨ Reconnect message draft ready!");
                playSystemSound('levelUp');
            } catch (err) {
                showToast("AI system temporary offline. Try again.");
            } finally {
                btn.disabled = false;
                loader.classList.add('hidden');
            }
        }

        // Action: AI Room Rescuer & Clean Coach
        async function generateAICleaningPlan() {
            const energy = document.getElementById('ai-coach-energy').value;
            const target = document.getElementById('ai-coach-target').value;

            const btn = document.getElementById('ai-coach-btn');
            const loader = document.getElementById('coach-btn-loader');
            const container = document.getElementById('ai-coach-output-container');
            const outputBox = document.getElementById('ai-coach-output-box');

            btn.disabled = true;
            loader.classList.remove('hidden');

            const coachPrompt = `You are a supportive, warm, and zero-judgment decluttering coach.
User current energy state: ${energy}
User priority mess target: ${target}

Draft a highly motivational, structured room-rescue action guide. Emphasize safe cleaning practices for mice/pests (damp-cleaning rather than sweeping/dry-vacuuming droppings to prevent breathing in dust). Give small, low-stress milestones. Break the guide down into simple phases with clear times (e.g., Phase 1: 5 minutes, Phase 2: 10 minutes). Do not use square brackets. Format using standard HTML paragraph tags.`;

            try {
                const coachResult = await fetchGeminiLlmResponse(coachPrompt);
                outputBox.innerHTML = coachResult;
                container.classList.remove('hidden');
                showToast("✨ Cleaning guide drafted successfully!");
                playSystemSound('levelUp');
            } catch (err) {
                showToast("AI system temporary offline. Try again.");
            } finally {
                btn.disabled = false;
                loader.classList.add('hidden');
            }
        }

        // ------------------ TAB NAVIGATION ------------------
        function switchTab(tabId) {
            // Hide all tab containers
            document.getElementById('tab-content-roadmap').classList.add('hidden');
            document.getElementById('tab-content-pip').classList.add('hidden');
            document.getElementById('tab-content-smallclaims').classList.add('hidden');
            document.getElementById('tab-content-hmrc').classList.add('hidden');
            document.getElementById('tab-content-checklists').classList.add('hidden');

            // Show active container
            document.getElementById('tab-content-' + tabId).classList.remove('hidden');

            // Reset navigation buttons styles
            const navButtons = document.querySelectorAll('#tab-nav button');
            navButtons.forEach(btn => {
                btn.classList.remove('bg-purple-950/40', 'border-purple-500/50', 'text-white', 'shadow-lg', 'shadow-purple-950/20');
                btn.classList.add('text-zinc-400', 'hover:bg-zinc-900', 'hover:text-white');
            });

            // Set active navigation button style
            const activeBtn = document.getElementById('nav-' + tabId);
            activeBtn.classList.remove('text-zinc-400', 'hover:bg-zinc-900', 'hover:text-white');
            activeBtn.classList.add('bg-purple-950/40', 'border-purple-500/50', 'text-white', 'shadow-lg', 'shadow-purple-950/20');
        }

        // ------------------ SYSTEM UTILITIES ------------------
        function copyText(textareaId, buttonId) {
            const textarea = document.getElementById(textareaId);
            textarea.select();
            textarea.setSelectionRange(0, 99999); // Mobile compatibility

            try {
                // Clipboard API fallback for standard iframe environments
                document.execCommand('copy');
                showToast("Text copied to clipboard!");
                playSystemSound('complete');
            } catch (err) {
                showToast("Copy failed. Please select and copy manually.");
            }
        }

        function showToast(message) {
            const toast = document.getElementById('toast-msg');
            const toastText = document.getElementById('toast-text');
            toastText.textContent = message;
            toast.classList.remove('translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');
            
            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        function addTrackRecord() {
            const company = document.getElementById('track-comp').value.trim();
            const role = document.getElementById('track-role').value.trim();
            const status = document.getElementById('track-status').value.trim();

            if (!company || !role || !status) {
                showToast("Please fill in all tracker fields.");
                return;
            }

            const table = document.getElementById('tracker-table').getElementsByTagName('tbody')[0];
            const newRow = table.insertRow();
            newRow.className = "hover:bg-purple-950/10";

            newRow.innerHTML = `
                <td class="p-3 font-medium text-white">${company}</td>
                <td class="p-3 text-zinc-300">${role}</td>
                <td class="p-3"><span class="px-2 py-0.5 rounded text-xs bg-violet-950 text-violet-400 border border-violet-850">${status}</span></td>
                <td class="p-3 text-right"><button onclick="deleteTrackerRow(this)" class="text-red-400 hover:text-red-300 text-xs font-mono uppercase">Delete</button></td>
            `;

            // Reset inputs
            document.getElementById('track-comp').value = '';
            document.getElementById('track-role').value = '';
            document.getElementById('track-status').value = '';
            showToast("Application added to log.");
            playSystemSound('complete');
            updateSystemProgress(true);
        }

        function deleteTrackerRow(button) {
            button.closest('tr').remove();
            playSystemSound('click');
            updateSystemProgress(true);
        }
    </script>
</body>
</html>

```
