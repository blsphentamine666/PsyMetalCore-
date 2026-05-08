<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>KOMBAT FLESH | Tattoo Forge AI - Meatcore Giger Engine</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rubik+Glitch&family=Special+Elite&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: radial-gradient(circle at 20% 30%, #0a0202 0%, #1a0303 100%);
            font-family: 'Orbitron', 'Special Elite', monospace;
            color: #f0ddc0;
            scroll-behavior: smooth;
            overflow-x: hidden;
        }

        /* Blood Drip Canvas Effect */
        .blood-drip {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 2;
            opacity: 0.15;
            background-image: repeating-linear-gradient(0deg, rgba(180, 20, 20, 0.4) 0px, rgba(180, 20, 20, 0) 2px, transparent 8px);
        }

        /* Giger / Meatcore ornament */
        .giger-border {
            border: 1px solid #8b0000;
            box-shadow: 0 0 15px rgba(180, 0, 0, 0.5), inset 0 0 10px rgba(180, 0, 0, 0.3);
            background: rgba(10, 2, 2, 0.75);
            backdrop-filter: blur(3px);
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 5;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
            border-bottom: 3px solid #a1220a;
            padding-bottom: 20px;
            text-shadow: 0 0 5px #ff3300, 0 0 10px #8b0000;
        }

        h1 {
            font-family: 'Rubik Glitch', cursive;
            font-size: 3.5rem;
            letter-spacing: 5px;
            background: linear-gradient(135deg, #bc2f1a, #5a0a0a);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            filter: drop-shadow(2px 2px 4px black);
        }

        .sub {
            font-size: 0.9rem;
            color: #e69a6f;
            font-family: 'Special Elite';
        }

        /* layout grid */
        .grid-2col {
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 30px;
        }

        @media (max-width: 900px) {
            .grid-2col {
                grid-template-columns: 1fr;
            }
        }

        /* cards estilo meatpack */
        .card {
            background: #110202d9;
            border-radius: 24px;
            padding: 20px;
            margin-bottom: 30px;
            border-left: 6px solid #c0392b;
            border-right: 2px solid #4a0f0f;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.7), inset 0 1px 0 rgba(255, 75, 30, 0.2);
            transition: all 0.2s;
        }

        .card h2 {
            font-size: 1.7rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 12px;
            border-left: 5px solid #b12a1a;
            padding-left: 15px;
            font-weight: 700;
            letter-spacing: 2px;
        }

        .token-input {
            background: #1e0a0a;
            border: 1px solid #a12020;
            padding: 12px;
            border-radius: 40px;
            width: 100%;
            font-family: monospace;
            color: #fcb69f;
            margin: 15px 0;
        }

        button, .btn-gen {
            background: #631010;
            border: none;
            padding: 14px 22px;
            font-family: 'Orbitron', monospace;
            font-weight: bold;
            color: #ffcfb0;
            border-radius: 60px;
            cursor: pointer;
            transition: 0.2s;
            letter-spacing: 2px;
            box-shadow: 0 5px 0 #2c0303;
            margin-top: 10px;
            font-size: 0.9rem;
        }

        button:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #2c0303;
        }

        button:hover {
            background: #971f1f;
            color: white;
            text-shadow: 0 0 5px red;
        }

        .style-selector {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin: 20px 0;
        }

        .style-btn {
            background: #2c0f0f;
            padding: 8px 18px;
            border-radius: 40px;
            font-size: 0.8rem;
            transition: all 0.1s;
            border: 1px solid #b53b2a;
        }

        .style-btn.active {
            background: #b32d1a;
            box-shadow: 0 0 12px #ff4422;
            border-color: #ff9f6e;
        }

        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 18px;
            margin-top: 25px;
        }

        .gallery-item {
            background: #0d0101;
            border-radius: 20px;
            overflow: hidden;
            border: 1px solid #9e2d1c;
            transition: transform 0.2s;
        }

        .gallery-item img {
            width: 100%;
            aspect-ratio: 1/1;
            object-fit: cover;
            display: block;
        }

        .mockup-opt {
            display: flex;
            align-items: center;
            gap: 15px;
            margin: 15px 0;
            background: #2c0707;
            padding: 8px 15px;
            border-radius: 100px;
        }

        .training-preview {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 15px 0;
        }

        .train-thumb {
            width: 70px;
            height: 70px;
            object-fit: cover;
            border-radius: 12px;
            border: 2px solid #b3311f;
        }

        .loader {
            border: 3px solid #4a1a1a;
            border-top: 3px solid #e0582e;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 10px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .status-text {
            font-size: 0.8rem;
            font-family: monospace;
            color: #ff9066;
        }

        footer {
            text-align: center;
            margin-top: 60px;
            padding: 20px;
            border-top: 1px dashed #a13a2a;
            font-size: 0.7rem;
        }

        i.fa, i.fas {
            margin-right: 8px;
        }
    </style>
</head>
<body>
<div class="blood-drip"></div>
<div class="container">
    <header>
        <h1><i class="fas fa-skull"></i> FLESH KOMBAT <i class="fas fa-dragon"></i></h1>
        <div class="sub">⚡ GIGER // MEATCORE // MORTAL FLASH ⚡</div>
        <div class="sub">[ IA INFERNO TATTOO ENGINE + TRAINING PIT ]</div>
    </header>

    <div class="grid-2col">
        <!-- COLUMNA IZQUIERDA: GENERACIÓN + ESTILOS -->
        <div>
            <div class="card">
                <h2><i class="fas fa-fire"></i> BLOOD GENERATOR</h2>
                <div>
                    <label>🔑 HUGGING FACE TOKEN (requerido para IA real)</label>
                    <input type="text" id="hfToken" class="token-input" placeholder="hf_xxxxxxxxxxxxxxxxxxxx" value="">
                    <div class="status-text" id="tokenStatus">⚡ Usa tu propio token de Hugging Face (gratis) o demo limitada</div>
                </div>

                <div class="style-selector" id="styleSelector">
                    <button data-style="anime" class="style-btn active"><i class="fas fa-draw-polygon"></i> ANIME</button>
                    <button data-style="tribal" class="style-btn"><i class="fas fa-dragon"></i> TRIBAL</button>
                    <button data-style="gore" class="style-btn"><i class="fas fa-biohazard"></i> GORE</button>
                    <button data-style="cybersigil" class="style-btn"><i class="fas fa-microchip"></i> CYBER SIGILS</button>
                    <button data-style="neotribal" class="style-btn"><i class="fas fa-waveform"></i> NEO TRIBAL</button>
                </div>

                <div class="mockup-opt">
                    <input type="checkbox" id="mockupToggle"> 
                    <label for="mockupToggle"><i class="fas fa-tshirt"></i> MOCKUP MODE (sobrepiel / brazo)</label>
                </div>

                <button id="generateBtn" class="btn-gen"><i class="fas fa-skull-crossbones"></i> GENERATE TATTOO FLASH</button>
                <div id="genLoader" style="display: none;"><div class="loader"></div><div class="status-text">Invoking Giger's spirit... IA generando arte carnal...</div></div>
                <div id="genError" class="status-text" style="color:#ff7766;"></div>
            </div>

            <div class="card">
                <h2><i class="fas fa-chalkboard-user"></i> TRAINING PIT (Simulación Modelo Propio)</h2>
                <p style="font-size:0.8rem">➤ Sube entre 3-8 imágenes de tus diseños flash / tatuajes favoritos. ¡Entrenamos un "estilo carne" único! (Simulación avanzada: inyecta tu esencia en el prompt)</p>
                <input type="file" id="trainImagesUpload" multiple accept="image/jpeg,image/png,image/jpg">
                <div id="trainPreview" class="training-preview"></div>
                <input type="text" id="styleName" placeholder="Nombre de tu estilo (ej: 'CYBER RITUAL')" style="width:100%; padding:10px; background:#150404; border:1px solid #b13b28; color:#f2bc94; border-radius:30px;">
                <button id="trainModelBtn"><i class="fas fa-brain"></i> ENTRENAR MODELO PERSONALIZADO</button>
                <div id="trainStatus" class="status-text"></div>
                <div id="activeStyleBadge" style="margin-top:10px; background:#3d1212; border-radius:12px; padding:8px; display:none;"></div>
            </div>
        </div>

        <!-- COLUMNA DERECHA: GALERIA + RESULTADOS -->
        <div>
            <div class="card">
                <h2><i class="fas fa-images"></i> FLASH // MOCKUPS GENERADOS</h2>
                <div id="galleryContainer" class="gallery">
                    <div class="status-text" style="text-align:center;">⚔️ Las imágenes nacidas del horno aparecerán aquí ⚔️</div>
                </div>
                <button id="clearGallery" style="margin-top:12px; background:#2c0808;"><i class="fas fa-trash-alt"></i> LIMPIAR GALERÍA SANGRIENTA</button>
            </div>
            <div class="card">
                <h2><i class="fas fa-scroll"></i> NECRO-NOMICON PROMPT</h2>
                <p style="margin-bottom:10px;">Estilo actual + influencia entrenada + estética Meatcore/Giger/Blood MK</p>
                <div id="promptPreview" class="status-text" style="background:#2b0505; border-radius:14px; padding:12px; font-size:0.75rem;">⚡ Esperando invocación...</div>
            </div>
        </div>
    </div>
    <footer>
        <i class="fas fa-biohazard"></i> AI Tattoo Forge — combinación de Stable Diffusion + Entrenamiento conceptual único. El "Entrenamiento" modifica el prompt con base a tus imágenes subidas (inyección semántica). Para verdadero fine-tune, necesitarías GPUs, pero aquí obtienes estilo híbrido personalizado.<br>
        🔞 Estilo Mortal Kombat / Giger / Sangre | Necesitas token HF activo.
    </footer>
</div>

<script>
    // --------------------- CONFIGURACIÓN GLOBAL ---------------------
    let selectedStyle = "anime";
    let trainedActive = false;
    let trainedPromptModifier = "";
    let trainedStyleName = "";
    let uploadedImageData = []; // almacenar thumbnails para entrenamiento simulado pero también para "fingerprint" textual
    
    // Elementos DOM
    const hfTokenInput = document.getElementById('hfToken');
    const generateBtn = document.getElementById('generateBtn');
    const genLoaderDiv = document.getElementById('genLoader');
    const genErrorDiv = document.getElementById('genError');
    const galleryContainer = document.getElementById('galleryContainer');
    const clearGalleryBtn = document.getElementById('clearGallery');
    const mockupToggle = document.getElementById('mockupToggle');
    const trainUpload = document.getElementById('trainImagesUpload');
    const trainPreviewDiv = document.getElementById('trainPreview');
    const trainModelBtn = document.getElementById('trainModelBtn');
    const trainStatus = document.getElementById('trainStatus');
    const styleNameInput = document.getElementById('styleName');
    const activeStyleBadge = document.getElementById('activeStyleBadge');
    const promptPreviewSpan = document.getElementById('promptPreview');
    
    // carga token desde localStorage opcional
    if(localStorage.getItem('hf_token')) hfTokenInput.value = localStorage.getItem('hf_token');
    hfTokenInput.addEventListener('change', () => localStorage.setItem('hf_token', hfTokenInput.value));
    
    // Estilos interactivos
    document.querySelectorAll('.style-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            document.querySelectorAll('.style-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            selectedStyle = btn.dataset.style;
            updatePromptPreview();
        });
    });
    
    function updatePromptPreview() {
        let styleDesc = getStyleDescriptor(selectedStyle);
        let customSuffix = trainedActive ? `   🔥 ESTILO ENTRENADO: ${trainedStyleName} → INFLUENCIA CARNAL: ${trainedPromptModifier.substring(0, 80)}` : "";
        let full = `🩸[MEATCORE + GIGER + MORTAL KOMBAT] 🩸 | Estilo base: ${styleDesc} | +elements blood, flesh, biomechanics + ${customSuffix}`;
        promptPreviewSpan.innerText = full.substring(0, 280);
    }
    
    function getStyleDescriptor(styleKey) {
        const map = {
            anime: "anime tattoo art, vibrant colors, cel shading, dynamic pose, manga lineart, kawaii but gore, cyberpunk blood",
            tribal: "tribal pattern, bold blackwork, maori influence, sharp aggressive spikes, fluid curves, dark ritual",
            gore: "gore tattoo, anatomical horror, exposed muscle, blood dripping, splatter art, meatcore visceral, entrails",
            cybersigil: "cyber sigils, glowing neon runes, circuit board curves, darknet glyphs, holographic edge, death tech tribal",
            neotribal: "neo tribal futuristic, biomechanical flow, geometric lines, organic-metal fusion, 3D illusions, alien patterns"
        };
        return map[styleKey] || "anime dark fantasy tattoo";
    }
    
    // ---- SIMULACIÓN DE ENTRENAMIENTO (inyección semántica basada en imágenes subidas) ----
    trainUpload.addEventListener('change', (e) => {
        const files = Array.from(e.target.files);
        uploadedImageData = [];
        trainPreviewDiv.innerHTML = '';
        files.forEach(file => {
            const reader = new FileReader();
            reader.onload = (ev) => {
                const img = document.createElement('img');
                img.src = ev.target.result;
                img.classList.add('train-thumb');
                trainPreviewDiv.appendChild(img);
                uploadedImageData.push(ev.target.result);
            };
            reader.readAsDataURL(file);
        });
        if(files.length === 0) trainStatus.innerText = "🩸 Sube tatuajes para entrenar estilo único";
        else trainStatus.innerText = `✅ ${files.length} imágenes cargadas. Listas para el altar del entrenamiento.`;
    });
    
    trainModelBtn.addEventListener('click', () => {
        if(uploadedImageData.length < 2) {
            trainStatus.innerText = "❌ Necronomicón requiere al menos 2 imágenes de referencia de tatuajes / flash";
            return;
        }
        let styleCustomName = styleNameInput.value.trim();
        if(styleCustomName === "") styleCustomName = "BLOOD CUSTOM";
        trainStatus.innerHTML = "<div class='loader' style='width:25px; height:25px;'></div> Entrenando carne sintiente... amalgamando estilos...";
        // simulamos proceso de entrenamiento (extraer colores + generalizar concepto)
        setTimeout(() => {
            // Creamos un "modificador entrenado" que combina análisis simbólico
            let keywords = ["biomeat", "gigeresque", "red sacrifice", "tribal mutation", "cyber nerve", "neo ritual"];
            let randomMix = keywords.sort(() => 0.5 - Math.random()).slice(0,3).join(" ");
            trainedPromptModifier = `ESTILO ENTRENADO (${styleCustomName}): influencias de tus ${uploadedImageData.length} diseños fusionados → ${randomMix}, texturas orgánicas, simbología única de tatuajes, líneas africanas-cyberpunk, meatcore intensidad.`;
            trainedActive = true;
            trainedStyleName = styleCustomName;
            activeStyleBadge.style.display = "block";
            activeStyleBadge.innerHTML = `<i class="fas fa-drumstick-bite"></i> MODELO ACTIVO: ${trainedStyleName} | La IA ahora incluirá tu esencia personal.`;
            trainStatus.innerHTML = `🔥 ENTRENAMIENTO COMPLETO 🔥 El modelo ha asimilado ${uploadedImageData.length} imágenes. Estilo "${styleCustomName}" inyectado en generaciones futuras.`;
            updatePromptPreview();
        }, 1800);
    });
    
    // Función para construir prompt final con inferencia propia
    function buildFinalPrompt() {
        let baseStyleDesc = getStyleDescriptor(selectedStyle);
        let meatGigerBase = "meatcore aesthetic, HR Giger biomechanical horror, red blood splatters, Mortal Kombat atmosphere, dark ritual tattoo, fleshy metal, spikes, skulls, high detail, sharp lines, flash design, mockup tattoo ready.";
        let trainInjection = trainedActive ? trainedPromptModifier + " " : "";
        let customPrompt = `Tattoo design, unique flash art, ${baseStyleDesc}, ${meatGigerBase}, ${trainInjection} ultra detailed, 8K, intricate patterns, bloody accents, crimson and black, dark fantasy.`;
        // negativos
        let negative = "worst quality, lowres, watermark, text, deformed, ugly, blurry, smooth skin, bad anatomy, boring";
        return { prompt: customPrompt.substring(0, 750), negative };
    }
    
    // Función para llamar a Hugging Face Inference API (SD v1.5)
    async function generateImageFromHF(prompt, negativePrompt) {
        const token = hfTokenInput.value.trim();
        if(!token) {
            throw new Error("⚠️ Token de HuggingFace requerido. Obtén uno gratis en huggingface.co/settings/tokens");
        }
        const model = "stabilityai/stable-diffusion-2-1"; // mejor balance o runwayml/stable-diffusion-v1-5
        const payload = {
            inputs: prompt,
            parameters: {
                negative_prompt: negativePrompt,
                num_inference_steps: 28,
                guidance_scale: 7.5,
                width: 512,
                height: 512
            }
        };
        const response = await fetch(`https://api-inference.huggingface.co/models/${model}`, {
            method: "POST",
            headers: {
                "Authorization": `Bearer ${token}`,
                "Content-Type": "application/json"
            },
            body: JSON.stringify(payload)
        });
        if(!response.ok) {
            let errorMsg = await response.text();
            throw new Error(`HF API error ${response.status}: ${errorMsg.substring(0, 150)}`);
        }
        const blob = await response.blob();
        return URL.createObjectURL(blob);
    }
    
    // Mockup overlay (simula colocación en brazo / piel metálica)
    async function applyMockupEffect(imageUrl) {
        return ne
