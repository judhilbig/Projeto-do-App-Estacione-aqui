# Projeto-do-App-Estacione-aqui
Projeto da interface de um App para vagas de estacionar/faculdade-Bsi
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Estacione Aqui - Arrumado</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
* { margin:0; padding:0; box-sizing:border-box; }
:root {
  --blue:#1a56db; --blue-dark:#1240a8; --blue-light:#e8f0fe;
  --green:#16a34a; --red:#dc2626; --yellow:#d97706;
  --bg:#f4f5f9; --white:#ffffff; --text:#111827; --sub:#6b7280; --border:#e5e7eb;
}
body { background:#1a1a2e; display:flex; justify-content:center; align-items:center; min-height:100vh; font-family:'Poppins',sans-serif; }

.phone {
  width:375px; height:812px; background:var(--bg);
  border-radius:50px;
  box-shadow: 0 0 0 2px #2a2a4a, 0 0 0 6px #111128, 0 0 0 8px #2a2a4a, 0 40px 80px rgba(0,0,0,.8);
  overflow:hidden; position:relative; display:flex; flex-direction:column;
}
.notch { position:absolute; top:0; left:50%; transform:translateX(-50%); width:126px; height:30px; border-radius:0 0 20px 20px; z-index:200; background:#0d1628; }
.status-bar {
  height:44px; display:flex; align-items:center; justify-content:space-between;
  padding:12px 28px 0; position:absolute; top:0; left:0; right:0; z-index:100; pointer-events:none;
}
.status-time { font-size:15px; font-weight:700; color:#fff; }
.status-icons { display:flex; gap:6px; align-items:center; }
.status-icons svg { fill:#fff; }
.status-bar.dk .status-time { color:var(--text); }
.status-bar.dk .status-icons svg { fill:var(--text); }

.app { flex:1; display:flex; flex-direction:column; overflow:hidden; position:relative; }

.screen {
  position:absolute; inset:0; display:flex; flex-direction:column;
  transition: transform .38s cubic-bezier(.4,0,.2,1), opacity .38s ease;
  transform:translateX(100%); opacity:0; pointer-events:none;
}
.screen.active { transform:translateX(0); opacity:1; pointer-events:auto; }
.screen.gone { transform:translateX(-40px); opacity:0; pointer-events:none; }

/* ── SPLASH ── */
#s-splash { background:linear-gradient(165deg,#0d1628 0%,#162e6e 55%,#0d1628 100%); align-items:center; justify-content:center; }
.orb { position:absolute; border-radius:50%; background:radial-gradient(circle,rgba(26,86,219,.3),transparent 70%); animation:flt 7s ease-in-out infinite; }
@keyframes flt{0%,100%{transform:translate(0,0);}50%{transform:translate(12px,-18px);}}
.logo-wrap { display:flex; flex-direction:column; align-items:center; gap:22px; animation:fup .9s ease both; }
@keyframes fup{from{opacity:0;transform:translateY(28px);}to{opacity:1;transform:translateY(0);}}
.logo-circle { width:130px; height:130px; border-radius:50%; border:2.5px solid rgba(255,255,255,.2); background:rgba(255,255,255,.06); display:flex; align-items:center; justify-content:center; box-shadow:0 0 70px rgba(26,86,219,.45); position:relative; }
.logo-ring { position:absolute; inset:-7px; border-radius:50%; border:3px solid var(--blue); opacity:.8; animation:spin 8s linear infinite; border-top-color:transparent; border-right-color:transparent; }
@keyframes spin{to{transform:rotate(360deg);}}
.logo-inner { width:104px; height:104px; border-radius:50%; background:white; display:flex; align-items:center; justify-content:center; box-shadow:0 8px 30px rgba(0,0,0,.35); }
.big-e { font-size:58px; font-weight:900; color:var(--blue); line-height:1; font-family:'Poppins',sans-serif; }
.brand-main { font-size:30px; font-weight:900; color:#fff; letter-spacing:3px; text-transform:uppercase; font-family:'Nunito',sans-serif; text-align:center; }
.brand-sub { font-size:12px; color:rgba(255,255,255,.5); letter-spacing:2px; text-align:center; margin-top:4px; }
.splash-cta {
  position:absolute; bottom:80px; left:30px; right:30px;
  background:linear-gradient(135deg,var(--blue),var(--blue-dark));
  color:#fff; font-size:16px; font-weight:700; padding:18px; border-radius:18px; border:none;
  cursor:pointer; font-family:'Poppins',sans-serif; box-shadow:0 8px 30px rgba(26,86,219,.55);
  animation:fup .9s .5s ease both; display:flex; align-items:center; justify-content:center; gap:8px;
}

/* ── SHARED HEADER ── */
.ob-top { background:white; padding:56px 24px 18px; position:relative; border-bottom:1px solid var(--border); }
.ob-back { position:absolute; top:56px; left:16px; width:38px; height:38px; border-radius:12px; background:var(--bg); border:none; cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:19px; color:var(--text); }
.ob-row { display:flex; align-items:center; gap:12px; }
.ob-logo { width:44px; height:44px; border-radius:50%; background:var(--blue-light); border:2.5px solid var(--blue); display:flex; align-items:center; justify-content:center; flex-shrink:0; }
.sm-e { font-size:22px; font-weight:900; color:var(--blue); font-family:'Poppins',sans-serif; }
.ob-h1 { font-size:19px; font-weight:800; color:var(--text); font-family:'Nunito',sans-serif; }
.ob-step { font-size:12px; color:var(--sub); margin-top:2px; font-weight:500; }
.ob-prog { display:flex; gap:6px; margin-top:14px; }
.pd { height:4px; border-radius:2px; background:var(--border); transition:all .3s; }
.pd.act { background:var(--blue); width:22px; }
.pd.dn { background:var(--blue); opacity:.35; width:8px; }
.pd.id { width:8px; }

/* ── BODY / FOOTER ── */
.ob-body { flex:1; overflow-y:auto; padding:20px 24px 8px; scrollbar-width:none; background:var(--bg); }
.ob-body::-webkit-scrollbar { display:none; }
.ob-foot { padding:14px 24px 22px; background:white; border-top:1px solid var(--border); }

/* ── FORM ELEMENTS ── */
.sec-title { font-size:11px; font-weight:700; color:var(--sub); text-transform:uppercase; letter-spacing:.8px; margin:16px 0 10px; display:flex; align-items:center; gap:6px; }
.sec-title:first-child { margin-top:4px; }
.divider { height:1px; background:var(--border); margin:14px 0; }

.row2 { display:flex; gap:10px; margin-bottom:14px; }
.row2 > * { flex:1; }

.flbl { font-size:11px; font-weight:700; color:var(--sub); text-transform:uppercase; letter-spacing:.6px; margin-bottom:5px; }
.fin {
  width:100%; background:white; border:2px solid var(--border); border-radius:14px;
  padding:12px 14px; font-size:14px; font-family:'Poppins',sans-serif; color:var(--text);
  outline:none; transition:border-color .2s; appearance:none;
}
.fin:focus { border-color:var(--blue); }
.fin::placeholder { color:#c0c4cc; }
.fwrap { margin-bottom:14px; }

.sel-wrap { position:relative; }
.sel-arrow { position:absolute; right:12px; top:50%; transform:translateY(-50%); pointer-events:none; font-size:12px; color:#aaa; }

/* radio */
.rrow { display:flex; gap:8px; }
.ropt { flex:1; background:white; border:2px solid var(--border); border-radius:12px; padding:10px 6px; text-align:center; font-size:12px; font-weight:700; color:var(--sub); cursor:pointer; transition:all .2s; user-select:none; }
.ropt.on { border-color:var(--blue); background:var(--blue-light); color:var(--blue); }

/* type grid */
.tgrid { display:grid; grid-template-columns:1fr 1fr 1fr; gap:8px; }
.topt { background:white; border:2px solid var(--border); border-radius:14px; padding:14px 8px; text-align:center; cursor:pointer; transition:all .2s; }
.topt .ti { font-size:22px; }
.topt .tn { font-size:11px; font-weight:700; color:var(--sub); margin-top:4px; }
.topt.on { border-color:var(--blue); background:var(--blue-light); }
.topt.on .tn { color:var(--blue); }

/* colors */
.colors { display:flex; gap:10px; flex-wrap:wrap; margin-top:6px; }
.cor { width:34px; height:34px; border-radius:50%; cursor:pointer; border:3px solid transparent; transition:all .2s; }
.cor.on { border-color:var(--blue); box-shadow:0 0 0 3px rgba(26,86,219,.25); }

/* terms */
.terms-row { display:flex; align-items:flex-start; gap:10px; margin-top:8px; padding:12px 14px; background:white; border-radius:14px; border:2px solid var(--border); cursor:pointer; }
.terms-row input[type=checkbox] { accent-color:var(--blue); width:16px; height:16px; flex-shrink:0; margin-top:2px; }
.terms-row span { font-size:12px; color:var(--sub); line-height:1.5; }
.terms-row a { color:var(--blue); font-weight:600; text-decoration:none; }

/* next btn */
.next-btn { width:100%; background:linear-gradient(135deg,var(--blue),var(--blue-dark)); color:#fff; font-size:15px; font-weight:700; padding:17px; border-radius:18px; border:none; cursor:pointer; font-family:'Poppins',sans-serif; box-shadow:0 6px 20px rgba(26,86,219,.35); display:flex; align-items:center; justify-content:center; gap:8px; transition:transform .15s; }
.next-btn:active { transform:scale(.97); }
.next-btn.grn { background:linear-gradient(135deg,#16a34a,#15803d); box-shadow:0 6px 20px rgba(22,163,74,.35); }

/* ── MAP ── */
#s-map { background:#e8dfd5; }
.map-bg { position:absolute; inset:0; overflow:hidden; }
.map-bg svg { width:100%; height:100%; }
.road-lbl { position:absolute; font-size:10px; font-weight:600; color:#888; background:rgba(255,255,255,.7); padding:2px 6px; border-radius:3px; }
.ppin { position:absolute; display:flex; flex-direction:column; align-items:center; cursor:pointer; transform:translateX(-50%); z-index:10; transition:transform .2s; }
.ppin:hover { transform:translateX(-50%) scale(1.1); }
.pb { color:white; font-size:11px; font-weight:700; padding:5px 9px; border-radius:10px; white-space:nowrap; box-shadow:0 4px 12px rgba(0,0,0,.25); font-family:'Nunito',sans-serif; }
.pb.gr{background:#16a34a;} .pb.bl{background:#2563eb;box-shadow:0 4px 20px rgba(37,99,235,.5);} .pb.ye{background:#d97706;} .pb.rd{background:#dc2626;}
.pt { width:2px; height:8px; }
.pt.gr{background:#16a34a;} .pt.bl{background:#2563eb;} .pt.ye{background:#d97706;} .pt.rd{background:#dc2626;}
.uring { position:absolute; width:80px; height:80px; border-radius:50%; background:rgba(37,99,235,.1); border:1px solid rgba(37,99,235,.3); top:44%; left:50%; transform:translate(-50%,-50%); z-index:14; }
.udot { position:absolute; width:20px; height:20px; background:#2563eb; border-radius:50%; border:3px solid white; box-shadow:0 0 0 8px rgba(37,99,235,.2),0 4px 10px rgba(0,0,0,.3); top:44%; left:50%; transform:translate(-50%,-50%); z-index:15; animation:pls 2s infinite; }
@keyframes pls{0%,100%{box-shadow:0 0 0 8px rgba(37,99,235,.2),0 4px 10px rgba(0,0,0,.3);}50%{box-shadow:0 0 0 14px rgba(37,99,235,.07),0 4px 10px rgba(0,0,0,.3);}}
.map-top { position:absolute; top:52px; left:0; right:0; padding:12px 16px; z-index:50; display:flex; flex-direction:column; gap:10px; }
.sbar2 { flex:1; background:white; border-radius:14px; padding:11px 16px; display:flex; align-items:center; gap:10px; box-shadow:0 4px 20px rgba(0,0,0,.15); }
.sbar2 input { border:none; outline:none; font-size:14px; font-family:'Poppins',sans-serif; color:#111; flex:1; background:transparent; }
.sbar2 input::placeholder { color:#aaa; }
.ibtn { width:46px; height:46px; background:white; border-radius:14px; display:flex; align-items:center; justify-content:center; box-shadow:0 4px 20px rgba(0,0,0,.15); cursor:pointer; border:none; flex-shrink:0; }
.chips { display:flex; gap:8px; overflow-x:auto; scrollbar-width:none; }
.chips::-webkit-scrollbar{display:none;}
.chip { background:white; border-radius:20px; padding:6px 14px; font-size:12px; font-weight:600; color:#555; white-space:nowrap; box-shadow:0 2px 10px rgba(0,0,0,.1); cursor:pointer; border:none; font-family:'Poppins',sans-serif; display:flex; align-items:center; gap:5px; transition:all .2s; }
.chip.on { background:#2563eb; color:white; }
.map-ctrls { position:absolute; right:16px; top:50%; transform:translateY(-50%); display:flex; flex-direction:column; gap:10px; z-index:50; }
.ctrl { width:44px; height:44px; background:white; border-radius:12px; display:flex; align-items:center; justify-content:center; box-shadow:0 4px 16px rgba(0,0,0,.15); cursor:pointer; border:none; font-size:18px; }
.bot-card { position:absolute; bottom:0; left:0; right:0; background:white; border-radius:28px 28px 0 0; padding:16px 20px 20px; box-shadow:0 -8px 30px rgba(0,0,0,.12); z-index:50; }
.handle { width:40px; height:4px; background:#e0e0e0; border-radius:2px; margin:0 auto 16px; }
.card-ttl { font-size:13px; font-weight:600; color:#888; margin-bottom:14px; text-transform:uppercase; letter-spacing:.8px; }
.spot { display:flex; align-items:center; gap:14px; padding:12px 14px; background:#f8f8fc; border-radius:16px; cursor:pointer; transition:all .2s; border:2px solid transparent; margin-bottom:10px; }
.spot:last-child{margin-bottom:0;}
.spot.sel,.spot:hover { border-color:#2563eb; background:#eff6ff; }
.sico2 { width:48px; height:48px; border-radius:14px; display:flex; align-items:center; justify-content:center; font-size:22px; flex-shrink:0; }
.sico2.g{background:#dcfce7;} .sico2.y{background:#fef9c3;}
.sinf { flex:1; }
.sn { font-size:14px; font-weight:700; color:#111; margin-bottom:2px; }
.sd { font-size:12px; color:#888; }
.sd b { font-weight:600; color:#555; }
.sprice { text-align:right; }
.pv { font-size:16px; font-weight:800; color:#2563eb; font-family:'Nunito',sans-serif; }
.pu { font-size:10px; color:#aaa; }
.avb { font-size:10px; font-weight:700; padding:3px 8px; border-radius:20px; display:inline-block; margin-top:4px; }
.avb.ok{background:#dcfce7;color:#16a34a;} .avb.low{background:#fef9c3;color:#92400e;}

/* ── DETAIL ── */
#s-detail { background:var(--bg); }
.dh { background:white; padding:56px 20px 20px; position:relative; }
.bk { position:absolute; top:58px; left:16px; width:38px; height:38px; border-radius:12px; background:var(--bg); border:none; cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:18px; }
.dname { font-size:20px; font-weight:800; color:#111; text-align:center; margin-bottom:4px; }
.daddr { font-size:13px; color:#888; text-align:center; }
.rrow2 { display:flex; align-items:center; justify-content:center; gap:6px; margin-top:8px; }
.stars{color:#f59e0b;font-size:14px;} .rn{font-size:13px;font-weight:700;color:#333;} .rc{font-size:12px;color:#aaa;}
.mmap { width:100%; height:120px; border-radius:20px; margin-top:16px; overflow:hidden; background:linear-gradient(135deg,#d0e8d8,#b8d4c0); position:relative; display:flex; align-items:center; justify-content:center; }
.rl { position:absolute; width:60%; height:2px; background:linear-gradient(90deg,#2563eb,#60a5fa); border-radius:2px; left:10%; }
.rl::before{content:'';position:absolute;left:0;top:-3px;width:8px;height:8px;background:#2563eb;border-radius:50%;border:2px solid white;}
.rl::after{content:'';position:absolute;right:0;top:-5px;width:12px;height:12px;background:#16a34a;border-radius:50%;border:2px solid white;}
.mpark{background:#16a34a;color:white;font-size:11px;font-weight:800;padding:5px 8px;border-radius:8px;font-family:'Nunito',sans-serif;position:absolute;right:18%;top:25%;}
.dscroll{flex:1;overflow-y:auto;padding:16px 20px;scrollbar-width:none;}
.dscroll::-webkit-scrollbar{display:none;}
.igrid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px;}
.ic{background:white;border-radius:18px;padding:16px;display:flex;flex-direction:column;gap:6px;}
.ici{font-size:22px;} .icl{font-size:11px;color:#aaa;font-weight:600;text-transform:uppercase;letter-spacing:.5px;}
.icv{font-size:18px;font-weight:800;color:#111;font-family:'Nunito',sans-serif;}
.icv.gr{color:#16a34a;} .icv.bl{color:#2563eb;}
.slbl{font-size:13px;font-weight:700;color:#333;margin-bottom:10px;margin-top:4px;}
.oc{background:white;border-radius:18px;padding:16px;margin-bottom:16px;}
.ob-bg{height:10px;background:#f0f0f0;border-radius:5px;overflow:hidden;margin:10px 0 6px;}
.ob-fill{height:100%;background:linear-gradient(90deg,#16a34a,#4ade80);border-radius:5px;width:35%;}
.olbl{display:flex;justify-content:space-between;font-size:11px;color:#aaa;font-weight:600;}
.ams{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:16px;}
.am{background:white;border-radius:12px;padding:8px 14px;font-size:12px;font-weight:600;color:#444;display:flex;align-items:center;gap:6px;}
.hr{background:white;border-radius:16px;padding:14px 16px;display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;}
.hd{font-size:13px;font-weight:600;color:#333;} .ht{font-size:13px;color:#666;}
.ht.bl{color:#2563eb;font-weight:700;}
.rfwrap{padding:16px 20px 20px;background:var(--bg);}
.rbtn2{width:100%;background:linear-gradient(135deg,#2563eb,#1d4ed8);color:white;font-size:16px;font-weight:700;padding:18px;border-radius:18px;border:none;cursor:pointer;font-family:'Poppins',sans-serif;box-shadow:0 8px 24px rgba(37,99,235,.4);display:flex;align-items:center;justify-content:center;gap:10px;transition:transform .15s;}
.rbtn2:active{transform:scale(.97);}

/* ── RESERVE ── */
#s-reserve{background:var(--bg);}
.rh{background:white;padding:60px 20px 20px;text-align:center;position:relative;}
.rtitle{font-size:18px;font-weight:800;color:#111;} .rsub{font-size:13px;color:#888;margin-top:4px;}
.rbody2{flex:1;overflow-y:auto;padding:16px 20px;scrollbar-width:none;}
.rbody2::-webkit-scrollbar{display:none;}
.tpc{background:white;border-radius:18px;padding:20px;margin-bottom:14px;}
.trow{display:flex;gap:12px;}
.tbox{flex:1;background:var(--bg);border-radius:14px;padding:14px;}
.tlbl{font-size:11px;color:#aaa;font-weight:700;text-transform:uppercase;margin-bottom:6px;}
.tval{font-size:20px;font-weight:800;color:#111;font-family:'Nunito',sans-serif;}
.tdate{font-size:11px;color:#888;margin-top:2px;}
.drow{display:flex;gap:8px;margin-top:16px;}
.dchip{flex:1;background:var(--bg);border-radius:12px;padding:10px 4px;text-align:center;font-size:12px;font-weight:700;color:#555;cursor:pointer;border:2px solid transparent;transition:all .2s;font-family:'Nunito',sans-serif;}
.dchip.on{border-color:#2563eb;color:#2563eb;background:#eff6ff;}
.vc2{background:white;border-radius:18px;padding:20px;margin-bottom:14px;}
.vo{display:flex;align-items:center;gap:14px;padding:12px;border-radius:14px;cursor:pointer;border:2px solid transparent;transition:all .2s;margin-bottom:8px;}
.vo:last-child{margin-bottom:0;}
.vo.sel{border-color:#2563eb;background:#eff6ff;}
.vi{font-size:28px;} .vinfo{flex:1;}
.vname{font-size:14px;font-weight:700;color:#111;} .vplate{font-size:12px;color:#888;}
.vck{width:22px;height:22px;border-radius:50%;background:#2563eb;display:flex;align-items:center;justify-content:center;color:white;font-size:12px;}
.sc{background:white;border-radius:18px;padding:20px;margin-bottom:14px;}
.sr{display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid #f0f0f0;font-size:13px;}
.sr:last-child{border-bottom:none;font-weight:800;font-size:15px;color:#111;}
.sr:last-child .sv{color:#2563eb;}
.sl{color:#666;} .sv{font-weight:600;color:#333;}
.cfbtn{width:100%;background:linear-gradient(135deg,#16a34a,#15803d);color:white;font-size:16px;font-weight:700;padding:18px;border-radius:18px;border:none;cursor:pointer;font-family:'Poppins',sans-serif;box-shadow:0 8px 24px rgba(22,163,74,.35);display:flex;align-items:center;justify-content:center;gap:10px;}

/* ── SUCCESS ── */
#s-success{background:var(--bg);align-items:center;justify-content:center;padding:40px 30px;gap:16px;text-align:center;}
.sico3{width:100px;height:100px;background:linear-gradient(135deg,#16a34a,#22c55e);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:48px;box-shadow:0 16px 40px rgba(22,163,74,.35);animation:pop .5s cubic-bezier(.34,1.56,.64,1);}
@keyframes pop{from{transform:scale(0);opacity:0;}to{transform:scale(1);opacity:1;}}
.st{font-size:26px;font-weight:900;color:#111;font-family:'Nunito',sans-serif;}
.ss{font-size:14px;color:#777;line-height:1.5;}
.cb2{background:white;border-radius:20px;padding:20px 30px;width:100%;box-shadow:0 4px 20px rgba(0,0,0,.08);}
.cl2{font-size:12px;color:#aaa;font-weight:700;text-transform:uppercase;letter-spacing:1px;margin-bottom:8px;}
.cv2{font-size:32px;font-weight:900;color:#2563eb;letter-spacing:6px;font-family:'Nunito',sans-serif;}
.ct2{font-size:13px;color:#888;margin-top:6px;}
.qr{width:120px;height:120px;background:white;border-radius:16px;padding:10px;box-shadow:0 4px 20px rgba(0,0,0,.08);display:grid;grid-template-columns:repeat(7,1fr);gap:2px;}
.qrc{border-radius:1px;}
.bmb{background:#111;color:white;font-size:15px;font-weight:700;padding:16px 40px;border-radius:16px;border:none;cursor:pointer;font-family:'Poppins',sans-serif;width:100%;}
</style>
</head>
<body>

<div class="phone">
  <div class="notch" id="notch"></div>
  <div class="status-bar" id="sbar">
    <span class="status-time">9:41</span>
    <div class="status-icons">
      <svg width="16" height="12" viewBox="0 0 16 12"><path d="M0 4h2v8H0zm3-2h2v10H3zm3-2h2v12H6zm3 4h2v6H9zm3-2h2v8h-2z"/></svg>
      <svg width="15" height="12" viewBox="0 0 15 12"><path d="M7.5 2.5C5 2.5 2.8 3.5 1.2 5.2L0 4C1.9 2 4.5.8 7.5.8s5.6 1.2 7.5 3.2L13.8 5.2C12.2 3.5 10 2.5 7.5 2.5zm0 3C6 5.5 4.6 6.1 3.6 7.2L2.4 6C3.7 4.7 5.5 3.8 7.5 3.8s3.8.9 5.1 2.2L11.4 7.2C10.4 6.1 9 5.5 7.5 5.5zm0 3c-.8 0-1.5.3-2 .8L4.2 8.1C5.1 7.1 6.2 6.5 7.5 6.5s2.4.6 3.3 1.6L9.5 9.3c-.5-.5-1.2-.8-2-.8zm0 3a1.5 1.5 0 100-3 1.5 1.5 0 000 3z"/></svg>
      <svg width="25" height="12" viewBox="0 0 25 12"><rect x="0" y="1" width="21" height="10" rx="2" stroke="white" stroke-width="1.5" fill="none"/><rect x="1.5" y="2.5" width="16" height="7" rx="1" fill="white"/><rect x="22" y="4" width="3" height="4" rx="1" fill="white" opacity=".5"/></svg>
    </div>
  </div>

  <div class="app">

  <!-- ── SPLASH ── -->
  <div id="s-splash" class="screen active">
    <div style="position:absolute;inset:0;background:linear-gradient(165deg,#0d1628,#162e6e 55%,#0d1628);"></div>
    <div class="orb" style="width:280px;height:280px;top:-90px;right:-70px;"></div>
    <div class="orb" style="width:220px;height:220px;bottom:120px;left:-60px;animation-direction:reverse;animation-duration:9s;"></div>
    <div style="flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;position:relative;gap:26px;">
      <div class="logo-wrap">
        <div class="logo-circle">
          <div class="logo-ring"></div>
          <div class="logo-inner"><span class="big-e">E</span></div>
        </div>
        <div>
          <div class="brand-main">Estacione</div>
          <div class="brand-main" style="font-size:22px;opacity:.8;letter-spacing:5px;margin-top:-4px;">AQUI</div>
          <div class="brand-sub">Encontre sua vaga ideal</div>
        </div>
      </div>
    </div>
    <button class="splash-cta" onclick="fwd('s-splash','s-motor')">Começar <svg width="20" height="20" fill="none" stroke="white" stroke-width="2.5" viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7"/></svg></button>
  </div>

  <!-- ── CADASTRO DO MOTORISTA ── -->
  <div id="s-motor" class="screen">
    <div class="ob-top">
      <div class="ob-row">
        <div class="ob-logo"><span class="sm-e">E</span></div>
        <div>
          <div class="ob-h1">Cadastro do Motorista</div>
          <div class="ob-step">Passo 1 de 3 · Dados pessoais</div>
        </div>
      </div>
      <div class="ob-prog">
        <div class="pd act"></div>
        <div class="pd id"></div>
        <div class="pd id"></div>
      </div>
    </div>

    <div class="ob-body">

      <!-- foto -->
      <div style="display:flex;flex-direction:column;align-items:center;padding:14px 0 6px;gap:10px;">
        <div style="width:80px;height:80px;border-radius:50%;background:var(--blue-light);border:3px dashed var(--blue);display:flex;align-items:center;justify-content:center;font-size:32px;cursor:pointer;">👤</div>
        <span style="font-size:12px;color:var(--blue);font-weight:600;cursor:pointer;">+ Adicionar foto</span>
      </div>

      <div class="sec-title">👤 Dados Pessoais</div>

      <div class="row2">
        <div><div class="flbl">Nome</div><input class="fin" placeholder="João"></div>
        <div><div class="flbl">Sobrenome</div><input class="fin" placeholder="da Silva"></div>
      </div>

      <div class="row2">
        <div><div class="flbl">Data de Nascimento</div><input class="fin" type="date"></div>
        <div>
          <div class="flbl">Sexo</div>
          <div class="sel-wrap">
            <select class="fin">
              <option value="" disabled selected>Selecione</option>
              <option>Masculino</option>
              <option>Feminino</option>
              <option>Outro</option>
              <option>Prefiro não dizer</option>
            </select>
            <span class="sel-arrow">▾</span>
          </div>
        </div>
      </div>

      <div class="fwrap"><div class="flbl">CPF</div><input class="fin" placeholder="000.000.000-00" maxlength="14" oninput="mCPF(this)"></div>
      <div class="row2">
        <div><div class="flbl">RG</div><input class="fin" placeholder="00.000.000-0"></div>
        <div><div class="flbl">Nacionalidade</div><input class="fin" placeholder="Brasileiro(a)"></div>
      </div>

      <div class="divider"></div>
      <div class="sec-title">🪪 CNH</div>

      <div class="fwrap"><div class="flbl">Número da CNH</div><input class="fin" placeholder="00000000000" maxlength="11"></div>
      <div class="row2">
        <div>
          <div class="flbl">Categoria</div>
          <div class="sel-wrap">
            <select class="fin">
              <option value="" disabled selected>Categoria</option>
              <option>A</option><option>B</option><option>AB</option><option>C</option><option>D</option><option>E</option>
            </select>
            <span class="sel-arrow">▾</span>
          </div>
        </div>
        <div><div class="flbl">Validade</div><input class="fin" type="date"></div>
      </div>

      <div class="divider"></div>
      <div class="sec-title">📞 Contato</div>

      <div class="fwrap"><div class="flbl">E-mail</div><input class="fin" type="email" placeholder="seuemail@exemplo.com"></div>
      <div class="row2">
        <div><div class="flbl">Celular</div><input class="fin" type="tel" placeholder="(11) 9 0000-0000" maxlength="16" oninput="mTel(this)"></div>
        <div><div class="flbl">Telefone fixo</div><input class="fin" type="tel" placeholder="(11) 0000-0000"></div>
      </div>

      <div class="divider"></div>
      <div class="sec-title">📍 Endereço</div>

      <div class="row2">
        <div><div class="flbl">CEP</div><input class="fin" placeholder="00000-000" maxlength="9" oninput="mCEP(this)"></div>
        <div>
          <div class="flbl">Estado</div>
          <div class="sel-wrap">
            <select class="fin">
              <option value="" disabled selected>UF</option>
              <option>AC</option><option>AL</option><option>AP</option><option>AM</option><option>BA</option>
              <option>CE</option><option>DF</option><option>ES</option><option>GO</option><option>MA</option>
              <option>MT</option><option>MS</option><option>MG</option><option>PA</option><option>PB</option>
              <option>PR</option><option>PE</option><option>PI</option><option>RJ</option><option>RN</option>
              <option>RS</option><option>RO</option><option>RR</option><option>SC</option><option selected>SP</option>
              <option>SE</option><option>TO</option>
            </select>
            <span class="sel-arrow">▾</span>
          </div>
        </div>
      </div>
      <div class="fwrap"><div class="flbl">Cidade</div><input class="fin" placeholder="São Paulo"></div>
      <div class="fwrap"><div class="flbl">Bairro</div><input class="fin" placeholder="Bela Vista"></div>
      <div class="row2">
        <div><div class="flbl">Rua / Avenida</div><input class="fin" placeholder="Av. Paulista"></div>
        <div><div class="flbl">Número</div><input class="fin" placeholder="1374"></div>
      </div>
      <div class="fwrap"><div class="flbl">Complemento (opcional)</div><input class="fin" placeholder="Apto 42, Bloco B..."></div>

      <div class="divider"></div>
      <div class="sec-title">🔒 Acesso</div>

      <div class="fwrap"><div class="flbl">Senha</div><input class="fin" type="password" placeholder="Mínimo 8 caracteres"></div>
      <div class="fwrap"><div class="flbl">Confirmar senha</div><input class="fin" type="password" placeholder="Repita a senha"></div>

      <label class="terms-row">
        <input type="checkbox">
        <span>Li e concordo com os <a href="#">Termos de Uso</a> e a <a href="#">Política de Privacidade</a> do Estacione Aqui.</span>
      </label>

      <div style="height:16px;"></div>
    </div>

    <div class="ob-foot">
      <button class="next-btn" onclick="fwd('s-motor','s-filtros')">Continuar <svg width="18" height="18" fill="none" stroke="white" stroke-width="2.5" viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7"/></svg></button>
    </div>
  </div>

  <!-- ── FILTROS ── -->
  <div id="s-filtros" class="screen">
    <div class="ob-top">
      <button class="ob-back" onclick="bk('s-filtros','s-motor')">←</button>
      <div class="ob-row" style="margin-left:50px;">
        <div class="ob-logo"><span class="sm-e">E</span></div>
        <div>
          <div class="ob-h1">Selecione seus filtros</div>
          <div class="ob-step">Passo 2 de 3</div>
        </div>
      </div>
      <div class="ob-prog">
        <div class="pd dn"></div>
        <div class="pd act"></div>
        <div class="pd id"></div>
      </div>
    </div>
    <div class="ob-body">
      <p style="font-size:13px;color:var(--sub);margin-bottom:16px;line-height:1.5;">Isso nos ajuda a encontrar vagas especiais para você. 🎯</p>

      <div style="background:white;border-radius:16px;padding:16px;margin-bottom:12px;">
        <div style="font-size:14px;font-weight:600;color:var(--text);margin-bottom:12px;">👴 Você tem credencial de idoso?</div>
        <div class="rrow"><div class="ropt" onclick="rsel(this)">✅ Sim</div><div class="ropt on" onclick="rsel(this)">❌ Não</div></div>
      </div>
      <div style="background:white;border-radius:16px;padding:16px;margin-bottom:12px;">
        <div style="font-size:14px;font-weight:600;color:var(--text);margin-bottom:12px;">🤰 Você está gestante?</div>
        <div class="rrow"><div class="ropt" onclick="rsel(this)">✅ Sim</div><div class="ropt on" onclick="rsel(this)">❌ Não</div></div>
      </div>
      <div style="background:white;border-radius:16px;padding:16px;margin-bottom:12px;">
        <div style="font-size:14px;font-weight:600;color:var(--text);margin-bottom:12px;">♿ Você é PCD?</div>
        <div class="rrow"><div class="ropt" onclick="rsel(this)">✅ Sim</div><div class="ropt on" onclick="rsel(this)">❌ Não</div></div>
      </div>
      <div style="background:white;border-radius:16px;padding:16px;margin-bottom:12px;">
        <div style="font-size:14px;font-weight:600;color:var(--text);margin-bottom:12px;">🔌 Precisa de recarga elétrica (EV)?</div>
        <div class="rrow"><div class="ropt" onclick="rsel(this)">✅ Sim</div><div class="ropt on" onclick="rsel(this)">❌ Não</div></div>
      </div>
      <div style="background:white;border-radius:16px;padding:16px;margin-bottom:12px;">
        <div style="font-size:14px;font-weight:600;color:var(--text);margin-bottom:12px;">🏢 Prefere estacionamento coberto?</div>
        <div class="rrow"><div class="ropt on" onclick="rsel(this)">✅ Sim</div><div class="ropt" onclick="rsel(this)">❌ Não</div></div>
      </div>
    </div>
    <div class="ob-foot">
      <button class="next-btn" onclick="fwd('s-filtros','s-veiculo')">Continuar <svg width="18" height="18" fill="none" stroke="white" stroke-width="2.5" viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7"/></svg></button>
    </div>
  </div>

  <!-- ── VEÍCULO ── -->
  <div id="s-veiculo" class="screen">
    <div class="ob-top">
      <button class="ob-back" onclick="bk('s-veiculo','s-filtros')">←</button>
      <div class="ob-row" style="margin-left:50px;">
        <div class="ob-logo"><span class="sm-e">E</span></div>
        <div>
          <div class="ob-h1">Dados do Veículo</div>
          <div class="ob-step">Passo 3 de 3</div>
        </div>
      </div>
      <div class="ob-prog">
        <div class="pd dn"></div>
        <div class="pd dn"></div>
        <div class="pd act"></div>
      </div>
    </div>
    <div class="ob-body">
      <div class="fwrap">
        <div class="flbl">Tipo de veículo</div>
        <div class="tgrid">
          <div class="topt on" onclick="tsel(this)"><div class="ti">🚗</div><div class="tn">Carro</div></div>
          <div class="topt" onclick="tsel(this)"><div class="ti">🏍</div><div class="tn">Moto</div></div>
          <div class="topt" onclick="tsel(this)"><div class="ti">🚐</div><div class="tn">Van/SUV</div></div>
        </div>
      </div>
      <div class="fwrap"><div class="flbl">Modelo</div><input class="fin" placeholder="Ex: Honda Civic, HB20, Gol..."></div>
      <div class="fwrap">
        <div class="flbl">Porte</div>
        <div class="rrow"><div class="ropt" onclick="rsel(this)">Pequeno</div><div class="ropt on" onclick="rsel(this)">Médio</div><div class="ropt" onclick="rsel(this)">Grande</div></div>
      </div>
      <div class="fwrap"><div class="flbl">Placa</div><input class="fin" placeholder="ABC-1D23" style="text-transform:uppercase;letter-spacing:3px;font-weight:700;"></div>
      <div class="row2">
        <div><div class="flbl">Ano</div><input class="fin" type="number" placeholder="2022"></div>
        <div><div class="flbl">Cor</div>
          <div class="colors">
            <div class="cor on" style="background:#111;" onclick="csel(this)"></div>
            <div class="cor" style="background:#fff;border:2px solid #ddd;" onclick="csel(this)"></div>
            <div class="cor" style="background:#c0392b;" onclick="csel(this)"></div>
            <div class="cor" style="background:#2980b9;" onclick="csel(this)"></div>
            <div class="cor" style="background:#7f8c8d;" onclick="csel(this)"></div>
            <div class="cor" style="background:#27ae60;" onclick="csel(this)"></div>
          </div>
        </div>
      </div>
    </div>
    <div class="ob-foot">
      <button class="next-btn" style="background:linear-gradient(135deg,#16a34a,#15803d);box-shadow:0 6px 20px rgba(22,163,74,.35);" onclick="fwd('s-veiculo','s-map')">🎯 Encontrar Vagas!</button>
    </div>
  </div>

  <!-- ── MAPA ── -->
  <div id="s-map" class="screen">
    <div class="map-bg">
      <svg viewBox="0 0 375 812" preserveAspectRatio="xMidYMid slice">
        <rect width="375" height="812" fill="#e8dfd5"/>
        <rect x="0" y="258" width="375" height="64" fill="#d2c8bc"/>
        <rect x="0" y="430" width="375" height="50" fill="#d2c8bc"/>
        <rect x="0" y="600" width="375" height="44" fill="#d2c8bc"/>
        <rect x="33" y="0" width="58" height="812" fill="#d2c8bc"/>
        <rect x="193" y="0" width="72" height="812" fill="#d2c8bc"/>
        <rect x="312" y="0" width="48" height="812" fill="#d2c8bc"/>
        <line x1="62" y1="0" x2="62" y2="812" stroke="#c4b8ac" stroke-width="1" stroke-dasharray="14,10"/>
        <line x1="229" y1="0" x2="229" y2="812" stroke="#c4b8ac" stroke-width="1" stroke-dasharray="14,10"/>
        <line x1="0" y1="290" x2="375" y2="290" stroke="#c4b8ac" stroke-width="1" stroke-dasharray="14,10"/>
        <line x1="0" y1="455" x2="375" y2="455" stroke="#c4b8ac" stroke-width="1" stroke-dasharray="14,10"/>
        <rect x="100" y="88" width="84" height="157" fill="#c8bfb4" rx="5"/>
        <rect x="280" y="78" width="28" height="172" fill="#c8bfb4" rx="4"/>
        <rect x="100" y="340" width="84" height="76" fill="#c8bfb4" rx="5"/>
        <rect x="270" y="342" width="38" height="74" fill="#c8bfb4" rx="4"/>
        <rect x="100" y="498" width="84" height="88" fill="#c8bfb4" rx="5"/>
        <rect x="270" y="500" width="38" height="84" fill="#c8bfb4" rx="4"/>
        <rect x="100" y="658" width="160" height="130" fill="#c8d9b4" rx="6"/>
        <circle cx="138" cy="698" r="18" fill="#a8c890" opacity=".7"/>
        <circle cx="178" cy="683" r="14" fill="#a8c890" opacity=".7"/>
        <circle cx="218" cy="698" r="16" fill="#a8c890" opacity=".7"/>
      </svg>
    </div>
    <div class="road-lbl" style="top:277px;left:50%;transform:translateX(-50%)">Av. Paulista</div>
    <div class="uring"></div>
    <div class="udot"></div>
    <div class="ppin" style="top:28%;left:38%;" onclick="fwd('s-map','s-detail')"><div class="pb bl">🅿 12 vagas</div><div class="pt bl"></div></div>
    <div class="ppin" style="top:20%;left:67%;"><div class="pb ye">🅿 3 vagas</div><div class="pt ye"></div></div>
    <div class="ppin" style="top:53%;left:24%;"><div class="pb gr">🅿 8 vagas</div><div class="pt gr"></div></div>
    <div class="ppin" style="top:58%;left:73%;"><div class="pb rd">🅿 Lotado</div><div class="pt rd"></div></div>
    <div class="ppin" style="top:70%;left:50%;"><div class="pb gr">🅿 5 vagas</div><div class="pt gr"></div></div>
    <div class="map-top">
      <div style="display:flex;gap:10px;align-items:center;">
        <div class="sbar2">
          <svg width="18" height="18" fill="none" stroke="#aaa" stroke-width="2" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
          <input placeholder="Buscar endereço..." value="Av. Paulista, SP">
          <svg width="16" height="16" fill="#2563eb" viewBox="0 0 24 24"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/></svg>
        </div>
        <button class="ibtn"><svg width="20" height="20" fill="none" stroke="#333" stroke-width="2" viewBox="0 0 24 24"><line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/></svg></button>
      </div>
      <div class="chips">
        <button class="chip on">🗺 Todos</button>
        <button class="chip">🕐 24h</button>
        <button class="chip">⚡ Coberto</button>
        <button class="chip">♿ PCD</button>
        <button class="chip">🔌 EV</button>
      </div>
    </div>
    <div class="map-ctrls">
      <button class="ctrl">＋</button>
      <button class="ctrl">－</button>
      <button class="ctrl" style="font-size:14px">🧭</button>
    </div>
    <div class="bot-card">
      <div class="handle"></div>
      <div class="card-ttl">📍 3 estacionamentos próximos</div>
      <div class="spot sel" onclick="fwd('s-map','s-detail')">
        <div class="sico2 g">🏢</div>
        <div class="sinf"><div class="sn">Park Paulista Premium</div><div class="sd"><b>280m</b> · Coberto · 24h</div><span class="avb ok">12 vagas livres</span></div>
        <div class="sprice"><div class="pv">R$8</div><div class="pu">/hora</div><div style="font-size:11px;color:#888;margin-top:2px;">★ 4.8</div></div>
      </div>
      <div class="spot" onclick="fwd('s-map','s-detail')">
        <div class="sico2 y">🏗</div>
        <div class="sinf"><div class="sn">Estac. Centro Vivo</div><div class="sd"><b>510m</b> · Descoberto</div><span class="avb low">3 vagas restantes</span></div>
        <div class="sprice"><div class="pv">R$5</div><div class="pu">/hora</div><div style="font-size:11px;color:#888;margin-top:2px;">★ 4.2</div></div>
      </div>
    </div>
  </div>

  <!-- ── DETAIL ── -->
  <div id="s-detail" class="screen">
    <div class="dh">
      <button class="bk" onclick="bk('s-detail','s-map')">←</button>
      <div class="dname">Park Paulista Premium</div>
      <div class="daddr">Av. Paulista, 1374 – Bela Vista, SP</div>
      <div class="rrow2"><span class="stars">★★★★★</span><span class="rn">4.8</span><span class="rc">(312 avaliações)</span></div>
      <div class="mmap"><div class="rl"></div><div class="mpark">🅿 P</div></div>
    </div>
    <div class="dscroll">
      <div class="igrid">
        <div class="ic"><div class="ici">🕐</div><div class="icl">Horário</div><div class="icv">24h</div></div>
        <div class="ic"><div class="ici">🚗</div><div class="icl">Distância</div><div class="icv bl">280m</div></div>
        <div class="ic"><div class="ici">💰</div><div class="icl">Tarifa/hora</div><div class="icv">R$ 8,00</div></div>
        <div class="ic"><div class="ici">✅</div><div class="icl">Vagas livres</div><div class="icv gr">12</div></div>
      </div>
      <div class="oc"><div class="slbl">Ocupação atual</div><div class="ob-bg"><div class="ob-fill"></div></div><div class="olbl"><span>0%</span><span>35% ocupado</span><span>100%</span></div></div>
      <div class="slbl">Comodidades</div>
      <div class="ams"><div class="am">🏢 Coberto</div><div class="am">📷 CFTV 24h</div><div class="am">♿ PCD</div><div class="am">🔌 EV</div><div class="am">🛎 Manobrista</div></div>
      <div class="slbl">Tabela de preços</div>
      <div class="hr"><span class="hd">1ª hora</span><span class="ht bl">R$ 8,00</span></div>
      <div class="hr"><span class="hd">Hora adicional</span><span class="ht">R$ 6,00</span></div>
      <div class="hr"><span class="hd">Diária (máx. 12h)</span><span class="ht">R$ 45,00</span></div>
    </div>
    <div class="rfwrap"><button class="rbtn2" onclick="fwd('s-detail','s-reserve')">🅿 Reservar vaga agora</button></div>
  </div>

  <!-- ── RESERVA ── -->
  <div id="s-reserve" class="screen">
    <div class="rh">
      <button class="bk" onclick="bk('s-reserve','s-detail')">←</button>
      <div class="rtitle">Reservar Vaga</div>
      <div class="rsub">Park Paulista Premium</div>
    </div>
    <div class="rbody2">
      <div class="tpc">
        <div class="slbl">⏰ Período da reserva</div>
        <div class="trow">
          <div class="tbox"><div class="tlbl">Entrada</div><div class="tval">14:00</div><div class="tdate">Hoje, 07/04</div></div>
          <div style="display:flex;align-items:center;font-size:20px;color:#ccc;margin-top:20px;">→</div>
          <div class="tbox"><div class="tlbl">Saída</div><div class="tval">16:00</div><div class="tdate">Hoje, 07/04</div></div>
        </div>
        <div style="margin-top:14px;font-size:12px;font-weight:700;color:#888;text-transform:uppercase;letter-spacing:.5px;margin-bottom:8px;">Duração</div>
        <div class="drow">
          <div class="dchip">1h</div><div class="dchip on">2h</div><div class="dchip">3h</div><div class="dchip">4h</div><div class="dchip">+</div>
        </div>
      </div>
      <div class="vc2">
        <div class="slbl">🚗 Veículo</div>
        <div class="vo sel"><div class="vi">🚗</div><div class="vinfo"><div class="vname">Civic Preto</div><div class="vplate">ABC-1D23</div></div><div class="vck">✓</div></div>
        <div class="vo" style="border:2px dashed #ddd;justify-content:center;color:#aaa;font-size:13px;font-weight:600;gap:8px;">＋ Adicionar veículo</div>
      </div>
      <div class="sc">
        <div class="slbl">📋 Resumo</div>
        <div class="sr"><span class="sl">2h × R$ 8,00</span><span class="sv">R$ 16,00</span></div>
        <div class="sr"><span class="sl">Taxa de reserva</span><span class="sv">R$ 2,00</span></div>
        <div class="sr"><span class="sl">Desconto fidelidade</span><span class="sv" style="color:#16a34a;">−R$ 1,00</span></div>
        <div class="sr"><span class="sl">Total</span><span class="sv">R$ 17,00</span></div>
      </div>
    </div>
    <div class="rfwrap"><button class="cfbtn" onclick="fwd('s-reserve','s-success')">✅ Confirmar reserva · R$ 17,00</button></div>
  </div>

  <!-- ── SUCESSO ── -->
  <div id="s-success" class="screen">
    <div class="sico3">✅</div>
    <div class="st">Vaga Reservada!</div>
    <div class="ss">Sua vaga está garantida.<br>Apresente o código na entrada.</div>
    <div class="cb2"><div class="cl2">Código de acesso</div><div class="cv2">EP4829</div><div class="ct2">⏳ Expira em 1h 59min</div></div>
    <div class="qr" id="qr"></div>
    <div style="font-size:13px;color:#aaa;line-height:1.6;text-align:center;">📍 <strong style="color:#333">Park Paulista Premium</strong><br>Av. Paulista, 1374 · Entrada B2<br>14:00 – 16:00 · Civic ABC-1D23</div>
    <button class="bmb" onclick="reset()">← Voltar ao Mapa</button>
  </div>

  </div><!-- /app -->
</div><!-- /phone -->

<script>
function updateChrome(id) {
  const bar = document.getElementById('sbar');
  const notch = document.getElementById('notch');
  if (id === 's-splash') { bar.classList.remove('dk'); notch.style.background='#0d1628'; }
  else if (id === 's-map') { bar.classList.remove('dk'); notch.style.background='white'; }
  else { bar.classList.add('dk'); notch.style.background='var(--bg)'; }
}
function fwd(from, to) {
  const f = document.getElementById(from), t = document.getElementById(to);
  if (!f || !t) return;

  f.classList.remove('active');
  f.classList.add('gone');

  t.classList.remove('gone');
  t.style.transform = '';
  t.style.opacity = '';
  t.classList.add('active');

  setTimeout(() => {
    f.classList.remove('gone');
    f.style.transform = '';
    f.style.opacity = '';
  }, 400);

  updateChrome(to);
}
function bk(from, to) {
  const f = document.getElementById(from), t = document.getElementById(to);
  if (!f || !t) return;

  f.classList.remove('active');
  f.classList.add('gone');

  t.classList.remove('gone');
  t.style.transform = '';
  t.style.opacity = '';
  t.classList.add('active');

  setTimeout(() => {
    f.classList.remove('gone');
    f.style.transform = '';
    f.style.opacity = '';
  }, 400);

  updateChrome(to);
}
function reset() {
  ['s-motor','s-filtros','s-veiculo','s-map','s-detail','s-reserve','s-success'].forEach(id=>{
    const el=document.getElementById(id);
    el.classList.remove('active','gone');
    el.style.transform='translateX(100%)'; el.style.opacity='0';
  });
  const sp=document.getElementById('s-splash');
  sp.classList.add('active'); sp.style.transform=''; sp.style.opacity='';
  updateChrome('s-splash');
}
function rsel(el){ el.closest('.rrow').querySelectorAll('.ropt').forEach(o=>o.classList.remove('on')); el.classList.add('on'); }
function tsel(el){ el.closest('.tgrid').querySelectorAll('.topt').forEach(o=>o.classList.remove('on')); el.classList.add('on'); }
function csel(el){ el.closest('.colors').querySelectorAll('.cor').forEach(o=>o.classList.remove('on')); el.classList.add('on'); }

function mCPF(el){ let v=el.value.replace(/\D/g,'').slice(0,11); v=v.replace(/(\d{3})(\d)/,'$1.$2').replace(/(\d{3})(\d)/,'$1.$2').replace(/(\d{3})(\d{1,2})$/,'$1-$2'); el.value=v; }
function mTel(el){ let v=el.value.replace(/\D/g,'').slice(0,11); v=v.replace(/^(\d{2})(\d)/,'($1) $2').replace(/(\d{5})(\d)/,'$1-$2'); el.value=v; }
function mCEP(el){ let v=el.value.replace(/\D/g,'').slice(0,8); v=v.replace(/(\d{5})(\d)/,'$1-$2'); el.value=v; }

// QR Code
const qrEl=document.getElementById('qr');
[1,1,1,0,0,1,0,1,1,1,0,1,0,0,1,0,1,1,0,1,0,0,1,0,1,1,0,0,1,0,0,1,0,1,1,0,1,0,1,0,1,0,1,0,0,0,1,1,1].forEach(v=>{
  const c=document.createElement('div'); c.className='qrc'; c.style.background=v?'#111':'white'; qrEl.appendChild(c);
});
updateChrome('s-splash');
</script>
</body>
</html>
