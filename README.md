# -talk
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>小豬與小豬寶寶的睡前talk</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Zen+Maru+Gothic:wght@400;500;700&family=Noto+Sans+TC:wght@300;400;500;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        night: {
                            900: '#090a16',
                            800: '#111328',
                            700: '#1b1e3d',
                        },
                        violet: {
                            400: '#a78bfa',
                            500: '#8b5cf6',
                            600: '#7c3aed',
                        },
                        piggy: {
                            100: '#ffe4e6',
                            300: '#f472b6',
                            400: '#fb7185',
                            500: '#ec4899',
                        }
                    },
                    fontFamily: {
                        sans: ['"Zen Maru Gothic"', '"Noto Sans TC"', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        /* 藍紫色夜幕夢幻背景 */
        body {
            background: radial-gradient(circle at 50% 20%, #2e1065 0%, #1e1b4b 40%, #0f172a 85%, #080811 100%);
            min-height: 100vh;
            color: #f1f5f9;
            overflow-x: hidden;
            font-family: 'Zen Maru Gothic', 'Noto Sans TC', sans-serif;
        }

        /* 閃爍星空 */
        .star {
            position: absolute;
            background: #ffffff;
            border-radius: 50%;
            opacity: 0.3;
            animation: twinkle var(--duration) infinite ease-in-out;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.2; transform: scale(0.8); }
            50% { opacity: 0.95; transform: scale(1.3); }
        }

        /* 玻璃質感面板 */
        .glass-panel {
            background: rgba(23, 23, 50, 0.65);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(167, 139, 250, 0.2);
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
        }

        /* 扭蛋機外觀 */
        .gacha-machine-body {
            background: linear-gradient(180deg, #3b0764 0%, #2e1065 50%, #1e1b4b 100%);
            border: 4px solid #a78bfa;
            box-shadow: 0 0 35px rgba(167, 139, 250, 0.3), inset 0 0 20px rgba(0, 0, 0, 0.5);
        }

        /* 尿布質感機身 */
        .diaper-body {
            background: linear-gradient(180deg, #ffffff 0%, #f1f5f9 100%);
            border: 3px solid #f472b6;
            box-shadow: 0 8px 25px rgba(244, 114, 182, 0.3), inset 0 -4px 6px rgba(0, 0, 0, 0.05);
        }

        /* 扭蛋透明穹頂 */
        .gacha-dome {
            background: radial-gradient(circle at 35% 35%, rgba(255, 255, 255, 0.25) 0%, rgba(255, 255, 255, 0.05) 50%, rgba(139, 92, 246, 0.15) 100%);
            border: 3px solid rgba(255, 255, 255, 0.4);
            box-shadow: inset 0 0 25px rgba(255, 255, 255, 0.2), 0 8px 32px rgba(0, 0, 0, 0.4);
        }

        /* 可愛小豬旋鈕 */
        .piggy-knob {
            background: linear-gradient(135deg, #f472b6 0%, #ec4899 100%);
            box-shadow: 0 8px 20px rgba(236, 72, 153, 0.4), inset 0 2px 4px rgba(255, 255, 255, 0.6);
            transition: transform 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        .piggy-knob.spinning {
            transform: rotate(360deg) scale(0.95);
        }

        /* 扭蛋掉落動畫 */
        @keyframes gachaDrop {
            0% { transform: translateY(-120px) scale(0.4) rotate(0deg); opacity: 0; }
            60% { transform: translateY(10px) scale(1.1) rotate(180deg); opacity: 1; }
            80% { transform: translateY(-5px) scale(0.95) rotate(220deg); }
            100% { transform: translateY(0) scale(1) rotate(240deg); opacity: 1; }
        }

        .gacha-drop-anim {
            animation: gachaDrop 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.27) forwards;
        }

        /* Modal Transitions */
        .modal {
            transition: opacity 0.3s ease, visibility 0.3s ease;
        }
        .modal-content {
            transition: transform 0.35s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        .modal.hidden-modal {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }
        .modal.hidden-modal .modal-content {
            transform: scale(0.85) translateY(30px);
        }

        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="relative flex flex-col justify-between min-h-screen selection:bg-pink-500 selection:text-white">

    <!-- 背景星空 -->
    <div id="stars-container" class="fixed inset-0 pointer-events-none z-0"></div>

    <!-- 頂部標題區 -->
    <header class="relative z-10 pt-6 pb-2 px-4 text-center">
        <div class="inline-flex items-center gap-2 bg-purple-500/20 text-purple-200 px-4 py-1 rounded-full text-xs md:text-sm font-medium border border-purple-400/30 mb-2.5 shadow-lg shadow-purple-950/50">
            <i class="fa-solid fa-moon text-amber-300"></i>
            <span>100 個適合睡前慢慢聊的甜蜜扭蛋話題</span>
            <i class="fa-solid fa-sparkles text-pink-300"></i>
        </div>
        <h1 class="text-2xl md:text-4xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-pink-300 via-purple-200 to-indigo-200 tracking-wide drop-shadow-md">
            小豬與小豬寶寶的睡前talk
        </h1>
    </header>

    <!-- 主要內容區 -->
    <main class="relative z-10 flex-1 max-w-5xl mx-auto w-full px-4 py-3 flex flex-col gap-6">

        <!-- 分類標籤切換 -->
        <div class="glass-panel p-2 rounded-2xl overflow-x-auto no-scrollbar shadow-lg">
            <div id="categoryTabs" class="flex items-center gap-1.5 min-w-max">
                <!-- 動態渲染分類頁籤 -->
            </div>
        </div>

        <div class="flex flex-col lg:flex-row items-center justify-center gap-8 my-2">

            <!-- 左側篩選與進度 -->
            <div class="w-full lg:w-80 flex flex-col gap-4 order-2 lg:order-1">
                
                <!-- 篩選卡片 -->
                <div class="glass-panel p-4 rounded-2xl flex flex-col gap-3">
                    <div class="flex justify-between items-center pb-2 border-b border-purple-500/20">
                        <span class="text-xs font-bold text-purple-200 uppercase tracking-wider flex items-center gap-1.5">
                            <i class="fa-solid fa-sliders text-pink-400"></i>扭蛋機篩選設定
                        </span>
                        <span id="poolStatusBadge" class="text-[11px] bg-purple-500/30 text-purple-200 border border-purple-400/30 px-2.5 py-0.5 rounded-full font-medium">
                            100 題可用
                        </span>
                    </div>

                    <label class="flex items-center justify-between cursor-pointer text-xs text-slate-300 hover:text-white transition py-1">
                        <span class="flex items-center gap-2">
                            <i class="fa-solid fa-eye-slash text-purple-400"></i>過濾已聊過話題
                        </span>
                        <input type="checkbox" id="filterAnswered" class="w-4 h-4 rounded border-purple-500 bg-slate-900 text-pink-500 focus:ring-pink-400">
                    </label>

                    <label class="flex items-center justify-between cursor-pointer text-xs text-slate-300 hover:text-white transition py-1">
                        <span class="flex items-center gap-2">
                            <i class="fa-solid fa-heart text-rose-400"></i>只抽「最愛」話題
                        </span>
                        <input type="checkbox" id="filterFavorites" class="w-4 h-4 rounded border-purple-500 bg-slate-900 text-pink-500 focus:ring-pink-400">
                    </label>
                </div>

                <!-- 進度卡片 -->
                <div class="glass-panel p-4 rounded-2xl">
                    <div class="flex justify-between items-center mb-2">
                        <span class="text-xs font-medium text-purple-200 flex items-center gap-1.5">
                            <i class="fa-solid fa-chart-line text-pink-400"></i>話題解鎖進度
                        </span>
                        <span id="progressPercent" class="text-xs font-bold text-pink-300">0%</span>
                    </div>
                    <div class="w-full bg-slate-900/80 h-2.5 rounded-full overflow-hidden p-0.5 border border-purple-900/50 mb-2">
                        <div id="progressBar" class="bg-gradient-to-r from-pink-500 via-purple-500 to-indigo-500 h-full rounded-full transition-all duration-500" style="width: 0%;"></div>
                    </div>
                    <div class="flex justify-between text-[11px] text-slate-400">
                        <span id="answeredStatsText">已解鎖: 0 題</span>
                        <span id="favoriteStatsText">最愛: 0 題</span>
                    </div>

                    <div class="grid grid-cols-2 gap-2 mt-4">
                        <button id="openDrawerBtn" class="glass-card hover:bg-purple-900/40 text-purple-200 py-2.5 px-3 rounded-xl text-xs font-medium flex items-center justify-center gap-1.5 transition">
                            <i class="fa-solid fa-list-check text-pink-400"></i>
                            <span>100題總清單</span>
                        </button>
                        <button id="randomPickBtn" class="glass-card hover:bg-purple-900/40 text-indigo-200 py-2.5 px-3 rounded-xl text-xs font-medium flex items-center justify-center gap-1.5 transition">
                            <i class="fa-solid fa-bolt text-amber-300"></i>
                            <span>速抽扭蛋</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- 中央扭蛋機 (Gachapon Machine) -->
            <div class="flex flex-col items-center justify-center order-1 lg:order-2">
                <div class="relative flex flex-col items-center">
                    
                    <!-- 頂部：包著尿布吸奶嘴的小豬頭頂飾 -->
                    <div class="relative -mb-6 z-20 flex flex-col items-center">
                        <!-- 雙耳朵 -->
                        <div class="absolute -top-3 left-3 w-8 h-8 bg-pink-400 rounded-full border-2 border-white transform -rotate-30"></div>
                        <div class="absolute -top-3 right-3 w-8 h-8 bg-pink-400 rounded-full border-2 border-white transform rotate-30"></div>
                        
                        <!-- 小豬大頭 -->
                        <div class="w-32 h-20 bg-gradient-to-b from-pink-300 to-pink-400 rounded-t-full border-4 border-pink-200 flex flex-col items-center justify-end pb-1 shadow-lg relative">
                            <!-- 豬眼睛 -->
                            <div class="flex items-center gap-6 mb-1">
                                <div class="w-2.5 h-3 bg-slate-900 rounded-full"></div>
                                <div class="w-2.5 h-3 bg-slate-900 rounded-full"></div>
                            </div>
                            <!-- 豬鼻子 + 嘴巴吸著藍色奶嘴 -->
                            <div class="relative flex items-center justify-center">
                                <div class="w-9 h-6 bg-pink-200 rounded-full border border-pink-500 flex items-center justify-center gap-1">
                                    <div class="w-1.5 h-2 bg-pink-600 rounded-full"></div>
                                    <div class="w-1.5 h-2 bg-pink-600 rounded-full"></div>
                                </div>
                                <!-- 吸着的奶嘴 (Pacifier) -->
                                <div class="absolute -bottom-2 z-10 flex flex-col items-center">
                                    <div class="w-6 h-4 bg-sky-400 rounded-full border-2 border-white shadow"></div>
                                    <div class="w-3 h-3 border-2 border-sky-300 rounded-full -mt-1"></div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- 扭蛋機主體 -->
                    <div class="gacha-machine-body w-[310px] sm:w-[350px] p-5 pt-8 rounded-[40px] flex flex-col items-center relative shadow-2xl">

                        <!-- 扭蛋玻璃穹頂 -->
                        <div class="gacha-dome relative w-full h-[220px] sm:h-[240px] rounded-3xl overflow-hidden mb-4">
                            <canvas id="gachaCanvas" width="310" height="240" class="w-full h-full"></canvas>
                        </div>

                        <!-- 下半部：可愛尿布造型區 (Diaper Area) -->
                        <div class="diaper-body w-full rounded-3xl p-3 relative flex items-center justify-between">
                            
                            <!-- 尿布左側可愛安全別針裝飾 -->
                            <div class="absolute -left-2 top-2 bg-pink-400 text-white w-6 h-6 rounded-full border-2 border-white flex items-center justify-center text-[10px] shadow transform -rotate-12">
                                🧷
                            </div>
                            <div class="absolute -right-2 top-2 bg-pink-400 text-white w-6 h-6 rounded-full border-2 border-white flex items-center justify-center text-[10px] shadow transform rotate-12">
                                🧷
                            </div>

                            <!-- 小豬旋鈕按鈕 -->
                            <div class="flex flex-col items-center pl-2">
                                <button id="spinBtn" class="piggy-knob relative w-20 h-20 rounded-full border-4 border-white/90 flex flex-col items-center justify-center cursor-pointer group active:scale-95">
                                    <!-- 豬鼻子 (旋鈕中心) -->
                                    <div class="w-10 h-7 bg-pink-200 rounded-full border-2 border-pink-400 flex items-center justify-center gap-1 shadow-inner">
                                        <div class="w-2 h-3 bg-pink-500/80 rounded-full"></div>
                                        <div class="w-2 h-3 bg-pink-500/80 rounded-full"></div>
                                    </div>
                                    <span class="text-[10px] font-bold text-white mt-0.5 tracking-tighter drop-shadow">轉動小豬</span>
                                </button>
                            </div>

                            <!-- 扭蛋出口槽 -->
                            <div class="relative w-28 h-24 bg-slate-900 rounded-2xl border-2 border-pink-300 p-2 flex items-center justify-center overflow-hidden shadow-inner">
                                <div class="absolute top-0 inset-x-0 h-3 bg-slate-950 border-b border-slate-800"></div>
                                <!-- 滾落的扭蛋球置放處 -->
                                <div id="chuteGachaArea" class="relative z-10 w-14 h-14 flex items-center justify-center cursor-pointer">
                                    <span class="text-xs text-purple-300/50 text-center leading-tight">扭蛋出口</span>
                                </div>
                            </div>

                        </div>

                        <p class="text-[11px] text-purple-200/80 mt-3 flex items-center gap-1.5">
                            <i class="fa-solid fa-hand-pointer text-pink-300"></i>
                            <span>點擊「尿布旋鈕」扭一顆話題扭蛋！</span>
                        </p>
                    </div>
                </div>
            </div>

        </div>
    </main>

    <!-- 頁腳 -->
    <footer class="relative z-10 text-center py-4 text-xs text-purple-300/60">
        <p>小豬與小豬寶寶的睡前talk ‧ 願今晚每個話題都化作最甜的夢境 🌙</p>
    </footer>

    <!-- 抽中話題 (開扭蛋) Modal -->
    <div id="resultModal" class="modal hidden-modal fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-950/80 backdrop-blur-md">
        <div class="modal-content glass-panel max-w-md w-full rounded-3xl p-6 sm:p-8 relative text-center border border-pink-400/40 shadow-2xl shadow-purple-950/80">
            <button id="closeModalBtn" class="absolute top-4 right-4 w-9 h-9 rounded-full bg-slate-800/80 text-slate-300 hover:text-white flex items-center justify-center transition">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <!-- 扭蛋彈出圖標展示 -->
            <div class="relative mx-auto w-28 h-28 mb-3">
                <!-- 包尿布吸奶嘴小豬大扭蛋球 -->
                <div class="w-28 h-28 rounded-full border-4 border-pink-200 overflow-hidden shadow-2xl shadow-pink-500/40 mx-auto relative bg-gradient-to-b from-pink-300 via-pink-400 to-white flex flex-col items-center justify-between p-1">
                    <!-- 豬耳朵裝飾 -->
                    <div class="absolute top-1 left-2 w-5 h-5 bg-pink-500 rounded-full border border-white transform -rotate-12"></div>
                    <div class="absolute top-1 right-2 w-5 h-5 bg-pink-500 rounded-full border border-white transform rotate-12"></div>
                    
                    <!-- 中央照片 -->
                    <div class="w-16 h-16 rounded-full border-2 border-white overflow-hidden z-10 mt-1 shadow">
                        <img src="image_fabfe5.jpg" alt="扭蛋相片" class="w-full h-full object-cover" onerror="this.src='https://placehold.co/100x100/ec4899/ffffff?text=Piggy'">
                    </div>

                    <!-- 豬鼻子與奶嘴裝飾 -->
                    <div class="z-10 flex items-center justify-center -mt-3">
                        <div class="w-6 h-4 bg-sky-400 rounded-full border border-white shadow flex items-center justify-center">
                            <div class="w-2 h-2 border border-white rounded-full"></div>
                        </div>
                    </div>

                    <!-- 尿布底座區 -->
                    <div class="w-full h-6 bg-white rounded-b-full border-t border-pink-300 flex items-center justify-center text-[10px] text-pink-400 font-bold z-0">
                        👶 尿布小豬
                    </div>
                </div>
                <div class="absolute -bottom-1 -right-1 bg-pink-500 text-white w-8 h-8 rounded-full border-2 border-white flex items-center justify-center text-sm shadow">
                    🎁
                </div>
            </div>

            <div class="mb-2">
                <span id="modalCategoryTag" class="inline-block bg-pink-500/20 text-pink-300 border border-pink-400/40 rounded-full px-3.5 py-1 text-xs font-medium">
                    01｜日常生活篇
                </span>
            </div>

            <div class="my-4 min-h-[90px] flex items-center justify-center px-2">
                <h3 id="modalQuestionText" class="text-xl sm:text-2xl font-bold text-white leading-relaxed tracking-wide">
                    「最近發生最開心的一件事是什麼？」
                </h3>
            </div>

            <!-- Modal 按鈕操作 -->
            <div class="flex items-center justify-center gap-3 mb-6">
                <button id="modalToggleFavBtn" class="px-4 py-2 rounded-xl bg-slate-800 border border-slate-700 text-slate-300 hover:text-rose-400 text-xs font-medium transition flex items-center gap-1.5">
                    <i class="fa-regular fa-heart text-rose-400"></i>
                    <span id="modalFavText">收藏</span>
                </button>
                <button id="modalToggleAnsweredBtn" class="px-4 py-2 rounded-xl bg-slate-800 border border-slate-700 text-slate-300 hover:text-emerald-400 text-xs font-medium transition flex items-center gap-1.5">
                    <i class="fa-regular fa-circle-check text-emerald-400"></i>
                    <span id="modalAnsweredText">標記已聊過</span>
                </button>
            </div>

            <div class="flex items-center justify-center">
                <button id="spinAgainModalBtn" class="w-full bg-gradient-to-r from-pink-500 via-purple-500 to-indigo-600 hover:from-pink-400 hover:to-indigo-500 text-white font-bold py-3.5 px-6 rounded-2xl text-sm transition shadow-lg shadow-pink-950/50 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-rotate-right"></i>
                    <span>再扭一顆話題扭蛋</span>
                </button>
            </div>
        </div>
    </div>

    <!-- 100 題總清單 Modal / Drawer -->
    <div id="drawerModal" class="modal hidden-modal fixed inset-0 z-50 flex items-end sm:items-center justify-center p-0 sm:p-4 bg-slate-950/80 backdrop-blur-md">
        <div class="modal-content glass-panel w-full sm:max-w-3xl h-[88vh] sm:h-[82vh] rounded-t-3xl sm:rounded-3xl flex flex-col border border-purple-500/30 shadow-2xl overflow-hidden">
            <div class="p-4 sm:p-5 border-b border-purple-500/20 flex items-center justify-between bg-slate-900/80">
                <div>
                    <h2 class="text-base sm:text-lg font-bold text-white flex items-center gap-2">
                        <i class="fa-solid fa-book-bookmark text-pink-400"></i>
                        <span>100 題話題庫總覽</span>
                    </h2>
                    <p class="text-xs text-purple-300/70 mt-0.5">點擊直接選擇話題或標記完成進度</p>
                </div>
                <button id="closeDrawerBtn" class="w-9 h-9 rounded-full bg-slate-800 text-slate-300 hover:text-white flex items-center justify-center transition">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div id="questionsList" class="flex-1 overflow-y-auto p-4 space-y-2.5">
                <!-- 動態生成題目列表 -->
            </div>

            <div class="p-3 bg-slate-900/90 border-t border-purple-900/40 text-center text-xs text-purple-300/70 flex items-center justify-between px-5">
                <span id="drawerProgressText">已完成 0 / 100 題</span>
                <button id="resetProgressBtn" class="text-rose-400 hover:text-rose-300 underline font-medium">重置所有紀錄</button>
            </div>
        </div>
    </div>

    <!-- 核心 JavaScript 邏輯與扭蛋物理動畫 -->
    <script>
        // --- 100 題話題完整資料 ---
        const CATEGORIES = [
            { id: 'all', name: '全部話題 (100題)', icon: 'fa-border-all' },
            { id: 0, name: '01｜日常生活篇', color: '#EC4899', icon: 'fa-mug-hot' },
            { id: 1, name: '02｜個人內心篇', color: '#8B5CF6', icon: 'fa-user-astronaut' },
            { id: 2, name: '03｜小豬與小豬寶寶的專屬記憶', color: '#F43F5E', icon: 'fa-heart' },
            { id: 3, name: '04｜感情觀與相處篇', color: '#3B82F6', icon: 'fa-comments' },
            { id: 4, name: '05｜假設與腦洞篇', color: '#10B981', icon: 'fa-lightbulb' },
            { id: 5, name: '06｜未來與夢想篇', color: '#F59E0B', icon: 'fa-compass' },
            { id: 6, name: '07｜睡前輕鬆小問題', color: '#6366F1', icon: 'fa-bed' }
        ];

        const RAW_QUESTIONS = [
            // 01｜日常生活篇 (1-15)
            "最近發生最開心的一件事是什麼？",
            "最近有沒有什麼事情讓你覺得很煩？",
            "如果最近的生活可以重新安排，你會想改變什麼？",
            "最近有沒有哪個瞬間突然想到我？",
            "最近有什麼事情一直想做卻還沒做？",
            "你最近最期待的一件事是什麼？",
            "如果明天不用上班或上課，你最想做什麼？",
            "你覺得自己最近有什麼改變？",
            "最近有沒有聽到一首很喜歡的歌？",
            "你最近最常煩惱的事情是什麼？",
            "如果可以立刻吃到一道料理，你會選什麼？",
            "你覺得自己是早睡派還是夜貓子？",
            "最近有沒有什麼小事讓你特別感動？",
            "最近有沒有什麼事情很想跟我分享，卻還沒找到機會？",
            "如果幫最近的生活打分數，你會給幾分？",

            // 02｜個人內心篇 (16-30)
            "你小時候最想成為什麼樣的人？",
            "小時候做過最調皮的事情是什麼？",
            "你覺得自己最大的優點是什麼？",
            "有沒有一個別人不知道的小習慣？",
            "你最不能接受別人對你做什麼？",
            "你生氣的時候，希望別人怎麼對待你？",
            "你是一個容易心軟的人嗎？",
            "你覺得自己最像哪種動物？",
            "你最喜歡自己哪個個性？",
            "你有沒有什麼一直想嘗試卻不敢做的事？",
            "你覺得自己是理性還是感性的人？",
            "你最珍惜人生中的哪一段時光？",
            "有沒有一件事情是你長大後才明白的？",
            "你最希望別人理解你哪個部分？",
            "如果要用三個詞形容自己，你會選什麼？",

            // 03｜小豬與小豬寶寶的專屬記憶 (31-45)
            "你對我們最初的印象是什麼？",
            "你覺得我們第一次相處和現在最大的差別是什麼？",
            "你最喜歡我們一起做過的哪件事？",
            "有沒有哪個我們的回憶，你特別想再經歷一次？",
            "你覺得我們誰比較容易鬧脾氣？",
            "你覺得我們最像的地方是什麼？",
            "我有沒有做過什麼讓你印象特別深刻的事情？",
            "你覺得我們最有默契的一次是什麼時候？",
            "如果把我們的相處拍成電影，你會取什麼名字？",
            "你覺得我們一起完成過最有成就感的事情是什麼？",
            "有沒有哪次相處讓你覺得時間過得特別快？",
            "你覺得我們之間有什麼只有彼此懂的梗？",
            "如果可以回到我們認識的第一天，你想對當時的自己說什麼？",
            "你覺得我們還有哪些事情沒有一起完成？",
            "你想把哪一天特別記錄下來？",

            // 04｜感情觀與相處篇 (46-60)
            "你認為一段好的關係最重要的是什麼？",
            "你覺得兩個人需要每天聊天嗎？",
            "你認為吵架後誰應該先開口？",
            "你比較喜歡直接表達，還是用行動表示在乎？",
            "你覺得什麼樣的陪伴最有意義？",
            "你認為兩個人需要保留多少自己的空間？",
            "你覺得什麼樣的溝通方式最有效？",
            "如果我們對一件事情有不同看法，你希望怎麼處理？",
            "你覺得信任是怎麼慢慢建立的？",
            "你認為兩個人應該有共同興趣嗎？",
            "你覺得怎樣才算真正理解一個人？",
            "你比較重視紀念日還是平常的小驚喜？",
            "你覺得陪伴和陪著做自己的事情有什麼不同？",
            "你希望別人怎麼尊重你的界線？",
            "你覺得一段健康的關係應該帶給彼此什麼？",

            // 05｜假設與腦洞篇 (61-75)
            "如果我們可以瞬間移動，你想去哪裡？",
            "如果中了1000萬，你第一件事會做什麼？",
            "如果可以回到任何一個年紀，你會選幾歲？",
            "如果可以擁有一種超能力，你會選什麼？",
            "如果可以和任何歷史人物吃飯，你會選誰？",
            "如果明天世界只剩下一種食物，你希望是什麼？",
            "如果可以在任何國家生活一年，你會去哪裡？",
            "如果我們可以一起開一家店，你想開什麼？",
            "如果可以交換一天的生活，你最想體驗什麼？",
            "如果要在荒島生活一個月，你會帶哪三樣東西？",
            "如果可以重新學會一項技能，你會選什麼？",
            "如果可以擁有一間夢想中的房子，你會怎麼設計？",
            "如果人生可以配背景音樂，你希望自己的主題曲是什麼？",
            "如果可以拍一部紀錄片，你想記錄什麼？",
            "如果有一張免費環遊世界的機票，你第一站會去哪？",

            // 06｜未來與夢想篇 (76-90)
            "你希望五年後的自己正在做什麼？",
            "你最想完成的人生目標是什麼？",
            "你理想中的退休生活是什麼樣子？",
            "你想在哪個城市長期生活？",
            "你希望未來的生活步調快還是慢？",
            "你最想帶家人去哪裡旅行？",
            "你有沒有一個一直沒實現的夢想？",
            "如果不考慮金錢，你最想從事什麼工作？",
            "你希望自己老了以後是什麼樣的人？",
            "你最想培養哪一種生活習慣？",
            "你想學會什麼語言？",
            "你希望未來的家裡有什麼特別的設計？",
            "你想挑戰一次什麼人生經歷？",
            "你覺得怎樣才算過著自己想要的人生？",
            "如果可以寫一封信給十年後的自己，你會寫什麼？",

            // 07｜睡前輕鬆小問題 (91-100)
            "如果現在可以吃宵夜，你會選什麼？",
            "你睡覺一定要抱著東西嗎？",
            "你睡覺會不會說夢話？",
            "你最喜歡什麼天氣？",
            "如果明天可以放假，你會睡到幾點？",
            "你最喜歡哪一種季節？",
            "你覺得自己洗澡時最常想什麼？",
            "如果可以養任何一種動物，你會養什麼？",
            "你最近最想買的東西是什麼？",
            "如果現在只能問對方一個問題，你最想問什麼？"
        ];

        const ALL_QUESTIONS = RAW_QUESTIONS.map((text, idx) => {
            let catId = 0;
            if (idx >= 15 && idx < 30) catId = 1;
            else if (idx >= 30 && idx < 45) catId = 2;
            else if (idx >= 45 && idx < 60) catId = 3;
            else if (idx >= 60 && idx < 75) catId = 4;
            else if (idx >= 75 && idx < 90) catId = 5;
            else if (idx >= 90) catId = 6;

            const categoryObj = CATEGORIES.find(c => c.id === catId);
            return {
                id: idx + 1,
                text: text,
                categoryId: catId,
                categoryName: categoryObj.name,
                color: categoryObj.color
            };
        });

        // --- 狀態控制 ---
        let answeredQuestions = new Set(JSON.parse(localStorage.getItem('piggy_talk_answered') || '[]'));
        let favoriteQuestions = new Set(JSON.parse(localStorage.getItem('piggy_talk_favorites') || '[]'));
        let currentCategory = 'all';
        let currentSelectedQuestion = null;
        let isOperating = false;

        // 音效系統
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

        function playGachaClack() {
            if (audioCtx.state === 'suspended') audioCtx.resume();
            try {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(320, audioCtx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(80, audioCtx.currentTime + 0.08);
                gain.gain.setValueAtTime(0.3, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.08);
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start();
                osc.stop(audioCtx.currentTime + 0.08);
            } catch(e){}
        }

        function playWinSound() {
            if (audioCtx.state === 'suspended') audioCtx.resume();
            try {
                const now = audioCtx.currentTime;
                const notes = [523.25, 659.25, 783.99, 1046.50]; // C Major Chord
                notes.forEach((freq, idx) => {
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(freq, now + idx * 0.08);
                    gain.gain.setValueAtTime(0, now + idx * 0.08);
                    gain.gain.linearRampToValueAtTime(0.2, now + idx * 0.08 + 0.02);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + idx * 0.08 + 0.5);
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    osc.start(now + idx * 0.08);
                    osc.stop(now + idx * 0.08 + 0.5);
                });
            } catch(e){}
        }

        // --- 扭蛋物理動畫 Canvas 實現 ---
        const gachaCanvas = document.getElementById('gachaCanvas');
        const gachaCtx = gachaCanvas.getContext('2d');
        const userImg = new Image();
        userImg.src = 'image_fabfe5.jpg';

        const BALL_COLORS = ['#f472b6', '#fb7185', '#ec4899', '#f43f5e', '#f472b6'];
        let gachaBalls = [];

        function initGachaBalls() {
            gachaBalls = [];
            const count = 16;
            for (let i = 0; i < count; i++) {
                gachaBalls.push({
                    x: Math.random() * (gachaCanvas.width - 60) + 30,
                    y: Math.random() * (gachaCanvas.height - 70) + 35,
                    radius: 22, // 稍微加大以容納耳朵與尿布裝飾
                    vx: (Math.random() - 0.5) * 1.5,
                    vy: (Math.random() - 0.5) * 1.5,
                    color: BALL_COLORS[i % BALL_COLORS.length]
                });
            }
        }

        function renderGachaDome() {
            gachaCtx.clearRect(0, 0, gachaCanvas.width, gachaCanvas.height);

            gachaBalls.forEach(ball => {
                // 物理邊界反彈
                ball.x += ball.vx;
                ball.y += ball.vy;

                if (ball.x - ball.radius < 10 || ball.x + ball.radius > gachaCanvas.width - 10) ball.vx *= -1;
                if (ball.y - ball.radius < 10 || ball.y + ball.radius > gachaCanvas.height - 15) ball.vy *= -1;

                gachaCtx.save();
                
                // 1. 畫耳朵 (Ears)
                gachaCtx.fillStyle = '#ec4899';
                gachaCtx.beginPath();
                gachaCtx.arc(ball.x - 14, ball.y - 14, 6, 0, Math.PI * 2);
                gachaCtx.arc(ball.x + 14, ball.y - 14, 6, 0, Math.PI * 2);
                gachaCtx.fill();

                // 2. 畫粉紅小豬頭部本體 (Piggy Ball Head)
                gachaCtx.beginPath();
                gachaCtx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
                gachaCtx.fillStyle = ball.color;
                gachaCtx.fill();
                gachaCtx.lineWidth = 1.5;
                gachaCtx.strokeStyle = '#ffffff';
                gachaCtx.stroke();

                // 3. 畫尿布下半部 (Diaper Bottom)
                gachaCtx.beginPath();
                gachaCtx.arc(ball.x, ball.y, ball.radius, 0.15 * Math.PI, 0.85 * Math.PI, false);
                gachaCtx.lineTo(ball.x - ball.radius * 0.8, ball.y + 6);
                gachaCtx.fillStyle = '#ffffff';
                gachaCtx.fill();

                // 4. 裁切中間圓形放置相片
                gachaCtx.save();
                gachaCtx.beginPath();
                gachaCtx.arc(ball.x, ball.y - 2, ball.radius - 8, 0, Math.PI * 2);
                gachaCtx.clip();

                if (userImg.complete && userImg.naturalWidth > 0) {
                    gachaCtx.drawImage(userImg, ball.x - (ball.radius - 8), ball.y - 2 - (ball.radius - 8), (ball.radius - 8) * 2, (ball.radius - 8) * 2);
                } else {
                    gachaCtx.fillStyle = '#fce7f3';
                    gachaCtx.fill();
                }
                gachaCtx.restore();

                // 5. 畫嘴巴吸著的藍色奶嘴 (Pacifier)
                gachaCtx.beginPath();
                gachaCtx.arc(ball.x, ball.y + 11, 4, 0, Math.PI * 2);
                gachaCtx.fillStyle = '#38bdf8';
                gachaCtx.fill();
                gachaCtx.strokeStyle = '#ffffff';
                gachaCtx.lineWidth = 1;
                gachaCtx.stroke();

                // 6. 球面立體光澤 (Highlight)
                gachaCtx.beginPath();
                gachaCtx.arc(ball.x - 7, ball.y - 10, 4, 0, Math.PI * 2);
                gachaCtx.fillStyle = 'rgba(255, 255, 255, 0.5)';
                gachaCtx.fill();

                gachaCtx.restore();
            });

            requestAnimationFrame(renderGachaDome);
        }

        function shakeBalls() {
            gachaBalls.forEach(ball => {
                ball.vx = (Math.random() - 0.5) * 16;
                ball.vy = (Math.random() - 0.5) * 16;
            });
        }

        // --- 元素抓取 ---
        const spinBtn = document.getElementById('spinBtn');
        const chuteGachaArea = document.getElementById('chuteGachaArea');
        const filterAnswered = document.getElementById('filterAnswered');
        const filterFavorites = document.getElementById('filterFavorites');
        const poolStatusBadge = document.getElementById('poolStatusBadge');
        const progressBar = document.getElementById('progressBar');
        const progressPercent = document.getElementById('progressPercent');
        const answeredStatsText = document.getElementById('answeredStatsText');
        const favoriteStatsText = document.getElementById('favoriteStatsText');
        const categoryTabs = document.getElementById('categoryTabs');

        const resultModal = document.getElementById('resultModal');
        const closeModalBtn = document.getElementById('closeModalBtn');
        const modalCategoryTag = document.getElementById('modalCategoryTag');
        const modalQuestionText = document.getElementById('modalQuestionText');
        const modalToggleFavBtn = document.getElementById('modalToggleFavBtn');
        const modalFavText = document.getElementById('modalFavText');
        const modalToggleAnsweredBtn = document.getElementById('modalToggleAnsweredBtn');
        const modalAnsweredText = document.getElementById('modalAnsweredText');
        const spinAgainModalBtn = document.getElementById('spinAgainModalBtn');

        const openDrawerBtn = document.getElementById('openDrawerBtn');
        const randomPickBtn = document.getElementById('randomPickBtn');
        const drawerModal = document.getElementById('drawerModal');
        const closeDrawerBtn = document.getElementById('closeDrawerBtn');
        const questionsList = document.getElementById('questionsList');
        const drawerProgressText = document.getElementById('drawerProgressText');
        const resetProgressBtn = document.getElementById('resetProgressBtn');

        // --- 頁籤與資料庫過濾 ---
        function renderCategoryTabs() {
            categoryTabs.innerHTML = '';
            CATEGORIES.forEach(cat => {
                const btn = document.createElement('button');
                const isActive = currentCategory === cat.id;
                btn.className = `px-3.5 py-1.5 rounded-xl text-xs font-medium transition flex items-center gap-1.5 cursor-pointer ${
                    isActive 
                        ? 'bg-gradient-to-r from-pink-500 to-indigo-600 text-white shadow-md shadow-pink-950/40' 
                        : 'bg-purple-950/50 text-purple-200/80 hover:bg-purple-900/50'
                }`;
                btn.innerHTML = `<i class="fa-solid ${cat.icon} ${isActive ? 'text-white' : 'text-pink-300'}"></i><span>${cat.name}</span>`;
                btn.addEventListener('click', () => {
                    currentCategory = cat.id;
                    renderCategoryTabs();
                    updatePoolBadge();
                });
                categoryTabs.appendChild(btn);
            });
        }

        function getFilteredPool() {
            let pool = ALL_QUESTIONS;
            if (currentCategory !== 'all') pool = pool.filter(q => q.categoryId === currentCategory);
            if (filterFavorites.checked) pool = pool.filter(q => favoriteQuestions.has(q.id));
            if (filterAnswered.checked) pool = pool.filter(q => !answeredQuestions.has(q.id));
            return pool;
        }

        function updatePoolBadge() {
            const pool = getFilteredPool();
            poolStatusBadge.textContent = `${pool.length} 題可用`;
        }

        function updateStats() {
            const total = ALL_QUESTIONS.length;
            const answeredCount = answeredQuestions.size;
            const favCount = favoriteQuestions.size;
            const percent = Math.round((answeredCount / total) * 100);

            progressBar.style.width = `${percent}%`;
            progressPercent.textContent = `${percent}%`;
            answeredStatsText.textContent = `已解鎖: ${answeredCount} 題`;
            favoriteStatsText.textContent = `最愛: ${favCount} 題`;
            drawerProgressText.textContent = `已完成 ${answeredCount} / ${total} 題`;

            localStorage.setItem('piggy_talk_answered', JSON.stringify(Array.from(answeredQuestions)));
            localStorage.setItem('piggy_talk_favorites', JSON.stringify(Array.from(favoriteQuestions)));
        }

        // --- 轉動小豬旋鈕抽扭蛋 ---
        function operateGachapon() {
            if (isOperating) return;
            const pool = getFilteredPool();
            if (pool.length === 0) {
                alert("目前條件下沒有符合的話題扭蛋，請調整篩選設定！");
                return;
            }

            isOperating = true;
            spinBtn.classList.add('spinning');
            playGachaClack();
            shakeBalls();

            // 清空出口區域
            chuteGachaArea.innerHTML = '';

            setTimeout(() => {
                spinBtn.classList.remove('spinning');
                
                // 產生滾落掉出的扭蛋球
                const pickedQuestion = pool[Math.floor(Math.random() * pool.length)];
                currentSelectedQuestion = pickedQuestion;

                const droppedBall = document.createElement('div');
                droppedBall.className = 'gacha-drop-anim w-12 h-12 rounded-full border-2 border-white shadow-lg overflow-hidden cursor-pointer relative bg-slate-900';
                droppedBall.innerHTML = `
                    <img src="image_fabfe5.jpg" class="w-full h-full object-cover" onerror="this.src='https://placehold.co/100x100/ec4899/ffffff?text=Piggy'">
                    <div class="absolute inset-0 bg-pink-500/20"></div>
                `;

                droppedBall.addEventListener('click', () => {
                    showResultModal(pickedQuestion);
                    playWinSound();
                    chuteGachaArea.innerHTML = '<span class="text-xs text-purple-300/50 text-center leading-tight">扭蛋出口</span>';
                    isOperating = false;
                });

                chuteGachaArea.appendChild(droppedBall);

                // 自動延遲彈出
                setTimeout(() => {
                    if (chuteGachaArea.contains(droppedBall)) {
                        droppedBall.click();
                    }
                }, 900);

            }, 700);
        }

        // --- 彈窗顯示話題結果 ---
        function showResultModal(question) {
            currentSelectedQuestion = question;
            modalCategoryTag.textContent = question.categoryName;
            modalQuestionText.textContent = `「${question.text}」`;
            updateModalButtonStates();
            resultModal.classList.remove('hidden-modal');
        }

        function updateModalButtonStates() {
            if (!currentSelectedQuestion) return;
            const isFav = favoriteQuestions.has(currentSelectedQuestion.id);
            const isAns = answeredQuestions.has(currentSelectedQuestion.id);

            if (isFav) {
                modalToggleFavBtn.className = "px-4 py-2 rounded-xl bg-rose-500/20 border border-rose-500/50 text-rose-300 text-xs font-medium transition flex items-center gap-1.5";
                modalToggleFavBtn.querySelector('i').className = "fa-solid fa-heart text-rose-400";
                modalFavText.textContent = "已收藏";
            } else {
                modalToggleFavBtn.className = "px-4 py-2 rounded-xl bg-slate-800 border border-slate-700 text-slate-300 hover:text-rose-400 text-xs font-medium transition flex items-center gap-1.5";
                modalToggleFavBtn.querySelector('i').className = "fa-regular fa-heart text-rose-400";
                modalFavText.textContent = "收藏";
            }

            if (isAns) {
                modalToggleAnsweredBtn.className = "px-4 py-2 rounded-xl bg-emerald-500/20 border border-emerald-500/50 text-emerald-300 text-xs font-medium transition flex items-center gap-1.5";
                modalToggleAnsweredBtn.querySelector('i').className = "fa-solid fa-circle-check text-emerald-400";
                modalAnsweredText.textContent = "已聊過";
            } else {
                modalToggleAnsweredBtn.className = "px-4 py-2 rounded-xl bg-slate-800 border border-slate-700 text-slate-300 hover:text-emerald-400 text-xs font-medium transition flex items-center gap-1.5";
                modalToggleAnsweredBtn.querySelector('i').className = "fa-regular fa-circle-check text-emerald-400";
                modalAnsweredText.textContent = "標記已聊過";
            }
        }

        function closeModal() {
            resultModal.classList.add('hidden-modal');
            isOperating = false;
        }

        // --- 100 題總清單 Drawer ---
        function renderDrawerList() {
            questionsList.innerHTML = '';
            ALL_QUESTIONS.forEach(q => {
                const isAns = answeredQuestions.has(q.id);
                const isFav = favoriteQuestions.has(q.id);

                const item = document.createElement('div');
                item.className = `glass-card p-3.5 rounded-2xl flex items-center justify-between gap-3 transition ${isAns ? 'opacity-60 border-l-4 border-l-emerald-500' : ''}`;

                item.innerHTML = `
                    <div class="flex items-center gap-3 flex-1 min-w-0">
                        <button class="ans-toggle-btn text-lg ${isAns ? 'text-emerald-400' : 'text-slate-600 hover:text-slate-400'}" data-id="${q.id}">
                            <i class="${isAns ? 'fa-solid fa-circle-check' : 'fa-regular fa-circle'}"></i>
                        </button>
                        <div class="truncate flex-1">
                            <span class="text-[10px] px-2 py-0.5 rounded-full bg-slate-800 text-purple-200 font-medium border border-purple-500/30 mr-1.5">${q.categoryName.split('｜')[0]}</span>
                            <span class="text-xs sm:text-sm font-medium ${isAns ? 'line-through text-slate-400' : 'text-slate-100'}">${q.id}. ${q.text}</span>
                        </div>
                    </div>
                    <div class="flex items-center gap-2 shrink-0">
                        <button class="fav-toggle-btn p-1.5 text-sm ${isFav ? 'text-rose-400' : 'text-slate-600 hover:text-rose-400'}" data-id="${q.id}">
                            <i class="${isFav ? 'fa-solid fa-heart' : 'fa-regular fa-heart'}"></i>
                        </button>
                        <button class="pick-single-btn text-xs bg-purple-500/20 hover:bg-purple-500/30 text-purple-200 px-2.5 py-1 rounded-xl border border-purple-400/30 transition" data-id="${q.id}">
                            看此題
                        </button>
                    </div>
                `;

                item.querySelector('.ans-toggle-btn').addEventListener('click', () => {
                    toggleAnswered(q.id);
                    renderDrawerList();
                });
                item.querySelector('.fav-toggle-btn').addEventListener('click', () => {
                    toggleFavorite(q.id);
                    renderDrawerList();
                });
                item.querySelector('.pick-single-btn').addEventListener('click', () => {
                    closeDrawerModal();
                    showResultModal(q);
                    playWinSound();
                });

                questionsList.appendChild(item);
            });
        }

        function toggleAnswered(id) {
            if (answeredQuestions.has(id)) answeredQuestions.delete(id);
            else answeredQuestions.add(id);
            updateStats();
            updatePoolBadge();
        }

        function toggleFavorite(id) {
            if (favoriteQuestions.has(id)) favoriteQuestions.delete(id);
            else favoriteQuestions.add(id);
            updateStats();
            updatePoolBadge();
        }

        function openDrawerModal() {
            renderDrawerList();
            drawerModal.classList.remove('hidden-modal');
        }

        function closeDrawerModal() {
            drawerModal.classList.add('hidden-modal');
        }

        // --- 建立夜空星光 ---
        function createStars() {
            const container = document.getElementById('stars-container');
            for (let i = 0; i < 50; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                const size = Math.random() * 2.8 + 1;
                star.style.width = `${size}px`;
                star.style.height = `${size}px`;
                star.style.top = `${Math.random() * 100}%`;
                star.style.left = `${Math.random() * 100}%`;
                star.style.setProperty('--duration', `${Math.random() * 3 + 2}s`);
                container.appendChild(star);
            }
        }

        // --- 初始化事件綁定 ---
        function initEvents() {
            spinBtn.addEventListener('click', operateGachapon);

            filterAnswered.addEventListener('change', updatePoolBadge);
            filterFavorites.addEventListener('change', updatePoolBadge);

            closeModalBtn.addEventListener('click', closeModal);
            spinAgainModalBtn.addEventListener('click', () => {
                closeModal();
                operateGachapon();
            });

            modalToggleFavBtn.addEventListener('click', () => {
                if (currentSelectedQuestion) {
                    toggleFavorite(currentSelectedQuestion.id);
                    updateModalButtonStates();
                }
            });

            modalToggleAnsweredBtn.addEventListener('click', () => {
                if (currentSelectedQuestion) {
                    toggleAnswered(currentSelectedQuestion.id);
                    updateModalButtonStates();
                }
            });

            openDrawerBtn.addEventListener('click', openDrawerModal);
            closeDrawerBtn.addEventListener('click', closeDrawerModal);

            randomPickBtn.addEventListener('click', () => {
                const pool = getFilteredPool();
                if (pool.length === 0) {
                    alert("目前條件下沒有符合的話題扭蛋！");
                    return;
                }
                const randomQ = pool[Math.floor(Math.random() * pool.length)];
                showResultModal(randomQ);
                playWinSound();
            });

            resetProgressBtn.addEventListener('click', () => {
                if (confirm("確定要重置所有話題的解答與收藏紀錄嗎？")) {
                    answeredQuestions.clear();
                    favoriteQuestions.clear();
                    updateStats();
                    updatePoolBadge();
                    renderDrawerList();
                }
            });

            resultModal.addEventListener('click', (e) => {
                if (e.target === resultModal) closeModal();
            });
            drawerModal.addEventListener('click', (e) => {
                if (e.target === drawerModal) closeDrawerModal();
            });
        }

        // 頁面載入
        window.onload = function () {
            createStars();
            renderCategoryTabs();
            updateStats();
