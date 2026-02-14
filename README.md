<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Engineer | Terminal Access</title>
    <style>
        /* إعدادات الصفحة الأساسية */
        body {
            background-color: #0d0d0d;
            color: #00ff41; 
            font-family: 'Courier New', Courier, monospace;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }

        /* تعريف حركة الصعود السينمائي */
        @keyframes cinematicUp {
            0% {
                opacity: 0;
                transform: translateY(100px) scale(0.95); /* يبدأ من تحت وبحجم أصغر قليلاً */
            }
            100% {
                opacity: 1;
                transform: translateY(0) scale(1); /* يستقر في مكانه وحجمه الطبيعي */
            }
        }

        /* نافذة التيرمينال مع تطبيق الحركة */
        .terminal-window {
            width: 800px;
            max-width: 90%;
            height: 500px;
            background-color: #000;
            border: 1px solid #333;
            border-radius: 8px;
            box-shadow: 0 0 30px rgba(0, 255, 65, 0.15); /* زدنا التوهج قليلاً */
            display: flex;
            flex-direction: column;
            overflow: hidden;
            
            /* تطبيق الأنيميشن */
            opacity: 0; /* مخفي بالبداية */
            animation: cinematicUp 1.2s cubic-bezier(0.22, 1, 0.36, 1) forwards; /* حركة انسيابية جداً */
        }

        /* باقي الستايل كما هو */
        .terminal-header {
            background-color: #1a1a1a;
            padding: 10px;
            display: flex;
            gap: 8px;
            border-bottom: 1px solid #333;
        }

        .dot { width: 12px; height: 12px; border-radius: 50%; }
        .red { background-color: #ff5f56; }
        .yellow { background-color: #ffbd2e; }
        .green { background-color: #27c93f; }

        .terminal-body {
            padding: 20px;
            flex-grow: 1;
            overflow-y: auto;
            font-size: 16px;
            line-height: 1.5;
        }

        .prompt { color: #bd93f9; font-weight: bold; }
        .command { color: #f8f8f2; }
        .output { color: #00ff41; margin-bottom: 15px; display: block; }
        .cursor {
            display: inline-block;
            width: 10px;
            height: 18px;
            background-color: #00ff41;
            animation: blink 1s infinite;
            vertical-align: middle;
            margin-left: 5px;
        }

        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 4px; }
    </style>
</head>
<body>

    <div class="terminal-window">
        <div class="terminal-header">
            <div class="dot red"></div>
            <div class="dot yellow"></div>
            <div class="dot green"></div>
        </div>
        <div class="terminal-body" id="terminal-content">
            </div>
    </div>

    <script>
        // هنا البيانات الحقيقية - عدل اسمك وخبراتك هنا
        const commands = [
            { type: 'input', text: 'whoami' },
            { type: 'output', text: '> Hey, My name is Humam i have 19 years.' },
            { type: 'output', text: '> My study is: Electronic & AI Engineering, 1st grade.'},
            
            { type: 'input', text: 'cat experience_log.txt' },
            { type: 'output', text: '> Senior Support Staff @ Discord London Community (a general chatting & gaming community with +~23000 user) June-2020 - September-2023 / Server Closed' },
            { type: 'output', text: '> Managed 450+ tickets with ~95% satisfaction rate.' },
            { type: 'output', text: '> Managed to build a good image on how the user think and what his needs' },
            
            { type: 'input', text: './run_skills.exe' },
            { type: 'output', text: '[LOADING] Analyzing skillset...' },
            { type: 'output', text: '✔ Network Analysis (WinMTR, Packet Loss Debugging)' },
            { type: 'output', text: '✔ Hypixel Watchdog Logic & Anticheat Mechanics Understanding' },
            { type: 'output', text: '✔ English Fluency (C1 Level)' },
            { type: 'output', text: '✔ Great Image on billing-related issues from Stripe/Tebex etc...' },

            { type: 'input', text: 'echo "Am I in Heaven?"' },
            { type: 'output', text: 'NO, But Might be Soon :D' },

            { type: 'input', text: 'What's 1+1?'},
            { type: 'output', text: 'Depends on the weather in your country and what are you doing right now it could be 2! good info isn't? :)' },
        ];

        const terminalContent = document.getElementById('terminal-content');
        let cmdIndex = 0;
        let charIndex = 0;

        function typeLine() {
            if (cmdIndex >= commands.length) return;

            const line = commands[cmdIndex];
            
            // إنشاء سطر جديد
            if (charIndex === 0) {
                const div = document.createElement('div');
                if (line.type === 'input') {
                    div.innerHTML = `<span class="prompt">root@engineer:~$</span> <span class="command"></span><span class="cursor"></span>`;
                } else {
                    div.innerHTML = `<span class="output"></span>`;
                }
                terminalContent.appendChild(div);
                terminalContent.scrollTop = terminalContent.scrollHeight;
            }

            // الكتابة
            const currentDiv = terminalContent.lastElementChild;
            const textSpan = line.type === 'input' ? currentDiv.querySelector('.command') : currentDiv.querySelector('.output');
            
            // إدارة المؤشر
            const allCursors = document.querySelectorAll('.cursor');
            allCursors.forEach(c => c.style.display = 'none');
            
            if (line.type === 'input') {
                const cursor = document.createElement('span');
                cursor.className = 'cursor';
                currentDiv.appendChild(cursor);
            }

            textSpan.textContent += line.text.charAt(charIndex);
            charIndex++;

            if (charIndex < line.text.length) {
                setTimeout(typeLine, 40); // سرعة الكتابة
            } else {
                cmdIndex++;
                charIndex = 0;
                setTimeout(typeLine, line.type === 'input' ? 400 : 150); // تأخير بين الأسطر
            }
        }

        // التعديل الجوهري: تأخير البدء حتى انتهاء حركة الصعود
        window.onload = function() {
            setTimeout(typeLine, 1500); // ينتظر 1.5 ثانية (حتى تصعد النافذة) ثم يبدأ الكتابة
        };
    </script>
</body>
</html>
