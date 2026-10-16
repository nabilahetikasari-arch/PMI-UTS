<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pythagoras Rescue Adventure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f7f2;
            color: #2d3748;
            touch-action: manipulation;
        }
        .game-card {
            background: #ffffff;
            border: 2px solid #e2e8f0;
            border-radius: 1rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
        }
        .btn-primary {
            background-color: #f97316;
            color: #ffffff;
            font-weight: 600;
            border-radius: 0.75rem;
            padding: 0.75rem 1.5rem;
            transition: all 0.2s ease;
            box-shadow: 0 4px 14px rgba(249, 115, 22, 0.3);
        }
        .btn-primary:hover {
            background-color: #ea580c;
        }
        .btn-secondary {
            background-color: #15803d;
            color: #ffffff;
            font-weight: 600;
            border-radius: 0.75rem;
            padding: 0.75rem 1.5rem;
            transition: all 0.2s ease;
            box-shadow: 0 4px 14px rgba(21, 128, 61, 0.3);
        }
        .btn-secondary:hover {
            background-color: #166534;
        }
        .draggable-square {
            cursor: grab;
            user-select: none;
            touch-action: none;
        }
        .draggable-square:active {
            cursor: grabbing;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between" onload="initApp()">

    <!-- Header -->
    <header class="bg-[#15803d] text-white shadow-md sticky top-0 z-50">
        <div class="max-w-4xl mx-auto px-4 py-3 flex flex-wrap justify-between items-center">
            <div class="flex items-center space-x-3">
                <div class="bg-white text-[#15803d] p-2 rounded-xl font-extrabold text-xl shadow-inner">
                    📐
                </div>
                <div>
                    <h1 class="font-extrabold text-base sm:text-lg tracking-wide">PYTHAGORAS RESCUE</h1>
                    <p class="text-xs text-emerald-100 font-medium">Petualangan Matematika SMP</p>
                </div>
            </div>
            <div class="flex items-center space-x-2">
                <div class="bg-[#166534] px-3 py-1.5 rounded-lg text-xs font-semibold flex items-center space-x-1 shadow-sm">
                    <span>🏆 Skor:</span>
                    <span id="header-total-score" class="text-orange-300 font-bold text-sm">0</span>
                    <span class="text-emerald-200">/ 950</span>
                </div>
                <button onclick="confirmReset()" class="bg-red-700 hover:bg-red-800 text-white text-xs px-3 py-1.5 rounded-lg font-semibold transition shadow-sm">
                    Ulangi
                </button>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-3xl w-full mx-auto p-4 sm:p-6 my-auto flex-grow flex flex-col justify-center">

        <!-- 1. WELCOME SCREEN -->
        <div id="screen-welcome" class="game-card p-6 sm:p-10 text-center space-y-6">
            <div class="max-w-md mx-auto">
                <div class="w-24 h-24 bg-emerald-100 text-[#15803d] rounded-full flex items-center justify-center mx-auto text-4xl shadow-inner mb-4">
                    🏫🏗️
                </div>
                <h2 class="text-2xl sm:text-3xl font-extrabold text-[#15803d]">Pythagoras Rescue Adventure</h2>
                <p class="text-gray-600 text-sm sm:text-base mt-2">
                    Selesaikan misi pembangunan dan penyelamatan fasilitas sekolah menggunakan Teorema Pythagoras secara mandiri!
                </p>
            </div>

            <div class="pt-2">
                <button onclick="startAdventure()" class="btn-primary text-base sm:text-lg px-8 py-3 shadow-lg">
                    🚀 Mulai Petualangan
                </button>
            </div>
        </div>

        <!-- 2. LEVEL 1: TRIANGLE EXPLORER -->
        <div id="screen-level1" class="game-card p-5 sm:p-8 space-y-6 hidden">
            <div class="flex justify-between items-center border-b pb-3">
                <div>
                    <span class="text-xs font-bold text-[#15803d] uppercase tracking-wider">Level 1 dari 4</span>
                    <h2 class="text-xl sm:text-2xl font-extrabold text-gray-800">Triangle Explorer</h2>
                </div>
                <span class="text-xs bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full font-semibold">Maks. 100 Poin</span>
            </div>

            <p class="text-xs sm:text-sm text-gray-600">
                Pilih bentuk geometri yang merupakan <b>segitiga siku-siku</b> di antara pilihan berikut:
            </p>

            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 py-2">
                <div onclick="selectLevel1Opt('A')" id="l1-opt-A" class="border-2 border-gray-200 bg-gray-50 rounded-xl p-4 text-center cursor-pointer hover:border-[#15803d] transition">
                    <svg viewBox="0 0 100 100" class="w-24 h-24 mx-auto fill-emerald-50 stroke-[#15803d] stroke-2">
                        <polygon points="15,85 85,85 15,15" />
                        <polyline points="15,70 30,70 30,85" fill="none" stroke="#15803d" stroke-width="1.5" />
                    </svg>
                    <span class="font-bold text-sm text-gray-700 mt-2 block">Bentuk A</span>
                </div>
                <div onclick="selectLevel1Opt('B')" id="l1-opt-B" class="border-2 border-gray-200 bg-gray-50 rounded-xl p-4 text-center cursor-pointer hover:border-[#15803d] transition">
                    <svg viewBox="0 0 100 100" class="w-24 h-24 mx-auto fill-emerald-50 stroke-[#15803d] stroke-2">
                        <polygon points="10,85 90,85 45,20" />
                    </svg>
                    <span class="font-bold text-sm text-gray-700 mt-2 block">Bentuk B</span>
                </div>
                <div onclick="selectLevel1Opt('C')" id="l1-opt-C" class="border-2 border-gray-200 bg-gray-50 rounded-xl p-4 text-center cursor-pointer hover:border-[#15803d] transition">
                    <svg viewBox="0 0 100 100" class="w-24 h-24 mx-auto fill-emerald-50 stroke-[#15803d] stroke-2">
                        <polygon points="20,85 80,85 50,15" />
                    </svg>
                    <span class="font-bold text-sm text-gray-700 mt-2 block">Bentuk C</span>
                </div>
            </div>

            <div id="feedback-l1" class="hidden p-3 rounded-lg text-sm font-medium text-center"></div>

            <div class="flex justify-end pt-2">
                <button onclick="submitLevel1()" class="btn-secondary">Konfirmasi Pilihan</button>
            </div>
        </div>

        <!-- 3. LEVEL 2: DISCOVER THE RULE -->
        <div id="screen-level2" class="game-card p-5 sm:p-8 space-y-6 hidden">
            <div class="flex justify-between items-center border-b pb-3">
                <div>
                    <span class="text-xs font-bold text-[#15803d] uppercase tracking-wider">Level 2 dari 4</span>
                    <h2 class="text-xl sm:text-2xl font-extrabold text-gray-800">Discover the Rule</h2>
                </div>
                <span class="text-xs bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full font-semibold">Maks. 150 Poin</span>
            </div>

            <p class="text-xs sm:text-sm text-gray-600">
                <b>Misi 1:</b> Tarik (drag) atau ketuk persegi di baki bawah lalu tempatkan pada sisi segitiga yang tepat.
            </p>

            <div class="bg-[#f7f7f2] border border-emerald-200 p-4 rounded-xl flex flex-col items-center justify-center space-y-3">
                <div class="relative w-full max-w-sm h-80 bg-white border border-gray-200 rounded-xl shadow-inner flex items-center justify-center p-2">
                    <svg viewBox="0 0 340 300" class="w-full h-full">
                        <!-- Segitiga Siku-Siku -->
                        <polygon points="120,120 120,220 220,220" fill="#fed7aa" stroke="#c2410c" stroke-width="2.5" />
                        <polyline points="120,200 140,200 140,220" fill="none" stroke="#c2410c" stroke-width="2" />
                        
                        <text x="160" y="155" font-size="12" font-weight="bold" fill="#2563eb">c = 5</text>
                        <text x="95" y="175" font-size="12" font-weight="bold" fill="#16a34a">b = 4</text>
                        <text x="165" y="238" font-size="12" font-weight="bold" fill="#dc2626">a = 3</text>

                        <!-- Square b=4 -->
                        <g id="svg-sq-4" class="opacity-0 transition-all duration-300">
                            <rect x="20" y="120" width="100" height="100" fill="#bbf7d0" stroke="#16a34a" stroke-width="2" rx="4" />
                        </g>

                        <!-- Square a=3 -->
                        <g id="svg-sq-3" class="opacity-0 transition-all duration-300">
                            <rect x="120" y="220" width="100" height="100" fill="#fecaca" stroke="#dc2626" stroke-width="2" rx="4" />
                        </g>

                        <!-- Square c=5 -->
                        <g id="svg-sq-5" class="opacity-0 transition-all duration-300">
                            <polygon points="120,120 220,220 320,120 220,20" fill="#bfdbfe" stroke="#2563eb" stroke-width="2" />
                        </g>
                    </svg>

                    <!-- Target Drop Zones -->
                    <div id="zone-3" ondragover="allowDrop(event)" ondrop="handleDrop(event, 3)" onclick="placeSquare(3)" class="absolute bottom-2 right-20 w-24 h-12 border-2 border-dashed border-red-400 bg-red-50/70 rounded flex items-center justify-center text-[10px] font-bold text-red-700 cursor-pointer">
                        <span id="label-zone-3">Sisi a=3</span>
                    </div>
                    <div id="zone-4" ondragover="allowDrop(event)" ondrop="handleDrop(event, 4)" onclick="placeSquare(4)" class="absolute left-2 top-28 w-12 h-24 border-2 border-dashed border-emerald-400 bg-emerald-50/70 rounded flex items-center justify-center text-[10px] font-bold text-emerald-700 cursor-pointer">
                        <span id="label-zone-4">Sisi b=4</span>
                    </div>
                    <div id="zone-5" ondragover="allowDrop(event)" ondrop="handleDrop(event, 5)" onclick="placeSquare(5)" class="absolute right-4 top-16 w-16 h-16 border-2 border-dashed border-blue-400 bg-blue-50/70 rounded flex items-center justify-center text-[10px] font-bold text-blue-700 cursor-pointer transform rotate-45">
                        <span id="label-zone-5" class="transform -rotate-45">Sisi c=5</span>
                    </div>
                </div>

                <!-- Tray for squares -->
                <div class="space-y-1.5 w-full max-w-sm text-center">
                    <p class="text-xs font-bold text-gray-700">Pilihan Persegi:</p>
                    <div class="flex justify-center gap-3">
                        <div id="sq-3" draggable="true" ondragstart="handleDragStart(event, 3)" onclick="selectSquareTray(3)" class="draggable-square w-12 h-12 bg-red-100 border-2 border-red-400 rounded-lg flex items-center justify-center text-xs font-bold text-red-800 shadow-sm">
                            a=3
                        </div>
                        <div id="sq-4" draggable="true" ondragstart="handleDragStart(event, 4)" onclick="selectSquareTray(4)" class="draggable-square w-12 h-12 bg-emerald-100 border-2 border-emerald-400 rounded-lg flex items-center justify-center text-xs font-bold text-emerald-800 shadow-sm">
                            b=4
                        </div>
                        <div id="sq-5" draggable="true" ondragstart="handleDragStart(event, 5)" onclick="selectSquareTray(5)" class="draggable-square w-12 h-12 bg-blue-100 border-2 border-blue-400 rounded-lg flex items-center justify-center text-xs font-bold text-blue-800 shadow-sm">
                            c=5
                        </div>
                    </div>
                </div>
            </div>

            <!-- Misi 2: Arahan Penemuan Rumus & Isian Luas -->
            <div id="level2-stage-b" class="space-y-4 pt-3 border-t hidden">
                <!-- Panduan Konseptual Penemuan Rumus & Hipotenusa -->
                <div class="bg-amber-50 border border-amber-200 p-4 rounded-xl space-y-2 text-xs sm:text-sm text-amber-900">
                    <h3 class="font-bold text-amber-900 text-sm sm:text-base flex items-center gap-1">
                        🔍 Arahan Penemuan Teorema Pythagoras:
                    </h3>
                    <p>
                        Perhatikan bentuk segitiga siku-siku dan ketiga persegi yang telah kamu susun di atas!
                    </p>
                    <ul class="list-disc list-inside space-y-1">
                        <li>
                            <b>Komponen Sisi Siku-Siku:</b> Sisi <span class="text-red-700 font-bold">a</span> dan sisi <span class="text-emerald-700 font-bold">b</span> adalah dua sisi tegak lurus yang membentuk sudut 90°.
                        </li>
                        <li>
                            <b>Hipotenusa (Sisi Miring):</b> Sisi <span class="text-blue-700 font-bold">c</span> dinamakan <b>Hipotenusa</b>, yaitu sisi terpanjang yang berada tepat di hadapan sudut siku-siku.
                        </li>
                        <li>
                            <b>Hubungan Luas Persegi:</b> Jika kamu menghitung luas persegi merah pada sisi <span class="text-red-700 font-bold">a</span> (<span class="italic">a²</span>) dan luas persegi hijau pada sisi <span class="text-emerald-700 font-bold">b</span> (<span class="italic">b²</span>), jumlah kedua luas persegi tersebut tepat sama dengan luas persegi biru pada hipotenusa <span class="text-blue-700 font-bold">c</span> (<span class="italic">c²</span>).
                        </li>
                    </ul>
                    <div class="bg-white/80 p-2.5 rounded-lg border border-amber-300 text-center font-bold text-amber-950 text-sm mt-2">
                        Rumus Teorema Pythagoras: <span class="text-orange-600 font-extrabold">a² + b² = c²</span>
                    </div>
                </div>

                <p class="text-xs sm:text-sm text-gray-600 font-medium">
                    <b>Misi 2:</b> Hitung dan masukkan luas masing-masing persegi berdasarkan panjang sisinya untuk membuktikan hubungan tersebut.
                </p>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-gray-700 mb-1">Luas Persegi Sisi a=3 (a²):</label>
                        <input type="number" id="input-l2-a" class="w-full border rounded-lg px-3 py-2 text-sm bg-white" placeholder="Luas persegi a...">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-gray-700 mb-1">Luas Persegi Sisi b=4 (b²):</label>
                        <input type="number" id="input-l2-b" class="w-full border rounded-lg px-3 py-2 text-sm bg-white" placeholder="Luas persegi b...">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-gray-700 mb-1">Luas Persegi Sisi c=5 (c²):</label>
                        <input type="number" id="input-l2-c" class="w-full border rounded-lg px-3 py-2 text-sm bg-white" placeholder="Luas persegi c...">
                    </div>
                </div>
            </div>

            <div id="feedback-l2" class="hidden p-3 rounded-lg text-sm font-medium text-center"></div>

            <div class="flex justify-end pt-2">
                <button onclick="submitLevel2()" class="btn-secondary">Periksa Jawaban</button>
            </div>
        </div>

        <!-- 4. LEVEL 3: PYTHAGORAS CHALLENGE -->
        <div id="screen-level3" class="game-card p-5 sm:p-8 space-y-6 hidden">
            <div class="flex justify-between items-center border-b pb-3">
                <div>
                    <span class="text-xs font-bold text-[#15803d] uppercase tracking-wider">Level 3 dari 4</span>
                    <h2 class="text-xl sm:text-2xl font-extrabold text-gray-800">Pythagoras Challenge</h2>
                </div>
                <span class="text-xs bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full font-semibold">Maks. 200 Poin</span>
            </div>

            <!-- Tantangan Soal dengan Gambar Segitiga Per Soal -->
            <div class="space-y-6">
                <!-- Tantangan 1 -->
                <div class="space-y-3">
                    <p class="text-xs sm:text-sm text-gray-700 font-medium">
                        <b>Tantangan 1:</b> Kedua sisi tegak lurus segitiga siku-siku memiliki panjang <b>3 cm</b> dan <b>4 cm</b>. Hitung panjang sisi di depan sudut siku-siku!
                    </p>
                    <div class="bg-amber-50 border border-amber-200 rounded-xl p-3 flex justify-center">
                        <svg viewBox="0 0 200 140" class="w-48 h-32">
                            <polygon points="40,110 160,110 40,30" fill="#fed7aa" stroke="#c2410c" stroke-width="2.5" />
                            <polyline points="40,95 55,95 55,110" fill="none" stroke="#c2410c" stroke-width="2" />
                            <text x="105" y="65" font-size="13" font-weight="bold" fill="#2563eb" text-anchor="middle">c = ?</text>
                            <text x="100" y="128" font-size="12" font-weight="bold" fill="#dc2626" text-anchor="middle">a = 3 cm</text>
                            <text x="15" y="75" font-size="12" font-weight="bold" fill="#16a34a">b = 4 cm</text>
                        </svg>
                    </div>
                    <input type="number" id="l3-input-1" class="w-full border rounded-lg px-3 py-2 text-sm bg-white" placeholder="Masukkan jawaban dalam cm...">
                </div>

                <!-- Tantangan 2 -->
                <div class="space-y-3 border-t pt-4">
                    <p class="text-xs sm:text-sm text-gray-700 font-medium">
                        <b>Tantangan 2:</b> Sisi di depan sudut siku-siku memiliki panjang <b>13 cm</b> dan salah satu sisi tegaknya <b>5 cm</b>. Hitung panjang sisi tegak yang belum diketahui!
                    </p>
                    <div class="bg-amber-50 border border-amber-200 rounded-xl p-3 flex justify-center">
                        <svg viewBox="0 0 200 140" class="w-48 h-32">
                            <polygon points="40,110 160,110 40,30" fill="#fed7aa" stroke="#c2410c" stroke-width="2.5" />
                            <polyline points="40,95 55,95 55,110" fill="none" stroke="#c2410c" stroke-width="2" />
                            <text x="105" y="65" font-size="12" font-weight="bold" fill="#2563eb" text-anchor="middle">c = 13 cm</text>
                            <text x="100" y="128" font-size="12" font-weight="bold" fill="#dc2626" text-anchor="middle">a = 5 cm</text>
                            <text x="15" y="75" font-size="13" font-weight="bold" fill="#16a34a">b = ?</text>
                        </svg>
                    </div>
                    <input type="number" id="l3-input-2" class="w-full border rounded-lg px-3 py-2 text-sm bg-white" placeholder="Masukkan jawaban dalam cm...">
                </div>

                <!-- Tantangan 3 -->
                <div class="space-y-3 border-t pt-4">
                    <p class="text-xs sm:text-sm text-gray-700 font-medium">
                        <b>Tantangan 3:</b> Sisi d
