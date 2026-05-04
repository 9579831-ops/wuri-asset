[wuri.html](https://github.com/user-attachments/files/27329371/wuri.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>우리집 자산관리</title>
<script>
// Firebase SDK (모듈 방식 아닌 compat 버전)
</script>
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Apple SD Gothic Neo','Malgun Gothic',sans-serif;background:#0f1117;color:#e8eaf6;min-height:100vh;font-size:14px}
button{cursor:pointer;font-family:inherit;border:none;outline:none;-webkit-tap-highlight-color:transparent}
input,select{font-family:inherit;outline:none;box-sizing:border-box}
/* 네비게이션 */
.nav{background:#1a1d27;border-bottom:1px solid #2e3352;padding:10px 14px;position:sticky;top:0;z-index:100;display:flex;align-items:center;justify-content:space-between}
.logo{font-size:15px;font-weight:700;color:#6c7bff}
.tabs{display:flex;gap:2px;background:#0f1117;border-radius:9px;padding:2px}
.tab{padding:6px 10px;border-radius:7px;font-size:13px;font-weight:600;color:#8890b5;background:transparent;transition:all .15s}
.tab.on{background:#6c7bff;color:#fff}
/* 페이지 */
.page{padding:14px}
/* 카드 그리드 */
.g2{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:12px}
.card{background:#1a1d27;border:1px solid #2e3352;border-radius:12px;padding:12px}
.card-lbl{font-size:10px;color:#8890b5;text-transform:uppercase;letter-spacing:.8px;margin-bottom:4px}
.card-val{font-size:15px;font-weight:700}
/* 박스 */
.box{background:#1a1d27;border:1px solid #2e3352;border-radius:12px;overflow:hidden;margin-bottom:12px}
.bh{display:flex;align-items:center;justify-content:space-between;padding:10px 13px;border-bottom:1px solid #2e3352}
.bh-title{font-size:13px;font-weight:600}
.bh-right{display:flex;gap:6px;align-items:center}
/* 아이템 */
.item{display:flex;align-items:center;gap:9px;padding:9px 13px;border-bottom:1px solid rgba(46,51,82,.35)}
.item:last-child{border-bottom:none}
.ico{width:28px;height:28px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:14px;flex-shrink:0}
/* 테이블 */
.tscroll{overflow-x:auto;-webkit-overflow-scrolling:touch}
table{width:100%;border-collapse:collapse;min-width:480px}
th{font-size:10px;color:#8890b5;text-transform:uppercase;padding:7px 9px;text-align:left;background:#22263a;border-bottom:1px solid #2e3352;white-space:nowrap}
td{padding:7px 9px;font-size:12px;border-bottom:1px solid rgba(46,51,82,.3);vertical-align:middle}
tfoot td{background:#22263a;border-top:2px solid #2e3352;font-weight:700}
/* 뱃지 */
.bdg{display:inline-block;padding:2px 8px;border-radius:18px;font-size:10px;font-weight:600}
/* 프로그레스 바 */
.pb{height:5px;background:#22263a;border-radius:3px;overflow:hidden;margin-top:4px}
.pbf{height:100%;border-radius:3px;transition:width .3s}
/* 버튼 */
.btn-p{padding:7px 13px;border-radius:8px;font-size:12px;font-weight:600;background:#6c7bff;color:#fff}
.btn-n{padding:7px 13px;border-radius:8px;font-size:12px;font-weight:600;background:#22263a;color:#8890b5}
.btn-d{padding:7px 13px;border-radius:8px;font-size:12px;font-weight:600;background:rgba(255,107,138,.2);color:#ff6b8a}
.btn-e{padding:5px 8px;border-radius:7px;font-size:13px;background:rgba(108,123,255,.15);color:#6c7bff}
.btn-x{padding:5px 8px;border-radius:7px;font-size:13px;background:rgba(255,107,138,.15);color:#ff6b8a}
/* 모달 */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.8);z-index:500;display:flex;align-items:center;justify-content:center;padding:16px}
.modal{background:#1a1d27;border:1px solid #2e3352;border-radius:16px;padding:18px;width:100%;max-width:460px;max-height:88vh;overflow-y:auto}
.modal-title{font-size:15px;font-weight:700;margin-bottom:14px}
.modal-footer{display:flex;gap:7px;justify-content:flex-end;margin-top:14px}
/* 폼 필드 */
.field{margin-bottom:11px}
.field label{display:block;font-size:11px;color:#8890b5;margin-bottom:4px;font-weight:500}
.field input,.field select{width:100%;padding:9px 11px;background:#22263a;border:1px solid #2e3352;border-radius:8px;color:#e8eaf6;font-size:13px}
/* 카테고리 선택 버튼 */
.cat-wrap{display:flex;flex-wrap:wrap;gap:5px}
.cat-btn{padding:5px 9px;border-radius:18px;font-size:11px;font-weight:600;background:#22263a;color:#8890b5;border:1px solid #2e3352;cursor:pointer;-webkit-tap-highlight-color:transparent}
.cat-btn.on{border:none;color:#fff}
.grp-lbl{font-size:9px;color:#8890b5;text-transform:uppercase;letter-spacing:.5px;margin:6px 0 3px}
/* 빈 상태 */
.empty{text-align:center;padding:24px;color:#8890b5;font-size:12px}
/* 목표 카드 */
.goal-card{background:#1a1d27;border:1px solid #2e3352;border-radius:12px;padding:12px}
</style>
</head>
<body>

<div class="nav">
  <div class="logo">🏠 우리집 자산관리</div>
  <div class="tabs" id="tabs"></div>
</div>
<div class="page" id="page"></div>
<div id="modal-root"></div>

<script>
// ===================== 데이터 =====================
var TABS = [["ov","📊"],["as","🏠"],["lk","📒"],["fx","🔁"],["ln","💳"],["gl","🎯"]];
var TAB_NAMES = {ov:"대시보드",as:"자산현황",lk:"가계부",fx:"고정비용",ln:"대출",gl:"목표"};
var curTab = "ov";

var OWS = ["오동주","오승헌","서지은","공동"];
var OWC = {오동주:"#4ecdc4",오승헌:"#6c7bff",서지은:"#ff6b8a",공동:"#ffd166"};
var OWBG = {오동주:"rgba(78,205,196,.15)",오승헌:"rgba(108,123,255,.15)",서지은:"rgba(255,107,138,.15)",공동:"rgba(255,209,102,.15)"};
var ACATS = ["부동산","예금·저축","주식·ETF","퇴직연금","금·실물자산","기타"];
var AICO = {부동산:"🏠","예금·저축":"🏦","주식·ETF":"📈",퇴직연금:"🧓","금·실물자산":"🥇",기타:"📦"};
var ACC = {부동산:"#6c7bff","예금·저축":"#4ecdc4","주식·ETF":"#ffd166",퇴직연금:"#ff9f43","금·실물자산":"#f7c948",기타:"#8890b5"};
var GCOLS = ["#6c7bff","#4ecdc4","#ffd166","#ff6b8a","#ff9f43"];

var IC = [
  {k:"급여",i:"💼",c:"#4caf88"},
  {k:"부업·프리랜서",i:"💻",c:"#4ecdc4"},
  {k:"투자수익",i:"📈",c:"#ffd166"},
  {k:"임대수입",i:"🏠",c:"#6c7bff"},
  {k:"기타수입",i:"🎁",c:"#ff9f43"}
];
var EC = [
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

var IMAP = {};
IC.concat(EC).forEach(function(c){ IMAP[c.k] = c.i; });

var BDGM = {
  "부동산":"rgba(108,123,255,.15)|#6c7bff",
  "예금·저축":"rgba(78,205,196,.15)|#4ecdc4",
  "주식·ETF":"rgba(255,209,102,.15)|#ffd166",
  "퇴직연금":"rgba(255,159,67,.15)|#ff9f43",
  "금·실물자산":"rgba(247,201,72,.15)|#f7c948",
  "주택담보대출":"rgba(108,123,255,.15)|#6c7bff",
  "전세대출":"rgba(78,205,196,.15)|#4ecdc4",
  "신용대출":"rgba(255,107,138,.15)|#ff6b8a",
  "자동차할부":"rgba(255,209,102,.15)|#ffd166",
  "카드론":"rgba(255,107,138,.15)|#ff6b8a"
};

var D = {
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
    {id:7,tp:"expense",nm:"카페",ct:"카페·음료",am:15000,dt:"2026-04-14",mm:""}
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

// ===================== 유틸 =====================
function fmt(n) {
  if (!n) return "0원";
  if (n >= 100000000) return (n/100000000).toFixed(1) + "억원";
  return n.toLocaleString() + "원";
}
function toDay() { return new Date().toISOString().slice(0,10); }
function toMon() { return new Date().toISOString().slice(0,7); }
var fbdb = null;
var fbReady = false;

function save() {
  try { localStorage.setItem("wuri", JSON.stringify(D)); } catch(e) {}
  if (fbReady && fbdb) {
    try { fbdb.ref("wuri").set(D); } catch(e) {}
  }
}
function load() {
  try { var s = localStorage.getItem("wuri"); if(s) D = JSON.parse(s); } catch(e) {}
}
function bdgEl(label) {
  var s = document.createElement("span");
  s.className = "bdg";
  var parts = (BDGM[label] || "rgba(136,144,181,.15)|#8890b5").split("|");
  s.style.background = parts[0];
  s.style.color = parts[1];
  s.textContent = label;
  return s;
}
function pbEl(pct, color) {
  var d = document.createElement("div"); d.className = "pb";
  var f = document.createElement("div"); f.className = "pbf";
  f.style.width = Math.min(Math.max(+pct||0, 0), 100) + "%";
  f.style.background = color || "#6c7bff";
  d.appendChild(f); return d;
}

// ===================== 모달 =====================
function openModal(html) {
  var root = document.getElementById("modal-root");
  root.innerHTML = "";
  var bg = document.createElement("div");
  bg.className = "modal-bg";
  bg.innerHTML = '<div class="modal">' + html + '</div>';
  bg.addEventListener("click", function(e) {
    if (e.target === bg) closeModal();
  });
  root.appendChild(bg);
}
function closeModal() {
  document.getElementById("modal-root").innerHTML = "";
}

// ===================== 탭 렌더 =====================
function renderTabs() {
  var wrap = document.getElementById("tabs");
  wrap.innerHTML = "";
  TABS.forEach(function(t) {
    var b = document.createElement("button");
    b.className = "tab" + (curTab === t[0] ? " on" : "");
    b.textContent = t[1];
    b.setAttribute("data-tab", t[0]);
    b.addEventListener("click", function() {
      curTab = t[0];
      renderTabs();
      renderPage();
    });
    wrap.appendChild(b);
  });
}

// ===================== 페이지 렌더 =====================
function renderPage() {
  var page = document.getElementById("page");
  page.innerHTML = '<div style="font-size:11px;color:#8890b5;font-weight:600;text-transform:uppercase;letter-spacing:.8px;margin-bottom:11px">' + (TAB_NAMES[curTab]||"") + '</div>';
  var content = document.createElement("div");
  if (curTab === "ov") renderOV(content);
  else if (curTab === "as") renderAS(content);
  else if (curTab === "lk") renderLK(content);
  else if (curTab === "fx") renderFX(content);
  else if (curTab === "ln") renderLN(content);
  else if (curTab === "gl") renderGL(content);
  page.appendChild(content);
}

// ===================== 대시보드 =====================
function renderOV(wrap) {
  var ta = D.assets.reduce(function(s,a){return s+a.cv;}, 0);
  var tl = D.loans.reduce(function(s,l){return s+l.bl;}, 0);
  var tm = toMon();
  var mx = D.txs.filter(function(t){return t.dt.slice(0,7)===tm;});
  var inc = mx.filter(function(t){return t.tp==="income";}).reduce(function(s,t){return s+t.am;},0);
  var exp = mx.filter(function(t){return t.tp==="expense";}).reduce(function(s,t){return s+t.am;},0);

  wrap.innerHTML += '<div class="g2">' +
    card("순자산", fmt(ta-tl), "#6c7bff") +
    card("이달수입", "+" + fmt(inc), "#4ecdc4") +
    card("이달지출", "-" + fmt(exp), "#ff6b8a") +
    card("총부채", fmt(tl), "#ffd166") +
  '</div>';

  var recent = D.txs.slice().sort(function(a,b){return b.dt.localeCompare(a.dt);}).slice(0,6);
  var box = document.createElement("div"); box.className = "box";
  box.innerHTML = '<div class="bh"><div class="bh-title">최근 거래</div></div>';
  if (!recent.length) {
    box.innerHTML += '<div class="empty">거래 없음</div>';
  } else {
    recent.forEach(function(t) {
      var d = document.createElement("div"); d.className = "item";
      d.innerHTML = '<div class="ico" style="background:' + (t.tp==="income"?"rgba(76,175,136,.15)":"rgba(255,107,138,.15)") + '">' + (IMAP[t.ct]||"📦") + '</div>' +
        '<div style="flex:1"><div style="font-size:12px;font-weight:600">' + t.nm + '</div><div style="font-size:10px;color:#8890b5">' + t.dt + ' · ' + t.ct + '</div></div>' +
        '<div style="font-size:12px;font-weight:700;color:' + (t.tp==="income"?"#4caf88":"#ff6b8a") + '">' + (t.tp==="income"?"+":"-") + fmt(t.am) + '</div>';
      box.appendChild(d);
    });
  }
  wrap.appendChild(box);
}
function card(lbl, val, color) {
  return '<div class="card"><div class="card-lbl">' + lbl + '</div><div class="card-val" style="color:' + color + '">' + val + '</div></div>';
}

// ===================== 자산현황 =====================
function renderAS(wrap) {
  var tCv = D.assets.reduce(function(s,a){return s+a.cv;},0);
  var tOv = D.assets.reduce(function(s,a){return s+a.ov;},0);
  var tG = tCv - tOv;

  var box = document.createElement("div"); box.className = "box";
  var bh = document.createElement("div"); bh.className = "bh";
  bh.innerHTML = '<div class="bh-title">자산 목록</div>';
  var addBtn = document.createElement("button"); addBtn.className = "btn-p"; addBtn.textContent = "+ 추가";
  addBtn.addEventListener("click", function(){ openAssetModal(null); });
  bh.appendChild(addBtn); box.appendChild(bh);

  var scroll = document.createElement("div"); scroll.className = "tscroll";
  var table = document.createElement("table");
  table.innerHTML = '<thead><tr><th>소유주</th><th>자산명</th><th>분류</th><th>평가금액</th><th>매입금액</th><th>손익</th><th>수익률</th><th></th></tr></thead>';
  var tbody = document.createElement("tbody");
  D.assets.forEach(function(a) {
    var g = a.cv - a.ov, pos = g >= 0;
    var pct = a.ov ? (g/a.ov*100).toFixed(1) : "0.0";
    var tr = document.createElement("tr");
    tr.innerHTML =
      '<td><span class="bdg" style="background:' + (OWBG[a.ow]||"rgba(136,144,181,.15)") + ';color:' + (OWC[a.ow]||"#8890b5") + '">' + (a.ow||"-") + '</span></td>' +
      '<td><strong style="font-size:12px">' + (AICO[a.ct]||"📦") + ' ' + a.nm + '</strong>' + (a.mm?'<div style="font-size:10px;color:#8890b5">' + a.mm + '</div>':"") + '</td>' +
      '<td></td>' +
      '<td style="font-size:12px;font-weight:600">' + fmt(a.cv) + '</td>' +
      '<td style="font-size:12px;color:#8890b5">' + fmt(a.ov) + '</td>' +
      '<td style="font-size:12px;font-weight:600;color:' + (pos?"#4caf88":"#ff6b8a") + '">' + (pos?"+":"") + fmt(g) + '</td>' +
      '<td style="font-size:11px;color:' + (pos?"#4caf88":"#ff6b8a") + '">' + (pos?"+":"") + pct + '%</td>' +
      '<td style="white-space:nowrap"></td>';
    // 뱃지
    tr.cells[2].appendChild(bdgEl(a.ct));
    // 수정 버튼
    var eb = document.createElement("button"); eb.className = "btn-e"; eb.textContent = "✏️";
    (function(asset){ eb.addEventListener("click", function(){ openAssetModal(asset); }); })(a);
    // 삭제 버튼
    var xb = document.createElement("button"); xb.className = "btn-x"; xb.textContent = "✕"; xb.style.marginLeft = "4px";
    (function(id){ xb.addEventListener("click", function(){
      D.assets = D.assets.filter(function(x){return x.id!==id;});
      save(); renderPage();
    }); })(a.id);
    tr.cells[7].appendChild(eb); tr.cells[7].appendChild(xb);
    tbody.appendChild(tr);
  });
  // 합계 행
  var tfoot = document.createElement("tfoot");
  var ftr = document.createElement("tr");
  var tG2 = tCv - tOv, pos2 = tG2 >= 0;
  ftr.innerHTML = '<td colspan="3" style="font-size:11px;color:#8890b5">합계</td>' +
    '<td style="font-size:13px;color:#6c7bff">' + fmt(tCv) + '</td>' +
    '<td style="color:#8890b5">' + fmt(tOv) + '</td>' +
    '<td style="color:' + (pos2?"#4caf88":"#ff6b8a") + '">' + (pos2?"+":"") + fmt(tG2) + '</td>' +
    '<td style="font-size:11px;color:' + (pos2?"#4caf88":"#ff6b8a") + '">' + (pos2?"+":"") + (tOv?(tG2/tOv*100).toFixed(1):"0") + '%</td><td></td>';
  tfoot.appendChild(ftr);
  table.appendChild(tbody); table.appendChild(tfoot);
  scroll.appendChild(table); box.appendChild(scroll);
  wrap.appendChild(box);
}

// ===================== 가계부 =====================
var lkFlt = "";
function renderLK(wrap) {
  var tm = toMon();
  var mx = D.txs.filter(function(t){return t.dt.slice(0,7)===tm;});
  var inc = mx.filter(function(t){return t.tp==="income";}).reduce(function(s,t){return s+t.am;},0);
  var exp = mx.filter(function(t){return t.tp==="expense";}).reduce(function(s,t){return s+t.am;},0);

  // 요약
  var sumBox = document.createElement("div"); sumBox.className = "box";
  sumBox.innerHTML = '<div class="bh"><div class="bh-title">이번 달 요약</div></div>' +
    '<div style="padding:11px 13px">' +
    sumRow("수입","#4caf88","+"+fmt(inc)) +
    sumRow("지출","#ff6b8a","-"+fmt(exp)) +
    sumRow("잔여",(inc-exp>=0?"#6c7bff":"#ff6b8a"),(inc-exp>=0?"+":"")+fmt(inc-exp)) +
    '</div>';
  wrap.appendChild(sumBox);

  // 거래 목록
  var listBox = document.createElement("div"); listBox.className = "box";
  var bh = document.createElement("div"); bh.className = "bh";
  bh.innerHTML = '<div class="bh-title">거래 내역</div>';
  var bhr = document.createElement("div"); bhr.className = "bh-right";

  var fltSel = document.createElement("select");
  fltSel.style.cssText = "padding:4px 8px;background:#22263a;border:1px solid #2e3352;border-radius:7px;color:#e8eaf6;font-size:11px;font-family:inherit";
  [["","전체"],["income","수입"],["expense","지출"]].forEach(function(o){
    var op = document.createElement("option"); op.value = o[0]; op.textContent = o[1];
    if (o[0] === lkFlt) op.selected = true;
    fltSel.appendChild(op);
  });
  fltSel.addEventListener("change", function(){ lkFlt = this.value; renderPage(); });

  var addBtn = document.createElement("button"); addBtn.className = "btn-p"; addBtn.textContent = "+ 추가";
  addBtn.addEventListener("click", function(){ openTxModal(); });

  bhr.appendChild(fltSel); bhr.appendChild(addBtn); bh.appendChild(bhr); listBox.appendChild(bh);

  var list = D.txs.slice().sort(function(a,b){return b.dt.localeCompare(a.dt);}).filter(function(t){return !lkFlt||t.tp===lkFlt;});
  if (!list.length) {
    listBox.innerHTML += '<div class="empty">거래 없음</div>';
  } else {
    list.forEach(function(t) {
      var ci = (t.tp==="income"?IC:EC).filter(function(c){return c.k===t.ct;})[0];
      var d = document.createElement("div"); d.className = "item";
      d.innerHTML = '<div class="ico" style="background:' + (t.tp==="income"?"rgba(76,175,136,.15)":"rgba(255,107,138,.15)") + '">' + (ci?ci.i:"📦") + '</div>' +
        '<div style="flex:1"><div style="font-size:12px;font-weight:600">' + t.nm + (t.mm?' <span style="font-size:10px;color:#8890b5">('+t.mm+')</span>':"") + '</div><div style="font-size:10px;color:#8890b5">' + t.dt + ' · ' + t.ct + '</div></div>' +
        '<div style="display:flex;align-items:center;gap:7px"><span style="font-size:12px;font-weight:700;color:' + (t.tp==="income"?"#4caf88":"#ff6b8a") + '">' + (t.tp==="income"?"+":"-") + fmt(t.am) + '</span></div>';
      var xb = document.createElement("button"); xb.className = "btn-x"; xb.textContent = "✕";
      (function(id){ xb.addEventListener("click", function(){
        D.txs = D.txs.filter(function(x){return x.id!==id;});
        save(); renderPage();
      }); })(t.id);
      d.lastElementChild.appendChild(xb);
      listBox.appendChild(d);
    });
  }
  wrap.appendChild(listBox);
}
function sumRow(lbl, color, val) {
  return '<div style="display:flex;justify-content:space-between;align-items:center;padding:7px 0;border-bottom:1px solid #2e3352"><span style="font-size:12px;color:#8890b5">' + lbl + '</span><span style="font-size:13px;font-weight:700;color:' + color + '">' + val + '</span></div>';
}

// ===================== 고정비용 =====================
function renderFX(wrap) {
  var now = new Date(), ym = toMon();
  var total = (D.fixed||[]).reduce(function(s,f){return s+f.am;},0);

  var topDiv = document.createElement("div");
  topDiv.style.cssText = "display:flex;justify-content:space-between;align-items:center;margin-bottom:10px";
  topDiv.innerHTML = '<div style="font-size:11px;color:#8890b5">매달 자동으로 가계부에 추가돼요</div>';
  var addBtn = document.createElement("button"); addBtn.className = "btn-p"; addBtn.textContent = "+ 추가";
  addBtn.addEventListener("click", function(){ openFixedModal(null); });
  topDiv.appendChild(addBtn); wrap.appendChild(topDiv);

  var box = document.createElement("div"); box.className = "box";
  box.innerHTML = '<div class="bh"><div class="bh-title">고정비용 목록</div></div>';

  if (!D.fixed || !D.fixed.length) {
    box.innerHTML += '<div class="empty">고정비용을 추가해주세요</div>';
  } else {
    D.fixed.forEach(function(fx) {
      var applied = D.txs.some(function(t){return t.fixedId===fx.id && t.dt.slice(0,7)===ym;});
      var dueDate = new Date(now.getFullYear(), now.getMonth(), fx.day);
      var ci = EC.filter(function(c){return c.k===fx.ct;})[0];

      var d = document.createElement("div"); d.className = "item";
      var ico = document.createElement("div"); ico.className = "ico"; ico.style.background = "rgba(255,107,138,.15)"; ico.textContent = ci?ci.i:"📦";
      var info = document.createElement("div"); info.style.flex = "1";
      info.innerHTML = '<div style="font-size:12px;font-weight:600">' + fx.nm + '</div><div style="font-size:10px;color:#8890b5">' + fx.ct + ' · 매월 ' + fx.day + '일 · ' + fmt(fx.am) + '</div>';

      var right = document.createElement("div"); right.style.cssText = "display:flex;gap:5px;align-items:center";

      // 상태 배지
      var status = document.createElement("span");
      if (applied) {
        status.style.cssText = "font-size:10px;color:#4caf88;background:rgba(76,175,136,.12);padding:2px 7px;border-radius:16px";
        status.textContent = "✅ 완료";
      } else if (now < dueDate) {
        status.style.cssText = "font-size:10px;color:#ffd166;background:rgba(255,209,102,.12);padding:2px 7px;border-radius:16px";
        status.textContent = "⏳ " + fx.day + "일 예정";
      } else {
        status = document.createElement("button");
        status.style.cssText = "font-size:10px;color:#6c7bff;background:rgba(108,123,255,.15);padding:3px 8px;border-radius:16px;border:none;cursor:pointer";
        status.textContent = "지금 적용";
        (function(f){ status.addEventListener("click", function(){
          var dt = ym + "-" + String(f.day).padStart(2,"0");
          D.txs.push({id:D.nid++, tp:"expense", nm:f.nm, ct:f.ct, am:f.am, dt:dt, mm:"고정", fixed:true, fixedId:f.id});
          save(); renderPage();
        }); })(fx);
      }

      var eb = document.createElement("button"); eb.className = "btn-e"; eb.textContent = "✏️";
      (function(f){ eb.addEventListener("click", function(){ openFixedModal(f); }); })(fx);
      var xb = document.createElement("button"); xb.className = "btn-x"; xb.textContent = "✕";
      (function(id){ xb.addEventListener("click", function(){
        D.fixed = D.fixed.filter(function(x){return x.id!==id;});
        save(); renderPage();
      }); })(fx.id);

      right.appendChild(status); right.appendChild(eb); right.appendChild(xb);
      d.appendChild(ico); d.appendChild(info); d.appendChild(right);
      box.appendChild(d);
    });

    var foot = document.createElement("div");
    foot.style.cssText = "padding:8px 13px;background:rgba(108,123,255,.06);border-top:1px solid #2e3352;display:flex;justify-content:space-between;font-size:12px";
    foot.innerHTML = '<span style="color:#8890b5">월 고정 지출 합계</span><span style="font-weight:700;color:#ff6b8a">' + fmt(total) + '</span>';
    box.appendChild(foot);
  }
  wrap.appendChild(box);
}

// ===================== 대출 =====================
function renderLN(wrap) {
  var tbl = D.loans.reduce(function(s,l){return s+l.bl;},0);
  var tog = D.loans.reduce(function(s,l){return s+l.og;},0);
  var tmy = D.loans.reduce(function(s,l){return s+l.my;},0);

  var box = document.createElement("div"); box.className = "box";
  var bh = document.createElement("div"); bh.className = "bh";
  bh.innerHTML = '<div class="bh-title">대출·부채</div>';
  var addBtn = document.createElement("button"); addBtn.className = "btn-p"; addBtn.textContent = "+ 추가";
  addBtn.addEventListener("click", function(){ openLoanModal(null); });
  bh.appendChild(addBtn); box.appendChild(bh);

  if (!D.loans.length) {
    box.innerHTML += '<div class="empty">대출 정보를 추가해주세요</div>';
  } else {
    D.loans.forEach(function(l) {
      var p = l.og ? ((l.og-l.bl)/l.og*100) : 0;
      var d = document.createElement("div"); d.style.cssText = "padding:11px 13px;border-bottom:1px solid rgba(46,51,82,.3)";

      var top = document.createElement("div"); top.style.cssText = "display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:6px";
      var left = document.createElement("div");
      left.innerHTML = '<div style="font-size:13px;font-weight:600;margin-bottom:4px">' + l.nm + '</div>';
      left.appendChild(bdgEl(l.ct));
      var right = document.createElement("div"); right.style.cssText = "display:flex;gap:5px;align-items:center";
      var am = document.createElement("span"); am.style.cssText = "font-size:13px;font-weight:700;color:#ff6b8a"; am.textContent = fmt(l.bl);
      var eb = document.createElement("button"); eb.className = "btn-e"; eb.textContent = "✏️";
      (function(loan){ eb.addEventListener("click", function(){ openLoanModal(loan); }); })(l);
      var xb = document.createElement("button"); xb.className = "btn-x"; xb.textContent = "✕";
      (function(id){ xb.addEventListener("click", function(){
        D.loans = D.loans.filter(function(x){return x.id!==id;});
        save(); renderPage();
      }); })(l.id);
      right.appendChild(am); right.appendChild(eb); right.appendChild(xb);
      top.appendChild(left); top.appendChild(right); d.appendChild(top);

      var info = document.createElement("div"); info.style.cssText = "display:flex;gap:12px;font-size:11px;color:#8890b5;margin-bottom:5px";
      ["금리 "+l.rt+"%", "월상환 "+fmt(l.my), "만기 "+(l.du||"-")].forEach(function(t){
        var s = document.createElement("span"); s.textContent = t; info.appendChild(s);
      });
      d.appendChild(info); d.appendChild(pbEl(p, "#6c7bff")); box.appendChild(d);
    });
  }
  wrap.appendChild(box);

  // 요약
  var sumBox = document.createElement("div"); sumBox.className = "box";
  sumBox.innerHTML = '<div class="bh"><div class="bh-title">부채 현황</div></div><div style="padding:11px 13px">' +
    sumRow("총 잔액","#ff6b8a",fmt(tbl)) + sumRow("월 상환","#e8eaf6",fmt(tmy)+"/월") + sumRow("상환 완료","#4caf88",fmt(tog-tbl)) +
    '</div>';
  wrap.appendChild(sumBox);
}

// ===================== 목표 =====================
function renderGL(wrap) {
  var topDiv = document.createElement("div"); topDiv.style.cssText = "display:flex;justify-content:flex-end;margin-bottom:10px";
  var addBtn = document.createElement("button"); addBtn.className = "btn-p"; addBtn.textContent = "+ 목표 추가";
  addBtn.addEventListener("click", function(){ openGoalModal(null); });
  topDiv.appendChild(addBtn); wrap.appendChild(topDiv);

  var grid = document.createElement("div"); grid.className = "g2";
  D.goals.forEach(function(g, i) {
    var col = GCOLS[i % GCOLS.length];
    var pct = g.tg ? Math.min(g.cv/g.tg*100, 100).toFixed(0) : 0;
    var card = document.createElement("div"); card.className = "goal-card";
    card.innerHTML = '<div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:7px"><div><div style="font-size:13px;font-weight:600">' + g.nm + '</div><div style="font-size:10px;color:#8890b5;margin-top:1px">' + (g.dt||"기한 미설정") + '</div></div><div style="display:flex;flex-direction:column;align-items:flex-end;gap:4px"><div style="font-size:16px">' + (g.em||"🎯") + '</div><div style="display:flex;gap:3px"></div></div></div><div style="font-size:18px;font-weight:700;color:' + col + '">' + pct + '%</div>';
    card.appendChild(pbEl(pct, col));
    var sub = document.createElement("div"); sub.style.cssText = "display:flex;justify-content:space-between;font-size:10px;color:#8890b5;margin-top:5px";
    sub.innerHTML = '<span>' + fmt(g.cv) + '</span><span>목표 ' + fmt(g.tg) + '</span>';
    card.appendChild(sub);

    var btnWrap = card.querySelector("div > div:last-child > div:last-child");
    var eb = document.createElement("button"); eb.className = "btn-e"; eb.textContent = "✏️";
    (function(goal){ eb.addEventListener("click", function(){ openGoalModal(goal); }); })(g);
    var xb = document.createElement("button"); xb.className = "btn-x"; xb.textContent = "✕";
    (function(id){ xb.addEventListener("click", function(){
      D.goals = D.goals.filter(function(x){return x.id!==id;});
      save(); renderPage();
    }); })(g.id);
    btnWrap.appendChild(eb); btnWrap.appendChild(xb);
    grid.appendChild(card);
  });
  wrap.appendChild(grid);
}

// ===================== 모달들 =====================
function makeCatBtns(cats, cur, onChange) {
  var wrap = document.createElement("div"); wrap.className = "cat-wrap";
  cats.forEach(function(c) {
    var b = document.createElement("button"); b.className = "cat-btn" + (c.k===cur?" on":"");
    b.textContent = c.i + " " + c.k;
    if (c.k===cur) b.style.background = c.c;
    b.addEventListener("click", function(e) { e.preventDefault(); onChange(c.k); });
    wrap.appendChild(b);
  });
  return wrap;
}
function makeEcatBtns(cur, onChange) {
  var wrap = document.createElement("div");
  var grps = [];
  EC.forEach(function(c){ if (grps.indexOf(c.g)<0) grps.push(c.g); });
  grps.forEach(function(g) {
    var gl = document.createElement("div"); gl.className = "grp-lbl"; gl.textContent = g; wrap.appendChild(gl);
    var row = document.createElement("div"); row.className = "cat-wrap";
    EC.filter(function(c){return c.g===g;}).forEach(function(c){
      var b = document.createElement("button"); b.className = "cat-btn" + (c.k===cur?" on":"");
      b.textContent = c.i + " " + c.k;
      if (c.k===cur) b.style.background = c.c;
      b.addEventListener("click", function(e) { e.preventDefault(); onChange(c.k); });
      row.appendChild(b);
    });
    wrap.appendChild(row);
  });
  return wrap;
}

function openAssetModal(init) {
  var ct = init ? init.ct : "주식·ETF";
  var ow = init ? (init.ow||"오동주") : "오동주";

  var modal = document.createElement("div"); modal.className = "modal";
  modal.innerHTML = '<div class="modal-title">' + (init?"✏️ 자산 수정":"자산 추가") + '</div>';

  // 자산명
  var nmF = document.createElement("div"); nmF.className = "field";
  nmF.innerHTML = '<label>자산명</label>';
  var nmI = document.createElement("input"); nmI.type = "text"; nmI.placeholder = "씨에스윈드, 우리은행"; nmI.value = init?init.nm:"";
  nmF.appendChild(nmI); modal.appendChild(nmF);

  // 소유주
  var owF = document.createElement("div"); owF.className = "field";
  owF.innerHTML = '<label>소유주</label>';
  var owWrap = document.createElement("div"); owWrap.className = "cat-wrap";
  function renderOw() {
    owWrap.innerHTML = "";
    OWS.forEach(function(o) {
      var b = document.createElement("button"); b.className = "cat-btn" + (o===ow?" on":"");
      b.textContent = o;
      if (o===ow) b.style.background = OWC[o];
      b.addEventListener("click", function(e){ e.preventDefault(); ow=o; renderOw(); });
      owWrap.appendChild(b);
    });
  }
  renderOw(); owF.appendChild(owWrap); modal.appendChild(owF);

  // 분류
  var ctF = document.createElement("div"); ctF.className = "field";
  ctF.innerHTML = '<label>분류</label>';
  var ctWrap = document.createElement("div"); ctWrap.className = "cat-wrap";
  var formWrap = document.createElement("div");
  function renderCt() {
    ctWrap.innerHTML = "";
    ACATS.forEach(function(c) {
      var b = document.createElement("button"); b.className = "cat-btn" + (c===ct?" on":"");
      b.textContent = (AICO[c]||"📦") + " " + c;
      if (c===ct) b.style.background = "#6c7bff";
      b.addEventListener("click", function(e){ e.preventDefault(); ct=c; renderCt(); renderForm(); });
      ctWrap.appendChild(b);
    });
  }
  function renderForm() {
    formWrap.innerHTML = "";
    var cv = init?init.cv:"", ov = init?init.ov:"", mm = init?(init.mm||""):"";
    var f = document.createElement;
    function inp(ph, val) { var i = document.createElement("input"); i.type="number"; i.placeholder=ph; i.value=val||""; return i; }
    function tinp(ph, val) { var i = document.createElement("input"); i.type="text"; i.placeholder=ph; i.value=val||""; return i; }
    function field(lbl, el) { var d=document.createElement("div"); d.className="field"; d.innerHTML="<label>"+lbl+"</label>"; d.appendChild(el); return d; }
    if (ct==="부동산") { formWrap.appendChild(field("현재 시세 (원)",inp("420000000",cv))); formWrap.appendChild(field("취득가 (원)",inp("380000000",ov))); formWrap.appendChild(field("주소/메모",tinp("성북구",mm))); }
    else if (ct==="예금·저축") { formWrap.appendChild(field("잔액 (원)",inp("8500000",cv))); formWrap.appendChild(field("금융기관/메모",tinp("카카오뱅크",mm))); }
    else if (ct==="주식·ETF") { formWrap.appendChild(field("평가금액 (원)",inp("1500000",cv))); formWrap.appendChild(field("매입금액 (원)",inp("1000000",ov))); formWrap.appendChild(field("메모",tinp("해외, 국내",mm))); }
    else if (ct==="금·실물자산") { formWrap.appendChild(field("현재가치 (원)",inp("5000000",cv))); formWrap.appendChild(field("취득가 (원)",inp("4000000",ov))); formWrap.appendChild(field("종류/수량",tinp("금 100g",mm))); }
    else { formWrap.appendChild(field("현재가치 (원)",inp("0",cv))); formWrap.appendChild(field("취득가 (원)",inp("0",ov))); formWrap.appendChild(field("메모",tinp("",mm))); }
  }
  renderCt(); renderForm();
  ctF.appendChild(ctWrap); modal.appendChild(ctF); modal.appendChild(formWrap);

  // 버튼
  var foot = document.createElement("div"); foot.className = "modal-footer";
  var cancelBtn = document.createElement("button"); cancelBtn.className = "btn-n"; cancelBtn.textContent = "취소";
  cancelBtn.addEventListener("click", closeModal);
  foot.appendChild(cancelBtn);

  if (init) {
    var delBtn = document.createElement("button"); delBtn.className = "btn-d"; delBtn.textContent = "🗑 삭제";
    delBtn.addEventListener("click", function(){
      D.assets = D.assets.filter(function(a){return a.id!==init.id;});
      save(); closeModal(); renderPage();
    });
    foot.appendChild(delBtn);
  }

  var saveBtn = document.createElement("button"); saveBtn.className = "btn-p"; saveBtn.textContent = "저장";
  saveBtn.addEventListener("click", function() {
    var nm = nmI.value.trim(); if (!nm) return;
    var inps = formWrap.querySelectorAll("input");
    var cv = parseFloat(inps[0]?inps[0].value:0)||0;
    var ov = parseFloat(inps[1]?inps[1].value:0)||cv;
    var mm = inps[2]?inps[2].value:"";
    if (!cv) return;
    if (init) {
      D.assets = D.assets.map(function(a){ return a.id===init.id ? {id:a.id,nm:nm,ct:ct,ow:ow,cv:cv,ov:ov,mm:mm} : a; });
    } else {
      D.assets.push({id:D.nid++,nm:nm,ct:ct,ow:ow,cv:cv,ov:ov,mm:mm});
    }
    save(); closeModal(); renderPage();
  });
  foot.appendChild(saveBtn); modal.appendChild(foot);

  var root = document.getElementById("modal-root"); root.innerHTML = "";
  var bg = document.createElement("div"); bg.className = "modal-bg";
  bg.addEventListener("click", function(e){ if(e.target===bg) closeModal(); });
  bg.appendChild(modal); root.appendChild(bg);
}

function openTxModal() {
  var tp = "expense", ct = "식비·장보기";
  var modal = document.createElement("div"); modal.className = "modal";
  modal.innerHTML = '<div class="modal-title">거래 추가</div>';

  // 유형
  var tpF = document.createElement("div"); tpF.className = "field"; tpF.innerHTML = "<label>유형</label>";
  var tpWrap = document.createElement("div"); tpWrap.className = "cat-wrap";
  function renderTp() {
    tpWrap.innerHTML = "";
    [["expense","지출","#ff6b8a"],["income","수입","#4caf88"]].forEach(function(arr) {
      var b = document.createElement("button"); b.className = "cat-btn" + (tp===arr[0]?" on":"");
      b.textContent = arr[1]; if(tp===arr[0]) b.style.background=arr[2];
      b.addEventListener("click", function(e){ e.preventDefault(); tp=arr[0]; ct=(tp==="income"?"급여":"식비·장보기"); renderTp(); renderCat(); });
      tpWrap.appendChild(b);
    });
  }
  var catF = document.createElement("div"); catF.className = "field"; catF.innerHTML = "<label>카테고리</label>";
  var catWrap = document.createElement("div");
  function renderCat() {
    catWrap.innerHTML = "";
    if (tp==="income") {
      catWrap.appendChild(makeCatBtns(IC, ct, function(k){ ct=k; renderCat(); }));
    } else {
      catWrap.appendChild(makeEcatBtns(ct, function(k){ ct=k; renderCat(); }));
    }
  }
  renderTp(); renderCat();
  tpF.appendChild(tpWrap); catF.appendChild(catWrap); modal.appendChild(tpF); modal.appendChild(catF);

  function field(lbl, el) { var d=document.createElement("div"); d.className="field"; d.innerHTML="<label>"+lbl+"</label>"; d.appendChild(el); return d; }
  var nmI = document.createElement("input"); nmI.type="text"; nmI.placeholder="마트 장보기";
  var amI = document.createElement("input"); amI.type="number"; amI.placeholder="0";
  var dtI = document.createElement("input"); dtI.type="date"; dtI.value=toDay();
  var mmI = document.createElement("input"); mmI.type="text"; mmI.placeholder="메모(선택)";
  modal.appendChild(field("내용",nmI)); modal.appendChild(field("금액 (원)",amI));
  modal.appendChild(field("날짜",dtI)); modal.appendChild(field("메모",mmI));

  var foot = document.createElement("div"); foot.className = "modal-footer";
  var cancelBtn = document.createElement("button"); cancelBtn.className = "btn-n"; cancelBtn.textContent = "취소";
  cancelBtn.addEventListener("click", closeModal);
  var saveBtn = document.createElement("button"); saveBtn.className = "btn-p"; saveBtn.textContent = "저장";
  saveBtn.addEventListener("click", function(){
    var nm=nmI.value.trim(), am=parseFloat(amI.value)||0;
    if(!nm||!am) return;
    D.txs.push({id:D.nid++,tp:tp,nm:nm,ct:ct,am:am,dt:dtI.value||toDay(),mm:mmI.value});
    save(); closeModal(); renderPage();
  });
  foot.appendChild(cancelBtn); foot.appendChild(saveBtn); modal.appendChild(foot);

  var root = document.getElementById("modal-root"); root.innerHTML = "";
  var bg = document.createElement("div"); bg.className = "modal-bg";
  bg.addEventListener("click", function(e){ if(e.target===bg) closeModal(); });
  bg.appendChild(modal); root.appendChild(bg);
}

function openLoanModal(init) {
  var modal = document.createElement("div"); modal.className = "modal";
  modal.innerHTML = '<div class="modal-title">' + (init?"✏️ 대출 수정":"대출 추가") + '</div>';
  function field(lbl, el) { var d=document.createElement("div"); d.className="field"; d.innerHTML="<label>"+lbl+"</label>"; d.appendChild(el); return d; }
  function inp(ph,val){ var i=document.createElement("input"); i.type="number"; i.placeholder=ph; i.value=val||""; return i; }
  var nmI=document.createElement("input"); nmI.type="text"; nmI.placeholder="신생아특례 주담대"; nmI.value=init?init.nm:"";
  var ctI=document.createElement("select"); ["주택담보대출","전세대출","신용대출","자동차할부","카드론","기타"].forEach(function(o){ var op=document.createElement("option"); op.value=o; op.textContent=o; if(init&&o===init.ct)op.selected=true; ctI.appendChild(op); });
  var ogI=inp("0",init?init.og:""), blI=inp("0",init?init.bl:""), rtI=inp("1.68",init?init.rt:""), myI=inp("0",init?init.my:"");
  var duI=document.createElement("input"); duI.type="date"; duI.value=init?init.du:"";
  modal.appendChild(field("대출명",nmI)); modal.appendChild(field("분류",ctI));
  modal.appendChild(field("원금 (원)",ogI)); modal.appendChild(field("잔액 (원)",blI));
  modal.appendChild(field("금리 (%)",rtI)); modal.appendChild(field("월 상환액 (원)",myI));
  modal.appendChild(field("만기일",duI));
  var foot=document.createElement("div"); foot.className="modal-footer";
  var cn=document.createElement("button"); cn.className="btn-n"; cn.textContent="취소"; cn.addEventListener("click",closeModal);
  foot.appendChild(cn);
  if(init){var db=document.createElement("button"); db.className="btn-d"; db.textContent="🗑 삭제"; db.addEventListener("click",function(){ D.loans=D.loans.filter(function(l){return l.id!==init.id;}); save();closeModal();renderPage(); }); foot.appendChild(db);}
  var sv=document.createElement("button"); sv.className="btn-p"; sv.textContent="저장";
  sv.addEventListener("click",function(){
    var nm=nmI.value.trim(); if(!nm)return;
    var og=parseFloat(ogI.value)||0;
    var row={nm:nm,ct:ctI.value,og:og,bl:parseFloat(blI.value)||og,rt:parseFloat(rtI.value)||0,my:parseFloat(myI.value)||0,du:duI.value};
    if(init){row.id=init.id;D.loans=D.loans.map(function(l){return l.id===init.id?row:l;});}
    else{row.id=D.nid++;D.loans.push(row);}
    save();closeModal();renderPage();
  });
  foot.appendChild(sv); modal.appendChild(foot);
  var root=document.getElementById("modal-root"); root.innerHTML="";
  var bg=document.createElement("div"); bg.className="modal-bg";
  bg.addEventListener("click",function(e){if(e.target===bg)closeModal();});
  bg.appendChild(modal); root.appendChild(bg);
}

function openGoalModal(init) {
  var modal=document.createElement("div"); modal.className="modal";
  modal.innerHTML='<div class="modal-title">'+(init?"✏️ 목표 수정":"목표 추가")+'</div>';
  function field(lbl,el){var d=document.createElement("div");d.className="field";d.innerHTML="<label>"+lbl+"</label>";d.appendChild(el);return d;}
  var nmI=document.createElement("input"); nmI.type="text"; nmI.placeholder="비상금, 여행"; nmI.value=init?init.nm:"";
  var emI=document.createElement("input"); emI.type="text"; emI.placeholder="🎯"; emI.value=init?(init.em||"🎯"):"🎯"; emI.style.width="65px";
  var tgI=document.createElement("input"); tgI.type="number"; tgI.placeholder="0"; tgI.value=init?init.tg:"";
  var cvI=document.createElement("input"); cvI.type="number"; cvI.placeholder="0"; cvI.value=init?init.cv:"";
  var dtI=document.createElement("input"); dtI.type="date"; dtI.value=init?init.dt:"";
  modal.appendChild(field("목표명",nmI)); modal.appendChild(field("이모지",emI));
  modal.appendChild(field("목표금액 (원)",tgI)); modal.appendChild(field("현재 적립액 (원)",cvI));
  modal.appendChild(field("목표일",dtI));
  var foot=document.createElement("div"); foot.className="modal-footer";
  var cn=document.createElement("button"); cn.className="btn-n"; cn.textContent="취소"; cn.addEventListener("click",closeModal); foot.appendChild(cn);
  if(init){var db=document.createElement("button"); db.className="btn-d"; db.textContent="🗑 삭제"; db.addEventListener("click",function(){D.goals=D.goals.filter(function(g){return g.id!==init.id;});save();closeModal();renderPage();}); foot.appendChild(db);}
  var sv=document.createElement("button"); sv.className="btn-p"; sv.textContent="저장";
  sv.addEventListener("click",function(){
    var nm=nmI.value.trim(),tg=parseFloat(tgI.value)||0; if(!nm||!tg)return;
    var row={nm:nm,em:emI.value||"🎯",tg:tg,cv:parseFloat(cvI.value)||0,dt:dtI.value};
    if(init){row.id=init.id;D.goals=D.goals.map(function(g){return g.id===init.id?row:g;});}
    else{row.id=D.nid++;D.goals.push(row);}
    save();closeModal();renderPage();
  });
  foot.appendChild(sv); modal.appendChild(foot);
  var root=document.getElementById("modal-root"); root.innerHTML="";
  var bg=document.createElement("div"); bg.className="modal-bg";
  bg.addEventListener("click",function(e){if(e.target===bg)closeModal();});
  bg.appendChild(modal); root.appendChild(bg);
}

function openFixedModal(init) {
  var ct = init?init.ct:"주거·관리비";
  var modal=document.createElement("div"); modal.className="modal";
  modal.innerHTML='<div class="modal-title">'+(init?"✏️ 고정비용 수정":"고정비용 추가")+'</div>';
  function field(lbl,el){var d=document.createElement("div");d.className="field";d.innerHTML="<label>"+lbl+"</label>";d.appendChild(el);return d;}
  var nmI=document.createElement("input"); nmI.type="text"; nmI.placeholder="관리비, 넷플릭스"; nmI.value=init?init.nm:"";
  var amI=document.createElement("input"); amI.type="number"; amI.placeholder="0"; amI.value=init?init.am:"";
  var dayI=document.createElement("input"); dayI.type="number"; dayI.min="1"; dayI.max="31"; dayI.value=init?init.day:1; dayI.style.width="70px";

  var catF=document.createElement("div"); catF.className="field"; catF.innerHTML="<label>카테고리</label>";
  var catWrap=document.createElement("div");
  function renderCat(){ catWrap.innerHTML=""; catWrap.appendChild(makeEcatBtns(ct,function(k){ct=k;renderCat();})); }
  renderCat(); catF.appendChild(catWrap);

  modal.appendChild(field("항목명",nmI)); modal.appendChild(catF);
  modal.appendChild(field("금액 (원)",amI)); modal.appendChild(field("매월 며칠?",dayI));

  var foot=document.createElement("div"); foot.className="modal-footer";
  var cn=document.createElement("button"); cn.className="btn-n"; cn.textContent="취소"; cn.addEventListener("click",closeModal); foot.appendChild(cn);
  if(init){var db=document.createElement("button"); db.className="btn-d"; db.textContent="🗑 삭제"; db.addEventListener("click",function(){D.fixed=D.fixed.filter(function(f){return f.id!==init.id;});save();closeModal();renderPage();}); foot.appendChild(db);}
  var sv=document.createElement("button"); sv.className="btn-p"; sv.textContent="저장";
  sv.addEventListener("click",function(){
    var nm=nmI.value.trim(),am=parseFloat(amI.value)||0; if(!nm||!am)return;
    var row={nm:nm,ct:ct,am:am,day:parseInt(dayI.value)||1};
    if(!D.fixed)D.fixed=[];
    if(init){row.id=init.id;D.fixed=D.fixed.map(function(f){return f.id===init.id?row:f;});}
    else{row.id=D.nid++;D.fixed.push(row);}
    save();closeModal();renderPage();
  });
  foot.appendChild(sv); modal.appendChild(foot);
  var root=document.getElementById("modal-root"); root.innerHTML="";
  var bg=document.createElement("div"); bg.className="modal-bg";
  bg.addEventListener("click",function(e){if(e.target===bg)closeModal();});
  bg.appendChild(modal); root.appendChild(bg);
}

// ===================== Firebase 초기화 =====================
try {
  firebase.initializeApp({
    apiKey: "AIzaSyBQvgqGwV-1GZs1Zqj8B1KyETIjW0a1Xps",
    authDomain: "wuri-asset.firebaseapp.com",
    databaseURL: "https://wuri-asset-default-rtdb.firebaseio.com",
    projectId: "wuri-asset",
    storageBucket: "wuri-asset.firebasestorage.app",
    messagingSenderId: "1049215486629",
    appId: "1:1049215486629:web:de64ee60796885b7455b4c"
  });
  fbdb = firebase.database();

  // 실시간 데이터 수신
  fbdb.ref("wuri").on("value", function(snap) {
    var val = snap.val();
    if (val && val.assets && val.assets.length > 0) {
      // Firebase에 데이터 있으면 사용
      D = val;
      try { localStorage.setItem("wuri", JSON.stringify(D)); } catch(e) {}
    } else if (!val) {
      // Firebase가 비어있으면 INIT 데이터를 Firebase에 저장
      fbdb.ref("wuri").set(D);
    }
    if (!fbReady) {
      fbReady = true;
      updateSyncBadge(true);
    }
    renderTabs();
    renderPage();
  }, function(err) {
    // Firebase 실패시 localStorage로
    fbReady = false;
    load();
    renderTabs();
    renderPage();
  });
} catch(e) {
  load();
  renderTabs();
  renderPage();
}

function updateSyncBadge(connected) {
  var logo = document.querySelector(".logo");
  if (!logo) return;
  var badge = logo.querySelector(".sync-badge");
  if (!badge) {
    badge = document.createElement("span");
    badge.className = "sync-badge";
    badge.style.cssText = "font-size:10px;padding:2px 7px;border-radius:10px;margin-left:6px;font-weight:600";
    logo.appendChild(badge);
  }
  if (connected) {
    badge.textContent = "🔥 동기화중";
    badge.style.background = "rgba(76,175,136,.15)";
    badge.style.color = "#4caf88";
  } else {
    badge.textContent = "💾 로컬";
    badge.style.background = "rgba(136,144,181,.15)";
    badge.style.color = "#8890b5";
  }
}

// ===================== 시작 =====================
load();
renderTabs();
renderPage();
</script>
</body>
</html>
