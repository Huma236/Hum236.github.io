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
            0% { opacity: 0; transform: translateY(100px) scale(0.95); }
            100% { opacity: 1; transform: translateY(0) scale(1); }
        }

        .terminal-window {
            width: 900px; 
            max-width: 95%;
            height: 600px; 
            background-color: rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
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

        
        .header-actions{
            margin-left: auto;
            display: flex;
            align-items: center;
        }
        .skip-btn{
            background: rgba(0,0,0,0.35);
            border: 1px solid #333;
            color: #f8f8f2;
            font-family: inherit;
            padding: 6px 10px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 13px;
        }
        .skip-btn:hover{
            border-color: #00ff41;
            box-shadow: 0 0 12px rgba(0, 255, 65, 0.12);
        }

        
        .terminal-footer{
            padding: 10px 12px;
            border-top: 1px solid #333;
            background: rgba(0,0,0,0.25);
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            align-items: center;
        }
        .footer-label{
            color: #f8f8f2;
            opacity: 0.85;
            font-size: 13px;
            margin-right: 8px;
        }
        .sample-btn{
            background: rgba(0,0,0,0.35);
            border: 1px solid #333;
            color: #bd93f9;
            font-family: inherit;
            padding: 8px 10px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 13px;
        }
        .sample-btn:hover{
            border-color: #00ff41;
            box-shadow: 0 0 12px rgba(0, 255, 65, 0.12);
        }

        
        .pdf-modal{
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.75);
            display: none;
            align-items: center;
            justify-content: center;
            padding: 18px;
            z-index: 9999;
        }
        .pdf-modal.show{ display: flex; }
        .pdf-modal-content{
            width: min(1100px, 98vw);
            height: min(720px, 92vh);
            background: rgba(0,0,0,0.35);
            backdrop-filter: blur(10px);
            border: 1px solid #333;
            border-radius: 10px;
            box-shadow: 0 0 30px rgba(0, 255, 65, 0.15);
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }
        .pdf-modal-header{
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 12px;
            padding: 10px 12px;
            border-bottom: 1px solid #333;
            background: rgba(0,0,0,0.35);
        }
        .pdf-modal-title{
            color: #00ff41;
            font-weight: bold;
        }
        .pdf-modal-actions{
            display: flex;
            gap: 10px;
            align-items: center;
        }
        .pdf-link{
            color: #bd93f9;
            text-decoration: none;
            border: 1px solid #333;
            padding: 7px 10px;
            border-radius: 6px;
            background: rgba(0,0,0,0.25);
        }
        .pdf-link:hover{ border-color: #00ff41; }
        .pdf-close{
            background: rgba(0,0,0,0.25);
            border: 1px solid #333;
            color: #f8f8f2;
            font-family: inherit;
            padding: 7px 10px;
            border-radius: 6px;
            cursor: pointer;
        }
        .pdf-close:hover{ border-color: #ff5f56; }
        .pdf-frame{
            flex: 1;
            width: 100%;
            border: 0;
            background: #111;
        }
    </style>
</head>
<body>

    <div class="terminal-window">
        <div class="terminal-header">
           <div class="dot red"></div>
           <div class="dot yellow"></div>
           <div class="dot green"></div>

           <div class="header-actions">
              <button id="skipBtn" class="skip-btn" type="button">SKIP</button>
           </div>
        </div>

        
        <div class="terminal-body" id="terminal-content"></div>

        
        <div class="terminal-footer">
            <span class="footer-label">workflow samples:</span>

            <button class="sample-btn" data-title="case-note" data-pdf="./assets/moderation/case-note.pdf">case-note</button>
            <button class="sample-btn" data-title="case-note-simulated-1" data-pdf="./assets/moderation/case-note-simulated-1.pdf">case-note-simulated-1</button>
            <button class="sample-btn" data-title="case-note-simulated-2" data-pdf="./assets/moderation/case-note-simulated-2.pdf">case-note-simulated-2</button>

            <button class="sample-btn" data-title="appeal" data-pdf="./assets/moderation/appeal.pdf">appeal</button>
            <button class="sample-btn" data-title="appeal-1" data-pdf="./assets/moderation/appeal-1.pdf">appeal-1</button>
            <button class="sample-btn" data-title="appeal-2" data-pdf="./assets/moderation/appeal-2.pdf">appeal-2</button>
        </div>
    </div>

    
    <div class="pdf-modal" id="pdfModal" aria-hidden="true">
        <div class="pdf-modal-content">
            <div class="pdf-modal-header">
                <div class="pdf-modal-title" id="pdfTitle">Document</div>

                <div class="pdf-modal-actions">
                    <a class="pdf-link" id="pdfOpenNew" href="#" target="_blank" rel="noopener">Open in new tab</a>
                    <button class="pdf-close" id="pdfClose" type="button">Close</button>
                </div>
            </div>

            <iframe class="pdf-frame" id="pdfFrame" loading="lazy"></iframe>
        </div>
    </div>

    <script>
        const commands = [
            { type: 'input', text: 'whoami' },
            { type: 'output', text: '> Hello, I am Humam. 19 years old.' },
            { type: 'output', text: '> Electronic & AI Engineering Student (First Year Undergraduate).' },
            { type: 'output', text: '> Highly disciplined schedule: Balancing Studies, Work, and Gaming.' },
            
            { type: 'input', text: 'cat experience_log.txt' },
            { type: 'output', text: '> Moderator Staff @ Discord London Community.' },
            { type: 'output', text: '> Managed a hybrid Social & Gaming Community of ~23,000 users (Jun 2020 - Sep 2022).' },
            { type: 'output', text: '> Status: Project Concluded / Server Closed.' },
            { type: 'output', text: '> Handled 450+ tickets.' },

            { type: 'input', text: 'echo "Am I in Heaven?"' },
            { type: 'output', text: 'NO, But you might be hired soon! ;)' },

            { type: 'input', text: './run_Why_me.exe' },
            { type: 'output', text: '> My goal in moderation is simple: keep the community safe, fair, and enjoyable.' },
            { type: 'output', text: '> I review reports with context and evidence (logs, screenshots/video) before taking action.' },
            { type: 'output', text: '> I document decisions clearly so enforcement stays consistent and appeals can be reviewed.' },
            { type: 'output', text: '> I de-escalate first when possible, and escalate edge cases to the right level when needed.' },
            { type: 'output', text: '> The Discord community I moderated is now closed, so I can’t share internal logs.' },
            { type: 'output', text: '> Instead, I created anonymized, simulated workflow samples below to demonstrate my process.' },
            { type: 'output', text: '> Workflow samples are simulated/anonymized to demonstrate my moderation process.'},
        ];

        const terminalContent = document.getElementById('terminal-content');
        let cmdIndex = 0;
        let charIndex = 0;

        
        let isSkipping = false;

        function typeLine() {
            if (isSkipping) return;
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

        /* ADD: render instantly for SKIP */
        function renderAllInstantly() {
            terminalContent.innerHTML = '';

            commands.forEach(line => {
                const div = document.createElement('div');

                if (line.type === 'input') {
                    const prompt = document.createElement('span');
                    prompt.className = 'prompt';
                    prompt.textContent = 'root@engineer:~$';

                    const cmd = document.createElement('span');
                    cmd.className = 'command';
                    cmd.textContent = ' ' + line.text;

                    div.appendChild(prompt);
                    div.appendChild(cmd);
                } else {
                    const out = document.createElement('span');
                    out.className = 'output';
                    out.textContent = line.text;
                    div.appendChild(out);
                }

                terminalContent.appendChild(div);
            });

            cmdIndex = commands.length;
            charIndex = 0;
            terminalContent.scrollTop = terminalContent.scrollHeight;
        }

        window.onload = function() {
            setTimeout(typeLine, 1200); 
        };

        /* ADD: SKIP button handler */
        document.getElementById('skipBtn').addEventListener('click', () => {
            isSkipping = true;
            renderAllInstantly();
        });

        /* ADD: PDF Modal Viewer */
        const pdfModal = document.getElementById('pdfModal');
        const pdfFrame = document.getElementById('pdfFrame');
        const pdfTitle = document.getElementById('pdfTitle');
        const pdfOpenNew = document.getElementById('pdfOpenNew');
        const pdfClose = document.getElementById('pdfClose');

        function openPDF(title, src){
            pdfTitle.textContent = title;
            pdfFrame.src = src;
            pdfOpenNew.href = src;
            pdfModal.classList.add('show');
            pdfModal.setAttribute('aria-hidden', 'false');
        }

        function closePDF(){
            pdfModal.classList.remove('show');
            pdfModal.setAttribute('aria-hidden', 'true');
            pdfFrame.src = 'about:blank';
        }

        document.querySelectorAll('.sample-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                openPDF(btn.dataset.title, btn.dataset.pdf);
            });
        });

        pdfClose.addEventListener('click', closePDF);

        pdfModal.addEventListener('click', (e) => {
            if (e.target === pdfModal) closePDF();
        });

        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && pdfModal.classList.contains('show')) closePDF();
        });
    </script>
</body>
</html>
