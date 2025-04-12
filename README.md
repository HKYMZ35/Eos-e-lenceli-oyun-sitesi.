<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E.O.S - EĞLENCELİ OYUN SİTESİ</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: black;
            color: neon green;
            text-align: center;
        }

        h1 {
            font-size: 40px;
        }

        h2 {
            font-size: 30px;
        }

        h3 {
            font-size: 24px;
        }

        button {
            margin: 10px;
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
            background-color: neon green;
            border: none;
            color: black;
        }

        button:hover {
            background-color: lime;
        }

        .game-container {
            margin: 20px;
            padding: 10px;
            border: 2px solid neon green;
            display: inline-block;
            width: 80%;
        }

        #drawingCanvas {
            border: 1px solid neon green;
            margin-top: 20px;
        }

        iframe {
            width: 100%;
            height: 500px;
        }
    </style>
</head>
<body>

    <header>
        <h1>E.O.S - EĞLENCELİ OYUN SİTESİ</h1>
    </header>

    <nav>
        <ul>
            <li><a href="#games" style="color: neon green;">Oyunlar</a></li>
            <li><a href="#drawing" style="color: neon green;">Çizim Alanı</a></li>
            <li><a href="#music" style="color: neon green;">Müzik</a></li>
        </ul>
    </nav>

    <!-- Oyunlar Bölümü -->
    <section id="games">
        <h2>Oyunlar</h2>
        <div class="game-container">
            <h3>2048</h3>
            <iframe src="https://play2048.co" frameborder="0"></iframe>
        </div>
        <div class="game-container">
            <h3>War Brokers</h3>
            <iframe src="https://warbrokers.io" frameborder="0"></iframe>
        </div>
    </section>

    <!-- Çizim Alanı -->
    <section id="drawing">
        <h2>Çizim Alanı</h2>
        <canvas id="drawingCanvas" width="800" height="600"></canvas>
        <br>
        <button id="classicBrush">Klasik Fırça</button>
        <button id="acrylicBrush">Akrilik Fırça</button>
        <button id="spiralBrush">Spiral Fırça</button>
        <button id="sprayBrush">Spray Fırça</button>
    </section>

    <!-- Müzik Bölümü -->
    <section id="music">
        <h2>Müzik</h2>
        <div class="music-container">
            <iframe src="https://open.spotify.com/embed/track/3n3Ppam7vgaVa1pXf8p3QG" width="300" height="80" frameborder="0" allowtransparency="true" allow="encrypted-media"></iframe>
        </div>
        <div class="music-container">
            <iframe src="https://open.spotify.com/embed/track/5KfRRr0mYtft9Tch5NlGno" width="300" height="80" frameborder="0" allowtransparency="true" allow="encrypted-media"></iframe>
        </div>
    </section>

    <script>
        // Canvas ve 2D context'i al
        const canvas = document.getElementById('drawingCanvas');
        const ctx = canvas.getContext('2d');

        // Fırça tipi ve başlangıç ayarları
        let currentBrush = 'classic'; // Başlangıç fırçası
        let isDrawing = false; // Çizim durumu
        let lastX = 0;
        let lastY = 0;

        // Fırçayı değiştirme işlevi
        function changeBrush(brushType) {
            currentBrush = brushType;
            console.log('Fırça tipi değişti:', brushType);
        }

        // Fırçayı değiştirirken işlevsellik
        canvas.addEventListener('mousedown', (e) => {
            isDrawing = true;
            [lastX, lastY] = [e.offsetX, e.offsetY];
        });

        canvas.addEventListener('mousemove', (e) => {
            if (!isDrawing) return;

            const [x, y] = [e.offsetX, e.offsetY];
            ctx.beginPath();
            ctx.moveTo(lastX, lastY);

            // Fırçaya göre çizim yapma
            if (currentBrush === 'classic') {
                ctx.lineWidth = 5;
                ctx.strokeStyle = 'black';
            } else if (currentBrush === 'acrylic') {
                ctx.lineWidth = 8;
                ctx.strokeStyle = 'rgba(0, 0, 255, 0.7)';
            } else if (currentBrush === 'spiral') {
                ctx.lineWidth = 4;
                ctx.strokeStyle = 'rgba(255, 0, 0, 0.7)';
                ctx.setLineDash([5, 15]); // Spiral etkisi için kesikli çizgi
            } else if (currentBrush === 'spray') {
                ctx.lineWidth = 10;
                ctx.strokeStyle = 'rgba(0, 255, 0, 0.5)';
                ctx.setLineDash([0]); // Spray için kesiksiz çizgi
            }

            ctx.lineTo(x, y);
            ctx.stroke();
            [lastX, lastY] = [x, y];
        });

        canvas.addEventListener('mouseup', () => {
            isDrawing = false;
        });
        canvas.addEventListener('mouseout', () => {
            isDrawing = false;
        });

        // Fırçaları değiştirme
        document.getElementById('classicBrush').addEventListener('click', () => changeBrush('classic'));
        document.getElementById('acrylicBrush').addEventListener('click', () => changeBrush('acrylic'));
        document.getElementById('spiralBrush').addEventListener('click', () => changeBrush('spiral'));
        document.getElementById('sprayBrush').addEventListener('click', () => changeBrush('spray'));
    </script>

</body>
</html>
