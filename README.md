<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Happy Birthday Rachel 🎀</title>
  <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --pink: #FF6EB4;
      --peach: #FFB347;
      --lavender: #C9A0FF;
      --mint: #7EEBB5;
      --cream: #FFF8F0;
      --deep: #3D1F5C;
    }

    html, body {
      height: 100%;
      overflow: hidden;
      font-family: 'Nunito', sans-serif;
      background: var(--cream);
    }

    /* ---- CONFETTI ---- */
    .confetti-container {
      position: fixed; inset: 0; pointer-events: none; z-index: 999;
    }
    .dot {
      position: absolute;
      width: 10px; height: 10px;
      border-radius: 50%;
      animation: fall linear infinite;
      opacity: 0;
    }
    @keyframes fall {
      0%   { transform: translateY(-20px) rotate(0deg); opacity: 1; }
      100% { transform: translateY(110vh) rotate(720deg); opacity: 0; }
    }

    /* ---- PAGES WRAPPER ---- */
    #pages {
      position: relative;
      width: 100%; height: 100vh;
      overflow: hidden;
    }

    .page {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 28px 24px;
      transition: transform 0.55s cubic-bezier(.77,0,.175,1), opacity 0.55s ease;
      will-change: transform, opacity;
    }

    /* States */
    .page.active   { transform: translateX(0);     opacity: 1; pointer-events: all; }
    .page.prev     { transform: translateX(-100%); opacity: 0; pointer-events: none; }
    .page.next     { transform: translateX(100%);  opacity: 0; pointer-events: none; }

    /* ---- PAGE BACKGROUNDS ---- */
    #p1 { background: linear-gradient(145deg, #FFD6E8 0%, #FFF0BA 100%); }
    #p2 { background: linear-gradient(145deg, #E3D5FF 0%, #D5F0FF 100%); }
    #p3 { background: linear-gradient(145deg, #D5FFE8 0%, #FFFAD5 100%); }

    /* ---- DECORATIVE BLOBS ---- */
    .blob {
      position: absolute;
      border-radius: 50%;
      filter: blur(60px);
      opacity: 0.35;
      pointer-events: none;
    }

    /* ---- NAV DOTS ---- */
    .nav-dots {
      position: fixed;
      bottom: 24px; left: 50%;
      transform: translateX(-50%);
      display: flex; gap: 10px;
      z-index: 100;
    }
    .dot-btn {
      width: 12px; height: 12px;
      border-radius: 50%;
      border: 2.5px solid var(--pink);
      background: transparent;
      cursor: pointer;
      transition: background 0.3s, transform 0.3s;
    }
    .dot-btn.active {
      background: var(--pink);
      transform: scale(1.3);
    }

    /* ---- ARROW BUTTONS ---- */
    .arrow {
      position: fixed;
      top: 50%; transform: translateY(-50%);
      background: white;
      border: none;
      width: 40px; height: 40px;
      border-radius: 50%;
      font-size: 18px;
      cursor: pointer;
      box-shadow: 0 4px 16px rgba(0,0,0,0.12);
      z-index: 100;
      transition: transform 0.2s, box-shadow 0.2s;
      display: flex; align-items: center; justify-content: center;
    }
    .arrow:hover { transform: translateY(-50%) scale(1.1); box-shadow: 0 6px 20px rgba(0,0,0,0.18); }
    #prev-btn { left: 14px; }
    #next-btn { right: 14px; }
    .arrow.hidden { opacity: 0; pointer-events: none; }

    /* ---- PAGE 1: WELCOME ---- */
    .crown { font-size: 56px; animation: bounce 1.4s ease-in-out infinite; }
    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50%       { transform: translateY(-12px); }
    }
    .birthday-title {
      font-family: 'Pacifico', cursive;
      font-size: clamp(2rem, 9vw, 3.4rem);
      color: var(--deep);
      text-align: center;
      line-height: 1.2;
      margin: 12px 0 6px;
    }
    .birthday-title span { color: var(--pink); }
    .subtitle {
      font-size: 1rem;
      color: #8A6B9A;
      margin-bottom: 32px;
      text-align: center;
    }
    .btn {
      background: linear-gradient(135deg, var(--pink), var(--lavender));
      color: white;
      border: none;
      padding: 14px 36px;
      border-radius: 50px;
      font-family: 'Nunito', sans-serif;
      font-size: 1rem;
      font-weight: 800;
      cursor: pointer;
      box-shadow: 0 6px 20px rgba(255,110,180,0.4);
      transition: transform 0.2s, box-shadow 0.2s;
      letter-spacing: 0.5px;
    }
    .btn:hover { transform: translateY(-3px); box-shadow: 0 10px 28px rgba(255,110,180,0.5); }
    .btn:active { transform: translateY(0); }

    .floating-emojis {
      position: absolute; inset: 0;
      pointer-events: none; overflow: hidden;
    }
    .fem {
      position: absolute;
      font-size: 24px;
      animation: floatup linear infinite;
      opacity: 0;
    }
    @keyframes floatup {
      0%   { transform: translateY(10px) scale(0.8); opacity: 0; }
      20%  { opacity: 1; }
      80%  { opacity: 1; }
      100% { transform: translateY(-120px) scale(1.1); opacity: 0; }
    }

    /* ---- PAGE 2: MESSAGE ---- */
    .card {
      background: white;
      border-radius: 24px;
      padding: 28px 26px;
      max-width: 420px;
      width: 100%;
      box-shadow: 0 8px 40px rgba(180,120,220,0.15);
      position: relative;
      z-index: 1;
    }
    .card-emoji { font-size: 42px; text-align: center; display: block; margin-bottom: 10px; }
    .card-title {
      font-family: 'Pacifico', cursive;
      font-size: 1.6rem;
      color: var(--deep);
      text-align: center;
      margin-bottom: 14px;
    }
    .card-text {
      font-size: 1rem;
      color: #6B4E8A;
      line-height: 1.75;
      text-align: center;
    }
    .card-text .highlight {
      color: var(--pink);
      font-weight: 800;
    }
    .divider {
      width: 48px; height: 4px;
      border-radius: 10px;
      background: linear-gradient(90deg, var(--pink), var(--lavender));
      margin: 16px auto;
    }

    /* ---- PAGE 3: WISHLIST ---- */
    .wish-title {
      font-family: 'Pacifico', cursive;
      font-size: clamp(1.5rem, 7vw, 2.2rem);
      color: var(--deep);
      text-align: center;
      margin-bottom: 6px;
    }
    .wish-sub {
      font-size: 0.95rem;
      color: #5A8A70;
      text-align: center;
      margin-bottom: 22px;
    }
    .wish-form {
      background: white;
      border-radius: 24px;
      padding: 24px 22px;
      max-width: 420px;
      width: 100%;
      box-shadow: 0 8px 40px rgba(100,200,150,0.15);
    }
    .wish-label {
      font-weight: 700;
      font-size: 0.88rem;
      color: #3D7A5C;
      display: block;
      margin-bottom: 6px;
    }
    .wish-input, .wish-textarea {
      width: 100%;
      border: 2px solid #D0F0E0;
      border-radius: 14px;
      padding: 11px 14px;
      font-family: 'Nunito', sans-serif;
      font-size: 0.95rem;
      color: var(--deep);
      outline: none;
      transition: border-color 0.3s;
      background: #F8FFFB;
      margin-bottom: 14px;
        text-align: left;
    }
    .wish-input:focus, .wish-textarea:focus {
      border-color: var(--mint);
    }
    .wish-textarea { resize: none; height: 180px; }
    .wish-btn {
      background: linear-gradient(135deg, var(--mint), #56C9A0);
      color: white;
      border: none;
      width: 100%;
      padding: 13px;
      border-radius: 50px;
      font-family: 'Nunito', sans-serif;
      font-weight: 800;
      font-size: 1rem;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
      box-shadow: 0 6px 20px rgba(126,235,181,0.45);
    }
    .wish-btn:hover { transform: translateY(-2px); }
    .wish-btn:active { transform: translateY(0); }

    .success-msg {
      display: none;
      text-align: center;
      font-weight: 700;
      color: #3D7A5C;
      font-size: 1rem;
      margin-top: 12px;
      animation: popIn 0.4s cubic-bezier(.34,1.56,.64,1);
    }
    @keyframes popIn {
      from { transform: scale(0.7); opacity: 0; }
      to   { transform: scale(1);   opacity: 1; }
    }

    /* ---- RESPONSIVE ---- */
    @media (max-width: 480px) {
      .arrow { width: 34px; height: 34px; font-size: 15px; }
      #prev-btn { left: 8px; }
      #next-btn { right: 8px; }
    }
  </style>
</head>
<body>

<!-- Confetti -->
<div class="confetti-container" id="confetti"></div>

<!-- Nav arrows -->
<button class="arrow hidden" id="prev-btn">◀</button>
<button class="arrow" id="next-btn">▶</button>

<!-- Nav dots -->
<div class="nav-dots">
  <button class="dot-btn active" data-page="0"></button>
  <button class="dot-btn" data-page="1"></button>
  <button class="dot-btn" data-page="2"></button>
</div>

<!-- PAGES -->
<div id="pages">

  <!-- PAGE 1: Welcome -->
  <div class="page active" id="p1">
    <div class="blob" style="width:200px;height:200px;background:var(--pink);top:-60px;left:-60px;"></div>
    <div class="blob" style="width:180px;height:180px;background:var(--peach);bottom:-40px;right:-40px;"></div>
    <div class="floating-emojis" id="floatEmojis"></div>

    <div class="crown">👑</div>
    <h1 class="birthday-title">Happy Birthday,<br><span>Rachel!</span> 🎀</h1>
    <p class="subtitle">Today is all about you, girl ✨</p>
    <button class="btn" onclick="goTo(1)">Open your surprise 🎁</button>
  </div>

  <!-- PAGE 2: Message -->
  <div class="page next" id="p2">
    <div class="blob" style="width:220px;height:220px;background:var(--lavender);top:-80px;right:-60px;"></div>
    <div class="blob" style="width:160px;height:160px;background:#A8D8FF;bottom:-40px;left:-40px;"></div>

    <div class="card">
      <span class="card-emoji">💌</span>
      <h2 class="card-title">A little note for you</h2>
      <div class="divider"></div>
      <p class="card-text">
        Haii <span class="highlight">Rachel</span>! 🥳<br><br>
I wanted to take a moment to tell you how much of a difference you make 
just by being yourself. You have this incredible spark that makes you so special, and different from any girl that I've ever met.
And being around you is always the highlight of my day.
<br><br>
I hope today is everything you’ve dreamed of.
<br><br>
You’re an <span class="highlight">amazing</span> person, 
and you deserve to be celebrated today and every day. 🌸✨
      </p>
      <div class="divider"></div>
      <button class="btn" style="margin-top:10px; width:100%;" onclick="goTo(2)">Now… what do you want? 🎀</button>
    </div>
  </div>

  <!-- PAGE 3: Wishlist -->
  <div class="page next" id="p3">
    <div class="blob" style="width:200px;height:200px;background:var(--mint);top:-60px;left:-60px;"></div>
    <div class="blob" style="width:170px;height:170px;background:var(--peach);bottom:-50px;right:-30px;"></div>

    <h2 class="wish-title"><span id="secretStar" style="cursor:pointer;user-select:none;">🌟</span> Do you want Robux? </h2>
    <p class="wish-sub">This time, I'll give you some Robux! 🎁</p>

    <div class="wish-form">
      <label class="wish-label">Your Username Account 🙍‍♀️</label>
      <input class="wish-input" type="text" placeholder="Pastiin bener yaa, kalo salah ya bakalan hangus" id="wName" />

      <label class="wish-label">How many robux are you wishing for? 🌠</label>
      <textarea class="wish-textarea" placeholder="Ada maksimalnya, cuma gabakal gw kasih tau 😈

Kelebihan = Gajadi gw beliin Robux 🫢
Tapi Minimal lu mintanya 100 Robux" id="wWish"></textarea>

      <label class="wish-label">Any birthday plans? 🎉</label>
      <input class="wish-input" type="text" placeholder="Ulang tahun gini mau kemana? dirumah? 🫢" id="wPlans" />

      <button class="wish-btn" onclick="submitWish()">Send my wish ✨</button>
      <p class="success-msg" id="successMsg">🎊 Yay! Your wish has been sent! 🎊</p>
    </div>
  </div>

</div>

<script>
  // ---- PAGE LOGIC ----
  const pages = ['p1','p2','p3'];
  let current = 0;

  function goTo(index) {
    const prev = document.getElementById(pages[current]);
    const next = document.getElementById(pages[index]);

    if (index > current) {
      prev.className = 'page prev';
      next.className = 'page active';
    } else {
      prev.className = 'page next';
      next.className = 'page active';
    }

    current = index;
    updateNav();
  }

  function updateNav() {
    document.getElementById('prev-btn').classList.toggle('hidden', current === 0);
    document.getElementById('next-btn').classList.toggle('hidden', current === pages.length - 1);
    document.querySelectorAll('.dot-btn').forEach((d, i) => {
      d.classList.toggle('active', i === current);
    });
  }

  document.getElementById('prev-btn').onclick = () => { if (current > 0) goTo(current - 1); };
  document.getElementById('next-btn').onclick = () => { if (current < pages.length - 1) goTo(current + 1); };
  document.querySelectorAll('.dot-btn').forEach(d => {
    d.onclick = () => goTo(+d.dataset.page);
  });

  // ---- SWIPE ----
  let touchStartX = 0;
  document.addEventListener('touchstart', e => { touchStartX = e.touches[0].clientX; });
  document.addEventListener('touchend', e => {
    const diff = touchStartX - e.changedTouches[0].clientX;
    if (Math.abs(diff) > 50) {
      if (diff > 0 && current < pages.length - 1) goTo(current + 1);
      if (diff < 0 && current > 0) goTo(current - 1);
    }
  });

  // ---- CONFETTI ----
  const confettiContainer = document.getElementById('confetti');
  const colors = ['#FF6EB4','#FFB347','#C9A0FF','#7EEBB5','#FF8FAB','#FFEAA7'];
  for (let i = 0; i < 30; i++) {
    const dot = document.createElement('div');
    dot.className = 'dot';
    dot.style.left = Math.random() * 100 + 'vw';
    dot.style.background = colors[Math.floor(Math.random() * colors.length)];
    dot.style.width = dot.style.height = (6 + Math.random() * 8) + 'px';
    dot.style.animationDuration = (4 + Math.random() * 6) + 's';
    dot.style.animationDelay = (Math.random() * 6) + 's';
    confettiContainer.appendChild(dot);
  }

  // ---- FLOATING EMOJIS PAGE 1 ----
  const emojis = ['🎂','🎈','🎁','🌸','✨','🎊','🍭'];
  const floatContainer = document.getElementById('floatEmojis');
  for (let i = 0; i < 10; i++) {
    const em = document.createElement('div');
    em.className = 'fem';
    em.textContent = emojis[Math.floor(Math.random() * emojis.length)];
    em.style.left = (5 + Math.random() * 90) + '%';
    em.style.bottom = '10px';
    em.style.animationDuration = (3 + Math.random() * 3) + 's';
    em.style.animationDelay = (Math.random() * 5) + 's';
    floatContainer.appendChild(em);
  }

  // ---- WISHLIST SUBMIT ----
  function submitWish() {
    const name = document.getElementById('wName').value.trim() || 'Rachel';
    const wish = document.getElementById('wWish').value.trim();
    const plans = document.getElementById('wPlans').value.trim();
    if (!wish) { alert('Tell us what you wish for! 🌟'); return; }

    const wishes = JSON.parse(localStorage.getItem('rachelWishes') || '[]');
    wishes.push({ name, wish, plans, time: new Date().toLocaleString() });
    localStorage.setItem('rachelWishes', JSON.stringify(wishes));

    document.getElementById('wName').value = '';
    document.getElementById('wWish').value = '';
    document.getElementById('wPlans').value = '';
    document.getElementById('successMsg').style.display = 'block';
    setTimeout(() => document.getElementById('successMsg').style.display = 'none', 3000);
  }

  // ---- SECRET ADMIN (tap star 15 times) ----
  let tapCount = 0;
  let tapTimer = null;
  document.getElementById('secretStar').addEventListener('click', () => {
    tapCount++;
    clearTimeout(tapTimer);
    tapTimer = setTimeout(() => { tapCount = 0; }, 2000);
    if (tapCount >= 50) {
      tapCount = 0;
      openAdmin();
    }
  });

  function openAdmin() {
    const wishes = JSON.parse(localStorage.getItem('rachelWishes') || '[]');
    const overlay = document.createElement('div');
    overlay.id = 'adminOverlay';
    overlay.style.cssText = `
      position:fixed;inset:0;background:rgba(30,10,50,0.97);z-index:9999;
      overflow-y:auto;padding:30px 20px;font-family:'Nunito',sans-serif;color:white;
    `;

    let html = `
      <div style="max-width:500px;margin:0 auto;">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:24px;">
          <h2 style="font-family:'Pacifico',cursive;font-size:1.8rem;color:#FF6EB4;">🎀 Rachel's Wishes</h2>
          <button onclick="document.getElementById('adminOverlay').remove()"
            style="background:#FF6EB4;border:none;color:white;padding:8px 18px;border-radius:20px;
            font-family:'Nunito',sans-serif;font-weight:800;cursor:pointer;font-size:0.9rem;">
            Close ✕
          </button>
        </div>
        <p style="color:#C9A0FF;font-size:0.9rem;margin-bottom:20px;">${wishes.length} wish${wishes.length !== 1 ? 'es' : ''} submitted 💫</p>
    `;

    if (wishes.length === 0) {
      html += `<div style="text-align:center;color:#888;padding:40px;">No wishes yet! 🌸</div>`;
    } else {
      wishes.slice().reverse().forEach((w, i) => {
        html += `
          <div style="background:rgba(255,255,255,0.08);border-radius:18px;padding:18px;margin-bottom:14px;border:1px solid rgba(255,110,180,0.2);">
            <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
              <span style="font-weight:800;color:#FF6EB4;font-size:1rem;">🌟 ${w.name}</span>
              <span style="font-size:0.75rem;color:#888;">${w.time}</span>
            </div>
            <p style="color:#E8D5FF;font-size:0.95rem;margin-bottom:6px;line-height:1.6;">💬 ${w.wish}</p>
            ${w.plans ? `<p style="color:#7EEBB5;font-size:0.88rem;">🎉 Plans: ${w.plans}</p>` : ''}
          </div>
        `;
      });

      html += `
        <button onclick="clearWishes()" style="
          background:transparent;border:2px solid #FF6EB4;color:#FF6EB4;
          padding:10px 24px;border-radius:20px;font-family:'Nunito',sans-serif;
          font-weight:700;cursor:pointer;margin-top:8px;font-size:0.9rem;">
          🗑️ Clear all wishes
        </button>
      `;
    }

    html += `</div>`;
    overlay.innerHTML = html;
    document.body.appendChild(overlay);
  }

  function clearWishes() {
    if (confirm('Are you sure you want to clear all wishes?')) {
      localStorage.removeItem('rachelWishes');
      document.getElementById('adminOverlay').remove();
    }
  }
</script>
</body>
</html>
