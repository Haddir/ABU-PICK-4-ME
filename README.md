ass="step-num">1</div>
      <h3>Tell Us Your Mood</h3>
      <p>Budget, cravings, or location — just say it on WhatsApp in plain English.</p>
    </div>
    <div class="step reveal">
      <div class="step-num">2</div>
      <h3>Chef Francois Picks</h3>
      <p>Our AI butler scans nearby vendors and finds your best options instantly.</p>
    </div>
    <div class="step reveal">
      <div class="step-num">3</div>
      <h3>Eat &amp; Earn Coins</h3>
      <p>Every recommendation earns you ABU Coins — redeem for discounts and free meals.</p>
    </div>
  </div>
</section>

<div class="section-divider"></div>

<!-- SIGNUP FORM -->
<section class="signup-section" id="signup">
  <div class="section-label" style="color: var(--green-light);">Join Early Access</div>
  <h2>Get In. Eat Better.</h2>
  <p>Quick signup. We collect the rest conversationally.</p>

  <div class="signup-card">
    <form id="signupForm">
      <div class="form-row">
        <div class="form-field">
          <span class="field-icon">👤</span>
          <input type="text" id="fname" placeholder="Your Name" required autocomplete="off"/>
        </div>
        <div class="form-field">
          <span class="field-icon">💬</span>
          <input type="tel" id="fwa" placeholder="WhatsApp Number (e.g. 0801...)" required autocomplete="off"/>
        </div>
        <div class="form-field">
          <span class="field-icon">📍</span>
          <select id="flocation">
            <option value="" disabled selected>Where do you stay?</option>
            <option>Samaru</option>
            <option>Main Campus</option>
            <option>Soba</option>
            <option>Town Area</option>
            <option>Other</option>
          </select>
        </div>
      </div>

      <p class="signup-note">
        <strong>That's it!</strong> Chef Francois will ask about your mood, budget, and cravings
        right on WhatsApp — no long forms needed. 🎉
      </p>

      <button class="btn-signup" type="submit">
        💬 Sign Up &amp; Start Chatting →
      </button>

      <div class="coin-bonus">🪙 +20 ABU Coins just for signing up!</div>
    </form>
    <div class="success-msg" id="successMsg">
      <span class="big-check">🎉</span>
      <strong>You're in, [name]!</strong><br/>
      Chef Francois will message you on WhatsApp shortly.
      <br/><br/>
      <a class="btn-primary" href="https://wa.me/2348025317032" target="_blank" style="margin:0 auto;">
        💬 Chat Now
      </a>
    </div>
  </div>
</section>

<!-- COINS SECTION -->
<section class="coins-section">
  <div class="section-label reveal">Rewards</div>
  <h2 class="reveal">Earn ABU Coins. Eat for Less.</h2>
  <p class="reveal">Simple points. Real discounts. No wallets, no blockchain.</p>

  <div class="coins-grid">
    <div class="coin-card reveal">
      <div class="coin-emoji">👤</div>
      <div class="coin-action">Sign Up</div>
      <div class="coin-reward">+20 Coins</div>
    </div>
    <div class="coin-card reveal">
      <div class="coin-emoji">👥</div>
      <div class="coin-action">Refer a Friend</div>
      <div class="coin-reward">+50 Coins</div>
    </div>
    <div class="coin-card reveal">
      <div class="coin-emoji">📅</div>
      <div class="coin-action">Daily Check-in</div>
      <div class="coin-reward">+5 Coins</div>
    </div>
    <div class="coin-card reveal">
      <div class="coin-emoji">⭐</div>
      <div class="coin-action">Write a Review</div>
      <div class="coin-reward">+10 Coins</div>
    </div>
  </div>

  <div class="coins-use">
    <div class="use-chip">💎 Meal Discounts</div>
    <div class="use-chip">🎁 Special Deals</div>
    <div class="use-chip">🍽️ Free Meals</div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">👨‍🍳 ABU Pick4Me</div>
  <p>Your Campus Food Butler — Built with 💚 in ABU</p>
  <div class="footer-contact">
    <a href="https://wa.me/2348025317032" target="_blank">💬 WhatsApp</a>
    <a href="#">About</a>
    <a href="#">Privacy</a>
    <a href="#">Terms</a>
  </div>
  <p>© 2026 ABU Pick4Me · Early Access · Launching inside ABU</p>
</footer>

<script>
  // ── CRAVING PICKER ──
  const cravingBtns = document.querySelectorAll('.craving-btn');
  const cravingResult = document.getElementById('cravingResult');
  const cravingTitle = document.getElementById('cravingTitle');
  const cravingBody = document.getElementById('cravingBody');
  const cravingWA = document.getElementById('cravingWA');

  const messages = {
    'Jollof Rice': ['🍛 Jollof Rice Picks Near You', '3 top vendors in Samaru are serving right now. Chef Francois has your best options ready.'],
    'Shawarma': ['🌯 Shawarma Spots Ready', 'Fresh shawarma from 2 verified ABU vendors. Tap to get the full picks on WhatsApp.'],
    'Suya': ['🔥 Suya Vibes Detected', 'Evening suya? We know the best spot. Chef Francois has the scoop.'],
    'Noodles': ['🍜 Noodles It Is', 'Budget meal? Great call. Chef Francois has your quick noodle picks ready.'],
    'Snacks': ['🥤 Snack Time', 'Quick bites near your hostel. Tap to see what\'s available right now.'],
  };

  cravingBtns.forEach(btn => {
    btn.addEventListener('click', () => {
      cravingBtns.forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      const food = btn.dataset.food;
      const wa = btn.dataset.wa;
      cravingTitle.textContent = messages[food][0];
      cravingBody.textContent = messages[food][1];
      cravingResult.classList.add('show');
      cravingWA.href = `https://wa.me/2348025317032?text=Hi+Chef+Francois!+I%27m+craving+${encodeURIComponent(food)}+right+now.+Please+help+me+find+the+best+option+near+me.`;

      // track click
      trackEvent('craving_pick', { food });
    });
  });

  // ── SIGNUP FORM ──
  document.getElementById('signupForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const name = document.getElementById('fname').value.trim();
    const phone = document.getElementById('fwa').value.trim();
    const location = document.getElementById('flocation').value;

    if (!name || !phone || !location) {
      // shake the card to hint missing fields
      const card = document.querySelector('.signup-card');
      card.style.animation = 'shake 0.4s ease';
      setTimeout(() => card.style.animation = '', 500);
      return;
    }

    trackEvent('signup', { name, location });

    // ── SAVE TO GOOGLE SHEET ──
    // Paste your Apps Script Web App URL below after deployment:
    const SHEET_URL = "PASTE_YOUR_APPS_SCRIPT_URL_HERE";

    const payload = { name, phone, location, source: "Landing Page" };

    if (SHEET_URL !== "PASTE_YOUR_APPS_SCRIPT_URL_HERE") {
      fetch(SHEET_URL, {
        method: "POST",
        mode: "no-cors",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload)
      }).catch(err => console.warn("Sheet save failed:", err));
    } else {
      console.warn("⚠️ Google Sheet URL not set yet. Paste your Apps Script URL into SHEET_URL.");
    }

    // Show success state
    document.getElementById('signupForm').style.display = 'none';
    const msg = document.getElementById('successMsg');
    msg.innerHTML = msg.innerHTML.replace('[name]', name.split(' ')[0]);
    msg.style.display = 'block';

    // Redirect to WhatsApp
    const waMsg = `Hi Chef Francois! 👋 I just signed up as ${name} from ${location}. My number is ${phone}. Ready to discover great food! 🍛`;
    const waURL = `https://wa.me/2348025317032?text=${encodeURIComponent(waMsg)}`;

    setTimeout(() => {
      window.location.href = waURL;
    }, 800);
  });

  // ── SCROLL REVEAL ──
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
  }, { threshold: 0.15 });
  reveals.forEach(el => observer.observe(el));

  // ── BASIC ANALYTICS TRACKER ──
  const analytics = { pageviews: 0, clicks: {}, signups: 0 };

  function trackEvent(event, data) {
    analytics.clicks[event] = (analytics.clicks[event] || 0) + 1;
    console.log('[ABU Pick4Me Analytics]', event, data);
    // Replace this log with your actual analytics endpoint when ready
    // e.g. fetch('/api/track', { method: 'POST', body: JSON.stringify({ event, data }) });
  }

  // Track WA CTA clicks
  document.querySelectorAll('a[href*="wa.me"]').forEach(a => {
    a.addEventListener('click', () => trackEvent('wa_cta_click', { href: a.href }));
  });

  // Track page load
  trackEvent('page_view', { ts: Date.now() });

  // ── CHEF BUBBLE ROTATION ──
  const chefLines = [
    "What are you craving today? 🍛",
    "Jollof or Shawarma? I'll decide! 😄",
    "Best food near Samaru right now 🗺️",
    "Low budget? I've got you covered 💚",
    "Students eat well too! Let's go 🔥",
    "Chef Francois at your service! 👨‍🍳",
  ];
  let chefIdx = 0;
  const bubbleEl = document.getElementById('chefBubble');
  if (bubbleEl) {
    setInterval(() => {
      chefIdx = (chefIdx + 1) % chefLines.length;
      bubbleEl.style.opacity = '0';
      bubbleEl.style.transform = 'translateY(4px)';
      setTimeout(() => {
        bubbleEl.textContent = chefLines[chefIdx];
        bubbleEl.style.opacity = '1';
        bubbleEl.style.transform = 'translateY(0)';
      }, 350);
    }, 3000);
    bubbleEl.style.transition = 'opacity 0.35s ease, transform 0.35s ease';
  }

  // ── LIVE COUNTER ROTATION ──
  const messages2 = [
    'Today\'s top pick in Samaru: Jollof Rice 🍛',
    '12 students checked dinner recs this hour',
    '3 new vendors joined this week 🏪',
    'Shawarma trending in North Campus 🌯',
    'Early access spots filling up fast 🔥',
  ];
  const dots = document.querySelectorAll('.activity-item');
  let msgIdx = 0;
  setInterval(() => {
    msgIdx = (msgIdx + 1) % messages2.length;
    if (dots[0]) dots[0].querySelector('span').textContent = messages2[msgIdx];
  }, 4000);
</script>
</body>
</html>
 page for Food suggestion bot, which would redirect you to WhatsApp bot after successful sign up.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>ABU Pick4Me – Find What To Eat in ABU Instantly</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=DM+Sans:wght@400;500;600&display=swap" rel="stylesheet"/>
<style>
  :root {
    --green: #1a9e52;
    --green-light: #25c467;
    --green-dim: #0f5e30;
    --yellow: #f7c948;
    --orange: #f4813a;
    --cream: #fdf8f0;
    --dark: #0e1a10;
    --text: #1c2d1e;
    --muted: #5a7060;
    --wa: #25D366;
    --radius: 16px;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--cream);
    color: var(--text);
    overflow-x: hidden;
  }

  h1, h2, h3, .logo-text { font-family: 'Syne', sans-serif; }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 14px 24px;
    background: rgba(253,248,240,0.88);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(26,158,82,0.1);
  }
  .logo { display: flex; align-items: center; gap: 8px; text-decoration: none; }
  .logo-icon { font-size: 22px; }
  .logo-text { font-size: 18px; font-weight: 800; color: var(--green-dim); }
  .logo-text span { color: var(--green); }
  .nav-cta {
    background: var(--wa); color: #fff;
    border: none; border-radius: 50px; padding: 9px 18px;
    font-family: 'DM Sans', sans-serif; font-size: 14px; font-weight: 600;
    cursor: pointer; text-decoration: none;
    display: flex; align-items: center; gap: 6px;
    transition: transform 0.2s, box-shadow 0.2s;
  }
  .nav-cta:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(37,211,102,0.35); }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    padding: 100px 24px 60px;
    text-align: center;
    position: relative;
    background: radial-gradient(ellipse 80% 60% at 50% 20%, rgba(26,158,82,0.08) 0%, transparent 70%);
  }

  /* Floating coins */
  .coin {
    position: absolute;
    width: 38px; height: 38px;
    background: linear-gradient(135deg, var(--yellow), #e8a800);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 16px;
    box-shadow: 0 4px 14px rgba(247,201,72,0.45);
    animation: floatCoin 4s ease-in-out infinite;
    opacity: 0.9;
  }
  .coin:nth-child(1) { top: 18%; left: 8%; animation-delay: 0s; }
  .coin:nth-child(2) { top: 32%; right: 7%; animation-delay: 1.2s; }
  .coin:nth-child(3) { bottom: 28%; left: 12%; animation-delay: 2.4s; }
  @keyframes floatCoin {
    0%, 100% { transform: translateY(0) rotate(0deg); }
    50% { transform: translateY(-14px) rotate(8deg); }
  }

  /* WA ping animation */
  .wa-ping {
    position: absolute;
    top: 22%; right: 5%;
    background: #fff;
    border-radius: 12px;
    padding: 10px 14px;
    font-size: 12px;
    font-weight: 600;
    color: var(--text);
    box-shadow: 0 4px 20px rgba(0,0,0,0.12);
    display: flex; align-items: center; gap: 6px;
    animation: waPing 3.5s ease-in-out infinite;
    white-space: nowrap;
  }
  .wa-ping::before {
    content: '';
    width: 8px; height: 8px; background: var(--wa);
    border-radius: 50%;
    animation: pulse 1.5s ease-in-out infinite;
  }
  @keyframes waPing {
    0%, 100% { transform: translateX(0); opacity: 1; }
    50% { transform: translateX(-4px); opacity: 0.85; }
  }
  @keyframes pulse {
    0%, 100% { transform: scale(1); opacity: 1; }
    50% { transform: scale(1.5); opacity: 0.6; }
  }

  .hero-badge {
    display: inline-flex; align-items: center; gap: 6px;
    background: rgba(26,158,82,0.1);
    border: 1px solid rgba(26,158,82,0.25);
    border-radius: 50px; padding: 6px 14px;
    font-size: 12px; font-weight: 600;
    color: var(--green-dim); letter-spacing: 0.5px;
    text-transform: uppercase; margin-bottom: 24px;
    animation: fadeUp 0.6s ease both;
  }

  .hero h1 {
    font-size: clamp(2rem, 6vw, 3.8rem);
    line-height: 1.1;
    color: var(--dark);
    max-width: 700px;
    margin-bottom: 18px;
    animation: fadeUp 0.6s 0.1s ease both;
  }
  .hero h1 .accent { color: var(--green); }

  .hero-sub {
    font-size: clamp(15px, 2.5vw, 18px);
    color: var(--muted);
    max-width: 480px;
    margin: 0 auto 16px;
    line-height: 1.6;
    animation: fadeUp 0.6s 0.2s ease both;
  }

  /* Emotional hook */
  .hero-hook {
    display: inline-block;
    background: linear-gradient(135deg, #fff8e6, #fff3d4);
    border: 1px solid rgba(247,201,72,0.4);
    border-radius: 12px;
    padding: 10px 18px;
    font-size: 14px; font-weight: 500;
    color: #7a5a00;
    margin-bottom: 32px;
    animation: fadeUp 0.6s 0.3s ease both;
  }

  .hero-cta-group {
    display: flex; gap: 12px; justify-content: center; flex-wrap: wrap;
    margin-bottom: 36px;
    animation: fadeUp 0.6s 0.4s ease both;
  }
  .btn-primary {
    background: var(--wa); color: #fff;
    border: none; border-radius: 50px;
    padding: 15px 28px; font-size: 16px; font-weight: 700;
    cursor: pointer; text-decoration: none;
    display: flex; align-items: center; gap: 8px;
    font-family: 'DM Sans', sans-serif;
    transition: transform 0.2s, box-shadow 0.2s;
    box-shadow: 0 6px 24px rgba(37,211,102,0.4);
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 10px 32px rgba(37,211,102,0.5); }
  .btn-secondary {
    background: transparent; color: var(--green-dim);
    border: 2px solid rgba(26,158,82,0.35);
    border-radius: 50px; padding: 13px 24px;
    font-size: 15px; font-weight: 600; cursor: pointer;
    font-family: 'DM Sans', sans-serif; text-decoration: none;
    transition: border-color 0.2s, background 0.2s;
  }
  .btn-secondary:hover { border-color: var(--green); background: rgba(26,158,82,0.06); }

  /* Social proof strip */
  .proof-strip {
    display: flex; align-items: center; gap: 16px; justify-content: center;
    font-size: 13px; color: var(--muted); flex-wrap: wrap;
    animation: fadeUp 0.6s 0.5s ease both;
  }
  .proof-strip .dot { width: 4px; height: 4px; background: var(--muted); border-radius: 50%; }
  .proof-badge {
    background: rgba(26,158,82,0.08);
    border-radius: 50px; padding: 5px 12px;
    color: var(--green-dim); font-weight: 600; font-size: 12px;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── CRAVING PICKER ── */
  .craving-section {
    padding: 70px 24px;
    text-align: center;
    background: #fff;
    border-top: 1px solid rgba(26,158,82,0.1);
    border-bottom: 1px solid rgba(26,158,82,0.1);
  }
  .section-label {
    font-size: 11px; font-weight: 700; letter-spacing: 2px;
    color: var(--green); text-transform: uppercase; margin-bottom: 12px;
  }
  .craving-section h2 {
    font-size: clamp(1.6rem, 4vw, 2.4rem);
    color: var(--dark); margin-bottom: 10px;
  }
  .craving-section p { color: var(--muted); font-size: 15px; margin-bottom: 36px; }

  .craving-grid {
    display: flex; flex-wrap: wrap; gap: 14px;
    justify-content: center; max-width: 560px; margin: 0 auto 32px;
  }
  .craving-btn {
    display: flex; align-items: center; gap: 10px;
    background: var(--cream); border: 2px solid transparent;
    border-radius: 50px; padding: 14px 22px;
    font-size: 16px; font-weight: 600; color: var(--text);
    cursor: pointer; font-family: 'DM Sans', sans-serif;
    transition: all 0.2s; user-select: none;
  }
  .craving-btn:hover, .craving-btn.active {
    border-color: var(--green);
    background: rgba(26,158,82,0.07);
    color: var(--green-dim);
    transform: scale(1.04);
  }
  .craving-btn .emoji { font-size: 22px; }

  .craving-result {
    display: none;
    background: linear-gradient(135deg, var(--green-dim), var(--green));
    color: #fff; border-radius: var(--radius);
    padding: 20px 24px; max-width: 400px; margin: 0 auto 24px;
    font-size: 15px; font-weight: 500; line-height: 1.5;
    animation: fadeUp 0.3s ease both;
  }
  .craving-result.show { display: block; }
  .craving-result strong { display: block; font-size: 17px; margin-bottom: 4px; }

  /* ── LIVE ACTIVITY ── */
  .activity-bar {
    display: flex; justify-content: center; gap: 24px; flex-wrap: wrap;
    padding: 18px 24px;
    background: var(--dark);
  }
  .activity-item {
    display: flex; align-items: center; gap: 8px;
    color: rgba(255,255,255,0.75); font-size: 13px; font-weight: 500;
  }
  .activity-dot {
    width: 7px; height: 7px; background: var(--green-light);
    border-radius: 50%;
    animation: pulse 1.5s ease-in-out infinite;
  }

  /* ── HOW IT WORKS ── */
  .how-section {
    padding: 80px 24px;
    max-width: 1000px; margin: 0 auto; text-align: center;
  }
  .how-section h2 { font-size: clamp(1.6rem, 4vw, 2.4rem); margin-bottom: 10px; }
  .how-section > p { color: var(--muted); margin-bottom: 52px; font-size: 15px; }

  .steps {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 24px;
  }
  .step {
    background: #fff;
    border-radius: 20px; padding: 32px 24px;
    border: 1px solid rgba(26,158,82,0.1);
    transition: transform 0.2s, box-shadow 0.2s;
  }
  .step:hover { transform: translateY(-4px); box-shadow: 0 12px 36px rgba(0,0,0,0.07); }
  .step-num {
    width: 44px; height: 44px;
    background: linear-gradient(135deg, var(--green), var(--green-light));
    border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Syne', sans-serif; font-size: 18px; font-weight: 800;
    color: #fff; margin: 0 auto 18px;
  }
  .step h3 { font-size: 17px; margin-bottom: 8px; }
  .step p { color: var(--muted); font-size: 14px; line-height: 1.6; }

  /* ── SIGNUP FORM ── */
  .signup-section {
    padding: 80px 24px;
    background: linear-gradient(160deg, #0e1a10 0%, #1a3d22 100%);
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .signup-section::before {
    content: '';
    position: absolute; top: -60px; left: 50%;
    transform: translateX(-50%);
    width: 500px; height: 300px;
    background: radial-gradient(ellipse, rgba(37,196,103,0.18) 0%, transparent 70%);
  }
  .signup-section h2 { color: #fff; font-size: clamp(1.6rem, 4vw, 2.4rem); margin-bottom: 8px; }
  .signup-section > p { color: rgba(255,255,255,0.6); font-size: 15px; margin-bottom: 36px; }

  .signup-card {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 24px;
    padding: 36px 32px;
    max-width: 420px; margin: 0 auto;
    backdrop-filter: blur(10px);
    position: relative;
  }

  .form-row {
    display: flex; flex-direction: column; gap: 14px; margin-bottom: 20px;
  }
  .form-field {
    display: flex; align-items: center; gap: 12px;
    background: rgba(255,255,255,0.08);
    border: 1px solid rgba(255,255,255,0.15);
    border-radius: 12px; padding: 14px 18px;
    transition: border-color 0.2s;
  }
  .form-field:focus-within { border-color: var(--green-light); }
  .form-field .field-icon { font-size: 18px; flex-shrink: 0; }
  .form-field input, .form-field select {
    background: transparent; border: none; outline: none;
    color: #fff; font-family: 'DM Sans', sans-serif;
    font-size: 15px; width: 100%;
  }
  .form-field input::placeholder { color: rgba(255,255,255,0.4); }
  .form-field select option { background: #1a3d22; color: #fff; }

  .signup-note {
    font-size: 12px; color: rgba(255,255,255,0.4);
    margin-bottom: 20px; line-height: 1.6;
  }
  .signup-note strong { color: rgba(255,255,255,0.7); }

  .btn-signup {
    width: 100%;
    background: var(--wa); color: #fff;
    border: none; border-radius: 50px;
    padding: 16px; font-size: 16px; font-weight: 700;
    cursor: pointer; font-family: 'DM Sans', sans-serif;
    display: flex; align-items: center; justify-content: center; gap: 8px;
    transition: transform 0.2s, box-shadow 0.2s;
    box-shadow: 0 6px 24px rgba(37,211,102,0.3);
  }
  .btn-signup:hover { transform: translateY(-2px); box-shadow: 0 10px 30px rgba(37,211,102,0.4); }

  .coin-bonus {
    display: flex; align-items: center; justify-content: center; gap: 6px;
    margin-top: 14px;
    font-size: 13px; color: var(--yellow); font-weight: 600;
  }

  /* ── COINS ── */
  .coins-section {
    padding: 80px 24px;
    background: #fff;
    text-align: center;
  }
  .coins-section h2 { font-size: clamp(1.6rem, 4vw, 2.4rem); margin-bottom: 10px; }
  .coins-section > p { color: var(--muted); font-size: 15px; margin-bottom: 48px; }

  .coins-grid {
    display: flex; flex-wrap: wrap; justify-content: center; gap: 20px;
    max-width: 800px; margin: 0 auto;
  }
  .coin-card {
    background: var(--cream);
    border-radius: 20px; padding: 28px 24px;
    flex: 1; min-width: 160px; max-width: 200px;
    border: 1px solid rgba(26,158,82,0.1);
    transition: transform 0.2s;
    text-align: center;
  }
  .coin-card:hover { transform: translateY(-4px); }
  .coin-emoji { font-size: 32px; margin-bottom: 12px; }
  .coin-action { font-size: 13px; color: var(--muted); margin-bottom: 6px; }
  .coin-reward { font-family: 'Syne', sans-serif; font-size: 20px; font-weight: 800; color: var(--green); }

  .coins-use {
    display: flex; justify-content: center; gap: 24px; flex-wrap: wrap;
    margin-top: 36px;
  }
  .use-chip {
    background: linear-gradient(135deg, var(--yellow), #e8a800);
    border-radius: 50px; padding: 10px 20px;
    font-size: 14px; font-weight: 700; color: var(--dark);
    display: flex; align-items: center; gap: 6px;
  }

  /* ── FOOTER ── */
  footer {
    background: var(--dark);
    padding: 40px 24px;
    text-align: center;
    color: rgba(255,255,255,0.5);
    font-size: 13px;
  }
  footer .footer-logo { font-family: 'Syne', sans-serif; font-size: 20px; font-weight: 800; color: #fff; margin-bottom: 8px; }
  footer a { color: rgba(255,255,255,0.5); text-decoration: none; margin: 0 10px; }
  footer a:hover { color: var(--green-light); }
  .footer-contact { margin: 16px 0; }

  /* ── UTILITY ── */
  .section-divider {
    height: 1px; background: linear-gradient(90deg, transparent, rgba(26,158,82,0.2), transparent);
    margin: 0 24px;
  }

  /* scroll reveal */
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* ── CHEF SCENE ── */
  .chef-scene {
    position: relative;
    width: 320px; height: 380px;
    margin: 40px auto 0;
    flex-shrink: 0;
    animation: fadeUp 0.7s 0.6s ease both;
  }

  /* plate glow */
  .chef-scene::after {
    content: '';
    position: absolute;
    bottom: 0; left: 50%;
    transform: translateX(-50%);
    width: 160px; height: 28px;
    background: radial-gradient(ellipse, rgba(26,158,82,0.25) 0%, transparent 70%);
    border-radius: 50%;
  }

  /* steam particles */
  .steam {
    position: absolute;
    width: 6px; border-radius: 3px;
    background: rgba(255,255,255,0.7);
    animation: steamRise 2.2s ease-in infinite;
    bottom: 148px;
    filter: blur(1px);
  }
  .steam:nth-child(1) { left: 138px; height: 22px; animation-delay: 0s; }
  .steam:nth-child(2) { left: 152px; height: 30px; animation-delay: 0.5s; }
  .steam:nth-child(3) { left: 166px; height: 18px; animation-delay: 1s; }
  @keyframes steamRise {
    0%   { opacity: 0; transform: translateY(0) scaleX(1); }
    30%  { opacity: 0.8; }
    100% { opacity: 0; transform: translateY(-40px) scaleX(1.6); }
  }

  /* sparkle stars floating off plate */
  .sparkle {
    position: absolute;
    font-size: 14px;
    animation: sparkleFly 3s ease-in-out infinite;
    pointer-events: none;
  }
  .sparkle:nth-child(4) { bottom: 160px; left: 105px; animation-delay: 0s; }
  .sparkle:nth-child(5) { bottom: 155px; right: 95px; animation-delay: 1s; }
  .sparkle:nth-child(6) { bottom: 175px; left: 148px; animation-delay: 1.8s; }
  @keyframes sparkleFly {
    0%   { opacity: 0; transform: translateY(0) scale(0.5) rotate(0deg); }
    40%  { opacity: 1; transform: translateY(-24px) scale(1) rotate(20deg); }
    100% { opacity: 0; transform: translateY(-52px) scale(0.4) rotate(45deg); }
  }

  /* chef body bob */
  .chef-svg {
    animation: chefBob 3s ease-in-out infinite;
    transform-origin: center bottom;
  }
  @keyframes chefBob {
    0%, 100% { transform: translateY(0); }
    50%       { transform: translateY(-8px); }
  }

  /* arm stir */
  .chef-arm-right {
    animation: stirArm 1.4s ease-in-out infinite;
    transform-origin: 220px 195px;
  }
  @keyframes stirArm {
    0%, 100% { transform: rotate(0deg); }
    50%       { transform: rotate(14deg); }
  }

  /* eye blink */
  .chef-eye-l, .chef-eye-r {
    animation: blink 4s ease-in-out infinite;
    transform-origin: center;
  }
  @keyframes blink {
    0%, 92%, 100% { transform: scaleY(1); }
    95%            { transform: scaleY(0.1); }
  }

  /* hat wiggle */
  .chef-hat {
    animation: hatWiggle 3s ease-in-out infinite;
    transform-origin: center bottom;
  }
  @keyframes hatWiggle {
    0%, 100% { transform: rotate(0deg); }
    25%       { transform: rotate(-2deg); }
    75%       { transform: rotate(2deg); }
  }

  /* food items orbit on plate */
  .food-orbit {
    animation: orbitFood 4s linear infinite;
    transform-origin: 160px 320px;
  }
  .food-orbit:nth-child(7) { animation-delay: 0s; }
  .food-orbit:nth-child(8) { animation-delay: 1.33s; }
  .food-orbit:nth-child(9) { animation-delay: 2.66s; }
  @keyframes orbitFood {
    0%   { opacity: 0; transform: translate(0,0) scale(0.5); }
    15%  { opacity: 1; transform: translate(0,-18px) scale(1); }
    85%  { opacity: 1; }
    100% { opacity: 0; transform: translate(0,-18px) scale(0.5); }
  }

  /* AI badge pulse on chef */
  .ai-badge-chef {
    position: absolute;
    top: 12px; right: 12px;
    background: linear-gradient(135deg, var(--green), var(--green-light));
    color: #fff; font-size: 10px; font-weight: 800;
    padding: 4px 9px; border-radius: 50px;
    font-family: 'Syne', sans-serif; letter-spacing: 0.5px;
    animation: badgePulse 2s ease-in-out infinite;
    box-shadow: 0 0 12px rgba(37,196,103,0.6);
  }
  @keyframes badgePulse {
    0%, 100% { box-shadow: 0 0 8px rgba(37,196,103,0.5); }
    50%       { box-shadow: 0 0 22px rgba(37,196,103,0.9); }
  }

  /* speech bubble */
  .chef-bubble {
    position: absolute;
    top: 20px; left: -30px;
    background: #fff;
    border-radius: 14px;
    padding: 10px 14px;
    font-size: 12px; font-weight: 600;
    color: var(--text);
    box-shadow: 0 4px 16px rgba(0,0,0,0.12);
    white-space: nowrap;
    animation: bubbleFloat 4s ease-in-out infinite;
    max-width: 180px;
    white-space: normal;
    line-height: 1.4;
  }
  .chef-bubble::after {
    content: '';
    position: absolute;
    bottom: -7px; right: 24px;
    border: 7px solid transparent;
    border-top-color: #fff;
    border-bottom: none;
  }
  @keyframes bubbleFloat {
    0%, 100% { transform: translateY(0); }
    50%       { transform: translateY(-5px); }
  }

  /* mobile */
  @media (max-width: 600px) {
    .wa-ping { display: none; }
    .coin:nth-child(3) { display: none; }
    .signup-card { padding: 28px 20px; }
    .chef-scene { width: 260px; height: 310px; transform: scale(0.85); }
    .chef-bubble { left: -10px; font-size: 11px; }
  }

  /* success state */
  .success-msg {
    display: none;
    text-align: center; padding: 20px;
    color: #fff; font-size: 16px; font-weight: 600;
    animation: fadeUp 0.4s ease both;
  }
  .success-msg .big-check { font-size: 48px; display: block; margin-bottom: 10px; }

  @keyframes shake {
    0%, 100% { transform: translateX(0); }
    20% { transform: translateX(-8px); }
    40% { transform: translateX(8px); }
    60% { tra
