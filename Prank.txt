<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Diagnosis Ponsel</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            background-color: #0d1117;
            color: #58a6ff;
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        .card {
            background-color: #161b22;
            border: 1px solid #30363d;
            border-radius: 12px;
            padding: 24px;
            max-width: 400px;
            width: 100%;
            text-align: center;
            box-shadow: 0 8px 24px rgba(0,0,0,0.5);
            position: relative;
            z-index: 1;
        }
        h2 {
            margin-bottom: 16px;
            color: #f0f6fc;
        }
        .btn {
            background-color: #238636;
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 16px;
            border-radius: 6px;
            cursor: pointer;
            margin-top: 16px;
            font-weight: bold;
        }
        .btn:hover {
            background-color: #2ea043;
        }
        .console {
            background-color: #010409;
            border: 1px solid #21262d;
            border-radius: 6px;
            padding: 12px;
            margin-top: 20px;
            text-align: left;
            font-size: 14px;
            height: 150px;
            overflow-y: auto;
            display: none;
        }
        .console p {
            margin-bottom: 6px;
        }
        .prank-result {
            display: none;
            margin-top: 20px;
            animation: popIn 0.5s ease-in-out;
        }
        .prank-result h1 {
            font-size: 48px;
            margin-bottom: 10px;
        }
        .prank-result p {
            color: #f0f6fc;
            font-size: 18px;
        }

        /* Layer pemblokir sentuhan */
        .blocker {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: transparent;
            z-index: 9999; /* Memastikan posisinya paling atas */
            pointer-events: all; /* Menangkap semua klik/sentuhan */
        }

        @keyframes popIn {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
    </style>
</head>
<body>

    <!-- Layer transparan yang mengunci layar -->
    <div class="blocker" id="blocker" onclick="alert('Layar terkunci! 😜')" ontouchstart="alert('Layar terkunci! 😜')"></div>

    <div class="card">
        <div id="main-ui">
            <h2>Pemeriksaan Keamanan</h2>
            <p style="color: #8b949e; font-size: 14px;">Klik tombol di bawah untuk memindai kesehatan perangkat Anda.</p>
            <button class="btn" onclick="startScan()">Mulai Pindai Perangkat</button>
        </div>

        <div class="console" id="console"></div>

        <div class="prank-result" id="prank-result">
            <h1>🤪😜</h1>
            <h2 style="color: #ff7b72;">KENA PRANK!</h2>
            <p>HP Anda terkunci sementara!</p>
        </div>
    </div>

    <script>
        const logs = [
            "Menghubungkan ke server...",
            "Memeriksa memori perangkat...",
            "Menganalisis sistem keamanan...",
            "Mengunci input sentuhan...",
            "Proses selesai 100%!"
        ];

        function startScan() {
            // Coba masuk mode layar penuh jika diizinkan browser
            if (document.documentElement.requestFullscreen) {
                document.documentElement.requestFullscreen().catch(() => {});
            }

            document.getElementById('main-ui').style.display = 'none';
            const consoleBox = document.getElementById('console');
            consoleBox.style.display = 'block';

            let delay = 0;

            logs.forEach((logText, index) => {
                delay += 1000;
                setTimeout(() => {
                    const p = document.createElement('p');
                    p.textContent = "> " + logText;
                    consoleBox.appendChild(p);
                    consoleBox.scrollTop = consoleBox.scrollHeight;

                    if (index === logs.length - 1) {
                        setTimeout(() => {
                            consoleBox.style.display = 'none';
                            document.getElementById('prank-result').style.display = 'block';
                            
                            // Aktifkan pemblokir sentuhan
                            document.getElementById('blocker').style.display = 'block';
                        }, 1200);
                    }
                }, delay);
            });
        }
    </script>

</body>
</html>
