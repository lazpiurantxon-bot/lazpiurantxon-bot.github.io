layout: page
title: "Ingeniero Pavazo"
permalink: /vp7
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>AV-7 · Grabadora</title>
    <style>
        :root {
            --bg: #d8d6d1;
            --device: #e9e7e2;
            --device-shadow: #c5c3be;
            --lcd-bg: #1a1c18;
            --lcd-text: #a3b899;
            --lcd-meter: #ff5500;
            --btn: #d1cfc9;
            --btn-active: #ff5500;
            --btn-rec: #e63946;
            --text: #333;
            --text-light: #777;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            background: var(--bg);
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: var(--text);
            overflow: hidden;
        }

        .device {
            width: 340px;
            height: 600px;
            background: var(--device);
            border-radius: 32px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.15), inset 0 1px 0 rgba(255,255,255,0.5);
            display: flex;
            flex-direction: column;
            padding: 24px;
            position: relative;
        }

        /* LCD */
        .lcd {
            background: var(--lcd-bg);
            border-radius: 12px;
            padding: 16px;
            color: var(--lcd-text);
            font-family: "Courier New", Courier, monospace;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.5);
            margin-bottom: 24px;
        }
        .lcd-top {
            display: flex;
            justify-content: space-between;
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 12px;
        }
        .lcd-meter-container {
            height: 8px;
            background: #0d0e0b;
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 12px;
        }
        .lcd-meter {
            height: 100%;
            width: 0%;
            background: var(--lcd-meter);
            transition: width 0.05s linear;
        }
        .lcd-bottom {
            font-size: 12px;
            opacity: 0.7;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* Disc */
        .disc-container {
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 24px;
        }
        .disc {
            width: 220px;
            height: 220px;
            border-radius: 50%;
            background: radial-gradient(circle, #f4f3f0 10%, #e0ddd5 40%, #c5c3be 100%);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2), inset 0 0 10px rgba(0,0,0,0.1);
            position: relative;
            touch-action: none;
            cursor: grab;
            transition: box-shadow 0.2s;
        }
        .disc:active { cursor: grabbing; }
        .disc-inner {
            position: absolute;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            width: 80px; height: 80px;
            border-radius: 50%;
            background: #d1cfc9;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.2);
        }
        .disc-dot {
            position: absolute;
            top: 20px; left: 50%;
            transform: translateX(-50%);
            width: 12px; height: 12px;
            border-radius: 50%;
            background: var(--btn-active);
        }

        /* Controls */
        .controls {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }
        .transport, .volume, .vol-btns {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 16px;
        }
        .volume {
            justify-content: space-between;
            padding: 0 10px;
        }
        .fader-container {
            display: flex;
            gap: 8px;
        }
        .fader-track {
            width: 6px;
            height: 60px;
            background: #c5c3be;
            border-radius: 3px;
            position: relative;
        }
        .fader-knob {
            position: absolute;
            left: -7px;
            top: 70%;
            width: 20px;
            height: 10px;
            background: #fff;
            border-radius: 2px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
            transition: top 0.1s ease-out;
        }

        .btn {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            border: none;
            background: var(--btn);
            color: var(--text);
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1), inset 0 1px 0 rgba(255,255,255,0.8);
            transition: all 0.1s;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .btn:active { transform: scale(0.95); box-shadow: 0 2px 3px rgba(0,0,0,0.1); }
        .btn.active { background: var(--btn-active); color: white; }
        .btn-rec.active { background: var(--btn-rec); }
        .btn-memo {
            width: 100%;
            border-radius: 24px;
            font-family: inherit;
            font-size: 14px;
            letter-spacing: 2px;
        }

        /* Permission Banner */
        .permission-banner {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(255, 85, 0, 0.95);
            color: white;
            padding: 16px 24px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            display: none;
            flex-direction: column;
            gap: 12px;
            z-index: 300;
            max-width: 90%;
            font-size: 14px;
        }
        .permission-banner.show {
            display: flex;
        }
        .permission-banner button {
            background: white;
            color: var(--btn-active);
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 14px;
        }
        .permission-banner .close-btn {
            position: absolute;
            top: 8px;
            right: 8px;
            background: none;
            color: white;
            font-size: 20px;
            padding: 4px 8px;
        }

        /* Memo Panel */
        .memo-panel {
            position: fixed;
            bottom: 0; left: 0; right: 0;
            background: white;
            border-radius: 24px 24px 0 0;
            box-shadow: 0 -10px 30px rgba(0,0,0,0.2);
            transform: translateY(100%);
            transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            max-height: 70vh;
            display: flex;
            flex-direction: column;
            z-index: 100;
        }
        .memo-panel.open { transform: translateY(0); }
        .memo-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            border-bottom: 1px solid #eee;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .memo-close {
            background: none; border: none; font-size: 24px; cursor: pointer; color: var(--text-light);
        }
        .memo-list {
            list-style: none;
            overflow-y: auto;
            padding: 10px 20px;
            flex: 1;
        }
        .memo-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 0;
            border-bottom: 1px solid #f0f0f0;
        }
        .memo-item.playing { background: #fff5f0; margin: 0 -20px; padding: 12px 20px; border-radius: 8px; }
        .memo-play {
            width: 36px; height: 36px; border-radius: 50%; border: none; background: var(--btn); cursor: pointer; font-size: 14px;
        }
        .memo-info { flex: 1; }
        .memo-name { font-weight: bold; font-size: 14px; }
        .memo-meta { font-size: 12px; color: var(--text-light); margin-top: 2px; }
        .memo-act {
            background: none; border: none; font-size: 18px; cursor: pointer; color: var(--text-light); text-decoration: none; padding: 8px;
        }
        .memo-empty {
            padding: 40px 20px;
            text-align: center;
            color: var(--text-light);
            font-size: 14px;
        }

        /* Toast */
        .toast {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: rgba(0,0,0,0.8);
            color: white;
            padding: 12px 24px;
            border-radius: 30px;
            font-size: 14px;
            opacity: 0;
            transition: all 0.3s;
            z-index: 200;
            pointer-events: none;
        }
        .toast.show {
            opacity: 1;
            transform: translateX(-50%) translateY(0);
        }
    </style>
</head>
<body>

<!-- Permission Banner -->
<div id="permissionBanner" class="permission-banner">
    <button class="close-btn" onclick="this.parentElement.classList.remove('show')">✕</button>
    <div>🎤 <strong>Se necesita acceso al micrófono</strong></div>
    <div style="font-size: 12px; opacity: 0.9;">Para grabar audio, debes permitir el acceso al micrófono en tu navegador.</div>
    <button id="grantPermissionBtn">Permitir micrófono</button>
</div>

<div class="device">
    <!-- LCD Screen -->
    <div class="lcd">
        <div class="lcd-top">
            <span id="lcdTime">0.00.00</span>
            <span id="lcdTake">00</span>
        </div>
        <div class="lcd-meter-container">
            <div id="lcdMeter" class="lcd-meter"></div>
        </div>
        <div class="lcd-bottom">HOY</div>
    </div>

    <!-- Rotating Disc -->
    <div class="disc-container">
        <div id="disc" class="disc">
            <div class="disc-inner"></div>
            <div class="disc-dot"></div>
        </div>
    </div>

    <!-- Controls -->
    <div class="controls">
        <div class="transport">
            <button id="recBtn" class="btn btn-rec" title="Grabar">●</button>
            <button id="playBtn" class="btn btn-play" title="Reproducir">▶</button>
            <button id="stopBtn" class="btn btn-stop" title="Parar">■</button>
            <button id="pinDot" class="btn btn-pin" title="Marca">▲</button>
        </div>
        <div class="volume">
            <div class="fader-container">
                <div class="fader-track"><div id="faderL" class="fader-knob"></div></div>
                <div class="fader-track"><div id="faderR" class="fader-knob"></div></div>
            </div>
            <div class="vol-btns">
                <button id="volDown" class="btn btn-vol" title="Bajar volumen">−</button>
                <button id="volUp" class="btn btn-vol" title="Subir volumen">+</button>
            </div>
        </div>
        <button id="memoBtn" class="btn btn-memo">MEMOS</button>
    </div>
</div>

<!-- Memo Panel -->
<div id="memoPanel" class="memo-panel" aria-hidden="true">
    <div class="memo-header">
        <span>Memos</span>
        <button id="memoClose" class="memo-close">✕</button>
    </div>
    <ul id="memoList" class="memo-list"></ul>
    <div id="memoEmpty" class="memo-empty">no hay grabaciones todavía —pulsa ● para grabar</div>
</div>

<!-- Toast -->
<div id="toast" class="toast"></div>

<script>
/* AV-7 — grabadora de voz. Grabación real (MediaRecorder), reproducción,
scrub girando el disco y persistencia en IndexedDB. */
(() => {
"use strict";
// ---------- elementos ----------
const disc = document.getElementById("disc");
const lcdTime = document.getElementById("lcdTime");
const lcdMeter = document.getElementById("lcdMeter");
const lcdTake = document.getElementById("lcdTake");
const recBtn = document.getElementById("recBtn");
const playBtn = document.getElementById("playBtn");
const stopBtn = document.getElementById("stopBtn");
const volUp = document.getElementById("volUp");
const volDown = document.getElementById("volDown");
const memoBtn = document.getElementById("memoBtn");
const memoPanel = document.getElementById("memoPanel");
const memoClose = document.getElementById("memoClose");
const memoList = document.getElementById("memoList");
const memoEmpty = document.getElementById("memoEmpty");
const faderL = document.getElementById("faderL");
const faderR = document.getElementById("faderR");
const toast = document.getElementById("toast");
const permissionBanner = document.getElementById("permissionBanner");
const grantPermissionBtn = document.getElementById("grantPermissionBtn");

// ---------- estado ----------
let mediaRecorder = null;
let analyser = null;
let audioCtx = null;
let chunks = [];
let recStart = 0;
let mode = "idle"; // idle | rec | play
let takes = []; // {id, name, blob, url, dur, date}
let currentTake = null;
let audio = new Audio();
let volume = 0.8;
audio.volume = volume;
let micPermissionGranted = false;

// giro del disco
let angle = 0;
let spinSpeed = 0; // grados por segundo
let lastTs = 0;

// scrub
let dragging = false;
let dragLastAngle = 0;
let wasPlayingBeforeDrag = false;

// ---------- utilidades ----------
const fmt = (s) => {
    s = Math.max(0, s);
    const h = Math.floor(s / 3600);
    const m = Math.floor((s % 3600) / 60);
    const sec = Math.floor(s % 60);
    return `${h}.${String(m).padStart(2, "0")}.${String(sec).padStart(2, "0")}`;
};

const fmtClock = (d) => d.toLocaleTimeString("es-ES", { hour: "2-digit", minute: "2-digit" });

let toastTimer;
const showToast = (msg) => {
    toast.textContent = msg;
    toast.classList.add("show");
    clearTimeout(toastTimer);
    toastTimer = setTimeout(() => toast.classList.remove("show"), 2600);
};

// ---------- permisos de micrófono ----------
const checkMicPermission = async () => {
    try {
        if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
            showToast("Tu navegador no soporta grabación de audio");
            return false;
        }
        
        const permission = await navigator.permissions.query({ name: 'microphone' });
        
        if (permission.state === 'granted') {
            micPermissionGranted = true;
            permissionBanner.classList.remove('show');
            return true;
        } else if (permission.state === 'prompt') {
            // El navegador preguntará cuando intentemos usar el micrófono
            return true;
        } else {
            // Denegado
            micPermissionGranted = false;
            permissionBanner.classList.add('show');
            return false;
        }
    } catch (err) {
        console.log("No se pudo verificar permisos:", err);
        // Algunos navegadores no soportan permissions.query
        return true; // Intentaremos pedir permisos al grabar
    }
};

const requestMicPermission = async () => {
    try {
        const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
        // Si llegamos aquí, tenemos permiso
        micPermissionGranted = true;
        permissionBanner.classList.remove('show');
        stream.getTracks().forEach(track => track.stop()); // Cerramos el stream de prueba
        showToast("✓ Micrófono permitido");
        return true;
    } catch (err) {
        console.error("Error al pedir permisos:", err);
        if (err.name === 'NotAllowedError' || err.name === 'PermissionDeniedError') {
            showToast("❌ Permiso de micrófono denegado");
        } else if (err.name === 'NotFoundError') {
            showToast("❌ No se encontró micrófono");
        } else if (err.name === 'SecurityError') {
            showToast("❌ Necesitas HTTPS o localhost para usar el micrófono");
            showLocalhostInstructions();
        } else {
            showToast("❌ Error al acceder al micrófono");
        }
        return false;
    }
};

const showLocalhostInstructions = () => {
    const instructions = `
Para usar el micrófono, necesitas ejecutar esta app desde un servidor local:

1. Abre una terminal en la carpeta donde guardaste este archivo
2. Ejecuta: python3 -m http.server 8000
3. Abre en tu navegador: http://localhost:8000

O usa una extensión del navegador que permita file:// con permisos especiales.
    `;
    console.log(instructions);
    showToast("Abre la consola (F12) para ver instrucciones");
};

grantPermissionBtn.addEventListener("click", async () => {
    await requestMicPermission();
});

// ---------- persistencia (IndexedDB) ----------
const DB_NAME = "av7";
const STORE = "takes";
let db = null;

const openDB = () => new Promise((resolve) => {
    const req = indexedDB.open(DB_NAME, 1);
    req.onupgradeneeded = () => req.result.createObjectStore(STORE, { keyPath: "id" });
    req.onsuccess = () => resolve(req.result);
    req.onerror = () => resolve(null);
});

const dbPut = (take) => {
    if (!db) return;
    const { url, ...rec } = take;
    db.transaction(STORE, "readwrite").objectStore(STORE).put(rec);
};

const dbDelete = (id) => {
    if (!db) return;
    db.transaction(STORE, "readwrite").objectStore(STORE).delete(id);
};

const dbLoadAll = () => new Promise((resolve) => {
    if (!db) return resolve([]);
    const req = db.transaction(STORE, "readonly").objectStore(STORE).getAll();
    req.onsuccess = () => resolve(req.result || []);
    req.onerror = () => resolve([]);
});

// ---------- LCD ----------
const updateTakeCounter = () => {
    lcdTake.textContent = String(takes.length).padStart(2, "0");
};

const meterLoop = () => {
    if (mode === "rec" && analyser) {
        const data = new Uint8Array(analyser.frequencyBinCount);
        analyser.getByteTimeDomainData(data);
        let peak = 0;
        for (let i = 0; i < data.length; i++) {
            peak = Math.max(peak, Math.abs(data[i] - 128));
        }
        lcdMeter.style.width = `${Math.min(100, (peak / 128) * 160)}%`;
    } else if (mode === "play") {
        lcdMeter.style.width = `${40 + Math.random() * 30}%`;
    } else {
        lcdMeter.style.width = "0%";
    }
};

// ---------- bucle de animación ----------
const tick = (ts) => {
    const dt = lastTs ? (ts - lastTs) / 1000 : 0;
    lastTs = ts;
    
    if (!dragging) {
        angle = (angle + spinSpeed * dt) % 360;
        disc.style.transform = `rotate(${angle}deg)`;
    }
    
    if (mode === "rec") {
        lcdTime.textContent = fmt((performance.now() - recStart) / 1000);
    } else if (mode === "play" && !audio.paused) {
        lcdTime.textContent = fmt(audio.currentTime);
    }
    
    meterLoop();
    requestAnimationFrame(tick);
};
requestAnimationFrame(tick);

// ---------- grabación ----------
const startRec = async () => {
    if (mode === "rec") return;
    
    // Verificar permisos antes de grabar
    if (!micPermissionGranted) {
        const granted = await requestMicPermission();
        if (!granted) {
            permissionBanner.classList.add('show');
            return;
        }
    }
    
    stopPlayback();
    let stream;
    try {
        stream = await navigator.mediaDevices.getUserMedia({ audio: true });
    } catch (err) {
        console.error("Error al obtener micrófono:", err);
        if (err.name === 'NotAllowedError' || err.name === 'PermissionDeniedError') {
            showToast("Permiso de micrófono denegado");
            permissionBanner.classList.add('show');
        } else if (err.name === 'SecurityError') {
            showToast("Necesitas HTTPS o localhost");
            showLocalhostInstructions();
        } else {
            showToast("Error al acceder al micrófono");
        }
        return;
    }
    
    audioCtx = audioCtx || new (window.AudioContext || window.webkitAudioContext)();
    if (audioCtx.state === "suspended") audioCtx.resume();
    
    const src = audioCtx.createMediaStreamSource(stream);
    analyser = audioCtx.createAnalyser();
    analyser.fftSize = 512;
    src.connect(analyser);
    
    chunks = [];
    const rec = new MediaRecorder(stream);
    mediaRecorder = rec;
    
    rec.ondataavailable = (e) => e.data.size && chunks.push(e.data);
    rec.onstop = () => {
        stream.getTracks().forEach((t) => t.stop());
        const blob = new Blob(chunks, { type: rec.mimeType || "audio/webm" });
        const dur = (performance.now() - recStart) / 1000;
        if (dur < 0.3) return;
        
        const now = new Date();
        const take = {
            id: Date.now(),
            name: `memo ${String(takes.length + 1).padStart(2, "0")}`,
            blob,
            url: URL.createObjectURL(blob),
            dur,
            date: now.toISOString(),
        };
        takes.push(take);
        currentTake = take;
        dbPut(take);
        updateTakeCounter();
        renderMemos();
        showToast(`${take.name} guardado · ${fmt(dur)}`);
    };
    
    rec.start();
    recStart = performance.now();
    mode = "rec";
    spinSpeed = 120;
    recBtn.classList.add("active");
};

const stopRec = () => {
    if (mediaRecorder && mediaRecorder.state !== "inactive") mediaRecorder.stop();
    mediaRecorder = null;
    analyser = null;
    mode = "idle";
    spinSpeed = 0;
    recBtn.classList.remove("active");
    lcdTime.textContent = "0.00.00";
};

// ---------- reproducción ----------
const playTake = (take) => {
    if (!take) {
        showToast("Nada que reproducir — graba un memo primero");
        return;
    }
    stopRec();
    currentTake = take;
    if (!take.url) take.url = URL.createObjectURL(take.blob);
    
    audio.src = take.url;
    audio.volume = volume;
    audio.play().then(() => {
        mode = "play";
        spinSpeed = 90;
        playBtn.classList.add("active");
        renderMemos();
    }).catch(() => showToast("No se pudo reproducir"));
};

const stopPlayback = () => {
    audio.pause();
    audio.currentTime = 0;
    if (mode === "play") mode = "idle";
    spinSpeed = 0;
    playBtn.classList.remove("active");
    lcdTime.textContent = "0.00.00";
    renderMemos();
};

audio.addEventListener("ended", () => {
    mode = "idle";
    spinSpeed = 0;
    playBtn.classList.remove("active");
    lcdTime.textContent = "0.00.00";
    renderMemos();
});

// ---------- scrub con el disco ----------
const pointerAngle = (e) => {
    const r = disc.getBoundingClientRect();
    const cx = r.left + r.width / 2;
    const cy = r.top + r.height / 2;
    return (Math.atan2(e.clientY - cy, e.clientX - cx) * 180) / Math.PI;
};

disc.addEventListener("pointerdown", (e) => {
    if (mode === "rec") return;
    dragging = true;
    dragLastAngle = pointerAngle(e);
    wasPlayingBeforeDrag = mode === "play" && !audio.paused;
    if (wasPlayingBeforeDrag) audio.pause();
    disc.setPointerCapture(e.pointerId);
});

disc.addEventListener("pointermove", (e) => {
    if (!dragging) return;
    const a = pointerAngle(e);
    let delta = a - dragLastAngle;
    if (delta > 180) delta -= 360;
    if (delta < -180) delta += 360;
    dragLastAngle = a;
    angle = (angle + delta) % 360;
    disc.style.transform = `rotate(${angle}deg)`;
    
    if (currentTake && audio.src) {
        const t = Math.min(
            Math.max(0, audio.currentTime + (delta / 360) * 8),
            audio.duration || currentTake.dur
        );
        if (isFinite(t)) {
            audio.currentTime = t;
            lcdTime.textContent = fmt(t);
        }
    }
});

const endDrag = () => {
    if (!dragging) return;
    dragging = false;
    if (wasPlayingBeforeDrag) audio.play();
};

disc.addEventListener("pointerup", endDrag);
disc.addEventListener("pointercancel", endDrag);

// ---------- volumen ----------
const setVolume = (v) => {
    volume = Math.min(1, Math.max(0, v));
    audio.volume = volume;
    faderL.style.top = `${70 - volume * 55}%`;
    faderR.style.top = `${70 - volume * 55}%`;
    showToast(`volumen ${Math.round(volume * 100)}%`);
};

volUp.addEventListener("click", () => setVolume(volume + 0.1));
volDown.addEventListener("click", () => setVolume(volume - 0.1));

// ---------- lista de memos ----------
const renderMemos = () => {
    memoList.innerHTML = "";
    memoEmpty.style.display = takes.length ? "none" : "block";
    
    [...takes].reverse().forEach((take) => {
        const li = document.createElement("li");
        li.className = "memo-item";
        if (mode === "play" && currentTake === take && !audio.paused) {
            li.classList.add("playing");
        }
        
        const d = new Date(take.date);
        
        const play = document.createElement("button");
        play.className = "memo-play";
        play.textContent = "▶";
        play.setAttribute("aria-label", `Reproducir ${take.name}`);
        play.addEventListener("click", () => {
            closeMemos();
            playTake(take);
        });
        
        const info = document.createElement("div");
        info.className = "memo-info";
        const name = document.createElement("div");
        name.className = "memo-name";
        name.textContent = take.name;
        const meta = document.createElement("div");
        meta.className = "memo-meta";
        meta.textContent = `${fmt(take.dur)} · ${d.toLocaleDateString("es-ES")} ${fmtClock(d)}`;
        info.append(name, meta);
        
        const dl = document.createElement("a");
        dl.className = "memo-act";
        dl.textContent = "↓";
        dl.href = take.url || (take.url = URL.createObjectURL(take.blob));
        dl.download = `${take.name.replace(/\s+/g, "-")}.webm`;
        dl.setAttribute("aria-label", `Descargar ${take.name}`);
        
        const del = document.createElement("button");
        del.className = "memo-act";
        del.textContent = "✕";
        del.setAttribute("aria-label", `Borrar ${take.name}`);
        del.addEventListener("click", () => {
            if (currentTake === take) stopPlayback();
            takes = takes.filter((t) => t !== take);
            if (take.url) URL.revokeObjectURL(take.url);
            dbDelete(take.id);
            updateTakeCounter();
            renderMemos();
        });
        
        li.append(play, info, dl, del);
        memoList.append(li);
    });
};

const openMemos = () => {
    memoPanel.classList.add("open");
    memoPanel.setAttribute("aria-hidden", "false");
};

const closeMemos = () => {
    memoPanel.classList.remove("open");
    memoPanel.setAttribute("aria-hidden", "true");
};

memoBtn.addEventListener("click", openMemos);
memoClose.addEventListener("click", closeMemos);

// ---------- transporte ----------
recBtn.addEventListener("click", () => (mode === "rec" ? stopRec() : startRec()));

playBtn.addEventListener("click", () => {
    if (mode === "play" && !audio.paused) {
        audio.pause();
        spinSpeed = 0;
        playBtn.classList.remove("active");
    } else if (currentTake) {
        playTake(currentTake);
    } else {
        playTake(takes[takes.length - 1]);
    }
});

stopBtn.addEventListener("click", () => {
    stopRec();
    stopPlayback();
});

document.getElementById("pinDot").addEventListener("click", () => {
    if (mode === "rec") {
        showToast(`marca en ${fmt((performance.now() - recStart) / 1000)}`);
    }
});

// ---------- arranque ----------
(async () => {
    // Verificar permisos al cargar
    await checkMicPermission();
    
    db = await openDB();
    const saved = await dbLoadAll();
    takes = saved
        .sort((a, b) => a.id - b.id)
        .map((t) => ({ ...t, url: URL.createObjectURL(t.blob) }));
    if (takes.length) currentTake = takes[takes.length - 1];
    updateTakeCounter();
    renderMemos();
})();

// ---------- service worker ----------
if ("serviceWorker" in navigator && location.protocol === "https:") {
    navigator.serviceWorker.register("sw.js").catch(() => {});
}
})();
</script>
</body>
</html>
