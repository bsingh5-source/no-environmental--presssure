<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Genetics Simulation - Environmental Pressure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;700&display=swap');
        body { font-family: 'Lexend', sans-serif; }
        .card { 
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 60px;
            height: 80px;
            margin: 5px;
            border: 2px solid #333;
            border-radius: 8px;
            font-weight: bold;
            font-size: 24px;
            transition: all 0.3s;
        }
        .card.L { background-color: #3b82f6; color: white; }
        .card.l { background-color: #ef4444; color: white; }
        .genotype-display {
            font-size: 32px;
            font-weight: bold;
            padding: 15px 25px;
            border-radius: 8px;
            text-align: center;
            min-width: 120px;
        }
        .genotype-LL { background-color: #dbeafe; color: #1e40af; }
        .genotype-Ll { background-color: #fef3c7; color: #92400e; }
        .genotype-ll { background-color: #fee2e2; color: #7f1d1d; }
        .rejection-alert {
            background-color: #fee2e2;
            border: 2px solid #ef4444;
            color: #7f1d1d;
            padding: 15px;
            border-radius: 10px;
            margin-top: 10px;
            font-weight: 600;
            animation: shake 0.5s;
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }
        .success-alert {
            background-color: #dcfce7;
            border: 2px solid #22c55e;
            color: #166534;
            padding: 15px;
            border-radius: 10px;
            margin-top: 10px;
            font-weight: 600;
        }
    </style>
</head>
<body class="bg-slate-100 min-h-screen pb-12">
    <div class="max-w-6xl mx-auto p-4">
        <!-- Header -->
        <header class="bg-white rounded-2xl shadow-sm p-6 mb-6 mt-4 border-b-4 border-red-500">
            <div>
                <h1 class="text-3xl font-bold text-slate-800">🧬 Environmental Pressure Simulator</h1>
                <p class="text-slate-500">Selection against ll genotype - natural selection in action</p>
            </div>
        </header>

        <!-- Environmental Pressure Warning -->
        <div class="bg-red-50 border-l-4 border-red-500 p-6 mb-6 rounded-lg">
            <h3 class="font-bold text-red-900 mb-2">⚠️ Environmental Pressure Active</h3>
            <p class="text-red-800"><strong>Selection Rule:</strong> If you produce an <strong>ll genotype</strong>, you cannot contribute to the next generation. You must return your cards and try again until you get <strong>LL or Ll</strong>.</p>
        </div>

        <!-- Trial Selection -->
        <div class="bg-white rounded-2xl shadow-sm p-6 mb-6 border border-slate-200">
            <h2 class="font-bold text-xl mb-4">Select Trial</h2>
            <div class="flex gap-4">
                <button onclick="setTrial(1)" id="trial-1" class="px-6 py-3 rounded-lg border-2 border-blue-500 bg-blue-50 text-blue-700 font-bold">Trial 1</button>
                <button onclick="setTrial(2)" id="trial-2" class="px-6 py-3 rounded-lg border-2 border-slate-200 text-slate-600 font-bold hover:border-blue-300">Trial 2</button>
                <button onclick="setTrial(3)" id="trial-3" class="px-6 py-3 rounded-lg border-2 border-slate-200 text-slate-600 font-bold hover:border-blue-300">Trial 3</button>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Left Panel -->
            <div class="space-y-4">
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
                    <h3 class="font-bold text-lg mb-4">Your Status</h3>
                    <div class="space-y-3">
                        <div>
                            <p class="text-sm text-slate-500 uppercase">Generation</p>
                            <p id="gen-display" class="text-3xl font-bold text-blue-600">1</p>
                        </div>
                        <div>
                            <p class="text-sm text-slate-500 uppercase">Your Genotype</p>
                            <div id="current-genotype" class="genotype-display genotype-Ll">Ll</div>
                        </div>
                        <div>
                            <p class="text-sm text-slate-500 uppercase">Attempts This Gen</p>
                            <p id="attempts" class="text-2xl font-bold text-red-600">0</p>


