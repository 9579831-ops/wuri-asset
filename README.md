[wuri-1.html](https://github.com/user-attachments/files/27316781/wuri-1.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>우리집 자산관리</title>

<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Apple SD Gothic Neo','Malgun Gothic',sans-serif;background:#0f1117;color:#e8eaf6;min-height:100vh}
button{cursor:pointer;font-family:inherit;border:none;outline:none}
input,select{font-family:inherit;outline:none;box-sizing:border-box}
.nav{display:flex;align-items:center;justify-content:space-between;padding:11px 14px;background:#1a1d27;border-bottom:1px solid #2e3352;position:sticky;top:0;z-index:50}
.logo{font-size:14px;font-weight:700;color:#6c7bff}
.sync{font-size:10px;color:#4caf88;background:rgba(76,175,136,.12);padding:2px 7px;border-radius:10px;margin-left:6px}
.tabs{display:flex;gap:2px;background:#0f1117;border-radius:9px;padding:2px}
.tab{padding:5px 9px;border-radius:7px;font-size:13px;font-weight:600;color:#8890b5;background:transparent}
.tab.on{background:#6c7bff;color:#fff}
.page{padding:12px 14px}
.ptitle{font-size:10px;color:#8890b5;font-weight:600;text-transform:uppercase;letter-spacing:.8px;margin-bottom:11px}
.box{background:#1a1d27;border:1px solid #2e3352;border-radius:13px;overflow:hidden;margin-bottom:13px}
.bh{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;border-bottom:1px solid #2e3352}
.bh h3{font-size:13px;font-weight:600}
.bhr{display:flex;gap:6px;align-items:center}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:11px;margin-bottom:13px}
.card{background:#1a1d27;border:1px solid #2e3352;border-radius:11px;padding:11px 13px}
.clbl{font-size:10px;color:#8890b5;text-transform:uppercase;letter-spacing:.8px;margin-bottom:4px}
.cval{font-size:14px;font-weight:700}
.pb{height:5px;background:#22263a;border-radius:3px;overflow:hidden;margin-top:4px}
.pbf{height:100%;border-radius:3px}
/* 버튼 */
.bp{padding:6px 12px;border-radius:8px;font-size:11px;font-weight:600;background:#6c7bff;color:#fff}
.bn{padding:6px 12px;border-radius:8px;font-size:11px;font-weight:600;background:#22263a;color:#8890b5}
.bd{padding:6px 12px;border-radius:8px;font-size:11px;font-weight:600;background:rgba(255,107,138,.18);color:#ff6b8a}
.be{padding:4px 7px;border-radius:7px;font-size:13px;background:rgba(108,123,255,.12);color:#6c7bff}
.bx{padding:4px 7px;border-radius:7px;font-size:13px;background:rgba(255,107,138,.12);color:#ff6b8a}
/* 테이블 */
.tscroll{overflow-x:auto}
table{width:100%;border-collapse:collapse;min-width:500px}
th{font-size:10px;color:#8890b5;text-transform:uppercase;padding:6px 9px;text-align:left;background:#22263a;border-bottom:1px solid #2e3352;white-space:nowrap}
td{padding:7px 9px;font-size:12px;border-bottom:1px solid rgba(46,51,82,.3);vertical-align:middle}
tfoot td{background:#22263a;border-top:2px solid #2e3352;font-weight:700}
/* 뱃지 */
.bdg{display:inline-block;padding:1px 7px;border-radius:20px;font-size:10px;font-weight:600}
/* 아이템 */
.item{display:flex;align-items:center;gap:9px;padding:8px 13px;border-bottom:1px solid rgba(46,51,82,.3)}
.item:last-child{border-bottom:none}
.ico{width:27px;height:27px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:13px;flex-shrink:0}
/* 모달 */
.mobg{position:fixed;inset:0;background:rgba(0,0,0,.8);display:flex;align-items:center;justify-content:center;z-index:200;padding:14px}
.mobox{background:#1a1d27;border:1px solid #2e3352;border-radius:16px;padding:18px;width:100%;max-width:450px;max-height:88vh;overflow-y:auto}
.motitle{font-size:14px;font-weight:700;margin-bottom:14px}
.mofoot{display:flex;gap:6px;justify-content:flex-end;margin-top:14px}
.fl{margin-bottom:11px}
.fl label{display:block;font-size:11px;color:#8890b5;margin-bottom:4px;font-weight:500}
.fl input,.fl select{width:100%;padding:8px 11px;background:#22263a;border:1px solid #2e3352;border-radius:8px;color:#e8eaf6;font-size:12px}
/* 카테고리 버튼 */
.cbwrap{display:flex;flex-wrap:wrap;gap:4px}
.cb{padding:4px 8px;border-radius:18px;font-size:10px;font-weight:600;background:#22263a;color:#8890b5;border:1px solid #2e3352}
.cb.on{border:none;color:#fff}
.glbl{font-size:9px;color:#8890b5;margin-bottom:2px;margin-top:5px;text-transform:uppercase;letter-spacing:.5px}
</style>
</head>
<body>
<div id="app"><div style="display:flex;align-items:center;justify-content:center;height:100vh;flex-direction:column;gap:14px"><div style="font-size:32px">🏠</div><div style="font-size:13px;color:#8890b5">불러오는 중...</div></div></div>

<script>
// ── 상수 ─────────────────────────────────────────
const OWS = ["오동주","오승헌","서지은","공동"];
const OWC = {"오동주":"#4ecdc4","오승헌":"#6c7bff","서지은":"#ff6b8a","공동":"#ffd166"};
const OWBG = {"오동주":"rgba(78,205,196,.15)","오승헌":"rgba(108,123,255,.15)","서지은":"rgba(255,107,138,.15)","공동":"rgba(255,209,102,.15)"};
const ACATS = ["부동산","예금·저축","주식·ETF","퇴직연금","금·실물자산","기타"];
const AICO = {"부동산":"🏠","예금·저축":"🏦","주식·ETF":"📈","퇴직연금":"🧓","금·실물자산":"🥇","기타":"📦"};
const ACC = {"부동산":"#6c7bff","예금·저축":"#4ecdc4","주식·ETF":"#ffd166","퇴직연금":"#ff9f43","금·실물자산":"#f7c948","기타":"#8890b5"};
const IC = [
  {k:"급여",i:"💼",c:"#4caf88"},
  {k:"부업·프리랜서",i:"💻",c:"#4ecdc4"},
  {k:"투자수익",i:"📈",c:"#ffd166"},
  {k:"임대수입",i:"🏠",c:"#6c7bff"},
  {k:"기타수입",i:"🎁",c:"#ff9f43"}
];
const EC = [
  {k:"식비·장보기",i:"🛒",c:"#ff6b8a",g:"식생활"},
  {k:"외식·배달",i:"🍽️",c:"#ff8fab",g:"식생활"},
  {k:"카페·음료",i:"☕",c:"#ffb3c1",g:"식생활"},
  {k:"주거·관리비",i:"🏠",c:"#6c7bff",g:"주거"},
  {k:"대출상환",i:"🏦",c:"#5a6aee",g:"주거"},
  {k:"공과금·통신",i:"📡",c:"#748ffc",g:"주거"},
  {k:"교통·주유",i:"🚗",c:"#4ecdc4",g:"교통"},
  {k:"자동차보험·정비",i:"🔧",c:"#38b2ac",g:"교통"},
  {k:"병원·약국",i:"🏥",c:"#f7c948",g:"건강"},
  {k:"운동·헬스",i:"💪",c:"#ffd166",g:"건강"},
  {k:"교육·학원",i:"📚",c:"#a78bfa",g:"교육"},
  {k:"육아·아이용품",i:"👶",c:"#c4b5fd",g:"교육"},
  {k:"저축·적금",i:"💰",c:"#4caf88",g:"저축·투자"},
  {k:"주식·ETF매수",i:"📊",c:"#38a169",g:"저축·투자"},
  {k:"코인매수",i:"₿",c:"#dd6b20",g:"저축·투자"},
  {k:"여행·숙박",i:"✈️",c:"#63b3ed",g:"여가"},
  {k:"문화·취미",i:"🎭",c:"#4299e1",g:"여가"},
  {k:"구독·OTT",i:"📺",c:"#3182ce",g:"여가"},
  {k:"쇼핑·의류",i:"👗",c:"#fc8181",g:"쇼핑"},
  {k:"생활용품",i:"🧴",c:"#feb2b2",g:"쇼핑"},
  {k:"경조사·선물",i:"🎀",c:"#8890b5",g:"기타"},
  {k:"기타지출",i:"📦",c:"#718096",g:"기타"},
  {k:"생명보험",i:"🛡️",c:"#667eea",g:"보험"},
  {k:"실손보험",i:"🏥",c:"#764ba2",g:"보험"},
  {k:"자동차보험",i:"🚗",c:"#6b46c1",g:"보험"},
  {k:"연금보험",i:"👴",c:"#553c9a",g:"보험"},
  {k:"기타보험",i:"📋",c:"#44337a",g:"보험"}
];
const IMAP = {};
[...IC,...EC].forEach(function(c){IMAP[c.k]=c.i;});
const GCOLS = ["#6c7bff","#4ecdc4","#ffd166","#ff6b8a","#ff9f43"];
const BDGM = {
  "부동산":"rgba(108,123,255,.15)|#6c7bff","예금·저축":"rgba(78,205,196,.15)|#4ecdc4",
  "주식·ETF":"rgba(255,209,102,.15)|#ffd166","퇴직연금":"rgba(255,159,67,.15)|#ff9f43",
  "금·실물자산":"rgba(247,201,72,.15)|#f7c948","주택담보대출":"rgba(108,123,255,.15)|#6c7bff",
  "전세대출":"rgba(78,205,196,.15)|#4ecdc4","신용대출":"rgba(255,107,138,.15)|#ff6b8a",
  "자동차할부":"rgba(255,209,102,.15)|#ffd166","카드론":"rgba(255,107,138,.15)|#ff6b8a"
};

// ── 초기 데이터 ──────────────────────────────────
var INIT = {
  assets:[
    {id:1,nm:"씨에스윈드",ct:"주식·ETF",ow:"오승헌",cv:4352000,ov:4855500,mm:"국내"},
    {id:2,nm:"아이온큐",ct:"주식·ETF",ow:"오승헌",cv:1323492,ov:1005853,mm:"해외"},
    {id:3,nm:"팔란티어",ct:"주식·ETF",ow:"오승헌",cv:1116338,ov:1144521,mm:"해외"},
    {id:4,nm:"QQQM",ct:"주식·ETF",ow:"오승헌",cv:2791193,ov:2603041,mm:"해외"},
    {id:5,nm:"SCHD",ct:"주식·ETF",ow:"오승헌",cv:1976295,ov:1962242,mm:"해외"},
    {id:6,nm:"달러",ct:"예금·저축",ow:"오승헌",cv:17216,ov:17216,mm:"증권"},
    {id:7,nm:"원화",ct:"예금·저축",ow:"오승헌",cv:8702,ov:8702,mm:"증권"},
    {id:8,nm:"아이온큐",ct:"주식·ETF",ow:"오동주",cv:1392854,ov:1024619,mm:"해외"},
    {id:9,nm:"팔란티어",ct:"주식·ETF",ow:"오동주",cv:1563598,ov:1546954,mm:"해외"},
    {id:10,nm:"QQQ",ct:"주식·ETF",ow:"오동주",cv:968153,ov:913555,mm:"해외"},
    {id:11,nm:"QQQM",ct:"주식·ETF",ow:"오동주",cv:3188989,ov:3028076,mm:"해외"},
    {id:12,nm:"SCHD",ct:"주식·ETF",ow:"오동주",cv:4827389,ov:4523546,mm:"해외"},
    {id:13,nm:"SPYM",ct:"주식·ETF",ow:"오동주",cv:1358144,ov:1315801,mm:"해외"},
    {id:14,nm:"달러",ct:"예금·저축",ow:"오동주",cv:326668,ov:326668,mm:"증권"},
    {id:15,nm:"비트코인",ct:"금·실물자산",ow:"오동주",cv:765000,ov:1095566,mm:""},
    {id:16,nm:"우리은행",ct:"예금·저축",ow:"오동주",cv:2000000,ov:2000000,mm:""},
    {id:17,nm:"우리은행",ct:"예금·저축",ow:"서지은",cv:2000000,ov:2000000,mm:""}
  ],
  txs:[
    {id:1,tp:"income",nm:"급여",ct:"급여",am:3100000,dt:"2026-04-25",mm:"동주"},
    {id:2,tp:"income",nm:"급여",ct:"급여",am:2500000,dt:"2026-04-25",mm:"와이프"},
    {id:3,tp:"expense",nm:"마트 장보기",ct:"식비·장보기",am:180000,dt:"2026-04-24",mm:""},
    {id:4,tp:"expense",nm:"교통카드",ct:"교통·주유",am:80000,dt:"2026-04-23",mm:""},
    {id:5,tp:"expense",nm:"주담대 상환",ct:"대출상환",am:900000,dt:"2026-04-20",mm:""},
    {id:6,tp:"expense",nm:"배달",ct:"외식·배달",am:45000,dt:"2026-04-19",mm:"배민"},
    {id:7,tp:"expense",nm:"병원",ct:"병원·약국",am:50000,dt:"2026-04-18",mm:""},
    {id:8,tp:"income",nm:"부업",ct:"부업·프리랜서",am:200000,dt:"2026-04-15",mm:""},
    {id:9,tp:"expense",nm:"카페",ct:"카페·음료",am:15000,dt:"2026-04-14",mm:""},
    {id:10,tp:"expense",nm:"헬스장",ct:"운동·헬스",am:70000,dt:"2026-04-10",mm:""}
  ],
  loans:[{id:1,nm:"신생아특례 주담대",ct:"주택담보대출",og:380000000,bl:372000000,rt:1.68,my:900000,du:"2054-01-01"}],
  goals:[
    {id:1,nm:"비상금",em:"🛡️",tg:10000000,cv:6200000,dt:"2026-12-31"},
    {id:2,nm:"제주도 여행",em:"✈️",tg:3000000,cv:850000,dt:"2026-08-01"},
    {id:3,nm:"자동차 교체",em:"🚗",tg:30000000,cv:4000000,dt:"2028-01-01"}
  ],
  fixed:[
    {id:1,nm:"신생아특례 주담대",ct:"대출상환",am:900000,day:20},
    {id:2,nm:"관리비",ct:"주거·관리비",am:180000,day:5},
    {id:3,nm:"넷플릭스",ct:"구독·OTT",am:17000,day:8},
    {id:4,nm:"생명보험",ct:"생명보험",am:150000,day:15},
    {id:5,nm:"실손보험",ct:"실손보험",am:80000,day:15}
  ],
  nid:200
};

// ── 상태 ─────────────────────────────────────────
var D = JSON.parse(JSON.stringify(INIT));
var TAB = "ov";
var MODAL = null;
var LKFLT = "";
var FBREADY = false;

// ── 유틸 ─────────────────────────────────────────
function fmt(n) {
  if (n >= 100000000) return (n/100000000).toFixed(1) + "억원";
  return n.toLocaleString() + "원";
}
function today() { return new Date().toISOString().slice(0,10); }
function thismon() { return new Date().toISOString().slice(0,7); }

var fbdb = null;

function save() {
  try { localStorage.setItem("wuri_data", JSON.stringify(D)); } catch(e) {}
}

// ── DOM 유틸 ──────────────────────────────────────
function el(tag, cls, html) {
  var e = document.createElement(tag);
  if (cls) e.className = cls;
  if (html) e.innerHTML = html;
  return e;
}
function div(cls, html) { return el("div", cls, html); }
function span(cls, html) { return el("span", cls, html); }
function btn(cls, text, fn) {
  var b = el("button", cls, text);
  b.onclick = fn;
  return b;
}
function ap(parent) {
  var args = Array.prototype.slice.call(arguments, 1);
  args.forEach(function(c) { if (c) parent.appendChild(c); });
  return parent;
}
function bdg(label) {
  var parts = (BDGM[label] || "rgba(136,144,181,.15)|#8890b5").split("|");
  var s = span("bdg");
  s.style.background = parts[0];
  s.style.color = parts[1];
  s.textContent = label;
  return s;
}
function pbar(pct, color) {
  var w = div("pb");
  var f = div("pbf");
  f.style.width = Math.min(+pct||0, 100) + "%";
  f.style.background = color || "#6c7bff";
  w.appendChild(f);
  return w;
}
function field(label, inputEl) {
  var d = div("fl");
  var lb = el("label"); lb.textContent = label;
  ap(d, lb, inputEl);
  return d;
}
function inp(type, ph, val) {
  var i = document.createElement("input");
  i.type = type || "text";
  i.placeholder = ph || "";
  i.value = val != null ? val : "";
  return i;
}
function sel(opts, val) {
  var s = document.createElement("select");
  opts.forEach(function(o) {
    var op = document.createElement("option");
    op.value = o; op.textContent = o;
    if (o === val) op.selected = true;
    s.appendChild(op);
  });
  return s;
}

// ── 모달 ─────────────────────────────────────────
function openModal(content) {
  closeModal();
  var bg = div("mobg");
  bg.onclick = function(e) { if (e.target === bg) closeModal(); };
  bg.appendChild(content);
  document.body.appendChild(bg);
  MODAL = bg;
}
function closeModal() {
  if (MODAL) { MODAL.remove(); MODAL = null; }
}

// ── 카테고리 버튼 ─────────────────────────────────
function catBtns(cats, current, onChange) {
  var wrap = div("cbwrap");
  cats.forEach(function(c) {
    var b = el("button", "cb" + (c.k === current ? " on" : ""));
    b.textContent = c.i + " " + c.k;
    if (c.k === current) b.style.background = c.c;
    b.onclick = function() { onChange(c.k); };
    wrap.appendChild(b);
  });
  return wrap;
}
function ecatBtns(current, onChange) {
  var wrap = div("");
  var grps = [];
  EC.forEach(function(c) { if (grps.indexOf(c.g) < 0) grps.push(c.g); });
  grps.forEach(function(g) {
    var gl = div("glbl"); gl.textContent = g;
    var row = div("cbwrap");
    EC.filter(function(c){return c.g===g;}).forEach(function(c) {
      var b = el("button", "cb" + (c.k === current ? " on" : ""));
      b.textContent = c.i + " " + c.k;
      if (c.k === current) b.style.background = c.c;
      b.onclick = function() { onChange(c.k); };
      row.appendChild(b);
    });
    ap(wrap, gl, row);
  });
  return wrap;
}

// ── 자산 모달 ─────────────────────────────────────
function openAssetModal(init) {
  var ct = init ? init.ct : "주식·ETF";
  var ow = init ? (init.ow || "오동주") : "오동주";
  var mobox = div("mobox");
  var title = div("motitle"); title.textContent = init ? "✏️ 자산 수정" : "자산 추가";

  var nmI = inp("text", "씨에스윈드, 우리은행", init ? init.nm : "");

  // 소유주
  var owWrap = div("cbwrap");
  function renderOw() {
    owWrap.innerHTML = "";
    OWS.forEach(function(o) {
      var b = el("button", "cb" + (o === ow ? " on" : ""));
      b.textContent = o;
      if (o === ow) b.style.background = OWC[o];
      b.onclick = function() { ow = o; renderOw(); };
      owWrap.appendChild(b);
    });
  }
  renderOw();

  // 분류
  var ctWrap = div("cbwrap");
  var formWrap = div("");
  function renderCt() {
    ctWrap.innerHTML = "";
    ACATS.forEach(function(c) {
      var b = el("button", "cb" + (c === ct ? " on" : ""));
      b.textContent = AICO[c] + " " + c;
      if (c === ct) b.style.background = "#6c7bff";
      b.onclick = function() { ct = c; renderCt(); renderForm(); };
      ctWrap.appendChild(b);
    });
  }
  function renderForm() {
    formWrap.innerHTML = "";
    var cv = init ? init.cv : "";
    var ov = init ? init.ov : "";
    var mm = init ? (init.mm || "") : "";
    var du = init ? (init.du || "") : "";
    var rt = init ? (init.rt || "") : "";
    var cvI, ovI, mmI, duI, rtI;
    if (ct === "부동산") {
      cvI = inp("number","420000000",cv); ovI = inp("number","380000000",ov); mmI = inp("text","성북구 xx동",mm);
      ap(formWrap, field("현재 시세 (원)",cvI), field("취득가 (원)",ovI), field("주소/메모",mmI));
    } else if (ct === "예금·저축") {
      cvI = inp("number","8500000",cv); mmI = inp("text","카카오뱅크",mm); duI = inp("date","",du); rtI = inp("number","3.5",rt);
      ap(formWrap, field("잔액 (원)",cvI), field("금융기관/메모",mmI), field("만기일",duI), field("금리(%)",rtI));
    } else if (ct === "주식·ETF") {
      cvI = inp("number","1500000",cv); ovI = inp("number","1000000",ov); mmI = inp("text","해외, 국내",mm);
      ap(formWrap, field("평가금액 (원)",cvI), field("매입금액 (원)",ovI), field("메모",mmI));
    } else if (ct === "퇴직연금") {
      cvI = inp("number","15000000",cv); mmI = inp("text","삼성생명 DC형",mm); rtI = sel(["","DC","DB","IRP"],rt);
      ap(formWrap, field("평가액 (원)",cvI), field("운용사/상품명",mmI), field("유형",rtI));
    } else if (ct === "금·실물자산") {
      cvI = inp("number","5000000",cv); ovI = inp("number","4000000",ov); mmI = inp("text","금 100g",mm);
      ap(formWrap, field("현재가치 (원)",cvI), field("취득가 (원)",ovI), field("종류/수량",mmI));
    } else {
      cvI = inp("number","0",cv); ovI = inp("number","0",ov); mmI = inp("text","",mm);
      ap(formWrap, field("현재가치 (원)",cvI), field("취득가 (원)",ovI), field("메모",mmI));
    }
  }
  renderCt(); renderForm();

  function save() {
    var nm = nmI.value.trim();
    if (!nm) return;
    var inps = formWrap.querySelectorAll("input,select");
    var vals = [];
    inps.forEach(function(i){ vals.push(i.value); });
    var cv=0,ov=0,mm="",du="",rt="";
    if (ct==="부동산"){ cv=parseFloat(vals[0])||0; ov=parseFloat(vals[1])||0; mm=vals[2]||""; }
    else if (ct==="예금·저축"){ cv=parseFloat(vals[0])||0; mm=vals[1]||""; du=vals[2]||""; rt=vals[3]||""; }
    else if (ct==="주식·ETF"){ cv=parseFloat(vals[0])||0; ov=parseFloat(vals[1])||0; mm=vals[2]||""; }
    else if (ct==="퇴직연금"){ cv=parseFloat(vals[0])||0; mm=vals[1]||""; rt=vals[2]||""; }
    else if (ct==="금·실물자산"){ cv=parseFloat(vals[0])||0; ov=parseFloat(vals[1])||0; mm=vals[2]||""; }
    else { cv=parseFloat(vals[0])||0; ov=parseFloat(vals[1])||0; mm=vals[2]||""; }
    if (!cv) return;
    var row = {nm:nm,ct:ct,ow:ow,cv:cv,ov:ov||cv,mm:mm,du:du,rt:rt};
    if (init) { row.id=init.id; D.assets=D.assets.map(function(a){return a.id===init.id?row:a;}); }
    else { row.id=D.nid++; D.assets.push(row); }
    save(); closeModal(); render();
  }
  function del() {
    D.assets=D.assets.filter(function(a){return a.id!==init.id;});
    save(); closeModal(); render();
  }

  var foot = div("mofoot");
  ap(foot, btn("bn","취소",closeModal));
  if (init) ap(foot, btn("bd","🗑 삭제",del));
  ap(foot, btn("bp","저장",save));

  ap(mobox, title,
    field("자산명",nmI),
    field("소유주",owWrap),
    field("분류",ctWrap),
    formWrap, foot
  );
  openModal(mobox);
}

// ── 거래 모달 ─────────────────────────────────────
function openTxModal() {
  var tp = "expense", ct = "식비·장보기";
  var mobox = div("mobox");
  ap(mobox, (function(){var d=div("motitle");d.textContent="거래 추가";return d;})());

  // 유형 토글
  var tpWrap = div("cbwrap");
  function renderTp() {
    tpWrap.innerHTML = "";
    [["expense","지출","#ff6b8a"],["income","수입","#4caf88"]].forEach(function(arr) {
      var b = el("button","cb"+(tp===arr[0]?" on":""));
      b.textContent = arr[1];
      if (tp===arr[0]) b.style.background = arr[2];
      b.onclick = function() { tp=arr[0]; ct=(tp==="income"?"급여":"식비·장보기"); renderTp(); renderCatWrap(); };
      tpWrap.appendChild(b);
    });
  }

  var catWrap = div("");
  function renderCatWrap() {
    catWrap.innerHTML = "";
    if (tp==="income") {
      catWrap.appendChild(catBtns(IC, ct, function(k){ct=k; renderCatWrap();}));
    } else {
      catWrap.appendChild(ecatBtns(ct, function(k){ct=k; renderCatWrap();}));
    }
  }
  renderTp(); renderCatWrap();

  var nmI=inp("text","마트 장보기"), amI=inp("number","0"), dtI=inp("date","",today()), mmI=inp("text","선택사항");

  function save() {
    var nm=nmI.value.trim(), am=parseFloat(amI.value)||0;
    if(!nm||!am) return;
    D.txs.push({id:D.nid++,tp:tp,nm:nm,ct:ct,am:am,dt:dtI.value||today(),mm:mmI.value});
    save(); closeModal(); render();
  }

  var foot=div("mofoot");
  ap(foot, btn("bn","취소",closeModal), btn("bp","저장",save));
  ap(mobox, field("유형",tpWrap), field("카테고리",catWrap),
    field("내용",nmI), field("금액 (원)",amI), field("날짜",dtI), field("메모",mmI), foot);
  openModal(mobox);
}

// ── 대출 모달 ─────────────────────────────────────
function openLoanModal(init) {
  var mobox=div("mobox");
  var title=div("motitle"); title.textContent=init?"✏️ 대출 수정":"대출 추가";
  var nmI=inp("text","신생아특례 주담대",init?init.nm:"");
  var ctI=sel(["주택담보대출","전세대출","신용대출","자동차할부","카드론","기타"],init?init.ct:"주택담보대출");
  var ogI=inp("number","0",init?init.og:""), blI=inp("number","0",init?init.bl:"");
  var rtI=inp("number","1.68",init?init.rt:""), myI=inp("number","0",init?init.my:""), duI=inp("date","",init?init.du:"");
  function save(){
    var nm=nmI.value.trim(); if(!nm)return;
    var og=parseFloat(ogI.value)||0;
    var row={nm:nm,ct:ctI.value,og:og,bl:parseFloat(blI.value)||og,rt:parseFloat(rtI.value)||0,my:parseFloat(myI.value)||0,du:duI.value};
    if(init){row.id=init.id;D.loans=D.loans.map(function(l){return l.id===init.id?row:l;});}
    else{row.id=D.nid++;D.loans.push(row);}
    save();closeModal();render();
  }
  function del(){D.loans=D.loans.filter(function(l){return l.id!==init.id;});save();closeModal();render();}
  var foot=div("mofoot");
  ap(foot,btn("bn","취소",closeModal));
  if(init)ap(foot,btn("bd","🗑 삭제",del));
  ap(foot,btn("bp","저장",save));
  ap(mobox,title,field("대출명",nmI),field("분류",ctI),field("원금 (원)",ogI),field("잔액 (원)",blI),
    field("금리 (%)",rtI),field("월 상환액 (원)",myI),field("만기일",duI),foot);
  openModal(mobox);
}

// ── 목표 모달 ─────────────────────────────────────
function openGoalModal(init) {
  var mobox=div("mobox");
  var title=div("motitle"); title.textContent=init?"✏️ 목표 수정":"목표 추가";
  var nmI=inp("text","비상금, 여행",init?init.nm:"");
  var emI=inp("text","🎯",init?init.em:"🎯"); emI.style.width="65px";
  var tgI=inp("number","0",init?init.tg:""), cvI=inp("number","0",init?init.cv:""), dtI=inp("date","",init?init.dt:"");
  function save(){
    var nm=nmI.value.trim(),tg=parseFloat(tgI.value)||0; if(!nm||!tg)return;
    var row={nm:nm,em:emI.value||"🎯",tg:tg,cv:parseFloat(cvI.value)||0,dt:dtI.value};
    if(init){row.id=init.id;D.goals=D.goals.map(function(g){return g.id===init.id?row:g;});}
    else{row.id=D.nid++;D.goals.push(row);}
    save();closeModal();render();
  }
  function del(){D.goals=D.goals.filter(function(g){return g.id!==init.id;});save();closeModal();render();}
  var foot=div("mofoot");
  ap(foot,btn("bn","취소",closeModal));
  if(init)ap(foot,btn("bd","🗑 삭제",del));
  ap(foot,btn("bp","저장",save));
  ap(mobox,title,field("목표명",nmI),field("이모지",emI),field("목표금액 (원)",tgI),field("현재 적립액 (원)",cvI),field("목표일",dtI),foot);
  openModal(mobox);
}

// ── 고정비용 모달 ─────────────────────────────────
function openFixedModal(init) {
  var mobox=div("mobox");
  var title=div("motitle"); title.textContent=init?"✏️ 고정비용 수정":"고정비용 추가";
  var nmI=inp("text","관리비, 넷플릭스",init?init.nm:"");
  var amI=inp("number","0",init?init.am:"");
  var dayI=inp("number","1",init?init.day:1); dayI.style.width="70px";
  var ct=init?init.ct:"주거·관리비";
  var catWrap=div("");
  function renderCat(){catWrap.innerHTML="";catWrap.appendChild(ecatBtns(ct,function(k){ct=k;renderCat();}));}
  renderCat();
  var dayWrap=div(""); dayWrap.style.display="flex"; dayWrap.style.alignItems="center"; dayWrap.style.gap="8px";
  var dayLbl=span(""); dayLbl.textContent="일 (매월)"; dayLbl.style.cssText="font-size:12px;color:#8890b5";
  ap(dayWrap,dayI,dayLbl);
  function save(){
    var nm=nmI.value.trim(),am=parseFloat(amI.value)||0; if(!nm||!am)return;
    var row={nm:nm,ct:ct,am:am,day:parseInt(dayI.value)||1};
    if(!D.fixed)D.fixed=[];
    if(init){row.id=init.id;D.fixed=D.fixed.map(function(f){return f.id===init.id?row:f;});}
    else{row.id=D.nid++;D.fixed.push(row);}
    save();closeModal();render();
  }
  function del(){D.fixed=D.fixed.filter(function(f){return f.id!==init.id;});save();closeModal();render();}
  var foot=div("mofoot");
  ap(foot,btn("bn","취소",closeModal));
  if(init)ap(foot,btn("bd","🗑 삭제",del));
  ap(foot,btn("bp","저장",save));
  ap(mobox,title,field("항목명",nmI),field("카테고리",catWrap),field("금액 (원)",amI),field("매월 며칠?",dayWrap),foot);
  openModal(mobox);
}

// ── 렌더 함수들 ───────────────────────────────────
function renderOV() {
  var ta=D.assets.reduce(function(s,a){return s+a.cv;},0);
  var tl=D.loans.reduce(function(s,l){return s+l.bl;},0);
  var tm=thismon(),mx=D.txs.filter(function(t){return t.dt.slice(0,7)===tm;});
  var inc=mx.filter(function(t){return t.tp==="income";}).reduce(function(s,t){return s+t.am;},0);
  var exp=mx.filter(function(t){return t.tp==="expense";}).reduce(function(s,t){return s+t.am;},0);

  var cards=div("g2");
  [{l:"순자산",v:fmt(ta-tl),c:"#6c7bff"},{l:"이달수입",v:"+"+fmt(inc),c:"#4ecdc4"},
   {l:"이달지출",v:"-"+fmt(exp),c:"#ff6b8a"},{l:"총부채",v:fmt(tl),c:"#ffd166"}].forEach(function(s){
    var card=div("card");
    var lbl=div("clbl"); lbl.textContent=s.l;
    var val=div("cval"); val.textContent=s.v; val.style.color=s.c;
    ap(card,lbl,val); cards.appendChild(card);
  });

  // 최근 거래
  var recentBox=div("box");
  var rh=div("bh"); var rht=div(""); rht.innerHTML="<h3>최근 거래</h3>"; recentBox.appendChild(rh); ap(rh,rht);
  var recent=[].concat(D.txs).sort(function(a,b){return b.dt.localeCompare(a.dt);}).slice(0,5);
  recent.forEach(function(t){
    var row=div("item");
    var ico=div("ico"); ico.textContent=IMAP[t.ct]||"📦";
    ico.style.background=t.tp==="income"?"rgba(76,175,136,.15)":"rgba(255,107,138,.15)";
    var info=div(""); info.style.flex="1";
    var nm=div(""); nm.style.cssText="font-size:12px;font-weight:600"; nm.textContent=t.nm;
    var sub=div(""); sub.style.cssText="font-size:10px;color:#8890b5"; sub.textContent=t.dt+" · "+t.ct;
    ap(info,nm,sub);
    var am=span(""); am.style.cssText="font-size:12px;font-weight:700;color:"+(t.tp==="income"?"#4caf88":"#ff6b8a");
    am.textContent=(t.tp==="income"?"+":"-")+fmt(t.am);
    ap(row,ico,info,am); recentBox.appendChild(row);
  });
  if(!recent.length){var empty=div(""); empty.style.cssText="text-align:center;padding:20px;color:#8890b5;font-size:12px"; empty.textContent="거래 없음"; recentBox.appendChild(empty);}

  var wrap=div(""); ap(wrap,cards,recentBox);
  return wrap;
}

function renderAS() {
  var box=div("box");
  var bh=div("bh");
  var title=div(""); title.innerHTML="<h3>자산 목록</h3>";
  var addBtn=btn("bp","+ 추가",function(){openAssetModal(null);});
  ap(bh,title,addBtn); box.appendChild(bh);

  var tCv=D.assets.reduce(function(s,a){return s+a.cv;},0);
  var tOv=D.assets.reduce(function(s,a){return s+a.ov;},0);
  var tG=tCv-tOv;

  var scroll=div("tscroll");
  var table=document.createElement("table");
  var thead=document.createElement("thead");
  var htr=document.createElement("tr");
  ["소유주","자산명","분류","평가금액","매입금액","손익","수익률",""].forEach(function(h){
    var th=document.createElement("th"); th.textContent=h; htr.appendChild(th);
  });
  thead.appendChild(htr); table.appendChild(thead);

  var tbody=document.createElement("tbody");
  D.assets.forEach(function(a){
    var g=a.cv-a.ov, pct=a.ov?(g/a.ov*100).toFixed(1):"0.0", pos=g>=0;
    var tr=document.createElement("tr");

    // 소유주
    var td0=document.createElement("td");
    var owbdg=span("bdg"); owbdg.textContent=a.ow||"-";
    owbdg.style.background=OWBG[a.ow]||"rgba(136,144,181,.15)";
    owbdg.style.color=OWC[a.ow]||"#8890b5";
    td0.appendChild(owbdg); tr.appendChild(td0);

    // 자산명
    var td1=document.createElement("td");
    var nm=document.createElement("strong"); nm.style.fontSize="12px";
    nm.textContent=AICO[a.ct]+" "+a.nm;
    td1.appendChild(nm);
    if(a.mm){var sub=div(""); sub.style.cssText="font-size:10px;color:#8890b5"; sub.textContent=a.mm; td1.appendChild(sub);}
    tr.appendChild(td1);

    // 분류
    var td2=document.createElement("td"); td2.appendChild(bdg(a.ct)); tr.appendChild(td2);

    // 금액들
    [fmt(a.cv), fmt(a.ov)].forEach(function(v){
      var td=document.createElement("td"); td.style.fontSize="12px"; td.textContent=v; tr.appendChild(td);
    });

    // 손익
    var tdg=document.createElement("td"); tdg.style.cssText="font-size:12px;font-weight:600;color:"+(pos?"#4caf88":"#ff6b8a");
    tdg.textContent=(pos?"+":"")+fmt(g); tr.appendChild(tdg);

    // 수익률
    var tdp=document.createElement("td"); tdp.style.cssText="font-size:11px;color:"+(pos?"#4caf88":"#ff6b8a");
    tdp.textContent=(pos?"+":"")+pct+"%"; tr.appendChild(tdp);

    // 버튼
    var tdb=document.createElement("td"); tdb.style.whiteSpace="nowrap";
    var eb=btn("be","✏️",(function(asset){return function(){openAssetModal(asset);};})(a));
    var db=btn("bx","✕",(function(id){return function(){D.assets=D.assets.filter(function(x){return x.id!==id;});save();render();};})(a.id));
    ap(tdb,eb,document.createTextNode(" "),db); tr.appendChild(tdb);

    tbody.appendChild(tr);
  });
  table.appendChild(tbody);

  // 합계 행
  var tfoot=document.createElement("tfoot");
  var ftr=document.createElement("tr");
  var f0=document.createElement("td"); f0.colSpan=3; f0.textContent="합계"; ftr.appendChild(f0);
  [fmt(tCv), fmt(tOv)].forEach(function(v){
    var td=document.createElement("td"); td.textContent=v; ftr.appendChild(td);
  });
  var fg=document.createElement("td"); fg.style.color=tG>=0?"#4caf88":"#ff6b8a";
  fg.textContent=(tG>=0?"+":"")+fmt(tG); ftr.appendChild(fg);
  var fp=document.createElement("td"); fp.style.cssText="font-size:11px;color:"+(tG>=0?"#4caf88":"#ff6b8a");
  fp.textContent=(tG>=0?"+":"")+(tOv?(tG/tOv*100).toFixed(1):"0")+"%"; ftr.appendChild(fp);
  var fe=document.createElement("td"); ftr.appendChild(fe);
  tfoot.appendChild(ftr); table.appendChild(tfoot);

  scroll.appendChild(table); box.appendChild(scroll);
  return box;
}

function renderLK() {
  var tm=thismon(),mx=D.txs.filter(function(t){return t.dt.slice(0,7)===tm;});
  var inc=mx.filter(function(t){return t.tp==="income";}).reduce(function(s,t){return s+t.am;},0);
  var exp=mx.filter(function(t){return t.tp==="expense";}).reduce(function(s,t){return s+t.am;},0);
  var ec={};
  mx.filter(function(t){return t.tp==="expense";}).forEach(function(t){ec[t.ct]=(ec[t.ct]||0)+t.am;});
  var maxC=Math.max.apply(null,[0].concat(Object.values(ec)));

  // 요약
  var sumBox=div("box");
  var sh=div("bh"); sh.innerHTML="<h3>이번 달</h3>"; sumBox.appendChild(sh);
  var sumBody=div(""); sumBody.style.padding="11px 13px";
  [["수입","#4caf88","+"+fmt(inc)],["지출","#ff6b8a","-"+fmt(exp)],
   ["잔여",inc-exp>=0?"#6c7bff":"#ff6b8a",(inc-exp>=0?"+":"")+fmt(inc-exp)]].forEach(function(arr,i,a){
    var row=div(""); row.style.cssText="display:flex;justify-content:space-between;align-items:center;padding:7px 0;border-bottom:"+(i<a.length-1?"1px solid #2e3352":"none");
    var lbl=span(""); lbl.style.cssText="font-size:12px;color:#8890b5"; lbl.textContent=arr[0];
    var val=span(""); val.style.cssText="font-size:13px;font-weight:700;color:"+arr[1]; val.textContent=arr[2];
    ap(row,lbl,val); sumBody.appendChild(row);
  });
  sumBox.appendChild(sumBody);

  // 거래 목록
  var listBox=div("box");
  var lh=div("bh");
  var lt=div(""); lt.innerHTML="<h3>거래 내역</h3>";
  var fltSel=document.createElement("select");
  fltSel.style.cssText="padding:4px 8px;background:#22263a;border:1px solid #2e3352;border-radius:7px;color:#e8eaf6;font-size:11px;font-family:inherit";
  ["전체","수입","지출"].forEach(function(o){
    var op=document.createElement("option"); op.value=o==="전체"?"":o==="수입"?"income":"expense"; op.textContent=o;
    if(op.value===LKFLT)op.selected=true;
    fltSel.appendChild(op);
  });
  fltSel.onchange=function(){LKFLT=fltSel.value; renderLKList(listBox);};
  var addBtn=btn("bp","+ 추가",openTxModal);
  var lhr=div("bhr"); ap(lhr,fltSel,addBtn);
  ap(lh,lt,lhr); listBox.appendChild(lh);
  renderLKList(listBox);

  var wrap=div(""); ap(wrap,sumBox,listBox);
  return wrap;
}

function renderLKList(listBox) {
  // 기존 아이템 제거 (헤더 제외)
  var children=Array.prototype.slice.call(listBox.children);
  children.forEach(function(c){
    if(!c.classList.contains("bh"))listBox.removeChild(c);
  });
  var list=[].concat(D.txs).sort(function(a,b){return b.dt.localeCompare(a.dt);}).filter(function(t){return !LKFLT||t.tp===LKFLT;});
  if(!list.length){
    var empty=div(""); empty.style.cssText="text-align:center;padding:20px;color:#8890b5;font-size:12px"; empty.textContent="거래 없음"; listBox.appendChild(empty); return;
  }
  list.forEach(function(t){
    var ci=t.tp==="income"?IC.filter(function(c){return c.k===t.ct;})[0]:EC.filter(function(c){return c.k===t.ct;})[0];
    var row=div("item");
    var ico=div("ico"); ico.textContent=(ci?ci.i:"📦");
    ico.style.background=t.tp==="income"?"rgba(76,175,136,.15)":"rgba(255,107,138,.15)";
    var info=div(""); info.style.flex="1";
    var nm=div(""); nm.style.cssText="font-size:12px;font-weight:600"; nm.textContent=t.nm+(t.mm?" ("+t.mm+")":"");
    var sub=div(""); sub.style.cssText="font-size:10px;color:#8890b5"; sub.textContent=t.dt+" · "+t.ct;
    ap(info,nm,sub);
    var right=div(""); right.style.cssText="display:flex;align-items:center;gap:7px";
    var am=span(""); am.style.cssText="font-size:12px;font-weight:700;color:"+(t.tp==="income"?"#4caf88":"#ff6b8a");
    am.textContent=(t.tp==="income"?"+":"-")+fmt(t.am);
    var db=btn("bx","✕",(function(id){return function(){D.txs=D.txs.filter(function(x){return x.id!==id;});save();render();};})(t.id));
    ap(right,am,db); ap(row,ico,info,right); listBox.appendChild(row);
  });
}

function renderLN() {
  var tbl=D.loans.reduce(function(s,l){return s+l.bl;},0);
  var tog=D.loans.reduce(function(s,l){return s+l.og;},0);
  var tmy=D.loans.reduce(function(s,l){return s+l.my;},0);

  var box=div("box");
  var bh=div("bh"); ap(bh,(function(){var d=div("");d.innerHTML="<h3>대출·부채</h3>";return d;})(),btn("bp","+ 추가",function(){openLoanModal(null);}));
  box.appendChild(bh);

  if(!D.loans.length){
    var e=div(""); e.style.cssText="text-align:center;padding:20px;color:#8890b5;font-size:12px"; e.textContent="대출 정보를 추가해주세요"; box.appendChild(e);
  } else {
    D.loans.forEach(function(l){
      var row=div(""); row.style.cssText="padding:11px 13px;border-bottom:1px solid rgba(46,51,82,.3)";
      var top=div(""); top.style.cssText="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:6px";
      var left=div(""); var nm=div(""); nm.style.cssText="font-size:13px;font-weight:600;margin-bottom:4px"; nm.textContent=l.nm;
      ap(left,nm,bdg(l.ct));
      var right=div(""); right.style.cssText="display:flex;gap:5px;align-items:center";
      var am=span(""); am.style.cssText="font-size:13px;font-weight:700;color:#ff6b8a"; am.textContent=fmt(l.bl);
      var eb=btn("be","✏️",(function(loan){return function(){openLoanModal(loan);};})(l));
      var db=btn("bx","✕",(function(id){return function(){D.loans=D.loans.filter(function(x){return x.id!==id;});save();render();};})(l.id));
      ap(right,am,eb,db); ap(top,left,right); row.appendChild(top);
      var info=div(""); info.style.cssText="display:flex;gap:12px;font-size:11px;color:#8890b5;margin-bottom:5px";
      ["금리 "+l.rt+"%","월상환 "+fmt(l.my),"만기 "+(l.du||"-")].forEach(function(t){var s=span("");s.textContent=t;info.appendChild(s);});
      row.appendChild(info);
      var p=l.og?((l.og-l.bl)/l.og*100):0; row.appendChild(pbar(p,"#6c7bff"));
      box.appendChild(row);
    });
  }

  // 요약
  var sumBox=div("box");
  var sh=div("bh"); sh.innerHTML="<h3>부채 현황</h3>"; sumBox.appendChild(sh);
  var sb=div(""); sb.style.padding="11px 13px";
  [["총 잔액",fmt(tbl),"#ff6b8a"],["월 상환",fmt(tmy)+"/월",""],["상환 완료",fmt(tog-tbl),"#4caf88"]].forEach(function(arr){
    var row=div(""); row.style.cssText="display:flex;justify-content:space-between;margin-bottom:9px";
    var lbl=span(""); lbl.style.cssText="font-size:12px;color:#8890b5"; lbl.textContent=arr[0];
    var val=span(""); val.style.cssText="font-size:12px;font-weight:700;color:"+(arr[2]||"#e8eaf6"); val.textContent=arr[1];
    ap(row,lbl,val); sb.appendChild(row);
  });
  sumBox.appendChild(sb);

  var wrap=div(""); ap(wrap,box,sumBox); return wrap;
}

function renderGL() {
  var addWrap=div(""); addWrap.style.cssText="display:flex;justify-content:flex-end;margin-bottom:10px";
  addWrap.appendChild(btn("bp","+ 목표 추가",function(){openGoalModal(null);}));
  var grid=div("g2");
  D.goals.forEach(function(g,i){
    var col=GCOLS[i%GCOLS.length];
    var card=div("goal-card"); card.style.cssText="background:#1a1d27;border:1px solid #2e3352;border-radius:11px;padding:12px 13px";
    var top=div(""); top.style.cssText="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:7px";
    var left=div(""); var nm=div(""); nm.style.cssText="font-size:13px;font-weight:600"; nm.textContent=g.nm;
    var dt=div(""); dt.style.cssText="font-size:10px;color:#8890b5;margin-top:1px"; dt.textContent=g.dt||"기한 미설정";
    ap(left,nm,dt);
    var right=div(""); right.style.cssText="display:flex;flex-direction:column;align-items:flex-end;gap:4px";
    var em=div(""); em.style.fontSize="17px"; em.textContent=g.em||"🎯";
    var btns=div(""); btns.style.cssText="display:flex;gap:3px";
    var eb=btn("be","✏️",(function(goal){return function(){openGoalModal(goal);};})(g));
    var db=btn("bx","✕",(function(id){return function(){D.goals=D.goals.filter(function(x){return x.id!==id;});save();render();};})(g.id));
    ap(btns,eb,db); ap(right,em,btns); ap(top,left,right); card.appendChild(top);
    var pct=g.tg?Math.min(g.cv/g.tg*100,100).toFixed(0):0;
    var pctD=div(""); pctD.style.cssText="font-size:17px;font-weight:700;color:"+col; pctD.textContent=pct+"%";
    card.appendChild(pctD); card.appendChild(pbar(pct,col));
    var sub=div(""); sub.style.cssText="display:flex;justify-content:space-between;font-size:10px;color:#8890b5;margin-top:5px";
    var s1=span(""); s1.textContent=fmt(g.cv); var s2=span(""); s2.textContent="목표 "+fmt(g.tg);
    ap(sub,s1,s2); card.appendChild(sub); grid.appendChild(card);
  });
  var wrap=div(""); ap(wrap,addWrap,grid); return wrap;
}

function renderFX() {
  var now=new Date(),ym=thismon();
  var fixed=D.fixed||[];
  var total=fixed.reduce(function(s,f){return s+f.am;},0);
  var addWrap=div(""); addWrap.style.cssText="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px";
  var desc=span(""); desc.style.cssText="font-size:11px;color:#8890b5"; desc.textContent="매달 자동으로 가계부에 추가돼요";
  addWrap.appendChild(desc); addWrap.appendChild(btn("bp","+ 추가",function(){openFixedModal(null);}));
  var box=div("box");
  var bh=div("bh"); bh.innerHTML="<h3>고정비용 목록</h3>"; box.appendChild(bh);
  if(!fixed.length){
    var e=div(""); e.style.cssText="text-align:center;padding:20px;color:#8890b5;font-size:12px"; e.textContent="고정비용을 추가해주세요"; box.appendChild(e);
  } else {
    fixed.forEach(function(fx){
      var applied=D.txs.some(function(t){return t.fixedId===fx.id&&t.dt.slice(0,7)===ym;});
      var dueDate=new Date(now.getFullYear(),now.getMonth(),fx.day);
      var row=div("item");
      var ci=EC.filter(function(c){return c.k===fx.ct;})[0];
      var ico=div("ico"); ico.textContent=(ci?ci.i:"📦"); ico.style.background="rgba(255,107,138,.15)";
      var info=div(""); info.style.flex="1";
      var nm=div(""); nm.style.cssText="font-size:12px;font-weight:600"; nm.textContent=fx.nm;
      var sub=div(""); sub.style.cssText="font-size:10px;color:#8890b5"; sub.textContent=fx.ct+" · 매월 "+fx.day+"일 · "+fmt(fx.am);
      ap(info,nm,sub);
      var right=div(""); right.style.cssText="display:flex;gap:5px;align-items:center";
      var status;
      if(applied){status=span(""); status.style.cssText="font-size:10px;color:#4caf88;background:rgba(76,175,136,.12);padding:2px 7px;border-radius:18px"; status.textContent="✅ 적용됨";}
      else if(now<dueDate){status=span(""); status.style.cssText="font-size:10px;color:#ffd166;background:rgba(255,209,102,.12);padding:2px 7px;border-radius:18px"; status.textContent="⏳ "+fx.day+"일 예정";}
      else{status=btn("","지금 적용",(function(f){return function(){var dt=ym+"-"+String(f.day).padStart(2,"0");D.txs.push({id:D.nid++,tp:"expense",nm:f.nm,ct:f.ct,am:f.am,dt:dt,mm:"고정",fixed:true,fixedId:f.id});save();render();};})(fx)); status.style.cssText="font-size:10px;color:#6c7bff;background:rgba(108,123,255,.15);padding:2px 7px;border-radius:18px;border:none;cursor:pointer";}
      var eb=btn("be","✏️",(function(f){return function(){openFixedModal(f);};})(fx));
      var db=btn("bx","✕",(function(id){return function(){D.fixed=D.fixed.filter(function(x){return x.id!==id;});save();render();};})(fx.id));
      ap(right,status,eb,db); ap(row,ico,info,right); box.appendChild(row);
    });
    var foot=div(""); foot.style.cssText="padding:8px 13px;background:rgba(108,123,255,.06);border-top:1px solid #2e3352;display:flex;justify-content:space-between;font-size:12px";
    var fl=span(""); fl.style.color="#8890b5"; fl.textContent="월 고정 지출 합계";
    var fv=span(""); fv.style.cssText="font-weight:700;color:#ff6b8a"; fv.textContent=fmt(total);
    ap(foot,fl,fv); box.appendChild(foot);
  }
  var wrap=div(""); ap(wrap,addWrap,box); return wrap;
}

// ── 메인 렌더 ─────────────────────────────────────
function render() {
  var app=document.getElementById("app");
  app.innerHTML="";

  // 네비게이션
  var nav=div("nav");
  var logoWrap=div("");
  var logo=span("logo"); logo.textContent="우리집 자산관리";
  var sync=span("sync"); sync.textContent="💾 저장됨";
  ap(logoWrap,logo,sync);

  var TABS=[["ov","📊"],["as","🏠"],["lk","📒"],["fx","🔁"],["ln","💳"],["gl","🎯"]];
  var tabs=div("tabs");
  TABS.forEach(function(arr){
    var b=el("button","tab"+(TAB===arr[0]?" on":""),arr[1]);
    b.onclick=(function(k){return function(){TAB=k;render();};})(arr[0]);
    tabs.appendChild(b);
  });
  ap(nav,logoWrap,tabs); app.appendChild(nav);

  // 페이지
  var NAMES={"ov":"대시보드","as":"자산현황","lk":"가계부","fx":"고정비용","ln":"대출","gl":"목표"};
  var page=div("page");
  var ptitle=div("ptitle"); ptitle.textContent=NAMES[TAB]||""; page.appendChild(ptitle);

  var content;
  try {
    if(TAB==="ov") content=renderOV();
    else if(TAB==="as") content=renderAS();
    else if(TAB==="lk") content=renderLK();
    else if(TAB==="ln") content=renderLN();
    else if(TAB==="gl") content=renderGL();
    else if(TAB==="fx") content=renderFX();
  } catch(e) {
    content=div(""); content.style.cssText="padding:20px;color:#ff6b8a;font-size:12px"; content.textContent="오류: "+e.message;
  }
  if(content) page.appendChild(content);
  app.appendChild(page);

  // 고정비용 자동 적용
  try {
    var now2=new Date(),ym2=thismon();
    var changed=false;
    (D.fixed||[]).forEach(function(fx){
      var already=D.txs.some(function(t){return t.fixedId===fx.id&&t.dt.slice(0,7)===ym2;});
      var due=new Date(now2.getFullYear(),now2.getMonth(),fx.day);
      if(!already&&now2>=due){
        D.txs.push({id:D.nid++,tp:"expense",nm:fx.nm,ct:fx.ct,am:fx.am,dt:ym2+"-"+String(fx.day).padStart(2,"0"),mm:"고정",fixed:true,fixedId:fx.id});
        changed=true;
      }
    });
    if(changed) save();
  } catch(e){}
}

// 초기 렌더
try {
  var saved=localStorage.getItem("wuri_data");
  if(saved) D=JSON.parse(saved);
} catch(e){}
render();
</script>
</body>
</html>
