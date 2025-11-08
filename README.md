<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI HUB - Futuristic Knowledge Gateway</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Load Inter font (the default) -->
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');
        /* Load Michroma font for title */
        @import url('https://fonts.googleapis.com/css2?family=Michroma&display=swap');
        
      body {
            font-family: 'Inter', sans-serif;
            /* Ensure body is full screen and has dark fallback */
            background-color: #111827; 
        }
        /* New class for the main title */
        .ai-hub-title {
            font-family: 'Michroma', sans-serif;
            text-shadow: 0 0 15px rgba(0, 255, 255, 0.7); /* Subtle glow for the title */
        }
        .neon-text-light {
            text-shadow: 0 0 5px #0ff, 0 0 10px #0ff, 0 0 20px #0ff;
            color: #ccf;
        }
        .neon-border {
            /* General border used for terminal windows */
            border: 1px solid #0ff;
            box-shadow: 0 0 10px #0ff4;
        }
        /* Scanner line for cards */
        .scanner-line {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(to right, transparent, #0ff, transparent);
            animation: scan 3s infinite linear;
        }
        @keyframes scan {
            0% { transform: translateY(0%); }
            50% { transform: translateY(1000%); } /* A large number to cover vertical scan */
            100% { transform: translateY(0%); }
        }
        /* Custom styles for hidden views */
        .hidden-view {
            display: none;
        }
        /* Custom CSS for Flowchart Arrow */
        .flow-arrow {
            width: 4px;
            height: 40px;
            background-color: #3b82f6; /* Blue for AI section */
            margin: 10px auto;
            position: relative;
            box-shadow: 0 0 8px #3b82f6;
        }
        .flow-arrow::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: -3px;
            border-left: 5px solid transparent;
            border-right: 5px solid transparent;
            border-top: 5px solid #3b82f6;
        }
        
        /* Flowchart styles for 'How AI Works' */
        .flow-node {
            @apply bg-gray-800/80 p-3 rounded-lg border border-orange-500 shadow-lg shadow-orange-500/20 w-full text-center;
        }
        .flow-connector {
            @apply w-full h-12 flex justify-center items-center;
        }
        .flow-connector-line {
            @apply w-1 h-full bg-orange-500/50 relative;
        }
        .flow-connector-arrow {
            @apply w-0 h-0 border-l-4 border-l-transparent border-r-4 border-r-transparent border-t-4 border-t-orange-500 absolute bottom-0;
        }
        
        /* Flowchart styles for 'AI Concepts' */
        .branch-node {
            @apply bg-gray-800/80 p-3 rounded-lg border border-blue-500 shadow-lg shadow-blue-500/20 w-full text-center z-10;
        }
        .branch-connector {
            @apply relative w-1 h-12 bg-blue-500/50 mx-auto;
        }
        .branch-line {
             @apply absolute left-1/2 w-1/2 h-1 bg-blue-500/50;
        }
        
        /* Neural Net Viz */
        .nn-layer {
            @apply flex flex-col justify-center gap-4;
        }
        .nn-node {
            @apply w-10 h-10 rounded-full border-2 border-orange-400 bg-gray-800 shadow-lg shadow-orange-500/30;
        }
        .nn-lines {
            @apply absolute w-full h-full top-0 left-0 z-0;
        }


    </style>
    <!-- Load Three.js Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body class="text-gray-100 min-h-screen p-4 sm:p-8 relative">

    <!-- Three.js Background Container (Fixed and behind content) -->
    <div id="three-bg" class="fixed inset-0 z-0 pointer-events-none"></div>

    <div class="max-w-6xl mx-auto z-10 relative bg-gray-900/90 rounded-xl shadow-2xl p-4 sm:p-8 backdrop-blur-sm">
        
        <!-- Header - AI HUB Title -->
        <header class="text-center mb-12 relative">
            <!-- Link to #menu (new default) for a full reset -->
            <a href="#menu" class="inline-block">
                <h1 class="text-6xl sm:text-7xl font-extrabold tracking-tight pt-4 pb-2 text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500 ai-hub-title">
                    AI HUB
                </h1>
            </a>
            <p class="text-xl sm:text-2xl font-light neon-text-light mt-1 mb-4">
                Knowledge Gateway for the Future
            </p>
            <!-- Navigation to Menu (only visible on content pages) -->
            <button onclick="window.location.hash = '#menu'" id="menu-nav-button"
                    class="hidden absolute top-4 left-0 text-sm py-1 px-3 rounded-full bg-gray-700/80 hover:bg-gray-600 text-cyan-400 border border-cyan-400 transition">
                &larr; Back to Menu
            </button>
        </header>


        <!-- 1. MENU VIEW (THE NEW DEFAULT LANDING PAGE) -->
        <div id="menu-view" class="view">
            <h2 class="text-4xl font-bold mb-8 text-center text-gray-200">Knowledge Network Index</h2>
            <p class="text-center text-lg text-gray-300 mb-12 max-w-2xl mx-auto">
                Select a knowledge module below to initialize the information terminal.
            </p>

            <!-- Main Menu Grid (Back to 6 cards) -->
            <main class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-12">
                
                <!-- 1. AI CONCEPTS Link Card -->
                <a href="#ai" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl transition duration-500 hover:shadow-blue-500/50 hover:bg-gray-700/80 relative overflow-hidden block group h-full cursor-pointer">
                    <div class="scanner-line" style="animation-delay: -1.5s;"></div>
                    <h2 class="text-xl font-extrabold mb-2 text-blue-400 group-hover:text-blue-300 transition">AI Concepts</h2>
                    <p class="text-gray-300 text-sm">
                        Explore the foundational ideas, sub-fields, and history of Artificial Intelligence.
                    </p>
                    <div class="mt-4 text-xs font-semibold text-blue-500 group-hover:underline">
                        Launch Terminal &rarr;
                    </div>
                </a>

                <!-- 2. IMPORTANCE OF AI Link Card -->
                <a href="#importance" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl transition duration-500 hover:shadow-green-500/50 hover:bg-gray-700/80 relative overflow-hidden block group h-full cursor-pointer">
                    <div class="scanner-line" style="background: linear-gradient(to right, transparent, #0f0, transparent);"></div>
                    <h2 class="text-xl font-extrabold mb-2 text-green-400 group-hover:text-green-300 transition">Societal Importance</h2>
                    <p class="text-gray-300 text-sm">
                        Understand the critical impact of AI across healthcare, finance, and other sectors.
                    </p>
                    <div class="mt-4 text-xs font-semibold text-green-500 group-hover:underline">
                        Launch Terminal &rarr;
                    </div>
                </a>
                
                <!-- 3. DIFFERENT BREAKTHROUGHS Link Card -->
                <a href="#breakthroughs" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl transition duration-500 hover:shadow-purple-500/50 hover:bg-gray-700/80 relative overflow-hidden block group h-full cursor-pointer">
                    <div class="scanner-line" style="background: linear-gradient(to right, transparent, #f0f, transparent); animation-delay: -0.75s;"></div>
                    <h2 class="text-xl font-extrabold mb-2 text-purple-400 group-hover:text-purple-300 transition">Recent Breakthroughs</h2>
                    <p class="text-gray-300 text-sm">
                        Review the most significant recent inventions and real-world applications of AI.
                    </p>
                    <div class="mt-4 text-xs font-semibold text-purple-500 group-hover:underline">
                        Launch Terminal &rarr;
                    </div>
                </a>

                <!-- 4. HOW AI WORKS Link Card -->
                <a href="#how" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl transition duration-500 hover:shadow-orange-500/50 hover:bg-gray-700/80 relative overflow-hidden block group h-full cursor-pointer">
                    <div class="scanner-line" style="background: linear-gradient(to right, transparent, #f90, transparent); animation-delay: -0.25s;"></div>
                    <h2 class="text-xl font-extrabold mb-2 text-orange-400 group-hover:text-orange-300 transition">How AI Works</h2>
                    <p class="text-gray-300 text-sm">
                        Learn about the core processes: data, model training, and inference loops.
                    </p>
                    <div class="mt-4 text-xs font-semibold text-orange-500 group-hover:underline">
                        Launch Terminal &rarr;
                    </div>
                </a>
                
                <!-- 5. APPLICATIONS OF AI Link Card (was 6) -->
                <a href="#applications" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl transition duration-500 hover:shadow-pink-500/50 hover:bg-gray-700/80 relative overflow-hidden block group h-full cursor-pointer">
                    <div class="scanner-line" style="background: linear-gradient(to right, transparent, #ec4899, transparent); animation-delay: -1.0s;"></div>
                    <h2 class="text-xl font-extrabold mb-2 text-pink-400 group-hover:text-pink-300 transition">Applications of AI</h2>
                    <p class="text-gray-300 text-sm">
                        Discover where AI is being applied today, from everyday apps to complex scientific research.
                    </p>
                    <div class="mt-4 text-xs font-semibold text-pink-500 group-hover:underline">
                        Launch Terminal &rarr;
                    </div>
                </a>
                
                <!-- 6. INTERACTIVE QUERY Link Card (was 5) -->
                 <a href="#query" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl transition duration-500 hover:shadow-yellow-500/50 hover:bg-gray-700/80 relative overflow-hidden block group h-full cursor-pointer">
                    <div class="scanner-line" style="background: linear-gradient(to right, transparent, #ff0, transparent); animation-delay: -0.5s;"></div>
                    <h2 class="text-xl font-extrabold mb-2 text-yellow-400 group-hover:text-yellow-300 transition">✨ Interactive Query Terminal</h2>
                    <p class="text-gray-300 text-sm">
                        Ask any question about AI, ML, or related future concepts. Live search grounding enabled.
                    </p>
                    <div class="mt-4 text-xs font-semibold text-yellow-500 group-hover:underline">
                        Launch Terminal &rarr;
                    </div>
                </a>

            </main>
        </div>

        <!-- 2. AI CONCEPTS SECTION VIEW -->
        <div id="ai-view" class="hidden-view view"> 
            
            <!-- This div contains the "First Page" content -->
            <div id="intro-ai"> 
                <h2 class="text-4xl font-bold mb-8 text-blue-400">AI Concepts & Branches</h2>
            
                <!-- Ladder Flowchart Structure -->
                <div class="max-w-xl mx-auto mb-12 p-4">
                    <div class="flex">
                        <!-- Main Trunk -->
                        <div class="w-1/4 flex justify-center relative">
                            <div class="w-2 h-full bg-blue-500/50 rounded-full shadow-lg shadow-blue-500/30"></div>
                            <div class="absolute top-0 branch-node w-32" style="left: 50%; transform: translateX(-50%);">
                                <p class="text-lg font-semibold text-blue-300">AI</p>
                            </div>
                        </div>
                
                        <!-- Branches -->
                        <div class="w-3/4 pl-8 pt-20 flex flex-col gap-10">
                            <!-- Branch 1: Machine Learning -->
                            <div class="relative">
                                <div class="branch-node">
                                    <p class="text-md font-semibold text-blue-300">Machine Learning (ML)</p>
                                    <p class="text-xs text-gray-400 mt-1">Learning from data (e.g., Regression, Clustering)</p>
                                </div>
                                <div class="absolute top-1/2 -left-8 w-8 h-1 bg-blue-500/50"></div>
                            </div>
                
                            <!-- Branch 2: NLP -->
                            <div class="relative">
                                <div class="branch-node">
                                    <p class="text-md font-semibold text-blue-300">Natural Language (NLP)</p>
                                    <p class="text-xs text-gray-400 mt-1">Understanding human language (e.g., LLMs, Translation)</p>
                                </div>
                                <div class="absolute top-1/2 -left-8 w-8 h-1 bg-blue-500/50"></div>
                            </div>
                
                            <!-- Branch 3: Computer Vision -->
                            <div class="relative">
                                <div class="branch-node">
                                    <p class="text-md font-semibold text-blue-300">Computer Vision (CV)</p>
                                    <p class="text-xs text-gray-400 mt-1">Interpreting visual information (e.g., Image Recognition)</p>
                                </div>
                                <div class="absolute top-1/2 -left-8 w-8 h-1 bg-blue-500/50"></div>
                            </div>
                            
                            <!-- Branch 4: Robotics -->
                            <div class="relative">
                                <div class="branch-node">
                                    <p class="text-md font-semibold text-blue-300">Robotics</p>
                                    <p class="text-xs text-gray-400 mt-1">Intelligent physical agents (e.g., Autonomous Drones)</p>
                                </div>
                                <div class="absolute top-1/2 -left-8 w-8 h-1 bg-blue-500/50"></div>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- End Flowchart Structure -->

                <p class="text-center text-xl text-gray-300 mb-8 max-w-4xl mx-auto pt-6">
                    Analyze the foundational concepts above. Press the button below to retrieve the detailed report on these topics, their history, and sub-disciplines.
                </p>
                
                <div class="flex justify-center">
                    <button onclick="fetchTopic('AI')"
                            id="ai-button"
                            class="w-full sm:w-auto py-3 px-8 text-xl font-semibold rounded-lg bg-blue-600 hover:bg-blue-500 transition duration-300 focus:outline-none focus:ring-4 focus:ring-blue-500/50 shadow-lg shadow-blue-500/30 mb-8">
                        INITIATE DATA STREAM
                    </button>
                </div>
            </div>
            
            <!-- Information Terminal - This is the "Second Page" for the section -->
            <section id="terminal-content-ai" class="hidden">
                <div id="ai-terminal" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl mt-4 neon-border" style="border-color: #60a5fa; box-shadow: 0 0 10px #60a5fa44;">
                    <h3 class="text-2xl font-bold mb-4 text-gray-200 border-b border-gray-700 pb-2">AI Output Log</h3>
                    <div id="loading-indicator-ai" class="hidden text-center py-10">
                        <div class="animate-spin inline-block w-8 h-8 border-4 rounded-full border-blue-500 border-t-transparent"></div>
                        <p class="mt-3 text-blue-400">Processing AI Request... Standby</p>
                    </div>
                    
                    <div id="output-content-ai" class="text-lg text-gray-300 whitespace-pre-wrap">
                        Data stream initialized. Awaiting system response...
                    </div>

                    <div id="sources-output-ai" class="mt-6 pt-4 border-t border-gray-700 hidden">
                        <p class="text-sm font-semibold text-gray-400 mb-2">Sources:</p>
                        <ul id="sources-list-ai" class="list-disc list-inside text-sm text-gray-500 space-y-1"></ul>
                    </div>
                    <div id="error-message-ai" class="hidden mt-4 text-red-400 text-sm p-3 bg-red-900/50 rounded"></div>
                    
                    <button onclick="resetSection('AI')" 
                            class="mt-6 py-2 px-4 rounded bg-gray-700/80 hover:bg-gray-700 text-blue-400 text-sm border border-blue-400 transition">
                        &larr; Return to Analysis Prompt
                    </button>
                </div>
            </section>
        </div>


        <!-- 3. IMPORTANCE SECTION VIEW -->
        <div id="importance-view" class="hidden-view view">
            <h2 class="text-4xl font-bold mb-6 text-green-400">The Societal Importance of Artificial Intelligence</h2>

            <div id="intro-importance"> <!-- "First Page" content -->
                <p class="text-xl text-gray-300 mb-8 max-w-4xl">
                    Begin the societal impact assessment. Press the button below to retrieve the latest synthesized report on AI's critical influence across global sectors.
                </p>
                <button onclick="fetchTopic('IMPORTANCE')"
                        id="importance-button"
                        class="w-full sm:w-auto py-3 px-8 text-xl font-semibold rounded-lg bg-green-600 hover:bg-green-500 transition duration-300 focus:outline-none focus:ring-4 focus:ring-green-500/50 shadow-lg shadow-green-500/30 mb-8">
                    INITIATE DATA STREAM
                </button>
            </div>

            <!-- Information Terminal - This is the "Second Page" for the section -->
            <section id="terminal-content-importance" class="hidden">
                <div id="importance-terminal" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl mt-4 neon-border" style="border-color: #4ade80; box-shadow: 0 0 10px #4ade8044;">
                    <h3 class="text-2xl font-bold mb-4 text-gray-200 border-b border-gray-700 pb-2">Importance Output Log</h3>
                    <div id="loading-indicator-importance" class="hidden text-center py-10">
                        <div class="animate-spin inline-block w-8 h-8 border-4 rounded-full border-green-500 border-t-transparent"></div>
                        <p class="mt-3 text-green-400">Processing Importance Request... Standby</p>
                    </div>
                    
                    <div id="output-content-importance" class="text-lg text-gray-300 whitespace-pre-wrap">
                        Data stream initialized. Awaiting system response...
                    </div>

                    <div id="sources-output-importance" class="mt-6 pt-4 border-t border-gray-700 hidden">
                        <p class="text-sm font-semibold text-gray-400 mb-2">Sources:</p>
                        <ul id="sources-list-importance" class="list-disc list-inside text-sm text-gray-500 space-y-1"></ul>
                    </div>
                    <div id="error-message-importance" class="hidden mt-4 text-red-400 text-sm p-3 bg-red-900/50 rounded"></div>

                    <button onclick="resetSection('IMPORTANCE')" 
                            class="mt-6 py-2 px-4 rounded bg-gray-700/80 hover:bg-gray-700 text-green-400 text-sm border border-green-400 transition">
                        &larr; Return to Analysis Prompt
                    </button>
                </div>
            </section>
        </div>
        
        <!-- 4. BREAKTHROUGHS SECTION VIEW -->
        <div id="breakthroughs-view" class="hidden-view view">
            <h2 class="text-4xl font-bold mb-6 text-purple-400">Recent AI Breakthroughs and Inventions</h2>

            <div id="intro-breakthroughs"> <!-- "First Page" content -->
                <p class="text-xl text-gray-300 mb-8 max-w-4xl">
                    Access the breakthrough log. Press the button below to retrieve the latest synthesized report on the most significant AI inventions and their real-world impact.
                </p>
                <button onclick="fetchTopic('BREAKTHROUGHS')"
                        id="breakthroughs-button"
                        class="w-full sm:w-auto py-3 px-8 text-xl font-semibold rounded-lg bg-purple-600 hover:bg-purple-500 transition duration-300 focus:outline-none focus:ring-4 focus:ring-purple-500/50 shadow-lg shadow-purple-500/30 mb-8">
                    INITIATE DATA STREAM
                </button>
            </div>

            <!-- Information Terminal - This is the "Second Page" for the section -->
            <section id="terminal-content-breakthroughs" class="hidden">
                <div id="breakthroughs-terminal" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl mt-4 neon-border" style="border-color: #c084fc; box-shadow: 0 0 10px #c084fc44;">
                    <h3 class="text-2xl font-bold mb-4 text-gray-200 border-b border-gray-700 pb-2">Breakthroughs Output Log</h3>
                    <div id="loading-indicator-breakthroughs" class="hidden text-center py-10">
                        <div class="animate-spin inline-block w-8 h-8 border-4 rounded-full border-purple-500 border-t-transparent"></div>
                        <p class="mt-3 text-purple-400">Processing Breakthroughs Request... Standby</p>
                    </div>
                    
                    <div id="output-content-breakthroughs" class="text-lg text-gray-300 whitespace-pre-wrap">
                        Data stream initialized. Awaiting system response...
                    </div>

                    <div id="sources-output-breakthroughs" class="mt-6 pt-4 border-t border-gray-700 hidden">
                        <p class="text-sm font-semibold text-gray-400 mb-2">Sources:</p>
                        <ul id="sources-list-breakthroughs" class="list-disc list-inside text-sm text-gray-500 space-y-1"></ul>
                    </div>
                    <div id="error-message-breakthroughs" class="hidden mt-4 text-red-400 text-sm p-3 bg-red-900/50 rounded"></div>

                    <button onclick="resetSection('BREAKTHROUGHS')" 
                            class="mt-6 py-2 px-4 rounded bg-gray-700/80 hover:bg-gray-700 text-purple-400 text-sm border border-purple-400 transition">
                        &larr; Return to Analysis Prompt
                    </button>
                </div>
            </section>
        </div>

        <!-- 5. HOW AI WORKS SECTION VIEW -->
        <div id="how-view" class="hidden-view view">
            <h2 class="text-4xl font-bold mb-8 text-orange-400">How Artificial Intelligence Works</h2>

            <div id="intro-how"> <!-- "First Page" content -->
                
                <!-- Simple Neural Net Visualization -->
                <div class="max-w-2xl mx-auto mb-12 p-4 relative flex justify-around items-center">
                    
                    <!-- Lines (Absolute positioned, Z-0) -->
                    <div class="nn-lines">
                        <svg class="w-full h-full" preserveAspectRatio="none" viewBox="0 0 100 100">
                            <!-- Input 1 to Hidden -->
                            <line x1="12" y1="20" x2="48" y2="30" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="12" y1="20" x2="48" y2="50" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="12" y1="20" x2="48" y2="70" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <!-- Input 2 to Hidden -->
                            <line x1="12" y1="50" x2="48" y2="30" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="12" y1="50" x2="48" y2="50" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="12" y1="50" x2="48" y2="70" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <!-- Input 3 to Hidden -->
                            <line x1="12" y1="80" x2="48" y2="30" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="12" y1="80" x2="48" y2="50" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="12" y1="80" x2="48" y2="70" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            
                            <!-- Hidden to Output -->
                            <line x1="52" y1="30" x2="88" y2="50" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="52" y1="50" x2="88" y2="50" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                            <line x1="52" y1="70" x2="88" y2="50" stroke="#fb923c" stroke-width="0.5" opacity="0.3"/>
                        </svg>
                    </div>
                
                    <!-- Input Layer -->
                    <div class="z-10 text-center">
                        <p class="text-lg font-semibold text-orange-300 mb-4">Input Layer</p>
                        <div class="nn-layer">
                            <div class="nn-node"></div>
                            <div class="nn-node"></div>
                            <div class="nn-node"></div>
                        </div>
                    </div>
                    
                    <!-- Hidden Layer -->
                    <div class="z-10 text-center">
                        <p class="text-lg font-semibold text-orange-300 mb-4">Hidden Layer</p>
                        <div class="nn-layer">
                            <div class="nn-node"></div>
                            <div class="nn-node"></div>
                            <div class="nn-node"></div>
                        </div>
                    </div>
                    
                    <!-- Output Layer -->
                    <div class="z-10 text-center">
                        <p class="text-lg font-semibold text-orange-300 mb-4">Output Layer</p>
                        <div class="nn-layer" style="justify-content: center; height: 100%;">
                            <div class="nn-node"></div>
                        </div>
                    </div>
                </div>
                <!-- End Neural Net Viz -->
                
                <p class="text-center text-xl text-gray-300 mb-8 max-w-4xl mx-auto pt-6">
                    A Neural Network, visualized above, is a core component of Deep Learning. Press the button to get a detailed explanation of this process, including training and inference.
                </p>
                
                <div class="flex justify-center">
                    <button onclick="fetchTopic('HOW')"
                            id="how-button"
                            class="w-full sm:w-auto py-3 px-8 text-xl font-semibold rounded-lg bg-orange-600 hover:bg-orange-500 transition duration-300 focus:outline-none focus:ring-4 focus:ring-orange-500/50 shadow-lg shadow-orange-500/30 mb-8">
                        INITIATE DATA STREAM
                    </button>
                </div>
            </div>
            
            <!-- Information Terminal - This is the "Second Page" for the section -->
            <section id="terminal-content-how" class="hidden">
                <div id="how-terminal" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl mt-4 neon-border" style="border-color: #fb923c; box-shadow: 0 0 10px #fb923c44;">
                    <h3 class="text-2xl font-bold mb-4 text-gray-200 border-b border-gray-700 pb-2">Process Output Log</h3>
                    <div id="loading-indicator-how" class="hidden text-center py-10">
                        <div class="animate-spin inline-block w-8 h-8 border-4 rounded-full border-orange-500 border-t-transparent"></div>
                        <p class="mt-3 text-orange-400">Processing Request... Standby</p>
                    </div>
                    
                    <div id="output-content-how" class="text-lg text-gray-300 whitespace-pre-wrap">
                        Data stream initialized. Awaiting system response...
                    </div>

                    <div id="sources-output-how" class="mt-6 pt-4 border-t border-gray-700 hidden">
                        <p class="text-sm font-semibold text-gray-400 mb-2">Sources:</p>
                        <ul id="sources-list-how" class="list-disc list-inside text-sm text-gray-500 space-y-1"></ul>
                    </div>
                    <div id="error-message-how" class="hidden mt-4 text-red-400 text-sm p-3 bg-red-900/50 rounded"></div>
                    
                    <button onclick="resetSection('HOW')" 
                            class="mt-6 py-2 px-4 rounded bg-gray-700/80 hover:bg-gray-700 text-orange-400 text-sm border border-orange-400 transition">
                        &larr; Return to Analysis Prompt
                    </button>
                </div>
            </section>
        </div>

        <!-- 6. APPLICATIONS OF AI SECTION VIEW (NEW) -->
        <div id="applications-view" class="hidden-view view">
            <h2 class="text-4xl font-bold mb-6 text-pink-400">Real-World Applications of AI</h2>

            <div id="intro-applications"> <!-- "First Page" content -->
                <p class="text-xl text-gray-300 mb-8 max-w-4xl">
                    Explore the diverse applications of AI. Press the button below to retrieve a detailed report on how AI is implemented in key industries.
                </p>
                
                <div class="flex justify-center">
                    <button onclick="fetchTopic('APPLICATIONS')"
                            id="applications-button"
                            class="w-full sm:w-auto py-3 px-8 text-xl font-semibold rounded-lg bg-pink-600 hover:bg-pink-500 transition duration-300 focus:outline-none focus:ring-4 focus:ring-pink-500/50 shadow-lg shadow-pink-500/30 mb-8">
                        INITIATE DATA STREAM
                    </button>
                </div>
            </div>
            
            <!-- Information Terminal - This is the "Second Page" for the section -->
            <section id="terminal-content-applications" class="hidden">
                <div id="applications-terminal" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl mt-4 neon-border" style="border-color: #ec4899; box-shadow: 0 0 10px #ec489944;">
                    <h3 class="text-2xl font-bold mb-4 text-gray-200 border-b border-gray-700 pb-2">Applications Output Log</h3>
                    <div id="loading-indicator-applications" class="hidden text-center py-10">
                        <div class="animate-spin inline-block w-8 h-8 border-4 rounded-full border-pink-500 border-t-transparent"></div>
                        <p class="mt-3 text-pink-400">Processing Request... Standby</p>
                    </div>
                    
                    <div id="output-content-applications" class="text-lg text-gray-300 whitespace-pre-wrap">
                        Data stream initialized. Awaiting system response...
                    </div>

                    <div id="sources-output-applications" class="mt-6 pt-4 border-t border-gray-700 hidden">
                        <p class="text-sm font-semibold text-gray-400 mb-2">Sources:</p>
                        <ul id="sources-list-applications" class="list-disc list-inside text-sm text-gray-500 space-y-1"></ul>
                    </div>
                    <div id="error-message-applications" class="hidden mt-4 text-red-400 text-sm p-3 bg-red-900/50 rounded"></div>
                    
                    <button onclick="resetSection('APPLICATIONS')" 
                            class="mt-6 py-2 px-4 rounded bg-gray-700/80 hover:bg-gray-700 text-pink-400 text-sm border border-pink-400 transition">
                        &larr; Return to Analysis Prompt
                    </button>
                </div>
            </section>
        </div>

        <!-- 7. INTERACTIVE QUERY TERMINAL VIEW (was 6) -->
        <div id="query-view" class="hidden-view view">
            <h2 class="text-4xl font-bold mb-6 text-yellow-400">✨ Interactive AI Query Terminal</h2>

            <div id="intro-query"> <!-- "First Page" content -->
                <p class="text-xl text-gray-300 mb-8 max-w-4xl">
                    Enter your specific question below to utilize the live LLM network. Ask about any AI/ML concept, history, or application.
                </p>
                
                <!-- Input Field for Custom Query -->
                <textarea id="query-input" rows="4" 
                          class="w-full p-4 mb-6 bg-gray-800/90 border border-yellow-500/50 rounded-lg text-gray-100 placeholder-gray-500 focus:ring-yellow-500 focus:border-yellow-500 transition"
                          placeholder="e.g., How does a Transformer model work? What is the ethical debate around synthetic data?"></textarea>

                <div class="flex justify-center">
                    <button onclick="fetchQuery()"
                            id="query-button"
                            class="w-full sm:w-auto py-3 px-8 text-xl font-semibold rounded-lg bg-yellow-600 hover:bg-yellow-500 transition duration-300 focus:outline-none focus:ring-4 focus:ring-yellow-500/50 shadow-lg shadow-yellow-500/30 mb-8">
                        SEND QUERY TO LLM NETWORK
                    </button>
                </div>
            </div>

            <!-- Information Terminal - This is the "Second Page" for the section -->
            <section id="terminal-content-query" class="hidden">
                <div id="query-terminal" class="bg-gray-800/90 p-6 rounded-xl shadow-2xl mt-4 neon-border" style="border-color: #facc15; box-shadow: 0 0 10px #facc1544;">
                    <h3 class="text-2xl font-bold mb-4 text-gray-200 border-b border-gray-700 pb-2">Query Response Log</h3>
                    <div id="loading-indicator-query" class="hidden text-center py-10">
                        <div class="animate-spin inline-block w-8 h-8 border-4 rounded-full border-yellow-500 border-t-transparent"></div>
                        <p class="mt-3 text-yellow-400">Processing Interactive Query... Standby</p>
                    </div>
                    
                    <div id="output-content-query" class="text-lg text-gray-300 whitespace-pre-wrap">
                        Awaiting user query submission...
                    </div>

                    <div id="sources-output-query" class="mt-6 pt-4 border-t border-gray-700 hidden">
                        <p class="text-sm font-semibold text-gray-400 mb-2">Sources (Grounded Search):</p>
                        <ul id="sources-list-query" class="list-disc list-inside text-sm text-gray-500 space-y-1"></ul>
                    </div>
                    <div id="error-message-query" class="hidden mt-4 text-red-400 text-sm p-3 bg-red-900/50 rounded"></div>

                    <button onclick="resetSection('QUERY')" 
                            class="mt-6 py-2 px-4 rounded bg-gray-700/80 hover:bg-gray-700 text-yellow-400 text-sm border border-yellow-400 transition">
                        &larr; Return to Input Terminal
                    </button>
                </div>
            </section>
        </div>


        <!-- ========== NEW FOOTER CONTENT BEGINS HERE ========== -->

        <!-- NEW "About Us" Section (Mission & Team) -->
        <section class="mt-16 border-t border-gray-700/50 pt-8">
            <h3 class="text-2xl font-bold text-center mb-8 text-gray-400 ai-hub-title" style="text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);">Our Mission & Team</h3>
            
            <!-- Mission Statement -->
            <div class="max-w-3xl mx-auto text-center mb-12">
                <h4 class="text-xl font-semibold text-teal-300 mb-3">Mission Statement</h4>
                <p class="text-lg italic text-gray-300">
                    "To demystify Artificial Intelligence and make its concepts, applications, and ethical considerations accessible to everyone, fostering a future where technology empowers all."
                </p>
            </div>

            <!-- Team Bios -->
            <div class="max-w-4xl mx-auto">
                <h4 class="text-xl font-semibold text-teal-300 mb-6 text-center">Meet the Team (Placeholders)</h4>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <!-- Team Member 1 -->
                    <div class="bg-gray-800/90 p-4 rounded-lg border border-teal-500/30 text-center shadow-lg shadow-teal-500/20">
                        <div class="w-20 h-20 rounded-full bg-gray-700 border-2 border-teal-400 mx-auto mb-3"></div>
                        <h5 class="font-bold text-lg text-teal-300">Dr. Alex Chen</h5>
                        <p class="text-sm text-gray-400">Lead AI Researcher</p>
                    </div>
                    <!-- Team Member 2 -->
                    <div class="bg-gray-800/90 p-4 rounded-lg border border-teal-500/30 text-center shadow-lg shadow-teal-500/20">
                        <div class="w-20 h-20 rounded-full bg-gray-700 border-2 border-teal-400 mx-auto mb-3"></div>
                        <h5 class="font-bold text-lg text-teal-300">Jasmine Kaur</h5>
                        <p class="text-sm text-gray-400">UX/UI Architect</p>
                    </div>
                    <!-- Team Member 3 -->
                    <div class="bg-gray-800/90 p-4 rounded-lg border border-teal-500/30 text-center shadow-lg shadow-teal-500/20">
                        <div class="w-20 h-20 rounded-full bg-gray-700 border-2 border-teal-400 mx-auto mb-3"></div>
                        <h5 class="font-bold text-lg text-teal-300">Leo Ramirez</h5>
                        <p class="text-sm text-gray-400">Ethics & Policy Lead</p>
                    </div>
                </div>
            </div>
        </section>


        <!-- ML Fast Facts Section -->
        <section class="mt-16 border-t border-gray-700/50 pt-8">
            <h3 class="text-2xl font-bold text-center mb-6 text-gray-400 ai-hub-title" style="text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);">ML Fast Facts</h3>
            <div class="flex flex-wrap justify-center gap-3 px-2">
                
                <div class="bg-gray-800/90 text-sm text-cyan-300 py-2 px-4 rounded-full border border-cyan-500/50 shadow-md shadow-cyan-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-cyan-500/40 cursor-default">
                    Coined by Arthur Samuel in 1959
                </div>
                <div class="bg-gray-800/90 text-sm text-green-300 py-2 px-4 rounded-full border border-green-500/50 shadow-md shadow-green-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-green-500/40 cursor-default">
                    Types: Supervised, Unsupervised, Reinforcement
                </div>
                <div class="bg-gray-800/90 text-sm text-purple-300 py-2 px-4 rounded-full border border-purple-500/50 shadow-md shadow-purple-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-purple-500/40 cursor-default">
                    Neural Networks are inspired by the human brain
                </div>
                <div class="bg-gray-800/90 text-sm text-orange-300 py-2 px-4 rounded-full border border-orange-500/50 shadow-md shadow-orange-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-orange-500/40 cursor-default">
                    'Overfitting' is a common training challenge
                </div>
                <div class="bg-gray-800/90 text-sm text-pink-300 py-2 px-4 rounded-full border border-pink-500/50 shadow-md shadow-pink-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-pink-500/40 cursor-default">
                    Used in everything from spam filters to art generation
                </div>

            </div>
        </section>


        <!-- AI Ethics Quotes Section -->
        <section class="mt-16 border-t border-gray-700/50 pt-8">
            <h3 class="text-2xl font-bold text-center mb-8 text-gray-400 ai-hub-title" style="text-shadow: 0 0 10px rgba(255, 100, 100, 0.5);">Ethical Considerations</h3>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 px-2">
                
                <!-- Quote 1: Bias -->
                <blockquote class="bg-gray-800/90 p-4 rounded-lg border-l-4 border-red-500 shadow-md shadow-red-500/20">
                    <p class="text-md italic text-gray-300">"AI systems are only as unbiased as the data they are trained on. Mitigating bias is a critical, ongoing challenge."</p>
                    <footer class="text-right text-sm text-red-400 mt-2">- Core Ethics Principle</footer>
                </blockquote>

                <!-- Quote 2: Accountability -->
                <blockquote class="bg-gray-800/90 p-4 rounded-lg border-l-4 border-yellow-500 shadow-md shadow-yellow-500/20">
                    <p class="text-md italic text-gray-300">"Who is responsible when an autonomous system makes a mistake? Establishing clear lines of accountability is essential."</p>
                    <footer class="text-right text-sm text-yellow-400 mt-2">- Legal &amp; Ethical Debate</footer>
                </blockquote>

                <!-- Quote 3: Transparency -->
                <blockquote class="bg-gray-800/90 p-4 rounded-lg border-l-4 border-cyan-500 shadow-md shadow-cyan-500/20">
                    <p class="text-md italic text-gray-300">"We must build 'explainable AI' (XAI) so that complex 'black box' decisions can be understood and trusted by humans."</p>
                    <footer class="text-right text-sm text-cyan-400 mt-2">- Transparency Guideline</footer>
                </blockquote>

                <!-- Quote 4: Human-in-the-Loop -->
                <blockquote class="bg-gray-800/90 p-4 rounded-lg border-l-4 border-green-500 shadow-md shadow-green-500/20">
                    <p class="text-md italic text-gray-300">"The goal is often not to replace humans, but to augment their capabilities, keeping human judgment at the center."</p>
                    <footer class="text-right text-sm text-green-400 mt-2">- Human-in-the-Loop (HITL)</footer>
                </blockquote>

            </div>
        </section>

        <!-- QUICK LINKS Section -->
        <section class="mt-16 border-t border-gray-700/50 pt-8">
            <h3 class="text-2xl font-bold text-center mb-8 text-gray-400 ai-hub-title" style="text-shadow: 0 0 10px rgba(100, 255, 100, 0.5);">Quick Links & Resources</h3>
            <div class="flex flex-wrap justify-center gap-4 px-2">
                
                <a href="#" onclick="event.preventDefault()" target="_blank"
                   class="bg-gray-800/90 text-sm text-green-300 py-2 px-4 rounded-lg border border-green-500/50 shadow-md shadow-green-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-green-500/40 cursor-not-allowed opacity-75">
                    AI Ethics Blog
                </a>
                <a href="#" onclick="event.preventDefault()" target="_blank"
                   class="bg-gray-800/90 text-sm text-green-300 py-2 px-4 rounded-lg border border-green-500/50 shadow-md shadow-green-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-green-500/40 cursor-not-allowed opacity-75">
                    ML Research Papers
                </a>
                <a href="#" onclick="event.preventDefault()" target="_blank"
                   class="bg-gray-800/90 text-sm text-green-300 py-2 px-4 rounded-lg border border-green-500/50 shadow-md shadow-green-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-green-500/40 cursor-not-allowed opacity-75">
                    AI Developer News
                </a>
                 <a href="#" onclick="event.preventDefault()" target="_blank"
                   class="bg-gray-800/90 text-sm text-green-300 py-2 px-4 rounded-lg border border-green-500/50 shadow-md shadow-green-500/20 transition duration-300 hover:bg-gray-700 hover:shadow-green-500/40 cursor-not-allowed opacity-75">
                    Community Hub
                </a>

            </div>
        </section>


        <!-- CONTACT FOOTER Section -->
        <footer class="mt-16 border-t border-gray-700/50 pt-8 text-center">
            <h3 class="text-2xl font-bold text-center mb-6 text-gray-400 ai-hub-title" style="text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);">Join the Network</h3>
            <p class="text-lg text-gray-300 mb-8 max-w-lg mx-auto">
                Want to connect with other developers, researchers, and students exploring AI?
            </p>
            <!-- A disabled button or link to show the feature is conceptual -->
            <a href="#" onclick="event.preventDefault()"
               class="inline-block py-3 px-8 text-xl font-semibold rounded-lg bg-cyan-600 hover:bg-cyan-500 transition duration-300 focus:outline-none focus:ring-4 focus:ring-cyan-500/50 shadow-lg shadow-cyan-500/30 mb-4 opacity-75 cursor-not-allowed">
                CONTACT & CONNECT
            </a>
            <p class="text-sm text-gray-500">(Note: Community features are in development)</p>
        </footer>


    </div> <!-- End Main Content Wrapper -->

    <script>
        // --- Gemini API Setup ---
        const apiKey = ""; // API key is provided at runtime if left as an empty string
        const apiUrl = "https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent";

        // --- View and Element Selectors (Updated for new default view) ---
        const VIEWS = {
            'menu': document.getElementById('menu-view'), 
            'ai': document.getElementById('ai-view'), 
            'importance': document.getElementById('importance-view'),
            'how': document.getElementById('how-view'),
            'breakthroughs': document.getElementById('breakthroughs-view'),
            'applications': document.getElementById('applications-view'), 
            'query': document.getElementById('query-view')
            // 'team' view has been removed
        };
        const menuNavButton = document.getElementById('menu-nav-button');

        const systemInstruction = "Act as an expert AI/ML educational assistant. Provide a concise, highly informative, and well-structured explanation of the requested topic, focusing on core concepts and real-world relevance. Always use Markdown for formatting (bold, lists).";

        // --- Three.js Setup and Parallax Variables ---
        let scene, camera, renderer, grid; 
        const container = document.getElementById('three-bg');

        let mouseX = 0;
        let mouseY = 0;
        let windowHalfX = window.innerWidth / 2;
        let windowHalfY = window.innerHeight / 2;


        function initThree() {
            // Scene
            scene = new THREE.Scene();
            
            // Camera
            camera = new THREE.PerspectiveCamera(75, container.clientWidth / container.clientHeight, 0.1, 1000);
            camera.position.z = 10; 

            // Renderer
            renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
            renderer.setSize(container.clientWidth, container.clientHeight);
            container.appendChild(renderer.domElement);
            
            window.addEventListener('resize', onWindowResize, false);
            document.addEventListener('mousemove', onDocumentMouseMove, false);

            // --- 3D Grid Wave Setup ---
            const width = 100;
            const height = 100;
            const segments = 60; 

            const geometry = new THREE.PlaneGeometry(width, height, segments, segments);
            
            const material = new THREE.MeshBasicMaterial({
                color: 0x00ffff, // Cyan neon color
                wireframe: true,
                transparent: true,
                opacity: 0.2 
            });

            grid = new THREE.Mesh(geometry, material);
            
            grid.rotation.x = -Math.PI / 2; 
            grid.position.y = -5; 

            scene.add(grid);
            
            const ambientLight = new THREE.AmbientLight(0x404040, 2); 
            scene.add(ambientLight);
        }

        function onWindowResize() {
            if (camera && renderer) {
                windowHalfX = window.innerWidth / 2;
                windowHalfY = window.innerHeight / 2;

                camera.aspect = container.clientWidth / container.clientHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(container.clientWidth, container.clientHeight);
            }
        }
        
        function onDocumentMouseMove(event) {
            mouseX = (event.clientX - windowHalfX) / windowHalfX;
            mouseY = (event.clientY - windowHalfY) / windowHalfY;
        }


        function animate() {
            requestAnimationFrame(animate);

            if (grid) {
                const positionAttribute = grid.geometry.getAttribute('position');
                const vertexCount = positionAttribute.count;
                const time = Date.now() * 0.001;
                
                const cursorInfluence = (Math.abs(mouseX) + Math.abs(mouseY)) / 2; 

                // Slower, more subtle ripple effect parameters
                const baseSpeed = 0.5; 
                const dynamicSpeed = baseSpeed + cursorInfluence * 0.1; 
                const baseAmplitude = 0.3; 
                const dynamicAmplitude = baseAmplitude + cursorInfluence * 0.1; 

                for (let i = 0; i < vertexCount; i++) {
                    const x = positionAttribute.getX(i);
                    const z = Math.sin(x * 0.4 + time * dynamicSpeed) * dynamicAmplitude * 0.5; 
                    positionAttribute.setZ(i, z);
                }

                positionAttribute.needsUpdate = true;
                
                grid.rotation.z += 0.0001;
            }
            
            // Parallax Effect
            const PARALLAX_STRENGTH = 0.08; 
            const targetRotationY = mouseX * PARALLAX_STRENGTH; 
            const targetRotationX = -mouseY * PARALLAX_STRENGTH * 0.7; 

            if (camera) {
                camera.rotation.y += (targetRotationY - camera.rotation.y) * 0.03;
                camera.rotation.x += (targetRotationX - camera.rotation.x) * 0.03;
            }
            
            if (renderer && scene && camera) {
                renderer.render(scene, camera);
            }
        }
        
        // --- View Navigation Logic ---

        function resetSection(topic) {
            const prefix = topic.toLowerCase();
            const introDiv = document.getElementById(`intro-${prefix}`);
            const terminalContainer = document.getElementById(`terminal-content-${prefix}`);
            
            // This check is important because the 'team' view doesn't have a terminal
            if (!introDiv || !terminalContainer) return; 

            const outputContent = document.getElementById(`output-content-${prefix}`);
            
            introDiv.classList.remove('hidden'); 
            terminalContainer.classList.add('hidden'); 
            
            outputContent.textContent = 'Data stream initialized. Awaiting system response...'; 
            document.getElementById(`sources-output-${prefix}`).classList.add('hidden');

            const button = document.getElementById(`${prefix}-button`);
            if(button) button.disabled = false;
        }


        function showView(viewName) {
            const targetId = viewName.replace('#', '');
            
            Object.keys(VIEWS).forEach(key => {
                const view = VIEWS[key];
                if (view) { 
                    if (key === targetId) {
                        view.classList.remove('hidden-view');
                        
                        // Only reset sections that are *not* the menu
                        // and *are* API-driven (i.e., not static pages)
                        if (key !== 'menu') {
                            resetSection(key.toUpperCase());
                        }
                    } else {
                        view.classList.add('hidden-view');
                    }
                } else {
                    console.error(`Error: View element with ID '${key}-view' not found.`);
                }
            });

            // Hide "Back to Menu" button only when on the menu page itself
            if (targetId === 'menu') {
                menuNavButton.classList.add('hidden');
            } else {
                menuNavButton.classList.remove('hidden');
            }
        }

        function handleHashChange() {
            // New default hash is #menu
            const hash = window.location.hash || '#menu';
            const viewName = hash.substring(1);
            if (VIEWS[viewName]) {
                showView(hash);
            } else {
                window.location.hash = '#menu'; 
            }
        }

        // --- Loading and API Fetching Logic ---
        
        function showLoading(topic) {
            const prefix = topic.toLowerCase();
            const introDiv = document.getElementById(`intro-${prefix}`);
            const terminalContainer = document.getElementById(`terminal-content-${prefix}`);

            introDiv.classList.add('hidden');
            terminalContainer.classList.remove('hidden');
            
            const loadingIndicator = document.getElementById(`loading-indicator-${prefix}`);
            const outputContent = document.getElementById(`output-content-${prefix}`);
            const sourcesOutput = document.getElementById(`sources-output-${prefix}`);
            const errorMessageDiv = document.getElementById(`error-message-${prefix}`);
            const button = document.getElementById(`${prefix}-button`);
            
            outputContent.textContent = topic === 'QUERY' ? 'Processing Interactive Query...' : 'Data stream initialized. Awaiting system response...';
            sourcesOutput.classList.add('hidden');
            errorMessageDiv.classList.add('hidden');
            
            loadingIndicator.classList.remove('hidden');
            if(button) button.disabled = true; 
        }

        function hideLoading(topic) {
            const prefix = topic.toLowerCase();
            const loadingIndicator = document.getElementById(`loading-indicator-${prefix}`);
            const button = document.getElementById(`${prefix}-button`);
            
            loadingIndicator.classList.add('hidden');
            if(button) button.disabled = false;
        }

        async function callGeminiApi(payload, retries = 0) {
            const maxRetries = 3;
            const delay = Math.pow(2, retries) * 1000;

            if (retries > 0) {
                await new Promise(resolve => setTimeout(resolve, delay));
            }

            try {
                const response = await fetch(`${apiUrl}?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    if (response.status === 429 && retries < maxRetries) {
                        return callGeminiApi(payload, retries + 1);
                    }
                    throw new Error(`HTTP error! Status: ${response.status}`);
                }

                return await response.json();

            } catch (error) {
                if (retries < maxRetries) {
                    return callGeminiApi(payload, retries + 1);
                }
                throw new Error(`Failed to fetch content after ${maxRetries} attempts: ${error.message}`);
            }
        }
        
        // Function for pre-set topics
        async function fetchTopic(topic) {
            const prefix = topic.toLowerCase();
            const outputContent = document.getElementById(`output-content-${prefix}`);
            const sourcesOutput = document.getElementById(`sources-output-${prefix}`);
            const sourcesList = document.getElementById(`sources-list-${prefix}`);
            const errorMessageDiv = document.getElementById(`error-message-${prefix}`);

            showLoading(topic);

            let userQuery;
            if (topic === 'AI') { 
                userQuery = "Explain the fundamental concepts of Artificial Intelligence, including the difference between narrow and general AI, and its main sub-disciplines like machine learning, deep learning, NLP, and computer vision, matching the flowchart provided.";
            } else if (topic === 'IMPORTANCE') {
                userQuery = "Summarize the critical importance and societal impact of Artificial Intelligence in the 21st century across five key domains: Healthcare, Finance, Transportation, Education, and Creative Arts.";
            } else if (topic === 'HOW') { 
                userQuery = "Explain how AI works, focusing on the core concepts visualized in the neural network diagram (Input Layer, Hidden Layers, Output Layer). Describe the process of 'training' (learning from data) and 'inference' (making predictions).";
            } else if (topic === 'BREAKTHROUGHS') {
                userQuery = "Detail the top five most significant recent breakthroughs and inventions in Artificial Intelligence, explaining how each breakthrough functions and its current real-world impact.";
            } else if (topic === 'APPLICATIONS') { 
                userQuery = "Provide a comprehensive overview of the real-world applications of Artificial Intelligence. Please categorize these applications by key industries such as Healthcare, Finance, Entertainment, Transportation, and E-commerce, and provide a specific example for each.";
            } else {
                console.error("Unknown topic requested:", topic);
                hideLoading(topic);
                errorMessageDiv.textContent = 'Error: Requested section does not exist in the current configuration.';
                errorMessageDiv.classList.remove('hidden');
                return;
            }

            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                tools: [{ "google_search": {} }],
                systemInstruction: {
                    parts: [{ text: systemInstruction }]
                },
            };
            
            try {
                const result = await callGeminiApi(payload);
                
                const candidate = result.candidates?.[0];

                if (candidate && candidate.content?.parts?.[0]?.text) {
                    const text = candidate.content.parts[0].text;
                    outputContent.textContent = text; 

                    let sources = [];
                    const groundingMetadata = candidate.groundingMetadata;
                    
                    if (groundingMetadata && groundingMetadata.groundingAttributions) {
                        sources = groundingMetadata.groundingAttributions
                            .map(attribution => ({
                                uri: attribution.web?.uri,
                                title: attribution.web?.title,
                            }))
                            .filter(source => source.uri && source.title); 
                    }
                    
                    if (sources.length > 0) {
                        sourcesList.innerHTML = sources.map((s, index) => 
                            `<li><a href="${s.uri}" target="_blank" class="text-cyan-500 hover:text-cyan-400 transition duration-150">${s.title}</a></li>`
                        ).join('');
                        sourcesOutput.classList.remove('hidden');
                    } else {
                        sourcesOutput.classList.add('hidden');
                    }

                } else {
                    outputContent.textContent = 'Error: The knowledge network returned an unexpected response structure.';
                }

            } catch (error) {
                console.error("API CallError:", error);
                errorMessageDiv.textContent = `A critical error occurred: ${error.message}. Please try again.`;
                errorMessageDiv.classList.remove('hidden');
                outputContent.textContent = 'Failed to load content due to a network or service error.';
            } finally {
                hideLoading(topic);
            }
        }
        
        // New function for interactive queries using the text box
        async function fetchQuery() {
            const topic = 'QUERY';
            const prefix = topic.toLowerCase();
            const outputContent = document.getElementById(`output-content-${prefix}`);
            const sourcesOutput = document.getElementById(`sources-output-${prefix}`);
            const sourcesList = document.getElementById(`sources-list-${prefix}`);
            const errorMessageDiv = document.getElementById(`error-message-${prefix}`);
            const queryInput = document.getElementById('query-input');
            const userQuery = queryInput.value.trim();

            if (!userQuery) {
                outputContent.textContent = 'Please enter a question to initiate the query.';
                // Immediately switch to the output view to show the prompt message
                const introDiv = document.getElementById(`intro-${prefix}`);
                const terminalContainer = document.getElementById(`terminal-content-${prefix}`);
                introDiv.classList.add('hidden');
                terminalContainer.classList.remove('hidden');
                return;
            }

            showLoading(topic);

            const fullUserQuery = `Answer this user question about AI/ML or a related future concept: ${userQuery}`;

            const payload = {
                contents: [{ parts: [{ text: fullUserQuery }] }],
                tools: [{ "google_search": {} }],
                systemInstruction: {
                    parts: [{ text: "Act as an expert AI/ML educational assistant. Provide a concise, highly informative, and well-structured answer to the user's question, focusing on core concepts and real-world relevance. Always use Markdown for formatting (bold, lists). Keep the response engaging and professional." }]
                },
            };

            try {
                const result = await callGeminiApi(payload);
                
                const candidate = result.candidates?.[0];

                if (candidate && candidate.content?.parts?.[0]?.text) {
                    const text = candidate.content.parts[0].text;
                    outputContent.textContent = text; 

                    let sources = [];
                    const groundingMetadata = candidate.groundingMetadata;
                    
                    if (groundingMetadata && groundingMetadata.groundingAttributions) {
                        sources = groundingMetadata.groundingAttributions
                            .map(attribution => ({
                                uri: attribution.web?.uri,
                                title: attribution.web?.title,
                            }))
                            .filter(source => source.uri && source.title); 
                    }
                    
                    if (sources.length > 0) {
                        // Use yellow link color for consistency
                        sourcesList.innerHTML = sources.map((s, index) => 
                            `<li><a href="${s.uri}" target="_blank" class="text-yellow-500 hover:text-yellow-400 transition duration-150">${s.title}</a></li>`
                        ).join('');
                        sourcesOutput.classList.remove('hidden');
                    } else {
                        sourcesOutput.classList.add('hidden');
                    }

                } else {
                    outputContent.textContent = 'Error: The knowledge network returned an unexpected response structure.';
                }

            } catch (error) {
                console.error("API Call Error:", error);
                errorMessageDiv.textContent = `A critical error occurred: ${error.message}. Please try again.`;
                errorMessageDiv.classList.remove('hidden');
                outputContent.textContent = 'Failed to load content due to a network or service error.';
            } finally {
                hideLoading(topic);
            }
        }


        // --- Initialization ---
        window.addEventListener('hashchange', handleHashChange);
        window.onload = function() {
            // Apply Tailwind utility classes dynamically
            // This is a common pattern when classes are generated by JS
            // For this project, it's mainly handled by toggling 'hidden'
            
            initThree();
            animate();
            
            windowHalfX = window.innerWidth / 2; 
            windowHalfY = window.innerHeight / 2;
            
            // Initial view setup
            handleHashChange(); 
        }
    </script>
</body>
</html>
