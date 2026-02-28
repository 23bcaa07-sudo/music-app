<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Velvet — Login</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #0a0708;
      --surface: #130f10;
      --border: rgba(255,255,255,0.07);
      --accent: #e8432d;
      --accent2: #f5a623;
      --text: #f2ede8;
      --muted: #7a6f6a;
      --input-bg: rgba(255,255,255,0.04);
    }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'DM Sans', sans-serif;
      min-height: 100vh;
      display: flex;
      overflow: hidden;
    }

    /* LEFT PANEL — Art */
    .art-panel {
      flex: 1;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .art-panel::before {
      content: '';
      position: absolute;
      inset: 0;
      background:
        radial-gradient(ellipse 60% 70% at 30% 50%, rgba(232,67,45,0.25) 0%, transparent 65%),
        radial-gradient(ellipse 50% 60% at 70% 30%, rgba(245,166,35,0.15) 0%, transparent 60%),
        radial-gradient(ellipse 80% 80% at 50% 80%, rgba(100,30,60,0.3) 0%, transparent 70%);
    }

    .vinyl {
      position: relative;
      width: 320px;
      height: 320px;
      animation: spin 8s linear infinite;
      filter: drop-shadow(0 0 60px rgba(232,67,45,0.4));
    }

    @keyframes spin {
      from { transform: rotate(0deg); }
      to   { transform: rotate(360deg); }
    }

    .vinyl svg {
      width: 100%;
      height: 100%;
    }

    .vinyl-label {
      position: absolute;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .vinyl-inner {
      width: 110px;
      height: 110px;
      border-radius: 50%;
      background: linear-gradient(135deg, #1a0e0a 0%, #2d1810 100%);
      border: 2px solid rgba(232,67,45,0.3);
      display: flex;
      align-items: center;
      justify-content: center;
      animation: spin-reverse 8s linear infinite;
    }

    @keyframes spin-reverse {
      from { transform: rotate(360deg); }
      to   { transform: rotate(0deg); }
    }

    .vinyl-inner span {
      font-family: 'Playfair Display', serif;
      font-size: 14px;
      color: var(--accent);
      letter-spacing: 2px;
      text-transform: uppercase;
    }

    /* Floating notes */
    .notes {
      position: absolute;
      inset: 0;
      pointer-events: none;
    }

    .note {
      position: absolute;
      font-size: 24px;
      opacity: 0;
      animation: float-note 6s ease-in-out infinite;
      color: var(--accent2);
    }

    .note:nth-child(1) { left: 15%; top: 20%; animation-delay: 0s; }
    .note:nth-child(2) { left: 75%; top: 35%; animation-delay: 1.5s; }
    .note:nth-child(3) { left: 25%; top: 70%; animation-delay: 3s; }
    .note:nth-child(4) { left: 65%; top: 75%; animation-delay: 4.5s; }
    .note:nth-child(5) { left: 50%; top: 15%; animation-delay: 2s; color: var(--accent); }

    @keyframes float-note {
      0%   { opacity: 0; transform: translateY(0) scale(0.8); }
      20%  { opacity: 0.6; }
      80%  { opacity: 0.3; }
      100% { opacity: 0; transform: translateY(-60px) scale(1.2); }
    }

    .tagline {
      position: absolute;
      bottom: 60px;
      left: 0; right: 0;
      text-align: center;
    }

    .tagline h1 {
      font-family: 'Playfair Display', serif;
      font-size: clamp(28px, 3vw, 44px);
      font-style: italic;
      line-height: 1.2;
      color: var(--text);
      opacity: 0;
      animation: fade-up 0.8s ease 0.3s forwards;
    }

    .tagline p {
      margin-top: 10px;
      color: var(--muted);
      font-size: 13px;
      letter-spacing: 3px;
      text-transform: uppercase;
      opacity: 0;
      animation: fade-up 0.8s ease 0.6s forwards;
    }

    @keyframes fade-up {
      from { opacity: 0; transform: translateY(16px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* Divider */
    .divider {
      width: 1px;
      background: var(--border);
      margin: 40px 0;
      align-self: stretch;
    }

    /* RIGHT PANEL — Form */
    .form-panel {
      width: 440px;
      min-height: 100vh;
      background: var(--surface);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 60px 50px;
      position: relative;
      opacity: 0;
      animation: slide-in 0.7s ease 0.2s forwards;
    }

    @keyframes slide-in {
      from { opacity: 0; transform: translateX(30px); }
      to   { opacity: 1; transform: translateX(0); }
    }

    .form-panel::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--accent), var(--accent2), transparent);
    }

    .logo {
      font-family: 'Playfair Display', serif;
      font-size: 32px;
      font-weight: 700;
      letter-spacing: -1px;
      margin-bottom: 8px;
      background: linear-gradient(135deg, var(--text) 40%, var(--accent) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .logo-sub {
      font-size: 11px;
      letter-spacing: 4px;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 48px;
    }

    .form-title {
      font-family: 'Playfair Display', serif;
      font-size: 22px;
      font-style: italic;
      color: var(--text);
      margin-bottom: 4px;
      align-self: flex-start;
    }

    .form-sub {
      font-size: 13px;
      color: var(--muted);
      margin-bottom: 32px;
      align-self: flex-start;
    }

    .form {
      width: 100%;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .field {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    label {
      font-size: 11px;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--muted);
    }

    .input-wrap {
      position: relative;
    }

    .input-wrap input {
      width: 100%;
      padding: 14px 16px 14px 44px;
      background: var(--input-bg);
      border: 1px solid var(--border);
      border-radius: 6px;
      color: var(--text);
      font-family: 'DM Sans', sans-serif;
      font-size: 14px;
      outline: none;
      transition: border-color 0.2s, background 0.2s;
    }

    .input-wrap input:focus {
      border-color: rgba(232,67,45,0.5);
      background: rgba(255,255,255,0.06);
    }

    .input-wrap input::placeholder { color: var(--muted); }

    .input-icon {
      position: absolute;
      left: 14px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--muted);
      font-size: 16px;
      pointer-events: none;
    }

    .eye-toggle {
      position: absolute;
      right: 14px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      color: var(--muted);
      font-size: 16px;
      background: none;
      border: none;
      padding: 0;
      transition: color 0.2s;
    }

    .eye-toggle:hover { color: var(--text); }

    .row {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .remember {
      display: flex;
      align-items: center;
      gap: 8px;
      cursor: pointer;
      font-size: 12px;
      color: var(--muted);
    }

    .remember input[type="checkbox"] {
      accent-color: var(--accent);
      width: 14px;
      height: 14px;
    }

    .forgot {
      font-size: 12px;
      color: var(--accent);
      text-decoration: none;
      transition: opacity 0.2s;
    }

    .forgot:hover { opacity: 0.7; }

    .btn-login {
      margin-top: 8px;
      width: 100%;
      padding: 15px;
      background: var(--accent);
      color: white;
      border: none;
      border-radius: 6px;
      font-family: 'DM Sans', sans-serif;
      font-size: 13px;
      font-weight: 500;
      letter-spacing: 2px;
      text-transform: uppercase;
      cursor: pointer;
      position: relative;
      overflow: hidden;
      transition: transform 0.15s, box-shadow 0.2s;
    }

    .btn-login::after {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(90deg, transparent 0%, rgba(255,255,255,0.15) 50%, transparent 100%);
      transform: translateX(-100%);
      transition: transform 0.5s;
    }

    .btn-login:hover { transform: translateY(-1px); box-shadow: 0 8px 30px rgba(232,67,45,0.4); }
    .btn-login:hover::after { transform: translateX(100%); }
    .btn-login:active { transform: translateY(0); }

    .or-row {
      display: flex;
      align-items: center;
      gap: 12px;
      margin: 4px 0;
    }

    .or-line { flex: 1; height: 1px; background: var(--border); }
    .or-text { font-size: 11px; color: var(--muted); letter-spacing: 2px; }

    .btn-social {
      width: 100%;
      padding: 13px;
      background: var(--input-bg);
      border: 1px solid var(--border);
      border-radius: 6px;
      color: var(--text);
      font-family: 'DM Sans', sans-serif;
      font-size: 13px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      transition: border-color 0.2s, background 0.2s;
    }

    .btn-social:hover { border-color: rgba(255,255,255,0.2); background: rgba(255,255,255,0.07); }

    .signup-row {
      margin-top: 32px;
      font-size: 13px;
      color: var(--muted);
      text-align: center;
    }

    .signup-row a {
      color: var(--accent2);
      text-decoration: none;
      font-weight: 500;
    }

    .signup-row a:hover { text-decoration: underline; }

    /* Now playing bar */
    .now-playing {
      position: absolute;
      bottom: 28px;
      left: 20px; right: 20px;
      background: rgba(255,255,255,0.04);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 12px 16px;
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .np-disc {
      width: 36px; height: 36px;
      border-radius: 50%;
      background: linear-gradient(135deg, #e8432d, #f5a623);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
      flex-shrink: 0;
      animation: spin 4s linear infinite;
    }

    .np-info { flex: 1; overflow: hidden; }
    .np-title { font-size: 12px; font-weight: 500; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .np-artist { font-size: 11px; color: var(--muted); margin-top: 2px; }

    .np-controls { display: flex; gap: 10px; align-items: center; }
    .np-btn { background: none; border: none; color: var(--muted); font-size: 14px; cursor: pointer; padding: 4px; transition: color 0.2s; }
    .np-btn:hover { color: var(--text); }
    .np-btn.play { color: var(--accent); font-size: 18px; }

    .progress-bar {
      position: absolute;
      bottom: 0; left: 0;
      width: 60%;
      height: 2px;
      background: var(--accent);
      border-radius: 0 0 0 8px;
      animation: progress 20s linear infinite;
    }

    @keyframes progress {
      from { width: 0%; }
      to { width: 100%; }
    }

    @media (max-width: 768px) {
      .art-panel { display: none; }
      .form-panel { width: 100%; min-height: 100vh; }
    }
  </style>
</head>
<body>

<!-- LEFT: Art Panel -->
<div class="art-panel">
  <div class="notes">
    <span class="note">♪</span>
    <span class="note">♫</span>
    <span class="note">♩</span>
    <span class="note">♬</span>
    <span class="note">♭</span>
  </div>

  <div class="vinyl">
    <svg viewBox="0 0 320 320">
      <defs>
        <radialGradient id="diskGrad" cx="50%" cy="50%" r="50%">
          <stop offset="0%" stop-color="#1a0a08"/>
          <stop offset="100%" stop-color="#0d0507"/>
        </radialGradient>
      </defs>
      <!-- Main disk -->
      <circle cx="160" cy="160" r="155" fill="url(#diskGrad)" stroke="#2a1210" stroke-width="1"/>
      <!-- Grooves -->
      <circle cx="160" cy="160" r="150" fill="none" stroke="rgba(255,255,255,0.03)" stroke-width="1"/>
      <circle cx="160" cy="160" r="140" fill="none" stroke="rgba(255,255,255,0.03)" stroke-width="1"/>
      <circle cx="160" cy="160" r="130" fill="none" stroke="rgba(255,255,255,0.03)" stroke-width="1"/>
      <circle cx="160" cy="160" r="120" fill="none" stroke="rgba(255,255,255,0.03)" stroke-width="1"/>
      <circle cx="160" cy="160" r="110" fill="none" stroke="rgba(255,255,255,0.03)" stroke-width="1"/>
      <circle cx="160" cy="160" r="100" fill="none" stroke="rgba(255,255,255,0.04)" stroke-width="1"/>
      <circle cx="160" cy="160" r="90" fill="none" stroke="rgba(255,255,255,0.04)" stroke-width="1"/>
      <circle cx="160" cy="160" r="80" fill="none" stroke="rgba(255,255,255,0.04)" stroke-width="1"/>
      <circle cx="160" cy="160" r="70" fill="none" stroke="rgba(255,255,255,0.04)" stroke-width="1"/>
      <!-- Accent ring -->
      <circle cx="160" cy="160" r="60" fill="none" stroke="rgba(232,67,45,0.2)" stroke-width="1.5"/>
      <!-- Label area -->
      <circle cx="160" cy="160" r="55" fill="#1a0e0a"/>
      <!-- Center hole -->
      <circle cx="160" cy="160" r="5" fill="#0a0708"/>
    </svg>
    <div class="vinyl-label">
      <div class="vinyl-inner">
        <span>V</span>
      </div>
    </div>
  </div>

  <div class="tagline">
    <h1>Music lives<br/>in the soul.</h1>
    <p>Premium listening experience</p>
  </div>
</div>

<!-- RIGHT: Form Panel -->
<div class="form-panel">
  <div class="logo">Velvet</div>
  <div class="logo-sub">Music for the discerning ear</div>

  <div class="form-title">Welcome back.</div>
  <div class="form-sub">Sign in to continue your journey.</div>

  <form class="form" onsubmit="handleLogin(event)">
    <div class="field">
      <label for="email">Email</label>
      <div class="input-wrap">
        <span class="input-icon">✉</span>
        <input type="email" id="email" placeholder="you@example.com" autocomplete="email"/>
      </div>
    </div>

    <div class="field">
      <label for="password">Password</label>
      <div class="input-wrap">
        <span class="input-icon">🔒</span>
        <input type="password" id="password" placeholder="••••••••" autocomplete="current-password"/>
        <button type="button" class="eye-toggle" onclick="togglePassword()" id="eyeBtn">👁</button>
      </div>
    </div>

    <div class="row">
      <label class="remember">
        <input type="checkbox"/> Keep me signed in
      </label>
      <a href="#" class="forgot">Forgot password?</a>
    </div>

    <button type="submit" class="btn-login" id="loginBtn">Sign In</button>

    <div class="or-row">
      <div class="or-line"></div>
      <span class="or-text">OR</span>
      <div class="or-line"></div>
    </div>

    <button type="button" class="btn-social" onclick="socialLogin('Google')">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
        <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
        <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
        <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
        <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
      </svg>
      Continue with Google
    </button>
  </form>

  <div class="signup-row">
    New to Velvet? <a href="#">Create a free account</a>
  </div>

  <!-- Now Playing bar -->
  <div class="now-playing">
    <div class="np-disc">♪</div>
    <div class="np-info">
      <div class="np-title">Clair de Lune</div>
      <div class="np-artist">Claude Debussy</div>
    </div>
    <div class="np-controls">
      <button class="np-btn">⏮</button>
      <button class="np-btn play">⏸</button>
      <button class="np-btn">⏭</button>
    </div>
    <div class="progress-bar"></div>
  </div>
</div>

<script>
  function togglePassword() {
    const input = document.getElementById('password');
    const btn = document.getElementById('eyeBtn');
    if (input.type === 'password') {
      input.type = 'text';
      btn.textContent = '🙈';
    } else {
      input.type = 'password';
      btn.textContent = '👁';
    }
  }

  function handleLogin(e) {
    e.preventDefault();
    const btn = document.getElementById('loginBtn');
    btn.textContent = 'Signing in…';
    btn.disabled = true;
    setTimeout(() => {
      btn.textContent = '✓ Welcome back';
      btn.style.background = '#2d7a3a';
      setTimeout(() => {
        btn.textContent = 'Sign In';
        btn.disabled = false;
        btn.style.background = '';
      }, 2000);
    }, 1400);
  }

  function socialLogin(provider) {
    alert(`Connecting with ${provider}…`);
  }
</script>

</body>
</html>
