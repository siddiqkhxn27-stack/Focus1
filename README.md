<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FOCUS App - Elite Edition</title>
    <style>
        :root {
            --primary-blue: #003366;
            --secondary-blue: #007bff;
            --glass-bg: rgba(255, 255, 255, 0.95);
            --text-dark: #1a1a1a;
            --accent-green: #2ecc71;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Roboto, sans-serif; }

        body {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            background-attachment: fixed;
            color: var(--text-dark);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header { color: white; text-align: center; padding: 2.5rem 1rem; }
        header h1 { font-size: 3.5rem; letter-spacing: 8px; text-shadow: 0 5px 15px rgba(0,0,0,0.3); margin-bottom: 5px; }
        header p { font-size: 0.9rem; letter-spacing: 1.5px; opacity: 0.9; font-weight: 600; text-transform: uppercase; }

        main { max-width: 700px; margin: 0 auto 3rem auto; padding: 0 1.5rem; width: 100%; }

        .container-card {
            background: var(--glass-bg);
            padding: 2.5rem;
            border-radius: 25px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.3);
        }

        h2.section-title {
            color: var(--primary-blue);
            margin-bottom: 1.5rem;
            font-size: 1rem;
            border-bottom: 2px solid #eef;
            padding-bottom: 10px;
            text-transform: uppercase;
            font-weight: 800;
        }

        .app-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            gap: 15px;
            margin-bottom: 2rem;
        }

        .app-card {
            background-color: #fff;
            border: 2px solid #f0f0f0;
            border-radius: 18px;
            padding: 15px 5px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
        }

        .app-card input[type="checkbox"] { position: absolute; opacity: 0; }
        
        .logo-box {
            width: 45px;
            height: 45px;
            margin: 0 auto 8px auto;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .app-logo { width: 100%; height: 100%; object-fit: contain; border-radius: 10px; }
        .logo-fallback { display: none; font-size: 0.8rem; font-weight: bold; color: #666; }

        .app-name { font-size: 0.75rem; font-weight: 700; color: #444; display: block; }

        .app-card:hover { transform: translateY(-5px); box-shadow: 0 5px 15px rgba(0,0,0,0.1); }

        .app-card:has(input:checked) {
            background-color: var(--secondary-blue);
            border-color: var(--primary-blue);
            color: white;
        }
        .app-card:has(input:checked) .app-name { color: white; }

        /* --- Refined Add More Card & Animation --- */
        .add-more-card {
            border: 2px dashed var(--secondary-blue);
            background: rgba(0, 123, 255, 0.02);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border-radius: 18px;
            min-height: 108px;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .plus-icon-circle {
            width: 38px;
            height: 38px;
            background: var(--secondary-blue);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.6rem;
            margin-bottom: 8px;
            transition: all 0.4s ease;
        }

        .add-more-card:hover {
            background: rgba(0, 123, 255, 0.1);
            border-color: var(--primary-blue);
            transform: translateY(-5px);
        }

        .add-more-card:hover .plus-icon-circle {
            transform: rotate(180deg);
            background: var(--primary-blue);
            box-shadow: 0 0 15px rgba(0, 123, 255, 0.5);
        }

        .start-btn {
            width: 100%;
            padding: 20px;
            background: linear-gradient(45deg, #0056b3, #00c6ff);
            color: white;
            border: none;
            border-radius: 15px;
            font-size: 1.2rem;
            font-weight: 900;
            cursor: pointer;
            box-shadow: 0 8px 15px rgba(0, 86, 179, 0.2);
            transition: all 0.3s ease;
        }

        .start-btn:hover { transform: scale(1.02); box-shadow: 0 10px 20px rgba(0, 86, 179, 0.4); }

        .time-inputs { display: flex; gap: 10px; margin-bottom: 1.5rem; }
        .time-box { flex: 1; text-align: center; }
        .time-box label { font-size: 0.65rem; font-weight: 800; color: #888; display: block; margin-bottom: 5px; }

        input[type="number"], input[type="text"] {
            width: 100%;
            padding: 15px;
            border: 2px solid #eee;
            border-radius: 12px;
            outline: none;
            text-align: center;
            font-weight: 600;
        }

        .screen { text-align: center; }
        .user-message-display { font-size: 2.5rem; font-weight: 900; color: var(--primary-blue); margin: 2rem 0; }
        #main-timer { font-size: 5rem; font-weight: bold; color: #333; margin: 1rem 0; letter-spacing: -2px; }
        .congrats-title { color: var(--accent-green); font-size: 2.5rem; margin-bottom: 1rem; }

        .hidden { display: none !important; }
    </style>
</head>
<body>

    <header>
        <h1>FOCUS</h1>
        <p>RE CLAIMS YOUR ATTENTION BY BUILDING FOCUS</p>
    </header>

    <main>
        <section id="setup-panel" class="container-card">
            <h2 class="section-title">1. SELECT DISTRACTION APPS TO BLOCK</h2>
            <div class="app-grid">
                
                <label class="app-card">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/2023_Facebook_icon.svg" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">FB</span>
                    </div>
                    <span class="app-name">Facebook</span>
                </label>

                <label class="app-card">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/0/09/YouTube_full-color_icon_%282017%29.svg" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">YT</span>
                    </div>
                    <span class="app-name">YouTube</span>
                </label>

                <label class="app-card">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">IG</span>
                    </div>
                    <span class="app-name">Instagram</span>
                </label>

                <label class="app-card extra-app hidden">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">WA</span>
                    </div>
                    <span class="app-name">WhatsApp</span>
                </label>

                <label class="app-card extra-app hidden">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/0/08/Netflix_2015_logo.svg" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">Netflix</span>
                    </div>
                    <span class="app-name">Netflix</span>
                </label>

                <label class="app-card extra-app hidden">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/1/12/Disney%2B_Hotstar_logo.svg" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">Hotstar</span>
                    </div>
                    <span class="app-name">Hotstar</span>
                </label>

                <label class="app-card extra-app hidden">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/en/a/a9/PUBG_Mobile_Logo.png" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">PUBG</span>
                    </div>
                    <span class="app-name">PUBG</span>
                </label>

                <label class="app-card extra-app hidden">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/en/5/51/Minecraft_cover.png" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">MC</span>
                    </div>
                    <span class="app-name">Minecraft</span>
                </label>

                <label class="app-card extra-app hidden">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/en/b/b1/Candy_Crush_Saga_logo.png" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">Candy</span>
                    </div>
                    <span class="app-name">Candy Crush</span>
                </label>

                <label class="app-card extra-app hidden">
                    <input type="checkbox">
                    <div class="logo-box">
                        <img src="https://upload.wikimedia.org/wikipedia/en/d/d3/Subway_Surfers_App_Icon.png" class="app-logo" onerror="handleError(this)">
                        <span class="logo-fallback">Subway</span>
                    </div>
                    <span class="app-name">Subway Surf</span>
                </label>

                <div class="add-more-card" id="add-more-btn">
                    <div class="plus-icon-circle">+</div>
                    <span class="app-name">Add More</span>
                </div>
            </div>

            <h2 class="section-title">2. Session Details</h2>
            <div class="time-inputs">
                <div class="time-box"><label>HH</label><input type="number" id="hr" placeholder="0" min="0"></div>
                <div class="time-box"><label>MM</label><input type="number" id="min" placeholder="0" min="0"></div>
                <div class="time-box"><label>SS</label><input type="number" id="sec" placeholder="0" min="0"></div>
            </div>

            <div style="margin-bottom: 2rem;">
                <label style="font-size: 0.7rem; font-weight: bold; color: #888; text-transform: uppercase;">Motivation Message</label>
                <input type="text" id="msg" placeholder="e.g., DO THE WORK FIRST">
            </div>

            <button id="start-btn" class="start-btn">START FOCUSING NOW</button>
        </section>

        <section id="timer-screen" class="container-card screen hidden">
            <h2 style="color:var(--primary-blue); font-size: 1rem; margin-bottom: 10px;">START BEING FOCUSED</h2>
            <div id="display-msg" class="user-message-display"></div>
            <div id="main-timer">00:00:00</div>
            <p style="color: #666;">Distractions are currently restricted.</p>
        </section>

        <section id="congrats-screen" class="container-card screen hidden">
            <div style="font-size: 5rem;">🎉</div>
            <h1 class="congrats-title">EXCELLENT WORK!</h1>
            <p style="font-size: 1.3rem; margin-bottom: 2rem; color: #444; font-weight: 600;">
                Congrates you complete the task by being focus
            </p>
            <button onclick="location.reload()" class="start-btn">FINISH</button>
        </section>
    </main>

    <script>
        function handleError(img) {
            img.style.display = 'none';
            img.nextElementSibling.style.display = 'block';
        }

        document.getElementById('add-more-btn').addEventListener('click', function() {
            const extraApps = document.querySelectorAll('.extra-app');
            extraApps.forEach(el => el.classList.remove('hidden'));
            this.style.opacity = '0';
            setTimeout(() => this.classList.add('hidden'), 400);
        });

        document.getElementById('start-btn').addEventListener('click', function() {
            const h = parseInt(document.getElementById('hr').value) || 0;
            const m = parseInt(document.getElementById('min').value) || 0;
            const s = parseInt(document.getElementById('sec').value) || 0;
            const userMsg = document.getElementById('msg').value || "DO THE WORK FIRST";

            let totalTime = (h * 3600) + (m * 60) + s;

            if (totalTime <= 0) {
                alert("Please set a time!");
                return;
            }

            document.getElementById('setup-panel').classList.add('hidden');
            document.getElementById('timer-screen').classList.remove('hidden');
            document.getElementById('display-msg').textContent = userMsg;
            
            const mainTimer = document.getElementById('main-timer');

            const countdown = setInterval(() => {
                if (totalTime <= 0) {
                    clearInterval(countdown);
                    document.getElementById('timer-screen').classList.add('hidden');
                    document.getElementById('congrats-screen').classList.remove('hidden');
                    return;
                }

                totalTime--;
                const hrs = Math.floor(totalTime / 3600);
                const mins = Math.floor((totalTime % 3600) / 60);
                const secs = totalTime % 60;

                mainTimer.textContent = 
                    `${String(hrs).padStart(2, '0')}:${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
            }, 1000);
        });
    </script>
</body>
</html>
