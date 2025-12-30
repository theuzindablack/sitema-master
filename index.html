<!DOCTYPE html>
<html lang="pt-pt">
<head>
    <meta charset="UTF-8">
    <title>Q-OS OMNI-CONTROL | v53.0</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
    <style>
        :root { --neon: #00ffcc; --pink: #ff00ff; --dark: #050505; }
        body, html { margin: 0; padding: 0; background: var(--dark); color: var(--neon); font-family: 'Consolas', monospace; height: 100vh; overflow: hidden; display: flex; }

        #side-panel { width: 360px; background: #0a0a0a; border-right: 2px solid #1a1a1a; display: flex; flex-direction: column; padding: 15px; box-sizing: border-box; }
        #chat-window { flex: 1; overflow-y: auto; font-size: 0.82em; margin-bottom: 10px; border-bottom: 1px solid #222; }
        .ai-msg { color: var(--neon); margin-bottom: 10px; border-left: 2px solid var(--pink); padding-left: 8px; }

        #code-area { height: 150px; width: 100%; background: #000; color: #fff; border: 1px solid #333; font-family: monospace; font-size: 11px; padding: 10px; margin-bottom: 10px; outline: none; }

        .btn-group { display: grid; grid-template-columns: 1fr 1fr; gap: 5px; }
        .btn-main { border: none; padding: 8px; font-weight: bold; cursor: pointer; border-radius: 4px; text-transform: uppercase; font-size: 10px; }
        
        .btn-select { background: #00aaff; color: #fff; grid-column: span 2; margin-bottom: 5px; }
        .btn-master { background: linear-gradient(45deg, #ff0055, #6600ff); color: #fff; grid-column: span 2; margin-bottom: 10px; border: 2px solid #fff; }
        .btn-master.active { background: #f00 !important; animation: pulse 0.6s infinite; }
        @keyframes pulse { 0% { box-shadow: 0 0 5px #f00; } 50% { box-shadow: 0 0 20px #f00; } 100% { box-shadow: 0 0 5px #f00; } }

        .btn-files { background: #ffcc00; color: #000; grid-column: span 2; }
        .btn-add { background: #008844; color: #fff; }
        .btn-rem { background: #aa0000; color: #fff; }
        .btn-inj { background: var(--neon); color: #000; }
        .btn-all { background: #fff; color: #000; }
        
        #viewport { flex-grow: 1; display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; padding: 10px; overflow-y: auto; background: #000; }
        .slot { background: #111; border: 2px solid #1a1a1a; height: 320px; display: flex; flex-direction: column; }
        .slot iframe { flex-grow: 1; border: none; background: #fff; }
        .slot-header { background: #1a1a1a; padding: 6px; display: flex; justify-content: space-between; font-size: 10px; }
        .is-master { border-color: var(--pink) !important; box-shadow: 0 0 10px var(--pink); }
    </style>
</head>
<body>

    <div id="side-panel">
        <div id="chat-window">
            <div class="ai-msg">[SISTEMA] **v53: Ghost Control.** <br>1. Injeta o código. <br>2. Liga o Mestre. <br>3. O **SLOT_0** agora comanda os outros por injeção de script.</div>
        </div>
        
        <button class="btn-main btn-select" onclick="document.getElementById('code-area').select()">🟦 SELECIONAR TUDO</button>
        <button class="btn-main btn-master" id="master-btn" onclick="toggleMasterSync()">⚡ LIGAR COMANDO GHOST</button>

        <input type="file" id="file-input" accept=".zip,.html" style="display:none" onchange="processarArquivo(event)">
        <button class="btn-main btn-files" onclick="document.getElementById('file-input').click()">📂 CARREGAR ZIP/HTML</button>

        <textarea id="code-area" placeholder="Código aqui..."></textarea>
        
        <div class="btn-group">
            <button class="btn-main btn-add" onclick="adicionarSlot()">+ SLOT</button>
            <button class="btn-main btn-rem" onclick="removerSlot()">- SLOT</button>
            <button class="btn-main btn-inj" onclick="atualizarSlot()">INJETAR</button>
            <button class="btn-main btn-all" onclick="injetarEmTodos()">INJETAR TUDO</button>
        </div>
    </div>

    <div id="viewport"></div>

<script>
    let totalSlots = 0;
    let codigosDosSlots = [];
    let masterSync = false;
    let slotAtivo = 0;

    function toggleMasterSync() {
        masterSync = !masterSync;
        const btn = document.getElementById('master-btn');
        btn.classList.toggle('active', masterSync);
        const s0 = document.getElementById('slot0');
        if(s0) s0.classList.toggle('is-master', masterSync);
        addChat(masterSync ? "GHOST ON: O SLOT_0 controla os outros." : "GHOST OFF", "ai-msg");
    }

    // O NOVO SCRIPT DE INJEÇÃO (Mais agressivo)
    function atualizarSlot(idx = slotAtivo) {
        const code = document.getElementById('code-area').value;
        codigosDosSlots[idx] = code;
        const frame = document.getElementById('f' + idx);
        
        const ghostScript = `
        <script>
            // CAPTURA TUDO NO MESTRE
            if(${idx} === 0) {
                document.addEventListener('click', (e) => {
                    window.parent.postMessage({type: 'GHOST_CLICK', x: e.clientX, y: e.clientY}, '*');
                }, true);
                document.addEventListener('keydown', (e) => {
                    window.parent.postMessage({type: 'GHOST_KEY', key: e.key, code: e.code}, '*');
                }, true);
            }

            // EXECUTA NOS ESCRAVOS
            window.addEventListener('message', (e) => {
                if(e.data.type === 'EXEC_CLICK') {
                    const el = document.elementFromPoint(e.data.x, e.data.y);
                    if(el) {
                        el.click();
                        el.focus();
                        // Força evento de mouse real
                        el.dispatchEvent(new MouseEvent('mousedown', {bubbles:true, clientX: e.data.x, clientY: e.data.y}));
                        el.dispatchEvent(new MouseEvent('mouseup', {bubbles:true}));
                    }
                }
                if(e.data.type === 'EXEC_KEY') {
                    const ev = new KeyboardEvent('keydown', {key: e.data.key, code: e.data.code, bubbles: true});
                    document.dispatchEvent(ev);
                    if(document.activeElement) document.activeElement.dispatchEvent(ev);
                }
            });
        <\/script>`;

        const doc = frame.contentDocument || frame.contentWindow.document;
        doc.open(); doc.write(code + ghostScript); doc.close();
    }

    // RELÉ DE COMANDO (Main Window)
    window.addEventListener('message', (e) => {
        if(!masterSync) return;

        for(let i=1; i<totalSlots; i++) {
            const f = document.getElementById('f' + i);
            if(f && f.contentWindow) {
                if(e.data.type === 'GHOST_CLICK') f.contentWindow.postMessage({type: 'EXEC_CLICK', x: e.data.x, y: e.data.y}, '*');
                if(e.data.type === 'GHOST_KEY') f.contentWindow.postMessage({type: 'EXEC_KEY', key: e.data.key, code: e.data.code}, '*');
            }
        }
    });

    function adicionarSlot() {
        const id = totalSlots;
        const div = document.createElement('div');
        div.className = 'slot'; div.id = 'slot' + id;
        div.innerHTML = `<div class="slot-header"><span>SLOT_${id}</span> <button onclick="selecionarSlot(${id})">EDIT</button></div><iframe id="f${id}"></iframe>`;
        document.getElementById('viewport').appendChild(div);
        codigosDosSlots.push("");
        totalSlots++;
        if(totalSlots === 1) selecionarSlot(0);
    }

    function injetarEmTodos() {
        for(let i=0; i<totalSlots; i++) atualizarSlot(i);
    }

    function selecionarSlot(idx) {
        slotAtivo = idx;
        document.querySelectorAll('.slot').forEach(s => s.style.borderColor = '#1a1a1a');
        if(document.getElementById('slot' + idx)) document.getElementById('slot' + idx).style.borderColor = 'var(--neon)';
        document.getElementById('code-area').value = codigosDosSlots[idx] || "";
    }

    function removerSlot() {
        if (totalSlots > 0) { document.getElementById('slot' + (totalSlots - 1)).remove(); codigosDosSlots.pop(); totalSlots--; }
    }

    async function processarArquivo(event) {
        const file = event.target.files[0];
        if (!file) return;
        const reader = new FileReader();
        reader.onload = async (e) => {
            let code = e.target.result;
            if (file.name.endsWith('.zip')) {
                const zip = await JSZip.loadAsync(e.target.result);
                const htmlFile = Object.values(zip.files).find(f => f.name.endsWith('.html'));
                code = htmlFile ? await htmlFile.async("string") : code;
            }
            document.getElementById('code-area').value = code;
            atualizarSlot();
        };
        if (file.name.endsWith('.zip')) reader.readAsArrayBuffer(file);
        else reader.readAsText(file);
    }

    function addChat(txt, cl) {
        const d = document.createElement('div'); d.className = cl;
        d.innerHTML = `[BIO.ZON] ${txt}`;
        document.getElementById('chat-window').appendChild(d);
        document.getElementById('chat-window').scrollTop = 9999;
    }

    for(let i=0; i<6; i++) adicionarSlot();
</script>
</body>
</html>
