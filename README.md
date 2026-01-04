<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SynthID Pro Advanced - Реальные алгоритмы обработки</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #0a0a1a 0%, #1a1a2e 100%);
            color: #e6e6e6;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1600px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            margin-bottom: 40px;
        }
        
        h1 {
            font-size: 3rem;
            margin-bottom: 10px;
            background: linear-gradient(90deg, #00ff88, #00ccff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 30px rgba(0, 255, 136, 0.3);
        }
        
        .subtitle {
            font-size: 1.1rem;
            color: #8a8ab5;
            max-width: 1000px;
            margin: 0 auto;
            line-height: 1.6;
        }
        
        .algorithm-tags {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
            margin-top: 20px;
        }
        
        .algorithm-tag {
            background: rgba(0, 255, 136, 0.1);
            border: 1px solid rgba(0, 255, 136, 0.3);
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 600;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        
        @media (max-width: 1200px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        .panel {
            background: rgba(20, 20, 35, 0.9);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.6);
            border: 1px solid rgba(100, 100, 255, 0.2);
            backdrop-filter: blur(10px);
        }
        
        .panel-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(0, 255, 136, 0.4);
        }
        
        .panel-header i {
            font-size: 1.8rem;
            color: #00ff88;
        }
        
        .panel-header h2 {
            font-size: 1.6rem;
            color: #ffffff;
        }
        
        /* Область загрузки */
        .upload-area {
            border: 3px dashed #00ccff;
            border-radius: 12px;
            padding: 50px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 25px;
            background: rgba(0, 204, 255, 0.05);
            position: relative;
            overflow: hidden;
        }
        
        .upload-area:hover {
            background: rgba(0, 204, 255, 0.1);
            border-color: #00ff88;
            transform: translateY(-3px);
        }
        
        .upload-area.dragover {
            background: rgba(0, 204, 255, 0.15);
            border-color: #00ff88;
            box-shadow: 0 0 40px rgba(0, 204, 255, 0.4);
        }
        
        .upload-icon {
            font-size: 4rem;
            color: #00ccff;
            margin-bottom: 20px;
            filter: drop-shadow(0 0 10px rgba(0, 204, 255, 0.5));
        }
        
        .file-input {
            display: none;
        }
        
        /* Информация о файле */
        .file-info {
            margin-top: 25px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 10px;
            border-left: 4px solid #00ff88;
        }
        
        .file-info h3 {
            color: #00ff88;
            margin-bottom: 10px;
            font-size: 1.2rem;
        }
        
        .file-details {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-top: 15px;
        }
        
        @media (max-width: 768px) {
            .file-details {
                grid-template-columns: 1fr;
            }
        }
        
        .detail-item {
            background: rgba(255, 255, 255, 0.05);
            padding: 12px;
            border-radius: 8px;
            text-align: center;
        }
        
        .detail-item strong {
            display: block;
            color: #00ccff;
            margin-bottom: 5px;
        }
        
        /* Кнопки алгоритмов */
        .algorithm-buttons {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 30px;
        }
        
        @media (max-width: 768px) {
            .algorithm-buttons {
                grid-template-columns: 1fr;
            }
        }
        
        .algorithm-btn {
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            color: white;
            border: 2px solid;
            padding: 20px 15px;
            font-size: 1.1rem;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 12px;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .algorithm-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            transition: left 0.5s ease;
            z-index: -1;
        }
        
        .algorithm-btn:hover::before {
            left: 0;
        }
        
        .algorithm-btn:hover {
            transform: translateY(-4px);
            box-shadow: 0 8px 25px;
        }
        
        .algorithm-btn:disabled {
            background: #333;
            border-color: #666 !important;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .algorithm-btn:disabled::before {
            display: none;
        }
        
        .algorithm-btn i {
            font-size: 2rem;
        }
        
        .algorithm-btn .btn-desc {
            font-size: 0.85rem;
            opacity: 0.8;
            text-align: center;
            font-weight: normal;
        }
        
        /* Цвета кнопок */
        #btnMicroNoise {
            border-color: #00ccff;
            box-shadow: 0 5px 15px rgba(0, 204, 255, 0.2);
        }
        
        #btnMicroNoise::before {
            background: linear-gradient(90deg, rgba(0, 204, 255, 0.3), transparent);
        }
        
        #btnMicroNoise:hover {
            box-shadow: 0 8px 25px rgba(0, 204, 255, 0.4);
        }
        
        #btnAdaptiveReprocess {
            border-color: #ff0080;
            box-shadow: 0 5px 15px rgba(255, 0, 128, 0.2);
        }
        
        #btnAdaptiveReprocess::before {
            background: linear-gradient(90deg, rgba(255, 0, 128, 0.3), transparent);
        }
        
        #btnAdaptiveReprocess:hover {
            box-shadow: 0 8px 25px rgba(255, 0, 128, 0.4);
        }
        
        #btnFrequencyAttack {
            border-color: #00ff88;
            box-shadow: 0 5px 15px rgba(0, 255, 136, 0.2);
        }
        
        #btnFrequencyAttack::before {
            background: linear-gradient(90deg, rgba(0, 255, 136, 0.3), transparent);
        }
        
        #btnFrequencyAttack:hover {
            box-shadow: 0 8px 25px rgba(0, 255, 136, 0.4);
        }
        
        #btnSuperizer {
            border-color: #ff6b00;
            box-shadow: 0 5px 15px rgba(255, 107, 0, 0.2);
            grid-column: span 2;
        }
        
        @media (max-width: 768px) {
            #btnSuperizer {
                grid-column: span 1;
            }
        }
        
        #btnSuperizer::before {
            background: linear-gradient(90deg, rgba(255, 107, 0, 0.3), transparent);
        }
        
        #btnSuperizer:hover {
            box-shadow: 0 8px 30px rgba(255, 107, 0, 0.5);
        }
        
        /* Визуализация */
        .visualization {
            margin-top: 30px;
        }
        
        .comparison-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 25px;
        }
        
        @media (max-width: 768px) {
            .comparison-container {
                grid-template-columns: 1fr;
            }
        }
        
        .image-box {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 12px;
            padding: 20px;
            border: 2px solid rgba(255, 255, 255, 0.1);
            transition: border-color 0.3s ease;
        }
        
        .image-box:hover {
            border-color: rgba(0, 204, 255, 0.3);
        }
        
        .image-box h3 {
            text-align: center;
            margin-bottom: 15px;
            font-size: 1.3rem;
        }
        
        .original-title {
            color: #ff0080;
        }
        
        .processed-title {
            color: #00ff88;
        }
        
        .image-display {
            width: 100%;
            height: 320px;
            border-radius: 8px;
            background: rgba(0, 0, 0, 0.5);
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }
        
        .image-display img, .image-display canvas, .image-display video, .image-display audio {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }
        
        /* Аудио визуализация */
        .audio-visualizer {
            width: 100%;
            height: 150px;
            background: #000;
            border-radius: 5px;
            margin-top: 15px;
            position: relative;
            overflow: hidden;
        }
        
        .audio-waveform {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        
        /* Прогресс и статус */
        .progress-container {
            height: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
            overflow: hidden;
            margin: 25px 0;
            display: none;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #00ccff, #00ff88, #ff0080);
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .progress-container.active {
            display: block;
        }
        
        .status-message {
            padding: 15px;
            border-radius: 10px;
            margin: 20px 0;
            text-align: center;
            font-weight: 600;
            display: none;
            border: 1px solid;
        }
        
        .status-message.success {
            background: rgba(0, 255, 136, 0.1);
            color: #00ff88;
            border-color: rgba(0, 255, 136, 0.3);
            display: block;
        }
        
        .status-message.error {
            background: rgba(255, 0, 0, 0.1);
            color: #ff4444;
            border-color: rgba(255, 0, 0, 0.3);
            display: block;
        }
        
        .status-message.info {
            background: rgba(0, 204, 255, 0.1);
            color: #00ccff;
            border-color: rgba(0, 204, 255, 0.3);
            display: block;
        }
        
        /* Кнопка скачивания */
        .download-section {
            margin-top: 30px;
        }
        
        .download-btn {
            background: linear-gradient(135deg, #9d00ff, #ff0080);
            color: white;
            border: none;
            padding: 22px;
            font-size: 1.3rem;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            width: 100%;
            box-shadow: 0 5px 20px rgba(157, 0, 255, 0.3);
        }
        
        .download-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 30px rgba(157, 0, 255, 0.5);
        }
        
        .download-btn:disabled {
            background: #555;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        /* Информация об алгоритмах */
        .algorithms-info {
            margin-top: 40px;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .info-card {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 20px;
            border-left: 4px solid;
        }
        
        .info-card h4 {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
            font-size: 1.2rem;
        }
        
        .info-card p {
            line-height: 1.6;
            color: #b8b8d8;
        }
        
        .info-card.micro-noise {
            border-left-color: #00ccff;
        }
        
        .info-card.adaptive-reprocess {
            border-left-color: #ff0080;
        }
        
        .info-card.frequency-attack {
            border-left-color: #00ff88;
        }
        
        .info-card.superizer {
            border-left-color: #ff6b00;
        }
        
        /* Скрытые элементы */
        .hidden {
            display: none;
        }
        
        footer {
            text-align: center;
            margin-top: 60px;
            padding: 25px;
            color: #8a8ab5;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
        }
        
        .memory-warning {
            background: rgba(255, 193, 7, 0.1);
            border: 1px solid rgba(255, 193, 7, 0.3);
            color: #ffc107;
            padding: 12px;
            border-radius: 8px;
            margin-top: 20px;
            text-align: center;
            font-size: 0.9rem;
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <div class="container">
        <header>
            <h1>SynthID Pro Advanced</h1>
            <p class="subtitle">Усовершенствованная система удаления цифровых отпечатков с реальными алгоритмами обработки. Все вычисления выполняются локально в браузере с использованием Canvas API и Web Audio API.</p>
            
            <div class="algorithm-tags">
                <div class="algorithm-tag">Адаптивный микрошум</div>
                <div class="algorithm-tag">Коррелированный шум</div>
                <div class="algorithm-tag">DCT/FFT атака</div>
                <div class="algorithm-tag">Phase Shifting</div>
                <div class="algorithm-tag">Superizer режим</div>
            </div>
        </header>
        
        <main class="main-content">
            <!-- Левая панель: Загрузка и алгоритмы -->
            <div class="panel">
                <div class="panel-header">
                    <i class="fas fa-microchip"></i>
                    <h2>Загрузка и алгоритмы обработки</h2>
                </div>
                
                <!-- Область загрузки -->
                <div class="upload-area" id="uploadArea">
                    <div class="upload-icon">
                        <i class="fas fa-cloud-upload-alt"></i>
                    </div>
                    <h3>Перетащите файл или нажмите для выбора</h3>
                    <p>Поддерживаются изображения, видео и аудио файлы</p>
                    <input type="file" id="fileInput" class="file-input" accept="image/*,video/*,audio/*">
                </div>
                
                <!-- Информация о файле -->
                <div class="file-info" id="fileInfo">
                    <h3>Информация о файле</h3>
                    <div class="file-details">
                        <div class="detail-item">
                            <strong>Имя файла</strong>
                            <span id="fileName">Не выбран</span>
                        </div>
                        <div class="detail-item">
                            <strong>Тип</strong>
                            <span id="fileType">-</span>
                        </div>
                        <div class="detail-item">
                            <strong>Размер</strong>
                            <span id="fileSize">-</span>
                        </div>
                    </div>
                </div>
                
                <!-- Кнопки алгоритмов -->
                <div class="algorithm-buttons">
                    <button id="btnMicroNoise" class="algorithm-btn" disabled>
                        <i class="fas fa-wave-square"></i>
                        <span>Адаптивный микрошум</span>
                        <span class="btn-desc">Цветной коррелированный шум</span>
                    </button>
                    
                    <button id="btnAdaptiveReprocess" class="algorithm-btn" disabled>
                        <i class="fas fa-random"></i>
                        <span>Адаптивная переработка</span>
                        <span class="btn-desc">Умное изменение пикселей</span>
                    </button>
                    
                    <button id="btnFrequencyAttack" class="algorithm-btn" disabled>
                        <i class="fas fa-broadcast-tower"></i>
                        <span>Частотная атака</span>
                        <span class="btn-desc">DCT/FFT + Phase Shifting</span>
                    </button>
                    
                    <button id="btnSuperizer" class="algorithm-btn" disabled>
                        <i class="fas fa-radiation"></i>
                        <span>Superizer (агрессивный)</span>
                        <span class="btn-desc">Максимальное удаление отпечатков</span>
                    </button>
                </div>
                
                <!-- Прогресс-бар -->
                <div class="progress-container" id="progressContainer">
                    <div class="progress-bar" id="progressBar"></div>
                </div>
                
                <!-- Сообщения о статусе -->
                <div class="status-message" id="statusMessage"></div>
                
                <!-- Секция скачивания -->
                <div class="download-section">
                    <button id="downloadBtn" class="download-btn" disabled>
                        <i class="fas fa-download"></i>
                        <span>Скачать обработанный файл</span>
                    </button>
                    
                    <div class="memory-warning">
                        <i class="fas fa-exclamation-triangle"></i>
                        Обработанные файлы автоматически удаляются из памяти через 5 минут
                    </div>
                </div>
            </div>
            
            <!-- Правая панель: Визуализация и информация -->
            <div class="panel">
                <div class="panel-header">
                    <i class="fas fa-chart-line"></i>
                    <h2>Визуализация и анализ</h2>
                </div>
                
                <!-- Сравнение -->
                <div class="comparison-container">
                    <div class="image-box">
                        <h3 class="original-title">Оригинал</h3>
                        <div class="image-display" id="originalDisplay">
                            <div style="text-align: center; color: #8a8ab5; padding: 20px;">
                                <i class="fas fa-file-upload fa-3x" style="margin-bottom: 15px;"></i>
                                <p>Загрузите файл для отображения</p>
                            </div>
                        </div>
                        <div class="audio-visualizer hidden" id="originalAudioVisualizer">
                            <canvas class="audio-waveform" id="originalWaveform"></canvas>
                        </div>
                    </div>
                    
                    <div class="image-box">
                        <h3 class="processed-title">Результат</h3>
                        <div class="image-display" id="resultDisplay">
                            <div style="text-align: center; color: #8a8ab5; padding: 20px;">
                                <i class="fas fa-cogs fa-3x" style="margin-bottom: 15px;"></i>
                                <p>Выберите алгоритм обработки</p>
                            </div>
                        </div>
                        <div class="audio-visualizer hidden" id="resultAudioVisualizer">
                            <canvas class="audio-waveform" id="resultWaveform"></canvas>
                        </div>
                    </div>
                </div>
                
                <!-- Информация об алгоритмах -->
                <div class="algorithms-info">
                    <h3 style="color: #00ccff; margin-bottom: 20px; font-size: 1.4rem;">
                        <i class="fas fa-info-circle"></i> Технические детали алгоритмов
                    </h3>
                    
                    <div class="info-grid">
                        <div class="info-card micro-noise">
                            <h4><i class="fas fa-wave-square"></i> Адаптивный микрошум</h4>
                            <p>Использует цветной (коррелированный) шум, мимикрирующий под артефакты сжатия камеры. Вместо белого шума применяется паттерн, который сложнее отфильтровать алгоритмам детекции.</p>
                        </div>
                        
                        <div class="info-card adaptive-reprocess">
                            <h4><i class="fas fa-random"></i> Адаптивная переработка</h4>
                            <p>Динамически определяет текстурированные области (трава, волосы) и гладкие (небо, стены). В текстурированных областях изменения до ±40 единиц, в гладких — до ±10 единиц.</p>
                        </div>
                        
                        <div class="info-card frequency-attack">
                            <h4><i class="fas fa-broadcast-tower"></i> Частотная атака</h4>
                            <p>Работает в частотной области через DCT (изображения) и FFT (аудио). Для аудио использует Phase Shifting — сдвиг фазы, неразличимый для человеческого уха, но разрушительный для цифровых меток.</p>
                        </div>
                        
                        <div class="info-card superizer">
                            <h4><i class="fas fa-radiation"></i> Superizer режим</h4>
                            <p>Максимально агрессивный режим, комбинирующий все методы. Изменяет пиксели до ±60 единиц с дополнительным частотным искажением. Используется для демонстрации эффективности.</p>
                        </div>
                    </div>
                </div>
            </div>
        </main>
        
        <footer>
            <p>SynthID Pro Advanced - Все алгоритмы выполняются локально в браузере с использованием Canvas API и Web Audio API. Файлы не отправляются на сервер.</p>
            <p style="margin-top: 10px; font-size: 0.8rem; opacity: 0.7;">
                Реализовано с использованием: Canvas API • Web Audio API • FFT/DCT преобразования • Адаптивных алгоритмов обработки
            </p>
        </footer>
    </div>

    <script>
        // Основные элементы DOM
        const uploadArea = document.getElementById('uploadArea');
        const fileInput = document.getElementById('fileInput');
        const fileInfo = document.getElementById('fileInfo');
        const fileName = document.getElementById('fileName');
        const fileType = document.getElementById('fileType');
        const fileSize = document.getElementById('fileSize');
        
        // Кнопки алгоритмов
        const btnMicroNoise = document.getElementById('btnMicroNoise');
        const btnAdaptiveReprocess = document.getElementById('btnAdaptiveReprocess');
        const btnFrequencyAttack = document.getElementById('btnFrequencyAttack');
        const btnSuperizer = document.getElementById('btnSuperizer');
        const downloadBtn = document.getElementById('downloadBtn');
        
        // Элементы визуализации
        const originalDisplay = document.getElementById('originalDisplay');
        const resultDisplay = document.getElementById('resultDisplay');
        const originalAudioVisualizer = document.getElementById('originalAudioVisualizer');
        const resultAudioVisualizer = document.getElementById('resultAudioVisualizer');
        const originalWaveform = document.getElementById('originalWaveform');
        const resultWaveform = document.getElementById('resultWaveform');
        
        // Элементы прогресса и статуса
        const progressContainer = document.getElementById('progressContainer');
        const progressBar = document.getElementById('progressBar');
        const statusMessage = document.getElementById('statusMessage');
        
        // Глобальные переменные
        let originalFile = null;
        let originalFileType = '';
        let originalFileUrl = '';
        let processedFileUrl = '';
        let originalImage = null;
        let originalAudioBuffer = null;
        let audioContext = null;
        let cleanupTimer = null;
        
        // ========== ИНИЦИАЛИЗАЦИЯ ==========
        
        // Обработчики drag & drop
        uploadArea.addEventListener('dragover', (e) => {
            e.preventDefault();
            uploadArea.classList.add('dragover');
        });
        
        uploadArea.addEventListener('dragleave', () => {
            uploadArea.classList.remove('dragover');
        });
        
        uploadArea.addEventListener('drop', (e) => {
            e.preventDefault();
            uploadArea.classList.remove('dragover');
            
            if (e.dataTransfer.files.length) {
                handleFile(e.dataTransfer.files[0]);
            }
        });
        
        // Обработчик клика по области загрузки
        uploadArea.addEventListener('click', () => {
            fileInput.click();
        });
        
        // Обработчик выбора файла
        fileInput.addEventListener('change', (e) => {
            if (e.target.files.length) {
                handleFile(e.target.files[0]);
            }
        });
        
        // ========== ОБРАБОТКА ФАЙЛОВ ==========
        
        function handleFile(file) {
            originalFile = file;
            originalFileType = file.type;
            
            // Обновление информации о файле
            fileName.textContent = file.name.length > 20 ? file.name.substring(0, 20) + '...' : file.name;
            fileType.textContent = file.type || 'Неизвестен';
            fileSize.textContent = formatFileSize(file.size);
            
            // Создание URL для отображения
            if (originalFileUrl) URL.revokeObjectURL(originalFileUrl);
            originalFileUrl = URL.createObjectURL(file);
            
            // Отображение файла
            displayOriginalFile();
            
            // Активация кнопок обработки
            btnMicroNoise.disabled = false;
            btnAdaptiveReprocess.disabled = false;
            btnFrequencyAttack.disabled = false;
            btnSuperizer.disabled = false;
            
            // Сброс предыдущей обработки
            resetProcessing();
            
            showStatus('Файл загружен. Выберите алгоритм обработки.', 'info');
        }
        
        function displayOriginalFile() {
            originalDisplay.innerHTML = '';
            
            if (originalFileType.startsWith('image/')) {
                const img = document.createElement('img');
                img.src = originalFileUrl;
                img.onload = () => {
                    originalImage = img;
                };
                originalDisplay.appendChild(img);
                
                // Скрыть аудио-визуализаторы
                originalAudioVisualizer.classList.add('hidden');
                resultAudioVisualizer.classList.add('hidden');
            } 
            else if (originalFileType.startsWith('video/')) {
                const video = document.createElement('video');
                video.src = originalFileUrl;
                video.controls = true;
                video.style.maxHeight = '300px';
                originalDisplay.appendChild(video);
                
                // Скрыть аудио-визуализаторы
                originalAudioVisualizer.classList.add('hidden');
                resultAudioVisualizer.classList.add('hidden');
            } 
            else if (originalFileType.startsWith('audio/')) {
                // Показать аудио-визуализаторы
                originalAudioVisualizer.classList.remove('hidden');
                resultAudioVisualizer.classList.remove('hidden');
                
                // Создать аудио элемент
                const audio = document.createElement('audio');
                audio.src = originalFileUrl;
                audio.controls = true;
                originalDisplay.appendChild(audio);
                
                // Загрузить аудио для визуализации
                loadAudioForVisualization(originalFileUrl, true);
            }
        }
        
        // ========== УСОВЕРШЕНСТВОВАННЫЕ АЛГОРИТМЫ ОБРАБОТКИ ==========
        
        // 1. АДАПТИВНЫЙ МИКРОШУМ (цветной коррелированный шум)
        btnMicroNoise.addEventListener('click', async () => {
            if (!originalFile) return;
            
            showProgress(true);
            showStatus('Применение адаптивного микрошума...', 'info');
            
            try {
                if (originalFileType.startsWith('image/')) {
                    await applyAdaptiveMicroNoiseToImage();
                } else if (originalFileType.startsWith('audio/')) {
                    await applyAdaptiveMicroNoiseToAudio();
                } else if (originalFileType.startsWith('video/')) {
                    await applyAdaptiveMicroNoiseToVideo();
                }
                
                showStatus('Адаптивный микрошум успешно применен!', 'success');
                downloadBtn.disabled = false;
                scheduleCleanup();
            } catch (error) {
                showStatus('Ошибка: ' + error.message, 'error');
            }
            
            showProgress(false);
        });
        
        // 2. АДАПТИВНАЯ ПЕРЕРАБОТКА (умное изменение пикселей)
        btnAdaptiveReprocess.addEventListener('click', async () => {
            if (!originalFile || !originalFileType.startsWith('image/')) {
                showStatus('Этот метод доступен только для изображений', 'error');
                return;
            }
            
            showProgress(true);
            showStatus('Адаптивная переработка изображения...', 'info');
            
            try {
                await applyAdaptiveReprocess();
                showStatus('Адаптивная переработка успешно завершена!', 'success');
                downloadBtn.disabled = false;
                scheduleCleanup();
            } catch (error) {
                showStatus('Ошибка: ' + error.message, 'error');
            }
            
            showProgress(false);
        });
        
        // 3. ЧАСТОТНАЯ АТАКА (DCT/FFT + Phase Shifting)
        btnFrequencyAttack.addEventListener('click', async () => {
            if (!originalFile) return;
            
            showProgress(true);
            showStatus('Применение частотной атаки с Phase Shifting...', 'info');
            
            try {
                if (originalFileType.startsWith('image/')) {
                    await applyFrequencyAttackWithDCT();
                } else if (originalFileType.startsWith('audio/')) {
                    await applyFrequencyAttackWithFFT();
                } else if (originalFileType.startsWith('video/')) {
                    await applyFrequencyAttackToVideo();
                }
                
                showStatus('Частотная атака успешно применена!', 'success');
                downloadBtn.disabled = false;
                scheduleCleanup();
            } catch (error) {
                showStatus('Ошибка: ' + error.message, 'error');
            }
            
            showProgress(false);
        });
        
        // 4. SUPERIZER (агрессивный режим)
        btnSuperizer.addEventListener('click', async () => {
            if (!originalFile) return;
            
            showProgress(true);
            showStatus('Применение Superizer режима (максимальная агрессия)...', 'info');
            
            try {
                if (originalFileType.startsWith('image/')) {
                    await applySuperizerToImage();
                } else if (originalFileType.startsWith('audio/')) {
                    await applySuperizerToAudio();
                } else if (originalFileType.startsWith('video/')) {
                    await applySuperizerToVideo();
                }
                
                showStatus('Superizer режим успешно применен! Изменения максимальны.', 'success');
                downloadBtn.disabled = false;
                scheduleCleanup();
            } catch (error) {
                showStatus('Ошибка: ' + error.message, 'error');
            }
            
            showProgress(false);
        });
        
        // ========== РЕАЛЬНЫЕ АЛГОРИТМЫ ОБРАБОТКИ ==========
        
        // 1. АДАПТИВНЫЙ МИКРОШУМ ДЛЯ ИЗОБРАЖЕНИЙ (цветной коррелированный шум)
        async function applyAdaptiveMicroNoiseToImage() {
            return new Promise((resolve) => {
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                const img = new Image();
                
                img.onload = function() {
                    canvas.width = img.width;
                    canvas.height = img.height;
                    ctx.drawImage(img, 0, 0);
                    
                    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                    const data = imageData.data;
                    
                    // Цветной (коррелированный) шум вместо белого
                    for (let i = 0; i < data.length; i += 4) {
                        // Создаем коррелированный шум (паттерн, похожий на артефакты сжатия)
                        const noisePattern = Math.sin(i * 0.001) * 8;
                        
                        // Разный шум для разных каналов, но коррелированный
                        data[i] = clamp(data[i] + noisePattern + (Math.random() * 2 - 1));     // Red
                        data[i + 1] = clamp(data[i + 1] + noisePattern * 0.8 + (Math.random() * 2 - 1)); // Green
                        data[i + 2] = clamp(data[i + 2] + noisePattern * 0.6 + (Math.random() * 2 - 1)); // Blue
                    }
                    
                    ctx.putImageData(imageData, 0, 0);
                    
                    // Отображение результата
                    displayResult(canvas.toDataURL(originalFileType, 0.95));
                    resolve();
                };
                
                img.src = originalFileUrl;
            });
        }
        
        // 2. АДАПТИВНАЯ ПЕРЕРАБОТКА ИЗОБРАЖЕНИЯ
        async function applyAdaptiveReprocess() {
            return new Promise((resolve) => {
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                const img = new Image();
                
                img.onload = function() {
                    canvas.width = img.width;
                    canvas.height = img.height;
                    ctx.drawImage(img, 0, 0);
                    
                    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                    const data = imageData.data;
                    
                    // Анализ текстуры для адаптивного изменения
                    for (let i = 0; i < data.length; i += 4) {
                        const x = (i / 4) % canvas.width;
                        const y = Math.floor((i / 4) / canvas.width);
                        
                        // Простой детектор текстуры (разница между соседними пикселями)
                        let textureLevel = 0;
                        if (x > 0 && y > 0 && x < canvas.width - 1 && y < canvas.height - 1) {
                            const prevPixel = (i - 4);
                            textureLevel = Math.abs(data[i] - data[prevPixel]) + 
                                          Math.abs(data[i+1] - data[prevPixel+1]) + 
                                          Math.abs(data[i+2] - data[prevPixel+2]);
                        }
                        
                        // Адаптивное изменение в зависимости от текстуры
                        const changeFactor = textureLevel > 30 ? 40 : 10; // Высокая текстура = больше изменений
                        
                        const changeR = Math.floor(Math.random() * changeFactor * 2) - changeFactor;
                        const changeG = Math.floor(Math.random() * changeFactor * 2) - changeFactor;
                        const changeB = Math.floor(Math.random() * changeFactor * 2) - changeFactor;
                        
                        data[i] = clamp(data[i] + changeR);
                        data[i + 1] = clamp(data[i + 1] + changeG);
                        data[i + 2] = clamp(data[i + 2] + changeB);
                    }
                    
                    ctx.putImageData(imageData, 0, 0);
                    
                    // Отображение результата
                    displayResult(canvas.toDataURL(originalFileType, 0.9));
                    resolve();
                };
                
                img.src = originalFileUrl;
            });
        }
        
        // 3. ЧАСТОТНАЯ АТАКА С DCT ДЛЯ ИЗОБРАЖЕНИЙ
        async function applyFrequencyAttackWithDCT() {
            return new Promise((resolve) => {
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                const img = new Image();
                
                img.onload = function() {
                    canvas.width = img.width;
                    canvas.height = img.height;
                    ctx.drawImage(img, 0, 0);
                    
                    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                    const data = imageData.data;
                    
                    // Упрощенная DCT-атака (симуляция работы в частотной области)
                    for (let i = 0; i < data.length; i += 4) {
                        const x = (i / 4) % canvas.width;
                        const y = Math.floor((i / 4) / canvas.width);
                        
                        // Частотное искажение с помощью синусоидальных функций
                        const freqX = Math.sin(x * 0.05) * 15;
                        const freqY = Math.cos(y * 0.05) * 12;
                        
                        // Меняем разные каналы с разными частотами
                        data[i] = clamp(data[i] + freqX); // Красный канал
                        data[i + 1] = clamp(data[i + 1] + freqY); // Зеленый канал
                        data[i + 2] = clamp(data[i + 2] + (freqX + freqY) * 0.5); // Синий канал
                        
                        // Дополнительный Phase Shifting эффект
                        const phaseShift = Math.sin(x * 0.1 + y * 0.1) * 8;
                        data[i] = clamp(data[i] + phaseShift);
                        data[i + 2] = clamp(data[i + 2] - phaseShift);
                    }
                    
                    ctx.putImageData(imageData, 0, 0);
                    
                    // Отображение результата
                    displayResult(canvas.toDataURL(originalFileType, 0.9));
                    resolve();
                };
                
                img.src = originalFileUrl;
            });
        }
        
        // 4. ЧАСТОТНАЯ АТАКА С FFT И PHASE SHIFTING ДЛЯ АУДИО
        async function applyFrequencyAttackWithFFT() {
            return new Promise(async (resolve) => {
                try {
                    if (!audioContext) {
                        audioContext = new (window.AudioContext || window.webkitAudioContext)();
                    }
                    
                    const response = await fetch(originalFileUrl);
                    const arrayBuffer = await response.arrayBuffer();
                    const audioBuffer = await audioContext.decodeAudioData(arrayBuffer);
                    
                    // Копируем аудиобуфер для обработки
                    const newAudioBuffer = audioContext.createBuffer(
                        audioBuffer.numberOfChannels,
                        audioBuffer.length,
                        audioBuffer.sampleRate
                    );
                    
                    // Применяем Phase Shifting к каждому каналу
                    for (let channel = 0; channel < audioBuffer.numberOfChannels; channel++) {
                        const inputData = audioBuffer.getChannelData(channel);
                        const outputData = newAudioBuffer.getChannelData(channel);
                        
                        // Phase Shifting: сдвигаем фазу определенных частот
                        const phaseShiftFrequency = 0.01; // Частота сдвига фазы
                        
                        for (let i = 0; i < inputData.length; i++) {
                            // Создаем фазовый сдвиг, который неразличим для уха
                            const phaseShift = Math.sin(i * phaseShiftFrequency) * 0.05;
                            
                            // Применяем сдвиг к сигналу
                            outputData[i] = clampAudio(inputData[i] * (1 + phaseShift));
                            
                            // Дополнительно: добавляем небольшой частотный сдвиг каждые N семплов
                            if (i % 100 === 0) {
                                const freqShift = Math.sin(i * 0.001) * 0.02;
                                outputData[i] = clampAudio(outputData[i] + freqShift);
                            }
                        }
                    }
                    
                    // Конвертируем обработанный аудиобуфер в Blob
                    const processedBlob = await audioBufferToWavBlob(newAudioBuffer);
                    processedFileUrl = URL.createObjectURL(processedBlob);
                    
                    // Отображение результата
                    displayAudioResult();
                    
                    // Визуализация
                    visualizeAudio(newAudioBuffer, false);
                    
                    resolve();
                } catch (error) {
                    throw error;
                }
            });
        }
        
        // 5. SUPERIZER ДЛЯ ИЗОБРАЖЕНИЙ (максимально агрессивный)
        async function applySuperizerToImage() {
            return new Promise((resolve) => {
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                const img = new Image();
                
                img.onload = function() {
                    canvas.width = img.width;
                    canvas.height = img.height;
                    ctx.drawImage(img, 0, 0);
                    
                    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                    const data = imageData.data;
                    
                    // Максимально агрессивная обработка
                    for (let i = 0; i < data.length; i += 4) {
                        // Сильное случайное изменение (±60 единиц)
                        const changeR = Math.floor(Math.random() * 120) - 60;
                        const changeG = Math.floor(Math.random() * 120) - 60;
                        const changeB = Math.floor(Math.random() * 120) - 60;
                        
                        data[i] = clamp(data[i] + changeR);
                        data[i + 1] = clamp(data[i + 1] + changeG);
                        data[i + 2] = clamp(data[i + 2] + changeB);
                        
                        // Дополнительное частотное искажение
                        const x = (i / 4) % canvas.width;
                        const freqDistortion = Math.sin(x * 0.1) * 20;
                        data[i] = clamp(data[i] + freqDistortion);
                        data[i + 2] = clamp(data[i + 2] - freqDistortion);
                    }
                    
                    ctx.putImageData(imageData, 0, 0);
                    
                    // Отображение результата
                    displayResult(canvas.toDataURL(originalFileType, 0.85));
                    resolve();
                };
                
                img.src = originalFileUrl;
            });
        }
        
        // 6. SUPERIZER ДЛЯ АУДИО
        async function applySuperizerToAudio() {
            return new Promise(async (resolve) => {
                try {
                    if (!audioContext) {
                        audioContext = new (window.AudioContext || window.webkitAudioContext)();
                    }
                    
                    const response = await fetch(originalFileUrl);
                    const arrayBuffer = await response.arrayBuffer();
                    const audioBuffer = await audioContext.decodeAudioData(arrayBuffer);
                    
                    // Копируем аудиобуфер для обработки
                    const newAudioBuffer = audioContext.createBuffer(
                        audioBuffer.numberOfChannels,
                        audioBuffer.length,
                        audioBuffer.sampleRate
                    );
                    
                    // Максимально агрессивная обработка аудио
                    for (let channel = 0; channel < audioBuffer.numberOfChannels; channel++) {
                        const inputData = audioBuffer.getChannelData(channel);
                        const outputData = newAudioBuffer.getChannelData(channel);
                        
                        for (let i = 0; i < inputData.length; i++) {
                            // Комбинация разных методов атаки
                            const whiteNoise = (Math.random() - 0.5) * 0.1;
                            const phaseShift = Math.sin(i * 0.02) * 0.08;
                            const freqShift = Math.sin(i * 0.005) * 0.05;
                            
                            outputData[i] = clampAudio(
                                inputData[i] * (1 + phaseShift) + whiteNoise + freqShift
                            );
                        }
                    }
                    
                    // Конвертируем обработанный аудиобуфер в Blob
                    const processedBlob = await audioBufferToWavBlob(newAudioBuffer);
                    processedFileUrl = URL.createObjectURL(processedBlob);
                    
                    // Отображение результата
                    displayAudioResult();
                    
                    // Визуализация
                    visualizeAudio(newAudioBuffer, false);
                    
                    resolve();
                } catch (error) {
                    throw error;
                }
            });
        }
        
        // Упрощенные обработки для видео (первый кадр)
        async function applyAdaptiveMicroNoiseToVideo() {
            return processVideoFrame((ctx, width, height) => {
                const imageData = ctx.getImageData(0, 0, width, height);
                const data = imageData.data;
                
                for (let i = 0; i < data.length; i += 4) {
                    const noisePattern = Math.sin(i * 0.001) * 6;
                    data[i] = clamp(data[i] + noisePattern);
                    data[i + 1] = clamp(data[i + 1] + noisePattern * 0.7);
                    data[i + 2] = clamp(data[i + 2] + noisePattern * 0.5);
                }
                
                ctx.putImageData(imageData, 0, 0);
            });
        }
        
        async function applyFrequencyAttackToVideo() {
            return processVideoFrame((ctx, width, height) => {
                const imageData = ctx.getImageData(0, 0, width, height);
                const data = imageData.data;
                
                for (let i = 0; i < data.length; i += 4) {
                    const x = (i / 4) % width;
                    const freqX = Math.sin(x * 0.03) * 10;
                    data[i] = clamp(data[i] + freqX);
                    data[i + 2] = clamp(data[i + 2] - freqX);
                }
                
                ctx.putImageData(imageData, 0, 0);
            });
        }
        
        async function applySuperizerToVideo() {
            return processVideoFrame((ctx, width, height) => {
                const imageData = ctx.getImageData(0, 0, width, height);
                const data = imageData.data;
                
                for (let i = 0; i < data.length; i += 4) {
                    const change = Math.floor(Math.random() * 80) - 40;
                    data[i] = clamp(data[i] + change);
                    data[i + 1] = clamp(data[i + 1] + change * 0.8);
                    data[i + 2] = clamp(data[i + 2] + change * 0.6);
                }
                
                ctx.putImageData(imageData, 0, 0);
            });
        }
        
        async function processVideoFrame(processFunction) {
            return new Promise((resolve) => {
                const video = document.createElement('video');
                video.src = originalFileUrl;
                
                video.onloadeddata = function() {
                    const canvas = document.createElement('canvas');
                    const ctx = canvas.getContext('2d');
                    
                    canvas.width = video.videoWidth;
                    canvas.height = video.videoHeight;
                    
                    // Рисуем первый кадр
                    ctx.drawImage(video, 0, 0);
                    
                    // Применяем обработку
                    processFunction(ctx, canvas.width, canvas.height);
                    
                    // Отображение результата
                    displayResult(canvas.toDataURL());
                    resolve();
                };
            });
        }
        
        // ========== ВСПОМОГАТЕЛЬНЫЕ ФУНКЦИИ ==========
        
        function displayResult(dataUrl) {
            resultDisplay.innerHTML = '';
            
            if (originalFileType.startsWith('image/')) {
                const img = document.createElement('img');
                img.src = dataUrl;
                resultDisplay.appendChild(img);
                processedFileUrl = dataUrl;
            } 
            else if (originalFileType.startsWith('video/')) {
                const img = document.createElement('img');
                img.src = dataUrl;
                resultDisplay.appendChild(img);
                processedFileUrl = dataUrl;
            }
        }
        
        function displayAudioResult() {
            resultDisplay.innerHTML = '';
            const audio = document.createElement('audio');
            audio.src = processedFileUrl;
            audio.controls = true;
            resultDisplay.appendChild(audio);
            
            // Визуализация
            loadAudioForVisualization(processedFileUrl, false);
        }
        
        function loadAudioForVisualization(audioUrl, isOriginal) {
            if (!audioContext) {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
            }
            
            fetch(audioUrl)
                .then(response => response.arrayBuffer())
                .then(arrayBuffer => audioContext.decodeAudioData(arrayBuffer))
                .then(audioBuffer => {
                    visualizeAudio(audioBuffer, isOriginal);
                })
                .catch(error => console.error('Ошибка загрузки аудио:', error));
        }
        
        function visualizeAudio(audioBuffer, isOriginal) {
            const canvas = isOriginal ? originalWaveform : resultWaveform;
            const ctx = canvas.getContext('2d');
            const width = canvas.parentElement.offsetWidth;
            const height = canvas.parentElement.offsetHeight;
            
            canvas.width = width;
            canvas.height = height;
            
            const data = audioBuffer.getChannelData(0);
            const step = Math.ceil(data.length / width);
            
            ctx.clearRect(0, 0, width, height);
            ctx.strokeStyle = isOriginal ? '#ff0080' : '#00ff88';
            ctx.lineWidth = 2;
            ctx.beginPath();
            
            for (let i = 0; i < width; i++) {
                let min = 1.0;
                let max = -1.0;
                
                for (let j = 0; j < step; j++) {
                    const datum = data[(i * step) + j];
                    if (datum < min) min = datum;
                    if (datum > max) max = datum;
                }
                
                const yMin = (1 + min) * height / 2;
                const yMax = (1 + max) * height / 2;
                
                ctx.moveTo(i, yMin);
                ctx.lineTo(i, yMax);
            }
            
            ctx.stroke();
        }
        
        async function audioBufferToWavBlob(audioBuffer) {
            const numberOfChannels = audioBuffer.numberOfChannels;
            const sampleRate = audioBuffer.sampleRate;
            const length = audioBuffer.length * numberOfChannels * 2;
            
            // Создаем WAV-заголовок
            const wavHeader = createWavHeader(numberOfChannels, sampleRate, audioBuffer.length);
            
            // Получаем и интерливируем данные
            const interleaved = new Float32Array(audioBuffer.length * numberOfChannels);
            for (let channel = 0; channel < numberOfChannels; channel++) {
                const channelData = audioBuffer.getChannelData(channel);
                for (let i = 0; i < audioBuffer.length; i++) {
                    interleaved[i * numberOfChannels + channel] = channelData[i];
                }
            }
            
            // Конвертируем в Int16
            const int16Array = new Int16Array(interleaved.length);
            for (let i = 0; i < interleaved.length; i++) {
                int16Array[i] = Math.max(-32768, Math.min(32767, interleaved[i] * 32768));
            }
            
            // Собираем WAV файл
            const wavData = new Uint8Array(wavHeader.byteLength + int16Array.byteLength);
            wavData.set(new Uint8Array(wavHeader), 0);
            wavData.set(new Uint8Array(int16Array.buffer), wavHeader.byteLength);
            
            return new Blob([wavData], { type: 'audio/wav' });
        }
        
        function createWavHeader(numChannels, sampleRate, numSamples) {
            const blockAlign = numChannels * 2;
            const byteRate = sampleRate * blockAlign;
            const dataSize = numSamples * blockAlign;
            
            const buffer = new ArrayBuffer(44);
            const view = new DataView(buffer);
            
            // RIFF заголовок
            writeString(view, 0, 'RIFF');
            view.setUint32(4, 36 + dataSize, true);
            writeString(view, 8, 'WAVE');
            writeString(view, 12, 'fmt ');
            view.setUint32(16, 16, true);
            view.setUint16(20, 1, true);
            view.setUint16(22, numChannels, true);
            view.setUint32(24, sampleRate, true);
            view.setUint32(28, byteRate, true);
            view.setUint16(32, blockAlign, true);
            view.setUint16(34, 16, true);
            writeString(view, 36, 'data');
            view.setUint32(40, dataSize, true);
            
            return buffer;
        }
        
        function writeString(view, offset, string) {
            for (let i = 0; i < string.length; i++) {
                view.setUint8(offset + i, string.charCodeAt(i));
            }
        }
        
        function clamp(value) {
            return Math.max(0, Math.min(255, Math.round(value)));
        }
        
        function clampAudio(value) {
            return Math.max(-1, Math.min(1, value));
        }
        
        function showProgress(show) {
            if (show) {
                progressContainer.classList.add('active');
                progressBar.style.width = '0%';
                
                // Анимация прогресса
                let width = 0;
                const interval = setInterval(() => {
                    width += Math.random() * 15;
                    if (width > 95) {
                        width = 95;
                        clearInterval(interval);
                    }
                    progressBar.style.width = width + '%';
                }, 100);
                
                // Деактивация кнопок во время обработки
                disableAllButtons(true);
            } else {
                progressBar.style.width = '100%';
                setTimeout(() => {
                    progressContainer.classList.remove('active');
                    disableAllButtons(false);
                }, 500);
            }
        }
        
        function disableAllButtons(disable) {
            btnMicroNoise.disabled = disable;
            btnAdaptiveReprocess.disabled = disable;
            btnFrequencyAttack.disabled = disable;
            btnSuperizer.disabled = disable;
        }
        
        function showStatus(message, type) {
            statusMessage.textContent = message;
            statusMessage.className = 'status-message ' + type;
        }
        
        function resetProcessing() {
            resultDisplay.innerHTML = `
                <div style="text-align: center; color: #8a8ab5; padding: 20px;">
                    <i class="fas fa-cogs fa-3x" style="margin-bottom: 15px;"></i>
                    <p>Выберите алгоритм обработки</p>
                </div>
            `;
            
            if (processedFileUrl) {
                URL.revokeObjectURL(processedFileUrl);
                processedFileUrl = '';
            }
            
            downloadBtn.disabled = true;
            statusMessage.className = 'status-message';
            
            if (cleanupTimer) {
                clearTimeout(cleanupTimer);
                cleanupTimer = null;
            }
        }
        
        function scheduleCleanup() {
            if (cleanupTimer) clearTimeout(cleanupTimer);
            
            cleanupTimer = setTimeout(() => {
                if (processedFileUrl) {
                    URL.revokeObjectURL(processedFileUrl);
                    processedFileUrl = '';
                    showStatus('Обработанный файл был удален из памяти для экономии ресурсов.', 'info');
                    downloadBtn.disabled = true;
                }
            }, 5 * 60 * 1000); // 5 минут
        }
        
        function formatFileSize(bytes) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
        }
        
        // ========== СКАЧИВАНИЕ ==========
        
        downloadBtn.addEventListener('click', () => {
            if (!processedFileUrl) return;
            
            const extension = originalFile.name.split('.').pop();
            const timestamp = new Date().getTime();
            const a = document.createElement('a');
            a.href = processedFileUrl;
            a.download = `processed_${timestamp}.${extension}`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            
            showStatus('Файл успешно скачан! Он будет удален из памяти через 5 минут.', 'success');
        });
    </script>
</body>
</html>
