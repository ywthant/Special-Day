
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Happy Birthday</title>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400;1,600&family=Poppins:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
html,body{font-family:'Poppins',sans-serif;background:linear-gradient(135deg,#1a0f14 0%,#2d1a22 50%,#1a0f14 100%);min-height:100vh;min-height:-webkit-fill-available;overflow-x:hidden;-webkit-tap-highlight-color:transparent;touch-action:manipulation}
.font-serif{font-family:'Playfair Display',serif}

/* Password Screen */
#password-screen{position:fixed;inset:0;z-index:200;background:linear-gradient(135deg,#1a0f14 0%,#2d1a22 100%);display:flex;flex-direction:column;align-items:center;justify-content:center;transition:opacity 1s ease,visibility 1s ease;-webkit-transition:opacity 1s ease,visibility 1s ease}
#password-screen.hidden{opacity:0;visibility:hidden;pointer-events:none}
.password-input{-webkit-appearance:none;appearance:none;background:rgba(255,255,255,0.05);border:2px solid rgba(183,110,121,0.3);border-radius:16px;padding:16px 24px;font-size:1.5rem;letter-spacing:0.3em;color:#f8e1e7;text-align:center;outline:none;transition:all 0.3s ease;-webkit-transition:all 0.3s ease;width:260px}
.password-input:focus{border-color:#d4a574;box-shadow:0 0 20px rgba(212,165,116,0.2);background:rgba(255,255,255,0.08)}
.password-input::placeholder{color:rgba(248,225,231,0.3);font-size:1rem;letter-spacing:0.1em}
.password-input.error{border-color:#e74c3c;-webkit-animation:shake 0.5s ease;animation:shake 0.5s ease}
@-webkit-keyframes shake{0%,100%{-webkit-transform:translateX(0)}20%{-webkit-transform:translateX(-10px)}40%{-webkit-transform:translateX(10px)}60%{-webkit-transform:translateX(-10px)}80%{-webkit-transform:translateX(10px)}}
@keyframes shake{0%,100%{transform:translateX(0)}20%{transform:translateX(-10px)}40%{transform:translateX(10px)}60%{transform:translateX(-10px)}80%{transform:translateX(10px)}}
.password-btn{-webkit-appearance:none;appearance:none;background:linear-gradient(135deg,#b76e79,#d4a574);border:none;border-radius:50px;padding:14px 40px;color:white;font-size:1rem;font-weight:500;cursor:pointer;transition:all 0.3s ease;-webkit-transition:all 0.3s ease;box-shadow:0 4px 20px rgba(183,110,121,0.3)}
.password-btn:active{transform:scale(0.97)}
.password-hint{opacity:0;transition:opacity 0.3s ease;-webkit-transition:opacity 0.3s ease}
.password-hint.show{opacity:1}

/* Intro Screen */
#intro-screen{position:fixed;inset:0;z-index:100;background:linear-gradient(135deg,#1a0f14 0%,#2d1a22 100%);display:flex;flex-direction:column;align-items:center;justify-content:center;transition:opacity 1.2s ease,visibility 1.2s ease;-webkit-transition:opacity 1.2s ease,visibility 1.2s ease;opacity:0;visibility:hidden}
#intro-screen.active{opacity:1;visibility:visible}
#intro-screen.hidden{opacity:0;visibility:hidden;pointer-events:none}
.intro-text{opacity:0}
.intro-text.animate{-webkit-animation:fadeInUp 1.5s ease forwards;animation:fadeInUp 1.5s ease forwards}
.intro-btn{opacity:0}
.intro-btn.animate{-webkit-animation:fadeInUp 1.5s ease forwards;animation:fadeInUp 1.5s ease forwards}
@-webkit-keyframes fadeInUp{from{opacity:0;-webkit-transform:translateY(30px)}to{opacity:1;-webkit-transform:translateY(0)}}
@keyframes fadeInUp{from{opacity:0;transform:translateY(30px)}to{opacity:1;transform:translateY(0)}}

/* Main Content */
#main-content{opacity:0;transition:opacity 1.5s ease;-webkit-transition:opacity 1.5s ease}
#main-content.visible{opacity:1}

/* Float */
@-webkit-keyframes float{0%,100%{-webkit-transform:translateY(0) rotate(-2deg)}50%{-webkit-transform:translateY(-20px) rotate(2deg)}}
@keyframes float{0%,100%{transform:translateY(0) rotate(-2deg)}50%{transform:translateY(-20px) rotate(2deg)}}
@-webkit-keyframes floatBalloon{0%,100%{-webkit-transform:translateY(0) translateX(0)}25%{-webkit-transform:translateY(-15px) translateX(5px)}50%{-webkit-transform:translateY(-25px) translateX(-5px)}75%{-webkit-transform:translateY(-10px) translateX(3px)}}
@keyframes floatBalloon{0%,100%{transform:translateY(0) translateX(0)}25%{transform:translateY(-15px) translateX(5px)}50%{transform:translateY(-25px) translateX(-5px)}75%{transform:translateY(-10px) translateX(3px)}}
.floating{-webkit-animation:float 4s ease-in-out infinite;animation:float 4s ease-in-out infinite}
.floating-balloon{-webkit-animation:floatBalloon 5s ease-in-out infinite;animation:floatBalloon 5s ease-in-out infinite}

/* ===== CANDLE FLAMES - iOS SAFE ===== */
.cake-wrapper{position:relative;display:inline-block;width:288px}
@media(min-width:768px){.cake-wrapper{width:384px}}
.cake-wrapper svg{display:block;width:100%;height:auto}

.candle-flame{
position:absolute;
width:20px;
height:32px;
pointer-events:auto;
cursor:pointer;
z-index:10;
left:40%;
bottom:90.625%;
-webkit-transform:translateX(-50%);
transform:translateX(-50%);
will-change:transform;
}

.candle-flame.c2{left:50%}
.candle-flame.c3{left:60%}

.flame-outer{
position:absolute;
bottom:0;
left:50%;
-webkit-transform:translateX(-50%);
transform:translateX(-50%);
width:16px;
height:26px;
background:linear-gradient(to top,#ff6b35 0%,#ff9a56 40%,#ffdb4d 100%);
border-radius:50% 50% 50% 50% / 60% 60% 40% 40%;
-webkit-filter:blur(0.3px);
filter:blur(0.3px);
-webkit-animation:flameWiggle 0.14s ease-in-out infinite;
animation:flameWiggle 0.14s ease-in-out infinite;
}

.flame-inner{
position:absolute;
bottom:2px;
left:50%;
-webkit-transform:translateX(-50%);
transform:translateX(-50%);
width:9px;
height:16px;
background:linear-gradient(to top,#ffdb4d 0%,#fff5a0 100%);
border-radius:50% 50% 50% 50% / 60% 60% 40% 40%;
-webkit-animation:flameWiggleInner 0.16s ease-in-out infinite;
animation:flameWiggleInner 0.16s ease-in-out infinite;
}

.flame-core{
position:absolute;
bottom:5px;
left:50%;
-webkit-transform:translateX(-50%);
transform:translateX(-50%);
width:4px;
height:8px;
background:#fff;
border-radius:50% 50% 50% 50% / 60% 60% 40% 40%;
-webkit-animation:flameWiggleCore 0.18s ease-in-out infinite;
animation:flameWiggleCore 0.18s ease-in-out infinite;
}

@-webkit-keyframes flameWiggle{
0%,100%{-webkit-transform:translateX(-50%) scale(1) rotate(-1deg)}
25%{-webkit-transform:translateX(-50%) scale(1.08) rotate(1deg)}
50%{-webkit-transform:translateX(-50%) scale(0.95) rotate(-0.5deg)}
75%{-webkit-transform:translateX(-50%) scale(1.05) rotate(0.5deg)}
}
@keyframes flameWiggle{
0%,100%{transform:translateX(-50%) scale(1) rotate(-1deg)}
25%{transform:translateX(-50%) scale(1.08) rotate(1deg)}
50%{transform:translateX(-50%) scale(0.95) rotate(-0.5deg)}
75%{transform:translateX(-50%) scale(1.05) rotate(0.5deg)}
}

@-webkit-keyframes flameWiggleInner{
0%,100%{-webkit-transform:translateX(-50%) scale(1)}
33%{-webkit-transform:translateX(-50%) scale(1.1) rotate(1deg)}
66%{-webkit-transform:translateX(-50%) scale(0.95) rotate(-1deg)}
}
@keyframes flameWiggleInner{
0%,100%{transform:translateX(-50%) scale(1)}
33%{transform:translateX(-50%) scale(1.1) rotate(1deg)}
66%{transform:translateX(-50%) scale(0.95) rotate(-1deg)}
}

@-webkit-keyframes flameWiggleCore{
0%,100%{-webkit-transform:translateX(-50%) scale(1)}
50%{-webkit-transform:translateX(-50%) scale(1.15)}
}
@keyframes flameWiggleCore{
0%,100%{transform:translateX(-50%) scale(1)}
50%{transform:translateX(-50%) scale(1.15)}
}

.candle-flame.blowout .flame-outer,
.candle-flame.blowout .flame-inner,
.candle-flame.blowout .flame-core{
-webkit-animation:none;
animation:none;
opacity:0;
-webkit-transition:opacity 0.4s ease;
transition:opacity 0.4s ease;
}

/* Smoke */
@-webkit-keyframes smokeRise{0%{opacity:0.6;-webkit-transform:translateY(0) scale(1)}100%{opacity:0;-webkit-transform:translateY(-40px) scale(2)}}
@keyframes smokeRise{0%{opacity:0.6;transform:translateY(0) scale(1)}100%{opacity:0;transform:translateY(-40px) scale(2)}}
.smoke-particle{position:absolute;width:8px;height:8px;background:rgba(200,200,200,0.4);border-radius:50%;-webkit-animation:smokeRise 1.5s ease-out forwards;animation:smokeRise 1.5s ease-out forwards}

/* Balloon Pop */
@-webkit-keyframes popBurst{0%{-webkit-transform:scale(1);opacity:1}50%{-webkit-transform:scale(1.3);opacity:0.8}100%{-webkit-transform:scale(0);opacity:0}}
@keyframes popBurst{0%{transform:scale(1);opacity:1}50%{transform:scale(1.3);opacity:0.8}100%{transform:scale(0);opacity:0}}
.balloon-popped{-webkit-animation:popBurst 0.3s ease-out forwards;animation:popBurst 0.3s ease-out forwards}

/* Envelope */
.envelope-container{-webkit-perspective:1000px;perspective:1000px}
.envelope{position:relative;width:280px;height:180px;background:linear-gradient(135deg,#f8e1e7 0%,#f0c8d3 100%);border-radius:4px;cursor:pointer;-webkit-transition:-webkit-transform 0.4s ease;transition:transform 0.4s ease;box-shadow:0 10px 40px rgba(183,110,121,0.3)}
.envelope:hover{-webkit-transform:translateY(-5px) scale(1.02);transform:translateY(-5px) scale(1.02)}
.envelope-flap{position:absolute;top:0;left:0;width:100%;height:50%;background:linear-gradient(135deg,#f0c8d3 0%,#e8b0c0 100%);-webkit-clip-path:polygon(0 0,50% 100%,100% 0);clip-path:polygon(0 0,50% 100%,100% 0);-webkit-transform-origin:top;transform-origin:top;-webkit-transition:-webkit-transform 0.6s ease;transition:transform 0.6s ease;z-index:2}
.envelope.open .envelope-flap{-webkit-transform:rotateX(180deg);transform:rotateX(180deg);z-index:0}
.envelope-body{position:absolute;bottom:0;left:0;width:100%;height:100%;background:linear-gradient(135deg,#f8e1e7 0%,#f0c8d3 100%);-webkit-clip-path:polygon(0 50%,50% 100%,100% 50%,100% 100%,0 100%);clip-path:polygon(0 50%,50% 100%,100% 50%,100% 100%,0 100%);z-index:1}
.envelope-seal{position:absolute;top:35%;left:50%;-webkit-transform:translate(-50%,-50%);transform:translate(-50%,-50%);width:40px;height:40px;background:linear-gradient(135deg,#d4a574,#c9956b);border-radius:50%;z-index:3;display:flex;align-items:center;justify-content:center;box-shadow:0 2px 10px rgba(0,0,0,0.1);-webkit-transition:opacity 0.3s ease;transition:opacity 0.3s ease}
.envelope.open .envelope-seal{opacity:0}
.letter{position:absolute;top:50%;left:50%;-webkit-transform:translate(-50%,-50%);transform:translate(-50%,-50%);width:260px;height:160px;background:#fff9fb;border-radius:4px;z-index:0;-webkit-transition:all 0.8s ease 0.3s;transition:all 0.8s ease 0.3s;padding:20px;box-shadow:0 5px 20px rgba(0,0,0,0.1);overflow:hidden}
.envelope.open .letter{-webkit-transform:translate(-50%,-140%);transform:translate(-50%,-140%);z-index:4;height:auto;min-height:300px;width:300px}

/* Present */
.present-container{-webkit-perspective:800px;perspective:800px;display:inline-block}
.present-box{position:relative;width:160px;height:140px;cursor:pointer;-webkit-transition:-webkit-transform 0.3s ease;transition:transform 0.3s ease}
.present-box:hover{-webkit-transform:scale(1.05);transform:scale(1.05)}
.present-box.opened{cursor:default}
.present-box.opened:hover{-webkit-transform:none;transform:none}
.present-lid{position:absolute;top:0;left:-10px;width:180px;height:35px;background:linear-gradient(135deg,#c97a8a,#b76e79);border-radius:4px 4px 2px 2px;z-index:3;-webkit-transition:-webkit-transform 0.6s cubic-bezier(0.34,1.56,0.64,1);transition:transform 0.6s cubic-bezier(0.34,1.56,0.64,1);-webkit-transform-origin:bottom left;transform-origin:bottom left;box-shadow:0 4px 15px rgba(0,0,0,0.2)}
.present-box.opened .present-lid{-webkit-transform:rotate(-110deg) translateY(-10px);transform:rotate(-110deg) translateY(-10px)}
.present-body{position:absolute;bottom:0;left:0;width:160px;height:110px;background:linear-gradient(135deg,#d4849c,#b76e79);border-radius:2px 2px 6px 6px;z-index:2;box-shadow:0 8px 30px rgba(0,0,0,0.25)}
.present-ribbon-v{position:absolute;left:50%;-webkit-transform:translateX(-50%);transform:translateX(-50%);width:24px;height:100%;background:linear-gradient(180deg,#d4a574,#c9956b);z-index:3}
.present-ribbon-h{position:absolute;top:50%;-webkit-transform:translateY(-50%);transform:translateY(-50%);width:100%;height:24px;background:linear-gradient(90deg,#d4a574,#c9956b);z-index:3}
.present-bow{position:absolute;top:-15px;left:50%;-webkit-transform:translateX(-50%);transform:translateX(-50%);z-index:4;-webkit-transition:all 0.4s ease;transition:all 0.4s ease}
.present-box.opened .present-bow{opacity:0;-webkit-transform:translateX(-50%) translateY(-20px) scale(0.5);transform:translateX(-50%) translateY(-20px) scale(0.5)}
.present-surprise{position:absolute;bottom:30px;left:50%;-webkit-transform:translateX(-50%) scale(0);transform:translateX(-50%) scale(0);opacity:0;z-index:1;text-align:center;-webkit-transition:all 0.7s cubic-bezier(0.34,1.56,0.64,1) 0.3s;transition:all 0.7s cubic-bezier(0.34,1.56,0.64,1) 0.3s;width:220px;pointer-events:none}
.present-box.opened .present-surprise{-webkit-transform:translateX(-50%) scale(1) translateY(-90px);transform:translateX(-50%) scale(1) translateY(-90px);opacity:1;z-index:10}
.present-glow{position:absolute;inset:-20px;border-radius:50%;background:radial-gradient(circle,rgba(212,165,116,0.3) 0%,transparent 70%);opacity:0;-webkit-transition:opacity 0.5s ease;transition:opacity 0.5s ease;pointer-events:none}
.present-box:hover .present-glow{opacity:1}

/* Modal */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.7);-webkit-backdrop-filter:blur(8px);backdrop-filter:blur(8px);z-index:50;display:flex;align-items:center;justify-content:center;opacity:0;visibility:hidden;-webkit-transition:all 0.4s ease;transition:all 0.4s ease}
.modal-overlay.active{opacity:1;visibility:visible}
.modal-content{background:linear-gradient(135deg,#fff9fb 0%,#f8e1e7 100%);border-radius:20px;padding:40px;max-width:500px;width:90%;max-height:80vh;overflow-y:auto;-webkit-transform:scale(0.8) translateY(20px);transform:scale(0.8) translateY(20px);-webkit-transition:all 0.5s ease;transition:all 0.5s ease;box-shadow:0 25px 80px rgba(0,0,0,0.3);border:1px solid rgba(212,165,116,0.3)}
.modal-overlay.active .modal-content{-webkit-transform:scale(1) translateY(0);transform:scale(1) translateY(0)}

/* Polaroid */
.polaroid{background:#fff9fb;padding:12px 12px 40px 12px;border-radius:4px;box-shadow:0 10px 40px rgba(0,0,0,0.2);-webkit-transform:rotate(-3deg);transform:rotate(-3deg);-webkit-transition:-webkit-transform 0.4s ease;transition:transform 0.4s ease}
.polaroid:hover{-webkit-transform:rotate(0deg) scale(1.02);transform:rotate(0deg) scale(1.02)}

/* Sparkles */
.sparkle{position:absolute;width:4px;height:4px;background:rgba(212,165,116,0.6);border-radius:50%;-webkit-animation:sparkle 3s ease-in-out infinite;animation:sparkle 3s ease-in-out infinite}
@-webkit-keyframes sparkle{0%,100%{opacity:0;-webkit-transform:scale(0)}50%{opacity:1;-webkit-transform:scale(1)}}
@keyframes sparkle{0%,100%{opacity:0;transform:scale(0)}50%{opacity:1;transform:scale(1)}}

/* Responsive */
@media(max-width:768px){.envelope{width:220px;height:140px}.letter{width:200px;height:120px}.envelope.open .letter{width:260px;min-height:250px}.password-input{width:220px;font-size:1.2rem}.present-surprise{width:180px}.present-box.opened .present-surprise{-webkit-transform:translateX(-50%) scale(1) translateY(-80px);transform:translateX(-50%) scale(1) translateY(-80px)}}

/* Scrollbar */
::-webkit-scrollbar{width:8px}
::-webkit-scrollbar-track{background:#1a0f14}
::-webkit-scrollbar-thumb{background:#b76e79;border-radius:4px}

/* Glow */
.glow-text{text-shadow:0 0 30px rgba(212,165,116,0.4),0 0 60px rgba(183,110,121,0.2)}

/* Heartbeat */
@-webkit-keyframes heartbeat{0%,100%{-webkit-transform:scale(1)}14%{-webkit-transform:scale(1.1)}28%{-webkit-transform:scale(1)}42%{-webkit-transform:scale(1.1)}70%{-webkit-transform:scale(1)}}
@keyframes heartbeat{0%,100%{transform:scale(1)}14%{transform:scale(1.1)}28%{transform:scale(1)}42%{transform:scale(1.1)}70%{transform:scale(1)}}
.heartbeat{-webkit-animation:heartbeat 1.5s ease-in-out infinite;animation:heartbeat 1.5s ease-in-out infinite}

/* Present float */
@-webkit-keyframes presentFloat{0%,100%{-webkit-transform:translateY(0)}50%{-webkit-transform:translateY(-8px)}}
@keyframes presentFloat{0%,100%{transform:translateY(0)}50%{transform:translateY(-8px)}}
.present-float{-webkit-animation:presentFloat 3s ease-in-out infinite;animation:presentFloat 3s ease-in-out infinite}
</style>
<base target="_blank">
</head>
<body class="text-white">

<div id="sparkles" class="fixed inset-0 pointer-events-none z-0"></div>

<!-- Password Screen -->
<div id="password-screen">
<div class="text-center px-6">
<div class="mb-8">
<svg width="64" height="64" viewBox="0 0 24 24" fill="none" stroke="#d4a574" stroke-width="1.5" class="mx-auto mb-4 opacity-80">
<rect x="3" y="11" width="18" height="11" rx="2" ry="2"/>
<path d="M7 11V7a5 5 0 0 1 10 0v4"/>
</svg>
</div>
<h1 class="font-serif text-3xl md:text-4xl mb-3 glow-text" style="color:#f8e1e7">A Secret Awaits</h1>
<p class="text-gray-400 text-sm mb-10 max-w-sm mx-auto font-light">Enter the special code to unlock your birthday surprise...</p>
<div class="space-y-5">
<input type="password" id="password-input" class="password-input" placeholder="Enter code" maxlength="7" inputmode="numeric" autocomplete="off" pattern="[0-9]*">
<div><button id="unlock-btn" class="password-btn">Unlock</button></div>
<p id="password-error" class="password-hint text-red-400 text-sm mt-3">Hmm, that is not quite right. Try again!</p>
<p class="text-gray-500 text-xs mt-6 font-light">Hint: The day the universe chose you  🎂</p>
</div>
</div>
</div>

<!-- Intro Screen -->
<div id="intro-screen">
<div class="text-center px-6">
<p class="intro-text text-lg md:text-xl font-light tracking-widest mb-4" style="color:#e8b0c0">TODAY IS SPECIAL</p>
<h1 class="intro-text font-serif text-4xl md:text-6xl lg:text-7xl font-bold mb-8 glow-text" style="color:#f8e1e7">Happy Birthday</h1>
<p class="intro-text text-base md:text-lg text-gray-300 max-w-md mx-auto mb-12 font-light">To someone who makes every day feel like a celebration.<br>This one is just for you.</p>
<button id="begin-btn" class="intro-btn group relative px-10 py-4 bg-gradient-to-r from-rose-400 to-amber-400 rounded-full text-white font-medium text-lg shadow-lg hover:shadow-2xl transition-all duration-300 hover:scale-105 overflow-hidden">
<span class="relative z-10">Click to Begin the Celebration</span>
<div class="absolute inset-0 bg-gradient-to-r from-amber-400 to-rose-400 opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
</button>
</div>
</div>

<!-- Main Content -->
<div id="main-content" class="relative z-10 min-h-screen">

<header class="text-center pt-12 pb-8 px-4">
<p class="tracking-[0.3em] text-sm uppercase mb-3" style="color:#e8b0c0">A Day to Remember</p>
<h1 class="font-serif text-5xl md:text-7xl font-bold glow-text mb-4" style="color:#f8e1e7">Happy Birthday</h1>
<div class="w-24 h-0.5 mx-auto rounded-full" style="background:linear-gradient(90deg,transparent,#d4a574,transparent)"></div>
</header>

<main class="max-w-6xl mx-auto px-4 pb-20 space-y-16">

<!-- Present Section -->
<section class="text-center py-4">
<h2 class="font-serif text-2xl md:text-3xl mb-4" style="color:#d4a574">A Special Gift For You</h2>
<p class="text-gray-300 text-sm mb-10 max-w-md mx-auto">Click the present to unwrap your surprise!</p>
<div class="present-container present-float">
<div id="present-box" class="present-box mx-auto">
<div class="present-glow"></div>
<div class="present-bow">
<svg width="50" height="35" viewBox="0 0 50 35">
<path d="M25 18 Q15 5 5 12 Q0 18 10 22 Q20 25 25 18" fill="#d4a574" stroke="#c9956b" stroke-width="1"/>
<path d="M25 18 Q35 5 45 12 Q50 18 40 22 Q30 25 25 18" fill="#d4a574" stroke="#c9956b" stroke-width="1"/>
<circle cx="25" cy="18" r="5" fill="#c9956b"/>
</svg>
</div>
<div class="present-lid">
<div class="present-ribbon-v" style="height:35px"></div>
<div class="present-ribbon-h" style="top:50%;height:24px"></div>
</div>
<div class="present-body">
<div class="present-ribbon-v"></div>
<div class="present-ribbon-h"></div>
</div>
<div class="present-surprise">
<div class="bg-white/95 rounded-xl p-5 shadow-2xl border border-rose-200">
<div class="text-4xl mb-2">💖</div>
<p class="font-serif text-sm font-semibold" style="color:#b76e79">You are the greatest gift of all.</p>
<p class="text-xs text-gray-500 mt-1">Happy Birthday, your existence, my favorite reason to celebrate..</p>
</div>
</div>
</div>
</div>
<p id="present-message" class="mt-8 text-sm opacity-0 transition-opacity duration-700" style="color:#f8c8d8">🎁 The best things in life are not things — they are people like you. 🎁</p>
</section>

<!-- Cake Section -->
<section class="text-center">
<h2 class="font-serif text-2xl md:text-3xl mb-8" style="color:#d4a574">Make a Wish</h2>
<p class="text-gray-300 text-sm mb-8 max-w-md mx-auto">Click on each candle to blow it out. Make your wish before the last flame fades!</p>

<div class="relative inline-block floating">
<div class="cake-wrapper">
<svg viewBox="0 0 400 320" class="w-full h-auto">
<ellipse cx="200" cy="300" rx="160" ry="25" fill="#3a252d" opacity="0.5"/>
<rect x="80" y="200" width="240" height="80" rx="8" fill="#5c3a4a"/>
<rect x="80" y="200" width="240" height="15" rx="4" fill="#7a5263"/>
<rect x="85" y="220" width="230" height="50" rx="4" fill="#6b4556"/>
<rect x="110" y="130" width="180" height="70" rx="6" fill="#7a5263"/>
<rect x="110" y="130" width="180" height="12" rx="3" fill="#9a7080"/>
<rect x="115" y="148" width="170" height="44" rx="3" fill="#8b6072"/>
<rect x="140" y="70" width="120" height="60" rx="5" fill="#9a7080"/>
<rect x="140" y="70" width="120" height="10" rx="2" fill="#b8909e"/>
<rect x="145" y="85" width="110" height="38" rx="2" fill="#a88090"/>
<path d="M80 200 Q95 215 110 200 Q125 218 140 200 Q155 212 170 200 Q185 216 200 200 Q215 214 230 200 Q245 210 260 200 Q275 216 290 200 Q305 212 320 200 L320 195 L80 195 Z" fill="#f8e1e7" opacity="0.9"/>
<path d="M110 130 Q120 142 130 130 Q140 144 150 130 Q160 140 170 130 Q180 145 190 130 Q200 142 210 130 Q220 140 230 130 Q240 144 250 130 Q260 142 270 130 Q280 140 290 130 L290 126 L110 126 Z" fill="#f0c8d3" opacity="0.9"/>
<path d="M140 70 Q150 80 160 70 Q170 82 180 70 Q190 78 200 70 Q210 80 220 70 Q230 82 240 70 Q250 78 260 70 L260 67 L140 67 Z" fill="#e8b0c0" opacity="0.9"/>
<circle cx="95" cy="230" r="4" fill="#d4a574" opacity="0.8"/>
<circle cx="125" cy="230" r="4" fill="#d4a574" opacity="0.8"/>
<circle cx="155" cy="230" r="4" fill="#d4a574" opacity="0.8"/>
<circle cx="185" cy="230" r="4" fill="#d4a574" opacity="0.8"/>
<circle cx="215" cy="230" r="4" fill="#d4a574" opacity="0.8"/>
<circle cx="245" cy="230" r="4" fill="#d4a574" opacity="0.8"/>
<circle cx="275" cy="230" r="4" fill="#d4a574" opacity="0.8"/>
<circle cx="305" cy="230" r="4" fill="#d4a574" opacity="0.8"/>

<!-- Candles (no flames in SVG) -->
<g transform="translate(160,70)">
<rect x="-4" y="-35" width="8" height="35" rx="2" fill="#f8e1e7"/>
<rect x="-4" y="-35" width="8" height="35" rx="2" fill="url(#cG1)" opacity="0.3"/>
<line x1="0" y1="-35" x2="0" y2="-40" stroke="#333" stroke-width="1.5"/>
</g>
<g transform="translate(200,70)">
<rect x="-4" y="-35" width="8" height="35" rx="2" fill="#f0c8d3"/>
<rect x="-4" y="-35" width="8" height="35" rx="2" fill="url(#cG2)" opacity="0.3"/>
<line x1="0" y1="-35" x2="0" y2="-40" stroke="#333" stroke-width="1.5"/>
</g>
<g transform="translate(240,70)">
<rect x="-4" y="-35" width="8" height="35" rx="2" fill="#e8b0c0"/>
<rect x="-4" y="-35" width="8" height="35" rx="2" fill="url(#cG3)" opacity="0.3"/>
<line x1="0" y1="-35" x2="0" y2="-40" stroke="#333" stroke-width="1.5"/>
</g>

<defs>
<linearGradient id="cG1" x1="0%" y1="0%" x2="100%" y2="0%"><stop offset="0%" style="stop-color:#b76e79;stop-opacity:1"/><stop offset="100%" style="stop-color:#f8e1e7;stop-opacity:1"/></linearGradient>
<linearGradient id="cG2" x1="0%" y1="0%" x2="100%" y2="0%"><stop offset="0%" style="stop-color:#b76e79;stop-opacity:1"/><stop offset="100%" style="stop-color:#f0c8d3;stop-opacity:1"/></linearGradient>
<linearGradient id="cG3" x1="0%" y1="0%" x2="100%" y2="0%"><stop offset="0%" style="stop-color:#b76e79;stop-opacity:1"/><stop offset="100%" style="stop-color:#e8b0c0;stop-opacity:1"/></linearGradient>
</defs>
</svg>

<!-- HTML FLAMES -->
<div class="candle-flame" data-candle="1">
<div class="flame-outer"></div>
<div class="flame-inner"></div>
<div class="flame-core"></div>
</div>
<div class="candle-flame c2" data-candle="2">
<div class="flame-outer"></div>
<div class="flame-inner"></div>
<div class="flame-core"></div>
</div>
<div class="candle-flame c3" data-candle="3">
<div class="flame-outer"></div>
<div class="flame-inner"></div>
<div class="flame-core"></div>
</div>
</div>

<p id="wish-text" class="mt-6 text-sm font-light opacity-0 transition-opacity duration-500" style="color:#e8b0c0">✨ Your wish has been made ✨</p>
</div>
</section>

<!-- Balloon Section -->
<section class="relative h-64 md:h-80 flex items-center justify-center overflow-hidden rounded-2xl" style="background:rgba(45,26,34,0.5)">
<div class="absolute inset-0 opacity-20" style="background:radial-gradient(circle at 30% 50%,#b76e79 0%,transparent 50%)"></div>
<div class="text-center z-10">
<p class="text-gray-300 text-sm mb-4">Pop the balloon for a surprise!</p>
<div id="balloon" class="floating-balloon cursor-pointer inline-block relative">
<svg viewBox="0 0 120 160" class="w-24 md:w-32 drop-shadow-lg">
<path d="M60 130 Q55 145 60 160" stroke="#d4a574" stroke-width="1.5" fill="none"/>
<ellipse cx="60" cy="65" rx="45" ry="55" fill="url(#bG)"/>
<ellipse cx="45" cy="45" rx="12" ry="18" fill="white" opacity="0.25"/>
<ellipse cx="42" cy="42" rx="5" ry="8" fill="white" opacity="0.4"/>
<polygon points="55,118 60,130 65,118" fill="#b76e79"/>
<defs>
<radialGradient id="bG" cx="30%" cy="30%" r="70%"><stop offset="0%" style="stop-color:#f8c8d8;stop-opacity:1"/><stop offset="50%" style="stop-color:#d4849c;stop-opacity:1"/><stop offset="100%" style="stop-color:#a85a72;stop-opacity:1"/></radialGradient>
</defs>
</svg>
</div>
<p id="balloon-message" class="mt-4 text-sm opacity-0 transition-opacity duration-500" style="color:#f8c8d8">🎉 Surprise! May your year be filled with joy! 🎉</p>
</div>
</section>

<!-- Envelope Section -->
<section class="text-center py-8">
<h2 class="font-serif text-2xl md:text-3xl mb-4" style="color:#d4a574">A Letter For You</h2>
<p class="text-gray-300 text-sm mb-10 max-w-md mx-auto">Click the envelope to open your special birthday message</p>
<div class="envelope-container inline-block">
<div id="envelope" class="envelope">
<div class="envelope-flap"></div>
<div class="envelope-body"></div>
<div class="envelope-seal">
<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2">
<path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>
</svg>
</div>
<div class="letter">
<div class="text-gray-800 text-left">
<p class="font-serif text-lg mb-3" style="color:#b76e79">The birthday angel 🪽,</p>
<p class="text-sm leading-relaxed mb-3" style="color:#5c3a4a">On this beautiful day, I want you to know just how incredibly special you are. Your kindness lights up every room, your laughter is the melody I never tire of hearing, and your presence makes the world a more beautiful place.</p>
<p class="text-sm leading-relaxed mb-3" style="color:#5c3a4a">May this year bring you countless reasons to smile, adventures that fill your heart with wonder, and moments that become cherished memories. You deserve all the love, happiness, and magic that life has to offer.</p>
<p class="text-sm leading-relaxed mb-4" style="color:#5c3a4a">Happy Birthday to someone who means the world to me. Here is to you, today and always.</p>
<p class="font-serif text-right" style="color:#b76e79"><br>❤️</p>
</div>
</div>
</div>
</div>
</section>

<!-- Photo & Poem Section -->
<section class="grid md:grid-cols-2 gap-10 items-center max-w-4xl mx-auto">
<div class="flex justify-center md:justify-end">
<div class="polaroid">
<div class="w-64 h-72 md:w-72 md:h-80 overflow-hidden rounded-sm bg-gray-200 relative">
<img src="https://images.unsplash.com/photo-1530103862676-de3c9a59aa38?w=600&h=700&fit=crop" alt="Birthday celebration" class="w-full h-full object-cover" onerror="this.src='https://images.unsplash.com/photo-1496337589254-7e19d01cec44?w=600&h=700&fit=crop'">
<div class="absolute inset-0 bg-gradient-to-t from-black/20 to-transparent"></div>
</div>
<p class="font-serif text-center mt-4 text-sm" style="color:#8b6072">A moment to cherish forever</p>
</div>
</div>
<div class="text-center md:text-left">
<h2 class="font-serif text-2xl md:text-3xl mb-6" style="color:#d4a574">A Birthday Poem</h2>
<div class="space-y-4 font-serif text-lg md:text-xl leading-relaxed" style="color:#f0c8d3">
<p class="italic">"The stars aligned on the day you were born,</p>
<p class="italic">Painting the sky with colors of dawn.</p>
<p class="italic">Each year you shine a little more bright,</p>
<p class="italic">A soul that fills the world with light.</p>
<p class="italic mt-4">May your path be lined with roses and gold,</p>
<p class="italic">And every dream your heart can hold.</p>
<p class="italic">For you deserve the sweetest things,</p>
<p class="italic">And all the joy that tomorrow brings."</p>
</div>
<div class="mt-6 flex items-center justify-center md:justify-start gap-2">
<span class="text-2xl heartbeat">❤️</span>
<span class="text-sm text-gray-400 font-light">Forever and always</span>
</div>
</div>
</section>

<!-- Footer -->
<footer class="text-center pt-12 pb-8">
<div class="w-16 h-0.5 mx-auto rounded-full mb-6" style="background:linear-gradient(90deg,transparent,#d4a574,transparent)"></div>
<p class="font-serif text-xl md:text-2xl mb-2" style="color:#f8e1e7">Wishing You the Happiest of Birthdays</p>
<p class="text-gray-400 text-sm">May your day be as wonderful as you are</p>
<div class="mt-6 flex justify-center gap-3">
<span class="text-rose-300 text-xl">🎂</span>
<span class="text-amber-300 text-xl">✨</span>
<span class="text-rose-300 text-xl">🎈</span>
<span class="text-amber-300 text-xl">💝</span>
<span class="text-rose-300 text-xl">🎂</span>
</div>
</footer>
</main>
</div>

<!-- Letter Modal -->
<div id="letter-modal" class="modal-overlay">
<div class="modal-content relative">
<button id="close-modal" class="absolute top-4 right-4 w-8 h-8 flex items-center justify-center rounded-full hover:bg-rose-100 transition-colors" style="color:#b76e79">
<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
<line x1="18" y1="6" x2="6" y2="18"/>
<line x1="6" y1="6" x2="18" y2="18"/>
</svg>
</button>
<div class="text-center mb-6">
<div class="w-12 h-12 mx-auto rounded-full flex items-center justify-center mb-3" style="background:linear-gradient(135deg,#f8e1e7,#f0c8d3)">
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#b76e79" stroke-width="2">
<path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>
</svg>
</div>
<h3 class="font-serif text-2xl" style="color:#b76e79">A Letter For You</h3>
</div>
<div class="space-y-4 text-gray-700 leading-relaxed">
<p class="font-serif text-lg" style="color:#b76e79">The Birthday Angel🪽,</p>
<p>On this beautiful day, I want you to know just how incredibly special you are. Your kindness lights up every room, your laughter is the melody I never tire of hearing, and your presence makes the world a more beautiful place.</p>
<p>May this year bring you countless reasons to smile, adventures that fill your heart with wonder, and moments that become cherished memories. You deserve all the love, happiness, and magic that life has to offer.</p>
<p>Happy Birthday to someone who means the world to me. Here is to you, today and always.</p>
<p class="font-serif text-right mt-6" style="color:#b76e79"><br>❤️</p>
</div>
</div>
</div>

<script>
// Sparkles
const sparklesContainer=document.getElementById('sparkles');
for(let i=0;i<30;i++){
const sparkle=document.createElement('div');
sparkle.className='sparkle';
sparkle.style.left=Math.random()*100+'%';
sparkle.style.top=Math.random()*100+'%';
sparkle.style.animationDelay=Math.random()*3+'s';
sparkle.style.animationDuration=(2+Math.random()*2)+'s';
sparklesContainer.appendChild(sparkle);
}

// Password
const passwordScreen=document.getElementById('password-screen');
const passwordInput=document.getElementById('password-input');
const unlockBtn=document.getElementById('unlock-btn');
const passwordError=document.getElementById('password-error');
const CORRECT_PASSWORD='1552005';

function checkPassword(){
const entered=passwordInput.value.trim();
if(entered===CORRECT_PASSWORD){
passwordError.classList.remove('show');
passwordInput.classList.remove('error');
confetti({particleCount:150,spread:80,origin:{y:0.6},colors:['#b76e79','#d4a574','#f8e1e7','#f0c8d3','#ffdb4d'],disableForReducedMotion:true});
setTimeout(()=>{
passwordScreen.classList.add('hidden');
introScreen.classList.add('active');
setTimeout(()=>{
document.querySelectorAll('#intro-screen .intro-text').forEach(el=>el.classList.add('animate'));
document.querySelector('#intro-screen .intro-btn').classList.add('animate');
},300);
},800);
}else{
passwordInput.classList.add('error');
passwordError.classList.add('show');
passwordInput.value='';
passwordInput.focus();
setTimeout(()=>passwordInput.classList.remove('error'),500);
}
}

unlockBtn.addEventListener('click',checkPassword);
passwordInput.addEventListener('keypress',(e)=>{if(e.key==='Enter')checkPassword()});
window.addEventListener('load',()=>{setTimeout(()=>passwordInput.focus(),500)});

// Intro
const introScreen=document.getElementById('intro-screen');
const beginBtn=document.getElementById('begin-btn');
const mainContent=document.getElementById('main-content');

beginBtn.addEventListener('click',()=>{
confetti({particleCount:100,spread:70,origin:{y:0.6},colors:['#b76e79','#d4a574','#f8e1e7','#f0c8d3','#ffdb4d'],disableForReducedMotion:true});
introScreen.classList.add('hidden');
setTimeout(()=>mainContent.classList.add('visible'),300);
});

// Present
const presentBox=document.getElementById('present-box');
const presentMessage=document.getElementById('present-message');
let presentOpened=false;

presentBox.addEventListener('click',function(){
if(presentOpened)return;
presentOpened=true;
this.classList.add('opened');
this.classList.remove('present-float');
const rect=this.getBoundingClientRect();
const x=(rect.left+rect.width/2)/window.innerWidth;
const y=(rect.top+rect.height/2)/window.innerHeight;
const defaults={spread:360,ticks:120,gravity:0.6,decay:0.95,startVelocity:35,colors:['#b76e79','#d4a574','#f8e1e7','#f0c8d3','#ffdb4d','#ff9a56','#e8b0c0','#c97a8a'],disableForReducedMotion:true};
confetti({...defaults,particleCount:100,origin:{x,y},scalar:1.2});
setTimeout(()=>confetti({...defaults,particleCount:60,origin:{x:x-0.1,y:y-0.1},scalar:0.8}),150);
setTimeout(()=>confetti({...defaults,particleCount:60,origin:{x:x+0.1,y:y-0.1},scalar:0.8}),300);
setTimeout(()=>presentMessage.style.opacity='1',600);
});

// Candles
const flames=document.querySelectorAll('.candle-flame');
const wishText=document.getElementById('wish-text');
let blownCandles=0;

flames.forEach(flame=>{
flame.addEventListener('click',function(){
if(this.classList.contains('blowout'))return;
this.classList.add('blowout');
blownCandles++;

const rect=this.getBoundingClientRect();
for(let i=0;i<3;i++){
setTimeout(()=>{
const smoke=document.createElement('div');
smoke.className='smoke-particle';
smoke.style.left=(rect.left+rect.width/2+(Math.random()-0.5)*15)+'px';
smoke.style.top=(rect.top)+'px';
document.body.appendChild(smoke);
setTimeout(()=>smoke.remove(),1500);
},i*100);
}

const x=(rect.left+rect.width/2)/window.innerWidth;
const y=(rect.top+rect.height/2)/window.innerHeight;
confetti({
particleCount:40,
spread:60,
origin:{x,y},
colors:['#ffdb4d','#ff9a56','#f8e1e7','#d4a574'],
gravity:1.2,
scalar:0.8,
disableForReducedMotion:true
});

if(blownCandles===flames.length){
setTimeout(()=>{
wishText.style.opacity='1';
setTimeout(()=>{
confetti({
particleCount:200,
spread:100,
origin:{y:0.5},
colors:['#b76e79','#d4a574','#f8e1e7','#f0c8d3','#ffdb4d','#ff9a56'],
disableForReducedMotion:true
});
},500);
},400);
}
});
});

// Balloon
const balloon=document.getElementById('balloon');
const balloonMessage=document.getElementById('balloon-message');
let balloonPopped=false;

balloon.addEventListener('click',function(){
if(balloonPopped)return;
balloonPopped=true;
this.classList.add('balloon-popped');
const rect=this.getBoundingClientRect();
const x=(rect.left+rect.width/2)/window.innerWidth;
const y=(rect.top+rect.height/2)/window.innerHeight;
const defaults={spread:360,ticks:100,gravity:0.8,decay:0.94,startVelocity:30,colors:['#b76e79','#d4a574','#f8e1e7','#f0c8d3','#ffdb4d','#ff9a56','#e8b0c0'],disableForReducedMotion:true};
confetti({...defaults,particleCount:80,origin:{x,y}});
setTimeout(()=>confetti({...defaults,particleCount:50,origin:{x,y}}),100);
setTimeout(()=>balloonMessage.style.opacity='1',400);
});

// Envelope
const envelope=document.getElementById('envelope');
const letterModal=document.getElementById('letter-modal');
const closeModal=document.getElementById('close-modal');
let envelopeOpen=false;

envelope.addEventListener('click',function(){
if(window.innerWidth<768){
letterModal.classList.add('active');
}else{
envelopeOpen=!envelopeOpen;
this.classList.toggle('open',envelopeOpen);
if(envelopeOpen){
const rect=this.getBoundingClientRect();
const x=(rect.left+rect.width/2)/window.innerWidth;
const y=(rect.top+rect.height/2)/window.innerHeight;
confetti({particleCount:30,spread:50,origin:{x,y},colors:['#f8e1e7','#f0c8d3','#d4a574'],scalar:0.6,disableForReducedMotion:true});
}
}
});

closeModal.addEventListener('click',()=>letterModal.classList.remove('active'));
letterModal.addEventListener('click',(e)=>{if(e.target===letterModal)letterModal.classList.remove('active')});

document.addEventListener('click',(e)=>{
if(window.innerWidth>=768&&envelopeOpen&&!envelope.contains(e.target)){
envelopeOpen=false;
envelope.classList.remove('open');
}
});

// Parallax
if(window.innerWidth>=768){
document.addEventListener('mousemove',(e)=>{
const x=(e.clientX/window.innerWidth-0.5)*20;
const y=(e.clientY/window.innerHeight-0.5)*20;
sparklesContainer.style.transform=`translate(${x*0.5}px,${y*0.5}px)`;
});
}

// Context menu
document.addEventListener('contextmenu',(e)=>{
if(e.target.closest('.candle-flame')||e.target.closest('#balloon')||e.target.closest('#envelope')||e.target.closest('#present-box')){
e.preventDefault();
}
});
</script>
</body>
</html>
