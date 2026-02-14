<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Engineer | Terminal Access</title>
    <style>
        /* إعدادات الصفحة الأساسية - الظلام الدامس */
        body {
            background-color: #0d0d0d;
            color: #00ff41; /* اللون الأخضر الهكر */
            font-family: 'Courier New', Courier, monospace; /* خط الآلة الكاتبة */
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }

        /* نافذة التيرمينال */
        .terminal-window {
            width: 800px;
            max-width: 90%;
            height: 500px;
            background-color: #000;
            border: 1px solid #333;
            border-radius: 8px;
            box-shadow: 0 0 30px rgba(0, 255, 65, 0.1); /* توهج خفيف */
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        /* شريط العنوان العلوي */
        .terminal-header {
            background-color: #1a1a1a;
            padding: 10px;
            display: flex;
            gap: 8px;
            border-bottom: 1px solid #333;
        }

        .dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }
        .red { background-color: #ff5f56; }
        .yellow { background-color: #ffbd2e; }
        .green { background-color: #27c93f; }

        /* منطقة النص */
        .terminal-body {
            padding: 20px;
            flex-grow: 1;
            overflow-y: auto;
            font-size: 16px;
            line-height: 1.5;
        }

        /* ستايل النصوص المختلفة */
        .prompt { color: #bd93f9; font-weight: bold; } /* لون اسم المستخدم */
        .command { color: #f8f8f2; } /* لون الأمر */
        .output { color: #00ff41; margin-bottom: 15px; } /* لون النتيجة */
        .highlight { color: #f1fa8c; font-weight: bold; } /* تمييز الكلمات المهمة */

        /* المؤشر الوامض */
        .cursor {
            display: inline-block;
            width: 10px;
            height: 18px;
            background-color: #00ff41;
            animation: blink 1s infinite;
            vertical-align: middle;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }

        /* إخفاء شريط التمرير للجمالية */
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
        // هنا البيانات الخاصة بك - عدلها كما تشاء
        const commands = [
            { type: 'input', text: 'whoami' },
            { type: 'output', text: '> AI Engineering Student & Support Specialist.' },
            
            { type: 'input', text: 'cat experience.txt' },
            { type: 'output', text: '> 2.5 Years as Senior Support in London Community Servers.' },
            { type: 'output', text: '> Expert in Conflict Resolution & Technical Troubleshooting.' },
            
            { type: 'input', text: './skills.sh --list' },
            { type: 'output', text: '[✔] Network Diagnostics (WinMTR, Logs Analysis)' },
            { type: 'output', text: '[✔] Hypixel Anti-Cheat Logic Understanding' },
            { type: 'output', text: '[✔] English Fluency & Professional Communication' },

            { type: 'input', text: 'echo "Ready to work?"' },
            { type: 'output', text: 'YES. Standing by for deployment...' }
        ];

        const terminalContent = document.getElementById('terminal-content');
        let cmdIndex = 0;
        let charIndex = 0;
        let isTyping = false;

        function typeLine() {
            if (cmdIndex >= commands.length) return; // انتهينا

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
                
                // التمرير للأسفل تلقائياً
                terminalContent.scrollTop = terminalContent.scrollHeight;
            }

            // الكتابة حرفاً بحرف
            const currentDiv = terminalContent.lastElementChild;
            const textSpan = line.type === 'input' ? currentDiv.querySelector('.command') : currentDiv.querySelector('.output');
            
            // إزالة المؤشر من الأسطر السابقة
            const allCursors = document.querySelectorAll('.cursor');
            allCursors.forEach(c => c.style.display = 'none');
            
            // إضافة المؤشر للسطر الحالي فقط (إذا كان أمراً)
            if (line.type === 'input') {
                const cursor = document.createElement('span');
                cursor.className = 'cursor';
                currentDiv.appendChild(cursor);
            }

            textSpan.textContent += line.text.charAt(charIndex);
            charIndex++;

            if (charIndex < line.text.length) {
                // سرعة الكتابة (عدل الرقم 50 لجعله أسرع أو أبطأ)
                setTimeout(typeLine, 50);
            } else {
                // الانتقال للسطر التالي بعد توقف بسيط
                cmdIndex++;
                charIndex = 0;
                setTimeout(typeLine, line.type === 'input' ? 300 : 100); // الأوامر تتأخر قليلاً لمحاكاة المعالجة
            }
        }

        // بدء التشغيل عند تحميل الصفحة
        window.onload = typeLine;
    </script>
</body>
</html>
