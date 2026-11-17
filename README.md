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
            max-width: 850px;
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

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 12px;
            margin-bottom: 20px;
            max-height: 400px;
            overflow-y: auto;
            padding-right: 5px;
        }

        .btn {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 12px 15px;
            border-radius: 12px;
            font-size: 0.95rem;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 3px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(236, 72, 153, 0.3);
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

        .wrong-summary-box {
            background: #fef2f2;
            border: 2px dashed #f87171;
            border-radius: 12px;
            padding: 15px;
            margin-top: 15px;
            text-align: left;
        }

        .screenshot-alert {
            background: #fef3c7;
            color: #b45309;
            padding: 10px;
            border-radius: 8px;
            font-weight: bold;
            margin-top: 15px;
            border: 1px solid #fcd34d;
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

    <!-- 主選單：16 課課程 -->
    <div id="lesson-menu">
        <h3>📚 請選擇學習單元 (共 16 課)：</h3>
        <div class="menu-grid" id="lesson-list"></div>
    </div>

    <!-- 單元內模式選單 -->
    <div id="mode-menu" class="hidden">
        <button class="back-btn" onclick="app.showLessonMenu()">⬅ 返回課程選單</button>
        <h2 id="current-lesson-title" style="color: var(--secondary);">單元名稱</h2>
        <p>請選擇挑戰模式：</p>
        <div class="menu-grid" style="grid-template-columns: repeat(3, 1fr);">
            <button class="btn" onclick="app.startMode(1)">
                🔊 <span>模式一：聽字填單字</span>
            </button>
            <button class="btn" onclick="app.startMode(2)">
                📝 <span>模式二：文法選擇題</span>
            </button>
            <button class="btn" onclick="app.startMode(3)">
                🧩 <span>模式三：卡牌配對</span>
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
    // 完整的 16 課課程資料庫
    const curriculumData = [
        { id: 1, title: "第 1 課：動詞與變化 (Carve ~ Delete)", words: [
            { word: "carve", translation: "雕刻", hint: "V. 雕刻" },
            { word: "knock", translation: "敲、打", hint: "V. 敲門" },
            { word: "drill", translation: "鑽孔、訓練", hint: "V. 練習、演習" },
            { word: "delete", translation: "刪去", hint: "V. 刪除檔案" }
        ], grammarQuestions: [
            { q: "He ________ his name on the wooden board yesterday.", options: ["carve", "carved", "carving", "carves"], answer: 1, hint: "發生在昨天，用過去式" },
            { q: "The worker ________ for oil in the mountains last month.", options: ["drill", "drilled", "drilling", "drills"], answer: 1, hint: "過去式變化" }
        ]},
        { id: 2, title: "第 2 課：復原與修繕 (Recover ~ A little)", words: [
            { word: "recover", translation: "復原、恢復", hint: "V. 康復" },
            { word: "repair", translation: "修復", hint: "V. 修理" },
            { word: "pair", translation: "一雙、對", hint: "N. 成雙成對" },
            { word: "little", translation: "少許、一些", hint: "Adj. 修飾不可數名詞" }
        ], grammarQuestions: [
            { q: "She has already ________ from a bad cold.", options: ["recover", "recovering", "recovered", "recovers"], answer: 2, hint: "現在完成時態：has + p.p." },
            { q: "I need a ________ bit of sugar for making the pie.", options: ["little", "few", "many", "these"], answer: 0, hint: "a little bit + 不可數名詞" }
        ]},
        { id: 3, title: "第 3 課：環境與日常 (Pond ~ Above all)", words: [
            { word: "pond", translation: "池塘", hint: "N. 魚池" },
            { word: "pour", translation: "傾注、倒", hint: "V. 倒水" },
            { word: "thicken", translation: "使變濃、變厚", hint: "V. 濃縮湯汁" },
            { word: "nap", translation: "打盹、午睡", hint: "N. 小睡" }
        ], grammarQuestions: [
            { q: "Five cattle ________ drinking at the pond now.", options: ["is", "are", "was", "were"], answer: 1, hint: "cattle 為複數集合名詞，現在進行式用 are" },
            { q: "Students usually take a ________ after lunch.", options: ["nap", "bath", "sigh", "pond"], answer: 0, hint: "take a nap 小睡片刻" }
        ]},
        { id: 4, title: "第 4 課：情緒與感官 (Bathe ~ As soon as)", words: [
            { word: "bathe", translation: "游泳、洗澡", hint: "V. 浸泡" },
            { word: "sigh", translation: "嘆息", hint: "V. / N. 嘆氣" },
            { word: "allow", translation: "允許", hint: "V. 准許" },
            { word: "happen", translation: "發生", hint: "V. 偶然發生" }
        ], grammarQuestions: [
            { q: "It started to rain as soon as she ________ shopping.", options: ["finish", "finishes", "finished", "finishing"], answer: 2, hint: "as soon as引導的時間副詞子句，時態需一致用過去式" },
            { q: "An accident happened ________ Jack yesterday.", options: ["to", "at", "with", "for"], answer: 0, hint: "固定句型：事 + happened to + 人" }
        ]},
        { id: 5, title: "第 5 課：心理與驚奇 (Amaze ~ Tiring)", words: [
            { word: "amaze", translation: "使驚訝", hint: "V. 令人驚奇" },
            { word: "bore", translation: "使無聊", hint: "V. 令人乏味" },
            { word: "excite", translation: "使興奮", hint: "V. 激動" },
            { word: "surprise", translation: "使驚奇", hint: "V. / N. 驚喜" }
        ], grammarQuestions: [
            { q: "His speech ________ me a lot last night.", options: ["bore", "bored", "boring", "bores"], answer: 1, hint: "過去式動詞" },
            { q: "We were ________ to see the old sailor in town.", options: ["amaze", "amazing", "amazed", "amazes"], answer: 2, hint: "主詞為人時，情緒形容詞用 -ed" }
        ]},
        { id: 6, title: "第 6 課：情感表達 (Anger ~ Fight)", words: [
            { word: "anger", translation: "憤怒", hint: "N. 生氣" },
            { word: "argue", translation: "爭吵", hint: "V. 爭辯" },
            { word: "worry", translation: "擔心", hint: "V. 煩惱" },
            { word: "proud", translation: "自豪的", hint: "Adj. 驕傲的" }
        ], grammarQuestions: [
            { q: "They always argue ________ money.", options: ["on", "at", "about", "with"], answer: 2, hint: "argue about sth 針對某事爭吵" },
            { q: "Dad is very proud ________ me.", options: ["of", "at", "in", "with"], answer: 0, hint: "be proud of 感到自豪" }
        ]},
        { id: 7, title: "第 7 課：字尾變化與形容詞 (-able)", words: [
            { word: "thinkable", translation: "可想像的", hint: "Adj. 能想到的" },
            { word: "changeable", translation: "易變的", hint: "Adj. 會改變的" },
            { word: "comfortable", translation: "舒適的", hint: "Adj. 舒服的" },
            { word: "portable", translation: "手提式的", hint: "Adj. 可攜帶的" }
        ], grammarQuestions: [
            { q: "This sofa is extremely ________ to sit on.", options: ["comfort", "comfortable", "comfortably", "comforting"], answer: 1, hint: "be動詞後方接形容詞 comfortable" },
            { q: "We need a ________ computer that we can take anywhere.", options: ["port", "portable", "ported", "porting"], answer: 1, hint: "修飾名詞用形容詞 portable" }
        ]},
        { id: 8, title: "第 8 課：購物與金錢 (Cost ~ Extra)", words: [
            { word: "cost", translation: "花費、價值", hint: "V. / N. 價錢" },
            { word: "bargain", translation: "討價還價", hint: "V. 講價" },
            { word: "cart", translation: "手推車", hint: "N. 購物車" },
            { word: "million", translation: "百萬", hint: "N. 1,000,000" }
        ], grammarQuestions: [
            { q: "How much ________ this jacket cost?", options: ["do", "does", "did", "is"], answer: 1, hint: "jacket 為第三人稱單數，現在式疑問句助動詞用 does" },
            { q: "The man won five ________ dollars in the lottery.", options: ["million", "millions", "million of", "millions of"], answer: 0, hint: "數字 + million + 複數名詞 (million不加s)" }
        ]},
        { id: 9, title: "第 9 課：交通與旅遊 (Traffic ~ Avoid)", words: [
            { word: "traffic", translation: "交通", hint: "N. 車流量" },
            { word: "flight", translation: "航班", hint: "N. 飛行" },
            { word: "arrive", translation: "抵達", hint: "V. 到達" },
            { word: "cancel", translation: "取消", hint: "V. 放棄行程" }
        ], grammarQuestions: [
            { q: "The traffic in Taipei ________ terrible during rush hour.", options: ["is", "are", "be", "were"], answer: 0, hint: "traffic 為不可數名詞，視為單數" },
            { q: "We arrived ________ the station at 7 o'clock.", options: ["in", "at", "to", "on"], answer: 1, hint: "小地方用 arrive at" }
        ]},
        { id: 10, title: "第 10 課：人際與狀態 (Single ~ Marry)", words: [
            { word: "single", translation: "單身的", hint: "Adj. 未婚的" },
            { word: "marry", translation: "結婚", hint: "V. 嫁、娶" },
            { word: "married", translation: "已婚的", hint: "Adj. 有配偶的" },
            { word: "album", translation: "相簿", hint: "N. 專輯" }
        ], grammarQuestions: [
            { q: "He is going to ________ Linda next month.", options: ["marry with", "marry to", "marry", "getting marry"], answer: 2, hint: "marry 為及物動詞，後面直接接受詞" },
            { q: "Are you ________? - Yes, I have a wife.", options: ["marry", "marrying", "married", "marriage"], answer: 2, hint: "詢問婚姻狀態用形容詞 married" }
        ]},
        { id: 11, title: "第 11 課：數量與容器 (Package ~ Amount)", words: [
            { word: "package", translation: "包裹", hint: "N. 箱子" },
            { word: "loaf", translation: "一條(麵包)", hint: "N. 塊" },
            { word: "bunch", translation: "一串、束", hint: "N. 香蕉或花" },
            { word: "amount", translation: "總量", hint: "N. 不可數名詞數量" }
        ], grammarQuestions: [
            { q: "He wanted a ________ of bread for breakfast.", options: ["loaf", "loafs", "loaves", "pieces"], answer: 0, hint: "a loaf of bread 一條麵包" },
            { q: "They gave me a large ________ of money.", options: ["number", "amount", "many", "few"], answer: 1, hint: "money 為不可數名詞，搭配 a large amount of" }
        ]},
        { id: 12, title: "第 12 課：心智與經驗 (Mind ~ Perhaps)", words: [
            { word: "mind", translation: "介意、心智", hint: "V. 心理" },
            { word: "experience", translation: "經驗", hint: "N. 經歷" },
            { word: "perhaps", translation: "也許", hint: "Adv. 或許" },
            { word: "possible", translation: "可能的", hint: "Adj. 會發生的" }
        ], grammarQuestions: [
            { q: "I don't mind ________ with him in the classroom.", options: ["sit", "to sit", "sitting", "sat"], answer: 2, hint: "mind 後方接動名詞 (V-ing)" },
            { q: "It's ________ for her to buy a big house now.", options: ["possible", "can", "may", "will"], answer: 0, hint: "句型：It's + adj. + for sb to do sth" }
        ]},
        { id: 13, title: "第 13 課：軍事與目標 (Aim ~ Goal)", words: [
            { word: "aim", translation: "瞄準、目標", hint: "V. 標的" },
            { word: "army", translation: "軍隊", hint: "N. 陸軍" },
            { word: "soldier", translation: "士兵", hint: "N. 軍人" },
            { word: "goal", translation: "目標", hint: "N. 目的" }
        ], grammarQuestions: [
            { q: "He aimed the gun ________ the target.", options: ["at", "to", "on", "in"], answer: 0, hint: "aim at 瞄準..." },
            { q: "His brother ________ a soldier ten years ago.", options: ["is", "was", "were", "be"], answer: 1, hint: "ten years ago 表示過去，用 was" }
        ]},
        { id: 14, title: "第 14 課：人群與部門 (Crowd ~ Department)", words: [
            { word: "crowd", translation: "人群", hint: "N. 聚集" },
            { word: "part", translation: "部分", hint: "N. 角色" },
            { word: "department", translation: "部門、系", hint: "N. 局" },
            { word: "drugstore", translation: "藥房", hint: "N. 藥局" }
        ], grammarQuestions: [
            { q: "I am a student from the English ________.", options: ["Department", "Crowd", "Part", "Cable"], answer: 0, hint: "系所用 department" },
            { q: "Is there a ________ around here to buy medicine?", options: ["drugstore", "cable", "program", "army"], answer: 0, hint: "買藥去 drugstore" }
        ]},
        { id: 15, title: "第 15 課：節目與科技 (Cable ~ Program)", words: [
            { word: "cable", translation: "電纜、有線電視", hint: "N. 頻道" },
            { word: "program", translation: "節目", hint: "N. 電視秀" },
            { word: "ready", translation: "準備好的", hint: "Adj. 備妥的" },
            { word: "active", translation: "活躍的", hint: "Adj. 積極的" }
        ], grammarQuestions: [
            { q: "I watch Ruby's ________ on TV every single evening.", options: ["program", "cable", "drugstore", "crowd"], answer: 0, hint: "電視節目用 program" },
            { q: "Paul is very active ________ sports at school.", options: ["in", "at", "on", "with"], answer: 0, hint: "be active in 活躍於..." }
        ]},
        { id: 16, title: "第 16 課：綜合片語與文法挑戰 (Review)", words: [
            { word: "afraid", translation: "害怕的", hint: "Adj. 恐懼的" },
            { word: "single", translation: "單身的", hint: "Adj. 獨特的" },
            { word: "except", translation: "除了...之外", hint: "Prep. 排除" },
            { word: "famous", translation: "有名的", hint: "Adj. 聞名的" }
        ], grammarQuestions: [
            { q: "Everyone knows her ________ me. (除了我以外都認識)", options: ["besides", "except", "beside", "with"], answer: 1, hint: "except 表示排除在外" },
            { q: "Yangmingshan is famous ________ its beautiful hot springs.", options: ["as", "for", "with", "to"], answer: 1, hint: "be famous for 以...聞名" }
        ]}
    ];

    class App {
        constructor() {
            this.coins = parseInt(localStorage.getItem('deb_coins')) || 0;
            this.currentLesson = null;
            this.currentMode = null;
            this.currentIndex = 0;
            this.wrongItems = []; // 紀錄錯題
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
                btn.innerHTML = `📖 <span>${lesson.title}</span>`;
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
            this.wrongItems = []; // 重置錯題
            document.getElementById('mode-menu').classList.add('hidden');
            document.getElementById('game-area').classList.remove('hidden');
            this.loadGameQuestion();
        }

        loadGameQuestion() {
            const container = document.getElementById('game-content');
            container.innerHTML = '';

            if (this.currentMode === 1) {
                if (this.currentIndex >= this.currentLesson.words.length) {
                    this.showSummary();
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
                            <button class="btn" onclick="app.checkWordAnswer('${item.word}', '${item.translation}')">提交答案</button>
                        </div>
                        <div class="feedback" id="feedback"></div>
                    </div>
                `;
            } else if (this.currentMode === 2) {
                if (this.currentIndex >= this.currentLesson.grammarQuestions.length) {
                    this.showSummary();
                    return;
                }
                const qData = this.currentLesson.grammarQuestions[this.currentIndex];
                let optionsHtml = '';
                qData.options.forEach((opt, idx) => {
                    optionsHtml += `<button class="option-btn" onclick="app.checkGrammarAnswer(${idx}, ${qData.answer}, '${qData.q}', '${qData.options[qData.answer]}')">${idx + 1}. ${opt}</button>`;
                });
                container.innerHTML = `
                    <h3>📝 模式二：文法選擇題 (${this.currentIndex + 1}/${this.currentLesson.grammarQuestions.length})</h3>
                    <div class="game-card" style="text-align: left;">
                        <p style="font-size: 1.1rem; font-weight: bold;">Q: ${qData.q}</p>
                        <div class="hint-box" style="width:100%; box-sizing:border-box;">💡 老師提示：${qData.hint}</div>
                        <div class="options-grid" style="margin-top: 15px;">${optionsHtml}</div>
                        <div class="feedback" id="feedback" style="text-align: center;"></div>
                    </div>
                `;
            } else if (this.currentMode === 3) {
                this.loadMatchingGame();
            }
        }

        speakWord(word) {
            const utterance = new SpeechSynthesisUtterance(word);
            utterance.lang = 'en-US';
            window.speechSynthesis.speak(utterance);
        }

        checkWordAnswer(correctWord, translation) {
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
                fb.innerHTML = `❌ 正確答案是：<strong>${correctWord}</strong>`;
                this.wrongItems.push(`單字：${translation} (${correctWord})`);
                setTimeout(() => {
                    this.currentIndex++;
                    this.loadGameQuestion();
                }, 1800);
            }
        }

        checkGrammarAnswer(selected, correct, questionText, correctText) {
            const fb = document.getElementById('feedback');
            const buttons = document.querySelectorAll('.option-btn');
            buttons.forEach(b => b.disabled = true);

            if (selected === correct) {
                buttons[selected].style.background = '#d1fae5';
                buttons[selected].style.borderColor = '#34d399';
                fb.style.color = '#059669';
                fb.innerHTML = '✨ 答對了！ (+1 金幣 🪙)';
                this.addCoins(1);
            } else {
                buttons[selected].style.background = '#fee2e2';
                buttons[selected].style.borderColor = '#f87171';
                buttons[correct].style.background = '#d1fae5';
                fb.style.color = '#dc2626';
                fb.innerHTML = `❌ 答錯囉！正確答案是：${correctText}`;
                this.wrongItems.push(`題目：${questionText} (正確解答：${correctText})`);
            }

            setTimeout(() => {
                this.currentIndex++;
                this.loadGameQuestion();
            }, 2000);
        }

        loadMatchingGame() {
            const container = document.getElementById('game-content');
            let words = [...this.currentLesson.words];
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
                            this.showSummary();
                        }, 1500);
                    }
                } else {
                    firstEl.classList.add('selected');
                    el.classList.add('selected');
                    let currentWordObj = this.currentLesson.words[id];
                    if(!this.wrongItems.includes(`配對失誤：${currentWordObj.word} (${currentWordObj.translation})`)) {
                        this.wrongItems.push(`配對失誤：${currentWordObj.word} (${currentWordObj.translation})`);
                    }
                    setTimeout(() => {
                        firstEl.classList.remove('selected');
                        el.classList.remove('selected');
                        document.getElementById('feedback').innerText = '❌ 配對錯誤！';
                    }, 600);
                    this.selectedMatch = null;
                }
            }
        }

        showSummary() {
            const container = document.getElementById('game-content');
            let wrongHtml = '';
            if (this.wrongItems.length === 0) {
                wrongHtml = `<p style="color: #059669; font-weight: bold;">🎉 太神啦！您本單元全部答對，沒有錯題！</p>`;
            } else {
                wrongHtml = `<ul style="margin: 5px 0; padding-left: 20px; color: #dc2626;">`;
                this.wrongItems.forEach(item => {
                    wrongHtml += `<li>${item}</li>`;
                });
                wrongHtml += `</ul>`;
            }

            container.innerHTML = `
                <h3>🏆 本單元挑戰結算與錯題統整</h3>
                <div class="wrong-summary-box">
                    <p style="font-weight: bold; margin-top: 0; color: #b91c1c;">📋 您的錯題統整清單：</p>
                    ${wrongHtml}
                </div>
                <div class="screenshot-alert">
                    ⚠️ 提醒：請將此畫面截圖回傳給 Debra 老師喔！
                </div>
                <br>
                <button class="btn" onclick="app.showModeMenu()" style="margin: 0 auto;">返回模式選單</button>
            `;
        }
    }

    const app = new App();
</script>

</body>
</html>
