<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Debra's 單字冒險樂園 🏡</title>
    <style>
        :root {
            --bg-color: #fdf2f8;
            --card-bg: #ffffff;
            --primary: #ec4899;
            --primary-light: #fbcfe8;
            --secondary: #8b5cf6;
            --accent: #f43f5e;
            --text-color: #374151;
            --border-radius: 20px;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            width: 100%;
            max-width: 800px;
            background: var(--card-bg);
            border-radius: var(--border-radius);
            box-shadow: 0 10px 25px rgba(236, 72, 153, 0.1);
            padding: 30px;
            box-sizing: border-box;
            position: relative;
        }

        header {
            text-align: center;
            margin-bottom: 25px;
            border-bottom: 2px dashed var(--primary-light);
            padding-bottom: 15px;
        }

        h1 {
            color: var(--primary);
            margin: 0 0 10px 0;
            font-size: 1.8rem;
        }

        .stats-bar {
            display: flex;
            justify-content: center;
            gap: 20px;
            font-size: 1.1rem;
            font-weight: bold;
            color: #6b7280;
            margin-top: 10px;
        }

        .badge {
            background: #fef3c7;
            color: #d97706;
            padding: 5px 12px;
            border-radius: 20px;
            display: inline-flex;
            align-items: center;
            gap: 5px;
        }

        .trophy-badge {
            background: #ede9fe;
            color: #7c3aed;
            padding: 5px 12px;
            border-radius: 20px;
            display: inline-flex;
            align-items: center;
            gap: 5px;
        }

        /* 導覽與選擇介面 */
        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .btn {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 15px 20px;
            border-radius: 15px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(236, 72, 153, 0.3);
        }

        .btn-secondary {
            background: white;
            color: var(--primary);
            border: 2px solid var(--primary);
        }

        .back-btn {
            background: #e5e7eb;
            color: #4b5563;
            padding: 8px 15px;
            border-radius: 10px;
            border: none;
            cursor: pointer;
            font-weight: bold;
            margin-bottom: 15px;
        }

        /* 遊戲介面通用樣式 */
        .game-card {
            background: #fdf4f8;
            border-radius: 15px;
            padding: 25px;
            text-align: center;
            margin-top: 15px;
            border: 2px solid var(--primary-light);
        }

        input[type="text"] {
            padding: 12px 20px;
            font-size: 1.1rem;
            border: 2px solid #cbd5e1;
            border-radius: 10px;
            width: 70%;
            max-width: 300px;
            margin-top: 10px;
            text-align: center;
            outline: none;
        }

        input[type="text"]:focus {
            border-color: var(--primary);
        }

        .options-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 10px;
            margin-top: 15px;
        }

        .option-btn {
            background: white;
            border: 2px solid #fbcfe8;
            padding: 12px;
            border-radius: 10px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.2s;
            text-align: left;
        }

        .option-btn:hover {
            background: var(--primary-light);
            border-color: var(--primary);
        }

        .feedback {
            margin-top: 15px;
            font-weight: bold;
            font-size: 1.1rem;
            min-height: 30px;
        }

        .hint-box {
            background: #e0f2fe;
            color: #0369a1;
            padding: 10px;
            border-radius: 8px;
            font-size: 0.9rem;
            margin-top: 10px;
            display: inline-block;
        }

        /* 配對遊戲樣式 */
        .matching-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 15px;
        }

        .match-card {
            background: white;
            border: 2px solid #cbd5e1;
            padding: 15px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s;
        }

        .match-card.selected {
            border-color: var(--secondary);
            background: #ede9fe;
        }

        .match-card.matched {
            background: #d1fae5;
            border-color: #34d399;
            color: #065f46;
            cursor: default;
        }

        .hidden { display: none !important; }
    </style>
</head>
<body>

<div class="container" id="app">
    <header>
        <h1>🏡 Debra's 單字冒險樂園</h1>
        <p>法鬥 Cookie 與您一起快樂學英語！</p>
        <div class="stats-bar">
            <div class="badge">🪙 金幣：<span id="coin-count">0</span></div>
            <div class="trophy-badge">🏆 金獎盃：<span id="trophy-count">0</span> (100金幣/座)</div>
        </div>
    </header>

    <!-- 主選單：選擇課程 -->
    <div id="lesson-menu">
        <h3>📚 請選擇學習單元：</h3>
        <div class="menu-grid" id="lesson-list">
            <!-- 動態生成課程 -->
        </div>
    </div>

    <!-- 單元內模式選單 -->
    <div id="mode-menu" class="hidden">
        <button class="back-btn" onclick="app.showLessonMenu()">⬅ 返回課程選單</button>
        <h2 id="current-lesson-title" style="color: var(--secondary);">單元名稱</h2>
        <p>請選擇挑戰模式：</p>
        <div class="menu-grid">
            <button class="btn" onclick="app.startMode(1)">
                🔊 <span>模式一：聽字填單字</span>
                <small style="font-size:0.8rem; font-weight:normal;">聆聽發音或看中文拼出單字</small>
            </button>
            <button class="btn" onclick="app.startMode(2)">
                📝 <span>模式二：文法選擇題</span>
                <small style="font-size:0.8rem; font-weight:normal;">動詞三態、時態與文法大考驗</small>
            </button>
            <button class="btn" onclick="app.startMode(3)">
                🧩 <span>模式三：單字配對卡牌</span>
                <small style="font-size:0.8rem; font-weight:normal;">英文與中文連線配對遊戲</small>
            </button>
        </div>
    </div>

    <!-- 遊戲互動區 -->
    <div id="game-area" class="hidden">
        <button class="back-btn" onclick="app.showModeMenu()">⬅ 返回模式選單</button>
        <div id="game-content"></div>
    </div>
</div>

<script>
    // 完整的 R7 課程資料庫
    const curriculumData = [
        {
            id: 1,
            title: "Unit 1: 動詞三態與變化 (Verbs & Forms)",
            words: [
                { word: "pour", translation: "傾注、倒", past: "poured", pp: "poured", hint: "V. 倒水、倒茶" },
                { word: "add", translation: "增加、附加", past: "added", pp: "added", hint: "V. 加上去" },
                { word: "allow", translation: "允許", past: "allowed", pp: "allowed", hint: "V. 准許某人做某事" },
                { word: "happen", translation: "發生", past: "happened", pp: "happened", hint: "V. 事情發生了" },
                { word: "argue", translation: "爭吵、爭辯", past: "argued", pp: "argued", hint: "V. 口角爭執" }
            ],
            grammarQuestions: [
                { q: "Jack ________ an accident on his way home yesterday. (過去式)", options: ["happened", "was happened", "happen", "happening"], answer: 0, hint: "注意 happen 的用法：事情 + happened to + 人" },
                { q: "We are not ________ to go outside after 10 PM.", options: ["allow", "allowing", "allowed", "allows"], answer: 2, hint: "被動語態：be not allowed to do sth" },
                { q: "He ________ three new words to his vocabulary list this morning.", options: ["add", "added", "adding", "adds"], answer: 1, hint: "發生在過去的時間，動詞要用過去式" }
            ]
        },
        {
            id: 2,
            title: "Unit 2: 情感與狀態形容詞 (Emotions)",
            words: [
                { word: "amazed", translation: "感到驚訝的", hint: "Adj. 某人感到驚訝的" },
                { word: "bored", translation: "覺得無聊的", hint: "Adj. 某人覺得無趣的" },
                { word: "excited", translation: "感到興奮的", hint: "Adj. 某人感到情緒高漲的" },
                { word: "surprised", translation: "感到驚奇的", hint: "Adj. 感到意外的" },
                { word: "tired", translation: "疲倦的、厭煩的", hint: "Adj. 覺得很累的" }
            ],
            grammarQuestions: [
                { q: "I was so ________ about the upcoming trip to Japan. (現在/過去情緒)", options: ["excite", "exciting", "excited", "excitement"], answer: 2, hint: "形容人的感受，情緒動詞要用 p.p. 形式 (-ed)" },
                { q: "The movie was so ________ that I fell asleep halfway.", options: ["boring", "bored", "bore", "boredom"], answer: 0, hint: "形容事物本身令人感到無聊，用 -ing 形容詞" },
                { q: "He is ________ of doing the same thing every single day.", options: ["tired", "tire", "tiring", "tiredly"], answer: 0, hint: "固定片語：be tired of + N/V-ing" }
            ]
        },
        {
            id: 3,
            title: "Unit 3: 日常生活與動作 (Daily Life & Actions)",
            words: [
                { word: "traffic", translation: "交通、運輸", hint: "N. 馬路上的車流量" },
                { word: "flight", translation: "飛行、航班", hint: "N. 搭飛機的班次" },
                { word: "arrive", translation: "到達、抵達", hint: "V. 抵達某地 (arrive at/in)" },
                { word: "cancel", translation: "取消、放棄", hint: "V. 把行程取消" },
                { word: "avoid", translation: "迴避、防止", hint: "V. 避免去做某事" }
            ],
            grammarQuestions: [
                { q: "We ________ our trip to Japan because of the heavy typhoon last week.", options: ["cancel", "cancels", "cancelled", "cancelling"], answer: 2, hint: "發生在上週，要用過去式" },
                { q: "I try to avoid ________ shopping on crowded Saturday afternoons.", options: ["go", "to go", "going", "went"], answer: 2, hint: "avoid 後方接動名詞 (V-ing)" },
                { q: "The train will ________ at the station in ten minutes. (未來式)", options: ["arrive", "arrived", "arriving", "arrives"], answer: 0, hint: "助動詞 will 後方接原形動詞" }
            ]
        }
    ];

    class App {
        constructor() {
            this.coins = parseInt(localStorage.getItem('deb_coins')) || 0;
            this.currentLesson = null;
            this.currentMode = null;
            this.currentIndex = 0;
            this.score = 0;
            this.updateStats();
            this.initLessonMenu();
        }

        updateStats() {
            document.getElementById('coin-count').innerText = this.coins;
            let trophies = Math.floor(this.coins / 100);
            document.getElementById('trophy-count').innerText = trophies;
            localStorage.setItem('deb_coins', this.coins);
        }

        addCoins(amount) {
            this.coins += amount;
            this.updateStats();
        }

        initLessonMenu() {
            const menu = document.getElementById('lesson-list');
            menu.innerHTML = '';
            curriculumData.forEach(lesson => {
                const btn = document.createElement('button');
                btn.className = 'btn';
                btn.innerHTML = `📖 <span>${lesson.title}</span> <small>${lesson.words.length} 個核心單字</small>`;
                btn.onclick = () => this.selectLesson(lesson.id);
                menu.appendChild(btn);
            });
        }

        selectLesson(id) {
            this.currentLesson = curriculumData.find(l => l.id === id);
            document.getElementById('current-lesson-title').innerText = this.currentLesson.title;
            document.getElementById('lesson-menu').classList.add('hidden');
            document.getElementById('mode-menu').classList.remove('hidden');
        }

        showLessonMenu() {
            document.getElementById('mode-menu').classList.add('hidden');
            document.getElementById('game-area').classList.add('hidden');
            document.getElementById('lesson-menu').classList.remove('hidden');
        }

        showModeMenu() {
            document.getElementById('game-area').classList.add('hidden');
            document.getElementById('mode-menu').classList.remove('hidden');
        }

        startMode(mode) {
            this.currentMode = mode;
            this.currentIndex = 0;
            document.getElementById('mode-menu').classList.add('hidden');
            document.getElementById('game-area').classList.remove('hidden');
            this.loadGameQuestion();
        }

        loadGameQuestion() {
            const container = document.getElementById('game-content');
            container.innerHTML = '';

            if (this.currentMode === 1) {
                // 模式一：聽字填單字
                if (this.currentIndex >= this.currentLesson.words.length) {
                    container.innerHTML = `<h3>🎉 恭喜完成本單元聽字填單字挑戰！</h3><button class="btn" onclick="app.showModeMenu()">返回模式選單</button>`;
                    return;
                }
                const item = this.currentLesson.words[this.currentIndex];
                container.innerHTML = `
                    <h3>🔊 模式一：聽字填單字 (${this.currentIndex + 1}/${this.currentLesson.words.length})</h3>
                    <div class="game-card">
                        <button class="btn" style="margin: 0 auto 15px auto; padding: 10px 20px;" onclick="app.speakWord('${item.word}')">🔊 點擊播放發音</button>
                        <p>中文意思：<strong>${item.translation}</strong></p>
                        <div class="hint-box">💡 提示：${item.hint}</div><br>
                        <input type="text" id="user-answer" placeholder="請輸入英文單字..." autocomplete="off">
                        <div class="options-grid" style="margin-top: 15px;">
                            <button class="btn" onclick="app.checkWordAnswer('${item.word}')">提交答案</button>
                        </div>
                        <div class="feedback" id="feedback"></div>
                    </div>
                `;
            } else if (this.currentMode === 2) {
                // 模式二：文法選擇題
                if (this.currentIndex >= this.currentLesson.grammarQuestions.length) {
                    container.innerHTML = `<h3>🎉 恭喜完成本單元文法挑戰！</h3><button class="btn" onclick="app.showModeMenu()">返回模式選單</button>`;
                    return;
                }
                const qData = this.currentLesson.grammarQuestions[this.currentIndex];
                let optionsHtml = '';
                qData.options.forEach((opt, idx) => {
                    optionsHtml += `<button class="option-btn" onclick="app.checkGrammarAnswer(${idx}, ${qData.answer})">${idx + 1}. ${opt}</button>`;
                });
                container.innerHTML = `
                    <h3>📝 模式二：文法與三態選擇題 (${this.currentIndex + 1}/${this.currentLesson.grammarQuestions.length})</h3>
                    <div class="game-card" style="text-align: left;">
                        <p style="font-size: 1.1rem; font-weight: bold;">Q: ${qData.q}</p>
                        <div class="hint-box" style="width:100%; box-sizing:border-box;">💡 老師提示：${qData.hint}</div>
                        <div class="options-grid" style="margin-top: 15px;">${optionsHtml}</div>
                        <div class="feedback" id="feedback" style="text-align: center;"></div>
                    </div>
                `;
            } else if (this.currentMode === 3) {
                // 模式三：配對遊戲
                this.loadMatchingGame();
            }
        }

        speakWord(word) {
            const utterance = new SpeechSynthesisUtterance(word);
            utterance.lang = 'en-US';
            window.speechSynthesis.speak(utterance);
        }

        checkWordAnswer(correctWord) {
            const userAns = document.getElementById('user-answer').value.trim().toLowerCase();
            const fb = document.getElementById('feedback');
            if (userAns === correctWord.toLowerCase()) {
                fb.style.color = '#059669';
                fb.innerHTML = '✨ 答對了！太棒囉！ (+1 金幣 🪙)';
                this.addCoins(1);
                setTimeout(() => {
                    this.currentIndex++;
                    this.loadGameQuestion();
                }, 1200);
            } else {
                fb.style.color = '#dc2626';
                fb.innerHTML = `❌ 哎呀，正確答案是：<strong>${correctWord}</strong>`;
            }
        }

        checkGrammarAnswer(selected, correct) {
            const fb = document.getElementById('feedback');
            const buttons = document.querySelectorAll('.option-btn');
            buttons.forEach(b => b.disabled = true);

            if (selected === correct) {
                buttons[selected].style.background = '#d1fae5';
                buttons[selected].style.borderColor = '#34d399';
                fb.style.color = '#059669';
                fb.innerHTML = '✨ 答對了！文法概念真棒！ (+1 金幣 🪙)';
                this.addCoins(1);
            } else {
                buttons[selected].style.background = '#fee2e2';
                buttons[selected].style.borderColor = '#f87171';
                buttons[correct].style.background = '#d1fae5';
                fb.style.color = '#dc2626';
                fb.innerHTML = `❌ 答錯囉！正確答案是選項 ${correct + 1}`;
            }

            setTimeout(() => {
                this.currentIndex++;
                this.loadGameQuestion();
            }, 1800);
        }

        loadMatchingGame() {
            const container = document.getElementById('game-content');
            let words = [...this.currentLesson.words].slice(0, 4); // 取 4 組進行配對
            let cards = [];
            words.forEach((item, idx) => {
                cards.push({ text: item.word, type: 'en', id: idx });
                cards.push({ text: item.translation, type: 'zh', id: idx });
            });
            cards.sort(() => Math.random() - 0.5);

            let gridHtml = '';
            cards.forEach((card, idx) => {
                gridHtml += `<div class="match-card" id="card-${idx}" onclick="app.selectMatchCard('${card.text}', ${card.id}, 'card-${idx}')">${card.text}</div>`;
            });

            container.innerHTML = `
                <h3>🧩 模式三：單字配對卡牌遊戲</h3>
                <p>請點擊配對相應的英文單字與中文意思！</p>
                <div class="matching-grid">${gridHtml}</div>
                <div class="feedback" id="feedback"></div>
            `;
            this.selectedMatch = null;
            this.matchedPairs = 0;
            this.totalPairs = words.length;
        }

        selectMatchCard(text, id, elementId) {
            const el = document.getElementById(elementId);
            if (el.classList.contains('matched') || el.classList.contains('selected')) return;

            if (!this.selectedMatch) {
                this.selectedMatch = { text, id, elementId };
                el.classList.add('selected');
            } else {
                const firstEl = document.getElementById(this.selectedMatch.elementId);
                if (this.selectedMatch.id === id && this.selectedMatch.elementId !== elementId) {
                    // 配對成功
                    firstEl.classList.remove('selected');
                    firstEl.classList.add('matched');
                    el.classList.add('matched');
                    this.selectedMatch = null;
                    this.matchedPairs++;
                    this.addCoins(1);
                    document.getElementById('feedback').style.color = '#059669';
                    document.getElementById('feedback').innerText = '🎉 配對成功！ (+1 金幣 🪙)';

                    if (this.matchedPairs === this.totalPairs) {
                        setTimeout(() => {
                            document.getElementById('game-content').innerHTML = `<h3>🏆 太神啦！您順利完成了本單元配對遊戲！</h3><button class="btn" onclick="app.showModeMenu()">返回模式選單</button>`;
                        }, 1500);
                    }
                } else {
                    // 配對失敗
                    firstEl.classList.add('selected');
                    el.classList.add('selected');
                    setTimeout(() => {
                        firstEl.classList.remove('selected');
                        el.classList.remove('selected');
                        document.getElementById('feedback').innerText = '❌ 配對錯誤，再試一次！';
                    }, 600);
                    this.selectedMatch = null;
                }
            }
        }
    }

    const app = new App();
</script>

</body>
</html>
