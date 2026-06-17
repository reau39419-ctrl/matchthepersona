<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Who Said That? — Difficult Negotiation Personas</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    background: #F4F6FA;
    min-height: 100vh;
    padding: 1.5rem 1rem 3rem;
    color: #1A1A2E;
  }

  .header {
    text-align: center;
    margin-bottom: 1.75rem;
  }

  .badge {
    display: inline-block;
    background: #EEEDFE;
    color: #3C3489;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.07em;
    text-transform: uppercase;
    padding: 4px 14px;
    border-radius: 20px;
    margin-bottom: 10px;
  }

  h1 {
    font-size: 22px;
    font-weight: 700;
    color: #1A1A2E;
    margin-bottom: 6px;
  }

  .subtitle {
    font-size: 14px;
    color: #5A6480;
    line-height: 1.5;
    max-width: 340px;
    margin: 0 auto;
  }

  .score-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #fff;
    border: 1px solid #E2E0F5;
    border-radius: 12px;
    padding: 10px 16px;
    margin-bottom: 1.25rem;
  }

  .score-label { font-size: 13px; color: #5A6480; }
  .score-num { font-size: 18px; font-weight: 700; color: #3C3489; }

  .section-label {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    color: #8A8AAA;
    margin-bottom: 8px;
    padding-left: 2px;
  }

  .phrases-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px;
    margin-bottom: 1.5rem;
  }

  .phrase-card {
    background: #fff;
    border: 1.5px solid #E2E0F5;
    border-radius: 12px;
    padding: 12px 14px;
    cursor: pointer;
    transition: border-color 0.15s, background 0.15s, transform 0.1s;
    min-height: 64px;
    display: flex;
    align-items: center;
  }

  .phrase-card:active { transform: scale(0.97); }

  .phrase-card.selected {
    border-color: #7F77DD;
    background: #EEEDFE;
  }

  .phrase-card.matched-correct {
    border-color: #1D9E75;
    background: #E1F5EE;
    cursor: default;
  }

  .phrase-card.matched-wrong {
    border-color: #E24B4A;
    background: #FCEBEB;
  }

  .phrase-text {
    font-size: 13px;
    font-style: italic;
    color: #2A2A4A;
    line-height: 1.45;
  }

  .phrase-card.matched-correct .phrase-text { color: #085041; }
  .phrase-card.matched-wrong .phrase-text { color: #791F1F; }

  .personas-list { margin-bottom: 1.5rem; }

  .persona-card {
    background: #fff;
    border: 1.5px solid #E2E0F5;
    border-radius: 12px;
    padding: 13px 16px;
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    gap: 12px;
    cursor: pointer;
    transition: border-color 0.15s, background 0.15s, transform 0.1s;
  }

  .persona-card:active { transform: scale(0.98); }

  .persona-card.matched-correct {
    border-color: #1D9E75;
    background: #E1F5EE;
    cursor: default;
  }

  .persona-card.matched-wrong {
    border-color: #E24B4A;
    background: #FCEBEB;
  }

  .persona-num {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background: #EEEDFE;
    color: #3C3489;
    font-size: 12px;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }

  .persona-card.matched-correct .persona-num { background: #1D9E75; color: #fff; }
  .persona-card.matched-wrong .persona-num { background: #E24B4A; color: #fff; }

  .persona-name {
    font-size: 14px;
    font-weight: 600;
    color: #1A1A2E;
    flex: 1;
  }

  .persona-card.matched-correct .persona-name { color: #085041; }
  .persona-card.matched-wrong .persona-name { color: #791F1F; }

  .matched-phrase {
    font-size: 12px;
    font-style: italic;
    color: #0F6E56;
    margin-top: 2px;
  }

  .check-icon {
    font-size: 18px;
    color: #1D9E75;
  }

  .hint {
    text-align: center;
    font-size: 13px;
    color: #8A8AAA;
    margin-bottom: 1.25rem;
    min-height: 20px;
    transition: opacity 0.2s;
  }

  .hint.active { color: #3C3489; font-weight: 500; }

  .reset-btn {
    display: block;
    width: 100%;
    padding: 14px;
    background: #3C3489;
    color: #fff;
    border: none;
    border-radius: 12px;
    font-size: 15px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.15s, transform 0.1s;
  }

  .reset-btn:active { transform: scale(0.98); background: #26215C; }

  .congrats {
    text-align: center;
    background: #E1F5EE;
    border: 1.5px solid #1D9E75;
    border-radius: 16px;
    padding: 20px;
    margin-bottom: 1.5rem;
    display: none;
  }

  .congrats.show { display: block; }
  .congrats h2 { font-size: 18px; color: #085041; margin-bottom: 6px; }
  .congrats p { font-size: 13px; color: #0F6E56; line-height: 1.5; }

  .step-indicator {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background: #fff;
    border: 1px solid #E2E0F5;
    border-radius: 20px;
    padding: 5px 14px;
    font-size: 12px;
    color: #5A6480;
    margin-bottom: 1.25rem;
  }

  .step-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: #7F77DD;
  }

  .step-dot.inactive { background: #D3D1C7; }
</style>
</head>
<body>

<div class="header">
  <div class="badge">Matching activity</div>
  <h1>Who said that?</h1>
  <p class="subtitle">Match each difficult negotiation persona to the phrase they are most likely to say.</p>
</div>

<div class="score-bar">
  <span class="score-label">Correct matches</span>
  <span class="score-num" id="score-display">0 / 7</span>
</div>

<div id="congrats" class="congrats">
  <h2>Well done!</h2>
  <p>You matched all 7 personas correctly. You are ready to spot these patterns at the negotiation table.</p>
</div>

<div id="step1-section">
  <div class="section-label">Step 1 — Select a phrase</div>
  <div class="phrases-grid" id="phrases-grid"></div>
</div>

<div id="step2-section" style="display:none;">
  <div style="display:flex; align-items:center; gap:10px; margin-bottom:10px;">
    <div class="section-label" style="margin-bottom:0;">Step 2 — Select the persona</div>
    <button onclick="clearPhraseSelection()" style="font-size:12px; color:#8A8AAA; background:none; border:1px solid #E2E0F5; border-radius:20px; padding:3px 10px; cursor:pointer;">Cancel</button>
  </div>
  <div id="selected-phrase-preview" style="background:#EEEDFE; border:1.5px solid #7F77DD; border-radius:12px; padding:10px 14px; margin-bottom:12px; font-size:13px; font-style:italic; color:#3C3489;"></div>
</div>

<div class="section-label" id="personas-label">Personas</div>
<div class="personas-list" id="personas-list"></div>

<p class="hint" id="hint">Select a phrase above to get started.</p>

<button class="reset-btn" onclick="resetAll()">Start over</button>

<script>
const personas = [
  { id: 1, name: "The Analyst",               phrase: "\u201CIf we just had more data\u2026\u201D" },
  { id: 2, name: "The Egoist",                phrase: "\u201CThat was actually my idea.\u201D" },
  { id: 3, name: "The Flopping Fish",         phrase: "\u201CI know I said yes, but\u2026\u201D" },
  { id: 4, name: "The Irrational Negotiator", phrase: "\u201CThat is completely unacceptable.\u201D" },
  { id: 5, name: "The Volcano",               phrase: "\u201CI\u2019ve had ENOUGH of this!\u201D" },
  { id: 6, name: "The Puppet Master",         phrase: "\u201CI\u2019m just asking questions.\u201D" },
  { id: 7, name: "The Brick Wall",            phrase: "\u201CThere\u2019s nothing to discuss.\u201D" }
];

let shuffledPhrases = [...personas].sort(() => Math.random() - 0.5);
let selectedPhraseId = null;
let matched = {};
let score = 0;

function renderPhrases() {
  const grid = document.getElementById('phrases-grid');
  grid.innerHTML = '';
  shuffledPhrases.forEach(p => {
    const div = document.createElement('div');
    const isMatched = matched[p.id] === true;
    div.className = 'phrase-card' + (isMatched ? ' matched-correct' : selectedPhraseId === p.id ? ' selected' : '');
    div.innerHTML = '<span class="phrase-text">' + p.phrase + (isMatched ? '' : '') + '</span>';
    if (!isMatched) div.onclick = () => selectPhrase(p.id);
    grid.appendChild(div);
  });
}

function renderPersonas() {
  const list = document.getElementById('personas-list');
  list.innerHTML = '';
  personas.forEach((p, i) => {
    const isMatched = matched[p.id] === true;
    const div = document.createElement('div');
    div.className = 'persona-card' + (isMatched ? ' matched-correct' : '');
    div.id = 'persona-card-' + p.id;

    if (isMatched) {
      div.innerHTML =
        '<div class="persona-num">' + (i + 1) + '</div>' +
        '<div style="flex:1"><div class="persona-name">' + p.name + '</div>' +
        '<div class="matched-phrase">' + p.phrase + '</div></div>' +
        '<span class="check-icon">&#10003;</span>';
    } else {
      div.innerHTML =
        '<div class="persona-num">' + (i + 1) + '</div>' +
        '<span class="persona-name">' + p.name + '</span>';
      if (selectedPhraseId !== null) div.onclick = () => selectPersona(p.id);
      else div.style.opacity = '0.5';
    }
    list.appendChild(div);
  });
}

function selectPhrase(id) {
  selectedPhraseId = id;
  const phrase = personas.find(p => p.id === id);
  document.getElementById('step1-section').style.display = 'none';
  document.getElementById('step2-section').style.display = 'block';
  document.getElementById('selected-phrase-preview').textContent = phrase.phrase;
  document.getElementById('hint').textContent = 'Now tap the persona who said this.';
  document.getElementById('hint').className = 'hint active';
  renderPhrases();
  renderPersonas();
}

function clearPhraseSelection() {
  selectedPhraseId = null;
  document.getElementById('step1-section').style.display = 'block';
  document.getElementById('step2-section').style.display = 'none';
  document.getElementById('hint').textContent = 'Select a phrase above to get started.';
  document.getElementById('hint').className = 'hint';
  renderPhrases();
  renderPersonas();
}

function selectPersona(personaId) {
  if (selectedPhraseId === null) return;
  const card = document.getElementById('persona-card-' + personaId);

  if (selectedPhraseId === personaId) {
    matched[personaId] = true;
    score++;
    document.getElementById('score-display').textContent = score + ' / 7';
    selectedPhraseId = null;
    document.getElementById('step1-section').style.display = 'block';
    document.getElementById('step2-section').style.display = 'none';
    document.getElementById('hint').textContent = score < 7 ? 'Correct! Keep going.' : '';
    document.getElementById('hint').className = 'hint active';
    if (score === 7) {
      document.getElementById('congrats').className = 'congrats show';
      document.getElementById('hint').textContent = '';
    }
  } else {
    card.className = 'persona-card matched-wrong';
    document.getElementById('hint').textContent = 'Not quite \u2014 try another persona.';
    document.getElementById('hint').className = 'hint active';
    setTimeout(() => {
      card.className = 'persona-card';
      card.onclick = () => selectPersona(personaId);
    }, 700);
  }

  renderPhrases();
  renderPersonas();
}

function resetAll() {
  shuffledPhrases = [...personas].sort(() => Math.random() - 0.5);
  selectedPhraseId = null;
  matched = {};
  score = 0;
  document.getElementById('score-display').textContent = '0 / 7';
  document.getElementById('congrats').className = 'congrats';
  document.getElementById('step1-section').style.display = 'block';
  document.getElementById('step2-section').style.display = 'none';
  document.getElementById('hint').textContent = 'Select a phrase above to get started.';
  document.getElementById('hint').className = 'hint';
  renderPhrases();
  renderPersonas();
}

renderPhrases();
renderPersonas();
</script>
</body>
</html>
