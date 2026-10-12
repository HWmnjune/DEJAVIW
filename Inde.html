<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>데자뷔 (Déjà Vu) v1.2.1 — 무의식의 회랑</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.css">
  <style>
    /* ── v1.2.1 통일 타입 시스템 ──
       기존엔 Pretendard 지정 + 곳곳의가 뒤섞여, 폰트가 안 불러와지면
       제각각인 시스템 폰트로 떨어져 "AI가 대충 만든" 인상을 줬다.
       이제 UI 전체를 Pretendard 하나로 통일하고(가독성 높은 한글 게임 표준 폰트),
       숫자 계기(HUD 수치)에만 mono를 쓴다. 크기·자간도 또렷하게 재정비. */
    :root { --font-ui: 'Pretendard Variable','Pretendard',-apple-system,system-ui,sans-serif;
            --font-num: 'Pretendard Variable','Pretendard',ui-monospace,monospace; }
    body {
      margin: 0;
      overflow: hidden;
      user-select: none;
      -webkit-user-select: none;
      font-family: var(--font-ui);
      letter-spacing: -0.01em;
      background-color: #050505;
      color: #f3f4f6;
      touch-action: none;
      -webkit-font-smoothing: antialiased;
    }
    /* 게임 전역: 몽환적 자간 남발을 억제하고 또렷하게 */
    .hud-title { font-weight: 800; letter-spacing: 0.06em; }
    .ui-num { font-family: var(--font-num); font-variant-numeric: tabular-nums; font-feature-settings: "tnum"; }
    .ui-note { font-family: var(--font-ui); letter-spacing: 0; }
    /* 타이틀만 살짝 넓은 자간 허용 (분위기), 본문·안내는 표준 자간 */
    #note-body, #note-title { letter-spacing: -0.005em; }
    .vhs-effect::after {
      content: " ";
      display: block;
      position: absolute;
      top: 0; left: 0; bottom: 0; right: 0;
      background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.28) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.045), rgba(0, 255, 0, 0.018), rgba(0, 0, 255, 0.045));
      background-size: 100% 4px, 6px 100%;
      pointer-events: none;
      z-index: 10;
      opacity: 0.8;
    }
    .vignette {
      position: absolute;
      top: 0; left: 0; width: 100%; height: 100%;
      box-shadow: inset 0 0 130px rgba(0,0,0,0.96);
      pointer-events: none;
      z-index: 5;
    }
    /* ══ 옷장 내부 시야 (v1.2.0) ══
       v1.1.0은 그냥 둥근 비네트라 "왜 시야가 좁아졌지?"로만 읽혔다.
       실제 사물함처럼 '가로 통풍 슬릿 사이로 내다본다'는 게 읽히도록,
       세로 방향 마스크 + 슬릿 줄무늬 + 금속 문틀을 겹쳐 그린다. */
    #locker-vision {
      position: absolute;
      inset: 0;
      pointer-events: none;
      z-index: 40;
      opacity: 0;
      transition: opacity 0.5s ease;
      background:
        /* 슬릿 살(louver) — 가로 막대.
           살이 너무 두껍고 진하면 '옷장답긴 한데 아무것도 안 보이는' 상태가 되어
           다가오는 위협을 판단할 수 없다. 살 5px / 틈 13px, 농도 0.78로 잡아
           시야는 확보하면서 격자만 읽히게 한다. */
        repeating-linear-gradient(
          180deg,
          rgba(0,0,0,0.78) 0px, rgba(0,0,0,0.78) 5px,
          rgba(0,0,0,0.04) 5px, rgba(0,0,0,0.04) 18px
        ),
        /* 문틈 밖 영역을 덮는 어둠 */
        radial-gradient(ellipse 44% 34% at 50% 47%, transparent 48%, rgba(0,0,0,0.96) 80%);
      -webkit-mask-image: radial-gradient(ellipse 60% 46% at 50% 47%, black 40%, transparent 92%);
      mask-image: radial-gradient(ellipse 60% 46% at 50% 47%, black 40%, transparent 92%);
    }
    /* 슬릿 바깥은 완전 암전 — 마스크가 미치지 않는 가장자리를 덮는다 */
    #locker-frame {
      position: absolute;
      inset: 0;
      pointer-events: none;
      z-index: 39;
      opacity: 0;
      transition: opacity 0.5s ease;
      background: radial-gradient(ellipse 44% 34% at 50% 47%, transparent 55%, rgba(0,0,0,0.99) 82%);
      box-shadow: inset 0 0 0 14px #0b0b0d, inset 0 0 60px 30px rgba(0,0,0,0.95);
    }
    .in-locker #locker-vision { opacity: 1; }
    .in-locker #locker-frame { opacity: 1; }
    /* 옷장 안에서는 조준점·크로스헤어를 감춘다 (조준할 게 없다) */
    .in-locker #crosshair { opacity: 0; }

    /* 옷장 전용 패널 — 금속 사물함 느낌 */
    #locker-panel {
      background: linear-gradient(180deg, #17181b 0%, #0e0f11 100%);
      border: 1px solid #33363c;
      box-shadow: 0 0 0 1px rgba(0,0,0,0.8), 0 18px 40px rgba(0,0,0,0.75), inset 0 1px 0 rgba(255,255,255,0.06);
    }
    #locker-panel .louver {
      height: 3px;
      background: repeating-linear-gradient(90deg, #2a2d33 0 10px, #14161a 10px 13px);
      border-radius: 2px;
    }

    #fade-overlay {
      position: absolute;
      inset: 0;
      background: #000;
      opacity: 0;
      pointer-events: none;
      z-index: 45;
      transition: opacity 0.16s ease;
    }
    #fade-overlay.on { opacity: 1; }

    /* 피격 잼스케어 */
    @keyframes hardShake {
      0%, 100% { transform: translate(0, 0); }
      12% { transform: translate(-14px, 8px); }
      25% { transform: translate(11px, -12px); }
      38% { transform: translate(-9px, -7px); }
      52% { transform: translate(13px, 9px); }
      66% { transform: translate(-12px, 5px); }
      80% { transform: translate(8px, -10px); }
    }
    #jumpscare-overlay {
      position: absolute;
      inset: 0;
      z-index: 60;
      display: none;
      align-items: center;
      justify-content: center;
      background: radial-gradient(circle at 50% 50%, rgba(127,4,4,0.92), rgba(0,0,0,0.99) 78%);
      pointer-events: none;
    }
    #jumpscare-overlay.on {
      display: flex;
      animation: hardShake 0.35s linear infinite;
    }
    #jumpscare-overlay .scare-eyes {
      display: flex;
      gap: 5.5rem;
      filter: drop-shadow(0 0 24px rgba(255,0,0,0.95));
    }
    #jumpscare-overlay .scare-eye {
      width: 3.2rem; height: 5.2rem;
      background: #ff1a1a;
      border-radius: 50% 50% 42% 42%;
    }
    #jumpscare-text {
      position: absolute;
      bottom: 18%;
      width: 100%;
      text-align: center;
      font-weight: 900;
      letter-spacing: 0.55em;
      font-size: 1.6rem;
      color: #fecaca;
      text-shadow: 0 0 18px rgba(255,0,0,0.9);
    }

    /* 상단 중앙 배너 토스트 */
    #event-banner {
      position: absolute;
      top: 4.5rem;
      left: 50%;
      transform: translate(-50%, -14px);
      z-index: 35;
      pointer-events: none;
      opacity: 0;
      transition: opacity 0.3s ease, transform 0.3s ease;
    }
    #event-banner.show {
      opacity: 1;
      transform: translate(-50%, 0);
    }

    /* 메모 종이 질감 */
    .note-paper {
      background:
        linear-gradient(rgba(6,182,212,0.03), rgba(0,0,0,0)),
        repeating-linear-gradient(0deg, rgba(255,255,255,0.02) 0 1px, transparent 1px 26px),
        #101012;
    }

    #canvas-container {
      filter: saturate(0.32) contrast(1.14) brightness(0.94);
    }
    .transition-all-300 { transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); }

    input[type="range"]::-webkit-slider-thumb { cursor: pointer; }

    /* 모바일/좁은 화면 대응 */
    @media (max-width: 768px) {
      #key-guide { display: none; }
      #hud-scanner { width: 13.5rem; padding: 0.8rem; }
      #hud-scanner .hud-title { font-size: 9px; }
    }
    .no-touch #touch-joystick-zone { display: none; }
  </style>
</head>
<body class="w-full h-screen select-none overflow-hidden">

  <!-- ══════════ 시작 화면 ══════════ -->
  <div id="start-screen" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center p-5 text-center select-none overflow-y-auto">
    <div class="max-w-xl w-full space-y-6 my-auto">
      <div class="space-y-2.5">
        <p class="text-red-500 text-xs md:text-sm font-black tracking-[0.4em] uppercase">Meta-Horror Memory Descent</p>
        <h1 class="text-5xl md:text-6xl font-black tracking-widest text-neutral-200">DÉJÀ VU</h1>
        <p class="text-xs md:text-sm text-neutral-500 font-bold tracking-[0.25em]">트라우마의 잠긴 방들 · v1.2.1</p>
      </div>

      <div class="p-5 md:p-7 bg-neutral-950 border border-neutral-900 rounded-2xl text-left text-sm text-neutral-300 space-y-4 leading-relaxed">
        <p>당신은 깨어날 수 없는 회랑에 격리되었습니다. <span class="text-cyan-400 font-bold">B10F</span>까지 하강해, 무의식이 유기한 <span class="text-cyan-400 font-bold">기억 4점</span>을 회수하십시오.</p>

        <div class="p-4 bg-black/60 border border-red-950/60 rounded-xl space-y-2">
          <p class="text-red-400 font-black text-sm tracking-wider">⚠ 하강 규칙 — 반드시 기억할 것</p>
          <p class="text-neutral-300 text-sm"><span class="text-red-300 font-bold">어긋남이 하나라도 있다면</span> 뒤돌아 <span class="text-amber-400 font-bold">회귀 게이트(▲)</span>로, <span class="text-neutral-100 font-bold">모든 것이 익숙하다면</span> <span class="text-cyan-400 font-bold">심층 게이트(▼)</span>로 나아가십시오. 올바른 판단만이 당신을 한 층 아래로 데려갑니다.</p>
          <p class="text-neutral-300 text-sm"><span class="text-amber-300 font-bold">어긋남은 회랑에만 있지 않습니다.</span> 세 개의 방(A·B·C) 안에도 숨어 있습니다. <span class="text-neutral-100 font-bold">방을 꼼꼼히 살피십시오.</span> 좌측 HUD의 점검 표시로 아직 확인하지 않은 방을 알 수 있습니다.</p>
          <p class="text-neutral-400 text-sm"><span class="text-red-300 font-bold">겁먹게 하는 모든 것은 어긋남입니다.</span> 갑작스러운 정전, 스쳐가는 실루엣, 문을 두드리는 소리, 그리고 '그것'의 출현 — 무엇이든 튀어나왔다면 그 층은 이미 어긋나 있습니다. 즉시 회귀하십시오.</p>
          <p class="text-neutral-500 text-xs">판단을 그르치면 한 층 위로 되돌아갑니다. 잃는 것은 언제나 한 층뿐입니다.</p>
        </div>

        <ul class="list-disc pl-5 space-y-1.5 text-neutral-400 text-xs md:text-sm">
          <li>이동 <span class="text-neutral-200 ui-num">WASD</span> · 달리기 <span class="text-neutral-200 ui-num">Shift</span> · 앉기 <span class="text-neutral-200 ui-num">Ctrl / C</span> · 상호작용 <span class="text-neutral-200 ui-num">E 또는 클릭</span></li>
          <li>PC: 화면을 한 번 클릭하면 <span class="text-cyan-400 font-bold">마우스만으로 시점이 회전</span>합니다. (ESC로 해제) 드래그도 지원됩니다.</li>
          <li>모바일: 좌하단 <span class="text-cyan-400 font-bold">가상 스틱</span>으로 이동, 화면 우측 절반 드래그로 시점 회전.</li>
          <li>세 개의 방을 수색해 기억을 동조하고, 쫓길 땐 회랑의 <span class="text-cyan-400 font-bold">옷장</span>에 웅크려 숨으십시오.</li>
          <li><span class="text-neutral-300 font-bold">B1F는 언제나 정상입니다.</span> 이곳의 모습을 '기준'으로 외워 두십시오.</li>
        </ul>
      </div>

      <button onclick="startGameEvent(event)" class="w-full py-4 bg-red-700 hover:bg-red-600 active:scale-95 text-white font-bold text-base tracking-widest rounded-xl transition-all shadow-[0_0_25px_rgba(185,28,28,0.6)] cursor-pointer">
        심연 속으로 입장 (NEW DIVE)
      </button>
      <button id="continue-btn" onclick="continueGame(event)" class="w-full py-3.5 bg-neutral-900 hover:bg-neutral-800 active:scale-95 text-cyan-300 font-bold text-sm tracking-widest rounded-xl transition-all border border-cyan-900/50 cursor-pointer hidden">
        이어하기 (CONTINUE) · <span id="continue-info" class="ui-num text-neutral-400"></span>
      </button>
      <p class="text-[10px] text-neutral-600">⚠ 헤드폰 착용 권장 · 급격한 화면 점멸과 큰 소리가 포함되어 있습니다. · 진행은 자동 저장됩니다.</p>
    </div>
  </div>

  <!-- ══════════ 메인 게임 뷰포트 ══════════ -->
  <div id="game-container" class="relative w-full h-full vhs-effect" style="pointer-events: none;">
    <div id="canvas-container" class="absolute inset-0 w-full h-full">
      <canvas id="three-canvas" class="absolute inset-0 w-full h-full block cursor-pointer z-1"></canvas>
    </div>
    <div class="vignette"></div>
    <div id="locker-frame"></div>
    <div id="locker-vision"></div>
    <div id="fade-overlay"></div>

    <!-- 시점 조작 최초 안내 -->
    <div id="pointer-lock-guide" class="absolute inset-0 bg-black/55 z-30 flex items-center justify-center text-center select-none pointer-events-none transition-opacity duration-300">
      <div class="p-7 bg-neutral-950/95 border border-neutral-800 rounded-2xl max-w-sm shadow-2xl">
        <svg class="w-11 h-11 text-cyan-400 mx-auto mb-4 animate-bounce" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15.042 21.672L13.684 16.6m0 0l-2.51 2.225.569-9.47 5.227 7.917-3.286-.672zM12 2.25V4.5m5.834.166l-1.591 1.591M20.25 10.5H18M7.757 14.743l-1.59 1.59M6 10.5H3.75m4.007-4.243l-1.59-1.59" /></svg>
        <p class="text-base font-bold text-neutral-200">화면을 클릭하면 마우스로 시점이 회전합니다.</p>
        <p class="text-xs text-neutral-500 mt-2">드래그로도 회전할 수 있습니다 · 설정은 우측 상단 톱니바퀴 또는 ESC</p>
      </div>
    </div>

    <!-- 크로스헤어 / 상호작용 안내 -->
    <div id="crosshair-container" class="absolute inset-0 flex items-center justify-center pointer-events-none z-30">
      <div id="crosshair" class="w-2.5 h-2.5 bg-white rounded-full opacity-80 transition-all duration-200 shadow-[0_0_8px_rgba(255,255,255,0.8)]"></div>
      <div id="interaction-prompt" class="absolute mt-16 bg-black/95 border border-cyan-900/60 text-xs px-4 py-2.5 rounded-lg text-cyan-300 font-bold tracking-wider hidden shadow-2xl">
        상호작용 [E]
      </div>
    </div>

    <!-- 옷장 내부 상시 안내 -->
    <div id="locker-hint" class="absolute bottom-24 md:bottom-10 left-1/2 -translate-x-1/2 z-[41] hidden pointer-events-none">
      <div id="locker-panel" class="rounded-xl px-6 py-3.5 w-72 text-center">
        <div class="louver mb-3 opacity-70"></div>
        <div class="flex items-center justify-center gap-2 mb-2">
          <span id="locker-led" class="w-2 h-2 rounded-full bg-cyan-400 shadow-[0_0_8px_rgba(34,211,238,0.9)]"></span>
          <p class="text-[11px] font-black tracking-[0.28em] text-neutral-400 uppercase">Locker · 은신 중</p>
        </div>
        <p id="locker-hide-status" class="text-sm font-bold text-cyan-300">완전히 숨었습니다</p>
        <p id="locker-hide-sub" class="text-[11px] mt-0.5 text-neutral-500">숨을 죽이고 문틈 너머를 살피십시오</p>
        <div class="louver mt-3 mb-2.5 opacity-70"></div>
        <div class="flex justify-center gap-4 text-[11px] text-neutral-500">
          <span><span class="text-neutral-300">E</span> 나가기</span>
          <span><span class="text-neutral-300">드래그</span> 둘러보기</span>
          <span><span class="text-neutral-300">Ctrl</span> 자세</span>
        </div>
      </div>
    </div>

    <!-- 상단 중앙 배너 -->
    <div id="event-banner">
      <div class="bg-black/90 border border-neutral-800 rounded-xl px-6 py-2.5 shadow-2xl">
        <p id="event-banner-text" class="text-sm font-black tracking-[0.2em] text-neutral-200"></p>
      </div>
    </div>

    <!-- 좌측 상단 HUD -->
    <div class="absolute top-4 left-4 z-20 flex flex-col gap-3 pointer-events-none select-none">
      <div id="hud-scanner" class="bg-black/85 border border-neutral-900 rounded-xl p-4 backdrop-blur-md w-72 shadow-2xl">
        <div class="flex items-center gap-2 border-b border-neutral-900 pb-2 mb-3">
          <span class="w-2 h-2 rounded-full bg-red-600 animate-ping"></span>
          <h2 class="hud-title text-xs font-black tracking-widest text-red-500 uppercase">무의식 심층 스캐너</h2>
          <span id="loop-counter" class="ml-auto text-sm ui-num font-black text-amber-400">B1F</span>
        </div>
        <div class="space-y-3.5">
          <div>
            <div class="flex justify-between items-center mb-1.5">
              <span class="text-xs text-neutral-300 font-semibold">기억 동조율 (Synchrony)</span>
              <span id="sync-text" class="text-sm ui-num font-bold text-cyan-400">0%</span>
            </div>
            <div class="w-full bg-neutral-900 h-2 rounded-full overflow-hidden border border-neutral-800">
              <div id="sync-bar" class="bg-cyan-500 h-full transition-all duration-500" style="width:0%"></div>
            </div>
          </div>
          <div>
            <div class="flex justify-between items-center mb-1.5">
              <span class="text-xs text-neutral-300 font-semibold">위협 지표 (HR)</span>
              <span id="heart-rate-text" class="text-sm ui-num font-bold text-red-500">72 BPM</span>
            </div>
            <div class="w-full bg-neutral-900 h-2 rounded-full overflow-hidden border border-neutral-800">
              <div id="heart-rate-bar" class="bg-red-600 h-full transition-all duration-300" style="width:14%"></div>
            </div>
          </div>
          <div class="border-t border-neutral-900/60 pt-2.5 space-y-1 text-xs">
            <div class="flex justify-between items-center">
              <span class="text-neutral-500">현재 구역</span>
              <span id="hud-location" class=" text-neutral-300">중앙 회랑</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-neutral-500">자세</span>
              <span id="hud-posture" class=" text-neutral-300">서 있음</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-neutral-500">방 점검</span>
              <span class=" flex gap-1.5">
                <span id="hud-room-a" class="px-1.5 rounded border border-neutral-800 text-neutral-600">A</span>
                <span id="hud-room-b" class="px-1.5 rounded border border-neutral-800 text-neutral-600">B</span>
                <span id="hud-room-c" class="px-1.5 rounded border border-neutral-800 text-neutral-600">C</span>
              </span>
            </div>
            <div class="flex justify-between items-center pt-1 border-t border-neutral-900/40">
              <span class="text-neutral-600 text-[10px]">어긋남 → <span class="text-amber-500 font-bold">▲ 회귀</span></span>
              <span class="text-neutral-600 text-[10px]">익숙함 → <span class="text-cyan-500 font-bold">심층 ▼</span></span>
            </div>
          </div>
        </div>
      </div>

      <div id="key-guide" class="bg-black/50 border border-neutral-950 rounded-lg p-3.5 backdrop-blur-sm w-72">
        <h3 class="text-[10px] text-neutral-400 font-bold mb-2 tracking-wider uppercase">조작 키 가이드</h3>
        <ul class="text-xs text-neutral-400 space-y-1">
          <li class="flex justify-between"><span>이동</span> <span class="text-neutral-200">WASD / 방향키</span></li>
          <li class="flex justify-between"><span>시점 회전</span> <span class="text-neutral-200">마우스 (클릭 후) / 드래그</span></li>
          <li class="flex justify-between"><span>상호작용</span> <span class="text-neutral-200">E / 좌클릭</span></li>
          <li class="flex justify-between"><span>달리기 · 앉기</span> <span class="text-neutral-200">Shift · Ctrl / C</span></li>
          <li class="flex justify-between"><span>소지품 · 일시정지</span> <span class="text-neutral-200">I · ESC</span></li>
        </ul>
      </div>
    </div>

    <!-- 우측 상단 버튼 -->
    <div class="absolute top-4 right-4 z-20 flex items-center gap-2">
      <button onclick="toggleInventory(event)" class="w-12 h-12 bg-black/85 hover:bg-neutral-900 text-neutral-400 hover:text-cyan-400 border border-neutral-800 rounded-xl flex items-center justify-center transition-all shadow-lg active:scale-95 pointer-events-auto" title="소지품 목록 [I]">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="1.7" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"/></svg>
      </button>
      <button onclick="togglePause(event)" class="w-12 h-12 bg-black/85 hover:bg-neutral-900 text-red-500 hover:text-red-400 border border-neutral-800 rounded-xl flex items-center justify-center transition-all shadow-lg active:scale-95 pointer-events-auto" title="설정 / 일시정지 [ESC]">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="1.7" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"/><path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
      </button>
    </div>

    <!-- 하단 조작 HUD (조이스틱: 터치 전용 / 액션 버튼: 공용) -->
    <div id="mobile-hud" class="absolute inset-0 pointer-events-none z-10 flex justify-between items-end p-5 select-none">
      <div id="touch-joystick-zone" class="w-1/2 h-[55%] pointer-events-auto relative">
        <div id="joystick-base" class="w-24 h-24 rounded-full border-2 border-white/25 bg-black/20 backdrop-blur-[1px] absolute hidden">
          <div id="joystick-stick" class="w-10 h-10 bg-white/40 rounded-full absolute top-1/2 left-1/2 shadow-xl" style="transform: translate(-50%, -50%);"></div>
        </div>
      </div>

      <div class="flex flex-col gap-2.5 items-end pointer-events-auto select-none">
        <button id="touch-interact" class="w-16 h-16 bg-neutral-950/90 border border-neutral-800 text-white rounded-full flex flex-col items-center justify-center transition-all shadow-xl active:scale-90 opacity-60">
          <svg class="w-6 h-6 text-cyan-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15.042 21.672L13.684 16.6m0 0l-2.51 2.225.569-9.47 5.227 7.917-3.286-.672z"/></svg>
          <span class="text-[10px] mt-0.5 font-bold">작용 E</span>
        </button>
        <button id="touch-sprint" class="w-16 h-16 bg-neutral-950/90 border border-neutral-800 text-white rounded-full flex flex-col items-center justify-center transition-all shadow-xl active:scale-90">
          <svg class="w-6 h-6 text-orange-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>
          <span class="text-[10px] mt-0.5 font-bold">달리기</span>
        </button>
        <button id="touch-crouch" class="w-16 h-16 bg-neutral-950/90 border border-neutral-800 text-white rounded-full flex flex-col items-center justify-center transition-all shadow-xl active:scale-90">
          <svg id="touch-crouch-icon-down" class="w-6 h-6 text-cyan-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M19 14l-7 7-7-7m14-8l-7 7-7-7"/></svg>
          <svg id="touch-crouch-icon-up" class="w-6 h-6 text-cyan-400 hidden" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 10l7-7 7 7M5 18l7-7 7 7"/></svg>
          <span class="text-[10px] mt-0.5 font-bold" id="touch-crouch-label">앉기</span>
        </button>
      </div>
    </div>

    <!-- 스릴/피격 글리치 점등 -->
    <div id="glitch-overlay" class="absolute inset-0 pointer-events-none z-40 transition-colors duration-75" style="background-color: rgba(153,27,27,0);"></div>

    <!-- 잼스케어 오버레이 -->
    <div id="jumpscare-overlay">
      <div class="scare-eyes">
        <div class="scare-eye"></div>
        <div class="scare-eye"></div>
      </div>
      <p id="jumpscare-text">붙잡혔다</p>
    </div>

    <!-- ══════════ 기억 튜닝 퍼즐 모달 (Room B 모니터) ══════════ -->
    <div id="puzzle-modal" class="absolute inset-0 bg-black/95 z-50 items-center justify-center p-4 hidden pointer-events-auto">
      <div class="bg-neutral-950 border-2 border-cyan-900/60 rounded-2xl max-w-md w-full p-6 shadow-[0_0_50px_rgba(6,182,212,0.15)] relative">
        <button onclick="closePuzzleModal(event)" class="absolute top-3 right-3 text-neutral-400 hover:text-white transition-colors p-2 rounded-lg hover:bg-neutral-900" title="닫기">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/></svg>
        </button>
        <div class="text-center mb-5">
          <h2 class="text-lg font-black text-cyan-400 uppercase tracking-widest">Memory Tuning · 기억 복원 동조기</h2>
          <p class="text-xs text-neutral-400 mt-1">두 슬라이더로 실선 파형을 점선 목표 파형에 겹치십시오.</p>
        </div>

        <div class="space-y-5 p-4 bg-neutral-900/40 rounded-xl border border-neutral-900">
          <div>
            <div class="flex justify-between text-sm text-neutral-300 mb-1.5">
              <span>알파 주파수 (파형 간격)</span>
              <span id="slider-val-1" class="ui-num text-cyan-400">10</span>
            </div>
            <input type="range" id="puzzle-slider-1" min="0" max="100" value="10" class="w-full accent-cyan-500 bg-neutral-800 h-2 rounded-lg appearance-none cursor-pointer">
          </div>
          <div>
            <div class="flex justify-between text-sm text-neutral-300 mb-1.5">
              <span>감마 공명도 (파형 높이)</span>
              <span id="slider-val-2" class="ui-num text-cyan-400">90</span>
            </div>
            <input type="range" id="puzzle-slider-2" min="0" max="100" value="90" class="w-full accent-cyan-500 bg-neutral-800 h-2 rounded-lg appearance-none cursor-pointer">
          </div>

          <div class="h-20 bg-neutral-950 rounded-lg border border-cyan-950/60 relative overflow-hidden flex items-center justify-center">
            <svg id="puzzle-wave-svg" class="w-full h-full" viewBox="0 0 200 60" preserveAspectRatio="none">
              <path id="wave-target" d="" fill="none" stroke="#155e75" stroke-width="2" stroke-dasharray="3,3"></path>
              <path id="wave-current" d="" fill="none" stroke="#06b6d4" stroke-width="2.5"></path>
            </svg>
            <div id="puzzle-success-text" class="absolute text-xs font-black text-green-400 tracking-wider hidden animate-pulse bg-black/85 px-4 py-2 rounded border border-green-950">
              동조 성공 — 기억 '멈춘 회중시계' 회수
            </div>
          </div>
        </div>
        <p class="text-xs text-neutral-500 text-center mt-4">두 값 모두 목표와의 오차 ±4 이내에 들어오면 자동 저장됩니다.</p>
      </div>
    </div>

    <!-- ══════════ 키패드 모달 (Room B 서랍) ══════════ -->
    <div id="keypad-modal" class="absolute inset-0 bg-black/95 z-50 items-center justify-center p-4 hidden pointer-events-auto">
      <div class="bg-neutral-950 border-2 border-amber-900/50 rounded-2xl max-w-xs w-full p-6 shadow-[0_0_50px_rgba(245,158,11,0.12)] relative">
        <button onclick="closeKeypadModal(event)" class="absolute top-3 right-3 text-neutral-400 hover:text-white transition-colors p-2 rounded-lg hover:bg-neutral-900" title="닫기">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/></svg>
        </button>
        <div class="text-center mb-4">
          <h2 class="text-base font-black text-amber-400 uppercase tracking-widest">잠긴 서랍</h2>
          <p class="text-xs text-neutral-500 mt-1">4자리 암호 — <span class="text-neutral-400">그날의 시간이 모든 잠금을 연다</span></p>
        </div>
        <div id="keypad-display" class="h-14 bg-black border border-neutral-800 rounded-xl flex items-center justify-center ui-num text-3xl tracking-[0.5em] text-amber-300 mb-4 pl-3">····</div>
        <div class="grid grid-cols-3 gap-2" id="keypad-grid">
          <!-- 숫자 버튼은 스크립트에서 생성 -->
        </div>
      </div>
    </div>

    <!-- ══════════ 메모 열람 모달 ══════════ -->
    <div id="note-modal" class="absolute inset-0 bg-black/95 z-50 items-center justify-center p-4 hidden pointer-events-auto">
      <div class="note-paper border border-neutral-800 rounded-2xl max-w-md w-full p-7 shadow-2xl relative">
        <button onclick="closeNoteModal(event)" class="absolute top-3 right-3 text-neutral-500 hover:text-white transition-colors p-2 rounded-lg hover:bg-neutral-900" title="닫기">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/></svg>
        </button>
        <p id="note-kicker" class="text-[10px] text-neutral-600 tracking-[0.3em] uppercase mb-2">Fragment</p>
        <h3 id="note-title" class="text-lg font-black text-neutral-100 mb-4"></h3>
        <div id="note-body" class="text-sm text-neutral-300 leading-loose whitespace-pre-line font-medium"></div>
        <p class="ui-note text-[11px] text-neutral-500 mt-5 text-right">아무 곳이나 눌러 덮기 · E · ESC</p>
      </div>
    </div>

    <!-- ══════════ 소지품 모달 ══════════ -->
    <div id="inventory-modal" class="absolute inset-0 bg-black/95 z-50 items-center justify-center p-4 hidden pointer-events-auto">
      <div class="bg-neutral-950 border border-neutral-800 rounded-2xl max-w-2xl w-full p-6 shadow-2xl relative max-h-[92vh] overflow-y-auto">
        <button onclick="closeInventory(event)" class="absolute top-3 right-3 text-neutral-400 hover:text-white transition-colors p-2 rounded-lg hover:bg-neutral-900" title="닫기 [I]">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/></svg>
        </button>
        <h2 class="text-xl font-black tracking-widest text-cyan-400 mb-1 uppercase border-b border-neutral-900 pb-3">
          Subconscious Storage · 무의식 수집함
        </h2>
        <p class="text-sm text-neutral-400 mb-5 font-medium">회수한 기억을 선택하면 봉인된 내면 기록이 복원됩니다. <span id="inv-progress" class="ui-num text-cyan-500">0 / 4</span></p>

        <div class="grid grid-cols-2 md:grid-cols-4 gap-3" id="inventory-grid">
          <div data-item-id="glasses" class="inventory-card bg-neutral-900/40 border border-neutral-800 rounded-xl p-4 flex flex-col items-center text-center cursor-pointer hover:border-cyan-500 hover:bg-neutral-900/60 transition-all group">
            <div class="w-16 h-16 flex items-center justify-center bg-neutral-950 rounded-lg mb-2.5 border border-neutral-800 group-hover:border-cyan-950">
              <svg class="w-10 h-10 text-neutral-600 group-hover:text-cyan-400 transition-colors" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                <circle cx="7" cy="13" r="3.2"/><circle cx="17" cy="13" r="3.2"/>
                <path stroke-linecap="round" d="M10.2 13h3.6M3.8 13H2.5m19 0h-1.3M5.5 10.4L4 6m14.5 4.4L20 6"/>
                <path stroke-linecap="round" d="M15.8 15.4l2.4 2.6" opacity="0.6"/>
              </svg>
            </div>
            <h3 class="font-bold text-xs text-neutral-300 group-hover:text-white">깨진 안경</h3>
            <span class="text-[10px] text-neutral-600 mt-1 uppercase tracking-wider" id="item-status-glasses">미회수</span>
          </div>

          <div data-item-id="clock" class="inventory-card bg-neutral-900/40 border border-neutral-800 rounded-xl p-4 flex flex-col items-center text-center cursor-pointer hover:border-cyan-500 hover:bg-neutral-900/60 transition-all group">
            <div class="w-16 h-16 flex items-center justify-center bg-neutral-950 rounded-lg mb-2.5 border border-neutral-800 group-hover:border-cyan-950">
              <svg class="w-10 h-10 text-neutral-600 group-hover:text-cyan-400 transition-colors" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                <circle cx="12" cy="13" r="7.5"/><path stroke-linecap="round" d="M12 13V9.5M12 13l-2.6 2.9M10 3.5h4M12 3.5v2"/>
              </svg>
            </div>
            <h3 class="font-bold text-xs text-neutral-300 group-hover:text-white">멈춘 회중시계</h3>
            <span class="text-[10px] text-neutral-600 mt-1 uppercase tracking-wider" id="item-status-clock">미회수</span>
          </div>

          <div data-item-id="diary" class="inventory-card bg-neutral-900/40 border border-neutral-800 rounded-xl p-4 flex flex-col items-center text-center cursor-pointer hover:border-cyan-500 hover:bg-neutral-900/60 transition-all group">
            <div class="w-16 h-16 flex items-center justify-center bg-neutral-950 rounded-lg mb-2.5 border border-neutral-800 group-hover:border-cyan-950">
              <svg class="w-10 h-10 text-neutral-600 group-hover:text-cyan-400 transition-colors" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 3.5h9.5l3 3V20a.5.5 0 01-.5.5H6a.5.5 0 01-.5-.5V4a.5.5 0 01.5-.5z"/>
                <path stroke-linecap="round" d="M8.5 9h7M8.5 12.5h7M8.5 16h4"/>
                <path stroke-linecap="round" d="M14.5 18.5l4-5" opacity="0.5"/>
              </svg>
            </div>
            <h3 class="font-bold text-xs text-neutral-300 group-hover:text-white">찢어진 일기장</h3>
            <span class="text-[10px] text-neutral-600 mt-1 uppercase tracking-wider" id="item-status-diary">미회수</span>
          </div>

          <div data-item-id="band" class="inventory-card bg-neutral-900/40 border border-neutral-800 rounded-xl p-4 flex flex-col items-center text-center cursor-pointer hover:border-cyan-500 hover:bg-neutral-900/60 transition-all group">
            <div class="w-16 h-16 flex items-center justify-center bg-neutral-950 rounded-lg mb-2.5 border border-neutral-800 group-hover:border-cyan-950">
              <svg class="w-10 h-10 text-neutral-600 group-hover:text-cyan-400 transition-colors" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                <ellipse cx="12" cy="12" rx="8.5" ry="4.5" transform="rotate(-25 12 12)"/>
                <rect x="8.6" y="9.6" width="6.8" height="3.4" rx="1" transform="rotate(-25 12 11.3)"/>
              </svg>
            </div>
            <h3 class="font-bold text-xs text-neutral-300 group-hover:text-white">환자 인식 팔찌</h3>
            <span class="text-[10px] text-neutral-600 mt-1 uppercase tracking-wider" id="item-status-band">미회수</span>
          </div>
        </div>

        <div class="mt-4 p-5 bg-neutral-900/80 rounded-xl border border-neutral-800" id="item-description-panel">
          <p class="text-sm text-neutral-400 text-center py-2">회수가 완료된 기억을 선택하면 내면 기록이 복원됩니다.</p>
        </div>
      </div>
    </div>

    <!-- ══════════ 일시정지 / 설정 모달 ══════════ -->
    <div id="pause-modal" class="absolute inset-0 bg-black/90 z-50 items-center justify-center p-4 hidden pointer-events-auto">
      <div class="bg-neutral-950 border border-neutral-900 rounded-2xl max-w-sm w-full p-6 shadow-2xl flex flex-col gap-5 text-center max-h-[92vh] overflow-y-auto">
        <div>
          <h2 class="text-2xl font-black text-red-500 uppercase tracking-widest mb-1">DREAM INTERRUPTED</h2>
          <p class="text-xs text-neutral-400">꿈이 일시적으로 정지되었습니다.</p>
        </div>

        <div class="flex flex-col gap-3.5">
          <button onclick="togglePause(event)" class="py-3 bg-red-950/40 hover:bg-red-900/50 text-red-400 hover:text-red-300 font-bold border border-red-900/50 rounded-xl transition-all active:scale-95 text-sm">
            다시 동조하기 (Resume)
          </button>

          <div class="bg-neutral-900/50 p-4 rounded-xl border border-neutral-900 text-left">
            <div class="flex justify-between items-center mb-1.5">
              <span class="text-xs text-neutral-400 font-bold">환청 볼륨 (Volume)</span>
              <span id="volume-indicator" class="text-xs text-neutral-200 ui-num">70%</span>
            </div>
            <input id="volume-slider" type="range" min="0" max="100" value="70" class="w-full h-1.5 bg-neutral-800 rounded-lg appearance-none cursor-pointer accent-red-600">
          </div>

          <div class="bg-neutral-900/50 p-4 rounded-xl border border-neutral-900 text-left">
            <div class="flex justify-between items-center mb-1.5">
              <span class="text-xs text-neutral-300 font-bold">시선 감도 (Sensitivity)</span>
              <span id="sensitivity-indicator" class="text-xs text-cyan-400 ui-num">1.0</span>
            </div>
            <input id="sensitivity-slider" type="range" min="10" max="300" value="100" class="w-full h-1.5 bg-neutral-800 rounded-lg appearance-none cursor-pointer accent-cyan-600">
          </div>

          <!-- 그래픽 품질 — 기기가 버거우면 '낮음'으로 내리면 즉시 프레임이 올라간다 -->
          <div class="bg-neutral-900/50 p-4 rounded-xl border border-neutral-900 text-left">
            <div class="flex justify-between items-center mb-2">
              <span class="text-xs text-neutral-300 font-bold">그래픽 품질 (Quality)</span>
              <span id="fps-indicator" class="text-xs text-neutral-500 ui-num">-- FPS</span>
            </div>
            <div class="grid grid-cols-3 gap-2" id="quality-buttons">
              <button data-q="low" class="quality-btn py-2 text-xs font-bold rounded-lg border transition-all active:scale-95">낮음</button>
              <button data-q="mid" class="quality-btn py-2 text-xs font-bold rounded-lg border transition-all active:scale-95">보통</button>
              <button data-q="high" class="quality-btn py-2 text-xs font-bold rounded-lg border transition-all active:scale-95">높음</button>
            </div>
            <p class="text-[10px] text-neutral-600 mt-2">프레임이 낮으면 품질을 내리십시오. 화면 선명도만 달라지고, 게임 내용은 동일합니다.</p>
          </div>

          <button onclick="confirmQuit(event)" class="py-2.5 bg-neutral-900 hover:bg-neutral-800 text-neutral-400 hover:text-neutral-200 border border-neutral-800 rounded-xl transition-all text-xs">
            기억 재시작 (Restart)
          </button>
        </div>

        <div id="quit-confirm-box" class="border-t border-neutral-900 pt-3 hidden">
          <p class="text-xs text-red-400 font-bold mb-3">경고: 현재 진행도가 영구 삭제됩니다. 처음부터 다시 잠수할까요?</p>
          <div class="flex gap-2">
            <button onclick="triggerSoftReset(event)" class="flex-1 py-2 bg-red-600 hover:bg-red-700 text-white text-xs font-bold rounded-lg transition-colors">예 (재시동)</button>
            <button onclick="cancelQuit(event)" class="flex-1 py-2 bg-neutral-800 text-neutral-400 text-xs font-bold rounded-lg transition-colors">아니오</button>
          </div>
        </div>
      </div>
    </div>

    <!-- ══════════ 엔딩 화면 ══════════ -->
    <div id="ending-screen" class="absolute inset-0 bg-black z-[70] flex-col items-center justify-center p-5 text-center select-none hidden pointer-events-auto overflow-y-auto">
      <div class="max-w-md w-full space-y-5 my-auto mx-auto">
        <div class="space-y-1">
          <p class="text-red-500 text-xs font-bold tracking-[0.25em] uppercase">Dream Record — Final Dive</p>
          <h2 id="ending-title" class="text-3xl font-black text-white uppercase tracking-widest">엔딩</h2>
          <p id="ending-subtitle" class="text-xs text-neutral-500 font-bold"></p>
        </div>

        <div class="p-6 bg-neutral-950 border border-neutral-900 rounded-xl text-left text-sm text-neutral-300 leading-relaxed space-y-3" id="ending-description"></div>

        <div class="flex justify-center gap-5 text-xs text-neutral-500">
          <span>기억 <span id="ending-items" class="text-cyan-400 font-bold">0/4</span></span>
          <span>기록 열람 <span id="ending-notes" class="text-amber-400 font-bold">0/3</span></span>
          <span>도달 <span id="ending-floor" class="text-red-400 font-bold">B10F</span></span>
        </div>

        <button onclick="triggerSoftReset(event)" class="w-full py-3.5 bg-neutral-900 hover:bg-neutral-800 text-neutral-300 hover:text-white border border-neutral-800 text-sm font-bold tracking-widest rounded-xl transition-all cursor-pointer">
          안전지대로 환원 (RE-DIVE)
        </button>
      </div>
    </div>
  </div>

  <script>
    // ════════════════════════════════════════════
    // 0. 유틸 & 환경 감지
    // ════════════════════════════════════════════
    const $ = (id) => document.getElementById(id);
    const clamp = (v, a, b) => Math.max(a, Math.min(b, v));
    const rand = (a, b) => a + Math.random() * (b - a);
    const IS_TOUCH = ('ontouchstart' in window) || (window.matchMedia && matchMedia('(pointer: coarse)').matches);
    if (!IS_TOUCH) document.body.classList.add('no-touch');

    // 설정은 재시작해도 유지
    const settings = { volume: 0.7, sensitivity: 1.0 };

    // ════ 성능 설정 (v1.2.0) ════
    // 렌더 해상도와 레이캐스트 주기를 한곳에서 통제한다.
    // 프레임을 가장 크게 좌우하는 건 '실제로 칠하는 픽셀 수'이므로,
    // 품질 조절은 픽셀비(렌더 해상도 배율) 하나로 일원화한다.
    // 셰이딩 비용 자체는 라이트 수 감축(15 → 7)과 그림자 제거로 이미 내려갔다.
    const QUALITY = {
      low:  { pixelRatio: 0.7, raycastEvery: 4 },
      mid:  { pixelRatio: 1.0, raycastEvery: 3 },
      high: { pixelRatio: 1.6, raycastEvery: 2 }
    };
    // 터치 기기는 대개 GPU가 약하면서 DPR만 높다 → 기본값을 한 단계 낮게 잡는다
    const PERF = Object.assign({ level: IS_TOUCH ? 'low' : 'mid' }, QUALITY[IS_TOUCH ? 'low' : 'mid']);

    // 손전등 기본 밝기 (v1.2.1: 기존 2.6~2.7의 약 25% 수준으로 낮춰 어둠을 되살림)
    const FLASH_ON = 0.68;

    function applyQuality(level) {
      const q = QUALITY[level];
      if (!q) return;
      PERF.level = level;
      PERF.pixelRatio = q.pixelRatio;
      PERF.raycastEvery = q.raycastEvery;
      if (renderer) {
        renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, PERF.pixelRatio));
        renderer.setSize(window.innerWidth, window.innerHeight);
      }
      document.querySelectorAll('.quality-btn').forEach((b) => {
        const on = b.getAttribute('data-q') === level;
        b.className = 'quality-btn py-2 text-xs font-bold rounded-lg border transition-all active:scale-95 ' +
          (on ? 'bg-cyan-950/50 border-cyan-800 text-cyan-300' : 'bg-neutral-900 border-neutral-800 text-neutral-500 hover:text-neutral-300');
      });
    }

    // ════════════════════════════════════════════
    // 1. 게임 상태 (재시작 시 통째로 재생성)
    // ════════════════════════════════════════════
    function createState() {
      return {
        phase: 'title',            // title | playing | ending
        loopCount: 1,              // B1F ~ B9F (B10F 도달 시 엔딩)
        loopTime: 0,
        transitioning: false,
        hr: { current: 72, target: 72, base: 72, shown: 72 },
        inventory: { glasses: false, clock: false, diary: false, band: false },
        notesRead: { corridor: false, roomB: false, roomC: false },
        roomsSeen: { roomA: false, roomB: false, roomC: false },  // 이번 층에서 확인한 방
        roomHintShown: false,      // "방도 살펴라" 안내 (런 1회)
        player: {
          x: 0, y: 1.6, z: 14,
          rotX: 0, rotY: 0,
          crouched: false, sprinting: false,
          dead: false, inLocker: false,
          room: 'corridor',
          stepDist: 0
        },
        puzzle: { t1: 42, t2: 60, v1: 10, v2: 90, solved: false },
        keypad: { input: '', solved: false },
        // zone: 'corridor' | 'roomA' | 'roomB' | 'roomC'   kind: 'static' | 'event'
        anomaly: { active: false, id: '', zone: 'corridor', kind: 'static', doorIdx: -1, t: 0, eventAt: 0, eventFired: false },
        stalker: { active: false, x: 0, z: -14, mode: 'chase', lingerT: 0, soundT: 0, doorWaitT: 0, reveal: false, revealT: 0 },
        ambient: { at: 999, kind: '', fired: true },
        flags: {
          mirrorDone: false,       // 거울 사건 (런 1회, 일기장 낙하 — 이상현상 아님)
          mannequinAway: false     // 루프 내 마네킹 시선 플래그
        },
        walkby: { on: false, t: 0 },
        blackout: { phase: 0, t: 0 },
        peek: { on: false, t: 0 },  // 갑툭튀(그것의 순간 출현) — 이상현상 이벤트
        knock: { on: false, t: 0, doorIdx: -1 }  // 문 두드림 진동 (evtKnock)
      };
    }
    let state = createState();

    // ════════════════════════════════════════════
    // 2. WEB AUDIO 신디사이저 (마스터 게인 일원화)
    // ════════════════════════════════════════════
    let audioCtx = null, masterGain = null, droneOsc = null, droneGain = null;
    let noiseBuffer = null;
    let heartTimer = null;

    function initAudio() {
      if (audioCtx) { audioCtx.resume && audioCtx.resume().catch(() => {}); return; }
      try {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        masterGain = audioCtx.createGain();
        masterGain.gain.value = settings.volume;
        masterGain.connect(audioCtx.destination);

        // 저역 드론 (배경 환청)
        droneOsc = audioCtx.createOscillator();
        droneGain = audioCtx.createGain();
        droneOsc.type = 'sawtooth';
        droneOsc.frequency.value = 38;
        const lowFilter = audioCtx.createBiquadFilter();
        lowFilter.type = 'lowpass';
        lowFilter.frequency.value = 100;
        droneGain.gain.value = 0.04;
        droneOsc.connect(lowFilter); lowFilter.connect(droneGain); droneGain.connect(masterGain);
        droneOsc.start();

        // 화이트노이즈 버퍼 (속삭임/노크/스태틱)
        const len = audioCtx.sampleRate * 2;
        noiseBuffer = audioCtx.createBuffer(1, len, audioCtx.sampleRate);
        const data = noiseBuffer.getChannelData(0);
        for (let i = 0; i < len; i++) data[i] = Math.random() * 2 - 1;

        startHeartLoop();
      } catch (e) { console.error('Audio init failed:', e); }
    }

    function setVolume(v) {
      settings.volume = v;
      if (masterGain && audioCtx) masterGain.gain.setTargetAtTime(v, audioCtx.currentTime, 0.05);
    }

    function playSynth(freq, duration, type, gainVal, slideTo) {
      if (!audioCtx) return;
      try {
        const osc = audioCtx.createOscillator();
        const g = audioCtx.createGain();
        osc.type = type || 'sine';
        osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
        if (slideTo) osc.frequency.exponentialRampToValueAtTime(Math.max(1, slideTo), audioCtx.currentTime + duration);
        g.gain.setValueAtTime(Math.max(0.0001, gainVal || 0.1), audioCtx.currentTime);
        g.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);
        osc.connect(g); g.connect(masterGain);
        osc.start(); osc.stop(audioCtx.currentTime + duration + 0.05);
      } catch (e) {}
    }

    function playNoise(duration, filterType, filterFreq, gainVal) {
      if (!audioCtx || !noiseBuffer) return;
      try {
        const src = audioCtx.createBufferSource();
        src.buffer = noiseBuffer; src.loop = true;
        const f = audioCtx.createBiquadFilter();
        f.type = filterType; f.frequency.value = filterFreq; f.Q.value = 2.5;
        const g = audioCtx.createGain();
        g.gain.setValueAtTime(0.0001, audioCtx.currentTime);
        g.gain.linearRampToValueAtTime(Math.max(0.0001, gainVal), audioCtx.currentTime + duration * 0.25);
        g.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);
        src.connect(f); f.connect(g); g.connect(masterGain);
        src.start(); src.stop(audioCtx.currentTime + duration + 0.05);
      } catch (e) {}
    }

    function playFootstep() {
      const pitch = state.player.crouched ? 42 : 55;
      const vol = state.player.crouched ? 0.02 : 0.055;
      playSynth(pitch + Math.random() * 6, 0.11, 'triangle', vol);
    }
    function playCreak() { playSynth(180 + Math.random() * 120, 0.3, 'sawtooth', 0.03, 90); }
    function playChime() { playSynth(523.25, 0.35, 'sine', 0.16); playSynth(659.25, 0.5, 'sine', 0.12); playSynth(783.99, 0.65, 'sine', 0.08); }
    function playBuzz() { playSynth(90, 0.3, 'sawtooth', 0.12); playSynth(85, 0.3, 'square', 0.06); }
    function playScareSound() {
      for (let i = 0; i < 4; i++) {
        playSynth(40 + Math.random() * 80, 1.4, 'sawtooth', 0.22);
        playSynth(500 + Math.random() * 700, 0.5, 'triangle', 0.1);
      }
      playNoise(0.8, 'highpass', 1500, 0.1);
    }
    function playWhisper() { playNoise(1.6, 'bandpass', 850 + Math.random() * 400, 0.05); playNoise(1.9, 'bandpass', 1400, 0.03); }
    function playKnock(n) {
      n = n || 3;
      for (let i = 0; i < n; i++) {
        setTimeout(() => { playNoise(0.09, 'lowpass', 180, 0.14); playSynth(60, 0.1, 'sine', 0.1); }, i * 380);
      }
    }
    function playStatic() { playNoise(0.4, 'highpass', 2500, 0.07); }
    function playDroneBend() {
      if (!audioCtx || !droneOsc) return;
      try {
        const t = audioCtx.currentTime;
        droneOsc.frequency.cancelScheduledValues(t);
        droneOsc.frequency.setValueAtTime(38, t);
        droneOsc.frequency.linearRampToValueAtTime(30, t + 1.2);
        droneOsc.frequency.linearRampToValueAtTime(38, t + 2.6);
      } catch (e) {}
    }
    function playChaseHorn() { playSynth(72, 0.6, 'sawtooth', 0.14, 60); playSynth(48, 0.7, 'square', 0.08); }

    // 옷장 철문 — 닫힐 땐 경첩이 끌리고 걸쇠가 '탁' 물린다 / 열릴 땐 그 역순
    function playLockerDoor(closing) {
      if (closing) {
        playSynth(210, 0.28, 'sawtooth', 0.045, 120);          // 경첩 끌림
        setTimeout(() => { playNoise(0.06, 'lowpass', 260, 0.16); playSynth(72, 0.09, 'square', 0.09); }, 230); // 걸쇠
        setTimeout(() => playSynth(48, 0.5, 'sine', 0.05), 300);  // 갇힌 저역 여운
      } else {
        playNoise(0.05, 'lowpass', 300, 0.13);                  // 걸쇠 풀림
        setTimeout(() => playSynth(130, 0.3, 'sawtooth', 0.05, 240), 60);
      }
    }

    // 심박: 자가 연쇄 타이머 (리셋 불필요, 항상 현재 BPM 참조)
    function startHeartLoop() {
      if (heartTimer) return;
      const step = () => {
        const bpm = clamp(state.hr.current, 45, 190);
        heartTimer = setTimeout(step, 60000 / bpm);
        if (!audioCtx || state.phase !== 'playing' || isPausedAny() || state.player.dead) return;
        const k = state.hr.current / 72;
        playSynth(55, 0.07, 'sine', 0.12 * k);
        setTimeout(() => playSynth(45, 0.1, 'sine', 0.085 * k), 135);
      };
      step();
    }

    function bumpHR(target) { state.hr.target = Math.max(state.hr.target, target); }

    // ════════════════════════════════════════════
    // 3. 프로시저럴 텍스처
    // ════════════════════════════════════════════
    const Textures = {};
    function makeTex(w, h, draw) {
      const c = document.createElement('canvas');
      c.width = w; c.height = h;
      draw(c.getContext('2d'), w, h);
      return new THREE.CanvasTexture(c);
    }

    function setupProceduralAssets() {
      Textures.wall = makeTex(512, 512, (ctx) => {
        ctx.fillStyle = '#1a1a1c'; ctx.fillRect(0, 0, 512, 512);
        ctx.strokeStyle = 'rgba(0,0,0,0.5)'; ctx.lineWidth = 1;
        for (let i = 0; i < 512; i += 64) { ctx.beginPath(); ctx.moveTo(i, 0); ctx.lineTo(i, 512); ctx.stroke(); }
        ctx.strokeStyle = 'rgba(0,0,0,0.3)';
        for (let i = 0; i < 512; i += 128) { ctx.beginPath(); ctx.moveTo(0, i); ctx.lineTo(512, i); ctx.stroke(); }
        for (let i = 0; i < 900; i++) {
          ctx.fillStyle = 'rgba(0,0,0,' + (Math.random() * 0.12) + ')';
          ctx.fillRect(Math.random() * 512, Math.random() * 512, 3, 3);
        }
        // 하단 걸레받이
        ctx.fillStyle = '#0c0c0e'; ctx.fillRect(0, 470, 512, 42);
      });
      Textures.wall.wrapS = THREE.RepeatWrapping; Textures.wall.wrapT = THREE.RepeatWrapping;

      Textures.floor = makeTex(256, 256, (ctx) => {
        ctx.fillStyle = '#232326'; ctx.fillRect(0, 0, 256, 256);
        ctx.strokeStyle = '#38383d'; ctx.lineWidth = 2;
        for (let i = 0; i < 256; i += 32) {
          ctx.beginPath(); ctx.moveTo(i, 0); ctx.lineTo(i, 256); ctx.stroke();
          ctx.beginPath(); ctx.moveTo(0, i); ctx.lineTo(256, i); ctx.stroke();
        }
        for (let i = 0; i < 250; i++) {
          ctx.fillStyle = 'rgba(0,0,0,' + (Math.random() * 0.18) + ')';
          ctx.fillRect(Math.random() * 256, Math.random() * 256, 4, 4);
        }
      });
      Textures.floor.wrapS = THREE.RepeatWrapping; Textures.floor.wrapT = THREE.RepeatWrapping;

      const plate = (letter, mirrored) => makeTex(128, 80, (ctx, w, h) => {
        ctx.fillStyle = '#2a2013'; ctx.fillRect(0, 0, w, h);
        ctx.strokeStyle = '#8a6a30'; ctx.lineWidth = 4; ctx.strokeRect(4, 4, w - 8, h - 8);
        ctx.font = '900 46px monospace'; ctx.fillStyle = '#d8b45a';
        ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
        if (mirrored) { ctx.save(); ctx.translate(w / 2, h / 2); ctx.scale(-1, 1); ctx.fillText(letter, 0, 2); ctx.restore(); }
        else ctx.fillText(letter, w / 2, h / 2 + 2);
      });
      Textures.plateA = plate('A', false); Textures.plateB = plate('B', false); Textures.plateC = plate('C', false);
      Textures.plateAm = plate('A', true); Textures.plateBm = plate('B', true); Textures.plateCm = plate('C', true);

      const gateSign = (label, arrow, color) => makeTex(512, 128, (ctx, w, h) => {
        ctx.fillStyle = '#050505'; ctx.fillRect(0, 0, w, h);
        ctx.strokeStyle = color; ctx.lineWidth = 6; ctx.strokeRect(6, 6, w - 12, h - 12);
        ctx.font = '900 58px monospace'; ctx.fillStyle = color;
        ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
        ctx.shadowColor = color; ctx.shadowBlur = 22;
        ctx.fillText(arrow + ' ' + label + ' ' + arrow, w / 2, h / 2 + 2);
      });
      Textures.signDeep = gateSign('심층 DEEPER', '▼', '#22d3ee');
      Textures.signReturn = gateSign('회귀 RETURN', '▲', '#f59e0b');

      Textures.clockFace = makeTex(256, 256, (ctx, w, h) => {
        ctx.fillStyle = '#101012'; ctx.fillRect(0, 0, w, h);
        ctx.beginPath(); ctx.arc(128, 128, 110, 0, Math.PI * 2);
        ctx.fillStyle = '#e8e4d8'; ctx.fill();
        ctx.lineWidth = 8; ctx.strokeStyle = '#3a3a3e'; ctx.stroke();
        ctx.strokeStyle = '#222'; ctx.lineWidth = 4;
        for (let i = 0; i < 12; i++) {
          const a = i * Math.PI / 6;
          ctx.beginPath();
          ctx.moveTo(128 + Math.sin(a) * 92, 128 - Math.cos(a) * 92);
          ctx.lineTo(128 + Math.sin(a) * 104, 128 - Math.cos(a) * 104);
          ctx.stroke();
        }
        // 4시 44분 고정
        const hourA = ((4 + 44 / 60) / 12) * Math.PI * 2;
        const minA = (44 / 60) * Math.PI * 2;
        ctx.strokeStyle = '#151515'; ctx.lineCap = 'round';
        ctx.lineWidth = 9;
        ctx.beginPath(); ctx.moveTo(128, 128); ctx.lineTo(128 + Math.sin(hourA) * 52, 128 - Math.cos(hourA) * 52); ctx.stroke();
        ctx.lineWidth = 6;
        ctx.beginPath(); ctx.moveTo(128, 128); ctx.lineTo(128 + Math.sin(minA) * 82, 128 - Math.cos(minA) * 82); ctx.stroke();
        // 유리 균열
        ctx.strokeStyle = 'rgba(40,40,40,0.55)'; ctx.lineWidth = 2;
        ctx.beginPath(); ctx.moveTo(60, 70); ctx.lineTo(120, 118); ctx.lineTo(150, 100); ctx.stroke();
      });

      Textures.poster = makeTex(256, 384, (ctx, w, h) => {
        ctx.fillStyle = '#c9c3b2'; ctx.fillRect(0, 0, w, h);
        ctx.fillStyle = '#8f8a7a'; ctx.fillRect(0, 0, w, 64);
        ctx.font = '900 34px sans-serif'; ctx.fillStyle = '#2a2a2a';
        ctx.textAlign = 'center';
        ctx.fillText('제 4 병 동', w / 2, 44);
        ctx.font = 'bold 20px sans-serif'; ctx.fillStyle = '#3d3a32';
        ctx.fillText('면회 시간 엄수', w / 2, 120);
        ctx.fillText('중환자 구역', w / 2, 160);
        ctx.fillText('관계자 외 출입금지', w / 2, 200);
        ctx.font = '16px sans-serif'; ctx.fillStyle = '#6b675c';
        ctx.fillText('AM 04:00 - 05:00', w / 2, 260);
        ctx.strokeStyle = 'rgba(0,0,0,0.25)'; ctx.strokeRect(8, 8, w - 16, h - 16);
        for (let i = 0; i < 60; i++) {
          ctx.fillStyle = 'rgba(90,80,60,' + Math.random() * 0.14 + ')';
          ctx.fillRect(Math.random() * w, Math.random() * h, 6, 6);
        }
      });

      Textures.memo = makeTex(128, 128, (ctx, w, h) => {
        ctx.fillStyle = '#d8d2bf'; ctx.fillRect(0, 0, w, h);
        ctx.strokeStyle = '#7a7462'; ctx.lineWidth = 2;
        for (let y = 28; y < h - 10; y += 18) { ctx.beginPath(); ctx.moveTo(14, y); ctx.lineTo(w - 14, y); ctx.stroke(); }
        ctx.fillStyle = '#3a352a'; ctx.font = 'bold 15px sans-serif';
        ctx.fillText('메모', 14, 20);
      });

      // 초상화 — 정상(흐릿한 인물) / 이상(정면 응시 + 검은 눈)
      const portraitBase = (wrong) => makeTex(160, 208, (ctx, w, h) => {
        ctx.fillStyle = '#0e0d0c'; ctx.fillRect(0, 0, w, h);
        ctx.strokeStyle = '#5a4a2e'; ctx.lineWidth = 8; ctx.strokeRect(6, 6, w - 12, h - 12);
        const g = ctx.createLinearGradient(0, 20, 0, h);
        g.addColorStop(0, wrong ? '#3a2a2a' : '#2a2a2e'); g.addColorStop(1, '#141416');
        ctx.fillStyle = g; ctx.fillRect(14, 14, w - 28, h - 28);
        // 어깨/머리 실루엣
        ctx.fillStyle = wrong ? '#242024' : '#3a3a40';
        ctx.beginPath(); ctx.ellipse(w / 2, h * 0.42, 34, 40, 0, 0, Math.PI * 2); ctx.fill();
        ctx.fillRect(w / 2 - 52, h * 0.68, 104, h);
        if (wrong) {
          // 텅 빈 검은 눈 + 벌어진 입
          ctx.fillStyle = '#000';
          ctx.beginPath(); ctx.ellipse(w / 2 - 14, h * 0.4, 6, 9, 0, 0, Math.PI * 2); ctx.fill();
          ctx.beginPath(); ctx.ellipse(w / 2 + 14, h * 0.4, 6, 9, 0, 0, Math.PI * 2); ctx.fill();
          ctx.fillRect(w / 2 - 8, h * 0.52, 16, 4);
        }
      });
      Textures.portrait = portraitBase(false);
      Textures.portraitWrong = portraitBase(true);

      const exitSign = (color, arrow) => makeTex(160, 64, (ctx, w, h) => {
        ctx.fillStyle = '#04160a'; ctx.fillRect(0, 0, w, h);
        ctx.fillStyle = color; ctx.font = '900 34px sans-serif'; ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
        ctx.shadowColor = color; ctx.shadowBlur = 16;
        ctx.fillText(arrow + ' EXIT', w / 2, h / 2 + 2);
      });
      Textures.exitGreen = exitSign('#4ade80', '→');
      Textures.exitRed = exitSign('#ff3030', '✕');

      Textures.bloodTrail = makeTex(64, 256, (ctx, w, h) => {
        ctx.clearRect(0, 0, w, h);
        ctx.fillStyle = 'rgba(0,0,0,0)'; ctx.fillRect(0, 0, w, h);
        for (let i = 0; i < 22; i++) {
          const y = (i / 22) * h;
          const r = 6 + Math.random() * 12;
          ctx.fillStyle = 'rgba(70,8,8,' + (0.35 + Math.random() * 0.4) + ')';
          ctx.beginPath(); ctx.arc(w / 2 + (Math.random() - 0.5) * 22, y, r, 0, Math.PI * 2); ctx.fill();
        }
      });

      Textures.clockWrong = makeTex(256, 256, (ctx, w, h) => {
        ctx.fillStyle = '#101012'; ctx.fillRect(0, 0, w, h);
        ctx.beginPath(); ctx.arc(128, 128, 110, 0, Math.PI * 2);
        ctx.fillStyle = '#e8e4d8'; ctx.fill();
        ctx.lineWidth = 8; ctx.strokeStyle = '#3a3a3e'; ctx.stroke();
        ctx.strokeStyle = '#222'; ctx.lineWidth = 4;
        for (let i = 0; i < 12; i++) {
          const a = i * Math.PI / 6;
          ctx.beginPath();
          ctx.moveTo(128 + Math.sin(a) * 92, 128 - Math.cos(a) * 92);
          ctx.lineTo(128 + Math.sin(a) * 104, 128 - Math.cos(a) * 104);
          ctx.stroke();
        }
        // 모든 바늘이 12를 향해 겹침 (잘못된 시각)
        ctx.strokeStyle = '#8f1010'; ctx.lineCap = 'round';
        ctx.lineWidth = 9; ctx.beginPath(); ctx.moveTo(128, 128); ctx.lineTo(128, 60); ctx.stroke();
        ctx.lineWidth = 6; ctx.beginPath(); ctx.moveTo(128, 128); ctx.lineTo(128, 44); ctx.stroke();
      });

      const monitorTex = (line1, line2, line3, color) => makeTex(256, 256, (ctx, w, h) => {
        ctx.fillStyle = '#020617'; ctx.fillRect(0, 0, w, h);
        ctx.strokeStyle = color; ctx.lineWidth = 3; ctx.strokeRect(10, 10, w - 20, h - 20);
        ctx.font = 'bold 19px monospace'; ctx.fillStyle = color;
        ctx.fillText(line1, 28, 66);
        ctx.fillText(line2, 28, 122);
        ctx.font = '13px monospace';
        ctx.fillText(line3, 28, 182);
        for (let i = 0; i < 40; i++) {
          ctx.fillStyle = 'rgba(255,255,255,' + Math.random() * 0.05 + ')';
          ctx.fillRect(Math.random() * w, Math.random() * h, w, 1);
        }
      });
      Textures.monitorIdle = monitorTex('MEM TUNE OS v2.0', 'SIGNAL LOSS', 'PRESS [E] TO SYNC', '#06b6d4');
      Textures.monitorDone = monitorTex('MEM TUNE OS v2.0', 'SYNC COMPLETE', 'MEMORY RESTORED — 04:44', '#4ade80');

      Textures.mirrorNormal = makeTex(128, 256, (ctx, w, h) => {
        ctx.fillStyle = '#3d3d42'; ctx.fillRect(0, 0, w, h);
        const grad = ctx.createLinearGradient(0, 0, w, h);
        grad.addColorStop(0, '#22262c'); grad.addColorStop(0.5, '#31363e'); grad.addColorStop(1, '#1b1e24');
        ctx.fillStyle = grad; ctx.fillRect(8, 8, w - 16, h - 16);
        ctx.strokeStyle = 'rgba(255,255,255,0.14)'; ctx.lineWidth = 3;
        ctx.beginPath(); ctx.moveTo(24, 30); ctx.lineTo(46, 90); ctx.stroke();
      });
      Textures.mirrorBlood = makeTex(128, 256, (ctx, w, h) => {
        ctx.fillStyle = '#3d3d42'; ctx.fillRect(0, 0, w, h);
        const grad = ctx.createLinearGradient(0, 0, w, h);
        grad.addColorStop(0, '#2a1214'); grad.addColorStop(0.5, '#451116'); grad.addColorStop(1, '#1c0a0c');
        ctx.fillStyle = grad; ctx.fillRect(8, 8, w - 16, h - 16);
        ctx.strokeStyle = 'rgba(255,60,60,0.5)'; ctx.lineWidth = 4;
        for (let i = 0; i < 7; i++) {
          ctx.beginPath();
          ctx.moveTo(64, 128);
          ctx.lineTo(64 + Math.cos(i * 0.9) * 55, 128 + Math.sin(i * 0.9) * 110);
          ctx.stroke();
        }
        ctx.font = 'bold 26px sans-serif'; ctx.fillStyle = 'rgba(255,80,80,0.85)';
        ctx.save(); ctx.translate(64, 210); ctx.scale(-1, 1);
        ctx.textAlign = 'center'; ctx.fillText('살려줘', 0, 0); ctx.restore();
      });

      // ── v1.1.0 신규 텍스처 ──

      // 거울 — 뒤에 선 검은 형체 (Room C 이상현상)
      Textures.mirrorFigure = makeTex(128, 256, (ctx, w, h) => {
        ctx.fillStyle = '#3d3d42'; ctx.fillRect(0, 0, w, h);
        const grad = ctx.createLinearGradient(0, 0, w, h);
        grad.addColorStop(0, '#22262c'); grad.addColorStop(0.5, '#2b3037'); grad.addColorStop(1, '#191c21');
        ctx.fillStyle = grad; ctx.fillRect(8, 8, w - 16, h - 16);
        // 어깨 위로 솟은 실루엣 — 관찰자 뒤에 서 있다
        ctx.fillStyle = 'rgba(6,6,8,0.9)';
        ctx.beginPath(); ctx.ellipse(64, 96, 22, 27, 0, 0, Math.PI * 2); ctx.fill();
        ctx.fillRect(30, 120, 68, 140);
        ctx.fillStyle = '#c81414';
        ctx.beginPath(); ctx.arc(57, 94, 3.6, 0, Math.PI * 2); ctx.fill();
        ctx.strokeStyle = 'rgba(255,255,255,0.1)'; ctx.lineWidth = 3;
        ctx.beginPath(); ctx.moveTo(24, 30); ctx.lineTo(46, 90); ctx.stroke();
      });

      // 거울 — 뿌옇게 김이 서리고 글자가 떠오름 (Room C 이상현상)
      Textures.mirrorFog = makeTex(128, 256, (ctx, w, h) => {
        ctx.fillStyle = '#3d3d42'; ctx.fillRect(0, 0, w, h);
        ctx.fillStyle = '#7d848c'; ctx.fillRect(8, 8, w - 16, h - 16);
        for (let i = 0; i < 200; i++) {
          ctx.fillStyle = 'rgba(255,255,255,' + Math.random() * 0.09 + ')';
          ctx.beginPath(); ctx.arc(Math.random() * w, Math.random() * h, Math.random() * 9, 0, Math.PI * 2); ctx.fill();
        }
        ctx.font = 'bold 22px sans-serif'; ctx.fillStyle = 'rgba(40,44,50,0.9)';
        ctx.textAlign = 'center';
        ctx.fillText('돌아보지', 64, 120);
        ctx.fillText('마', 64, 150);
      });

      // 벽에 번진 손자국 (회랑 이상현상)
      Textures.handPrints = makeTex(256, 192, (ctx, w, h) => {
        ctx.clearRect(0, 0, w, h);
        const hand = (cx, cy, s, a) => {
          ctx.save(); ctx.translate(cx, cy); ctx.rotate(a); ctx.scale(s, s);
          ctx.fillStyle = 'rgba(58,10,10,0.62)';
          ctx.beginPath(); ctx.ellipse(0, 8, 12, 15, 0, 0, Math.PI * 2); ctx.fill();
          for (let f = 0; f < 4; f++) {
            ctx.beginPath();
            ctx.ellipse(-9 + f * 6, -10, 2.7, 10, (f - 1.5) * 0.16, 0, Math.PI * 2); ctx.fill();
          }
          ctx.beginPath(); ctx.ellipse(-14, 6, 3, 7.5, -0.7, 0, Math.PI * 2); ctx.fill();
          ctx.restore();
        };
        for (let i = 0; i < 9; i++) hand(24 + Math.random() * 210, 24 + Math.random() * 150, 0.75 + Math.random() * 0.6, (Math.random() - 0.5) * 1.5);
      });

      // 달력 — 정상 / 이상 (Room B)
      const calendarTex = (wrong) => makeTex(192, 192, (ctx, w, h) => {
        ctx.fillStyle = '#d6d1c2'; ctx.fillRect(0, 0, w, h);
        ctx.fillStyle = wrong ? '#5a1414' : '#3a4550'; ctx.fillRect(0, 0, w, 38);
        ctx.font = 'bold 20px monospace'; ctx.fillStyle = '#e8e4d8'; ctx.textAlign = 'center';
        ctx.fillText(wrong ? '44월' : '4월', w / 2, 26);
        ctx.font = 'bold 14px monospace'; ctx.fillStyle = '#3a352a';
        for (let r = 0; r < 5; r++) {
          for (let c = 0; c < 7; c++) {
            const d = r * 7 + c + 1;
            if (d > 30) continue;
            ctx.fillText(wrong ? '44' : String(d), 16 + c * 27, 62 + r * 26);
          }
        }
        ctx.strokeStyle = wrong ? '#8f1010' : '#8f1010'; ctx.lineWidth = 3;
        ctx.beginPath(); ctx.arc(16 + 3 * 27, 62 + 2 * 26 - 4, 13, 0, Math.PI * 2); ctx.stroke();
      });
      Textures.calendar = calendarTex(false);
      Textures.calendarWrong = calendarTex(true);

      // 모니터 — 이상 문구 (Room B)
      Textures.monitorWrong = makeTex(256, 256, (ctx, w, h) => {
        ctx.fillStyle = '#160404'; ctx.fillRect(0, 0, w, h);
        ctx.strokeStyle = '#ef4444'; ctx.lineWidth = 3; ctx.strokeRect(10, 10, w - 20, h - 20);
        ctx.font = 'bold 19px monospace'; ctx.fillStyle = '#ef4444';
        ctx.fillText('MEM TUNE OS v2.0', 28, 66);
        ctx.fillText('SUBJECT: 당신', 28, 122);
        ctx.font = '13px monospace';
        ctx.fillText('WHO IS WATCHING WHO', 28, 182);
        for (let i = 0; i < 60; i++) {
          ctx.fillStyle = 'rgba(255,60,60,' + Math.random() * 0.08 + ')';
          ctx.fillRect(Math.random() * w, Math.random() * h, w, 1);
        }
      });

      // 병상 시트 — 정상(빈 침대) / 이상(사람 형상이 눌린 자국)
      const sheetTex = (occupied) => makeTex(128, 256, (ctx, w, h) => {
        ctx.fillStyle = '#b9b5a9'; ctx.fillRect(0, 0, w, h);
        ctx.strokeStyle = 'rgba(0,0,0,0.12)'; ctx.lineWidth = 2;
        for (let i = 20; i < h; i += 34) { ctx.beginPath(); ctx.moveTo(0, i); ctx.lineTo(w, i); ctx.stroke(); }
        if (occupied) {
          ctx.fillStyle = 'rgba(70,68,62,0.55)';
          ctx.beginPath(); ctx.ellipse(64, 44, 21, 25, 0, 0, Math.PI * 2); ctx.fill();
          ctx.beginPath(); ctx.ellipse(64, 150, 34, 88, 0, 0, Math.PI * 2); ctx.fill();
          ctx.fillStyle = 'rgba(60,10,10,0.35)';
          ctx.beginPath(); ctx.ellipse(64, 44, 12, 14, 0, 0, Math.PI * 2); ctx.fill();
        }
      });
      Textures.sheetEmpty = sheetTex(false);
      Textures.sheetOccupied = sheetTex(true);
    }

    // ════════════════════════════════════════════
    // 4. THREE.JS 월드 (1회 구축, 재시작 시 상태만 복원)
    // ════════════════════════════════════════════
    let scene = null, camera = null, renderer = null, flashLight = null;
    let worldBuilt = false;
    let lockerMesh = null, stalkerMesh = null, walkbyMesh = null, blackoutEyes = null;
    let corridorMannequin = null, roomMannequin = null, roomMannequinHome = new THREE.Vector3(-6.6, 0.85, 3.6);
    let mirrorMesh = null, monitorMesh = null, cabinetMesh = null, drawerMesh = null;
    let itemGlasses = null, itemDiaryPage = null;
    let doorDefs = [];            // {group, panel, plate, room, letter, side}
    let corridorLamps = [];       // {mesh, light(null 가능), baseColor, baseIntensity}
    let lampsDirty = true;        // 조명 상태를 다시 써야 하는가 (매 프레임 갱신 방지)
    // (방 조명은 아래 roomLight 단일 PointLight로 통합됨 — v1.2.0)
    let floaters = [];            // 둥실거리는 아이템 메시
    let interactables = [];       // 레이캐스트 대상
    let blockers = [];            // 시야 차단 벽 (벽 너머 상호작용 방지)
    const props = {};             // 평상시 회랑 소품 (이상현상의 '정상 기준')
    const anomObj = {};           // 이상현상 전용 객체 (평소엔 숨김)
    const TARGET_FLOOR = 10;      // 이 층에 도달하면 엔딩 (하강 9회)

    // ── 방 좌표: 회랑에서 카메라 far(90) 밖으로 완전 격리 ──
    // v1.0.0에서는 방이 회랑 바로 옆에 있어, 단면(FrontSide) 벽 너머로 방 내부가
    // 그대로 비쳐 보이고 방 조명이 회랑까지 샜다. 문은 포털(텔레포트)이므로
    // 물리적 인접이 전혀 필요 없어, 서로 100m 이상 떨어뜨려 근본 차단한다.
    const ROOM_S = 2.2;           // 방 반폭
    const ROOMS = {
      roomA: { cx: 200, cz: 0 },
      roomB: { cx: 200, cz: 100 },
      roomC: { cx: 200, cz: 200 }
    };
    const RB = 1.9;               // 플레이어 이동 한계 (벽에서 0.3 여유)
    const ROOM_BOUNDS = {
      roomA: { x: [ROOMS.roomA.cx - RB, ROOMS.roomA.cx + RB], z: [ROOMS.roomA.cz - RB, ROOMS.roomA.cz + RB] },
      roomB: { x: [ROOMS.roomB.cx - RB, ROOMS.roomB.cx + RB], z: [ROOMS.roomB.cz - RB, ROOMS.roomB.cz + RB] },
      roomC: { x: [ROOMS.roomC.cx - RB, ROOMS.roomC.cx + RB], z: [ROOMS.roomC.cz - RB, ROOMS.roomC.cz + RB] }
    };
    // L자 회랑: 세로팔(입구, +z) → 모서리 → 가로팔(−x, 심층). 한눈에 다 안 보임.
    const HW = 1.75;                          // 통로 반폭
    const WALK = [
      { x: [-HW, HW], z: [-HW, 20] },         // 세로팔(V)
      { x: [-22, HW], z: [-HW, HW] }          // 가로팔(H)
    ];
    const CORNER = { x: 0, z: 0 };
    const GATE_RETURN_Z = 19.4;               // 세로팔 끝 = 회귀 게이트
    const GATE_DEEP_X = -21.4;                // 가로팔 끝 = 심층 게이트
    const SPAWN = { x: 0, z: 17 };
    const LOCKER_POS = { x: 1.4, z: 6 };
    function inWalk(x, z) {
      for (const r of WALK) if (x >= r.x[0] && x <= r.x[1] && z >= r.z[0] && z <= r.z[1]) return true;
      return false;
    }
    const ROOM_NAMES = {
      corridor: '중앙 회랑', roomA: '기억의 수렁 — Room A',
      roomB: '조율 연산실 — Room B', roomC: '환각의 거울방 — Room C'
    };
    // into = 방 안쪽 문 앞 / out = 회랑 쪽 문 앞
    // rotIn/rotOut = 그때 바라볼 방향(yaw). 카메라 전방은 (-sin(yaw), -cos(yaw)).
    //   yaw = 0     → −z 방향
    //   yaw = +π/2  → −x 방향
    //   yaw = −π/2  → +x 방향
    //   yaw = π     → +z 방향
    // v1.1.0은 이 값을 전혀 지정하지 않아, 문을 통과하면 이전 시선각이 그대로 남아
    // 방금 나온 문(벽)을 도로 마주보는 일이 잦았다. 나올 때는 항상 통로 안쪽을,
    // 들어갈 때는 항상 방 안쪽을 수평으로 바라보게 고정한다.
    const HALF_PI = Math.PI / 2;
    const DOOR_TELEPORT = {
      // V 좌벽 문 → 방 안에선 서쪽(−x)을 보고, 회랑에선 동쪽(+x)을 본다
      roomA: { into: [ROOMS.roomA.cx + 1.5, ROOMS.roomA.cz], rotIn: HALF_PI,  out: [-1.05, 8],   rotOut: -HALF_PI },
      // V 우벽 문 → 방 안에선 동쪽(+x), 회랑에선 서쪽(−x)
      roomB: { into: [ROOMS.roomB.cx - 1.5, ROOMS.roomB.cz], rotIn: -HALF_PI, out: [1.05, 12],   rotOut: HALF_PI },
      // H 원벽 문 → 방 안에선 서쪽(−x), 회랑에선 북쪽(+z, 회랑 안쪽)
      roomC: { into: [ROOMS.roomC.cx + 1.5, ROOMS.roomC.cz], rotIn: HALF_PI,  out: [-12, -1.05], rotOut: Math.PI }
    };

    function mkMesh(geo, mat, x, y, z) {
      const m = new THREE.Mesh(geo, mat);
      m.position.set(x, y, z);
      scene.add(m);
      return m;
    }

    function buildWorld() {
      if (worldBuilt) return;
      worldBuilt = true;

      scene = new THREE.Scene();
      scene.fog = new THREE.FogExp2(0x030303, 0.055);

      camera = new THREE.PerspectiveCamera(62, window.innerWidth / window.innerHeight, 0.1, 90);
      camera.position.set(0, 1.6, 14);

      // ════ v1.2.0 성능 개편 ════
      // v1.1.0의 렉 원인은 두 가지였다.
      //  (1) 그림자 패스: flashLight.castShadow + PCFSoftShadowMap(1024²) 때문에
      //      매 프레임 씬을 사실상 두 번 그렸다. 회랑은 원래 어두워 그림자가
      //      거의 보이지도 않았으므로, 비용만 내고 얻는 게 없었다 → 완전 제거.
      //  (2) 라이트 13개(Ambient1+Spot1+회랑8+방3)를 MeshStandardMaterial이
      //      픽셀마다 전부 계산 → 7개로 감축 (아래 buildCorridor / makeRoomShell).
      renderer = new THREE.WebGLRenderer({ canvas: $('three-canvas'), antialias: false, powerPreference: 'high-performance' });
      renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, PERF.pixelRatio));
      renderer.setSize(window.innerWidth, window.innerHeight);
      renderer.shadowMap.enabled = false;   // 그림자 패스 제거 (최대 이득)

      setupProceduralAssets();

      scene.add(new THREE.AmbientLight(0x0a0d14, 0.62));

      // v1.2.1: 손전등을 약 75% 어둡게 (2.7 → 0.68). 회랑이 지나치게 환해
      // 공포 분위기를 깎던 문제. 이제 어둠이 짙어져 무엇이 '어긋났는지' 더 긴장하며 살핀다.
      flashLight = new THREE.SpotLight(0xfff6e0, FLASH_ON, 22, Math.PI / 4.2, 0.5, 0.9);
      flashLight.castShadow = false;
      scene.add(flashLight);
      scene.add(flashLight.target);

      buildCorridor();
      buildRoomA();
      buildRoomB();
      buildRoomC();
      buildLocker();
      buildStalker();
      buildScareProps();

      window.addEventListener('resize', onWindowResize);
    }

    function buildCorridor() {
      const floorMat = () => { const t = Textures.floor.clone(); t.needsUpdate = true; t.wrapS = t.wrapT = THREE.RepeatWrapping; return t; };
      const ceilMat = new THREE.MeshStandardMaterial({ color: 0x121214, roughness: 0.9 });
      const H = 3.2;

      // ── 바닥/천장 (두 팔) ──
      const ftV = floorMat(); ftV.repeat.set(2, 11);
      const flV = mkMesh(new THREE.PlaneGeometry(2 * HW, 21.75), new THREE.MeshStandardMaterial({ map: ftV, roughness: 0.85 }), 0, 0, 9.125);
      flV.rotation.x = -Math.PI / 2; flV.receiveShadow = true;
      const ftH = floorMat(); ftH.repeat.set(12, 2);
      const flH = mkMesh(new THREE.PlaneGeometry(23.75, 2 * HW), new THREE.MeshStandardMaterial({ map: ftH, roughness: 0.85 }), -10.125, 0, 0);
      flH.rotation.x = -Math.PI / 2; flH.receiveShadow = true;
      const clV = mkMesh(new THREE.PlaneGeometry(2 * HW, 21.75), ceilMat, 0, H, 9.125); clV.rotation.x = Math.PI / 2;
      const clH = mkMesh(new THREE.PlaneGeometry(23.75, 2 * HW), ceilMat, -10.125, H, 0); clH.rotation.x = Math.PI / 2;

      const wallTex = () => { const t = Textures.wall.clone(); t.needsUpdate = true; t.wrapS = t.wrapT = THREE.RepeatWrapping; return t; };
      const mkWall = (len, cx, cz, ry, rep) => {
        const tx = wallTex(); tx.repeat.set(rep, 1);
        const w = mkMesh(new THREE.PlaneGeometry(len, H), new THREE.MeshStandardMaterial({ map: tx, roughness: 0.95 }), cx, H / 2, cz);
        w.rotation.y = ry; w.receiveShadow = true; blockers.push(w); return w;
      };
      // W1 V좌벽 (z 1.75~20), W2 V우벽 (z -1.75~20)
      mkWall(18.25, -HW, 10.875, Math.PI / 2, 9);
      mkWall(21.75, HW, 9.125, -Math.PI / 2, 11);
      // W4 H근벽 (z=1.75, x -22~-1.75), W5 H원벽 (z=-1.75, x -22~1.75)
      mkWall(20.25, -11.875, HW, Math.PI, 10);
      mkWall(23.75, -10.125, -HW, 0, 12);

      // ── 게이트 (막 + 사인) ──
      const gateMat = new THREE.MeshBasicMaterial({ color: 0x010101 });
      const gRet = mkMesh(new THREE.PlaneGeometry(2 * HW, H), gateMat, 0, H / 2, 20); gRet.rotation.y = Math.PI; blockers.push(gRet);
      const gDeep = mkMesh(new THREE.PlaneGeometry(2 * HW, H), gateMat, -22, H / 2, 0); gDeep.rotation.y = Math.PI / 2; blockers.push(gDeep);
      const signRet = mkMesh(new THREE.PlaneGeometry(2.4, 0.6), new THREE.MeshBasicMaterial({ map: Textures.signReturn, transparent: true }), 0, 2.6, 19.85); signRet.rotation.y = Math.PI;
      const signDeep = mkMesh(new THREE.PlaneGeometry(2.2, 0.55), new THREE.MeshBasicMaterial({ map: Textures.signDeep, transparent: true }), -21.85, 2.6, 0); signDeep.rotation.y = Math.PI / 2;

      // ── 천장등 (V 4기 + H 4기) ──
      // 등 '기구'는 8기 그대로 보이지만, 실제 PointLight는 격등으로 4개만 둔다.
      // 조명 없는 등에는 밝은 판(MeshBasicMaterial)만 남아 시각적으로는 8기로 보인다.
      // 라이트 8 → 4로 줄이는 것만으로 픽셀 셰이더 비용이 크게 떨어진다.
      const lampGeo = new THREE.BoxGeometry(0.85, 0.06, 0.4);
      const lampAt = (x, z, withLight) => {
        const lampMesh = mkMesh(lampGeo, new THREE.MeshBasicMaterial({ color: 0xfff0d8 }), x, H - 0.04, z);
        let pl = null;
        if (withLight) {
          pl = new THREE.PointLight(0xfff0d8, 0.95, 11); pl.position.set(x, H - 0.3, z); scene.add(pl);
        }
        corridorLamps.push({ mesh: lampMesh, light: pl, baseColor: 0xfff0d8, baseIntensity: 0.95, phase: Math.random() * 10 });
      };
      [[0, 17, true], [0, 12, false], [0, 6, true], [0, 1, false]].forEach(([x, z, L]) => lampAt(x, z, L));
      [[-4, 0, true], [-9, 0, false], [-14, 0, true], [-19, 0, false]].forEach(([x, z, L]) => lampAt(x, z, L));

      // ── 문 3개 (포털) ──
      // 벽면은 x=±1.75 / z=±1.75 평면이며 단면(FrontSide)이다.
      // v1.0.0은 문을 ±1.93(벽 '뒤')에 두어, 렌더링에서 벽에 가려 보이지 않았고
      // 레이캐스트도 벽에 먼저 맞아 방에 진입할 수조차 없었다. 벽 '앞'으로 이동한다.
      makeDoor('A', 'roomA', -1.68, 8, Math.PI / 2, Textures.plateA);   // V 좌벽
      makeDoor('B', 'roomB', 1.68, 12, -Math.PI / 2, Textures.plateB);  // V 우벽
      makeDoor('C', 'roomC', -12, -1.68, 0, Textures.plateC);           // H 원벽

      // ── 벽시계 (V 우벽) · 포스터 (H 근벽) · 스폰 메모 (V 우벽) ──
      const clock = mkMesh(new THREE.PlaneGeometry(0.55, 0.55), new THREE.MeshStandardMaterial({ map: Textures.clockFace, roughness: 0.5 }), 1.72, 2.15, 3);
      clock.rotation.y = -Math.PI / 2; clock.userData.interact = { kind: 'lore', id: 'clock' }; interactables.push(clock);
      const poster = mkMesh(new THREE.PlaneGeometry(0.7, 1.05), new THREE.MeshStandardMaterial({ map: Textures.poster, roughness: 0.9 }), -7, 1.73, 1.72); poster.rotation.y = Math.PI; poster.userData.interact = { kind: 'lore', id: 'poster' }; interactables.push(poster);
      const memo1 = mkMesh(new THREE.PlaneGeometry(0.34, 0.34), new THREE.MeshStandardMaterial({ map: Textures.memo, roughness: 0.9 }), 1.72, 1.55, 15); memo1.rotation.y = -Math.PI / 2; memo1.userData.interact = { kind: 'note', id: 'corridor' }; interactables.push(memo1);

      props.clock = clock; props.poster = poster;
      buildCorridorFixtures();
      buildAnomalyObjects();
    }

    // 평상시 회랑 소품 — 플레이어가 '정상 상태'로 기억하게 되는 요소들 (L자 배치)
    // 모든 벽면 부착물은 벽(x=±1.75 / z=±1.75)보다 '안쪽'이어야 보인다.
    function buildCorridorFixtures() {
      // 초상화 4점 (V·H 벽)
      props.portraits = [];
      const portraitInfo = [[-1.72, 5, Math.PI / 2], [1.72, 4, -Math.PI / 2], [-6, -1.72, 0], [-16, -1.72, 0]];
      portraitInfo.forEach(([x, z, ry]) => {
        const m = mkMesh(new THREE.PlaneGeometry(0.5, 0.66), new THREE.MeshStandardMaterial({ map: Textures.portrait, roughness: 0.85 }), x, 1.85, z);
        m.rotation.y = ry;
        m.userData.interact = { kind: 'lore', id: 'portrait' };
        interactables.push(m);
        props.portraits.push(m);
      });

      // 휠체어 (V 좌벽 근처)
      props.wheelchair = makeWheelchair();
      props.wheelchair.position.set(-1.3, 0, 13); props.wheelchair.rotation.y = 0.6;
      props.wheelchairHome = props.wheelchair.position.clone(); props.wheelchairHomeRotY = 0.6;
      scene.add(props.wheelchair);

      // 이송침대(거니) — H 가로팔 (심층 쪽에서 굴러옴)
      props.gurney = makeGurney();
      props.gurney.position.set(-18, 0, 0.1); props.gurney.rotation.y = 0;
      props.gurneyHome = props.gurney.position.clone();
      scene.add(props.gurney);

      // 죽은 화분 (모서리 근처)
      // v1.1.0은 원뿔 하나 = '초록 고깔'이었다. 마른 가지 다발로 바꿔 고사한 식물임을 읽히게.
      const potMat = new THREE.MeshStandardMaterial({ color: 0x3a2c1e, roughness: 0.95 });
      mkMesh(new THREE.CylinderGeometry(0.14, 0.11, 0.3, 10), potMat, 1.5, 0.15, -1.4);
      mkMesh(new THREE.TorusGeometry(0.14, 0.016, 5, 12), potMat, 1.5, 0.295, -1.4).rotation.x = Math.PI / 2;  // 화분 테두리
      mkMesh(new THREE.CylinderGeometry(0.12, 0.12, 0.04, 10), new THREE.MeshStandardMaterial({ color: 0x241c14, roughness: 1 }), 1.5, 0.3, -1.4); // 마른 흙
      props.plant = new THREE.Group();
      const twigMat = new THREE.MeshStandardMaterial({ color: 0x4a412f, roughness: 1 });
      for (let i = 0; i < 5; i++) {
        const a = (i / 5) * Math.PI * 2 + 0.4;
        const len = 0.3 + Math.random() * 0.22;
        const tw = new THREE.Mesh(new THREE.CylinderGeometry(0.006, 0.012, len, 4), twigMat);
        tw.position.set(Math.sin(a) * 0.04, 0.32 + len / 2, Math.cos(a) * 0.04);
        tw.rotation.set(Math.cos(a) * 0.42, 0, -Math.sin(a) * 0.42);
        props.plant.add(tw);
        const leaf = new THREE.Mesh(new THREE.ConeGeometry(0.03, 0.07, 4), new THREE.MeshStandardMaterial({ color: 0x3d3a25, roughness: 1 }));
        leaf.position.set(Math.sin(a) * (0.04 + len * 0.42), 0.3 + len * 0.92, Math.cos(a) * (0.04 + len * 0.42));
        leaf.rotation.x = Math.PI;   // 시들어 아래로 처진 잎
        props.plant.add(leaf);
      }
      props.plant.position.set(1.5, 0, -1.4);
      scene.add(props.plant);

      // 소화기 (V 우벽) — 유일한 채도 빨강 랜드마크
      props.extinguisher = makeExtinguisher();
      props.extinguisher.position.set(1.58, 0.48, 9);
      scene.add(props.extinguisher);
      props.extinguisherHome = props.extinguisher.position.clone();

      // 환풍구 (H 원벽 상단) — v1.2.0 재조형
      // v1.1.0은 검은 평면 한 장이라 '벽에 난 얼룩'으로 보였다. 환풍구인지 알아야
      // 그 안에서 눈이 뜨이는 이상현상(ventEyes)이 의미를 갖는다.
      // 어두운 안쪽 공동 + 금속 테두리 + 경사진 살 5장 + 모서리 나사로 조형한다.
      props.vent = new THREE.Group();
      const ventDark = new THREE.Mesh(new THREE.PlaneGeometry(0.5, 0.34), new THREE.MeshBasicMaterial({ color: 0x030304 }));
      props.vent.add(ventDark);   // 살 뒤의 새카만 공동
      const ventFrameMat = new THREE.MeshStandardMaterial({ color: 0x4a4d52, roughness: 0.6, metalness: 0.55 });
      [[0, 0.175, 0.54, 0.04], [0, -0.175, 0.54, 0.04], [-0.25, 0, 0.04, 0.39], [0.25, 0, 0.04, 0.39]].forEach(([fx, fy, fw, fh]) => {
        const bar = new THREE.Mesh(new THREE.BoxGeometry(fw, fh, 0.03), ventFrameMat);
        bar.position.set(fx, fy, 0.015); props.vent.add(bar);
      });
      const slatMat = new THREE.MeshStandardMaterial({ color: 0x63666c, roughness: 0.55, metalness: 0.5 });
      for (let i = 0; i < 5; i++) {   // 아래로 기울어진 살 — 안쪽이 들여다보이지 않는 각도
        const slat = new THREE.Mesh(new THREE.BoxGeometry(0.46, 0.045, 0.02), slatMat);
        slat.position.set(0, 0.125 - i * 0.062, 0.012);
        slat.rotation.x = -0.42;
        props.vent.add(slat);
      }
      const screwMat = new THREE.MeshStandardMaterial({ color: 0x9aa0a6, roughness: 0.35, metalness: 0.8 });
      [[-0.215, 0.145], [0.215, 0.145], [-0.215, -0.145], [0.215, -0.145]].forEach(([sx, sy]) => {
        const sc = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.012, 6), screwMat);
        sc.position.set(sx, sy, 0.032); sc.rotation.x = Math.PI / 2; props.vent.add(sc);
      });
      props.vent.position.set(-9, 2.5, -1.72);
      scene.add(props.vent);

      // 비상구 유도등 (심층 게이트 위)
      props.exitSign = mkMesh(new THREE.PlaneGeometry(0.5, 0.2), new THREE.MeshBasicMaterial({ map: Textures.exitGreen, transparent: true }), -21.8, 2.2, 0); props.exitSign.rotation.y = Math.PI / 2;

      // ── v1.1.0 신규 소품 (정상 기준선 확장 → 이상현상의 판별 재료) ──

      // 링거 스탠드 2기 (V 세로팔) — 액체 색이 이상현상 대상
      props.ivStands = [];
      props.ivBags = [];
      [[-1.42, 16.2], [1.42, 5.6]].forEach(([x, z]) => {
        const g = new THREE.Group();
        const pole = new THREE.Mesh(new THREE.CylinderGeometry(0.018, 0.018, 1.6, 6), new THREE.MeshStandardMaterial({ color: 0x8b8f96, roughness: 0.35, metalness: 0.7 }));
        pole.position.y = 0.8; g.add(pole);
        const base = new THREE.Mesh(new THREE.CylinderGeometry(0.17, 0.17, 0.03, 10), new THREE.MeshStandardMaterial({ color: 0x2a2a2e, roughness: 0.6 }));
        base.position.y = 0.015; g.add(base);
        const bag = new THREE.Mesh(new THREE.BoxGeometry(0.15, 0.24, 0.06), new THREE.MeshStandardMaterial({ color: 0xcfe4e8, roughness: 0.3, transparent: true, opacity: 0.82 }));
        bag.position.set(0.09, 1.42, 0); g.add(bag);
        g.position.set(x, 0, z);
        scene.add(g);
        props.ivStands.push(g);
        props.ivBags.push(bag);
      });

      // 벤치 (H 가로팔 근벽) — 앉는 방향이 이상현상 대상
      props.bench = new THREE.Group();
      const bMat = new THREE.MeshStandardMaterial({ color: 0x3b3025, roughness: 0.85 });
      const bSeat = new THREE.Mesh(new THREE.BoxGeometry(1.6, 0.07, 0.4), bMat); bSeat.position.y = 0.44; props.bench.add(bSeat);
      const bBack = new THREE.Mesh(new THREE.BoxGeometry(1.6, 0.42, 0.06), bMat); bBack.position.set(0, 0.66, -0.17); props.bench.add(bBack);
      [[-0.7, 0], [0.7, 0]].forEach(([dx]) => {
        const lg = new THREE.Mesh(new THREE.BoxGeometry(0.06, 0.44, 0.34), new THREE.MeshStandardMaterial({ color: 0x1e1e22 }));
        lg.position.set(dx, 0.22, 0); props.bench.add(lg);
      });
      props.bench.position.set(-12.5, 0, 1.4);
      props.benchHomeRotY = 0;
      scene.add(props.bench);

      // 자판기 (H 가로팔 근벽) — 진열창 발광색이 이상현상 대상
      // v1.1.0은 박스 + 평면 하나라 '벽장'처럼 보였다. 진열창·상품·버튼·반환구를 넣는다.
      // (그룹 로컬 −z가 회랑을 향한다 = 정면)
      props.vending = new THREE.Group();
      const vSteel = new THREE.MeshStandardMaterial({ color: 0x24282e, roughness: 0.55, metalness: 0.3 });
      const vDark = new THREE.MeshStandardMaterial({ color: 0x101216, roughness: 0.8 });
      const vBody = new THREE.Mesh(new THREE.BoxGeometry(0.82, 1.9, 0.52), vSteel);
      vBody.position.y = 0.98; props.vending.add(vBody);
      // 진열창 (발광) — 이상현상 시 붉게 변한다
      props.vendGlass = new THREE.Mesh(new THREE.PlaneGeometry(0.52, 1.02), new THREE.MeshBasicMaterial({ color: 0x2f4f52 }));
      props.vendGlass.position.set(-0.09, 1.34, -0.265); props.vendGlass.rotation.y = Math.PI;
      props.vending.add(props.vendGlass);
      // 진열창 안 상품 (실루엣) — 3단 × 4열
      for (let r = 0; r < 3; r++) {
        for (let c = 0; c < 4; c++) {
          const can = new THREE.Mesh(new THREE.CylinderGeometry(0.036, 0.036, 0.1, 6),
            new THREE.MeshBasicMaterial({ color: [0x6b2222, 0x1f4a3a, 0x2b3a5c, 0x54471e][c] }));
          can.position.set(-0.29 + c * 0.135, 0.95 + r * 0.31, -0.255);
          props.vending.add(can);
        }
        const shelf = new THREE.Mesh(new THREE.BoxGeometry(0.5, 0.012, 0.03), vDark);
        shelf.position.set(-0.09, 0.89 + r * 0.31, -0.255); props.vending.add(shelf);
      }
      // 창틀
      const vFrame = new THREE.Mesh(new THREE.BoxGeometry(0.56, 1.06, 0.02), vDark);
      vFrame.position.set(-0.09, 1.34, -0.245); props.vending.add(vFrame);
      // 버튼 패널 (우측 세로 열)
      const vPanel = new THREE.Mesh(new THREE.BoxGeometry(0.16, 1.0, 0.02), vDark);
      vPanel.position.set(0.28, 1.34, -0.265); props.vending.add(vPanel);
      for (let i = 0; i < 5; i++) {
        const btn = new THREE.Mesh(new THREE.CylinderGeometry(0.022, 0.022, 0.012, 8), new THREE.MeshBasicMaterial({ color: 0x8a2020 }));
        btn.position.set(0.28, 1.68 - i * 0.16, -0.28); btn.rotation.x = Math.PI / 2;
        props.vending.add(btn);   // 전부 붉은 SOLD OUT 램프
      }
      // 취출구 (아래 검은 구멍) + 동전 반환구
      const vSlot = new THREE.Mesh(new THREE.BoxGeometry(0.44, 0.2, 0.03), new THREE.MeshBasicMaterial({ color: 0x000000 }));
      vSlot.position.set(-0.09, 0.34, -0.265); props.vending.add(vSlot);
      const vLip = new THREE.Mesh(new THREE.BoxGeometry(0.48, 0.03, 0.06), vSteel);
      vLip.position.set(-0.09, 0.23, -0.28); props.vending.add(vLip);
      const vCoin = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.012, 0.02), vDark);
      vCoin.position.set(0.28, 0.58, -0.265); props.vending.add(vCoin);
      // 짧은 다리 (바닥에서 살짝 띄워 자판기 특유의 실루엣)
      [[-0.32, -0.18], [0.32, -0.18], [-0.32, 0.18], [0.32, 0.18]].forEach(([dx, dz]) => {
        const lg = new THREE.Mesh(new THREE.BoxGeometry(0.06, 0.06, 0.06), vDark);
        lg.position.set(dx, 0.03, dz); props.vending.add(lg);
      });
      props.vending.position.set(-4.6, 0, 1.42);
      props.vending.rotation.y = Math.PI;
      scene.add(props.vending);
      props.vending.userData.interact = { kind: 'lore', id: 'vending' };
      const vendHit = new THREE.Mesh(new THREE.BoxGeometry(0.85, 1.9, 0.55), new THREE.MeshBasicMaterial({ visible: false }));
      vendHit.position.set(-4.6, 0.95, 1.42);
      vendHit.userData.interact = { kind: 'lore', id: 'vending' };
      scene.add(vendHit); interactables.push(vendHit);

      // 청소 카트 (V 세로팔) — 위치가 이상현상 대상
      // v1.1.0은 상자 + 막대 = 정체불명이었다. 바퀴·양동이·짜개·봉투를 더해 청소 카트로 읽히게.
      props.cart = new THREE.Group();
      const cSteel = new THREE.MeshStandardMaterial({ color: 0x9aa0a6, metalness: 0.6, roughness: 0.4 });
      const cPlastic = new THREE.MeshStandardMaterial({ color: 0xc9a227, roughness: 0.75 });  // 청소용 노란 플라스틱
      const cDark = new THREE.MeshStandardMaterial({ color: 0x22262b, roughness: 0.85 });

      // 프레임(선반 2단) + 캐스터 4개
      [0.16, 0.52].forEach((y) => {
        const shelf = new THREE.Mesh(new THREE.BoxGeometry(0.52, 0.02, 0.38), cDark);
        shelf.position.y = y; props.cart.add(shelf);
      });
      [[-0.22, -0.15], [0.22, -0.15], [-0.22, 0.15], [0.22, 0.15]].forEach(([dx, dz]) => {
        const post = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.86, 5), cSteel);
        post.position.set(dx, 0.43, dz); props.cart.add(post);
        const caster = new THREE.Mesh(new THREE.TorusGeometry(0.045, 0.016, 5, 10), cDark);
        caster.position.set(dx, 0.045, dz); caster.rotation.y = Math.PI / 2; props.cart.add(caster);
      });
      // 밀대 손잡이 (가로 바)
      const cHandle = new THREE.Mesh(new THREE.CylinderGeometry(0.014, 0.014, 0.5, 6), cSteel);
      cHandle.position.set(0, 0.88, -0.15); cHandle.rotation.z = Math.PI / 2; props.cart.add(cHandle);

      // 양동이 + 짜개(wringer) — 청소 카트의 결정적 단서
      const bucket = new THREE.Mesh(new THREE.CylinderGeometry(0.15, 0.12, 0.24, 12), cPlastic);
      bucket.position.set(-0.12, 0.3, 0.02); props.cart.add(bucket);
      const water = new THREE.Mesh(new THREE.CylinderGeometry(0.135, 0.135, 0.01, 12), new THREE.MeshStandardMaterial({ color: 0x3d4a44, roughness: 0.25 }));
      water.position.set(-0.12, 0.4, 0.02); props.cart.add(water);   // 탁한 물
      const wringer = new THREE.Mesh(new THREE.BoxGeometry(0.16, 0.12, 0.13), cPlastic);
      wringer.position.set(-0.12, 0.48, 0.02); props.cart.add(wringer);
      const wLever = new THREE.Mesh(new THREE.CylinderGeometry(0.01, 0.01, 0.2, 5), cSteel);
      wLever.position.set(-0.12, 0.58, 0.1); wLever.rotation.x = 0.6; props.cart.add(wLever);

      // 대걸레 (자루 + 젖은 머리)
      const mopStick = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.012, 1.15, 6), new THREE.MeshStandardMaterial({ color: 0x6b5a3c, roughness: 0.9 }));
      mopStick.position.set(0.2, 0.72, 0.1); mopStick.rotation.z = 0.2; props.cart.add(mopStick);
      const mopHead = new THREE.Mesh(new THREE.CylinderGeometry(0.05, 0.075, 0.18, 8), new THREE.MeshStandardMaterial({ color: 0x8f8a7a, roughness: 1 }));
      mopHead.position.set(0.32, 0.19, 0.1); mopHead.rotation.z = 0.2; props.cart.add(mopHead);

      // 쓰레기 봉투 (뒤쪽에 매달림)
      const bag = new THREE.Mesh(new THREE.SphereGeometry(0.13, 8, 7), cDark);
      bag.position.set(0.14, 0.36, -0.14); bag.scale.set(1, 1.25, 0.8); props.cart.add(bag);

      props.cart.position.set(-1.35, 0, 2.6);
      props.cartHome = props.cart.position.clone();
      scene.add(props.cart);

      // 게시판 (V 우벽) — 붙은 종이 수가 이상현상 대상
      props.boardNotes = [];
      const boardBack = mkMesh(new THREE.PlaneGeometry(1.1, 0.75), new THREE.MeshStandardMaterial({ color: 0x2b2620, roughness: 0.95 }), 1.72, 1.8, 17.5);
      boardBack.rotation.y = -Math.PI / 2;
      for (let i = 0; i < 3; i++) {
        const n = mkMesh(new THREE.PlaneGeometry(0.22, 0.28), new THREE.MeshStandardMaterial({ map: Textures.memo, roughness: 0.95 }), 1.71, 1.86 - (i % 2) * 0.24, 17.2 + i * 0.3);
        n.rotation.y = -Math.PI / 2;
        n.rotation.z = (Math.random() - 0.5) * 0.16;
        props.boardNotes.push(n);
      }

      // 소화전 함 (H 원벽) — 문 열림 여부가 이상현상 대상
      props.hydrantBox = mkMesh(new THREE.BoxGeometry(0.42, 0.6, 0.14), new THREE.MeshStandardMaterial({ color: 0x7a2020, roughness: 0.7 }), -19.5, 1.2, -1.66);
      props.hydrantDoor = mkMesh(new THREE.BoxGeometry(0.4, 0.56, 0.03), new THREE.MeshStandardMaterial({ color: 0x9a2a2a, roughness: 0.6 }), -19.5, 1.2, -1.57);
      props.hydrantDoorHomeZ = -1.57;
    }

    function makeWheelchair() {
      const g = new THREE.Group();
      const frame = new THREE.MeshStandardMaterial({ color: 0x6f747c, roughness: 0.45, metalness: 0.65 }); // 크롬 프레임
      const fabric = new THREE.MeshStandardMaterial({ color: 0x1f2126, roughness: 0.95 });                 // 시트 천
      const rubber = new THREE.MeshStandardMaterial({ color: 0x18181c, roughness: 0.85 });

      // 시트 + 등받이 (천)
      const seat = new THREE.Mesh(new THREE.BoxGeometry(0.44, 0.04, 0.42), fabric); seat.position.y = 0.46; g.add(seat);
      const back = new THREE.Mesh(new THREE.BoxGeometry(0.44, 0.52, 0.03), fabric); back.position.set(0, 0.73, -0.21); g.add(back);

      // 큰 뒷바퀴 + 스포크 + 핸드림 (휠체어의 핵심 실루엣)
      const tireGeo = new THREE.TorusGeometry(0.28, 0.028, 6, 20);
      const rimGeo = new THREE.TorusGeometry(0.23, 0.012, 5, 16);
      [-0.26, 0.26].forEach((dx) => {
        const tire = new THREE.Mesh(tireGeo, rubber);
        tire.position.set(dx, 0.28, -0.02); tire.rotation.y = Math.PI / 2; g.add(tire);
        const rim = new THREE.Mesh(rimGeo, frame);
        rim.position.set(dx + (dx > 0 ? 0.03 : -0.03), 0.28, -0.02); rim.rotation.y = Math.PI / 2; g.add(rim);
        for (let i = 0; i < 6; i++) {           // 스포크
          const sp = new THREE.Mesh(new THREE.CylinderGeometry(0.006, 0.006, 0.54, 4), frame);
          sp.position.set(dx, 0.28, -0.02);
          sp.rotation.set(0, 0, i * Math.PI / 6);
          sp.rotation.z = i * Math.PI / 6;
          g.add(sp);
        }
        const hub = new THREE.Mesh(new THREE.CylinderGeometry(0.035, 0.035, 0.06, 8), frame);
        hub.position.set(dx, 0.28, -0.02); hub.rotation.z = Math.PI / 2; g.add(hub);
      });

      // 앞 캐스터 (작은 바퀴 + 포크) — 이게 없어서 '의자'인지 알기 어려웠다
      [-0.19, 0.19].forEach((dx) => {
        const fork = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.26, 5), frame);
        fork.position.set(dx, 0.21, 0.26); g.add(fork);
        const cw = new THREE.Mesh(new THREE.TorusGeometry(0.075, 0.022, 5, 12), rubber);
        cw.position.set(dx, 0.075, 0.26); cw.rotation.y = Math.PI / 2; g.add(cw);
      });

      // 팔걸이
      [-0.25, 0.25].forEach((dx) => {
        const arm = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.03, 0.36), fabric);
        arm.position.set(dx, 0.66, 0.0); g.add(arm);
        const post = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.2, 5), frame);
        post.position.set(dx, 0.56, 0.15); g.add(post);
      });

      // 밀대 손잡이 (등받이 뒤로 솟은 두 개)
      [-0.2, 0.2].forEach((dx) => {
        const h = new THREE.Mesh(new THREE.CylinderGeometry(0.014, 0.014, 0.2, 5), frame);
        h.position.set(dx, 1.03, -0.24); h.rotation.x = -0.35; g.add(h);
      });

      // 발판
      const fpBar = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.3, 5), frame);
      fpBar.position.set(0, 0.24, 0.34); fpBar.rotation.z = Math.PI / 2; g.add(fpBar);
      [-0.11, 0.11].forEach((dx) => {
        const fp = new THREE.Mesh(new THREE.BoxGeometry(0.12, 0.02, 0.16), frame);
        fp.position.set(dx, 0.16, 0.38); fp.rotation.x = -0.2; g.add(fp);
      });
      return g;
    }
    // ════ 마네킹 (v1.2.0 재조형) ════
    // v1.1.0은 원통 1 + 구 1 = 두 덩이뿐이라, 사람인지 기둥인지 분간이 안 됐다.
    // 의류 매장 마네킹처럼 골반–허리–흉곽–어깨–팔–민머리 + 금속 지주와 받침대를 갖춘다.
    // 얼굴은 여전히 없다(이목구비 부재 = 이 게임의 공포 문법).
    const MQ_MAT = () => new THREE.MeshStandardMaterial({ color: 0xe6e2da, roughness: 0.32 });
    function makeMannequinFigure() {
      const g = new THREE.Group();
      const m = MQ_MAT();
      const steel = new THREE.MeshStandardMaterial({ color: 0x6a6e74, roughness: 0.4, metalness: 0.7 });

      // 받침 원판 + 지주 (마네킹임을 즉시 알려주는 단서)
      const base = new THREE.Mesh(new THREE.CylinderGeometry(0.24, 0.26, 0.03, 14), steel);
      base.position.y = 0.015; g.add(base);
      const pole = new THREE.Mesh(new THREE.CylinderGeometry(0.02, 0.02, 0.42, 6), steel);
      pole.position.y = 0.21; g.add(pole);

      // 다리 (붙은 형태 — 마네킹은 보통 하반신이 한 덩이)
      const legs = new THREE.Mesh(new THREE.CylinderGeometry(0.15, 0.11, 0.52, 10), m);
      legs.position.y = 0.66; g.add(legs);
      // 골반
      const hip = new THREE.Mesh(new THREE.SphereGeometry(0.17, 10, 8), m);
      hip.position.y = 0.95; hip.scale.set(1, 0.72, 0.85); g.add(hip);
      // 허리 (잘록하게 — 실루엣의 핵심)
      const waist = new THREE.Mesh(new THREE.CylinderGeometry(0.135, 0.16, 0.2, 10), m);
      waist.position.y = 1.11; g.add(waist);
      // 흉곽 (위로 벌어짐)
      const chest = new THREE.Mesh(new THREE.CylinderGeometry(0.2, 0.14, 0.34, 10), m);
      chest.position.y = 1.36; g.add(chest);
      const bust = new THREE.Mesh(new THREE.SphereGeometry(0.2, 10, 8), m);
      bust.position.set(0, 1.44, 0.03); bust.scale.set(1, 0.62, 0.78); g.add(bust);

      // 어깨 (구체 2개) + 팔 (약간 벌린 각도)
      [-1, 1].forEach((s) => {
        const sh = new THREE.Mesh(new THREE.SphereGeometry(0.062, 8, 8), m);
        sh.position.set(s * 0.19, 1.52, 0); g.add(sh);
        const upper = new THREE.Mesh(new THREE.CylinderGeometry(0.045, 0.038, 0.36, 7), m);
        upper.position.set(s * 0.235, 1.35, 0.01); upper.rotation.z = s * 0.16; g.add(upper);
        const elbow = new THREE.Mesh(new THREE.SphereGeometry(0.038, 7, 7), m);
        elbow.position.set(s * 0.27, 1.17, 0.02); g.add(elbow);
        const fore = new THREE.Mesh(new THREE.CylinderGeometry(0.034, 0.026, 0.33, 7), m);
        fore.position.set(s * 0.285, 1.0, 0.05); fore.rotation.z = s * 0.06; fore.rotation.x = -0.12; g.add(fore);
        // 손은 뭉툭하게 (손가락 없음 — 마네킹 규격)
        const hand = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.11, 0.03), m);
        hand.position.set(s * 0.295, 0.84, 0.08); g.add(hand);
      });

      // 목 + 민머리 (이목구비 없음)
      const neck = new THREE.Mesh(new THREE.CylinderGeometry(0.05, 0.06, 0.11, 8), m);
      neck.position.y = 1.6; g.add(neck);
      const head = new THREE.Mesh(new THREE.SphereGeometry(0.115, 12, 10), m);
      head.position.y = 1.73; head.scale.set(0.92, 1.18, 1.0); g.add(head);
      // 이음매 선 (관절 분리형 마네킹의 표식)
      const seam = new THREE.Mesh(new THREE.TorusGeometry(0.137, 0.006, 4, 14), steel);
      seam.position.y = 1.21; seam.rotation.x = Math.PI / 2; g.add(seam);
      return g;
    }

    // 소화기 (v1.2.0 재조형)
    // v1.1.0은 맨 원통 하나라 '빨간 기둥'으로만 보였다. 노즐·호스·레버·압력계·브래킷을 붙인다.
    function makeExtinguisher() {
      const gEx = new THREE.Group();
      const exRed = new THREE.MeshStandardMaterial({ color: 0xb01818, roughness: 0.45, metalness: 0.35 });
      const exSteel = new THREE.MeshStandardMaterial({ color: 0x4a4d53, roughness: 0.4, metalness: 0.75 });
      const exBody = new THREE.Mesh(new THREE.CylinderGeometry(0.085, 0.085, 0.4, 12), exRed);
      exBody.position.y = 0.2; gEx.add(exBody);
      const exTop = new THREE.Mesh(new THREE.SphereGeometry(0.085, 12, 8), exRed);
      exTop.position.y = 0.4; exTop.scale.y = 0.55; gEx.add(exTop);
      const exNeck = new THREE.Mesh(new THREE.CylinderGeometry(0.028, 0.034, 0.07, 8), exSteel);
      exNeck.position.y = 0.46; gEx.add(exNeck);
      const exLever = new THREE.Mesh(new THREE.BoxGeometry(0.12, 0.018, 0.04), exSteel);   // 손잡이 레버
      exLever.position.set(0.03, 0.52, 0); gEx.add(exLever);
      const exGauge = new THREE.Mesh(new THREE.CylinderGeometry(0.022, 0.022, 0.015, 8), new THREE.MeshBasicMaterial({ color: 0xd8d8c8 }));
      exGauge.position.set(-0.05, 0.5, 0.03); exGauge.rotation.x = Math.PI / 2; gEx.add(exGauge);  // 압력계
      const exHose = new THREE.Mesh(new THREE.TorusGeometry(0.09, 0.012, 5, 12, Math.PI * 1.2), new THREE.MeshStandardMaterial({ color: 0x1a1a1c, roughness: 0.9 }));
      exHose.position.set(0.02, 0.3, 0.09); exHose.rotation.set(0.4, 0.2, 1.6); gEx.add(exHose);   // 호스
      const exNozzle = new THREE.Mesh(new THREE.ConeGeometry(0.035, 0.09, 8), new THREE.MeshStandardMaterial({ color: 0x141416, roughness: 0.9 }));
      exNozzle.position.set(0.05, 0.14, 0.11); exNozzle.rotation.x = 1.9; gEx.add(exNozzle);       // 나팔 노즐
      [0.1, 0.32].forEach((y) => {                                                                 // 벽 브래킷
        const br = new THREE.Mesh(new THREE.BoxGeometry(0.03, 0.02, 0.13), exSteel);
        br.position.set(0, y, -0.11); gEx.add(br);
      });
      return gEx;
    }

    function makeGurney() {
      const g = new THREE.Group();
      const fMat = new THREE.MeshStandardMaterial({ color: 0x30323a, roughness: 0.5, metalness: 0.5 });
      const bed = new THREE.Mesh(new THREE.BoxGeometry(1.7, 0.1, 0.62), fMat); bed.position.y = 0.7; g.add(bed);
      const sheet = new THREE.Mesh(new THREE.BoxGeometry(1.55, 0.08, 0.55), new THREE.MeshStandardMaterial({ color: 0xb8b4a8, roughness: 0.95 })); sheet.position.y = 0.76; g.add(sheet);
      const legMat = new THREE.MeshStandardMaterial({ color: 0x1e1e22 });
      [[-0.75, -0.24], [0.75, -0.24], [-0.75, 0.24], [0.75, 0.24]].forEach(([dx, dz]) => {
        const leg = new THREE.Mesh(new THREE.CylinderGeometry(0.03, 0.03, 0.7, 6), legMat); leg.position.set(dx, 0.35, dz); g.add(leg);
      });
      return g;
    }

    // 이상현상 전용 객체 (L자 배치) — 벽면 부착물은 반드시 벽 '안쪽'
    function buildAnomalyObjects() {
      anomObj.endFigure = makeFigureSlot();
      anomObj.endFigure.position.set(-20.5, 0, 0);
      anomObj.endFigure.visible = false;
      scene.add(anomObj.endFigure);

      anomObj.ventEyes = new THREE.Group();
      const em = new THREE.MeshBasicMaterial({ color: 0xff1414, transparent: true });
      const ea = new THREE.Mesh(new THREE.SphereGeometry(0.03, 6, 6), em); ea.position.x = -0.08;
      const eb = new THREE.Mesh(new THREE.SphereGeometry(0.03, 6, 6), em); eb.position.x = 0.08;
      anomObj.ventEyes.add(ea, eb);
      anomObj.ventEyes.position.set(-9, 2.5, -1.68);
      anomObj.ventEyes.visible = false;
      scene.add(anomObj.ventEyes);

      // 존재하지 않아야 할 여분의 문 (H 근벽)
      anomObj.extraDoor = new THREE.Group();
      const ef = new THREE.Mesh(new THREE.BoxGeometry(1.1, 2.2, 0.12), new THREE.MeshStandardMaterial({ color: 0x140b06, roughness: 0.9 }));
      ef.position.y = 1.1; anomObj.extraDoor.add(ef);
      const eg = new THREE.Mesh(new THREE.PlaneGeometry(0.9, 2.0), new THREE.MeshBasicMaterial({ color: 0x000000 }));
      eg.position.set(0, 1.05, -0.08); anomObj.extraDoor.add(eg);
      anomObj.extraDoor.position.set(-15, 0, 1.68);
      anomObj.extraDoor.rotation.y = Math.PI;
      anomObj.extraDoor.visible = false;
      scene.add(anomObj.extraDoor);

      // 복제 휠체어 (모서리 부근 한가운데)
      anomObj.dupWheelchair = makeWheelchair();
      anomObj.dupWheelchair.position.set(0, 0, 8);
      anomObj.dupWheelchair.rotation.y = Math.PI;
      anomObj.dupWheelchair.visible = false;
      scene.add(anomObj.dupWheelchair);

      // 바닥 핏자국 (H 가로팔, 심층으로)
      anomObj.bloodTrail = mkMesh(new THREE.PlaneGeometry(0.7, 10), new THREE.MeshBasicMaterial({ map: Textures.bloodTrail, transparent: true }), -10, 0.02, 0);
      anomObj.bloodTrail.rotation.set(-Math.PI / 2, 0, Math.PI / 2);
      anomObj.bloodTrail.visible = false;

      // ── v1.1.0 신규 회랑 이상현상 객체 ──

      // 천장에 매달린 형체 (V 세로팔 상단) — 뚜렷
      anomObj.hangingFigure = new THREE.Group();
      const hMat = new THREE.MeshStandardMaterial({ color: 0x8d867c, roughness: 1 });
      const hRope = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.012, 0.7, 5), new THREE.MeshStandardMaterial({ color: 0x2a2620 }));
      hRope.position.y = 2.85; anomObj.hangingFigure.add(hRope);
      const hBody = new THREE.Mesh(new THREE.CylinderGeometry(0.11, 0.14, 0.95, 7), hMat);
      hBody.position.y = 2.05; anomObj.hangingFigure.add(hBody);
      const hHead = new THREE.Mesh(new THREE.SphereGeometry(0.16, 9, 8), hMat);
      hHead.position.y = 2.62; hHead.rotation.z = 0.5; anomObj.hangingFigure.add(hHead);
      const hLeg = new THREE.Mesh(new THREE.CylinderGeometry(0.04, 0.03, 0.75, 5), hMat);
      hLeg.position.set(0.04, 1.2, 0.02); anomObj.hangingFigure.add(hLeg);
      anomObj.hangingFigure.position.set(0, 0, 10.5);
      anomObj.hangingFigure.visible = false;
      scene.add(anomObj.hangingFigure);

      // 무한히 이어지는 복제 초상화 벽 (H 원벽) — 뚜렷
      anomObj.portraitWall = new THREE.Group();
      for (let i = 0; i < 7; i++) {
        const pm = new THREE.Mesh(new THREE.PlaneGeometry(0.5, 0.66), new THREE.MeshStandardMaterial({ map: Textures.portraitWrong, roughness: 0.85 }));
        pm.position.set(-3 - i * 2.4, 1.85, -1.71);
        anomObj.portraitWall.add(pm);
      }
      anomObj.portraitWall.visible = false;
      scene.add(anomObj.portraitWall);

      // 뒤집힌 천장 소화기 (V 우벽 천장) — 미묘
      anomObj.ceilExtin = makeExtinguisher();
      anomObj.ceilExtin.position.set(1.4, 2.72, 9);
      anomObj.ceilExtin.rotation.z = Math.PI;   // 천장에 거꾸로 매달려 있다
      anomObj.ceilExtin.visible = false;
      scene.add(anomObj.ceilExtin);

      // 여분의 옷장 (H 가로팔) — 미묘
      // 진짜 옷장과 같은 팩토리로 만든다. 똑같이 생겨야 "하나 더 있다"가 읽힌다.
      // 문이 회랑 쪽(+z)을 보도록 180° 돌린다.
      anomObj.dupLocker = makeLockerBody();
      anomObj.dupLocker.position.set(-7.5, 0, -1.2);
      anomObj.dupLocker.rotation.y = Math.PI;
      anomObj.dupLocker.visible = false;
      scene.add(anomObj.dupLocker);

      // 벽에 번지는 손자국 (V 좌벽) — 미묘
      anomObj.handPrints = mkMesh(new THREE.PlaneGeometry(1.6, 1.2), new THREE.MeshBasicMaterial({ map: Textures.handPrints, transparent: true }), -1.71, 1.5, 11);
      anomObj.handPrints.rotation.y = Math.PI / 2;
      anomObj.handPrints.visible = false;

      // 젖은 바닥 표지 (H 가로팔) — 미묘 (평소엔 없다)
      anomObj.wetSign = new THREE.Group();
      const wsMat = new THREE.MeshStandardMaterial({ color: 0xc9a227, roughness: 0.7, side: THREE.DoubleSide });
      const wsA = new THREE.Mesh(new THREE.PlaneGeometry(0.36, 0.5), wsMat); wsA.position.set(0, 0.25, 0.06); wsA.rotation.x = 0.22;
      const wsB = new THREE.Mesh(new THREE.PlaneGeometry(0.36, 0.5), wsMat); wsB.position.set(0, 0.25, -0.06); wsB.rotation.x = -0.22;
      anomObj.wetSign.add(wsA, wsB);
      anomObj.wetSign.position.set(-13.5, 0, 0);
      anomObj.wetSign.visible = false;
      scene.add(anomObj.wetSign);
    }

    function makeDoor(letter, room, x, z, rotY, plateTex) {
      const group = new THREE.Group();
      group.position.set(x, 0, z);
      group.rotation.y = rotY;

      const frame = new THREE.Mesh(new THREE.BoxGeometry(1.34, 2.36, 0.16), new THREE.MeshStandardMaterial({ color: 0x18120a, roughness: 0.85 }));
      frame.position.set(0, 1.18, 0);
      group.add(frame);

      const panelMat = new THREE.MeshStandardMaterial({ color: 0x4a2c14, roughness: 0.8 });
      const panel = new THREE.Mesh(new THREE.BoxGeometry(1.06, 2.14, 0.09), panelMat);
      panel.position.set(0, 1.07, 0.045);
      group.add(panel);

      const knob = new THREE.Mesh(new THREE.SphereGeometry(0.05, 10, 10), new THREE.MeshStandardMaterial({ color: 0xb9a35e, roughness: 0.3, metalness: 0.7 }));
      knob.position.set(0.4, 1.05, 0.12);
      group.add(knob);

      const plate = new THREE.Mesh(new THREE.PlaneGeometry(0.4, 0.25), new THREE.MeshStandardMaterial({ map: plateTex, roughness: 0.6 }));
      plate.position.set(0, 1.95, 0.11);
      group.add(plate);

      const info = { kind: 'door', room: room, letter: letter };
      [frame, panel, knob, plate].forEach((m) => { m.userData.interact = info; interactables.push(m); });

      scene.add(group);
      doorDefs.push({ group, panel, plate, room, letter, basePlate: plateTex, baseColor: 0x4a2c14, homeX: x, homeZ: z });
      return group;
    }

    // ════ 방 조명 통합 (v1.2.0) ════
    // 방 3개는 서로 100m 이상, 회랑에서 200m 이상 떨어져 있어 동시에 보일 수 없다.
    // 그런데 v1.1.0은 PointLight를 방마다 하나씩(총 3개) 상주시켜, 회랑에 있는
    // 동안에도 픽셀마다 쓸모없는 조명 3개를 계산했다.
    // → PointLight 하나만 두고, 플레이어가 들어간 방으로 옮겨 쓴다.
    const ROOM_LIGHT_CFG = {
      roomA: { color: 0xffe6c8, intensity: 1.35 },
      roomB: { color: 0x9ad7e0, intensity: 1.30 },
      roomC: { color: 0xfcb5b5, intensity: 1.20 }
    };
    let roomLight = null;
    function setRoomLight(room) {
      if (!roomLight) return;
      const cfg = ROOM_LIGHT_CFG[room];
      if (!cfg) { roomLight.intensity = 0; return; }
      const r = ROOMS[room];
      roomLight.position.set(r.cx, 2.7, r.cz);
      roomLight.color.setHex(cfg.color);
      roomLight.intensity = cfg.intensity;
    }

    // 방 공통 골조 (안쪽을 향한 벽 4면 + 바닥 + 천장 + 등기구)
    function makeRoomShell(cx, cz, lightColor, lightIntensity) {
      const S = 2.2, H = 3.2;
      const floorTex = Textures.floor.clone(); floorTex.needsUpdate = true;
      floorTex.wrapS = THREE.RepeatWrapping; floorTex.wrapT = THREE.RepeatWrapping;
      floorTex.repeat.set(2.2, 2.2);
      const fl = mkMesh(new THREE.PlaneGeometry(S * 2, S * 2), new THREE.MeshStandardMaterial({ map: floorTex, roughness: 0.85 }), cx, 0.01, cz);
      fl.rotation.x = -Math.PI / 2;

      const cl = mkMesh(new THREE.PlaneGeometry(S * 2, S * 2), new THREE.MeshStandardMaterial({ color: 0x111113, roughness: 0.9 }), cx, H, cz);
      cl.rotation.x = Math.PI / 2;

      const wallTex = Textures.wall.clone(); wallTex.needsUpdate = true;
      wallTex.wrapS = THREE.RepeatWrapping; wallTex.wrapT = THREE.RepeatWrapping;
      wallTex.repeat.set(2.2, 1);
      const wMat = new THREE.MeshStandardMaterial({ map: wallTex, roughness: 0.95 });
      const wGeo = new THREE.PlaneGeometry(S * 2, H);
      const wN = mkMesh(wGeo, wMat, cx, H / 2, cz - S);                    // 북벽 → +z 방향
      const wS2 = mkMesh(wGeo, wMat, cx, H / 2, cz + S); wS2.rotation.y = Math.PI;
      const wE = mkMesh(wGeo, wMat, cx + S, H / 2, cz); wE.rotation.y = -Math.PI / 2;
      const wW = mkMesh(wGeo, wMat, cx - S, H / 2, cz); wW.rotation.y = Math.PI / 2;
      blockers.push(wN, wS2, wE, wW);

      // 등기구(발광판)는 방마다 두되, 실제 PointLight는 전 방이 공유하는 1개뿐
      mkMesh(new THREE.BoxGeometry(0.7, 0.05, 0.7), new THREE.MeshBasicMaterial({ color: lightColor }), cx, H - 0.04, cz);
      if (!roomLight) {
        roomLight = new THREE.PointLight(0xffffff, 0, 9);
        roomLight.position.set(cx, 2.7, cz);
        scene.add(roomLight);
      }
      return roomLight;
    }

    function buildRoomA() {
      const cx = ROOMS.roomA.cx, cz = ROOMS.roomA.cz;
      makeRoomShell(cx, cz, 0xffe6c8, 1.35);

      // 방 안쪽 문 (동쪽 벽) — 벽 안쪽
      makeDoor('A', 'roomA', cx + 2.12, cz, -Math.PI / 2, Textures.plateA);

      const mkMannequin = (x, z, ry) => {
        const g = makeMannequinFigure();
        g.position.set(x, 0, z);
        g.rotation.y = ry;
        scene.add(g);
        return g;
      };
      // 고정 마네킹 2기 — 정상 시엔 서로 다른 방향을 본다
      props.mqFixed = [
        mkMannequin(cx - 1.5, cz + 1.6, 2.4),
        mkMannequin(cx + 1.1, cz + 1.7, -2.9)
      ];
      props.mqFixedHomeRotY = [2.4, -2.9];

      // 움직이는 개체 (위핑엔젤 — 정상 기준선의 일부)
      roomMannequinHome.set(cx - 1.4, 0, cz - 1.4);
      roomMannequin = mkMannequin(roomMannequinHome.x, roomMannequinHome.z, 0.8);

      // 병상 (신규) — 시트의 눌린 자국이 이상현상 대상
      props.bed = new THREE.Group();
      const bedFrame = new THREE.Mesh(new THREE.BoxGeometry(0.85, 0.09, 1.95), new THREE.MeshStandardMaterial({ color: 0x30323a, roughness: 0.5, metalness: 0.45 }));
      bedFrame.position.y = 0.62; props.bed.add(bedFrame);
      props.bedSheet = new THREE.Mesh(new THREE.PlaneGeometry(0.8, 1.9), new THREE.MeshStandardMaterial({ map: Textures.sheetEmpty, roughness: 0.95 }));
      props.bedSheet.position.y = 0.675; props.bedSheet.rotation.x = -Math.PI / 2; props.bed.add(props.bedSheet);
      [[-0.36, -0.88], [0.36, -0.88], [-0.36, 0.88], [0.36, 0.88]].forEach(([dx, dz]) => {
        const lg = new THREE.Mesh(new THREE.CylinderGeometry(0.028, 0.028, 0.62, 6), new THREE.MeshStandardMaterial({ color: 0x1e1e22 }));
        lg.position.set(dx, 0.31, dz); props.bed.add(lg);
      });
      const rail = new THREE.Mesh(new THREE.BoxGeometry(0.86, 0.34, 0.03), new THREE.MeshStandardMaterial({ color: 0x8b8f96, roughness: 0.4, metalness: 0.6 }));
      rail.position.set(0, 0.86, -0.95); props.bed.add(rail);
      props.bed.position.set(cx + 1.2, 0, cz - 0.9);
      scene.add(props.bed);
      const bedHit = new THREE.Mesh(new THREE.BoxGeometry(0.95, 0.9, 2.05), new THREE.MeshBasicMaterial({ visible: false }));
      bedHit.position.set(cx + 1.2, 0.5, cz - 0.9);
      bedHit.userData.interact = { kind: 'lore', id: 'bed' };
      scene.add(bedHit); interactables.push(bedHit);

      // 링거 스탠드 (병상 옆)
      const ivG = new THREE.Group();
      const ivPole = new THREE.Mesh(new THREE.CylinderGeometry(0.018, 0.018, 1.6, 6), new THREE.MeshStandardMaterial({ color: 0x8b8f96, roughness: 0.35, metalness: 0.7 }));
      ivPole.position.y = 0.8; ivG.add(ivPole);
      const ivBase = new THREE.Mesh(new THREE.CylinderGeometry(0.16, 0.16, 0.03, 10), new THREE.MeshStandardMaterial({ color: 0x2a2a2e, roughness: 0.6 }));
      ivBase.position.y = 0.015; ivG.add(ivBase);
      props.roomAIvBag = new THREE.Mesh(new THREE.BoxGeometry(0.15, 0.24, 0.06), new THREE.MeshStandardMaterial({ color: 0xcfe4e8, roughness: 0.3, transparent: true, opacity: 0.82 }));
      props.roomAIvBag.position.set(0.09, 1.42, 0); ivG.add(props.roomAIvBag);
      ivG.position.set(cx + 1.75, 0, cz - 1.75);
      scene.add(ivG);

      // 커튼 (신규 세트드레싱)
      props.curtain = mkMesh(new THREE.PlaneGeometry(1.5, 2.3), new THREE.MeshStandardMaterial({ color: 0x707a80, roughness: 0.95, side: THREE.DoubleSide }), cx + 0.15, 1.3, cz - 1.9);
      props.curtainHomeX = cx + 0.15;

      // 깨진 안경 (수집)
      itemGlasses = new THREE.Group();
      const lensMat = new THREE.MeshStandardMaterial({ color: 0x22d3ee, roughness: 0.15, metalness: 0.4 });
      const l1 = new THREE.Mesh(new THREE.TorusGeometry(0.075, 0.014, 8, 24), lensMat); l1.position.x = -0.09;
      const l2 = new THREE.Mesh(new THREE.TorusGeometry(0.075, 0.014, 8, 24), lensMat); l2.position.x = 0.09;
      const bridge = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.012, 0.012), lensMat);
      itemGlasses.add(l1, l2, bridge);
      itemGlasses.position.set(cx - 1.6, 0.35, cz + 0.2);
      itemGlasses.rotation.x = Math.PI / 2.4;
      scene.add(itemGlasses);
      const glassHit = new THREE.Mesh(new THREE.SphereGeometry(0.24, 8, 8), new THREE.MeshBasicMaterial({ visible: false }));
      glassHit.position.copy(itemGlasses.position);
      glassHit.userData.interact = { kind: 'item', id: 'glasses' };
      scene.add(glassHit); interactables.push(glassHit);
      itemGlasses.userData.hitProxy = glassHit;
      floaters.push(itemGlasses);

      // 아이 낙서 (북벽 안쪽)
      const draw = mkMesh(new THREE.PlaneGeometry(0.5, 0.4), new THREE.MeshStandardMaterial({ map: Textures.memo, roughness: 0.9 }), cx - 0.6, 1.5, cz - 2.16);
      draw.userData.interact = { kind: 'lore', id: 'drawing' };
      interactables.push(draw);

      // ── Room A 이상현상 객체 ──
      anomObj.mqExtra = mkMannequin(cx + 1.75, cz + 1.55, 3.9);   // 4번째 마네킹 (평소엔 없다)
      anomObj.mqExtra.visible = false;
    }

    function buildRoomB() {
      const cx = ROOMS.roomB.cx, cz = ROOMS.roomB.cz;
      makeRoomShell(cx, cz, 0x9ad7e0, 1.3);

      makeDoor('B', 'roomB', cx - 2.12, cz, Math.PI / 2, Textures.plateB);

      // 책상 + 모니터
      mkMesh(new THREE.BoxGeometry(1.5, 0.08, 0.7), new THREE.MeshStandardMaterial({ color: 0x2b2b2e, roughness: 0.6 }), cx + 0.6, 0.78, cz - 1.6);
      const legMat = new THREE.MeshStandardMaterial({ color: 0x1c1c1f });
      [[-0.65, -0.28], [0.65, -0.28], [-0.65, 0.28], [0.65, 0.28]].forEach(([dx, dz]) => {
        mkMesh(new THREE.BoxGeometry(0.06, 0.78, 0.06), legMat, cx + 0.6 + dx, 0.39, cz - 1.6 + dz);
      });
      monitorMesh = mkMesh(new THREE.BoxGeometry(0.78, 0.5, 0.07), new THREE.MeshBasicMaterial({ map: Textures.monitorIdle }), cx + 0.6, 1.18, cz - 1.75);
      monitorMesh.userData.interact = { kind: 'computer' };
      interactables.push(monitorMesh);

      // 캐비닛 + 잠긴 서랍 (키패드)
      cabinetMesh = mkMesh(new THREE.BoxGeometry(0.8, 1.1, 0.6), new THREE.MeshStandardMaterial({ color: 0x232326, roughness: 0.55, metalness: 0.35 }), cx - 1.4, 0.55, cz - 1.6);
      drawerMesh = mkMesh(new THREE.BoxGeometry(0.68, 0.26, 0.55), new THREE.MeshStandardMaterial({ color: 0x2f2f33, roughness: 0.5, metalness: 0.4 }), cx - 1.4, 0.82, cz - 1.58);
      const kpGlow = mkMesh(new THREE.PlaneGeometry(0.16, 0.12), new THREE.MeshBasicMaterial({ color: 0xf59e0b }), cx - 1.4, 0.82, cz - 1.29);
      const kpInfo = { kind: 'keypad' };
      cabinetMesh.userData.interact = kpInfo;
      drawerMesh.userData.interact = kpInfo;
      kpGlow.userData.interact = kpInfo;
      interactables.push(cabinetMesh, drawerMesh, kpGlow);

      // 힌트 메모 (동벽 안쪽)
      const memoB = mkMesh(new THREE.PlaneGeometry(0.34, 0.34), new THREE.MeshStandardMaterial({ map: Textures.memo, roughness: 0.9 }), cx + 2.16, 1.5, cz + 0.6);
      memoB.rotation.y = -Math.PI / 2;
      memoB.userData.interact = { kind: 'note', id: 'roomB' };
      interactables.push(memoB);

      // ── v1.1.0 신규 소품 ──

      // 사무 의자 (책상 앞) — 회전이 이상현상 대상
      props.officeChair = new THREE.Group();
      const ocMat = new THREE.MeshStandardMaterial({ color: 0x26262b, roughness: 0.75 });
      const ocSeat = new THREE.Mesh(new THREE.CylinderGeometry(0.24, 0.24, 0.07, 12), ocMat); ocSeat.position.y = 0.46; props.officeChair.add(ocSeat);
      const ocBack = new THREE.Mesh(new THREE.BoxGeometry(0.42, 0.5, 0.06), ocMat); ocBack.position.set(0, 0.74, -0.2); props.officeChair.add(ocBack);
      const ocPole = new THREE.Mesh(new THREE.CylinderGeometry(0.035, 0.035, 0.42, 6), new THREE.MeshStandardMaterial({ color: 0x54585e, metalness: 0.6, roughness: 0.4 }));
      ocPole.position.y = 0.23; props.officeChair.add(ocPole);
      for (let i = 0; i < 5; i++) {
        const a = (i / 5) * Math.PI * 2;
        const foot = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.03, 0.26), new THREE.MeshStandardMaterial({ color: 0x2a2a2e }));
        foot.position.set(Math.sin(a) * 0.13, 0.03, Math.cos(a) * 0.13);
        foot.rotation.y = a; props.officeChair.add(foot);
      }
      props.officeChair.position.set(cx + 0.6, 0, cz - 0.85);
      props.officeChairHomeRotY = 0;
      scene.add(props.officeChair);

      // 서류 더미 3장 (책상 위) — 부양이 이상현상 대상
      props.papers = [];
      for (let i = 0; i < 3; i++) {
        const pp = mkMesh(new THREE.PlaneGeometry(0.24, 0.3), new THREE.MeshStandardMaterial({ map: Textures.memo, roughness: 0.95, side: THREE.DoubleSide }), cx + 0.05 + i * 0.22, 0.83, cz - 1.45 + (i % 2) * 0.14);
        pp.rotation.x = -Math.PI / 2;
        pp.rotation.z = (Math.random() - 0.5) * 0.5;
        pp.userData.baseY = 0.83;
        props.papers.push(pp);
      }

      // 벽 달력 (남벽 안쪽) — 날짜가 이상현상 대상
      props.calendar = mkMesh(new THREE.PlaneGeometry(0.44, 0.44), new THREE.MeshStandardMaterial({ map: Textures.calendar, roughness: 0.9 }), cx - 0.7, 1.75, cz + 2.16);
      props.calendar.rotation.y = Math.PI;
      props.calendar.userData.interact = { kind: 'lore', id: 'calendar' };
      interactables.push(props.calendar);

      // 서류함 (서벽)
      mkMesh(new THREE.BoxGeometry(0.5, 1.5, 0.42), new THREE.MeshStandardMaterial({ color: 0x2a2a2f, roughness: 0.6, metalness: 0.3 }), cx - 1.85, 0.75, cz + 1.3);
    }

    function buildRoomC() {
      const cx = ROOMS.roomC.cx, cz = ROOMS.roomC.cz;
      makeRoomShell(cx, cz, 0xfcb5b5, 1.2);

      makeDoor('C', 'roomC', cx + 2.12, cz, -Math.PI / 2, Textures.plateC);

      // 거울 (서쪽 벽 안쪽)
      mirrorMesh = mkMesh(new THREE.PlaneGeometry(1.3, 2.1), new THREE.MeshStandardMaterial({ map: Textures.mirrorNormal, roughness: 0.15, metalness: 0.85 }), cx - 2.14, 1.25, cz);
      mirrorMesh.rotation.y = Math.PI / 2;
      mirrorMesh.userData.interact = { kind: 'lore', id: 'mirror' };
      interactables.push(mirrorMesh);

      // 넘어진 의자 — 다시 서 있는 것이 이상현상
      props.fallenChair = new THREE.Group();
      const cMat = new THREE.MeshStandardMaterial({ color: 0x3a2c20, roughness: 0.8 });
      const seat = new THREE.Mesh(new THREE.BoxGeometry(0.42, 0.05, 0.42), cMat); seat.position.y = 0.02; props.fallenChair.add(seat);
      const back = new THREE.Mesh(new THREE.BoxGeometry(0.42, 0.5, 0.05), cMat); back.position.set(0, 0.02, -0.24); back.rotation.x = Math.PI / 2.2; props.fallenChair.add(back);
      props.fallenChair.position.set(cx + 0.7, 0.22, cz + 1.1);
      props.fallenChair.rotation.set(0, 1.2, Math.PI / 2);
      scene.add(props.fallenChair);

      // 세면대 2기 (남벽) — 물때·핏물이 이상현상 대상
      props.sinks = [];
      props.sinkBasins = [];
      [-0.9, 0.5].forEach((dx) => {
        const g = new THREE.Group();
        const col = new THREE.Mesh(new THREE.CylinderGeometry(0.09, 0.12, 0.62, 8), new THREE.MeshStandardMaterial({ color: 0xd6d2c8, roughness: 0.35 }));
        col.position.y = 0.31; g.add(col);
        const basin = new THREE.Mesh(new THREE.CylinderGeometry(0.24, 0.18, 0.16, 12), new THREE.MeshStandardMaterial({ color: 0xe2ded4, roughness: 0.3 }));
        basin.position.y = 0.7; g.add(basin);
        const tap = new THREE.Mesh(new THREE.CylinderGeometry(0.018, 0.018, 0.22, 6), new THREE.MeshStandardMaterial({ color: 0x9aa0a6, metalness: 0.75, roughness: 0.3 }));
        tap.position.set(0, 0.86, -0.16); g.add(tap);
        g.position.set(cx + dx, 0, cz + 1.85);
        scene.add(g);
        props.sinks.push(g);
        props.sinkBasins.push(basin);
      });

      // 수건걸이 + 수건 3장 (동벽) — 사라지는 것이 이상현상
      mkMesh(new THREE.CylinderGeometry(0.014, 0.014, 1.0, 6), new THREE.MeshStandardMaterial({ color: 0x9aa0a6, metalness: 0.6, roughness: 0.4 }), cx + 2.05, 1.55, cz + 1.0).rotation.x = Math.PI / 2;
      props.towels = [];
      [-0.3, 0, 0.3].forEach((dz) => {
        const t = mkMesh(new THREE.PlaneGeometry(0.2, 0.42), new THREE.MeshStandardMaterial({ color: 0xbfc4c0, roughness: 0.95, side: THREE.DoubleSide }), cx + 2.02, 1.32, cz + 1.0 + dz);
        t.rotation.y = -Math.PI / 2;
        props.towels.push(t);
      });

      // 일기장 페이지 (거울 사건 후 등장)
      itemDiaryPage = mkMesh(new THREE.PlaneGeometry(0.3, 0.4), new THREE.MeshStandardMaterial({ map: Textures.memo, roughness: 0.9, side: THREE.DoubleSide }), cx - 1.5, 0.35, cz + 0.4);
      itemDiaryPage.rotation.x = -Math.PI / 2.6;
      itemDiaryPage.visible = false;
      const diaryHit = new THREE.Mesh(new THREE.SphereGeometry(0.26, 8, 8), new THREE.MeshBasicMaterial({ visible: false }));
      diaryHit.position.copy(itemDiaryPage.position);
      diaryHit.userData.interact = { kind: 'item', id: 'diary' };
      scene.add(diaryHit); interactables.push(diaryHit);
      itemDiaryPage.userData.hitProxy = diaryHit;
      floaters.push(itemDiaryPage);

      // 일기 앞부분 메모 (남벽 안쪽)
      const memoC = mkMesh(new THREE.PlaneGeometry(0.34, 0.34), new THREE.MeshStandardMaterial({ map: Textures.memo, roughness: 0.9 }), cx + 1.5, 1.45, cz + 2.16);
      memoC.rotation.y = Math.PI;
      memoC.userData.interact = { kind: 'note', id: 'roomC' };
      interactables.push(memoC);
    }

    // ════ 옷장 (v1.2.0 재조형) ════
    // v1.1.0은 회색 박스 하나 + 가는 막대 몇 개였다. 쫓기는 와중에 한눈에
    // "저기 숨을 수 있다"를 읽어내야 하는 물건인데, 그냥 기둥처럼 보였다.
    // 문 분할선 · 경사 통풍 슬릿 · 레버형 손잡이 · 번호판 · 받침다리를 넣어
    // 명백한 '철제 사물함'으로 조형한다. (문은 로컬 −z를 향한다)
    //
    // 팩토리로 뽑아 두는 이유: 이상현상 'dupLocker'(여분의 옷장)가 진짜 옷장과
    // 똑같이 생겨야 "옷장이 하나 더 있다"로 읽힌다. v1.1.0은 복제본만 민무늬
    // 박스여서, 원본과 닮지 않아 복제라는 사실 자체가 전달되지 않았다.
    function makeLockerBody() {
      const g = new THREE.Group();
      const steel = new THREE.MeshStandardMaterial({ color: 0x2e3138, roughness: 0.45, metalness: 0.6 });
      const dark = new THREE.MeshStandardMaterial({ color: 0x0a0a0c, roughness: 0.9 });
      const chrome = new THREE.MeshStandardMaterial({ color: 0xa8adb5, roughness: 0.3, metalness: 0.85 });
      const add = (geo, mat, x, y, z) => { const m = new THREE.Mesh(geo, mat); m.position.set(x, y, z); g.add(m); return m; };

      const F = -0.45;   // 문이 있는 앞면(로컬 −z)

      // 본체
      const body = add(new THREE.BoxGeometry(0.9, 2.3, 0.9), new THREE.MeshStandardMaterial({ color: 0x24262b, roughness: 0.5, metalness: 0.55 }), 0, 1.15, 0);

      // 문짝 (본체보다 살짝 앞으로 나와 분할선이 생긴다)
      const door = add(new THREE.BoxGeometry(0.82, 2.14, 0.04), steel, 0, 1.2, F - 0.02);

      // 오목한 패널
      add(new THREE.BoxGeometry(0.7, 2.0, 0.012), new THREE.MeshStandardMaterial({ color: 0x282b31, roughness: 0.55, metalness: 0.5 }), 0, 1.2, F - 0.05);

      // 상단 통풍 슬릿 6장 (아래로 기운 살) — 안에서 내다보는 바로 그 구멍
      for (let i = 0; i < 6; i++) {
        const s = add(new THREE.BoxGeometry(0.54, 0.035, 0.03), dark, 0, 1.98 - i * 0.075, F - 0.055);
        s.rotation.x = -0.5;
      }

      // 레버형 손잡이 + 자물쇠 고리
      add(new THREE.BoxGeometry(0.07, 0.26, 0.035), chrome, 0.3, 1.18, F - 0.06);
      add(new THREE.TorusGeometry(0.035, 0.009, 5, 10), chrome, 0.3, 0.99, F - 0.06);

      // 번호판 — '사물함'이라는 결정적 기표
      add(new THREE.PlaneGeometry(0.16, 0.1), new THREE.MeshBasicMaterial({ map: Textures.plateA }), -0.2, 2.06, F - 0.06);

      // 받침 다리 4개
      [[-0.36, -0.36], [0.36, -0.36], [-0.36, 0.36], [0.36, 0.36]].forEach(([dx, dz]) => {
        add(new THREE.BoxGeometry(0.06, 0.06, 0.06), dark, dx, 0.03, dz);
      });

      g.userData.hitParts = [body, door];   // 레이캐스트로 집어야 할 면
      return g;
    }

    function buildLocker() {
      const lg = makeLockerBody();
      lg.position.set(LOCKER_POS.x, 0, LOCKER_POS.z);
      scene.add(lg);
      lockerMesh = lg;
      // 본체와 문짝 어느 쪽을 조준해도 숨을 수 있어야 한다
      lg.userData.hitParts.forEach((m) => {
        m.userData.interact = { kind: 'locker' };
        interactables.push(m);
      });
    }

    // 공포 형체를 담는 부모 슬롯. 안의 실제 형체는 등장할 때마다 무작위로 교체한다.
    // (v1.2.1: 늘 같은 모델이 나오던 문제 해결 — 위치/판정 코드는 슬롯만 참조하면 된다)
    function makeFigureSlot() {
      const slot = new THREE.Group();
      slot.userData.swap = () => {
        while (slot.children.length) slot.remove(slot.children[0]);
        const fig = makeRandomFigure();
        slot.add(fig);
        slot.userData.fig = fig;
        // 애니메이션 부위 프록시 (형체마다 없을 수 있어 애니메이션 코드는 null-가드됨)
        slot.userData.head = fig.userData.head || null;
        slot.userData.armL = fig.userData.armL || null;
        slot.userData.armR = fig.userData.armR || null;
        slot.userData.kind = fig.userData.kind;
        return fig;
      };
      slot.userData.swap();
      return slot;
    }

    function buildStalker() {
      stalkerMesh = makeFigureSlot();
      stalkerMesh.visible = false;
      scene.add(stalkerMesh);

      // 실루엣·갑툭튀용 별도 개체 (역시 무작위 형체)
      walkbyMesh = makeFigureSlot();
      walkbyMesh.visible = false;
      scene.add(walkbyMesh);
    }

    // "환자" — 병원 바디호러: 야위고 굽은 인체, 붕대 머리에 뚫린 한쪽 붉은 눈, 비대칭으로 늘어진 팔
    function makeStalkerFigure() {
      const g = new THREE.Group();
      const flesh = new THREE.MeshStandardMaterial({ color: 0x9a938a, roughness: 1.0 });      // 파리한 살
      const gown = new THREE.MeshStandardMaterial({ color: 0x6e6a63, roughness: 1.0 });        // 때 탄 환자복
      const bandage = new THREE.MeshStandardMaterial({ color: 0xb8b1a4, roughness: 1.0 });     // 붕대
      const dark = new THREE.MeshStandardMaterial({ color: 0x1a1712, roughness: 1.0 });
      const eyeMat = new THREE.MeshBasicMaterial({ color: 0xff1414 });

      // 골반 → 굽은 상체 (앞으로 수그림)
      const pelvis = new THREE.Mesh(new THREE.CylinderGeometry(0.16, 0.18, 0.3, 7), gown);
      pelvis.position.y = 0.82; g.add(pelvis);
      const torso = new THREE.Mesh(new THREE.CylinderGeometry(0.13, 0.18, 0.85, 7), gown);
      torso.position.set(0.03, 1.32, -0.05); torso.rotation.x = 0.26; g.add(torso);
      // 드러난 갈비뼈 (바디 호러)
      const ribMat = flesh;
      for (let i = 0; i < 4; i++) {
        const rib = new THREE.Mesh(new THREE.TorusGeometry(0.11 - i * 0.012, 0.012, 5, 10, Math.PI), ribMat);
        rib.position.set(0.03, 1.12 + i * 0.12, 0.08); rib.rotation.set(Math.PI / 2 + 0.26, 0, 0); g.add(rib);
      }

      // 길게 뒤틀린 목 + 수그린 머리
      const neck = new THREE.Mesh(new THREE.CylinderGeometry(0.045, 0.06, 0.5, 6), flesh);
      neck.position.set(0.05, 1.78, 0.05); neck.rotation.x = 0.5; g.add(neck);
      const head = new THREE.Mesh(new THREE.SphereGeometry(0.19, 10, 9), bandage);
      head.position.set(0.07, 1.96, 0.16); head.scale.set(0.9, 1.05, 0.95); head.rotation.x = 0.35; g.add(head);
      // 붕대 감긴 줄
      for (let i = 0; i < 3; i++) {
        const wrap = new THREE.Mesh(new THREE.TorusGeometry(0.185, 0.02, 5, 14), dark);
        wrap.position.copy(head.position); wrap.rotation.set(0.35 + (i - 1) * 0.4, 0.3, 0.2); g.add(wrap);
      }
      // 뚫린 한쪽 붉은 눈 (P.T. 원리: 결손된 얼굴)
      const eye = new THREE.Mesh(new THREE.SphereGeometry(0.045, 8, 8), eyeMat);
      eye.position.set(0.0, 1.99, 0.32); g.add(eye);
      const socket = new THREE.Mesh(new THREE.CircleGeometry(0.055, 10), new THREE.MeshBasicMaterial({ color: 0x120202 }));
      socket.position.set(0.16, 2.0, 0.3); socket.rotation.y = -0.3; g.add(socket); // 반대쪽은 검은 구멍
      // ── v1.2.0 성능 ──
      // v1.1.0은 눈마다 PointLight를 달았다. 이 함수는 3번 호출되므로(스토커/실루엣/
      // 끝의 형체) 보이지 않을 때조차 PointLight 3개가 씬에 상주하며, 모든
      // MeshStandardMaterial 픽셀이 이 3개를 매 프레임 계산했다 — 순수한 낭비다.
      // 라이트를 지우고, 반투명 발광 껍질 두 겹으로 '붉게 타는 눈'을 흉내 낸다.
      const glowMat = (o) => new THREE.MeshBasicMaterial({ color: 0xff2a2a, transparent: true, opacity: o, depthWrite: false });
      const glowA = new THREE.Mesh(new THREE.SphereGeometry(0.075, 8, 8), glowMat(0.35));
      glowA.position.copy(eye.position); g.add(glowA);
      const glowB = new THREE.Mesh(new THREE.SphereGeometry(0.12, 8, 8), glowMat(0.14));
      glowB.position.copy(eye.position); g.add(glowB);

      // 팔 — 좌우 길이가 다르고, 긴 쪽이 바닥에 끌린다 (비대칭 바디호러)
      const armL = new THREE.Group();
      const upL = new THREE.Mesh(new THREE.CylinderGeometry(0.04, 0.045, 1.15, 6), flesh); upL.position.y = -0.575; armL.add(upL);
      const handL = new THREE.Mesh(new THREE.CylinderGeometry(0.02, 0.03, 0.28, 5), flesh); handL.position.y = -1.2; armL.add(handL);
      armL.position.set(-0.2, 1.6, 0.0); armL.rotation.z = 0.14; g.add(armL);

      const armR = new THREE.Group();
      const upR = new THREE.Mesh(new THREE.CylinderGeometry(0.04, 0.045, 1.7, 6), flesh); upR.position.y = -0.85; armR.add(upR); // 훨씬 긴 팔
      const clawR = new THREE.Group();
      for (let f = 0; f < 4; f++) {
        const finger = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.018, 0.34, 4), flesh);
        finger.position.set((f - 1.5) * 0.03, -1.85, 0.02 + f * 0.006); finger.rotation.x = 0.25; armR.add(finger);
      }
      armR.position.set(0.22, 1.62, 0.0); armR.rotation.z = -0.06; g.add(armR);

      // 가늘고 뻣뻣한 다리
      const legMat = flesh;
      const legL = new THREE.Mesh(new THREE.CylinderGeometry(0.05, 0.04, 0.85, 6), legMat); legL.position.set(-0.1, 0.42, 0); g.add(legL);
      const legR = new THREE.Mesh(new THREE.CylinderGeometry(0.05, 0.04, 0.9, 6), legMat); legR.position.set(0.11, 0.4, 0.01); g.add(legR);

      g.userData.armL = armL; g.userData.armR = armR; g.userData.head = head;
      g.userData.kind = 'patient';
      return g;
    }

    // ── 공포 형체 다양화 (v1.2.1) ──
    // v1.2.0까지는 '뒤틀린 환자' 하나만 스토커·실루엣·끝의형체에 전부 재사용해,
    // 어떤 사건이 터져도 늘 같은 모델이 나왔다 → "놀래키는 게 하나뿐" 문제.
    // 실루엣부터 다른 세 종을 만들고, 등장할 때마다 무작위로 뽑는다.

    // ② 늘어진 목의 '문지기' — 비정상적으로 키가 크고, 머리가 한쪽으로 꺾여 매달린 듯하다
    function makeTallFigure() {
      const g = new THREE.Group();
      const skin = new THREE.MeshStandardMaterial({ color: 0x7d7269, roughness: 1 });
      const cloth = new THREE.MeshStandardMaterial({ color: 0x14161a, roughness: 1 });
      const dark = new THREE.MeshBasicMaterial({ color: 0x050505 });

      // 지나치게 긴 몸통 (2.6m급)
      const torso = new THREE.Mesh(new THREE.CylinderGeometry(0.14, 0.1, 1.9, 7), cloth);
      torso.position.y = 1.55; g.add(torso);
      // 툭 불거진 어깨뼈
      [-0.16, 0.16].forEach((dx) => {
        const bl = new THREE.Mesh(new THREE.SphereGeometry(0.1, 7, 6), skin);
        bl.position.set(dx, 2.35, 0); bl.scale.set(1, 0.7, 0.8); g.add(bl);
      });
      // 목이 길게 늘어나 옆으로 꺾임
      const neck = new THREE.Mesh(new THREE.CylinderGeometry(0.045, 0.05, 0.7, 6), skin);
      neck.position.set(0.12, 2.55, 0); neck.rotation.z = -0.8; g.add(neck);
      // 갸웃 꺾인 긴 얼굴
      const head = new THREE.Mesh(new THREE.CylinderGeometry(0.11, 0.08, 0.42, 8), skin);
      head.position.set(0.42, 2.7, 0); head.rotation.z = -1.2; g.add(head);
      const jaw = new THREE.Mesh(new THREE.ConeGeometry(0.08, 0.22, 6), skin);
      jaw.position.set(0.6, 2.62, 0); jaw.rotation.z = -2.0; g.add(jaw);   // 축 늘어진 턱
      // 텅 빈 눈구멍 둘
      [[-0.03, 0.06], [-0.03, -0.06]].forEach(([dy, dz]) => {
        const s = new THREE.Mesh(new THREE.SphereGeometry(0.028, 6, 6), dark);
        s.position.set(0.44, 2.74 + dy, dz); g.add(s);
      });
      // 바닥에 닿을 듯 늘어진 두 팔
      [-0.16, 0.16].forEach((dx) => {
        const arm = new THREE.Mesh(new THREE.CylinderGeometry(0.03, 0.024, 1.9, 5), skin);
        arm.position.set(dx * 1.3, 1.35, 0.05); arm.rotation.x = 0.06; g.add(arm);
        const hand = new THREE.Mesh(new THREE.CylinderGeometry(0.02, 0.008, 0.4, 5), skin);
        hand.position.set(dx * 1.35, 0.42, 0.08); g.add(hand);
      });
      // 가느다란 다리
      [-0.07, 0.07].forEach((dx) => {
        const leg = new THREE.Mesh(new THREE.CylinderGeometry(0.045, 0.03, 1.3, 6), cloth);
        leg.position.set(dx, 0.6, 0); g.add(leg);
      });
      const glow = (o, r) => { const m = new THREE.Mesh(new THREE.SphereGeometry(r, 8, 8), new THREE.MeshBasicMaterial({ color: 0xff3020, transparent: true, opacity: o, depthWrite: false })); m.position.set(0.44, 2.74, 0); g.add(m); return m; };
      glow(0.3, 0.09); glow(0.12, 0.15);
      g.userData.kind = 'tall'; g.userData.head = head;
      return g;
    }

    // ③ 네 발로 기는 '포복체' — 낮고 넓어, 실루엣만으로 사람이 아님을 안다
    function makeCrawlerFigure() {
      const g = new THREE.Group();
      const skin = new THREE.MeshStandardMaterial({ color: 0x86756a, roughness: 1 });
      const dark = new THREE.MeshBasicMaterial({ color: 0x070707 });

      // 활처럼 휜 등 (역관절)
      const spine = new THREE.Mesh(new THREE.CylinderGeometry(0.13, 0.16, 0.95, 8), skin);
      spine.position.set(0, 0.72, 0); spine.rotation.z = Math.PI / 2; g.add(spine);
      // 도드라진 등뼈 마디
      for (let i = 0; i < 6; i++) {
        const v = new THREE.Mesh(new THREE.ConeGeometry(0.04, 0.1, 5), skin);
        v.position.set(-0.4 + i * 0.16, 0.85, 0); g.add(v);
      }
      // 앞으로 쑥 내민 머리 (땅을 향해)
      const head = new THREE.Mesh(new THREE.SphereGeometry(0.15, 9, 8), skin);
      head.position.set(0.55, 0.5, 0); head.scale.set(1.3, 0.8, 0.85); g.add(head);
      const eyeM = new THREE.MeshBasicMaterial({ color: 0xff2a2a });
      [[0.66, 0.06], [0.66, -0.06]].forEach(([x, z]) => {
        const e = new THREE.Mesh(new THREE.SphereGeometry(0.022, 6, 6), eyeM);
        e.position.set(x, 0.52, z); g.add(e);
      });
      // 벌어진 입
      const mouth = new THREE.Mesh(new THREE.ConeGeometry(0.07, 0.14, 6), dark);
      mouth.position.set(0.68, 0.44, 0); mouth.rotation.z = -Math.PI / 2; g.add(mouth);
      // 역관절 네 다리 (뾰족하게 꺾여 위로 솟음)
      const legAt = (x, z) => {
        const up = new THREE.Mesh(new THREE.CylinderGeometry(0.03, 0.028, 0.55, 5), skin);
        up.position.set(x, 0.95, z); up.rotation.x = z > 0 ? -0.6 : 0.6; g.add(up);   // 무릎이 등 위로
        const low = new THREE.Mesh(new THREE.CylinderGeometry(0.024, 0.016, 0.6, 5), skin);
        low.position.set(x, 0.42, z + (z > 0 ? 0.18 : -0.18)); low.rotation.x = z > 0 ? 0.7 : -0.7; g.add(low);
      };
      legAt(0.34, 0.22); legAt(0.34, -0.22); legAt(-0.34, 0.22); legAt(-0.34, -0.22);
      g.userData.kind = 'crawler'; g.userData.head = head;
      return g;
    }

    // 무작위 공포 형체 (등장 지점의 높이·판정은 호출부에서 처리)
    const FIGURE_MAKERS = [makeStalkerFigure, makeTallFigure, makeCrawlerFigure];
    function makeRandomFigure() {
      return FIGURE_MAKERS[Math.floor(Math.random() * FIGURE_MAKERS.length)]();
    }

    function buildScareProps() {
      // B7F 정전용 붉은 눈
      blackoutEyes = new THREE.Group();
      const em = new THREE.MeshBasicMaterial({ color: 0xff1515 });
      const a = new THREE.Mesh(new THREE.SphereGeometry(0.06, 8, 8), em); a.position.x = -0.14;
      const b = new THREE.Mesh(new THREE.SphereGeometry(0.06, 8, 8), em); b.position.x = 0.14;
      blackoutEyes.add(a, b);
      blackoutEyes.position.set(0, 1.7, 0);
      blackoutEyes.visible = false;
      scene.add(blackoutEyes);
    }

    // ════════════════════════════════════════════
    // 5. 이상현상 시스템 (v1.1.0 — 회랑 / 방 / 이벤트 3계열 통합)
    // ════════════════════════════════════════════
    //
    // 설계 원칙 (v1.0.0에서 바뀐 점)
    //  1. zone: 이상현상은 회랑뿐 아니라 '방 안'에도 발생한다. 방에만 있는 경우
    //     회랑은 완벽히 정상으로 보이므로, 플레이어는 반드시 방을 점검해야 한다.
    //  2. kind='event': 잼스케어·정전·실루엣·추격 같은 '겁주는 사건'은 더 이상
    //     층 고정 스크립트가 아니라 그 자체로 이상현상이다.
    //     "튀어나왔다 = 이 층은 어긋나 있다" 규칙이 예외 없이 성립한다.
    //  3. tier: obvious(뚜렷) / subtle(미묘). 깊은 층일수록 subtle 비중이 커진다.
    //
    const ANOMALIES = {
      // ══ 회랑 · 뚜렷 ══
      mannequin:     { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { if (corridorMannequin) corridorMannequin.visible = true; } },
      lampsRed:      { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { /* 명멸은 updateWorldFX */ } },
      wheelHall:     { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { anomObj.dupWheelchair.visible = true; } },
      gurneyRoll:    { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { props.gurney.rotation.y = 0; } },
      ventEyes:      { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { anomObj.ventEyes.visible = true; } },
      endFigure:     { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { if (anomObj.endFigure.userData.swap) anomObj.endFigure.userData.swap(); anomObj.endFigure.visible = true; anomObj.endFigure.position.set(-20.5, 0, 0); } },
      portraitFace:  { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { props.portraits.forEach((p) => { p.material.map = Textures.portraitWrong; p.material.needsUpdate = true; }); } },
      hanging:       { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { anomObj.hangingFigure.visible = true; } },
      portraitWall:  { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { anomObj.portraitWall.visible = true; } },
      handPrints:    { tier: 'obvious', zone: 'corridor', kind: 'static', apply: () => { anomObj.handPrints.visible = true; } },

      // ══ 회랑 · 미묘 ══
      doorAjar:      { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { state.anomaly.doorIdx = Math.floor(Math.random() * 3); const d = doorDefs[state.anomaly.doorIdx]; if (d) d.panel.rotation.y = 0.5; } },
      lampOut:       { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { const l = corridorLamps[Math.floor(Math.random() * corridorLamps.length)]; if (l) { if (l.light) l.light.intensity = 0; l.mesh.material.color.setHex(0x1a1a1a); l._out = true; } } },
      portraitFlip:  { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { const p = props.portraits[Math.floor(Math.random() * props.portraits.length)]; if (p) p.rotation.z = Math.PI; } },
      clockWrong:    { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.clock) { props.clock.material.map = Textures.clockWrong; props.clock.material.needsUpdate = true; } } },
      clockGone:     { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.clock) props.clock.visible = false; } },
      extraDoor:     { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { anomObj.extraDoor.visible = true; } },
      exitRed:       { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.exitSign) { props.exitSign.material.map = Textures.exitRed; props.exitSign.material.needsUpdate = true; } } },
      extinGone:     { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.extinguisher) props.extinguisher.visible = false; } },
      extinCeiling:  { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.extinguisher) props.extinguisher.visible = false; anomObj.ceilExtin.visible = true; } },
      bloodTrail:    { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { anomObj.bloodTrail.visible = true; } },
      wheelMoved:    { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { props.wheelchair.position.set(0.1, 0, 11); props.wheelchair.rotation.y = Math.PI; } },
      ivBlood:       { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { props.ivBags.forEach((b) => { b.material.color.setHex(0x8a1414); b.material.opacity = 0.95; }); } },
      benchTurned:   { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.bench) props.bench.rotation.y = Math.PI; } },
      vendingRed:    { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.vendGlass) props.vendGlass.material.color.setHex(0x6e1414); } },
      cartMoved:     { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.cart) props.cart.position.set(-8.5, 0, -1.2); } },
      boardEmpty:    { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { props.boardNotes.forEach((n) => { n.visible = false; }); } },
      hydrantOpen:   { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { if (props.hydrantDoor) { props.hydrantDoor.position.z = props.hydrantDoorHomeZ + 0.22; props.hydrantDoor.rotation.y = 0.8; } } },
      wetSign:       { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { anomObj.wetSign.visible = true; } },
      dupLocker:     { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { anomObj.dupLocker.visible = true; } },
      lampsDim:      { tier: 'subtle', zone: 'corridor', kind: 'static', apply: () => { corridorLamps.forEach((l) => { l._dim = true; }); } },

      // ══ 회랑 · 이벤트 (겁주는 사건 = 어긋남의 신호) ══
      evtWalkby:     { tier: 'obvious', zone: 'corridor', kind: 'event', apply: () => {} },   // 실루엣이 회랑을 가로지른다
      evtBlackout:   { tier: 'obvious', zone: 'corridor', kind: 'event', apply: () => {} },   // 정전 + 붉은 눈
      evtPeek:       { tier: 'obvious', zone: 'corridor', kind: 'event', apply: () => {} },   // '그것'이 순간 튀어나왔다 사라진다
      evtKnock:      { tier: 'subtle',  zone: 'corridor', kind: 'event', apply: () => {} },   // 문이 안에서 두드려진다

      // ══ Room A · 병실 ══
      rA_bed:        { tier: 'obvious', zone: 'roomA', kind: 'static', apply: () => { if (props.bedSheet) { props.bedSheet.material.map = Textures.sheetOccupied; props.bedSheet.material.needsUpdate = true; } } },
      rA_extraMq:    { tier: 'obvious', zone: 'roomA', kind: 'static', apply: () => { if (anomObj.mqExtra) anomObj.mqExtra.visible = true; } },
      rA_mqFace:     { tier: 'subtle',  zone: 'roomA', kind: 'static', apply: () => { props.mqFixed.forEach((m) => { m.rotation.y = -Math.PI / 2; }); } },
      rA_ivBlood:    { tier: 'subtle',  zone: 'roomA', kind: 'static', apply: () => { if (props.roomAIvBag) { props.roomAIvBag.material.color.setHex(0x8a1414); props.roomAIvBag.material.opacity = 0.95; } } },
      rA_curtain:    { tier: 'subtle',  zone: 'roomA', kind: 'static', apply: () => { if (props.curtain) props.curtain.position.x = props.curtainHomeX + 1.15; } },

      // ══ Room B · 연산실 ══
      rB_papers:     { tier: 'obvious', zone: 'roomB', kind: 'static', apply: () => { props.papers.forEach((p) => { p.userData.floatUp = true; }); } },
      rB_chairSpin:  { tier: 'obvious', zone: 'roomB', kind: 'static', apply: () => { if (props.officeChair) props.officeChair.userData.spin = true; } },
      rB_monitor:    { tier: 'subtle',  zone: 'roomB', kind: 'static', apply: () => { if (monitorMesh) { monitorMesh.material.map = Textures.monitorWrong; monitorMesh.material.needsUpdate = true; } } },
      rB_calendar:   { tier: 'subtle',  zone: 'roomB', kind: 'static', apply: () => { if (props.calendar) { props.calendar.material.map = Textures.calendarWrong; props.calendar.material.needsUpdate = true; } } },

      // ══ Room C · 거울방 ══
      rC_figure:     { tier: 'obvious', zone: 'roomC', kind: 'static', apply: () => { if (mirrorMesh) { mirrorMesh.material.map = Textures.mirrorFigure; mirrorMesh.material.needsUpdate = true; mirrorMesh.userData.anomMirror = true; } } },
      rC_fog:        { tier: 'obvious', zone: 'roomC', kind: 'static', apply: () => { if (mirrorMesh) { mirrorMesh.material.map = Textures.mirrorFog; mirrorMesh.material.needsUpdate = true; mirrorMesh.userData.anomMirror = true; } } },
      rC_chairUp:    { tier: 'subtle',  zone: 'roomC', kind: 'static', apply: () => { if (props.fallenChair) { props.fallenChair.rotation.set(0, 1.2, 0); props.fallenChair.position.y = 0.24; } } },
      rC_sinkBlood:  { tier: 'subtle',  zone: 'roomC', kind: 'static', apply: () => { props.sinkBasins.forEach((b) => b.material.color.setHex(0x7a1a1a)); } },
      rC_towels:     { tier: 'subtle',  zone: 'roomC', kind: 'static', apply: () => { props.towels.forEach((t) => { t.visible = false; }); } }
    };

    const ANOM_IDS = Object.keys(ANOMALIES);

    // 층이 깊을수록: 이상현상 발생률 ↑, 미묘 비중 ↑, 방 이상현상 비중 ↑
    // (B1F는 언제나 정상 — 정상 기준선 학습 구간)
    // 층 낙차는 항상 -1층뿐이므로, 변별력은 오로지 '이상현상 밀도와 미묘도'가 담당한다.
    function anomalyChance(floor) {
      if (floor <= 1) return 0;
      return clamp(0.46 + (floor - 2) * 0.026, 0.46, 0.64);
    }
    function subtleRatio(floor) { return clamp(0.28 + (floor - 2) * 0.062, 0.28, 0.76); }
    function roomRatio(floor) { return floor < 4 ? 0 : clamp(0.14 + (floor - 4) * 0.05, 0.14, 0.4); }

    function rollAnomalyId(floor) {
      const wantRoom = Math.random() < roomRatio(floor);
      const wantSubtle = Math.random() < subtleRatio(floor);
      const pick = (roomFlag, tier) => ANOM_IDS.filter((id) => {
        const a = ANOMALIES[id];
        return ((a.zone !== 'corridor') === roomFlag) && a.tier === tier;
      });
      let pool = pick(wantRoom, wantSubtle ? 'subtle' : 'obvious');
      if (!pool.length) pool = pick(wantRoom, wantSubtle ? 'obvious' : 'subtle');
      if (!pool.length) pool = pick(false, 'obvious');
      return pool[Math.floor(Math.random() * pool.length)];
    }

    function applyAnomaly(id) {
      const a = ANOMALIES[id];
      const an = state.anomaly;
      an.t = 0;
      an.zone = a ? a.zone : 'corridor';
      an.kind = a ? a.kind : 'static';
      an.eventFired = false;
      // 이벤트형은 회랑 진입 후 일정 시간 뒤 발화 (즉시 터지면 관찰할 틈이 없다)
      an.eventAt = rand(4.5, 13);
      if (a) a.apply();
      lampsDirty = true;
      // 미묘한 청각 단서: 배경 드론이 아주 살짝 어긋난다 (38Hz → 41.5Hz)
      if (droneOsc && audioCtx) { try { droneOsc.frequency.setValueAtTime(41.5, audioCtx.currentTime); } catch (e) {} }
    }

    function clearAnomaly() {
      if (corridorMannequin) corridorMannequin.visible = false;
      // 문 복원 (0~2 = 회랑 쪽 문)
      doorDefs.forEach((d, i) => {
        if (i < 3) {
          d.panel.material.color.setHex(d.baseColor);
          d.panel.rotation.y = 0;
          d.plate.material.map = d.basePlate;
          d.plate.material.needsUpdate = true;
        }
        d.group.position.x = d.homeX;
        d.group.position.z = d.homeZ;
      });
      // 조명 복원
      corridorLamps.forEach((l) => {
        if (l.light) { l.light.intensity = l.baseIntensity; l.light.color.setHex(l.baseColor); }
        l.mesh.material.color.setHex(l.baseColor);
        l._out = false;
        l._dim = false;
      });
      lampsDirty = true;

      // ── 회랑 소품 복원 ──
      if (props.portraits) props.portraits.forEach((p) => { p.rotation.z = 0; p.material.map = Textures.portrait; p.material.needsUpdate = true; });
      if (props.clock) { props.clock.visible = true; props.clock.material.map = Textures.clockFace; props.clock.material.needsUpdate = true; }
      if (props.exitSign) { props.exitSign.material.map = Textures.exitGreen; props.exitSign.material.needsUpdate = true; }
      if (props.extinguisher) { props.extinguisher.visible = true; props.extinguisher.position.copy(props.extinguisherHome); }
      if (props.wheelchair) { props.wheelchair.position.copy(props.wheelchairHome); props.wheelchair.rotation.y = props.wheelchairHomeRotY; }
      if (props.gurney) { props.gurney.position.copy(props.gurneyHome); props.gurney.rotation.y = 0; }
      if (props.ivBags) props.ivBags.forEach((b) => { b.material.color.setHex(0xcfe4e8); b.material.opacity = 0.82; });
      if (props.bench) props.bench.rotation.y = props.benchHomeRotY;
      if (props.vendGlass) props.vendGlass.material.color.setHex(0x2f4f52);
      if (props.cart && props.cartHome) props.cart.position.copy(props.cartHome);
      if (props.boardNotes) props.boardNotes.forEach((n) => { n.visible = true; });
      if (props.hydrantDoor) { props.hydrantDoor.position.z = props.hydrantDoorHomeZ; props.hydrantDoor.rotation.y = 0; }

      // ── Room A 복원 ──
      if (props.bedSheet) { props.bedSheet.material.map = Textures.sheetEmpty; props.bedSheet.material.needsUpdate = true; }
      if (props.mqFixed) props.mqFixed.forEach((m, i) => { m.rotation.y = props.mqFixedHomeRotY[i]; });
      if (props.roomAIvBag) { props.roomAIvBag.material.color.setHex(0xcfe4e8); props.roomAIvBag.material.opacity = 0.82; }
      if (props.curtain) props.curtain.position.x = props.curtainHomeX;
      if (anomObj.mqExtra) anomObj.mqExtra.visible = false;

      // ── Room B 복원 ──
      if (props.papers) props.papers.forEach((p) => { p.userData.floatUp = false; p.position.y = p.userData.baseY; p.rotation.x = -Math.PI / 2; });
      if (props.officeChair) { props.officeChair.userData.spin = false; props.officeChair.rotation.y = props.officeChairHomeRotY; }
      if (props.calendar) { props.calendar.material.map = Textures.calendar; props.calendar.material.needsUpdate = true; }
      // 모니터: 퍼즐 진행 상태를 존중해 복원
      if (monitorMesh) {
        monitorMesh.material.map = state.puzzle.solved ? Textures.monitorDone : Textures.monitorIdle;
        monitorMesh.material.needsUpdate = true;
      }

      // ── Room C 복원 ──
      // 거울은 '거울 사건'(런 1회, 이상현상 아님) 이후엔 핏빛을 유지해야 한다.
      if (mirrorMesh) {
        mirrorMesh.material.map = state.flags.mirrorDone ? Textures.mirrorBlood : Textures.mirrorNormal;
        mirrorMesh.material.needsUpdate = true;
        mirrorMesh.userData.anomMirror = false;
      }
      if (props.fallenChair) { props.fallenChair.rotation.set(0, 1.2, Math.PI / 2); props.fallenChair.position.y = 0.22; }
      if (props.sinkBasins) props.sinkBasins.forEach((b) => b.material.color.setHex(0xe2ded4));
      if (props.towels) props.towels.forEach((t) => { t.visible = true; });

      // ── 이상현상 전용 객체 숨김 ──
      if (anomObj.endFigure) anomObj.endFigure.visible = false;
      if (anomObj.ventEyes) anomObj.ventEyes.visible = false;
      if (anomObj.extraDoor) anomObj.extraDoor.visible = false;
      if (anomObj.dupWheelchair) anomObj.dupWheelchair.visible = false;
      if (anomObj.bloodTrail) anomObj.bloodTrail.visible = false;
      if (anomObj.hangingFigure) anomObj.hangingFigure.visible = false;
      if (anomObj.portraitWall) anomObj.portraitWall.visible = false;
      if (anomObj.ceilExtin) anomObj.ceilExtin.visible = false;
      if (anomObj.dupLocker) anomObj.dupLocker.visible = false;
      if (anomObj.handPrints) anomObj.handPrints.visible = false;
      if (anomObj.wetSign) anomObj.wetSign.visible = false;

      // ── 이벤트형 잔재 정리 (정전 도중 층이 바뀌어도 암전이 고착되지 않도록) ──
      state.walkby.on = false;
      if (walkbyMesh) walkbyMesh.visible = false;
      state.peek.on = false;
      if (state.knock) {   // 문 두드림 진동 중이었다면 즉시 멈추고 원위치
        if (state.knock.on) { const kd = doorDefs[state.knock.doorIdx]; if (kd) { kd.group.position.x = kd.homeX; kd.group.position.z = kd.homeZ; } }
        state.knock.on = false;
      }
      state.blackout.phase = 0;
      if (blackoutEyes) blackoutEyes.visible = false;
      if (flashLight) flashLight.intensity = FLASH_ON;
      setRoomLight(state.player.room);

      if (droneOsc && audioCtx) { try { droneOsc.frequency.setValueAtTime(38, audioCtx.currentTime); } catch (e) {} }
      state.anomaly.doorIdx = -1;
    }

    function buildCorridorMannequin() {
      corridorMannequin = makeMannequinFigure();
      // 회랑 마네킹만의 표식 — 이마의 붉은 점 (방의 마네킹과 구별된다)
      const dot = new THREE.Mesh(new THREE.SphereGeometry(0.018, 6, 6), new THREE.MeshBasicMaterial({ color: 0x8f1010 }));
      dot.position.set(0, 1.76, 0.1); corridorMannequin.add(dot);
      // v1.0.0은 (0.75, -3.5) — L자 보행영역 밖이라 벽 뒤에 묻혀 보이지 않았다.
      corridorMannequin.position.set(0.85, 0, 10.5);
      corridorMannequin.visible = false;
      scene.add(corridorMannequin);
    }

    // ════════════════════════════════════════════
    // 6. 일시정지 관리자 (사유 기반 — 이중 루프/소프트락 원천 차단)
    // ════════════════════════════════════════════
    const pauseReasons = new Set();
    function isPausedAny() { return pauseReasons.size > 0; }
    function showModal(el) { if (el) { el.classList.remove('hidden'); el.classList.add('flex'); } }
    function hideModal(el) { if (el) { el.classList.add('hidden'); el.classList.remove('flex'); } }
    function openWithPause(reason, el) {
      pauseReasons.add(reason);
      showModal(el);
      if (document.pointerLockElement) document.exitPointerLock();
    }
    function closeWithResume(reason, el) {
      pauseReasons.delete(reason);
      hideModal(el);
    }

    function togglePause(e) {
      if (e) e.stopPropagation();
      if (state.phase !== 'playing') return;
      if (pauseReasons.has('menu')) {
        closeWithResume('menu', $('pause-modal'));
        $('quit-confirm-box').classList.add('hidden');
      } else {
        openWithPause('menu', $('pause-modal'));
        refreshFpsLabel();   // 마지막으로 측정된 '플레이 중' 프레임을 보여준다
      }
    }
    function toggleInventory(e) {
      if (e) e.stopPropagation();
      if (state.phase !== 'playing') return;
      if (pauseReasons.has('inventory')) closeInventory();
      else if (pauseReasons.size === 0) {
        refreshInventoryUI();
        openWithPause('inventory', $('inventory-modal'));
      }
    }
    function closeInventory(e) { if (e) e.stopPropagation(); closeWithResume('inventory', $('inventory-modal')); }
    function closePuzzleModal(e) { if (e) e.stopPropagation(); closeWithResume('puzzle', $('puzzle-modal')); }
    function closeKeypadModal(e) { if (e) e.stopPropagation(); closeWithResume('keypad', $('keypad-modal')); }
    function closeNoteModal(e) { if (e) e.stopPropagation(); closeWithResume('note', $('note-modal')); }
    function confirmQuit(e) { if (e) e.stopPropagation(); $('quit-confirm-box').classList.remove('hidden'); }
    function cancelQuit(e) { if (e) e.stopPropagation(); $('quit-confirm-box').classList.add('hidden'); }

    // ════════════════════════════════════════════
    // 7. 텍스트 데이터 (기억/메모/기록)
    // ════════════════════════════════════════════
    const itemData = {
      glasses: { title: '깨진 안경', desc: '왼쪽 렌즈에 금이 간 안경. 마네킹들 발치에 놓여 있었다. 흐려진 시야를 핑계로 그날 눈을 감아버렸던 자책 — 이제는 금 간 렌즈 너머라도 똑바로 본다.' },
      clock: { title: '멈춘 회중시계', desc: '바늘이 4시 44분에 얼어붙은 회중시계. 회랑의 모든 시계가 가리키는 바로 그 시각. 동조를 마친 지금, 초침이 아주 미세하게 떨리기 시작했다.' },
      diary: { title: '찢어진 일기장', desc: '거울이 깨지며 떨어진 뒷장. 앞장의 절망과 달리, 뒷장에는 눌러쓴 한 줄이 남아 있다 — "나도 살고 싶었어. 살려줘." 무의식 가장 깊은 곳의 생존 신호.' },
      band: { title: '환자 인식 팔찌', desc: '제4병동의 환자 인식 팔찌. 이름 칸은 닳아 지워졌지만, 손목 둘레가 낯설지 않다. 침대에 누워 있는 사람이 누구인지, 이제는 인정할 수 있다.' }
    };

    const NOTES = {
      corridor: { kicker: '낡은 안내문', title: '관리인의 경고', body: '낯익음이 완벽할 때만 나아가라.\n무엇 하나라도 어긋나 있다면 — 조명이든, 문이든,\n서 있지 말아야 할 것이 서 있든 —\n뒤돌아 회귀하라.\n\n그것은 어긋남 속에서만 눈을 뜬다.' },
      roomB: { kicker: '구겨진 처방전 뒷면', title: '떨리는 글씨', body: '또 그 시간에 멈췄다. 병실의 벽시계도,\n복도의 시계도, 전부 같은 시간에.\n\n그날의 시간이 모든 잠금을 연다.\n네 자리. 잊고 싶어도 잊히지 않는.' },
      roomC: { kicker: '찢겨나간 페이지', title: '일기장 — 앞부분', body: '…거울을 볼 수가 없다.\n그 애가 아직 거기 서 있을까 봐.\n\n미안하다는 말은 유리 저편까지 닿지 않는다.\n하지만 뒷장은 아직 찢기지 않았다.\n아직, 쓸 수 있다.' }
    };

    const LORE = {
      clock: { kicker: '벽시계', title: '멈춘 시침', body: '4시 44분.\n초침은 죽어 있고, 유리에는 가는 금이 가 있다.\n\n이 회랑의 모든 시계는 같은 시간을 가리킨다.' },
      poster: { kicker: '빛바랜 게시물', title: '제4병동 안내', body: '면회 시간을 엄수해 주십시오.\n중환자 구역 — 관계자 외 출입 금지.\n\n…이 회랑은 어느 병원의 복도를 닮아 있다.\n지나치게.' },
      drawing: { kicker: '벽에 붙은 종이', title: '아이의 낙서', body: '크레파스로 그린 세 사람.\n한 명의 얼굴 위에만 검은 선이\n몇 번이고 덧그어져 있다.\n\n뒷면에는 서툰 글씨 — "미안해".' },
      computerDone: { kicker: '단말기', title: 'SYNC COMPLETE', body: '주파수는 이미 겹쳐졌다.\n화면에는 초록 잔광만이 맴돌고,\n구석에 작게 04:44 가 깜빡인다.' },
      drawerEmpty: { kicker: '열린 서랍', title: '비어 있는 안쪽', body: '팔찌가 놓여 있던 자리에\n손목 모양의 옅은 자국만 남아 있다.' },
      portrait: { kicker: '벽에 걸린 초상', title: '누구의 얼굴', body: '흐릿하게 번진 인물 사진.\n볼 때마다 눈매가 조금씩 다른 것 같다.\n\n…분명 어제는 이쪽을 보고 있지 않았다.' },
      vending: { kicker: '자판기', title: '품절', body: '모든 칸에 붉은 SOLD OUT 램프가 켜져 있다.\n동전 반환구에 손을 넣자, 차갑고 축축한 것이 닿는다.\n\n꺼내 보지 않는 편이 낫겠다.' },
      bed: { kicker: '병상', title: '비어 있는 침대', body: '시트는 팽팽하게 당겨져 있고,\n베개에는 눌린 자국조차 없다.\n\n…지금은.' },
      calendar: { kicker: '벽 달력', title: '4월', body: '어느 날짜 하나에만 붉은 동그라미.\n무슨 날이었는지는 적혀 있지 않다.\n\n그날 이후의 칸은 전부 비어 있다.' },
      mirror: { kicker: '전신 거울', title: '유리 저편', body: '거울 속의 당신은 조금 늦게 움직인다.\n아주 조금.\n\n눈을 깜빡이면, 저쪽이 먼저 깜빡인 것 같다.' }
    };

    // ════════════════════════════════════════════
    // 8. HUD / 배너 / 연출 헬퍼
    // ════════════════════════════════════════════
    let bannerTimer = null;
    function showBanner(text, ms) {
      const b = $('event-banner');
      $('event-banner-text').innerText = text;
      b.classList.add('show');
      if (bannerTimer) clearTimeout(bannerTimer);
      bannerTimer = setTimeout(() => b.classList.remove('show'), ms || 2300);
    }
    function showFlashGlitch(opacity) {
      const g = $('glitch-overlay');
      g.style.backgroundColor = 'rgba(153, 27, 27, ' + opacity + ')';
      setTimeout(() => { g.style.backgroundColor = 'rgba(153, 27, 27, 0)'; }, 150);
    }
    function fadePulse(midFn, lock) {
      if (lock) state.transitioning = true;
      $('fade-overlay').classList.add('on');
      setTimeout(() => {
        if (midFn) midFn();
        setTimeout(() => $('fade-overlay').classList.remove('on'), 140);
        if (lock) setTimeout(() => { state.transitioning = false; }, 380);
      }, 180);
    }
    function updateHUDLocation() { $('hud-location').innerText = ROOM_NAMES[state.player.room] || '???'; }
    function updateHUDLoop() { $('loop-counter').innerText = 'B' + state.loopCount + 'F'; }
    // 이번 층에서 어떤 방을 확인했는지 — 어긋남은 방 안에도 숨어 있다
    function updateHUDRooms() {
      [['roomA', 'hud-room-a'], ['roomB', 'hud-room-b'], ['roomC', 'hud-room-c']].forEach(([key, id]) => {
        const el = $(id);
        if (!el) return;
        if (state.roomsSeen[key]) el.className = 'px-1.5 rounded border border-cyan-800 bg-cyan-950/40 text-cyan-300';
        else el.className = 'px-1.5 rounded border border-neutral-800 text-neutral-600';
      });
    }
    function updateHUDPosture() {
      const p = state.player;
      $('hud-posture').innerText = p.inLocker ? (p.crouched ? '옷장 은신 (완전)' : '옷장 (노출!)') : (p.crouched ? '앉음' : '서 있음');
      const lbl = $('touch-crouch-label');
      if (lbl) lbl.innerText = p.crouched ? '일어서기' : '앉기';
      $('touch-crouch-icon-down').classList.toggle('hidden', p.crouched);
      $('touch-crouch-icon-up').classList.toggle('hidden', !p.crouched);
      const st = $('locker-hide-status');
      const sub = $('locker-hide-sub');
      const led = $('locker-led');
      if (st && sub && led) {
        if (p.crouched) {
          st.innerText = '완전히 숨었습니다';
          st.className = 'text-sm font-bold text-cyan-300';
          sub.innerText = '숨을 죽이고 문틈 너머를 살피십시오';
          led.className = 'w-2 h-2 rounded-full bg-cyan-400 shadow-[0_0_8px_rgba(34,211,238,0.9)]';
        } else {
          st.innerText = '머리가 슬릿 위로 나와 있습니다';
          st.className = 'text-sm font-bold text-amber-300';
          sub.innerText = '[Ctrl] 웅크려야 완전히 가려집니다';
          led.className = 'w-2 h-2 rounded-full bg-amber-400 shadow-[0_0_8px_rgba(251,191,36,0.9)] animate-pulse';
        }
      }
    }
    function updateHRDisplay() {
      const shown = Math.round(state.hr.current);
      if (shown === state.hr.shown) return;
      state.hr.shown = shown;
      $('heart-rate-text').innerText = shown + ' BPM';
      $('heart-rate-bar').style.width = clamp(((shown - 55) / 115) * 100, 8, 100) + '%';
    }
    function recalcSync() {
      const inv = state.inventory;
      const n = ['glasses', 'clock', 'diary', 'band'].filter((k) => inv[k]).length;
      const pct = Math.floor((n / 4) * 100);
      $('sync-text').innerText = pct + '%';
      $('sync-bar').style.width = pct + '%';
      $('inv-progress').innerText = n + ' / 4';
    }
    function collectItem(id) {
      if (state.inventory[id]) return;
      state.inventory[id] = true;
      const st = $('item-status-' + id);
      if (st) { st.innerText = '회수 완료'; st.className = 'text-[10px] text-cyan-400 mt-1 uppercase tracking-wider'; }
      if (id === 'glasses' && itemGlasses) { itemGlasses.visible = false; itemGlasses.userData.hitProxy.visible = false; }
      if (id === 'diary' && itemDiaryPage) { itemDiaryPage.visible = false; itemDiaryPage.userData.hitProxy.visible = false; }
      playChime();
      showFlashGlitch(0.3);
      showBanner('기억 회수 — ' + itemData[id].title);
      recalcSync();
      saveProgress();
    }
    function openNote(id, counted) {
      const src = counted ? NOTES[id] : LORE[id];
      if (!src) return;
      $('note-kicker').innerText = src.kicker;
      $('note-title').innerText = src.title;
      $('note-body').innerText = src.body;
      if (counted && !state.notesRead[id]) { state.notesRead[id] = true; }
      playSynth(300, 0.2, 'triangle', 0.06);
      openWithPause('note', $('note-modal'));
    }

    // ════════════════════════════════════════════
    // 9. 조작 (키보드 / 마우스 / 터치 멀티포인트)
    // ════════════════════════════════════════════
    const keysPressed = {};
    const MOUSE_SENS = 0.0025;
    let isPointerLocked = false;
    let isDragging = false;
    let dragMoved = 0;
    let prevMouseX = 0, prevMouseY = 0;
    let lookTouchId = null, lookPrevX = 0, lookPrevY = 0;
    let joyTouchId = null, joyOrigin = { x: 0, y: 0 }, joyDir = { x: 0, y: 0 };
    let guideHidden = false;
    let controlsBound = false;

    function hideGuide() {
      if (guideHidden) return;
      guideHidden = true;
      $('pointer-lock-guide').classList.add('opacity-0');
    }
    function resetGuide() {
      guideHidden = false;
      $('pointer-lock-guide').classList.remove('opacity-0');
    }
    function canPlayInput() { return state.phase === 'playing' && !isPausedAny() && !state.player.dead; }

    function applyLook(dx, dy) {
      const p = state.player;
      p.rotY -= dx;
      p.rotX = clamp(p.rotX - dy, -Math.PI / 2.3, Math.PI / 2.3);
      if (p.inLocker) {
        // v1.1.0의 ±0.55rad(≈31°)는 지나치게 좁아 조작이 답답했다.
        // ±1.15rad(≈66°)로 넓혀, 문틈 너머 회랑을 좌우로 훑어볼 수 있게 한다.
        // (완전 자유 회전은 아니다 — 옷장 안이라는 감각은 남긴다)
        p.rotY = clamp(p.rotY, -1.15, 1.15);
        p.rotX = clamp(p.rotX, -0.7, 0.55);
      }
    }

    function setupControls() {
      if (controlsBound) return;
      controlsBound = true;
      const canvas3d = $('three-canvas');

      canvas3d.addEventListener('contextmenu', (e) => e.preventDefault());

      canvas3d.addEventListener('click', () => {
        if (!canPlayInput()) return;
        if (dragMoved > 6) return; // 드래그 후 클릭 오발동 방지
        if (!IS_TOUCH && !isPointerLocked && canvas3d.requestPointerLock) {
          try {
            const r = canvas3d.requestPointerLock();
            if (r && r.catch) r.catch(() => {});
            return;
          } catch (err) {
            // 포인터락 미지원/차단 환경 → 클릭을 상호작용으로 사용
          }
        }
        attemptInteract();
      });

      document.addEventListener('pointerlockchange', () => {
        isPointerLocked = (document.pointerLockElement === canvas3d);
        if (isPointerLocked) hideGuide();
      });

      canvas3d.addEventListener('mousedown', (e) => {
        if (!canPlayInput()) return;
        isDragging = true; dragMoved = 0;
        prevMouseX = e.clientX; prevMouseY = e.clientY;
      });
      window.addEventListener('mouseup', () => { isDragging = false; });
      window.addEventListener('mousemove', (e) => {
        if (!canPlayInput()) return;
        const s = MOUSE_SENS * settings.sensitivity;
        if (isPointerLocked) {
          applyLook(e.movementX * s, e.movementY * s);
        } else if (isDragging) {
          const dx = e.clientX - prevMouseX, dy = e.clientY - prevMouseY;
          dragMoved += Math.abs(dx) + Math.abs(dy);
          applyLook(dx * s * 1.5, dy * s * 1.5);
          prevMouseX = e.clientX; prevMouseY = e.clientY;
          if (dragMoved > 10) hideGuide();
        }
      });

      // ── 터치: 식별자 추적으로 멀티터치 완전 지원 ──
      canvas3d.addEventListener('touchstart', (e) => {
        if (!canPlayInput()) return;
        for (const t of e.changedTouches) {
          if (lookTouchId === null && t.clientX > window.innerWidth * 0.5) {
            lookTouchId = t.identifier;
            lookPrevX = t.clientX; lookPrevY = t.clientY;
          }
        }
      }, { passive: true });
      canvas3d.addEventListener('touchmove', (e) => {
        if (!canPlayInput()) return;
        for (const t of e.changedTouches) {
          if (t.identifier === lookTouchId) {
            const s = 0.0065 * settings.sensitivity;
            applyLook((t.clientX - lookPrevX) * s, (t.clientY - lookPrevY) * s);
            lookPrevX = t.clientX; lookPrevY = t.clientY;
            hideGuide();
          }
        }
      }, { passive: true });
      const endLook = (e) => {
        for (const t of e.changedTouches) {
          if (t.identifier === lookTouchId) lookTouchId = null;
        }
      };
      canvas3d.addEventListener('touchend', endLook);
      canvas3d.addEventListener('touchcancel', endLook);

      // ── 키보드 ──
      window.addEventListener('keydown', (e) => {
        const key = e.key.toLowerCase();
        // 게임 키의 브라우저 기본동작 차단 (Ctrl+W 탭닫기, Ctrl+S 저장 등 최대한 억제)
        if (['w', 'a', 's', 'd', 'arrowup', 'arrowdown', 'arrowleft', 'arrowright', ' '].includes(key)) e.preventDefault();
        if (e.ctrlKey && ['w', 's', 'a', 'd'].includes(key)) e.preventDefault();

        // 키패드 모달 입력 라우팅
        if (pauseReasons.has('keypad')) {
          if (/^[0-9]$/.test(e.key)) keypadPress(e.key);
          else if (e.key === 'Backspace') keypadPress('del');
          else if (e.key === 'Enter') keypadPress('ok');
          else if (e.key === 'Escape') closeKeypadModal();
          return;
        }
        if (e.key === 'Escape') {
          if (pauseReasons.has('note')) return closeNoteModal();
          if (pauseReasons.has('puzzle')) return closePuzzleModal();
          if (pauseReasons.has('inventory')) return closeInventory();
          return togglePause();
        }
        if (key === 'i' && !e.repeat) return toggleInventory();
        if (key === 'e' && !e.repeat) {
          if (pauseReasons.has('note')) return closeNoteModal();
          if (isPausedAny()) return;
          return attemptInteract();
        }
        if ((e.key === 'Control' || key === 'c') && !e.repeat) {
          e.preventDefault();
          if (canPlayInput()) toggleCrouch();
          return;
        }
        keysPressed[key] = true;
      });
      window.addEventListener('keyup', (e) => { keysPressed[e.key.toLowerCase()] = false; });
      window.addEventListener('blur', () => {
        for (const k in keysPressed) keysPressed[k] = false;
        isDragging = false;
      });

      // ── 가상 조이스틱 (터치 전용, 식별자 추적) ──
      const zone = $('touch-joystick-zone');
      zone.addEventListener('touchstart', (e) => {
        if (!canPlayInput() || joyTouchId !== null) return;
        const t = e.changedTouches[0];
        joyTouchId = t.identifier;
        joyOrigin.x = t.clientX; joyOrigin.y = t.clientY;
        const base = $('joystick-base');
        const rect = zone.getBoundingClientRect();
        base.style.left = (t.clientX - rect.left - 48) + 'px';
        base.style.top = (t.clientY - rect.top - 48) + 'px';
        base.classList.remove('hidden');
      }, { passive: true });
      window.addEventListener('touchmove', (e) => {
        if (joyTouchId === null) return;
        for (const t of e.changedTouches) {
          if (t.identifier !== joyTouchId) continue;
          const dx = t.clientX - joyOrigin.x, dy = t.clientY - joyOrigin.y;
          const dist = Math.hypot(dx, dy), lim = 45;
          const mx = dist > lim ? (dx / dist) * lim : dx;
          const my = dist > lim ? (dy / dist) * lim : dy;
          $('joystick-stick').style.transform = 'translate(calc(-50% + ' + mx + 'px), calc(-50% + ' + my + 'px))';
          joyDir.x = mx / lim; joyDir.y = -my / lim;
        }
      }, { passive: true });
      const endJoy = (e) => {
        for (const t of e.changedTouches) {
          if (t.identifier === joyTouchId) {
            joyTouchId = null; joyDir.x = 0; joyDir.y = 0;
            $('joystick-base').classList.add('hidden');
            $('joystick-stick').style.transform = 'translate(-50%, -50%)';
          }
        }
      };
      window.addEventListener('touchend', endJoy);
      window.addEventListener('touchcancel', endJoy);

      // ── 화면 액션 버튼 (마우스/터치 공용: Pointer Events) ──
      $('touch-interact').addEventListener('pointerdown', (e) => {
        e.preventDefault();
        if (pauseReasons.has('note')) return closeNoteModal();
        if (canPlayInput()) attemptInteract();
      });
      const btnSprint = $('touch-sprint');
      btnSprint.addEventListener('pointerdown', (e) => {
        e.preventDefault();
        state.player.sprinting = true;
        btnSprint.classList.add('bg-orange-800');
      });
      const sprintOff = () => { state.player.sprinting = false; btnSprint.classList.remove('bg-orange-800'); };
      btnSprint.addEventListener('pointerup', sprintOff);
      btnSprint.addEventListener('pointerleave', sprintOff);
      btnSprint.addEventListener('pointercancel', sprintOff);
      $('touch-crouch').addEventListener('pointerdown', (e) => {
        e.preventDefault();
        if (canPlayInput()) toggleCrouch();
      });
    }

    function toggleCrouch() {
      const p = state.player;
      p.crouched = !p.crouched;
      const btn = $('touch-crouch');
      btn.classList.toggle('bg-blue-800', p.crouched);
      playSynth(p.crouched ? 90 : 130, 0.15, 'triangle', 0.05);
      updateHUDPosture();
    }

    // ════════════════════════════════════════════
    // 10. 레이캐스트 상호작용
    // ════════════════════════════════════════════
    const raycaster = new THREE.Raycaster();
    raycaster.far = 3.2;                     // 상호작용 사거리 밖은 애초에 검사하지 않는다
    const screenCenter = new THREE.Vector2(0, 0);
    let targetInteract = null; // { mesh, info }
    // 매 호출마다 filter/concat으로 새 배열을 두 개씩 만들던 것을 재사용 버퍼로 교체
    const _rayPool = [];
    const _camDir = new THREE.Vector3();
    const _toMq = new THREE.Vector3();

    function isWorldVisible(m) {
      let o = m;
      while (o) { if (o.visible === false) return false; o = o.parent; }
      return true;
    }

    // 사거리(3.2m) 밖 오브젝트는 레이캐스트 후보에서 제외 — 방 3개가 200m 밖에 있으므로
    // 회랑에 있을 때 방 안 오브젝트 수십 개를 매번 검사하던 낭비가 사라진다.
    const _wp = new THREE.Vector3();
    function buildRayPool() {
      _rayPool.length = 0;
      const p = state.player;
      const R2 = 16; // 4m² 여유 (3.2m 사거리 + 오브젝트 크기)
      for (let i = 0; i < interactables.length; i++) {
        const m = interactables[i];
        if (!isWorldVisible(m)) continue;
        // v1.2.1 치명 버그 수정: 문의 frame/panel/knob/plate는 door 그룹의 '자식'이라
        // m.position이 로컬 좌표(≈원점)다. 이걸 그대로 플레이어와 비교하면 방쪽 문이
        // 언제나 수백 m 밖으로 계산돼 레이풀에서 제외됐다 → 방에서 나갈 수 없었다.
        // 반드시 월드 좌표로 거리 필터를 건다.
        m.getWorldPosition(_wp);
        const dx = _wp.x - p.x, dz = _wp.z - p.z;
        if (dx * dx + dz * dz > R2 * R2) continue;
        _rayPool.push(m);
      }
      for (let i = 0; i < blockers.length; i++) _rayPool.push(blockers[i]);
      return _rayPool;
    }

    function checkRaycast() {
      const prompt = $('interaction-prompt');
      const cross = $('crosshair');
      const btn = $('touch-interact');

      if (state.player.inLocker) {
        targetInteract = null;
        prompt.classList.add('hidden');
        btn.classList.remove('opacity-60');
        btn.classList.add('ring-2', 'ring-cyan-500');
        return;
      }

      raycaster.setFromCamera(screenCenter, camera);
      const hits = raycaster.intersectObjects(buildRayPool(), false);

      targetInteract = null;
      if (hits.length > 0 && hits[0].distance < 3.0 && hits[0].object.userData.interact) {
        targetInteract = { mesh: hits[0].object, info: hits[0].object.userData.interact };
      }

      if (targetInteract) {
        prompt.innerText = promptTextFor(targetInteract.info);
        prompt.classList.remove('hidden');
        cross.classList.add('scale-150', 'bg-cyan-400');
        cross.classList.remove('bg-white');
        btn.classList.remove('opacity-60');
        btn.classList.add('ring-2', 'ring-cyan-500');
      } else {
        prompt.classList.add('hidden');
        cross.classList.remove('scale-150', 'bg-cyan-400');
        cross.classList.add('bg-white');
        btn.classList.add('opacity-60');
        btn.classList.remove('ring-2', 'ring-cyan-500');
      }
    }

    function promptTextFor(info) {
      switch (info.kind) {
        case 'door':
          return state.player.room === 'corridor' ? '[방 ' + info.letter + '] 문 열기 — E / 클릭' : '[회랑으로] 문 열기 — E / 클릭';
        case 'locker': return '옷장에 숨기 — E / 클릭';
        case 'item': return '기억 회수 — ' + (itemData[info.id] ? itemData[info.id].title : '') + ' [E]';
        case 'computer': return state.puzzle.solved ? '단말기 확인 [E]' : '기억 동조기 부팅 [E]';
        case 'keypad': return state.keypad.solved ? '열린 서랍 확인 [E]' : '잠긴 서랍 — 키패드 [E]';
        case 'note': return '메모 읽기 [E]';
        case 'lore': return '살펴보기 [E]';
        default: return '상호작용 [E]';
      }
    }

    function attemptInteract() {
      const p = state.player;
      if (isPausedAny() || state.phase !== 'playing' || p.dead || state.transitioning) return;

      // 옷장 탈출은 조준 불문 최우선
      if (p.inLocker) {
        p.inLocker = false;
        p.crouched = false;               // 옷장에서 나오면 웅크리기 자동 해제
        const cbtn = $('touch-crouch');
        if (cbtn) cbtn.classList.remove('bg-blue-800');
        document.body.classList.remove('in-locker');
        $('locker-hint').classList.add('hidden');
        // v1.1.0은 옷장 옆(x−0.9)으로 밀어내고 rotY=−π/2(=+x, 우벽)를 보게 해서
        // 나오자마자 벽을 코앞에서 마주보는 꼴이었다.
        // 옷장 문은 −z를 향하므로, 문 앞으로 한 걸음 나와 그대로 −z(회랑)를 본다.
        p.x = LOCKER_POS.x; p.z = LOCKER_POS.z - 1.0;
        p.rotY = 0; p.rotX = 0;           // 정면·수평
        playLockerDoor(false);
        updateHUDPosture();
        return;
      }
      if (!targetInteract) return;
      const info = targetInteract.info;

      if (info.kind === 'door') {
        playSynth(130, 0.3, 'sine', 0.1);
        const tp = DOOR_TELEPORT[info.room];
        fadePulse(() => {
          if (p.room === 'corridor') {
            p.room = info.room;
            p.x = tp.into[0]; p.z = tp.into[1];
            p.rotY = tp.rotIn;   // 방 안쪽을 바라보며 들어선다
            p.rotX = 0;          // 시선은 항상 수평으로 (고개가 젖혀진 채 넘어가지 않도록)
            // 이 층에서 이 방을 확인했다고 기록
            if (!state.roomsSeen[info.room]) {
              state.roomsSeen[info.room] = true;
              updateHUDRooms();
            }
          } else {
            p.room = 'corridor';
            p.x = tp.out[0]; p.z = tp.out[1];
            p.rotY = tp.rotOut;  // 회랑 안쪽을 바라보며 나선다 (문/벽을 마주보지 않는다)
            p.rotX = 0;
          }
          setRoomLight(p.room);  // 공유 조명을 현재 방으로 이동
          updateHUDLocation();
        }, true);
      }
      else if (info.kind === 'locker') {
        p.inLocker = true;
        p.crouched = true;   // 들어가면 자동으로 웅크려 은신 성립 (노출 방지)
        document.body.classList.add('in-locker');
        $('locker-hint').classList.remove('hidden');
        p.x = LOCKER_POS.x; p.z = LOCKER_POS.z;
        p.rotY = 0; p.rotX = 0;
        // v1.1.0은 여기서 showFlashGlitch(0.25)로 화면을 붉게 물들였다.
        // 붉은 섬광은 이 게임에서 '피격/공포 신호'로 쓰이는 색이라,
        // 안전한 은신처에 들어가는 행동에 붙으면 오독을 부른다 → 제거.
        // 대신 철제 문이 닫히는 소리로 '들어왔다'를 알린다.
        playLockerDoor(true);
        updateHUDPosture();
      }
      else if (info.kind === 'item') collectItem(info.id);
      else if (info.kind === 'computer') {
        if (state.puzzle.solved) openNote('computerDone', false);
        else openTuningPuzzle();
      }
      else if (info.kind === 'keypad') {
        if (state.keypad.solved) openNote('drawerEmpty', false);
        else openKeypad();
      }
      else if (info.kind === 'note') openNote(info.id, true);
      else if (info.kind === 'lore') openNote(info.id, false);
    }

    // ════════════════════════════════════════════
    // 11. 퍼즐 A — 파형 동조 (Room B 모니터)
    // ════════════════════════════════════════════
    function openTuningPuzzle() {
      const pz = state.puzzle;
      pz.t1 = 25 + Math.floor(Math.random() * 56); // 25~80
      pz.t2 = 18 + Math.floor(Math.random() * 58); // 18~75
      pz.v1 = 10; pz.v2 = 90; pz.solved = false;
      $('puzzle-slider-1').value = 10;
      $('puzzle-slider-2').value = 90;
      $('puzzle-success-text').classList.add('hidden');
      drawPuzzleWaves();
      openWithPause('puzzle', $('puzzle-modal'));
    }

    function drawPuzzleWaves() {
      const pz = state.puzzle;
      let dT = 'M 0 30', dC = 'M 0 30';
      for (let x = 0; x <= 200; x += 2) {
        const yT = 30 + Math.sin(x * (pz.t1 / 15) * 0.1) * (pz.t2 / 3) * 0.4;
        const yC = 30 + Math.sin(x * (pz.v1 / 15) * 0.1) * (pz.v2 / 3) * 0.4;
        dT += ' L ' + x + ' ' + yT.toFixed(1);
        dC += ' L ' + x + ' ' + yC.toFixed(1);
      }
      $('wave-target').setAttribute('d', dT);
      $('wave-current').setAttribute('d', dC);
      $('slider-val-1').innerText = pz.v1;
      $('slider-val-2').innerText = pz.v2;

      if (!pz.solved && Math.abs(pz.v1 - pz.t1) <= 4 && Math.abs(pz.v2 - pz.t2) <= 4) {
        pz.solved = true;
        $('puzzle-success-text').classList.remove('hidden');
        if (monitorMesh) { monitorMesh.material.map = Textures.monitorDone; monitorMesh.material.needsUpdate = true; }
        collectItem('clock');
        setTimeout(() => closePuzzleModal(), 1200);
      }
    }

    // ════════════════════════════════════════════
    // 12. 퍼즐 B — 키패드 서랍 (암호 0444)
    // ════════════════════════════════════════════
    const KEYPAD_CODE = '0444';
    function buildKeypadButtons() {
      const grid = $('keypad-grid');
      const keys = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'del', '0', 'ok'];
      keys.forEach((k) => {
        const b = document.createElement('button');
        if (k === 'del') { b.innerText = '지움'; b.className = 'py-3.5 bg-neutral-900 hover:bg-neutral-800 text-neutral-400 text-sm font-bold rounded-xl border border-neutral-800 transition-colors active:scale-95'; }
        else if (k === 'ok') { b.innerText = '확인'; b.className = 'py-3.5 bg-amber-900/40 hover:bg-amber-800/50 text-amber-300 text-sm font-bold rounded-xl border border-amber-900/50 transition-colors active:scale-95'; }
        else { b.innerText = k; b.className = 'py-3.5 bg-neutral-900 hover:bg-neutral-800 text-neutral-200 text-lg font-bold rounded-xl border border-neutral-800 transition-colors active:scale-95'; }
        b.addEventListener('click', (e) => { e.stopPropagation(); keypadPress(k); });
        grid.appendChild(b);
      });
    }
    function openKeypad() {
      state.keypad.input = '';
      refreshKeypadDisplay(false);
      openWithPause('keypad', $('keypad-modal'));
    }
    function refreshKeypadDisplay(errorFlash) {
      const d = $('keypad-display');
      const s = state.keypad.input;
      d.innerText = (s + '····').slice(0, 4).split('').map((c, i) => i < s.length ? c : '·').join('');
      d.classList.toggle('text-red-400', !!errorFlash);
      d.classList.toggle('text-amber-300', !errorFlash);
    }
    function keypadPress(k) {
      const kp = state.keypad;
      if (kp.solved) return;
      if (k === 'del') { kp.input = kp.input.slice(0, -1); refreshKeypadDisplay(false); playSynth(200, 0.06, 'triangle', 0.05); return; }
      if (k === 'ok') {
        if (kp.input === KEYPAD_CODE) {
          kp.solved = true;
          if (drawerMesh) drawerMesh.position.z += 0.3; // 서랍 개방
          playChime();
          showBanner('서랍이 열렸다');
          collectItem('band');
          setTimeout(() => closeKeypadModal(), 850);
        } else {
          playBuzz();
          refreshKeypadDisplay(true);
          setTimeout(() => { kp.input = ''; refreshKeypadDisplay(false); }, 450);
        }
        return;
      }
      if (kp.input.length < 4) { kp.input += k; refreshKeypadDisplay(false); playSynth(420, 0.05, 'square', 0.04); }
    }

    // ════════════════════════════════════════════
    // 13. 루프 / 게이트 / 이상현상 롤
    // ════════════════════════════════════════════
    function setupLoop(n) {
      state.loopCount = n;
      state.loopTime = 0;
      const p = state.player;
      p.x = SPAWN.x; p.z = SPAWN.z; p.rotX = 0; p.rotY = 0;
      p.room = 'corridor'; p.dead = false;
      if (p.inLocker) {
        p.inLocker = false;
        document.body.classList.remove('in-locker');
        $('locker-hint').classList.add('hidden');
      }
      deactivateStalker();
      state.flags.mannequinAway = false;
      if (roomMannequin) {
        roomMannequin.position.set(roomMannequinHome.x, 0, roomMannequinHome.z);
        roomMannequin.rotation.y = 0.8;
      }
      state.walkby.on = false;
      if (walkbyMesh) walkbyMesh.visible = false;
      state.peek.on = false;
      state.blackout.phase = 0;

      // 층마다 방 점검 기록 초기화 — 어긋남은 방 안에도 있다
      state.roomsSeen = { roomA: false, roomB: false, roomC: false };
      updateHUDRooms();

      // 이상현상 롤 (B1F는 항상 정상 — 기준 학습 구간)
      clearAnomaly();
      state.anomaly.active = false; state.anomaly.id = '';
      state.anomaly.zone = 'corridor'; state.anomaly.kind = 'static';
      state.anomaly.eventFired = false;
      if (Math.random() < anomalyChance(n)) {
        state.anomaly.active = true;
        state.anomaly.id = rollAnomalyId(n);
        applyAnomaly(state.anomaly.id);
      }

      // 방 이상현상이 처음 가능해지는 층에서 1회 안내
      if (n >= 4 && !state.roomHintShown) {
        state.roomHintShown = true;
        setTimeout(() => {
          if (state.phase === 'playing') showBanner('어긋남은 회랑에만 있지 않다 — 방을 꼼꼼히 살펴라', 4200);
        }, 1400);
      }

      // 루프당 환경음 (순수 분위기 — 판정과 무관)
      // 'knock'은 이상현상 evtKnock과 헷갈리므로 환경음 풀에서 제외한다.
      if (Math.random() < 0.55) {
        const kinds = ['whisper', 'steps', 'static', 'bend'];
        state.ambient = { at: rand(6, 18), kind: kinds[Math.floor(Math.random() * kinds.length)], fired: false };
      } else {
        state.ambient = { at: 999, kind: '', fired: true };
      }

      state.hr.target = state.hr.base;
      updateHUDLoop();
      updateHUDLocation();
      updateHUDPosture();
      saveProgress();
    }

    function transitionLoop(n, bannerText) {
      fadePulse(() => {
        setupLoop(n);
        if (bannerText) showBanner(bannerText);
      }, true);
    }

    function checkGates() {
      const p = state.player;
      if (p.room !== 'corridor' || state.transitioning || p.dead) return;

      // 추격 중 심층 게이트(−x) 접근 봉쇄 (팝아웃 등장 중엔 예외)
      if (state.stalker.active && !state.stalker.reveal && p.x < -19) p.x = -19;

      const atDeep = (p.x < GATE_DEEP_X);
      const atReturn = (p.z > GATE_RETURN_Z);
      if (!atDeep && !atReturn) return;

      const anomalyHere = state.anomaly.active;

      if (atDeep) {
        // 심층 게이트로 전진
        if (anomalyHere) {
          triggerChase();                       // 어긋남 중 전진 = 오판 → 추격
        } else {
          advanceFloor('B%F — 낯익음이 짙어진다');  // 정상 중 전진 = 정답
        }
      } else if (atReturn) {
        // 회귀 게이트로 후퇴
        if (state.stalker.active) {
          deactivateStalker();
          penaltyFloor('간신히 벗어났다 — 하지만 한 층 위로');  // 추격을 부른 건 오판
        } else if (anomalyHere) {
          advanceFloor('B%F — 어긋남을 등지고');   // 어긋남 중 후퇴 = 정답
        } else {
          penaltyFloor('길을 잘못 들었다 — 회랑이 되감긴다'); // 정상 중 후퇴 = 오판
        }
      }
    }

    function advanceFloor(bannerTmpl) {
      const next = state.loopCount + 1;
      playSynth(330, 0.35, 'sine', 0.1);
      if (next >= TARGET_FLOOR) triggerGameFinalEnding();
      else transitionLoop(next, bannerTmpl.replace('%', next));
    }

    // v1.0.0은 체크포인트(1/4/7)로 되돌려 B6F 오판 시 B4F까지 2층이 날아갔다.
    // 큰 낙차는 재도전 의욕을 꺾으므로, 어떤 실패든 손실은 항상 '한 층'뿐이다.
    // 난이도 변별은 층별 이상현상 밀도·미묘도(anomalyChance/subtleRatio/roomRatio)가 담당한다.
    function penaltyFloor(msg) {
      const back = Math.max(1, state.loopCount - 1);
      playBuzz();
      transitionLoop(back, msg + ' (B' + back + 'F)');
    }

    // ════════════════════════════════════════════
    // 14. 스토커 (추격 / 은신 / 이탈)
    // ════════════════════════════════════════════
    const CHASE_SPEED = 2.95;
    const REVEAL_DUR = 0.5;
    let lockerHintShown = false;
    function triggerChase() {
      const s = state.stalker;
      if (s.active) return;
      s.active = true; s.mode = 'chase';
      s.reveal = true; s.revealT = 0;
      s.lingerT = 0; s.soundT = 0; s.doorWaitT = 0;
      lockerHintShown = false;

      // "훅" — 심층 게이트(−x) 지척에서 즉시 튀어나온다
      const p = state.player;
      if (stalkerMesh.userData.swap) stalkerMesh.userData.swap();   // 매 추격마다 다른 형체
      s.x = -21.4; s.z = 0;
      stalkerMesh.position.set(s.x, 0, s.z);
      stalkerMesh.scale.setScalar(1);
      stalkerMesh.rotation.y = Math.atan2(p.x - s.x, p.z - s.z);
      stalkerMesh.visible = true;

      p.x = -20; p.z = 0;   // 지척(간격 ≈1.4)
      p.rotY = Math.PI / 2; // −x(정면) 응시
      p.rotX = -0.05;

      playSynth(120, 0.5, 'sawtooth', 0.28, 900);
      playNoise(0.4, 'highpass', 1800, 0.16);
      playScareSound();
      showFlashGlitch(0.95);
      bumpHR(165);
    }
    function deactivateStalker() {
      const s = state.stalker;
      s.active = false; s.reveal = false; s.revealT = 0;
      if (stalkerMesh) {
        stalkerMesh.visible = false;
        stalkerMesh.scale.setScalar(1);
        stalkerMesh.position.y = 0;
      }
    }
    function doorFrontOf(room) { return DOOR_TELEPORT[room] ? DOOR_TELEPORT[room].out : [0, 0]; }

    // 짧은 팝아웃 비트: 지척에서 잠깐 응시 → 곧바로 추격
    function updateReveal(dt) {
      const s = state.stalker;
      s.revealT += dt;
      const k = clamp(s.revealT / REVEAL_DUR, 0, 1);
      const p = state.player;
      s.x = -21.4 + k * 0.5; // 무심하게 한 발
      stalkerMesh.position.set(s.x, Math.sin(s.revealT * 22) * 0.02, s.z);
      stalkerMesh.rotation.y = Math.atan2(p.x - s.x, p.z - s.z);

      if (k >= 1) {
        s.reveal = false;
        stalkerMesh.scale.setScalar(1.05);
        p.x = -18.4;              // 도주 여유(헤드스타트)
        playChaseHorn();
        showFlashGlitch(0.5);
        bumpHR(160);
        showBanner('돌아서 도망쳐 — 모서리를 돌아 ▲ 회귀 게이트로!', 3200);
      }
    }

    // L자 인지: 스토커가 플레이어와 다른 팔에 있으면 모서리부터 경유
    function stalkerNavStep(dt) {
      const s = state.stalker, p = state.player;
      const sInH = s.x < -1.0, pInV = p.z > 1.0;
      const sInV = s.z > 1.0, pInH = p.x < -1.0;
      if ((sInH && pInV) || (sInV && pInH)) {
        moveStalkerToward(CORNER.x, CORNER.z, dt);
        return false; // 아직 플레이어에 직접 접근 아님
      }
      moveStalkerToward(p.x, p.z, dt);
      return true;
    }

    function updateStalker(dt, t) {
      const s = state.stalker;
      if (!s.active) return;
      if (s.reveal) { updateReveal(dt); return; }  // 등장 팝아웃 중엔 추격/포획 정지
      const p = state.player;
      const hiddenOK = p.inLocker && p.crouched;

      s.soundT += dt;
      if (s.soundT > 1.1) { s.soundT = 0; playChaseHorn(); }
      if (Math.random() < dt * 2.2) playCreak();

      let tx, tz;
      if (s.mode === 'chase') {
        if (hiddenOK) { s.mode = 'linger'; s.lingerT = 0; }
        else if (p.room !== 'corridor') {
          const df = doorFrontOf(p.room);
          tx = df[0]; tz = df[1];
          const dd = Math.hypot(tx - s.x, tz - s.z);
          if (dd < 0.4) {
            s.doorWaitT += dt;
            if (s.doorWaitT > 7) s.mode = 'retreat';
          } else moveStalkerToward(tx, tz, dt);
        } else {
          s.doorWaitT = 0;
          const direct = stalkerNavStep(dt); // 모서리 경유 포함
          const dist = Math.hypot(p.x - s.x, p.z - s.z);
          bumpHR(clamp(165 - dist * 3.5, 110, 165));
          if (!lockerHintShown && !p.inLocker) {
            const dl = Math.hypot(LOCKER_POS.x - p.x, LOCKER_POS.z - p.z);
            if (dl < 2.6) { lockerHintShown = true; showBanner('E — 옷장에 숨을 수 있다', 2200); }
          }
          if (direct && dist < 0.8) return catchPlayer();
        }
      }
      if (s.mode === 'linger') {
        if (!hiddenOK && p.room === 'corridor' && !p.inLocker) { s.mode = 'chase'; }
        else {
          const dd = Math.hypot(LOCKER_POS.x - s.x, LOCKER_POS.z - s.z);
          if (dd > 0.25) stalkerNavStep(dt);
          else {
            s.lingerT += dt;
            bumpHR(128);
            if (!hiddenOK && s.lingerT > 0.8) return catchPlayer();
            if (s.lingerT > 5) s.mode = 'retreat';
          }
        }
      }
      if (s.mode === 'retreat') {
        moveStalkerToward(-21, 0, dt, 2.2);
        if (s.x < -20.4) {
          deactivateStalker();
          showBanner('…멀어졌다');
        }
      }
      // 미세 부유 + 기괴한 팔/머리 흔들림 (등장 팝아웃 중엔 y를 건드리지 않음)
      if (!s.reveal) {
        stalkerMesh.position.y = Math.sin(t * 7) * 0.03;
        const moving = (s.mode === 'chase' || s.mode === 'retreat');
        const amp = moving ? 1 : 0.4;
        if (stalkerMesh.userData.armL) stalkerMesh.userData.armL.rotation.x = Math.sin(t * 6) * 0.35 * amp;
        if (stalkerMesh.userData.armR) stalkerMesh.userData.armR.rotation.x = Math.sin(t * 6 + 1.1) * 0.4 * amp;
        if (stalkerMesh.userData.head) stalkerMesh.userData.head.rotation.z = 0.18 + Math.sin(t * 2.3) * 0.12;
      }
    }
    function moveStalkerToward(tx, tz, dt, speedMul) {
      const s = state.stalker;
      const dx = tx - s.x, dz = tz - s.z;
      const d = Math.hypot(dx, dz);
      if (d < 0.02) return;
      const sp = CHASE_SPEED * (speedMul || 1) * dt;
      s.x += (dx / d) * Math.min(sp, d);
      s.z += (dz / d) * Math.min(sp, d);
      stalkerMesh.position.x = s.x;
      stalkerMesh.position.z = s.z;
      stalkerMesh.rotation.y = Math.atan2(dx, dz);
    }
    function catchPlayer() {
      const p = state.player;
      if (p.dead) return;
      p.dead = true;
      playScareSound();
      playChaseHorn();
      $('jumpscare-overlay').classList.add('on');
      bumpHR(185);
      setTimeout(() => {
        $('jumpscare-overlay').classList.remove('on');
        deactivateStalker();
        const back = Math.max(1, state.loopCount - 1);
        transitionLoop(back, '의식이 튕겨나갔다… B' + back + 'F');
      }, 1600);
    }

    // ════════════════════════════════════════════
    // 15. 방 고유 공포 트리거
    // ════════════════════════════════════════════
    // v1.1.0 — "겁주는 것 = 어긋남" 규칙을 지키기 위해, 방의 상시 연출에서
    // 잼스케어(굉음+화면 강타)를 걷어냈다. v1.0.0에서는 정상 층의 Room A에서도
    // 마네킹 잼스케어가 터져, 규칙을 믿은 플레이어를 오히려 함정에 빠뜨렸다.
    // 마네킹의 접근과 거울 사건은 '정상 기준선'에 속하는 조용한 연출로 남긴다.
    function updateRoomTriggers(dt) {
      const p = state.player;

      // Room A — 위핑엔젤 마네킹 (상시 = 정상. 소리 없이 다가올 뿐이다)
      if (p.room === 'roomA' && roomMannequin) {
        const mq = roomMannequin;
        const dx = p.x - mq.position.x, dz = p.z - mq.position.z;
        const dist = Math.hypot(dx, dz);
        mq.rotation.y = Math.atan2(dx, dz); // 언제나 당신을 향한다

        _camDir.set(0, 0, -1).applyQuaternion(camera.quaternion);
        _toMq.set(mq.position.x - p.x, 0, mq.position.z - p.z).normalize();
        const looking = _camDir.dot(_toMq) > 0.35;

        if (!looking) {
          if (!state.flags.mannequinAway && dist > 0.9) {
            state.flags.mannequinAway = true;
            const step = Math.min(0.5, dist - 0.8);
            mq.position.x = clamp(mq.position.x + (dx / dist) * step, ROOM_BOUNDS.roomA.x[0], ROOM_BOUNDS.roomA.x[1]);
            mq.position.z = clamp(mq.position.z + (dz / dist) * step, ROOM_BOUNDS.roomA.z[0], ROOM_BOUNDS.roomA.z[1]);
            playCreak();
            bumpHR(Math.min(112, state.hr.target + 8));
          }
        } else {
          state.flags.mannequinAway = false;
          // 코앞까지 왔다면, 굉음 대신 낮은 숨소리와 함께 조용히 제자리로 물러난다
          if (dist < 1.0) {
            playWhisper();
            bumpHR(118);
            mq.position.set(roomMannequinHome.x, 0, roomMannequinHome.z);
          }
        }
      }

      // Room C — 거울 사건 (런 1회, 일기장 페이지 낙하 = 진행 필수 스토리)
      // 이상현상이 아니므로 잼스케어 없이, 유리가 갈라지는 소리로만 처리한다.
      if (p.room === 'roomC' && !state.flags.mirrorDone && p.x < ROOMS.roomC.cx - 1.0) {
        state.flags.mirrorDone = true;
        playSynth(1400, 0.5, 'triangle', 0.14, 300);
        playNoise(0.7, 'highpass', 3000, 0.09);
        showFlashGlitch(0.35);
        bumpHR(126);
        // 이 층에 Room C 거울 이상현상이 걸려 있다면 그 텍스처를 덮어쓰지 않는다
        if (mirrorMesh && !mirrorMesh.userData.anomMirror) {
          mirrorMesh.material.map = Textures.mirrorBlood;
          mirrorMesh.material.needsUpdate = true;
        }
        if (itemDiaryPage) {
          itemDiaryPage.visible = true;
          itemDiaryPage.userData.hitProxy.visible = true;
        }
        showBanner('거울에 금이 갔다 — 무언가 떨어졌다', 2800);
      }
    }

    // ════════════════════════════════════════════
    // 16. 이벤트형 이상현상 (v1.1.0)
    // ════════════════════════════════════════════
    //
    // v1.0.0에서 실루엣(B5F)·정전(B8F)은 '층 고정 스크립트'였다. 즉 이상현상과
    // 무관하게 터졌고, 그 결과 플레이어는 "무서운 일이 일어났다"를 판단 근거로
    // 삼을 수 없었다 — 오히려 오독을 유발했다.
    //
    // 이제 이 사건들은 전부 이상현상 ID(evt*)이며, 발생 조건은 단 하나다:
    //   "이번 층에 그 이상현상이 롤되었을 때만 발생한다."
    // 따라서 규칙이 예외 없이 성립한다 — 튀어나왔다면, 이 층은 어긋나 있다.
    //
    function updateScriptedEvents(dt) {
      const an = state.anomaly;
      const p = state.player;

      // 환경음 (순수 분위기 — 층 판정과 무관하며, 시각적 변화를 동반하지 않는다)
      if (!state.ambient.fired && state.loopTime > state.ambient.at) {
        state.ambient.fired = true;
        const k = state.ambient.kind;
        if (k === 'whisper') playWhisper();
        else if (k === 'steps') { for (let i = 0; i < 5; i++) setTimeout(() => playSynth(58, 0.1, 'triangle', 0.05), i * 170); }
        else if (k === 'static') playStatic();
        else if (k === 'bend') playDroneBend();
        bumpHR(90);
      }

      // ── 이벤트형 이상현상 발화 ──
      if (an.active && an.kind === 'event' && !an.eventFired &&
          p.room === 'corridor' && !p.inLocker && state.loopTime > an.eventAt) {
        an.eventFired = true;
        fireAnomalyEvent(an.id);
      }

      // ── 실루엣이 회랑을 가로지른다 (evtWalkby) ──
      if (state.walkby.on) {
        state.walkby.t += dt;
        const k = state.walkby.t / 2.2;
        walkbyMesh.position.x = state.walkby.x0 + k * state.walkby.dx;
        walkbyMesh.position.z = state.walkby.z0 + k * state.walkby.dz;
        walkbyMesh.rotation.y = state.walkby.ry;
        if (k >= 1) { state.walkby.on = false; walkbyMesh.visible = false; }
      }

      // ── '그것'의 순간 출현 = 갑툭튀 (evtPeek) ──
      // 해치지 않는다. 보여주고 사라진다. 그러나 그 자체가 어긋남의 증거다.
      if (state.peek.on) {
        state.peek.t += dt;
        if (walkbyMesh) {
          walkbyMesh.rotation.y = Math.atan2(p.x - walkbyMesh.position.x, p.z - walkbyMesh.position.z);
          walkbyMesh.position.y = Math.sin(state.peek.t * 20) * 0.03;
        }
        if (state.peek.t > 1.15) {
          state.peek.on = false;
          if (walkbyMesh) { walkbyMesh.visible = false; walkbyMesh.position.y = 0; }
          playStatic();
        }
      }

      // ── 정전 + 붉은 눈 (evtBlackout) ──
      if (state.blackout.phase === 1) {
        state.blackout.t += dt;
        flashLight.intensity = 0;
        corridorLamps.forEach((l) => { if (l.light) l.light.intensity = 0; l.mesh.material.color.setHex(0x050505); });
        if (roomLight) roomLight.intensity = 0;
        if (state.blackout.t > 2.6) {
          state.blackout.phase = 0;
          blackoutEyes.visible = false;
          flashLight.intensity = FLASH_ON;
          lampsDirty = true;
          setRoomLight(state.player.room);
          playStatic();
        }
      }
    }

    function fireAnomalyEvent(id) {
      const p = state.player;
      const inV = p.z > 1.75;   // 세로팔에 있는가

      if (id === 'evtWalkby') {
        // 플레이어 앞쪽을 무언가가 가로질러 지나간다
        if (inV) {
          const z = clamp(p.z - 5.5, 0.5, 17);
          state.walkby = { on: true, t: 0, x0: -2.4, z0: z, dx: 4.8, dz: 0, ry: Math.PI / 2 };
        } else {
          const x = clamp(p.x - 5.5, -20, -1);
          state.walkby = { on: true, t: 0, x0: x, z0: -2.4, dx: 0, dz: 4.8, ry: 0 };
        }
        if (walkbyMesh.userData.swap) walkbyMesh.userData.swap();   // 매번 다른 형체
        walkbyMesh.position.set(state.walkby.x0, 0, state.walkby.z0);
        walkbyMesh.visible = true;
        playCreak(); playWhisper();
        bumpHR(118);
        showFlashGlitch(0.22);

      } else if (id === 'evtBlackout') {
        state.blackout.phase = 1; state.blackout.t = 0;
        blackoutEyes.visible = true;
        if (inV) blackoutEyes.position.set(0, 1.7, clamp(p.z - 6, 0.5, 18));
        else blackoutEyes.position.set(clamp(p.x - 6, -20, -0.5), 1.7, 0);
        playWhisper(); playDroneBend();
        bumpHR(152);

      } else if (id === 'evtPeek') {
        // 시야 안쪽에 '그것'이 불쑥 나타났다가 사라진다 (해를 끼치지 않는 갑툭튀)
        if (walkbyMesh.userData.swap) walkbyMesh.userData.swap();   // 매번 다른 형체
        if (inV) walkbyMesh.position.set(0, 0, clamp(p.z - 4.5, 0.5, 17));
        else walkbyMesh.position.set(clamp(p.x - 4.5, -20.5, -1), 0, 0);
        walkbyMesh.visible = true;
        state.peek = { on: true, t: 0 };
        playScareSound();
        showFlashGlitch(0.75);
        bumpHR(158);

      } else if (id === 'evtKnock') {
        // 어느 방의 문이 안에서 두드려진다 (미묘 — 소리와 미세 진동뿐)
        // v1.2.1: setInterval은 층이 전환돼도 계속 돌아 문을 영원히 흔들 위험이 있었다.
        // 틱 구동 상태(state.knock)로 바꿔, clearAnomaly가 자연히 멈추게 한다.
        const d = doorDefs[Math.floor(Math.random() * 3)];
        if (d) {
          state.anomaly.doorIdx = doorDefs.indexOf(d);
          playKnock(3);
          state.knock = { on: true, t: 0, doorIdx: doorDefs.indexOf(d) };
        }
        bumpHR(106);
      }
    }

    // 문 두드림 진동 — 틱에서 갱신 (evtKnock)
    function updateKnock(dt) {
      const k = state.knock;
      if (!k || !k.on) return;
      k.t += dt;
      const d = doorDefs[k.doorIdx];
      if (!d) { k.on = false; return; }
      const cycle = Math.floor(k.t / 0.12);
      const amp = (cycle % 2 === 0) ? 0.035 : 0;
      const alongZ = (d.homeZ === -1.68);   // H 원벽 문은 z가 벽면
      d.group.position.x = d.homeX + (alongZ ? 0 : amp);
      d.group.position.z = d.homeZ + (alongZ ? amp : 0);
      if (k.t > 1.3) {
        k.on = false;
        d.group.position.x = d.homeX;
        d.group.position.z = d.homeZ;
      }
    }

    // ════════════════════════════════════════════
    // 17. 이동 물리 & 메인 틱 (단일 rAF 체인)
    // ════════════════════════════════════════════
    const gameClock = new THREE.Clock();
    let tickerStarted = false;
    let globalT = 0;

    function updatePlayer(dt) {
      const p = state.player;
      if (p.dead || p.inLocker) return;
      if (state.stalker.reveal) { p.stepDist = 0; return; } // 정면 등장 비트 동안 이동 정지

      let speed = p.crouched ? 1.1 : 2.3;
      if (keysPressed['shift']) p.sprinting = true;
      else if (joyTouchId === null && !$('touch-sprint').classList.contains('bg-orange-800')) p.sprinting = false;
      if (p.sprinting && !p.crouched) speed = 3.8;

      let mx = 0, mz = 0;
      if (keysPressed['w'] || keysPressed['arrowup']) mz -= 1;
      if (keysPressed['s'] || keysPressed['arrowdown']) mz += 1;
      if (keysPressed['a'] || keysPressed['arrowleft']) mx -= 1;
      if (keysPressed['d'] || keysPressed['arrowright']) mx += 1;
      if (joyTouchId !== null) { mx = joyDir.x; mz = -joyDir.y; }

      const len = Math.hypot(mx, mz);
      if (len > 0.01) {
        const nx = mx / len, nz = mz / len;
        const yaw = p.rotY;
        const fX = Math.sin(yaw), fZ = Math.cos(yaw);
        const rX = Math.cos(yaw), rZ = -Math.sin(yaw);
        const dx = (fX * nz + rX * nx) * speed * dt;
        const dz = (fZ * nz + rZ * nx) * speed * dt;
        const tx = p.x + dx, tz = p.z + dz;

        if (p.room === 'corridor') {
          // L자 보행영역 + 벽 슬라이딩 (막혀도 갇히지 않음)
          if (inWalk(tx, tz)) { p.x = tx; p.z = tz; }
          else if (inWalk(tx, p.z)) { p.x = tx; }
          else if (inWalk(p.x, tz)) { p.z = tz; }
        } else {
          const b = ROOM_BOUNDS[p.room];
          p.x = clamp(tx, b.x[0], b.x[1]);
          p.z = clamp(tz, b.z[0], b.z[1]);
        }

        p.stepDist += speed * dt;
        const stepLen = p.crouched ? 1.1 : 0.85;
        if (p.stepDist > stepLen) { p.stepDist = 0; playFootstep(); }
      }
    }

    function updateHR(dt) {
      const hr = state.hr;
      // v1.0.0은 이상현상이 있으면 HR을 +7 올려, 숫자만 보고도 100% 판별이 가능했다.
      // 관찰 게임의 근간을 무너뜨리므로 제거한다.
      // 대신 층이 깊어질수록 기본 심박이 오른다 (판별 정보가 아닌 순수 긴장 표현).
      hr.base = 72 + (state.loopCount - 1) * 1.6;
      hr.target += (hr.base - hr.target) * Math.min(1, dt * 0.55);
      hr.current += (hr.target - hr.current) * Math.min(1, dt * 2.2);
      updateHRDisplay();
    }

    function updateWorldFX(dt, t) {
      const anom = state.anomaly;
      const p = state.player;

      // 조명: lampsRed(붉은 명멸) / lampsDim(전체 감광) / lampOut(특정 등 꺼짐) / 정상
      // 스토커 등장·정전 중엔 유지
      // 명멸(lampsRed)일 때만 매 프레임 갱신이 필요하다. 나머지 상태는 값이 고정이므로
      // 이미 적용돼 있으면 건너뛴다 (v1.1.0은 매 프레임 8회씩 무의미하게 다시 썼다).
      const flickering = anom.active && anom.id === 'lampsRed';
      if (state.blackout.phase === 0 && !state.stalker.reveal && (flickering || lampsDirty)) {
        corridorLamps.forEach((l) => {
          if (flickering) {
            const flick = 0.18 + Math.abs(Math.sin(t * 9 + l.phase)) * (Math.random() < 0.06 ? 0.05 : 0.55);
            if (l.light) { l.light.intensity = l.baseIntensity * flick * 1.4; l.light.color.setHex(0xffb9a2); }
            l.mesh.material.color.setHex(0xdd9a86);
          } else if (l._out) {
            if (l.light) l.light.intensity = 0;
            l.mesh.material.color.setHex(0x1a1a1a);
          } else if (l._dim) {
            // 미묘: 전등 색이 아주 살짝 푸르고 어둡다 (기억해 두지 않으면 놓친다)
            if (l.light) { l.light.intensity = l.baseIntensity * 0.52; l.light.color.setHex(0xc8d4e6); }
            l.mesh.material.color.setHex(0xa8b4c6);
          } else {
            if (l.light) { l.light.intensity = l.baseIntensity; l.light.color.setHex(l.baseColor); }
            l.mesh.material.color.setHex(l.baseColor);
          }
        });
        if (!flickering) lampsDirty = false;
      }

      // ── 회랑 이상현상 모션 ──
      if (anom.active && !state.stalker.active && p.room === 'corridor') {
        anom.t += dt;
        if (anom.id === 'gurneyRoll' && props.gurney) {
          // 거니가 심층(−x)에서 플레이어를 향해 가로팔을 따라 굴러온다
          const gx = props.gurney.position.x;
          const targetX = clamp(p.x - 1.2, -20, 0);
          if (gx < targetX - 0.05) {
            props.gurney.position.x = Math.min(targetX, gx + dt * 1.5);
            props.gurney.rotation.y = 0;
            if (Math.random() < dt * 1.5) playCreak();
          }
        } else if (anom.id === 'endFigure' && anomObj.endFigure && anomObj.endFigure.visible) {
          const f = anomObj.endFigure;
          f.rotation.y = Math.atan2(p.x - f.position.x, p.z - f.position.z);
          f.position.y = Math.sin(t * 5) * 0.02;
        } else if (anom.id === 'ventEyes' && anomObj.ventEyes && anomObj.ventEyes.visible) {
          const on = (Math.sin(t * 3) > -0.4) ? 1 : 0.15; // 깜빡임
          anomObj.ventEyes.children.forEach((e) => e.material.opacity = on);
          anomObj.ventEyes.scale.setScalar(1 + Math.sin(t * 1.3) * 0.06);
        } else if (anom.id === 'wheelHall' && anomObj.dupWheelchair && anomObj.dupWheelchair.visible) {
          anomObj.dupWheelchair.rotation.y = Math.atan2(p.x - anomObj.dupWheelchair.position.x, p.z - anomObj.dupWheelchair.position.z) + Math.PI;
        } else if (anom.id === 'hanging' && anomObj.hangingFigure && anomObj.hangingFigure.visible) {
          // 아주 느리게 흔들린다
          anomObj.hangingFigure.rotation.y = Math.sin(t * 0.55) * 0.5;
          anomObj.hangingFigure.rotation.z = Math.sin(t * 0.8) * 0.035;
          if (Math.random() < dt * 0.35) playCreak();
        }
      }

      // ── 방 이상현상 모션 ──
      if (anom.active && anom.zone === p.room) {
        if (anom.id === 'rB_chairSpin' && props.officeChair && props.officeChair.userData.spin) {
          props.officeChair.rotation.y += dt * 0.85;
          if (Math.random() < dt * 0.6) playCreak();
        } else if (anom.id === 'rA_extraMq' && anomObj.mqExtra && anomObj.mqExtra.visible) {
          anomObj.mqExtra.rotation.y = Math.atan2(p.x - anomObj.mqExtra.position.x, p.z - anomObj.mqExtra.position.z);
        }
      }
      // 서류 부양 (Room B) — 방 밖에서도 상태가 유지돼야 하므로 조건 밖에서 처리
      if (props.papers) {
        props.papers.forEach((pp, i) => {
          if (pp.userData.floatUp) {
            const tgt = pp.userData.baseY + 0.55 + Math.sin(t * 1.4 + i) * 0.09;
            pp.position.y += (tgt - pp.position.y) * Math.min(1, dt * 1.6);
            pp.rotation.x = -Math.PI / 2 + Math.sin(t * 0.9 + i * 2) * 0.5;
          }
        });
      }

      // 아이템 부유
      floaters.forEach((m, i) => {
        if (!m.visible) return;
        if (m.userData.baseY === undefined) m.userData.baseY = m.position.y;
        m.position.y = m.userData.baseY + Math.sin(t * 2 + i * 1.7) * 0.045;
        m.rotation.z = (m.rotation.z || 0) + dt * 0.4;
      });
      // 복도 마네킹은 언제나 당신을 향해 있다
      if (corridorMannequin && corridorMannequin.visible) {
        corridorMannequin.rotation.y = Math.atan2(p.x - corridorMannequin.position.x, p.z - corridorMannequin.position.z);
      }
    }

    // 매 프레임 new 하지 않도록 미리 만들어 두고 재사용한다 (GC 압박 제거)
    const _euler = new THREE.Euler(0, 0, 0, 'YXZ');
    const _fwd = new THREE.Vector3();
    let frameNo = 0;

    function tick() {
      requestAnimationFrame(tick);
      const dt = Math.min(0.05, gameClock.getDelta());
      frameNo++;

      if (state.phase === 'playing' && !isPausedAny() && !state.transitioning && !state.player.dead) {
        globalT += dt;
        state.loopTime += dt;
        updatePlayer(dt);
        updateHR(dt);
        updateRoomTriggers(dt);
        updateScriptedEvents(dt);
        updateKnock(dt);
        updateStalker(dt, globalT);
        updateWorldFX(dt, globalT);
        // 레이캐스트는 매 프레임 필요 없다 (조준 판정은 3프레임 주기로 충분)
        if (frameNo % PERF.raycastEvery === 0) checkRaycast();
        checkGates();
      }

      if (camera) {
        const p = state.player;
        const targetY = p.crouched ? 0.9 : 1.6;
        p.y += (targetY - p.y) * Math.min(1, dt * 9);
        camera.position.set(p.x, p.y, p.z);
        _euler.set(p.rotX, p.rotY, 0, 'YXZ');
        camera.quaternion.setFromEuler(_euler);
        if (flashLight) {
          _fwd.set(0, 0, -1).applyQuaternion(camera.quaternion);
          flashLight.position.copy(camera.position);
          flashLight.target.position.copy(camera.position).add(_fwd);
        }
      }
      if (renderer && scene && camera) renderer.render(scene, camera);

      // FPS 집계 (1초 창)
      // 일시정지 중에는 갱신·물리가 멈춰 프레임이 부풀려지므로, '플레이 중'에만 잰다.
      // 그래야 메뉴를 열었을 때 보이는 값이 실제 게임 부하를 뜻한다.
      if (state.phase === 'playing' && !isPausedAny()) {
        fpsFrames++;
        fpsAccum += dt;
        if (fpsAccum >= 1) {
          fpsValue = Math.round(fpsFrames / fpsAccum);
          fpsFrames = 0; fpsAccum = 0;
          refreshFpsLabel();
        }
      }
    }
    let fpsFrames = 0, fpsAccum = 0, fpsValue = 0;
    function refreshFpsLabel() {
      const el = $('fps-indicator');
      if (!el) return;
      if (!fpsValue) { el.innerText = '-- FPS'; return; }
      el.innerText = fpsValue + ' FPS';
      el.className = 'text-xs ' + (fpsValue >= 50 ? 'text-green-400' : fpsValue >= 30 ? 'text-amber-400' : 'text-red-400');
    }
    function startTicker() {
      if (tickerStarted) return;
      tickerStarted = true;
      gameClock.getDelta();
      tick();
    }

    // ════════════════════════════════════════════
    // 18. 엔딩 (3분기 — 떡밥 회수)
    // ════════════════════════════════════════════
    function triggerGameFinalEnding() {
      state.phase = 'ending';
      clearSave();
      if (document.pointerLockElement) document.exitPointerLock();
      deactivateStalker();
      clearAnomaly();

      const inv = state.inventory;
      const count = ['glasses', 'clock', 'diary', 'band'].filter((k) => inv[k]).length;
      const notes = ['corridor', 'roomB', 'roomC'].filter((k) => state.notesRead[k]).length;

      const title = $('ending-title'), sub = $('ending-subtitle'), desc = $('ending-description');
      $('ending-items').innerText = count + '/4';
      $('ending-notes').innerText = notes + '/3';

      if (count === 4) {
        title.innerText = 'Ending A — 04:45';
        title.className = 'text-3xl font-black text-cyan-400 tracking-widest uppercase';
        sub.innerText = '“멈춘 시계가 다시 간다” (True)';
        let bonus = '';
        if (notes === 3) bonus = '<p class="text-cyan-300/80 text-xs border-t border-neutral-900 pt-3">침대 곁 낡은 일기장의 마지막 장에는, 어젯밤 필체로 이렇게 적혀 있었다 — <span class="font-bold">"돌아온 걸 환영해."</span></p>';
        desc.innerHTML =
          '<p class="font-bold text-white text-base">네 개의 자물쇠가 전부 풀렸습니다.</p>' +
          '<p class="text-sm">외면했던 시야(깨진 안경), 그날 4시 44분에 얼어붙은 시간(회중시계), 유리 저편에 두고 온 목소리(일기장), 그리고 침대 위의 자신(환자 팔찌)까지 — 당신은 도망치지 않고 전부 마주했습니다.</p>' +
          '<p class="text-sm text-neutral-400">귀를 짓누르던 저음의 드론이 잦아들고, 규칙적인 심박 모니터 소리가 그 자리를 대신합니다. 제4병동, 창으로 새벽빛. 벽시계의 초침이 — 움직입니다. 4시 45분.</p>' +
          '<p class="text-sm text-neutral-300 font-semibold">당신은 눈을 뜹니다.</p>' + bonus;
      } else if (count > 0) {
        title.innerText = 'Ending B — 조작된 아침';
        title.className = 'text-3xl font-black text-yellow-500 tracking-widest uppercase';
        sub.innerText = '“완성되지 못한 기시감” (Normal)';
        desc.innerHTML =
          '<p class="font-bold text-white text-base">기억을 ' + count + '조각만 쥔 채, 당신은 아침을 맞은 것 같습니다.</p>' +
          '<p class="text-sm">깨끗하게 도배된 익숙한 침실. 안도하며 문손잡이를 잡는 순간 — 벽시계가 눈에 들어옵니다. 4시 44분. 초침은 죽어 있습니다.</p>' +
          '<p class="text-sm text-neutral-400">문 너머 복도는 이상하리만치 어둡고, 끝없이 뻗어 있습니다. 그 끝에서 익숙한 심박이 다시, 은근하게 울리기 시작합니다. 쿵… 쿵…</p>' +
          '<p class="text-xs text-neutral-500">회수하지 못한 기억이 아직 회랑에 남아 있습니다.</p>';
      } else {
        title.innerText = 'Ending C — 무기한 보류';
        title.className = 'text-3xl font-black text-red-600 tracking-widest uppercase';
        sub.innerText = '“기억을 전부 버린 자” (Bad)';
        desc.innerHTML =
          '<p class="font-bold text-white text-base">당신은 단 하나의 기억도 줍지 않고 출구만을 향해 달렸습니다.</p>' +
          '<p class="text-sm">B10F의 문이 열리고 — 그 너머는 B1F였습니다. 4시 44분의 벽시계, 제4병동의 게시물, 전부 그대로. 기시감의 저주는 회수되지 않은 기억을 연료로 완성되었습니다.</p>' +
          '<p class="text-sm text-neutral-400">현실의 육체는 깊은 동면으로 가라앉습니다. 이제 당신이 아는 가장 안전한 곳은 회랑의 좁은 옷장 속. 숨을 죽인 채, 붉은 눈이 문틈을 스치는 소리를 영원히 듣게 될 것입니다.</p>';
      }
      const scr = $('ending-screen');
      scr.classList.remove('hidden');
      scr.classList.add('flex');
    }

    // ════════════════════════════════════════════
    // 18.5. 진행도 자동 저장 / 이어하기 (localStorage, 안전 래핑)
    // ════════════════════════════════════════════
    // v1.1.0: 저장 스키마가 바뀌었으므로 키를 올려 구버전 세이브와 충돌시키지 않는다.
    const SAVE_KEY = 'dejavu_save_v11';
    function saveProgress() {
      if (state.phase !== 'playing') return;
      try {
        localStorage.setItem(SAVE_KEY, JSON.stringify({
          v: 2,
          loopCount: state.loopCount,
          inventory: state.inventory,
          notesRead: state.notesRead,
          puzzleSolved: state.puzzle.solved,
          keypadSolved: state.keypad.solved,
          mirrorDone: state.flags.mirrorDone,
          roomHintShown: state.roomHintShown,
          ts: Date.now()
        }));
      } catch (e) {}
    }
    function loadSave() {
      try {
        const raw = localStorage.getItem(SAVE_KEY);
        if (!raw) return null;
        const s = JSON.parse(raw);
        if (!s || s.v !== 2 || !s.loopCount) return null;
        return s;
      } catch (e) { return null; }
    }
    function clearSave() { try { localStorage.removeItem(SAVE_KEY); } catch (e) {} }

    function applySave(s) {
      state.loopCount = clamp(s.loopCount || 1, 1, TARGET_FLOOR - 1);
      state.inventory = Object.assign({ glasses: false, clock: false, diary: false, band: false }, s.inventory || {});
      state.notesRead = Object.assign({ corridor: false, roomB: false, roomC: false }, s.notesRead || {});
      state.puzzle.solved = !!s.puzzleSolved;
      state.keypad.solved = !!s.keypadSolved;
      state.flags.mirrorDone = !!s.mirrorDone;
      state.roomHintShown = !!s.roomHintShown;

      // 월드 시각 상태 복원
      if (state.inventory.glasses && itemGlasses) { itemGlasses.visible = false; itemGlasses.userData.hitProxy.visible = false; }
      if (state.puzzle.solved && monitorMesh) { monitorMesh.material.map = Textures.monitorDone; monitorMesh.material.needsUpdate = true; }
      if (state.keypad.solved && drawerMesh) { drawerMesh.position.z += 0.3; }
      if (state.flags.mirrorDone && mirrorMesh) { mirrorMesh.material.map = Textures.mirrorBlood; mirrorMesh.material.needsUpdate = true; }
      // 거울 사건은 끝났는데 일기장을 아직 안 주웠다면, 페이지는 바닥에 남아 있어야 한다
      if (itemDiaryPage) {
        const show = state.flags.mirrorDone && !state.inventory.diary;
        itemDiaryPage.visible = show;
        itemDiaryPage.userData.hitProxy.visible = show;
      }
      refreshItemStatusUI();
    }

    function refreshItemStatusUI() {
      ['glasses', 'clock', 'diary', 'band'].forEach((id) => {
        const st = $('item-status-' + id);
        if (!st) return;
        if (state.inventory[id]) { st.innerText = '회수 완료'; st.className = 'text-[10px] text-cyan-400 mt-1 uppercase tracking-wider'; }
        else { st.innerText = '미회수'; st.className = 'text-[10px] text-neutral-600 mt-1 uppercase tracking-wider'; }
      });
      recalcSync();
    }

    function refreshContinueButton() {
      const btn = $('continue-btn');
      if (!btn) return;
      const s = loadSave();
      if (s) {
        const n = ['glasses', 'clock', 'diary', 'band'].filter((k) => s.inventory && s.inventory[k]).length;
        $('continue-info').innerText = 'B' + clamp(s.loopCount, 1, TARGET_FLOOR - 1) + 'F · 기억 ' + n + '/4';
        btn.classList.remove('hidden');
      } else {
        btn.classList.add('hidden');
      }
    }

    let unloadGuardOn = false;
    function unloadHandler(e) {
      if (state.phase === 'playing') {
        saveProgress();
        e.preventDefault();
        e.returnValue = ''; // 브라우저 확인창 (실수 이탈 방지)
        return '';
      }
    }
    function enableUnloadGuard() {
      if (unloadGuardOn) return;
      unloadGuardOn = true;
      window.addEventListener('beforeunload', unloadHandler);
    }

    // ════════════════════════════════════════════
    // 19. 시작 / 완전 초기화 (렌더러 보존 — 흰 화면 원천 차단)
    // ════════════════════════════════════════════
    function beginGame(save) {
      buildWorld();
      if (!corridorMannequin) buildCorridorMannequin();
      if (itemDiaryPage && itemDiaryPage.userData.hitProxy) itemDiaryPage.userData.hitProxy.visible = false;
      initAudio();
      setupControls();

      $('start-screen').classList.add('hidden');
      $('game-container').style.pointerEvents = 'auto';
      state.phase = 'playing';
      if (save) applySave(save);
      setupLoop(state.loopCount);
      recalcSync();
      refreshItemStatusUI();
      startTicker();
      enableUnloadGuard();
      setTimeout(hideGuide, 6000);
    }
    function startGameEvent(e) {
      if (e) { e.stopPropagation(); e.preventDefault(); }
      clearSave();          // 새 게임 → 이전 저장 폐기
      state = createState();
      beginGame(null);
    }
    function continueGame(e) {
      if (e) { e.stopPropagation(); e.preventDefault(); }
      const s = loadSave();
      if (!s) { startGameEvent(e); return; }
      state = createState();
      beginGame(s);
    }

    function resetWorldObjects() {
      if (!worldBuilt) return;
      // 주의: clearAnomaly()가 state.flags.mirrorDone / state.puzzle.solved를 참조하므로
      // 반드시 state를 재생성하기 '전에' 호출되어야 한다 (triggerSoftReset이 그 순서를 지킨다).
      state.flags.mirrorDone = false;   // 거울을 새 상태로 되돌린 뒤 clearAnomaly가 정상 텍스처를 복원하도록
      state.puzzle.solved = false;
      clearAnomaly();
      deactivateStalker();
      if (walkbyMesh) { walkbyMesh.visible = false; walkbyMesh.position.y = 0; }
      if (blackoutEyes) blackoutEyes.visible = false;
      if (flashLight) flashLight.intensity = FLASH_ON;
      setRoomLight('corridor');
      if (roomMannequin) { roomMannequin.position.set(roomMannequinHome.x, 0, roomMannequinHome.z); roomMannequin.rotation.y = 0.8; }
      if (itemGlasses) { itemGlasses.visible = true; itemGlasses.userData.hitProxy.visible = true; }
      if (itemDiaryPage) { itemDiaryPage.visible = false; itemDiaryPage.userData.hitProxy.visible = false; }
      if (monitorMesh) { monitorMesh.material.map = Textures.monitorIdle; monitorMesh.material.needsUpdate = true; }
      if (drawerMesh && state.keypad.solved) drawerMesh.position.z -= 0.3;
    }

    function resetHUD() {
      ['glasses', 'clock', 'diary', 'band'].forEach((id) => {
        const st = $('item-status-' + id);
        st.innerText = '미회수';
        st.className = 'text-[10px] text-neutral-600 mt-1 uppercase tracking-wider';
      });
      $('sync-text').innerText = '0%'; $('sync-bar').style.width = '0%';
      $('heart-rate-text').innerText = '72 BPM'; $('heart-rate-bar').style.width = '14%';
      $('hud-location').innerText = '중앙 회랑';
      $('hud-posture').innerText = '서 있음';
      $('loop-counter').innerText = 'B1F';
      $('inv-progress').innerText = '0 / 4';
      $('item-description-panel').innerHTML = '<p class="text-sm text-neutral-400 text-center py-2">회수가 완료된 기억을 선택하면 내면 기록이 복원됩니다.</p>';
      $('touch-crouch-label').innerText = '앉기';
      $('touch-crouch').classList.remove('bg-blue-800');
      $('touch-crouch-icon-down').classList.remove('hidden');
      $('touch-crouch-icon-up').classList.add('hidden');
      ['hud-room-a', 'hud-room-b', 'hud-room-c'].forEach((id) => {
        const el = $(id);
        if (el) el.className = 'px-1.5 rounded border border-neutral-800 text-neutral-600';
      });
    }

    function triggerSoftReset(e) {
      if (e) e.stopPropagation();
      resetWorldObjects();          // (state.keypad를 참조하므로 상태 재생성 전에 실행)
      clearSave();                  // 재시작 → 저장 폐기
      state = createState();
      pauseReasons.clear();
      for (const k in keysPressed) keysPressed[k] = false;

      hideModal($('pause-modal'));
      hideModal($('inventory-modal'));
      hideModal($('puzzle-modal'));
      hideModal($('keypad-modal'));
      hideModal($('note-modal'));
      const scr = $('ending-screen');
      scr.classList.add('hidden'); scr.classList.remove('flex');
      $('quit-confirm-box').classList.add('hidden');
      $('jumpscare-overlay').classList.remove('on');
      $('fade-overlay').classList.remove('on');
      $('event-banner').classList.remove('show');
      $('locker-hint').classList.add('hidden');
      document.body.classList.remove('in-locker');

      resetHUD();
      if (document.pointerLockElement) document.exitPointerLock();
      $('game-container').style.pointerEvents = 'none';
      $('start-screen').classList.remove('hidden');
      refreshContinueButton();
      resetGuide();
    }

    // ════════════════════════════════════════════
    // 20. 페이지 이벤트 부트스트랩 (1회 바인딩)
    // ════════════════════════════════════════════
    function initPageEvents() {
      buildKeypadButtons();
      refreshContinueButton();

      // 백그라운드 전환/이탈 시 진행 저장 (닫혀도 복구 가능)
      window.addEventListener('pagehide', saveProgress);
      document.addEventListener('visibilitychange', () => { if (document.hidden) saveProgress(); });

      const volS = $('volume-slider');
      volS.addEventListener('input', (e) => {
        const v = e.target.value;
        setVolume(v / 100);
        $('volume-indicator').innerText = v + '%';
      });
      const senS = $('sensitivity-slider');
      senS.addEventListener('input', (e) => {
        settings.sensitivity = e.target.value / 100;
        $('sensitivity-indicator').innerText = settings.sensitivity.toFixed(1);
      });

      // 그래픽 품질 — 렌더 해상도 배율만 바꾼다 (게임 내용은 완전히 동일)
      document.querySelectorAll('.quality-btn').forEach((b) => {
        b.addEventListener('click', (e) => {
          e.stopPropagation();
          applyQuality(b.getAttribute('data-q'));
          playSynth(420, 0.06, 'triangle', 0.04);
        });
      });
      applyQuality(PERF.level);   // 버튼 초기 하이라이트

      // 퍼즐 슬라이더 (v0.3 누락분 — 이 리스너가 없으면 퍼즐이 영구 미해결)
      $('puzzle-slider-1').addEventListener('input', (e) => {
        state.puzzle.v1 = parseInt(e.target.value, 10);
        drawPuzzleWaves();
      });
      $('puzzle-slider-2').addEventListener('input', (e) => {
        state.puzzle.v2 = parseInt(e.target.value, 10);
        drawPuzzleWaves();
      });

      document.querySelectorAll('.inventory-card').forEach((card) => {
        card.addEventListener('click', () => {
          const id = card.getAttribute('data-item-id');
          const panel = $('item-description-panel');
          if (!state.inventory[id]) {
            panel.innerHTML = '<p class="text-sm text-red-500 font-bold mb-1">신호 유실 (Unrecovered)</p>' +
              '<p class="text-xs text-neutral-500 leading-relaxed">이 기억은 아직 회랑 어딘가에 봉인되어 있습니다.</p>';
          } else {
            const it = itemData[id];
            panel.innerHTML = '<h4 class="text-sm font-bold text-cyan-400 mb-1.5">' + it.title + '</h4>' +
              '<p class="text-xs text-neutral-200 leading-relaxed">' + it.desc + '</p>';
          }
          playSynth(360, 0.08, 'triangle', 0.04);
        });
      });

      // 배경 클릭으로 각 모달 닫기
      const backdropClose = [
        ['inventory-modal', closeInventory],
        ['keypad-modal', closeKeypadModal],
        ['puzzle-modal', closePuzzleModal],
        ['pause-modal', togglePause]
      ];
      backdropClose.forEach(([id, fn]) => {
        const el = $(id);
        el.addEventListener('click', (e) => { if (e.target === el) fn(); });
      });
      // 노트(메모·관찰문)는 '읽고 넘기는' 화면이므로, 배경 여백뿐 아니라
      // 내용 어디를 눌러도 닫히게 한다. (E 재입력만 되던 불편 해소)
      $('note-modal').addEventListener('click', () => { if (pauseReasons.has('note')) closeNoteModal(); });
    }
    function refreshInventoryUI() { recalcSync(); }

    function onWindowResize() {
      if (camera && renderer) {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
      }
    }

    if (document.readyState === 'loading') document.addEventListener('DOMContentLoaded', initPageEvents);
    else initPageEvents();
  </script>
</body>
</html>
