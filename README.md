<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Fun Facts!</title>
  <link href="https://fonts.googleapis.com/css2?family=Righteous&family=Syne:wght@400;700;800&family=DM+Sans:ital,wght@0,300;0,500;1,300&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #fdf6e3;
      --ink: #1a1208;
      --accent1: #f4500c;
      --accent2: #1b4bff;
      --accent3: #ffcc00;
      --card-bg: #fff9ee;
      --border: #1a1208;
    }

    body {
      background-color: var(--bg);
      color: var(--ink);
      font-family: 'DM Sans', sans-serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 20px 60px;
      overflow-x: hidden;
    }

    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 0;
      opacity: 0.5;
    }

    header {
      text-align: center;
      margin-bottom: 36px;
      position: relative;
      z-index: 1;
    }

    .eyebrow {
      font-size: 11px;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: var(--accent1);
      font-weight: 500;
      margin-bottom: 6px;
    }

    h1 {
      font-family: 'Righteous', cursive;
      font-size: clamp(52px, 10vw, 96px);
      line-height: 0.95;
      color: var(--ink);
      letter-spacing: -1px;
      position: relative;
    }

    h1 span.highlight {
      color: var(--accent1);
      position: relative;
      display: inline-block;
    }

    h1 span.highlight::after {
      content: '';
      position: absolute;
      bottom: 4px; left: 0;
      width: 100%; height: 6px;
      background: var(--accent3);
      z-index: -1;
      transform: skewX(-5deg);
    }

    .subtitle {
      margin-top: 14px;
      font-size: 15px;
      color: #6b5c3e;
      font-style: italic;
    }

    #fact-area {
      position: relative;
      z-index: 1;
      width: 100%;
      max-width: 720px;
    }

    .card-wrapper { perspective: 1000px; }

    #fact-card {
      background: var(--card-bg);
      border: 2.5px solid var(--border);
      border-radius: 4px;
      padding: 44px 48px;
      position: relative;
      box-shadow: 6px 6px 0 var(--border);
      min-height: 200px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      transition: transform 0.15s ease, box-shadow 0.15s ease;
    }

    #fact-card:hover {
      transform: translate(-2px, -2px);
      box-shadow: 8px 8px 0 var(--border);
    }

    .card-number {
      font-family: 'Righteous', cursive;
      font-size: 80px;
      color: var(--accent3);
      line-height: 1;
      position: absolute;
      top: -24px; left: 36px;
      z-index: -1;
      -webkit-text-stroke: 2px var(--border);
    }

    .category-tag {
      font-size: 10px;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      font-weight: 700;
      color: #fff;
      background: var(--accent2);
      border: 1.5px solid var(--border);
      display: inline-block;
      padding: 3px 10px;
      border-radius: 2px;
      margin-bottom: 18px;
      align-self: flex-start;
    }

    #fact-text {
      font-size: clamp(18px, 3vw, 24px);
      line-height: 1.55;
      font-weight: 300;
      color: var(--ink);
      min-height: 80px;
    }

    #fact-text.loading { color: #bba97a; font-style: italic; }

    .corner-deco {
      position: absolute;
      bottom: 14px; right: 20px;
      font-size: 11px;
      letter-spacing: 0.1em;
      color: #c5b08a;
      text-transform: uppercase;
    }

    .controls {
      margin-top: 28px;
      display: flex;
      gap: 12px;
      align-items: center;
      flex-wrap: wrap;
    }

    button {
      font-family: 'Syne', sans-serif;
      font-weight: 800;
      font-size: 13px;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      cursor: pointer;
      border: 2.5px solid var(--border);
      border-radius: 3px;
      padding: 12px 28px;
      transition: transform 0.1s, box-shadow 0.1s;
    }

    button:active { transform: translate(3px, 3px); box-shadow: none !important; }

    #btn-new {
      background: var(--accent1);
      color: #fff;
      box-shadow: 4px 4px 0 var(--border);
    }

    #btn-new:hover {
      transform: translate(-2px, -2px);
      box-shadow: 6px 6px 0 var(--border);
    }

    .category-select {
      font-family: 'Syne', sans-serif;
      font-weight: 700;
      font-size: 12px;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      border: 2.5px solid var(--border);
      border-radius: 3px;
      padding: 11px 16px;
      background: var(--bg);
      color: var(--ink);
      cursor: pointer;
      box-shadow: 4px 4px 0 var(--border);
      appearance: none;
      -webkit-appearance: none;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8'%3E%3Cpath d='M0 0l6 8 6-8z' fill='%231a1208'/%3E%3C/svg%3E");
      background-repeat: no-repeat;
      background-position: right 12px center;
      padding-right: 36px;
    }

    #history-section {
      margin-top: 44px;
      width: 100%;
      max-width: 720px;
      position: relative;
      z-index: 1;
    }

    .history-label {
      font-family: 'Syne', sans-serif;
      font-size: 10px;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: #a08b60;
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .history-label::after {
      content: '';
      flex: 1;
      height: 1px;
      background: #d4c49a;
    }

    #history-list { display: flex; flex-direction: column; gap: 10px; }

    .history-item {
      border-left: 3px solid var(--accent3);
      padding: 8px 14px;
      font-size: 13px;
      color: #6b5c3e;
      line-height: 1.5;
      animation: slideIn 0.35s ease;
    }

    @keyframes slideIn {
      from { opacity: 0; transform: translateX(-12px); }
      to   { opacity: 1; transform: translateX(0); }
    }

    @keyframes cardFlip {
      0%   { transform: rotateY(0deg) scale(1); }
      40%  { transform: rotateY(90deg) scale(0.95); }
      60%  { transform: rotateY(90deg) scale(0.95); }
      100% { transform: rotateY(0deg) scale(1); }
    }

    .flipping { animation: cardFlip 0.5s ease; }

    .fact-counter {
      font-family: 'Righteous', cursive;
      font-size: 13px;
      color: #a08b60;
      margin-left: auto;
    }

    @media (max-width: 540px) {
      #fact-card { padding: 32px 24px; }
      .card-number { font-size: 60px; top: -18px; left: 20px; }
    }
  </style>
</head>
<body>

  <header>
    <p class="eyebrow">✦ Today's knowledge ✦</p>
    <h1>FUN <span class="highlight">FACTS</span></h1>
    <p class="subtitle">The world is stranger & more wonderful than you think.</p>
  </header>

  <div id="fact-area">
    <div class="card-wrapper">
      <div id="fact-card">
        <span class="card-number" id="card-number">01</span>
        <span class="category-tag" id="category-tag">Loading…</span>
        <p id="fact-text" class="loading">Fetching a fact just for you…</p>
        <span class="corner-deco">funfacts.io</span>
      </div>
    </div>

    <div class="controls">
      <select class="category-select" id="category-select">
        <option value="any">🎲 Any Category</option>
        <option value="science">🔬 Science</option>
        <option value="animals">🐾 Animals</option>
        <option value="history">📜 History</option>
        <option value="space">🚀 Space</option>
        <option value="food">🍕 Food</option>
        <option value="human body">🧠 Human Body</option>
        <option value="geography">🌍 Geography</option>
      </select>
      <button id="btn-new">⚡ New Fact</button>
      <span class="fact-counter" id="fact-counter">#1</span>
    </div>
  </div>

  <div id="history-section">
    <p class="history-label">Previously discovered</p>
    <div id="history-list"></div>
  </div>

  <script>
    const API_URL = "https://api.anthropic.com/v1/messages";

    let factCount = 0;
    const history = [];
    const usedFacts = new Set();

    const factCard    = document.getElementById("fact-card");
    const factText    = document.getElementById("fact-text");
    const categoryTag = document.getElementById("category-tag");
    const cardNumber  = document.getElementById("card-number");
    const factCounter = document.getElementById("fact-counter");
    const historyList = document.getElementById("history-list");
    const btnNew      = document.getElementById("btn-new");
    const catSelect   = document.getElementById("category-select");

    const CATEGORY_COLORS = {
      "science":    "#1b4bff",
      "animals":    "#2a9d5c",
      "history":    "#a0522d",
      "space":      "#6a0dad",
      "food":       "#e67e22",
      "human body": "#c0392b",
      "geography":  "#16a085",
      "any":        "#1a1208",
    };

    async function fetchFact() {
      btnNew.disabled = true;
      btnNew.textContent = "Loading…";
      factText.className = "loading";
      factText.textContent = "Reaching into the cosmos of knowledge…";

      const cat = catSelect.value;
      const avoidList = [...usedFacts].slice(-10).join("; ");

      const prompt = `Give me ONE surprising, delightful fun fact${cat === "any" ? "" : ` about ${cat}`}.
It must be true, specific, and genuinely interesting — not generic.
${avoidList ? `Do NOT repeat these recently used facts: ${avoidList}` : ""}
Return ONLY a JSON object with two fields:
- "category": a short 1-2 word label (e.g. "Animals", "Space", "History")
- "fact": the fun fact as a single sentence or two, max 60 words

No preamble, no markdown, just raw JSON.`;

      try {
        const res = await fetch(API_URL, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            model: "claude-sonnet-4-20250514",
            max_tokens: 1000,
            messages: [{ role: "user", content: prompt }]
          })
        });

        const data = await res.json();
        const raw = data.content.map(b => b.text || "").join("").trim()
          .replace(/```json|```/g, "").trim();

        const { category, fact } = JSON.parse(raw);

        factCard.classList.remove("flipping");
        void factCard.offsetWidth;
        factCard.classList.add("flipping");

        setTimeout(() => {
          factCount++;
          usedFacts.add(fact.slice(0, 60));

          factText.className = "";
          factText.textContent = fact;
          categoryTag.textContent = category.toUpperCase();
          categoryTag.style.background = CATEGORY_COLORS[cat] || "#1a1208";
          cardNumber.textContent = String(factCount).padStart(2, "0");
          factCounter.textContent = `#${factCount}`;

          if (history.length >= 5) history.shift();
          history.push({ category, fact });
          renderHistory();
        }, 250);

      } catch (err) {
        factText.className = "";
        factText.textContent = "Couldn't load a fact right now. Try again!";
        console.error(err);
      } finally {
        btnNew.disabled = false;
        btnNew.textContent = "⚡ New Fact";
      }
    }

    function renderHistory() {
      historyList.innerHTML = "";
      [...history].reverse().slice(1).forEach(item => {
        const el = document.createElement("div");
        el.className = "history-item";
        el.textContent = `[${item.category}] ${item.fact}`;
        historyList.appendChild(el);
      });
    }

    btnNew.addEventListener("click", fetchFact);
    fetchFact();
  </script>
</body>
</html>