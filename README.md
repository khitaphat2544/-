<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>โพยหวย</title>
<meta name="theme-color" content="#1d2b3a">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="โพยหวย">
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai+Looped:wght@400;600;800&display=swap" rel="stylesheet">
<style>
:root{--bg:#eef2ee;--card:#fff;--ink:#1d2b3a;--mut:#6a7886;--line:#d5ddd6;--red:#c8322b;--grn:#2f7d4f;--hi:#fff1d6;color-scheme:light}
@media (prefers-color-scheme:dark){:root{--bg:#121a22;--card:#1b2631;--ink:#e8eef4;--mut:#93a1af;--line:#2d3b49;--red:#ff6b61;--grn:#5fcf8c;--hi:#3a2f14;color-scheme:dark}}
*{box-sizing:border-box}html,body{margin:0}
body{background:var(--bg);color:var(--ink);font:16px/1.5 "Noto Sans Thai Looped",system-ui,sans-serif;padding-bottom:calc(150px + env(safe-area-inset-bottom,0px))}
button{cursor:pointer;touch-action:manipulation}
header{position:sticky;top:0;z-index:5;background:var(--bg);padding:calc(12px + env(safe-area-inset-top,0px)) 16px 8px;display:flex;gap:10px;align-items:center}
h1{font-size:22px;margin:0;font-weight:800;flex:1}
select,input,button,textarea{font:inherit;color:var(--ink)}
select,input[type=text],input[type=number],input[type=date],input[type=tel],textarea{background:var(--card);border:1.5px solid var(--line);border-radius:10px;padding:9px 11px;width:100%}
main{padding:0 14px;max-width:680px;margin:auto}
.card{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:14px;margin:0 0 12px}
h2{font-size:17px;margin:0 0 8px}
.mut{color:var(--mut);font-size:14px}
.row{display:flex;gap:8px;align-items:center}.row>*{flex:1}.sp{justify-content:space-between}.sp>*{flex:none}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.stat b{display:block;font-size:21px}
.num{font-weight:800;font-size:20px;letter-spacing:1px}
.dup{background:var(--hi);border-color:#e3b24f}
.tag{display:inline-block;font-size:12px;border:1px solid var(--line);border-radius:6px;padding:0 6px;margin-left:6px;color:var(--mut)}
.btn{background:var(--ink);color:var(--bg);border:0;border-radius:10px;padding:10px 14px;font-weight:600}
.btn.sec{background:transparent;color:var(--ink);border:1.5px solid var(--line)}
.btn.w{width:100%;margin-bottom:10px}
.x{background:none;border:0;color:var(--red);font-size:20px;padding:4px 8px}
.paid,.pos{color:var(--grn);font-weight:600}.unpaid,.neg{color:var(--red);font-weight:600}
.item{display:flex;gap:10px;align-items:center;padding:9px 0;border-top:1px solid var(--line)}
.item .g{flex:1;min-width:0}
nav{position:fixed;left:0;right:0;bottom:0;z-index:6;background:var(--card);border-top:1px solid var(--line);display:flex;padding-bottom:env(safe-area-inset-bottom,0px)}
nav button{flex:1;background:none;border:0;padding:10px 2px;color:var(--mut);font-weight:600;font-size:14px;line-height:1.25}
nav button.on{color:var(--ink);box-shadow:inset 0 3px var(--red)}
label.l{display:block;font-size:13px;color:var(--mut);margin:8px 0 3px}
.win{border-left:5px solid var(--grn)}
.chk{display:flex;align-items:center;gap:8px}.chk input{width:22px;height:22px;flex:none}
dialog{border:0;border-radius:16px;padding:16px;width:min(92vw,440px);background:var(--card);color:var(--ink)}
dialog::backdrop{background:rgba(0,0,0,.45)}
.empty{text-align:center;padding:24px 10px;color:var(--mut)}
table{width:100%;border-collapse:collapse;font-size:14px}td,th{padding:6px 4px;border-top:1px solid var(--line);text-align:right}th{font-weight:600;color:var(--mut)}td:first-child,th:first-child{text-align:left}
.sc{overflow-x:auto}
.chip{border:0;border-radius:99px;padding:6px 12px;font-weight:600;font-size:13px}
.chip.ok{background:rgba(47,125,79,.18);color:var(--grn)}.chip.no{background:rgba(200,50,43,.14);color:var(--red)}
.fab{position:fixed;right:16px;bottom:calc(86px + env(safe-area-inset-bottom,0px));z-index:8;background:var(--red);color:#fff;border:0;border-radius:99px;padding:14px 22px;font-weight:800;font-size:17px;box-shadow:0 4px 14px rgba(0,0,0,.28)}
.toast{position:fixed;left:50%;transform:translateX(-50%);bottom:calc(150px + env(safe-area-inset-bottom,0px));max-width:90vw;background:var(--ink);color:var(--bg);padding:8px 16px;border-radius:99px;opacity:0;transition:opacity .2s;pointer-events:none;z-index:20}.toast.on{opacity:1}
.warn{background:var(--hi);border-color:#e3b24f}
#aNum,#aAmt{font-size:22px;font-weight:800}
.pc{display:inline-block;font-weight:800;font-size:17px;letter-spacing:1px;background:var(--bg);border:1px solid var(--line);border-radius:8px;padding:1px 8px;margin:3px 4px 3px 0}
</style>
</head>
<body>
<header><h1>โพยหวย</h1><select id="drawSel" style="width:auto;max-width:58%"></select></header>
<main id="app"></main>
<nav>
<button data-a="tab" data-t="home">🏠<br>ภาพรวม</button><button data-a="tab" data-t="cust">👥<br>ลูกค้า</button><button data-a="tab" data-t="res">🎯<br>ผลรางวัล</button><button data-a="tab" data-t="sum">📊<br>สรุปยอด</button><button data-a="tab" data-t="menu">⚙️<br>เมนู</button>
</nav>
<button class="fab" data-a="fab">+ แทง</button><div class="toast" id="toast"></div>

<dialog id="dlgDraw"><h2>เปิดงวดใหม่</h2><label class="l">วันที่หวยออก</label><input type="date" id="dDate">
<div class="row" style="margin-top:14px"><button class="btn sec" data-a="close" data-d="dlgDraw">ยกเลิก</button><button class="btn" data-a="saveDraw">เปิดงวด</button></div></dialog>

<dialog id="dlgAdd"><h2>บันทึกเลขลูกค้า</h2>
<label class="l">ลูกค้า</label><select id="aCust"></select>
<div class="row"><div><label class="l">ประเภท</label><select id="aType"></select></div><div><label class="l">เลข</label><input type="tel" id="aNum" inputmode="numeric" maxlength="3"></div></div>
<div class="row"><div><label class="l">จำนวนเงิน (บาท)</label><input type="number" id="aAmt" inputmode="decimal" min="0"></div><div><label class="l">วันที่ซื้อ</label><input type="date" id="aDate"></div></div>
<div class="mut" id="aPrev" style="margin-top:8px"></div>
<label class="chk" id="aPerWrap" style="margin-top:8px"><input type="checkbox" id="aPer"> คิดเงินทุกชุดที่สลับ (ราคานี้ต่อ 1 ชุด)</label>
<label class="chk" style="margin-top:12px"><input type="checkbox" id="aPaid"> จ่ายเงินแล้ว</label>
<p id="aErr" style="color:var(--red);margin:6px 0 0;font-size:14px"></p>
<div class="row" style="margin-top:12px"><button class="btn sec" data-a="close" data-d="dlgAdd">ปิด</button><button class="btn" data-a="saveAdd">บันทึก แล้วเพิ่มต่อ</button></div></dialog>

<dialog id="dlgOut"><h2 id="oTitle"></h2><textarea id="oText" rows="12" readonly style="font-size:14px"></textarea>
<div class="row" style="margin-top:10px"><button class="btn sec" data-a="close" data-d="dlgOut">ปิด</button><button class="btn sec" data-a="oCopy">คัดลอก</button><button class="btn" data-a="oSave">บันทึกไฟล์</button></div>
<p class="mut" id="oMsg"></p></dialog>

<dialog id="dlgAsk"><p id="askMsg" style="margin:0 0 14px"></p><div class="row"><button class="btn sec" data-a="askNo">ยกเลิก</button><button class="btn" data-a="askOk">ยืนยัน</button></div></dialog>
<input type="file" id="fileIn" accept=".json,application/json" hidden>

<script>
const dlgDraw=document.getElementById('dlgDraw'),dlgAdd=document.getElementById('dlgAdd'),dlgOut=document.getElementById('dlgOut'),dlgAsk=document.getElementById('dlgAsk');
const $=id=>document.getElementById(id);
const TYPES={t2:{n:'2 ตัวบน เต็ง',g:'เต็ง',len:2,c:70,h:80},b2:{n:'2 ตัวล่าง เต็ง',g:'เต็ง',len:2,c:70,h:80},t3:{n:'3 ตัวบน เต็ง',g:'เต็ง',len:3,c:500,h:600},d2:{n:'2 ตัวบน โต๊ด',g:'โต๊ด',len:2,c:35,h:40},e2:{n:'2 ตัวล่าง โต๊ด',g:'โต๊ด',len:2,c:35,h:40},d3:{n:'3 ตัวโต๊ด',g:'โต๊ด',len:3,c:100,h:120},rt:{n:'วิ่งบน',g:'วิ่ง',len:1,c:3,h:4},rb:{n:'วิ่งล่าง',g:'วิ่ง',len:1,c:3,h:4}};
const isToad=t=>TYPES[t]&&TYPES[t].g==='โต๊ด';
const perms=x=>{if(x.length<=1)return[x];const o=new Set();for(let i=0;i<x.length;i++)for(const p of perms(x.slice(0,i)+x.slice(i+1)))o.add(x[i]+p);return[...o]};
const canon=(t,n)=>isToad(t)?n.split('').sort().join(''):n;
const chips=n=>perms(n).map(p=>`<span class="pc">${p}</span>`).join('');
const stake=e=>e.per&&isToad(e.type)?e.amt*perms(e.num).length:e.amt;
const KEY='poyhuay.v1';
const def=()=>({customers:[],draws:{},cur:null,rc:{},rh:{},pct:100});
let S=def(),memOnly=false,raw=null,tab='home',hist='all',lastType='t2',askFn=null,outName='',outData='';
try{raw=localStorage.getItem(KEY)}catch(e){memOnly=true}
if(raw){try{const o=JSON.parse(raw);if(o&&typeof o==='object')S=Object.assign(def(),o)}catch(e){try{localStorage.setItem(KEY+'.bad',raw)}catch(_){}}}
const uid=()=>Date.now().toString(36)+Math.random().toString(36).slice(2,7);
function save(){try{localStorage.setItem(KEY,JSON.stringify(S))}catch(e){memOnly=true}}
function fix(){
 if(!Array.isArray(S.customers))S.customers=[];
 if(!S.draws||typeof S.draws!=='object')S.draws={};
 S.rc=S.rc||{};S.rh=S.rh||{};
 if(S.rates){for(const k in S.rates)if(S.rc[k]==null)S.rc[k]=S.rates[k];delete S.rates}
 for(const k in TYPES){if(typeof S.rc[k]!=='number')S.rc[k]=TYPES[k].c;if(typeof S.rh[k]!=='number')S.rh[k]=TYPES[k].h}
 S.pct=isFinite(+S.pct)?+S.pct:100;
 for(const d of Object.values(S.draws)){if(!Array.isArray(d.entries))d.entries=[];d.res=d.res||{};
  for(const e of d.entries){e.amt=+e.amt||0;
   if(!e.cid){let c=S.customers.find(x=>x.name===e.name);if(!c){c={id:uid(),name:e.name||'ไม่ระบุชื่อ'};S.customers.push(c)}e.cid=c.id;delete e.name}}}}
fix();
const iso=d=>d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
const fmt=n=>(Math.round(n*100)/100).toLocaleString('th-TH');
const dstr=d=>new Date(d+'T00:00:00').toLocaleDateString('th-TH',{day:'numeric',month:'short',year:'numeric'});
const esc=s=>String(s).replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const cur=()=>S.draws[S.cur];
const cname=id=>(S.customers.find(c=>c.id===id)||{name:'(ลบแล้ว)'}).name;
const sgn=n=>`<span class="${n>=0?'pos':'neg'}">${n>=0?'+':'−'}${fmt(Math.abs(n))}</span>`;
const openD=d=>{try{d.showModal()}catch(e){d.setAttribute('open','')}};
const closeD=d=>{try{d.close()}catch(e){d.removeAttribute('open')}};
function say(m){const t=$('toast');t.textContent=m;t.classList.add('on');clearTimeout(say.t);say.t=setTimeout(()=>t.classList.remove('on'),2200)}
function ask(m,fn){askFn=fn;$('askMsg').textContent=m;openD(dlgAsk)}

function openDraw(date,select){let id=Object.keys(S.draws).find(i=>S.draws[i].date===date);
 if(!id){id=uid();S.draws[id]={date,entries:[],res:{}};if(select)S.cur=id}return id}
function autoOpen(){const t=new Date(),y=t.getFullYear(),m=t.getMonth(),d=t.getDate();
 // วันที่ 10 เปิดงวดวันที่ 16 / วันที่ 25 เปิดงวดวันที่ 1 เดือนถัดไป
 const tgt=d>=25?iso(new Date(y,m+1,1)):d>=10?iso(new Date(y,m,16)):iso(new Date(y,m,1));
 openDraw(tgt,true);
 if(!S.cur||!S.draws[S.cur])S.cur=Object.keys(S.draws).find(i=>S.draws[i].date===tgt);save()}
autoOpen();

function winnersOf(d){const r=d.res||{},f=r.first||'',l2=r.low2||'';if(f.length!==6&&l2.length!==2)return[];
 const l3=f.length===6?f.slice(3):'',t2=f.length===6?f.slice(4):'',srt=s=>s.split('').sort().join(''),out=[];
 for(const e of d.entries){const T=e.type;let h=false;
  if(T==='t2')h=t2&&e.num===t2;if(T==='b2')h=l2&&e.num===l2;if(T==='t3')h=l3&&e.num===l3;
  if(T==='d3')h=l3&&srt(e.num)===srt(l3);if(T==='d2')h=t2&&srt(e.num)===srt(t2);if(T==='e2')h=l2&&srt(e.num)===srt(l2);if(T==='rt')h=l3&&l3.includes(e.num);if(T==='rb')h=l2&&l2.includes(e.num);
  if(h)out.push(Object.assign({},e,{payC:e.amt*S.rc[T],payH:e.amt*S.rh[T]*S.pct/100}))}
 return out}
function calc(d){const W=winnersOf(d),bets=d.entries.reduce((a,e)=>a+stake(e),0),sent=bets*S.pct/100;
 const winC=W.reduce((a,w)=>a+w.payC,0),recH=W.reduce((a,w)=>a+w.payH,0);
 const per={};d.entries.forEach(e=>{const p=per[e.cid]=per[e.cid]||{bets:0,unpaid:0,win:0};p.bets+=stake(e);if(!e.paid)p.unpaid+=s
