# City-Time

<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Время в городе</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
            padding: 20px;
        }
        .card {
            background: rgba(255, 255, 255, 0.12);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-radius: 40px;
            padding: 40px 35px;
            max-width: 500px;
            width: 100%;
            box-shadow: 0 30px 50px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.15);
            transition: 0.3s;
            text-align: center;
            color: #fff;
        }
        h1 {
            font-weight: 400;
            font-size: 26px;
            letter-spacing: 1px;
            margin-bottom: 8px;
            opacity: 0.9;
        }
        .sub {
            font-size: 14px;
            opacity: 0.7;
            margin-bottom: 30px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            padding-bottom: 20px;
        }
        .input-group {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 25px;
        }
        .input-group input {
            flex: 1;
            min-width: 160px;
            padding: 16px 20px;
            border: none;
            border-radius: 60px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(4px);
            color: #fff;
            font-size: 16px;
            outline: 2px solid transparent;
            transition: 0.3s;
        }
        .input-group input::placeholder {
            color: rgba(255, 255, 255, 0.5);
            font-weight: 300;
        }
        .input-group input:focus {
            outline: 2px solid rgba(255, 255, 255, 0.6);
            background: rgba(255, 255, 255, 0.2);
        }
        .input-group button {
            padding: 16px 30px;
            border: none;
            border-radius: 60px;
            background: #f7c948;
            color: #1e2a4a;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 8px 20px rgba(247, 201, 72, 0.25);
            letter-spacing: 0.3px;
        }
        .input-group button:hover {
            background: #ffd966;
            transform: scale(1.02);
            box-shadow: 0 12px 28px rgba(247, 201, 72, 0.4);
        }
        .input-group button:active {
            transform: scale(0.96);
        }
        .quick-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            justify-content: center;
            margin-bottom: 20px;
        }
        .quick-buttons button {
            padding: 8px 16px;
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 30px;
            background: rgba(255,255,255,0.05);
            color: #fff;
            font-size: 13px;
            cursor: pointer;
            transition: 0.2s;
            backdrop-filter: blur(4px);
        }
        .quick-buttons button:hover {
            background: rgba(255,255,255,0.15);
            transform: scale(1.05);
        }
        .result-box {
            margin-top: 12px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 30px;
            padding: 22px 16px;
            border: 1px solid rgba(255,255,255,0.05);
            min-height: 85px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .city-name {
            font-size: 22px;
            font-weight: 300;
            letter-spacing: 1px;
            opacity: 0.9;
        }
        .time-display {
            font-size: 48px;
            font-weight: 300;
            letter-spacing: 2px;
            margin: 8px 0 4px;
            font-variant-numeric: tabular-nums;
            color: #f7c948;
            text-shadow: 0 0 20px rgba(247, 201, 72, 0.15);
        }
        .timezone-offset {
            font-size: 14px;
            opacity: 0.6;
            margin-top: 4px;
        }
        .error-msg {
            color: #ffb3b3;
            font-size: 15px;
            background: rgba(255, 80, 80, 0.15);
            padding: 8px 16px;
            border-radius: 40px;
            display: inline-block;
        }
        .footer-note {
            margin-top: 25px;
            font-size: 12px;
            opacity: 0.4;
            letter-spacing: 0.5px;
        }
        .status-badge {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            background: rgba(0,255,0,0.15);
            color: #7dff7d;
            font-size: 11px;
            margin-top: 8px;
            border: 1px solid rgba(0,255,0,0.1);
        }
        @media (max-width: 450px) {
            .card { padding: 30px 18px; }
            .time-display { font-size: 36px; }
            .input-group input { min-width: 130px; }
        }
    </style>
</head>
<body>

<div class="card">
    <h1>🕒 Время в городе</h1>
    <div class="sub">Введите город на русском или английском</div>

    <div class="quick-buttons">
        <button onclick="setCity('Москва')">Москва</button>
        <button onclick="setCity('London')">Лондон</button>
        <button onclick="setCity('New York')">Нью-Йорк</button>
        <button onclick="setCity('Tokyo')">Токио</button>
        <button onclick="setCity('Paris')">Париж</button>
        <button onclick="setCity('Dubai')">Дубай</button>
    </div>

    <div class="input-group">
        <input type="text" id="cityInput" placeholder="Например: Москва, London, Токио" value="Москва">
        <button id="getTimeBtn">Узнать время</button>
    </div>

    <div class="result-box" id="resultBox">
        <div class="city-name" id="cityName">Москва</div>
        <div class="time-display" id="timeDisplay">--:--:--</div>
        <div class="timezone-offset" id="timezoneOffset">UTC+3</div>
        <div class="status-badge">✅ API готов к работе</div>
    </div>
    <div class="footer-note">Данные с TimeAPI.io • Работает с ИИ-ассистентом</div>
</div>

<script>
    (function() {
        const cityInput = document.getElementById('cityInput');
        const getTimeBtn = document.getElementById('getTimeBtn');
        const cityName = document.getElementById('cityName');
        const timeDisplay = document.getElementById('timeDisplay');
        const timezoneOffset = document.getElementById('timezoneOffset');

        // Функция для получения часового пояса по названию города
        async function getTimeZoneFromCity(city) {
            const geocodeUrl = `https://nominatim.openstreetmap.org/search?q=${encodeURIComponent(city)}&format=json&limit=1`;
            
            const response = await fetch(geocodeUrl, {
                headers: {
                    'User-Agent': 'CityTimeApp/1.0'
                }
            });

            if (!response.ok) {
                throw new Error(`Геокодинг не удался: ${response.status}`);
            }

            const data = await response.json();
            
            if (!data || data.length === 0) {
                throw new Error(`Город "${city}" не найден`);
            }

            const lat = parseFloat(data[0].lat);
            const lon = parseFloat(data[0].lon);
            const displayName = data[0].display_name;

            const timezoneUrl = `https://timeapi.io/api/Time/current/coordinate?latitude=${lat}&longitude=${lon}`;
            
            const timeResponse = await fetch(timezoneUrl);
            
            if (!timeResponse.ok) {
                throw new Error(`Ошибка получения времени: ${timeResponse.status}`);
            }

            const timeData = await timeResponse.json();
            
            if (!timeData || !timeData.dateTime) {
                throw new Error('Некорректный ответ от сервера');
            }

            return {
                timeData: timeData,
                displayName: displayName,
                timeZone: timeData.timeZone || 'Unknown'
            };
        }

        // Основная функция получения времени
        async function fetchTimeForCity(city) {
            if (!city || city.trim() === '') {
                setError('Введите название города');
                return null;
            }

            const cleanCity = city.trim();
            
            cityName.textContent = cleanCity;
            timeDisplay.textContent = '⏳';
            timezoneOffset.textContent = 'Поиск...';

            try {
                const result = await getTimeZoneFromCity(cleanCity);
                
                const dateObj = new Date(result.timeData.dateTime);
                if (isNaN(dateObj.getTime())) {
                    throw new Error('Некорректная дата');
                }

                const hours = String(dateObj.getHours()).padStart(2, '0');
                const minutes = String(dateObj.getMinutes()).padStart(2, '0');
                const seconds = String(dateObj.getSeconds()).padStart(2, '0');
                const formattedTime = `${hours}:${minutes}:${seconds}`;

                const offsetMinutes = dateObj.getTimezoneOffset();
                const offsetHours = Math.floor(Math.abs(offsetMinutes) / 60);
                const offsetMins = Math.abs(offsetMinutes) % 60;
                const sign = offsetMinutes <= 0 ? '+' : '-';
                let offsetStr = `UTC${sign}${offsetHours}`;
                if (offsetMins !== 0) offsetStr += `:${String(offsetMins).padStart(2, '0')}`;

                cityName.textContent = result.timeZone;
                timeDisplay.textContent = formattedTime;
                timezoneOffset.textContent = offsetStr;

                // Возвращаем данные для API
                return {
                    success: true,
                    city: result.timeZone,
                    time: formattedTime,
                    fullTime: dateObj.toLocaleTimeString('ru-RU'),
                    date: dateObj.toLocaleDateString('ru-RU', { 
                        day: '2-digit', 
                        month: '2-digit', 
                        year: 'numeric' 
                    }),
                    timezone: offsetStr,
                    raw: result.timeData
                };

            } catch (error) {
                console.error('Ошибка:', error);
                setError(error.message || `Не удалось найти город "${cleanCity}"`);
                return {
                    success: false,
                    error: error.message || `Город "${cleanCity}" не найден`
                };
            }
        }

        function setError(message) {
            cityName.textContent = '❌ Ошибка';
            timeDisplay.textContent = '--:--:--';
            timezoneOffset.textContent = message;
        }

        function setCity(city) {
            cityInput.value = city;
            fetchTimeForCity(city);
        }

        function handleGetTime() {
            const city = cityInput.value.trim();
            if (city) {
                fetchTimeForCity(city);
            } else {
                setError('Введите город');
                cityInput.focus();
            }
        }

        // === API ДЛЯ ВНЕШНЕГО ВЗАИМОДЕЙСТВИЯ (ДЛЯ ИИ-АССИСТЕНТА) ===
        
        // Глобальная функция для получения времени (доступна извне)
        window.getCityTime = async function(city) {
            return await fetchTimeForCity(city);
        };

        // Обработка сообщений от родительского окна (iframe)
        window.addEventListener('message', async function(event) {
            // Проверяем, что сообщение от нашего приложения
            if (event.data && event.data.type === 'getTime') {
                const city = event.data.city || 'Москва';
                const result = await fetchTimeForCity(city);
                
                // Отправляем ответ обратно
                if (event.source) {
                    event.source.postMessage({
                        type: 'timeResponse',
                        data: result,
                        requestId: event.data.requestId || null
                    }, '*');
                }
            }
        });

        // Обработка API-запросов через URL параметры (для прямых запросов)
        if (window.location.search.includes('api=true')) {
            const params = new URLSearchParams(window.location.search);
            const city = params.get('city') || 'Москва';
            
            // Отвечаем JSON для прямых API-запросов
            fetchTimeForCity(city).then(data => {
                // Если запрос пришёл из iframe, отправляем через postMessage
                if (window.parent && window.parent !== window) {
                    window.parent.postMessage({
                        type: 'timeData',
                        data: data
                    }, '*');
                }
                
                // Если запрос прямой, выводим JSON
                if (!window.parent || window.parent === window) {
                    document.body.innerHTML = `<pre style="color: white; padding: 20px;">${JSON.stringify(data, null, 2)}</pre>`;
                }
            });
        }

        // === ОБРАБОТЧИКИ СОБЫТИЙ ===

        cityInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                e.preventDefault();
                handleGetTime();
            }
        });

        getTimeBtn.addEventListener('click', handleGetTime);

        // Загружаем время для Москвы при старте
        window.addEventListener('DOMContentLoaded', () => {
            setTimeout(() => {
                fetchTimeForCity('Москва');
            }, 200);
        });

        cityInput.addEventListener('focus', function() {
            this.select();
        });

        // Экспортируем функции для глобального доступа
        window.setCity = setCity;
        window.fetchTimeForCity = fetchTimeForCity;

    })();
</script>
</body>
</html>
