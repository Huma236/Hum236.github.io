
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Humam | Engineer Portfolio</title>
    <style>
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
            background: 
                linear-gradient(rgba(0, 0, 0, 0.9), rgba(0, 0, 0, 0)),
                url('https://imgs.search.brave.com/7nToAkaPPhZfa8bxRu26_pAbi-R8rSlg3Xo9pVgqaHc/rs:fit:500:0:1:0/g:ce/aHR0cHM6Ly9wcmV2/aWV3LnJlZGQuaXQv/ZWh2Z29xZjJncmQ2/MS5wbmc_d2lkdGg9/MTkyMCZmb3JtYXQ9/cG5nJmF1dG89d2Vi/cCZzPWQ2Y2IxN2Y3/NzNhOGMwNTg5NTcz/NDlmZWU1OTJlOTA2/NDM3MTc2YmE'); 
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }

        @keyframes cinematicUp {
            0% {
                opacity: 0;
                transform: translateY(100px) scale(0.95);
            }
            100% {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }

        .terminal-window {
            width: 900px; 
            max-width: 95%;
            height: 600px; 
            background-color: rgba(0, 0, 0, 0.6);
            border: 1px solid #333;
            border-radius: 8px;
            box-shadow: 0 0 30px rgba(0, 255, 65, 0.15);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            opacity: 0;
            animation: cinematicUp 1.2s cubic-bezier(0.22, 1, 0.36, 1) forwards;
        }

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
            line-height: 1.6; 
        }

        .prompt { color: #bd93f9; font-weight: bold; }
        .command { color: #f8f8f2; }
        .output { color: #00ff41; margin-bottom: 15px; display: block; text-shadow: 0 0 5px rgba(0, 255, 65, 0.3); }
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
        const commands = [
            { type: 'input', text: 'whoami' },
            { type: 'output', text: '> Hello, I am Humam. 19 years old.' },
            { type: 'output', text: '> Electronic & AI Engineering Student (First Year Undergraduate).' },
            { type: 'output', text: '> Highly disciplined schedule: Balancing Studies, Work, and Gaming.' },
            
            { type: 'input', text: 'cat experience_log.txt' },
            { type: 'output', text: '> Senior Support Staff @ Discord London Community.' },
            { type: 'output', text: '> Managed a hybrid Social & Gaming Community of ~23,000 users (Jun 2020 - Sep 2023).' },
            { type: 'output', text: '> Status: Project Concluded / Server Closed.' },
            { type: 'output', text: '> Handled 450+ tickets with a 95% satisfaction rate.' },
            { type: 'output', text: '> Developed deep understanding of user psychology and needs analysis.' },
            
            { type: 'input', text: './run_skills.exe' },
            { type: 'output', text: '[LOADING] Analyzing skillset...' },
            { type: 'output', text: '✔ Network Analysis (WinMTR, Packet Loss Debugging)' },
            { type: 'output', text: '✔ Hypixel Watchdog Logic & Anticheat Mechanics' },
            { type: 'output', text: '✔ English Fluency (C1 Level)' },
            { type: 'output', text: '✔ Payment & Billing Troubleshooting (Stripe/Tebex)' },

            { type: 'input', text: 'echo "Am I in Heaven?"' },
            { type: 'output', text: 'NO, But you might be hired soon! ;)' },

            { type: 'input', text: './run_Why_me.exe' },
            { type: 'output', text: '> Because I offer the rare blend of a Gamer\'s passion and an Engineer\'s logic.' },
            { type: 'output', text: '> Over the past 2 years, I dedicated thousands of hours to deep-dive debugging.' },
            { type: 'output', text: '> Specialized in dissecting Minecraft Client-side vs Server-side anomalies.' },
            { type: 'output', text: '> As an AI Engineering Student, I treat support tickets as logical system errors.' },
            { type: 'output', text: '> I aim to elevate my technical expertise by working alongside industry leaders at Hypixel Inc.' },
            
            { type: 'input', text: 'status' },
            { type: 'output', text: 'READY FOR DEPLOYMENT.' },
        ];

        const terminalContent = document.getElementById('terminal-content');
        let cmdIndex = 0;
        let charIndex = 0;

        function typeLine() {
            if (cmdIndex >= commands.length) return;

            const line = commands[cmdIndex];
            
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

            const currentDiv = terminalContent.lastElementChild;
            const textSpan = line.type === 'input' ? currentDiv.querySelector('.command') : currentDiv.querySelector('.output');
            
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
                setTimeout(typeLine, 35); 
            } else {
                cmdIndex++;
                charIndex = 0;
                setTimeout(typeLine, line.type === 'input' ? 500 : 150); 
            }
        }

        window.onload = function() {
            setTimeout(typeLine, 1200); 
        };
    </script>
</body>
</html>
