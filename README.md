<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <title>⚗️ LAB DETEKTIF ELEKTROLIT</title>
  <link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@600;700;800&family=Nunito:wght@400;600;700;800;900&display=swap" rel="stylesheet">
  <style>
    /* ========== RESET & GLOBAL ========== */
    * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
    body {
      font-family: 'Nunito', sans-serif;
      background: linear-gradient(145deg, #fef9e8 0%, #f0f9ff 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding: 12px;
      color: #1e293b;
    }
    #app {
      width: 100%;
      max-width: 520px;
      background: rgba(255, 255, 255, 0.75);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border-radius: 42px;
      padding: 20px 16px 28px;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25), 0 0 0 1px rgba(255, 255, 255, 0.7), 0 8px 20px rgba(255, 215, 0, 0.2);
      transition: all 0.2s;
    }
    h1, h2, h3, h4, .font-baloo { font-family: 'Baloo 2', cursive; font-weight: 800; letter-spacing: -0.01em; }
    .gradient-text {
      background: linear-gradient(135deg, #f59e0b, #ec4899, #8b5cf6, #06b6d4);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    /* ========== KARTU ========== */
    .card {
      background: #ffffff;
      border-radius: 32px;
      padding: 20px 18px;
      margin-bottom: 18px;
      box-shadow: 0 10px 25px -8px rgba(0, 0, 0, 0.08), 0 4px 12px rgba(0, 0, 0, 0.02);
      border: 1px solid rgba(255, 255, 255, 0.8);
      transition: transform 0.1s;
    }
    .card-cyan { border-left: 8px solid #06b6d4; }
    .card-purple { border-left: 8px solid #a855f7; }
    .card-pink { border-left: 8px solid #ec4899; }
    .card-lime { border-left: 8px solid #84cc16; }
    .badge {
      display: inline-block;
      padding: 4px 14px;
      border-radius: 999px;
      font-size: 0.75rem;
      font-weight: 800;
      letter-spacing: 0.02em;
      text-transform: uppercase;
    }
    .badge-strong { background: #d1fae5; color: #065f46; }
    .badge-weak { background: #fef9c3; color: #854d0e; }
    .badge-non { background: #fee2e2; color: #991b1b; }
    /* ========== TOMBOL ========== */
    .btn {
      border: none;
      border-radius: 60px;
      padding: 16px 20px;
      font-weight: 800;
      font-family: 'Baloo 2', cursive;
      font-size: 1.1rem;
      cursor: pointer;
      transition: all 0.15s;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      box-shadow: 0 6px 0 rgba(0, 0, 0, 0.1);
      user-select: none;
      width: 100%;
    }
    .btn:active { transform: translateY(4px); box-shadow: 0 2px 0 rgba(0, 0, 0, 0.1); }
    .btn-primary { background: linear-gradient(135deg, #fbbf24, #f59e0b); color: #451a03; }
    .btn-success { background: linear-gradient(135deg, #4ade80, #22c55e); color: #052e16; }
    .btn-ghost { background: #fff; border: 2px solid #e2e8f0; color: #475569; box-shadow: 0 4px 0 #e2e8f0; }
    /* ========== TAB ========== */
    .tab-bar {
      display: flex;
      gap: 6px;
      margin-bottom: 14px;
      background: #f1f5f9;
      padding: 6px;
      border-radius: 999px;
    }
    .tab-btn {
      flex: 1;
      border: none;
      background: transparent;
      padding: 10px 4px;
      border-radius: 999px;
      font-weight: 800;
      font-family: 'Baloo 2', cursive;
      font-size: 0.9rem;
      color: #64748b;
      cursor: pointer;
      transition: all 0.15s;
    }
    .tab-btn.active { background: #ffffff; color: #0f172a; box-shadow: 0 4px 10px rgba(0,0,0,0.05); }
    .tab-panel { display: none; }
    .tab-panel.active { display: block; animation: fade 0.2s; }
    @keyframes fade { from { opacity: 0.3; } to { opacity: 1; } }
    /* ========== AVATAR ========== */
    .avatar-grid { display: flex; gap: 12px; justify-content: center; margin: 12px 0; }
    .avatar-option {
      border: 4px solid transparent;
      border-radius: 28px;
      padding: 8px;
      background: #f8fafc;
      cursor: pointer;
      transition: all 0.15s;
      text-align: center;
      flex: 1;
    }
    .avatar-option.selected {
      border-color: #ec4899;
      background: #fdf2f8;
      box-shadow: 0 8px 20px -6px rgba(236, 72, 153, 0.4);
      transform: scale(1.02);
    }
    .avatar-option svg { width: 70px; height: 70px; display: block; margin: 0 auto 4px; }
    .avatar-name { font-weight: 800; font-size: 0.8rem; color: #475569; }
    /* ========== CANVAS 3D ========== */
    #canvas-container {
      position: relative;
      width: 100%;
      aspect-ratio: 1 / 1;
      background: #d9f0ff;
      border-radius: 32px;
      overflow: hidden;
      margin-bottom: 12px;
      box-shadow: inset 0 0 0 2px rgba(255,255,255,0.6), 0 12px 28px -8px rgba(0,0,0,0.2);
    }
    #lab-canvas { display: block; width: 100%; height: 100%; touch-action: none; }
    /* ========== HUD ========== */
    .hud {
      position: absolute;
      top: 12px;
      right: 12px;
      background: rgba(255,255,255,0.9);
      backdrop-filter: blur(8px);
      border-radius: 28px;
      padding: 10px 14px;
      font-size: 0.75rem;
      font-weight: 800;
      color: #1e293b;
      display: flex;
      flex-direction: column;
      gap: 4px;
      box-shadow: 0 8px 20px -6px rgba(0,0,0,0.15);
      border: 1px solid rgba(255,255,255,0.8);
      pointer-events: none;
      min-width: 110px;
    }
    .hud span { display: flex; justify-content: space-between; gap: 10px; }
    .hud .sound-toggle {
      pointer-events: auto;
      background: #f1f5f9;
      border: none;
      border-radius: 20px;
      padding: 4px 8px;
      font-size: 1rem;
      cursor: pointer;
      width: 100%;
      text-align: center;
      margin-top: 2px;
    }
    /* ========== JOYSTICK ========== */
    #joystick-base {
      position: absolute;
      bottom: 20px;
      left: 20px;
      width: 96px;
      height: 96px;
      background: rgba(255,255,255,0.5);
      backdrop-filter: blur(6px);
      border-radius: 50%;
      border: 2px solid rgba(255,255,255,0.9);
      box-shadow: 0 8px 20px -4px rgba(0,0,0,0.1);
      touch-action: none;
      z-index: 5;
    }
    #joystick-knob {
      position: absolute;
      top: 50%; left: 50%;
      width: 44px; height: 44px;
      background: linear-gradient(135deg, #fbbf24, #f59e0b);
      border-radius: 50%;
      transform: translate(-50%, -50%);
      box-shadow: 0 6px 0 #b45309, 0 6px 12px rgba(0,0,0,0.2);
      pointer-events: none;
      transition: box-shadow 0.1s;
    }
    #joystick-base.active #joystick-knob { box-shadow: 0 2px 0 #b45309, 0 4px 8px rgba(0,0,0,0.2); }
    /* ========== TOMBOL UJI ========== */
    #test-btn {
      position: absolute;
      bottom: 24px;
      right: 20px;
      background: linear-gradient(135deg, #a855f7, #7c3aed);
      color: white;
      border: none;
      border-radius: 60px;
      padding: 14px 18px;
      font-weight: 800;
      font-family: 'Baloo 2', cursive;
      font-size: 0.9rem;
      box-shadow: 0 6px 0 #4c1d95, 0 10px 20px -6px rgba(124, 58, 237, 0.6);
      cursor: pointer;
      z-index: 6;
      display: none;
      align-items: center;
      gap: 6px;
      max-width: 200px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    #test-btn:active { transform: translateY(4px); box-shadow: 0 2px 0 #4c1d95; }
    /* ========== MODAL ========== */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.35);
      backdrop-filter: blur(6px);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 100;
      padding: 16px;
    }
    .modal-overlay.show { display: flex; }
    .modal-box {
      background: #ffffff;
      border-radius: 36px;
      padding: 24px 20px;
      width: 100%;
      max-width: 400px;
      box-shadow: 0 30px 60px -12px rgba(0,0,0,0.3);
      animation: pop 0.25s cubic-bezier(0.34, 1.56, 0.64, 1);
    }
    @keyframes pop { from { transform: scale(0.9); opacity: 0; } to { transform: scale(1); opacity: 1; } }
    .modal-box h3 { font-size: 1.3rem; margin-bottom: 8px; }
    .option-btn {
      display: block;
      width: 100%;
      text-align: left;
      padding: 14px 18px;
      border-radius: 24px;
      border: 2px solid #e2e8f0;
      background: #f8fafc;
      font-weight: 700;
      font-size: 0.95rem;
      margin-bottom: 8px;
      cursor: pointer;
      transition: all 0.1s;
      font-family: 'Nunito', sans-serif;
    }
    .option-btn:active { background: #f1f5f9; transform: scale(0.98); }
    .option-btn.correct { background: #d1fae5; border-color: #22c55e; }
    .option-btn.wrong { background: #fee2e2; border-color: #ef4444; }
    /* ========== PROGRESS ========== */
    .progress-bar {
      width: 100%;
      height: 12px;
      background: #e2e8f0;
      border-radius: 999px;
      overflow: hidden;
      margin: 12px 0;
    }
    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #fbbf24, #ec4899, #8b5cf6);
      border-radius: 999px;
      transition: width 0.4s ease;
      width: 0%;
    }
    /* ========== SERTIFIKAT ========== */
    .cert-container {
      border: 6px solid;
      border-image: linear-gradient(135deg, #fbbf24, #ec4899, #8b5cf6, #06b6d4) 1;
      border-radius: 24px;
      padding: 22px 16px;
      background: #fffdf5;
      text-align: center;
      margin-bottom: 16px;
    }
    .cert-score strong { font-size: 2rem; font-weight: 900; }
    /* ========== UTIL ========== */
    .flex-row { display: flex; gap: 10px; align-items: center; }
    .text-center { text-align: center; }
    .mt-2 { margin-top: 8px; }
    .mb-2 { margin-bottom: 8px; }
    .hidden { display: none !important; }
    /* ========== SCREEN ========== */
    .screen { display: none; }
    .screen.active { display: block; animation: slideUp 0.3s ease; }
    @keyframes slideUp { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }
    /* Small scroll fix */
    .scrollable { max-height: 70vh; overflow-y: auto; padding-right: 4px; }
    .scrollable::-webkit-scrollbar { width: 4px; }
    .scrollable::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 10px; }
  </style>
</head>
<body>
<div id="app">

  <!-- ==================== LAYAR 1: HALAMAN AWAL ==================== -->
  <div id="screen-home" class="screen active">
    <div class="text-center" style="margin-bottom:18px;">
      <div style="font-size:3.2rem; line-height:1;">⚗️</div>
      <h1 class="gradient-text" style="font-size:2rem; margin-top:4px;">LAB DETEKTIF ELEKTROLIT</h1>
      <p style="font-weight:700; color:#64748b; font-size:0.85rem;">Petualangan Virtual ala Roblox · Kimia Kelas X</p>
    </div>

    <!-- Tujuan -->
    <div class="card card-cyan">
      <h3 style="font-size:1.15rem; margin-bottom:6px;">🎯 Tujuan Pembelajaran</h3>
      <p style="font-size:0.9rem; font-weight:600; color:#334155;">Murid mampu <strong>mengklasifikasikan</strong> dan <strong>membedakan</strong> larutan elektrolit dan non-elektrolit berdasarkan daya hantar listriknya.</p>
    </div>

    <!-- Teori 3 Tab -->
    <div class="card card-purple">
      <h3 style="font-size:1.15rem; margin-bottom:10px;">📚 Teori Dasar & Contoh Larutan</h3>
      <div class="tab-bar">
        <button class="tab-btn active" data-tab="tab-kuat">⚡ Kuat</button>
        <button class="tab-btn" data-tab="tab-lemah">💧 Lemah</button>
        <button class="tab-btn" data-tab="tab-non">🚫 Non</button>
      </div>
      <div id="tab-kuat" class="tab-panel active">
        <div class="flex-row mb-2"><span class="badge badge-strong">α = 1</span><span style="font-weight:700; font-size:0.8rem;">Terionisasi sempurna</span></div>
        <p style="font-size:0.85rem; font-weight:600; color:#334155;">Lampu menyala <strong>TERANG</strong>, gelembung gas <strong>banyak</strong>.</p>
        <div style="margin-top:10px; display:flex; flex-direction:column; gap:6px;">
          <div style="background:#f0fdf4; padding:8px 12px; border-radius:16px;"><strong>HCl</strong> — Asam Klorida</div>
          <div style="background:#f0fdf4; padding:8px 12px; border-radius:16px;"><strong>NaOH</strong> — Natrium Hidroksida</div>
          <div style="background:#f0fdf4; padding:8px 12px; border-radius:16px;"><strong>NaCl</strong> — Garam Dapur</div>
          <div style="background:#f0fdf4; padding:8px 12px; border-radius:16px;"><strong>H₂SO₄</strong> — Asam Sulfat</div>
          <div style="background:#f0fdf4; padding:8px 12px; border-radius:16px;"><strong>KOH</strong> — Kalium Hidroksida</div>
        </div>
      </div>
      <div id="tab-lemah" class="tab-panel">
        <div class="flex-row mb-2"><span class="badge badge-weak">0 &lt; α &lt; 1</span><span style="font-weight:700; font-size:0.8rem;">Terionisasi sebagian</span></div>
        <p style="font-size:0.85rem; font-weight:600; color:#334155;">Lampu menyala <strong>REDUP</strong>, gelembung gas <strong>sedikit</strong>.</p>
        <div style="margin-top:10px; display:flex; flex-direction:column; gap:6px;">
          <div style="background:#fefce8; padding:8px 12px; border-radius:16px;"><strong>CH₃COOH</strong> — Asam Cuka</div>
          <div style="background:#fefce8; padding:8px 12px; border-radius:16px;"><strong>NH₃</strong> — Amonia</div>
          <div style="background:#fefce8; padding:8px 12px; border-radius:16px;"><strong>H₂CO₃</strong> — Asam Karbonat</div>
          <div style="background:#fefce8; padding:8px 12px; border-radius:16px;"><strong>Al(OH)₃</strong> — Aluminium Hidroksida</div>
          <div style="background:#fefce8; padding:8px 12px; border-radius:16px;"><strong>C₆H₈O₇</strong> — Asam Sitrat</div>
        </div>
      </div>
      <div id="tab-non" class="tab-panel">
        <div class="flex-row mb-2"><span class="badge badge-non">α = 0</span><span style="font-weight:700; font-size:0.8rem;">Tidak terionisasi</span></div>
        <p style="font-size:0.85rem; font-weight:600; color:#334155;">Lampu <strong>MATI</strong>, tidak ada gelembung. Molekul netral.</p>
        <div style="margin-top:10px; display:flex; flex-direction:column; gap:6px;">
          <div style="background:#fef2f2; padding:8px 12px; border-radius:16px;"><strong>C₆H₁₂O₆</strong> — Glukosa</div>
          <div style="background:#fef2f2; padding:8px 12px; border-radius:16px;"><strong>CO(NH₂)₂</strong> — Urea</div>
          <div style="background:#fef2f2; padding:8px 12px; border-radius:16px;"><strong>C₂H₅OH</strong> — Etanol</div>
          <div style="background:#fef2f2; padding:8px 12px; border-radius:16px;"><strong>C₁₂H₂₂O₁₁</strong> — Sukrosa</div>
          <div style="background:#fef2f2; padding:8px 12px; border-radius:16px;"><strong>C₃H₈O₃</strong> — Gliserol</div>
        </div>
      </div>
      <p style="font-size:0.75rem; font-weight:700; color:#64748b; margin-top:12px; text-align:center;">Derajat ionisasi: α = mol terionisasi / mol mula-mula</p>
    </div>

    <!-- Petunjuk -->
    <div class="card card-pink">
      <h3 style="font-size:1.15rem; margin-bottom:8px;">📖 Petunjuk Bermain</h3>
      <ol style="font-size:0.85rem; font-weight:600; color:#334155; padding-left:18px; display:flex; flex-direction:column; gap:6px;">
        <li>Isi nama detektif & pilih avatar</li>
        <li>Jelajahi laboratorium 3D dengan joystick / tap</li>
        <li>Dekati gelas kimia & tekan tombol <strong>🔬 Uji</strong></li>
        <li>Amati nyala lampu & gelembung gas</li>
        <li>Jawab klasifikasi larutan (Kuat / Lemah / Non)</li>
        <li>Jawaban benar +10, salah −5 (boleh ulang)</li>
        <li>Setelah 10 gelas, jawab 6 soal berpikir kritis</li>
      </ol>
    </div>

    <!-- Data Detektif -->
    <div class="card card-lime">
      <h3 style="font-size:1.15rem; margin-bottom:8px;">👤 Data Detektif</h3>
      <input id="player-name" type="text" placeholder="Nama lengkap (min. 2 huruf)" maxlength="30"
        style="width:100%; padding:14px 18px; border-radius:60px; border:2px solid #e2e8f0; font-weight:700; font-size:0.95rem; outline:none; transition:0.15s; font-family:'Nunito',sans-serif;"
        onfocus="this.style.borderColor='#84cc16'" onblur="this.style.borderColor='#e2e8f0'">
      <p id="name-warning" style="color:#ef4444; font-size:0.75rem; font-weight:700; margin-top:4px; display:none;">Minimal 2 karakter ya!</p>
      <div class="avatar-grid" id="avatar-grid">
        <div class="avatar-option selected" data-avatar="putri">
          <svg viewBox="0 0 100 100" fill="none">
            <circle cx="50" cy="38" r="20" fill="#fcd34d"/>
            <path d="M30 20 Q50 5 70 20 Q75 40 68 55 Q50 65 32 55 Q25 40 30 20Z" fill="#4b2e1e"/>
            <rect x="35" y="52" width="30" height="30" rx="4" fill="#ffffff" stroke="#cbd5e1" stroke-width="1.5"/>
            <rect x="42" y="58" width="16" height="10" rx="2" fill="#f9a8d4"/>
            <circle cx="43" cy="36" r="2.5" fill="#1e293b"/><circle cx="57" cy="36" r="2.5" fill="#1e293b"/>
            <path d="M45 46 Q50 50 55 46" stroke="#1e293b" stroke-width="1.5" fill="none" stroke-linecap="round"/>
          </svg>
          <div class="avatar-name">Detektif Putri</div>
        </div>
        <div class="avatar-option" data-avatar="putra">
          <svg viewBox="0 0 100 100" fill="none">
            <circle cx="50" cy="38" r="20" fill="#fcd34d"/>
            <path d="M32 18 Q50 8 68 18 Q72 30 68 36 Q50 28 32 36 Q28 30 32 18Z" fill="#2d1b0e"/>
            <rect x="35" y="52" width="30" height="30" rx="4" fill="#ffffff" stroke="#cbd5e1" stroke-width="1.5"/>
            <rect x="42" y="58" width="16" height="10" rx="2" fill="#f9a8d4"/>
            <circle cx="43" cy="36" r="2.5" fill="#1e293b"/><circle cx="57" cy="36" r="2.5" fill="#1e293b"/>
            <path d="M45 46 Q50 50 55 46" stroke="#1e293b" stroke-width="1.5" fill="none" stroke-linecap="round"/>
          </svg>
          <div class="avatar-name">Detektif Putra</div>
        </div>
      </div>
    </div>

    <button class="btn btn-primary" id="btn-start" style="font-size:1.3rem; padding:18px;">🚀 MULAI PENJELAJAHAN</button>
  </div>

  <!-- ==================== LAYAR 2: LAB 3D ==================== -->
  <div id="screen-lab" class="screen">
    <div id="canvas-container">
      <canvas id="lab-canvas"></canvas>
      <!-- HUD -->
      <div class="hud" id="hud">
        <span>👤 <span id="hud-name">Detektif</span></span>
        <span>⭐ <span id="hud-poin">0</span></span>
        <span>🧪 <span id="hud-progress">0/10</span></span>
        <button class="sound-toggle" id="sound-toggle">🔊</button>
      </div>
      <!-- Joystick -->
      <div id="joystick-base"><div id="joystick-knob"></div></div>
      <!-- Tombol Uji -->
      <button id="test-btn">🔬 Uji</button>
    </div>
    <p style="text-align:center; font-size:0.8rem; font-weight:700; color:#64748b;">Geser joystick · Tap gelas untuk jalan otomatis · WASD/Arrow</p>
  </div>

  <!-- ==================== LAYAR 3: SOAL KRITIS ==================== -->
  <div id="screen-critical" class="screen">
    <h2 class="gradient-text" style="font-size:1.6rem; text-align:center; margin-bottom:6px;">🧠 SOAL BERPIKIR KRITIS</h2>
    <div class="progress-bar"><div class="progress-fill" id="critical-progress" style="width:0%"></div></div>
    <p style="text-align:center; font-weight:700; font-size:0.85rem; color:#64748b;" id="critical-counter">Soal 1 dari 6</p>
    <div id="critical-question-box" class="card" style="border-left:8px solid #f59e0b;">
      <p id="critical-question-text" style="font-weight:700; font-size:0.95rem; margin-bottom:12px;">Memuat soal...</p>
      <div id="critical-options"></div>
    </div>
    <div id="critical-feedback" class="card" style="display:none; border-left:8px solid #22c55e;">
      <p id="critical-feedback-text" style="font-weight:700; font-size:0.9rem;"></p>
    </div>
    <button class="btn btn-success" id="btn-next-critical" style="display:none;">➡️ SOAL BERIKUTNYA</button>
  </div>

  <!-- ==================== LAYAR 4: SERTIFIKAT ==================== -->
  <div id="screen-cert" class="screen">
    <div class="cert-container" id="certificate">
      <div style="font-size:3rem;">🏅</div>
      <h3 style="font-size:0.95rem; font-weight:800; color:#475569; letter-spacing:0.08em;">SMA SANTO PAULUS PONTIANAK</h3>
      <h1 class="gradient-text" style="font-size:2.4rem; margin:4px 0;">SERTIFIKAT</h1>
      <p style="font-size:0.75rem; font-weight:800; color:#64748b; letter-spacing:0.1em;">PENGHARGAAN PENYELESAIAN GAMIFIKASI KIMIA</p>
      <p style="font-size:0.85rem; font-weight:600; margin-top:12px;">Diberikan dengan bangga kepada</p>
      <p id="cert-name" style="font-size:1.4rem; font-weight:900; border-bottom:2px dashed #ec4899; display:inline-block; padding:0 12px 4px; margin:8px 0;">Nama Siswa</p>
      <p style="font-size:0.8rem; font-weight:600; color:#475569; margin:12px 0;">Telah menyelesaikan gamifikasi pembelajaran kimia tentang klasifikasi larutan elektrolit dan non-elektrolit dengan sangat baik.</p>
      <div style="display:flex; gap:12px; justify-content:center; margin:16px 0;">
        <div style="background:#f0f9ff; border-radius:20px; padding:10px 20px;">
          <p style="font-size:0.7rem; font-weight:800; color:#0891b2;">NILAI</p>
          <p class="cert-score" style="font-size:1.8rem; font-weight:900; color:#0891b2;" id="cert-score">0</p>
        </div>
        <div style="background:#fdf2f8; border-radius:20px; padding:10px 20px;">
          <p style="font-size:0.7rem; font-weight:800; color:#db2777;">PREDIKAT</p>
          <p class="cert-score" style="font-size:1.8rem; font-weight:900; color:#db2777;" id="cert-grade">-</p>
        </div>
      </div>
      <p style="font-size:0.8rem; font-weight:700; margin-top:12px;">GURU KIMIA — Agustinus Ridwan, S.Pd.</p>
      <p style="font-size:0.75rem; font-weight:600; color:#64748b;">Pontianak, <span id="cert-date"></span></p>
    </div>
    <button class="btn btn-success" id="btn-download-pdf" style="margin-bottom:10px;">⬇️ UNDUH SERTIFIKAT PDF</button>
    <button class="btn btn-ghost" id="btn-restart">🔄 MAIN LAGI DARI AWAL</button>
  </div>

</div>

<!-- ==================== MODAL ==================== -->
<div class="modal-overlay" id="modal-overlay">
  <div class="modal-box" id="modal-box"></div>
</div>

<!-- ==================== LIBRARY CDN ==================== -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<script>
/* ================================================================
   SOUND SYSTEM (Web Audio API)
   ================================================================ */
const Sound = {
  ctx: null, enabled: true, bgInterval: null,
  init() { if (!this.ctx) { try { this.ctx = new (window.AudioContext || window.webkitAudioContext)(); } catch(e){} } },
  tone(freq, dur=0.15, type='sine', vol=0.2, delay=0) {
    if (!this.ctx || !this.enabled) return;
    const t = this.ctx.currentTime + delay;
    const o = this.ctx.createOscillator();
    const g = this.ctx.createGain();
    o.type = type; o.frequency.value = freq;
    g.gain.setValueAtTime(0.001, t);
    g.gain.exponentialRampToValueAtTime(vol, t + 0.02);
    g.gain.exponentialRampToValueAtTime(0.001, t + dur);
    o.connect(g); g.connect(this.ctx.destination);
    o.start(t); o
