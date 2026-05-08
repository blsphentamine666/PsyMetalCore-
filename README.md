
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>MEATCORE // GIGER FORGE | TATTOO AI + TRAINING PIT</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rubik+Glitch&family=Special+Elite&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }

        body {
            background: #0a0101;
            font-family: 'Orbitron', 'Special Elite', monospace;
            color: #ecc9b0;
            overflow-x: hidden;
            position: relative;
        }

        /* ---- TEXTURAS GIGER / ROJAS / CARNE ---- */
        body::before {
            content: "";
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background-image: repeating-linear-gradient(45deg, rgba(120, 20, 10, 0.15) 0px, rgba(120, 20, 10, 0.15) 2px, transparent 2px, transparent 8px),
                              repeating-linear-gradient(135deg, rgba(80, 8, 8, 0.2) 0px, rgba(80, 8, 8, 0.2) 1px, transparent 1px, transparent 12px),
                              url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" opacity="0.2"><path fill="%238b0000" d="M20,30 L35,15 L50,28 L65,12 L80,25 L75,45 L85,60 L70,78 L50,72 L30,82 L15,65 L20,45 Z" /></svg>');
            background-repeat: repeat, repeat, repeat;
            background-size: auto, auto, 45px;
            pointer-events: none;
            z-index: 0;
        }

        /* venas biomecánicas */
        .veins {
            position: fixed;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 30% 20%, transparent 60%, #6a0e0e30 90%);
            pointer-events: none;
            z-index: 1;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 10;
        }

        /* estilo cajas metálico sangriento */
        .giger-card {
            background: rgba(12, 2, 2, 0.85);
            backdrop-filter: blur(6px);
            border: 1px solid #b32b1a;
            border-radius: 32px;
            padding: 22px;
            margin-bottom: 28px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.6), inset 0 0 20px rgba(180, 20, 0, 0.3);
            transition: transform 0.2s, border-color 0.2s;
        }

        .giger-card:hover {
            border-color: #ec4a2e;
            box-shadow: 0 0 15px #b12b1a;
        }

        h2 {
            font-family: 'Rubik Glitch', cursive;
            font-size: 1.9rem;
            border-left: 7px solid #c02a18;
            padding-left: 18px;
            margin-bottom: 20px;
            text-shadow: 2px 2px 0 #3a0303;
            letter-spacing: 1px;
        }

        button, .btn-style {
            background: #2d0d0d;
            border: none;
            font-family: 'Orbitron', monospace;
            font-weight: bold;
            color: #ffcdb0;
            border-radius: 40px;
            padding: 12px 24px;
            cursor: pointer;
            transition: all 0.15s linear;
            box-shadow: 0 4px 0 #4a0c0c;
            margin: 8px 6px 0 0;
            font-size: 0.9rem;
        }

        button:active {
            transform: translateY(2px);
            box-shadow: 0 1px 0 #4a0c0c;
        }

        button:hover {
            background: #a82414;
            color: white;
            text-shadow: 0 0 4px red;
            letter-spacing: 1px;
        }

        .style-btn {
            background: #1d0404;
            border: 1px solid #aa3a28;
            padding: 8px 20px;
            border-radius: 60px;
        }

        .active-style {
            background: #b12a1a;
            box-shadow: 0 0 12px #ff5722;
            border-color: #ffa066;
        }

        input, textarea {
            background: #170202;
            border: 1px solid #b34e3a;
            border-radius: 60px;
            padding: 12px 18px;
            width: 100%;
            color: #ffbc8c;
            font-family: monospace;
            margin: 12px 0;
        }

        .token-area {
            display: flex;
            gap: 12px;
            align-items: center;
        }

        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 28px;
        }

        @media (max-width: 880px) {
            .grid-2 { grid-template-columns: 1fr; }
        }

        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
            gap: 18px;
            margin-top: 20px;
        }

        .gallery-item {
            background: #080000;
            border-radius: 24px;
            overflow: hidden;
            border: 1px solid #bc3925;
            transition: 0.2s;
        }

        .gallery-item img {
            width: 100%;
            aspect-ratio: 1 / 1;
            object-fit: cover;
            display: block;
        }

        .train-thumb {
            width: 70px;
            height: 70px;
            object-fit: cover;
            border-radius: 18px;
            border: 2px solid #c5422c;
            margin: 5px;
        }

        .loader {
            width: 45px;
            height: 45px;
            border: 4px solid #411010;
            border-top: 4px solid #e64b2e;
            border-radius: 50%;
            animation: spin 0.9s linear infinite;
            margin: 12px auto;
        }

        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        .mockup-check {
            background: #2d0e0a;
            border-radius: 40px;
            padding: 10px 16px;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            margin: 12px 0;
        }

        footer {
            text-align: center;
            margin-top: 50px;
            padding: 22px;
            border-top: 1px solid #ab2c1a;
            font-size: 0.7rem;
        }

        .status-text {
            font-family: monospace;
            font-size: 0.8rem;
            color: #e68a6a;
        }

        i {
            margin-right: 8px;
        }
    </style>
</head>
<body>
<div class="veins"></div>
<div class="container">
    <div style="text-align:center; margin-bottom: 25px;">
        <h1 style="font-family: 'Rubik Glitch'; font-size: 3.7rem; letter-spacing: 5px; background: linear-gradient(145deg, #bc3824, #560d0d); -webkit-background-clip: text; background-clip: text; color: transparent; filter: drop-shadow(0 0 12px #8a1c0c);"><i class="fas fa-skull"></i> KOMBAT NEXUS <i class="fas fa-dragon"></i></h1>
        <div class="status-text">⚡ GIGER // MEATCORE // FLESH ALCHEMY ⚡ [ TATTOO INFERNO ENGINE + STYLE TRAINING ]</div>
    </div>

    <div class="grid-2">
        <!-- COLUMNA IZQ: GENERACIÓN + ENTRENAMIENTO -->
        <div>
            <div class="giger-card">
                <h2><i class="fas fa-fire"></i> BLOOD GENERATOR</h2>
                <div class="token-area">
                    <input type="text" id="hfToken" placeholder="🔑 hf_xxxxxxxx... (token Hugging Face)" style="flex:2">
                    <button id="saveTokenBtn" style="padding:10px 20px;"><i class="fas fa-key"></i> Guardar</button>
                </div>
                <div id="tokenMsg" class="status-text"></div>
                
                <div style="display: flex; flex-wrap: wrap; gap: 12px; margin: 20px 0 10px;">
                    <button data-style="anime" class="style-btn active-style"><i class="fas fa-draw-polygon"></i> ANIME</button>
                    <button data-style="tribal" class="style-btn"><i class="fas fa-dragon"></i> TRIBAL</button>
                    <button data-style="gore" class="style-btn"><i class="fas fa-biohazard"></i> GORE</button>
                    <button data-style="cybersigil" class="style-btn"><i class="fas fa-microchip"></i> CYBER SIGILS</button>
                    <button data-style="neotribal" class="style-btn"><i class="fas fa-waveform"></i> NEO TRIBAL</button>
                </div>
                
                <div class="mockup-check">
                    <input type="checkbox" id="mockupMode"> 
                    <label><i class="fas fa-tshirt"></i> MOCKUP TATTOO (efecto brazo/piel biomecánica)</label>
                </div>
                
                <button id="generateImageBtn" style="width:100%; margin-top: 12px;"><i class="fas fa-skull-crossbones"></i> INVOCAR FLASH / MOCKUP</button>
                <div id="genLoader" style="display: none;"><div class="loader"></div><div class="status-text">🩸 Giger está tejiendo carne y tinta...</div></div>
                <div id="genError" class="status-text" style="color:#ff7568;"></div>
            </div>

            <div class="giger-card">
                <h2><i class="fas fa-chalkboard-user"></i> ENTRENA TU PROPIO ESTILO</h2>
                <p style="font-size:0.75rem;"><i class="fas fa-info-circle"></i> Sube entre 3 y 8 diseños Flash / Tatuajes tuyos. El sistema extraerá la paleta y esencia para personalizar prompts futuros.</p>
                <input type="file" id="trainInput" multiple accept="image/jpeg,image/png,image/jpg">
                <div id="trainPreviewArea" class="training-preview" style="display:flex; flex-wrap:wrap; gap:10px; margin:15px 0;"></div>
                <input type="text" id="customStyleName" placeholder="Nombre de tu estilo (ej: RITUAL CARNE)">
                <button id="trainStyleBtn"><i class="fas fa-brain"></i> ENTRENAR MODELO (inyección semántica)</button>
                <div id="trainStatusDisplay" class="status-text"></div>
                <div id="trainedBadge" style="background:#2f0b0b; border-radius:20px; padding:8px; margin-top:12px; display:none;"></div>
            </div>
        </div>

        <!-- COLUMNA DER: GALERIA Y PROMPT DINÁMICO-->
        <div>
            <div class="giger-card">
                <h2><i class="fas fa-images"></i> FLASH // MOCKUPS SANGRIENTOS</h2>
                <div id="gallery" class="gallery">
                    <div class="status-text" style="text-align:center;">⚔️ Las invocaciones aparecerán aquí ⚔️</div>
                </div>
                <button id="clearGalleryBtn" style="margin-top:16px;"><i class="fas fa-trash-alt"></i> VACIAR CARNERO</button>
            </div>
            <div class="giger-card">
                <h2><i class="fas fa-scroll"></i> NECRO PROMPT ENGINE</h2>
                <div id="promptPreviewLive" class="status-text" style="background:#200606; border-radius: 24px; padding: 16px; font-size:0.75rem; white-space: pre-wrap; word-break: break-word;">⚡ Esperando forja...</div>
                <div class="status-text" style="margin-top: 10px;"><i class="fas fa-dice-d6"></i> El entrenamiento modifica el prompt con tu ADN visual</div>
            </div>
        </div>
    </div>
    <footer>
        <i class="fas fa-cog"></i> INFERNO AI · Modelo: Stable Diffusion v2.1 · Entrenamiento conceptual (simulación con análisis de imagen) · Para usar IA real necesitas token HF gratis · Mockup overlays biomecánicos
    </footer>
</div>

<script>
    // -------------------- ESTADO GLOBAL --------------------
    let activeStyle = "anime";
    let trainedActive = false;
    let trainedPromptAddon = "";
    let trainedName = "";
    let uploadedImagesData = []; // almacena objetos {src, colorFeatures}
    let hfToken = localStorage.getItem("hf_token") || "";
    
    // DOM elements
    const tokenInput = document.getElementById('hfToken');
    const saveTokenBtn = document.getElementById('saveTokenBtn');
    const styleBtns = document.querySelectorAll('.style-btn');
    const generateBtn = document.getElementById('generateImageBtn');
    const genLoader = document.getElementById('genLoader');
    const genError = document.getElementById('genError');
    const galleryDiv = document.getElementById('gallery');
    const clearGalleryBtn = document.getElementById('clearGalleryBtn');
    const mockupCheck = document.getElementById('mockupMode');
    const trainInput = document.getElementById('trainInput');
    const trainPreviewArea = document.getElementById('trainPreviewArea');
    const customStyleNameInput = document.getElementById('customStyleName');
    const trainStyleBtn = document.getElementById('trainStyleBtn');
    const trainStatusDisplay = document.getElementById('trainStatusDisplay');
    const trainedBadge = document.getElementById('trainedBadge');
    const promptPreviewLive = document.getElementById('promptPreviewLive');
    
    if(hfToken) tokenInput.value = hfToken;
    
    saveTokenBtn.addEventListener('click', () => {
        hfToken = tokenInput.value.trim();
        localStorage.setItem("hf_token", hfToken);
        document.getElementById('tokenMsg').innerHTML = "✅ Token almacenado (cárnico)";
        setTimeout(()=> document.getElementById('tokenMsg').innerHTML="", 2000);
    });
    
    // Estilos
    styleBtns.forEach(btn => {
        btn.addEventListener('click', () => {
            styleBtns.forEach(b => b.classList.remove('active-style'));
            btn.classList.add('active-style');
            activeStyle = btn.dataset.style;
            updatePromptPreview();
        });
    });
    
    function getStyleDescriptor(style) {
        const map = {
            anime: "anime tattoo, vibrant inks, cel-shaded, manga screentone, kawaii but dark, dynamic action lines",
            tribal: "tribal blackwork, polynesian-maori fusion, sharp pointed arcs, aggressive patterns, dark symmetry",
            gore: "gore tattoo, visceral meat, exposed flesh, blood splatter, biomechanical entrails, splatterpunk",
            cybersigil: "cyber sigils, neon ritual symbols, cyberpunk tribal, encrypted runes, glitch circuits, bio-digital",
            neotribal: "neo tribal, futuristic geometry, organic techno ornaments, 3D relief, alien biomechanics"
        };
        return map[style] || "dark fantasy tattoo";
    }
    
    // Construir prompt final + modificación de entrenamiento
    function buildUltimatePrompt() {
        let baseDesc = getStyleDescriptor(activeStyle);
        let meatGigerCore = "meatcore aesthetic, HR Giger biomechanical, blood red, Mortal Kombat fatalities atmosphere, body horror, flesh metal, spikes, skull motifs, chains, high detailed tattoo design, flash art, sharp lines, dark red and black.";
        let trainedInjection = trainedActive ? ` || ESTILO ENTRENADO: ${trainedName} -> INFLUENCIA VISUAL: ${trainedPromptAddon} || ` : "";
        let prompt = `Tattoo design, ${baseDesc}, ${meatGigerCore}, ${trainedInjection} ultra detailed, 8k, intricate, symmetrical, album cover art, dark ritual.`;
        let negative = "worst quality, lowres, watermark, text, ugly, deformed, blurry, smooth, boring, plain background, cartoonish, 3d render";
        return { prompt: prompt.substring(0, 800), negative };
    }
    
    function updatePromptPreview() {
        let { prompt } = buildUltimatePrompt();
        promptPreviewLive.innerHTML = `<i class="fas fa-fire"></i> ${prompt.substring(0, 280)}...`;
    }
    
    // ----- GENERACIÓN REAL CON HUGGING FACE (SD) -----
    async function generateTattooImage(prompt, negative) {
        if(!hfToken) throw new Error("🔴 Token de Hugging Face requerido. Ingrésalo y guarda.");
        const model = "stabilityai/stable-diffusion-2-1";
        const response = await fetch(`https://api-inference.huggingface.co/models/${model}`, {
            method: "POST",
            headers: { "Authorization": `Bearer ${hfToken}`, "Content-Type": "application/json" },
            body: JSON.stringify({
                inputs: prompt,
                parameters: { negative_prompt: negative, num_inference_steps: 30, guidance_scale: 8, width: 512, height: 512 }
            })
        });
        if(!response.ok) {
            let errText = await response.text();
            throw new Error(`HF error ${response.status}: ${errText.slice(0,120)}`);
        }
        const blob = await response.blob();
        return URL.createObjectURL(blob);
    }
    
    // efector mockup: simular tatuaje sobre piel metálica giger
    async function mockupEffect(imageUrl) {
        return new Promise((resolve) => {
            const img = new Image();
            img.crossOrigin = "Anonymous";
            img.onload = () => {
                const canvas = document.createElement('canvas');
                canvas.width = 512; canvas.height = 512;
                const ctx = canvas.getContext('2d');
                // fondo textura carne oscura
                ctx.fillStyle = "#8f5e45";
                ctx.fillRect(0,0,512,512);
                // textura rugosa
                for(let i=0;i<500;i++) {
                    ctx.fillStyle = `rgba(70,25,15,${Math.random()*0.5})`;
                    ctx.fillRect(Math.random()*512, Math.random()*512, 3, 3);
                }
                // añadir venas
                ctx.strokeStyle = "#a03322";
                ctx.lineWidth = 4;
                for(let v=0;v<30;v++) {
                    ctx.beginPath();
                    ctx.moveTo(Math.random()*512, Math.random()*512);
                    ctx.lineTo(Math.random()*512, Math.random()*512);
                    ctx.stroke();
                }
                // superponer tatuaje modo multiplicar
                ctx.globalCompositeOperation = "multiply";
                ctx.drawImage(img, 40, 70, 432, 380);
                ctx.globalCompositeOperation = "source-over";
                // bordes biomecánicos con remaches
                ctx.strokeStyle = "#be3420";
                ctx.lineWidth = 14;
                ctx.strokeRect(20, 50, 472, 420);
                for(let r=0;r<12;r++) {
                    ctx.fillStyle = "#c04228";
                    ctx.beginPath();
                    ctx.arc(35 + r*40, 70, 8, 0, Math.PI*2);
                    ctx.fill();
                    ctx.fillStyle = "#6a1a0c";
                    ctx.beginPath();
                    ctx.arc(35 + r*40, 70, 3, 0, Math.PI*2);
                    ctx.fill();
                }
                canvas.toBlob(blob => resolve(URL.createObjectURL(blob)));
            };
            img.src = imageUrl;
        });
    }
    
    function addImageToGallery(imageUrl) {
        if(galleryDiv.children.length === 1 && galleryDiv.children[0].innerText.includes("Las invocaciones")) galleryDiv.innerHTML = '';
        const item = document.createElement('div');
        item.className = 'gallery-item';
        const img = document.createElement('img');
        img.src = imageUrl;
        const delBtn = document.createElement('button');
        delBtn.innerHTML = '<i class="fas fa-trash-alt"></i>';
        delBtn.style.margin = "8px auto";
        delBtn.style.display = "block";
        delBtn.style.padding = "5px";
        delBtn.onclick = () => item.remove();
        item.appendChild(img);
        item.appendChild(delBtn);
        galleryDiv.prepend(item);
    }
    
    generateBtn.addEventListener('click', async () => {
        genLoader.style.display = "block";
        genError.innerText = "";
        try {
            const { prompt, negative } = buildUltimatePrompt();
            console.log("Prompt:", prompt);
            let rawImgUrl = await generateTattooImage(prompt, negative);
            let finalUrl = rawImgUrl;
            if(mockupCheck.checked) {
                finalUrl = await mockupEffect(rawImgUrl);
                URL.revokeObjectURL(rawImgUrl);
            }
            addImageToGallery(finalUrl);
        } catch(err) {
            genError.innerText = "
