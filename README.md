
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    
</body>
</html>
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>7 Profile Cards — 3D Animated</title>
  <style>
    :root{
      --bg:#0f1724;
      --card-bg: linear-gradient(135deg, rgba(255,255,255,0.04), rgba(255,255,255,0.02));
      --glass: rgba(255,255,255,0.03);
      --glass-2: rgba(255,255,255,0.02);
      --accent: 210 100% 60%; /* H S L via hsl(var(--accent)) */
      --radius: 18px;
      --gap: 1.1rem;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      background: radial-gradient(1200px 500px at 10% 10%, rgba(50,100,200,0.06), transparent),
                  radial-gradient(1000px 400px at 90% 90%, rgba(200,80,200,0.04), transparent),
                  var(--bg);
                  background: url("https://i.pinimg.com/736x/e7/bf/9d/e7bf9df13f6f5ebbf50363567115446f.jpg") no-repeat center center/cover;
      color:#e6eef8;
      -webkit-font-smoothing:antialiased;
      display:flex;align-items:center;justify-content:center;padding:40px;
    }

    .wrap{
      width:1200px;max-width:calc(100% - 48px);
    }

    h1{font-weight:700;margin:0 0 18px 0;font-size:20px;letter-spacing:0.2px;color:rgba(255,255,255,0.92)}
    p.lead{margin:0 0 20px 0;color:rgba(255,255,255,0.6);font-size:13px}

    .grid{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap:var(--gap);
      align-items:stretch;
    }
    @media (max-width:980px){.grid{grid-template-columns:repeat(2,1fr)}}
    @media (max-width:640px){.grid{grid-template-columns:1fr}}

    /* Card base */
    .card{
      --tiltX: 0deg; --tiltY: 0deg; --scale: 1; --h: 210; /* accent hue */
      perspective: 1200px;
      transform-style:preserve-3d;
      background:var(--card-bg);
      border-radius:var(--radius);
      padding:18px;
      position:relative;
      overflow:visible;
      transition:transform 400ms cubic-bezier(.2,.9,.3,1), box-shadow 240ms ease;
      box-shadow: 0 8px 30px rgba(2,6,23,0.6);
      transform: translateZ(0) rotateX(var(--tiltX)) rotateY(var(--tiltY)) scale(var(--scale));
      will-change: transform;
      min-height:220px;
    }

    /* neon border */
    .card::before{
      content:"";position:absolute;inset:0;border-radius:inherit;z-index:0;
      background: linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      pointer-events:none;
    }

    .card .inner{position:relative;z-index:2;display:flex;gap:14px;align-items:center}

    .avatar{
      width:96px;height:96px;border-radius:14px;flex:0 0 96px;overflow:hidden;position:relative;
      transform-style:preserve-3d;backface-visibility:hidden;box-shadow:0 6px 18px rgba(2,6,23,0.6);
      border:1px solid rgba(255,255,255,0.06);
    }
    .avatar img{width:100%;height:100%;object-fit:cover;display:block}

    .meta{flex:1}
    .name{font-size:16px;font-weight:700;margin:0 0 6px 0}
    .role{font-size:12px;margin:0 0 10px 0;color:rgba(255,255,255,0.65)}
    .bio{font-size:13px;margin:0;color:rgba(255,255,255,0.66);line-height:1.3}

    .actions{margin-top:12px;display:flex;gap:8px;align-items:center}
    .btn{
      display:inline-flex;align-items:center;gap:8px;padding:8px 12px;border-radius:10px;font-size:13px;font-weight:600;
      text-decoration:none;color:inherit;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border:1px solid rgba(255,255,255,0.04);backdrop-filter: blur(6px);
      transition:transform 180ms ease, box-shadow 180ms ease, background 120ms ease;
      box-shadow: 0 3px 10px rgba(2,6,23,0.45);
    }
    .btn:active{transform:translateY(1px)}
    .btn svg{width:16px;height:16px;display:block;opacity:0.95}

    /* colorful accent strip at bottom */
    .accent{
      position:absolute;left:12px;right:12px;bottom:12px;height:6px;border-radius:6px;z-index:1;filter:blur(8px) saturate(1.2);
      background:linear-gradient(90deg, hsl(var(--h) 100% 56%), hsl(calc(var(--h) + 40) 100% 56%));
      opacity:0.95;
      transform-origin:center;transform:translateZ(30px) scaleY(1);
    }

    /* shine + parallax layers */
    .card .shine{position:absolute;inset:0;border-radius:inherit;z-index:3;pointer-events:none;background:linear-gradient(120deg, rgba(255,255,255,0.06), rgba(255,255,255,0.0));mix-blend-mode:overlay;opacity:0;transition:opacity 220ms ease}

    .card:hover .shine{opacity:1}

    /* subtle floating animation to make cards lively */
    .floaty{animation:floaty 6s ease-in-out infinite}
    @keyframes floaty{0%{transform:translateY(0)}50%{transform:translateY(-6px)}100%{transform:translateY(0)}}

    /* small responsive tweaks */
    @media (max-width:420px){.avatar{width:84px;height:84px}}

    /* utility: different hues per card */
    .card[data-h="190"]{--h:190}
    .card[data-h="210"]{--h:210}
    .card[data-h="270"]{--h:270}
    .card[data-h="30"]{--h:30}
    .card[data-h="320"]{--h:320}
    .card[data-h="120"]{--h:120}
    .card[data-h="15"]{--h:15}

    /* small accessibility focus */
    .card:focus-within{outline:2px solid rgba(255,255,255,0.06);box-shadow:0 12px 40px rgba(0,0,0,0.6)}

  </style>
</head>
<body>
  <div class="wrap">
    <h1>7 Profile Cards — 3D Animated</h1>
    <p class="lead">WEBSITE DEV BY VIRUS /FDI TEAM / DRARI ZWININ TA3 VAGOS OU VPV ❤️.</p>

    <div class="grid" id="grid">
      <!-- Seven cards -->
      <article class="card floaty" data-h="210" tabindex="0">
        <div class="shine"></div>
        <div class="inner">
          <div class="avatar layer" data-depth="18">
            <img src="https://files.kick.com/images/user/16649165/profile_image/conversion/8c09c6e1-39d3-4401-a8fc-7c4ea9445613-fullsize.webp" alt="Avatar A"/>
          </div>
          <div class="meta">
            <div class="name">AguerroX9"</div>
            <div class="role">streamer</div>
            <div class="bio">AGUERROX9 DERI ZWIN MAKIDIRCH DSSARA DAYMAN KIGOL CHOF DAYMAN M3A 6 MOD SPORT OU KATLA9AH MCHA LBHAR KIB9A DERI ZWIN❤️.</div>
            <div class="actions">
              <a href="https://www.instagram.com/agueerrox9/" target="_blank" rel="noopener noreferrer" aria-label="Open Instagram profile (opens in new tab)" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Instagram SVG (simple) -->
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false" xmlns="https://www.instagram.com/agueerrox9/">
    <rect x="3" y="3" width="18" height="18" rx="5" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="12" cy="12" r="3.2" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/>
  </svg>

  <span>@agueerrox9</span>
</a>

</a>
              <a href="https://discord.gg/VJmeDUpP" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Discord SVG Icon -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
    <path d="M20 4a19.8 19.8 0 0 0-4.9-1.5l-.2.4c.8.2 1.5.5 2.2.9-.9-.3-1.8-.6-2.8-.8a16.9 16.9 0 0 0-7.6 0c-1 .2-1.9.5-2.8.8.7-.4 1.4-.7 2.2-.9l-.2-.4A19.8 19.8 0 0 0 4 4C1.8 7.3 1 10.6 1 14a11.6 11.6 0 0 0 8.2 4c-.2-.5-.4-1.1-.5-1.6a7.2 7.2 0 0 1-4.4-2.1 2.5 2.5 0 0 1 .3-.3 7.1 7.1 0 0 0 3.4 1.5c1.4.3 2.9.3 4.3 0a7.1 7.1 0 0 0 3.4-1.5 2.5 2.5 0 0 1 .3.3 7.2 7.2 0 0 1-4.4 2.1c-.1.5-.3 1.1-.5 1.6A11.6 11.6 0 0 0 23 14c0-3.4-.8-6.7-3-10z"/>
  </svg>
  <span>Join Discord</span>
</a>
<a href="https://kick.com/aguerrox9" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Kick Icon (SVG) -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="#52FF00" aria-hidden="true">
    <path d="M4 3h4v7l4-4h4l-4 4 4 4h-4l-4-4v7H4z"/>
  </svg>
  <span>Follow </span>
</a>

            </div>
          </div>
        </div>
        <div class="accent"></div>
      </article>

      <article class="card floaty" data-h="190" tabindex="0">
        <div class="shine"></div>
        <div class="inner">
          <div class="avatar layer" data-depth="20">
            <img src="https://files.kick.com/images/user/58580153/profile_image/conversion/0a1176f8-163d-4df1-a2ad-5f28512a241c-fullsize.webp" alt="Avatar B"/>
          </div>
          <div class="meta">
            <div class="name">TOKYOO</div>
            <div class="role">streamer</div>
            <div class="bio">TOKYO MOLA9AB B PETCHOO DRI DRIF TSSBO IRBRB 3LIK 9ASSIR L9AMA WALAKIN KIB9A DERI ZWIN❤️.</div>
            <div class="actions">
              <a href="https://www.instagram.com/soufiane__ro/" target="_blank" rel="noopener noreferrer" aria-label="Open Instagram profile (opens in new tab)" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Instagram SVG (simple) -->
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false" xmlns="http://www.w3.org/2000/svg">
    <rect x="3" y="3" width="18" height="18" rx="5" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="12" cy="12" r="3.2" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/>
  </svg>

  <span>@soufiane__ro</span>
</a>

              <a href="https://kick.com/tokyoo3" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Kick Icon (SVG) -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="#52FF00" aria-hidden="true">
    <path d="M4 3h4v7l4-4h4l-4 4 4 4h-4l-4-4v7H4z"/>
  </svg>
  <span>Follow</span>
</a>

            </div>
          </div>
        </div>
        <div class="accent"></div>
      </article>

      <article class="card floaty" data-h="270" tabindex="0">
        <div class="shine"></div>
        <div class="inner">
          <div class="avatar layer" data-depth="22">
            <img src="https://files.kick.com/images/user/7022051/profile_image/conversion/69528510-2978-49cc-9c3f-e8fc25076e42-fullsize.webp" alt="Avatar C"/>
          </div>
          <div class="meta">
            <div class="name">TACHTOUCH</div>
            <div class="role">streamer</div>
            <div class="bio">TACHTOUCH MSS SSKLA SSL3A KATBRI OU L7YA KMLHA MN 3NDK DERI ZWIN❤️.</div>
            <div class="actions">
              <a href="https://www.instagram.com/tachtouch007/" target="_blank" rel="noopener noreferrer" aria-label="Open Instagram profile (opens in new tab)" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Instagram SVG (simple) -->
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false" xmlns="http://www.w3.org/2000/svg">
    <rect x="3" y="3" width="18" height="18" rx="5" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="12" cy="12" r="3.2" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/>
  </svg>

  <span>@tachtouch007
</span>
</a>

              <a href="https://kick.com/tachtouch" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Kick Icon (SVG) -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="#52FF00" aria-hidden="true">
    <path d="M4 3h4v7l4-4h4l-4 4 4 4h-4l-4-4v7H4z"/>
  </svg>
  <span>Follow </span>
</a>

            </div>
          </div>
        </div>
        <div class="accent"></div>
      </article>

      <article class="card floaty" data-h="30" tabindex="0">
        <div class="shine"></div>
        <div class="inner">
          <div class="avatar layer" data-depth="16">
            <img src="https://files.kick.com/images/user/27669366/profile_image/conversion/1cb33187-c2ca-41d2-9062-28089dfcc1d9-fullsize.webp" alt="Avatar D"/>
          </div>
          <div class="meta">
            <div class="name">SMOOKS</div>
            <div class="role">streamer</div>
            <div class="bio">SMOOKS 9AHIR LMIMAT OU CHABAT OU PAPAP ACHKIDIR LMAKLA KIKHLT OU KIYAKL OU KIB9A DERI ZWIN❤️.</div>
            <div class="actions">
              <a href="https://www.instagram.com/smooks10/" target="_blank" rel="noopener noreferrer" aria-label="Open Instagram profile (opens in new tab)" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Instagram SVG (simple) -->
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false" xmlns="http://www.w3.org/2000/svg">
    <rect x="3" y="3" width="18" height="18" rx="5" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="12" cy="12" r="3.2" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/>
  </svg>

  <span>@smooks10</span>
</a>

              <a href="https://kick.com/smooks1" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Kick Icon (SVG) -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="#52FF00" aria-hidden="true">
    <path d="M4 3h4v7l4-4h4l-4 4 4 4h-4l-4-4v7H4z"/>
  </svg>
  <span>Follow </span>
</a>

            </div>
          </div>
        </div>
        <div class="accent"></div>
      </article>

      <article class="card floaty" data-h="320" tabindex="0">
        <div class="shine"></div>
        <div class="inner">
          <div class="avatar layer" data-depth="18">
            <img src="file:///C:/Users/slend/Pictures/ab10bc13c91ddeef1aad52e9a9582138.webp" alt="Avatar E"/>
          </div>
          <div class="meta">
            <div class="name">CONTRIX</div>
            <div class="role">streamer</div>
            <div class="bio">CONTIRX NFAA7 DYALLNA DERI ZWIN OU AY W9 KIT3AYER M3A 3CHIRNA NHWIW AMOO OU KIB9A CONTRIX DERI ZWIN❤️.</div>
            <div class="actions">
              <a href="https://www.instagram.com/houssam.bayhou/" target="_blank" rel="noopener noreferrer" aria-label="Open Instagram profile (opens in new tab)" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Instagram SVG (simple) -->
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false" xmlns="http://www.w3.org/2000/svg">
    <rect x="3" y="3" width="18" height="18" rx="5" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="12" cy="12" r="3.2" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/>
  </svg>

  <span>@houssam.bayhou</span>
</a>

              <a href="https://kick.com/contrix01" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Kick Icon (SVG) -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="#52FF00" aria-hidden="true">
    <path d="M4 3h4v7l4-4h4l-4 4 4 4h-4l-4-4v7H4z"/>
  </svg>
  <span>Follow </span>
</a>

            </div>
          </div>
        </div>
        <div class="accent"></div>
      </article>

      <article class="card floaty" data-h="120" tabindex="0">
        <div class="shine"></div>
        <div class="inner">
          <div class="avatar layer" data-depth="20">
            <img src="https://files.kick.com/images/user/29543640/profile_image/conversion/6fe7677a-8511-493d-95ca-db1a9adf57b3-fullsize.webp" alt="Avatar F"/>
          </div>
          <div class="meta">
            <div class="name">DANZO</div>
            <div class="role">streamer</div>
            <div class="bio">the danzo leo metii msfioui dyalna ou lah ikhli lina rann.. 9te3 mn 3ND DERI ZWIN❤️.</div>
            <div class="actions">
              <a href="https://www.instagram.com/unes_bd/" target="_blank" rel="noopener noreferrer" aria-label="Open Instagram profile (opens in new tab)" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Instagram SVG (simple) -->
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false" xmlns="http://www.w3.org/2000/svg">
    <rect x="3" y="3" width="18" height="18" rx="5" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="12" cy="12" r="3.2" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/>
  </svg>

  <span>@unes_bd</span>
</a>

              <a href="https://kick.com/danzo_1" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Kick Icon (SVG) -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="#52FF00" aria-hidden="true">
    <path d="M4 3h4v7l4-4h4l-4 4 4 4h-4l-4-4v7H4z"/>
  </svg>
  <span>Follow </span>
</a>

            </div>
          </div>
        </div>
        <div class="accent"></div>
      </article>

      <article class="card floaty" data-h="15" tabindex="0">
        <div class="shine"></div>
        <div class="inner">
          <div class="avatar layer" data-depth="18">
            <img src="https://files.kick.com/images/user/15299552/profile_image/conversion/c97a6ba1-7d3b-422a-8d63-83efdf050967-fullsize.webp" alt="Avatar G"/>
          </div>
          <div class="meta">
            <div class="name">SBAII</div>
            <div class="role">streamer</div>
            <div class="bio">sbaii mola9AB B chakchabani 3TIH LABANI NASS KITKHRAWA OU HOWA ki7WI f l gunsmith OU KIB9A DERI ZWIN❤️.</div>
            <div class="actions">
              <a href="https://www.instagram.com/amine__ake/" target="_blank" rel="noopener noreferrer" aria-label="Open Instagram profile (opens in new tab)" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Instagram SVG (simple) -->
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" focusable="false" xmlns="http://www.w3.org/2000/svg">
    <rect x="3" y="3" width="18" height="18" rx="5" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="12" cy="12" r="3.2" stroke="currentColor" stroke-width="1.4"/>
    <circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/>
  </svg>

  <span>@
amine__ake</span>
</a>

              <a href="https://kick.com/sbaii" target="_blank" rel="noopener noreferrer" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;color:inherit;">
  <!-- Kick Icon (SVG) -->
  <svg width="20" height="20" viewBox="0 0 24 24" fill="#52FF00" aria-hidden="true">
    <path d="M4 3h4v7l4-4h4l-4 4 4 4h-4l-4-4v7H4z"/>
  </svg>
  <span>Follow </span>
</a>

            </div>
          </div>
        </div>
        <div class="accent"></div>
      </article>

    </div>
  </div>

  <script>
    // 3D tilt effect with parallax. Works on mousemove and touch.
    (function(){
      const cards = document.querySelectorAll('.card');

      function onMove(e, card){
        const rect = card.getBoundingClientRect();
        const px = ( (e.clientX ?? (e.touches && e.touches[0].clientX)) - rect.left) / rect.width;
        const py = ( (e.clientY ?? (e.touches && e.touches[0].clientY)) - rect.top) / rect.height;
        const tiltX = (py - 0.5) * -14; // rotateX
        const tiltY = (px - 0.5) * 20;  // rotateY
        const scale = 1.02;
        card.style.setProperty('--tiltX', tiltX.toFixed(2) + 'deg');
        card.style.setProperty('--tiltY', tiltY.toFixed(2) + 'deg');
        card.style.setProperty('--scale', scale);

        // parallax on avatar
        const layers = card.querySelectorAll('.layer');
        layers.forEach(layer => {
          const depth = parseFloat(layer.dataset.depth || 12);
          const moveX = (px - 0.5) * depth;
          const moveY = (py - 0.5) * depth * -1;
          layer.style.transform = `translate3d(${moveX}px, ${moveY}px, 0)`;
        });

        // shine
        const shine = card.querySelector('.shine');
        if(shine){
          const angle = Math.atan2(py - 0.5, px - 0.5) * (180/Math.PI) + 90;
          shine.style.background = `linear-gradient(${angle}deg, rgba(255,255,255,0.09), rgba(255,255,255,0))`;
        }
      }

      function reset(card){
        card.style.setProperty('--tiltX','0deg');
        card.style.setProperty('--tiltY','0deg');
        card.style.setProperty('--scale','1');
        const layers = card.querySelectorAll('.layer');
        layers.forEach(layer => layer.style.transform = 'translate3d(0,0,0)');
      }

      cards.forEach(card => {
        let pointerDown = false;
        card.addEventListener('pointermove', (ev) => onMove(ev, card));
        card.addEventListener('pointerenter', ()=> card.classList.add('is-hover'));
        card.addEventListener('pointerleave', ()=> reset(card));

        // mobile tap toggle: on tap show slight pop
        card.addEventListener('click', ()=>{
          card.style.setProperty('--scale','1.03');
          setTimeout(()=> card.style.setProperty('--scale','1'), 220);
        });
      });

      // reduce motion respecting prefers-reduced-motion
      const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
      if(reduced){
        document.querySelectorAll('.floaty').forEach(n => n.style.animation = 'none');
      }
    })();
  </script>
</body>
</html>
