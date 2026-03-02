<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="theme-color" content="#6C63FF">
<meta name="description" content="SpellStar - Fun spelling practice game for kids!">
<title>⭐ SpellStar ⭐</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@700;800;900&display=swap" rel="stylesheet">

<style>
:root {
  --purple: #6C63FF;
  --coral: #FF6B6B;
  --teal: #4ECDC4;
  --yellow: #FFE66D;
  --green: #6BCB77;
  --orange: #FF9F1C;
  --pink: #FF85A1;
  --bg: #1a1a2e;
  --card: rgba(255,255,255,0.12);
  --white: #FFFFFF;
  --radius: 24px;
  --shadow: 0 8px 32px rgba(0,0,0,0.3);
}

* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

body {
  font-family: 'Nunito', sans-serif;
  background: #1a1a2e;
  min-height: 100dvh;
  overflow-x: hidden;
  position: relative;
  color: white;
}

/* ====== ANIMATED BACKGROUND ====== */
.bg-stars {
  position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background: 
    radial-gradient(ellipse at 20% 50%, #16213e 0%, transparent 60%),
    radial-gradient(ellipse at 80% 20%, #0f3460 0%, transparent 50%),
    linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
}
.bg-stars::before, .bg-stars::after {
  content:''; position:absolute; inset:0;
  background-image: 
    radial-gradient(2px 2px at 20px 30px, rgba(255,255,255,0.4), transparent),
    radial-gradient(2px 2px at 40px 70px, rgba(255,255,255,0.3), transparent),
    radial-gradient(2px 2px at 80px 10px, rgba(255,255,255,0.5), transparent),
    radial-gradient(1px 1px at 120px 50px, rgba(255,255,255,0.3), transparent),
    radial-gradient(2px 2px at 160px 30px, rgba(255,255,255,0.4), transparent),
    radial-gradient(1px 1px at 200px 80px, rgba(255,255,255,0.2), transparent),
    radial-gradient(2px 2px at 240px 20px, rgba(255,255,255,0.5), transparent),
    radial-gradient(1px 1px at 280px 60px, rgba(255,255,255,0.3), transparent),
    radial-gradient(2px 2px at 320px 40px, rgba(255,255,255,0.4), transparent),
    radial-gradient(1px 1px at 360px 10px, rgba(255,255,255,0.2), transparent),
    radial-gradient(2px 2px at 400px 70px, rgba(255,255,255,0.3), transparent),
    radial-gradient(1px 1px at 440px 30px, rgba(255,255,255,0.4), transparent);
  background-size: 450px 100px;
  animation: twinkle 4s infinite alternate;
}
.bg-stars::after { animation-delay: 2s; background-size: 350px 80px; opacity: 0.7; }
@keyframes twinkle { from {opacity:0.6} to {opacity:1} }

/* Floating orbs */
.orb {
  position: fixed; border-radius: 50%; filter: blur(60px); pointer-events: none; z-index: 0;
  animation: floatOrb 8s ease-in-out infinite;
}
.orb-1 { width:300px; height:300px; background: rgba(108,99,255,0.25); top:-100px; left:-100px; }
.orb-2 { width:200px; height:200px; background: rgba(255,107,107,0.2); bottom:-50px; right:-50px; animation-delay:-3s; }
.orb-3 { width:150px; height:150px; background: rgba(78,205,196,0.2); top:50%; left:60%; animation-delay:-5s; }
@keyframes floatOrb { 0%,100%{transform:translate(0,0)} 50%{transform:translate(30px,-30px)} }

/* ====== LAYOUT ====== */
#app { position: relative; z-index: 1; min-height: 100dvh; }

.screen { display: none; flex-direction: column; align-items: center; justify-content: center; min-height: 100dvh; padding: 20px; }
.screen.active { display: flex; }

/* ====== SETUP SCREEN ====== */
.logo {
  font-family: 'Fredoka One', cursive;
  font-size: clamp(52px, 10vw, 88px);
  line-height: 1;
  background: linear-gradient(135deg, var(--yellow) 0%, var(--orange) 40%, var(--coral) 70%, var(--pink) 100%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  filter: drop-shadow(0 4px 20px rgba(255,107,107,0.4));
  animation: logoBounce 2s ease-in-out infinite;
  letter-spacing: 2px;
}
@keyframes logoBounce { 0%,100%{transform:translateY(0) rotate(-1deg)} 50%{transform:translateY(-8px) rotate(1deg)} }

.logo-sub {
  font-family: 'Fredoka One', cursive;
  font-size: clamp(14px, 3vw, 20px);
  color: var(--teal);
  letter-spacing: 4px;
  text-transform: uppercase;
  margin-top: -8px;
  margin-bottom: 32px;
  opacity: 0.9;
}

.mascot { font-size: 80px; animation: mascotBounce 1.5s ease-in-out infinite; display: block; }
@keyframes mascotBounce { 0%,100%{transform:translateY(0) scale(1)} 50%{transform:translateY(-15px) scale(1.05)} }

.card {
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255,255,255,0.15);
  border-radius: var(--radius);
  padding: 28px;
  box-shadow: var(--shadow);
  width: 100%;
  max-width: 520px;
}

.card-title {
  font-family: 'Fredoka One', cursive;
  font-size: 22px;
  color: var(--yellow);
  margin-bottom: 12px;
  text-align: center;
}

textarea {
  width: 100%;
  background: rgba(255,255,255,0.1);
  border: 2px solid rgba(255,255,255,0.2);
  border-radius: 16px;
  color: white;
  font-family: 'Nunito', sans-serif;
  font-size: 16px;
  font-weight: 700;
  padding: 14px 16px;
  resize: vertical;
  min-height: 120px;
  transition: border-color 0.3s;
  outline: none;
}
textarea:focus { border-color: var(--purple); }
textarea::placeholder { color: rgba(255,255,255,0.35); }

.word-count {
  text-align: right;
  font-size: 13px;
  color: rgba(255,255,255,0.5);
  margin-top: 6px;
  font-weight: 700;
}
.word-count.ok { color: var(--green); }
.word-count.bad { color: var(--coral); }

.hint-text {
  font-size: 13px;
  color: rgba(255,255,255,0.45);
  text-align: center;
  margin-top: 8px;
}

.btn {
  font-family: 'Fredoka One', cursive;
  font-size: 22px;
  letter-spacing: 1px;
  border: none;
  border-radius: 100px;
  padding: 16px 40px;
  cursor: pointer;
  transition: all 0.2s;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  position: relative;
  overflow: hidden;
}
.btn::after {
  content:''; position:absolute; inset:0; background:white; opacity:0;
  transition: opacity 0.2s;
}
.btn:active::after { opacity: 0.15; }
.btn:hover { transform: translateY(-3px) scale(1.03); }
.btn:active { transform: translateY(0) scale(0.97); }

.btn-primary {
  background: linear-gradient(135deg, var(--purple), var(--coral));
  color: white;
  box-shadow: 0 8px 24px rgba(108,99,255,0.5), 0 0 0 0 rgba(108,99,255,0.5);
  animation: pulseGlow 2s ease-in-out infinite;
}
@keyframes pulseGlow {
  0%,100%{box-shadow:0 8px 24px rgba(108,99,255,0.4)}
  50%{box-shadow:0 8px 40px rgba(255,107,107,0.6), 0 0 60px rgba(108,99,255,0.3)}
}
.btn-teal { background: linear-gradient(135deg, var(--teal), var(--green)); color: #1a1a2e; box-shadow: 0 6px 20px rgba(78,205,196,0.4); }
.btn-yellow { background: linear-gradient(135deg, var(--yellow), var(--orange)); color: #1a1a2e; box-shadow: 0 6px 20px rgba(255,230,109,0.4); }
.btn-sm { font-size: 16px; padding: 10px 24px; }
.btn-disabled { opacity: 0.4; pointer-events: none; cursor: not-allowed; }

/* ====== LEVEL SELECTOR ====== */
.level-cards { display: flex; gap: 12px; flex-wrap: wrap; justify-content: center; margin: 20px 0; }
.level-card {
  flex: 1; min-width: 130px; max-width: 150px;
  background: rgba(255,255,255,0.08);
  border: 2px solid rgba(255,255,255,0.1);
  border-radius: 18px;
  padding: 16px 12px;
  text-align: center;
  cursor: pointer;
  transition: all 0.25s;
}
.level-card:hover { transform: translateY(-4px); border-color: rgba(255,255,255,0.3); }
.level-card.selected { border-color: var(--yellow); background: rgba(255,230,109,0.15); }
.level-card-icon { font-size: 32px; display: block; margin-bottom: 6px; }
.level-card-name { font-family: 'Fredoka One', cursive; font-size: 14px; color: var(--yellow); }
.level-card-desc { font-size: 11px; color: rgba(255,255,255,0.5); margin-top: 4px; }

/* ====== GAME SCREEN ====== */
.game-header {
  width: 100%; max-width: 700px;
  display: flex; align-items: center; justify-content: space-between;
  margin-bottom: 16px; padding: 0 4px;
}

.progress-bar-wrap {
  flex: 1; background: rgba(255,255,255,0.15); border-radius: 100px; height: 10px; margin: 0 12px;
}
.progress-bar { height: 100%; border-radius: 100px; background: linear-gradient(90deg, var(--teal), var(--purple)); transition: width 0.6s ease; }

.word-num {
  font-family: 'Fredoka One', cursive;
  font-size: 15px; color: rgba(255,255,255,0.6); white-space: nowrap;
}

.lives {
  display: flex; gap: 4px; font-size: 22px;
}

/* Level badge */
.level-badge {
  display: inline-flex; align-items: center; gap: 6px;
  background: rgba(255,255,255,0.1);
  border: 1px solid rgba(255,255,255,0.2);
  border-radius: 100px;
  padding: 4px 14px;
  font-family: 'Fredoka One', cursive;
  font-size: 14px;
  color: var(--yellow);
  margin-bottom: 10px;
}
.level-badge-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--yellow); }

/* Word display card */
.word-card {
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255,255,255,0.15);
  border-radius: 28px;
  padding: 28px 32px;
  width: 100%; max-width: 680px;
  text-align: center;
  box-shadow: var(--shadow);
  animation: cardIn 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
}
@keyframes cardIn { from{opacity:0; transform:scale(0.85) translateY(20px)} to{opacity:1; transform:scale(1) translateY(0)} }

.emoji-hint {
  font-size: clamp(60px, 15vw, 100px);
  display: block;
  margin-bottom: 8px;
  animation: emojiPop 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
  filter: drop-shadow(0 6px 20px rgba(0,0,0,0.3));
}
@keyframes emojiPop { from{transform:scale(0) rotate(-15deg)} to{transform:scale(1) rotate(0)} }

.speak-btn {
  background: linear-gradient(135deg, var(--purple), var(--pink));
  border: none;
  border-radius: 100px;
  color: white;
  font-family: 'Fredoka One', cursive;
  font-size: 18px;
  padding: 12px 28px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  transition: all 0.2s;
  box-shadow: 0 4px 16px rgba(108,99,255,0.4);
  animation: speakPulse 2s ease-in-out infinite;
  margin-bottom: 20px;
}
.speak-btn:hover { transform: scale(1.05); }
.speak-btn:active { transform: scale(0.95); }
@keyframes speakPulse { 0%,100%{box-shadow:0 4px 16px rgba(108,99,255,0.4)} 50%{box-shadow:0 4px 30px rgba(255,133,161,0.6)} }

.speak-icon { font-size: 22px; animation: speakWave 1s ease-in-out infinite; }
@keyframes speakWave { 0%,100%{transform:scale(1)} 50%{transform:scale(1.2)} }

/* ====== LEVEL 1: MULTIPLE CHOICE ====== */
.choices { display: flex; flex-direction: column; gap: 12px; width: 100%; }

.choice-btn {
  width: 100%;
  background: rgba(255,255,255,0.1);
  border: 2px solid rgba(255,255,255,0.15);
  border-radius: 16px;
  color: white;
  font-family: 'Nunito', sans-serif;
  font-weight: 900;
  font-size: clamp(18px, 4vw, 26px);
  padding: 16px 24px;
  cursor: pointer;
  transition: all 0.2s;
  letter-spacing: 2px;
  text-transform: uppercase;
}
.choice-btn:hover { background: rgba(255,255,255,0.18); border-color: var(--purple); transform: scale(1.02); }
.choice-btn.correct-anim { background: rgba(107, 203, 119, 0.3); border-color: var(--green); animation: correctShake 0.4s; }
.choice-btn.wrong-anim { background: rgba(255,107,107,0.25); border-color: var(--coral); animation: wrongShake 0.4s; }
@keyframes correctShake { 0%,100%{transform:scale(1)} 50%{transform:scale(1.05)} }
@keyframes wrongShake { 0%,100%{transform:translateX(0)} 20%,60%{transform:translateX(-8px)} 40%,80%{transform:translateX(8px)} }

/* ====== LEVEL 2: LETTER BUILD ====== */
.build-answer {
  min-height: 64px;
  background: rgba(0,0,0,0.25);
  border: 2px dashed rgba(255,255,255,0.25);
  border-radius: 18px;
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  padding: 12px;
  margin-bottom: 16px;
  align-items: center;
  justify-content: center;
  transition: border-color 0.3s;
}
.build-answer.has-letters { border-color: rgba(108,99,255,0.5); border-style: solid; }
.answer-placeholder { color: rgba(255,255,255,0.25); font-family: 'Fredoka One', cursive; font-size: 16px; }

.letter-pool {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
  margin-bottom: 16px;
}

.letter-tile {
  width: 52px; height: 58px;
  background: linear-gradient(135deg, rgba(108,99,255,0.6), rgba(255,107,107,0.4));
  border: 2px solid rgba(255,255,255,0.3);
  border-radius: 12px;
  color: white;
  font-family: 'Fredoka One', cursive;
  font-size: 26px;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer;
  transition: all 0.18s cubic-bezier(0.34, 1.56, 0.64, 1);
  box-shadow: 0 4px 12px rgba(0,0,0,0.3), inset 0 1px 0 rgba(255,255,255,0.2);
  user-select: none;
  text-transform: uppercase;
}
.letter-tile:hover { transform: translateY(-6px) scale(1.12); box-shadow: 0 10px 24px rgba(0,0,0,0.4); }
.letter-tile:active { transform: scale(0.9); }
.letter-tile.used { opacity: 0.25; pointer-events: none; transform: scale(0.85); }
.letter-tile.answer-tile {
  background: linear-gradient(135deg, rgba(78,205,196,0.6), rgba(107,203,119,0.5));
  border-color: rgba(78,205,196,0.6);
  cursor: pointer;
}
.letter-tile.answer-tile:hover { transform: translateY(-4px) scale(1.08); }

.build-controls { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; }

/* ====== LEVEL 3: TYPE ====== */
.type-input-wrap { position: relative; width: 100%; margin-bottom: 16px; }
.type-input {
  width: 100%;
  background: rgba(255,255,255,0.08);
  border: 3px solid rgba(108,99,255,0.5);
  border-radius: 18px;
  color: white;
  font-family: 'Fredoka One', cursive;
  font-size: clamp(28px, 6vw, 42px);
  padding: 16px 24px;
  text-align: center;
  letter-spacing: 6px;
  text-transform: uppercase;
  outline: none;
  transition: border-color 0.3s;
}
.type-input:focus { border-color: var(--purple); box-shadow: 0 0 0 4px rgba(108,99,255,0.2); }
.type-input::placeholder { color: rgba(255,255,255,0.2); font-size: 18px; letter-spacing: 2px; }
.type-input.correct-anim { border-color: var(--green); box-shadow: 0 0 0 4px rgba(107,203,119,0.25); }
.type-input.wrong-anim { border-color: var(--coral); box-shadow: 0 0 0 4px rgba(255,107,107,0.25); animation: wrongShake 0.4s; }

/* ====== HINT ====== */
.hint-box {
  background: rgba(255,230,109,0.15);
  border: 2px solid rgba(255,230,109,0.4);
  border-radius: 14px;
  padding: 10px 20px;
  font-family: 'Fredoka One', cursive;
  font-size: 16px;
  color: var(--yellow);
  margin-bottom: 16px;
  animation: hintPop 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  display: flex; align-items: center; gap: 8px;
}
@keyframes hintPop { from{transform:scale(0.5);opacity:0} to{transform:scale(1);opacity:1} }

/* ====== FEEDBACK OVERLAY ====== */
#feedback-overlay {
  position: fixed; inset: 0; z-index: 100;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.3s;
}
#feedback-overlay.show { opacity: 1; pointer-events: all; }

.feedback-bubble {
  background: white;
  border-radius: 30px;
  padding: 30px 50px;
  text-align: center;
  transform: scale(0);
  transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  box-shadow: 0 20px 60px rgba(0,0,0,0.4);
}
#feedback-overlay.show .feedback-bubble { transform: scale(1); }

.feedback-emoji { font-size: 80px; display: block; animation: feedbackBounce 0.5s infinite alternate; }
@keyframes feedbackBounce { from{transform:scale(1)} to{transform:scale(1.15)} }
.feedback-text {
  font-family: 'Fredoka One', cursive;
  font-size: 42px;
  margin: 8px 0 4px;
}
.feedback-sub { font-family: 'Nunito', sans-serif; font-weight: 800; font-size: 20px; color: rgba(0,0,0,0.6); }

/* ====== STAR SCORE ====== */
.star-score { display: flex; gap: 6px; justify-content: center; margin-bottom: 12px; }
.star-score span { font-size: 28px; transition: all 0.3s; }
.star-score span.earned { animation: starEarn 0.4s cubic-bezier(0.34, 1.56, 0.64, 1); }
@keyframes starEarn { 0%{transform:scale(0) rotate(-30deg)} 100%{transform:scale(1) rotate(0)} }

/* ====== CONFETTI ====== */
#confetti-canvas { position: fixed; inset: 0; z-index: 200; pointer-events: none; }

/* ====== COMPLETE SCREEN ====== */
.complete-hero {
  font-size: 100px; display: block;
  animation: completeHero 1s cubic-bezier(0.34, 1.56, 0.64, 1);
}
@keyframes completeHero { from{transform:scale(0) rotate(-20deg)} to{transform:scale(1) rotate(0)} }

.complete-title {
  font-family: 'Fredoka One', cursive;
  font-size: clamp(36px, 8vw, 64px);
  background: linear-gradient(135deg, var(--yellow), var(--orange), var(--coral));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  text-align: center; line-height: 1.1; margin-bottom: 8px;
}

.score-display {
  font-family: 'Fredoka One', cursive;
  font-size: 48px;
  color: white;
  text-align: center;
  margin: 8px 0;
}
.score-display span { color: var(--yellow); font-size: 64px; }

.word-results {
  max-height: 220px; overflow-y: auto;
  display: flex; flex-wrap: wrap; gap: 8px;
  justify-content: center; margin: 16px 0;
}
.word-result-pill {
  background: rgba(255,255,255,0.1);
  border-radius: 100px;
  padding: 6px 16px;
  font-family: 'Nunito', sans-serif;
  font-weight: 800;
  font-size: 15px;
  display: flex; align-items: center; gap: 6px;
}

/* ====== RESPONSIVE ====== */
@media (max-width: 480px) {
  .word-card { padding: 20px 16px; }
  .letter-tile { width: 44px; height: 50px; font-size: 22px; }
  .choice-btn { font-size: 18px; padding: 14px 16px; }
  .type-input { font-size: 26px; letter-spacing: 4px; }
  .btn { font-size: 18px; padding: 14px 28px; }
}

/* ====== TRANSITION ANIMATIONS ====== */
.fade-in { animation: fadeIn 0.4s ease forwards; }
@keyframes fadeIn { from{opacity:0;transform:translateY(10px)} to{opacity:1;transform:translateY(0)} }

.spin { animation: spin 0.5s ease; }
@keyframes spin { from{transform:rotate(0deg)} to{transform:rotate(360deg)} }
</style>
</head>
<body>
<div class="bg-stars"></div>
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>
<canvas id="confetti-canvas"></canvas>
<div id="feedback-overlay">
  <div class="feedback-bubble" id="feedback-bubble">
    <span class="feedback-emoji" id="feedback-emoji"></span>
    <div class="feedback-text" id="feedback-text"></div>
    <div class="feedback-sub" id="feedback-sub"></div>
  </div>
</div>

<div id="app">

  <!-- ===== SETUP SCREEN ===== -->
  <div class="screen active" id="screen-setup">
    <div class="mascot">🌟</div>
    <div class="logo">SpellStar</div>
    <div class="logo-sub">Spelling Adventure!</div>

    <div class="card fade-in">
      <div class="card-title">📝 Enter Your Words</div>
      <textarea id="word-input" placeholder="cat dog apple tree happy... (5 to 30 words)" rows="4" autocomplete="off" autocapitalize="none" spellcheck="false"></textarea>
      <div class="word-count" id="word-count">Type your words above</div>
      <div class="hint-text">Separate words with spaces, commas, or new lines</div>
    </div>

    <div class="card fade-in" style="margin-top:14px">
      <div class="card-title">🎮 Choose Your Level</div>
      <div class="level-cards">
        <div class="level-card selected" data-level="1">
          <span class="level-card-icon">🔤</span>
          <div class="level-card-name">Level 1</div>
          <div class="level-card-desc">Pick the right spelling!</div>
        </div>
        <div class="level-card" data-level="2">
          <span class="level-card-icon">🧩</span>
          <div class="level-card-name">Level 2</div>
          <div class="level-card-desc">Build it with letters!</div>
        </div>
        <div class="level-card" data-level="3">
          <span class="level-card-icon">⌨️</span>
          <div class="level-card-name">Level 3</div>
          <div class="level-card-desc">Type it from memory!</div>
        </div>
      </div>
    </div>

    <button class="btn btn-primary btn-disabled" id="start-btn" style="margin-top:20px">
      🚀 Let's Go!
    </button>
  </div>

  <!-- ===== GAME SCREEN ===== -->
  <div class="screen" id="screen-game">
    <div class="game-header">
      <div class="word-num" id="word-num">1 / 10</div>
      <div class="progress-bar-wrap">
        <div class="progress-bar" id="progress-bar" style="width:0%"></div>
      </div>
      <div class="lives" id="lives">❤️❤️❤️</div>
    </div>

    <div class="level-badge" id="level-badge">
      <div class="level-badge-dot"></div>
      <span id="level-name">Level 1 – Match It!</span>
    </div>

    <div class="word-card" id="word-card">
      <span class="emoji-hint" id="emoji-hint">🌟</span>
      <button class="speak-btn" id="speak-btn" onclick="speakWord()">
        <span class="speak-icon">🔊</span> Hear the word
      </button>

      <!-- Star score display -->
      <div class="star-score" id="star-score">
        <span>⭐</span><span>⭐</span><span>⭐</span>
      </div>

      <!-- Hint box (hidden by default) -->
      <div class="hint-box" id="hint-box" style="display:none">
        💡 Hint: The word starts with "<span id="hint-letter"></span>"
      </div>

      <!-- Level 1: Multiple choice -->
      <div id="level1-area" style="display:none">
        <div class="choices" id="choices"></div>
      </div>

      <!-- Level 2: Build with letters -->
      <div id="level2-area" style="display:none">
        <div class="build-answer" id="build-answer">
          <span class="answer-placeholder">Tap letters to spell the word ⬇️</span>
        </div>
        <div class="letter-pool" id="letter-pool"></div>
        <div class="build-controls">
          <button class="btn btn-sm" onclick="clearAnswer()" style="background:rgba(255,107,107,0.3);border:2px solid var(--coral);">🗑️ Clear</button>
          <button class="btn btn-teal btn-sm" id="build-check-btn" onclick="checkBuild()">✓ Check!</button>
        </div>
      </div>

      <!-- Level 3: Type it -->
      <div id="level3-area" style="display:none">
        <div class="type-input-wrap">
          <input type="text" class="type-input" id="type-input"
            placeholder="Type the word here..."
            autocomplete="off" autocapitalize="none"
            autocorrect="off" spellcheck="false">
        </div>
        <button class="btn btn-teal" id="type-check-btn" onclick="checkType()">✓ Check!</button>
      </div>
    </div>

    <button class="btn btn-sm" onclick="skipWord()" style="margin-top:16px; background:rgba(255,255,255,0.08); border:1px solid rgba(255,255,255,0.2); color:rgba(255,255,255,0.5); font-size:14px; padding:8px 20px;">
      Skip word ⏭️
    </button>
  </div>

  <!-- ===== COMPLETE SCREEN ===== -->
  <div class="screen" id="screen-complete">
    <span class="complete-hero" id="complete-emoji">🏆</span>
    <div class="complete-title" id="complete-title">Amazing Job!</div>
    <div class="score-display">You scored <span id="final-score">0</span> stars!</div>

    <div class="card fade-in" style="margin-top:16px; width:100%; max-width:520px;">
      <div class="card-title" style="margin-bottom:12px;">📋 Word Results</div>
      <div class="word-results" id="word-results"></div>
    </div>

    <div style="display:flex; gap:12px; flex-wrap:wrap; justify-content:center; margin-top:20px;">
      <button class="btn btn-primary" onclick="playAgain()">🔁 Play Again!</button>
      <button class="btn btn-yellow" onclick="newWords()">✏️ New Words</button>
    </div>
  </div>

</div>

<script>
// ===========================
//  EMOJI HINT DATABASE
// ===========================
const emojiDB = {
  // Animals
  cat:'🐱',dog:'🐶',fish:'🐟',bird:'🐦',duck:'🦆',frog:'🐸',bear:'🐻',lion:'🦁',
  tiger:'🐯',horse:'🐴',pig:'🐷',cow:'🐮',sheep:'🐑',hen:'🐔',fox:'🦊',owl:'🦉',
  bat:'🦇',ant:'🐜',bee:'🐝',bug:'🐛',snake:'🐍',wolf:'🐺',deer:'🦌',mouse:'🐭',
  rat:'🐀',rabbit:'🐰',bunny:'🐰',squirrel:'🐿️',elephant:'🐘',monkey:'🐒',gorilla:'🦍',
  giraffe:'🦒',zebra:'🦓',penguin:'🐧',parrot:'🦜',eagle:'🦅',whale:'🐳',shark:'🦈',
  octopus:'🐙',crab:'🦀',lobster:'🦞',butterfly:'🦋',caterpillar:'🐛',snail:'🐌',
  turtle:'🐢',crocodile:'🐊',dinosaur:'🦕',dragon:'🐲',unicorn:'🦄',
  // Food & drink
  apple:'🍎',banana:'🍌',orange:'🍊',grape:'🍇',strawberry:'🍓',cherry:'🍒',
  lemon:'🍋',mango:'🥭',pear:'🍐',peach:'🍑',pineapple:'🍍',watermelon:'🍉',
  melon:'🍈',kiwi:'🥝',coconut:'🥥',tomato:'🍅',corn:'🌽',carrot:'🥕',
  potato:'🥔',broccoli:'🥦',pizza:'🍕',burger:'🍔',taco:'🌮',sushi:'🍣',
  cake:'🎂',cookie:'🍪',donut:'🍩',candy:'🍬',chocolate:'🍫',icecream:'🍦',
  ice:'🧊',milk:'🥛',juice:'🧃',coffee:'☕',tea:'🍵',bread:'🍞',egg:'🥚',
  cheese:'🧀',rice:'🍚',noodle:'🍜',soup:'🥣',pie:'🥧',sandwich:'🥪',
  // Colors
  red:'🔴',blue:'🔵',green:'🟢',yellow:'🟡',orange:'🟠',purple:'🟣',
  black:'⚫',white:'⚪',brown:'🟤',pink:'🩷',
  // Nature
  sun:'☀️',moon:'🌙',star:'⭐',cloud:'☁️',rain:'🌧️',snow:'❄️',wind:'💨',
  storm:'⛈️',flower:'🌸',rose:'🌹',tree:'🌳',leaf:'🍃',grass:'🌿',cactus:'🌵',
  mushroom:'🍄',earth:'🌍',fire:'🔥',water:'💧',ocean:'🌊',mountain:'⛰️',
  volcano:'🌋',island:'🏝️',cave:'🕳️',
  // Places & buildings
  house:'🏠',home:'🏠',school:'🏫',hospital:'🏥',castle:'🏰',tower:'🗼',
  church:'⛪',tent:'⛺',barn:'🏚️',bridge:'🌉',city:'🏙️',park:'🏞️',
  beach:'🏖️',farm:'🌾',garden:'🏡',
  // Transport
  car:'🚗',bus:'🚌',train:'🚂',plane:'✈️',boat:'⛵',ship:'🚢',
  rocket:'🚀',bike:'🚲',truck:'🚚',helicopter:'🚁',submarine:'🤿',
  tractor:'🚜',ambulance:'🚑',taxi:'🚕',
  // Sports & games
  ball:'⚽',football:'🏈',basketball:'🏀',tennis:'🎾',golf:'⛳',swim:'🏊',
  run:'🏃',jump:'🤸',ski:'⛷️',skate:'⛸️',dance:'💃',
  // Objects
  book:'📚',pen:'✏️',pencil:'✏️',scissors:'✂️',ruler:'📏',bag:'👜',
  hat:'🎩',shoe:'👟',sock:'🧦',shirt:'👕',dress:'👗',glasses:'👓',
  phone:'📱',computer:'💻',camera:'📷',music:'🎵',guitar:'🎸',piano:'🎹',
  drum:'🥁',trumpet:'🎺',violin:'🎻',
  // People
  baby:'👶',girl:'👧',boy:'👦',woman:'👩',man:'👨',family:'👨‍👩‍👧‍👦',
  king:'🤴',queen:'👸',wizard:'🧙',fairy:'🧚',
  // Emotions
  happy:'😊',sad:'😢',angry:'😠',scared:'😨',love:'❤️',laugh:'😂',
  sleep:'😴',sick:'🤒',cool:'😎',
  // Numbers & letters
  one:'1️⃣',two:'2️⃣',three:'3️⃣',four:'4️⃣',five:'5️⃣',
  // Space
  planet:'🪐',rocket:'🚀',alien:'👽',telescope:'🔭',
  // Body
  hand:'✋',foot:'🦶',eye:'👁️',ear:'👂',nose:'👃',mouth:'👄',heart:'❤️',brain:'🧠',
  // Weather
  rainbow:'🌈',lightning:'⚡',tornado:'🌪️',
  // Misc fun
  robot:'🤖',ghost:'👻',monster:'👹',zombie:'🧟',witch:'🧙‍♀️',
  gift:'🎁',party:'🎉',balloon:'🎈',crown:'👑',trophy:'🏆',medal:'🥇',
  key:'🔑',lock:'🔒',magic:'✨',wand:'🪄',map:'🗺️',compass:'🧭',
  crystal:'🔮',diamond:'💎',gold:'🏅',treasure:'💰',
  // Common sight words
  the:'📖',a:'🅰️',is:'❓',it:'💡',in:'📥',on:'📌',at:'📍',
  up:'⬆️',go:'🚦',do:'✅',to:'➡️',so:'💬',no:'🚫',yes:'✅',
  // More common words  
  big:'🐘',little:'🐭',small:'🐭',tall:'🦒',short:'🐧',fast:'🐆',slow:'🐢',
  hot:'🔥',cold:'🧊',wet:'💧',dry:'☀️',
  old:'🧓',new:'✨',good:'👍',bad:'👎',
  night:'🌙',day:'☀️',morning:'🌅',evening:'🌆',
  light:'💡',dark:'🌑',
  open:'📂',close:'📁',
  play:'🎮',read:'📚',write:'✍️',draw:'🎨',sing:'🎤',
  eat:'🍽️',drink:'🥤',sleep:'😴',walk:'🚶',sit:'🪑',
  help:'🤝',stop:'🛑',wait:'⏳',look:'👀',listen:'👂',
  think:'💭',know:'🧠',want:'🙋',need:'💡',like:'❤️',love:'💖',
  make:'🔨',take:'🤲',give:'🎁',put:'📥',get:'📤',
  see:'👁️',find:'🔍',say:'💬',tell:'📢',call:'📞',
  work:'⚙️',live:'🏠',move:'🏃',turn:'🔄',show:'👀',
  clean:'🧹',cook:'🍳',plant:'🌱',build:'🏗️',paint:'🎨',
};

function getEmoji(word) {
  const w = word.toLowerCase().trim();
  return emojiDB[w] || '✨';
}

// ===========================
//  GAME STATE
// ===========================
let words = [];
let wordEmojis = [];
let currentWordIdx = 0;
let currentLevel = 1;
let wrongAttempts = 0;
let wordScores = [];
let tileMap = []; // for level 2: {letter, idx, used}
let answerTiles = []; // for level 2: [{letter, poolIdx}]
let isAnimating = false;
let selectedStartLevel = 1;

// ===========================
//  SETUP
// ===========================
document.querySelectorAll('.level-card').forEach(card => {
  card.addEventListener('click', () => {
    document.querySelectorAll('.level-card').forEach(c => c.classList.remove('selected'));
    card.classList.add('selected');
    selectedStartLevel = parseInt(card.dataset.level);
  });
});

const wordInput = document.getElementById('word-input');
const wordCount = document.getElementById('word-count');
const startBtn = document.getElementById('start-btn');

wordInput.addEventListener('input', updateWordCount);

function parseWords(text) {
  return text.split(/[\s,\n]+/).map(w => w.trim().toLowerCase()).filter(w => w.length > 0 && /^[a-zA-Z]+$/.test(w));
}

function updateWordCount() {
  const parsed = parseWords(wordInput.value);
  const n = parsed.length;
  if (n === 0) {
    wordCount.textContent = 'Type your words above';
    wordCount.className = 'word-count';
    startBtn.classList.add('btn-disabled');
  } else if (n < 5) {
    wordCount.textContent = `${n} word${n>1?'s':''} – need at least 5`;
    wordCount.className = 'word-count bad';
    startBtn.classList.add('btn-disabled');
  } else if (n > 30) {
    wordCount.textContent = `${n} words – maximum is 30`;
    wordCount.className = 'word-count bad';
    startBtn.classList.add('btn-disabled');
  } else {
    wordCount.textContent = `✅ ${n} word${n>1?'s':''} ready to go!`;
    wordCount.className = 'word-count ok';
    startBtn.classList.remove('btn-disabled');
  }
}

startBtn.addEventListener('click', () => {
  const parsed = parseWords(wordInput.value);
  if (parsed.length < 5 || parsed.length > 30) return;
  words = parsed;
  wordEmojis = words.map(getEmoji);
  wordScores = words.map(() => ({stars: 3, levelsPassed: [], attempts: 0}));
  currentWordIdx = 0;
  currentLevel = selectedStartLevel;
  wrongAttempts = 0;
  showScreen('screen-game');
  loadWord();
});

// ===========================
//  SCREEN MANAGEMENT
// ===========================
function showScreen(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

// ===========================
//  SPEECH
// ===========================
function speakWord() {
  if (!words[currentWordIdx]) return;
  const utter = new SpeechSynthesisUtterance(words[currentWordIdx]);
  utter.rate = 0.75;
  utter.pitch = 1.1;
  speechSynthesis.cancel();
  speechSynthesis.speak(utter);
  const btn = document.getElementById('speak-btn');
  btn.style.transform = 'scale(1.15)';
  setTimeout(() => btn.style.transform = '', 200);
}

// ===========================
//  AUDIO FEEDBACK
// ===========================
let audioCtx = null;
function getAudioCtx() {
  if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  return audioCtx;
}

function playCorrectSound() {
  try {
    const ctx = getAudioCtx();
    const notes = [523, 659, 784, 1047]; // C E G C major chord
    notes.forEach((freq, i) => {
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      osc.connect(gain); gain.connect(ctx.destination);
      osc.frequency.value = freq;
      osc.type = 'sine';
      gain.gain.setValueAtTime(0, ctx.currentTime + i*0.07);
      gain.gain.linearRampToValueAtTime(0.2, ctx.currentTime + i*0.07 + 0.05);
      gain.gain.linearRampToValueAtTime(0, ctx.currentTime + i*0.07 + 0.3);
      osc.start(ctx.currentTime + i*0.07);
      osc.stop(ctx.currentTime + i*0.07 + 0.4);
    });
  } catch(e) {}
}

function playWrongSound() {
  try {
    const ctx = getAudioCtx();
    const osc = ctx.createOscillator();
    const gain = ctx.createGain();
    osc.connect(gain); gain.connect(ctx.destination);
    osc.frequency.value = 200;
    osc.type = 'sawtooth';
    gain.gain.setValueAtTime(0.15, ctx.currentTime);
    gain.gain.linearRampToValueAtTime(0, ctx.currentTime + 0.4);
    osc.start(ctx.currentTime);
    osc.stop(ctx.currentTime + 0.4);
  } catch(e) {}
}

function playLevelUpSound() {
  try {
    const ctx = getAudioCtx();
    const notes = [523, 659, 784, 1047, 1175];
    notes.forEach((freq, i) => {
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      osc.connect(gain); gain.connect(ctx.destination);
      osc.frequency.value = freq;
      osc.type = 'sine';
      gain.gain.setValueAtTime(0.25, ctx.currentTime + i*0.1);
      gain.gain.linearRampToValueAtTime(0, ctx.currentTime + i*0.1 + 0.35);
      osc.start(ctx.currentTime + i*0.1);
      osc.stop(ctx.currentTime + i*0.1 + 0.5);
    });
  } catch(e) {}
}

// ===========================
//  LOAD WORD
// ===========================
function loadWord() {
  if (currentWordIdx >= words.length) {
    showComplete();
    return;
  }

  const word = words[currentWordIdx];
  wrongAttempts = 0;

  // Update header
  document.getElementById('word-num').textContent = `${currentWordIdx + 1} / ${words.length}`;
  const pct = (currentWordIdx / words.length) * 100;
  document.getElementById('progress-bar').style.width = pct + '%';
  updateLives();

  // Emoji & level badge
  document.getElementById('emoji-hint').textContent = wordEmojis[currentWordIdx];
  const levelNames = ['', 'Level 1 – Match It! 🔤', 'Level 2 – Build It! 🧩', 'Level 3 – Type It! ⌨️'];
  document.getElementById('level-name').textContent = levelNames[currentLevel];

  // Star score
  updateStarDisplay();

  // Hide hint
  document.getElementById('hint-box').style.display = 'none';

  // Hide all level areas
  ['level1-area','level2-area','level3-area'].forEach(id => {
    document.getElementById(id).style.display = 'none';
  });

  // Animate card
  const card = document.getElementById('word-card');
  card.style.animation = 'none';
  requestAnimationFrame(() => {
    card.style.animation = '';
    card.style.animation = 'cardIn 0.4s cubic-bezier(0.34, 1.56, 0.64, 1)';
  });

  // Animate emoji
  const emoji = document.getElementById('emoji-hint');
  emoji.style.animation = 'none';
  requestAnimationFrame(() => {
    emoji.style.animation = '';
    emoji.style.animation = 'emojiPop 0.5s cubic-bezier(0.34, 1.56, 0.64, 1)';
  });

  // Speak the word
  setTimeout(() => speakWord(), 600);

  // Show level UI
  if (currentLevel === 1) setupLevel1();
  else if (currentLevel === 2) setupLevel2();
  else setupLevel3();
}

function updateLives() {
  const hearts = wrongAttempts >= 3 ? '💔' : (wrongAttempts >= 2 ? '💔💔❤️' : (wrongAttempts >= 1 ? '💔❤️❤️' : '❤️❤️❤️'));
  document.getElementById('lives').textContent = wrongAttempts >= 3 ? '💔💔💔' : 
    '❤️'.repeat(3 - wrongAttempts) + (wrongAttempts > 0 ? '🖤'.repeat(wrongAttempts) : '');
}

function updateStarDisplay() {
  const stars = wordScores[currentWordIdx].stars;
  const starEl = document.getElementById('star-score');
  starEl.innerHTML = '';
  for (let i = 0; i < 3; i++) {
    const s = document.createElement('span');
    s.textContent = i < stars ? '⭐' : '☆';
    if (i < stars) s.style.textShadow = '0 0 10px gold';
    starEl.appendChild(s);
  }
}

function deductStar() {
  if (wordScores[currentWordIdx].stars > 0) {
    wordScores[currentWordIdx].stars = Math.max(0, wordScores[currentWordIdx].stars - 1);
    updateStarDisplay();
  }
}

// ===========================
//  LEVEL 1 – MULTIPLE CHOICE
// ===========================
function setupLevel1() {
  document.getElementById('level1-area').style.display = 'block';
  const word = words[currentWordIdx];
  const options = generateOptions(word);
  const choicesEl = document.getElementById('choices');
  choicesEl.innerHTML = '';
  options.forEach(opt => {
    const btn = document.createElement('button');
    btn.className = 'choice-btn';
    btn.textContent = opt.toUpperCase();
    btn.addEventListener('click', () => checkLevel1(opt, btn));
    choicesEl.appendChild(btn);
  });
}

// Generate exactly 2 distinct misspellings + 1 correct, all of the SAME word
function generateOptions(correct) {
  const misspellings = generateSmartMisspellings(correct);
  // Pick 2 different ones
  const chosen = [];
  for (const m of misspellings) {
    if (chosen.length >= 2) break;
    if (!chosen.includes(m)) chosen.push(m);
  }
  // Pad if not enough variants (very short words)
  while (chosen.length < 2) {
    const fallback = fallbackMisspell(correct, chosen);
    if (fallback && !chosen.includes(fallback)) chosen.push(fallback);
    else break;
  }
  return shuffle([correct, ...chosen.slice(0, 2)]);
}

// Smart misspelling engine – models the most common English spelling errors kids make
function generateSmartMisspellings(word) {
  const candidates = [];
  const w = word.toLowerCase();

  // ── 1. VOWEL TEAM / DIGRAPH CONFUSIONS ──────────────────────────────
  const vowelSwaps = [
    // ea ↔ ee ↔ ie ↔ e
    [/ea/g, 'ee'], [/ea/g, 'e'], [/ea/g, 'ie'],
    [/ee/g, 'ea'], [/ee/g, 'e'], [/ee/g, 'ie'],
    [/ie/g, 'ee'], [/ie/g, 'ei'], [/ie/g, 'i'],
    // ai ↔ ay ↔ a
    [/ai/g, 'ay'], [/ai/g, 'a'], [/ay/g, 'ai'], [/ay/g, 'ae'],
    // oa ↔ ow ↔ o
    [/oa/g, 'ow'], [/oa/g, 'o'], [/ow/g, 'oa'],
    // ou ↔ ow ↔ oo
    [/ou/g, 'ow'], [/ou/g, 'oo'], [/ow/g, 'ou'],
    // oo ↔ u ↔ ue
    [/oo/g, 'u'], [/oo/g, 'ue'], [/oo/g, 'ew'],
    // igh ↔ i ↔ ie ↔ y
    [/igh/g, 'i'], [/igh/g, 'ie'], [/igh/g, 'y'],
    // au ↔ aw ↔ a
    [/au/g, 'aw'], [/aw/g, 'au'], [/au/g, 'or'],
    // oi ↔ oy
    [/oi/g, 'oy'], [/oy/g, 'oi'],
    // ew ↔ ue ↔ oo
    [/ew/g, 'ue'], [/ew/g, 'oo'],
    // er ↔ ir ↔ ur (r-controlled)
    [/er/g, 'ir'], [/er/g, 'ur'], [/ir/g, 'er'], [/ur/g, 'er'],
    [/ar/g, 'er'], [/or/g, 'ar'],
  ];
  for (const [pat, rep] of vowelSwaps) {
    if (pat.test(w)) {
      const v = w.replace(pat, rep);
      if (v !== w) candidates.push(v);
    }
    pat.lastIndex = 0;
  }

  // ── 2. SILENT / DROPPED LETTERS ──────────────────────────────────────
  const silentDrops = [
    [/kn/g, 'n'],   // know→now, knight→night
    [/wr/g, 'r'],   // write→rite
    [/gn/g, 'n'],   // gnome→nome
    [/mb$/g, 'm'],  // lamb→lam, climb→clim
    [/gh/g, ''],    // night→nit, light→lit (already in igh)
    [/ck/g, 'k'],   // black→blak
    [/ck/g, 'c'],   // black→blac
    [/tch/g, 'ch'], // catch→cach
    [/dge/g, 'j'],  // bridge→brij
    [/lk$/g, 'k'],  // milk→mik, walk→wak
  ];
  for (const [pat, rep] of silentDrops) {
    if (pat.test(w)) {
      const v = w.replace(pat, rep);
      if (v !== w && v.length > 0) candidates.push(v);
    }
    pat.lastIndex = 0;
  }

  // ── 3. CONSONANT SOUND CONFUSIONS ────────────────────────────────────
  const consonantSwaps = [
    // c/k confusion
    [/^c([^h])/g, (_, x) => `k${x}`], [/^k/g, 'c'],
    // f/ph
    [/ph/g, 'f'], [/ff/g, 'f'],
    // s/c (soft c)
    [/ce/g, 'se'], [/ci/g, 'si'], [/cy/g, 'sy'],
    // j/g (soft g)
    [/ge/g, 'je'], [/gi/g, 'ji'],
    // qu/kw
    [/qu/g, 'kw'],
    // x/ks/z
    [/x/g, 'ks'], [/^z/g, 's'],
    // ch/sh confusion  
    [/ch/g, 'sh'], [/sh/g, 'ch'],
    // wh/w
    [/wh/g, 'w'],
    // th/d (some kids)
    [/^th/g, 'd'],
  ];
  for (const [pat, rep] of consonantSwaps) {
    if (typeof rep === 'string' ? pat.test(w) : pat.test(w)) {
      const v = typeof rep === 'function' ? w.replace(pat, rep) : w.replace(pat, rep);
      if (v !== w && v.length > 0) candidates.push(v);
    }
    pat.lastIndex = 0;
  }

  // ── 4. DOUBLE LETTER ERRORS ──────────────────────────────────────────
  // Undoubling: running→runing
  const dbl = /(.)\1/g;
  let m;
  while ((m = dbl.exec(w)) !== null) {
    const v = w.slice(0, m.index + 1) + w.slice(m.index + 2);
    if (v !== w) candidates.push(v);
  }
  // Extra doubling: clean→cleann, open→oppen
  for (let i = 1; i < w.length; i++) {
    if (!/[aeiou]/.test(w[i]) && /[aeiou]/.test(w[i-1])) {
      const v = w.slice(0, i) + w[i] + w.slice(i);
      if (v !== w) candidates.push(v);
    }
  }

  // ── 5. VOWEL SUBSTITUTIONS (single vowels) ───────────────────────────
  const singleVowels = [
    ['a', ['e', 'u']], ['e', ['i', 'a']], ['i', ['e', 'y']],
    ['o', ['u', 'a']], ['u', ['o', 'e']],
  ];
  for (const [vowel, subs] of singleVowels) {
    for (let i = 0; i < w.length; i++) {
      if (w[i] === vowel) {
        for (const sub of subs) {
          const v = w.slice(0, i) + sub + w.slice(i + 1);
          if (v !== w) candidates.push(v);
        }
        break; // only change first occurrence to keep it recognisable
      }
    }
  }

  // ── 6. SILENT E ERRORS ───────────────────────────────────────────────
  if (w.endsWith('e') && w.length > 3) {
    candidates.push(w.slice(0, -1)); // drop silent e: make→mak
  } else if (!/e$/.test(w) && w.length > 2) {
    candidates.push(w + 'e'); // add spurious e: dog→doge, run→rune
  }

  // ── 7. COMMON SUFFIX ERRORS ──────────────────────────────────────────
  const suffixSwaps = [
    [/tion$/g, 'shun'], [/tion$/g, 'sion'],
    [/sion$/g, 'tion'],
    [/ment$/g, 'mint'], [/ment$/g, 'mant'],
    [/ness$/g, 'niss'], [/ness$/g, 'nis'],
    [/ful$/g, 'full'], [/full$/g, 'ful'],
    [/less$/g, 'lis'],
    [/ly$/g, 'lee'], [/ly$/g, 'li'],
    [/ing$/g, 'eng'], [/ing$/g, 'in'],
    [/ed$/g, 'd'], [/ed$/g, 't'],
    [/er$/g, 'a'], [/er$/g, 'or'],
    [/est$/g, 'ist'],
    [/ight$/g, 'ite'], [/ight$/g, 'it'],
  ];
  for (const [pat, rep] of suffixSwaps) {
    if (pat.test(w)) {
      const v = w.replace(pat, rep);
      if (v !== w) candidates.push(v);
    }
    pat.lastIndex = 0;
  }

  // ── 8. COMMON PREFIX ERRORS ──────────────────────────────────────────
  const prefixSwaps = [
    [/^un/, 'on'], [/^dis/, 'diss'], [/^mis/, 'miss'],
    [/^pre/, 'pri'], [/^pro/, 'pra'],
    [/^ex/, 'ix'], [/^in/, 'en'], [/^en/, 'in'],
  ];
  for (const [pat, rep] of prefixSwaps) {
    if (pat.test(w)) {
      const v = w.replace(pat, rep);
      if (v !== w) candidates.push(v);
    }
  }

  // ── 9. LETTER REVERSAL / TRANSPOSITION (common in early learners) ────
  for (let i = 0; i < w.length - 1; i++) {
    if (w[i] !== w[i+1]) {
      const arr = w.split('');
      [arr[i], arr[i+1]] = [arr[i+1], arr[i]];
      candidates.push(arr.join(''));
    }
  }

  // ── Filter: must be different from correct, length ≥ 2, only a-z ────
  const valid = [...new Set(candidates)].filter(
    c => c !== w && c.length >= 2 && /^[a-z]+$/.test(c)
  );

  // ── Sort by "believability" — prefer candidates that look most like the word ──
  const scored = valid.map(c => ({
    word: c,
    score: levenshtein(w, c) + (Math.abs(c.length - w.length) * 0.5)
  }));
  scored.sort((a, b) => a.score - b.score);

  return scored.map(s => s.word);
}

// Simple Levenshtein distance for sorting misspelling quality
function levenshtein(a, b) {
  const dp = Array.from({length: a.length + 1}, (_, i) => [i]);
  for (let j = 1; j <= b.length; j++) dp[0][j] = j;
  for (let i = 1; i <= a.length; i++) {
    for (let j = 1; j <= b.length; j++) {
      dp[i][j] = a[i-1] === b[j-1]
        ? dp[i-1][j-1]
        : 1 + Math.min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]);
    }
  }
  return dp[a.length][b.length];
}

// Absolute last-resort fallback misspelling
function fallbackMisspell(word, exclude) {
  const w = word.toLowerCase();
  // Swap first two letters
  if (w.length >= 2) {
    const v = w[1] + w[0] + w.slice(2);
    if (v !== w && !exclude.includes(v)) return v;
  }
  // Change last vowel
  const vowels = 'aeiou';
  for (let i = w.length - 1; i >= 0; i--) {
    if (vowels.includes(w[i])) {
      for (const v of vowels) {
        if (v !== w[i]) {
          const candidate = w.slice(0, i) + v + w.slice(i + 1);
          if (!exclude.includes(candidate)) return candidate;
        }
      }
    }
  }
  return w.slice(0, -1) + (w.endsWith('e') ? 'i' : 'e');
}

function checkLevel1(chosen, btn) {
  if (isAnimating) return;
  const correct = words[currentWordIdx];
  if (chosen === correct) {
    handleCorrect(btn, 'choice-btn correct-anim');
  } else {
    handleWrong(btn, 'choice-btn wrong-anim');
  }
}

// ===========================
//  LEVEL 2 – BUILD
// ===========================
const ALPHABET = 'abcdefghijklmnopqrstuvwxyz';

function setupLevel2() {
  document.getElementById('level2-area').style.display = 'block';
  const word = words[currentWordIdx];

  // Create letter pool: word letters shuffled + 5 random extras
  let letters = word.split('');
  const extra = 5;
  const usedSet = new Set(letters);
  let extras = [];
  for (let i = 0; i < extra; i++) {
    let r;
    do { r = ALPHABET[Math.floor(Math.random() * 26)]; } while (usedSet.has(r) && Math.random() > 0.3);
    extras.push(r);
  }
  letters = shuffle([...letters, ...extras]);

  tileMap = letters.map((letter, idx) => ({ letter, idx, used: false }));
  answerTiles = [];

  renderPool();
  renderAnswer();
}

function renderPool() {
  const pool = document.getElementById('letter-pool');
  pool.innerHTML = '';
  tileMap.forEach((tile, i) => {
    const el = document.createElement('div');
    el.className = 'letter-tile' + (tile.used ? ' used' : '');
    el.textContent = tile.letter.toUpperCase();
    if (!tile.used) {
      el.addEventListener('click', () => addLetterFromPool(i));
    }
    pool.appendChild(el);
  });
}

function renderAnswer() {
  const ans = document.getElementById('build-answer');
  ans.innerHTML = '';
  if (answerTiles.length === 0) {
    const ph = document.createElement('span');
    ph.className = 'answer-placeholder';
    ph.textContent = 'Tap letters to spell the word ⬇️';
    ans.appendChild(ph);
    ans.classList.remove('has-letters');
  } else {
    ans.classList.add('has-letters');
    answerTiles.forEach((tile, i) => {
      const el = document.createElement('div');
      el.className = 'letter-tile answer-tile';
      el.textContent = tile.letter.toUpperCase();
      el.addEventListener('click', () => removeLetterFromAnswer(i));
      ans.appendChild(el);
    });
  }
}

function addLetterFromPool(poolIdx) {
  if (tileMap[poolIdx].used) return;
  tileMap[poolIdx].used = true;
  answerTiles.push({ letter: tileMap[poolIdx].letter, poolIdx });
  renderPool();
  renderAnswer();
}

function removeLetterFromAnswer(ansIdx) {
  const tile = answerTiles[ansIdx];
  tileMap[tile.poolIdx].used = false;
  answerTiles.splice(ansIdx, 1);
  renderPool();
  renderAnswer();
}

function clearAnswer() {
  answerTiles.forEach(t => { tileMap[t.poolIdx].used = false; });
  answerTiles = [];
  renderPool();
  renderAnswer();
}

function checkBuild() {
  if (isAnimating) return;
  const built = answerTiles.map(t => t.letter).join('');
  const correct = words[currentWordIdx];
  if (built === correct) {
    handleCorrect(document.getElementById('build-check-btn'), '');
  } else {
    handleWrong(document.getElementById('build-check-btn'), '');
    // Shake answer area
    const ans = document.getElementById('build-answer');
    ans.style.animation = 'none';
    ans.style.borderColor = 'var(--coral)';
    requestAnimationFrame(() => {
      ans.style.animation = 'wrongShake 0.4s';
      setTimeout(() => { ans.style.animation = ''; ans.style.borderColor = ''; }, 500);
    });
  }
}

// ===========================
//  LEVEL 3 – TYPE
// ===========================
function setupLevel3() {
  document.getElementById('level3-area').style.display = 'block';
  const input = document.getElementById('type-input');
  input.value = '';
  input.className = 'type-input';
  setTimeout(() => input.focus(), 400);
  input.onkeydown = (e) => { if (e.key === 'Enter') checkType(); };
}

function checkType() {
  if (isAnimating) return;
  const input = document.getElementById('type-input');
  const typed = input.value.trim().toLowerCase();
  const correct = words[currentWordIdx];
  if (typed === correct) {
    handleCorrect(input, 'type-input correct-anim');
  } else {
    input.className = 'type-input wrong-anim';
    setTimeout(() => { input.className = 'type-input'; }, 500);
    handleWrong(null, '');
  }
}

// ===========================
//  CORRECT / WRONG HANDLERS
// ===========================
const correctMessages = [
  ['🎉', 'AMAZING!', 'That\'s exactly right!'],
  ['⭐', 'SUPERSTAR!', 'You nailed it!'],
  ['🌈', 'BRILLIANT!', 'You\'re a spelling wizard!'],
  ['🚀', 'FANTASTIC!', 'Out of this world!'],
  ['🎯', 'PERFECT!', 'Bullseye! Great spelling!'],
  ['🏆', 'CHAMPION!', 'You\'re a spelling champion!'],
  ['💫', 'DAZZLING!', 'Your brain is amazing!'],
  ['🦄', 'MAGICAL!', 'Incredible spelling!'],
  ['🎸', 'AWESOME!', 'You rock at spelling!'],
  ['🌟', 'STELLAR!', 'You\'re shining bright!'],
];
const wrongMessages = [
  ['😊', 'Almost!', 'Try one more time!'],
  ['💪', 'So close!', 'You can do it!'],
  ['🤔', 'Hmm...', 'Give it another go!'],
  ['🎵', 'Oops!', 'That\'s okay, try again!'],
  ['🌸', 'Nice try!', 'Keep going, you\'ve got this!'],
];

function handleCorrect(el, animClass) {
  isAnimating = true;
  playCorrectSound();
  if (el && animClass) {
    el.classList.add(animClass.split(' ').filter(Boolean).pop() || '');
  }

  // Pick random message
  const msg = correctMessages[Math.floor(Math.random() * correctMessages.length)];
  showFeedback(msg[0], msg[1], msg[2], true);
  launchConfetti();

  setTimeout(() => {
    hideFeedback();
    setTimeout(() => {
      advanceAfterCorrect();
      isAnimating = false;
    }, 300);
  }, 1500);
}

function handleWrong(el, animClass) {
  isAnimating = true;
  playWrongSound();
  wrongAttempts++;
  deductStar();
  updateLives();

  const msg = wrongMessages[Math.floor(Math.random() * wrongMessages.length)];
  showFeedback(msg[0], msg[1], msg[2], false);

  // Show hint after 3 wrong
  if (wrongAttempts >= 3) {
    const word = words[currentWordIdx];
    document.getElementById('hint-letter').textContent = word[0].toUpperCase();
    document.getElementById('hint-box').style.display = 'flex';
  }

  setTimeout(() => {
    hideFeedback();
    isAnimating = false;
  }, 1200);
}

function advanceAfterCorrect() {
  const maxLevel = 3;
  // Check if we need to advance level or word
  if (currentLevel < selectedStartLevel) {
    // Shouldn't happen
  }
  // Go to next word
  currentWordIdx++;
  wrongAttempts = 0;
  if (currentWordIdx >= words.length) {
    setTimeout(() => showComplete(), 200);
  } else {
    loadWord();
  }
}

function skipWord() {
  if (wordScores[currentWordIdx]) {
    wordScores[currentWordIdx].stars = 0;
  }
  currentWordIdx++;
  wrongAttempts = 0;
  if (currentWordIdx >= words.length) {
    showComplete();
  } else {
    loadWord();
  }
}

// ===========================
//  FEEDBACK OVERLAY
// ===========================
function showFeedback(emoji, text, sub, isCorrect) {
  const overlay = document.getElementById('feedback-overlay');
  const bubble = document.getElementById('feedback-bubble');
  document.getElementById('feedback-emoji').textContent = emoji;
  document.getElementById('feedback-text').textContent = text;
  document.getElementById('feedback-text').style.color = isCorrect ? '#6C63FF' : '#FF6B6B';
  document.getElementById('feedback-sub').textContent = sub;
  bubble.style.background = isCorrect ? 'white' : '#fff5f5';
  overlay.classList.add('show');
}

function hideFeedback() {
  document.getElementById('feedback-overlay').classList.remove('show');
}

// ===========================
//  CONFETTI
// ===========================
const canvas = document.getElementById('confetti-canvas');
const ctx2d = canvas.getContext('2d');
let confettiParticles = [];
let animFrame = null;

function launchConfetti() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  const colors = ['#FF6B6B','#FFE66D','#4ECDC4','#6C63FF','#FF85A1','#6BCB77','#FF9F1C'];
  for (let i = 0; i < 80; i++) {
    confettiParticles.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height * 0.5 - canvas.height * 0.3,
      r: Math.random() * 10 + 4,
      color: colors[Math.floor(Math.random() * colors.length)],
      vel: { x: (Math.random() - 0.5) * 8, y: Math.random() * 4 + 2 },
      rot: Math.random() * Math.PI * 2,
      rotV: (Math.random() - 0.5) * 0.2,
      shape: Math.random() > 0.5 ? 'rect' : 'circle',
      life: 1,
    });
  }
  if (animFrame) cancelAnimationFrame(animFrame);
  animateConfetti();
}

function animateConfetti() {
  ctx2d.clearRect(0, 0, canvas.width, canvas.height);
  confettiParticles = confettiParticles.filter(p => p.life > 0);
  confettiParticles.forEach(p => {
    p.x += p.vel.x; p.y += p.vel.y;
    p.vel.y += 0.15; p.rot += p.rotV; p.life -= 0.012;
    ctx2d.save();
    ctx2d.globalAlpha = p.life;
    ctx2d.fillStyle = p.color;
    ctx2d.translate(p.x, p.y);
    ctx2d.rotate(p.rot);
    if (p.shape === 'rect') {
      ctx2d.fillRect(-p.r, -p.r/2, p.r*2, p.r);
    } else {
      ctx2d.beginPath();
      ctx2d.arc(0, 0, p.r, 0, Math.PI*2);
      ctx2d.fill();
    }
    ctx2d.restore();
  });
  if (confettiParticles.length > 0) {
    animFrame = requestAnimationFrame(animateConfetti);
  } else {
    ctx2d.clearRect(0, 0, canvas.width, canvas.height);
  }
}

// ===========================
//  COMPLETE SCREEN
// ===========================
function showComplete() {
  playLevelUpSound();
  const totalStars = wordScores.reduce((sum, s) => sum + s.stars, 0);
  const maxStars = words.length * 3;
  const pct = totalStars / maxStars;

  let emoji, title;
  if (pct >= 0.9) { emoji = '🏆'; title = 'You\'re a SPELLING SUPERSTAR!'; }
  else if (pct >= 0.7) { emoji = '🌟'; title = 'Awesome Job!'; }
  else if (pct >= 0.5) { emoji = '👍'; title = 'Great Effort!'; }
  else { emoji = '💪'; title = 'Keep Practicing!'; }

  document.getElementById('complete-emoji').textContent = emoji;
  document.getElementById('complete-title').textContent = title;
  document.getElementById('final-score').textContent = totalStars;

  // Word results
  const resultsEl = document.getElementById('word-results');
  resultsEl.innerHTML = '';
  words.forEach((word, i) => {
    const pill = document.createElement('div');
    pill.className = 'word-result-pill';
    const stars = wordScores[i]?.stars || 0;
    const starStr = '⭐'.repeat(stars) + '☆'.repeat(3 - stars);
    pill.innerHTML = `<span>${wordEmojis[i]}</span><span style="text-transform:uppercase;letter-spacing:1px">${word}</span><span>${starStr}</span>`;
    resultsEl.appendChild(pill);
  });

  showScreen('screen-complete');
  setTimeout(() => launchConfetti(), 300);
  if (pct >= 0.7) setTimeout(() => launchConfetti(), 1200);
}

function playAgain() {
  wordScores = words.map(() => ({stars: 3}));
  currentWordIdx = 0;
  currentLevel = selectedStartLevel;
  wrongAttempts = 0;
  showScreen('screen-game');
  loadWord();
}

function newWords() {
  showScreen('screen-setup');
}

// ===========================
//  UTILS
// ===========================
function shuffle(arr) {
  for (let i = arr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [arr[i], arr[j]] = [arr[j], arr[i]];
  }
  return arr;
}

// ===========================
//  PWA SERVICE WORKER
// ===========================
if ('serviceWorker' in navigator) {
  const swCode = `
    const CACHE = 'spellstar-v1';
    self.addEventListener('install', e => {
      e.waitUntil(caches.open(CACHE).then(c => c.addAll(['/'])));
    });
    self.addEventListener('fetch', e => {
      e.respondWith(caches.match(e.request).then(r => r || fetch(e.request)));
    });
  `;
  const blob = new Blob([swCode], { type: 'application/javascript' });
  const swUrl = URL.createObjectURL(blob);
  navigator.serviceWorker.register(swUrl).catch(() => {});
}

// Resize canvas on window resize
window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});
</script>
</body>
</html>
