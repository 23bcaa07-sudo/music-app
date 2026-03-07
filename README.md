<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Resonance — Login</title>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --bg: #0a0a0c;
      --card: #111115;
      --border: rgba(255,255,255,0.06);
      --accent: #e8ff47;
      --accent2: #ff4f7b;
      --text: #f0ede8;
      --muted: rgba(240,237,232,0.4);
      --input-bg: rgba(255,255,255,0.04);
    }

    body {
      font-family: 'DM Sans', sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      position: relative;
    }

    /* Animated background blobs */
    .bg-blobs {
      position: fixed;
      inset: 0;
      z-index: 0;
      pointer-events: none;
    }

    .blob {
      position: absolute;
      border-radius: 50%;
      filter: blur(80px);
      opacity: 0.18;
      animation: drift 12s ease-in-out infinite alternate;
    }

    .blob-1 {
      width: 520px; height: 520px;
      background: radial-gradient(circle, #e8ff47, transparent 70%);
      top: -120px; left: -100px;
      animation-delay: 0s;
    }

    .blob-2 {
      width: 400px; height: 400px;
      background: radial-gradient(circle, #ff4f7b, transparent 70%);
      bottom: -80px; right: -80px;
      animation-delay: -4s;
    }

    .blob-3 {
      width: 300px; height: 300px;
      background: radial-gradient(circle, #7b5fff, transparent 70%);
      top: 40%; left: 60%;
      animation-delay: -8s;
    }

    @keyframes drift {
      from { transform: translate(0, 0) scale(1); }
      to   { transform: translate(30px, 20px) scale(1.08); }
    }

    /* Waveform decoration */
    .waveform {
      position: fixed;
      bottom: 0; left: 0; right: 0;
      height: 100px;
      display: flex;
      align-items: flex-end;
      gap: 3px;
      padding: 0 20px;
      opacity: 0.12;
      z-index: 0;
      pointer-events: none;
    }

    .wave-bar {
      flex: 1;
      background: var(--accent);
      border-radius: 2px 2px 0 0;
      animation: wave 1.4s ease-in-out infinite alternate;
      transform-origin: bottom;
    }

    @keyframes wave {
      from { transform: scaleY(var(--min)); }
      to   { transform: scaleY(var(--max)); }
    }

    /* Layout */
    .page {
      position: relative;
      z-index: 1;
      display: grid;
      grid-template-columns: 1fr 1fr;
      min-height: 100vh;
      width: 100%;
      max-width: 1100px;
      margin: 0 auto;
    }

    /* Left panel */
    .left-panel {
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 60px 50px;
      animation: fadeUp 0.8s cubic-bezier(0.22,1,0.36,1) both;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 60px;
    }

    .brand-icon {
      width: 40px; height: 40px;
      background: var(--accent);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .brand-icon svg { width: 22px; height: 22px; }

    .brand-name {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 26px;
      letter-spacing: 3px;
      color: var(--text);
    }

    .left-headline {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(52px, 6vw, 88px);
      line-height: 0.9;
      letter-spacing: 1px;
      margin-bottom: 24px;
    }

    .left-headline em {
      font-style: normal;
      color: var(--accent);
    }

    .left-sub {
      font-size: 15px;
      line-height: 1.6;
      color: var(--muted);
      max-width: 340px;
      margin-bottom: 40px;
      font-weight: 300;
    }

    .stats {
      display: flex;
      gap: 32px;
    }

    .stat-item {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    .stat-num {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 28px;
      color: var(--text);
      letter-spacing: 1px;
    }

    .stat-label {
      font-size: 11px;
      color: var(--muted);
      text-transform: uppercase;
      letter-spacing: 1.5px;
    }

    /* Divider between panels */
    .divider {
      width: 1px;
      background: var(--border);
      margin: 40px 0;
      align-self: stretch;
    }

    /* Right panel — form */
    .right-panel {
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 60px 50px;
      animation: fadeUp 0.8s cubic-bezier(0.22,1,0.36,1) 0.15s both;
    }

    .form-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 36px;
      letter-spacing: 2px;
      margin-bottom: 6px;
    }

    .form-subtitle {
      font-size: 14px;
      color: var(--muted);
      margin-bottom: 36px;
      font-weight: 300;
    }

    .form-subtitle a {
      color: var(--accent);
      text-decoration: none;
      font-weight: 500;
      border-bottom: 1px solid transparent;
      transition: border-color 0.2s;
    }

    .form-subtitle a:hover { border-color: var(--accent); }

    /* Social login */
    .social-buttons {
      display: flex;
      gap: 12px;
      margin-bottom: 28px;
    }

    .social-btn {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      padding: 12px;
      border-radius: 10px;
      border: 1px solid var(--border);
      background: var(--input-bg);
      color: var(--text);
      font-family: 'DM Sans', sans-serif;
      font-size: 13px;
      cursor: pointer;
      transition: all 0.2s;
      font-weight: 400;
    }

    .social-btn:hover {
      border-color: rgba(255,255,255,0.15);
      background: rgba(255,255,255,0.07);
      transform: translateY(-1px);
    }

    .social-btn svg { width: 18px; height: 18px; }

    .or-divider {
      display: flex;
      align-items: center;
      gap: 14px;
      margin-bottom: 24px;
    }

    .or-line {
      flex: 1;
      height: 1px;
      background: var(--border);
    }

    .or-text {
      font-size: 12px;
      color: var(--muted);
      letter-spacing: 1px;
      text-transform: uppercase;
    }

    /* Form fields */
    .field {
      margin-bottom: 16px;
    }

    label {
      display: block;
      font-size: 12px;
      font-weight: 500;
      letter-spacing: 1.2px;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 8px;
    }

    .input-wrap {
      position: relative;
    }

    input {
      width: 100%;
      padding: 14px 16px 14px 44px;
      background: var(--input-bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      color: var(--text);
      font-family: 'DM Sans', sans-serif;
      font-size: 14px;
      outline: none;
      transition: all 0.25s;
      font-weight: 300;
    }

    input::placeholder { color: rgba(240,237,232,0.2); }

    input:focus {
      border-color: var(--accent);
      background: rgba(232,255,71,0.04);
      box-shadow: 0 0 0 3px rgba(232,255,71,0.08);
    }

    .input-icon {
      position: absolute;
      left: 14px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--muted);
      pointer-events: none;
    }

    .input-icon svg { width: 17px; height: 17px; display: block; }

    .eye-toggle {
      position: absolute;
      right: 14px;
      top: 50%;
      transform: translateY(-50%);
      background: none;
      border: none;
      color: var(--muted);
      cursor: pointer;
      padding: 0;
      display: flex;
      align-items: center;
      transition: color 0.2s;
    }

    .eye-toggle:hover { color: var(--text); }
    .eye-toggle svg { width: 17px; height: 17px; }

    .form-options {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 24px;
    }

    .remember {
      display: flex;
      align-items: center;
      gap: 8px;
      cursor: pointer;
      font-size: 13px;
      color: var(--muted);
      user-select: none;
    }

    .remember input[type="checkbox"] {
      width: 16px; height: 16px;
      padding: 0;
      accent-color: var(--accent);
      cursor: pointer;
    }

    .forgot {
      font-size: 13px;
      color: var(--muted);
      text-decoration: none;
      transition: color 0.2s;
    }

    .forgot:hover { color: var(--accent); }

    /* Submit button */
    .btn-login {
      width: 100%;
      padding: 15px;
      background: var(--accent);
      color: #0a0a0c;
      border: none;
      border-radius: 10px;
      font-family: 'Bebas Neue', sans-serif;
      font-size: 18px;
      letter-spacing: 3px;
      cursor: pointer;
      position: relative;
      overflow: hidden;
      transition: all 0.25s;
      margin-bottom: 20px;
    }

    .btn-login::before {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, rgba(255,255,255,0.2), transparent);
      opacity: 0;
      transition: opacity 0.25s;
    }

    .btn-login:hover {
      transform: translateY(-2px);
      box-shadow: 0 10px 40px rgba(232,255,71,0.3);
    }

    .btn-login:hover::before { opacity: 1; }

    .btn-login:active { transform: translateY(0); }

    /* Ripple effect */
    .ripple {
      position: absolute;
      border-radius: 50%;
      background: rgba(0,0,0,0.2);
      transform: scale(0);
      animation: ripple-anim 0.5s linear;
      pointer-events: none;
    }

    @keyframes ripple-anim {
      to { transform: scale(4); opacity: 0; }
    }

    /* Now playing pill */
    .now-playing {
      display: flex;
      align-items: center;
      gap: 10px;
      background: rgba(255,255,255,0.04);
      border: 1px solid var(--border);
      border-radius: 40px;
      padding: 8px 14px;
      width: fit-content;
      margin-top: 12px;
      animation: fadeUp 0.8s cubic-bezier(0.22,1,0.36,1) 0.4s both;
    }

    .np-dot {
      width: 8px; height: 8px;
      background: var(--accent2);
      border-radius: 50%;
      animation: pulse 1.5s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; transform: scale(1); }
      50%       { opacity: 0.6; transform: scale(0.8); }
    }

    .np-text {
      font-size: 12px;
      color: var(--muted);
      font-weight: 300;
    }

    .np-text span {
      color: var(--text);
      font-weight: 500;
    }

    /* Mini equalizer bars */
    .eq-bars {
      display: flex;
      align-items: flex-end;
      gap: 2px;
      height: 14px;
    }

    .eq-bar {
      width: 3px;
      background: var(--accent2);
      border-radius: 1px;
      animation: eq 0.8s ease-in-out infinite alternate;
    }

    .eq-bar:nth-child(1) { height: 6px;  animation-delay: 0s;    }
    .eq-bar:nth-child(2) { height: 12px; animation-delay: 0.1s;  }
    .eq-bar:nth-child(3) { height: 8px;  animation-delay: 0.2s;  }
    .eq-bar:nth-child(4) { height: 14px; animation-delay: 0.05s; }

    @keyframes eq {
      from { transform: scaleY(0.3); }
      to   { transform: scaleY(1); }
    }

    /* Fade-up entry animation */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* Success state */
    .btn-login.success {
      background: #4ade80;
      pointer-events: none;
    }

    /* Responsive */
    @media (max-width: 768px) {
      .page { grid-template-columns: 1fr; }
      .left-panel { display: none; }
      .divider { display: none; }
      .right-panel { padding: 40px 28px; }
    }
  </style>
</head>
<body>

  <!-- Background -->
  <div class="bg-blobs">
    <div class="blob blob-1"></div>
    <div class="blob blob-2"></div>
    <div class="blob blob-3"></div>
  </div>

  <!-- Waveform -->
  <div class="waveform" id="waveform"></div>

  <div class="page">

    <!-- LEFT PANEL -->
    <div class="left-panel">
      <div class="brand">
        <div class="brand-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="#0a0a0c" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="4"/>
            <path d="M12 2v2M12 20v2M2 12h2M20 12h2"/>
            <circle cx="12" cy="12" r="10" stroke-opacity="0.3"/>
          </svg>
        </div>
        <span class="brand-name">Resonance</span>
      </div>

      <h1 class="left-headline">
        FEEL<br/>
        THE<br/>
        <em>BEAT.</em>
      </h1>

      <p class="left-sub">
        Millions of songs. Zero limits. Your soundtrack,
        perfectly tuned to every moment of your life.
      </p>

      <div class="stats">
        <div class="stat-item">
          <span class="stat-num">80M+</span>
          <span class="stat-label">Tracks</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">200+</span>
          <span class="stat-label">Countries</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">500K</span>
          <span class="stat-label">Artists</span>
        </div>
      </div>

      <div class="now-playing">
        <div class="np-dot"></div>
        <div class="eq-bars">
          <div class="eq-bar"></div>
          <div class="eq-bar"></div>
          <div class="eq-bar"></div>
          <div class="eq-bar"></div>
        </div>
        <span class="np-text"><span>Blinding Lights</span> · The Weeknd</span>
      </div>
    </div>

    <div class="divider"></div>

    <!-- RIGHT PANEL -->
    <div class="right-panel">
      <p class="form-title">Welcome Back</p>
      <p class="form-subtitle">
        New here? <a href="#">Create a free account</a>
      </p>

      <!-- Social -->
      <div class="social-buttons">
        <button class="social-btn">
          <!-- Google icon -->
          <svg viewBox="0 0 24 24" fill="none">
            <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
            <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
            <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l3.66-2.84z" fill="#FBBC05"/>
            <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
          </svg>
          Google
        </button>
        <button class="social-btn">
          <!-- Apple icon -->
          <svg viewBox="0 0 24 24" fill="currentColor">
            <path d="M17.05 20.28c-.98.95-2.05.8-3.08.35-1.09-.46-2.09-.48-3.24 0-1.44.62-2.2.44-3.06-.35C2.79 15.25 3.51 7.7 9.05 7.31c1.35.07 2.29.74 3.08.8 1.18-.24 2.31-.93 3.57-.84 1.51.12 2.65.72 3.4 1.8-3.12 1.87-2.38 5.98.48 7.13-.57 1.56-1.31 3.1-2.53 4.08zM12.03 7.25c-.15-2.23 1.66-4.07 3.74-4.25.29 2.58-2.34 4.5-3.74 4.25z"/>
          </svg>
          Apple
        </button>
        <button class="social-btn">
          <!-- Spotify icon -->
          <svg viewBox="0 0 24 24" fill="#1DB954">
            <path d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm4.586 14.424a.623.623 0 01-.857.207c-2.348-1.435-5.304-1.76-8.785-.964a.623.623 0 01-.277-1.215c3.809-.87 7.077-.496 9.712 1.115.294.18.387.563.207.857zm1.223-2.722a.78.78 0 01-1.072.257c-2.687-1.652-6.785-2.13-9.965-1.166a.78.78 0 01-.963-.519.781.781 0 01.52-.963c3.632-1.102 8.147-.568 11.223 1.329a.78.78 0 01.257 1.062zm.105-2.835C14.692 8.95 9.375 8.775 6.297 9.71a.937.937 0 11-.543-1.794c3.504-1.063 9.336-.857 13.019 1.357a.937.937 0 01-.86 1.664z"/>
          </svg>
          Spotify
        </button>
      </div>

      <div class="or-divider">
        <div class="or-line"></div>
        <span class="or-text">or</span>
        <div class="or-line"></div>
      </div>

      <!-- Form -->
      <div class="field">
        <label for="email">Email Address</label>
        <div class="input-wrap">
          <span class="input-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <rect x="2" y="4" width="20" height="16" rx="2"/>
              <path d="m2 7 10 7 10-7"/>
            </svg>
          </span>
          <input type="email" id="email" placeholder="you@example.com" autocomplete="email"/>
        </div>
      </div>

      <div class="field">
        <label for="password">Password</label>
        <div class="input-wrap">
          <span class="input-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <rect x="3" y="11" width="18" height="11" rx="2"/>
              <path d="M7 11V7a5 5 0 0 1 10 0v4"/>
            </svg>
          </span>
          <input type="password" id="password" placeholder="••••••••" autocomplete="current-password"/>
          <button class="eye-toggle" id="eyeToggle" type="button" aria-label="Toggle password">
            <svg id="eyeIcon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/>
              <circle cx="12" cy="12" r="3"/>
            </svg>
          </button>
        </div>
      </div>

      <div class="form-options">
        <label class="remember">
          <input type="checkbox" id="remember"/>
          Remember me
        </label>
        <a href="#" class="forgot">Forgot password?</a>
      </div>

      <button class="btn-login" id="loginBtn" type="button">
        Sign In
      </button>

      <p style="text-align:center; font-size:12px; color:var(--muted); font-weight:300;">
        By signing in, you agree to our
        <a href="#" style="color:var(--muted); text-decoration:underline;">Terms</a> &amp;
        <a href="#" style="color:var(--muted); text-decoration:underline;">Privacy Policy</a>
      </p>
    </div>

  </div>

  <script>
    // Generate waveform bars
    const waveform = document.getElementById('waveform');
    const numBars = Math.floor(window.innerWidth / 8);
    for (let i = 0; i < numBars; i++) {
      const bar = document.createElement('div');
      bar.className = 'wave-bar';
      const min = 0.1 + Math.random() * 0.3;
      const max = 0.4 + Math.random() * 0.9;
      bar.style.setProperty('--min', min);
      bar.style.setProperty('--max', max);
      bar.style.animationDelay = (Math.random() * 2) + 's';
      bar.style.animationDuration = (0.8 + Math.random() * 1.2) + 's';
      waveform.appendChild(bar);
    }

    // Password toggle
    const eyeToggle = document.getElementById('eyeToggle');
    const passwordInput = document.getElementById('password');
    let visible = false;
    eyeToggle.addEventListener('click', () => {
      visible = !visible;
      passwordInput.type = visible ? 'text' : 'password';
      eyeToggle.innerHTML = visible
        ? `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M17.94 17.94A10.07 10.07 0 0 1 12 20c-7 0-11-8-11-8a18.45 18.45 0 0 1 5.06-5.94M9.9 4.24A9.12 9.12 0 0 1 12 4c7 0 11 8 11 8a18.5 18.5 0 0 1-2.16 3.19m-6.72-1.07a3 3 0 1 1-4.24-4.24"/><line x1="1" y1="1" x2="23" y2="23"/></svg>`
        : `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/></svg>`;
    });

    // Ripple + login
    const loginBtn = document.getElementById('loginBtn');
    loginBtn.addEventListener('click', function(e) {
      // Ripple
      const rect = loginBtn.getBoundingClientRect();
      const size = Math.max(rect.width, rect.height);
      const ripple = document.createElement('span');
      ripple.className = 'ripple';
      ripple.style.cssText = `width:${size}px;height:${size}px;left:${e.clientX-rect.left-size/2}px;top:${e.clientY-rect.top-size/2}px`;
      loginBtn.appendChild(ripple);
      setTimeout(() => ripple.remove(), 600);

      // Validation
      const email = document.getElementById('email').value.trim();
      const password = document.getElementById('password').value;
      if (!email || !password) {
        loginBtn.style.background = '#ff4f7b';
        loginBtn.textContent = 'Fill All Fields';
        setTimeout(() => {
          loginBtn.style.background = 'var(--accent)';
          loginBtn.textContent = 'Sign In';
        }, 1800);
        return;
      }

      // Success
      loginBtn.classList.add('success');
      loginBtn.textContent = '✓ Welcome Back!';
    });

    // Social button hover sound-like feedback (visual)
    document.querySelectorAll('.social-btn').forEach(btn => {
      btn.addEventListener('mouseenter', () => {
        btn.style.transform = 'translateY(-2px)';
      });
      btn.addEventListener('mouseleave', () => {
        btn.style.transform = '';
      });
    });
  </script>
</body>
</html>
