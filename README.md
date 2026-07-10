
<!doctype html>
<html lang="zh-Hant">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>CIA 科系星球 · 營隊探索</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;600;800;900&display=swap" rel="stylesheet">
<style>
  :root{
    --lemon:#FFD60A;--lemon-soft:#FFE873;--ink:#fff;--sub:#C7D2FF;--kicker:#FFE873;
    --line:rgba(255,255,255,.14);--card:rgba(255,255,255,.05);
    --m-red:#E2553E;--m-blue:#3D7BE0;--m-green:#3FA66A;--m-yellow:#D9A03A;
    --good:#7CF0B8;--pink:#FF6FA3;--aqua:#3fe0d0;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  html,body{height:100%}
  body{font-family:"PingFang TC","Noto Sans TC","Microsoft JhengHei",system-ui,-apple-system,sans-serif;
    background:#070b22;color:var(--ink);overflow:hidden;-webkit-font-smoothing:antialiased}
  /* 宇宙背景 */
  #space{position:fixed;inset:0;z-index:0;overflow:hidden;
    background:radial-gradient(120% 90% at 18% 8%,#241a55 0%,rgba(36,26,85,0) 55%),
      radial-gradient(120% 90% at 85% 90%,#0e2a55 0%,rgba(14,42,85,0) 55%),
      linear-gradient(160deg,#0a0e2e 0%,#10103a 45%,#0a1330 100%)}
  .neb{position:absolute;inset:-10%;background:
    radial-gradient(40% 40% at 70% 25%,rgba(120,90,255,.16),transparent 70%),
    radial-gradient(45% 45% at 25% 75%,rgba(40,150,255,.14),transparent 70%);
    filter:blur(8px);animation:drift 26s ease-in-out infinite alternate}
  @keyframes drift{from{transform:translate3d(0,0,0) scale(1)}to{transform:translate3d(2%,-2%,0) scale(1.05)}}
  #stars{position:absolute;inset:0}
  .star{position:absolute;border-radius:50%;background:#fff;opacity:.7;animation:tw 4s ease-in-out infinite}
  @keyframes tw{0%,100%{opacity:.25}50%{opacity:.95}}
  #egg{position:absolute;inset:0;pointer-events:none}.egg{position:absolute;will-change:transform,opacity}
  /* 舞台 */
  #stage{position:fixed;inset:0;z-index:2;display:flex;align-items:center;justify-content:center;
    padding:clamp(64px,11vh,96px) clamp(20px,5vw,80px) clamp(20px,4.5vh,54px);transition:opacity .22s ease,transform .22s ease}
  #stage.swap{opacity:0;transform:translateY(10px) scale(.992)}
  .scene{width:100%;max-width:1120px;display:flex;flex-direction:column;align-items:center;
    text-align:center;gap:clamp(9px,1.5vh,17px);max-height:100%}
  .kicker{color:var(--kicker);font-weight:800;letter-spacing:.14em;font-size:clamp(14px,1.7vw,21px)}
  .art{width:clamp(118px,14vw,186px);height:auto;flex:0 0 auto}
  .scene.dense{gap:clamp(8px,1.25vh,15px)}
  .scene.dense .art{width:clamp(94px,10vw,138px)}
  .art svg{width:100%;height:100%;display:block;filter:drop-shadow(0 8px 26px rgba(0,0,0,.45))}
  .title{font-weight:900;line-height:1.18;font-size:clamp(26px,3.6vw,50px);text-wrap:balance}
  .title .hl{color:var(--lemon)}
  .sub{color:var(--sub);font-weight:600;line-height:1.6;font-size:clamp(17px,2vw,25px);max-width:900px}
  [data-seq]{opacity:0;transform:translateY(10px);transition:opacity .42s ease,transform .42s ease}
  [data-seq].on{opacity:1;transform:none}
  /* 測驗 */
  .vote{display:inline-flex;align-items:center;gap:.5em;color:var(--lemon-soft);font-weight:800;
    font-size:clamp(13px,1.5vw,18px);border:1px dashed rgba(255,214,10,.45);border-radius:999px;padding:.35em 1em}
  .q{font-weight:900;line-height:1.28;font-size:clamp(22px,3vw,40px);max-width:980px}
  .options{display:flex;flex-direction:column;gap:clamp(8px,1.3vh,14px);width:100%;max-width:900px}
  .opt{display:flex;align-items:center;gap:clamp(10px,1.4vw,18px);text-align:left;background:var(--card);
    border:1.5px solid var(--line);border-radius:18px;padding:clamp(11px,1.5vh,16px) clamp(14px,1.7vw,22px);transition:.3s}
  .react{width:clamp(36px,3.8vw,46px);height:clamp(36px,3.8vw,46px);flex:0 0 auto;border-radius:50%;
    background:rgba(255,255,255,.10);display:flex;align-items:center;justify-content:center;
    font-size:clamp(18px,2.1vw,25px);line-height:1}
  .react svg{width:64%;height:64%}
  .otext{font-weight:700;color:#fff;font-size:clamp(16px,1.8vw,22px);line-height:1.4}
  .check{margin-left:auto;color:var(--good);font-weight:900;font-size:clamp(20px,2.2vw,28px);opacity:0;transition:.3s}
  .options.revealed .opt{opacity:.42}
  .options.revealed .opt.correct{opacity:1;border-color:var(--lemon);
    box-shadow:0 0 0 2px rgba(255,214,10,.4),0 12px 34px rgba(255,214,10,.18);background:rgba(255,214,10,.08)}
  .options.revealed .opt.correct .check{opacity:1}
  .explain{color:var(--sub);font-weight:600;line-height:1.6;font-size:clamp(16px,1.8vw,21px);max-width:900px;
    background:rgba(61,123,224,.12);border:1px solid rgba(61,123,224,.32);border-radius:16px;padding:.8em 1.1em}
  /* 表情評分 */
  .semo{display:flex;gap:clamp(10px,1.5vw,18px);flex-wrap:wrap;justify-content:center;width:100%;max-width:780px}
  .scard{flex:1 1 150px;max-width:182px;background:var(--card);border:1.5px solid var(--line);border-radius:18px;
    padding:clamp(12px,1.8vh,18px);display:flex;flex-direction:column;align-items:center;gap:.25em}
  .scard .si{width:clamp(42px,4.6vw,56px);height:clamp(42px,4.6vw,56px);border-radius:50%;
    background:rgba(255,255,255,.09);display:flex;align-items:center;justify-content:center;
    font-size:clamp(20px,2.3vw,28px);line-height:1}
  .scard .si svg{width:64%;height:64%}
  .scard b{font-size:clamp(20px,2.3vw,28px);color:#fff}
  .scard span{color:var(--sub);font-weight:700;font-size:clamp(14px,1.5vw,18px)}
  .scard.s7{border-color:var(--pink)}.scard.s5{border-color:var(--m-green)}
  .scard.s3{border-color:var(--m-blue)}.scard.s1{border-color:rgba(159,176,216,.6)}
  .hint{color:var(--sub);font-weight:700;font-size:clamp(15px,1.6vw,19px);
    background:rgba(125,240,184,.10);border:1px solid rgba(125,240,184,.32);padding:.5em 1.1em;border-radius:999px}
  /* 全景卡片 */
  .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:clamp(10px,1.4vw,18px);width:100%;max-width:1080px}
  .grid.four{grid-template-columns:repeat(4,1fr)}
  .gcard{background:var(--card);border:1px solid rgba(255,214,10,.22);border-radius:18px;
    padding:clamp(12px,1.7vh,18px);text-align:center;display:flex;flex-direction:column;align-items:center;gap:.5em}
  .gcard .gi{width:clamp(38px,4vw,52px);height:clamp(38px,4vw,52px)}
  .gcard h4{color:var(--lemon);font-size:clamp(15px,1.7vw,20px);font-weight:900}
  .gcard p{color:var(--sub);font-size:clamp(13px,1.4vw,16px);font-weight:600;line-height:1.45}
  /* 方法步驟 */
  .steps{display:flex;flex-direction:column;gap:clamp(9px,1.3vh,14px);width:100%;max-width:880px}
  .step{display:flex;align-items:center;gap:clamp(12px,1.6vw,18px);text-align:left;background:var(--card);
    border:1px solid var(--line);border-radius:18px;padding:clamp(12px,1.6vh,18px) clamp(14px,1.8vw,22px)}
  .badge{flex:0 0 auto;width:clamp(44px,4.6vw,58px);height:clamp(44px,4.6vw,58px);border-radius:14px;
    display:flex;align-items:center;justify-content:center;font-weight:900;color:#0a0e2e;
    font-size:clamp(20px,2.2vw,28px);box-shadow:0 8px 20px rgba(0,0,0,.3)}
  .stext h4{color:#fff;font-size:clamp(17px,1.9vw,23px);font-weight:900;margin-bottom:.15em}
  .stext h4 b{color:var(--lemon)}
  .stext p{color:var(--sub);font-size:clamp(14px,1.6vw,19px);font-weight:600;line-height:1.5}
  .slido-note{color:var(--sub);font-weight:700;font-size:clamp(14px,1.5vw,18px);
    border:1px dashed var(--line);border-radius:14px;padding:.6em 1em;opacity:.9}
  /* 主頁選系 */
  .home-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:clamp(14px,2vw,30px);width:100%;max-width:960px}
  .zoom-tip{color:var(--sub);font-weight:600;font-size:clamp(10.5px,1.1vw,12.5px);opacity:.7;margin-top:6px;text-align:center}
  .dcol{display:flex;flex-direction:column;gap:10px}
  .dhead{color:var(--lemon-soft);font-weight:900;letter-spacing:.12em;font-size:clamp(15px,1.7vw,21px);
    text-align:center;padding-bottom:6px;border-bottom:1px solid var(--line)}
  .dept{display:flex;align-items:center;justify-content:center;background:var(--card);border:1.5px solid var(--line);
    border-radius:14px;padding:.85em 1em;color:#cdd6f5;font-weight:800;font-size:clamp(15px,1.7vw,21px);
    cursor:pointer;font-family:inherit;transition:.2s;position:relative}
  .dept:hover{border-color:rgba(255,214,10,.5);color:#fff;transform:translateY(-2px)}
  .dept.active{border-color:var(--lemon);color:#fff;background:rgba(255,214,10,.10);
    box-shadow:0 0 0 2px rgba(255,214,10,.35),0 10px 30px rgba(255,214,10,.16)}
  .dept.soon{opacity:.6}
  /* Part 轉場 */
  .pe{color:var(--lemon-soft);font-weight:900;letter-spacing:.34em;font-size:clamp(14px,1.6vw,20px)}
  .pno{font-weight:900;color:var(--lemon);line-height:.95;font-size:clamp(70px,12vw,160px);
    text-shadow:0 12px 44px rgba(255,214,10,.28)}
  .plabel{font-weight:900;font-size:clamp(22px,3.1vw,42px)}
  .pdots{display:flex;gap:11px}
  .pdot{width:12px;height:12px;border-radius:50%;background:rgba(255,255,255,.2)}
  .pdot.on{background:var(--lemon);box-shadow:0 0 12px rgba(255,214,10,.6)}
  .redbox{border:1.5px solid rgba(226,85,62,.75);background:rgba(226,85,62,.10);border-radius:14px;
    padding:.7em 1.1em;color:#fff;font-weight:600;font-size:clamp(14px,1.6vw,18px);line-height:1.55;max-width:840px;text-align:left}
  .redbox .rl{color:#ff9a86;font-weight:900;font-size:.82em;letter-spacing:.08em;display:block;margin-bottom:.3em}
  /* 休息頁：計時器 + 音樂（縮小版，讓其他內容/截圖有更多空間） */
  .break-wrap{display:flex;gap:clamp(10px,1.4vw,18px);flex-wrap:wrap;justify-content:center;width:100%;max-width:600px}
  .timer-card,.music-card{flex:1 1 200px;max-width:250px;background:var(--card);border:1.5px solid var(--line);
    border-radius:16px;padding:clamp(10px,1.4vh,16px) clamp(12px,1.4vw,16px);display:flex;flex-direction:column;
    align-items:center;gap:8px}
  .timer-digits{font-weight:900;font-size:clamp(26px,3.8vw,38px);color:var(--lemon);letter-spacing:.02em;
    font-variant-numeric:tabular-nums;text-shadow:0 6px 18px rgba(255,214,10,.25)}
  .timer-btns{display:flex;gap:6px;align-items:center;flex-wrap:wrap;justify-content:center}
  .timer-set{display:flex;gap:6px;align-items:center;justify-content:center;width:100%}
  .timer-set input[type=number]{width:70px;background:rgba(255,255,255,.08);border:1.5px solid var(--line);
    border-radius:999px;color:#fff;font-weight:800;font-size:13px;padding:.4em .7em;text-align:center;
    font-family:inherit}
  .timer-set input[type=number]::-webkit-outer-spin-button,.timer-set input[type=number]::-webkit-inner-spin-button{
    -webkit-appearance:none;margin:0}
  .timer-set input[type=number]:focus{outline:none;border-color:rgba(255,214,10,.6)}
  .tbtn{background:rgba(255,255,255,.08);border:1.5px solid var(--line);color:#fff;font-weight:800;
    font-size:clamp(11px,1.1vw,13px);border-radius:999px;padding:.4em .85em;cursor:pointer;font-family:inherit;
    transition:.2s}
  .tbtn:hover{border-color:rgba(255,214,10,.5);background:rgba(255,214,10,.12)}
  .tbtn-main{background:var(--lemon);color:#0a0e2e;border-color:var(--lemon);padding:.4em 1.1em}
  .tbtn-main:hover{background:var(--lemon-soft)}
  .tbtn-ghost{opacity:.75;font-size:clamp(10px,1vw,12px)}
  /* 背景音樂按鈕 */
  .music-btn{display:inline-flex;align-items:center;gap:.5em;font-family:'Noto Sans TC',sans-serif;font-weight:700;
    font-size:clamp(15px,1.5vw,20px);color:var(--aqua);background:rgba(63,224,208,.12);
    border:1.5px solid rgba(63,224,208,.45);border-radius:999px;padding:.55em 1.3em;cursor:pointer;
    transition:transform .2s ease, background .2s ease, border-color .2s ease}
  .music-btn:hover{background:rgba(63,224,208,.22);transform:translateY(-2px)}
  .music-btn:active{transform:scale(.96)}
  .music-btn .mb-ic{font-size:1.1em}
  .music-btn.playing{color:var(--lemon);background:rgba(255,214,59,.15);border-color:rgba(255,214,59,.55)}
  .music-btn.playing .mb-ic{animation:mbPulse 1.1s ease-in-out infinite}
  @keyframes mbPulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.55;transform:scale(.86)}}
  /* 音樂列：播放按鈕 + 音量滑桿 */
  .music-row{width:100%;display:flex;justify-content:center}
  .music-bar{display:inline-flex;align-items:center;gap:clamp(12px,1.6vw,22px);flex-wrap:wrap;justify-content:center}
  .vol-box{display:inline-flex;align-items:center;gap:.5em;background:rgba(63,224,208,.1);border:1.5px solid rgba(63,224,208,.35);border-radius:999px;padding:.4em 1em}
  .vol-box .vol-ic{font-size:1.05em;line-height:1;min-width:1.2em;text-align:center}
  .vol-slider{-webkit-appearance:none;appearance:none;width:clamp(90px,11vw,150px);height:6px;border-radius:3px;
    background:linear-gradient(to right,var(--aqua) 0%,var(--aqua) 60%,rgba(63,224,208,.22) 60%,rgba(63,224,208,.22) 100%);
    cursor:pointer}
  .vol-slider::-webkit-slider-thumb{-webkit-appearance:none;appearance:none;width:15px;height:15px;border-radius:50%;
    background:var(--aqua);cursor:pointer;box-shadow:0 2px 6px rgba(0,0,0,.4)}
  .vol-slider::-moz-range-thumb{width:15px;height:15px;border-radius:50%;border:none;background:var(--aqua);cursor:pointer}
  .prog-row{display:flex;align-items:center;gap:6px;width:100%;color:var(--sub);font-size:11px;font-variant-numeric:tabular-nums}
  .prog-row input[type=range]{flex:1;accent-color:var(--lemon);height:4px}
  .music-hint{color:var(--sub);font-weight:600;font-size:clamp(10px,1vw,11.5px);text-align:center;opacity:.85}
  .shotcap{color:var(--lemon-soft);font-weight:800;font-size:clamp(13px,1.5vw,17px)}
  .shot{display:flex;justify-content:center;width:100%}
  .shot img{max-width:min(1280px,97vw);max-height:74vh;width:auto;height:auto;border-radius:14px;
    border:1px solid rgba(255,255,255,.18);box-shadow:0 16px 46px rgba(0,0,0,.5);background:#fff}
  .shot.sm img{max-height:52vh}
  .shot.shotph{align-items:center}
  .shotph-box{width:100%;max-width:640px;aspect-ratio:16/9;border:2.5px dashed rgba(255,214,10,.5);
    border-radius:16px;display:flex;align-items:center;justify-content:center;background:rgba(255,255,255,.04);
    color:var(--lemon-soft);font-weight:800;font-size:clamp(16px,2vw,22px);letter-spacing:.04em}
  .shotfoot{color:#fff;font-weight:900;font-size:clamp(21px,2.7vw,36px);letter-spacing:.02em;margin-top:2px}
  /* HUD */
  #hud{position:fixed;z-index:5;left:0;right:0;bottom:0;display:flex;align-items:center;gap:10px;
    padding:12px clamp(14px,3vw,28px);pointer-events:none}
  #hud>*{pointer-events:auto}
  #stageBar{position:fixed;top:0;left:0;right:0;z-index:6;padding:clamp(10px,1.8vh,18px) clamp(16px,3.5vw,40px) 8px;
    pointer-events:none;background:linear-gradient(to bottom,rgba(7,11,34,.72),transparent)}
  .sb-row{display:flex;align-items:flex-start;width:100%}
  .sb-dotcol{display:flex;flex-direction:column;align-items:center;flex:0 0 auto}
  .sb-dot{width:11px;height:11px;border-radius:50%;background:rgba(255,255,255,.25);border:2px solid rgba(255,255,255,.35);
    flex:0 0 auto;transition:.25s}
  .sb-dot.done{background:var(--lemon);border-color:var(--lemon)}
  .sb-dot.active{background:var(--lemon);border-color:#fff;box-shadow:0 0 0 4px rgba(255,214,10,.28);width:14px;height:14px}
  .sb-time{margin-top:4px;font-size:clamp(8px,.85vw,10px);font-weight:700;color:rgba(255,255,255,.4);white-space:nowrap}
  .sb-time.active{color:var(--lemon-soft)}
  .sb-time.done{color:rgba(255,255,255,.7)}
  .sb-seg{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:flex-start;position:relative;
    min-width:6px;padding:0 2px}
  .sb-seg.sb-seg-end{flex:0 0 auto;min-width:0}
  .sb-segline{width:100%;height:2px;background:rgba(255,255,255,.18);margin-top:4.5px}
  .sb-seg.done .sb-segline,.sb-seg.active .sb-segline{background:var(--lemon)}
  .sb-seglabel{font-size:clamp(8.5px,.95vw,11px);font-weight:800;color:rgba(255,255,255,.5);white-space:nowrap;
    margin-bottom:2px}
  .sb-seg.active .sb-seglabel{color:var(--lemon)}
  .sb-seg.done .sb-seglabel{color:rgba(255,255,255,.75)}
  @media(max-width:680px){.sb-seglabel{font-size:7.5px}#stageBar{padding-top:6px}}
  .hbtn{background:rgba(255,255,255,.07);border:1px solid var(--line);color:#fff;font-weight:800;font-size:14px;
    border-radius:999px;padding:.5em 1em;cursor:pointer;font-family:inherit;transition:.2s}
  .hbtn:hover{background:rgba(255,214,10,.16);border-color:rgba(255,214,10,.5)}
  #chapter{color:var(--lemon-soft);font-weight:800;font-size:14px}
  #progress{margin-left:auto;color:rgba(255,255,255,.5);font-weight:700;font-size:13px;letter-spacing:.05em}
  #ophint{position:fixed;left:50%;bottom:13px;transform:translateX(-50%);z-index:4;color:rgba(255,255,255,.28);
    font-size:12px;font-weight:600;letter-spacing:.04em;pointer-events:none;white-space:nowrap}
  @media(max-width:680px){#ophint{display:none}.grid,.grid.four{grid-template-columns:repeat(2,1fr)}
    .home-grid{grid-template-columns:1fr}}
  /* 選單 / 彈窗 */
  .overlay{position:fixed;inset:0;z-index:9;background:rgba(7,11,34,.86);backdrop-filter:blur(6px);
    display:none;align-items:center;justify-content:center;padding:24px}
  .overlay.open{display:flex}
  /* 章節導覽：靠左側的抽屜面板，背景半透明可以看到目前頁面 */
  .overlay#menu{align-items:stretch;justify-content:flex-start;padding:0;
    background:rgba(7,11,34,.45);backdrop-filter:blur(1.5px)}
  .overlay#menu .mpanel{width:min(80vw,860px);max-width:860px;height:100%;max-height:100%;
    border-radius:0 22px 22px 0;box-shadow:24px 0 60px rgba(0,0,0,.5)}
  .mpanel{position:relative;width:100%;max-width:920px;max-height:86vh;overflow:auto;background:rgba(16,18,52,.96);
    border:1px solid var(--line);border-radius:24px;padding:clamp(20px,3vw,34px)}
  .mpanel h3{color:var(--lemon);font-size:clamp(18px,2vw,24px);margin-bottom:14px}
  .mcols{display:flex;gap:14px;align-items:flex-start;overflow-x:auto;padding-bottom:6px}
  .mcol{flex:0 0 clamp(180px,26vw,224px);max-width:224px;display:flex;flex-direction:column}
  .mcolhead{color:var(--lemon-soft);font-weight:900;font-size:12.5px;letter-spacing:.08em;margin-bottom:8px;
    padding-bottom:8px;border-bottom:1px solid var(--line)}
  .msession{color:var(--lemon);font-weight:900;font-size:12px;letter-spacing:.14em;margin:8px 0 6px}
  .msession.pmsession{margin-top:14px;padding-top:12px;border-top:1px solid rgba(255,214,10,.4)}
  .mitem{display:flex;gap:.6em;width:100%;text-align:left;background:rgba(255,255,255,.05);border:1px solid var(--line);
    color:#fff;border-radius:11px;padding:.6em .9em;margin-bottom:6px;font-family:inherit;font-weight:700;
    font-size:14.5px;cursor:pointer;transition:.18s}
  .mitem:hover{background:rgba(255,214,10,.14);border-color:rgba(255,214,10,.5)}
  .mitem .pg{color:var(--lemon);font-weight:900;min-width:2.6em}
  .mitem .prange{margin-left:auto;color:var(--sub);font-weight:700;font-size:12px;opacity:.85}
  .mitem.mfolder{border-style:dashed}
  .mitem.sel{background:rgba(255,214,10,.16);border-color:rgba(255,214,10,.55);color:#fff}
  .mclose{position:absolute;top:18px;right:22px;background:none;border:none;color:#fff;font-size:30px;cursor:pointer}
  .soonbox{max-width:460px;text-align:center}
  .soonbox h3{color:var(--lemon);font-size:clamp(20px,2.4vw,28px);margin-bottom:12px}
  .soonbox p{color:var(--sub);font-weight:600;line-height:1.6;font-size:clamp(15px,1.7vw,19px);margin-bottom:18px}
  #fade{position:fixed;inset:0;z-index:3;pointer-events:none;opacity:0;
    background:radial-gradient(60% 60% at 50% 50%,rgba(160,130,255,.18),transparent 70%);transition:opacity .22s ease}

  /* ===== 開場暖身（嵌入簡報）專屬樣式 ===== */
  .scene-inner{max-width:1080px;width:100%;display:flex;flex-direction:column;align-items:center;gap:2.6vh;margin:0 auto}
  .scene-inner.wide{max-width:1240px}
  .h-mid{font-weight:700;font-size:clamp(28px,3.6vw,48px);line-height:1.3}
  .lead{font-size:clamp(20px,2.4vw,30px);color:var(--sub);line-height:1.6;font-weight:400;max-width:880px}
  .hl-aqua{color:#3fe0d0} .hl-coral{color:#ff8c7a}
  .art-xl svg{width:clamp(180px,24vw,320px)}
  .art-hero svg{width:clamp(170px,22vw,300px)}
  .art-lg svg{width:clamp(150px,18vw,240px)}
  .art-scene svg{width:clamp(320px,42vw,560px);max-height:52vh}
  .art-notion svg{width:clamp(360px,46vw,620px);filter:drop-shadow(0 20px 50px rgba(0,0,0,.4));max-height:48vh}
  .cover-sub{font-family:'Outfit',sans-serif;letter-spacing:.4em;text-transform:uppercase;color:#3fe0d0;font-size:clamp(14px,1.6vw,20px);font-weight:600}
  .cover-title{white-space:nowrap}
  .cover-title.h-mega{font-size:clamp(32px,5.2vw,72px)}
  .bigtime{font-family:'Outfit',sans-serif;font-weight:900;font-size:clamp(60px,11vw,150px);line-height:1;color:var(--lemon);text-shadow:0 0 60px rgba(255,214,59,.4)}
  .bigtime.xl{font-size:clamp(76px,13vw,180px)}
  .split{display:flex;align-items:center;justify-content:center;gap:clamp(20px,4vw,56px);width:100%;flex-wrap:wrap}
  .split-l{flex:1;min-width:280px;display:flex;flex-direction:column;gap:1.2vh;align-items:flex-start;text-align:left}
  .split-r{flex:1;min-width:260px;display:flex;justify-content:center;align-items:center}
  .split .h-mega,.split .h-big{text-align:left}
  .split-h{font-size:clamp(32px,4.6vw,68px);line-height:1.16}
  .center-split{max-width:860px;margin:0 auto;gap:clamp(16px,2.5vw,44px)}
  .center-split .split-l{padding-left:clamp(0px,1.5vw,22px)}
  .choose-h{white-space:nowrap;font-size:clamp(24px,3.8vw,54px)}
  .action-hint{display:inline-flex;align-items:center;gap:.6em;color:#070b1f;background:#3fe0d0;font-weight:800;
    padding:.55em 1.4em;border-radius:999px;font-size:clamp(16px,2vw,26px);box-shadow:0 10px 30px rgba(63,224,208,.35);line-height:1.3}
  .action-hint .ah-emoji{width:1.3em;height:1.3em;display:inline-block;flex-shrink:0}
  .action-hint .ah-emoji svg{width:100%;height:100%}
  .op-cards{display:grid;gap:clamp(16px,2vw,26px);width:100%}
  .op-cards.c3{grid-template-columns:repeat(3,1fr)}
  .op-cards.c4{grid-template-columns:repeat(4,1fr)}
  .op-cards.c2{grid-template-columns:repeat(2,1fr)}
  .op-promo{display:flex;align-items:center;justify-content:center;gap:clamp(16px,2.4vw,36px);margin-top:1.4vh;
    background:linear-gradient(120deg,rgba(255,214,10,.16),rgba(63,224,208,.12));border:2px dashed rgba(255,214,10,.55);
    border-radius:20px;padding:clamp(14px,1.8vw,24px) clamp(20px,3vw,44px)}
  .op-promo-l{font-weight:900;font-size:clamp(16px,1.7vw,23px);color:#fff;line-height:1.3;text-align:right}
  .op-promo-note{font-weight:700;font-size:clamp(11px,1.1vw,14.5px);color:var(--sub)}
  .op-promo-code{font-family:'Outfit',sans-serif;font-weight:900;letter-spacing:.08em;font-size:clamp(32px,4.6vw,62px);
    color:var(--lemon);text-shadow:0 4px 20px rgba(255,214,10,.4);background:rgba(13,19,48,.5);
    border-radius:14px;padding:.1em .35em}
  .op-time-badge{display:inline-flex;align-items:center;gap:.5em;font-weight:800;font-size:clamp(16px,1.9vw,25px);color:var(--lemon);
    background:rgba(255,214,10,.12);border:2px solid rgba(255,214,10,.45);border-radius:999px;padding:.5em 1.3em;margin-top:.8vh}
  .op-card{background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.12);border-radius:20px;
    padding:clamp(18px,2.2vw,32px);text-align:left;display:flex;flex-direction:column;gap:.5em;backdrop-filter:blur(6px)}
  .op-card .ic{font-size:clamp(32px,3.4vw,48px);line-height:1}
  .op-card h3{font-weight:900;font-size:clamp(20px,2.2vw,30px)}
  .op-card p{color:var(--sub);font-size:clamp(14px,1.3vw,18px);line-height:1.5}
  .op-cards.big-cards .op-card{align-items:center;text-align:center;gap:.8em;padding:clamp(22px,2.6vw,40px);justify-content:flex-start}
  .op-card-art{width:clamp(60px,7vw,100px);height:clamp(60px,7vh,100px);display:flex;align-items:center;justify-content:center;margin-bottom:.2em}
  .op-card-art svg{height:100%;width:auto;max-width:100%}
  .op-cards.big-cards h3{font-size:clamp(24px,2.8vw,38px)}
  .op-steps{list-style:none;display:flex;flex-direction:column;gap:1.2vh;text-align:left}
  .op-steps li{display:flex;align-items:center;gap:.7em;font-size:clamp(18px,2vw,26px);color:var(--sub)}
  .op-steps li b{color:#fff}
  .op-step-n{width:1.5em;height:1.5em;border-radius:50%;background:var(--lemon);color:#070b1f;
    font-family:'Outfit',sans-serif;font-weight:800;display:flex;align-items:center;justify-content:center;font-size:.8em;flex-shrink:0}
  .meet-bar{display:flex;justify-content:center;margin:1vh 0}
  .op-emoji-bar{display:inline-flex;align-items:center;gap:clamp(6px,1vw,14px);
    background:#1c1c1f;border:1px solid #34343a;border-radius:999px;padding:clamp(10px,1.2vw,16px) clamp(14px,1.6vw,22px);
    box-shadow:0 14px 40px rgba(0,0,0,.5)}
  .op-emoji{width:clamp(32px,3.6vw,52px);height:clamp(32px,3.6vw,52px);border-radius:50%;transition:transform .2s}
  .op-emoji svg{width:100%;height:100%;display:block}
  .op-emoji:hover{transform:translateY(-6px) scale(1.12)}
  .check-row{display:flex;flex-direction:column;gap:1.2vh;align-items:flex-start;background:rgba(255,255,255,.04);
    border:1px solid rgba(255,255,255,.1);border-radius:20px;padding:clamp(16px,2vw,28px) clamp(20px,2.4vw,36px)}
  .check-item{display:flex;align-items:center;gap:.7em;font-size:clamp(18px,2vw,26px);font-weight:500}
  .ci-emoji{width:1.4em;height:1.4em;display:inline-block;flex-shrink:0}
  .ci-emoji svg{width:100%;height:100%}
  .grad-row{display:flex;align-items:flex-end;justify-content:center;gap:clamp(4px,1.2vw,22px);width:100%;flex-wrap:wrap}
  .grad-fig{width:clamp(64px,9vw,120px)}
  .grad-fig.big{width:clamp(88px,12vw,160px)}
  .deco-row{display:flex;align-items:center;justify-content:center;gap:clamp(12px,2vw,32px);flex-wrap:wrap}
  .deco{width:clamp(48px,6vw,96px)}
  .move-split{display:flex;align-items:center;gap:clamp(20px,4vw,56px);width:100%}
  .move-list{flex:1.05;display:flex;flex-direction:column;gap:clamp(8px,1.2vw,16px);min-width:0}
  .move-row{display:flex;align-items:center;gap:clamp(10px,1.3vw,20px);border-radius:14px;padding:clamp(10px,1.3vw,18px) clamp(14px,1.6vw,22px);
    border:1px solid rgba(255,255,255,.12);border-left:6px solid var(--row-c,#FFD60A);background:linear-gradient(100deg,var(--row-bg,rgba(255,214,10,.12)),rgba(255,255,255,.03))}
  .move-row .mr-letter{font-family:'Outfit',sans-serif;font-weight:900;font-size:clamp(28px,3.4vw,48px);line-height:1;color:var(--row-c,#FFD60A);flex-shrink:0;width:1.1em;text-align:center}
  .move-row .mr-en{font-family:'Outfit',sans-serif;font-weight:700;letter-spacing:.14em;text-transform:uppercase;font-size:clamp(11px,1.1vw,15px);color:var(--row-c,#FFD60A);opacity:.95}
  .move-row .mr-tc{font-weight:900;font-size:clamp(18px,2vw,28px);line-height:1.1;margin:.05em 0 .15em}
  .move-row .mr-desc{color:var(--sub);font-size:clamp(12px,1.2vw,17px);line-height:1.45}
  .move-row.cell-major{--row-c:#e06a55;--row-bg:rgba(224,106,85,.14)}
  .move-row.cell-oper{--row-c:#5b7bff;--row-bg:rgba(91,123,255,.14)}
  .move-row.cell-vision{--row-c:#46c46a;--row-bg:rgba(70,196,106,.14)}
  .move-row.cell-exp{--row-c:#d9b73a;--row-bg:rgba(217,183,58,.14)}
  .move-art{flex:.95;position:relative;height:clamp(180px,28vh,300px);display:flex;align-items:center;justify-content:center}
  .ma-img{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;opacity:0;transform:scale(.85);
    transition:opacity .45s ease, transform .45s cubic-bezier(.22,.61,.36,1);pointer-events:none}
  .ma-img svg{width:clamp(150px,20vw,280px);height:auto;max-height:100%}
  .ma-img.show{opacity:1;transform:scale(1)}
  @media (max-width:820px){
    .op-cards.c3,.move-split{grid-template-columns:1fr}
    .move-split{flex-direction:column}
    .move-art{height:clamp(140px,24vh,220px);order:-1}
    .split{flex-direction:column}.split-l{text-align:center;align-items:center}
    .cover-title{white-space:normal}.choose-h{white-space:normal}
  }

  @media (prefers-reduced-motion: reduce){.neb,.star{animation:none!important}#stage{transition:none}
    [data-seq]{transition:opacity .01s}}
</style>
</head>
<body>
  <div id="space"><div class="neb"></div><div id="stars"></div><div id="egg"></div></div>
  <div id="fade"></div>
  <div id="ytWrap" style="position:fixed;right:6px;bottom:6px;width:8px;height:8px;overflow:hidden;opacity:.01;pointer-events:none;z-index:1"><div id="ytPlayer"></div></div>
  <main id="stage"></main>

  <div id="hud">
    <button class="hbtn" id="homeBtn">🏠 主頁</button>
    <button class="hbtn" id="menuBtn">☰ 章節</button>
    <div id="chapter"></div>
  </div>
  <div id="ophint">操作方式：點畫面 / → 前進，← 後退，M 章節，H 主頁，F 全螢幕</div>

  <div class="overlay" id="menu"><div class="mpanel"><button class="mclose" id="menuClose">×</button>
    <h3>章節導覽（點分類 → Part → 頁碼，逐欄往右展開）</h3><div id="menuList" class="mcols"></div></div></div>

  <div class="overlay" id="soon"><div class="mpanel soonbox"><button class="mclose" id="soonClose">×</button>
    <h3 id="soonTitle"></h3><p id="soonMsg"></p>
    <button class="hbtn" id="soonBack" style="border-color:rgba(255,214,10,.5)">返回主頁重選</button></div></div>

<script>
/* ===== SVG 插畫庫 ===== */
const I={
 chip:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round"><rect x="34" y="34" width="52" height="52" rx="8" fill="rgba(255,214,10,.12)"/><rect x="48" y="48" width="24" height="24" rx="4" fill="#3D7BE0"/>${[40,52,64,76].map(y=>`<line x1="20" y1="${y}" x2="34" y2="${y}"/><line x1="86" y1="${y}" x2="100" y2="${y}"/>`).join('')}${[40,52,64,76].map(x=>`<line x1="${x}" y1="20" x2="${x}" y2="34"/><line x1="${x}" y1="86" x2="${x}" y2="100"/>`).join('')}</g></svg>`,
 circuit:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M16 60 H40 M80 60 H104"/><rect x="40" y="48" width="40" height="24" rx="6" fill="rgba(61,123,224,.25)"/><path d="M60 16 V40 M60 80 V104"/><circle cx="16" cy="60" r="5" fill="#FFD60A"/><circle cx="104" cy="60" r="5" fill="#FFD60A"/><circle cx="60" cy="16" r="5" fill="#3FA66A"/><circle cx="60" cy="104" r="5" fill="#3FA66A"/></g></svg>`,
 antenna:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round"><path d="M60 96 V52"/><circle cx="60" cy="46" r="8" fill="#FFD60A"/><path d="M44 96 H76"/><path d="M40 40a28 28 0 0 1 40 0" stroke="#3D7BE0"/><path d="M30 30a42 42 0 0 1 60 0" stroke="rgba(61,123,224,.55)"/></g></svg>`,
 rocket:`<svg viewBox="0 0 120 120"><g stroke-linejoin="round"><path d="M60 14c14 10 20 28 20 46l-12 12H52L40 60c0-18 6-36 20-46Z" fill="rgba(255,214,10,.15)" stroke="#FFD60A" stroke-width="3"/><circle cx="60" cy="48" r="9" fill="#3D7BE0" stroke="#fff" stroke-width="2"/><path d="M40 72l-12 8 12 2Z M80 72l12 8-12 2Z" fill="#E2553E"/><path d="M52 84h16l-4 18-4 6-4-6Z" fill="#FFD60A"/></g></svg>`,
 planet:`<svg viewBox="0 0 120 120"><circle cx="60" cy="56" r="28" fill="rgba(61,123,224,.3)" stroke="#FFD60A" stroke-width="3"/><ellipse cx="60" cy="60" rx="46" ry="14" fill="none" stroke="#FFE873" stroke-width="3" transform="rotate(-18 60 60)"/><circle cx="50" cy="48" r="5" fill="rgba(255,255,255,.4)"/></svg>`,
 astronaut:`<svg viewBox="0 0 120 120"><g stroke="#FFD60A" stroke-width="3"><circle cx="60" cy="40" r="20" fill="rgba(255,255,255,.92)"/><path d="M48 38a14 12 0 0 1 24 0Z" fill="#3D7BE0"/><rect x="42" y="60" width="36" height="34" rx="12" fill="rgba(255,255,255,.85)"/><path d="M42 70l-12 10 M78 70l12-2" stroke-linecap="round"/></g></svg>`,
 lightbulb:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round"><path d="M60 20a26 26 0 0 1 16 46c-4 3-6 7-6 12H50c0-5-2-9-6-12a26 26 0 0 1 16-46Z" fill="rgba(255,214,10,.16)"/><path d="M50 90h20 M53 100h14"/><path d="M60 8v8 M22 30l6 6 M98 30l-6 6" stroke="#FFE873"/></g></svg>`,
 gear:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3"><circle cx="60" cy="60" r="20" fill="rgba(63,166,106,.25)"/><circle cx="60" cy="60" r="8"/>${Array.from({length:8}).map((_,i)=>{const a=i*45*Math.PI/180;return `<line x1="${(60+24*Math.cos(a)).toFixed(1)}" y1="${(60+24*Math.sin(a)).toFixed(1)}" x2="${(60+33*Math.cos(a)).toFixed(1)}" y2="${(60+33*Math.sin(a)).toFixed(1)}" stroke-linecap="round"/>`}).join('')}</g></svg>`,
 telescope:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><rect x="30" y="44" width="52" height="18" rx="6" fill="rgba(61,123,224,.25)" transform="rotate(-20 56 53)"/><path d="M50 64L42 98 M64 58l14 30"/><path d="M86 30l4 4 M96 24l5 1" stroke="#FFE873"/></g></svg>`,
 trophy:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M40 28h40v18a20 20 0 0 1-40 0Z" fill="rgba(255,214,10,.2)"/><path d="M40 32H26v8a14 14 0 0 0 14 12 M80 32h14v8a14 14 0 0 1-14 12"/><path d="M60 66v16 M46 94h28 M52 82h16v12H52Z" fill="rgba(255,214,10,.12)"/></g></svg>`,
 question:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round"><circle cx="60" cy="60" r="34" fill="rgba(61,123,224,.2)"/><path d="M48 50a12 12 0 0 1 22 6c0 8-10 8-10 16" stroke-width="4"/><circle cx="60" cy="86" r="3.4" fill="#FFD60A" stroke="none"/></g></svg>`,
 lunch:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linejoin="round"><rect x="28" y="46" width="64" height="44" rx="10" fill="rgba(226,85,62,.25)"/><path d="M28 64h64"/><circle cx="46" cy="55" r="4" fill="#3FA66A"/><rect x="58" y="51" width="22" height="8" rx="4" fill="#FFE873"/><path d="M40 36c0-6 6-6 6 0 M58 34c0-6 6-6 6 0 M76 36c0-6 6-6 6 0" stroke="#FFE873"/></g></svg>`,
 notion:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linejoin="round"><rect x="34" y="24" width="52" height="72" rx="8" fill="rgba(255,255,255,.06)"/><path d="M46 42h28 M46 56h28 M46 70h18" stroke-linecap="round"/></g></svg>`,
 star:`<svg viewBox="0 0 120 120"><path d="M60 22l11 24 26 3-19 18 5 26-23-13-23 13 5-26-19-18 26-3Z" fill="rgba(255,214,10,.2)" stroke="#FFD60A" stroke-width="3" stroke-linejoin="round"/></svg>`,
 rise:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M26 86L52 60l16 14 26-30"/><path d="M84 44h16v16"/><circle cx="100" cy="30" r="3" fill="#FFE873" stroke="none"/></g></svg>`,
 reflect:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round"><circle cx="56" cy="54" r="26" fill="rgba(61,123,224,.2)"/><path d="M48 52a10 8 0 0 1 18 0"/><path d="M86 78a18 18 0 1 1-6-13" stroke="#FFE873"/><path d="M80 56v10h-10" stroke="#FFE873"/></g></svg>`,
 film:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linejoin="round"><rect x="26" y="34" width="68" height="52" rx="10" fill="rgba(61,123,224,.2)"/><path d="M52 50l20 12-20 12Z" fill="#FFD60A"/></g></svg>`,
 hand:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M48 60V36a6 6 0 0 1 12 0v20 M60 56V32a6 6 0 0 1 12 0v28 M72 60V42a6 6 0 0 1 12 0v30c0 14-10 22-24 22-12 0-18-6-24-16l-8-14a6 6 0 0 1 10-7l6 8" fill="rgba(255,214,10,.12)"/></g></svg>`,
 flag:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M42 24v72"/><path d="M42 28h40l-8 12 8 12H42Z" fill="rgba(226,85,62,.3)"/></g></svg>`,
 path:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round"><path d="M30 94c10-20 0-28 16-40s10-30 30-40" stroke-dasharray="2 9"/><circle cx="30" cy="94" r="5" fill="#3FA66A"/><circle cx="76" cy="14" r="6" fill="#FFD60A"/></g></svg>`,
 car:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linejoin="round"><path d="M24 70l8-18h44l12 18h8a6 6 0 0 1 6 6v8H22v-8a6 6 0 0 1 6-6Z" fill="rgba(61,123,224,.25)"/><circle cx="42" cy="84" r="7"/><circle cx="84" cy="84" r="7"/><path d="M40 52l2-8h28" stroke="#FFE873"/></g></svg>`,
 brain:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linejoin="round"><path d="M52 30a14 14 0 0 0-14 18 12 12 0 0 0 0 22 12 12 0 0 0 14 14V30Z" fill="rgba(63,166,106,.22)"/><path d="M68 30a14 14 0 0 1 14 18 12 12 0 0 1 0 22 12 12 0 0 1-14 14V30Z" fill="rgba(255,214,10,.14)"/></g></svg>`,
 pulse:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><circle cx="60" cy="60" r="34" stroke="#3D7BE0"/><path d="M30 60h12l6-16 10 32 8-22 6 6h10"/></g></svg>`,
 energy:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linejoin="round" stroke-linecap="round"><path d="M64 22L40 64h18l-6 34 30-46H62Z" fill="rgba(255,214,10,.2)"/></g></svg>`,
 cpu:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3"><rect x="38" y="38" width="44" height="44" rx="6" fill="rgba(61,123,224,.22)"/><rect x="50" y="50" width="20" height="20" rx="3"/><path d="M50 30v8 M70 30v8 M50 82v8 M70 82v8 M30 50h8 M30 70h8 M82 50h8 M82 70h8" stroke-linecap="round"/></g></svg>`,
 coffee:`<svg viewBox="0 0 120 120"><g fill="none" stroke="#FFD60A" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M32 46h44v26a22 22 0 0 1-22 22h-0a22 22 0 0 1-22-22V46Z" fill="rgba(255,214,10,.14)"/><path d="M76 52h8a12 12 0 0 1 0 24h-8"/><path d="M40 30c0-6 6-6 6 0 M52 26c0-6 6-6 6 0 M64 30c0-6 6-6 6 0" stroke="#FFE873"/></g></svg>`,
};
/* 反應圖示（統一風格） */
const R={
 heart:`<svg viewBox="0 0 24 24"><path d="M12 21s-8-5-8-11a4.5 4.5 0 0 1 8-3 4.5 4.5 0 0 1 8 3c0 6-8 11-8 11Z" fill="#FF6FA3"/></svg>`,
 thumb:`<svg viewBox="0 0 24 24"><path d="M8 10l4-7c2 0 3 1 3 3v3h4a2 2 0 0 1 2 2l-2 7a2 2 0 0 1-2 1H8Z" fill="#FFD60A"/><rect x="3" y="10" width="4" height="11" rx="1" fill="#FFE873"/></svg>`,
 smile:`<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10" fill="#FFD60A"/><circle cx="8.4" cy="10" r="1.5" fill="#0a0e2e"/><circle cx="15.6" cy="10" r="1.5" fill="#0a0e2e"/><path d="M7.4 13.4a5 4.4 0 0 0 9.2 0Z" fill="#0a0e2e"/></svg>`,
 clap:`<svg viewBox="0 0 24 24"><path d="M9 13l-3-3a1.6 1.6 0 0 1 2-2l5 4 4-3a1.6 1.6 0 0 1 2 3l-6 7-7-2Z" fill="#FFB84D"/><path d="M5 4l1 3 M3 9l3 1 M9 3l1 3" stroke="#FFE873" stroke-width="1.6" stroke-linecap="round"/></svg>`,
 down:`<svg viewBox="0 0 24 24"><path d="M16 14l-4 7c-2 0-3-1-3-3v-3H5a2 2 0 0 1-2-2l2-7a2 2 0 0 1 2-1h9Z" fill="#9FB0D8"/><rect x="17" y="3" width="4" height="11" rx="1" fill="#C2D0EE"/></svg>`,
};
const QEMO=['❤️','👍','🎉','👏'];                              /* 題目選項：❤️👍🎉👏 */
const SCORE=[{i:R.heart,s:'7 分',t:'非常喜歡',c:'s7'},{i:R.thumb,s:'5 分',t:'喜歡',c:'s5'},
             {i:R.clap,s:'3 分',t:'還好',c:'s3'},{i:R.down,s:'1 分',t:'不太喜歡',c:'s1'}]; /* 評分：❤️7 👍5 👏3 👎1 */
const SCORE_DENTAL=[
  {i:'❤️',s:'7 分',t:'非常喜歡，期待能深入研究此領域內容',c:'s7'},
  {i:'👍',s:'5～6 分',t:'感興趣，期待能更深入了解',c:'s5'},
  {i:'🎉',s:'4 分',t:'不確定是否合適，但會想要進一步了解',c:'s3'},
  {i:'👏',s:'1～3 分',t:'沒什麼興趣或會排斥，不會主動接觸學習',c:'s1'}];
const PCOL=['var(--m-blue)','var(--m-green)','var(--m-yellow)','var(--m-red)'];

/* ===== 主頁營隊 ===== */
const DEPTS=[
 {g:'一類組',items:['法律營','商管營','財經營','行銷營']},
 {g:'二類組',items:['電機營','資工營','AI 營','材料營']},
 {g:'三類組',items:['牙醫營','醫學營','藥學營','心理營']},
];
let currentCamp=null; /* 目前瀏覽中的營隊，用來讓「☰ 章節」選單只顯示該營隊自己的分類 */
const SHOTS={
5:"images/img001.png",
7:"images/img002.png",
11:"images/img003.png",
13:"images/img004.png",
16:"images/img005.png",
22:"images/img006.png",
25:"images/img007.png",
27:"images/img008.png"
};

/* ===== 場景 ===== */
const SCENES=[
{"ch":"主頁","m":"主頁 · 選擇營隊","type":"home"},
{"ch":"科系所學","p":"Part 1","m":"Part 1：互動提問 → Before","type":"part","no":1,"total":3,"chLabel":"科系所學","title":"前導 · 互動提問 → 寫 Before"},
{"ch":"科系所學","p":"Part 1","m":"測驗 · 品牌力 4P","type":"quiz","noans":true,"kicker":"科系所學 · 第 1 題","art":"star","q":"一個商品要成功賣出去，行銷人會同時顧好哪四件事（行銷 4P）？","opts":["拍照、發文、按讚、分享","產品、價格、通路、促銷","顏色、字型、Logo、包裝","老闆、員工、客人、對手"],"ans":1},
{"ch":"科系所學","p":"Part 1","m":"測驗 · 社群擴散","type":"quiz","noans":true,"kicker":"科系所學 · 第 2 題","art":"rise","q":"一支影片在 IG、TikTok 被瘋狂轉發、一夜爆紅，行銷上最接近哪個詞？","opts":["網紅經濟","內容農場","病毒行銷","演算法作弊"],"ans":2},
{"ch":"科系所學","p":"Part 1","m":"測驗 · 選擇校系","type":"quiz","noans":true,"kicker":"科系所學 · 第 3 題","art":"path","q":"想走行銷，大學一定要唸「行銷系」嗎？","opts":["對，只有行銷系能做行銷","要先當網紅才有資格唸","行銷完全用不到商業和數學","不一定——行銷課多的科系可以，企管／國企打全面商業底也行"],"ans":3},
{"ch":"科系所學","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"科系所學","p":"Part 1","m":"影片一","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>","sub":"到 Notion 看影片一吧"},
{"ch":"科系所學","m":"RAP 反思法","type":"frame","kicker":"停下來，帶你反思一次","art":"reflect","title":"用 <span class=\"hl\">RAP</span> 反思","steps":[{"b":"R","c":"var(--m-blue)","h":"Review｜複習","p":"複習剛剛的課程筆記——今天到底學了哪些內容？"},{"b":"A","c":"var(--m-green)","h":"Ask｜自問","p":"問問自己：這個領域，我喜歡嗎？有沒有讓我想深入的地方？"},{"b":"P","c":"var(--m-yellow)","h":"Present｜表達","p":"把想法講出來、闡述出來——等一下用感受評分表達，並寫進講義。"}],"p":"Part 1"},
{"ch":"科系所學","p":"Part 1","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","p":"Part 2","m":"Part 2：看影片一","type":"part","no":2,"total":3,"chLabel":"科系所學","title":"複習 · 一起看影片一"},
{"ch":"科系所學","p":"Part 2","m":"Before & After 概念","type":"frame","kicker":"先搞懂一個概念","art":"reflect","title":"什麼是 <span class=\"hl\">Before & After</span>","steps":[{"b":"B","c":"var(--m-blue)","h":"Before｜上課前","p":"把你「原本的猜測、認知」先寫下來（就是剛剛三題你的答案）。"},{"b":"A","c":"var(--m-green)","h":"After｜上課後","p":"看完影片、對過答案後，把你「修正、補充的內容」寫下來。"},{"b":"＝","c":"var(--m-yellow)","h":"兩者一對照","p":"你就看得到自己「學到了什麼、想法怎麼變」——這就是最好的學習證據。"}]},
{"ch":"科系所學","p":"Part 2","m":"複習 · 影片一重點","type":"demo","kicker":"複習 · 影片一重點筆記","art":"lightbulb","title":"行銷的<span class=\"hl\">三大力</span>","cards":[{"i":"star","h":"品牌力","p":"STP、行銷 4P、Persona、行銷研究、全球品牌管理"},{"i":"brain","h":"消費者洞察力","p":"購前中後心理、質化量化研究、對價值品質風險的感知"},{"i":"antenna","h":"社群擴散力","p":"病毒／內容行銷、CRM、社群平台實務、廣告公關促銷"}]},
{"ch":"科系所學","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"科系所學","p":"Part 2","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","p":"Part 3","m":"Part 3：自主反思","type":"part","no":3,"total":3,"chLabel":"科系所學","title":"反思 · 自主反思 · RAP + 感受評分"},
{"ch":"科系所學","p":"Part 3","m":"感受 · 需要的能力","type":"score","kicker":"感受評分 · 1／3","art":"star","q":"對於行銷要培養的能力，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">品牌力、消費者洞察力、社群擴散力</span>"},
{"ch":"科系所學","p":"Part 3","m":"感受 · 課程規劃","type":"score","kicker":"感受評分 · 2／3","art":"path","q":"對於行銷大學課程規劃，你<span class=\"hl\">想學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">打好商業基礎 → 行銷原理 → 行銷研究 → 實戰整合</span>"},
{"ch":"科系所學","p":"Part 3","m":"感受 · 課外活動","type":"score","kicker":"感受評分 · 3／3","art":"rise","q":"行銷領域的課外活動，你<span class=\"hl\">想參加</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">社團提案、比賽經驗、實習體驗</span>"},
{"ch":"科系所學","p":"Part 3","m":"發現反思 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 After<br>（自主反思）"},
{"ch":"科系所學","p":"Part 3","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"科系所學","p":"Part 3","m":"SMART 撰寫法","type":"frame","kicker":"學習歷程怎麼寫","art":"notion","title":"用 <span class=\"hl\">SMART</span> 五步，不卡關","steps":[{"b":"S","c":"var(--m-blue)","h":"Summarize｜摘要","p":"這份檔案想呈現的重點，先寫在最前面。"},{"b":"M","c":"var(--m-green)","h":"Mention｜說明","p":"說明你參加的動機，以及這個課程／活動在做什麼。"},{"b":"A","c":"var(--m-yellow)","h":"Action｜行動","p":"記錄你做了哪些具體的事、採取了哪些行動。"},{"b":"R","c":"var(--m-red)","h":"Review｜反思","p":"反思喜不喜歡、原因，以及接下來想做什麼。"},{"b":"T","c":"var(--m-blue)","h":"Template｜模板","p":"選一個模板輸出——Canva、Notion 都可以。"}]},
{"ch":"科系所學","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"科系所學","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"科系所學","p":"Part 3","m":"分享一個最有感的內容","type":"cover","art":"reflect","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得最有感的內容"},
{"ch":"科系所學","p":"Part 3","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"休息","m":"中場休息 · 計時器＋音樂","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"休息","m":"聊天室分享","type":"cover","art":"hand","timer":180,"title":"請同學在<span class=\"hl\">聊天室</span>分享","sub":"趁這幾分鐘，把你現在的想法、心得，或任何問題打在聊天室裡分享給大家！"},
{"ch":"未來發展","p":"Part 1","m":"Part 1：互動提問 → Before","type":"part","no":1,"total":3,"chLabel":"未來發展","title":"前導 · 互動提問 → 寫 Before"},
{"ch":"未來發展","p":"Part 1","m":"測驗 · 品牌定位","type":"quiz","noans":true,"kicker":"未來發展 · 第 1 題","art":"star","q":"一個新產品要上市，行銷最先要想清楚的通常是？","opts":["要賣給誰、他為什麼會買（品牌定位）","先把廣告拍得越貴越好","先決定產品要賣多少錢","先想好包裝要什麼顏色"],"ans":0},
{"ch":"未來發展","p":"Part 1","m":"測驗 · 甲方乙方","type":"quiz","noans":true,"kicker":"未來發展 · 第 2 題","art":"gear","q":"行銷工作分「甲方」和「乙方」，哪個配對是對的？","opts":["甲方＝工讀生；乙方＝正職","甲方＝品牌自己的行銷團隊；乙方＝幫品牌做事的代理商","甲方和乙方其實是同一種工作","甲方只能做設計，乙方只能跑業務"],"ans":1},
{"ch":"未來發展","p":"Part 1","m":"測驗 · 品牌思維","type":"quiz","noans":true,"kicker":"未來發展 · 第 3 題","art":"brain","q":"影片建議，想做行銷平常可以怎麼練功？","opts":["每天背 100 句廣告詞","完全不用理會自己的缺點","把自己當品牌經營：怎麼定位自己、放大優勢、改善弱點","長得好看最重要"],"ans":2},
{"ch":"未來發展","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"未來發展","p":"Part 1","m":"影片一 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>＋寫 After","sub":"先看第一支影片，再到 Notion 補上你的 After"},
{"ch":"未來發展","p":"Part 2","m":"Part 2：影片一 → 複習 → After","type":"part","no":2,"total":3,"chLabel":"未來發展","title":"複習 · 看影片一 → 複習 → 寫 After"},
{"ch":"未來發展","p":"Part 2","m":"複習 · 影片一重點","type":"demo","kicker":"複習 · 影片一重點筆記","art":"rise","four":true,"title":"行銷的<span class=\"hl\">實戰四步</span>","cards":[{"i":"star","h":"品牌定位","p":"賣給誰、為什麼買；消費者分群、聚焦客群"},{"i":"path","h":"長期策略","p":"三年藍圖、SMART 目標、產品路線圖"},{"i":"gear","h":"部門合作","p":"後勤／財務／業務一起把產品做出來、賣出去"},{"i":"rocket","h":"上市計畫","p":"整合行銷、通路佈局、上市後追蹤"}]},
{"ch":"未來發展","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"未來發展","p":"Part 2","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"未來發展","p":"Part 3","m":"Part 3：複合學習（影片二＋截圖＋筆記＋After）","type":"part","no":3,"total":3,"chLabel":"未來發展","title":"反思 · 複合學習：影片二 → 截圖 → 筆記 → After"},
{"ch":"未來發展","p":"Part 3","m":"感受 · 工作流程","type":"score","kicker":"感受評分 · 1／3","art":"gear","q":"對於行銷的工作流程，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">品牌定位 → 長期策略 → 部門合作 → 上市計畫</span>"},
{"ch":"未來發展","p":"Part 3","m":"感受 · 畢業職缺","type":"score","kicker":"感受評分 · 2／3","art":"rise","q":"對於行銷相關的畢業職缺，你的<span class=\"hl\">期待</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">甲方：專員／經理／總監　乙方：廣告／媒體代理商</span>"},
{"ch":"未來發展","p":"Part 3","m":"感受 · 需要能力","type":"score","kicker":"感受評分 · 3／3","art":"brain","q":"對於行銷需要的能力，你<span class=\"hl\">想培養</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">品牌思維：把自己當品牌　隱惡揚善：放大優勢、改善弱點</span>"},
{"ch":"未來發展","p":"Part 3","m":"寫 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 After<br>（自主反思）"},
{"ch":"未來發展","p":"Part 3","m":"Action 行動","type":"frame","kicker":"寫 Action · 三個要訣","art":"hand","title":"<b style=\"color:var(--lemon)\">A</b>　Action 行動","steps":[{"b":"1","c":"var(--m-yellow)","h":"先列有感重點","p":"把「未來發展」這段你有感覺的重點先列出來。"},{"b":"2","c":"var(--m-green)","h":"加上延伸說明","p":"每個列點後面補一句說明，讓內容更完整。"},{"b":"3","c":"var(--m-blue)","h":"用 AI 潤飾","p":"整段丟給 ChatGPT 或 Claude 幫你潤飾。"}],"redbox":"了解了行銷「甲方 vs 乙方」的差別，也認識品牌定位與上市流程；對「把自己當品牌經營、放大優勢」這個觀念最有共鳴。","note":"寫不出來就回頭看 Before & After，把你發現的差異寫下來。"},
{"ch":"未來發展","p":"Part 3","m":"Review 反思","type":"frame","kicker":"最後，寫 Review","art":"reflect","title":"<b style=\"color:var(--lemon)\">R</b>　Review 反思","steps":[{"b":"1","c":"var(--m-red)","h":"這些未來，我嚮往嗎？","p":"哪條路讓我心動？為什麼？"},{"b":"2","c":"var(--m-yellow)","h":"我和它合得來嗎？","p":"這種工作型態、需要的能力，符合我的樣子嗎？"},{"b":"3","c":"var(--m-green)","h":"我的下一步","p":"想更靠近的話，接下來可以先做什麼？"}],"redbox":"請幫我把下面這段學習反思潤飾得更通順、有條理，並保留我的原意：〔貼上你的反思〕","note":"已經寫好的同學，可以用這個 Prompt 到 ChatGPT 優化學習歷程。"},
{"ch":"未來發展","m":"競賽 · Kahoot","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"吃飯前，先來一場 PK！打開 Kahoot、輸入 PIN，看看你記住多少、答對多少～","p":"Part 3"},
{"ch":"收尾","m":"午餐前 · 問學長姐 Slido","type":"frame","kicker":"吃飯前，先問問學長姐","art":"question","title":"到 <span class=\"hl\">Slido</span>，用 USB 三個方向問","steps":[{"b":"U","c":"var(--m-blue)","h":"Usually｜平常","p":"學長姐平常都在忙什麼？課堂、社團、實習的日常長什麼樣？"},{"b":"S","c":"var(--m-green)","h":"Situation｜實況","p":"這個領域真實的狀況——和老師怎麼互動、實際在做什麼專案？"},{"b":"B","c":"var(--m-yellow)","h":"Be Back｜重來","p":"如果回到高中，會給當時的自己、或給我們什麼建議？"}],"note":"其他想問的也都可以——直接把問題打在 Slido 上！（此處可放 Slido 畫面）"},
{"ch":"收尾","m":"午餐 · 1:30 回來","type":"cover","art":"lunch","title":"午餐時間到！","sub":"記得先去吃飯、補充能量～ 下午 <span class=\"hl\">1:30 準時回來</span>！"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"科系所學","title":"前導"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 1","m":"測驗 · 三大能力","type":"quiz","noans":true,"kicker":"科系所學 · 第 1 題","art":"pulse","q":"牙醫系的核心「三大能力」是什麼？","opts":["美術繪畫、雕刻捏塑、審美天分","做業務銷售、跑客戶關係、簽約談判","反應要快、記憶力要好、天生手巧","外傷急診疼痛控制、組織修復功能重建、治療規劃與病患溝通"],"ans":3},
{"ch":"科系所學","camp":"牙醫營","p":"Part 1","m":"測驗 · 必修課程","type":"quiz","noans":true,"kicker":"科系所學 · 第 2 題","art":"path","q":"牙醫系有哪些必修課程？","opts":["純靠自學，學校不排課","人體解剖學、口腔組織學、牙髓病學（根管治療）、口腔外科學","只上美容美學課程，不碰醫學基礎","畢業前完全不用值班或實習"],"ans":1},
{"ch":"科系所學","camp":"牙醫營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 1","m":"影片一","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>","sub":"到 Notion 看影片一吧"},
{"ch":"科系所學","camp":"牙醫營","m":"RAP 反思法","type":"frame","kicker":"停下來，帶你反思一次","art":"reflect","title":"用 <span class=\"hl\">RAP</span> 反思","steps":[{"b":"R","c":"var(--m-blue)","h":"Review｜複習","p":"複習剛剛的課程筆記——今天到底學了哪些內容？"},{"b":"A","c":"var(--m-green)","h":"Ask｜自問","p":"問問自己：這個領域，我喜歡嗎？有沒有讓我想深入的地方？"},{"b":"P","c":"var(--m-yellow)","h":"Present｜表達","p":"把想法講出來、闡述出來——等一下用感受評分表達，並寫進講義。"}],"p":"Part 1"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 1","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"科系所學","title":"複習"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 2","m":"複習一下 · 科系掃盲","type":"frame","kicker":"複習一下 · 科系掃盲","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"科系盲點","p":"「手作能力不好或沒美術天分是否不適合牙醫系？」其實大多數是進大學後才開始訓練，天分不是決定關鍵要素。"},{"b":"2","c":"var(--m-green)","h":"培養能力","p":"溝通力：與病人建立信任關係／專注力：長時間治療與精細操作需要高度集中／自學力：醫療知識持續進化，需主動吸收更新。"},{"b":"3","c":"var(--m-yellow)","h":"先修資源","p":"建議觀察 YouTube 創作者「面白牙醫-黃偉家」的影片，了解實務與生活情境。"}]},
{"ch":"科系所學","camp":"牙醫營","p":"Part 2","m":"想想看 · 想先培養的能力","type":"quiz","noans":true,"kicker":"想想看 · 六年課程規劃","art":"path","q":"如果從大一讀到大六，你覺得自己最想先培養哪個能力？","opts":["溝通力——想先學會怎麼跟病人建立信任","專注力——想先練習長時間精細操作的耐心","自學力——想先培養持續吸收新知識的習慣","都還沒想清楚，想先多方嘗試看看"]},
{"ch":"科系所學","camp":"牙醫營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 2","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"科系所學","title":"反思"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"感受 · 需要的能力","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於需要培養的能力，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">外傷急診疼痛控制、組織修復功能重建、治療規劃病患溝通</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"感受 · 課程規劃","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於牙醫系的課程，你<span class=\"hl\">想學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">口腔外科學、牙科麻醉疼痛控制、牙科藥理學／牙體復形學、牙髓病學、口腔胚胎學‧組織學／口腔放射學＋臨床診斷學</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"感受 · 六年規劃","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"牙醫系大學六年規劃，你<span class=\"hl\">期待</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">大一／二：打好醫學基礎、了解口腔專業知識｜大三／四：掌握臨床基本、深入專科臨床實務｜大五／六：實習臨床、加強技能、國考準備</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"發現反思 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 After<br>（自主反思）"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"科系所學","camp":"牙醫營","m":"SMART 撰寫法","type":"frame","kicker":"學習歷程怎麼寫","art":"notion","title":"用 <span class=\"hl\">SMART</span> 五步，不卡關","steps":[{"b":"S","c":"var(--m-blue)","h":"Summarize｜摘要","p":"這份檔案想呈現的重點，先寫在最前面。"},{"b":"M","c":"var(--m-green)","h":"Mention｜說明","p":"說明你參加的動機，以及這個課程／活動在做什麼。"},{"b":"A","c":"var(--m-yellow)","h":"Action｜行動","p":"記錄你做了哪些具體的事、採取了哪些行動。"},{"b":"R","c":"var(--m-red)","h":"Review｜反思","p":"反思喜不喜歡、原因，以及接下來想做什麼。"},{"b":"T","c":"var(--m-blue)","h":"Template｜模板","p":"選一個模板輸出——Canva、Notion 都可以。"}],"p":"Part 3"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"分享一個最有感的內容","type":"cover","art":"reflect","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得最有感的內容"},
{"ch":"科系所學","camp":"牙醫營","p":"Part 3","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"未來發展","title":"前導"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 1","m":"測驗 · 職涯路徑","type":"quiz","noans":true,"kicker":"未來發展 · 第 1 題","art":"rise","q":"牙醫系的職涯路徑，長怎樣？","opts":["畢業後馬上能自己開業當院長","只能受僱於醫院，沒有機會自己開業","從實習／PGY訓練起步，累積臨床經驗後走向診所執業或專科發展，資深後可成為診所負責人或專科自營醫師","考到執照後薪水職位就定型不會再變"],"ans":2},
{"ch":"未來發展","camp":"牙醫營","p":"Part 1","m":"測驗 · 重要特質","type":"quiz","noans":true,"kicker":"未來發展 · 第 2 題","art":"reflect","q":"成為牙醫師最重要的特質是？","opts":["同理心——理解病患的害怕與需求，建立信任感並持續關注","只要技術好，不需要在乎病患感受","口才好、很會推銷療程最重要","只要考試成績好，其他能力都不重要"],"ans":0},
{"ch":"未來發展","camp":"牙醫營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 1","m":"影片一 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>＋寫 After","sub":"先看第一支影片，再到 Notion 補上你的 After"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"未來發展","title":"複習"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 2","m":"複習一下","type":"frame","kicker":"複習一下 · 牙醫專科、職涯與趨勢","art":"reflect","title":"複習一下","steps":[{"b":"牙醫專科","c":"var(--m-blue)","h":"四大特質分類","p":"邏輯精準：牙髓病科、牙體復形科、口腔顎面外科／規劃理性：口腔病理科、牙周病科／陪伴溝通：兒童牙科、家庭牙科／審美設計：齒顎矯正科、贗復補綴科"},{"b":"診所職涯","c":"var(--m-green)","h":"三階段成長路徑","p":"學生／實習 → 一般診所牙醫師（月薪 8～18萬）→ 診所負責人／院長（月薪 20萬～百萬）"},{"b":"專科職涯","c":"var(--m-yellow)","h":"四階段成長路徑","p":"PGY 訓練 → 住院主治醫師 → 專科牙醫師（院所／自營）→ 學術／教學研發牙醫師"},{"b":"目前趨勢","c":"var(--m-red)","h":"產業正在往哪走","p":"數位科技進步、美觀與個人化治療、病患體驗與溝通升級"}]},
{"ch":"未來發展","camp":"牙醫營","p":"Part 2","m":"想想看 · 最想優先培養的特質","type":"quiz","noans":true,"kicker":"想想看 · 同理心與自我提問","art":"question","q":"你覺得，成為牙醫師最需要優先培養的特質是？","opts":["同理心——理解並陪伴病患的感受","喜歡與人互動——享受和病患建立關係","職人精神——追求技術與細節的完美","商業經營意識——兼顧診所營運與專業"]},
{"ch":"未來發展","camp":"牙醫營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 2","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"未來發展","title":"反思"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 3","m":"感受 · 專科類別","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於牙醫專科類別，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">邏輯精準：牙髓病、牙體復形、口腔顎面｜規劃理性：口腔病理、牙周病｜陪伴溝通：兒童牙科、家庭牙科｜審美設計：齒顎矯正、贗復補綴</span>"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 3","m":"感受 · 職涯路徑","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於牙醫系的職涯路徑，你<span class=\"hl\">期待</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">診所：學生實習 → 一般診所 → 診所負責人｜專科：醫師訓練 → 主治 → 專科 → 學術</span>"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 3","m":"感受 · 牙醫師特質","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於牙醫師特質，你<span class=\"hl\">想培養</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">同理心很重要｜每位牙醫師都曾是病患｜用病患視角設計角色</span>"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 3","m":"寫 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 After<br>（自主反思）"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"未來發展","camp":"牙醫營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"未來發展","m":"競賽 · Kahoot","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"吃飯前，先來一場 PK！打開 Kahoot、輸入 PIN，看看你記住多少、答對多少～","p":"Part 3","camp":"牙醫營"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"寫 Slido","type":"cover","art":"question","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">Slido</span>","sub":"把你的想法或問題打在 Slido 上，我們稍後一起看！"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":2,"chLabel":"實際操作","title":"前導"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"測驗 · 命名系統","type":"quiz","noans":true,"kicker":"實際操作 · 第 1 題","art":"pulse","q":"牙醫溝通牙齒位置時，最常使用哪個命名系統？","opts":["直接用中文講「左上第二顆」就夠清楚","每間診所自己發明一套編號","牙齒外觀就能溝通，不必命名","FDI system——台灣主要使用，恆牙以1～4象限、每象限1～8編號"],"ans":3},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"測驗 · 口腔構造","type":"quiz","noans":true,"kicker":"實際操作 · 第 2 題","art":"path","q":"牙齒的基本構造，由外到內依序是？","opts":["牙齒每層材質一樣硬，沒有分層","琺瑯質（最硬、保護層）→ 牙本質（傳導冷熱）→ 牙髓腔（有神經血管，蛀牙侵入會劇痛）","神經包在牙齒最外層，最先感覺到痛","只有琺瑯質，沒有牙本質或牙髓腔"],"ans":1},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"互動：實際操作最有感的地方","type":"cover","art":"question","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得實際操作最有感的地方"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 1","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":2,"chLabel":"實際操作","title":"複習"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 2","m":"複習一下 · 科系掃盲","type":"frame","kicker":"複習一下 · 科系掃盲","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"科系盲點","p":"「手作能力不好或沒美術天分是否不適合牙醫系？」其實大多數是進大學後才開始訓練，天分不是決定關鍵要素。"},{"b":"2","c":"var(--m-green)","h":"培養能力","p":"溝通力：與病人建立信任關係／專注力：長時間治療與精細操作需要高度集中／自學力：醫療知識持續進化，需主動吸收更新。"},{"b":"3","c":"var(--m-yellow)","h":"先修資源","p":"建議觀察 YouTube 創作者「面白牙醫-黃偉家」的影片，了解實務與生活情境。"}]},
{"ch":"實際操作","camp":"牙醫營","p":"Part 2","m":"想想看 · 最想加強的能力","type":"quiz","noans":true,"kicker":"想想看 · 六年課程規劃","art":"path","q":"回顧六年的訓練歷程，你覺得自己現在最想加強的是？","opts":["專注力——想先練習長時間精細操作的耐心","自學力——想先培養持續吸收新知識的習慣","溝通力——想先學會怎麼跟病人建立信任","還在摸索，想先多方嘗試看看"]},
{"ch":"實際操作","camp":"牙醫營","p":"Part 2","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 2","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"實際操作","title":"引導"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"牙醫系引導 3","type":"cover","art":"compass","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"牙醫系<span class=\"hl\">引導 3</span>","sub":"跟著引導活動，繼續深入體驗這個科系"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"感受 · 牙齒構造","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"在了解牙齒的構造，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">牙冠、琺瑯質、牙本質｜牙周組織、牙髓腔、牙根與根管｜牙齒方位、FDI 編號</span>"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"感受 · 實作描繪","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"在實作描繪的過程，你對牙齒<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">實作一：門牙｜實作二：上、下顎大臼齒</span>"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"感受 · 各構造與功能","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"了解牙齒各構造與功能，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">牙齒：門牙、犬齒、小臼齒、大臼齒、乳牙｜介紹：功能、構造、特徵</span>"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"Action + Review","type":"cover","art":"hand","shotPlaceholder":true,"timer":900,"title":"Action ＋ <span class=\"hl\">Review</span>"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 3","m":"Kahoot：實際操作","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"打開 Kahoot、輸入 PIN，看看實際操作這段你記住多少、答對多少～"},
{"ch":"實際操作","camp":"牙醫營","p":"Part 2","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"休息","camp":"牙醫營","m":"中場休息 · 計時器＋音樂","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"休息","camp":"牙醫營","m":"聊天室分享","type":"cover","art":"hand","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"趁這幾分鐘，把你現在的想法、心得，或任何問題打在聊天室裡分享給大家！"},
{"ch":"收尾","camp":"牙醫營","m":"午餐後，問學長姐 Slido","type":"frame","kicker":"吃飯後，問問學長姐","art":"question","title":"到 <span class=\"hl\">Slido</span>，用 USB 三個方向問","steps":[{"b":"U","c":"var(--m-blue)","h":"Usually｜平常","p":"學長姐平常都在忙什麼？課堂、實習、值班的日常長什麼樣？"},{"b":"S","c":"var(--m-green)","h":"Situation｜實況","p":"這個領域真實的狀況——課業、實作訓練、實際在做什麼？"},{"b":"B","c":"var(--m-yellow)","h":"Be Back｜重來","p":"如果回到高中，會給當時的自己、或給我們什麼建議？"}],"note":"其他想問的也都可以——直接把問題打在 Slido 上！（此處可放 Slido 畫面）"},
{"ch":"收尾","camp":"牙醫營","m":"午餐吃什麼？","type":"cover","art":"lunch","timer":30,"title":"午餐吃什麼？","sub":"趁午休前，先在聊天室或 Slido 上分享一下你今天想吃什麼、或推薦附近好吃的店家吧！"},
{"ch":"收尾","camp":"牙醫營","m":"午餐 · 1:30 回來","type":"cover","art":"lunch","music":true,"title":"午餐時間到！","sub":"記得先去吃飯、補充能量～ 下午 <span class=\"hl\">1:30 準時回來</span>！"},
{"ch":"科系所學","camp":"材料營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"科系所學","title":"前導"},
{"ch":"科系所學","camp":"材料營","p":"Part 1","m":"測驗 · 核心能力","type":"quiz","noans":true,"kicker":"科系所學 · 第 1 題","art":"pulse","q":"材料系的核心能力有哪些？","opts":["美術設計、色彩搭配、模型雕塑","財務規劃、行銷企劃、業務銷售","材料結構分析、性質與可靠性評估、製程優化改良","只要背公式、記憶力好就能學好"],"ans":2},
{"ch":"科系所學","camp":"材料營","p":"Part 1","m":"測驗 · 必修課程","type":"quiz","noans":true,"kicker":"科系所學 · 第 2 題","art":"path","q":"材料系有哪些必修課程？","opts":["會計學、行銷管理、財務報表分析","純美學設計課程，不碰數理基礎","不用做實驗，全部用背的就好","材料科學與工程導論、材料熱力學、物理冶金、材料實驗"],"ans":3},
{"ch":"科系所學","camp":"材料營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 1","m":"影片一","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>","sub":"到 Notion 看影片一吧"},
{"ch":"科系所學","camp":"材料營","m":"RAP 反思法","type":"frame","kicker":"停下來，帶你反思一次","art":"reflect","title":"用 <span class=\"hl\">RAP</span> 反思","steps":[{"b":"R","c":"var(--m-blue)","h":"Review｜複習","p":"複習剛剛的課程筆記——今天到底學了哪些內容？"},{"b":"A","c":"var(--m-green)","h":"Ask｜自問","p":"問問自己：這個領域，我喜歡嗎？有沒有讓我想深入的地方？"},{"b":"P","c":"var(--m-yellow)","h":"Present｜表達","p":"把想法講出來、闡述出來——等一下用感受評分表達，並寫進講義。"}],"p":"Part 1"},
{"ch":"科系所學","camp":"材料營","p":"Part 1","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"科系所學","title":"複習"},
{"ch":"科系所學","camp":"材料營","p":"Part 2","m":"複習一下 · 材料系三大能力","type":"frame","kicker":"複習一下 · 材料結構分析、可靠性評估、製程優化","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"材料結構分析","p":"用電子顯微鏡（如 TEM）觀察原子排列是否整齊、有無缺陷——缺陷有時反而能強化材料（如提升導電性）。例如晶片裡上億個電晶體，就是靠結構分析確認製程沒問題（比對 FinFET 不同寬度的電晶體結構）。"},{"b":"2","c":"var(--m-green)","h":"性質與可靠性評估","p":"測試材料在高溫、受力、化學反應等情境下會不會變形、老化或失效，確保產品能長時間穩定運作。半導體晶片材料只要稍有變形，就可能導致晶片出錯。"},{"b":"3","c":"var(--m-yellow)","h":"製程優化改良","p":"調整溫度、時間、壓力等製程參數，提高品質與良率、降低成本。材料選對、製法調整好，就能做出導電佳、不易過熱的晶片，例如調整金屬導線厚度（Cu、Mo、Ru）來控制導電性。"}]},
{"ch":"科系所學","camp":"材料營","p":"Part 2","m":"想想看 · 最期待的學習階段","type":"quiz","noans":true,"kicker":"想想看 · 四年學習地圖","art":"path","q":"材料系四年的學習歷程，你最期待哪個階段？","opts":["大一：打材料與數理基礎（材料導論、普通化學、微積分）","大二：理論建構＋基礎操作能力（材料熱力學、晶體結構、材料實驗）","大三：專題研究、深入理論與實務（機械性質、擴散與相變化）","大四：進入固態物理、金屬、高分子等進階應用領域"]},
{"ch":"科系所學","camp":"材料營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"科系所學","camp":"材料營","p":"Part 2","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"科系所學","title":"反思"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"感受 · 培養的能力","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於材料系培養的能力，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">材料結構分析：看原子如何排列｜性質與穩定判斷：選正確材料，不變形不壞掉｜製程優化改良：改流程控溫度，東西更好更省</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"感受 · 相關課程","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對材料系的相關課程，你<span class=\"hl\">想學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">材料科學與工程導論、材料熱力學｜物理冶金、晶體結構與繞射導論、材料實驗</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"感受 · 四年規劃","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"材料系大學四年規劃，你<span class=\"hl\">期待</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">大一：基礎材料與數理知識｜大二：材料理論實驗操作｜大三：材料結構應用分析｜大四：整合知識實作創新</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"發現反思 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 After<br>（自主反思）"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"科系所學","camp":"材料營","m":"SMART 撰寫法","type":"frame","kicker":"學習歷程怎麼寫","art":"notion","title":"用 <span class=\"hl\">SMART</span> 五步，不卡關","steps":[{"b":"S","c":"var(--m-blue)","h":"Summarize｜摘要","p":"這份檔案想呈現的重點，先寫在最前面。"},{"b":"M","c":"var(--m-green)","h":"Mention｜說明","p":"說明你參加的動機，以及這個課程／活動在做什麼。"},{"b":"A","c":"var(--m-yellow)","h":"Action｜行動","p":"記錄你做了哪些具體的事、採取了哪些行動。"},{"b":"R","c":"var(--m-red)","h":"Review｜反思","p":"反思喜不喜歡、原因，以及接下來想做什麼。"},{"b":"T","c":"var(--m-blue)","h":"Template｜模板","p":"選一個模板輸出——Canva、Notion 都可以。"}],"p":"Part 3"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"分享一個最有感的內容","type":"cover","art":"reflect","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得最有感的內容"},
{"ch":"科系所學","camp":"材料營","p":"Part 3","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"未來發展","camp":"材料營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"未來發展","title":"前導"},
{"ch":"未來發展","camp":"材料營","p":"Part 1","m":"測驗 · 畢業職缺","type":"quiz","noans":true,"kicker":"未來發展 · 第 1 題","art":"rise","q":"材料系畢業後，有哪些職缺？你比較嚮往哪一種？","opts":["研究開發工程師（R&D）——做材料實驗、儀器分析、開發新材料","製程整合／製程工程師——優化生產流程、解決現場技術問題","學術界、研究機構——做研究、發表論文、指導學生","還沒想清楚，想多方嘗試看看"]},
{"ch":"未來發展","camp":"材料營","p":"Part 1","m":"測驗 · 相關公司","type":"quiz","noans":true,"kicker":"未來發展 · 第 2 題","art":"reflect","q":"材料系畢業後，可以去哪些公司？你比較想進哪一種？","opts":["半導體公司——如台積電、聯電，做晶片相關製造","化工材料公司——如信越化學、默克，提供先進製程化學品","設備商——如 ASML、應用材料，做微影／蝕刻／鍍膜設備","能源生醫公司——如寧德時代、晶鑽生醫，做電池或生醫材料"]},
{"ch":"未來發展","camp":"材料營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"未來發展","camp":"材料營","p":"Part 1","m":"影片一 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>＋寫 After","sub":"先看第一支影片，再到 Notion 補上你的 After"},
{"ch":"未來發展","camp":"材料營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"未來發展","title":"複習"},
{"ch":"未來發展","camp":"材料營","p":"Part 2","m":"複習一下 · 三種職涯選擇","type":"frame","kicker":"複習一下 · R&D、製程工程師、學術研究","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"研究開發工程師（R&D）","p":"工作內容：材料實驗操作、儀器分析（XRD、SEM、TEM）、數據分析、新材料開發、技術文件與專利整合。所需能力：材料科學知識、儀器操作技能、研發與創新思維。"},{"b":"2","c":"var(--m-green)","h":"製程整合、製程工程師","p":"工作內容：材料實驗操作、儀器分析、生產流程優化、解決製造現場問題、調整製程參數提升良率。所需能力：熟悉半導體製程、邏輯分析力、跨部門溝通、快速反應能力。"},{"b":"3","c":"var(--m-yellow)","h":"學術界、研究機構","p":"工作內容：儀器實驗與教學、發表學術論文、執行研究計畫並指導學生、與研究團隊合作推進科研任務。所需能力：儀器操作與教學、論文寫作（含英文）、學生指導與團隊合作。"}]},
{"ch":"未來發展","camp":"材料營","p":"Part 2","m":"想想看 · 想了解的公司與趨勢","type":"quiz","noans":true,"kicker":"想想看 · 半導體、材料設備、能源生醫、未來趨勢","art":"question","q":"材料相關的公司與趨勢，你比較好奇哪一塊？","opts":["半導體公司——如台積電、聯電，做晶片製造與代工","材料與設備供應商——如信越化學、ASML，提供先進製程化學品與設備","能源生醫公司——如寧德時代、晶鑽生醫，做電池或生醫材料","未來趨勢——EUV 光阻劑、綠能材料、生醫感測器等新興領域"]},
{"ch":"未來發展","camp":"材料營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"未來發展","camp":"材料營","p":"Part 2","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"未來發展","camp":"材料營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"未來發展","title":"反思"},
{"ch":"未來發展","camp":"材料營","p":"Part 3","m":"感受 · 材料系職缺","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於材料系的職缺，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">研究開發工程師（R&D）｜製程整合、製程工程師｜學術界、研究機構</span>"},
{"ch":"未來發展","camp":"材料營","p":"Part 3","m":"感受 · 常見公司","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於材料系常見公司，你的<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">半導體：台積電、聯電、Intel｜化工材料：信越化學工業、默克集團、勝高｜設備商：ASML、科林研發、應用材料｜能源生醫：寧德時代、晶鑽生醫、長聖國際</span>"},
{"ch":"未來發展","camp":"材料營","p":"Part 3","m":"感受 · 未來產業趨勢","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於未來產業趨勢，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">半導體材料、綠能／碳中和、生醫／醫療材料</span>"},
{"ch":"未來發展","camp":"材料營","p":"Part 3","m":"寫 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 After<br>（自主反思）"},
{"ch":"未來發展","camp":"材料營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"未來發展","camp":"材料營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"未來發展","m":"競賽 · Kahoot","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"吃飯前，先來一場 PK！打開 Kahoot、輸入 PIN，看看你記住多少、答對多少～","p":"Part 3","camp":"材料營"},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"寫 Slido","type":"cover","art":"question","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">Slido</span>","sub":"把你的想法或問題打在 Slido 上，我們稍後一起看！"},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":2,"chLabel":"實際操作","title":"前導"},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"測驗 · 能帶是什麼","type":"quiz","noans":true,"kicker":"實際操作 · 第 1 題","art":"pulse","q":"能帶是什麼？如果用「電子住在樓層」來比喻，你覺得哪一種最好理解？","opts":["導體——樓層相連，電子可以自由移動（傳導帶與價帶重疊）","絕緣體——樓層距離太遠，電子幾乎跳不上去（能隙很大）","半導體——特定條件下可以跳到更高樓層（能隙適中）","還是有點抽象，需要多看幾次圖解"]},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"測驗 · 可靠性評估","type":"quiz","noans":true,"kicker":"實際操作 · 第 2 題","art":"path","q":"半導體晶片材料為什麼需要做可靠性評估？","opts":["因為要讓晶片看起來更美觀","為了讓材料賣相更好，方便行銷","只是例行公事，跟晶片品質無關","確認材料在高溫、受力、化學反應等情境下會不會變形、老化或失效，避免產品出錯"],"ans":3},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"互動：實際操作最有感的地方","type":"cover","art":"question","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得實際操作最有感的地方"},
{"ch":"實際操作","camp":"材料營","p":"Part 1","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"實際操作","camp":"材料營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":2,"chLabel":"實際操作","title":"複習"},
{"ch":"實際操作","camp":"材料營","p":"Part 2","m":"複習一下 · 半導體物理入門","type":"frame","kicker":"複習一下 · 原子電子結構、能帶理論、摻雜、PN接面","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"原子與電子的結構","p":"道耳吞提出原子理論，認為原子是不可再分的最小粒子；材料性質要從原子層級看起，了解電子在原子核外不同能階的分布——能階越高離原子核越遠，電子可吸收或釋放能量在能階間移動，能階距離也影響材料的導電性。"},{"b":"2","c":"var(--m-green)","h":"能帶理論","p":"能帶包含「價帶」與「傳導帶」，材料可分為金屬（導體）、半導體、絕緣體。就像電子住在樓層裡：導體樓層相連、電子自由移動；絕緣體樓層太遠、能隙大難以躍遷；半導體能隙適中，特定條件下可以跳上更高樓層導電。"},{"b":"3","c":"var(--m-yellow)","h":"摻雜與半導體","p":"純矽導電性低，加入少量雜質（摻雜）可改變導電性：加硼形成缺少電子的「電洞」，成為 P 型半導體；加磷形成多餘的「自由電子」，成為 N 型半導體。控制摻雜物質種類與濃度，就能調控半導體的導電特性。"},{"b":"4","c":"var(--m-red)","h":"PN 接面與二極體","p":"把 P 型與 N 型半導體接合，形成 PN 接面；電子與電洞在交界處重新分布，建立內建電位（0.3～0.7V）。正向偏壓時導通、反向時不導通，這就是二極體的單向導電特性，可作為開關與整流元件。"}]},
{"ch":"實際操作","camp":"材料營","p":"Part 2","m":"想想看 · 二極體與PN接面","type":"quiz","noans":true,"kicker":"想想看 · 電流方向、手機應用、內建電場、正向偏壓","art":"path","q":"關於二極體與 PN 接面的原理，你最想先搞懂哪一個？","opts":["電流為什麼只能單向流動——反向偏壓會擋住電流","為什麼手機電路離不開二極體——防止電流逆流、保護元件","P 型與 N 型接合為什麼會有內建電場——電子電洞擴散形成耗盡區","正向偏壓時電流為什麼突然變大——載子越過耗盡區重新流動"]},
{"ch":"實際操作","camp":"材料營","p":"Part 2","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"材料營","p":"Part 2","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"實際操作","title":"引導"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"材料系引導 3","type":"cover","art":"compass","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"材料系<span class=\"hl\">引導 3</span>","sub":"跟著引導活動，繼續深入體驗這個科系"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"感受 · PN接面與二極體","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"了解 PN 接面、二極體的過程，<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">P 型與 N 型半導體、電子與電洞擴散｜二極體具有單向導電特性，可作開關與整流</span>"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"感受 · PhET 模擬","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"用 PhET 了解電子流動的過程，<span class=\"hl\">喜歡</span>程度是？"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"感受 · 電洞電子答題","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"在答題了解電洞、電子的過程，<span class=\"hl\">感興趣</span>程度是？"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"Action + Review","type":"cover","art":"hand","shotPlaceholder":true,"timer":900,"title":"Action ＋ <span class=\"hl\">Review</span>"},
{"ch":"實際操作","camp":"材料營","p":"Part 3","m":"Kahoot：實際操作","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"打開 Kahoot、輸入 PIN，看看實際操作這段你記住多少、答對多少～"},
{"ch":"實際操作","camp":"材料營","p":"Part 2","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"休息","camp":"材料營","m":"中場休息 · 計時器＋音樂","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"休息","camp":"材料營","m":"聊天室分享","type":"cover","art":"hand","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"趁這幾分鐘，把你現在的想法、心得，或任何問題打在聊天室裡分享給大家！"},
{"ch":"收尾","camp":"材料營","m":"午餐後，問學長姐 Slido","type":"frame","kicker":"吃飯後，問問學長姐","art":"question","title":"到 <span class=\"hl\">Slido</span>，用 USB 三個方向問","steps":[{"b":"U","c":"var(--m-blue)","h":"Usually｜平常","p":"學長姐平常都在忙什麼？課堂、實習、值班的日常長什麼樣？"},{"b":"S","c":"var(--m-green)","h":"Situation｜實況","p":"這個領域真實的狀況——課業、實作訓練、實際在做什麼？"},{"b":"B","c":"var(--m-yellow)","h":"Be Back｜重來","p":"如果回到高中，會給當時的自己、或給我們什麼建議？"}],"note":"其他想問的也都可以——直接把問題打在 Slido 上！（此處可放 Slido 畫面）"},
{"ch":"收尾","camp":"材料營","m":"午餐吃什麼？","type":"cover","art":"lunch","timer":30,"title":"午餐吃什麼？","sub":"趁午休前，先在聊天室或 Slido 上分享一下你今天想吃什麼、或推薦附近好吃的店家吧！"},
{"ch":"收尾","camp":"材料營","m":"午餐 · 1:30 回來","type":"cover","art":"lunch","music":true,"title":"午餐時間到！","sub":"記得先去吃飯、補充能量～ 下午 <span class=\"hl\">1:30 準時回來</span>！"},
{"ch":"科系所學","camp":"商管營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"科系所學","title":"前導"},
{"ch":"科系所學","camp":"商管營","p":"Part 1","m":"測驗 · 常見課程","type":"quiz","noans":true,"kicker":"科系所學 · 第 1 題","art":"pulse","q":"在商管系，有哪些常見課程？","opts":["經濟學、初級會計、統計學——建立財務與量化分析基礎","企業管理、組織行為學——培養個案分析與人資組織能力","行銷管理、生產與作業管理——學習如何讓產品被市場接受、掌握生產流程","策略管理、財務管理——訓練企業整體策略思考與資金管理能力"]},
{"ch":"科系所學","camp":"商管營","p":"Part 1","m":"測驗 · 所需特質","type":"quiz","noans":true,"kicker":"科系所學 · 第 2 題","art":"path","q":"商管系學生，有哪些所需特質？","opts":["邏輯數理與量化分析能力——面對統計、財務報表、投資評估等數字運算","溝通表達與人際互動能力——個案討論、行銷企劃、跨部門協調不可少","策略思考與整合判斷能力——面對市場趨勢與企業決策，需要宏觀分析","對商業趨勢的好奇心與敏銳度——留意科技、消費者行為與產業變化"]},
{"ch":"科系所學","camp":"商管營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shot":"images/img009.png","timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 1","m":"影片一","type":"cover","art":"film","shot":"images/img010.png","timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>","sub":"到 Notion 看影片一吧"},
{"ch":"科系所學","camp":"商管營","m":"RAP 反思法","type":"frame","kicker":"停下來，帶你反思一次","art":"reflect","title":"用 <span class=\"hl\">RAP</span> 反思","steps":[{"b":"R","c":"var(--m-blue)","h":"Review｜複習","p":"複習剛剛的課程筆記——今天到底學了哪些內容？"},{"b":"A","c":"var(--m-green)","h":"Ask｜自問","p":"問問自己：這個領域，我喜歡嗎？有沒有讓我想深入的地方？"},{"b":"P","c":"var(--m-yellow)","h":"Present｜表達","p":"把想法講出來、闡述出來——等一下用感受評分表達，並寫進講義。"}],"p":"Part 1"},
{"ch":"科系所學","camp":"商管營","p":"Part 1","m":"發現反思 After","type":"cover","art":"notion","shot":"images/img011.png","timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"科系所學","title":"複習"},
{"ch":"科系所學","camp":"商管營","p":"Part 2","m":"複習一下 · 五大核心領域與必修地圖","type":"frame","kicker":"複習一下 · 五系共同課程、產銷人發財、四年必修地圖","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"五系共同課程","p":"台大管院五系（財金、國企、工管、會計、資管）雖各自發展，但大一大二都會接觸共同基礎課程：財金系的經濟學、國企系的初級會計、工管系的微積分、會計系的統計學，打好量化與商業知識的地基。"},{"b":"2","c":"var(--m-green)","h":"產銷人發財｜五大核心領域","p":"以工管系為例，商管科系常見五大領域——產（生產與作業管理：規劃生產流程與數量）、銷（行銷管理：鎖定客群、消費者分析與定價）、人（人力資源管理：薪酬福利與選才）、發（研究發展管理：用定量方法輔助決策）、財（財務管理：計算資金的時間價值，含股票、債券、投資案）。"},{"b":"3","c":"var(--m-yellow)","h":"四年必修地圖","p":"大一：企業管理培養個案分析能力、程式設計打程式基礎；大二：統計學學習資料檢定與可信度、組織行為學認識人資與組織心理；大三：策略管理訓練企業整體與事業單位的策略思考；大四：財務管理深入資金管理、資本預算與投資評估。"}]},
{"ch":"科系所學","camp":"商管營","p":"Part 2","m":"想想看 · 想先深入了解的一塊","type":"quiz","noans":true,"kicker":"想想看 · 模組課程、所需特質、高中準備、學測建議","art":"path","q":"商管系的學習歷程中，你最想先深入了解哪一塊？","opts":["模組課程——行銷、營運數據分析、人資組織管理、科技創新，選一個方向鑽研","所需特質——分析能力、團隊合作、樂於探索、自我管理，看看自己合不合適","高中就能做的準備——參加營隊、搜尋資料、日常思考商業現象背後原理","給學測生的建議——認真讀書、瞭解科系、熟悉自己的經歷、準備面試問題"]},
{"ch":"科系所學","camp":"商管營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img012.png","timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"科系所學","camp":"商管營","p":"Part 2","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img013.png","timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"科系所學","title":"反思"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"感受 · 學習內容","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於商管系的學習內容，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">產：評估產品數量，達到最大利潤｜銷：設定受眾與售價，推廣產品｜人：管理薪資福利，招募適才｜發：研發產品，融入科技趨勢｜財：優化報表，管理稅務問題</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"感受 · 大學課程","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於商管系大學課程，你<span class=\"hl\">想學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">行銷管理、營運與商業數據分析｜人力資源與組織管理、科技與創新管理</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"感受 · 商管系特質","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於商管系特質，你<span class=\"hl\">期待具備</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">分析能力、團隊合作、樂於探索、自我管理</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"發現反思 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img014.png","timer":180,"title":"發現反思 After<br>（自主反思）"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"科系所學","camp":"商管營","m":"SMART 撰寫法","type":"frame","kicker":"學習歷程怎麼寫","art":"notion","title":"用 <span class=\"hl\">SMART</span> 五步，不卡關","steps":[{"b":"S","c":"var(--m-blue)","h":"Summarize｜摘要","p":"這份檔案想呈現的重點，先寫在最前面。"},{"b":"M","c":"var(--m-green)","h":"Mention｜說明","p":"說明你參加的動機，以及這個課程／活動在做什麼。"},{"b":"A","c":"var(--m-yellow)","h":"Action｜行動","p":"記錄你做了哪些具體的事、採取了哪些行動。"},{"b":"R","c":"var(--m-red)","h":"Review｜反思","p":"反思喜不喜歡、原因，以及接下來想做什麼。"},{"b":"T","c":"var(--m-blue)","h":"Template｜模板","p":"選一個模板輸出——Canva、Notion 都可以。"}],"p":"Part 3"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img015.png","timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"shot":"images/img015.png","timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"分享一個最有感的內容","type":"cover","art":"reflect","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得最有感的內容"},
{"ch":"科系所學","camp":"商管營","p":"Part 3","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"未來發展","camp":"商管營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"未來發展","title":"前導"},
{"ch":"未來發展","camp":"商管營","p":"Part 1","m":"測驗 · 畢業職缺","type":"quiz","noans":true,"kicker":"未來發展 · 第 1 題","art":"rise","q":"商管系的職涯走向，長怎樣？","opts":["金融——多由行銷、管理入行後再轉職，例如業務執行（奧美廣告）","管理——多數人都以管理職為目標，例如專案管理師（酷寶資訊）","行銷——品牌與數位行銷，例如 P&G 寶僑","先多方嘗試——透過多份實習累積履歷，就業幾年後再讀 MBA 轉換跑道"]},
{"ch":"未來發展","camp":"商管營","p":"Part 1","m":"測驗 · 相關公司","type":"quiz","noans":true,"kicker":"未來發展 · 第 2 題","art":"reflect","q":"創投＆管顧，這兩個職位在做什麼？","opts":["創投——在初級市場尋找投資標的，面談新創創辦人並協助企業成長","管顧——像企業的醫生，提供市場策略與管理建議，快速解決客戶問題","兩者的共同點——都需要對產業趨勢有敏銳觀察力，並能承受高壓工作環境","兩者適合的性格——創投適合善於社交、持續追蹤趨勢的人；管顧適合喜歡快速學習、面對挑戰的人"]},
{"ch":"未來發展","camp":"商管營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img016.png","timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"未來發展","camp":"商管營","p":"Part 1","m":"影片一 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img017.png","timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>＋寫 After","sub":"先看第一支影片，再到 Notion 補上你的 After"},
{"ch":"未來發展","camp":"商管營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"未來發展","title":"複習"},
{"ch":"未來發展","camp":"商管營","p":"Part 2","m":"複習一下 · 職涯走向、技能、薪資、趨勢","type":"frame","kicker":"複習一下 · 垂直職缺、常備技能、產業薪資、未來趨勢","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"垂直職缺與從業趨勢","p":"主要職涯走向分為金融、管理、行銷三塊，例如業務執行（奧美廣告）、專案管理師（酷寶資訊）、P&G 寶僑的行銷職缺。多數人由行銷或管理入行，之後部分會轉職至金融業，且多數人都以管理職為目標。"},{"b":"2","c":"var(--m-green)","h":"商管人才常備技能","p":"工具面：熟悉 Microsoft、Adobe 工具；能力面：專案時間與進度控管、提案簡報、財務營業分析、品牌行銷管理、市場調查與報告撰寫；證照面：多益、托福、雅思等外語檢定，以及證券商業務員、金融市場常識等專業證照。"},{"b":"3","c":"var(--m-yellow)","h":"產業薪資概況","p":"國內：管理職起薪較低但工時較穩定，專案管理約 3～6 萬；行銷職落差大，外商頂級品牌行銷新鮮人可達 8 萬、年薪 150 萬，數位行銷約 3～5 萬。國外：頂尖 MBA 畢業後年薪可達 15 萬美金，投資銀行業更可挑戰 20 萬美金。"},{"b":"4","c":"var(--m-red)","h":"產業未來趨勢","p":"現況重視產學合作，透過多份實習累積履歷、爭取高起薪；就業三至五年後常再讀 MBA 轉換跑道。未來則更看重數位能力（數據分析、數位工具）與科技掌握度（AI、Blockchain、Cloud、Data、Edge Computing、5G）。"}]},
{"ch":"未來發展","camp":"商管營","p":"Part 2","m":"想想看 · 想先深入了解的一塊","type":"quiz","noans":true,"kicker":"想想看 · 延伸領域、大學所學、高中準備","art":"question","q":"商管職涯的延伸探索，你最想先深入了解哪一塊？","opts":["延伸領域——私募／創投尋找投資標的並協助企業成長，管顧則像企業的醫生解決策略問題","職缺對應大學所學——財經修會計財務、行銷修大數據行銷策略、管理修策略與專案管理","高中就能準備——多讀 Financial Times、WSJ 等財經媒體，培養口說與統計數據分析能力","營隊與競賽——參加台大管院營、GIS 集思、模擬聯合國等，累積商管視野與人脈"]},
{"ch":"未來發展","camp":"商管營","p":"Part 2","m":"影片二 + 截圖 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img018.png","timer":780,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>＋寫 After","sub":"到 Notion 看影片二吧，記得把重點截圖存下來，並寫下你的 After"},
{"ch":"未來發展","camp":"商管營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"未來發展","title":"反思"},
{"ch":"未來發展","camp":"商管營","p":"Part 3","m":"感受 · 常見職缺與領域","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於商管系的常見職缺與領域，你<span class=\"hl\">喜歡</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">領域：金融／管理／行銷｜職務：PM、人資、營運、企劃、創投、管顧</span>"},
{"ch":"未來發展","camp":"商管營","p":"Part 3","m":"感受 · 常備技能","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於商管人才常備技能，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">專案控管、提案簡報、企劃規劃、品牌行銷｜策略擬定、市場調查、財務分析</span>"},
{"ch":"未來發展","camp":"商管營","p":"Part 3","m":"感受 · 未來趨勢與應用","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於商管的未來趨勢與應用，你<span class=\"hl\">期待</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">數據分析、數位工具、ABCDEF</span>"},
{"ch":"未來發展","camp":"商管營","p":"Part 3","m":"寫 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img019.png","timer":180,"title":"寫 After<br>（自主反思）"},
{"ch":"未來發展","camp":"商管營","p":"Part 3","m":"Action 行動 + Review 反思","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img020.png","timer":900,"title":"Action <span class=\"hl\">行動</span>＋Review <span class=\"hl\">反思</span>"},
{"ch":"收尾","camp":"商管營","m":"午餐後，問學長姐 Slido","type":"frame","kicker":"吃飯後，問問學長姐","art":"question","title":"到 <span class=\"hl\">Slido</span>，用 USB 三個方向問","steps":[{"b":"U","c":"var(--m-blue)","h":"Usually｜平常","p":"學長姐平常都在忙什麼？課堂、實習、值班的日常長什麼樣？"},{"b":"S","c":"var(--m-green)","h":"Situation｜實況","p":"這個領域真實的狀況——課業、實作訓練、實際在做什麼？"},{"b":"B","c":"var(--m-yellow)","h":"Be Back｜重來","p":"如果回到高中，會給當時的自己、或給我們什麼建議？"}],"note":"其他想問的也都可以——直接把問題打在 Slido 上！（此處可放 Slido 畫面）"},
{"ch":"收尾","camp":"商管營","m":"午餐吃什麼？","type":"cover","art":"lunch","timer":30,"title":"午餐吃什麼？","sub":"趁午休前，先在聊天室或 Slido 上分享一下你今天想吃什麼、或推薦附近好吃的店家吧！"},
{"ch":"收尾","camp":"商管營","m":"午餐 · 1:30 回來","type":"cover","art":"lunch","music":true,"title":"午餐時間到！","sub":"記得先去吃飯、補充能量～ 下午 <span class=\"hl\">1:30 準時回來</span>！"},
{"ch":"未來發展","m":"競賽 · Kahoot","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"吃飯前，先來一場 PK！打開 Kahoot、輸入 PIN，看看你記住多少、答對多少～","p":"Part 3","camp":"商管營"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"寫 Slido","type":"cover","art":"question","shotPlaceholder":true,"shotMaxWidth":"360px","shot":"images/img021.png","timer":180,"title":"寫 <span class=\"hl\">Slido</span>","sub":"把你的想法或問題打在 Slido 上，我們稍後一起看！"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":2,"chLabel":"實際操作","title":"前導"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"測驗 · 個案分析是什麼","type":"quiz","noans":true,"kicker":"實際操作 · 第 1 題","art":"pulse","q":"「個案分析」，是什麼？","opts":["起源自哈佛課程，用於高階經理人的培訓與實踐","以實際商業問題為例，思考「如果主角是我會怎麼做？」","常出現在課堂討論、課堂報告、面試等時機","分成個人（費米題型、問答題型）與團體（完整個案、情境個案）兩大類型"]},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"測驗 · 個案分析培養能力","type":"quiz","noans":true,"kicker":"實際操作 · 第 2 題","art":"path","q":"學習「個案分析」，可以培養什麼能力？","opts":["預先準備與辨識——收集分析資料、分辨事實與意見，做出更明智的決策","偏見識別與判斷力——識別並避開偏見，在複雜情境中做出正確合理的決策","合作與好奇心——與他人協同工作，並保持對新知識的探索與學習","自信心——對自己的分析與判斷充滿信心，能自信表達並捍衛觀點"]},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"測驗 · MECE是什麼","type":"quiz","noans":true,"kicker":"實際操作 · 第 3 題","art":"question","q":"「MECE」，是什麼？","opts":["建立架構時使用的拆解方法，讓分類彼此獨立、互無遺漏","釐清問題階段的工具，用來確認要解決的問題到底是什麼","個案分析中，用來組織與拆解複雜問題的思考工具","還不熟悉，想在這堂課多了解實際怎麼運用"]},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img022.png","timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img023.png","timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"個案分析介紹 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img024.png","timer":600,"noMusic":true,"title":"看「個案分析介紹」影片＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"個案分析步驟：釐清問題+建立架構 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img025.png","timer":600,"noMusic":true,"title":"看「個案分析步驟」影片＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"互動：實際操作最有感的地方","type":"cover","art":"question","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得實際操作最有感的地方"},
{"ch":"實際操作","camp":"商管營","p":"Part 1","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":2,"chLabel":"實際操作","title":"複習"},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"複習一下 · 個案分析步驟","type":"frame","kicker":"複習一下 · 釐清問題、建立架構、填入內容、提出總結","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"一、釐清問題","p":"重述題目，確定你接收到的訊息和面試官提出的問題一致；提出問題，詢問不清楚的詞彙、該企業或市場的背景資訊；再藉由對方提出的內容，確定要解決的分析目標是什麼。"},{"b":"2","c":"var(--m-green)","h":"二、建立架構","p":"用 MECE 的方式不斷拆解問題，畫出樹狀圖；架構中的問題至少要包含一個「量性問題」與一個「質性問題」，讓分類彼此獨立、互無遺漏。"},{"b":"3","c":"var(--m-yellow)","h":"三、填入內容","p":"從建立好的架構中，挑選一個量性問題與一個質性問題來回答：量性問題列出你的估算架構，質性問題寫下你的解決方案。"},{"b":"4","c":"var(--m-red)","h":"四、提出總結","p":"統整上述內容，依序講述分析邏輯、建議解方、下一步建議——包含架構中尚未探索的部分、現階段沒有答案的問題，以及提出建議的潛在風險。"}]},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"想想看 · 質性量性、問題拆解、提出總結","type":"quiz","noans":true,"kicker":"想想看 · 質性與量性、質性問題拆解、提出總結","art":"path","q":"個案分析的實作步驟，你最想先搞懂哪一個？","opts":["質性與量性問題——分辨腦力激盪、商業建議等質性問題，與市場規模、利潤等量性問題","質性問題拆解——用經濟障礙與非經濟障礙，分析進入市場的可行性","提出總結——依序講述分析邏輯、建議解方、下一步建議","我還想多了解實際案例是怎麼操作的"]},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"看影片","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img026.png","timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片</span>","sub":"到 Notion 看影片，了解實作的內容吧"},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"實作 + 寫 After（1）","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img027.png","timer":600,"music":true,"title":"實作＋寫 <span class=\"hl\">After</span>","sub":"動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"實作 + 寫 After（2）","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img028.png","timer":600,"music":true,"title":"實作＋寫 <span class=\"hl\">After</span>","sub":"動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"實作 + 寫 After（3）","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img029.png","timer":600,"music":true,"title":"實作＋寫 <span class=\"hl\">After</span>","sub":"動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"實作 + 寫 After（4）","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img030.png","timer":600,"music":true,"title":"實作＋寫 <span class=\"hl\">After</span>","sub":"動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"實際操作","title":"引導"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"感受 · 釐清問題","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於「釐清問題」的過程，你<span class=\"hl\">喜歡</span>的程度為何？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">重述題目、提出問題、確定分析目標</span>"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"感受 · MECE","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於使用 MECE 的過程，你<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">拆解問題、建立樹狀架構、量性問題、質性問題</span>"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"感受 · 練習解決問題","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"在練習解決問題的環節，你<span class=\"hl\">想學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">量性問題，估算數值架構｜質性問題，提出解決方案</span>"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img031.png","timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"Action + Review","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img032.png","timer":900,"title":"Action ＋ <span class=\"hl\">Review</span>"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"Kahoot：實際操作","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"打開 Kahoot、輸入 PIN，看看實際操作這段你記住多少、答對多少～"},
{"ch":"實際操作","camp":"商管營","p":"Part 3","m":"實際操作結束中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"實際操作","camp":"商管營","p":"Part 2","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"休息","camp":"商管營","m":"中場休息 · 計時器＋音樂","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"休息","camp":"商管營","m":"聊天室分享","type":"cover","art":"hand","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"趁這幾分鐘，把你現在的想法、心得，或任何問題打在聊天室裡分享給大家！"},
{"ch":"開場暖身","type":"raw","m":"閒聊 · 今天早餐吃什麼","music":true,"html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>先來閒聊一下</div>\n      <div class=\"art-xl\" data-seq=\"0\"><svg viewBox=\"0 0 200 170\" xmlns=\"http://www.w3.org/2000/svg\">\n  <ellipse cx=\"100\" cy=\"128\" rx=\"78\" ry=\"18\" fill=\"#3fe0d0\" opacity=\".15\"/>\n  <ellipse cx=\"100\" cy=\"108\" rx=\"70\" ry=\"22\" fill=\"#cdd6f5\"/><ellipse cx=\"100\" cy=\"102\" rx=\"70\" ry=\"22\" fill=\"#fff\"/>\n  <circle cx=\"80\" cy=\"96\" r=\"22\" fill=\"#FFD63B\"/><circle cx=\"80\" cy=\"96\" r=\"22\" fill=\"none\" stroke=\"#fff5d0\" stroke-width=\"3\" opacity=\".5\"/>\n  <ellipse cx=\"126\" cy=\"98\" rx=\"20\" ry=\"11\" fill=\"#e8a85c\"/>\n  <path d=\"M118 92 q8 -6 16 0\" stroke=\"#c47a3a\" stroke-width=\"2.5\" fill=\"none\"/>\n  <g stroke=\"#3fe0d0\" stroke-width=\"5\" stroke-linecap=\"round\" opacity=\".6\" fill=\"none\">\n    <path d=\"M78 52 Q86 40 78 28\"><animate attributeName=\"opacity\" values=\".6;.2;.6\" dur=\"2s\" repeatCount=\"indefinite\"/></path>\n    <path d=\"M96 50 Q104 38 96 26\"><animate attributeName=\"opacity\" values=\".3;.6;.3\" dur=\"2.3s\" repeatCount=\"indefinite\"/></path>\n  </g>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">今天的<span class=\"hl\">早餐</span><br>吃了什麼？</h2>\n      <div class=\"action-hint\" data-seq=\"0\">💬 在聊天室打上你今天早餐吃什麼</div>\n      \n    </div>"},
{"ch":"開場暖身","type":"raw","m":"封面 · Welcome","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"cover-sub\" data-seq=\"0\">CIA · COMPANY IN AIR</div>\n      <div class=\"art-scene\" data-seq=\"0\" style=\"max-width:min(48vw,500px)\"><svg viewBox=\"0 0 600 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <radialGradient id=\"ls-earth\" cx=\"40%\" cy=\"40%\" r=\"80%\"><stop offset=\"0%\" stop-color=\"#6cc9ff\"/><stop offset=\"60%\" stop-color=\"#2a7fd4\"/><stop offset=\"100%\" stop-color=\"#143f7a\"/></radialGradient>\n    <linearGradient id=\"ls-rk\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#fff\"/><stop offset=\"100%\" stop-color=\"#cdd6f5\"/></linearGradient>\n    <linearGradient id=\"ls-fl\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"70%\" stop-color=\"#ff8c3b\"/><stop offset=\"100%\" stop-color=\"#ff5b5b\"/></linearGradient>\n    <linearGradient id=\"ls-trail\" x1=\"0\" y1=\"1\" x2=\"1\" y2=\"0\"><stop offset=\"0%\" stop-color=\"#FFD63B\" stop-opacity=\"0\"/><stop offset=\"100%\" stop-color=\"#FFD63B\" stop-opacity=\".55\"/></linearGradient>\n  </defs>\n  <g>\n    <circle cx=\"120\" cy=\"360\" r=\"130\" fill=\"url(#ls-earth)\"/>\n    <path d=\"M70 300 Q110 286 150 304 Q166 326 138 342 Q92 348 70 326 Z\" fill=\"#3fbf7a\" opacity=\".9\"/>\n    <path d=\"M170 340 Q210 334 230 352 Q236 372 206 380 Q172 384 162 364 Z\" fill=\"#3fbf7a\" opacity=\".85\"/>\n    <ellipse cx=\"92\" cy=\"312\" rx=\"22\" ry=\"10\" fill=\"#fff\" opacity=\".22\"/>\n    <circle cx=\"120\" cy=\"360\" r=\"130\" fill=\"none\" stroke=\"#aee9ff\" stroke-width=\"2.5\" opacity=\".4\"/>\n  </g>\n  <path d=\"M150 320 Q300 260 430 130\" stroke=\"url(#ls-trail)\" stroke-width=\"10\" fill=\"none\" stroke-linecap=\"round\" stroke-dasharray=\"2 16\"><animate attributeName=\"stroke-dashoffset\" values=\"0;-180\" dur=\"3s\" repeatCount=\"indefinite\"/></path>\n  <g transform=\"translate(430 120) rotate(42)\">\n    <path d=\"M0 -52 C20 -28 22 6 18 40 L-18 40 C-22 6 -20 -28 0 -52Z\" fill=\"url(#ls-rk)\"/>\n    <circle cx=\"0\" cy=\"-16\" r=\"11\" fill=\"#161e4a\"/><circle cx=\"0\" cy=\"-16\" r=\"7\" fill=\"#3fe0d0\"/>\n    <path d=\"M-18 26 L-36 54 L-18 44Z\" fill=\"#ff6b6b\"/><path d=\"M18 26 L36 54 L18 44Z\" fill=\"#ff6b6b\"/>\n    <rect x=\"-18\" y=\"40\" width=\"36\" height=\"9\" rx=\"3\" fill=\"#7c5cff\"/>\n    <path d=\"M-11 49 Q0 92 11 49 Q0 66 -11 49Z\" fill=\"url(#ls-fl)\"><animate attributeName=\"opacity\" values=\"1;.5;1\" dur=\".4s\" repeatCount=\"indefinite\"/></path>\n  </g>\n  <g fill=\"#fff\"><circle cx=\"320\" cy=\"80\" r=\"2\"/><circle cx=\"500\" cy=\"200\" r=\"2.5\"/><circle cx=\"380\" cy=\"200\" r=\"1.6\"/><circle cx=\"540\" cy=\"90\" r=\"1.8\"/><circle cx=\"260\" cy=\"140\" r=\"1.6\"/></g>\n  <g fill=\"#FFD63B\"><circle cx=\"470\" cy=\"60\" r=\"2\"/><circle cx=\"350\" cy=\"300\" r=\"1.8\"/></g>\n</svg></div>\n      <h1 class=\"h-mega cover-title\" data-seq=\"0\">歡迎來到 <span class=\"hl\">CIA 科系星球</span></h1>\n      <p class=\"lead\" data-seq=\"1\">請同學們準備好，和我們一起開始探索的旅程吧～～</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"今日節奏 · 午餐 12:30","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>今日航程</div>\n      <div class=\"split\" data-seq=\"0\">\n        <div class=\"split-l\"><div class=\"bigtime xl\">12:30</div><h2 class=\"h-mid\">午餐時間（依進度微調）</h2></div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 400 320\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><linearGradient id=\"lb\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ff8c6b\"/><stop offset=\"100%\" stop-color=\"#e85c3a\"/></linearGradient></defs>\n  <ellipse cx=\"200\" cy=\"280\" rx=\"150\" ry=\"24\" fill=\"#3fe0d0\" opacity=\".15\"/>\n  <rect x=\"70\" y=\"150\" width=\"260\" height=\"120\" rx=\"18\" fill=\"url(#lb)\"/>\n  <rect x=\"70\" y=\"150\" width=\"260\" height=\"36\" rx=\"18\" fill=\"#ffb088\" opacity=\".6\"/>\n  <rect x=\"86\" y=\"166\" width=\"100\" height=\"88\" rx=\"10\" fill=\"#fff3e0\"/>\n  <circle cx=\"120\" cy=\"200\" r=\"16\" fill=\"#FFD63B\"/>\n  <ellipse cx=\"150\" cy=\"220\" rx=\"22\" ry=\"13\" fill=\"#e8a85c\"/>\n  <rect x=\"196\" y=\"166\" width=\"60\" height=\"40\" rx=\"8\" fill=\"#3fbf7a\" opacity=\".85\"/>\n  <rect x=\"196\" y=\"212\" width=\"60\" height=\"42\" rx=\"8\" fill=\"#fff3e0\"/>\n  <circle cx=\"226\" cy=\"233\" r=\"13\" fill=\"#ff6b6b\"/>\n  <rect x=\"266\" y=\"166\" width=\"50\" height=\"88\" rx=\"10\" fill=\"#fff3e0\"/>\n  <circle cx=\"291\" cy=\"210\" r=\"6\" fill=\"#ffd0a0\"/>\n  <g stroke=\"#fff\" stroke-width=\"4\" stroke-linecap=\"round\" opacity=\".5\" fill=\"none\">\n    <path d=\"M150 140 Q158 126 150 112\"><animate attributeName=\"opacity\" values=\".5;.1;.5\" dur=\"2s\" repeatCount=\"indefinite\"/></path>\n    <path d=\"M220 140 Q228 126 220 112\"><animate attributeName=\"opacity\" values=\".3;.6;.3\" dur=\"2.4s\" repeatCount=\"indefinite\"/></path>\n  </g>\n  <rect x=\"338\" y=\"120\" width=\"6\" height=\"150\" rx=\"3\" fill=\"#c98e1a\" transform=\"rotate(8 341 195)\"/>\n  <rect x=\"352\" y=\"120\" width=\"6\" height=\"150\" rx=\"3\" fill=\"#c98e1a\" transform=\"rotate(8 355 195)\"/>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">記得提醒家人，大約 <span class=\"hl\">12:20</span> 幫你準備好午餐 🍱</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"今日節奏 · 重返地球 18:30","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>今日航程 · 重返地球</div>\n      <div class=\"split\" data-seq=\"0\">\n        <div class=\"split-l\"><div class=\"bigtime xl\">18:30</div><h2 class=\"h-mid\">營隊閉幕，<span class=\"hl\">重返地球</span> 🌍</h2></div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 600 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <radialGradient id=\"re-earth\" cx=\"50%\" cy=\"46%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#7fd4ff\"/><stop offset=\"55%\" stop-color=\"#2a7fd4\"/><stop offset=\"100%\" stop-color=\"#10336a\"/></radialGradient>\n    <linearGradient id=\"re-heat\" x1=\"0\" y1=\"0\" x2=\"1\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ff5b5b\"/><stop offset=\"50%\" stop-color=\"#ff8c3b\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></linearGradient>\n    <linearGradient id=\"re-trail\" x1=\"1\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ff8c3b\" stop-opacity=\"0\"/><stop offset=\"100%\" stop-color=\"#ff5b5b\" stop-opacity=\".5\"/></linearGradient>\n  </defs>\n  <g>\n    <circle cx=\"300\" cy=\"600\" r=\"360\" fill=\"url(#re-earth)\"/>\n    <ellipse cx=\"300\" cy=\"262\" rx=\"300\" ry=\"30\" fill=\"#aee9ff\" opacity=\".25\"/>\n    <path d=\"M160 300 Q230 286 300 306 Q330 330 286 346 Q200 352 168 326 Z\" fill=\"#3fbf7a\" opacity=\".8\"/>\n    <path d=\"M360 320 Q430 312 470 332 Q480 354 440 364 Q380 368 358 346 Z\" fill=\"#3fbf7a\" opacity=\".75\"/>\n  </g>\n  <path d=\"M520 70 Q400 130 320 200\" stroke=\"url(#re-trail)\" stroke-width=\"14\" fill=\"none\" stroke-linecap=\"round\"><animate attributeName=\"opacity\" values=\".7;.35;.7\" dur=\"2s\" repeatCount=\"indefinite\"/></path>\n  <g transform=\"translate(320 200) rotate(135)\">\n    <path d=\"M0 -46 C18 -24 20 4 16 36 L-16 36 C-20 4 -18 -24 0 -46Z\" fill=\"#fff\"/>\n    <path d=\"M0 -46 C8 -36 12 -14 10 20 L-10 20 C-12 -14 -8 -36 0 -46Z\" fill=\"#cdd6f5\"/>\n    <circle cx=\"0\" cy=\"-14\" r=\"9\" fill=\"#161e4a\"/><circle cx=\"0\" cy=\"-14\" r=\"6\" fill=\"#3fe0d0\"/>\n    <path d=\"M-16 22 L-32 44 L-16 36Z\" fill=\"#7c5cff\"/><path d=\"M16 22 L32 44 L16 36Z\" fill=\"#7c5cff\"/>\n    <path d=\"M-22 34 Q0 56 22 34 Q0 48 -22 34Z\" fill=\"url(#re-heat)\"><animate attributeName=\"opacity\" values=\"1;.6;1\" dur=\".4s\" repeatCount=\"indefinite\"/></path>\n  </g>\n  <g fill=\"#fff\"><circle cx=\"120\" cy=\"80\" r=\"2\"/><circle cx=\"480\" cy=\"160\" r=\"2.2\"/><circle cx=\"200\" cy=\"130\" r=\"1.6\"/><circle cx=\"90\" cy=\"180\" r=\"1.8\"/></g>\n  <g fill=\"#FFD63B\"><circle cx=\"150\" cy=\"50\" r=\"1.8\"/><circle cx=\"450\" cy=\"70\" r=\"2\"/></g>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">相信我 —— 時間真的會過超快的！</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"規則 · 全程開鏡頭","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split\" data-seq=\"0\">\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 480 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"wc-screen\" x1=\"0\" y1=\"0\" x2=\"1\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#1b2658\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></linearGradient>\n    <radialGradient id=\"wc-face\" cx=\"50%\" cy=\"40%\" r=\"60%\"><stop offset=\"0%\" stop-color=\"#ffe2c4\"/><stop offset=\"100%\" stop-color=\"#f0b98a\"/></radialGradient>\n  </defs>\n  <path d=\"M70 330 L410 330 L450 372 L30 372 Z\" fill=\"#2a3470\"/>\n  <rect x=\"60\" y=\"322\" width=\"360\" height=\"14\" rx=\"4\" fill=\"#3a4690\"/>\n  <rect x=\"80\" y=\"70\" width=\"320\" height=\"256\" rx=\"14\" fill=\"#0a0f24\"/>\n  <rect x=\"92\" y=\"82\" width=\"296\" height=\"220\" rx=\"8\" fill=\"url(#wc-screen)\"/>\n  <circle cx=\"240\" cy=\"180\" r=\"52\" fill=\"url(#wc-face)\"/>\n  <path d=\"M214 168 a8 8 0 0 1 16 0\" fill=\"#2a2030\"/><path d=\"M250 168 a8 8 0 0 1 16 0\" fill=\"#2a2030\"/>\n  <path d=\"M224 200 Q240 214 256 200\" stroke=\"#b5654a\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/>\n  <path d=\"M188 168 Q200 120 240 118 Q280 120 292 168 Q292 140 240 132 Q188 140 188 168Z\" fill=\"#3a2a22\"/>\n  <rect x=\"206\" y=\"232\" width=\"68\" height=\"50\" rx=\"20\" fill=\"#3fe0d0\"/>\n  <g transform=\"translate(240 96)\"><circle cx=\"0\" cy=\"0\" r=\"6\" fill=\"#3fbf7a\"><animate attributeName=\"opacity\" values=\"1;.4;1\" dur=\"1.4s\" repeatCount=\"indefinite\"/></circle></g>\n  <g transform=\"translate(330 250)\">\n    <rect x=\"-26\" y=\"-15\" width=\"44\" height=\"30\" rx=\"7\" fill=\"#3fe0d0\"/>\n    <path d=\"M18 -8 L34 -16 L34 16 L18 8Z\" fill=\"#3fe0d0\"/>\n  </g>\n  <g fill=\"#FFD63B\"><circle cx=\"50\" cy=\"120\" r=\"2.5\"/><circle cx=\"430\" cy=\"150\" r=\"2.5\"/><circle cx=\"60\" cy=\"240\" r=\"2\"/></g>\n</svg></div>\n        <div class=\"split-l\">\n          <div class=\"eyebrow\"><span class=\"dot\"></span>小小的請求</div>\n          <h2 class=\"h-big\" style=\"text-align:left\">全程請<br><span class=\"hl\">打開鏡頭</span> 📷</h2>\n        </div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">沒有打開鏡頭的同學，很難過的，我們會把你踢出去喔 😭</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"互動方式 · 總覽","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>今天的互動方式</div>\n      <h2 class=\"h-big\" data-seq=\"0\">用這些方式，<br>一起玩起來！</h2>\n      <div class=\"op-cards c3\" data-seq=\"1\">\n        <div class=\"op-card\"><span class=\"ic\">😆</span><h3>點擊表情符號</h3><p>在 Google Meet 點下方的反應</p></div>\n        <div class=\"op-card\"><span class=\"ic\">✋</span><h3>鏡頭前比手勢</h3><p>把手舉到鏡頭前讓我看到</p></div>\n        <div class=\"op-card\"><span class=\"ic\">💬</span><h3>聊天室打字</h3><p>把你的想法打出來</p></div>\n      </div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"互動① · 點擊表情符號","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>互動方式 ①</div>\n      <h2 class=\"h-big\" data-seq=\"0\">在 Google Meet<br>點擊這些<span class=\"hl\">表情符號</span></h2>\n      <div class=\"meet-bar\" data-seq=\"0\"><div class=\"op-emoji-bar\"><div class=\"op-emoji\" data-k=\"heart\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"eh\" cx=\"40%\" cy=\"35%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ff9ec7\"/><stop offset=\"100%\" stop-color=\"#ff4d94\"/></radialGradient></defs><path d=\"M50 84 C16 60 12 38 26 26 C38 16 50 24 50 36 C50 24 62 16 74 26 C88 38 84 60 50 84Z\" fill=\"url(#eh)\"/><path d=\"M70 20 l3 7 l7 3 l-7 3 l-3 7 l-3 -7 l-7 -3 l7 -3Z\" fill=\"#fff\"/><circle cx=\"34\" cy=\"34\" r=\"4\" fill=\"#fff\" opacity=\".7\"/></svg></div><div class=\"op-emoji\" data-k=\"thumb\"><svg viewBox=\"0 0 100 100\"><defs><linearGradient id=\"et\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#f0b429\"/></linearGradient></defs><rect x=\"20\" y=\"46\" width=\"20\" height=\"36\" rx=\"6\" fill=\"#e89a2c\"/><path d=\"M42 48 C42 38 52 34 52 22 C52 14 62 14 62 24 C62 32 58 40 58 44 L74 44 C82 44 84 52 80 64 C78 76 74 82 64 82 L46 82 C42 82 42 78 42 74Z\" fill=\"url(#et)\"/></svg></div><div class=\"op-emoji\" data-k=\"party\"><svg viewBox=\"0 0 100 100\"><path d=\"M22 80 L40 34 L66 60Z\" fill=\"#FFD63B\"/><path d=\"M22 80 L34 50 L52 68Z\" fill=\"#ff8c3b\"/><g><circle cx=\"60\" cy=\"24\" r=\"4\" fill=\"#ff6b6b\"/><circle cx=\"74\" cy=\"38\" r=\"3.5\" fill=\"#3fe0d0\"/><circle cx=\"50\" cy=\"18\" r=\"3\" fill=\"#7c5cff\"/><circle cx=\"78\" cy=\"22\" r=\"3\" fill=\"#FFD63B\"/><rect x=\"66\" y=\"50\" width=\"6\" height=\"6\" fill=\"#ff6b6b\" transform=\"rotate(20 69 53)\"/><rect x=\"80\" y=\"56\" width=\"5\" height=\"5\" fill=\"#7c5cff\" transform=\"rotate(30 82 58)\"/></g><path d=\"M58 30 Q70 26 80 34\" stroke=\"#3fe0d0\" stroke-width=\"2.5\" fill=\"none\"/></svg></div><div class=\"op-emoji\" data-k=\"clap\"><svg viewBox=\"0 0 100 100\"><defs><linearGradient id=\"ec\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#f0b429\"/></linearGradient></defs><g transform=\"rotate(-12 50 50)\"><rect x=\"30\" y=\"40\" width=\"34\" height=\"30\" rx=\"14\" fill=\"url(#ec)\"/><rect x=\"34\" y=\"30\" width=\"9\" height=\"26\" rx=\"4\" fill=\"url(#ec)\"/><rect x=\"44\" y=\"26\" width=\"9\" height=\"30\" rx=\"4\" fill=\"url(#ec)\"/><rect x=\"54\" y=\"30\" width=\"9\" height=\"26\" rx=\"4\" fill=\"url(#ec)\"/></g><g stroke=\"#FFD63B\" stroke-width=\"3\" stroke-linecap=\"round\"><line x1=\"70\" y1=\"30\" x2=\"80\" y2=\"24\"/><line x1=\"74\" y1=\"44\" x2=\"86\" y2=\"42\"/><line x1=\"66\" y1=\"20\" x2=\"70\" y2=\"10\"/></g></svg></div><div class=\"op-emoji\" data-k=\"joy\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"ej\" cx=\"40%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ffe98a\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient></defs><circle cx=\"50\" cy=\"50\" r=\"40\" fill=\"url(#ej)\"/><path d=\"M28 42 Q36 34 46 42\" stroke=\"#5a3a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M54 42 Q64 34 72 42\" stroke=\"#5a3a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M32 58 Q50 80 68 58 Q50 70 32 58Z\" fill=\"#7a4a00\"/><path d=\"M34 60 Q50 74 66 60\" fill=\"#ff5b5b\"/><path d=\"M26 50 Q20 58 24 64\" stroke=\"#6cc9ff\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M74 50 Q80 58 76 64\" stroke=\"#6cc9ff\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/></svg></div><div class=\"op-emoji\" data-k=\"wow\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"ew\" cx=\"40%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ffe98a\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient></defs><circle cx=\"50\" cy=\"50\" r=\"40\" fill=\"url(#ew)\"/><circle cx=\"38\" cy=\"42\" r=\"5\" fill=\"#5a3a00\"/><circle cx=\"62\" cy=\"42\" r=\"5\" fill=\"#5a3a00\"/><ellipse cx=\"50\" cy=\"66\" rx=\"11\" ry=\"14\" fill=\"#7a4a00\"/></svg></div><div class=\"op-emoji\" data-k=\"cry\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"ecr\" cx=\"40%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ffe98a\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient></defs><circle cx=\"50\" cy=\"50\" r=\"40\" fill=\"url(#ecr)\"/><path d=\"M30 40 Q38 36 46 40\" stroke=\"#5a3a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M54 40 Q62 36 70 40\" stroke=\"#5a3a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M36 70 Q50 60 64 70\" stroke=\"#7a4a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M34 48 Q30 64 36 72 Q42 64 38 48Z\" fill=\"#6cc9ff\"><animate attributeName=\"opacity\" values=\"1;.5;1\" dur=\"1.6s\" repeatCount=\"indefinite\"/></path></svg></div><div class=\"op-emoji\" data-k=\"think\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"eth2\" cx=\"40%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ffe98a\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient></defs><circle cx=\"50\" cy=\"50\" r=\"40\" fill=\"url(#eth2)\"/><circle cx=\"37\" cy=\"44\" r=\"4\" fill=\"#5a3a00\"/><circle cx=\"60\" cy=\"44\" r=\"4\" fill=\"#5a3a00\"/><path d=\"M40 64 L62 60\" stroke=\"#5a3a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M52 70 Q66 70 66 60 Q66 54 58 56\" fill=\"none\" stroke=\"#c98e1a\" stroke-width=\"5\" stroke-linecap=\"round\"/><circle cx=\"56\" cy=\"56\" r=\"4\" fill=\"#e89a2c\"/></svg></div><div class=\"op-emoji\" data-k=\"thumbDown\"><svg viewBox=\"0 0 100 100\"><defs><linearGradient id=\"etd\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#f0b429\"/><stop offset=\"100%\" stop-color=\"#d99318\"/></linearGradient></defs><rect x=\"20\" y=\"18\" width=\"20\" height=\"36\" rx=\"6\" fill=\"#e89a2c\"/><path d=\"M42 52 C42 62 52 66 52 78 C52 86 62 86 62 76 C62 68 58 60 58 56 L74 56 C82 56 84 48 80 36 C78 24 74 18 64 18 L46 18 C42 18 42 22 42 26Z\" fill=\"url(#etd)\"/></svg></div></div></div>\n      <p class=\"lead\" data-seq=\"1\">我請大家「按 ❤️」，就點一下愛心；<br>覺得誰講得很爛，就送他一個 👎！</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"互動② · 比手勢","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split\" data-seq=\"0\">\n        <div class=\"split-l\">\n          <div class=\"eyebrow\"><span class=\"dot\"></span>互動方式 ②</div>\n          <h2 class=\"h-big\" style=\"text-align:left\">在鏡頭前<br><span class=\"hl\">比手勢</span> ✌️</h2>\n        </div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 480 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"ya-screen\" x1=\"0\" y1=\"0\" x2=\"1\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#1b2658\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></linearGradient>\n    <radialGradient id=\"ya-face\" cx=\"50%\" cy=\"40%\" r=\"60%\"><stop offset=\"0%\" stop-color=\"#ffe2c4\"/><stop offset=\"100%\" stop-color=\"#f0b98a\"/></radialGradient>\n  </defs>\n  <path d=\"M70 330 L410 330 L450 372 L30 372 Z\" fill=\"#2a3470\"/>\n  <rect x=\"60\" y=\"322\" width=\"360\" height=\"14\" rx=\"4\" fill=\"#3a4690\"/>\n  <rect x=\"80\" y=\"70\" width=\"320\" height=\"256\" rx=\"14\" fill=\"#0a0f24\"/>\n  <rect x=\"92\" y=\"82\" width=\"296\" height=\"220\" rx=\"8\" fill=\"url(#ya-screen)\"/>\n  <!-- 頭 -->\n  <circle cx=\"210\" cy=\"165\" r=\"46\" fill=\"url(#ya-face)\"/>\n  <path d=\"M168 150 Q180 108 210 106 Q240 108 252 150 Q252 124 210 118 Q168 124 168 150Z\" fill=\"#3a2a22\"/>\n  <circle cx=\"196\" cy=\"160\" r=\"4\" fill=\"#2a2030\"/><circle cx=\"224\" cy=\"160\" r=\"4\" fill=\"#2a2030\"/>\n  <path d=\"M198 182 Q210 194 222 182\" stroke=\"#b5654a\" stroke-width=\"3.5\" fill=\"none\" stroke-linecap=\"round\"/>\n  <!-- 身體 -->\n  <rect x=\"180\" y=\"222\" width=\"60\" height=\"60\" rx=\"20\" fill=\"#3fe0d0\"/>\n  <!-- 比 Ya 的手（V 手勢） -->\n  <g transform=\"translate(290 200)\">\n    <rect x=\"-14\" y=\"0\" width=\"28\" height=\"40\" rx=\"13\" fill=\"url(#ya-face)\"/>\n    <rect x=\"-12\" y=\"-34\" width=\"11\" height=\"42\" rx=\"5\" fill=\"url(#ya-face)\"/>\n    <rect x=\"2\" y=\"-38\" width=\"11\" height=\"46\" rx=\"5\" fill=\"url(#ya-face)\"/>\n    <circle cx=\"-6\" cy=\"6\" r=\"6\" fill=\"#f0b98a\"/>\n  </g>\n  <!-- 開鏡頭燈 -->\n  <circle cx=\"240\" cy=\"96\" r=\"6\" fill=\"#3fbf7a\"><animate attributeName=\"opacity\" values=\"1;.4;1\" dur=\"1.4s\" repeatCount=\"indefinite\"/></circle>\n  <g fill=\"#FFD63B\"><circle cx=\"120\" cy=\"120\" r=\"2.5\"/><circle cx=\"360\" cy=\"150\" r=\"2.5\"/><circle cx=\"350\" cy=\"250\" r=\"2\"/></g>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">等等請你比 <span class=\"hl\">Ya</span>、比 <span class=\"hl\">5</span>、拿出<span class=\"hl-aqua\">綠色的東西</span>、再拿出<span class=\"hl-aqua\">一本書</span>！</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"互動③ · 聊天室打綽號","timer":30,"html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>互動方式 ③</div>\n      <div class=\"art-lg\" data-seq=\"0\"><svg viewBox=\"0 0 200 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <rect x=\"20\" y=\"22\" width=\"130\" height=\"84\" rx=\"22\" fill=\"#FFD63B\"/>\n  <path d=\"M54 104 L46 134 L82 104Z\" fill=\"#FFD63B\"/>\n  <circle cx=\"58\" cy=\"64\" r=\"8\" fill=\"#161e4a\"/><circle cx=\"86\" cy=\"64\" r=\"8\" fill=\"#161e4a\"/><circle cx=\"114\" cy=\"64\" r=\"8\" fill=\"#161e4a\"/>\n  <rect x=\"100\" y=\"70\" width=\"80\" height=\"56\" rx=\"18\" fill=\"#7c5cff\"/>\n  <path d=\"M148 124 L156 146 L120 124Z\" fill=\"#7c5cff\"/>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">在聊天室打上你的<span class=\"hl\">綽號</span></h2>\n      <ol class=\"op-steps\" data-seq=\"1\">\n        <li><span class=\"op-step-n\">1</span>點開<b>右下角</b>的聊天室</li>\n        <li><span class=\"op-step-n\">2</span>打上<b>你的綽號</b></li>\n      </ol>\n      \n    </div>"},
{"ch":"開場暖身","type":"raw","m":"團隊 · 頂大學長姐","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>關於我們</div>\n      <h2 class=\"h-big\" data-seq=\"0\">一群<span class=\"hl\">頂大學長姐</span><br>組成的探索團隊</h2>\n      <div class=\"grad-row\" data-seq=\"1\">\n        <div class=\"grad-fig\"><svg viewBox=\"0 0 160 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"gsFFD63B\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"gv3fe0d0\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#3fe0d0\"/><stop offset=\"72%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <ellipse cx=\"80\" cy=\"190\" rx=\"42\" ry=\"8\" fill=\"#000\" opacity=\".18\"/>\n  <path d=\"M44 120 Q80 108 116 120 L122 178 L38 178 Z\" fill=\"url(#gsFFD63B)\"/>\n  <path d=\"M70 112 L90 112 L86 178 L74 178 Z\" fill=\"#FFD63B\" opacity=\".9\"/>\n  <rect x=\"28\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gsFFD63B)\"/><rect x=\"112\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gsFFD63B)\"/>\n  <circle cx=\"38\" cy=\"166\" r=\"12\" fill=\"#FFD63B\"/><circle cx=\"122\" cy=\"166\" r=\"12\" fill=\"#FFD63B\"/>\n  <circle cx=\"80\" cy=\"74\" r=\"40\" fill=\"url(#gsFFD63B)\"/><circle cx=\"80\" cy=\"74\" r=\"29\" fill=\"url(#gv3fe0d0)\"/>\n  <ellipse cx=\"69\" cy=\"64\" rx=\"8\" ry=\"11\" fill=\"#fff\" opacity=\".5\"/>\n  <g transform=\"translate(80 36)\">\n    <rect x=\"-34\" y=\"-6\" width=\"68\" height=\"14\" rx=\"3\" fill=\"#1a2150\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"#222c63\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"none\" stroke=\"#FFD63B\" stroke-width=\"2\"/>\n    <circle cx=\"0\" cy=\"0\" r=\"4\" fill=\"#FFD63B\"/>\n    <path d=\"M0 0 L30 6 L30 22\" stroke=\"#FFD63B\" stroke-width=\"2.5\" fill=\"none\"/>\n    <circle cx=\"30\" cy=\"24\" r=\"4\" fill=\"#FFD63B\"/>\n  </g>\n  <rect x=\"68\" y=\"130\" width=\"24\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n</svg></div>\n        <div class=\"grad-fig\"><svg viewBox=\"0 0 160 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"gs7c5cff\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"gva48bff\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#a48bff\"/><stop offset=\"72%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <ellipse cx=\"80\" cy=\"190\" rx=\"42\" ry=\"8\" fill=\"#000\" opacity=\".18\"/>\n  <path d=\"M44 120 Q80 108 116 120 L122 178 L38 178 Z\" fill=\"url(#gs7c5cff)\"/>\n  <path d=\"M70 112 L90 112 L86 178 L74 178 Z\" fill=\"#7c5cff\" opacity=\".9\"/>\n  <rect x=\"28\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gs7c5cff)\"/><rect x=\"112\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gs7c5cff)\"/>\n  <circle cx=\"38\" cy=\"166\" r=\"12\" fill=\"#7c5cff\"/><circle cx=\"122\" cy=\"166\" r=\"12\" fill=\"#7c5cff\"/>\n  <circle cx=\"80\" cy=\"74\" r=\"40\" fill=\"url(#gs7c5cff)\"/><circle cx=\"80\" cy=\"74\" r=\"29\" fill=\"url(#gva48bff)\"/>\n  <ellipse cx=\"69\" cy=\"64\" rx=\"8\" ry=\"11\" fill=\"#fff\" opacity=\".5\"/>\n  <g transform=\"translate(80 36)\">\n    <rect x=\"-34\" y=\"-6\" width=\"68\" height=\"14\" rx=\"3\" fill=\"#1a2150\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"#222c63\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"none\" stroke=\"#7c5cff\" stroke-width=\"2\"/>\n    <circle cx=\"0\" cy=\"0\" r=\"4\" fill=\"#7c5cff\"/>\n    <path d=\"M0 0 L30 6 L30 22\" stroke=\"#7c5cff\" stroke-width=\"2.5\" fill=\"none\"/>\n    <circle cx=\"30\" cy=\"24\" r=\"4\" fill=\"#7c5cff\"/>\n  </g>\n  <rect x=\"68\" y=\"130\" width=\"24\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n</svg></div>\n        <div class=\"grad-fig big\"><svg viewBox=\"0 0 160 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"gs3fe0d0\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"gv8df3e8\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#8df3e8\"/><stop offset=\"72%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <ellipse cx=\"80\" cy=\"190\" rx=\"42\" ry=\"8\" fill=\"#000\" opacity=\".18\"/>\n  <path d=\"M44 120 Q80 108 116 120 L122 178 L38 178 Z\" fill=\"url(#gs3fe0d0)\"/>\n  <path d=\"M70 112 L90 112 L86 178 L74 178 Z\" fill=\"#3fe0d0\" opacity=\".9\"/>\n  <rect x=\"28\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gs3fe0d0)\"/><rect x=\"112\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gs3fe0d0)\"/>\n  <circle cx=\"38\" cy=\"166\" r=\"12\" fill=\"#3fe0d0\"/><circle cx=\"122\" cy=\"166\" r=\"12\" fill=\"#3fe0d0\"/>\n  <circle cx=\"80\" cy=\"74\" r=\"40\" fill=\"url(#gs3fe0d0)\"/><circle cx=\"80\" cy=\"74\" r=\"29\" fill=\"url(#gv8df3e8)\"/>\n  <ellipse cx=\"69\" cy=\"64\" rx=\"8\" ry=\"11\" fill=\"#fff\" opacity=\".5\"/>\n  <g transform=\"translate(80 36)\">\n    <rect x=\"-34\" y=\"-6\" width=\"68\" height=\"14\" rx=\"3\" fill=\"#1a2150\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"#222c63\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"2\"/>\n    <circle cx=\"0\" cy=\"0\" r=\"4\" fill=\"#3fe0d0\"/>\n    <path d=\"M0 0 L30 6 L30 22\" stroke=\"#3fe0d0\" stroke-width=\"2.5\" fill=\"none\"/>\n    <circle cx=\"30\" cy=\"24\" r=\"4\" fill=\"#3fe0d0\"/>\n  </g>\n  <rect x=\"68\" y=\"130\" width=\"24\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n</svg></div>\n        <div class=\"grad-fig\"><svg viewBox=\"0 0 160 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"gsff6b6b\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"gvff9d8a\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ff9d8a\"/><stop offset=\"72%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <ellipse cx=\"80\" cy=\"190\" rx=\"42\" ry=\"8\" fill=\"#000\" opacity=\".18\"/>\n  <path d=\"M44 120 Q80 108 116 120 L122 178 L38 178 Z\" fill=\"url(#gsff6b6b)\"/>\n  <path d=\"M70 112 L90 112 L86 178 L74 178 Z\" fill=\"#ff6b6b\" opacity=\".9\"/>\n  <rect x=\"28\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gsff6b6b)\"/><rect x=\"112\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gsff6b6b)\"/>\n  <circle cx=\"38\" cy=\"166\" r=\"12\" fill=\"#ff6b6b\"/><circle cx=\"122\" cy=\"166\" r=\"12\" fill=\"#ff6b6b\"/>\n  <circle cx=\"80\" cy=\"74\" r=\"40\" fill=\"url(#gsff6b6b)\"/><circle cx=\"80\" cy=\"74\" r=\"29\" fill=\"url(#gvff9d8a)\"/>\n  <ellipse cx=\"69\" cy=\"64\" rx=\"8\" ry=\"11\" fill=\"#fff\" opacity=\".5\"/>\n  <g transform=\"translate(80 36)\">\n    <rect x=\"-34\" y=\"-6\" width=\"68\" height=\"14\" rx=\"3\" fill=\"#1a2150\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"#222c63\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"none\" stroke=\"#ff6b6b\" stroke-width=\"2\"/>\n    <circle cx=\"0\" cy=\"0\" r=\"4\" fill=\"#ff6b6b\"/>\n    <path d=\"M0 0 L30 6 L30 22\" stroke=\"#ff6b6b\" stroke-width=\"2.5\" fill=\"none\"/>\n    <circle cx=\"30\" cy=\"24\" r=\"4\" fill=\"#ff6b6b\"/>\n  </g>\n  <rect x=\"68\" y=\"130\" width=\"24\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n</svg></div>\n        <div class=\"grad-fig\"><svg viewBox=\"0 0 160 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"gs6cc9ff\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"gvaee9ff\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#aee9ff\"/><stop offset=\"72%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <ellipse cx=\"80\" cy=\"190\" rx=\"42\" ry=\"8\" fill=\"#000\" opacity=\".18\"/>\n  <path d=\"M44 120 Q80 108 116 120 L122 178 L38 178 Z\" fill=\"url(#gs6cc9ff)\"/>\n  <path d=\"M70 112 L90 112 L86 178 L74 178 Z\" fill=\"#6cc9ff\" opacity=\".9\"/>\n  <rect x=\"28\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gs6cc9ff)\"/><rect x=\"112\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gs6cc9ff)\"/>\n  <circle cx=\"38\" cy=\"166\" r=\"12\" fill=\"#6cc9ff\"/><circle cx=\"122\" cy=\"166\" r=\"12\" fill=\"#6cc9ff\"/>\n  <circle cx=\"80\" cy=\"74\" r=\"40\" fill=\"url(#gs6cc9ff)\"/><circle cx=\"80\" cy=\"74\" r=\"29\" fill=\"url(#gvaee9ff)\"/>\n  <ellipse cx=\"69\" cy=\"64\" rx=\"8\" ry=\"11\" fill=\"#fff\" opacity=\".5\"/>\n  <g transform=\"translate(80 36)\">\n    <rect x=\"-34\" y=\"-6\" width=\"68\" height=\"14\" rx=\"3\" fill=\"#1a2150\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"#222c63\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"none\" stroke=\"#6cc9ff\" stroke-width=\"2\"/>\n    <circle cx=\"0\" cy=\"0\" r=\"4\" fill=\"#6cc9ff\"/>\n    <path d=\"M0 0 L30 6 L30 22\" stroke=\"#6cc9ff\" stroke-width=\"2.5\" fill=\"none\"/>\n    <circle cx=\"30\" cy=\"24\" r=\"4\" fill=\"#6cc9ff\"/>\n  </g>\n  <rect x=\"68\" y=\"130\" width=\"24\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">清交、台大、政大、成大、北醫、陽明……<br>一起陪你做科系探索 🚀</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"主持人自介","html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>今天陪你的人</div>\n      <div class=\"art-hero\" data-seq=\"0\"><svg viewBox=\"0 0 160 180\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"suit\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"visor\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#3fe0d0\"/><stop offset=\"70%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <ellipse cx=\"80\" cy=\"166\" rx=\"40\" ry=\"8\" fill=\"#000\" opacity=\".2\"/>\n  <rect x=\"48\" y=\"92\" width=\"64\" height=\"62\" rx=\"26\" fill=\"url(#suit)\"/>\n  <rect x=\"30\" y=\"100\" width=\"22\" height=\"46\" rx=\"11\" fill=\"url(#suit)\"/><rect x=\"108\" y=\"100\" width=\"22\" height=\"46\" rx=\"11\" fill=\"url(#suit)\"/>\n  <circle cx=\"38\" cy=\"146\" r=\"13\" fill=\"#FFD63B\"/>\n  <rect x=\"56\" y=\"150\" width=\"20\" height=\"26\" rx=\"8\" fill=\"url(#suit)\"/><rect x=\"84\" y=\"150\" width=\"20\" height=\"26\" rx=\"8\" fill=\"url(#suit)\"/>\n  <circle cx=\"80\" cy=\"58\" r=\"42\" fill=\"url(#suit)\"/><circle cx=\"80\" cy=\"58\" r=\"30\" fill=\"url(#visor)\"/>\n  <ellipse cx=\"68\" cy=\"48\" rx=\"9\" ry=\"12\" fill=\"#fff\" opacity=\".5\"/>\n  <rect x=\"70\" y=\"108\" width=\"20\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/><circle cx=\"80\" cy=\"124\" r=\"4\" fill=\"#FFD63B\"/>\n</svg></div>\n      <h2 class=\"h-mega\" data-seq=\"0\">我是今天的<span class=\"hl\">主持人</span></h2>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"主持人 · 3 個 Hashtag","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>認識我</div>\n      <h2 class=\"h-mega\" data-seq=\"0\">用 <span class=\"hl\">3 個 Hashtag</span><br>認識我</h2>\n      <div class=\"deco-row\" data-seq=\"0\">\n        <div class=\"deco\"><svg viewBox=\"0 0 120 120\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"pp\" cx=\"38%\" cy=\"35%\" r=\"75%\"><stop offset=\"0%\" stop-color=\"#a48bff\"/><stop offset=\"100%\" stop-color=\"#4a2fb0\"/></radialGradient></defs>\n  <circle cx=\"60\" cy=\"60\" r=\"44\" fill=\"url(#pp)\"/><circle cx=\"44\" cy=\"46\" r=\"9\" fill=\"#fff\" opacity=\".3\"/>\n  <circle cx=\"74\" cy=\"72\" r=\"6\" fill=\"#2e1a78\" opacity=\".5\"/><circle cx=\"56\" cy=\"80\" r=\"4\" fill=\"#2e1a78\" opacity=\".4\"/>\n</svg></div>\n        <div class=\"deco\"><svg viewBox=\"0 0 160 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <path d=\"M80 12 L96 62 L148 64 L106 94 L122 144 L80 112 L38 144 L54 94 L12 64 L64 62Z\" fill=\"#FFD63B\"/>\n  <path d=\"M80 42 L90 68 L114 70 L94 86 L102 112 L80 96 L58 112 L66 86 L46 70 L70 68Z\" fill=\"#ff8c3b\"/>\n</svg></div>\n        <div class=\"deco\"><svg viewBox=\"0 0 120 120\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"pa\" cx=\"38%\" cy=\"35%\" r=\"75%\"><stop offset=\"0%\" stop-color=\"#8df3e8\"/><stop offset=\"100%\" stop-color=\"#1d9d90\"/></radialGradient></defs>\n  <circle cx=\"60\" cy=\"60\" r=\"42\" fill=\"url(#pa)\"/><circle cx=\"46\" cy=\"48\" r=\"8\" fill=\"#fff\" opacity=\".35\"/>\n  <path d=\"M40 72 Q60 66 82 74\" stroke=\"#0e6e63\" stroke-width=\"4\" fill=\"none\" opacity=\".5\"/>\n</svg></div>\n        <div class=\"deco\"><svg viewBox=\"0 0 140 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"rk\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#cdd6f5\"/></linearGradient>\n    <linearGradient id=\"fl\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"60%\" stop-color=\"#ff8c3b\"/><stop offset=\"100%\" stop-color=\"#ff5b5b\"/></linearGradient>\n  </defs>\n  <path d=\"M70 8 C100 36 104 86 100 132 L40 132 C36 86 40 36 70 8Z\" fill=\"url(#rk)\"/>\n  <circle cx=\"70\" cy=\"64\" r=\"17\" fill=\"#161e4a\"/><circle cx=\"70\" cy=\"64\" r=\"11\" fill=\"#3fe0d0\" opacity=\".85\"/>\n  <path d=\"M40 110 L16 150 L40 138Z\" fill=\"#ff6b6b\"/><path d=\"M100 110 L124 150 L100 138Z\" fill=\"#ff6b6b\"/>\n  <rect x=\"40\" y=\"132\" width=\"60\" height=\"14\" rx=\"4\" fill=\"#7c5cff\"/>\n  <path d=\"M52 146 Q70 200 88 146 Q70 168 52 146Z\" fill=\"url(#fl)\"><animate attributeName=\"opacity\" values=\"1;.5;1\" dur=\"0.5s\" repeatCount=\"indefinite\"/></path>\n</svg></div>\n        <div class=\"deco\"><svg viewBox=\"0 0 120 120\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"pr\" cx=\"38%\" cy=\"35%\" r=\"75%\"><stop offset=\"0%\" stop-color=\"#ff9d8a\"/><stop offset=\"100%\" stop-color=\"#b13a2c\"/></radialGradient></defs>\n  <circle cx=\"60\" cy=\"60\" r=\"40\" fill=\"url(#pr)\"/><circle cx=\"46\" cy=\"48\" r=\"7\" fill=\"#fff\" opacity=\".3\"/>\n  <ellipse cx=\"68\" cy=\"70\" rx=\"14\" ry=\"6\" fill=\"#7a2418\" opacity=\".5\"/>\n</svg></div>\n      </div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"主持人 · 我的探索故事","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>開始前，和你聊聊</div>\n      <div class=\"art-lg\" data-seq=\"0\"><svg viewBox=\"0 0 180 180\" xmlns=\"http://www.w3.org/2000/svg\">\n  <circle cx=\"90\" cy=\"90\" r=\"72\" fill=\"#161e4a\" stroke=\"#FFD63B\" stroke-width=\"5\"/>\n  <circle cx=\"90\" cy=\"90\" r=\"72\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"1.5\" opacity=\".4\"/>\n  <circle cx=\"90\" cy=\"90\" r=\"60\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"1\" opacity=\".25\" stroke-dasharray=\"3 6\"/>\n  <path d=\"M90 90 L118 62 L90 100Z\" fill=\"#ff6b6b\"/><path d=\"M90 90 L62 118 L90 80Z\" fill=\"#cdd6f5\"/>\n  <circle cx=\"90\" cy=\"90\" r=\"7\" fill=\"#FFD63B\"/>\n  <text x=\"90\" y=\"34\" text-anchor=\"middle\" fill=\"#FFD63B\" font-size=\"14\" font-weight=\"800\" font-family=\"Outfit\">N</text>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">開始前和你聊聊，<br>為什麼<span class=\"hl\">科系探索</span>這麼重要</h2>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"如何享受今天","html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>開始前，想跟你分享</div>\n      <div class=\"art-lg\" data-seq=\"0\"><svg viewBox=\"0 0 200 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><linearGradient id=\"ts\" x1=\"0\" y1=\"0\" x2=\"1\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#c98e1a\"/></linearGradient></defs>\n  <rect x=\"92\" y=\"118\" width=\"12\" height=\"56\" fill=\"#cdd6f5\"/>\n  <path d=\"M66 174 L130 174 L116 190 L80 190Z\" fill=\"#7c5cff\"/>\n  <g transform=\"rotate(-32 110 90)\">\n    <rect x=\"48\" y=\"74\" width=\"120\" height=\"30\" rx=\"15\" fill=\"url(#ts)\"/>\n    <rect x=\"158\" y=\"69\" width=\"24\" height=\"40\" rx=\"7\" fill=\"#3fe0d0\"/>\n    <circle cx=\"56\" cy=\"89\" r=\"10\" fill=\"#161e4a\"/>\n  </g>\n  <g fill=\"#FFD63B\"><circle cx=\"40\" cy=\"36\" r=\"3.5\"/><circle cx=\"64\" cy=\"22\" r=\"2.5\"/><circle cx=\"28\" cy=\"58\" r=\"2.5\"/><circle cx=\"160\" cy=\"30\" r=\"3\"/></g>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">如何讓自己<br>好好<span class=\"hl\">享受</span>今天？</h2>\n      <p class=\"lead\" data-seq=\"1\">過往發現，做到這 <span class=\"hl\">3 件事</span>，<br>今天你一定會玩得很過癮 👇</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"三把鑰匙 · 總覽","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>享受今天的三把鑰匙</div>\n      <div class=\"op-cards c3 big-cards\" data-seq=\"1\">\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 160 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <path d=\"M80 12 L96 62 L148 64 L106 94 L122 144 L80 112 L38 144 L54 94 L12 64 L64 62Z\" fill=\"#FFD63B\"/>\n  <path d=\"M80 42 L90 68 L114 70 L94 86 L102 112 L80 96 L58 112 L66 86 L46 70 L70 68Z\" fill=\"#ff8c3b\"/>\n</svg></div><span class=\"num\">KEY 01</span><h3>積極投入</h3></div>\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 140 190\" xmlns=\"http://www.w3.org/2000/svg\">\n  <rect x=\"50\" y=\"20\" width=\"40\" height=\"80\" rx=\"20\" fill=\"#FFD63B\"/>\n  <path d=\"M32 82 a38 38 0 0 0 76 0\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"6\"/>\n  <rect x=\"66\" y=\"118\" width=\"8\" height=\"30\" fill=\"#cdd6f5\"/>\n  <rect x=\"46\" y=\"148\" width=\"48\" height=\"10\" rx=\"5\" fill=\"#7c5cff\"/>\n  <g stroke=\"#fff\" stroke-width=\"3.5\" opacity=\".5\"><line x1=\"60\" y1=\"44\" x2=\"80\" y2=\"44\"/><line x1=\"60\" y1=\"58\" x2=\"80\" y2=\"58\"/></g>\n</svg></div><span class=\"num\">KEY 02</span><h3>勇於發言</h3></div>\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 160 180\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"bl\" cx=\"50%\" cy=\"40%\" r=\"60%\"><stop offset=\"0%\" stop-color=\"#fff6cc\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient></defs>\n  <circle cx=\"80\" cy=\"74\" r=\"50\" fill=\"url(#bl)\"/>\n  <rect x=\"60\" y=\"120\" width=\"40\" height=\"12\" rx=\"4\" fill=\"#7c5cff\"/><rect x=\"64\" y=\"136\" width=\"32\" height=\"10\" rx=\"4\" fill=\"#7c5cff\"/><rect x=\"68\" y=\"150\" width=\"24\" height=\"10\" rx=\"5\" fill=\"#7c5cff\"/>\n  <path d=\"M80 54 L80 104 M62 74 L98 74\" stroke=\"#c98e1a\" stroke-width=\"3.5\" opacity=\".5\"/>\n  <g stroke=\"#3fe0d0\" stroke-width=\"5\" stroke-linecap=\"round\"><path d=\"M20 74 L6 74\"/><path d=\"M154 74 L140 74\"/><path d=\"M36 30 L26 20\"/><path d=\"M124 30 L134 20\"/></g>\n</svg></div><span class=\"num\">KEY 03</span><h3>主動解決</h3></div>\n      </div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"① 積極投入","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split\" data-seq=\"0\">\n        <div class=\"split-l\">\n          <div class=\"eyebrow\"><span class=\"dot\"></span>KEY 01</div>\n          <h2 class=\"h-mega\" style=\"text-align:left\"><span class=\"hl\">積極投入</span></h2>\n        </div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 460 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"ac-suit\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#fff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"ac-visor\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#3fe0d0\"/><stop offset=\"70%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n    <radialGradient id=\"ac-star\" cx=\"50%\" cy=\"45%\" r=\"60%\"><stop offset=\"0%\" stop-color=\"#fff6cc\"/><stop offset=\"60%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#ff8c3b\"/></radialGradient>\n  </defs>\n  <!-- 上升能量線 -->\n  <g stroke=\"#FFD63B\" stroke-width=\"5\" stroke-linecap=\"round\" opacity=\".6\" fill=\"none\">\n    <path d=\"M120 300 L120 250\"><animate attributeName=\"opacity\" values=\".2;.8;.2\" dur=\"1.6s\" repeatCount=\"indefinite\"/></path>\n    <path d=\"M330 290 L330 240\"><animate attributeName=\"opacity\" values=\".6;.2;.6\" dur=\"1.9s\" repeatCount=\"indefinite\"/></path>\n    <path d=\"M80 250 L80 215\" opacity=\".4\"/><path d=\"M380 260 L380 225\" opacity=\".4\"/>\n  </g>\n  <!-- 太空人（舉手） -->\n  <g transform=\"translate(230 230)\">\n    <ellipse cx=\"0\" cy=\"120\" rx=\"56\" ry=\"10\" fill=\"#000\" opacity=\".18\"/>\n    <rect x=\"-34\" y=\"20\" width=\"68\" height=\"64\" rx=\"28\" fill=\"url(#ac-suit)\"/>\n    <!-- 舉起的右臂 -->\n    <g transform=\"rotate(-38 28 30)\"><rect x=\"22\" y=\"-16\" width=\"22\" height=\"50\" rx=\"11\" fill=\"url(#ac-suit)\"/><circle cx=\"33\" cy=\"-16\" r=\"13\" fill=\"#FFD63B\"/></g>\n    <rect x=\"-56\" y=\"28\" width=\"22\" height=\"48\" rx=\"11\" fill=\"url(#ac-suit)\"/><circle cx=\"-45\" cy=\"76\" r=\"12\" fill=\"#FFD63B\"/>\n    <rect x=\"-26\" y=\"80\" width=\"22\" height=\"28\" rx=\"9\" fill=\"url(#ac-suit)\"/><rect x=\"4\" y=\"80\" width=\"22\" height=\"28\" rx=\"9\" fill=\"url(#ac-suit)\"/>\n    <circle cx=\"0\" cy=\"-22\" r=\"44\" fill=\"url(#ac-suit)\"/><circle cx=\"0\" cy=\"-22\" r=\"31\" fill=\"url(#ac-visor)\"/>\n    <ellipse cx=\"-12\" cy=\"-32\" rx=\"8\" ry=\"11\" fill=\"#fff\" opacity=\".5\"/>\n    <rect x=\"-10\" y=\"34\" width=\"20\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n  </g>\n  <!-- 大星星（右上） -->\n  <g transform=\"translate(360 90)\">\n    <path d=\"M0 -42 L12 -12 L44 -10 L18 10 L28 42 L0 22 L-28 42 L-18 10 L-44 -10 L-12 -12Z\" fill=\"url(#ac-star)\"/>\n  </g>\n  <g fill=\"#FFD63B\"><circle cx=\"70\" cy=\"80\" r=\"3\"/><circle cx=\"410\" cy=\"180\" r=\"2.5\"/><circle cx=\"60\" cy=\"160\" r=\"2\"/></g>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">探索就探索、討論就討論、撰寫就撰寫，<br>該玩的時候就好好玩！</p>\n      <div class=\"action-hint\" data-seq=\"2\"><span class=\"ah-emoji\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"eh\" cx=\"40%\" cy=\"35%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ff9ec7\"/><stop offset=\"100%\" stop-color=\"#ff4d94\"/></radialGradient></defs><path d=\"M50 84 C16 60 12 38 26 26 C38 16 50 24 50 36 C50 24 62 16 74 26 C88 38 84 60 50 84Z\" fill=\"url(#eh)\"/><path d=\"M70 20 l3 7 l7 3 l-7 3 l-3 7 l-3 -7 l-7 -3 l7 -3Z\" fill=\"#fff\"/><circle cx=\"34\" cy=\"34\" r=\"4\" fill=\"#fff\" opacity=\".7\"/></svg></span>願意積極投入的同學，幫我按個愛心 ❤️</div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"② 勇於發言","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split\" data-seq=\"0\">\n        <div class=\"split-l\">\n          <div class=\"eyebrow\"><span class=\"dot\"></span>KEY 02</div>\n          <h2 class=\"h-mega\" style=\"text-align:left\"><span class=\"hl\">勇於發言</span></h2>\n        </div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 460 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"sp-suit\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#fff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"sp-visor\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#3fe0d0\"/><stop offset=\"70%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <!-- 太空人 -->\n  <g transform=\"translate(170 220)\">\n    <ellipse cx=\"0\" cy=\"130\" rx=\"54\" ry=\"10\" fill=\"#000\" opacity=\".18\"/>\n    <rect x=\"-32\" y=\"30\" width=\"64\" height=\"62\" rx=\"26\" fill=\"url(#sp-suit)\"/>\n    <rect x=\"-52\" y=\"38\" width=\"20\" height=\"46\" rx=\"10\" fill=\"url(#sp-suit)\"/>\n    <!-- 持麥的手 -->\n    <g transform=\"rotate(28 40 40)\"><rect x=\"30\" y=\"20\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#sp-suit)\"/><circle cx=\"40\" cy=\"20\" r=\"12\" fill=\"#FFD63B\"/></g>\n    <rect x=\"-24\" y=\"88\" width=\"20\" height=\"28\" rx=\"9\" fill=\"url(#sp-suit)\"/><rect x=\"4\" y=\"88\" width=\"20\" height=\"28\" rx=\"9\" fill=\"url(#sp-suit)\"/>\n    <circle cx=\"0\" cy=\"-14\" r=\"42\" fill=\"url(#sp-suit)\"/><circle cx=\"0\" cy=\"-14\" r=\"30\" fill=\"url(#sp-visor)\"/>\n    <ellipse cx=\"-11\" cy=\"-24\" rx=\"8\" ry=\"10\" fill=\"#fff\" opacity=\".5\"/>\n    <rect x=\"-10\" y=\"42\" width=\"20\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n  </g>\n  <!-- 麥克風 -->\n  <g transform=\"translate(238 188) rotate(18)\">\n    <rect x=\"-16\" y=\"-30\" width=\"32\" height=\"60\" rx=\"16\" fill=\"#FFD63B\"/>\n    <path d=\"M-26 18 a26 26 0 0 0 52 0\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"5\"/>\n    <rect x=\"-4\" y=\"44\" width=\"8\" height=\"26\" fill=\"#cdd6f5\"/>\n    <g stroke=\"#fff\" stroke-width=\"3\" opacity=\".5\"><line x1=\"-9\" y1=\"-14\" x2=\"9\" y2=\"-14\"/><line x1=\"-9\" y1=\"-2\" x2=\"9\" y2=\"-2\"/></g>\n  </g>\n  <!-- 聊天泡泡 -->\n  <g transform=\"translate(340 110)\">\n    <rect x=\"-50\" y=\"-34\" width=\"100\" height=\"64\" rx=\"20\" fill=\"#7c5cff\"/>\n    <path d=\"M-20 28 L-30 52 L4 28Z\" fill=\"#7c5cff\"/>\n    <circle cx=\"-22\" cy=\"-2\" r=\"7\" fill=\"#fff\"/><circle cx=\"0\" cy=\"-2\" r=\"7\" fill=\"#fff\"/><circle cx=\"22\" cy=\"-2\" r=\"7\" fill=\"#fff\"/>\n  </g>\n  <g fill=\"#FFD63B\"><circle cx=\"400\" cy=\"180\" r=\"2.5\"/><circle cx=\"80\" cy=\"100\" r=\"2.5\"/><circle cx=\"410\" cy=\"60\" r=\"2\"/></g>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">不逼你開口，但盡量在<span class=\"hl-aqua\">聊天室</span>打出想法 —<br>釐清自己，也讓我能好好陪你聊。</p>\n      <div class=\"action-hint\" data-seq=\"2\"><span class=\"ah-emoji\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"ej\" cx=\"40%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ffe98a\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient></defs><circle cx=\"50\" cy=\"50\" r=\"40\" fill=\"url(#ej)\"/><path d=\"M28 42 Q36 34 46 42\" stroke=\"#5a3a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M54 42 Q64 34 72 42\" stroke=\"#5a3a00\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M32 58 Q50 80 68 58 Q50 70 32 58Z\" fill=\"#7a4a00\"/><path d=\"M34 60 Q50 74 66 60\" fill=\"#ff5b5b\"/><path d=\"M26 50 Q20 58 24 64\" stroke=\"#6cc9ff\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/><path d=\"M74 50 Q80 58 76 64\" stroke=\"#6cc9ff\" stroke-width=\"4\" fill=\"none\" stroke-linecap=\"round\"/></svg></span>願意把想法打出來的同學，幫我按個笑臉 😂</div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"③ 主動解決","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split\" data-seq=\"0\">\n        <div class=\"split-l\">\n          <div class=\"eyebrow\"><span class=\"dot\"></span>KEY 03</div>\n          <h2 class=\"h-mega\" style=\"text-align:left\"><span class=\"hl\">主動解決</span></h2>\n        </div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 460 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"so-suit\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#fff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"so-visor\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#3fe0d0\"/><stop offset=\"70%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n    <radialGradient id=\"so-bulb\" cx=\"50%\" cy=\"40%\" r=\"60%\"><stop offset=\"0%\" stop-color=\"#fff6cc\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient>\n  </defs>\n  <!-- 太空人 -->\n  <g transform=\"translate(160 225)\">\n    <ellipse cx=\"0\" cy=\"128\" rx=\"54\" ry=\"10\" fill=\"#000\" opacity=\".18\"/>\n    <rect x=\"-32\" y=\"28\" width=\"64\" height=\"62\" rx=\"26\" fill=\"url(#so-suit)\"/>\n    <rect x=\"-52\" y=\"36\" width=\"20\" height=\"46\" rx=\"10\" fill=\"url(#so-suit)\"/>\n    <!-- 指向燈泡的手 -->\n    <g transform=\"rotate(-30 36 36)\"><rect x=\"28\" y=\"14\" width=\"20\" height=\"46\" rx=\"10\" fill=\"url(#so-suit)\"/><circle cx=\"38\" cy=\"14\" r=\"12\" fill=\"#FFD63B\"/></g>\n    <rect x=\"-24\" y=\"86\" width=\"20\" height=\"28\" rx=\"9\" fill=\"url(#so-suit)\"/><rect x=\"4\" y=\"86\" width=\"20\" height=\"28\" rx=\"9\" fill=\"url(#so-suit)\"/>\n    <circle cx=\"0\" cy=\"-16\" r=\"42\" fill=\"url(#so-suit)\"/><circle cx=\"0\" cy=\"-16\" r=\"30\" fill=\"url(#so-visor)\"/>\n    <ellipse cx=\"-11\" cy=\"-26\" rx=\"8\" ry=\"10\" fill=\"#fff\" opacity=\".5\"/>\n    <rect x=\"-10\" y=\"40\" width=\"20\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n  </g>\n  <!-- 燈泡（發光） -->\n  <g transform=\"translate(310 130)\">\n    <circle cx=\"0\" cy=\"0\" r=\"46\" fill=\"url(#so-bulb)\"/>\n    <rect x=\"-18\" y=\"42\" width=\"36\" height=\"11\" rx=\"4\" fill=\"#7c5cff\"/><rect x=\"-14\" y=\"56\" width=\"28\" height=\"9\" rx=\"4\" fill=\"#7c5cff\"/>\n    <g stroke=\"#3fe0d0\" stroke-width=\"5\" stroke-linecap=\"round\"><path d=\"M-58 0 L-72 0\"/><path d=\"M58 0 L72 0\"/><path d=\"M-42 -42 L-52 -52\"/><path d=\"M42 -42 L52 -52\"/><path d=\"M0 -58 L0 -72\"/></g>\n  </g>\n  <!-- 齒輪 -->\n  <g transform=\"translate(370 240)\" fill=\"#3fe0d0\">\n    <circle cx=\"0\" cy=\"0\" r=\"20\"/><circle cx=\"0\" cy=\"0\" r=\"9\" fill=\"#0d1330\"/>\n    <g><rect x=\"-4\" y=\"-28\" width=\"8\" height=\"10\"/><rect x=\"-4\" y=\"18\" width=\"8\" height=\"10\"/><rect x=\"-28\" y=\"-4\" width=\"10\" height=\"8\"/><rect x=\"18\" y=\"-4\" width=\"10\" height=\"8\"/></g>\n  </g>\n  <g fill=\"#FFD63B\"><circle cx=\"80\" cy=\"100\" r=\"2.5\"/><circle cx=\"410\" cy=\"170\" r=\"2.5\"/><circle cx=\"400\" cy=\"80\" r=\"2\"/></g>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">遇到問題別緊張 — 講義和教學影片都有，<br>可以先自己試著解決。</p>\n      <div class=\"action-hint\" data-seq=\"2\"><span class=\"ah-emoji\"><svg viewBox=\"0 0 100 100\"><defs><linearGradient id=\"et\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#f0b429\"/></linearGradient></defs><rect x=\"20\" y=\"46\" width=\"20\" height=\"36\" rx=\"6\" fill=\"#e89a2c\"/><path d=\"M42 48 C42 38 52 34 52 22 C52 14 62 14 62 24 C62 32 58 40 58 44 L74 44 C82 44 84 52 80 64 C78 76 74 82 64 82 L46 82 C42 82 42 78 42 74Z\" fill=\"url(#et)\"/></svg></span>沒問題、願意主動解決的同學，幫我按個讚 👍</div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"真的有問題怎麼辦","html":"\n    <div class=\"scene-inner\">\n      <div class=\"art-hero\" data-seq=\"0\"><svg viewBox=\"0 0 160 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <rect x=\"66\" y=\"86\" width=\"28\" height=\"56\" rx=\"8\" fill=\"#cdd6f5\"/>\n  <circle cx=\"80\" cy=\"68\" r=\"28\" fill=\"#ff6b6b\"/>\n  <text x=\"80\" y=\"79\" text-anchor=\"middle\" fill=\"#fff\" font-size=\"34\" font-weight=\"900\" font-family=\"Outfit\">!</text>\n  <g stroke=\"#FFD63B\" stroke-width=\"5\" fill=\"none\" stroke-linecap=\"round\" opacity=\".8\">\n    <path d=\"M36 48 Q26 68 36 88\"><animate attributeName=\"opacity\" values=\".8;.3;.8\" dur=\"1.5s\" repeatCount=\"indefinite\"/></path>\n    <path d=\"M124 48 Q134 68 124 88\"><animate attributeName=\"opacity\" values=\".8;.3;.8\" dur=\"1.5s\" repeatCount=\"indefinite\"/></path>\n    <path d=\"M22 36 Q8 68 22 100\"/><path d=\"M138 36 Q152 68 138 100\"/>\n  </g>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">真的卡住了？<br><span class=\"hl\">私訊學長姐</span>就對了</h2>\n      <p class=\"lead\" data-seq=\"1\">直接私訊學長姐的 Line，<br>我們會在旁邊協助你解決 💪</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"三把鑰匙 · 你選哪個","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>換你了</div>\n      <h2 class=\"h-big choose-h\" data-seq=\"0\">這三件事，哪一件你<span class=\"hl\">最能辦到</span>？</h2>\n      <div class=\"op-cards c3 big-cards\" data-seq=\"1\">\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 160 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <path d=\"M80 12 L96 62 L148 64 L106 94 L122 144 L80 112 L38 144 L54 94 L12 64 L64 62Z\" fill=\"#FFD63B\"/>\n  <path d=\"M80 42 L90 68 L114 70 L94 86 L102 112 L80 96 L58 112 L66 86 L46 70 L70 68Z\" fill=\"#ff8c3b\"/>\n</svg></div><h3>積極投入</h3></div>\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 140 190\" xmlns=\"http://www.w3.org/2000/svg\">\n  <rect x=\"50\" y=\"20\" width=\"40\" height=\"80\" rx=\"20\" fill=\"#FFD63B\"/>\n  <path d=\"M32 82 a38 38 0 0 0 76 0\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"6\"/>\n  <rect x=\"66\" y=\"118\" width=\"8\" height=\"30\" fill=\"#cdd6f5\"/>\n  <rect x=\"46\" y=\"148\" width=\"48\" height=\"10\" rx=\"5\" fill=\"#7c5cff\"/>\n  <g stroke=\"#fff\" stroke-width=\"3.5\" opacity=\".5\"><line x1=\"60\" y1=\"44\" x2=\"80\" y2=\"44\"/><line x1=\"60\" y1=\"58\" x2=\"80\" y2=\"58\"/></g>\n</svg></div><h3>勇於發言</h3></div>\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 160 180\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"bl\" cx=\"50%\" cy=\"40%\" r=\"60%\"><stop offset=\"0%\" stop-color=\"#fff6cc\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></radialGradient></defs>\n  <circle cx=\"80\" cy=\"74\" r=\"50\" fill=\"url(#bl)\"/>\n  <rect x=\"60\" y=\"120\" width=\"40\" height=\"12\" rx=\"4\" fill=\"#7c5cff\"/><rect x=\"64\" y=\"136\" width=\"32\" height=\"10\" rx=\"4\" fill=\"#7c5cff\"/><rect x=\"68\" y=\"150\" width=\"24\" height=\"10\" rx=\"5\" fill=\"#7c5cff\"/>\n  <path d=\"M80 54 L80 104 M62 74 L98 74\" stroke=\"#c98e1a\" stroke-width=\"3.5\" opacity=\".5\"/>\n  <g stroke=\"#3fe0d0\" stroke-width=\"5\" stroke-linecap=\"round\"><path d=\"M20 74 L6 74\"/><path d=\"M154 74 L140 74\"/><path d=\"M36 30 L26 20\"/><path d=\"M124 30 L134 20\"/></g>\n</svg></div><h3>主動解決</h3></div>\n      </div>\n      <div class=\"action-hint\" data-seq=\"2\">😆 用表情符號告訴我，你最能辦到哪一件</div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"對標期待 · 開場","html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>開始之前</div>\n      <div class=\"art-hero\" data-seq=\"1\"><svg viewBox=\"0 0 180 180\" xmlns=\"http://www.w3.org/2000/svg\">\n  <circle cx=\"86\" cy=\"94\" r=\"74\" fill=\"none\" stroke=\"#7c5cff\" stroke-width=\"10\"/>\n  <circle cx=\"86\" cy=\"94\" r=\"50\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"10\"/>\n  <circle cx=\"86\" cy=\"94\" r=\"26\" fill=\"#FFD63B\"/>\n  <path d=\"M86 94 L166 30\" stroke=\"#ff6b6b\" stroke-width=\"8\" stroke-linecap=\"round\"/>\n  <path d=\"M156 20 L172 26 L166 42Z\" fill=\"#ff6b6b\"/>\n</svg></div>\n      <h2 class=\"h-mega\" data-seq=\"1\">先跟你<span class=\"hl\">對標</span><br>今天的期待</h2>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"不會學會某個技能","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split center-split\" data-seq=\"0\">\n        <div class=\"split-l\"><h2 class=\"h-big split-h\">你今天<br><span class=\"hl-coral\">不會</span>學會<br>某個技能</h2></div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 120 120\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"pp\" cx=\"38%\" cy=\"35%\" r=\"75%\"><stop offset=\"0%\" stop-color=\"#a48bff\"/><stop offset=\"100%\" stop-color=\"#4a2fb0\"/></radialGradient></defs>\n  <circle cx=\"60\" cy=\"60\" r=\"44\" fill=\"url(#pp)\"/><circle cx=\"44\" cy=\"46\" r=\"9\" fill=\"#fff\" opacity=\".3\"/>\n  <circle cx=\"74\" cy=\"72\" r=\"6\" fill=\"#2e1a78\" opacity=\".5\"/><circle cx=\"56\" cy=\"80\" r=\"4\" fill=\"#2e1a78\" opacity=\".4\"/>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">畢竟一天的時間，這不現實 🙂</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"不會完成全部內容","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split center-split\" data-seq=\"0\">\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 120 120\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"pa\" cx=\"38%\" cy=\"35%\" r=\"75%\"><stop offset=\"0%\" stop-color=\"#8df3e8\"/><stop offset=\"100%\" stop-color=\"#1d9d90\"/></radialGradient></defs>\n  <circle cx=\"60\" cy=\"60\" r=\"42\" fill=\"url(#pa)\"/><circle cx=\"46\" cy=\"48\" r=\"8\" fill=\"#fff\" opacity=\".35\"/>\n  <path d=\"M40 72 Q60 66 82 74\" stroke=\"#0e6e63\" stroke-width=\"4\" fill=\"none\" opacity=\".5\"/>\n</svg></div>\n        <div class=\"split-l\"><h2 class=\"h-big split-h\">我們也<br><span class=\"hl-coral\">不會逼你</span><br>完成全部內容</h2></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">節奏跟著你走，不用焦慮。</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"100% 陪你探索","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"split center-split\" data-seq=\"0\">\n        <div class=\"split-l\"><h2 class=\"h-big split-h\">但只要你<br>想探索 ——<br>我會用 <span class=\"hl\">100%</span><br>力氣陪你！</h2></div>\n        <div class=\"split-r art-scene\"><svg viewBox=\"0 0 140 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"rk\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#cdd6f5\"/></linearGradient>\n    <linearGradient id=\"fl\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"60%\" stop-color=\"#ff8c3b\"/><stop offset=\"100%\" stop-color=\"#ff5b5b\"/></linearGradient>\n  </defs>\n  <path d=\"M70 8 C100 36 104 86 100 132 L40 132 C36 86 40 36 70 8Z\" fill=\"url(#rk)\"/>\n  <circle cx=\"70\" cy=\"64\" r=\"17\" fill=\"#161e4a\"/><circle cx=\"70\" cy=\"64\" r=\"11\" fill=\"#3fe0d0\" opacity=\".85\"/>\n  <path d=\"M40 110 L16 150 L40 138Z\" fill=\"#ff6b6b\"/><path d=\"M100 110 L124 150 L100 138Z\" fill=\"#ff6b6b\"/>\n  <rect x=\"40\" y=\"132\" width=\"60\" height=\"14\" rx=\"4\" fill=\"#7c5cff\"/>\n  <path d=\"M52 146 Q70 200 88 146 Q70 168 52 146Z\" fill=\"url(#fl)\"><animate attributeName=\"opacity\" values=\"1;.5;1\" dur=\"0.5s\" repeatCount=\"indefinite\"/></path>\n</svg></div>\n      </div>\n      <p class=\"lead\" data-seq=\"1\">這趟科系探索，我們一起飛 🚀</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"你今天的態度","timer":90,"html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>你今天會用什麼樣的態度來面對呢？</div>\n      <h2 class=\"h-big\" data-seq=\"1\">「我會用 <span class=\"hl\">___</span> 的態度，<br>來 <span class=\"hl\">___</span>」</h2>\n      <p class=\"lead\" data-seq=\"2\">例：我會用<span class=\"hl-aqua\">積極</span>的態度，<br>來<span class=\"hl-aqua\">釐清自己喜不喜歡這個科系</span>。</p>\n      \n    </div>"},
{"ch":"開場暖身","type":"raw","m":"課前暖身複習","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"art-lg\" data-seq=\"0\"><svg viewBox=\"0 0 180 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <path d=\"M90 34 C70 22 38 22 22 30 L22 128 C38 120 70 120 90 132Z\" fill=\"#7c5cff\"/>\n  <path d=\"M90 34 C110 22 142 22 158 30 L158 128 C142 120 110 120 90 132Z\" fill=\"#3fe0d0\"/>\n  <path d=\"M90 34 L90 132\" stroke=\"#161e4a\" stroke-width=\"3.5\"/>\n  <g stroke=\"#fff\" stroke-width=\"3\" opacity=\".6\"><line x1=\"36\" y1=\"54\" x2=\"74\" y2=\"58\"/><line x1=\"36\" y1=\"72\" x2=\"74\" y2=\"76\"/><line x1=\"36\" y1=\"90\" x2=\"68\" y2=\"94\"/><line x1=\"106\" y1=\"58\" x2=\"144\" y2=\"54\"/><line x1=\"106\" y1=\"76\" x2=\"144\" y2=\"72\"/><line x1=\"106\" y1=\"94\" x2=\"138\" y2=\"90\"/></g>\n  <circle cx=\"90\" cy=\"24\" r=\"8\" fill=\"#FFD63B\"/>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">開始前，先複習<br><span class=\"hl\">課前暖身</span></h2>\n      <div class=\"check-row\" data-seq=\"1\">\n        <div class=\"check-item\"><span class=\"ci-emoji\"><svg viewBox=\"0 0 100 100\"><defs><linearGradient id=\"et\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#f0b429\"/></linearGradient></defs><rect x=\"20\" y=\"46\" width=\"20\" height=\"36\" rx=\"6\" fill=\"#e89a2c\"/><path d=\"M42 48 C42 38 52 34 52 22 C52 14 62 14 62 24 C62 32 58 40 58 44 L74 44 C82 44 84 52 80 64 C78 76 74 82 64 82 L46 82 C42 82 42 78 42 74Z\" fill=\"url(#et)\"/></svg></span>已複製講義 → 按讚 👍</div>\n        <div class=\"check-item\"><span class=\"ci-emoji\"><svg viewBox=\"0 0 100 100\"><defs><linearGradient id=\"etd\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#f0b429\"/><stop offset=\"100%\" stop-color=\"#d99318\"/></linearGradient></defs><rect x=\"20\" y=\"18\" width=\"20\" height=\"36\" rx=\"6\" fill=\"#e89a2c\"/><path d=\"M42 52 C42 62 52 66 52 78 C52 86 62 86 62 76 C62 68 58 60 58 56 L74 56 C82 56 84 48 80 36 C78 24 74 18 64 18 L46 18 C42 18 42 22 42 26Z\" fill=\"url(#etd)\"/></svg></span>還沒複製 → 按倒讚 👎</div>\n        <div class=\"check-item\"><span class=\"ci-emoji\"><svg viewBox=\"0 0 100 100\"><defs><radialGradient id=\"eh\" cx=\"40%\" cy=\"35%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#ff9ec7\"/><stop offset=\"100%\" stop-color=\"#ff4d94\"/></radialGradient></defs><path d=\"M50 84 C16 60 12 38 26 26 C38 16 50 24 50 36 C50 24 62 16 74 26 C88 38 84 60 50 84Z\" fill=\"url(#eh)\"/><path d=\"M70 20 l3 7 l7 3 l-7 3 l-3 7 l-3 -7 l-7 -3 l7 -3Z\" fill=\"#fff\"/><circle cx=\"34\" cy=\"34\" r=\"4\" fill=\"#fff\" opacity=\".7\"/></svg></span>完成 Notion 暖身 → 按愛心 ❤️</div>\n      </div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"MOVE 探索法 · 登場","html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>CIA 核心方法論</div>\n      <h2 class=\"h-mega\" data-seq=\"0\"><span class=\"hl\">MOVE</span> 探索法</h2>\n      <p class=\"lead\" data-seq=\"1\">開始前，先來看一下我們到底要怎麼探索吧！<br>科系範圍太廣，用四個面向看清<span class=\"hl\">整體樣貌</span>。</p>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"MOVE · 四格內容","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>點一下，逐一認識探索的四個面向</div>\n      <div class=\"move-split\">\n        <div class=\"move-list\">\n          <div class=\"move-row cell-major\" data-seq=\"1\">\n            <div class=\"mr-letter\">M</div>\n            <div class=\"mr-text\"><div class=\"mr-en\">Major</div><div class=\"mr-tc\">科系所學</div><div class=\"mr-desc\">大學四年在學什麼、會獲得哪些能力</div></div>\n          </div>\n          <div class=\"move-row cell-oper\" data-seq=\"2\">\n            <div class=\"mr-letter\">O</div>\n            <div class=\"mr-text\"><div class=\"mr-en\">Operation</div><div class=\"mr-tc\">實際操作</div><div class=\"mr-desc\">動手做常見情境，感受自己適不適合</div></div>\n          </div>\n          <div class=\"move-row cell-vision\" data-seq=\"3\">\n            <div class=\"mr-letter\">V</div>\n            <div class=\"mr-text\"><div class=\"mr-en\">Vision</div><div class=\"mr-tc\">未來發展</div><div class=\"mr-desc\">了解出路、需要的能力與工作內容</div></div>\n          </div>\n          <div class=\"move-row cell-exp\" data-seq=\"4\">\n            <div class=\"mr-letter\">E</div>\n            <div class=\"mr-text\"><div class=\"mr-en\">Experience</div><div class=\"mr-tc\">前輩分享</div><div class=\"mr-desc\">前輩點出盲點、迷思與地雷點</div></div>\n          </div>\n        </div>\n        <div class=\"move-art\">\n          <div class=\"ma-img show\" data-art=\"0\"><svg viewBox=\"0 0 180 180\" xmlns=\"http://www.w3.org/2000/svg\">\n  <circle cx=\"90\" cy=\"90\" r=\"72\" fill=\"#161e4a\" stroke=\"#FFD63B\" stroke-width=\"5\"/>\n  <circle cx=\"90\" cy=\"90\" r=\"72\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"1.5\" opacity=\".4\"/>\n  <circle cx=\"90\" cy=\"90\" r=\"60\" fill=\"none\" stroke=\"#3fe0d0\" stroke-width=\"1\" opacity=\".25\" stroke-dasharray=\"3 6\"/>\n  <path d=\"M90 90 L118 62 L90 100Z\" fill=\"#ff6b6b\"/><path d=\"M90 90 L62 118 L90 80Z\" fill=\"#cdd6f5\"/>\n  <circle cx=\"90\" cy=\"90\" r=\"7\" fill=\"#FFD63B\"/>\n  <text x=\"90\" y=\"34\" text-anchor=\"middle\" fill=\"#FFD63B\" font-size=\"14\" font-weight=\"800\" font-family=\"Outfit\">N</text>\n</svg></div>\n          <div class=\"ma-img\" data-art=\"1\"><svg viewBox=\"0 0 180 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <path d=\"M90 34 C70 22 38 22 22 30 L22 128 C38 120 70 120 90 132Z\" fill=\"#7c5cff\"/>\n  <path d=\"M90 34 C110 22 142 22 158 30 L158 128 C142 120 110 120 90 132Z\" fill=\"#3fe0d0\"/>\n  <path d=\"M90 34 L90 132\" stroke=\"#161e4a\" stroke-width=\"3.5\"/>\n  <g stroke=\"#fff\" stroke-width=\"3\" opacity=\".6\"><line x1=\"36\" y1=\"54\" x2=\"74\" y2=\"58\"/><line x1=\"36\" y1=\"72\" x2=\"74\" y2=\"76\"/><line x1=\"36\" y1=\"90\" x2=\"68\" y2=\"94\"/><line x1=\"106\" y1=\"58\" x2=\"144\" y2=\"54\"/><line x1=\"106\" y1=\"76\" x2=\"144\" y2=\"72\"/><line x1=\"106\" y1=\"94\" x2=\"138\" y2=\"90\"/></g>\n  <circle cx=\"90\" cy=\"24\" r=\"8\" fill=\"#FFD63B\"/>\n</svg></div>\n          <div class=\"ma-img\" data-art=\"2\"><svg viewBox=\"0 0 240 240\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"gr-big\" cx=\"40%\" cy=\"35%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#5ef0e0\"/><stop offset=\"100%\" stop-color=\"#2bb8a8\"/></radialGradient></defs>\n  <g transform=\"translate(95 105)\">\n    <g fill=\"url(#gr-big)\">\n      <circle r=\"52\"/>\n      <g><rect x=\"-9\" y=\"-68\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-9\" y=\"48\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-68\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/><rect x=\"48\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/></g>\n      <g transform=\"rotate(45)\"><rect x=\"-9\" y=\"-68\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-9\" y=\"48\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-68\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/><rect x=\"48\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/></g>\n    </g>\n    <circle r=\"20\" fill=\"#0d1330\"/>\n  </g>\n  <g transform=\"translate(176 158)\">\n    <g fill=\"#FFD63B\">\n      <circle r=\"34\"/>\n      <g><rect x=\"-7\" y=\"-46\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-7\" y=\"30\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-46\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/><rect x=\"30\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/></g>\n      <g transform=\"rotate(45)\"><rect x=\"-7\" y=\"-46\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-7\" y=\"30\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-46\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/><rect x=\"30\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/></g>\n    </g>\n    <circle r=\"13\" fill=\"#0d1330\"/>\n  </g>\n  <g fill=\"#fff\" opacity=\".5\"><circle cx=\"40\" cy=\"50\" r=\"2.5\"/><circle cx=\"205\" cy=\"60\" r=\"2\"/><circle cx=\"55\" cy=\"200\" r=\"2.5\"/></g>\n</svg></div>\n          <div class=\"ma-img\" data-art=\"3\"><svg viewBox=\"0 0 200 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><linearGradient id=\"ts\" x1=\"0\" y1=\"0\" x2=\"1\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#c98e1a\"/></linearGradient></defs>\n  <rect x=\"92\" y=\"118\" width=\"12\" height=\"56\" fill=\"#cdd6f5\"/>\n  <path d=\"M66 174 L130 174 L116 190 L80 190Z\" fill=\"#7c5cff\"/>\n  <g transform=\"rotate(-32 110 90)\">\n    <rect x=\"48\" y=\"74\" width=\"120\" height=\"30\" rx=\"15\" fill=\"url(#ts)\"/>\n    <rect x=\"158\" y=\"69\" width=\"24\" height=\"40\" rx=\"7\" fill=\"#3fe0d0\"/>\n    <circle cx=\"56\" cy=\"89\" r=\"10\" fill=\"#161e4a\"/>\n  </g>\n  <g fill=\"#FFD63B\"><circle cx=\"40\" cy=\"36\" r=\"3.5\"/><circle cx=\"64\" cy=\"22\" r=\"2.5\"/><circle cx=\"28\" cy=\"58\" r=\"2.5\"/><circle cx=\"160\" cy=\"30\" r=\"3\"/></g>\n</svg></div>\n          <div class=\"ma-img\" data-art=\"4\"><svg viewBox=\"0 0 200 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <rect x=\"20\" y=\"22\" width=\"130\" height=\"84\" rx=\"22\" fill=\"#FFD63B\"/>\n  <path d=\"M54 104 L46 134 L82 104Z\" fill=\"#FFD63B\"/>\n  <circle cx=\"58\" cy=\"64\" r=\"8\" fill=\"#161e4a\"/><circle cx=\"86\" cy=\"64\" r=\"8\" fill=\"#161e4a\"/><circle cx=\"114\" cy=\"64\" r=\"8\" fill=\"#161e4a\"/>\n  <rect x=\"100\" y=\"70\" width=\"80\" height=\"56\" rx=\"18\" fill=\"#7c5cff\"/>\n  <path d=\"M148 124 L156 146 L120 124Z\" fill=\"#7c5cff\"/>\n</svg></div>\n        </div>\n      </div>\n    </div>"},
{"ch":"開場暖身","type":"raw","m":"進入 · 科系所學","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>09:00 – 10:45</div>\n          <h2 class=\"h-big\">先從 <span class=\"hl\">Major</span><br>科系所學出發 🚀</h2>\n      <p class=\"lead\" data-seq=\"1\">打開你的 Notion 講義，我們的探索正式開始！</p>\n    </div>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"科系所學","title":"前導"},
{"ch":"科系所學","camp":"醫學營","p":"Part 1","m":"測驗 · 醫學系優缺點","type":"quiz","noans":true,"kicker":"科系所學 · 第 1 題","art":"pulse","q":"讀醫學系，你覺得有什麼優缺？","opts":["社會地位高、工作穩定——長輩眼中體面又穩定的工作","工時長、壓力大——醫學人手不足，背負病患生命健康的責任","社會貢獻——能幫助他人，獲得自我滿足","醫療糾紛——任何醫療行為都有風險"]},
{"ch":"科系所學","camp":"醫學營","p":"Part 1","m":"測驗 · 常見課程","type":"quiz","noans":true,"kicker":"科系所學 · 第 2 題","art":"path","q":"醫學系，有哪些常見課程？","opts":["共同課程——微積分、普通生物等基礎課程","基礎醫學——人體運作、人體與病原體的交互作用、醫學人文","臨床醫學——解剖學、解剖學實驗、小組討論（PBL）、臨床實習","國考——大五大六準備考取醫師執照"]},
{"ch":"科系所學","camp":"醫學營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img033.png","timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 1","m":"影片一","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img034.png","timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>","sub":"到 Notion 看影片一吧"},
{"ch":"科系所學","camp":"醫學營","m":"RAP 反思法","type":"frame","kicker":"停下來，帶你反思一次","art":"reflect","title":"用 <span class=\"hl\">RAP</span> 反思","steps":[{"b":"R","c":"var(--m-blue)","h":"Review｜複習","p":"複習剛剛的課程筆記——今天到底學了哪些內容？"},{"b":"A","c":"var(--m-green)","h":"Ask｜自問","p":"問問自己：這個領域，我喜歡嗎？有沒有讓我想深入的地方？"},{"b":"P","c":"var(--m-yellow)","h":"Present｜表達","p":"把想法講出來、闡述出來——等一下用感受評分表達，並寫進講義。"}],"p":"Part 1"},
{"ch":"科系所學","camp":"醫學營","p":"Part 1","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img035.png","timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"科系所學","title":"複習"},
{"ch":"科系所學","camp":"醫學營","p":"Part 2","m":"複習一下 · 醫學系優缺點","type":"frame","kicker":"複習一下 · 醫學系的優點與缺點","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"優點","p":"社會地位高：在長輩觀念裡，是個體面的工作；工作穩定：每個人都需要醫生，長期醫學人手不足；社會貢獻：能幫助他人，獲得自我滿足。"},{"b":"2","c":"var(--m-red)","h":"缺點","p":"工時長：醫學人手不足，工作時數拉長；壓力大：背負對病患生命及身體健康的責任；醫療糾紛：任何醫療行為都存在風險。"}]},
{"ch":"科系所學","camp":"醫學營","p":"Part 2","m":"想想看 · 課程規劃延伸","type":"quiz","noans":true,"kicker":"想想看 · 醫學系課程延伸","art":"path","q":"醫學系的四年課程規劃，你最想先深入了解哪個階段？","opts":["大一大二：基礎課程——微積分、普通生物、醫學人文","大三大四：解剖學與小組討論——解剖學實驗、PBL 問題導向學習","大五大六：臨床實習——問診、檢查、寫病歷、見習","國考：如何準備成為合格的醫生"]},
{"ch":"科系所學","camp":"醫學營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img036.png","timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"科系所學","camp":"醫學營","p":"Part 2","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img037.png","timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"科系所學","title":"反思"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"感受 · 醫學系優缺點","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於醫學系的優缺點，你的<span class=\"hl\">接受度</span>是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">社會地位高、工作穩定、社會貢獻｜工時長、壓力大、醫療糾紛</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"感受 · 診治流程","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於「診治流程」，你<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">檢傷分類、問診、各式檢查｜鑑別診斷、治療方案、持續追蹤</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"感受 · 醫學系課程","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於醫學系課程，你<span class=\"hl\">想深入學習</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">基礎：微積分、普通生物、醫學人文｜進階：解剖實驗、PBL 小組討論、臨床實習</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"發現反思 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img038.png","timer":180,"title":"發現反思 After<br>（自主反思）"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"科系所學","camp":"醫學營","m":"SMART 撰寫法","type":"frame","kicker":"學習歷程怎麼寫","art":"notion","title":"用 <span class=\"hl\">SMART</span> 五步，不卡關","steps":[{"b":"S","c":"var(--m-blue)","h":"Summarize｜摘要","p":"這份檔案想呈現的重點，先寫在最前面。"},{"b":"M","c":"var(--m-green)","h":"Mention｜說明","p":"說明你參加的動機，以及這個課程／活動在做什麼。"},{"b":"A","c":"var(--m-yellow)","h":"Action｜行動","p":"記錄你做了哪些具體的事、採取了哪些行動。"},{"b":"R","c":"var(--m-red)","h":"Review｜反思","p":"反思喜不喜歡、原因，以及接下來想做什麼。"},{"b":"T","c":"var(--m-blue)","h":"Template｜模板","p":"選一個模板輸出——Canva、Notion 都可以。"}],"p":"Part 3"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img039.png","timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"shot":"images/img039.png","timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"分享一個最有感的內容","type":"cover","art":"reflect","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得最有感的內容"},
{"ch":"科系所學","camp":"醫學營","p":"Part 3","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"未來發展","camp":"醫學營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"未來發展","title":"前導"},
{"ch":"未來發展","camp":"醫學營","p":"Part 1","m":"測驗 · 職涯升遷方式","type":"quiz","noans":true,"kicker":"未來發展 · 第 1 題","art":"rise","q":"醫學系的職涯升遷方式為何？","opts":["醫學生準備國考——大一至大四準備第一階段、見習醫生（Clerk）準備第二階段","PGY 不分科住院醫師——需擔任兩年，月薪約 7～10 萬","住院醫師到總醫師——依年資分 R1、R2……單週工時 72 小時","主治醫師——月收平均 18～26 萬，甚至可達 30、40 萬"]},
{"ch":"未來發展","camp":"醫學營","p":"Part 1","m":"測驗 · 醫師外的出路","type":"quiz","noans":true,"kicker":"未來發展 · 第 2 題","art":"reflect","q":"醫學系除了醫師外，還有哪些出路？","opts":["創投投資總監——洞悉產業趨勢，把基礎醫學知識變成市場上的產品","法醫——事傷鑑別、屍體相驗解剖、藥物毒品之驗定","醫師工程師／醫師科學家——國內外雙主修學程，跨足研究與科技領域","智慧醫療相關領域——結合 AI、大數據、雲端等新興科技應用"]},
{"ch":"未來發展","camp":"醫學營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img040.png","timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"未來發展","camp":"醫學營","p":"Part 1","m":"影片一 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img041.png","timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>＋寫 After","sub":"先看第一支影片，再到 Notion 補上你的 After"},
{"ch":"未來發展","camp":"醫學營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"未來發展","title":"複習"},
{"ch":"未來發展","camp":"醫學營","p":"Part 2","m":"複習一下 · 升遷、工作性質、未來趨勢","type":"frame","kicker":"複習一下 · 醫師升遷、工作性質、產業未來趨勢","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"醫師升遷與科別","p":"從醫學生準備國考、見習醫生（Clerk），到 PGY 不分科住院醫師（月薪 7～10 萬）、住院醫師（依年資 R1、R2……單週工時 72 小時）、總醫師、Fellow，最後成為主治醫師（月收平均 18～26 萬）；科別則分傳統大科、傳統小科、神經相關、儀器診療相關、醫學社會交界等。"},{"b":"2","c":"var(--m-green)","h":"工作性質與收入","p":"依病人與家屬族群、診斷治療形式（是否有 procedure）、執業機構規模、醫糾風險、自費醫療市場、執業地區而有所不同；經常性薪資（底薪）看似不高，但加上加班費、撰寫病歷費、手術費，總薪資會高於經常性薪資。"},{"b":"3","c":"var(--m-yellow)","h":"產業未來趨勢","p":"國內外雙主修學程：醫師工程師、醫師科學家、MD/PhD、MD/MB、MD/JD 等；智慧醫療＝人工智慧＋人腦智慧＋環境智慧（ABCDEF：AI、Blockchain、Cloud、Data、Edge Computing、5G），用來解決醫療現場過勞與台灣老化危機。"}]},
{"ch":"未來發展","camp":"醫學營","p":"Part 2","m":"想想看 · 醫師以外的出路延伸","type":"quiz","noans":true,"kicker":"想想看 · 延伸職缺、競賽活動、高中準備","art":"question","q":"醫學系的延伸出路，你最想先深入了解哪一塊？","opts":["創投投資總監——洞悉產業趨勢，把基礎醫學知識變成市場上的產品","法醫——事傷鑑別、屍體相驗解剖、藥物毒品之驗定","大學相關競賽——iGEM、哈佛 BIOMOD、FITI、產創中心活動","高中如何準備——生物、化學、英文、程式、實驗；醫學營、醫療展、醫學媒體"]},
{"ch":"未來發展","camp":"醫學營","p":"Part 2","m":"影片二 + 截圖 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img042.png","timer":780,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>＋寫 After","sub":"到 Notion 看影片二吧，記得把重點截圖存下來，並寫下你的 After"},
{"ch":"未來發展","camp":"醫學營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"未來發展","title":"反思"},
{"ch":"未來發展","camp":"醫學營","p":"Part 3","m":"感受 · 醫學知識","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於學習「醫學知識」的過程，你<span class=\"hl\">喜歡</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">構造英文學名、器官構造、生理機制</span>"},
{"ch":"未來發展","camp":"醫學營","p":"Part 3","m":"感受 · 解剖構造","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於了解「解剖構造」的過程，你<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">外部構造、分層構造、內部構造、器官位置</span>"},
{"ch":"未來發展","camp":"醫學營","p":"Part 3","m":"感受 · 病症報告","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於實作「病症報告」，你<span class=\"hl\">想深入學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">病因、症狀、診斷方法、治療方法</span>"},
{"ch":"未來發展","camp":"醫學營","p":"Part 3","m":"寫 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img043.png","timer":180,"title":"寫 After<br>（自主反思）"},
{"ch":"未來發展","camp":"醫學營","p":"Part 3","m":"Action 行動 + Review 反思","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img044.png","timer":900,"title":"Action <span class=\"hl\">行動</span>＋Review <span class=\"hl\">反思</span>"},
{"ch":"未來發展","m":"競賽 · Kahoot","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"吃飯前，先來一場 PK！打開 Kahoot、輸入 PIN，看看你記住多少、答對多少～","p":"Part 3","camp":"醫學營"},
{"ch":"收尾","camp":"醫學營","m":"午餐後，問學長姐 Slido","type":"frame","kicker":"吃飯後，問問學長姐","art":"question","title":"到 <span class=\"hl\">Slido</span>，用 USB 三個方向問","steps":[{"b":"U","c":"var(--m-blue)","h":"Usually｜平常","p":"學長姐平常都在忙什麼？課堂、實習、值班的日常長什麼樣？"},{"b":"S","c":"var(--m-green)","h":"Situation｜實況","p":"這個領域真實的狀況——課業、實作訓練、實際在做什麼？"},{"b":"B","c":"var(--m-yellow)","h":"Be Back｜重來","p":"如果回到高中，會給當時的自己、或給我們什麼建議？"}],"note":"其他想問的也都可以——直接把問題打在 Slido 上！（此處可放 Slido 畫面）"},
{"ch":"收尾","camp":"醫學營","m":"午餐吃什麼？","type":"cover","art":"lunch","timer":30,"title":"午餐吃什麼？","sub":"趁午休前，先在聊天室或 Slido 上分享一下你今天想吃什麼、或推薦附近好吃的店家吧！"},
{"ch":"收尾","camp":"醫學營","m":"午餐 · 1:30 回來","type":"cover","art":"lunch","music":true,"title":"午餐時間到！","sub":"記得先去吃飯、補充能量～ 下午 <span class=\"hl\">1:30 準時回來</span>！"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"寫 Slido","type":"cover","art":"question","shotPlaceholder":true,"shot":"images/img045.png","timer":180,"title":"寫 <span class=\"hl\">Slido</span>","sub":"把你的想法或問題打在 Slido 上，我們稍後一起看！"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":2,"chLabel":"實際操作","title":"前導"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"測驗 · 心臟構造","type":"quiz","noans":true,"kicker":"實際操作 · 第 1 題","art":"pulse","q":"印象中，心臟有哪些構造？","opts":["四個腔室——兩個心房、兩個心室","心臟分層構造——心內膜、心肌、心包膜","心臟內部構造——房室瓣、半月瓣、腱索、乳突狀肌","心臟傳導構造——竇房結、房室結"]},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"測驗 · 上下左右前後英文","type":"quiz","noans":true,"kicker":"實際操作 · 第 2 題","art":"path","q":"心臟「上下左右前後」的英文是？","opts":["Left 左／Right 右","Superior 上／Inferior 下","Anterior 前／Posterior 後","Circumflex 迴——環繞的方向"]},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"測驗 · 心肌梗塞","type":"quiz","noans":true,"kicker":"實際操作 · 第 3 題","art":"question","q":"什麼是心肌梗塞？","opts":["缺血性心臟疾病——占全球死亡率 15% 以上，為 2019 WHO 最大死因","病因與機制——養分、氧氣不足，冠狀動脈嚴重堵塞","症狀——胸悶、胸痛、呼吸困難、冒冷汗、心絞痛","診斷與治療——心電圖、冠狀動脈血管攝影術、藥物或氣球支架手術"]},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img046.png","timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img047.png","timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"看影片 + 寫 After（2）","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img048.png","timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"看影片 + 寫 After（3）","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img049.png","timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"Action 行動 + Review 反思","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img050.png","timer":900,"title":"Action <span class=\"hl\">行動</span>＋Review <span class=\"hl\">反思</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"互動：實際操作最有感的地方","type":"cover","art":"question","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得實際操作最有感的地方"},
{"ch":"實際操作","camp":"醫學營","p":"Part 1","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":2,"chLabel":"實際操作","title":"複習"},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"複習一下 · 心臟構造、方向英文、心肌梗塞","type":"frame","kicker":"複習一下 · 心臟構造、方向英文、心肌梗塞","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"心臟構造","p":"四個腔室（兩個心房、兩個心室）；心臟分層構造包含心內膜、心肌、心包膜；心臟內部構造有房室瓣、半月瓣、腱索、乳突狀肌；心臟傳導構造則有竇房結與房室結。"},{"b":"2","c":"var(--m-green)","h":"上下左右前後英文","p":"Left 左／Right 右；Superior 上／Inferior 下；Anterior 前／Posterior 後；Circumflex 迴，表示環繞的方向。"},{"b":"3","c":"var(--m-yellow)","h":"心肌梗塞","p":"缺血性心臟疾病，占全球死亡率 15% 以上；病因是養分、氧氣不足與冠狀動脈嚴重堵塞；症狀有胸悶、胸痛、呼吸困難、冒冷汗、心絞痛；可透過心電圖、冠狀動脈血管攝影術診斷，並以藥物或氣球支架手術治療。"}]},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"測驗 · 病症報告內容","type":"quiz","noans":true,"kicker":"實際操作 · 第 1 題","art":"path","q":"「病症報告」會有哪些內容？","opts":["解剖構造介紹——由外到內，依序介紹相關構造","病症介紹——病因、症狀、診斷方法、治療方法","衛教資料來源——衛福部網站、各家醫院衛教網站","學術資料來源——UpToDate、PubMed 等期刊論文"]},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img051.png","timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img052.png","timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"實際操作","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img053.png","timer":600,"music":true,"title":"動手<span class=\"hl\">實際操作</span>","sub":"動手實際操作，再到 Notion 補上你的紀錄"},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"看影片 + 寫 After（2）","type":"cover","art":"film","shotPlaceholder":true,"shot":"images/img054.png","timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"醫學營","p":"Part 2","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"實際操作","title":"引導"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"感受 · 醫學知識","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於學習「醫學知識」的過程，你<span class=\"hl\">喜歡</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">構造英文學名、器官構造、生理機制</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"感受 · 解剖構造","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於了解「解剖構造」的過程，你<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">外部構造、分層構造、內部構造、器官位置</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"感受 · 病症報告","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於實作「病症報告」，你<span class=\"hl\">想深入學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">病因、症狀、診斷方法、治療方法</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"shot":"images/img055.png","timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"Action + Review","type":"cover","art":"hand","shotPlaceholder":true,"shot":"images/img056.png","timer":900,"title":"Action ＋ <span class=\"hl\">Review</span>"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"Kahoot：實際操作","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"打開 Kahoot、輸入 PIN，看看實際操作這段你記住多少、答對多少～"},
{"ch":"實際操作","camp":"醫學營","p":"Part 3","m":"實際操作結束中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"學長姐分享","type":"cover","art":"question","shotPlaceholder":true,"shot":"images/img057.png","title":"學長姐<span class=\"hl\">分享</span>","sub":"記得寫下學長姐分享的三個重點及截圖。"},
{"ch":"學長姐分享","m":"學長姐分享後中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"學習反思","type":"raw","m":"封面 · 尾聲","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"cover-sub\" data-seq=\"0\">CIA · COMPANY IN AIR</div>\n      <div class=\"art-scene\" data-seq=\"0\" style=\"max-width:min(46vw,460px)\"><svg viewBox=\"0 0 600 400\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <radialGradient id=\"re-earth\" cx=\"50%\" cy=\"46%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#7fd4ff\"/><stop offset=\"55%\" stop-color=\"#2a7fd4\"/><stop offset=\"100%\" stop-color=\"#10336a\"/></radialGradient>\n    <linearGradient id=\"re-heat\" x1=\"0\" y1=\"0\" x2=\"1\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ff5b5b\"/><stop offset=\"50%\" stop-color=\"#ff8c3b\"/><stop offset=\"100%\" stop-color=\"#FFD63B\"/></linearGradient>\n    <linearGradient id=\"re-trail\" x1=\"1\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ff8c3b\" stop-opacity=\"0\"/><stop offset=\"100%\" stop-color=\"#ff5b5b\" stop-opacity=\".5\"/></linearGradient>\n  </defs>\n  <g>\n    <circle cx=\"300\" cy=\"600\" r=\"360\" fill=\"url(#re-earth)\"/>\n    <ellipse cx=\"300\" cy=\"262\" rx=\"300\" ry=\"30\" fill=\"#aee9ff\" opacity=\".25\"/>\n    <path d=\"M160 300 Q230 286 300 306 Q330 330 286 346 Q200 352 168 326 Z\" fill=\"#3fbf7a\" opacity=\".8\"/>\n    <path d=\"M360 320 Q430 312 470 332 Q480 354 440 364 Q380 368 358 346 Z\" fill=\"#3fbf7a\" opacity=\".75\"/>\n  </g>\n  <path d=\"M520 70 Q400 130 320 200\" stroke=\"url(#re-trail)\" stroke-width=\"14\" fill=\"none\" stroke-linecap=\"round\"><animate attributeName=\"opacity\" values=\".7;.35;.7\" dur=\"2s\" repeatCount=\"indefinite\"/></path>\n  <g transform=\"translate(320 200) rotate(135)\">\n    <path d=\"M0 -46 C18 -24 20 4 16 36 L-16 36 C-20 4 -18 -24 0 -46Z\" fill=\"#fff\"/>\n    <path d=\"M0 -46 C8 -36 12 -14 10 20 L-10 20 C-12 -14 -8 -36 0 -46Z\" fill=\"#cdd6f5\"/>\n    <circle cx=\"0\" cy=\"-14\" r=\"9\" fill=\"#161e4a\"/><circle cx=\"0\" cy=\"-14\" r=\"6\" fill=\"#3fe0d0\"/>\n    <path d=\"M-16 22 L-32 44 L-16 36Z\" fill=\"#7c5cff\"/><path d=\"M16 22 L32 44 L16 36Z\" fill=\"#7c5cff\"/>\n    <path d=\"M-22 34 Q0 56 22 34 Q0 48 -22 34Z\" fill=\"url(#re-heat)\"><animate attributeName=\"opacity\" values=\"1;.6;1\" dur=\".4s\" repeatCount=\"indefinite\"/></path>\n  </g>\n  <g fill=\"#fff\"><circle cx=\"120\" cy=\"80\" r=\"2\"/><circle cx=\"480\" cy=\"160\" r=\"2.2\"/><circle cx=\"200\" cy=\"130\" r=\"1.6\"/><circle cx=\"90\" cy=\"180\" r=\"1.8\"/></g>\n  <g fill=\"#FFD63B\"><circle cx=\"150\" cy=\"50\" r=\"1.8\"/><circle cx=\"450\" cy=\"70\" r=\"2\"/></g>\n</svg></div>\n      <h1 class=\"h-mega cover-title\" data-seq=\"0\">最後一段<span class=\"hl\">航程</span></h1>\n      <p class=\"lead\" data-seq=\"1\">一起完成今天的探索，好好為這趟旅程畫下句點 🌍</p>\n    </div>"},
{"ch":"學習反思","type":"cover","timer":180,"music":true,"shotMaxWidth":"13%","shot":"images/img058.png","title":"感受評分加總"},
{"ch":"學習反思","type":"cover","timer":480,"shotMaxWidth":"25%","shot":"images/img059.png","title":"學習歷程：Review"},
{"ch":"學習反思","type":"raw","m":"探索包 ① · 探索還沒結束","html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>探索，還沒結束</div>\n      <div class=\"art-lg\" data-seq=\"0\"><svg viewBox=\"0 0 240 240\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"gb-body\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#9a7bff\"/><stop offset=\"100%\" stop-color=\"#6b4ee0\"/></linearGradient>\n    <linearGradient id=\"gb-lid\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#5ef0e0\"/><stop offset=\"100%\" stop-color=\"#2bb8a8\"/></linearGradient>\n  </defs>\n  <ellipse cx=\"120\" cy=\"214\" rx=\"74\" ry=\"12\" fill=\"#000\" opacity=\".2\"/>\n  <rect x=\"58\" y=\"104\" width=\"124\" height=\"104\" rx=\"10\" fill=\"url(#gb-body)\"/>\n  <rect x=\"48\" y=\"78\" width=\"144\" height=\"36\" rx=\"10\" fill=\"url(#gb-lid)\"/>\n  <rect x=\"108\" y=\"104\" width=\"24\" height=\"104\" fill=\"#FFD63B\"/>\n  <rect x=\"108\" y=\"78\" width=\"24\" height=\"36\" fill=\"#ffe35c\"/>\n  <g fill=\"none\" stroke=\"#FFD63B\" stroke-width=\"14\" stroke-linecap=\"round\">\n    <path d=\"M120 70 C 96 40, 70 56, 84 72 C 94 82, 116 74, 120 70Z\" fill=\"#FFD63B\" stroke=\"none\"/>\n    <path d=\"M120 70 C 144 40, 170 56, 156 72 C 146 82, 124 74, 120 70Z\" fill=\"#ffe35c\" stroke=\"none\"/>\n  </g>\n  <circle cx=\"120\" cy=\"70\" r=\"11\" fill=\"#ff8c7a\"/>\n  <g fill=\"#fff\" opacity=\".85\"><circle cx=\"40\" cy=\"60\" r=\"3\"/><circle cx=\"206\" cy=\"100\" r=\"2.5\"/><circle cx=\"50\" cy=\"150\" r=\"2.5\"/><circle cx=\"200\" cy=\"170\" r=\"3\"/></g>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">營隊結束了，<br>但你的<span class=\"hl\">探索</span>才正要開始</h2>\n      <p class=\"lead\" data-seq=\"1\">填寫營後問卷，就能拿到我們為你準備的<br><span class=\"hl-aqua\">科系探索包</span> 🎁</p>\n    </div>"},
{"ch":"學習反思","type":"raw","m":"探索包 ② · 裡面有什麼","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>科系探索包 · 裡面有什麼</div>\n      <h2 class=\"h-big\" data-seq=\"0\">還有點<span class=\"hl\">迷惘</span>？<br>這份包幫你補齊資源</h2>\n      <div class=\"op-cards c4\" data-seq=\"1\">\n        <div class=\"op-card\"><span class=\"ic\">🌐</span><h3>網站與影片</h3><p>各科系網站、YouTube</p></div>\n        <div class=\"op-card\"><span class=\"ic\">📚</span><h3>推薦書籍</h3><p>幫你入門的好書</p></div>\n        <div class=\"op-card\"><span class=\"ic\">🎓</span><h3>學長姐經驗</h3><p>過來人的真實分享</p></div>\n        <div class=\"op-card\"><span class=\"ic\">🚀</span><h3>營隊與課程</h3><p>值得參與的下一步</p></div>\n      </div>\n    </div>"},
{"ch":"學習反思","type":"raw","m":"探索包 ③ · 怎麼拿到","html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>怎麼拿到科系探索包</div>\n      <div class=\"art-lg\" data-seq=\"0\"><svg viewBox=\"0 0 260 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"env-b\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#fff\"/><stop offset=\"100%\" stop-color=\"#d9e0f5\"/></linearGradient>\n  </defs>\n  <ellipse cx=\"130\" cy=\"184\" rx=\"92\" ry=\"11\" fill=\"#000\" opacity=\".18\"/>\n  <!-- 露出的卡片 -->\n  <rect x=\"78\" y=\"34\" width=\"104\" height=\"86\" rx=\"8\" fill=\"#fff8e0\"/>\n  <rect x=\"92\" y=\"52\" width=\"60\" height=\"8\" rx=\"4\" fill=\"#FFD63B\"/>\n  <rect x=\"92\" y=\"68\" width=\"76\" height=\"6\" rx=\"3\" fill=\"#cdd6f5\"/>\n  <rect x=\"92\" y=\"80\" width=\"76\" height=\"6\" rx=\"3\" fill=\"#cdd6f5\"/>\n  <rect x=\"92\" y=\"92\" width=\"50\" height=\"6\" rx=\"3\" fill=\"#cdd6f5\"/>\n  <!-- 信封身 -->\n  <rect x=\"44\" y=\"78\" width=\"172\" height=\"100\" rx=\"12\" fill=\"url(#env-b)\"/>\n  <path d=\"M44 90 L130 142 L216 90\" fill=\"none\" stroke=\"#aeb7cc\" stroke-width=\"5\" stroke-linecap=\"round\"/>\n  <path d=\"M44 88 L130 40 L216 88\" fill=\"#eef2ff\" stroke=\"#aeb7cc\" stroke-width=\"4\" stroke-linejoin=\"round\"/>\n  <circle cx=\"216\" cy=\"64\" r=\"22\" fill=\"#3fe0d0\"/><path d=\"M206 64 l7 7 l13 -14\" fill=\"none\" stroke=\"#fff\" stroke-width=\"5\" stroke-linecap=\"round\" stroke-linejoin=\"round\"/>\n  <g fill=\"#FFD63B\"><circle cx=\"34\" cy=\"50\" r=\"3\"/><circle cx=\"240\" cy=\"140\" r=\"2.5\"/></g>\n</svg></div>\n      <h2 class=\"h-big\" data-seq=\"0\">到 <span class=\"hl\">Notion</span> 填寫營後表單，<br>探索包就<span class=\"hl\">寄到你的信箱</span> ✉️</h2>\n      <p class=\"lead\" data-seq=\"1\">幫你更深入了解各科系的內容與方向</p>\n    </div>"},
{"ch":"學習反思","type":"cover","timer":1200,"shotMaxWidth":"9%","shot":"images/img060.png","title":"營後表單"},
{"ch":"學習反思","type":"raw","m":"大合照","html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>留下今天的回憶</div>\n      <div class=\"art-xl\" data-seq=\"0\" style=\"max-width:min(46vw,500px)\"><svg viewBox=\"0 0 300 210\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"vg-win\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#222b5c\"/><stop offset=\"100%\" stop-color=\"#161d44\"/></linearGradient>\n  </defs>\n  <ellipse cx=\"150\" cy=\"198\" rx=\"120\" ry=\"10\" fill=\"#000\" opacity=\".2\"/>\n  <rect x=\"8\" y=\"8\" width=\"284\" height=\"180\" rx=\"16\" fill=\"url(#vg-win)\" stroke=\"#3a4690\" stroke-width=\"2\"/>\n  <g transform=\"translate(20 20)\">\n      <rect width=\"76\" height=\"72\" rx=\"9\" fill=\"#2c3568\"/>\n      <circle cx=\"38\" cy=\"30\" r=\"13\" fill=\"#FFD63B\"/>\n      <path d=\"M16 66 Q16 45 38 45 Q60 45 60 66 Z\" fill=\"#FFD63B\"/>\n    </g><g transform=\"translate(112 20)\">\n      <rect width=\"76\" height=\"72\" rx=\"9\" fill=\"#2c3568\"/>\n      <circle cx=\"38\" cy=\"30\" r=\"13\" fill=\"#3fe0d0\"/>\n      <path d=\"M16 66 Q16 45 38 45 Q60 45 60 66 Z\" fill=\"#3fe0d0\"/>\n    </g><g transform=\"translate(204 20)\">\n      <rect width=\"76\" height=\"72\" rx=\"9\" fill=\"#2c3568\"/>\n      <circle cx=\"38\" cy=\"30\" r=\"13\" fill=\"#9a7bff\"/>\n      <path d=\"M16 66 Q16 45 38 45 Q60 45 60 66 Z\" fill=\"#9a7bff\"/>\n    </g><g transform=\"translate(20 104)\">\n      <rect width=\"76\" height=\"72\" rx=\"9\" fill=\"#2c3568\"/>\n      <circle cx=\"38\" cy=\"30\" r=\"13\" fill=\"#ff8c7a\"/>\n      <path d=\"M16 66 Q16 45 38 45 Q60 45 60 66 Z\" fill=\"#ff8c7a\"/>\n    </g><g transform=\"translate(112 104)\">\n      <rect width=\"76\" height=\"72\" rx=\"9\" fill=\"#2c3568\"/>\n      <circle cx=\"38\" cy=\"30\" r=\"13\" fill=\"#46c46a\"/>\n      <path d=\"M16 66 Q16 45 38 45 Q60 45 60 66 Z\" fill=\"#46c46a\"/>\n    </g><g transform=\"translate(204 104)\">\n      <rect width=\"76\" height=\"72\" rx=\"9\" fill=\"#2c3568\"/>\n      <circle cx=\"38\" cy=\"30\" r=\"13\" fill=\"#5b7bff\"/>\n      <path d=\"M16 66 Q16 45 38 45 Q60 45 60 66 Z\" fill=\"#5b7bff\"/>\n    </g>\n  <g><circle cx=\"132\" cy=\"172\" r=\"7\" fill=\"#3fe0d0\"/><circle cx=\"152\" cy=\"172\" r=\"7\" fill=\"#3a4690\"/><circle cx=\"172\" cy=\"172\" r=\"7\" fill=\"#ff8c7a\"/></g>\n  <g fill=\"#fff\" opacity=\".6\"><circle cx=\"280\" cy=\"30\" r=\"2.5\"/><circle cx=\"20\" cy=\"150\" r=\"2\"/></g>\n</svg></div>\n      <h2 class=\"h-mega\" data-seq=\"0\"><span class=\"hl\">大合照</span>＋給證書</h2>\n    </div>"},
{"ch":"學習反思","type":"cover","timer":120,"music":true,"shot":"images/img061.png","title":"檢查證書 + 合照"},
{"ch":"學習反思","type":"raw","m":"閉幕 ① · 恭喜完成","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>恭喜你，完成了今天的旅程</div>\n      <h2 class=\"h-big\" data-seq=\"0\">短短一天，<br>你完成了這 <span class=\"hl\">三件大事</span></h2>\n      <div class=\"op-cards c3 big-cards\" data-seq=\"1\">\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 180 160\" xmlns=\"http://www.w3.org/2000/svg\">\n  <path d=\"M90 34 C70 22 38 22 22 30 L22 128 C38 120 70 120 90 132Z\" fill=\"#7c5cff\"/>\n  <path d=\"M90 34 C110 22 142 22 158 30 L158 128 C142 120 110 120 90 132Z\" fill=\"#3fe0d0\"/>\n  <path d=\"M90 34 L90 132\" stroke=\"#161e4a\" stroke-width=\"3.5\"/>\n  <g stroke=\"#fff\" stroke-width=\"3\" opacity=\".6\"><line x1=\"36\" y1=\"54\" x2=\"74\" y2=\"58\"/><line x1=\"36\" y1=\"72\" x2=\"74\" y2=\"76\"/><line x1=\"36\" y1=\"90\" x2=\"68\" y2=\"94\"/><line x1=\"106\" y1=\"58\" x2=\"144\" y2=\"54\"/><line x1=\"106\" y1=\"76\" x2=\"144\" y2=\"72\"/><line x1=\"106\" y1=\"94\" x2=\"138\" y2=\"90\"/></g>\n  <circle cx=\"90\" cy=\"24\" r=\"8\" fill=\"#FFD63B\"/>\n</svg></div><span class=\"num\">01</span><h3>科系所學</h3><p>大學在學什麼、會獲得哪些能力</p></div>\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 240 240\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><radialGradient id=\"gr-big\" cx=\"40%\" cy=\"35%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#5ef0e0\"/><stop offset=\"100%\" stop-color=\"#2bb8a8\"/></radialGradient></defs>\n  <g transform=\"translate(95 105)\">\n    <g fill=\"url(#gr-big)\">\n      <circle r=\"52\"/>\n      <g><rect x=\"-9\" y=\"-68\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-9\" y=\"48\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-68\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/><rect x=\"48\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/></g>\n      <g transform=\"rotate(45)\"><rect x=\"-9\" y=\"-68\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-9\" y=\"48\" width=\"18\" height=\"20\" rx=\"3\"/><rect x=\"-68\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/><rect x=\"48\" y=\"-9\" width=\"20\" height=\"18\" rx=\"3\"/></g>\n    </g>\n    <circle r=\"20\" fill=\"#0d1330\"/>\n  </g>\n  <g transform=\"translate(176 158)\">\n    <g fill=\"#FFD63B\">\n      <circle r=\"34\"/>\n      <g><rect x=\"-7\" y=\"-46\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-7\" y=\"30\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-46\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/><rect x=\"30\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/></g>\n      <g transform=\"rotate(45)\"><rect x=\"-7\" y=\"-46\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-7\" y=\"30\" width=\"14\" height=\"16\" rx=\"3\"/><rect x=\"-46\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/><rect x=\"30\" y=\"-7\" width=\"16\" height=\"14\" rx=\"3\"/></g>\n    </g>\n    <circle r=\"13\" fill=\"#0d1330\"/>\n  </g>\n  <g fill=\"#fff\" opacity=\".5\"><circle cx=\"40\" cy=\"50\" r=\"2.5\"/><circle cx=\"205\" cy=\"60\" r=\"2\"/><circle cx=\"55\" cy=\"200\" r=\"2.5\"/></g>\n</svg></div><span class=\"num\">02</span><h3>實際操作</h3><p>自己動手，紮實做過一遍</p></div>\n        <div class=\"op-card\"><div class=\"op-card-art\"><svg viewBox=\"0 0 200 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs><linearGradient id=\"ts\" x1=\"0\" y1=\"0\" x2=\"1\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#FFD63B\"/><stop offset=\"100%\" stop-color=\"#c98e1a\"/></linearGradient></defs>\n  <rect x=\"92\" y=\"118\" width=\"12\" height=\"56\" fill=\"#cdd6f5\"/>\n  <path d=\"M66 174 L130 174 L116 190 L80 190Z\" fill=\"#7c5cff\"/>\n  <g transform=\"rotate(-32 110 90)\">\n    <rect x=\"48\" y=\"74\" width=\"120\" height=\"30\" rx=\"15\" fill=\"url(#ts)\"/>\n    <rect x=\"158\" y=\"69\" width=\"24\" height=\"40\" rx=\"7\" fill=\"#3fe0d0\"/>\n    <circle cx=\"56\" cy=\"89\" r=\"10\" fill=\"#161e4a\"/>\n  </g>\n  <g fill=\"#FFD63B\"><circle cx=\"40\" cy=\"36\" r=\"3.5\"/><circle cx=\"64\" cy=\"22\" r=\"2.5\"/><circle cx=\"28\" cy=\"58\" r=\"2.5\"/><circle cx=\"160\" cy=\"30\" r=\"3\"/></g>\n</svg></div><span class=\"num\">03</span><h3>未來發展</h3><p>對這個科系的出路更有概念</p></div>\n      </div>\n      <p class=\"lead\" data-seq=\"2\">用一天完成這些，真的<span class=\"hl\">超級棒</span>！👏</p>\n    </div>"},
{"ch":"學習反思","type":"raw","m":"道別前分享旅程","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>在道別之前</div>\n      <h1 class=\"h-mega cover-title\" data-seq=\"0\">在道別前，<br>和你<span class=\"hl\">分享</span>我的旅程</h1>\n      <p class=\"lead\" data-seq=\"1\">回顧今天的探索，有哪些發現、感受，想跟大家分享呢？</p>\n    </div>"},
{"ch":"學習反思","type":"raw","m":"最後想和你說","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>寫在最後</div>\n      <h1 class=\"h-mega cover-title\" data-seq=\"0\">最後，<br>想和你<span class=\"hl\">說</span></h1>\n      <p class=\"lead\" data-seq=\"1\">把今天最想記住的一句話，寫給未來的自己吧！</p>\n    </div>"},
{"ch":"學習反思","type":"raw","m":"探索更多 · 折扣碼","html":"\n    <div class=\"scene-inner wide\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span>想探索更多？兩件事想跟你說</div>\n      <div class=\"op-cards c2 reason-cards\" data-seq=\"0\">\n        <div class=\"op-card\"><span class=\"ic\">🎉</span><h3>發現不喜歡，超棒的！</h3><p>代表你不用花大學四年，<br>耗在一個不喜歡的科系上</p></div>\n        <div class=\"op-card\"><span class=\"ic\">🧭</span><h3>還不確定？去看看別的</h3><p>多參加不同科系的課程，<br>實際了解各系在做什麼</p></div>\n      </div>\n      <div class=\"op-promo\" data-seq=\"1\">\n        <div class=\"op-promo-l\">今天限定折扣碼<br><span class=\"op-promo-note\">折抵 200 元 · 僅限今天</span></div>\n        <div class=\"op-promo-code\">CIA200</div>\n      </div>\n    </div>"},
{"ch":"學習反思","type":"raw","m":"感謝 · 營隊結束","music":true,"html":"\n    <div class=\"scene-inner\">\n      <div class=\"eyebrow\" data-seq=\"0\"><span class=\"dot\"></span></div>\n      <div class=\"art-hero\" data-seq=\"0\" style=\"width:clamp(128px,15vw,195px)\"><svg viewBox=\"0 0 160 200\" xmlns=\"http://www.w3.org/2000/svg\">\n  <defs>\n    <linearGradient id=\"gsFFD63B\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#ffffff\"/><stop offset=\"100%\" stop-color=\"#d4dbf0\"/></linearGradient>\n    <radialGradient id=\"gv3fe0d0\" cx=\"42%\" cy=\"36%\" r=\"70%\"><stop offset=\"0%\" stop-color=\"#3fe0d0\"/><stop offset=\"72%\" stop-color=\"#1a2a66\"/><stop offset=\"100%\" stop-color=\"#0d1330\"/></radialGradient>\n  </defs>\n  <ellipse cx=\"80\" cy=\"190\" rx=\"42\" ry=\"8\" fill=\"#000\" opacity=\".18\"/>\n  <path d=\"M44 120 Q80 108 116 120 L122 178 L38 178 Z\" fill=\"url(#gsFFD63B)\"/>\n  <path d=\"M70 112 L90 112 L86 178 L74 178 Z\" fill=\"#FFD63B\" opacity=\".9\"/>\n  <rect x=\"28\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gsFFD63B)\"/><rect x=\"112\" y=\"124\" width=\"20\" height=\"44\" rx=\"10\" fill=\"url(#gsFFD63B)\"/>\n  <circle cx=\"38\" cy=\"166\" r=\"12\" fill=\"#FFD63B\"/><circle cx=\"122\" cy=\"166\" r=\"12\" fill=\"#FFD63B\"/>\n  <circle cx=\"80\" cy=\"74\" r=\"40\" fill=\"url(#gsFFD63B)\"/><circle cx=\"80\" cy=\"74\" r=\"29\" fill=\"url(#gv3fe0d0)\"/>\n  <ellipse cx=\"69\" cy=\"64\" rx=\"8\" ry=\"11\" fill=\"#fff\" opacity=\".5\"/>\n  <g transform=\"translate(80 36)\">\n    <rect x=\"-34\" y=\"-6\" width=\"68\" height=\"14\" rx=\"3\" fill=\"#1a2150\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"#222c63\"/>\n    <path d=\"M-40 0 L0 -16 L40 0 L0 16 Z\" fill=\"none\" stroke=\"#FFD63B\" stroke-width=\"2\"/>\n    <circle cx=\"0\" cy=\"0\" r=\"4\" fill=\"#FFD63B\"/>\n    <path d=\"M0 0 L30 6 L30 22\" stroke=\"#FFD63B\" stroke-width=\"2.5\" fill=\"none\"/>\n    <circle cx=\"30\" cy=\"24\" r=\"4\" fill=\"#FFD63B\"/>\n  </g>\n  <rect x=\"68\" y=\"130\" width=\"24\" height=\"8\" rx=\"4\" fill=\"#7c5cff\"/>\n</svg></div>\n      <h2 class=\"h-mega\" data-seq=\"0\">謝謝你來參加 <span class=\"hl\">CIA</span>！</h2>\n      <p class=\"lead\" data-seq=\"0\">今天的營隊就到這裡，我們下次再見 👋</p>\n    </div>"},
{"ch":"休息","camp":"醫學營","m":"中場休息 · 計時器＋音樂","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"休息","camp":"醫學營","m":"聊天室分享","type":"cover","art":"hand","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"趁這幾分鐘，把你現在的想法、心得，或任何問題打在聊天室裡分享給大家！"},
{"ch":"科系所學","camp":"財經營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"科系所學","title":"前導"},
{"ch":"科系所學","camp":"財經營","p":"Part 1","m":"測驗 · 核心能力","type":"quiz","noans":true,"kicker":"科系所學 · 第 1 題","art":"pulse","q":"材料系的核心能力有哪些？","opts":["美術設計、色彩搭配、模型雕塑","財務規劃、行銷企劃、業務銷售","材料結構分析、性質與可靠性評估、製程優化改良","只要背公式、記憶力好就能學好"],"ans":2},
{"ch":"科系所學","camp":"財經營","p":"Part 1","m":"測驗 · 必修課程","type":"quiz","noans":true,"kicker":"科系所學 · 第 2 題","art":"path","q":"材料系有哪些必修課程？","opts":["會計學、行銷管理、財務報表分析","純美學設計課程，不碰數理基礎","不用做實驗，全部用背的就好","材料科學與工程導論、材料熱力學、物理冶金、材料實驗"],"ans":3},
{"ch":"科系所學","camp":"財經營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 1","m":"影片一","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>","sub":"到 Notion 看影片一吧"},
{"ch":"科系所學","camp":"財經營","m":"RAP 反思法","type":"frame","kicker":"停下來，帶你反思一次","art":"reflect","title":"用 <span class=\"hl\">RAP</span> 反思","steps":[{"b":"R","c":"var(--m-blue)","h":"Review｜複習","p":"複習剛剛的課程筆記——今天到底學了哪些內容？"},{"b":"A","c":"var(--m-green)","h":"Ask｜自問","p":"問問自己：這個領域，我喜歡嗎？有沒有讓我想深入的地方？"},{"b":"P","c":"var(--m-yellow)","h":"Present｜表達","p":"把想法講出來、闡述出來——等一下用感受評分表達，並寫進講義。"}],"p":"Part 1"},
{"ch":"科系所學","camp":"財經營","p":"Part 1","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"科系所學","title":"複習"},
{"ch":"科系所學","camp":"財經營","p":"Part 2","m":"複習一下 · 材料系三大能力","type":"frame","kicker":"複習一下 · 材料結構分析、可靠性評估、製程優化","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"材料結構分析","p":"用電子顯微鏡（如 TEM）觀察原子排列是否整齊、有無缺陷——缺陷有時反而能強化材料（如提升導電性）。例如晶片裡上億個電晶體，就是靠結構分析確認製程沒問題（比對 FinFET 不同寬度的電晶體結構）。"},{"b":"2","c":"var(--m-green)","h":"性質與可靠性評估","p":"測試材料在高溫、受力、化學反應等情境下會不會變形、老化或失效，確保產品能長時間穩定運作。半導體晶片材料只要稍有變形，就可能導致晶片出錯。"},{"b":"3","c":"var(--m-yellow)","h":"製程優化改良","p":"調整溫度、時間、壓力等製程參數，提高品質與良率、降低成本。材料選對、製法調整好，就能做出導電佳、不易過熱的晶片，例如調整金屬導線厚度（Cu、Mo、Ru）來控制導電性。"}]},
{"ch":"科系所學","camp":"財經營","p":"Part 2","m":"想想看 · 最期待的學習階段","type":"quiz","noans":true,"kicker":"想想看 · 四年學習地圖","art":"path","q":"材料系四年的學習歷程，你最期待哪個階段？","opts":["大一：打材料與數理基礎（材料導論、普通化學、微積分）","大二：理論建構＋基礎操作能力（材料熱力學、晶體結構、材料實驗）","大三：專題研究、深入理論與實務（機械性質、擴散與相變化）","大四：進入固態物理、金屬、高分子等進階應用領域"]},
{"ch":"科系所學","camp":"財經營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"科系所學","camp":"財經營","p":"Part 2","m":"發現反思 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 <span class=\"hl\">After</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"科系所學","title":"反思"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"感受 · 培養的能力","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於材料系培養的能力，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">材料結構分析：看原子如何排列｜性質與穩定判斷：選正確材料，不變形不壞掉｜製程優化改良：改流程控溫度，東西更好更省</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"感受 · 相關課程","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對材料系的相關課程，你<span class=\"hl\">想學習</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">材料科學與工程導論、材料熱力學｜物理冶金、晶體結構與繞射導論、材料實驗</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"感受 · 四年規劃","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"材料系大學四年規劃，你<span class=\"hl\">期待</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">大一：基礎材料與數理知識｜大二：材料理論實驗操作｜大三：材料結構應用分析｜大四：整合知識實作創新</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"發現反思 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"發現反思 After<br>（自主反思）"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"科系所學","camp":"財經營","m":"SMART 撰寫法","type":"frame","kicker":"學習歷程怎麼寫","art":"notion","title":"用 <span class=\"hl\">SMART</span> 五步，不卡關","steps":[{"b":"S","c":"var(--m-blue)","h":"Summarize｜摘要","p":"這份檔案想呈現的重點，先寫在最前面。"},{"b":"M","c":"var(--m-green)","h":"Mention｜說明","p":"說明你參加的動機，以及這個課程／活動在做什麼。"},{"b":"A","c":"var(--m-yellow)","h":"Action｜行動","p":"記錄你做了哪些具體的事、採取了哪些行動。"},{"b":"R","c":"var(--m-red)","h":"Review｜反思","p":"反思喜不喜歡、原因，以及接下來想做什麼。"},{"b":"T","c":"var(--m-blue)","h":"Template｜模板","p":"選一個模板輸出——Canva、Notion 都可以。"}],"p":"Part 3"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"分享一個最有感的內容","type":"cover","art":"reflect","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得最有感的內容"},
{"ch":"科系所學","camp":"財經營","p":"Part 3","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"未來發展","camp":"財經營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":3,"chLabel":"未來發展","title":"前導"},
{"ch":"未來發展","camp":"財經營","p":"Part 1","m":"測驗 · 畢業職缺","type":"quiz","noans":true,"kicker":"未來發展 · 第 1 題","art":"rise","q":"材料系畢業後，有哪些職缺？你比較嚮往哪一種？","opts":["研究開發工程師（R&D）——做材料實驗、儀器分析、開發新材料","製程整合／製程工程師——優化生產流程、解決現場技術問題","學術界、研究機構——做研究、發表論文、指導學生","還沒想清楚，想多方嘗試看看"]},
{"ch":"未來發展","camp":"財經營","p":"Part 1","m":"測驗 · 相關公司","type":"quiz","noans":true,"kicker":"未來發展 · 第 2 題","art":"reflect","q":"材料系畢業後，可以去哪些公司？你比較想進哪一種？","opts":["半導體公司——如台積電、聯電，做晶片相關製造","化工材料公司——如信越化學、默克，提供先進製程化學品","設備商——如 ASML、應用材料，做微影／蝕刻／鍍膜設備","能源生醫公司——如寧德時代、晶鑽生醫，做電池或生醫材料"]},
{"ch":"未來發展","camp":"財經營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"未來發展","camp":"財經營","p":"Part 1","m":"影片一 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片一</span>＋寫 After","sub":"先看第一支影片，再到 Notion 補上你的 After"},
{"ch":"未來發展","camp":"財經營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":3,"chLabel":"未來發展","title":"複習"},
{"ch":"未來發展","camp":"財經營","p":"Part 2","m":"複習一下 · 三種職涯選擇","type":"frame","kicker":"複習一下 · R&D、製程工程師、學術研究","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"研究開發工程師（R&D）","p":"工作內容：材料實驗操作、儀器分析（XRD、SEM、TEM）、數據分析、新材料開發、技術文件與專利整合。所需能力：材料科學知識、儀器操作技能、研發與創新思維。"},{"b":"2","c":"var(--m-green)","h":"製程整合、製程工程師","p":"工作內容：材料實驗操作、儀器分析、生產流程優化、解決製造現場問題、調整製程參數提升良率。所需能力：熟悉半導體製程、邏輯分析力、跨部門溝通、快速反應能力。"},{"b":"3","c":"var(--m-yellow)","h":"學術界、研究機構","p":"工作內容：儀器實驗與教學、發表學術論文、執行研究計畫並指導學生、與研究團隊合作推進科研任務。所需能力：儀器操作與教學、論文寫作（含英文）、學生指導與團隊合作。"}]},
{"ch":"未來發展","camp":"財經營","p":"Part 2","m":"想想看 · 想了解的公司與趨勢","type":"quiz","noans":true,"kicker":"想想看 · 半導體、材料設備、能源生醫、未來趨勢","art":"question","q":"材料相關的公司與趨勢，你比較好奇哪一塊？","opts":["半導體公司——如台積電、聯電，做晶片製造與代工","材料與設備供應商——如信越化學、ASML，提供先進製程化學品與設備","能源生醫公司——如寧德時代、晶鑽生醫，做電池或生醫材料","未來趨勢——EUV 光阻劑、綠能材料、生醫感測器等新興領域"]},
{"ch":"未來發展","camp":"財經營","p":"Part 2","m":"影片二 + 截圖","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看<span class=\"hl\">影片二</span>","sub":"到 Notion 看影片二吧，記得把重點截圖存下來"},
{"ch":"未來發展","camp":"財經營","p":"Part 2","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"未來發展","camp":"財經營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"未來發展","title":"反思"},
{"ch":"未來發展","camp":"財經營","p":"Part 3","m":"感受 · 材料系職缺","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於材料系的職缺，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">研究開發工程師（R&D）｜製程整合、製程工程師｜學術界、研究機構</span>"},
{"ch":"未來發展","camp":"財經營","p":"Part 3","m":"感受 · 常見公司","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於材料系常見公司，你的<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">半導體：台積電、聯電、Intel｜化工材料：信越化學工業、默克集團、勝高｜設備商：ASML、科林研發、應用材料｜能源生醫：寧德時代、晶鑽生醫、長聖國際</span>"},
{"ch":"未來發展","camp":"財經營","p":"Part 3","m":"感受 · 未來產業趨勢","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"對於未來產業趨勢，你<span class=\"hl\">感興趣</span>的程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">半導體材料、綠能／碳中和、生醫／醫療材料</span>"},
{"ch":"未來發展","camp":"財經營","p":"Part 3","m":"寫 After（自主反思）","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 After<br>（自主反思）"},
{"ch":"未來發展","camp":"財經營","p":"Part 3","m":"Action 行動","type":"cover","art":"hand","shotPlaceholder":true,"timer":420,"title":"Action <span class=\"hl\">行動</span>"},
{"ch":"未來發展","camp":"財經營","p":"Part 3","m":"Review 反思","type":"cover","art":"reflect","shotPlaceholder":true,"timer":540,"title":"Review <span class=\"hl\">反思</span>"},
{"ch":"未來發展","m":"競賽 · Kahoot","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"吃飯前，先來一場 PK！打開 Kahoot、輸入 PIN，看看你記住多少、答對多少～","p":"Part 3","camp":"財經營"},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"寫 Slido","type":"cover","art":"question","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">Slido</span>","sub":"把你的想法或問題打在 Slido 上，我們稍後一起看！"},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"Part 1：內容準備中","type":"part","no":1,"total":2,"chLabel":"實際操作","title":"前導"},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"測驗 · 能帶是什麼","type":"quiz","noans":true,"kicker":"實際操作 · 第 1 題","art":"pulse","q":"能帶是什麼？如果用「電子住在樓層」來比喻，你覺得哪一種最好理解？","opts":["導體——樓層相連，電子可以自由移動（傳導帶與價帶重疊）","絕緣體——樓層距離太遠，電子幾乎跳不上去（能隙很大）","半導體——特定條件下可以跳到更高樓層（能隙適中）","還是有點抽象，需要多看幾次圖解"]},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"測驗 · 可靠性評估","type":"quiz","noans":true,"kicker":"實際操作 · 第 2 題","art":"path","q":"半導體晶片材料為什麼需要做可靠性評估？","opts":["因為要讓晶片看起來更美觀","為了讓材料賣相更好，方便行銷","只是例行公事，跟晶片品質無關","確認材料在高溫、受力、化學反應等情境下會不會變形、老化或失效，避免產品出錯"],"ans":3},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"互動：實際操作最有感的地方","type":"cover","art":"question","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"分享你覺得實際操作最有感的地方"},
{"ch":"實際操作","camp":"財經營","p":"Part 1","m":"中場休息","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"實際操作","camp":"財經營","p":"Part 2","m":"Part 2：內容準備中","type":"part","no":2,"total":2,"chLabel":"實際操作","title":"複習"},
{"ch":"實際操作","camp":"財經營","p":"Part 2","m":"複習一下 · 半導體物理入門","type":"frame","kicker":"複習一下 · 原子電子結構、能帶理論、摻雜、PN接面","art":"reflect","title":"複習一下","steps":[{"b":"1","c":"var(--m-blue)","h":"原子與電子的結構","p":"道耳吞提出原子理論，認為原子是不可再分的最小粒子；材料性質要從原子層級看起，了解電子在原子核外不同能階的分布——能階越高離原子核越遠，電子可吸收或釋放能量在能階間移動，能階距離也影響材料的導電性。"},{"b":"2","c":"var(--m-green)","h":"能帶理論","p":"能帶包含「價帶」與「傳導帶」，材料可分為金屬（導體）、半導體、絕緣體。就像電子住在樓層裡：導體樓層相連、電子自由移動；絕緣體樓層太遠、能隙大難以躍遷；半導體能隙適中，特定條件下可以跳上更高樓層導電。"},{"b":"3","c":"var(--m-yellow)","h":"摻雜與半導體","p":"純矽導電性低，加入少量雜質（摻雜）可改變導電性：加硼形成缺少電子的「電洞」，成為 P 型半導體；加磷形成多餘的「自由電子」，成為 N 型半導體。控制摻雜物質種類與濃度，就能調控半導體的導電特性。"},{"b":"4","c":"var(--m-red)","h":"PN 接面與二極體","p":"把 P 型與 N 型半導體接合，形成 PN 接面；電子與電洞在交界處重新分布，建立內建電位（0.3～0.7V）。正向偏壓時導通、反向時不導通，這就是二極體的單向導電特性，可作為開關與整流元件。"}]},
{"ch":"實際操作","camp":"財經營","p":"Part 2","m":"想想看 · 二極體與PN接面","type":"quiz","noans":true,"kicker":"想想看 · 電流方向、手機應用、內建電場、正向偏壓","art":"path","q":"關於二極體與 PN 接面的原理，你最想先搞懂哪一個？","opts":["電流為什麼只能單向流動——反向偏壓會擋住電流","為什麼手機電路離不開二極體——防止電流逆流、保護元件","P 型與 N 型接合為什麼會有內建電場——電子電洞擴散形成耗盡區","正向偏壓時電流為什麼突然變大——載子越過耗盡區重新流動"]},
{"ch":"實際操作","camp":"財經營","p":"Part 2","m":"探索暖身 Before","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"探索暖身 <span class=\"hl\">Before</span>"},
{"ch":"實際操作","camp":"財經營","p":"Part 2","m":"看影片 + 寫 After","type":"cover","art":"film","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"看影片 / 實際操作＋寫 <span class=\"hl\">After</span>","sub":"看影片或動手實際操作，再到 Notion 補上你的 After"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"Part 3：內容準備中","type":"part","no":3,"total":3,"chLabel":"實際操作","title":"引導"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"材料系引導 3","type":"cover","art":"compass","shotPlaceholder":true,"timer":600,"noMusic":true,"title":"材料系<span class=\"hl\">引導 3</span>","sub":"跟著引導活動，繼續深入體驗這個科系"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"感受 · PN接面與二極體","type":"score","kicker":"感受評分 · 1／3","art":"pulse","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"了解 PN 接面、二極體的過程，<span class=\"hl\">感興趣</span>程度是？<br><span style=\"font-size:.6em;color:var(--sub);font-weight:600\">P 型與 N 型半導體、電子與電洞擴散｜二極體具有單向導電特性，可作開關與整流</span>"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"感受 · PhET 模擬","type":"score","kicker":"感受評分 · 2／3","art":"notion","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"用 PhET 了解電子流動的過程，<span class=\"hl\">喜歡</span>程度是？"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"感受 · 電洞電子答題","type":"score","kicker":"感受評分 · 3／3","art":"path","scoreOpts":[{"i":"❤️","s":"7 分","t":"非常喜歡，期待能深入研究此領域內容","c":"s7"},{"i":"👍","s":"5～6 分","t":"感興趣，期待能更深入了解","c":"s5"},{"i":"🎉","s":"4 分","t":"不確定是否合適，但會想要進一步了解","c":"s3"},{"i":"👏","s":"1～3 分","t":"沒什麼興趣或會排斥，不會主動接觸學習","c":"s1"}],"q":"在答題了解電洞、電子的過程，<span class=\"hl\">感興趣</span>程度是？"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"寫 After","type":"cover","art":"notion","shotPlaceholder":true,"timer":180,"title":"寫 <span class=\"hl\">After</span>"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"Action + Review","type":"cover","art":"hand","shotPlaceholder":true,"timer":900,"title":"Action ＋ <span class=\"hl\">Review</span>"},
{"ch":"實際操作","camp":"財經營","p":"Part 3","m":"Kahoot：實際操作","type":"cover","art":"trophy","title":"來玩 <span class=\"hl\">Kahoot</span>！","sub":"打開 Kahoot、輸入 PIN，看看實際操作這段你記住多少、答對多少～"},
{"ch":"實際操作","camp":"財經營","p":"Part 2","m":"休息一下再出發","type":"break","kicker":"休息一下","art":"coffee","title":"辛苦了，休息一下 <span class=\"hl\">☕</span>","sub":"這段結束了，起來動一動、喝口水，準備進入下一個段落！"},
{"ch":"休息","camp":"財經營","m":"中場休息 · 計時器＋音樂","type":"break","kicker":"中場休息","art":"coffee","title":"休息一下，喘口氣 <span class=\"hl\">☕</span>","sub":"去洗手間、喝口水、動一動——倒數結束前回到座位，我們就繼續下一段！"},
{"ch":"休息","camp":"財經營","m":"聊天室分享","type":"cover","art":"hand","timer":30,"title":"請在<span class=\"hl\">聊天室</span>分享吧","sub":"趁這幾分鐘，把你現在的想法、心得，或任何問題打在聊天室裡分享給大家！"},
{"ch":"收尾","camp":"財經營","m":"午餐後，問學長姐 Slido","type":"frame","kicker":"吃飯後，問問學長姐","art":"question","title":"到 <span class=\"hl\">Slido</span>，用 USB 三個方向問","steps":[{"b":"U","c":"var(--m-blue)","h":"Usually｜平常","p":"學長姐平常都在忙什麼？課堂、實習、值班的日常長什麼樣？"},{"b":"S","c":"var(--m-green)","h":"Situation｜實況","p":"這個領域真實的狀況——課業、實作訓練、實際在做什麼？"},{"b":"B","c":"var(--m-yellow)","h":"Be Back｜重來","p":"如果回到高中，會給當時的自己、或給我們什麼建議？"}],"note":"其他想問的也都可以——直接把問題打在 Slido 上！（此處可放 Slido 畫面）"},
{"ch":"收尾","camp":"財經營","m":"午餐吃什麼？","type":"cover","art":"lunch","timer":30,"title":"午餐吃什麼？","sub":"趁午休前，先在聊天室或 Slido 上分享一下你今天想吃什麼、或推薦附近好吃的店家吧！"},
{"ch":"收尾","camp":"財經營","m":"午餐 · 1:30 回來","type":"cover","art":"lunch","music":true,"title":"午餐時間到！","sub":"記得先去吃飯、補充能量～ 下午 <span class=\"hl\">1:30 準時回來</span>！"},
];

const DENTAL_FLOW_START=SCENES.findIndex(s=>s.camp==='牙醫營');
const MATERIALS_FLOW_START=SCENES.findIndex(s=>s.camp==='材料營');
const BIZ_FLOW_START=SCENES.findIndex(s=>s.camp==='商管營');
const MED_FLOW_START=SCENES.findIndex(s=>s.camp==='醫學營');
const FIN_FLOW_START=SCENES.findIndex(s=>s.camp==='財經營');
/* 已經有內容／可以點進去的營隊，對照它們各自流程開始的場景索引 */
const IMPLEMENTED={
  '行銷營':{start:1},
  '牙醫營':{start:DENTAL_FLOW_START},
  '材料營':{start:MATERIALS_FLOW_START},
  '商管營':{start:BIZ_FLOW_START},
  '醫學營':{start:MED_FLOW_START},
  '財經營':{start:FIN_FLOW_START},
};


/* ===== 渲染 ===== */
const stage=document.getElementById('stage');
let idx=0,step=0,maxStep=0;
const artHTML=n=>n?`<div class="art">${I[n]||''}</div>`:'';

function homeHTML(){
  const cols=DEPTS.map(col=>`<div class="dcol"><div class="dhead">${col.g}</div>${
    col.items.map(name=>{const on=!!IMPLEMENTED[name];
      return `<button class="dept ${on?'active':'soon'}" data-dept="${name}">${name}</button>`}).join('')
  }</div>`).join('');
  return `<div class="scene">
    <div class="kicker">CIA 科系星球</div>
    <div class="title">選擇你今天要帶的<span class="hl">營隊</span></div>
    <div class="sub" style="font-size:clamp(15px,1.7vw,20px)">主持人：點選下方營隊進入課程（目前開放 <b style="color:var(--lemon)">行銷營、牙醫營、材料營、商管營、醫學營、財經營</b>，其餘陸續上線）</div>
    <div class="home-grid">${cols}</div>
    <div class="zoom-tip">畫面放大　Windows：Ctrl + ／ Mac：Command +　　畫面縮小　Windows：Ctrl - ／ Mac：Command -</div>
  </div>`;
}
function partHTML(s){
  return `<div class="scene">
    <div class="pe">${s.chLabel} · PART</div>
    <div class="pno">0${s.no}</div>
    <div class="plabel">${s.title}</div>
  </div>`;
}
function quizHTML(s){
  const opts=s.opts.map((t,i)=>`<div class="opt${i===s.ans?' correct':''}">
    <div class="react">${QEMO[i]}</div><div class="otext">${t}</div><div class="check">✓</div></div>`).join('');
  return `<div class="scene">
    <div class="kicker">${s.kicker}</div>${artHTML(s.art)}
    <div class="vote">選一個就好，用 Google Meet 表情符號投票（或打在聊天室）</div>
    <div class="q">${s.q}</div>
    <div class="options">${opts}</div>
    ${s.explain&&!s.noans?`<div class="explain" data-seq="1">${s.explain}</div>`:''}</div>`;
}
function scoreHTML(s){
  const opts=s.scoreOpts||SCORE;
  const cards=opts.map(o=>`<div class="scard ${o.c}"><div class="si">${o.i}</div><b>${o.s}</b><span>${o.t}</span></div>`).join('');
  return `<div class="scene">
    <div class="kicker">${s.kicker}</div>${artHTML(s.art)}
    <div class="q">${s.q}</div>
    <div class="semo" data-seq="1">${cards}</div>
    <div class="hint" data-seq="1">在 Google Meet 按下對應的表情符號，讓我們快速統計！</div></div>`;
}
function demoHTML(s){
  const cards=s.cards.map(c=>`<div class="gcard"><div class="gi">${I[c.i]||''}</div><h4>${c.h}</h4><p>${c.p}</p></div>`).join('');
  return `<div class="scene"><div class="kicker">${s.kicker}</div><div class="title">${s.title}</div>
    <div class="grid${s.four?' four':''}" data-seq="1">${cards}</div></div>`;
}
function frameHTML(s){
  const steps=s.steps.map((st,i)=>`<div class="step" data-seq="${i+1}"><div class="badge" style="background:${st.c}">${st.b}</div>
    <div class="stext"><h4>${st.h}</h4><p>${st.p}</p></div></div>`).join('');
  let seq=s.steps.length;
  if(s.shot) return `<div class="scene dense"><div class="kicker">${s.kicker}</div>
    <div class="title" style="font-size:clamp(22px,2.8vw,38px)">${s.title}</div>
    <div class="steps" style="max-width:860px;gap:8px">${steps}</div>
    <div class="shot sm" data-seq="${seq+1}"><img src="${s.shot}" alt="Notion 講義截圖"></div></div>`;
  const redbox=s.redbox?`<div class="redbox" data-seq="${++seq}"><span class="rl">紅框範例</span>${s.redbox}</div>`:'';
  const note=s.note?`<div class="slido-note" data-seq="${++seq}">${s.note}</div>`:'';
  const shotph=s.shotPlaceholder?`<div class="shot shotph"><div class="shotph-box">📷 截圖預留區</div></div>`:'';
  const timerBlock=s.timer?timerWidgetHTML(s.timer,s.noMusic,true):'';
  return `<div class="scene${s.shotPlaceholder||s.timer?' dense':''}"><div class="kicker">${s.kicker}</div>${artHTML(s.art)}
    <div class="title">${s.title}</div><div class="steps">${steps}</div>${redbox}${note}${shotph}${timerBlock}</div>`;
}
function fmtSec(total){const m=Math.floor(total/60),sec=total%60;return `${String(m).padStart(2,'0')}:${String(sec).padStart(2,'0')}`;}
function timerWidgetHTML(seconds,noMusic,directInput){
  seconds=seconds||600;
  const resetLabel=seconds<60?`${seconds} 秒`:`${Math.round(seconds/60)} 分鐘`;
  return `<div class="break-wrap">
      <div class="timer-card">
        <div class="timer-digits" id="tmDigits">${fmtSec(seconds)}</div>
        <div class="timer-btns">
          <button class="tbtn" id="tmMinus" type="button">−1 分</button>
          <button class="tbtn tbtn-main" id="tmToggle" type="button">▶ 開始</button>
          <button class="tbtn" id="tmPlus" type="button">+1 分</button>
        </div>
        <button class="tbtn tbtn-ghost" id="tmReset" type="button">重設為 ${resetLabel}</button>
        ${directInput?`<div class="timer-set">
          <input type="number" id="tmInput" min="1" max="120" placeholder="分鐘">
          <button class="tbtn" id="tmSetBtn" type="button">設定</button>
        </div>`:''}
      </div>
      ${noMusic?'':`<div class="music-card">
        <div class="music-row"><button class="music-btn${mzPlaying?' playing':''}" id="mzToggle" type="button"><span class="mb-ic">🎵</span><span class="mb-label">${mzPlaying?'音樂播放中 · 點我暫停':'點我播放音樂'}</span></button></div>
        <div class="prog-row"><span id="mzElapsed">${fmtSec(getElapsedSeconds())}</span><input type="range" id="mzSeek" min="0" max="1000" value="0"><span id="mzDuration">00:00</span></div>
        <div class="music-row"><div class="vol-box"><span class="vol-ic">🔊</span><input type="range" class="vol-slider" id="mzVol" min="0" max="100" value="${mzVolPercent}"></div></div>
        <div class="music-hint">單曲循環播放，全站共用進度</div>
      </div>`}
    </div>`;
}
function breakHTML(s){
  return `<div class="scene">${s.kicker?`<div class="kicker">${s.kicker}</div>`:''}${artHTML(s.art)}
    <div class="title">${s.title}</div>${s.sub?`<div class="sub">${s.sub}</div>`:''}
    ${timerWidgetHTML(s.timer||600,false,true)}</div>`;
}
function musicOnlyHTML(){
  return `<div class="break-wrap" style="max-width:260px">
    <div class="music-card" style="max-width:100%">
      <div class="music-row"><button class="music-btn${mzPlaying?' playing':''}" id="mzToggle" type="button"><span class="mb-ic">🎵</span><span class="mb-label">${mzPlaying?'音樂播放中 · 點我暫停':(ytReady?'點我播放音樂':'音樂載入中…')}</span></button></div>
      <div class="prog-row"><span id="mzElapsed">${fmtSec(getElapsedSeconds())}</span><input type="range" id="mzSeek" min="0" max="1000" value="0"><span id="mzDuration">00:00</span></div>
      <div class="music-row"><div class="vol-box"><span class="vol-ic">🔊</span><input type="range" class="vol-slider" id="mzVol" min="0" max="100" value="${mzVolPercent}"></div></div>
      <div class="music-hint">單曲循環播放，全站共用進度</div>
    </div>
  </div>`;
}
function coverHTML(s){
  if(s.shot){
    const side=s.timer?timerWidgetHTML(s.timer,s.noMusic,true):(s.music?musicOnlyHTML():'');
    return `<div class="scene">${s.kicker?`<div class="kicker">${s.kicker}</div>`:''}
    <div class="title">${s.title}</div>${s.sub?`<div class="sub">${s.sub}</div>`:''}
    <div class="shotcap">👉 這是你講義裡對應的區塊</div>
    <div class="shot"${s.shotMaxWidth?` style="max-width:${s.shotMaxWidth}"`:''}><img src="${s.shot}" alt="Notion 講義截圖"></div>
    ${side}</div>`;
  }
  if(s.shotPlaceholder){
    const side=s.timer?timerWidgetHTML(s.timer,s.noMusic,true):(s.music?musicOnlyHTML():'');
    return `<div class="scene">${s.kicker?`<div class="kicker">${s.kicker}</div>`:''}
    <div class="title">${s.title}</div>${s.sub?`<div class="sub">${s.sub}</div>`:''}
    <div class="shot shotph"><div class="shotph-box">📷 截圖預留區</div>${s.footnote?`<div class="shotfoot" style="font-size:clamp(14px,1.6vw,20px)">${s.footnote}</div>`:''}</div>
    ${side}</div>`;
  }
  return `<div class="scene">${s.kicker?`<div class="kicker">${s.kicker}</div>`:''}${artHTML(s.art)}
    <div class="title">${s.title}</div>${s.sub?`<div class="sub" data-seq="1">${s.sub}</div>`:''}
    ${s.timer?timerWidgetHTML(s.timer,s.noMusic,true):(s.music?musicOnlyHTML():'')}</div>`;
}
function rawHTML(s){
  return `<div class="scene">${s.html}${s.timerInline?'':(s.timer?timerWidgetHTML(s.timer,false,true):(s.music?musicOnlyHTML():''))}</div>`;
}
function build(s){
  switch(s.type){
    case 'home': return homeHTML();
    case 'part': return partHTML(s);
    case 'quiz': return quizHTML(s);
    case 'score': return scoreHTML(s);
    case 'demo': return demoHTML(s);
    case 'frame': return frameHTML(s);
    case 'break': return breakHTML(s);
    case 'raw': return rawHTML(s);
    default: return coverHTML(s);
  }
}

const STAGES=[
  {key:'開場暖身',label:'開場暖身',time:'08:30'},
  {key:'科系所學',label:'科系所學',time:'09:00'},
  {key:'未來發展',label:'未來發展',time:'10:45'},
  {key:'午餐',label:'午餐',time:'12:30'},
  {key:'實際操作',label:'實際操作',time:'13:30'},
  {key:'學長姐分享',label:'學長姐分享',time:'16:10'},
  {key:'自主反思',label:'自主反思',time:'17:10'},
  {key:'學習反思',label:'',time:'18:30'},
];
function getStageIndex(s){
  if(s.ch==='學習反思')return 7;
  if(s.ch==='學長姐分享')return 5;
  if(s.ch==='開場暖身')return 0;
  if(s.ch==='科系所學')return s.p==='Part 3'?6:1;
  if(s.ch==='未來發展')return 2;
  if(s.ch==='收尾')return 3;
  if(s.ch==='實際操作')return 4;
  return -1;
}
function renderStageBar(s){
  const bar=document.getElementById('stageBar');
  if(!bar)return;
  if(s.type==='home'){bar.innerHTML='';return;}
  const cur=getStageIndex(s);
  let html='<div class="sb-row">';
  STAGES.forEach((st,i)=>{
    const dotState=cur<0?'':(i<cur?'done':(i===cur?'active':''));
    html+=`<div class="sb-dotcol"><div class="sb-dot ${dotState}"></div><div class="sb-time ${dotState}">${st.time}</div></div>`;
    if(i<STAGES.length-1){
      const segState=cur<0?'':(i<cur?'done':(i===cur?'active':''));
      html+=`<div class="sb-seg ${segState}"><span class="sb-seglabel">${st.label}</span><div class="sb-segline"></div></div>`;
    }else{
      html+=`<div class="sb-seg sb-seg-end"><span class="sb-seglabel">${st.label}</span></div>`;
    }
  });
  html+='</div>';
  bar.innerHTML=html;
}
function render(){
  const s={...SCENES[idx]}; if(typeof SHOTS!=="undefined"&&SHOTS[idx]&&!s.noShot)s.shot=SHOTS[idx];
  stage.innerHTML=build(s);
  const sc=stage.querySelector('.scene');
  if(sc&&(s.type==='quiz'||s.type==='frame'))sc.classList.add('dense');
  if(s.type==='home'){currentCamp=null;stage.querySelectorAll('.dept').forEach(b=>b.onclick=e=>{e.stopPropagation();pickDept(b.dataset.dept);});}
  if(s.type==='break') bindBreak(s.timer||600); else if(s.timer) bindBreak(s.timer); else if(s.music) bindMusicOnly();
  const seqs=[...stage.querySelectorAll('[data-seq]')].map(e=>+e.dataset.seq);
  maxStep=seqs.length?Math.max(...seqs):0;step=0;applyStep();
  document.getElementById('chapter').textContent=s.type==='home'?'選擇營隊':(s.p?s.ch+' · '+s.p:s.ch);
}
function applyStep(){
  stage.querySelectorAll('[data-seq]').forEach(e=>e.classList.toggle('on',+e.dataset.seq<=step));
  const o=stage.querySelector('.options');if(o)o.classList.toggle('revealed',step>=1);
}
function next(){
  if(step<maxStep){step++;applyStep();return;}
  const cur=SCENES[idx];
  if(cur.ch==='開場暖身'){
    const isLastOpening=!SCENES[idx+1]||SCENES[idx+1].ch!=='開場暖身';
    if(isLastOpening){const targetCamp=currentCamp||'行銷營';if(IMPLEMENTED[targetCamp]){currentCamp=targetCamp;goto(IMPLEMENTED[targetCamp].start);return;}}
  }
  if(idx<SCENES.length-1)goto(idx+1);
}
function prev(){if(step>0){step--;applyStep();return;}if(idx>0)goto(idx-1);}
function goto(n){
  const cur=SCENES[idx];
  if(cur.type==='break'||cur.timer)cleanupBreak();
  const fade=document.getElementById('fade');stage.classList.add('swap');fade.style.opacity='1';
  setTimeout(()=>{idx=Math.max(0,Math.min(SCENES.length-1,n));render();stage.classList.remove('swap');fade.style.opacity='0';},180);
}
function pickDept(name){
  if(IMPLEMENTED[name]){currentCamp=name;goto(IMPLEMENTED[name].start);}else{showSoon(name);}
}

/* ===== 倒數計時器（每頁獨立）+ 背景音樂（YouTube，全站共用同一個播放器、進度不重置）===== */
let tmSeconds=600,tmInterval=null,tmRunning=false;
const YT_VIDEO_ID='GSAI6bnf25A'; /* 使用者指定的影片，單曲循環播放（用 YouTube 官方嵌入播放器，非下載檔案） */
let ytPlayer=null,ytReady=false,ytPendingPlay=false;
let mzPlaying=false,mzVolPercent=45;
(function loadYT(){
  const tag=document.createElement('script');tag.src='https://www.youtube.com/iframe_api';
  document.head.appendChild(tag);
})();
window.onYouTubeIframeAPIReady=function(){
  ytPlayer=new YT.Player('ytPlayer',{
    height:'1',width:'1',videoId:YT_VIDEO_ID,
    playerVars:{autoplay:0,controls:0,disablekb:1,fs:0,iv_load_policy:3,modestbranding:1,rel:0,
      playsinline:1,loop:1,playlist:YT_VIDEO_ID},
    events:{
      onReady:()=>{ytReady=true;ytPlayer.setVolume(mzVolPercent);
        if(ytPendingPlay){ytPlayer.playVideo();ytPendingPlay=false;} syncMusicUI();},
      onStateChange:e=>{
        if(e.data===YT.PlayerState.PLAYING)mzPlaying=true;
        else if(e.data===YT.PlayerState.PAUSED||e.data===YT.PlayerState.ENDED)mzPlaying=false;
        syncMusicUI();
      },
      onError:()=>{ /* 清單裡若有某首影片被上傳者關閉嵌入播放，自動跳到下一首，不讓整個播放卡住 */
        if(ytPlayer&&ytPlayer.nextVideo)ytPlayer.nextVideo();
      }
    }
  });
};
function playTimerChime(){
  try{
    const ctx=new (window.AudioContext||window.webkitAudioContext)();
    /* 「叮昤」小鈴鐺音效：快速兩聲上揚高音，帶泛音，聽起來清脆帶點鈴鐺的殘響感 */
    const notes=[{freq:1567.98,t:0,vol:.3},{freq:2093.00,t:.11,vol:.26}]; /* G6 → C7 */
    notes.forEach(n=>{
      const t0=ctx.currentTime+n.t;
      const o=ctx.createOscillator();o.type='sine';o.frequency.value=n.freq;
      const o2=ctx.createOscillator();o2.type='triangle';o2.frequency.value=n.freq*2; /* 高八度泛音，增加鈴鐺感 */
      const g=ctx.createGain();g.gain.setValueAtTime(0,t0);
      g.gain.linearRampToValueAtTime(n.vol,t0+.006);
      g.gain.exponentialRampToValueAtTime(.001,t0+.75);
      const g2=ctx.createGain();g2.gain.setValueAtTime(0,t0);
      g2.gain.linearRampToValueAtTime(n.vol*.3,t0+.006);
      g2.gain.exponentialRampToValueAtTime(.001,t0+.45);
      o.connect(g);g.connect(ctx.destination);
      o2.connect(g2);g2.connect(ctx.destination);
      o.start(t0);o.stop(t0+.8);o2.start(t0);o2.stop(t0+.5);
    });
    setTimeout(()=>ctx.close(),1200);
  }catch(err){}
}
function bindBreak(initialSeconds){
  initialSeconds=initialSeconds||600;
  tmSeconds=initialSeconds;tmRunning=false;
  const digits=stage.querySelector('#tmDigits'),toggleBtn=stage.querySelector('#tmToggle'),
    minusBtn=stage.querySelector('#tmMinus'),plusBtn=stage.querySelector('#tmPlus'),
    resetBtn=stage.querySelector('#tmReset'),mzBtn=stage.querySelector('#mzToggle'),mzVol=stage.querySelector('#mzVol'),
    tmInput=stage.querySelector('#tmInput'),tmSetBtn=stage.querySelector('#tmSetBtn');
  const fmt=()=>{digits.textContent=fmtSec(tmSeconds);};
  fmt();
  const tick=()=>{if(tmSeconds>0){tmSeconds--;fmt();}
    if(tmSeconds<=0){stopTimer();digits.textContent='00:00';toggleBtn.textContent='▶ 開始';playTimerChime();}};
  const startTimer=()=>{if(tmInterval)return;tmInterval=setInterval(tick,1000);tmRunning=true;toggleBtn.textContent='⏸ 暫停';};
  const stopTimer=()=>{clearInterval(tmInterval);tmInterval=null;tmRunning=false;};
  toggleBtn.onclick=e=>{e.stopPropagation();if(tmRunning){stopTimer();toggleBtn.textContent='▶ 開始';}else{startTimer();}};
  minusBtn.onclick=e=>{e.stopPropagation();stopTimer();toggleBtn.textContent='▶ 開始';tmSeconds=Math.max(60,tmSeconds-60);fmt();};
  plusBtn.onclick=e=>{e.stopPropagation();tmSeconds=Math.min(3600,tmSeconds+60);fmt();};
  resetBtn.onclick=e=>{e.stopPropagation();stopTimer();tmSeconds=initialSeconds;fmt();toggleBtn.textContent='▶ 開始';};
  if(tmInput&&tmSetBtn){
    const applyInput=e=>{e.stopPropagation();const mins=Math.round(+tmInput.value);
      if(!mins||mins<1)return;
      stopTimer();toggleBtn.textContent='▶ 開始';
      tmSeconds=Math.min(7200,mins*60);fmt();tmInput.value='';};
    tmSetBtn.onclick=applyInput;
    tmInput.onclick=e=>e.stopPropagation();
    tmInput.onkeydown=e=>{e.stopPropagation();if(e.key==='Enter')applyInput(e);};
  }
  if(mzBtn){mzBtn.onclick=e=>{e.stopPropagation();mzPlaying?pauseMusic():startMusic();};}
  if(mzVol){mzVol.oninput=e=>{mzVolPercent=+e.target.value;if(ytReady&&ytPlayer)ytPlayer.setVolume(mzVolPercent);};}
  if(mzBtn)syncMusicUI(); /* 進入頁面時，把按鈕文字/已播放時間同步成全站目前的實際狀態（沒有音樂卡片的頁面就略過） */
}
function startMusic(){
  if(ytReady&&ytPlayer){ytPlayer.playVideo();}else{ytPendingPlay=true;}
}
function pauseMusic(){ /* 暫停：YouTube 播放器本身會記住播放位置，不用自己計算進度 */
  ytPendingPlay=false;
  if(ytReady&&ytPlayer)ytPlayer.pauseVideo();
  mzPlaying=false;syncMusicUI();
}
function bindMusicOnly(){
  const mzBtn=stage.querySelector('#mzToggle'),mzVol=stage.querySelector('#mzVol');
  if(mzBtn)mzBtn.onclick=e=>{e.stopPropagation();mzPlaying?pauseMusic():startMusic();};
  if(mzVol)mzVol.oninput=e=>{mzVolPercent=+e.target.value;if(ytReady&&ytPlayer)ytPlayer.setVolume(mzVolPercent);};
  syncMusicUI();
}
function getElapsedSeconds(){
  return (ytReady&&ytPlayer&&ytPlayer.getCurrentTime)?Math.floor(ytPlayer.getCurrentTime()):0;
}
function getDurationSeconds(){
  return (ytReady&&ytPlayer&&ytPlayer.getDuration)?Math.floor(ytPlayer.getDuration()):0;
}
function updateProgressUI(){
  const elapsed=getElapsedSeconds(),duration=getDurationSeconds();
  const elEl=stage.querySelector('#mzElapsed');if(elEl)elEl.textContent=fmtSec(elapsed);
  const durEl=stage.querySelector('#mzDuration');if(durEl)durEl.textContent=fmtSec(duration);
  const seek=stage.querySelector('#mzSeek');
  if(seek&&document.activeElement!==seek){seek.value=duration>0?Math.round((elapsed/duration)*1000):0;}
}
function syncMusicUI(){
  const btn=stage.querySelector('#mzToggle');
  if(btn)btn.textContent=mzPlaying?'⏸ 暫停音樂':(ytReady?'🎵 播放背景音樂':'🎵 音樂載入中…');
  const seek=stage.querySelector('#mzSeek');
  if(seek){
    seek.onclick=e=>e.stopPropagation();
    seek.oninput=e=>{const durEl=stage.querySelector('#mzDuration');const elEl=stage.querySelector('#mzElapsed');
      const duration=getDurationSeconds();const target=duration*(+e.target.value/1000);
      if(elEl)elEl.textContent=fmtSec(Math.floor(target));};
    seek.onchange=e=>{const duration=getDurationSeconds();if(!duration||!ytReady||!ytPlayer)return;
      const target=duration*(+e.target.value/1000);ytPlayer.seekTo(target,true);};
  }
  updateProgressUI();
}
setInterval(updateProgressUI,1000);
function cleanupBreak(){ /* 只清掉「這一頁」的倒數計時器，背景音樂（YouTube播放器）維持全站共用、不中斷 */
  if(tmInterval){clearInterval(tmInterval);tmInterval=null;}
  tmRunning=false;
}


/* ===== 操作 ===== */
const anyOverlayOpen=()=>document.querySelector('.overlay.open');
document.addEventListener('keydown',e=>{
  if(anyOverlayOpen()){if(e.key==='Escape')closeOverlays();return;}
  if(e.key==='ArrowRight'||e.key===' '||e.key==='Enter'){e.preventDefault();next();}
  else if(e.key==='ArrowLeft'){e.preventDefault();prev();}
  else if(e.key==='m'||e.key==='M')openMenu();
  else if(e.key==='h'||e.key==='H')goto(0);
  else if(e.key==='f'||e.key==='F')toggleFull();
});
stage.addEventListener('click',e=>{
  if(SCENES[idx].type==='home')return;        /* 主頁不靠點畫面前進，避免誤跳 */
  if(e.clientX/window.innerWidth<0.25)prev();else next();
});
function toggleFull(){if(!document.fullscreenElement)document.documentElement.requestFullscreen?.();else document.exitFullscreen?.();}

/* ===== 章節選單（分類 → Part → 逐頁）===== */
const menu=document.getElementById('menu');
/* 科系所學：選單上把原本的 Part 2-5 併為「Part 2」、Part 6-8 併為「Part 3」（不影響簡報本身的 Part 轉場頁） */
const DEPT1_PART_MAP={
  'Part 1':'Part 1',
  'Part 2':'Part 2','Part 3':'Part 2','Part 4':'Part 2','Part 5':'Part 2',
  'Part 6':'Part 3','Part 7':'Part 3','Part 8':'Part 3',
};
const MENU_GROUPS=[
  {key:'openingWarmup',label:'開場暖身',match:s=>s.ch==='開場暖身',hasParts:false,camp:null,session:'am',block:'main'},
  {key:'dept1',label:'科系所學',match:s=>s.ch==='科系所學'&&!s.camp&&!!s.p,hasParts:true,camp:'行銷營',session:'am',block:'main'},
  {key:'dept2',label:'未來發展',match:s=>s.ch==='未來發展'&&!s.camp,hasParts:true,camp:'行銷營',session:'am',block:'main'},
  {key:'end',label:'午餐互動',match:s=>s.ch==='收尾'&&!s.camp,hasParts:false,camp:'行銷營',session:'am',block:'end'},
  {key:'dent1',label:'科系所學',match:s=>s.ch==='科系所學'&&s.camp==='牙醫營'&&!!s.p,hasParts:true,camp:'牙醫營',session:'am',block:'main'},
  {key:'dent2',label:'未來發展',match:s=>s.ch==='未來發展'&&s.camp==='牙醫營',hasParts:true,camp:'牙醫營',session:'am',block:'main'},
  {key:'dentend',label:'午餐互動',match:s=>s.ch==='收尾'&&s.camp==='牙醫營',hasParts:false,camp:'牙醫營',session:'am',block:'end'},
  {key:'dent3',label:'實際操作',match:s=>s.ch==='實際操作'&&s.camp==='牙醫營',hasParts:true,camp:'牙醫營',session:'pm',block:'main'},
  {key:'mat1',label:'科系所學',match:s=>s.ch==='科系所學'&&s.camp==='材料營'&&!!s.p,hasParts:true,camp:'材料營',session:'am',block:'main'},
  {key:'mat2',label:'未來發展',match:s=>s.ch==='未來發展'&&s.camp==='材料營',hasParts:true,camp:'材料營',session:'am',block:'main'},
  {key:'matend',label:'午餐互動',match:s=>s.ch==='收尾'&&s.camp==='材料營',hasParts:false,camp:'材料營',session:'am',block:'end'},
  {key:'mat3',label:'實際操作',match:s=>s.ch==='實際操作'&&s.camp==='材料營',hasParts:true,camp:'材料營',session:'pm',block:'main'},
  {key:'biz1',label:'科系所學',match:s=>s.ch==='科系所學'&&s.camp==='商管營'&&!!s.p,hasParts:true,camp:'商管營',session:'am',block:'main'},
  {key:'biz2',label:'未來發展',match:s=>s.ch==='未來發展'&&s.camp==='商管營',hasParts:true,camp:'商管營',session:'am',block:'main'},
  {key:'bizend',label:'午餐互動',match:s=>s.ch==='收尾'&&s.camp==='商管營',hasParts:false,camp:'商管營',session:'am',block:'end'},
  {key:'biz3',label:'實際操作',match:s=>s.ch==='實際操作'&&s.camp==='商管營',hasParts:true,camp:'商管營',session:'pm',block:'main'},
  {key:'med1',label:'科系所學',match:s=>s.ch==='科系所學'&&s.camp==='醫學營'&&!!s.p,hasParts:true,camp:'醫學營',session:'am',block:'main'},
  {key:'med2',label:'未來發展',match:s=>s.ch==='未來發展'&&s.camp==='醫學營',hasParts:true,camp:'醫學營',session:'am',block:'main'},
  {key:'medend',label:'午餐互動',match:s=>s.ch==='收尾'&&s.camp==='醫學營',hasParts:false,camp:'醫學營',session:'am',block:'end'},
  {key:'med3',label:'實際操作',match:s=>s.ch==='實際操作'&&s.camp==='醫學營',hasParts:true,camp:'醫學營',session:'pm',block:'main'},
  {key:'fin1',label:'科系所學',match:s=>s.ch==='科系所學'&&s.camp==='財經營'&&!!s.p,hasParts:true,camp:'財經營',session:'am',block:'main'},
  {key:'fin2',label:'未來發展',match:s=>s.ch==='未來發展'&&s.camp==='財經營',hasParts:true,camp:'財經營',session:'am',block:'main'},
  {key:'finend',label:'午餐互動',match:s=>s.ch==='收尾'&&s.camp==='財經營',hasParts:false,camp:'財經營',session:'am',block:'end'},
  {key:'fin3',label:'實際操作',match:s=>s.ch==='實際操作'&&s.camp==='財經營',hasParts:true,camp:'財經營',session:'pm',block:'main'},
  {key:'seniorShare',label:'學長姐分享',match:s=>s.ch==='學長姐分享',hasParts:false,camp:null,session:'pm',block:'main'},
  {key:'campClosing',label:'學習反思',match:s=>s.ch==='學習反思',hasParts:false,camp:null,session:'pm',block:'main'},
  /* 其他：休息、互動各自獨立成一個只有單頁的分類 */
];
function visibleMenuGroups(){return MENU_GROUPS.filter(g=>!g.camp||g.camp===currentCamp);}
function groupItems(g){return SCENES.map((s,i)=>({s,i})).filter(o=>g.match(o.s));}
function groupParts(g){
  const map=new Map();
  groupItems(g).forEach(({s,i})=>{
    const key=(g.partKeyFn?g.partKeyFn(s.p):s.p)||'總覽';
    if(!map.has(key))map.set(key,[]);
    map.get(key).push({s,i});
  });
  return map;
}
let menuSel={groupKey:null,partKey:null};
function campPageNumberMap(camp){
  const map=new Map();let n=0;
  MENU_GROUPS.filter(g=>!g.camp||g.camp===camp).forEach(g=>{
    if(g.hasParts){
      const parts=groupParts(g);
      parts.forEach(items=>{items.forEach(({i})=>{if(!map.has(i)){n++;map.set(i,String(n).padStart(2,'0'));}});});
    }else{
      groupItems(g).forEach(({i})=>{if(!map.has(i)){n++;map.set(i,String(n).padStart(2,'0'));}});
    }
  });
  return map;
}
function renderMenu(){
  const groups=visibleMenuGroups();
  const dentNum=currentCamp?campPageNumberMap(currentCamp):null;
  const sessionLabel={am:'早場',pm:'晚場',other:'其他'};
  let col1='';let lastSession=null,firstSession=true;
  groups.forEach(g=>{
    if(g.session!==lastSession){
      col1+=`<div class="msession${firstSession?'':' pmsession'}">${sessionLabel[g.session]||''}</div>`;
      firstSession=false;
    }
    lastSession=g.session;
    const sel=g.key===menuSel.groupKey;
    col1+=`<button class="mitem mfolder${sel?' sel':''}" data-open-group="${g.key}"><span class="pg">📁</span><span>${g.label}</span></button>`;
  });
  let html=`<div class="mcol"><div class="mcolhead">分類</div>${col1}</div>`;

  const curGroup=groups.find(g=>g.key===menuSel.groupKey);
  if(curGroup){
    if(curGroup.hasParts){
      const parts=groupParts(curGroup);
      html+=`<div class="mcol"><div class="mcolhead">${curGroup.label} · Part</div>${
        [...parts.keys()].map(k=>{
          const sel=k===menuSel.partKey;
          return `<button class="mitem mfolder${sel?' sel':''}" data-open-part="${k}"><span class="pg">${k}</span></button>`;
        }).join('')
      }</div>`;
      if(menuSel.partKey&&parts.has(menuSel.partKey)){
        html+=`<div class="mcol"><div class="mcolhead">${menuSel.partKey} · 頁碼</div>${
          parts.get(menuSel.partKey).map(({s,i})=>{
            const pg=i===0?'主頁':(dentNum&&dentNum.has(i)?dentNum.get(i):`P${i}`);
            return `<button class="mitem" data-go="${i}"><span class="pg">${pg}</span><span>${s.m}</span></button>`;
          }).join('')
        }</div>`;
      }
    }else{
      const items=groupItems(curGroup);
      html+=`<div class="mcol"><div class="mcolhead">${curGroup.label} · 頁碼</div>${
        items.map(({s,i})=>{
          const pg=i===0?'主頁':(dentNum&&dentNum.has(i)?dentNum.get(i):`P${i}`);
          return `<button class="mitem" data-go="${i}"><span class="pg">${pg}</span><span>${s.m}</span></button>`;
        }).join('')
      }</div>`;
    }
  }
  document.getElementById('menuList').innerHTML=html;
  bindMenuEvents();
}
function bindMenuEvents(){
  menu.querySelectorAll('.mitem[data-go]').forEach(b=>b.onclick=()=>{closeOverlays();goto(+b.dataset.go);});
  menu.querySelectorAll('[data-open-group]').forEach(b=>b.onclick=()=>{
    const key=b.dataset.openGroup;
    const g=visibleMenuGroups().find(x=>x.key===key);
    if(g&&!g.hasParts){
      const items=groupItems(g);
      if(items.length===1){closeOverlays();goto(items[0].i);return;}
    }
    menuSel=(menuSel.groupKey===key)?{groupKey:null,partKey:null}:{groupKey:key,partKey:null};
    renderMenu();
  });
  menu.querySelectorAll('[data-open-part]').forEach(b=>b.onclick=()=>{
    const key=b.dataset.openPart;
    menuSel.partKey=(menuSel.partKey===key)?null:key;
    renderMenu();
  });
}
function openMenu(){menuSel={groupKey:null,partKey:null};renderMenu();menu.classList.add('open');}
function closeOverlays(){document.querySelectorAll('.overlay').forEach(o=>o.classList.remove('open'));}
document.getElementById('menuBtn').onclick=openMenu;
document.getElementById('menuClose').onclick=closeOverlays;
document.getElementById('homeBtn').onclick=()=>goto(0);
menu.addEventListener('click',e=>{if(e.target===menu)closeOverlays();});

/* ===== 準備中彈窗 ===== */
const soon=document.getElementById('soon');
function showSoon(name){
  document.getElementById('soonTitle').textContent=name+' · 內容準備中';
  document.getElementById('soonMsg').textContent='這個營隊的課程我們之後再一起完成 🚧　今天可以先體驗「行銷營」與「牙醫營」的完整流程。';
  soon.classList.add('open');
}
document.getElementById('soonClose').onclick=closeOverlays;
document.getElementById('soonBack').onclick=()=>{closeOverlays();goto(0);};
soon.addEventListener('click',e=>{if(e.target===soon)closeOverlays();});

/* ===== 星空 ===== */
(function(){let h='';for(let i=0;i<120;i++){const s=(Math.random()*2+0.6).toFixed(1);
  h+=`<span class="star" style="left:${(Math.random()*100).toFixed(2)}%;top:${(Math.random()*100).toFixed(2)}%;width:${s}px;height:${s}px;animation-delay:${(Math.random()*4).toFixed(1)}s"></span>`;}
  document.getElementById('stars').innerHTML=h;})();

/* ===== 背景小彩蛋 ===== */
const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;
const EGGSVG={
 meteor:`<svg viewBox="0 0 60 30"><line x1="6" y1="24" x2="40" y2="6" stroke="#FFE873" stroke-width="2.4" stroke-linecap="round"/><circle cx="42" cy="5" r="3.4" fill="#fff"/></svg>`,
 rock:`<svg viewBox="0 0 40 40"><path d="M8 22l4-10 12-4 8 8-4 14-14 2Z" fill="rgba(180,185,210,.5)" stroke="rgba(220,225,255,.5)" stroke-width="1.5"/></svg>`,
 ship:`<svg viewBox="0 0 70 34"><path d="M6 18h40l16-8-10 16H10Z" fill="rgba(61,123,224,.45)" stroke="#FFE873" stroke-width="1.6"/><circle cx="40" cy="15" r="3" fill="#fff"/></svg>`,
 ufo:`<svg viewBox="0 0 60 40"><ellipse cx="30" cy="24" rx="22" ry="7" fill="rgba(120,90,255,.45)" stroke="#FFE873" stroke-width="1.4"/><path d="M18 22a12 8 0 0 1 24 0Z" fill="rgba(200,210,255,.55)"/><circle cx="30" cy="16" r="2.4" fill="#0a0e2e"/></svg>`,
};
function spawnEgg(){
  if(reduce)return;
  const layer=document.getElementById('egg');const ks=Object.keys(EGGSVG);const t=ks[Math.floor(Math.random()*ks.length)];
  const el=document.createElement('div');el.className='egg';el.innerHTML=EGGSVG[t];
  const top=(Math.random()<.5?Math.random()*32:70+Math.random()*22);
  const size=t==='meteor'?(30+Math.random()*26):(22+Math.random()*30);const dir=Math.random()<.5?1:-1;
  el.style.top=top+'%';el.style.width=size+'px';el.style.opacity='0';el.style.transform=`scaleX(${dir})`;
  el.style.left=dir>0?'-8%':'108%';layer.appendChild(el);
  const dur=t==='meteor'?(7+Math.random()*4):(22+Math.random()*16);const endX=dir>0?'116%':'-16%';
  el.animate([{left:el.style.left,opacity:0},{opacity:.5,offset:.15},{opacity:.45,offset:.85},{left:endX,opacity:0}],
    {duration:dur*1000,easing:'linear'}).onfinish=()=>el.remove();
}
setTimeout(function loop(){spawnEgg();setTimeout(loop,(9+Math.random()*13)*1000);},6000);

render();
</script>
</body>
</html>
