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
function calc(d){const W=winnersOf(d),bets=d.entries.reduce((a,e)=>a+e.amt,0),sent=bets*S.pct/100;
 const winC=W.reduce((a,w)=>a+w.payC,0),recH=W.reduce((a,w)=>a+w.payH,0);
 const per={};d.entries.forEach(e=>{const p=per[e.cid]=per[e.cid]||{bets:0,unpaid:0,win:0};p.bets+=e.amt;if(!e.paid)p.unpaid+=e.amt});
 W.forEach(w=>{per[w.cid].win+=w.payC});
 const hasRes=!!(d.res&&((d.res.first||'').length===6||(d.res.low2||'').length===2));
 return{W,bets,sent,winC,recH,per,profit:bets-winC-sent+recH,hasRes}}
function group(d){const g={};for(const e of d.entries){const k=e.type+'|'+canon(e.type,e.num);(g[k]=g[k]||[]).push(e)}return g}

function home(){const d=cur(),E=d.entries,tot=E.reduce((a,e)=>a+e.amt,0),pd=E.filter(e=>e.paid).reduce((a,e)=>a+e.amt,0),g=group(d),keys=Object.keys(g).sort(),dups=keys.filter(k=>g[k].length>1);
 const who=k=>g[k].map(e=>esc(cname(e.cid))+' '+fmt(e.amt)).join(' · ');
 const n=Math.round((new Date(d.date+'T00:00:00')-new Date(iso(new Date())+'T00:00:00'))/864e5);
 let h=`<div class="card"><h2>งวด ${dstr(d.date)}</h2><div class="mut" style="margin:-6px 0 8px">${n>0?'อีก '+n+' วันหวยออก':n===0?'หวยออกวันนี้':'หวยออกแล้ว'} · ${E.length} รายการ</div><div class="stats"><div class="stat"><span class="mut">ยอดรวม</span><b>${fmt(tot)}</b></div><div class="stat"><span class="mut">รับแล้ว</span><b class="paid">${fmt(pd)}</b></div><div class="stat"><span class="mut">ค้างจ่าย</span><b class="unpaid">${fmt(tot-pd)}</b></div></div></div>
 <div class="card ${dups.length?'dup':''}"><h2>เลขซ้ำ (${dups.length})</h2>`+
 (dups.length?dups.map(k=>{const[t,n]=k.split('|');return`<div class="item"><span class="num">${n}</span><div class="g"><span class="tag">${TYPES[t].n}</span> ${g[k].length} คน<div class="mut">${who(k)}</div></div><b>${fmt(g[k].reduce((a,e)=>a+e.amt,0))}</b></div>`}).join(''):'<div class="mut">ยังไม่มีเลขซ้ำ</div>')+
 `</div><div class="card"><h2>ใครซื้อเลขอะไรบ้าง</h2>`+
 (keys.length?keys.map(k=>{const[t,n]=k.split('|');return`<div class="item"><span class="num">${n}</span><div class="g"><span class="tag">${TYPES[t].n}</span><div class="mut">${who(k)}</div></div></div>`}).join(''):'<div class="empty">ยังไม่มีโพย ไปที่แท็บ “ลูกค้า”</div>')+'</div>';
 return h}

function cust(){const d=cur();let h=`<div class="card"><h2>เพิ่มลูกค้า</h2><div class="row"><input type="text" id="cNew" placeholder="พิมพ์ชื่อลูกค้า" autocomplete="off"><button class="btn" data-a="cAdd" style="flex:none">เพิ่ม</button></div></div>`;
 if(!S.customers.length)return h+'<div class="card empty">ยังไม่มีลูกค้า พิมพ์ชื่อด้านบนแล้วกด “เพิ่ม”</div>';
 for(const c of [...S.customers].sort((a,b)=>a.name.localeCompare(b.name,'th'))){const es=d.entries.filter(e=>e.cid===c.id).sort((a,b)=>(b.date||'').localeCompare(a.date||'')),t=es.reduce((s,e)=>s+e.amt,0),u=es.filter(e=>!e.paid).reduce((s,e)=>s+e.amt,0);
  h+=`<div class="card"><div class="row sp"><h2 style="margin:0">${esc(c.name)}</h2><span><button class="btn" data-a="add" data-id="${c.id}">+ แทง</button> <button class="x" data-a="dc" data-id="${c.id}" aria-label="ลบลูกค้า">🗑</button></span></div>
  <div class="mut">รวม ${fmt(t)} บาท · <span class="${u?'unpaid':'paid'}">${u?'ค้าง '+fmt(u):'จ่ายครบ'}</span></div>`+
  es.map(e=>`<div class="item"><span class="num">${e.num}</span><div class="g"><span class="tag">${TYPES[e.type]?TYPES[e.type].n:e.type}</span> ${fmt(e.amt)} บาท<div class="mut">ซื้อวันที่ ${e.date?dstr(e.date):'-'}</div>${isToad(e.type)?`<div class="mut">โต๊ด ถูกเมื่อออก: ${perms(e.num).join(' · ')}</div>`:''}</div><button class="chip ${e.paid?'ok':'no'}" data-a="pay" data-id="${e.id}">${e.paid?'จ่ายแล้ว ✓':'ยังไม่จ่าย'}</button><button class="x" data-a="del" data-id="${e.id}" aria-label="ลบ">×</button></div>`).join('')+'</div>'}
 return h}

function res(){const d=cur(),r=d.res||{};
 let h=`<div class="card"><h2>ระบุรางวัลที่ออก</h2><div class="row"><div><label class="l">รางวัลที่ 1 (6 หลัก)</label><input type="tel" inputmode="numeric" maxlength="6" id="rFirst" value="${r.first||''}"></div><div><label class="l">เลขท้าย 2 ตัวล่าง</label><input type="tel" inputmode="numeric" maxlength="2" id="rLow" value="${r.low2||''}"></div></div></div>
 <div class="card"><h2>กำหนดตัวคูณ (บาทละกี่บาท)</h2><table><tr><th>ประเภท</th><th>จ่ายลูกค้า</th><th>เจ้าจ่ายเรา</th></tr>`+
 Object.keys(TYPES).map(k=>`<tr><td>${TYPES[k].n}</td><td><input type="number" inputmode="decimal" data-rc="${k}" value="${S.rc[k]}"></td><td><input type="number" inputmode="decimal" data-rh="${k}" value="${S.rh[k]}"></td></tr>`).join('')+
 `</table><label class="l">สัดส่วนยอดที่ส่งต่อให้เจ้า (%)</label><input type="number" inputmode="decimal" id="pct" value="${S.pct}"><div class="mut">โต๊ด = ถูกเลขสลับตำแหน่งได้ ตั้งราคาจ่ายโต๊ดแยกจากเต็งในตารางนี้ได้ เช่น ส่งต่อทั้งหมด = 100, ส่งครึ่งเดียว = 50 ตัวคูณใช้กับทุกงวด</div></div>`;
 return h+'<div id="resOut">'+resOut()+'</div>'}
function resOut(){const d=cur();let h='';const c=calc(d);if(!c.hasRes)return h+'<div class="card empty">ใส่เลขที่ออก แอพจะตรวจให้ทันที</div>';
 if(!c.W.length)return h+'<div class="card empty">งวดนี้ไม่มีใครถูกรางวัล</div>';
 const by={};c.W.forEach(w=>(by[w.cid]=by[w.cid]||[]).push(w));
 h+=`<h2 style="margin:6px 2px">ลูกค้าที่ถูกรางวัล ${Object.keys(by).length} คน</h2>`;
 for(const id in by){const a=by[id];h+=`<div class="card win"><div class="row sp"><h2 style="margin:0">${esc(cname(id))}</h2><b class="neg" style="font-size:22px">${fmt(a.reduce((s,w)=>s+w.payC,0))}</b></div>`+
  a.map(w=>`<div class="item"><span class="num">${w.num}</span><div class="g"><span class="tag">${TYPES[w.type].n}</span> ${fmt(w.amt)} × ${S.rc[w.type]}<div class="mut">${w.paid?'':'⚠ ยังไม่ได้รับเงินซื้อ'}</div></div><b>${fmt(w.payC)}</b></div>`).join('')+'</div>'}
 return h}

function sum(){const d=cur(),c=calc(d);
 let h=`<div class="card"><h2>สรุปยอดรวมงวด ${dstr(d.date)}</h2><table>
 <tr><td>ยอดซื้อรวมทุกลูกค้า</td><td>${fmt(c.bets)}</td></tr>
 <tr><td>ส่งให้เจ้า (${S.pct}%)</td><td>${fmt(c.sent)}</td></tr>
 <tr><td>ต้องจ่ายลูกค้า (ถูกรางวัล)</td><td class="neg">${fmt(c.winC)}</td></tr>
 <tr><td>เจ้าต้องจ่ายเรา</td><td class="pos">${fmt(c.recH)}</td></tr>
 <tr><td><b>${c.profit>=0?'กำไรสุทธิ':'ขาดทุนสุทธิ'}</b></td><td><b>${sgn(c.profit)}</b></td></tr></table>
 ${c.hasRes?'':'<div class="mut" style="margin-top:6px">ยังไม่ได้ใส่ผลรางวัล</div>'}
 <button class="btn w" style="margin-top:12px" data-a="sendH">ส่งไฟล์สรุปยอดให้เจ้า</button></div>`;
 h+=`<div class="card"><h2>สรุปรายลูกค้า (งวดนี้)</h2><div class="sc"><table><tr><th>ลูกค้า</th><th>ซื้อ</th><th>ถูก</th><th>สุทธิ</th></tr>`+
 (Object.keys(c.per).map(id=>{const p=c.per[id];return`<tr><td>${esc(cname(id))}${p.unpaid?`<div class="mut">ค้างจ่าย ${fmt(p.unpaid)}</div>`:''}</td><td>${fmt(p.bets)}</td><td>${fmt(p.win)}</td><td>${sgn(p.win-p.bets)}</td></tr>`}).join('')||'<tr><td colspan="4" class="empty">ไม่มีข้อมูล</td></tr>')+
 `</table></div><div class="mut" style="margin-top:6px">สุทธิ + = เราต้องจ่ายลูกค้า · − = เก็บเงินจากลูกค้า</div></div>`;
 const ids=Object.keys(S.draws).sort((a,b)=>S.draws[b].date.localeCompare(S.draws[a].date));
 h+=`<div class="card"><h2>สรุปย้อนหลังรายงวด</h2><select id="histSel"><option value="all">ลูกค้าทุกคน</option>${S.customers.map(x=>`<option value="${x.id}" ${hist===x.id?'selected':''}>${esc(x.name)}</option>`).join('')}</select><div class="sc"><table style="margin-top:8px"><tr><th>งวด</th><th>ซื้อ</th><th>ถูก</th><th>สุทธิ</th></tr>`;
 let tb=0,tw=0;for(const i of ids){const dd=S.draws[i],cc=calc(dd);let b,w;
  if(hist==='all'){b=cc.bets;w=cc.winC}else{const p=cc.per[hist]||{bets:0,win:0};b=p.bets;w=p.win}
  if(!b&&!w)continue;tb+=b;tw+=w;h+=`<tr><td>${dstr(dd.date)}${cc.hasRes?'':' <span class="mut">(ยังไม่ออก)</span>'}</td><td>${fmt(b)}</td><td>${fmt(w)}</td><td>${sgn(w-b)}</td></tr>`}
 return h+`<tr><th>รวม</th><th>${fmt(tb)}</th><th>${fmt(tw)}</th><th>${sgn(tw-tb)}</th></tr></table></div></div>`}

function menu(){return `<div class="card"><h2>เมนู</h2>
 <button class="btn w" data-a="mNew">เปิดงวดใหม่ (กำหนดวันที่เอง)</button>
 <button class="btn w sec" data-a="mBackup">บันทึกไฟล์สำรองข้อมูลทั้งหมด</button>
 <button class="btn w sec" data-a="mLoad">โหลดไฟล์โพยจากเครื่อง</button>
 <p class="mut">ระบบเปิดงวดให้อัตโนมัติ: วันที่ 10 เปิดงวดวันที่ 16 ของเดือน และวันที่ 25 เปิดงวดวันที่ 1 ของเดือนถัดไป การโหลดไฟล์จะรวมลูกค้าและงวดจากไฟล์เข้ากับข้อมูลในเครื่อง</p></div>
 <div class="card"><h2>ลบงวดนี้</h2><p class="mut">ลบรายการและผลรางวัลของงวด ${dstr(cur().date)} ทั้งหมด</p><button class="btn sec" data-a="mDel">ลบงวดนี้</button></div>`}

function render(){
 if(!S.draws[S.cur])autoOpen();
 const ids=Object.keys(S.draws).sort((a,b)=>S.draws[b].date.localeCompare(S.draws[a].date));
 $('drawSel').innerHTML=ids.map(i=>`<option value="${i}" ${i===S.cur?'selected':''}>งวด ${dstr(S.draws[i].date)}</option>`).join('');
 const warn=memOnly?'<div class="card warn">⚠ เบราว์เซอร์นี้ไม่ยอมเก็บข้อมูลถาวร (อาจเปิดโหมดส่วนตัวอยู่) ข้อมูลจะหายเมื่อปิดหน้านี้ ควรกด “บันทึกไฟล์สำรองข้อมูล” ในเมนูบ่อย ๆ</div>':'';
 $('app').innerHTML=warn+{home,cust,res,sum,menu}[tab]();
 document.querySelectorAll('nav button').forEach(b=>b.classList.toggle('on',b.dataset.t===tab))}

function addCust(){const i=$('cNew');if(!i)return;const n=i.value.trim();
 if(!n)return say('พิมพ์ชื่อลูกค้าก่อน');
 if(S.customers.some(c=>c.name.toLowerCase()===n.toLowerCase()))return say('มีชื่อ “'+n+'” อยู่แล้ว');
 S.customers.push({id:uid(),name:n});save();render();say('เพิ่ม “'+n+'” แล้ว');const j=$('cNew');if(j)j.focus()}
function openAdd(cid){if(!S.customers.length){tab='cust';render();return say('เพิ่มรายชื่อลูกค้าก่อน')}
 $('aCust').innerHTML=S.customers.map(c=>`<option value="${c.id}" ${c.id===cid?'selected':''}>${esc(c.name)}</option>`).join('');
 $('aType').innerHTML=['เต็ง','โต๊ด','วิ่ง'].map(g=>`<optgroup label="${g==='เต็ง'?'เต็ง (ถูกเลขและตำแหน่ง)':g==='โต๊ด'?'โต๊ด (ถูกเลข สลับที่ได้)':'วิ่ง'}">`+Object.keys(TYPES).filter(k=>TYPES[k].g===g).map(k=>`<option value="${k}">${TYPES[k].n}</option>`).join('')+'</optgroup>').join('');
 $('aType').value=lastType;$('aNum').maxLength=TYPES[lastType].len;$('aNum').value='';$('aAmt').value='';$('aDate').value=iso(new Date());$('aErr').textContent='';prev();
 openD(dlgAdd);setTimeout(()=>$('aNum').focus(),80)}
function prev(){const t=$('aType').value,n=$('aNum').value.trim();let s='จ่ายลูกค้าบาทละ '+S.rc[t]+' · ';
 if(isToad(t))s+=n.length===TYPES[t].len?'โต๊ด ถูกเมื่อออก: '+perms(n).join(' · '):'โต๊ด ถูกเลข สลับตำแหน่งได้ (แอพรันให้)';
 else if(TYPES[t].g==='เต็ง')s+='เต็ง ต้องถูกทั้งเลขและตำแหน่ง';else s+='วิ่ง ถูกถ้ามีเลขนี้ออก';
 $('aPrev').textContent=s}
function saveAdd(){const cid=$('aCust').value,type=$('aType').value,num=$('aNum').value.trim(),amt=parseFloat($('aAmt').value),err=$('aErr');
 if(!cid)return err.textContent='เลือกลูกค้า';
 if(!new RegExp('^\\d{'+TYPES[type].len+'}$').test(num))return err.textContent='เลขต้องเป็นตัวเลข '+TYPES[type].len+' หลัก';
 if(!(amt>0))return err.textContent='ใส่จำนวนเงิน';
 cur().entries.push({id:uid(),cid,type,num,amt,date:$('aDate').value||iso(new Date()),paid:$('aPaid').checked});save();render();
 $('aNum').value='';$('aAmt').value='';$('aNum').focus();err.textContent='บันทึกแล้ว ✓ '+cname(cid)+' '+num;prev()}
function sendHouse(){const d=cur(),c=calc(d),g=group(d),L=['สรุปยอดส่งเจ้า งวดวันที่ '+dstr(d.date),''];
 const agg={};for(const k in g)agg[k]=g[k].reduce((a,e)=>a+e.amt,0);
 for(const t in TYPES){const ks=Object.keys(agg).filter(k=>k.startsWith(t+'|')).sort();if(!ks.length)continue;
  L.push('['+TYPES[t].n+']');ks.forEach(k=>L.push(k.split('|')[1]+' = '+fmt(agg[k]*S.pct/100)));L.push('')}
 L.push('ยอดรวมที่ส่ง: '+fmt(c.sent)+' บาท ('+S.pct+'% ของยอดซื้อ '+fmt(c.bets)+')');
 if(c.hasRes){L.push('ผลรางวัล: '+(d.res.first||'-')+' / ล่าง '+(d.res.low2||'-'));L.push('ยอดที่เจ้าต้องจ่าย: '+fmt(c.recH)+' บาท')}
 output('สรุปยอดส่งเจ้า','poy-'+d.date+'.txt',L.join('\n'))}
function output(title,name,text){outName=name;outData=text;$('oTitle').textContent=title;$('oText').value=text;$('oMsg').textContent='';openD(dlgOut)}

function act(a,t){switch(a){
 case 'tab':tab=t.dataset.t;render();scrollTo(0,0);break;
 case 'cAdd':addCust();break;
 case 'add':openAdd(t.dataset.id);break;
 case 'fab':openAdd(null);break;
 case 'dc':{const id=t.dataset.id;ask('ลบลูกค้า “'+cname(id)+'” และรายการทั้งหมดของลูกค้ารายนี้ (ทุกงวด)?',()=>{S.customers=S.customers.filter(c=>c.id!==id);for(const x of Object.values(S.draws))x.entries=x.entries.filter(e=>e.cid!==id);save();render();say('ลบแล้ว')});break}
 case 'pay':{const e=cur().entries.find(x=>x.id===t.dataset.id);if(e){e.paid=!e.paid;save();render()}break}
 case 'del':{const id=t.dataset.id;ask('ลบรายการนี้?',()=>{cur().entries=cur().entries.filter(x=>x.id!==id);save();render()});break}
 case 'sendH':sendHouse();break;
 case 'mNew':$('dDate').value=iso(new Date());openD(dlgDraw);break;
 case 'mBackup':output('สำรองข้อมูลทั้งหมด','poyhuay-backup-'+iso(new Date())+'.json',JSON.stringify(S));break;
 case 'mLoad':$('fileIn').click();break;
 case 'mDel':ask('ลบงวดนี้ทั้งหมด?',()=>{delete S.draws[S.cur];S.cur=null;autoOpen();save();render()});break;
 case 'saveDraw':{const d=$('dDate').value;if(!d)return;const id=openDraw(d,true);S.cur=id;save();closeD(dlgDraw);tab='home';render();break}
 case 'saveAdd':saveAdd();break;
 case 'close':closeD($(t.dataset.d));break;
 case 'oSave':try{const u=URL.createObjectURL(new Blob(['\ufeff'+outData],{type:'text/plain;charset=utf-8'}));const l=document.createElement('a');l.href=u;l.download=outName;document.body.appendChild(l);l.click();l.remove();setTimeout(()=>URL.revokeObjectURL(u),2000);$('oMsg').textContent='บันทึกไฟล์แล้ว (ดูในโฟลเดอร์ดาวน์โหลด)'}catch(e){$('oMsg').textContent='บันทึกไม่ได้ กด “คัดลอก” แทน'}break;
 case 'oCopy':(async()=>{try{await navigator.clipboard.writeText(outData)}catch(e){$('oText').select();document.execCommand('copy')}$('oMsg').textContent='คัดลอกแล้ว'})();break;
 case 'askOk':{const f=askFn;askFn=null;closeD(dlgAsk);if(f)f();break}
 case 'askNo':askFn=null;closeD(dlgAsk);break}}

document.addEventListener('click',e=>{const t=e.target.closest('[data-a]');if(!t)return;try{act(t.dataset.a,t)}catch(err){say('ผิดพลาด: '+err.message)}});
document.addEventListener('change',e=>{const t=e.target;try{
 if(t.id==='rFirst'||t.id==='rLow'){cur().res={first:$('rFirst').value.replace(/\D/g,''),low2:$('rLow').value.replace(/\D/g,'')};save();upd()}
 else if(t.id==='pct'){S.pct=Math.min(100,Math.max(0,parseFloat(t.value)||0));save();upd()}
 else if(t.dataset.rc){S.rc[t.dataset.rc]=parseFloat(t.value)||0;save();upd()}
 else if(t.dataset.rh){S.rh[t.dataset.rh]=parseFloat(t.value)||0;save();upd()}
 else if(t.id==='histSel'){hist=t.value;render()}
 else if(t.id==='drawSel'){S.cur=t.value;save();render()}
 else if(t.id==='aType'){lastType=t.value;$('aNum').maxLength=TYPES[lastType].len;prev();$('aNum').focus()}
 else if(t.id==='fileIn'){importFile(t)}
}catch(err){say('ผิดพลาด: '+err.message)}});
document.addEventListener('keydown',e=>{if(e.key!=='Enter')return;
 if(e.target.id==='cNew'){e.preventDefault();addCust()}
 else if(e.target.id==='aAmt'||e.target.id==='aNum'){e.preventDefault();saveAdd()}});
document.addEventListener('input',e=>{if(e.target.id==='aNum'){prev();if(e.target.value.length>=TYPES[$('aType').value].len)$('aAmt').focus()}});

function upd(){const o=$('resOut');if(o)o.innerHTML=resOut()}
function importFile(inp){const f=inp.files[0];if(!f)return;const r=new FileReader();
 r.onload=()=>{try{const o=JSON.parse(r.result);if(!o.draws)throw 0;
  const mp={};for(const c of o.customers||[]){let x=S.customers.find(k=>k.name===c.name);if(!x){x={id:c.id||uid(),name:c.name};S.customers.push(x)}mp[c.id]=x.id}
  for(const d of Object.values(o.draws)){const id=openDraw(d.date,false),t=S.draws[id];if(!t.entries.length)t.res=d.res||{};
   for(const en of d.entries||[]){const cid=mp[en.cid];if(cid&&!t.entries.some(x=>x.id===en.id))t.entries.push(Object.assign({},en,{cid}))}}
  fix();save();render();say('โหลดไฟล์เรียบร้อย')}catch(x){say('ไฟล์นี้ไม่ใช่ไฟล์สำรองจากแอพนี้')}inp.value=''};
 r.readAsText(f)}

window.addEventListener('error',e=>say('ผิดพลาด: '+e.message));
render();
</script>
</body>
</html>
