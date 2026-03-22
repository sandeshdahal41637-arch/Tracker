<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Your Recovery Journey</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;
    --surface: #161b22;
    --surface2: #1c2128;
    --border: #30363d;
    --text: #e6edf3;
    --muted: #7d8590;
    --accent: #58a6ff;
    --green: #3fb950;
    --orange: #d29922;
    --red: #f85149;
    --purple: #bc8cff;
    --teal: #39d353;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
    padding: 24px 16px 80px;
  }

  .noise {
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    opacity: 0.4;
  }

  .container { max-width: 680px; margin: 0 auto; position: relative; z-index: 1; }

  /* Header */
  .header { text-align: center; padding: 32px 0 40px; }
  .header .day-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: linear-gradient(135deg, rgba(88,166,255,0.15), rgba(188,140,255,0.15));
    border: 1px solid rgba(88,166,255,0.3);
    border-radius: 100px; padding: 6px 18px;
    font-size: 13px; color: var(--accent); font-weight: 500;
    margin-bottom: 20px; letter-spacing: 0.5px;
  }
  .header h1 {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(28px, 6vw, 42px);
    line-height: 1.15;
    background: linear-gradient(135deg, #e6edf3 30%, #bc8cff);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 10px;
  }
  .header p { color: var(--muted); font-size: 15px; line-height: 1.6; }

  /* Streak bar */
  .streak-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    margin-bottom: 20px;
    display: flex; align-items: center; gap: 20px;
  }
  .streak-num {
    font-family: 'DM Serif Display', serif;
    font-size: 56px; line-height: 1;
    color: var(--teal);
    min-width: 80px; text-align: center;
  }
  .streak-label { font-size: 13px; color: var(--muted); margin-top: 4px; }
  .streak-info h3 { font-size: 18px; font-weight: 600; margin-bottom: 6px; }
  .streak-info p { font-size: 13px; color: var(--muted); line-height: 1.5; }

  .progress-bar-wrap { margin-top: 14px; }
  .progress-label { display: flex; justify-content: space-between; font-size: 12px; color: var(--muted); margin-bottom: 6px; }
  .progress-bar {
    height: 6px; background: var(--surface2); border-radius: 10px; overflow: hidden;
  }
  .progress-fill {
    height: 100%; border-radius: 10px;
    background: linear-gradient(90deg, var(--accent), var(--purple));
    transition: width 0.6s ease;
  }

  /* Section headers */
  .section-title {
    font-size: 11px; font-weight: 600; letter-spacing: 1.2px;
    color: var(--muted); text-transform: uppercase;
    margin: 28px 0 12px;
  }

  /* Daily check-in */
  .checkin-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px; overflow: hidden;
    margin-bottom: 16px;
  }
  .checkin-header {
    padding: 18px 20px 14px;
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 10px;
  }
  .checkin-header .dot {
    width: 8px; height: 8px; border-radius: 50%;
    background: var(--green); flex-shrink: 0;
    box-shadow: 0 0 8px var(--green);
  }
  .checkin-header h3 { font-size: 15px; font-weight: 600; }
  .checkin-header span { font-size: 12px; color: var(--muted); margin-left: auto; }

  .mood-row { padding: 16px 20px; display: flex; gap: 10px; flex-wrap: wrap; }
  .mood-btn {
    background: var(--surface2); border: 1px solid var(--border);
    border-radius: 100px; padding: 8px 16px;
    font-size: 14px; cursor: pointer; color: var(--text);
    font-family: 'DM Sans', sans-serif;
    transition: all 0.2s;
  }
  .mood-btn:hover, .mood-btn.active {
    border-color: var(--accent); background: rgba(88,166,255,0.12);
    color: var(--accent);
  }

  .symptom-grid { padding: 0 20px 16px; display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  .symptom-item {
    display: flex; align-items: center; gap: 10px;
    background: var(--surface2); border: 1px solid var(--border);
    border-radius: 10px; padding: 10px 12px;
    cursor: pointer; transition: all 0.2s;
    font-size: 13px;
  }
  .symptom-item:hover { border-color: var(--border); }
  .symptom-item.checked { border-color: var(--orange); background: rgba(210,153,34,0.1); }
  .symptom-item .cb {
    width: 16px; height: 16px; border-radius: 4px;
    border: 1.5px solid var(--border); flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    font-size: 10px;
  }
  .symptom-item.checked .cb { border-color: var(--orange); background: var(--orange); color: #000; }

  .note-area { padding: 0 20px 16px; }
  .note-area textarea {
    width: 100%; background: var(--surface2); border: 1px solid var(--border);
    border-radius: 10px; padding: 12px; color: var(--text);
    font-family: 'DM Sans', sans-serif; font-size: 14px;
    resize: none; height: 80px; outline: none;
    transition: border-color 0.2s;
  }
  .note-area textarea:focus { border-color: var(--accent); }
  .note-area textarea::placeholder { color: var(--muted); }

  .checkin-footer { padding: 0 20px 18px; }
  .save-btn {
    width: 100%; background: linear-gradient(135deg, var(--accent), var(--purple));
    border: none; border-radius: 10px; padding: 13px;
    color: #fff; font-family: 'DM Sans', sans-serif;
    font-size: 15px; font-weight: 600; cursor: pointer;
    transition: opacity 0.2s, transform 0.1s;
  }
  .save-btn:hover { opacity: 0.9; }
  .save-btn:active { transform: scale(0.99); }

  /* Reconnection plan */
  .recon-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px; overflow: hidden;
    margin-bottom: 16px;
  }
  .recon-header {
    padding: 18px 20px;
    background: linear-gradient(135deg, rgba(188,140,255,0.1), rgba(57,211,83,0.05));
    border-bottom: 1px solid var(--border);
  }
  .recon-header h3 { font-size: 15px; font-weight: 600; margin-bottom: 3px; }
  .recon-header p { font-size: 13px; color: var(--muted); }

  .recon-step {
    padding: 16px 20px;
    border-bottom: 1px solid var(--border);
    display: flex; gap: 14px; align-items: flex-start;
    cursor: pointer; transition: background 0.15s;
  }
  .recon-step:last-child { border-bottom: none; }
  .recon-step:hover { background: rgba(255,255,255,0.02); }
  .step-num {
    width: 28px; height: 28px; border-radius: 50%;
    background: var(--surface2); border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    font-size: 12px; font-weight: 600; color: var(--muted);
    flex-shrink: 0; margin-top: 1px;
    transition: all 0.2s;
  }
  .recon-step.done .step-num {
    background: rgba(63,185,80,0.2); border-color: var(--green); color: var(--green);
  }
  .step-content h4 { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
  .step-content p { font-size: 13px; color: var(--muted); line-height: 1.5; }
  .step-content .week-tag {
    display: inline-block; font-size: 11px; font-weight: 500;
    color: var(--purple); background: rgba(188,140,255,0.1);
    border-radius: 4px; padding: 2px 7px; margin-bottom: 5px;
  }

  /* Coping toolkit */
  .toolkit-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 16px; }
  .tool-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 14px; padding: 16px;
    cursor: pointer; transition: all 0.2s;
  }
  .tool-card:hover { border-color: var(--accent); transform: translateY(-1px); }
  .tool-icon { font-size: 22px; margin-bottom: 8px; }
  .tool-card h4 { font-size: 13px; font-weight: 600; margin-bottom: 4px; }
  .tool-card p { font-size: 12px; color: var(--muted); line-height: 1.4; }

  /* Milestones */
  .milestone-row {
    display: flex; gap: 8px; overflow-x: auto;
    padding-bottom: 8px; margin-bottom: 16px;
    scrollbar-width: none;
  }
  .milestone-row::-webkit-scrollbar { display: none; }
  .milestone {
    flex-shrink: 0; background: var(--surface);
    border: 1px solid var(--border); border-radius: 12px;
    padding: 12px 16px; text-align: center; min-width: 90px;
    transition: all 0.2s;
  }
  .milestone.reached { border-color: var(--teal); background: rgba(57,211,83,0.08); }
  .milestone.reached .m-days { color: var(--teal); }
  .m-icon { font-size: 20px; margin-bottom: 4px; }
  .m-days { font-size: 18px; font-weight: 700; font-family: 'DM Serif Display', serif; color: var(--muted); }
  .m-label { font-size: 11px; color: var(--muted); }

  /* Log */
  .log-entry {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 12px; padding: 14px 16px; margin-bottom: 8px;
    display: flex; gap: 12px; align-items: flex-start;
  }
  .log-date { font-size: 11px; color: var(--muted); min-width: 60px; padding-top: 2px; }
  .log-content { flex: 1; }
  .log-mood { font-size: 14px; margin-bottom: 3px; }
  .log-note { font-size: 13px; color: var(--muted); line-height: 1.4; }
  .log-symptoms { display: flex; gap: 5px; flex-wrap: wrap; margin-top: 5px; }
  .log-tag {
    font-size: 11px; padding: 2px 8px; border-radius: 4px;
    background: rgba(210,153,34,0.15); color: var(--orange);
  }

  /* Empty state */
  .empty { text-align: center; padding: 32px 20px; color: var(--muted); font-size: 14px; }
  .empty .e-icon { font-size: 32px; margin-bottom: 10px; }

  /* Modal */
  .modal-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(0,0,0,0.7); z-index: 100;
    align-items: center; justify-content: center; padding: 20px;
  }
  .modal-overlay.open { display: flex; }
  .modal {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 18px; padding: 28px; max-width: 400px; width: 100%;
    animation: slideUp 0.25s ease;
  }
  @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
  .modal h3 { font-size: 20px; font-family: 'DM Serif Display', serif; margin-bottom: 10px; }
  .modal p { font-size: 14px; color: var(--muted); line-height: 1.65; margin-bottom: 16px; }
  .modal-close {
    width: 100%; background: var(--surface2); border: 1px solid var(--border);
    border-radius: 10px; padding: 12px; color: var(--text);
    font-family: 'DM Sans', sans-serif; font-size: 14px; cursor: pointer;
  }

  /* Toast */
  .toast {
    position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%) translateY(100px);
    background: var(--green); color: #000; padding: 12px 24px;
    border-radius: 100px; font-size: 14px; font-weight: 600;
    transition: transform 0.3s ease; z-index: 200;
  }
  .toast.show { transform: translateX(-50%) translateY(0); }

  /* Nav */
  .bottom-nav {
    position: fixed; bottom: 0; left: 0; right: 0;
    background: rgba(13,17,23,0.95); border-top: 1px solid var(--border);
    display: flex; z-index: 50;
    backdrop-filter: blur(12px);
  }
  .nav-btn {
    flex: 1; padding: 12px 8px; background: none; border: none;
    color: var(--muted); font-family: 'DM Sans', sans-serif;
    font-size: 11px; cursor: pointer; transition: color 0.2s;
    display: flex; flex-direction: column; align-items: center; gap: 4px;
  }
  .nav-btn .nav-icon { font-size: 20px; }
  .nav-btn.active { color: var(--accent); }

  .tab { display: none; }
  .tab.active { display: block; }

  @media (min-width: 480px) {
    .symptom-grid { grid-template-columns: 1fr 1fr 1fr; }
    .toolkit-grid { grid-template-columns: 1fr 1fr 1fr 1fr; }
  }
</style>
</head>
<body>
<div class="noise"></div>
<div class="container">

  <!-- HOME TAB -->
  <div class="tab active" id="tab-home">
    <div class="header">
      <div class="day-badge">🌱 Recovery Tracker</div>
      <h1>One day<br><em>at a time</em></h1>
      <p>Your personal space to stay honest, stay strong,<br>and find your way back to the people you love.</p>
    </div>

    <div class="streak-card">
      <div>
        <div class="streak-num" id="streak-num">0</div>
        <div class="streak-label">days clean</div>
      </div>
      <div class="streak-info" style="flex:1">
        <h3 id="streak-phrase">Today is Day One 💙</h3>
        <p id="streak-sub">Every hour you get through today matters. You don't have to be perfect — just present.</p>
        <div class="progress-bar-wrap">
          <div class="progress-label">
            <span>Day 0</span><span id="prog-next">Next: Day 7</span>
          </div>
          <div class="progress-bar"><div class="progress-fill" id="prog-fill" style="width:0%"></div></div>
        </div>
      </div>
    </div>

    <div class="section-title">Milestones</div>
    <div class="milestone-row">
      <div class="milestone" id="m1"><div class="m-icon">🌱</div><div class="m-days">1</div><div class="m-label">day</div></div>
      <div class="milestone" id="m3"><div class="m-icon">🔥</div><div class="m-days">3</div><div class="m-label">days</div></div>
      <div class="milestone" id="m7"><div class="m-icon">⭐</div><div class="m-days">7</div><div class="m-label">days</div></div>
      <div class="milestone" id="m14"><div class="m-icon">💪</div><div class="m-days">14</div><div class="m-label">days</div></div>
      <div class="milestone" id="m30"><div class="m-icon">🏆</div><div class="m-days">30</div><div class="m-label">days</div></div>
      <div class="milestone" id="m60"><div class="m-icon">🌟</div><div class="m-days">60</div><div class="m-label">days</div></div>
      <div class="milestone" id="m90"><div class="m-icon">👑</div><div class="m-days">90</div><div class="m-label">days</div></div>
    </div>

    <div class="section-title">Today's Check-In</div>
    <div class="checkin-card">
      <div class="checkin-header">
        <div class="dot"></div>
        <h3>How are you right now?</h3>
        <span id="today-date"></span>
      </div>

      <div class="mood-row" id="mood-row">
        <button class="mood-btn" onclick="selectMood(this,'😔 Struggling')">😔 Struggling</button>
        <button class="mood-btn" onclick="selectMood(this,'😐 Okay')">😐 Okay</button>
        <button class="mood-btn" onclick="selectMood(this,'🙂 Holding on')">🙂 Holding on</button>
        <button class="mood-btn" onclick="selectMood(this,'💪 Strong today')">💪 Strong today</button>
      </div>

      <div class="section-title" style="padding: 0 20px; margin-top:0; margin-bottom:8px;">Any symptoms today?</div>
      <div class="symptom-grid" id="symptom-grid">
        <div class="symptom-item" onclick="toggleSymptom(this,'Fatigue')"><div class="cb"></div>Fatigue</div>
        <div class="symptom-item" onclick="toggleSymptom(this,'Cravings')"><div class="cb">✓</div>Cravings</div>
        <div class="symptom-item" onclick="toggleSymptom(this,'Bad sleep')"><div class="cb"></div>Bad sleep</div>
        <div class="symptom-item" onclick="toggleSymptom(this,'Anxiety')"><div class="cb"></div>Anxiety</div>
        <div class="symptom-item" onclick="toggleSymptom(this,'Low mood')"><div class="cb"></div>Low mood</div>
        <div class="symptom-item" onclick="toggleSymptom(this,'Irritable')"><div class="cb"></div>Irritable</div>
      </div>

      <div class="note-area">
        <textarea id="day-note" placeholder="Anything on your mind today? (optional — just for you)"></textarea>
      </div>
      <div class="checkin-footer">
        <button class="save-btn" onclick="saveCheckin()">Save Today's Check-In ✓</button>
      </div>
    </div>
  </div>

  <!-- RECONNECT TAB -->
  <div class="tab" id="tab-reconnect">
    <div class="header" style="padding-top:20px;">
      <h1>Reconnecting<br><em>with family</em></h1>
      <p>Two years of silence doesn't erase love.<br>They're waiting. Here's your roadmap.</p>
    </div>

    <div class="section-title">The 5-Step Plan</div>
    <div class="recon-card">
      <div class="recon-header">
        <h3>💙 Parents & Siblings</h3>
        <p>Go gently. Small steps rebuild trust faster than big gestures.</p>
      </div>

      <div class="recon-step" id="rs1" onclick="toggleStep('rs1')">
        <div class="step-num">1</div>
        <div class="step-content">
          <div class="week-tag">Week 1–2 of being clean</div>
          <h4>Send a short message — no explanations yet</h4>
          <p>Just: "Hi, I'm okay. I've been going through something hard but I'm working on it. I miss you." That's enough. You don't owe a full story yet. Let them know you're alive and thinking of them.</p>
        </div>
      </div>

      <div class="recon-step" id="rs2" onclick="toggleStep('rs2')">
        <div class="step-num">2</div>
        <div class="step-content">
          <div class="week-tag">Week 2–3</div>
          <h4>One short phone call or voice note</h4>
          <p>Don't feel pressured to explain everything. Even 5–10 minutes of normal conversation — asking how they're doing — starts warming the relationship again. They want to hear your voice.</p>
        </div>
      </div>

      <div class="recon-step" id="rs3" onclick="toggleStep('rs3')">
        <div class="step-num">3</div>
        <div class="step-content">
          <div class="week-tag">Week 4 (if comfortable)</div>
          <h4>Be honest in your own words</h4>
          <p>You don't need to say "meth." You can say: "I got into something that took over my life and I pushed everyone away. I'm getting better and I'm sorry." Honesty doesn't need to be perfect — just real.</p>
        </div>
      </div>

      <div class="recon-step" id="rs4" onclick="toggleStep('rs4')">
        <div class="step-num">4</div>
        <div class="step-content">
          <div class="week-tag">Month 2</div>
          <h4>Regular, consistent contact</h4>
          <p>Show up consistently — a weekly call, voice note, or message. Trust is rebuilt through pattern, not through one big conversation. Show them the person you're becoming.</p>
        </div>
      </div>

      <div class="recon-step" id="rs5" onclick="toggleStep('rs5')">
        <div class="step-num">5</div>
        <div class="step-content">
          <div class="week-tag">Month 3+</div>
          <h4>Let them in further</h4>
          <p>As you get stronger, share more of your journey with the family members you trust most. Letting someone support you is a gift to them — it gives them a role in your recovery.</p>
        </div>
      </div>
    </div>

    <div class="section-title">Things to Remember</div>
    <div class="recon-card">
      <div class="recon-step" style="cursor:default;">
        <div style="font-size:22px; flex-shrink:0;">💬</div>
        <div class="step-content">
          <h4>They may need time too</h4>
          <p>If they seem guarded or emotional at first, that's not rejection — it's love that was worried. Give them space to adjust to having you back.</p>
        </div>
      </div>
      <div class="recon-step" style="cursor:default;">
        <div style="font-size:22px; flex-shrink:0;">🛡️</div>
        <div class="step-content">
          <h4>You don't have to explain everything</h4>
          <p>You owe honesty, not a detailed account. Share what feels right, when it feels right. Recovery is yours first.</p>
        </div>
      </div>
      <div class="recon-step" style="cursor:default; border:none;">
        <div style="font-size:22px; flex-shrink:0;">🌱</div>
        <div class="step-content">
          <h4>Being clean IS the best thing you can give them</h4>
          <p>Every day you stay clean, you're already giving your family the most important gift. Let that be enough for now.</p>
        </div>
      </div>
    </div>
  </div>

  <!-- TOOLKIT TAB -->
  <div class="tab" id="tab-toolkit">
    <div class="header" style="padding-top:20px;">
      <h1>Coping<br><em>toolkit</em></h1>
      <p>Tools for cravings, hard shifts, bad nights.<br>Tap any card for the full technique.</p>
    </div>

    <div class="section-title">When a craving hits</div>
    <div class="toolkit-grid">
      <div class="tool-card" onclick="openTool('15min')">
        <div class="tool-icon">⏱️</div>
        <h4>15-Minute Rule</h4>
        <p>Delay, don't decide</p>
      </div>
      <div class="tool-card" onclick="openTool('breath')">
        <div class="tool-icon">🌬️</div>
        <h4>Box Breathing</h4>
        <p>Reset your nervous system</p>
      </div>
      <div class="tool-card" onclick="openTool('grounding')">
        <div class="tool-icon">🌿</div>
        <h4>5-4-3-2-1</h4>
        <p>Ground yourself now</p>
      </div>
      <div class="tool-card" onclick="openTool('urge')">
        <div class="tool-icon">🌊</div>
        <h4>Urge Surfing</h4>
        <p>Ride it, don't fight it</p>
      </div>
    </div>

    <div class="section-title">For sleep problems</div>
    <div class="toolkit-grid">
      <div class="tool-card" onclick="openTool('sleep1')">
        <div class="tool-icon">🌙</div>
        <h4>Wind-Down Routine</h4>
        <p>30-min pre-sleep ritual</p>
      </div>
      <div class="tool-card" onclick="openTool('sleep2')">
        <div class="tool-icon">💊</div>
        <h4>Melatonin & Timing</h4>
        <p>Available in UAE pharmacies</p>
      </div>
    </div>

    <div class="section-title">After a hard shift at work</div>
    <div class="toolkit-grid">
      <div class="tool-card" onclick="openTool('walk')">
        <div class="tool-icon">🚶</div>
        <h4>Post-Shift Walk</h4>
        <p>20 min resets the brain</p>
      </div>
      <div class="tool-card" onclick="openTool('eat')">
        <div class="tool-icon">🍽️</div>
        <h4>Eat & Hydrate</h4>
        <p>Meth depletes everything</p>
      </div>
    </div>
  </div>

  <!-- LOG TAB -->
  <div class="tab" id="tab-log">
    <div class="header" style="padding-top:20px;">
      <h1>Your<br><em>progress log</em></h1>
      <p>Every check-in you save appears here.<br>Evidence that you're showing up for yourself.</p>
    </div>
    <div id="log-list"></div>
  </div>

</div><!-- /container -->

<!-- Bottom Nav -->
<nav class="bottom-nav">
  <button class="nav-btn active" id="nav-home" onclick="switchTab('home')">
    <span class="nav-icon">🏠</span>Home
  </button>
  <button class="nav-btn" id="nav-reconnect" onclick="switchTab('reconnect')">
    <span class="nav-icon">💙</span>Reconnect
  </button>
  <button class="nav-btn" id="nav-toolkit" onclick="switchTab('toolkit')">
    <span class="nav-icon">🛠️</span>Toolkit
  </button>
  <button class="nav-btn" id="nav-log" onclick="switchTab('log')">
    <span class="nav-icon">📖</span>Log
  </button>
</nav>

<!-- Tool Modals -->
<div class="modal-overlay" id="modal">
  <div class="modal">
    <h3 id="modal-title"></h3>
    <p id="modal-body"></p>
    <button class="modal-close" onclick="closeModal()">Got it ✓</button>
  </div>
</div>

<div class="toast" id="toast">✓ Check-in saved</div>

<script>
const tools = {
  '15min': {
    title: '⏱️ The 15-Minute Rule',
    body: 'When a craving hits, don\'t try to fight it or decide anything. Just say to yourself: "I will wait 15 minutes." Set a timer. Do something else — drink water, go outside, splash cold water on your face. Most cravings peak and pass within 15 minutes. You don\'t have to win forever. Just the next 15 minutes.'
  },
  'breath': {
    title: '🌬️ Box Breathing',
    body: 'Breathe IN for 4 counts. Hold for 4 counts. Breathe OUT for 4 counts. Hold for 4 counts. Repeat 4 times. This activates your parasympathetic nervous system and physically reduces the anxiety spike that comes with cravings. Do it in a bathroom stall at work if needed — no one will know.'
  },
  'grounding': {
    title: '🌿 5-4-3-2-1 Grounding',
    body: 'Name 5 things you can SEE right now. 4 things you can TOUCH. 3 things you can HEAR. 2 things you can SMELL. 1 thing you can TASTE. This technique pulls your brain out of craving-mode and back into the present moment. It works especially well during anxiety or when your mind starts to spiral.'
  },
  'urge': {
    title: '🌊 Urge Surfing',
    body: 'Instead of fighting the craving, observe it like a wave. Close your eyes and notice where you feel it in your body. Notice it rising — getting stronger. Know that like all waves, it will peak and then fall. You don\'t have to act on it. You\'re surfing it, not drowning in it. Most urges peak at 20–30 minutes then fade on their own.'
  },
  'sleep1': {
    title: '🌙 Wind-Down Routine',
    body: 'Start 30 minutes before bed: put your phone face-down, dim the lights, drink something warm (herbal tea or warm water), and do 5 minutes of slow breathing. During meth recovery, your brain needs consistent sleep signals. Even if you can\'t sleep, lying down and resting is still helping your brain heal.'
  },
  'sleep2': {
    title: '💊 Melatonin for Sleep',
    body: 'Melatonin 1–5mg is available without prescription at pharmacies in the UAE (look for it at Aster, Life, or Boots pharmacies). Take it 30–60 minutes before your planned sleep time. It helps reset your sleep-wake cycle which gets disrupted during meth recovery. Start with the lowest dose. It\'s not addictive.'
  },
  'walk': {
    title: '🚶 The Post-Shift Walk',
    body: 'After your restaurant shift, instead of going straight home (which can trigger old patterns), walk for 20 minutes first. Even a short walk around the block. This lowers cortisol, reduces cravings, burns off the adrenaline from work, and resets your mood. It\'s one of the most evidence-backed tools for early recovery.'
  },
  'eat': {
    title: '🍽️ Eat, Drink, Recover',
    body: 'Meth suppresses appetite and depletes your body of nutrients — especially dopamine precursors. In recovery, eating regularly (even small amounts) helps your brain start producing dopamine naturally again. Focus on: protein (eggs, chicken, fish), complex carbs, and lots of water. Working in a restaurant actually helps — access to food is right there.'
  }
};

let selectedMood = '';
let selectedSymptoms = [];

function selectMood(btn, mood) {
  document.querySelectorAll('.mood-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  selectedMood = mood;
}

function toggleSymptom(el, name) {
  el.classList.toggle('checked');
  if (el.classList.contains('checked')) {
    if (!selectedSymptoms.includes(name)) selectedSymptoms.push(name);
  } else {
    selectedSymptoms = selectedSymptoms.filter(s => s !== name);
  }
}

function saveCheckin() {
  if (!selectedMood) { alert('Please select how you\'re feeling today.'); return; }
  const note = document.getElementById('day-note').value.trim();
  const logs = JSON.parse(localStorage.getItem('recovery_logs') || '[]');
  const today = new Date().toISOString().split('T')[0];
  const entry = { date: today, mood: selectedMood, symptoms: [...selectedSymptoms], note };
  // Remove existing entry for today if any
  const filtered = logs.filter(l => l.date !== today);
  filtered.unshift(entry);
  localStorage.setItem('recovery_logs', JSON.stringify(filtered));

  // Update streak
  updateStreak(filtered);
  renderLog(filtered);

  // Reset form
  selectedMood = '';
  selectedSymptoms = [];
  document.querySelectorAll('.mood-btn').forEach(b => b.classList.remove('active'));
  document.querySelectorAll('.symptom-item').forEach(b => b.classList.remove('checked'));
  document.getElementById('day-note').value = '';

  showToast('✓ Check-in saved — well done for showing up today');
}

function updateStreak(logs) {
  let streak = 0;
  const today = new Date();
  for (let i = 0; i < 365; i++) {
    const d = new Date(today); d.setDate(today.getDate() - i);
    const ds = d.toISOString().split('T')[0];
    if (logs.find(l => l.date === ds)) streak++;
    else if (i > 0) break;
  }
  document.getElementById('streak-num').textContent = streak;
  const phrases = {
    0: ['Today is Day One 💙', 'Every hour you get through today matters. You don\'t have to be perfect — just present.'],
    1: ['Day 1 Complete 🌱', 'You did it. One whole day. Your brain is already starting to heal.'],
    3: ['3 Days Strong 🔥', 'The worst of the crash is easing. You\'ve proven you can do hard things.'],
    7: ['One Full Week ⭐', 'One week clean. Your sleep, mood, and energy are starting to stabilize.'],
    14: ['Two Weeks 💪', 'Two weeks in. The cravings are still there but they\'re getting shorter and less intense.'],
    30: ['30 Days — One Month 🏆', 'A month of fighting for yourself. Your family is going to see a different person.'],
  };
  const keys = Object.keys(phrases).map(Number).sort((a,b)=>b-a);
  for (const k of keys) { if (streak >= k) { document.getElementById('streak-phrase').textContent = phrases[k][0]; document.getElementById('streak-sub').textContent = phrases[k][1]; break; } }
  const milestones = [1,3,7,14,30,60,90];
  milestones.forEach(m => { const el = document.getElementById('m'+m); if (el) el.classList.toggle('reached', streak >= m); });
  const next = milestones.find(m => streak < m) || 90;
  document.getElementById('prog-next').textContent = 'Next: Day ' + next;
  const prev = milestones.filter(m => m <= streak).pop() || 0;
  const pct = Math.min(100, ((streak - prev) / (next - prev)) * 100);
  document.getElementById('prog-fill').style.width = pct + '%';
}

function renderLog(logs) {
  const el = document.getElementById('log-list');
  if (!logs.length) { el.innerHTML = '<div class="empty"><div class="e-icon">📖</div>No check-ins yet. Your log will appear here after your first save.</div>'; return; }
  el.innerHTML = logs.map(l => `
    <div class="log-entry">
      <div class="log-date">${l.date.slice(5)}</div>
      <div class="log-content">
        <div class="log-mood">${l.mood}</div>
        ${l.note ? `<div class="log-note">${l.note}</div>` : ''}
        ${l.symptoms.length ? `<div class="log-symptoms">${l.symptoms.map(s=>`<span class="log-tag">${s}</span>`).join('')}</div>` : ''}
      </div>
    </div>
  `).join('');
}

function toggleStep(id) {
  const el = document.getElementById(id);
  el.classList.toggle('done');
  const num = el.querySelector('.step-num');
  num.textContent = el.classList.contains('done') ? '✓' : id.replace('rs','');
}

function openTool(key) {
  const t = tools[key];
  document.getElementById('modal-title').textContent = t.title;
  document.getElementById('modal-body').textContent = t.body;
  document.getElementById('modal').classList.add('open');
}
function closeModal() { document.getElementById('modal').classList.remove('open'); }
document.getElementById('modal').addEventListener('click', e => { if (e.target === document.getElementById('modal')) closeModal(); });

function switchTab(name) {
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-'+name).classList.add('active');
  document.getElementById('nav-'+name).classList.add('active');
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

// Init
const d = new Date();
document.getElementById('today-date').textContent = d.toLocaleDateString('en-GB', {day:'numeric',month:'short'});
const logs = JSON.parse(localStorage.getItem('recovery_logs') || '[]');
updateStreak(logs);
renderLog(logs);
</script>
</body>
</html>