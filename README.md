<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>FootGuard</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<style>
:root {
  --mint:#00C9A7; --mint-l:#E6FAF6; --mint-m:#00a88c;
  --navy:#0F2744; --navy-m:#1B3E6F; --navy-l:#243d5c;
  --slate:#4A6080; --smoke:#F4F7FB; --bdr:#E2EAF4;
  --warn:#FF8C42; --danger:#E63946; --safe:#52B788; --yellow:#FFD166;
  --sh:0 2px 18px rgba(15,39,68,.10);
  --sh2:0 8px 32px rgba(15,39,68,.16);
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;font-family:'DM Sans',sans-serif;background:#B8C8DF;overscroll-behavior:none;}

/* WRAPPER */
.wrap{min-height:100vh;min-height:100dvh;display:flex;justify-content:center;align-items:flex-start;padding:20px 10px 36px;}
@media(max-width:500px){
  .wrap{padding:0;background:#0F2744;}
  .phone{border-radius:0!important;box-shadow:none!important;width:100vw!important;min-height:100vh;min-height:100dvh;}
}

/* PHONE SHELL */
.phone{width:375px;background:#F4F7FB;border-radius:44px;
  box-shadow:0 32px 80px rgba(15,39,68,.35),0 0 0 3px #C8D8EE,inset 0 0 0 1px rgba(255,255,255,.6);
  overflow:hidden;display:flex;flex-direction:column;position:relative;min-height:780px;}

/* SCREENS */
.scr{display:none;flex-direction:column;flex:1;overflow:hidden;}
.scr.on{display:flex;}
.scroll{flex:1;overflow-y:auto;overflow-x:hidden;-webkit-overflow-scrolling:touch;}
.scroll::-webkit-scrollbar{width:3px;}
.scroll::-webkit-scrollbar-thumb{background:var(--bdr);border-radius:2px;}
.pad{padding:16px;}

/* HEADER */
.hdr{background:linear-gradient(135deg,var(--navy),var(--navy-m));padding:16px 18px 20px;flex-shrink:0;position:relative;overflow:hidden;}
.hdr::after{content:'';position:absolute;top:-30px;right:-30px;width:120px;height:120px;background:radial-gradient(circle,rgba(0,201,167,.2),transparent 70%);}
.hdr-t{color:#fff;font-family:'DM Serif Display',serif;font-size:1rem;font-weight:700;}
.hdr-s{color:rgba(255,255,255,.5);font-size:.68rem;margin-top:2px;}
.shdr{background:var(--navy);padding:13px 16px;display:flex;align-items:center;gap:10px;flex-shrink:0;}
.shdr-bk{color:#fff;font-size:1.4rem;cursor:pointer;line-height:1;}
.shdr-t{color:#fff;font-family:'DM Serif Display',serif;font-size:.9rem;font-weight:700;flex:1;}

/* CARDS */
.card{background:#fff;border-radius:16px;padding:16px;box-shadow:var(--sh);margin-bottom:12px;}
.card-t{font-family:'DM Serif Display',serif;font-size:.78rem;font-weight:700;color:var(--navy);margin-bottom:12px;display:flex;justify-content:space-between;align-items:center;}

/* BUTTONS */
.btn{width:100%;background:var(--mint);color:var(--navy);border:none;border-radius:13px;padding:13px;font-size:.86rem;font-weight:700;font-family:'DM Sans',sans-serif;cursor:pointer;transition:transform .12s,opacity .12s;}
.btn:active{transform:scale(.97);opacity:.9;}
.btn:disabled{opacity:.5;cursor:not-allowed;transform:none;}
.btn-out{background:transparent;border:2px solid var(--mint);color:var(--mint);}
.btn-ghost{background:var(--smoke);color:var(--slate);border:none;}
.btn-danger{background:var(--danger);color:#fff;}
.btn-sm{padding:8px 14px;font-size:.72rem;width:auto;border-radius:9px;}

/* FORM */
.inp-wrap{margin-bottom:10px;}
.inp-lbl{font-size:.68rem;font-weight:600;color:var(--slate);margin-bottom:4px;display:block;}
.inp{width:100%;background:var(--smoke);border:1.5px solid var(--bdr);border-radius:10px;padding:10px 12px;font-size:.82rem;font-family:'DM Sans',sans-serif;color:var(--navy);outline:none;transition:border-color .2s;}
.inp:focus{border-color:var(--mint);background:#fff;}
.inp.err{border-color:var(--danger);}
.err-msg{color:var(--danger);font-size:.63rem;margin-top:3px;}

/* ══════════════════════
   SCREEN: ROLE SELECT
══════════════════════ */
#scr-role .login-bg{flex:1;background:linear-gradient(160deg,var(--navy) 0%,var(--navy-m) 55%,#1a5276 100%);display:flex;flex-direction:column;padding:24px 20px 30px;overflow-y:auto;}
.logo-row{display:flex;align-items:center;gap:10px;margin-bottom:8px;}
.logo-box{width:44px;height:44px;border-radius:12px;overflow:hidden;display:flex;align-items:center;justify-content:center;background:var(--navy);}
.logo-name{color:#fff;font-family:'DM Serif Display',serif;font-weight:800;font-size:1.1rem;}
.logo-sub{color:var(--mint);font-size:.58rem;font-weight:600;text-transform:uppercase;letter-spacing:.08em;}
.hero{text-align:center;margin:20px 0 24px;}
.hero h2{color:#fff;font-family:'DM Serif Display',serif;font-size:1.4rem;font-weight:800;line-height:1.3;}
.hero p{color:rgba(255,255,255,.55);font-size:.76rem;margin-top:6px;line-height:1.6;}
.role-row{display:flex;gap:10px;margin-bottom:20px;}
.role-c{flex:1;border:2px solid rgba(255,255,255,.18);border-radius:16px;padding:16px 10px;text-align:center;cursor:pointer;transition:all .22s;background:rgba(255,255,255,.07);}
.role-c:active,.role-c.sel{border-color:var(--mint);background:rgba(0,201,167,.18);}
.role-icon{font-size:2rem;margin-bottom:7px;}
.role-t{color:#fff;font-family:'DM Serif Display',serif;font-size:.82rem;font-weight:700;}
.role-s{color:rgba(255,255,255,.45);font-size:.63rem;margin-top:3px;line-height:1.4;}
.glass{background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.18);border-radius:16px;padding:16px;margin-bottom:12px;}
.glass-t{color:rgba(255,255,255,.5);font-size:.64rem;font-weight:700;text-transform:uppercase;letter-spacing:.07em;margin-bottom:12px;}
.oinp{background:rgba(255,255,255,.13);border:1.5px solid rgba(255,255,255,.22);border-radius:10px;padding:10px 12px;color:#fff;font-size:.82rem;font-family:'DM Sans',sans-serif;width:100%;margin-bottom:8px;outline:none;transition:border-color .2s;}
.oinp:focus{border-color:var(--mint);}
.oinp::placeholder{color:rgba(255,255,255,.35);}
.oinp.err{border-color:var(--danger);}
.oerr{color:#ff8a8a;font-size:.63rem;margin:-4px 0 8px 2px;}
.toggle-row{text-align:center;margin-top:12px;}
.toggle-row span{color:rgba(255,255,255,.45);font-size:.72rem;}
.toggle-row a{color:var(--mint);font-size:.72rem;font-weight:600;cursor:pointer;text-decoration:none;}

/* ══════════════════════
   SCREEN: PATIENT HOME
══════════════════════ */
.phdr{background:linear-gradient(135deg,var(--navy),var(--navy-m));padding:16px 18px 20px;flex-shrink:0;position:relative;overflow:hidden;}
.phdr::after{content:'';position:absolute;bottom:-20px;right:-20px;width:100px;height:100px;background:radial-gradient(circle,rgba(0,201,167,.2),transparent 70%);}
.greet{color:rgba(255,255,255,.55);font-size:.72rem;}
.pname{color:#fff;font-family:'DM Serif Display',serif;font-size:1.05rem;font-weight:700;margin-top:2px;}

/* PATIENT CODE BADGE */
.code-badge{background:rgba(0,201,167,.15);border:1.5px solid rgba(0,201,167,.4);border-radius:10px;padding:8px 12px;margin-top:10px;display:flex;align-items:center;justify-content:space-between;}
.code-lbl{color:rgba(255,255,255,.5);font-size:.6rem;font-weight:700;text-transform:uppercase;letter-spacing:.07em;}
.code-val{color:var(--mint);font-family:'DM Serif Display',serif;font-size:1.1rem;font-weight:800;letter-spacing:.08em;}
.code-copy{color:rgba(255,255,255,.4);font-size:.7rem;cursor:pointer;padding:3px 7px;border-radius:6px;border:1px solid rgba(255,255,255,.15);background:rgba(255,255,255,.07);}
.code-copy:active{background:rgba(255,255,255,.15);}

/* CTA */
.cta{background:linear-gradient(135deg,var(--mint),var(--mint-m));border-radius:14px;padding:16px;display:flex;align-items:center;gap:12px;cursor:pointer;box-shadow:0 4px 18px rgba(0,201,167,.28);transition:transform .15s;margin-bottom:12px;}
.cta:active{transform:scale(.98);}
.cta .ci{font-size:1.9rem;}
.cta .ct .t{color:#fff;font-family:'DM Serif Display',serif;font-size:.9rem;font-weight:700;}
.cta .ct .s{color:rgba(255,255,255,.75);font-size:.68rem;margin-top:2px;}
.cta .ca{margin-left:auto;color:#fff;font-size:1.2rem;}

/* HISTORY ROW */
.hist-item{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid var(--bdr);}
.hist-item:last-child{border-bottom:none;}
.hist-dot{width:9px;height:9px;border-radius:50%;flex-shrink:0;}
.hist-dot.ok{background:var(--safe);}
.hist-dot.warn{background:var(--warn);}
.hist-date{font-size:.72rem;color:var(--navy);font-weight:600;flex:1;}
.hist-status{font-size:.65rem;color:var(--slate);}
.hist-empty{text-align:center;padding:16px 0;color:var(--slate);font-size:.76rem;}

/* ══════════════════════
   SCREEN: LOG CHECK
══════════════════════ */
.step-bar{display:flex;gap:4px;padding:12px 16px;background:#fff;flex-shrink:0;border-bottom:1px solid var(--bdr);}
.step-dot{flex:1;height:4px;border-radius:2px;background:var(--bdr);transition:background .3s;}
.step-dot.done{background:var(--mint);}
.step-dot.active{background:var(--mint);opacity:.5;}
.step-panel{display:none;}
.step-panel.on{display:block;}
.step-t{font-family:'DM Serif Display',serif;font-size:.88rem;font-weight:700;color:var(--navy);margin-bottom:4px;}
.step-s{font-size:.72rem;color:var(--slate);margin-bottom:14px;line-height:1.5;}

/* SCORE SLIDER */
.score-row{display:flex;align-items:center;gap:10px;margin-bottom:12px;}
.score-lbl{font-size:.72rem;color:var(--slate);font-weight:500;min-width:70px;}
.score-val{font-family:'DM Serif Display',serif;font-size:1rem;font-weight:700;color:var(--navy);min-width:20px;text-align:right;}
input[type=range]{flex:1;accent-color:var(--mint);}

/* SYMPTOMS */
.sym-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:12px;}
.sym-b{background:#fff;border:2px solid var(--bdr);border-radius:10px;padding:9px 7px;text-align:center;cursor:pointer;transition:all .18s;}
.sym-b.sel{border-color:var(--mint);background:var(--mint-l);}
.sym-b:active{transform:scale(.95);}
.sym-icon{font-size:1.2rem;margin-bottom:3px;}
.sym-t{font-size:.65rem;font-weight:600;color:var(--navy);}

/* PHOTO UPLOAD */
.photo-area{border:2px dashed var(--bdr);border-radius:12px;padding:20px;text-align:center;cursor:pointer;transition:border-color .2s;margin-bottom:10px;}
.photo-area:hover{border-color:var(--mint);}
.photo-area input{display:none;}
.photo-preview{display:flex;flex-wrap:wrap;gap:6px;margin-top:8px;}
.photo-thumb{width:60px;height:60px;border-radius:8px;object-fit:cover;border:2px solid var(--bdr);}

/* ══════════════════════
   SCREEN: DOCTOR
══════════════════════ */
.dhdr{background:linear-gradient(135deg,#1B3E6F,#0F2744);padding:16px 18px 20px;flex-shrink:0;position:relative;overflow:hidden;}
.dhdr::after{content:'';position:absolute;top:-20px;right:-20px;width:100px;height:100px;background:radial-gradient(circle,rgba(255,141,66,.2),transparent 70%);}
.d-name{color:#fff;font-family:'DM Serif Display',serif;font-size:1.05rem;font-weight:700;margin-top:2px;}
.d-role{color:var(--warn);font-size:.65rem;font-weight:700;text-transform:uppercase;letter-spacing:.07em;}

/* LOOKUP */
.lookup-box{background:#fff;border-radius:16px;padding:16px;box-shadow:var(--sh);margin-bottom:12px;}
.lookup-row{display:flex;gap:8px;margin-top:8px;}
.lookup-row .inp{flex:1;margin-bottom:0;text-transform:uppercase;letter-spacing:.06em;font-weight:700;}

/* PATIENT RESULT */
.pat-result{background:#fff;border-radius:16px;padding:16px;box-shadow:var(--sh);margin-bottom:12px;}
.pat-info{display:flex;align-items:center;gap:12px;margin-bottom:14px;padding-bottom:12px;border-bottom:1px solid var(--bdr);}
.pat-avatar{width:42px;height:42px;border-radius:50%;background:var(--mint-l);display:flex;align-items:center;justify-content:center;font-size:1.1rem;flex-shrink:0;}
.pat-nm{font-family:'DM Serif Display',serif;font-size:.9rem;font-weight:700;color:var(--navy);}
.pat-cd{font-size:.65rem;color:var(--slate);margin-top:1px;}
.check-row{display:flex;align-items:flex-start;gap:10px;padding:10px 0;border-bottom:1px solid var(--bdr);}
.check-row:last-child{border-bottom:none;}
.check-date{font-size:.7rem;font-weight:600;color:var(--navy);min-width:70px;}
.check-detail{flex:1;}
.check-tag{display:inline-block;padding:2px 7px;border-radius:5px;font-size:.6rem;font-weight:700;margin-right:3px;margin-bottom:3px;}
.tag-pain{background:#FFF0F0;color:var(--danger);}
.tag-burn{background:#FFF4E8;color:var(--warn);}
.tag-glu{background:#E8F4FF;color:#2A7FE0;}
.check-notes{font-size:.68rem;color:var(--slate);margin-top:4px;line-height:1.5;}
.no-checks{text-align:center;padding:16px;color:var(--slate);font-size:.76rem;}

/* TOAST */
.toast{position:absolute;bottom:80px;left:50%;transform:translateX(-50%);background:var(--navy);color:#fff;padding:8px 18px;border-radius:20px;font-size:.74rem;font-weight:600;white-space:nowrap;z-index:999;animation:fadeup .3s ease;}
@keyframes fadeup{from{opacity:0;transform:translateX(-50%) translateY(10px);}to{opacity:1;transform:translateX(-50%) translateY(0);}}

/* SPINNER */
.spinner{display:inline-block;width:16px;height:16px;border:2px solid rgba(255,255,255,.3);border-top-color:#fff;border-radius:50%;animation:spin .7s linear infinite;vertical-align:middle;margin-right:6px;}
@keyframes spin{to{transform:rotate(360deg);}}

/* LOGOUT BTN */
.logout-btn{position:absolute;top:14px;right:15px;z-index:2;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.2);border-radius:8px;color:rgba(255,255,255,.7);font-size:.65rem;padding:4px 9px;cursor:pointer;}
.logout-btn:active{background:rgba(255,255,255,.22);}
</style>
</head>
<body>
<div class="wrap">
<div class="phone" id="phone">

<!-- ══════════════════════════════════
     SCREEN 1: ROLE SELECT / LOGIN
══════════════════════════════════ -->
<div class="scr on" id="scr-role">
  <div class="login-bg">
    <div class="logo-row">
      <div class="logo-box"><img src="data:image/png;base64,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" style="width:44px;height:44px;object-fit:cover;border-radius:12px;"></div>
      <div>
        <div class="logo-name">FootGuard</div>
        <div class="logo-sub">Diabetic Foot Monitor</div>
      </div>
    </div>

    <div class="hero">
      <h2>Daily foot care,<br>made simple.</h2>
      <p>Track symptoms, share with your doctor,<br>catch problems early.</p>
    </div>

    <!-- Role selector -->
    <div class="role-row">
      <div class="role-c sel" id="role-patient" onclick="selectRole('patient')">
        <div class="role-icon">🧑‍⚕️</div>
        <div class="role-t">Patient</div>
        <div class="role-s">Log daily foot checks</div>
      </div>
      <div class="role-c" id="role-doctor" onclick="selectRole('doctor')">
        <div class="role-icon">👨‍⚕️</div>
        <div class="role-t">Doctor</div>
        <div class="role-s">Review patient data</div>
      </div>
    </div>

    <!-- Login form -->
    <div class="glass" id="login-form">
      <div class="glass-t" id="form-title">Sign In</div>
      <input class="oinp" id="inp-name" placeholder="Full name" style="display:none">
      <div class="oerr" id="err-name" style="display:none"></div>
      <input class="oinp" id="inp-email" type="email" placeholder="Email address">
      <div class="oerr" id="err-email" style="display:none"></div>
      <input class="oinp" id="inp-pass" type="password" placeholder="Password">
      <div class="oerr" id="err-pass" style="display:none"></div>
      <div style="margin-top:4px"></div>
      <button class="btn" id="auth-btn" onclick="doAuth()">Sign In</button>
      <div class="toggle-row" style="margin-top:10px">
        <span id="toggle-txt">Don't have an account? </span>
        <a onclick="toggleMode()"><span id="toggle-lnk">Sign Up</span></a>
      </div>
    </div>

    <div id="auth-err" style="color:#ff8a8a;font-size:.7rem;text-align:center;margin-top:6px;display:none"></div>
  </div>
</div>

<!-- ══════════════════════════════════
     SCREEN 2: PATIENT HOME
══════════════════════ -->
<div class="scr" id="scr-patient">
  <div class="phdr">
    <button class="logout-btn" onclick="doLogout()">Sign out</button>
    <div class="greet">Good day 👋</div>
    <div class="pname" id="p-name">Loading…</div>
    <div class="code-badge">
      <div>
        <div class="code-lbl">Your Patient Code</div>
        <div class="code-val" id="p-code">—</div>
      </div>
      <div class="code-copy" onclick="copyCode()">Copy</div>
    </div>
  </div>

  <div class="scroll pad">
    <div class="cta" onclick="goTo('scr-log')">
      <div class="ci">🦶</div>
      <div class="ct">
        <div class="t">Log Today's Check</div>
        <div class="s">Takes about 3 minutes</div>
      </div>
      <div class="ca">›</div>
    </div>

    <div class="card">
      <div class="card-t">Recent Checks</div>
      <div id="hist-list"><div class="hist-empty">No checks yet. Log your first one!</div></div>
    </div>

    <div class="card" style="background:linear-gradient(135deg,var(--mint-l),#f0fbf8);border:1px solid #b0ead8;">
      <div style="display:flex;gap:10px;align-items:flex-start;">
        <div style="font-size:1.4rem">💡</div>
        <div>
          <div style="font-size:.76rem;font-weight:700;color:var(--navy);margin-bottom:3px;">Share your code with your doctor</div>
          <div style="font-size:.7rem;color:var(--slate);line-height:1.5;">Give your doctor your Patient Code above so they can look up your records from their dashboard.</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════
     SCREEN 3: LOG FOOT CHECK
══════════════════════ -->
<div class="scr" id="scr-log">
  <div class="shdr">
    <div class="shdr-bk" onclick="goTo('scr-patient')">‹</div>
    <div class="shdr-t">Log Foot Check</div>
  </div>

  <!-- Step bar -->
  <div class="step-bar">
    <div class="step-dot active" id="sdot-0"></div>
    <div class="step-dot" id="sdot-1"></div>
    <div class="step-dot" id="sdot-2"></div>
    <div class="step-dot" id="sdot-3"></div>
    <div class="step-dot" id="sdot-4"></div>
  </div>

  <div class="scroll pad">

    <!-- Step 0: Symptoms -->
    <div class="step-panel on" id="sp-0">
      <div class="step-t">Any symptoms today?</div>
      <div class="step-s">Tap all that apply. Tap again to deselect.</div>
      <div class="sym-grid">
        <div class="sym-b" data-sym="Redness" onclick="toggleSym(this)"><div class="sym-icon">🔴</div><div class="sym-t">Redness</div></div>
        <div class="sym-b" data-sym="Swelling" onclick="toggleSym(this)"><div class="sym-icon">🫧</div><div class="sym-t">Swelling</div></div>
        <div class="sym-b" data-sym="Blister" onclick="toggleSym(this)"><div class="sym-icon">🔵</div><div class="sym-t">Blister</div></div>
        <div class="sym-b" data-sym="Numbness" onclick="toggleSym(this)"><div class="sym-icon">😶</div><div class="sym-t">Numbness</div></div>
        <div class="sym-b" data-sym="Wound/Cut" onclick="toggleSym(this)"><div class="sym-icon">🩹</div><div class="sym-t">Wound/Cut</div></div>
        <div class="sym-b" data-sym="Discoloration" onclick="toggleSym(this)"><div class="sym-icon">🟡</div><div class="sym-t">Discoloration</div></div>
        <div class="sym-b" data-sym="Odour" onclick="toggleSym(this)"><div class="sym-icon">💨</div><div class="sym-t">Odour</div></div>
        <div class="sym-b" data-sym="None" onclick="toggleSym(this)"><div class="sym-icon">✅</div><div class="sym-t">None</div></div>
      </div>
      <button class="btn" onclick="nextStep(0)">Continue →</button>
    </div>

    <!-- Step 1: Pain & Burn -->
    <div class="step-panel" id="sp-1">
      <div class="step-t">Pain & Sensation</div>
      <div class="step-s">Rate your discomfort from 0 (none) to 10 (severe).</div>
      <div class="score-row">
        <div class="score-lbl">Pain level</div>
        <input type="range" min="0" max="10" value="0" id="sl-pain" oninput="document.getElementById('sv-pain').textContent=this.value">
        <div class="score-val" id="sv-pain">0</div>
      </div>
      <div class="score-row">
        <div class="score-lbl">Burning/tingling</div>
        <input type="range" min="0" max="10" value="0" id="sl-burn" oninput="document.getElementById('sv-burn').textContent=this.value">
        <div class="score-val" id="sv-burn">0</div>
      </div>
      <button class="btn" onclick="nextStep(1)" style="margin-top:10px">Continue →</button>
      <button class="btn btn-ghost" onclick="prevStep(1)" style="margin-top:8px">← Back</button>
    </div>

    <!-- Step 2: Blood Glucose -->
    <div class="step-panel" id="sp-2">
      <div class="step-t">Blood Glucose</div>
      <div class="step-s">Enter your readings if available. Leave blank to skip.</div>
      <div class="inp-wrap">
        <label class="inp-lbl">Pre-meal glucose (mg/dL)</label>
        <input class="inp" id="inp-pre" type="number" placeholder="e.g. 110" inputmode="numeric">
      </div>
      <div class="inp-wrap">
        <label class="inp-lbl">Post-meal glucose (mg/dL)</label>
        <input class="inp" id="inp-post" type="number" placeholder="e.g. 140" inputmode="numeric">
      </div>
      <button class="btn" onclick="nextStep(2)" style="margin-top:4px">Continue →</button>
      <button class="btn btn-ghost" onclick="prevStep(2)" style="margin-top:8px">← Back</button>
    </div>

    <!-- Step 3: Photo -->
    <div class="step-panel" id="sp-3">
      <div class="step-t">Add Photos</div>
      <div class="step-s">Optional: Take or upload photos of your feet for your doctor.</div>
      <div class="photo-area" onclick="document.getElementById('photo-inp').click()">
        <input type="file" id="photo-inp" accept="image/*" multiple onchange="previewPhotos(this)">
        <div style="font-size:2rem;margin-bottom:6px">📷</div>
        <div style="font-size:.76rem;color:var(--slate);font-weight:600">Tap to add photos</div>
        <div style="font-size:.65rem;color:var(--tm);margin-top:3px">JPG, PNG — max 5MB each</div>
      </div>
      <div class="photo-preview" id="photo-preview"></div>
      <button class="btn" onclick="nextStep(3)" style="margin-top:10px">Continue →</button>
      <button class="btn btn-ghost" onclick="prevStep(3)" style="margin-top:8px">← Back</button>
    </div>

    <!-- Step 4: Notes + Submit -->
    <div class="step-panel" id="sp-4">
      <div class="step-t">Notes & Submit</div>
      <div class="step-s">Add any extra observations, then submit your check.</div>
      <div class="inp-wrap">
        <label class="inp-lbl">Notes (optional)</label>
        <textarea class="inp" id="inp-notes" rows="3" placeholder="Any other observations…" style="resize:none;line-height:1.5"></textarea>
      </div>
      <button class="btn" id="submit-btn" onclick="submitCheck()">Submit Check ✓</button>
      <button class="btn btn-ghost" onclick="prevStep(4)" style="margin-top:8px">← Back</button>
    </div>

  </div>
</div>

<!-- ══════════════════════════════════
     SCREEN 4: DOCTOR HOME
══════════════════════ -->
<div class="scr" id="scr-doctor">
  <div class="dhdr">
    <button class="logout-btn" onclick="doLogout()">Sign out</button>
    <div class="d-role">Doctor Dashboard</div>
    <div class="d-name" id="d-name">Loading…</div>
  </div>

  <div class="scroll pad">
    <div class="lookup-box">
      <div class="card-t" style="margin-bottom:6px">🔍 Look Up Patient</div>
      <div style="font-size:.72rem;color:var(--slate);margin-bottom:10px;">Enter the patient's unique code (e.g. PAT-K7MR)</div>
      <div class="lookup-row">
        <input class="inp" id="inp-lookup" placeholder="PAT-XXXX" maxlength="8" oninput="this.value=this.value.toUpperCase()" onkeydown="if(event.key==='Enter')lookupPatient()">
        <button class="btn btn-sm" onclick="lookupPatient()" id="lookup-btn">Search</button>
      </div>
      <div id="lookup-err" style="color:var(--danger);font-size:.66rem;margin-top:6px;display:none"></div>
    </div>

    <div id="pat-result" style="display:none">
      <!-- filled dynamically -->
    </div>

    <div class="card" style="background:var(--smoke);border:1.5px dashed var(--bdr);">
      <div style="text-align:center;padding:8px 0;">
        <div style="font-size:1.6rem;margin-bottom:6px">👆</div>
        <div style="font-size:.76rem;font-weight:600;color:var(--slate);">Enter a patient code above to view their foot check history</div>
      </div>
    </div>
  </div>
</div>

</div><!-- /phone -->
</div><!-- /wrap -->

<script>
/* ══════════════════════════════════════
   SUPABASE INIT
   ⚠️ Replace with your actual keys
══════════════════════════════════════ */
const SUPABASE_URL = 'https://bsviguqdrgyihuwsrvzy.supabase.co';
const SUPABASE_ANON = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJzdmlndXFkcmd5aWh1d3Nydnp5Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzM2NDExNjUsImV4cCI6MjA4OTIxNzE2NX0.AY9YLl_bDLsKuBKZ44KOgYZm0PNr4jqA1pLtaDBn3D8';

const { createClient } = supabase;
const db = createClient(SUPABASE_URL, SUPABASE_ANON);

/* ══════════════════════════════════════
   STATE
══════════════════════════════════════ */
let currentRole = 'patient';
let isSignUp = false;
let currentStep = 0;
let selectedSymptoms = [];
let photoFiles = [];
let currentUser = null;
let currentProfile = null;

/* ══════════════════════════════════════
   NAVIGATION
══════════════════════════════════════ */
function goTo(id) {
  document.querySelectorAll('.scr').forEach(s => s.classList.remove('on'));
  document.getElementById(id).classList.add('on');
}

/* ══════════════════════════════════════
   ROLE SELECT
══════════════════════════════════════ */
function selectRole(role) {
  currentRole = role;
  document.getElementById('role-patient').classList.toggle('sel', role === 'patient');
  document.getElementById('role-doctor').classList.toggle('sel', role === 'doctor');
}

/* ══════════════════════════════════════
   AUTH MODE TOGGLE
══════════════════════════════════════ */
function toggleMode() {
  isSignUp = !isSignUp;
  document.getElementById('inp-name').style.display = isSignUp ? 'block' : 'none';
  document.getElementById('form-title').textContent = isSignUp ? 'Create Account' : 'Sign In';
  document.getElementById('auth-btn').textContent = isSignUp ? 'Sign Up' : 'Sign In';
  document.getElementById('toggle-txt').textContent = isSignUp ? 'Already have an account? ' : "Don't have an account? ";
  document.getElementById('toggle-lnk').textContent = isSignUp ? 'Sign In' : 'Sign Up';
  clearErrors();
}

function clearErrors() {
  ['err-name','err-email','err-pass'].forEach(id => {
    document.getElementById(id).style.display = 'none';
    document.getElementById(id).textContent = '';
  });
  document.getElementById('auth-err').style.display = 'none';
}

/* ══════════════════════════════════════
   PATIENT CODE GENERATOR
══════════════════════════════════════ */
function generatePatientCode() {
  const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
  let code = 'PAT-';
  for (let i = 0; i < 4; i++) code += chars[Math.floor(Math.random() * chars.length)];
  return code;
}

/* ══════════════════════════════════════
   AUTH: SIGN IN / SIGN UP
══════════════════════════════════════ */
async function doAuth() {
  clearErrors();
  const email = document.getElementById('inp-email').value.trim();
  const pass = document.getElementById('inp-pass').value;
  const name = document.getElementById('inp-name').value.trim();
  let valid = true;

  if (isSignUp && !name) {
    showFieldErr('err-name','Please enter your name'); valid = false;
  }
  if (!email || !email.includes('@')) {
    showFieldErr('err-email','Enter a valid email'); valid = false;
  }
  if (!pass || pass.length < 6) {
    showFieldErr('err-pass','Password must be at least 6 characters'); valid = false;
  }
  if (!valid) return;

  const btn = document.getElementById('auth-btn');
  btn.disabled = true;
  btn.innerHTML = '<span class="spinner"></span>' + (isSignUp ? 'Creating account…' : 'Signing in…');

  try {
    if (isSignUp) {
      // SIGN UP
      const { data, error } = await db.auth.signUp({ email, password: pass });
      if (error) throw error;

      const patientCode = currentRole === 'patient' ? generatePatientCode() : null;
      const { error: profErr } = await db.from('profiles').insert({
        id: data.user.id,
        name,
        role: currentRole,
        patient_code: patientCode
      });
      if (profErr) throw profErr;

      currentUser = data.user;
      currentProfile = { name, role: currentRole, patient_code: patientCode };
      routeToDashboard();
    } else {
      // SIGN IN
      const { data, error } = await db.auth.signInWithPassword({ email, password: pass });
      if (error) throw error;

      const { data: profile, error: profErr } = await db.from('profiles')
        .select('*').eq('id', data.user.id).single();
      if (profErr) throw profErr;

      currentUser = data.user;
      currentProfile = profile;
      routeToDashboard();
    }
  } catch (err) {
    const errEl = document.getElementById('auth-err');
    errEl.textContent = err.message || 'Something went wrong. Try again.';
    errEl.style.display = 'block';
  } finally {
    btn.disabled = false;
    btn.textContent = isSignUp ? 'Sign Up' : 'Sign In';
  }
}

function showFieldErr(id, msg) {
  const el = document.getElementById(id);
  el.textContent = msg;
  el.style.display = 'block';
}

function routeToDashboard() {
  if (currentProfile.role === 'patient') {
    document.getElementById('p-name').textContent = currentProfile.name;
    document.getElementById('p-code').textContent = currentProfile.patient_code || '—';
    loadPatientHistory();
    goTo('scr-patient');
  } else {
    document.getElementById('d-name').textContent = 'Dr. ' + currentProfile.name;
    goTo('scr-doctor');
  }
}

/* ══════════════════════════════════════
   LOGOUT
══════════════════════════════════════ */
async function doLogout() {
  await db.auth.signOut();
  currentUser = null;
  currentProfile = null;
  goTo('scr-role');
  showToast('Signed out');
}

/* ══════════════════════════════════════
   COPY PATIENT CODE
══════════════════════════════════════ */
function copyCode() {
  const code = document.getElementById('p-code').textContent;
  if (navigator.clipboard) navigator.clipboard.writeText(code);
  showToast('Code copied: ' + code);
}

/* ══════════════════════════════════════
   PATIENT HISTORY
══════════════════════════════════════ */
async function loadPatientHistory() {
  const { data, error } = await db.from('foot_checks')
    .select('*')
    .eq('patient_id', currentUser.id)
    .order('created_at', { ascending: false })
    .limit(10);

  const list = document.getElementById('hist-list');
  if (error || !data || data.length === 0) {
    list.innerHTML = '<div class="hist-empty">No checks yet. Log your first one!</div>';
    return;
  }

  list.innerHTML = data.map(c => {
    const d = new Date(c.created_at);
    const dateStr = d.toLocaleDateString('en-IN', { day:'numeric', month:'short' });
    const hasSymptoms = c.symptoms && c.symptoms.length > 0 && !c.symptoms.includes('None');
    return `<div class="hist-item">
      <div class="hist-dot ${hasSymptoms ? 'warn' : 'ok'}"></div>
      <div class="hist-date">${dateStr}</div>
      <div class="hist-status">${hasSymptoms ? c.symptoms.join(', ') : 'All clear'}</div>
    </div>`;
  }).join('');
}

/* ══════════════════════════════════════
   LOG CHECK — STEPS
══════════════════════════════════════ */
function nextStep(from) {
  document.getElementById('sp-' + from).classList.remove('on');
  document.getElementById('sdot-' + from).classList.remove('active');
  document.getElementById('sdot-' + from).classList.add('done');
  currentStep = from + 1;
  document.getElementById('sp-' + currentStep).classList.add('on');
  document.getElementById('sdot-' + currentStep).classList.add('active');
  document.querySelector('.scroll').scrollTop = 0;
}

function prevStep(from) {
  document.getElementById('sp-' + from).classList.remove('on');
  document.getElementById('sdot-' + from).classList.remove('active');
  currentStep = from - 1;
  document.getElementById('sp-' + currentStep).classList.add('on');
  document.getElementById('sdot-' + currentStep).classList.remove('done');
  document.getElementById('sdot-' + currentStep).classList.add('active');
  document.querySelector('.scroll').scrollTop = 0;
}

function toggleSym(el) {
  const sym = el.dataset.sym;
  el.classList.toggle('sel');
  if (el.classList.contains('sel')) {
    if (sym === 'None') {
      // Deselect others
      document.querySelectorAll('.sym-b').forEach(b => { if(b!==el) b.classList.remove('sel'); });
      selectedSymptoms = ['None'];
    } else {
      document.querySelectorAll('.sym-b[data-sym="None"]').forEach(b => b.classList.remove('sel'));
      selectedSymptoms = selectedSymptoms.filter(s => s !== 'None');
      if (!selectedSymptoms.includes(sym)) selectedSymptoms.push(sym);
    }
  } else {
    selectedSymptoms = selectedSymptoms.filter(s => s !== sym);
  }
}

function previewPhotos(input) {
  photoFiles = Array.from(input.files);
  const preview = document.getElementById('photo-preview');
  preview.innerHTML = '';
  photoFiles.forEach(f => {
    const url = URL.createObjectURL(f);
    const img = document.createElement('img');
    img.className = 'photo-thumb';
    img.src = url;
    preview.appendChild(img);
  });
}

async function submitCheck() {
  const btn = document.getElementById('submit-btn');
  btn.disabled = true;
  btn.innerHTML = '<span class="spinner"></span>Saving…';

  try {
    // Upload photos if any
    let photoUrls = [];
    for (const file of photoFiles) {
      const ext = file.name.split('.').pop();
      const path = `${currentUser.id}/${Date.now()}.${ext}`;
      const { data, error } = await db.storage.from('foot-photos').upload(path, file);
      if (!error && data) {
        const { data: urlData } = db.storage.from('foot-photos').getPublicUrl(path);
        photoUrls.push(urlData.publicUrl);
      }
    }

    const { error } = await db.from('foot_checks').insert({
      patient_id: currentUser.id,
      pain_score: parseInt(document.getElementById('sl-pain').value),
      burn_score: parseInt(document.getElementById('sl-burn').value),
      symptoms: selectedSymptoms,
      pre_glucose: parseInt(document.getElementById('inp-pre').value) || null,
      post_glucose: parseInt(document.getElementById('inp-post').value) || null,
      notes: document.getElementById('inp-notes').value.trim() || null,
      photo_urls: photoUrls
    });

    if (error) throw error;

    // Reset form
    selectedSymptoms = [];
    photoFiles = [];
    document.querySelectorAll('.sym-b').forEach(b => b.classList.remove('sel'));
    document.getElementById('sl-pain').value = 0;
    document.getElementById('sl-burn').value = 0;
    document.getElementById('sv-pain').textContent = '0';
    document.getElementById('sv-burn').textContent = '0';
    document.getElementById('inp-pre').value = '';
    document.getElementById('inp-post').value = '';
    document.getElementById('inp-notes').value = '';
    document.getElementById('photo-preview').innerHTML = '';
    // Reset steps
    for (let i = 0; i <= 4; i++) {
      document.getElementById('sp-' + i).classList.remove('on');
      document.getElementById('sdot-' + i).classList.remove('done','active');
    }
    document.getElementById('sp-0').classList.add('on');
    document.getElementById('sdot-0').classList.add('active');
    currentStep = 0;

    loadPatientHistory();
    goTo('scr-patient');
    showToast('✅ Check saved!');
  } catch (err) {
    showToast('Error: ' + (err.message || 'Could not save'));
  } finally {
    btn.disabled = false;
    btn.textContent = 'Submit Check ✓';
  }
}

/* ══════════════════════════════════════
   DOCTOR: PATIENT LOOKUP
══════════════════════════════════════ */
async function lookupPatient() {
  const code = document.getElementById('inp-lookup').value.trim().toUpperCase();
  const errEl = document.getElementById('lookup-err');
  errEl.style.display = 'none';

  if (!code || code.length < 4) {
    errEl.textContent = 'Enter a valid patient code';
    errEl.style.display = 'block';
    return;
  }

  const btn = document.getElementById('lookup-btn');
  btn.disabled = true;
  btn.innerHTML = '<span class="spinner"></span>';

  try {
    // Look up profile by patient_code
    const { data: profile, error: pErr } = await db.from('profiles')
      .select('*').eq('patient_code', code).single();

    if (pErr || !profile) {
      errEl.textContent = 'Patient not found. Check the code and try again.';
      errEl.style.display = 'block';
      document.getElementById('pat-result').style.display = 'none';
      return;
    }

    // Fetch their checks
    const { data: checks } = await db.from('foot_checks')
      .select('*')
      .eq('patient_id', profile.id)
      .order('created_at', { ascending: false })
      .limit(20);

    renderPatientResult(profile, checks || []);
  } catch (err) {
    errEl.textContent = err.message || 'Something went wrong';
    errEl.style.display = 'block';
  } finally {
    btn.disabled = false;
    btn.textContent = 'Search';
  }
}

function renderPatientResult(profile, checks) {
  const resultEl = document.getElementById('pat-result');

  const checksHtml = checks.length === 0
    ? '<div class="no-checks">No foot checks recorded yet.</div>'
    : checks.map(c => {
        const d = new Date(c.created_at);
        const dateStr = d.toLocaleDateString('en-IN', { day:'numeric', month:'short', year:'numeric' });
        const syms = (c.symptoms && c.symptoms.length > 0) ? c.symptoms.join(', ') : 'No symptoms';
        return `<div class="check-row">
          <div class="check-date">${dateStr}</div>
          <div class="check-detail">
            ${c.pain_score > 0 ? `<span class="check-tag tag-pain">Pain ${c.pain_score}/10</span>` : ''}
            ${c.burn_score > 0 ? `<span class="check-tag tag-burn">Burn ${c.burn_score}/10</span>` : ''}
            ${c.pre_glucose ? `<span class="check-tag tag-glu">Glucose ${c.pre_glucose}/${c.post_glucose||'—'}</span>` : ''}
            <div class="check-notes">${syms}${c.notes ? ' · ' + c.notes : ''}</div>
            ${c.photo_urls && c.photo_urls.length > 0
              ? `<div style="display:flex;gap:4px;margin-top:5px;">${c.photo_urls.map(u=>`<img src="${u}" style="width:48px;height:48px;border-radius:6px;object-fit:cover;border:1.5px solid var(--bdr)">`).join('')}</div>`
              : ''}
          </div>
        </div>`;
      }).join('');

  resultEl.innerHTML = `
    <div class="pat-result card">
      <div class="pat-info">
        <div class="pat-avatar">🧑‍⚕️</div>
        <div>
          <div class="pat-nm">${profile.name}</div>
          <div class="pat-cd">Code: ${profile.patient_code} · ${checks.length} check${checks.length !== 1 ? 's' : ''}</div>
        </div>
      </div>
      <div class="card-t">Foot Check History</div>
      ${checksHtml}
    </div>`;
  resultEl.style.display = 'block';
}

/* ══════════════════════════════════════
   TOAST
══════════════════════════════════════ */
function showToast(msg) {
  const ex = document.querySelector('.toast');
  if (ex) ex.remove();
  const t = document.createElement('div');
  t.className = 'toast';
  t.textContent = msg;
  document.getElementById('phone').appendChild(t);
  setTimeout(() => t.remove(), 2400);
}

/* ══════════════════════════════════════
   SESSION RESTORE on load
══════════════════════════════════════ */
(async () => {
  const { data: { session } } = await db.auth.getSession();
  if (session) {
    const { data: profile } = await db.from('profiles')
      .select('*').eq('id', session.user.id).single();
    if (profile) {
      currentUser = session.user;
      currentProfile = profile;
      routeToDashboard();
    }
  }
})();
</script>
</body>
</html>
# footguard-v2
