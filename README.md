# Theatres-CRM
a tailored CRM for the theatres desk
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>South Theatres CRM</title>
<style>
:root{
--bg:#f5f4f1;--su:#fff;--su2:#efede8;--su3:#e8e6e0;
--b1:rgba(0,0,0,0.08);--b2:rgba(0,0,0,0.16);
--tx:#18180f;--t2:#5c5b52;--t3:#99978d;
--bl:#1558a0;--blbg:#e8f0fa;--bltx:#1558a0;
--gr:#157a52;--grbg:#e2f4ec;--grtx:#157a52;
--am:#a06010;--ambg:#faf0df;--amtx:#a06010;--redbg:#faeaea;
--r:8px;--rl:12px;
}
@media(prefers-color-scheme:dark){:root{
--bg:#161612;--su:#1f1f1a;--su2:#272722;--su3:#2f2f29;
--b1:rgba(255,255,255,0.07);--b2:rgba(255,255,255,0.14);
--tx:#f0ede6;--t2:#a09d94;--t3:#66645c;
--blbg:#102240;--bltx:#6fa8dc;
--grbg:#0e2e1e;--grtx:#5dbf8e;
--ambg:#2e1e06;--amtx:#d4923a;
--redbg:#2e0e0e;
}}
*{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%;overflow:hidden}
body{font-family:-apple-system,'Helvetica Neue',Arial,sans-serif;background:var(--bg);color:var(--tx);font-size:14px;display:flex;flex-direction:column}
button,input{font-family:inherit;font-size:14px}
nav{background:var(--su);border-bottom:0.5px solid var(--b2);padding:0 16px;display:flex;align-items:center;height:46px;flex-shrink:0;z-index:100;overflow:visible;z-index:10000;position:relative}
.brand{font-size:13px;font-weight:500;margin-right:16px;white-space:nowrap;flex-shrink:0;color:var(--tx)}
.brand em{color:var(--t2);font-style:normal;font-weight:400}
.ntab{padding:0 12px;height:46px;display:flex;align-items:center;font-size:13px;color:var(--t2);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap;user-select:none;flex-shrink:0}
.ntab:hover{color:var(--tx)}.ntab.on{color:var(--bl);border-bottom-color:var(--bl)}
#app{flex:1;overflow:hidden;display:flex;flex-direction:column}
.pg{display:none;flex:1;overflow:hidden;flex-direction:column}.pg.on{display:flex}
.scr{flex:1;overflow-y:auto;padding:14px 16px}

/* WEEK BAR */
.wkbar{display:flex;align-items:center;gap:7px;margin-bottom:10px;flex-shrink:0;flex-wrap:wrap}
.wb{padding:4px 11px;font-size:12px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;color:var(--t2);white-space:nowrap}
.wb:hover{background:var(--su2);color:var(--tx)}.wb.on{background:var(--bl);color:#fff;border-color:transparent}
.wklbl{font-size:13px;font-weight:500}

/* METRICS */
.mets{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:10px;flex-shrink:0}
.met{background:var(--su2);border-radius:var(--r);padding:10px 13px}
.metl{font-size:11px;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:3px}
.metv{font-size:22px;font-weight:500}
.mets2{font-size:11px;color:var(--t3);margin-top:1px}

/* SHIFT TABLE */
.stw{flex:1;overflow:auto}
table.st{border-collapse:collapse;min-width:100%}
table.st thead th{position:sticky;top:0;background:var(--su);z-index:10;padding:0;border-bottom:0.5px solid var(--b2)}
.thi{padding:7px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.04em;white-space:nowrap}
table.st td{padding:2px 2px;border-bottom:0.5px solid var(--b1);vertical-align:middle}
table.st tbody tr:hover td{background:var(--su2)}
.cn{padding:3px 7px;font-size:12px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:168px;display:block}
.cs{font-size:10px;color:var(--t3);font-weight:400}

/* CELL INPUT — key fix: pointer-events always on */
.ci{width:108px;padding:5px 6px;font-size:12px;border:0.5px solid transparent;border-radius:5px;background:transparent;color:var(--tx);outline:none;cursor:pointer}
.ci:hover{background:var(--su3)}.ci:focus{background:var(--su);border-color:var(--bl);cursor:text}
.ci.f{background:var(--blbg);color:var(--bltx);font-weight:500}
.ci.f:focus{background:var(--su);border-color:var(--bl);color:var(--tx);font-weight:400}

/* TOTALS ROW */
.trow td{background:var(--su2);padding:5px 6px;font-size:12px;font-weight:500;border-top:0.5px solid var(--b2);border-bottom:none;position:sticky;bottom:0;color:var(--bl)}

/* DROPDOWN — key fix: pointer-events:all, no display:none flicker */
.dd{position:fixed;background:var(--su);border:0.5px solid var(--b2);border-radius:var(--r);max-height:220px;overflow-y:auto;z-index:9999;visibility:hidden;pointer-events:none;min-width:180px}
.dd.open{visibility:visible;pointer-events:all}
.ddo{padding:7px 11px;font-size:13px;cursor:pointer;user-select:none}
.ddo:hover,.ddo.hi{background:var(--su2)}.ddo.hi{color:var(--bltx)}

/* SAVE BAR */
.savebar{display:flex;align-items:center;gap:10px;padding:9px 16px;background:var(--su);border-top:0.5px solid var(--b2);flex-shrink:0}
.sbtn{padding:6px 16px;background:var(--bl);color:#fff;border:none;border-radius:var(--r);cursor:pointer;font-size:13px;font-weight:500}
.sbtn:hover{background:#0C447C}

/* DASHBOARD */
.dash-grid{display:grid;grid-template-columns:1.4fr 1fr;gap:12px;margin-bottom:12px}
.card{background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px}
.card-h{font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.06em;margin-bottom:12px}
.hrow{display:flex;align-items:center;gap:7px;padding:5px 0;border-bottom:0.5px solid var(--b1);cursor:pointer}
.hrow:last-child{border-bottom:none}.hrow:hover{opacity:.75}
.hrow-name{flex:1;font-size:13px;font-weight:500;min-width:0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.hrow-bar-w{width:66px;height:3px;background:var(--b2);border-radius:2px;flex-shrink:0}
.hrow-bar{height:3px;border-radius:2px;background:var(--bl)}
.hrow-n{font-size:12px;color:var(--t2);width:30px;text-align:right;flex-shrink:0}
.hrow-m{font-size:11px;color:var(--t3);width:50px;text-align:right;flex-shrink:0}
.barchart{display:flex;align-items:flex-end;gap:2px;height:72px;margin-bottom:2px}
.barchart .bw{flex:1;display:flex;flex-direction:column;align-items:center;gap:0;min-width:0}
.barchart .b{width:100%;border-radius:2px 2px 0 0;min-width:0}
#map-container .leaflet-pane{z-index:1 !important}
#map-container .leaflet-top,#map-container .leaflet-bottom{z-index:2 !important}
.barchart .blbl{font-size:8px;color:var(--t3);text-align:center;line-height:1.2;margin-top:1px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;width:100%}
.chartlbls{display:flex;justify-content:space-between}
.chartlbl{font-size:10px;color:var(--t3)}
.specrow{display:flex;align-items:center;gap:8px;margin-bottom:8px}
.specrow-lbl{font-size:12px;width:68px;flex-shrink:0}
.specrow-bw{flex:1;height:5px;background:var(--b1);border-radius:3px}
.specrow-b{height:5px;border-radius:3px}
.specrow-n{font-size:12px;color:var(--t2);width:22px;text-align:right}
.avrow{display:flex;align-items:center;gap:8px;padding:4px 0;border-bottom:0.5px solid var(--b1)}
.avrow:last-child{border-bottom:none}

/* SUMMARY CARDS */
.hg{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:9px}
.hc{background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;cursor:pointer}
.hc:hover{border-color:var(--b2)}

/* TAGS */
.tag{display:inline-flex;font-size:10px;padding:2px 7px;border-radius:20px;font-weight:500}
.tb{background:var(--blbg);color:var(--bltx)}.tg{background:var(--grbg);color:var(--grtx)}
.ta{background:var(--ambg);color:var(--amtx)}.tgr{background:var(--su3);color:var(--t2)}
.m{color:var(--t2)}.fw{font-weight:500}.sh{font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.06em;margin-bottom:10px}
@media(max-width:700px){.mets,.dash-grid{grid-template-columns:1fr 1fr}}

.edit-btn{background:none;border:0.5px solid var(--b2);border-radius:20px;padding:2px 8px;font-size:11px;color:var(--t2);cursor:pointer;margin-left:5px;vertical-align:middle}
.edit-btn:hover{background:var(--su2);color:var(--tx)}
.add-item-btn{background:none;border:0.5px solid var(--bl);border-radius:20px;padding:3px 10px;font-size:11px;color:var(--bl);cursor:pointer;margin-top:8px}
.add-item-btn:hover{background:var(--blbg)}
.ef{background:var(--su2);border-radius:var(--r);padding:11px 13px;margin-top:8px}
.ef input,.ef textarea,.ef select{width:100%;padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;margin-bottom:5px;font-family:inherit;box-sizing:border-box}
.ef input:focus,.ef textarea:focus,.ef select:focus{border-color:var(--bl)}
.ef textarea{min-height:52px;resize:vertical}
.ef-g2{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:5px}
.ef-g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px;margin-bottom:5px}
.ef-btns{display:flex;gap:6px;margin-top:2px}
.ef-save{padding:5px 14px;background:var(--bl);color:#fff;border:none;border-radius:var(--r);cursor:pointer;font-size:12px;font-weight:500}
.ef-cancel{padding:5px 11px;background:transparent;border:0.5px solid var(--b2);border-radius:var(--r);cursor:pointer;font-size:12px;color:var(--t2)}
.delbtn{background:none;border:none;cursor:pointer;color:var(--t3);font-size:13px;padding:0 2px;line-height:1;flex-shrink:0}
.delbtn:hover{color:#921f1f}

#cand-panel{transform:translateX(100%);transition:transform .2s ease;pointer-events:none}
#cand-panel.open{transform:translateX(0);pointer-events:all}

/* Hospital edit mode — hide all edit controls in view mode */
.hosp-view .edit-btn { display:none !important }
.hosp-view .delbtn { display:none !important }
.hosp-view .del-btn { display:none !important }
.hosp-view .rc-del { display:none !important }
.hosp-view .site-del { display:none !important }
.hosp-view .site-add { display:none !important }
.hosp-view .del-trust { display:none !important }
.hosp-view .staff-toggle-hint { display:none !important }
.hosp-view .ef { display:none !important }
.hosp-view .staff-toggle { cursor:default !important }

/* NAV GROUPS */
.ngrp{position:relative;height:46px;display:flex;align-items:center;flex-shrink:0}
.ngrp-btn{padding:0 12px;height:46px;display:flex;align-items:center;gap:5px;font-size:13px;color:var(--t2);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap;user-select:none;border:none;background:transparent}
.ngrp-btn:hover{color:var(--tx)}
.ngrp-btn.on{color:var(--tx);border-bottom:2px solid var(--bl)}
.ngrp-btn .chev{font-size:9px;opacity:.6;transition:transform .15s}
.ngrp.open .chev{transform:rotate(180deg)}
.ngrp-drop{display:none;position:absolute;top:46px;left:0;background:var(--su);border:0.5px solid var(--b2);border-radius:var(--r);box-shadow:0 4px 16px rgba(0,0,0,.12);min-width:160px;z-index:200;padding:4px 0}
.ngrp-drop-right{left:auto;right:0}
.ngrp.open .ngrp-drop{display:block}
.ngrp-item{padding:9px 16px;font-size:13px;color:var(--t2);cursor:pointer;white-space:nowrap;display:block}
.ngrp-item:hover{background:var(--su2);color:var(--tx)}
.ngrp-item.on{color:var(--bl);font-weight:500}

/* DAY WEBSTER BRANDING */
nav{background:linear-gradient(to right,#ffffff 0%,#e8f6fb 65%,#c8e6f0 100%)!important;border-bottom:1.5px solid #d0e8f0!important;box-shadow:0 2px 8px rgba(0,0,0,.07)!important}
.ntab{color:#1a5f7a!important;font-size:12.5px!important}
.ntab:hover{color:#003087!important}
.ntab.on{color:#003087!important;border-bottom-color:#00AEEF!important;font-weight:600!important}
.ngrp-btn{color:#1a5f7a!important;font-size:12.5px!important;border:none!important;background:none!important}
.ngrp-btn:hover{color:#003087!important}
.ngrp-btn.on{color:#003087!important;border-bottom-color:#00AEEF!important;font-weight:600!important}
.ngrp-drop{background:#fff!important;border-color:#d0e8f0!important;box-shadow:0 4px 16px rgba(0,0,0,.1)!important}
.ngrp-item{color:#1a5f7a!important;font-size:13px!important}
.ngrp-item:hover{background:#f0f8fc!important;color:#003087!important}
.ngrp-item.on{color:#00AEEF!important;font-weight:600!important}
#nav-clock{color:#003087!important;font-size:18px!important;font-weight:700!important}

/* TRUST CARDS */
.trust-card{transition:box-shadow .2s,transform .2s}
.trust-card:hover{transform:translateY(-1px)}
.tc-slice{transition:flex .3s cubic-bezier(.4,0,.2,1)}
.slice-label{transition:opacity .25s}
</style>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
</head>
<body>
<nav>
<div class="brand" style="display:flex;align-items:center;gap:0;flex-shrink:0">
<svg width="210" height="44" viewBox="0 0 210 44" xmlns="http://www.w3.org/2000/svg">
<!-- Light blue circle (back-right) -->
<circle cx="30" cy="26" r="12" fill="#7ab8d4"/>
<!-- Lightest blue small circle (top-right) -->
<circle cx="33" cy="14" r="8" fill="#aad4e8"/>
<!-- Dark navy circle (front, overlaps all others) -->
<circle cx="16" cy="22" r="15" fill="#1a3a5c"/>
<!-- "Day" in grey -->
<text x="48" y="26" font-family="Arial,Helvetica,sans-serif" font-size="20" font-weight="400" fill="#555555">Day</text>
<!-- "Webster" bold darker -->
<text x="84" y="26" font-family="Arial,Helvetica,sans-serif" font-size="20" font-weight="700" fill="#333333">Webster</text>
<!-- "Group" cyan -->
<text x="149" y="37" font-family="Arial,Helvetica,sans-serif" font-size="11" font-weight="500" fill="#00AEEF" letter-spacing="0.3">Group</text>
</svg>
<span style="font-size:9px;font-weight:600;color:#888;letter-spacing:.15em;text-transform:uppercase;border-left:1px solid #ddd;padding-left:10px;margin-left:2px;white-space:nowrap">South Theatres</span>
</div>
<div style="flex:1;display:flex;justify-content:center;align-items:center;pointer-events:none">
<span id="nav-clock" style="font-size:18px;font-weight:400;font-family:'Share Tech Mono','Courier New',monospace;letter-spacing:.12em;color:#002060"></span>
</div>

<!-- Dashboard (standalone) -->
<div class="ntab on" id="tab-dashboard" onclick="gp('dashboard')">Dashboard</div>
<div class="ntab" id="tab-links" onclick="gp('links')">Quick Links</div>
<div class="ntab" id="tab-todo" onclick="gp('todo')">Tasks</div>

<!-- Bookings group -->
<div class="ngrp" id="ngrp-bookings">
<button class="ngrp-btn" id="ngrp-bookings-btn" onclick="toggleNGrp('bookings',event)">
Bookings <span class="chev">&#9660;</span>
</button>
<div class="ngrp-drop">
<div class="ngrp-item" id="tab-shifts" onclick="gp('shifts');closeNGrps()">Shift count</div>
<div class="ngrp-item" id="tab-summary" onclick="gp('summary');closeNGrps()">Weekly summary</div>
<div class="ngrp-item" id="tab-candidates" onclick="gp('candidates');closeNGrps()">Candidates</div>
<div class="ngrp-item" id="tab-hospitals" onclick="gp('hospitals');closeNGrps()">Trusts</div>
<div class="ngrp-item" id="tab-rates" onclick="gp('rates');closeNGrps()">Rates</div>
<div class="ngrp-item" id="tab-rostercheck" onclick="gp('rostercheck');closeNGrps()">Roster Check</div>
<div class="ngrp-item" id="tab-documents" onclick="gp('documents');closeNGrps()">Documents</div>
<div class="ngrp-item" id="tab-pipeline" onclick="gp('pipeline');closeNGrps()">Pipeline</div>
</div>
</div>

<!-- Payroll group -->
<div class="ngrp" id="ngrp-payroll">
<button class="ngrp-btn" id="ngrp-payroll-btn" onclick="toggleNGrp('payroll',event)">
Payroll <span class="chev">&#9660;</span>
</button>
<div class="ngrp-drop ngrp-drop-right">
<div class="ngrp-item" id="tab-timesheets" onclick="gp('timesheets');closeNGrps()">Timesheets</div>
<div class="ngrp-item" id="tab-payonly" onclick="gp('payonly');closeNGrps()">Pay Only</div>
<div class="ngrp-item" id="tab-selfbill" onclick="gp('selfbill');closeNGrps()">Self Bill</div>
<div class="ngrp-item" id="tab-placement" onclick="gp('placement');closeNGrps()">Live Placement</div>
<div class="ngrp-item" id="tab-payqueries" onclick="gp('payqueries');closeNGrps()">Pay Queries</div>
<div class="ngrp-item" id="tab-divcon" onclick="gp('divcon');closeNGrps()">Div Con</div>
</div>
</div>

</nav>
<div id="app">

<!-- DASHBOARD -->
<div class="pg on" id="pg-dashboard">
<div class="scr">
<div class="mets" style="margin-top:4px">
<div class="met"><div class="metl">Active candidates</div><div class="metv" id="dv-activecands">&#8212;</div><div class="mets2" id="dv-allcands">&#8212; total</div></div>
<div class="met"><div class="metl">Shifts this week</div><div class="metv" id="dv-wk">&#8212;</div><div class="mets2">from shift entry</div></div>
<div class="met"><div class="metl">Est. margin this wk</div><div class="metv" id="dv-mg">&#8212;</div><div class="mets2">based on PPS</div></div>
<div class="met"><div class="metl">Open queries</div><div class="metv" id="dv-openq">&#8212;</div><div class="mets2" id="dv-inprogq">&#8212;</div></div>
</div>
<div class="dash-grid">
<div class="card">
<div class="card-h">Hospital shift volume &#8212; Div Con</div>
<div id="dv-hosps"></div>
</div>
<div class="card">
<div class="card-h">Top earners</div>
<div id="dv-avail"></div>
<div class="card-h" style="margin-top:16px">Candidate mix</div>
<div id="dv-specs"></div>
</div>
</div>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
<div class="card">
<div class="card-h">Weekly shifts &#8212; full year</div>
<div class="barchart" id="dv-shchart"></div>
<div class="chartlbls" id="dv-shlbls"></div>
</div>
<div class="card">
<div class="card-h">Weekly margin &#8212; billed weeks</div>
<div class="barchart" id="dv-mgchart"></div>
<div class="chartlbls" id="dv-mglbls"></div>
</div>
</div>
</div>
</div>

<!-- SHIFTS -->
<div class="pg" id="pg-shifts">
<div style="padding:10px 16px 0;flex-shrink:0">
<div class="wkbar">
<button class="wb" onclick="chWk(-1)">&#8592; prev</button>
<button class="wb on" id="wb0" onclick="chWk(0)">This week</button>
<button class="wb" onclick="chWk(1)">next &#8594;</button>
<span class="wklbl" id="wkl"></span>
</div>
<div class="mets">
<div class="met"><div class="metl">Total shifts</div><div class="metv" id="m0">0</div><div class="mets2">this week</div></div>
<div class="met"><div class="metl">Hospitals active</div><div class="metv" id="m1">0</div><div class="mets2">with shifts</div></div>
<div class="met"><div class="metl">Candidates working</div><div class="metv" id="m2">0</div><div class="mets2">this week</div></div>
<div class="met"><div class="metl">Est. margin</div><div class="metv" id="m3">&#8212;</div><div class="mets2">based on PPS</div></div>
</div>
</div>
<div class="stw"><table class="st"><thead id="sth"></thead><tbody id="stb"></tbody><tfoot id="stf"></tfoot></table></div>

</div>

<!-- SUMMARY -->
<div class="pg" id="pg-summary">
<div style="padding:10px 16px 0;flex-shrink:0">
<div class="wkbar">
<button class="wb" onclick="chWk(-1)">&#8592; prev</button>
<button class="wb on" id="wb1" onclick="chWk(0)">This week</button>
<button class="wb" onclick="chWk(1)">next &#8594;</button>
<span class="wklbl" id="wkl2"></span>
</div>
</div>
<div class="scr"><div class="hg" id="hgrid"></div><div id="hdet"></div></div>
</div>

<!-- CANDIDATES -->
<div class="pg" id="pg-candidates">
<div class="scr">
<div style="display:flex;align-items:center;gap:9px;margin-bottom:10px;flex-wrap:wrap">
<h2 style="font-size:15px;font-weight:500">Candidates</h2>
<input type="text" id="cq" placeholder="Search&#8230;" oninput="rCands()"
style="padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);outline:none;width:190px">
<div style="display:flex;gap:5px;flex-wrap:wrap" id="cpills">
<button class="wb on" onclick="setCF('active',this)">Active</button>
<button class="wb" onclick="setCF('available',this)">Available</button>
<button class="wb" onclick="setCF('booked',this)">Booked</button>
<button class="wb" onclick="setCF('ODP',this)">ODP</button>
<button class="wb" onclick="setCF('Scrub',this)">Scrub</button>
<button class="wb" onclick="setCF('inactive',this)">Inactive</button>
<button class="wb" onclick="setCF('all',this)">All</button>
</div>
<span style="font-size:12px;color:var(--t3);margin-left:auto" id="cqc"></span>
<button class="ef-save" onclick="addNewCand()" style="padding:6px 14px;font-size:12px">+ Add candidate</button>
</div>
<div id="ctbl"></div>
</div>
</div>

<div class="pg" id="pg-hospitals">
<div class="scr">
<div id="hosp-main">
<div style="padding:40px;text-align:center;color:var(--t3)">Loading&#8230;</div>
</div>
</div>
</div>
<!-- TIMESHEETS -->
<div class="pg" id="pg-timesheets">
<div class="scr">

<!-- SESSION BAR -->
<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:11px 16px;margin-bottom:12px;display:flex;align-items:center;gap:12px;flex-wrap:wrap">
<span style="font-size:12px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Session</span>
<div style="display:flex;align-items:center;gap:6px">
<label style="font-size:12px;color:var(--t2)">Date</label>
<input id="ts-sess-date" type="date" oninput="tsDeriveDay()" onchange="tsDeriveDay()" style="padding:5px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
</div>
<div style="display:flex;align-items:center;gap:6px">
<label style="font-size:12px;color:var(--t2)">Day</label>
<input id="ts-sess-day" readonly value="" style="padding:5px 9px;border:0.5px solid var(--b1);border-radius:var(--r);background:var(--su2);color:var(--t2);font-size:12px;outline:none;width:90px">
</div>
<button onclick="tsSessToday()" style="padding:5px 12px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">Set to today</button>
<span id="ts-sess-lbl" style="font-size:12px;color:var(--t3);font-style:italic"></span>
</div>

<!-- QUICK ENTRY -->
<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:14px">
<div class="sh" style="margin-bottom:12px">Log timesheet</div>
<div style="position:relative;margin-bottom:10px">
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Candidate *</div>
<input id="ts-q" type="text" placeholder="Type to search active candidates&#8230;" oninput="tsCandSearch()" autocomplete="off" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<div id="ts-cand-drop" style="display:none;position:absolute;left:0;right:0;top:100%;background:var(--su);border:0.5px solid var(--b2);border-radius:var(--r);box-shadow:0 4px 16px rgba(0,0,0,.12);z-index:100;max-height:220px;overflow-y:auto"></div>
</div>
<div id="ts-selected-row" style="display:none;margin-bottom:10px">
<div style="display:flex;align-items:center;gap:8px;padding:7px 12px;background:var(--blbg);border-radius:var(--r)">
<span id="ts-sel-name" style="font-size:13px;font-weight:500;color:var(--bltx);flex:1"></span>
<span id="ts-sel-spec" style="font-size:11px;color:var(--t2)"></span>
<button onclick="tsClearCand()" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:18px;padding:0 2px;line-height:1">&#215;</button>
</div>
</div>
<div style="display:grid;grid-template-columns:1fr 1fr 1fr auto;gap:8px;align-items:end">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Trust</div>
<input id="ts-trust" type="text" placeholder="Auto-filled from candidate" list="ts-trust-list" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<datalist id="ts-trust-list"></datalist>
</div>
<div style="position:relative">
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Shift dates</div>
<button id="ts-dates-btn" onclick="tsToggleCal()" type="button" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--t2);font-size:13px;cursor:pointer;text-align:left;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;box-sizing:border-box">Pick dates&#8230;</button>
<input type="hidden" id="ts-dates" value="">
<div id="ts-cal" style="display:none;position:absolute;bottom:calc(100% + 6px);left:0;z-index:300;background:var(--su);border:0.5px solid var(--b2);border-radius:var(--rl);box-shadow:0 4px 20px rgba(0,0,0,.18);padding:12px;min-width:236px">
<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:8px">
<button onclick="tsCalNav(-1);event.stopPropagation()" type="button" style="background:none;border:none;cursor:pointer;font-size:14px;color:var(--t2);padding:2px 8px">&#8592;</button>
<span id="ts-cal-lbl" style="font-size:13px;font-weight:500"></span>
<button onclick="tsCalNav(1);event.stopPropagation()" type="button" style="background:none;border:none;cursor:pointer;font-size:14px;color:var(--t2);padding:2px 8px">&#8594;</button>
</div>
<div id="ts-cal-grid" style="display:grid;grid-template-columns:repeat(7,1fr);gap:2px;text-align:center"></div>
<div style="margin-top:10px;display:flex;justify-content:space-between;align-items:center;border-top:0.5px solid var(--b1);padding-top:8px">
<button onclick="tsClearDates();event.stopPropagation()" type="button" style="background:none;border:none;cursor:pointer;font-size:11px;color:var(--t3)">Clear</button>
<button onclick="tsConfirmDates();event.stopPropagation()" type="button" class="ef-save" style="padding:4px 14px;font-size:12px">Done</button>
</div>
</div>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Shifts</div>
<div style="padding:7px 9px;border:0.5px solid var(--b1);border-radius:var(--r);background:var(--su2);color:var(--t2);font-size:13px;text-align:center">
<span id="ts-shifts-lbl">&#8212;</span>
</div>
<input type="hidden" id="ts-shifts" value="0">
</div>
<button class="ef-save" onclick="addTimesheet()" style="padding:8px 18px;white-space:nowrap">+ Log</button>
</div>
<div style="font-size:11px;color:var(--t3);margin-top:7px">Date and day are taken from the session bar &#8212; set once per batch</div>
</div>

<!-- FILTERS -->
<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;flex-wrap:wrap">
<input type="text" placeholder="Search&#8230;" oninput="tsSetFilter('q',this.value)" style="padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);outline:none;font-size:12px;width:180px">
<select id="ts-trust-filter" onchange="tsSetFilter('trust',this.value)" style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<option value="">All trusts</option>
</select>
<select onchange="tsSetFilter('day',this.value)" style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<option value="">All days</option>
<option>Monday</option>
<option>Tuesday</option>
<option>Wednesday</option>
<option>Thursday</option>
<option>Friday</option>
<option>Saturday</option>
<option>Sunday</option>
</select>
<div id="ts-stats" style="margin-left:auto;font-size:12px;color:var(--t2)"></div>
</div>

<!-- TOTALS -->
<div id="ts-totals" style="display:none;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:12px 16px;margin-bottom:12px">
<div class="sh" style="margin-bottom:8px">Timesheet totals</div>
<div style="display:grid;grid-template-columns:repeat(7,1fr);gap:8px;margin-bottom:10px" id="ts-day-totals"></div>
<div style="display:flex;align-items:center;gap:16px;padding-top:8px;border-top:0.5px solid var(--b1)">
<span style="font-size:12px;color:var(--t2)">Week total: <strong id="ts-week-total">0</strong> shifts</span>
<span style="font-size:12px;color:var(--t2)">Entries: <strong id="ts-entry-count">0</strong></span>
</div>
</div>

<!-- TABLE -->
<div style="overflow-x:auto">
<table style="border-collapse:collapse;width:100%;min-width:680px">
<thead>
<tr style="border-bottom:0.5px solid var(--b2)">
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 0 7px;text-transform:uppercase;letter-spacing:.05em">Submitted</th>
<th style="text-align:center;font-size:11px;font-weight:500;color:var(--t2);padding:0 8px 7px;text-transform:uppercase;letter-spacing:.05em">Shifts</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 8px 7px;text-transform:uppercase;letter-spacing:.05em">Candidate</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 8px 7px;text-transform:uppercase;letter-spacing:.05em">Dates</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 8px 7px;text-transform:uppercase;letter-spacing:.05em">Trust</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 8px 7px;text-transform:uppercase;letter-spacing:.05em">Day</th>
<th></th>
</tr>
</thead>
<tbody id="ts-tbody">
<tr><td colspan="7" style="padding:24px;text-align:center;color:var(--t3);font-size:13px">No timesheets logged yet</td></tr>
</tbody>
</table>
</div>

</div>
</div>
<!-- RATES -->
<div class="pg" id="pg-rates">
<div class="scr">
<div style="margin-bottom:10px">
<h2 style="font-size:15px;font-weight:500">Rate cards</h2>
<p style="font-size:12px;color:var(--t2);margin-top:2px">Pay and charge rates &#8212; Day / Night / Sunday</p>
</div>
<div style="overflow-x:auto" id="rtbl"></div>
</div>
</div>

<div class="dd" id="dd"></div>

<!-- PAY ONLY -->
<div class="pg" id="pg-payonly">
<div class="scr">

<!-- LOG PAY ONLY SHIFT -->
<div id="po-form-section" style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:14px">
<div class="sh" style="margin-bottom:10px">Log pay only shift</div>

<!-- ROW 1: Candidate, Hospital, Shift date, Request date + TS attach -->
<div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr auto;gap:8px;margin-bottom:8px;align-items:end">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Candidate *</div>
<input id="po-name" type="text" placeholder="Search candidate&#8230;" list="po-name-list"
oninput="setTimeout(poOnCandChange,50)" onchange="poOnCandChange()"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<datalist id="po-name-list"></datalist>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Hospital</div>
<input id="po-hospital" type="text" placeholder="Hospital" list="po-hosp-list"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<datalist id="po-hosp-list"></datalist>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Shift date *</div>
<input id="po-date" type="date"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Request date</div>
<input id="po-reqdate" type="date"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<!-- Compact TS attach -->
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Timesheet</div>
<div id="po-ts-drop" style="border:1.5px dashed var(--b2);border-radius:var(--r);padding:6px 10px;text-align:center;cursor:pointer;min-width:90px;transition:all .15s;height:36px;display:flex;align-items:center;justify-content:center;box-sizing:border-box">
<span id="po-ts-label" style="font-size:11px;color:var(--t3)">&#128196; Attach</span>
<input type="file" id="po-ts-input" accept=".xlsx,.xls,.pdf" style="display:none">
</div>
</div>
</div>

<!-- Timesheet preview (shown after attach) -->
<div id="po-ts-preview" style="display:none;margin-bottom:8px"></div>

<!-- ROW 2: Times, Break, Hours, Pay, Charge, System, Reason + Log -->
<div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr auto;gap:8px;align-items:end">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Start</div>
<input id="po-start" type="time" oninput="poCalc()"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">End</div>
<input id="po-end" type="time" oninput="poCalc()"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Break (min)</div>
<input id="po-break" type="number" placeholder="0" oninput="poCalc()"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Hours</div>
<input id="po-hours" type="number" step="0.01" placeholder="0.00" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su2);color:var(--t2);font-size:13px;outline:none;box-sizing:border-box" readonly>
<div id="po-hours-disp" style="font-size:11px;color:var(--t3);min-height:12px;margin-top:2px"></div>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Pay rate</div>
<input id="po-payrate" type="number" step="0.01" placeholder="0.00" oninput="poCalcCharges()"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Charge rate</div>
<input id="po-chgrate" type="number" step="0.01" placeholder="0.00" oninput="poCalcCharges()"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">System</div>
<select id="po-system"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<option value="">Select</option>
<option>NHS Professionals</option>
<option>Health Roster</option>
<option>Retinue</option>
<option>ID Medical</option>
<option>Bank Partners</option>
<option>Liaison</option>
<option>Other</option>
</select>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Reason</div>
<input id="po-reason" type="text" placeholder="Reason"
style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<button class="ef-save" onclick="addPayOnly()" style="padding:8px 16px;white-space:nowrap;align-self:end">Log shift</button>
</div>

<!-- Calc display -->
<div style="display:flex;gap:14px;margin-top:8px;font-size:12px;color:var(--t2)">
<span>Total charge: <strong id="po-charge-disp" style="color:var(--bl)">--</strong></span>
<span>Margin: <strong id="po-margin-disp" style="color:var(--grtx)">--</strong></span>
<input type="hidden" id="po-hours-calc" value="">
<input type="hidden" id="po-charge" value="">
<input type="hidden" id="po-margin" value="">
</div>
</div>


<!-- EMAIL BAR -->
<div id="po-email-bar" style="display:none;align-items:center;gap:10px;background:var(--blbg);border:0.5px solid var(--bl);border-radius:var(--rl);padding:10px 16px;margin-bottom:12px">
<span style="font-size:13px;color:var(--bltx);flex:1">&#10003; Shift logged. Send pay only request email?</span>
<button onclick="poOpenEmail()" style="padding:6px 16px;background:var(--bl);color:#fff;border:none;border-radius:var(--r);cursor:pointer;font-size:13px;font-weight:500">Open email</button>
<button onclick="document.getElementById('po-email-bar').style.display='none'" style="padding:6px 10px;background:none;border:0.5px solid var(--bl);border-radius:var(--r);cursor:pointer;font-size:12px;color:var(--bltx)">Dismiss</button>
</div>

<!-- OUTSTANDING PANEL -->
<div id="po-outstanding" style="display:none;background:var(--su);border:0.5px solid var(--am);border-radius:var(--rl);padding:13px 16px;margin-bottom:12px"></div>

<!-- FILTERS + STATS -->
<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;flex-wrap:wrap">
<input type="text" placeholder="Search candidate, hospital&#8230;" oninput="poSetFilter('q',this.value)"
style="padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);outline:none;font-size:12px;width:220px">
<select id="po-hosp-filter" onchange="poSetFilter('hospital',this.value)"
style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<option value="">All hospitals</option>
</select>
<select onchange="poSetFilter('day',this.value)"
style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<option value="">All days</option>
<option>Monday</option><option>Tuesday</option><option>Wednesday</option>
<option>Thursday</option><option>Friday</option><option>Saturday</option><option>Sunday</option>
</select>
<div id="po-stats" style="margin-left:auto;display:flex;gap:16px;font-size:12px;color:var(--t2)"></div>
</div>
<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px" id="po-pages"><button id="po-clear-filter" onclick="poSetFilter('charged','')" style="display:none;padding:4px 11px;border:0.5px solid var(--am);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--amtx)">&#215; Showing outstanding only</button></div>

<!-- TABLE -->
<div style="overflow-x:auto">
<table style="border-collapse:collapse;width:100%;min-width:780px">
<thead><tr>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Date</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Candidate</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Hospital</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Day</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Times</th>
<th style="padding:4px 7px;text-align:right;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2)">Hours</th>
<th style="padding:4px 7px;text-align:right;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2)">Pay/hr</th>
<th style="padding:4px 7px;text-align:right;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2)">Charge</th>
<th style="padding:4px 7px;text-align:right;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2)">Margin</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">System</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Reason</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Requested</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:left">Date charged</th>
<th style="padding:4px 7px;font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;border-bottom:0.5px solid var(--b2);text-align:center">TS</th>
<th style="border-bottom:0.5px solid var(--b2)"></th>
</tr></thead>
<tbody id="po-tbody">
<tr><td colspan="10" style="padding:24px;text-align:center;color:var(--t3)">Loading&#8230;</td></tr>
</tbody>
</table>
</div>

</div>
</div>

<!-- ROSTER CHECK -->
<div class="pg" id="pg-rostercheck">
<div class="scr">
<div style="display:flex;align-items:center;gap:16px;margin-bottom:16px;flex-wrap:wrap">
<div>
<div class="sh">Roster Check</div>
<div style="font-size:12px;color:var(--t2);margin-top:2px" id="rc-wk-lbl"></div>
</div>
<div id="rc-summary" style="margin-left:auto;text-align:right"></div>
</div>
<div style="display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap">
<select id="rc-sys-filter" onchange="rRC()" style="padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<option value="">All systems</option>
<option value="HR">Health Roster</option>
<option value="NHSP">NHSP</option>
<option value="Retinue">Retinue</option>
<option value="ID Medical">ID Medical</option>
<option value="No System">No System</option>
</select>
<button onclick="rRC()" style="padding:6px 12px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">&#8635; Refresh</button>
</div>
<div id="rc-grid"></div>
</div>
</div>

<!-- SELF BILL -->
<div class="pg" id="pg-selfbill">
<div class="scr">

<!-- WEEK SUMMARY -->
<div id="sb-week-summary" style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:12px"></div>

<!-- DROP ZONE -->
<div id="sb-drop-zone" style="border:1.5px dashed var(--b2);border-radius:var(--rl);padding:20px 24px;margin-bottom:10px;cursor:pointer;transition:all .15s;text-align:center">
<div style="font-size:14px;font-weight:500;color:var(--t2);margin-bottom:4px">&#8681; Drop self-bill spreadsheet here</div>
<div style="font-size:12px;color:var(--t3)">Or click to browse &mdash; auto-detects columns, fuzzy-matches candidates, deduplicates</div>
<input type="file" id="sb-file-input" accept=".xlsx,.xls" style="display:none">
</div>
<div id="sb-drop-status" style="font-size:12px;color:var(--t2);margin-bottom:8px;min-height:18px"></div>

<!-- IMPORT PREVIEW -->
<div id="sb-import-preview" style="display:none;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:14px">
<div style="display:flex;align-items:center;gap:10px;margin-bottom:10px;flex-wrap:wrap">
<div class="sh">Review &amp; confirm</div>
<span id="sb-import-count" style="font-size:12px;color:var(--t2)"></span>
<div style="margin-left:auto;display:flex;gap:6px">
<button onclick="sbSelectAllImport(true)" style="padding:4px 10px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">Select all</button>
<button onclick="sbSelectAllImport(false)" style="padding:4px 10px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">Deselect all</button>
<button class="ef-save" onclick="sbConfirmImport()" style="padding:4px 16px">Import</button>
<button onclick="sbCancelImport()" style="padding:4px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>
</div>
</div>
<div id="sb-hosp-picker-wrap"></div>
<div style="overflow-x:auto;max-height:280px;overflow-y:auto;border:0.5px solid var(--b1);border-radius:var(--r)">
<table style="border-collapse:collapse;width:100%;min-width:600px">
<thead><tr style="border-bottom:0.5px solid var(--b2);background:var(--su2)">
<th style="padding:6px 8px;width:30px"></th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Candidate</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Hospital</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Shift date</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Ref</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">SB amount</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Expected</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Diff</th>
</tr></thead>
<tbody id="sb-import-tbody"></tbody>
</table>
</div>
</div>

<!-- FILTERS + STATS -->
<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;flex-wrap:wrap">
<input type="text" placeholder="Search candidate, ref&#8230;" oninput="sbSetFilter('q',this.value)"
style="padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);outline:none;font-size:12px;width:200px">
<select id="sb-hosp-filter" onchange="sbSetFilter('hospital',this.value)"
style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<option value="">All hospitals</option>
</select>
<select onchange="sbSetFilter('status',this.value)"
style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<option value="">All statuses</option>
<option value="unreconciled">Unreconciled</option>
<option value="reconciled">Reconciled</option>
<option value="queried">Queried</option>
<option value="discrepancy">Discrepancy only</option>
</select>
<div id="sb-stats" style="margin-left:auto;display:flex;gap:14px;font-size:12px;color:var(--t2);flex-wrap:wrap"></div>
</div>
<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px" id="sb-pages"></div>

<!-- TABLE -->
<div style="overflow-x:auto">
<table style="border-collapse:collapse;width:100%;min-width:800px">
<thead><tr style="border-bottom:0.5px solid var(--b2)">
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 0 7px;text-transform:uppercase;letter-spacing:.05em">SB Date</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Candidate</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Hospital</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Shift date</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Ref</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">SB amount</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Expected</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Diff</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Status</th>
<th></th>
</tr></thead>
<tbody id="sb-tbody">
<tr><td colspan="10" style="padding:24px;text-align:center;color:var(--t3)">Drop a self-bill file above to import, or use the manual form below.</td></tr>
</tbody>
</table>
</div>

<!-- MANUAL SINGLE ENTRY (collapsed by default) -->
<details style="margin-top:16px">
<summary style="font-size:12px;color:var(--t3);cursor:pointer;user-select:none;padding:8px 0">+ Log single entry manually</summary>
<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-top:8px">
<div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:8px;margin-bottom:8px">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">SB date *</div>
<input id="sb-sbdate" type="date" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Candidate *</div>
<input id="sb-cand" type="text" placeholder="Name" list="sb-cand-list" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<datalist id="sb-cand-list"></datalist>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Hospital</div>
<input id="sb-hospital" type="text" placeholder="Hospital" list="sb-hosp-list" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<datalist id="sb-hosp-list"></datalist>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Shift date</div>
<input id="sb-shiftdate" type="date" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
</div>
<div style="display:grid;grid-template-columns:1fr 1fr 1fr auto;gap:8px;align-items:end">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Reference</div>
<input id="sb-ref" type="text" placeholder="Ref number" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">SB amount (&#163;)</div>
<input id="sb-amount" type="number" step="0.01" placeholder="0.00" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Expected (&#163;)</div>
<input id="sb-expected" type="number" step="0.01" placeholder="0.00" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<button class="ef-save" onclick="addSelfBill()" style="padding:8px 18px;white-space:nowrap">+ Log</button>
</div>
</div>
</details>

</div>
</div><!-- LIVE PLACEMENT -->
<div class="pg" id="pg-placement">
<div class="scr">
<div id="lp-week-summary" style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:12px"></div>
<div id="lp-drop-zone" style="border:1.5px dashed var(--b2);border-radius:var(--rl);padding:20px 24px;margin-bottom:10px;cursor:pointer;transition:all .15s;text-align:center">
<div style="font-size:14px;font-weight:500;color:var(--t2);margin-bottom:4px">&#8681; Drop live placement spreadsheet here</div>
<div style="font-size:12px;color:var(--t3)">Or click to browse &mdash; auto-filters to South Theatres, deduplicates against existing data</div>
<input type="file" id="lp-file-input" accept=".xlsx,.xls" style="display:none">
</div>
<div style="text-align:right;margin-bottom:4px">
<button id="lp-clear-btn" onclick="lpClearData()" style="padding:3px 10px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t3)">Clear all data</button>
</div>
<div id="lp-drop-status" style="font-size:12px;color:var(--t2);margin-bottom:8px;min-height:18px"></div>
<div id="lp-import-preview" style="display:none;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:14px">
<div style="display:flex;align-items:center;gap:10px;margin-bottom:10px;flex-wrap:wrap">
<div class="sh">New shifts to import</div>
<span id="lp-import-count" style="font-size:12px;color:var(--t2)"></span>
<div style="margin-left:auto;display:flex;gap:8px">
<button class="ef-save" onclick="lpConfirmImport()" style="padding:6px 16px">Import all</button>
<button onclick="lpCancelImport()" style="padding:6px 12px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>
</div>
</div>
<div style="overflow-x:auto;max-height:280px;overflow-y:auto;border:0.5px solid var(--b1);border-radius:var(--r)">
<table style="border-collapse:collapse;width:100%;min-width:500px">
<thead><tr style="border-bottom:0.5px solid var(--b2);background:var(--su2)">
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Candidate</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Client</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Shift date</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Hours</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Charge</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:6px 8px;text-transform:uppercase;letter-spacing:.05em">Margin</th>
</tr></thead>
<tbody id="lp-import-tbody"></tbody>
</table>
</div>
</div>
<div id="lp-stats" style="display:flex;gap:16px;font-size:12px;color:var(--t2);flex-wrap:wrap;margin-bottom:14px;padding:12px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl)"></div>
<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;flex-wrap:wrap">
<button onclick="lpClearData()" style="padding:6px 12px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t3)">Clear data</button>
<input type="text" placeholder="Search candidate or client&#8230;" oninput="lpSetFilter('q',this.value)"
style="padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);outline:none;font-size:12px;width:220px">
<select id="lp-client-filter" onchange="lpSetFilter('client',this.value)"
style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;max-width:220px">
<option value="">All clients</option>
</select>
<input type="date" onchange="lpSetFilter('dateFrom',this.value)"
style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
<input type="date" onchange="lpSetFilter('dateTo',this.value)"
style="padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">
</div>
<div style="display:flex;align-items:center;gap:8px;margin-bottom:8px" id="lp-pages"></div>
<div style="overflow-x:auto;margin-bottom:16px">
<table style="border-collapse:collapse;width:100%;min-width:750px">
<thead><tr style="border-bottom:0.5px solid var(--b2)">
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 0 7px;text-transform:uppercase;letter-spacing:.05em">Shift date</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Candidate</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Client</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Consultant</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Hours</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Cost</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Charge</th>
<th style="text-align:right;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Margin</th>
<th style="text-align:left;font-size:11px;font-weight:500;color:var(--t2);padding:0 7px 7px;text-transform:uppercase;letter-spacing:.05em">Created</th>
<th></th>
</tr></thead>
<tbody id="lp-tbody">
<tr><td colspan="10" style="padding:24px;text-align:center;color:var(--t3)">Drop the live placement report above to import data.</td></tr>
</tbody>
</table>
</div>
</div>
</div>

<!-- QUICK LINKS -->
<div class="pg" id="pg-links">
<div class="scr">
<div class="sh" style="margin-bottom:16px">Quick Links</div>
<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:12px;margin-bottom:24px">

<a href="https://quickpick.daywebster.com/QuickPick2/ViewList/764" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#9889;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">Quick Pick</div>
<div style="font-size:11px;color:var(--t3)">quickpick.daywebster.com</div>
</a>

<a href="https://apps.daywebster.com/Allocate/ViewVacancies" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#128203;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">API</div>
<div style="font-size:11px;color:var(--t3)">apps.daywebster.com</div>
</a>

<a href="https://commshub.daywebster.com/Task/ChannelTasks/?channelId=bb5b6e72-1458-4bab-9cc9-b6ae8b3d41db&TaskId=13208" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#128172;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">Comms Hub</div>
<div style="font-size:11px;color:var(--t3)">commshub.daywebster.com</div>
</a>

<a href="https://supporthub.daywebster.com/Support/Index" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#127891;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">Support Hub</div>
<div style="font-size:11px;color:var(--t3)">supporthub.daywebster.com</div>
</a>

<a href="https://web.whatsapp.com/" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#128242;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">WhatsApp</div>
<div style="font-size:11px;color:var(--t3)">web.whatsapp.com</div>
</a>

<a href="https://daywebstergroup.3cx.uk/#/people" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#128222;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">3CX - Phone</div>
<div style="font-size:11px;color:var(--t3)">daywebstergroup.3cx.uk</div>
</a>

<a href="https://daywebster-my.sharepoint.com/:x:/p/scott_lane/EVITTbU0ruJEtqf7Fwxsmx4B3J2vi-3qP4ycqAcFtam6fg?e=4%3AbgEm7Q&at=9&CID=277CD118-E8F0-49A4-8D0A-6AC521F4481D&wdLOR=c8EA005A7-7054-4C60-A55A-59BAFE5BDDFF" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#128202;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">Sales Floor Shift Count</div>
<div style="font-size:11px;color:var(--t3)">daywebster.sharepoint.com</div>
</a>

</div>

<div class="sh" style="margin-bottom:16px">Booking Systems</div>
<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:12px">

<a href="https://bookings.nhsprofessionals.nhs.uk/NewLoginFrame.asp" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#127973;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">NHSP</div>
<div style="font-size:11px;color:var(--t3)">nhsprofessionals.nhs.uk</div>
</a>

<a href="https://bridgevms.i-resource.co.uk/login" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#128279;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">Bridge</div>
<div style="font-size:11px;color:var(--t3)">bridgevms.i-resource.co.uk</div>
</a>

<a href="https://e-tips.com/" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#9881;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">e-tips</div>
<div style="font-size:11px;color:var(--t3)">e-tips.com</div>
</a>

<a href="https://id-medical.skillstream.co.uk/users/sign_in" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:border-color .15s"
onmouseover="this.style.borderColor='var(--bl)'" onmouseout="this.style.borderColor='var(--b1)'">
<div style="font-size:22px">&#128084;</div>
<div style="font-size:14px;font-weight:500;color:var(--tx)">ID Medical</div>
<div style="font-size:11px;color:var(--t3)">id-medical.skillstream.co.uk</div>
</a>

<a href="https://www.google.com/maps/dir///@52.1747515,-3.3264807,172121m/data=!3m1!1e3!4m2!4m1!3e3?entry=ttu&g_ep=EgoyMDI2MDQwNi4wIKXMDSoASAFQAw%3D%3D" target="_blank"

style="display:flex;flex-direction:column;gap:6px;padding:18px 16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);text-decoration:none;transition:box-shadow .15s" onmouseover="this.style.boxShadow='0 2px 8px rgba(0,0,0,.08)'" onmouseout="this.style.boxShadow=''">
<div style="font-size:22px">&#x1F5FA;</div>
<div style="font-size:13px;font-weight:500;color:var(--tx)">Maps</div>
<div style="font-size:11px;color:var(--t3)">google.com/maps</div>
</a>

</div>
</div>
</div>


<!-- TODO PAGE -->
<div class="pg" id="pg-todo">
<div class="scr">
<div id="todo-main">
<div style="padding:40px;text-align:center;color:var(--t3)">Loading tasks&#8230;</div>
</div>
</div>
</div>

<!-- DOCUMENTS PAGE -->
<div class="pg" id="pg-documents">
<div class="scr">
<div id="docs-main">
<div style="padding:40px;text-align:center;color:var(--t3)">Loading&#8230;</div>
</div>
</div>
</div>

<!-- PAY QUERIES PAGE -->
<div class="pg" id="pg-payqueries">
<div class="scr">
<div style="display:flex;align-items:center;margin-bottom:14px">
<div class="sh" style="margin:0">Pay Queries</div>
</div>
<div id="pq-main">
<div style="padding:40px;text-align:center;color:var(--t3)">Loading&#8230;</div>
</div>
</div>
</div>

<!-- DIV CON PAGE -->
<div class="pg" id="pg-divcon">
<div class="scr">
<div id="divcon-main">
<div style="padding:40px;text-align:center;color:var(--t3)">Loading&#8230;</div>
</div>
</div>
</div>

<!-- PIPELINE PAGE -->
<div class="pg" id="pg-pipeline">
<div class="scr">
<div id="pipeline-main">
<div style="padding:40px;text-align:center;color:var(--t3)">Loading&#8230;</div>
</div>
</div>
</div>

<!-- CANDIDATE EDIT PANEL -->
<div id="cand-panel" style="position:fixed;right:0;top:46px;bottom:0;width:400px;background:var(--su);border-left:0.5px solid var(--b2);overflow-y:auto;z-index:9000;padding:20px;box-sizing:border-box">
<div style="display:flex;align-items:center;margin-bottom:16px">
<h3 id="cp-title" style="font-size:15px;font-weight:500;flex:1">Edit candidate</h3>
<button onclick="closeCandPanel()" style="background:none;border:none;cursor:pointer;font-size:20px;color:var(--t2);padding:0 4px;line-height:1">&#215;</button>
</div>
<div style="display:flex;flex-direction:column;gap:10px">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Full name *</div>
<input id="ce-n" type="text" placeholder="Full name" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Spec</div>
<div id="ce-spec-widget" style="position:relative">
<div id="ce-spec-display" onclick="ceToggleSpecDrop()" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;cursor:pointer;box-sizing:border-box;min-height:36px;display:flex;align-items:center;justify-content:space-between">
<span id="ce-spec-label" style="color:var(--t3)">Select spec(s)...</span>
<span style="font-size:10px;color:var(--t3)">&#9660;</span>
</div>
<div id="ce-spec-drop" style="display:none;position:absolute;top:100%;left:0;right:0;background:var(--su);border:0.5px solid var(--b2);border-radius:var(--r);z-index:200;box-shadow:0 4px 12px rgba(0,0,0,.1);max-height:220px;overflow-y:auto">
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="ODP" onchange="ceSpecChanged()"> ODP</label>
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="Scrub" onchange="ceSpecChanged()"> Scrub</label>
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="Recovery" onchange="ceSpecChanged()"> Recovery</label>
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="Chemo" onchange="ceSpecChanged()"> Chemo</label>
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="Anaesthetics" onchange="ceSpecChanged()"> Anaesthetics</label>
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="SFA" onchange="ceSpecChanged()"> SFA</label>
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="TSW" onchange="ceSpecChanged()"> TSW</label>
<label style="display:flex;align-items:center;gap:8px;padding:7px 10px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)" onmouseover="this.style.background='var(--su2)'" onmouseout="this.style.background=''"><input type="checkbox" value="Other" onchange="ceSpecChanged()"> Other</label>
</div>
</div>
<input id="ce-s-other" type="text" placeholder="Specify other spec..." style="display:none;margin-top:4px;width:100%;padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
<div id="ce-subspec-wrap" style="display:none;margin-top:8px">
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Scrub sub-specialties</div>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:4px">
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="General"> General</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="ENT"> ENT</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Urology"> Urology</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Plastics"> Plastics</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Major Orthopaedics"> Major Orthopaedics</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Minor Orthopaedics"> Minor Orthopaedics</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Cardiac"> Cardiac</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Ophthalmic"> Ophthalmic</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Obs &amp; Gynae"> Obs &amp; Gynae</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Breast"> Breast</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="CEPOD"> CEPOD</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="MaxFax"> MaxFax</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Dental"> Dental</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Dermatology"> Dermatology</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Neuro"> Neuro</label>
<label style="display:flex;align-items:center;gap:6px;font-size:12px;cursor:pointer"><input type="checkbox" name="ce-subspec" value="Robotics"> Robotics</label>
</div>
</div>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Activity</div>
<select id="ce-ac" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none">
<option value="Active">Active</option>
<option value="Inactive">Inactive</option>
</select>
</div>
</div>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Email</div>
<input id="ce-e" type="email" placeholder="email@example.com" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Phone</div>
<input id="ce-p" type="tel" placeholder="07xxx xxxxxx" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Main hospital</div>
<select id="ce-h" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none">
<option value="">-- select hospital --</option>
</select>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:6px;text-transform:uppercase;letter-spacing:.05em">Also works at</div>
<div id="ce-sites-list" style="max-height:160px;overflow-y:auto;border:0.5px solid var(--b2);border-radius:var(--r);padding:4px 8px;background:var(--su)">
<div style="font-size:12px;color:var(--t3);padding:4px 0">Loading sites&#8230;</div>
</div>
</div>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Area</div>
<input id="ce-a" type="text" placeholder="e.g. London, Surrey" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Min day rate (&#163;)</div>
<input id="ce-r" type="number" step="0.50" placeholder="e.g. 26.50" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box">
</div>
</div>
<div>
<div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.05em">Availability preference</div>
<select id="ce-av" style="width:100%;padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none">
<option value="">-- select --</option>
<option value="Always Free">Always Free</option>
<option value="Self Book">Self Book</option>
<option value="Ask">Ask</option>
</select>
</div>
<div style="display:flex;gap:8px;margin-top:6px;padding-top:12px;border-top:0.5px solid var(--b1)">
<button onclick="saveCandEdit(_editCandIdx)" style="flex:1;padding:9px;background:var(--bl);color:#fff;border:none;border-radius:var(--r);cursor:pointer;font-size:13px;font-weight:500">Save</button>
<button onclick="closeCandPanel()" style="padding:9px 14px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:13px;color:var(--t2)">Cancel</button>
</div>
<div id="cp-deact" style="text-align:center">
<button onclick="deactivateCand(_editCandIdx)" style="background:none;border:none;cursor:pointer;font-size:12px;color:var(--t3);text-decoration:underline">Mark as inactive</button>
</div>
</div>
</div>

<script>
var C=[{"n": "Aaron Gascon", "s": "ODP", "ac": "Active", "e": "aaron.gascon94@gmail.com", "p": "07380858288", "av": "Self Book", "h": "Luton", "a": "Bedfordshire", "r": 21.0, "st": "available", "b": ""}, {"n": "Abdelkrim Djebbour", "s": "ODP", "ac": "Inactive", "e": "kareem.djebbour@yahoo.co.uk", "p": "07852133461", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Abdul-Fatau Musah", "s": "ODP", "ac": "Active", "e": "fmusah@aol.com", "p": "07967752216", "av": "Self-Book", "h": "Luton", "a": "London", "r": 0, "st": "booked", "b": "LDH"}, {"n": "Abidemi Layo Jegede", "s": "Scrub", "ac": "Active", "e": "abyjegede@yahoo.co.uk", "p": "07943504831", "av": "Uses App", "h": "Lew/Hom", "a": "London", "r": 0, "st": "booked", "b": "Lew"}, {"n": "Abigail Ametefe", "s": "Recovery", "ac": "Inactive", "e": "baflo2001@yahoo.com", "p": "07958593018", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Abigail Machote", "s": "Scrub", "ac": "Inactive", "e": "abigailmachote@yahoo.co.uk", "p": "07747513724", "av": "", "h": "", "a": "Milton Keynes", "r": 20.0, "st": "unknown", "b": ""}, {"n": "Abiodun Mohammed", "s": "Scrub", "ac": "Inactive", "e": "abimohammed@yahoo.co.uk", "p": "07956521801", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Adanna Charity Osunta", "s": "ODP", "ac": "Inactive", "e": "charitax23@gmail.com", "p": "07908105331", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Adebukola Akintayo", "s": "ODP", "ac": "Active", "e": "adebukola.akintayo@yahoo.co.uk", "p": "07949588501", "av": "", "h": "Royal Surrey", "a": "London", "r": 0, "st": "booked", "b": "RSCH"}, {"n": "Adekanmi Ogunbufunmi", "s": "ODP", "ac": "Inactive", "e": "amuwababy@yahoo.co.uk", "p": "07972328316", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Adelaide Sackeyfio", "s": "Scrub", "ac": "Inactive", "e": "adelphil14@yahoo.com", "p": "07940906324", "av": "", "h": "Spa Medica", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Ademola Adeola", "s": "ODP", "ac": "Inactive", "e": "AdemolaAdeola@msn.com", "p": "07730484730", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Adeola Kayode", "s": "ODP", "ac": "Inactive", "e": "adeolarem@yahoo.com", "p": "07737407981", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Aisha Ramadhan", "s": "scrub", "ac": "Active", "e": "aisha.costella@yahoo.co.uk", "p": "07411135197", "av": "", "h": "Luton", "a": "", "r": 0, "st": "unknown", "b": ""}, {"n": "Aisha Costella", "s": "scrub", "ac": "Inactive", "e": "aisha.costella@yahoo.co.uk", "p": "07411 135 197", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Ajoke Fatayo", "s": "ODP", "ac": "Inactive", "e": "ajokefatayo@aol.com", "p": "07985701717", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Aleksandra Lacey", "s": "Scrub", "ac": "Active", "e": "aleksandra_fiddes@hotmail.com", "p": "07747696961", "av": "Self Book", "h": "Royal Surrey", "a": "Surrey", "r": 0, "st": "booked", "b": "RSCH"}, {"n": "Alex Amponsah", "s": "Scrub", "ac": "Active", "e": "", "p": "", "av": "Always Free", "h": "MSE", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Alex Acheampong", "s": "ODP", "ac": "Active", "e": "ca6aac@gmail.com", "p": "07702573955", "av": "Ask", "h": "MSE/Hom", "a": "London", "r": 0, "st": "booked", "b": "Med"}, {"n": "Alexio Hungwa", "s": "Scrub", "ac": "Active", "e": "lexxdefao@hotmail.co.uk", "p": "07960590884", "av": "Ask", "h": "", "a": "London", "r": 0, "st": "unavailable", "b": ""}, {"n": "Alfreda Yamoah", "s": "ODP", "ac": "Inactive", "e": "yalfreda@yahoo.com", "p": "07951350772", "av": "", "h": "", "a": "Chigwell", "r": 0, "st": "unknown", "b": ""}, {"n": "Ali Al-odat", "s": "ODP", "ac": "Inactive", "e": "amodat@hotmail.com", "p": "07899787447", "av": "", "h": "", "a": "Luton", "r": 0, "st": "unknown", "b": ""}, {"n": "Alvin Tabusares", "s": "Scrub", "ac": "Inactive", "e": "dmx_ph@yahoo.com", "p": "07887516393", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Amaka Ebele Okeke", "s": "Scrub", "ac": "Active", "e": "amaka.okeke@hotmail.com", "p": "07960469823", "av": "", "h": "", "a": "Kent", "r": 25.0, "st": "available", "b": ""}, {"n": "Amanda Maison", "s": "ODP", "ac": "Inactive", "e": "amandajanemaison@hotmail.com", "p": "07880439213", "av": "", "h": "", "a": "Milton Keynes", "r": 0, "st": "unknown", "b": ""}, {"n": "Amarachukwu Anadu", "s": "Scrub", "ac": "Inactive", "e": "acini_a@yahoo.comacini_a@yahoo.com", "p": "07723370459", "av": "", "h": "", "a": "Chertsey", "r": 0, "st": "available", "b": ""}, {"n": "Amber Asif", "s": "ODP", "ac": "Active", "e": "", "p": "", "av": "Self-Book", "h": "", "a": "", "r": 0, "st": "unknown", "b": ""}, {"n": "Amer Samson", "s": "Scrub", "ac": "Inactive", "e": "amer.samson@hotmail.co.uk", "p": "07375794448", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Aminata Cham", "s": "Scrub", "ac": "Inactive", "e": "aminatacham@gmail.com", "p": "07572442103", "av": "", "h": "", "a": "Buckinghamshire", "r": 0, "st": "unknown", "b": ""}, {"n": "Andrew P Crawford", "s": "ODP", "ac": "Active", "e": "", "p": "", "av": "", "h": "Luton", "a": "", "r": 0, "st": "unknown", "b": ""}, {"n": "Amma Asiedu-Baning", "s": "Scrub", "ac": "Active", "e": "eusiedua@myself.com", "p": "07838666000", "av": "", "h": "", "a": "Milton Keynes", "r": 24.0, "st": "unknown", "b": ""}, {"n": "Angela Ayeni", "s": "ODP", "ac": "Inactive", "e": "imoinsi@gmail.com", "p": "07443929292", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Angelo Marco Salomeo", "s": "Scrub", "ac": "Inactive", "e": "gelo_rocks1212@yahoo.com", "p": "07809717547", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Ann Noreen Trinidad", "s": "ODP", "ac": "Inactive", "e": "antrinidad2000@yahoo.com", "p": "07889887910", "av": "", "h": "", "a": "Hampshire", "r": 0, "st": "unknown", "b": ""}, {"n": "Anthea Samuels", "s": "ODP", "ac": "Inactive", "e": "theaophelia@gmail.com", "p": "07939618352", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Antony O'Toole", "s": "ODP", "ac": "Inactive", "e": "devise76@gmail.com", "p": "07572519962", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Anupama Sibin Thottathil", "s": "Recovery", "ac": "Inactive", "e": "achusibin8@gmail.com", "p": "07460850805", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Ashley Davids", "s": "Scrub", "ac": "Inactive", "e": "poekanoeks@gmail.com", "p": "07930964747", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Audrey Mudima", "s": "Scrub", "ac": "Inactive", "e": "mudimas@outlook.com", "p": "07904703757", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Augustina Akujobi", "s": "Scrub", "ac": "Active", "e": "takujobi@googlemail.com", "p": "07800931211", "av": "Always Free", "h": "Hom/Lew", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Augustina Okafor", "s": "Scrub", "ac": "Inactive", "e": "auok7@outlook.com", "p": "07984329507", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Avon Altea", "s": "TSW", "ac": "Inactive", "e": "avonaltea@gmail.com", "p": "07874730058", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Ayisha Adam", "s": "ODP", "ac": "Inactive", "e": "aisha0203@hotmail.co.uk", "p": "07985132847", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Ayokunmi Tobi Ogunleye", "s": "ODP", "ac": "Active", "e": "ayoogunleye1@gmail.com", "p": "07861479410", "av": "", "h": "", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Azam Sheikh", "s": "ODP", "ac": "Inactive", "e": "samsheikh.ast@gmail.com", "p": "07800503629", "av": "", "h": "", "a": "Northampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Babajide Fasuji", "s": "Scrub", "ac": "Active", "e": "babajidefasuji@yahoo.co.uk", "p": "07930402735", "av": "Ask", "h": "Hom/RNOH", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Beata Bartoszewicz", "s": "ODP", "ac": "Inactive", "e": "bertunia@hotmail.com", "p": "07412949321", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Beata Luchmun", "s": "ODP", "ac": "Inactive", "e": "beata_szuba84@yahoo.co.uk", "p": "07706952609", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Beatrice Adisah Yakubu", "s": "Recovery", "ac": "Inactive", "e": "bay22@hotmail.co.uk", "p": "07400322344", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Benjamin Davis", "s": "ODP", "ac": "Active", "e": "bendownunder36@hotmail.com", "p": "07517524431", "av": "", "h": "RBH", "a": "Reading", "r": 0, "st": "booked", "b": "RBH"}, {"n": "Benjamin Obaile Peters", "s": "ODP", "ac": "Inactive", "e": "bpeters@hotmail.co.uk", "p": "07881653310", "av": "", "h": "", "a": "Cambridge", "r": 0, "st": "unknown", "b": ""}, {"n": "Betty Stanly", "s": "Scrub", "ac": "Inactive", "e": "bettystanly@yahoo.co.uk", "p": "07563360734", "av": "", "h": "", "a": "Leicester", "r": 0, "st": "unknown", "b": ""}, {"n": "Bibi Nazila Caunhye", "s": "Recovery", "ac": "Inactive", "e": "caunhye04@yahoo.co.uk", "p": "07429388622", "av": "", "h": "", "a": "Uxbridge", "r": 0, "st": "unknown", "b": ""}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "ac": "Active", "e": "jugonsakilla@yahoo.com", "p": "07912758274", "av": "Uses App", "h": "Lew/Hom", "a": "London", "r": 0, "st": "booked", "b": "Lew"}, {"n": "Bimbola Oduyemi", "s": "Scrub", "ac": "Active", "e": "bimbeebee@yahoo.co.uk", "p": "07984159780", "av": "Always Free", "h": "MSE", "a": "London", "r": 25.0, "st": "booked", "b": "Lew"}, {"n": "Biren Chheda", "s": "ODP", "ac": "Inactive", "e": "bchheda@yahoo.co.uk", "p": "07825372188", "av": "", "h": "", "a": "Slough", "r": 0, "st": "unknown", "b": ""}, {"n": "Blessing Dododawa", "s": "Scrub", "ac": "Active", "e": "blessingsmith@btinternet.com", "p": "07581282371", "av": "Uses App", "h": "Lew", "a": "London", "r": 0, "st": "booked", "b": "Lew"}, {"n": "Bob Musarurwa", "s": "Scrub", "ac": "Inactive", "e": "bcutter22@hotmail.com", "p": "07412018175", "av": "", "h": "", "a": "Northampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Bridie Newton", "s": "ODP", "ac": "Inactive", "e": "bridie.newton@hotmail.co.uk", "p": "07788257423", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Buddha Gurung", "s": "ODP", "ac": "Inactive", "e": "Juniorbuds80@gmail.com", "p": "07970366904", "av": "", "h": "", "a": "Reading", "r": 0, "st": "unknown", "b": ""}, {"n": "Carl Wheat", "s": "ODP", "ac": "Active", "e": "karl14@btinternet.com", "p": "07795842575", "av": "Self-Book", "h": "Royal Surrey", "a": "Guildford", "r": 0, "st": "booked", "b": "RSCH"}, {"n": "Carla Margarida Lobato", "s": "Scrub", "ac": "Inactive", "e": "lobato.ps@gmail.com", "p": "07481915016", "av": "", "h": "", "a": "Stevenage", "r": 0, "st": "unknown", "b": ""}, {"n": "Caryn Darunday", "s": "Scrub", "ac": "Inactive", "e": "GAGIE4@YAHOO.COM", "p": "07809635981", "av": "", "h": "", "a": "", "r": 0, "st": "unknown", "b": ""}, {"n": "Chan Ganeshamoorthy", "s": "Scrub", "ac": "Active", "e": "changanesh@hotmail.com", "p": "07565446008", "av": "", "h": "", "a": "Essex", "r": 0, "st": "available", "b": ""}, {"n": "Charlotte Phillips", "s": "ODP", "ac": "Inactive", "e": "cep88@hotmail.co.uk", "p": "07475736405", "av": "", "h": "", "a": "Cardiff", "r": 0, "st": "unknown", "b": ""}, {"n": "Charmain Yvette Reis", "s": "Scrub", "ac": "Active", "e": "Charmaine.reis23@gmail.com", "p": "07830039833", "av": "", "h": "Spa", "a": "Essex", "r": 25.0, "st": "available", "b": ""}, {"n": "Charren Torralba", "s": "SFA", "ac": "Inactive", "e": "cutorralba@yahoo.co.uk", "p": "07453263880", "av": "", "h": "", "a": "Portsmouth", "r": 0, "st": "unknown", "b": ""}, {"n": "Cherry May Luz", "s": "Scrub", "ac": "Inactive", "e": "cblanquisco@yahoo.co.uk", "p": "07557535833", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Chidinma Asota", "s": "Scrub", "ac": "Inactive", "e": "mmanc3@yahoo.com", "p": "07448633156", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Chipo Kanda", "s": "Scrub", "ac": "Active", "e": "mufarokanda@yahoo.co.uk", "p": "07932694628", "av": "", "h": "", "a": "Essex", "r": 0, "st": "available", "b": ""}, {"n": "Chris Pasipanodya", "s": "ODP", "ac": "Inactive", "e": "chinoswevhu@yahoo.co.uk", "p": "07510128054", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Christine Gikurumi", "s": "Scrub", "ac": "Active", "e": "gikchristine@yahoo.com", "p": "07447913277", "av": "", "h": "East surrey", "a": "London", "r": 0, "st": "unavailable", "b": ""}, {"n": "Christine Faith mwaura", "s": "ODP", "ac": "Inactive", "e": "cfaithmwaura2@hotmail.com", "p": "07576366831", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Christopher Bwalya", "s": "ODP", "ac": "Active", "e": "xrisbwalya@yahoo.co.uk", "p": "07472645996", "av": "", "h": "Hom", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Christopher Davies", "s": "ODP", "ac": "Active", "e": "csomeone.79@gmail.com", "p": "07930413772", "av": "Self-Book", "h": "Luton", "a": "London", "r": 0, "st": "booked", "b": "LDH"}, {"n": "Comfort Raji", "s": "Scrub", "ac": "Active", "e": "kemmyraj1@yahoo.com", "p": "07944005148", "av": "Ask", "h": "Lewisham", "a": "London", "r": 24.0, "st": "available", "b": ""}, {"n": "Consuelo Johnson", "s": "ODP", "ac": "Inactive", "e": "CONIJOHNSON@HOTMAIL.CO.UK", "p": "07999875998", "av": "", "h": "", "a": "Hertfordshire", "r": 0, "st": "unknown", "b": ""}, {"n": "Damilola Fatima Satoye", "s": "ODP", "ac": "Active", "e": "damilolasatoye@yahoo.co.uk", "p": "07950651122", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Dan Aurel Gabriel Isachi", "s": "Scrub", "ac": "Inactive", "e": "Dan.Isachi@yahoo.com", "p": "07491817654", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Daniel Pakbonyan", "s": "ODP", "ac": "Active", "e": "danielpakbonyan@gmail.com", "p": "07889568687", "av": "Ask", "h": "Luton/Hom", "a": "London", "r": 0, "st": "unavailable", "b": ""}, {"n": "Daniel Simon", "s": "ODP", "ac": "Inactive", "e": "danielsimon@hotmail.co.uk", "p": "07800986730", "av": "", "h": "Barts", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "David Joy", "s": "ODP", "ac": "Active", "e": "Dave-cathy@sky.com", "p": "07804274493", "av": "Ask", "h": "Royal London", "a": "Essex", "r": 0, "st": "available", "b": ""}, {"n": "Dawn Davis", "s": "ODP", "ac": "Inactive", "e": "dee897@hotmail.com", "p": "07944171016", "av": "", "h": "", "a": "Luton", "r": 0, "st": "unknown", "b": ""}, {"n": "Dennis Duncan", "s": "ODP", "ac": "Inactive", "e": "daduncan0@gmail.com", "p": "07939192631", "av": "", "h": "", "a": "Coventry", "r": 0, "st": "unknown", "b": ""}, {"n": "Dermot Finn", "s": "ODP", "ac": "Inactive", "e": "dermotfinn50@hotmail.com", "p": "07922277500", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Derrick Asamoah", "s": "ODP", "ac": "Active", "e": "derrick.oppong76@hotmail.com", "p": "07535410227", "av": "Ask", "h": "", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Diego Sevilla", "s": "ODP", "ac": "Active", "e": "diegoportimao@gmail.com", "p": "07878918118", "av": "Ask", "h": "Luton", "a": "LDH", "r": 0, "st": "unknown", "b": ""}, {"n": "Dinah Baluyot", "s": "Scrub", "ac": "Active", "e": "", "p": "", "av": "Self-Book", "h": "Circle, RNOH", "a": "RNOH", "r": 0, "st": "unknown", "b": ""}, {"n": "Dino Milan", "s": "Scrub", "ac": "Active", "e": "deanomilan@yahoo.com", "p": "07814133804", "av": "", "h": "", "a": "London", "r": 22.0, "st": "available", "b": ""}, {"n": "Dionisio Jr Villegas Lopez", "s": "Scrub", "ac": "Inactive", "e": "jhonnny23@aol.com", "p": "07990571742", "av": "", "h": "Cromwell", "a": "Norwich", "r": 0, "st": "unknown", "b": ""}, {"n": "Diosdado B Wagan", "s": "Scrub", "ac": "Active", "e": "dbwagan@ymail.com", "p": "07540800276", "av": "Self-Book", "h": "East surrey", "a": "Surrey", "r": 0, "st": "booked", "b": "Ramsay"}, {"n": "Donette Irving-Harvey", "s": "Scrub", "ac": "Inactive", "e": "nurseddirvingharvey@yahoo.com", "p": "07393282509", "av": "", "h": "", "a": "Blackburn", "r": 0, "st": "unknown", "b": ""}, {"n": "Dorrel Nelson", "s": "Recovery", "ac": "Inactive", "e": "dorrel9@yahoo.co.uk", "p": "07723047935", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Edison Pardo Paz", "s": "Scrub", "ac": "Inactive", "e": "edisonpaz1984@yahoo.com", "p": "07414990892", "av": "", "h": "Cromwell", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Edith Obioha", "s": "Recovery", "ac": "Inactive", "e": "edithlinus@hotmail.com", "p": "07940023330", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Edward Brooks", "s": "ODP", "ac": "Active", "e": "mredwardbrooks@yahoo.co.uk", "p": "07796850775", "av": "", "h": "Bristol", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Eduard Constantin Batog", "s": "Scrub", "ac": "Active", "e": "edi.batogc@gmail.com", "p": "07821663246", "av": "Always Free", "h": "MSE, Spa Med", "a": "MSE", "r": 0, "st": "unknown", "b": ""}, {"n": "Edward Owusu-Appiah", "s": "ODP", "ac": "Active", "e": "eddy.appiah@yahoo.co.uk", "p": "07900996425", "av": "Self-Book", "h": "Homerton", "a": "London", "r": 0, "st": "booked", "b": "Hom"}, {"n": "Ellen Tottie Aguilar", "s": "Chemo", "ac": "Active", "e": "totsaguilar@yahoo.com", "p": "07411801196", "av": "", "h": "", "a": "London", "r": 0, "st": "unavailable", "b": ""}, {"n": "Elsy Babu", "s": "Scrub", "ac": "Inactive", "e": "libranelsy2005@hotmail.co.uk", "p": "07946405299", "av": "", "h": "", "a": "Bedford", "r": 0, "st": "unknown", "b": ""}, {"n": "Emilia Mugwindiri", "s": "Scrub", "ac": "Inactive", "e": "emilia.mugwindiri@yahoo.co.uk", "p": "07514995005", "av": "", "h": "", "a": "Reading", "r": 0, "st": "unknown", "b": ""}, {"n": "Emily Olukunle", "s": "ODP", "ac": "Inactive", "e": "idoreyen@yahoo.com", "p": "07760201410", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Ernest Kofi Agyei", "s": "ODP", "ac": "Inactive", "e": "kofiagyei@hotmail.co.uk", "p": "07985694772", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Ethel Ikeh", "s": "Scrub", "ac": "Active", "e": "ethyinno@yahoo.com", "p": "07908743680", "av": "Uses App", "h": "MSE/Lewisham", "a": "Essex", "r": 0, "st": "booked", "b": "Lew"}, {"n": "Ethel Mandega", "s": "Scrub", "ac": "Active", "e": "ermandega@hotmail.co.uk", "p": "07799007780", "av": "", "h": "Hom", "a": "Stevenage", "r": 0, "st": "unknown", "b": ""}, {"n": "Eugene Igwe", "s": "Scrub", "ac": "Active", "e": "eugene_igwe@yahoo.ca", "p": "07931461637", "av": "Ask", "h": "Spa", "a": "Essex", "r": 0, "st": "booked", "b": "Spa"}, {"n": "Eustacia Philbert", "s": "Scrub/Anaes", "ac": "Inactive", "e": "eustaciaphilbert@hotmail.com", "p": "07479549980", "av": "", "h": "", "a": "Hertfordshire", "r": 0, "st": "unknown", "b": ""}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "ac": "Active", "e": "evelyn.kabba@outlook.com", "p": "07951829278", "av": "Self-Book", "h": "MSE", "a": "Essex", "r": 0, "st": "booked", "b": "MSE"}, {"n": "Everjoy Sena", "s": "scrub", "ac": "Inactive", "e": "joysen@hotmail.co.uk", "p": "07958247511", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Fanol Gjata", "s": "ODP", "ac": "Active", "e": "fanolgjata@gmail.com", "p": "07769856821", "av": "Ask", "h": "Royal Surrey", "a": "Surrey", "r": 0, "st": "booked", "b": "RSCH"}, {"n": "Farzad Sajjad", "s": "ODP", "ac": "Active", "e": "farzadsajjad7@gmail.com", "p": "07507713225", "av": "Ask", "h": "", "a": "Berkshire", "r": 0, "st": "unavailable", "b": ""}, {"n": "Febin Paul", "s": "ODP", "ac": "Active", "e": "paul.febin@gmail.com", "p": "07574428290", "av": "Ask", "h": "", "a": "Kent", "r": 20.0, "st": "unknown", "b": ""}, {"n": "Ferenc Habermann", "s": "ODP", "ac": "Inactive", "e": "ferenc.habermann@gmail.com", "p": "07983450446", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Florah Mudeke", "s": "Scrub", "ac": "Active", "e": "fmudeke@yahoo.co.uk", "p": "07730349734", "av": "Self-Book", "h": "MSE", "a": "Essex", "r": 0, "st": "booked", "b": "MSE"}, {"n": "Florence Afari-obeng", "s": "Scrub", "ac": "Inactive", "e": "afariobengf@yahoo.com", "p": "07412130011", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Fortune Nyamhamba", "s": "ODP", "ac": "Inactive", "e": "fortunenyamhamba@yahoo.com", "p": "07413032279", "av": "", "h": "", "a": "Oxford", "r": 0, "st": "unknown", "b": ""}, {"n": "Frackson Banda", "s": "ODP", "ac": "Inactive", "e": "fracksonbanda@hotmail.com", "p": "07903031556", "av": "", "h": "Homerton", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Francis Lee Pedrosa", "s": "Rec/Anaes", "ac": "Inactive", "e": "vanhohenheimltd@gmail.com", "p": "07853514884", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Gareth Hughes", "s": "ODP", "ac": "Inactive", "e": "gehughes@mac.com", "p": "07791764486", "av": "", "h": "", "a": "Cardiff", "r": 0, "st": "unknown", "b": ""}, {"n": "Gary John Lovett", "s": "ODP", "ac": "Inactive", "e": "gjlovett31@gmail.com", "p": "07961566705", "av": "", "h": "", "a": "Bournemouth", "r": 0, "st": "unknown", "b": ""}, {"n": "Gemima Redd", "s": "ODP", "ac": "Inactive", "e": "redd360@me.com", "p": "07900491906", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "ac": "Active", "e": "gendia_91@yahoo.co.uk", "p": "07747847261", "av": "Ask", "h": "Homerton", "a": "Chertsey", "r": 0, "st": "unknown", "b": ""}, {"n": "George Adormeo", "s": "Recovery", "ac": "Inactive", "e": "georgeadormeo@gmail.com", "p": "07810652413", "av": "", "h": "", "a": "Watford", "r": 0, "st": "unknown", "b": ""}, {"n": "George Cobbina", "s": "TSW", "ac": "Active", "e": "cobbisco@hotmail.com", "p": "07507221980", "av": "Ask", "h": "Spa", "a": "Dartford", "r": 0, "st": "booked", "b": "Spa"}, {"n": "Georgina Elizabeth Roy", "s": "ODP", "ac": "Inactive", "e": "georgina.e.roy@gmail.com", "p": "07354826868", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Ghazaleh Dehghan", "s": "ODP", "ac": "Active", "e": "gdehghan74@gmail.com", "p": "07863823724", "av": "", "h": "", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Gina-Oana Tilvic", "s": "ODP", "ac": "Active", "e": "nice_oanita@yahoo.com", "p": "07450229164", "av": "Ask", "h": "Basildon", "a": "Essex", "r": 21.0, "st": "available", "b": ""}, {"n": "Giovanni Paolo Vinci", "s": "ODP", "ac": "Inactive", "e": "giovannivinci85@gmail.com", "p": "07454338388", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Gladys Pastore-Jones", "s": "ODP", "ac": "Inactive", "e": "pastoreg74@yahoo.co.uk", "p": "07902392039", "av": "", "h": "", "a": "Bicester", "r": 0, "st": "available", "b": ""}, {"n": "Gloria Anane-Koramah", "s": "Recovery", "ac": "Inactive", "e": "koramah2002@yahoo.co.uk", "p": "07737712026", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Gloria Kasumu", "s": "Scrub", "ac": "Inactive", "e": "gloriaeagle2011@gmail.com", "p": "07721456337", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Gloria Tawonezvi", "s": "Scrub", "ac": "Active", "e": "gloriatawonezvi@yahoo.co.uk", "p": "07874980449", "av": "", "h": "DVH", "a": "Dartford", "r": 0, "st": "available", "b": ""}, {"n": "Grace Ito Ninalga", "s": "ODP", "ac": "Inactive", "e": "grace_ninalga@outlook.com", "p": "07846006616", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Griechelle Alonzo Manginsay", "s": "Scrub", "ac": "Inactive", "e": "crayzellee@yahoo.co.uk", "p": "07725751181", "av": "", "h": "Cromwell", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Guy Stevens", "s": "ODP", "ac": "Active", "e": "nevstevens@aol.com", "p": "07861259977", "av": "Ask", "h": "", "a": "Hampshire", "r": 0, "st": "available", "b": ""}, {"n": "Haleema Ghazi", "s": "Recovery", "ac": "Inactive", "e": "haleemabano@yahoo.com", "p": "07920793702", "av": "", "h": "", "a": "Aylesbury", "r": 0, "st": "unknown", "b": ""}, {"n": "Harriet Odhiambo", "s": "Scrub", "ac": "Inactive", "e": "harriet97hartie@gmail.com", "p": "07312266770", "av": "", "h": "", "a": "Reading", "r": 0, "st": "unknown", "b": ""}, {"n": "Hayley Richardson", "s": "ODP", "ac": "Inactive", "e": "hayleyrichardson31@yahoo.co.uk", "p": "07599860581", "av": "", "h": "", "a": "Norwich", "r": 0, "st": "unknown", "b": ""}, {"n": "Hector R Pablo", "s": "Scrub", "ac": "Inactive", "e": "Ljhrp@yahoo.com", "p": "07438589668", "av": "", "h": "", "a": "Swindon", "r": 0, "st": "unknown", "b": ""}, {"n": "Hellen Wadzanayi Chipudhla", "s": "Chemo", "ac": "Inactive", "e": "h.chipudhla@sky.com", "p": "07540541996", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Hope Lucas", "s": "ODP", "ac": "Inactive", "e": "hopeluc80@gmail.com", "p": "07456577177", "av": "", "h": "", "a": "Swindon", "r": 0, "st": "unknown", "b": ""}, {"n": "Ian Ali", "s": "ODP", "ac": "Active", "e": "ian9ali@yahoo.co.uk", "p": "07800828830", "av": "Ask", "h": "Whittington", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Ian Paula Yague", "s": "Recovery", "ac": "Inactive", "e": "paulalacandula@gmail.com", "p": "07578021656", "av": "", "h": "", "a": "Milton Keynes", "r": 0, "st": "unknown", "b": ""}, {"n": "Isa Makama Muazu", "s": "ODP", "ac": "Active", "e": "muazu6@aol.com", "p": "07748770817", "av": "", "h": "Lewisham", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Ivy Ndabai", "s": "ODP", "ac": "Active", "e": "ivyndabai@gmail.com", "p": "07817793648", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Iyabo Olufunke Olaiya", "s": "ODP", "ac": "Active", "e": "unique5u@yahoo.com", "p": "07868679142", "av": "", "h": "", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Janet Balacanao", "s": "Chemo", "ac": "Active", "e": "janetbalacanao@yahoo.co.uk", "p": "07545384747", "av": "", "h": "Barts", "a": "London", "r": 30.0, "st": "booked", "b": "BHT"}, {"n": "Janet Wright", "s": "ODP", "ac": "Inactive", "e": "janet.wright5@nhs.net", "p": "07427603199", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Janine Brown-Grant", "s": "ODP", "ac": "Inactive", "e": "Janinebrown-grant@hotmail.com", "p": "07908553946", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Jasmin Khanom", "s": "TSW", "ac": "Inactive", "e": "khanomjasmin@icloud.com", "p": "07982688935", "av": "", "h": "", "a": "Luton", "r": 0, "st": "unknown", "b": ""}, {"n": "Jayson Panganiban", "s": "Scrub", "ac": "Active", "e": "maverickmen_2005@yahoo.co.uk", "p": "07530353545", "av": "Ask", "h": "", "a": "Epsom", "r": 0, "st": "unavailable", "b": ""}, {"n": "Joanna Markowska", "s": "ODP", "ac": "Inactive", "e": "asiamarkowska@yahoo.co.uk", "p": "07850168602", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "John Arthur", "s": "ODP", "ac": "Active", "e": "TEN7HSLTD@GMAIL.COM", "p": "07495918039", "av": "Always Free", "h": "Hom", "a": "Essex", "r": 21.0, "st": "available", "b": ""}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "ac": "Active", "e": "johnb.mcdonnell@hotmail.co.uk", "p": "07968393770", "av": "Ask", "h": "Spa", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Jolaade Ogunleye", "s": "Scrub", "ac": "Active", "e": "jolaade.ogunleye@yahoo.com", "p": "07735770224", "av": "Ask", "h": "", "a": "Dartford", "r": 0, "st": "unknown", "b": ""}, {"n": "Jomel Frangue", "s": "ODP", "ac": "Inactive", "e": "jomfrangue@yahoo.com", "p": "07766651225", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "ac": "Active", "e": "jonathan_montoya_2@hotmail.com", "p": "07718090762", "av": "Always Free", "h": "Barts/Spa", "a": "Dartford", "r": 0, "st": "booked", "b": "Spa"}, {"n": "Jose Gomez", "s": "ODP", "ac": "Inactive", "e": "Jose.gomez1967@outlook.com", "p": "07523456701", "av": "", "h": "", "a": "Reading", "r": 0, "st": "unknown", "b": ""}, {"n": "Josefina Bajao", "s": "Scrub", "ac": "Active", "e": "Cefinejoy@hotmail.com", "p": "07792978250", "av": "Self-Book", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Josephloid veloso", "s": "Scrub", "ac": "Active", "e": "phloid_v@yahoo.com", "p": "07870864784", "av": "Ask", "h": "Royal Surrey", "a": "London", "r": 0, "st": "booked", "b": "RSCH"}, {"n": "Josette Constance", "s": "Recovery", "ac": "Inactive", "e": "constance_josette@msn.com", "p": "07703391874", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Joshua Tanimowo", "s": "ODP", "ac": "Active", "e": "JoshuaTanimowo@gmail.com", "p": "07854909543", "av": "Self-Book", "h": "Luton", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Josiah Nyabango", "s": "Scrub", "ac": "Active", "e": "nkomo2418@gmail.com", "p": "07728987606", "av": "Always Free", "h": "MSE", "a": "Luton", "r": 0, "st": "unknown", "b": ""}, {"n": "Jovanie Santos", "s": "ODP", "ac": "Active", "e": "vaniegc@yahoo.com", "p": "07900087823", "av": "Self-Book", "h": "Ramsay/Crawley", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Joy Aitkens", "s": "Recovery", "ac": "Inactive", "e": "ajony@hotmail.co.uk", "p": "07949414270", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Joy Chinedu Ossai", "s": "Scrub", "ac": "Inactive", "e": "ossaij944@gmail.com", "p": "07852525263", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Star Samuel", "s": "Scrub", "ac": "Active", "e": "prophetess1434@gmail.com", "p": "07307384442", "av": "", "h": "", "a": "London", "r": 0, "st": "booked", "b": "Med"}, {"n": "Kaif Rashid", "s": "ODP", "ac": "Active", "e": "kaif_18@hotmail.co.uk", "p": "07437607119", "av": "Self-Book", "h": "Royal Surrey", "a": "Burnley", "r": 0, "st": "unknown", "b": ""}, {"n": "Karen Agbuya", "s": "Recovery", "ac": "Active", "e": "k.a.sept@hotmail.com", "p": "07901165453", "av": "Self-Book", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Karen Nuala Vaughan", "s": "ODP", "ac": "Inactive", "e": "Vaughk9@gmail.com", "p": "07930633660", "av": "", "h": "", "a": "East Sussex", "r": 0, "st": "unknown", "b": ""}, {"n": "Katie Wilson", "s": "ODP", "ac": "Inactive", "e": "katiew373@gmail.com", "p": "07814235869", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Kelly Marie Peel", "s": "Scrub", "ac": "Inactive", "e": "kellysmith203@hotmail.com", "p": "07858719180", "av": "", "h": "", "a": "Reading", "r": 0, "st": "unknown", "b": ""}, {"n": "Kerlene Cuffie-Paul", "s": "ODP", "ac": "Active", "e": "kcpperiopltd@gmail.com", "p": "07447653611", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Kiran Sharma", "s": "Scrub", "ac": "Active", "e": "coconut6989@yahoo.co.uk", "p": "07889218745", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Kudakwashe Makoni", "s": "ODP", "ac": "Inactive", "e": "monalisamak@gmail.com", "p": "07462943413", "av": "", "h": "", "a": "Uxbridge", "r": 0, "st": "unknown", "b": ""}, {"n": "Kumi Agbesi", "s": "ODP", "ac": "Inactive", "e": "up642041@gmail.com", "p": "07557783069", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "lana vaughan", "s": "Scrub", "ac": "Inactive", "e": "lanavaughan@hotmail.co.uk", "p": "07545334344", "av": "", "h": "", "a": "Reading", "r": 0, "st": "unknown", "b": ""}, {"n": "Laura Pembele", "s": "ODP", "ac": "Inactive", "e": "laura.oni@hotmail.com", "p": "07957003136", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Lauren Amy Orgar", "s": "ODP", "ac": "Active", "e": "laurenorgar@gmail.com", "p": "07881803498", "av": "", "h": "Royal Berkshire", "a": "Surrey", "r": 0, "st": "unavailable", "b": ""}, {"n": "Lavert Banza", "s": "ODP", "ac": "Inactive", "e": "tre2168@gmail.com", "p": "07446261476", "av": "", "h": "", "a": "Dartford", "r": 0, "st": "unknown", "b": ""}, {"n": "Leah Namerae Saoli", "s": "Scrub", "ac": "Inactive", "e": "leahsaoli@gmail.com", "p": "07594596911", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Lena O'Leary", "s": "Scrub", "ac": "Active", "e": "lenaoleary12@gmail.com", "p": "07890574789", "av": "Ask", "h": "Spa", "a": "Essex", "r": 0, "st": "booked", "b": "Optegra"}, {"n": "Leonida Untalan White", "s": "Scrub", "ac": "Active", "e": "lizawhiteuk@yahoo.com", "p": "07765252124", "av": "Always Free", "h": "Spa", "a": "Oxford", "r": 0, "st": "unknown", "b": ""}, {"n": "Liberty Galin", "s": "Scrub", "ac": "Inactive", "e": "liberty_maala@yahoo.com", "p": "07795482899", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Librada Tagelo", "s": "Scrub", "ac": "Active", "e": "ltagelo@yahoo.co.uk", "p": "07377634193", "av": "Ask", "h": "Homerton", "a": "Watford", "r": 0, "st": "available", "b": ""}, {"n": "Lioniza D'Apresentacao Mayola", "s": "ODP", "ac": "Inactive", "e": "lioniza.mayola@gmail.com", "p": "07556537011", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Lisa Schembri", "s": "ODP", "ac": "Inactive", "e": "Lisa.marie7@hotmail.co.uk", "p": "07855217413", "av": "", "h": "", "a": "West Sussex", "r": 0, "st": "unknown", "b": ""}, {"n": "Lorraine Marie Tumbos", "s": "Scrub", "ac": "Inactive", "e": "LorraineMarieTumbos@yahoo.com", "p": "07464752000", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Louisa Boateng", "s": "Scrub", "ac": "Inactive", "e": "Louboateng@gmail.com", "p": "07477654840", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Lovie Pascual", "s": "ODP", "ac": "Active", "e": "loviebisain@yahoo.com", "p": "07955291884", "av": "", "h": "Royal Surrey", "a": "Surrey", "r": 0, "st": "booked", "b": "RSCH"}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "ac": "Active", "e": "Imperialcollege95@yahoo.com", "p": "07946871917", "av": "", "h": "Spa", "a": "London", "r": 0, "st": "booked", "b": "BRI"}, {"n": "Lyn Hamu Chiwenga", "s": "ODP", "ac": "Active", "e": "Lyncwen@yahoo.co.uk", "p": "07716214213", "av": "Self-Book", "h": "", "a": "London", "r": 20.0, "st": "available", "b": ""}, {"n": "Ma Therese Say", "s": "Scrub", "ac": "Active", "e": "mariatheresesay@gmail.com", "p": "07472365594", "av": "Ask", "h": "", "a": "Essex", "r": 20.0, "st": "available", "b": ""}, {"n": "Machona Nyoni", "s": "ODP", "ac": "Active", "e": "machonanyoni@yahoo.co.uk", "p": "07931217546", "av": "Ask", "h": "", "a": "London", "r": 23.0, "st": "available", "b": ""}, {"n": "Magdalene F Webb", "s": "ODP", "ac": "Active", "e": "maggie.stjames@outlook.com", "p": "07572904208", "av": "", "h": "St Richards", "a": "Sussex", "r": 0, "st": "available", "b": ""}, {"n": "Mahir Ahmed", "s": "ODP", "ac": "Active", "e": "mahir.19ahmed@gmail.com", "p": "07956132267", "av": "Always Free", "h": "Hom/Watford", "a": "London", "r": 0, "st": "booked", "b": "WGH"}, {"n": "Malcolm Orr", "s": "ODP", "ac": "Inactive", "e": "mal.orr@hotmail.com", "p": "07714101479", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Manuel Rodriguez", "s": "Scrub", "ac": "Active", "e": "manuelrcmrodriguezjr@gmail.com", "p": "07576316861", "av": "Ask", "h": "Ramsay Rivers", "a": "London", "r": 0, "st": "unavailable", "b": ""}, {"n": "Marcheous Gustilo", "s": "Scrub", "ac": "Inactive", "e": "marcheousg@gmail.com", "p": "07858505844", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Margaret Cas", "s": "Recovery", "ac": "Inactive", "e": "margiecasph@yahoo.com", "p": "07786327397", "av": "", "h": "", "a": "Peterborough", "r": 0, "st": "unknown", "b": ""}, {"n": "Margareth Landicho", "s": "Scrub", "ac": "Inactive", "e": "m.blandicho@yahoo.com", "p": "07880950473", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Maria Fuentes", "s": "Scrub", "ac": "Inactive", "e": "guiamalinit@yahoo.com", "p": "07886043576", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Maria Corazon Castro", "s": "Scrub", "ac": "Inactive", "e": "castrom_68@yahoo.co.uk", "p": "07738477163", "av": "", "h": "", "a": "Portsmouth", "r": 0, "st": "unknown", "b": ""}, {"n": "Maria Roslyn Beckford", "s": "Scrub", "ac": "Inactive", "e": "maria.r.beckford@gmail.com", "p": "07398781995", "av": "", "h": "", "a": "Telford", "r": 0, "st": "unknown", "b": ""}, {"n": "Marian Tolulope Gbadamosi", "s": "ODP", "ac": "Inactive", "e": "tolugb@gmail.com", "p": "07818435130", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Mariana Claudia Gherghe", "s": "Scrub", "ac": "Inactive", "e": "claugherghe@yahoo.co.uk", "p": "07929160566", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Marichelle Alvarez", "s": "Scrub", "ac": "Inactive", "e": "marilogarta@yahoo.com", "p": "07745745179", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Marielle Alexandria Diwata", "s": "Scrub", "ac": "Inactive", "e": "lhexydiwata1311@gmail.com", "p": "07450587452", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Marius Mihai Vlad", "s": "ODP", "ac": "Inactive", "e": "Marrius@btinternet.com", "p": "07900041857", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Mark Angelo De Jesus", "s": "Scrub", "ac": "Active", "e": "Mark.85@outlook.com", "p": "07852283255", "av": "Ask", "h": "", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Mark Anthony Pablico", "s": "Scrub", "ac": "Inactive", "e": "jehmasp_02@yahoo.com.ph", "p": "07462330800", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Mark Cyril Salo", "s": "Scrub", "ac": "Inactive", "e": "mcpsalo@hotmail.com", "p": "07473454422", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Mark Robert Shea", "s": "ODP", "ac": "Active", "e": "markshea2003@yahoo.co.uk", "p": "07595353157", "av": "", "h": "", "a": "Reading", "r": 0, "st": "available", "b": ""}, {"n": "Marlon Orio", "s": "ODP", "ac": "Active", "e": "marlon_orio@yahoo.co.uk", "p": "07732240493", "av": "Self-Book", "h": "East Surrey", "a": "London", "r": 0, "st": "booked", "b": "ESH"}, {"n": "Martin Glean", "s": "ODP", "ac": "Inactive", "e": "martinglean@yahoo.com", "p": "07776041357", "av": "", "h": "", "a": "Yorkshire", "r": 0, "st": "unknown", "b": ""}, {"n": "Martin Makungu", "s": "ODP", "ac": "Inactive", "e": "kobomart@yahoo.co.uk", "p": "07595483701", "av": "", "h": "", "a": "Oldhsam", "r": 0, "st": "unknown", "b": ""}, {"n": "Martin Rowan", "s": "ODP", "ac": "Active", "e": "bezzym369@gmail.com", "p": "07981852124", "av": "", "h": "Royal Berkshire", "a": "Surrey", "r": 25.0, "st": "booked", "b": "RBH"}, {"n": "Martine Howard", "s": "ODP", "ac": "Inactive", "e": "Martinehoward@hotmail.com", "p": "07496782228", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Mary Daisy Ezekiel", "s": "Scrub", "ac": "Inactive", "e": "mezekiel87@gmail.com", "p": "07903895626", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Maryleen Mahike", "s": "ODP", "ac": "Active", "e": "mahike1@msn.com", "p": "07808861917", "av": "", "h": "", "a": "Milton Keynes", "r": 0, "st": "unknown", "b": ""}, {"n": "Matirasa Taruvinga", "s": "Recovery", "ac": "Inactive", "e": "mattitaruvinga@gmail.com", "p": "07850690869", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Matthew Olusegun Awe", "s": "ODP", "ac": "Inactive", "e": "mattlag2000@yahoo.co.uk", "p": "07538677913", "av": "", "h": "", "a": "Bedford", "r": 0, "st": "unknown", "b": ""}, {"n": "Maudy Hoyi", "s": "ODP", "ac": "Active", "e": "maudnya@yahoo.com", "p": "07877650049", "av": "Ask", "h": "Ramsay", "a": "Essex", "r": 0, "st": "booked", "b": "Ramsay"}, {"n": "Michelle Lim", "s": "Scrub", "ac": "Active", "e": "maelim2003@outlook.com", "p": "07825987518", "av": "", "h": "Cromwell", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Maureen Chukwuma", "s": "Recovery", "ac": "Active", "e": "onsofor@yahoo.com", "p": "07727190760", "av": "Uses App", "h": "Lewisham", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Maxmore Nyazema", "s": "Recovery", "ac": "Active", "e": "Maxzolla@yahoo.com", "p": "07878119756", "av": "Uses App", "h": "Lewisham", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Mehmet Remzi", "s": "ODP", "ac": "Inactive", "e": "mremzi1@hotmail.com", "p": "07776198319", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Melania Cosmina Motorca", "s": "Cath Lab", "ac": "Inactive", "e": "mel.motorca@yahoo.com", "p": "07879305180", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Melody Mamire", "s": "Scrub", "ac": "Active", "e": "melotakaz@yahoo.co.uk", "p": "07944698163", "av": "Self-Book", "h": "MSE", "a": "Essex", "r": 0, "st": "booked", "b": "MSE"}, {"n": "Melrick Rasquinha", "s": "ODP", "ac": "Inactive", "e": "melrickchrisel@yahoo.co.uk", "p": "07415746531", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Meltrin Ferrer Castaneda", "s": "Scrub", "ac": "Active", "e": "sweetymel73@yahoo.com", "p": "07595157127", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Mercy Afolabi", "s": "Scrub", "ac": "Active", "e": "mercy_afolabi@yahoo.co.uk", "p": "07879559691", "av": "Ask", "h": "QEH", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Michelle Chewter", "s": "ODP", "ac": "Inactive", "e": "mchewter@hotmail.com", "p": "07980767758", "av": "", "h": "", "a": "Weston-Super-Mare", "r": 0, "st": "unknown", "b": ""}, {"n": "Mirela Florineta Gocsman", "s": "Scrub", "ac": "Inactive", "e": "alcrimimi@yahoo.it", "p": "07756668153", "av": "", "h": "", "a": "Bedford", "r": 0, "st": "unknown", "b": ""}, {"n": "Miren Ribera-Edwards", "s": "Scrub", "ac": "Inactive", "e": "anxone@blueyonder.co.uk", "p": "07906689654", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Mitchell Balogun", "s": "Scrub", "ac": "Active", "e": "mishie_balogun@yahoo.co.uk", "p": "07939201401", "av": "", "h": "SABP", "a": "Berkshire", "r": 25.0, "st": "booked", "b": "SABP"}, {"n": "CHRISTINAH XABANISA", "s": "Recovery", "ac": "Inactive", "e": "Xabanisa@icloud.com", "p": "07405903781", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Mohamed Zulfihar Amanulla", "s": "ODP", "ac": "Inactive", "e": "Zulfihar.amanulla@yahoo.com", "p": "07827335543", "av": "", "h": "", "a": "London", "r": 22.0, "st": "unknown", "b": ""}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "ac": "Active", "e": "m.mohammad57@yahoo.co.uk", "p": "07851646706", "av": "Self-Book", "h": "Luton", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Monsurat Bolanle Raji", "s": "Scrub", "ac": "Inactive", "e": "bodejiba@hotmail.com", "p": "07949128489", "av": "", "h": "", "a": "Dartford", "r": 0, "st": "unknown", "b": ""}, {"n": "Moses Olufunwa", "s": "ODP", "ac": "Active", "e": "moviccare@gmail.com", "p": "07841028330", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Moses Chika Megwaonye", "s": "ODP", "ac": "Active", "e": "rave4h@yahoo.com", "p": "07939426133", "av": "", "h": "Whipps Cross", "a": "London", "r": 25.0, "st": "booked", "b": "QVH"}, {"n": "Munashe Blessing Mhembere", "s": "ODP", "ac": "Inactive", "e": "munashemhembere@yahoo.co.uk", "p": "07988036931", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Myla Rose Borromeo", "s": "Recovery", "ac": "Inactive", "e": "alymrose24@gmail.com", "p": "07481953027", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Myles J Roberts", "s": "ODP", "ac": "Inactive", "e": "mylesr1906@hotmail.co.uk", "p": "07455328433", "av": "", "h": "", "a": "Cornwall", "r": 0, "st": "unknown", "b": ""}, {"n": "Natasha Riaz", "s": "Scrub", "ac": "Inactive", "e": "natasha.riaz@yahoo.co.uk", "p": "07412915146", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Ndanatsei Madilaya", "s": "Scrub", "ac": "Active", "e": "ndana823@gmail.com", "p": "07940420020", "av": "", "h": "St Richards", "a": "Berkshire", "r": 0, "st": "booked", "b": "StRichards"}, {"n": "Ndidi Catherine Onyeama", "s": "Pre Assess", "ac": "Active", "e": "kathryn_dsca@yahoo.com", "p": "07733756342", "av": "", "h": "", "a": "Dartford", "r": 0, "st": "booked", "b": "Spa"}, {"n": "Neal Fletcher", "s": "ODP", "ac": "Inactive", "e": "nealfletcher1970@gmail.com", "p": "07377368336", "av": "", "h": "", "a": "Northampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Nelson Kaguda", "s": "ODP", "ac": "Inactive", "e": "nkaguda@gmail.com", "p": "07931310362", "av": "", "h": "", "a": "Bedford", "r": 23.0, "st": "available", "b": ""}, {"n": "Onias Mupfacha", "s": "ODP", "ac": "Inactive", "e": "oniasmupfacha@yahoo.co.uk", "p": "07545283607", "av": "", "h": "", "a": "Northampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Nicola Sundercombe", "s": "Scrub", "ac": "Inactive", "e": "nicolagladwell@hotmail.co.uk", "p": "07805049272", "av": "", "h": "", "a": "Southampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Nicole Corbin", "s": "ODP", "ac": "Inactive", "e": "sn904@yahoo.co.uk", "p": "07949104826", "av": "", "h": "", "a": "Luton", "r": 0, "st": "unknown", "b": ""}, {"n": "Nicole Reyes", "s": "ODP", "ac": "Active", "e": "nicoleseyer1@icloud.com", "p": "07738657075", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Nonhlanhla Edelfrieda Khuzwayo", "s": "Recovery", "ac": "Inactive", "e": "nonhlanhlakhuzwayo@yahoo.com", "p": "07769694213", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Novlette Panton", "s": "Scrub", "ac": "Active", "e": "novlettepanton1@hotmail.co.uk", "p": "07999963811", "av": "", "h": "Lew", "a": "Essex", "r": 0, "st": "available", "b": ""}, {"n": "Nyasha Jena", "s": "Scrub", "ac": "Active", "e": "nyashajenna@aol.com", "p": "07786273387", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "booked", "b": "SABP"}, {"n": "Obianuju Stella Okoroafor", "s": "Scrub", "ac": "Active", "e": "uju.aniakor@yahoo.com", "p": "07788276989", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Obinna Valentine Ogbankwa", "s": "Scrub", "ac": "Inactive", "e": "ogbankwa1@yahoo.co.uk", "p": "07411454698", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Odette Nicholson", "s": "Recovery", "ac": "Inactive", "e": "nickyboo2cutie@gmail.com", "p": "07578457664", "av": "", "h": "", "a": "Wolverhampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Esther Adigun", "s": "Scrub", "ac": "Active", "e": "egbekobartokunbo@yahoo.com", "p": "07798683515", "av": "", "h": "St Richards", "a": "Surrey", "r": 0, "st": "available", "b": ""}, {"n": "Olatunji Isaiah Olaleye", "s": "ODP", "ac": "Inactive", "e": "tunjileye02@gmail.com", "p": "07424669193", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Oliver Okoro Nnabugwu", "s": "Recovery", "ac": "Active", "e": "olivernnabugwu@yahoo.co.uk", "p": "07574014764", "av": "", "h": "", "a": "Lodnon", "r": 0, "st": "unknown", "b": ""}, {"n": "Sunday Olaniyan", "s": "ODP", "ac": "Active", "e": "busayolaniyan@yahoo.com", "p": "07538926564", "av": "", "h": "Lew", "a": "London", "r": 0, "st": "booked", "b": "LEW"}, {"n": "Olutoyin Latinwo", "s": "Scrub", "ac": "Active", "e": "Toylat54@yahoo.com", "p": "07889431412", "av": "", "h": "Lew", "a": "Surrey", "r": 21.0, "st": "booked", "b": "Lew"}, {"n": "Oluwamayowa Fabunmi", "s": "ODP", "ac": "Active", "e": "dmaolyn@gmail.com", "p": "07943730364", "av": "Ask", "h": "", "a": "Essex", "r": 0, "st": "available", "b": ""}, {"n": "Oluwatoyin Emmanuel", "s": "Scrub", "ac": "Active", "e": "toyinemmanuel@ymail.com", "p": "07939215431", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Oluwatoyin Akinnawo", "s": "Scrub", "ac": "Inactive", "e": "takinnawo@gmail.com", "p": "07961518264", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Omolara Ogunmola", "s": "ODP", "ac": "Inactive", "e": "ogunmolaomolara@yahoo.co.uk", "p": "07882100959", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "ac": "Active", "e": "paiviraulamo@gmail.com", "p": "07380313808", "av": "", "h": "East Surrey", "a": "London", "r": 25.0, "st": "unknown", "b": ""}, {"n": "Pamela Hore", "s": "ODP", "ac": "Inactive", "e": "Pamelafarai@yahoo.Co.uk", "p": "07853327988", "av": "", "h": "", "a": "Reading", "r": 0, "st": "unknown", "b": ""}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "ac": "Active", "e": "pamncubee@gmail.com", "p": "07900178195", "av": "Ask", "h": "RBH", "a": "Birmingham", "r": 0, "st": "booked", "b": "RBH"}, {"n": "Parmanan Pagoo", "s": "ODP", "ac": "Active", "e": "p_pagoo@yahoo.co.uk", "p": "07944092183", "av": "", "h": "", "a": "Uxbridge", "r": 0, "st": "unavailable", "b": ""}, {"n": "Parveen Kumar Nehra", "s": "Scrub", "ac": "Inactive", "e": "pknehra_ciis@yahoo.co.in", "p": "07411413582", "av": "", "h": "", "a": "Southampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Patrick Adutwim", "s": "ODP", "ac": "Active", "e": "patadu1977@gmail.com", "p": "07852202296", "av": "Self-Book", "h": "Homerton", "a": "London", "r": 0, "st": "booked", "b": "Hom"}, {"n": "Patrick Gambold", "s": "ODP", "ac": "Inactive", "e": "pknehra_ciis@yahoo.co.in", "p": "07411413582", "av": "", "h": "", "a": "Wiltshire", "r": 0, "st": "unknown", "b": ""}, {"n": "Patrick Mitchell", "s": "ODP", "ac": "Active", "e": "", "p": "", "av": "", "h": "", "a": "", "r": 0, "st": "booked", "b": "QVH"}, {"n": "Patrick Mitchell", "s": "ODP", "ac": "Active", "e": "salestvc@hotmail.co.uk", "p": "07958928802", "av": "Self-Book", "h": "QVH", "a": "Surrey", "r": 0, "st": "booked", "b": "QVH"}, {"n": "Paul Harris", "s": "ODP", "ac": "Inactive", "e": "abcodp@gmail.com", "p": "07940008230", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Paul O Keeffe", "s": "ODP", "ac": "Inactive", "e": "okeeffe42@gmail.com", "p": "07853806135", "av": "", "h": "", "a": "Bedford", "r": 0, "st": "unknown", "b": ""}, {"n": "Paula Ibanez Ballester", "s": "Scrub", "ac": "Active", "e": "paula.iballester@gmail.com", "p": "07932911488", "av": "Ask", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Paulo Sabo", "s": "Chemo", "ac": "Active", "e": "paulo_sabo@yahoo.com", "p": "07789078266", "av": "", "h": "Jersey", "a": "Southampton", "r": 0, "st": "booked", "b": "SGH"}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "ac": "Active", "e": "spongychaN@yahoo.co.uk", "p": "07988901205", "av": "", "h": "Optegra", "a": "Barking", "r": 0, "st": "unknown", "b": ""}, {"n": "Penelope Piccio", "s": "ODP", "ac": "Active", "e": "pennypiccio@yahoo.co.uk", "p": "07701087772", "av": "", "h": "", "a": "Berkshire", "r": 0, "st": "booked", "b": "CIR"}, {"n": "Peter Gilbert", "s": "ODP", "ac": "Inactive", "e": "PG.theheap@yahoo.co.uk", "p": "07808223111", "av": "", "h": "", "a": "Cumbria", "r": 0, "st": "unknown", "b": ""}, {"n": "Peter West", "s": "ODP", "ac": "Inactive", "e": "peterwest1@tiscali.co.uk", "p": "07931979684", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Petru Bogdan Malanciuc", "s": "Scrub", "ac": "Inactive", "e": "malanciucpetrub@yahoo.com", "p": "07459509509", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Philip Dapaah", "s": "ODP", "ac": "Inactive", "e": "dapphl@sky.com", "p": "07932675850", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Philip White", "s": "ODP", "ac": "Inactive", "e": "philipawhite@me.com", "p": "07740644505", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Phillip Mwaijumba", "s": "Scrub", "ac": "Active", "e": "mwaijumba@yahoo.co.uk", "p": "07748065030", "av": "Self-Book", "h": "MSE", "a": "Essex", "r": 20.0, "st": "booked", "b": "MSE"}, {"n": "Phillip Cabanero Maravilla", "s": "ODP", "ac": "Inactive", "e": "phillip_qm@yahoo.com", "p": "07463293657", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Raheela Ashraf", "s": "Scrub", "ac": "Active", "e": "Nrramp@yahoo.com", "p": "07908409120", "av": "Ask", "h": "Royal London", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Rainier Jr. Santiago", "s": "Scrub", "ac": "Active", "e": "rainiermsantiagojrbetelgeuse@yahoo.com", "p": "07402304550", "av": "Ask", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Rajni Nawah", "s": "Recovery", "ac": "Inactive", "e": "nawahrajni@yahoo.co.uk", "p": "07808065020", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Rayven-Renee Arboine", "s": "ODP", "ac": "Active", "e": "rayvenarboine@hotmail.co.uk", "p": "07711185048", "av": "", "h": "Homerton", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Rebecca O'Reilly", "s": "Scrub", "ac": "Inactive", "e": "beckydoodah@hotmail.co.uk", "p": "07597743428", "av": "", "h": "", "a": "Portsmouth", "r": 0, "st": "unknown", "b": ""}, {"n": "Rebecca Shields", "s": "Scrub", "ac": "Inactive", "e": "bekr2008@hotmail.com", "p": "07427779712", "av": "", "h": "", "a": "Birmingham", "r": 0, "st": "unknown", "b": ""}, {"n": "Reeni Mathew", "s": "Scrub", "ac": "Inactive", "e": "mathewreeni@yahoo.com", "p": "07730262153", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Rehana Ijaz", "s": "Scrub", "ac": "Inactive", "e": "rehanadaniel@hotmail.com", "p": "07737805470", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Renitta Manyukile", "s": "Scrub", "ac": "Inactive", "e": "renniemanyux@gmail.com", "p": "07768693865", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Rhita Berempya-Nambago", "s": "Recovery", "ac": "Inactive", "e": "rberempya@gmail.com", "p": "07539839921", "av": "", "h": "", "a": "Dartford", "r": 0, "st": "unknown", "b": ""}, {"n": "Ricardo Miguel Pinto Loureiro", "s": "Scrub", "ac": "Inactive", "e": "ricardo_mlp@hotmail.com", "p": "07759178340", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Richard Gairy", "s": "ODP", "ac": "Inactive", "e": "rgairy@gmail.com", "p": "07704807419", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Rikki Aherne", "s": "ODP", "ac": "Inactive", "e": "rikkiwanless@hotmail.com", "p": "07964753566", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Rinah Bheekharry", "s": "SFA", "ac": "Active", "e": "m_ag@hotmail.co.uk", "p": "07877827209", "av": "Self-Book", "h": "Ramsay", "a": "Aylesbury", "r": 0, "st": "booked", "b": "Ramsay"}, {"n": "Robert Maskell", "s": "ODP", "ac": "Active", "e": "marirob21@hotmail.co.uk", "p": "07969444574", "av": "", "h": "", "a": "Great Yarmouth", "r": 20.0, "st": "unknown", "b": ""}, {"n": "Robyn Callaghan", "s": "Scrub", "ac": "Inactive", "e": "robyn.m.taylor@outlook.com", "p": "07969444412", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Rodrick Chirimarara", "s": "ODP", "ac": "Inactive", "e": "chirimararar@gmail.com", "p": "07428554743", "av": "", "h": "", "a": "Watford", "r": 0, "st": "unknown", "b": ""}, {"n": "Rogelio Banzon", "s": "Scrub", "ac": "Inactive", "e": "rcbanzonjr@hotmail.com", "p": "07794578361", "av": "", "h": "", "a": "Oxford", "r": 0, "st": "unknown", "b": ""}, {"n": "Ronan Perez", "s": "ODP", "ac": "Active", "e": "ronanperez@yahoo.com", "p": "07919108347", "av": "", "h": "Royal Surrey", "a": "Basingstoke", "r": 0, "st": "unknown", "b": ""}, {"n": "Rose Onyendoro", "s": "ODP", "ac": "Active", "e": "rose.onyendoro75@gmail.com", "p": "07951441938", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Roseline Emmanuel", "s": "Scrub", "ac": "Active", "e": "Rose.emeka@gmail.com", "p": "07432159400", "av": "Ask", "h": "Royal Surrey/Hom", "a": "London", "r": 0, "st": "booked", "b": "ESH"}, {"n": "Ross Bowman", "s": "ODP", "ac": "Inactive", "e": "rossco59@hotmail.com", "p": "07717532339", "av": "", "h": "", "a": "Northampton", "r": 0, "st": "unknown", "b": ""}, {"n": "Rowland Kapota", "s": "Scrub", "ac": "Inactive", "e": "Sach19july@yahoo.com", "p": "07779551895", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Rutendo Munyati", "s": "ODP", "ac": "Active", "e": "ruechik@yahoo.co.uk", "p": "07830840827", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "ac": "Active", "e": "ruthmagambo@ymail.com", "p": "07425718791", "av": "", "h": "Spa", "a": "Bournemouth", "r": 0, "st": "unknown", "b": ""}, {"n": "Sahana Aravind", "s": "Scrub", "ac": "Inactive", "e": "anjusanu2005@yahoo.co.uk", "p": "07720395559", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Sandra Amoa-Agyeman", "s": "ODP", "ac": "Inactive", "e": "Sandra-amoa@hotmail.co.uk", "p": "07854962058", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Sandra Popoola", "s": "Recovery", "ac": "Inactive", "e": "sandray@mail.com", "p": "07851873960", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "ac": "Active", "e": "firstsandra3@aol.com", "p": "07528860616", "av": "Self-Book", "h": "Ramsey", "a": "Buckinghamshire", "r": 0, "st": "booked", "b": "Ramsay"}, {"n": "Sasa Jokic", "s": "ODP", "ac": "Active", "e": "sjokic@icloud.com", "p": "07827440672", "av": "Self-Book", "h": "John Radcliffe", "a": "Oxford", "r": 0, "st": "booked", "b": "OXF"}, {"n": "Sebolatan Folashade Owolabi", "s": "Chemo", "ac": "Inactive", "e": "sebolatanolokode1980@gmail.com", "p": "07917192888", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Seyi-Hannah Siwoku", "s": "Recovery", "ac": "Inactive", "e": "seyibanjo_78@yahoo.com", "p": "07883946941", "av": "", "h": "", "a": "Gloucester", "r": 0, "st": "unknown", "b": ""}, {"n": "Shabana Sultana", "s": "ODP", "ac": "Inactive", "e": "shabana1986@hotmail.co.uk", "p": "07535036837", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Shan Shand", "s": "ODP", "ac": "Inactive", "e": "contact.shand@yahoo.com", "p": "07956760761", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Shane Patrick Ford", "s": "ODP", "ac": "Inactive", "e": "sford101@icloud.com", "p": "07921865448", "av": "", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Shauna Henderson-Rose", "s": "Scrub", "ac": "Active", "e": "babybemine3@yahoo.co.uk", "p": "07411241969", "av": "Ask", "h": "", "a": "Essex", "r": 0, "st": "available", "b": ""}, {"n": "Shepherd Masara", "s": "ODP", "ac": "Inactive", "e": "shepherd.masara@yahoo.co.uk", "p": "07814292596", "av": "", "h": "", "a": "Bicester", "r": 0, "st": "unknown", "b": ""}, {"n": "Shivali Bhatia", "s": "Scrub", "ac": "Inactive", "e": "shivalibhatia@yahoo.co.in", "p": "07902496332", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Sholay Shabu", "s": "ODP", "ac": "Active", "e": "shabusholay@hotmail.co.uk", "p": "07595395530", "av": "Ask", "h": "", "a": "Kent", "r": 0, "st": "unknown", "b": ""}, {"n": "Silvestre Salalima", "s": "Scrub", "ac": "Active", "e": "srsjp98@yahoo.com", "p": "07877747216", "av": "Ask", "h": "East Surrey/Hom", "a": "Essex", "r": 0, "st": "booked", "b": "ESH"}, {"n": "Simbarashe Makarau", "s": "ODP", "ac": "Active", "e": "ssmakarau@gmail.com", "p": "07590124425", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Simon Broughton", "s": "ODP", "ac": "Active", "e": "simonbroughton@hotmail.com", "p": "07952980160", "av": "", "h": "Homerton", "a": "London", "r": 0, "st": "unavailable", "b": ""}, {"n": "Stella Maina-Indiazi", "s": "ODP", "ac": "Active", "e": "MAINASTELLA@HOTMAIL.COM", "p": "07984159216", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Stephen Alake", "s": "ODP", "ac": "Active", "e": "stephenalake7@gmail.com", "p": "07419133387", "av": "Ask", "h": "Lew/MSE", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Steve Wilson", "s": "ODP", "ac": "Active", "e": "steve53wilson@outlook.com", "p": "07710882024", "av": "Ask", "h": "", "a": "Milton Keynes", "r": 0, "st": "unknown", "b": ""}, {"n": "Stuart Hicks", "s": "ODP", "ac": "Inactive", "e": "hicksodp@hotmail.com", "p": "07789792529", "av": "", "h": "", "a": "Somerset", "r": 0, "st": "unknown", "b": ""}, {"n": "Stuart Williams", "s": "Scrub", "ac": "Inactive", "e": "Spw1607@gmail.com", "p": "07575167321", "av": "", "h": "", "a": "Milton Keynes", "r": 0, "st": "unknown", "b": ""}, {"n": "Sundar Ponnusamy", "s": "Scrub", "ac": "Inactive", "e": "sunderji_06@yahoo.com", "p": "07584037805", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Susan Mandizha", "s": "Scrub", "ac": "Active", "e": "schilembwe@aol.com", "p": "07984465674", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "SUSAN OKPARA", "s": "Scrub", "ac": "Inactive", "e": "cy.sue@btinternet.com", "p": "07735066980", "av": "", "h": "", "a": "Dartford", "r": 0, "st": "unknown", "b": ""}, {"n": "Swapna Fernandez", "s": "Scrub", "ac": "Inactive", "e": "fernandezswapna@yahoo.com", "p": "07538743094", "av": "", "h": "", "a": "Bristol", "r": 0, "st": "unknown", "b": ""}, {"n": "Sylwia Bartoszewicz", "s": "ODP", "ac": "Inactive", "e": "sylwiagv@yahoo.com", "p": "07572349121", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Tamara Boswell", "s": "Scrub", "ac": "Active", "e": "tamaraboswell@hotmail.co.uk", "p": "07711097662", "av": "Uses App", "h": "Lew/Hom/Barts", "a": "London", "r": 23.0, "st": "available", "b": ""}, {"n": "Tanya Williams", "s": "Scrub", "ac": "Active", "e": "thatslife689@gmail.com", "p": "07943064486", "av": "Ask", "h": "Lew/Hom", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Tatenda Chitiyo", "s": "ODP", "ac": "Active", "e": "valentinechitiyo@hotmail.co.uk", "p": "07876115424", "av": "", "h": "Chelsea", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Thaddee Balebela Mubenga", "s": "Scrub", "ac": "Active", "e": "laurainengalu@yahoo.fr", "p": "07468583544", "av": "Ask", "h": "", "a": "Peterborough", "r": 21.0, "st": "unknown", "b": ""}, {"n": "Thanooja Fahadh", "s": "Scrub", "ac": "Inactive", "e": "Thanif02@yahoo.co.uk", "p": "07808316720", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Tirett Millard", "s": "ODP", "ac": "Active", "e": "tirettmillard@hotmail.com", "p": "07970394338", "av": "Self-Book", "h": "Royal Surrey", "a": "Surrey", "r": 0, "st": "booked", "b": "RSCH"}, {"n": "Tochukwu R Agada", "s": "ODP", "ac": "Inactive", "e": "roysmalz@yahoo.com", "p": "07899668198", "av": "", "h": "", "a": "Hertfordshire", "r": 0, "st": "unknown", "b": ""}, {"n": "Tolulope ALABI (Olalekan)", "s": "Recovery", "ac": "Inactive", "e": "Tolulopeolalekan97@gmail.com", "p": "07704486188", "av": "", "h": "", "a": "Bedford", "r": 0, "st": "unknown", "b": ""}, {"n": "Uzoma Akosim", "s": "ODP", "ac": "Active", "e": "uzoakosim@yahoo.com", "p": "07795278002", "av": "Ask", "h": "Royal Surrey/MSE/Hom", "a": "London", "r": 0, "st": "unavailable", "b": ""}, {"n": "Varkey Thuruthiyil Varkey", "s": "Scrub", "ac": "Inactive", "e": "rennyswaraj76@gmail.com", "p": "07533030199", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Victor Nwaki", "s": "Recovery", "ac": "Inactive", "e": "dr_nwaki@msn.com", "p": "07988261869", "av": "", "h": "", "a": "Watford", "r": 0, "st": "unknown", "b": ""}, {"n": "Victor Provido", "s": "ODP", "ac": "Inactive", "e": "providovictor@gmail.com", "p": "07714793569", "av": "", "h": "", "a": "Surrey", "r": 0, "st": "unknown", "b": ""}, {"n": "Victoria Adeola", "s": "Recovery", "ac": "Inactive", "e": "vicade5@aol.com", "p": "07533349417", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Vigil Chakwendama", "s": "Recovery", "ac": "Active", "e": "verlleinc@gmail.com", "p": "07312126183", "av": "Ask", "h": "", "a": "Oxford", "r": 0, "st": "unknown", "b": ""}, {"n": "Vimbai Magwenjere", "s": "ODP", "ac": "Active", "e": "vimbsykamuruko@yahoo.co.uk", "p": "07454685386", "av": "", "h": "", "a": "Bedford", "r": 0, "st": "unknown", "b": ""}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "ac": "Active", "e": "veemapolisa@yahoo.com", "p": "07832386605", "av": "Uses App", "h": "Lewisham", "a": "London", "r": 0, "st": "booked", "b": "Lew"}, {"n": "Vincent Breslin", "s": "ODP", "ac": "Active", "e": "vincebreslin@live.co.uk", "p": "07778269823", "av": "", "h": "Chelsea", "a": "London", "r": 0, "st": "available", "b": ""}, {"n": "Visshal Roy Issuree", "s": "ODP", "ac": "Active", "e": "v.issuree@gmail.com", "p": "07375533292", "av": "Self-Book", "h": "Royal Surrey", "a": "London", "r": 0, "st": "booked", "b": "BHT"}, {"n": "Vivian Anyanwu", "s": "ODP", "ac": "Inactive", "e": "vivigerty@yahoo.com", "p": "07944032447", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Vivian Owusu", "s": "RGN", "ac": "Inactive", "e": "vivienne_owusu@hotmail.com", "p": "07983141368", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Vusumzi Michael Khaka", "s": "Scrub", "ac": "Inactive", "e": "michaelkhaka767@hotmail.com", "p": "07985202055", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Wilhemina John", "s": "ODP", "ac": "Inactive", "e": "wilheminajohn2006@yahoo.co.uk", "p": "07951698367", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Willard Mandaza", "s": "ODP", "ac": "Active", "e": "veemapolisa@yahoo.com", "p": "07832386605", "av": "Ask", "h": "Royal London/MSE/Hom", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Xiaohong (Ruby) Fan", "s": "ODP", "ac": "Inactive", "e": "wintor2018@gmail.com", "p": "07445526188", "av": "", "h": "", "a": "Bournemouth", "r": 0, "st": "unknown", "b": ""}, {"n": "Yasmin Pattrick", "s": "ODP", "ac": "Inactive", "e": "yasmin_x@live.co.uk", "p": "07901724219", "av": "", "h": "", "a": "Great Yarmouth", "r": 0, "st": "unknown", "b": ""}, {"n": "Yohannes Adamu", "s": "ODP", "ac": "Active", "e": "yohannesadamu2005@yahoo.com", "p": "07908458064", "av": "", "h": "MSE", "a": "", "r": 0, "st": "unknown", "b": ""}, {"n": "Yvonne Patsanza", "s": "ODP", "ac": "Inactive", "e": "ypatsanza@yahoo.co.uk", "p": "07340456941", "av": "", "h": "", "a": "Essex", "r": 0, "st": "unknown", "b": ""}, {"n": "Zahra Noor", "s": "ODP", "ac": "Inactive", "e": "znoor90@hotmail.co.uk", "p": "07950304729", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Zahra Rana", "s": "Scrub", "ac": "Inactive", "e": "zahra_abdulsattar@yahoo.co.uk", "p": "07713437128", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Zamzam Abdulle", "s": "ODP", "ac": "Inactive", "e": "zamygure6@outlook.com", "p": "07377942724", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}, {"n": "Zoe Hodge", "s": "ODP", "ac": "Inactive", "e": "zoehodge85@hotmail.com", "p": "07850280375", "av": "", "h": "", "a": "London", "r": 0, "st": "unknown", "b": ""}];
var H=[{"name": "Lewisham & QEH", "area": "London", "pps": 33.155, "total": 907}, {"name": "MSE", "area": "Essex", "pps": 23.56, "total": 1231}, {"name": "Homerton", "area": "London", "pps": 33.44, "total": 820}, {"name": "Barts", "area": "London", "pps": 45.41, "total": 271}, {"name": "Royal Surrey", "area": "Surrey", "pps": 36.195, "total": 764}, {"name": "East Surrey", "area": "Surrey", "pps": 40.945, "total": 466}, {"name": "QVH", "area": "Kent", "pps": 47.88, "total": 312}, {"name": "Ramsay", "area": "Private", "pps": 0, "total": 315}, {"name": "Watford", "area": "Hertfordshire", "pps": 26.72, "total": 142}, {"name": "Luton & Bedford", "area": "Hertfordshire", "pps": 39.615, "total": 890}, {"name": "Royal Berkshire", "area": "Surrey", "pps": 38.0, "total": 156}, {"name": "Cromwell", "area": "Private", "pps": 20.33, "total": 90}, {"name": "Spa Medica", "area": "Private", "pps": 47.5, "total": 321}];
var R=[{"trust": "Royal Surrey", "hospital": "Royal Surrey", "ward": "Theatres - RSCH", "pd": 29.7, "pn": 31.68, "ps": 31.68, "cd": 33.5, "cn": 35.0, "md": 3.8}, {"trust": "Surrey & Sussex", "hospital": "East Surrey", "ward": "Theatres - East Surrey", "pd": 29.7, "pn": 37.61, "ps": 40.57, "cd": 34.0, "cn": 44.23, "md": 4.3}, {"trust": "Surrey & Sussex", "hospital": "Crawley", "ward": "", "pd": 29.7, "pn": 37.61, "ps": 40.57, "cd": 34.0, "cn": 44.23, "md": 4.3}, {"trust": "West Herfordshire", "hospital": "Watford", "ward": "Main Theatres", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "md": 4.45}, {"trust": "West Herfordshire", "hospital": "St Albans", "ward": "Main Theatres", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "md": 4.45}, {"trust": "Royal Berkshire", "hospital": "Royal Berkshire", "ward": "Main Theatres - RBH", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "md": 4.45}, {"trust": "Mid Essex", "hospital": "Southend", "ward": "Main Theatres", "pd": 26.5, "pn": 30.0, "ps": 35.0, "cd": 28.98, "cn": 37.82, "md": 2.48}, {"trust": "Mid Essex", "hospital": "Broomfield", "ward": "Main Theatres", "pd": 26.5, "pn": 30.0, "ps": 35.0, "cd": 28.98, "cn": 37.82, "md": 2.48}, {"trust": "Mid Essex", "hospital": "Basildon", "ward": "Main Theatres", "pd": 26.5, "pn": 30.0, "ps": 35.0, "cd": 28.98, "cn": 37.82, "md": 2.48}, {"trust": "Mid Essex", "hospital": "Southend", "ward": "Main Theatres", "pd": 20.0, "pn": 26.0, "ps": 31.0, "cd": 23.32, "cn": 30.48, "md": 3.32}, {"trust": "Mid Essex", "hospital": "Broomfield", "ward": "Main Theatres", "pd": 20.0, "pn": 26.0, "ps": 31.0, "cd": 23.32, "cn": 30.48, "md": 3.32}, {"trust": "Mid Essex", "hospital": "Basildon", "ward": "Main Theatres", "pd": 21.0, "pn": 27.0, "ps": 32.0, "cd": 24.51, "cn": 31.67, "md": 3.51}, {"trust": "Sussex", "hospital": "St Richards", "ward": "Chichester Main Theatres", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "md": 4.3}, {"trust": "Sussex", "hospital": "Princess Royal", "ward": "Theatres - PRH", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "md": 4.3}, {"trust": "Sussex", "hospital": "Royal Sussex County", "ward": "Theatres RSCH", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "md": 4.3}, {"trust": "Sussex", "hospital": "Worthing", "ward": "Main Theatres - Worthing", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "md": 4.3}, {"trust": "Bedfordshire", "hospital": "Luton", "ward": "Theatres - L&DH", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "md": 4.45}, {"trust": "Bedfordshire", "hospital": "Bedford", "ward": "Theatres - Bedford", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "md": 4.45}, {"trust": "Queen Victoria", "hospital": "Queen Victoria", "ward": "", "pd": 24.74, "pn": 29.69, "ps": 34.64, "cd": 29.78, "cn": 38.71, "md": 5.04}, {"trust": "Barts Health", "hospital": "St Barts (Inner)", "ward": "Theatres - St Barts", "pd": 22.76, "pn": 24.74, "ps": 29.69, "cd": 26.94, "cn": 29.45, "md": 4.18}, {"trust": "Barts Health", "hospital": "St Barts (Inner)", "ward": "Theatres - St Barts", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 32.8, "cn": 37.03, "md": 6.08}, {"trust": "Barts Health", "hospital": "Royal London (Inner)", "ward": "Theatres - Royal London", "pd": 22.76, "pn": 24.74, "ps": 29.69, "cd": 26.94, "cn": 29.45, "md": 4.18}, {"trust": "Barts Health", "hospital": "Royal London (Inner)", "ward": "Theatres - Royal London", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 32.8, "cn": 37.03, "md": 6.08}, {"trust": "Barts Health", "hospital": "Whipps Cross (Outer)", "ward": "Theatres - Whipps", "pd": 20.79, "pn": 23.75, "ps": 27.71, "cd": 25.88, "cn": 29.9, "md": 5.09}, {"trust": "Barts Health", "hospital": "Whipps Cross (Outer)", "ward": "Theatres - Whipps", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 31.5, "cn": 35.59, "md": 4.78}, {"trust": "Barts Health", "hospital": "Newham (Outer)", "ward": "Theatres 4 Main", "pd": 20.79, "pn": 23.75, "ps": 27.71, "cd": 25.88, "cn": 29.9, "md": 5.09}, {"trust": "Barts Health", "hospital": "Newham (Outer)", "ward": "Theatres 4 Main", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 31.5, "cn": 35.59, "md": 4.78}];
var A=["Barts", "Bristol & Western", "Care Fertility", "Crawley", "Cromwell", "Croydon", "DVH", "East Suffolk", "East Surrey", "Homerton", "Jersey", "Lewisham & QEH", "Luton & Bedford", "MSE", "Medway", "Northampton", "Oxford", "QVH", "RNOH", "Ramsay", "Royal Berkshire", "Royal Free", "Royal Surrey", "Salisbury", "Spa Medica", "St Richards", "UCLH", "Watford", "Whittington"];
var W=[{"wk": 51, "shifts": 274, "margin": 8127}, {"wk": 52, "shifts": 227, "margin": 13108}, {"wk": 1, "shifts": 188, "margin": 9915}, {"wk": 2, "shifts": 102, "margin": 7339}, {"wk": 3, "shifts": 110, "margin": 4574}, {"wk": 4, "shifts": 161, "margin": 6185}, {"wk": 5, "shifts": 120, "margin": 8434}, {"wk": 6, "shifts": 141, "margin": 6587}, {"wk": 7, "shifts": 151, "margin": 9331}, {"wk": 8, "shifts": 121, "margin": 8020}, {"wk": 9, "shifts": 129, "margin": 6340}, {"wk": 10, "shifts": 115, "margin": 8599}, {"wk": 11, "shifts": 151, "margin": 7196}, {"wk": 12, "shifts": 156, "margin": 9312}, {"wk": 13, "shifts": 136, "margin": 7167}, {"wk": 14, "shifts": 130, "margin": 9008}, {"wk": 15, "shifts": 133, "margin": 9008}, {"wk": 16, "shifts": 123, "margin": 6496}, {"wk": 17, "shifts": 133, "margin": 4854}, {"wk": 18, "shifts": 157, "margin": 7846}, {"wk": 19, "shifts": 145, "margin": 7834}, {"wk": 20, "shifts": 139, "margin": 7886}, {"wk": 21, "shifts": 126, "margin": 6488}, {"wk": 22, "shifts": 138, "margin": 4768}, {"wk": 23, "shifts": 145, "margin": 7106}, {"wk": 24, "shifts": 164, "margin": 7112}, {"wk": 25, "shifts": 158, "margin": 6446}, {"wk": 26, "shifts": 153, "margin": 5395}, {"wk": 27, "shifts": 161, "margin": 7834}, {"wk": 28, "shifts": 154, "margin": 0}, {"wk": 29, "shifts": 158, "margin": 4852}, {"wk": 30, "shifts": 145, "margin": 6158}, {"wk": 31, "shifts": 150, "margin": 5862}, {"wk": 32, "shifts": 113, "margin": 8207}, {"wk": 33, "shifts": 146, "margin": 3522}, {"wk": 34, "shifts": 177, "margin": 6209}, {"wk": 35, "shifts": 158, "margin": 5442}, {"wk": 36, "shifts": 156, "margin": 4417}, {"wk": 37, "shifts": 115, "margin": 0}, {"wk": 38, "shifts": 41, "margin": 0}, {"wk": 39, "shifts": 65, "margin": 0}, {"wk": 40, "shifts": 156, "margin": 0}, {"wk": 41, "shifts": 167, "margin": 0}, {"wk": 42, "shifts": 181, "margin": 0}, {"wk": 43, "shifts": 168, "margin": 0}, {"wk": 44, "shifts": 147, "margin": 0}];
var HC=[{"name": "Lewisham & QEH", "area": "London", "pps": 33.155, "total": 907, "weekly": [9, 19, 6, 0, 0, 2, 4, 14, 14, 8, 21, 17, 12, 15, 9, 0], "processes": [{"action": "Self-Bill report (Shifts Authorised Monday and Friday)", "day": "Weekly", "time": ""}, {"action": "TS Rejection report from bank- lg.tsbankstaffsupportteam@nhs.net", "day": "Weekly", "time": ""}, {"action": "Email amended timesheet back to support team - lg.tsbankstaffsupportteam@nhs.net", "day": "", "time": ""}, {"action": "Availability to be added to Ursa (To be updated if availability is no longer needed)", "day": "Weekly", "time": ""}, {"action": "Run a slave from 8am (to maximise chance of getting shifts)", "day": "Daily", "time": ""}, {"action": "Comfort Raji", "day": "", "time": ""}, {"action": "Sunday Olaniyan", "day": "", "time": ""}, {"action": "Sakilla Jugon", "day": "", "time": ""}], "rota": [], "issues": [{"issue": "Candidate Cancellation", "resolution": "Email bank - To be done 24 hours befor shift start"}, {"issue": "Unfinalised shifts (Payment)", "resolution": "Email LG.TSBankstaffSupportTeam@nhs.net with timesheet to action payment which is overdue"}, {"issue": "Mary Mapolisa", "resolution": "Mary Mapolisa"}, {"issue": "CV Approval", "resolution": "CV Approval"}, {"issue": "Ian Ali", "resolution": "Ian Ali"}, {"issue": "Karen Agbuya", "resolution": "Karen Agbuya"}], "roster_link": "", "contacts": [{"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "lg.agencyliaisonteam@nhs.net", "phone": "02088364844", "lastContacted": ""}], "rates": [], "personalRates": []}, {"name": "MSE", "area": "Essex", "pps": 23.56, "total": 1231, "weekly": [47, 46, 46, 13, 24, 41, 42, 41, 44, 33, 37, 40, 42, 44, 47, 0], "processes": [{"action": "Shift Authorised on HR", "day": "Monday", "time": "10:00"}, {"action": "Litmus Scrap Finalised shifts", "day": "Monday", "time": "12:00"}, {"action": "Receive 1st Litmus Self-bill", "day": "Wednesday", "time": "11:00"}, {"action": "Cross-check HR and Litmus Payments", "day": "Wednesday", "time": "12:00"}, {"action": "Inform Litmus of any missing or underpayments", "day": "Wednesday", "time": "12:00"}, {"action": "Add shifts to QP and email self-bill team", "day": "Wednesday", "time": "12:00"}, {"action": "Payroll Process payment", "day": "Wednesday", "time": "17:00"}, {"action": "Receive 2nd Litmus Self-bill", "day": "Friday", "time": "11:00"}, {"action": "Oana Tilvic - TS portal", "day": "", "time": ""}], "rota": [{"name": "David Joy (Non-DE)", "spec": "ODP"}, {"name": "Willard Mandaza (Non-DE)", "spec": "ODP"}, {"name": "Gina-Oana Tilvic (Non-DE)", "spec": "ODP"}, {"name": "Lena O'leary (Non-DE)", "spec": "ODP + Scrub"}, {"name": "Stephen Alake", "spec": "ODP"}, {"name": "Daniel Pakbonyan", "spec": "ODP"}, {"name": "Oluwamayowa Fabunmi", "spec": "ODP"}, {"name": "Sholay Shabu", "spec": "Scrub"}, {"name": "Bimbola Oduyemi", "spec": "Scrub"}, {"name": "Phillip Mwaijumba", "spec": "Scrub"}, {"name": "Melody Mamire", "spec": "Scrub"}, {"name": "Evelyn kabba", "spec": "Scrub"}, {"name": "Florah Mudeke", "spec": "Scrub"}], "issues": [{"issue": "Shift not approved on HR", "resolution": "Ask staff bank to authorise / candidate check with manager"}, {"issue": "Missing from Litmus Report", "resolution": "Email Litmus Adjustments (likely missed cut off)"}, {"issue": "Timesheet & Litmus Self-bill mismatch", "resolution": "Confirm with candidate (breaktimes may be added) confirm with staff bank"}, {"issue": "Charge lower than agreed rate", "resolution": "Email Litmus and Staff bank to change"}], "roster_link": "https://www.onlinets.co.uk/meritportal/external_login.aspx?id=aEJf1wroAll0XRo0K6jbWxjjto5W%2ffyv5f9jN%23%2d%23%2d%23RVYdlDkMyRyQZuhw%3d%3d&aid=20", "contacts": [{"name": "Nina Martin", "title": "Snr Client Relationship Manager", "dept": "Temporary Staffing", "email": "nina.martin6@nhs.net", "phone": "03004430160", "lastContacted": ""}, {"name": "Kaylee Crooks", "title": "Workforce Solutions Consultant", "dept": "Temporary Staffing", "email": "kaylee.crooks@nhs.net", "phone": "03004430160", "lastContacted": "2026-01-13"}, {"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "mse.group.temporarystaffing@nhs.net", "phone": "03004430160", "lastContacted": ""}], "rates": [], "personalRates": [{"name": "Bimbola Oduyemi", "spec": "Scrub", "rate": 25.0}, {"name": "Phillip Mwaijumba", "spec": "Scrub", "rate": 20.0}]}, {"name": "Homerton", "area": "London", "pps": 33.44, "total": 820, "weekly": [25, 17, 10, 13, 15, 26, 27, 37, 41, 40, 26, 30, 32, 32, 26, 0], "processes": [{"action": "Pay by Timesheet - Ref required", "day": "", "time": ""}], "rota": [{"name": "Patrick Adutwim", "spec": "ODP"}, {"name": "Mahir Ahmed", "spec": "ODP"}, {"name": "Alex Acheampong", "spec": "ODP"}, {"name": "John Arthur", "spec": "ODP"}, {"name": "Willard Mandaza", "spec": "ODP"}, {"name": "Daniel Pakbonyan", "spec": "ODP"}, {"name": "Uzoma Akosim", "spec": "ODP"}, {"name": "Alexio Hungwa", "spec": "Anae/Scrub"}, {"name": "BIBI SAKILLA JUGON", "spec": "Anae/Scrub"}, {"name": "Babajide Fasuji", "spec": "Anae/Scrub -Ortho"}, {"name": "Roseline Emmanuel", "spec": "Scrub -Ortho"}, {"name": "Joseph Veloso", "spec": "Scrub - Ortho"}, {"name": "Genn Agduyeng", "spec": "Scrub -Ortho"}, {"name": "Abidemi Jegede", "spec": "Scrub"}, {"name": "Ethel Ikeh", "spec": "Scrub"}, {"name": "Augustina Akujobi", "spec": "Scrub"}, {"name": "Librada Tagelo", "spec": "Scrub"}, {"name": "Bimbola Odiemui", "spec": "Scrub"}, {"name": "Mercy Afolabi", "spec": "Scrub"}, {"name": "Tamara Boswell", "spec": "Scrub"}, {"name": "Christopher Bwalya", "spec": "ODP"}, {"name": "Simon Broughton", "spec": "ODP"}], "issues": [{"issue": "not able to allocate ODPs on Roster", "resolution": "Email staff bank to book shift"}], "roster_link": "", "contacts": [{"name": "Joleen Jones", "title": "Lead ODP", "dept": "Main Theatres", "email": "joleen.jones@nhs.net", "phone": "07958930019", "lastContacted": "2026-01-12"}, {"name": "Catia Jardim", "title": "B6 ODP", "dept": "Main Theatres", "email": "Catia.jardim@nhs.net", "phone": "07427657075", "lastContacted": ""}, {"name": "Kwame Konadu", "title": "B7 Recovery", "dept": "Main Theatres", "email": "kwame.konadu-yiadom@nhs.net", "phone": "07590023736", "lastContacted": ""}, {"name": "Fiona Feighney", "title": "Senior Nurse", "dept": "Peri-Operative and Surgical Services", "email": "fiona.feighney1@nhs.net", "phone": "07481309247", "lastContacted": ""}, {"name": "Bernice Alexis", "title": "B7 Scrub", "dept": "Main Theatres", "email": "b.alexis@nhs.net", "phone": "02085105757", "lastContacted": ""}, {"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "huh-tr.staff.bank@nhs.net", "phone": "02085105119", "lastContacted": ""}, {"name": "Reshma Zaina", "title": "Staff Bank Co-ordinator", "dept": "Temporary Staffing", "email": "Reshma.zaina@nhs.net", "phone": "02085105119", "lastContacted": ""}, {"name": "Michelle Allen", "title": "Temporary Staffing Manager", "dept": "Temporary Staffing", "email": "michelle.allen1@nhs.net", "phone": "07940999518", "lastContacted": ""}], "rates": [], "personalRates": []}, {"name": "Barts", "area": "London", "pps": 45.41, "total": 271, "weekly": [5, 5, 5, 0, 0, 0, 1, 4, 3, 5, 3, 1, 4, 0, 0, 0], "processes": [{"action": "Self-Bill report (Link in login details section)", "day": "", "time": ""}, {"action": "Check Theatre shifts on report and approve if hours, banding & rates are correct based on ", "day": "", "time": ""}, {"action": "Payment made to candidate on Thursday", "day": "", "time": ""}, {"action": "Raheela Ashraf", "day": "", "time": ""}, {"action": "Shifts which come over on the self bill report but have been paid by timesheet should not ", "day": "", "time": ""}, {"action": "Rayven Renee", "day": "", "time": ""}, {"action": "Lena O'Leary", "day": "", "time": ""}, {"action": "Stella Maina-Indiazi", "day": "", "time": ""}, {"action": "Alexio Hungwa", "day": "", "time": ""}], "rota": [{"name": "Chipo Kanda", "spec": "Scrub"}, {"name": "John Arthur", "spec": "ODP"}, {"name": "Raheela Ashraf", "spec": "Scrub"}, {"name": "Tamara Boswell", "spec": "Scrub"}, {"name": "Rayven Renee", "spec": "ODP"}, {"name": "Will Mandaza", "spec": "ODP"}, {"name": "Mahir Ahmed", "spec": "ODP"}, {"name": "Daniel Pakbonyan", "spec": "ODP"}, {"name": "Moses Olufunwa", "spec": "ODP + Scrub"}, {"name": "Jonathan Rendon", "spec": "ODP"}], "issues": [{"issue": "Abidemi Layo Jegede", "resolution": "Abidemi Layo Jegede"}, {"issue": "chipo Kanda (Ursa)", "resolution": "chipo Kanda (Ursa)"}, {"issue": "John Arthur (Ursa)", "resolution": "John Arthur (Ursa)"}, {"issue": "Olutoyin Latinwo (Ursa)", "resolution": "Olutoyin Latinwo (Ursa)"}, {"issue": "Raheela Ashraf (Ursa)", "resolution": "Raheela Ashraf (Ursa)"}, {"issue": "Tamara Boswell (Ursa)", "resolution": "Tamara Boswell (Ursa)"}], "roster_link": "", "contacts": [{"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "bartsnursebookings@bankpartners.co.uk", "phone": "", "lastContacted": ""}], "rates": [{"trust": "Barts Health", "hospital": "St Barts (Inner)", "card": "CB5 - The (Care Providers)", "ward": "Theatres - St Barts", "pd": 22.76, "pn": 24.74, "ps": 29.69, "cd": 26.94, "cn": 29.45, "cs": 35.11, "md": 4.18}, {"trust": "Barts Health", "hospital": "St Barts (Inner)", "card": "CB6 - Theatres (Care Providers)", "ward": "Theatres - St Barts", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 32.8, "cn": 37.03, "cs": 42.67, "md": 6.08}, {"trust": "Barts Health", "hospital": "Royal London (Inner)", "card": "CB5 - The (Care Providers)", "ward": "Theatres - Royal London", "pd": 22.76, "pn": 24.74, "ps": 29.69, "cd": 26.94, "cn": 29.45, "cs": 35.11, "md": 4.18}, {"trust": "Barts Health", "hospital": "Royal London (Inner)", "card": "CB6 - Theatres (Care Providers )", "ward": "Theatres - Royal London", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 32.8, "cn": 37.03, "cs": 42.67, "md": 6.08}, {"trust": "Barts Health", "hospital": "Whipps Cross (Outer)", "card": "CB5 - The (Care Providers)", "ward": "Theatres - Whipps", "pd": 20.79, "pn": 23.75, "ps": 27.71, "cd": 25.88, "cn": 29.9, "cs": 35.0, "md": 5.09}, {"trust": "Barts Health", "hospital": "Whipps Cross (Outer)", "card": "CB6 - The (Care Providers)", "ward": "Theatres - Whipps", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 31.5, "cn": 35.59, "cs": 41.28, "md": 4.78}], "personalRates": [{"name": "Janet Balacanao", "spec": "Chemo", "rate": 30.0}]}, {"name": "Royal Surrey", "area": "Surrey", "pps": 36.195, "total": 764, "weekly": [12, 8, 5, 6, 3, 8, 8, 10, 7, 6, 4, 9, 5, 5, 11, 0], "processes": [{"action": "Self-Bill Report", "day": "", "time": ""}, {"action": "Shifts not on or missing from Self-Bill report email Staff Bank - rsc-tr.staffbank@nhs.net", "day": "", "time": ""}, {"action": "Uzoma Akosim", "day": "", "time": ""}, {"action": "Roseline Emmanuel", "day": "", "time": ""}, {"action": "Fanol Gjata", "day": "", "time": ""}, {"action": "Aleksandra Lacey", "day": "", "time": ""}, {"action": "Tirett Millard", "day": "", "time": ""}, {"action": "Josephloid Veloso", "day": "", "time": ""}], "rota": [], "issues": [], "roster_link": "", "contacts": [{"name": "Lisa Tinker", "title": "Lead ODP", "dept": "Main Theatres", "email": "lisa.tinker@nhs.net", "phone": "07967730177", "lastContacted": ""}, {"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "rsc-tr.staffbank@nhs.net", "phone": "01493571122", "lastContacted": ""}, {"name": "Khader", "title": "Theatre Manager", "dept": "Main Theatres", "email": "", "phone": "07850932324", "lastContacted": ""}, {"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "rf-tr.tsbookings@nhs.net", "phone": "02078302065", "lastContacted": "2026-01-13"}, {"name": "Richard", "title": "Staff Bank Co-ordinator", "dept": "Temporary Staffing", "email": "", "phone": "", "lastContacted": ""}], "rates": [{"trust": "Royal Surrey", "hospital": "Royal Surrey", "card": "CB6 - The (Day Webster Ltd)", "ward": "Theatres - RSCH", "pd": 29.7, "pn": 31.68, "ps": 31.68, "cd": 33.5, "cn": 35.0, "cs": 35.0, "md": 3.8}, {"trust": "Surrey & Sussex", "hospital": "East Surrey", "card": "CB5 - The (Daywebster Ltd)", "ward": "Theatres - East Surrey", "pd": 29.7, "pn": 37.61, "ps": 40.57, "cd": 34.0, "cn": 44.23, "cs": 48.35, "md": 4.3}, {"trust": "Surrey & Sussex", "hospital": "Crawley", "card": "", "ward": "", "pd": 29.7, "pn": 37.61, "ps": 40.57, "cd": 34.0, "cn": 44.23, "cs": 48.35, "md": 4.3}, {"trust": "Royal Berkshire", "hospital": "Royal Berkshire", "card": "CB6 - The PRC Rate NEW", "ward": "Main Theatres - RBH", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "cs": 41.0, "md": 4.45}, {"trust": "Sussex", "hospital": "Princess Royal", "card": "CB6 - The Esc (Day Webster)", "ward": "Theatres - PRH", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "cs": 34.0, "md": 4.3}, {"trust": "Sussex", "hospital": "Royal Sussex County", "card": "CB6 - The Esc (Day Webster)", "ward": "Theatres RSCH", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "cs": 34.0, "md": 4.3}], "personalRates": []}, {"name": "East Surrey", "area": "Surrey", "pps": 40.945, "total": 466, "weekly": [7, 5, 8, 2, 7, 3, 7, 5, 6, 2, 8, 10, 9, 14, 9, 0], "processes": [{"action": "Client will email timesheets either on a Monday or Tuesday to theatres", "day": "Monday", "time": ""}, {"action": "Upload timesheet to QP (add booking if need to) - has to include ref number", "day": "", "time": ""}, {"action": "Make sure Cawley and ESH timesheets received for named workers before adding booking *", "day": "", "time": ""}, {"action": "Lauren Orgar *", "day": "", "time": ""}, {"action": "Jovanie Santos", "day": "", "time": ""}, {"action": "Marlon Orio", "day": "", "time": ""}], "rota": [{"name": "Ortho Scrub", "spec": "Recovery"}], "issues": [{"issue": "Timesheets may be recieved on different days for each site, please only process once all t", "resolution": "Check staff names to know who to look out for - email contacts below"}, {"issue": "Both candidates and clients will send in timesheets", "resolution": "You can only process the timesheet which the client sends as it will have the reference numbers atta"}, {"issue": "Approval email*", "resolution": ""}, {"issue": "Good Afternoon/morning,", "resolution": ""}, {"issue": "I hope you\u2019re doing well.", "resolution": ""}, {"issue": "Please find below CV approval to work in theatres.", "resolution": ""}, {"issue": "I have also attached their compliance credentials for your consideration.", "resolution": ""}, {"issue": "They will also require a cerner card and co-sign account,", "resolution": ""}], "roster_link": "", "contacts": [{"name": "Lisa Tinker", "title": "Lead ODP", "dept": "Main Theatres", "email": "lisa.tinker@nhs.net", "phone": "07967730177", "lastContacted": ""}, {"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "rsc-tr.staffbank@nhs.net", "phone": "01493571122", "lastContacted": ""}], "rates": [{"trust": "Royal Surrey", "hospital": "Royal Surrey", "card": "CB6 - The (Day Webster Ltd)", "ward": "Theatres - RSCH", "pd": 29.7, "pn": 31.68, "ps": 31.68, "cd": 33.5, "cn": 35.0, "cs": 35.0, "md": 3.8}, {"trust": "Surrey & Sussex", "hospital": "East Surrey", "card": "CB5 - The (Daywebster Ltd)", "ward": "Theatres - East Surrey", "pd": 29.7, "pn": 37.61, "ps": 40.57, "cd": 34.0, "cn": 44.23, "cs": 48.35, "md": 4.3}, {"trust": "Surrey & Sussex", "hospital": "Crawley", "card": "", "ward": "", "pd": 29.7, "pn": 37.61, "ps": 40.57, "cd": 34.0, "cn": 44.23, "cs": 48.35, "md": 4.3}], "personalRates": [{"name": "Paivi Hannele Raulamo", "spec": "Scrub", "rate": 25.0}]}, {"name": "QVH", "area": "Kent", "pps": 47.88, "total": 0, "weekly": [], "processes": [{"action": "Upload timsheets once recieved", "day": "ASAP", "time": ""}, {"action": "Amber Asif", "day": "", "time": ""}, {"action": "Josh Tanimowo", "day": "", "time": ""}, {"action": "Rob Maskell", "day": "", "time": ""}, {"action": "Patrick Mitchell", "day": "", "time": ""}, {"action": "John Arthur", "day": "", "time": ""}, {"action": "Oliver Nnabugwu", "day": "", "time": ""}], "rota": [], "issues": [{"issue": "Patrick Mitchell's timesheets", "resolution": "Patrick sends multiple timesheets for the following - QVH Day shifts/Oncall Shifts & Care Fertility "}], "roster_link": "", "contacts": [], "rates": [], "personalRates": []}, {"name": "Ramsay", "area": "Private", "pps": 0, "total": 315, "weekly": [6, 3, 0, 0, 0, 7, 6, 3, 0, 0, 8, 7, 9, 2, 6, 0], "processes": [{"action": "Timesheet received by candidate", "day": "Monday", "time": "10:00"}, {"action": "Timesheets hour inputted to Retinue Bridge (if shifts are confirmed)", "day": "Tuesday", "time": "12:00"}, {"action": "Hospital approve hours", "day": "Wednesday", "time": "12:00"}, {"action": "Retinue send self-bill", "day": "Friday", "time": "11:00"}, {"action": "Payroll process payment", "day": "Friday", "time": "17:00"}, {"action": "Sandra Maria Duarte-Botello", "day": "", "time": ""}], "rota": [{"name": "Adebukola Akintayo", "spec": "ODP Recovery"}, {"name": "Adekanmi Ogunbufunmi", "spec": "ODP Recovery"}, {"name": "Adelaide Sackeyfio", "spec": "Scrub opthalmic"}, {"name": "Aleksandra Lacey", "spec": "ODP , Scrub"}, {"name": "Alex Acheampong", "spec": "ODP"}, {"name": "Alex Amponsah", "spec": "Scrub (Ortho)"}, {"name": "Alexio Hungwa", "spec": "ODP"}, {"name": "Alvin Tabusares", "spec": "Scrub(Ortho) + SFA"}, {"name": "Amanda Maison", "spec": "ODP"}, {"name": "Amarachukwu (Amara) Anadu", "spec": "Scrub (Ortho)"}, {"name": "Amma Asiedu-Baning", "spec": "Scrub"}, {"name": "Bridie Newton", "spec": "ODP"}, {"name": "Chompunuch Chiratanawatana", "spec": "ODP"}, {"name": "Daniel Pakbonyan", "spec": "ODP"}, {"name": "Fanol Gjata", "spec": "ODP"}], "issues": [{"issue": "Shifts not on Retinue", "resolution": "Email timesheet to Retinue to add"}, {"issue": "Contradicted Shift specialities (on the Timesheet and Bridge)", "resolution": "email retinue to amend the speciality\u00a0 or getting the TS amended"}, {"issue": "Shifts not authorised by hospital", "resolution": "Email department to authorise shift"}, {"issue": "Incorrect rate", "resolution": "Query with retinue"}, {"issue": "Hours not approved", "resolution": "Email timesheet to Retinue to approve"}, {"issue": "If hours were approved after Tuesday", "resolution": "Pay only's"}], "roster_link": "", "contacts": [{"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "ramsayhealth@retinue-solutions.com", "phone": "02036678640", "lastContacted": ""}, {"name": "Julie", "title": "Theatre Coordinator", "dept": "Springfield - Theatres", "email": "", "phone": "07776204603", "lastContacted": ""}, {"name": "Claire Lopez", "title": "Theatre Coordinator", "dept": "Oaks - theatres", "email": "claire.lopes@ramsayhealth.co.uk", "phone": "07845330857", "lastContacted": ""}], "rates": [], "personalRates": []}, {"name": "Watford", "area": "Hertfordshire", "pps": 26.72, "total": 0, "weekly": [], "processes": [{"action": "Band 7 approve hours on NHSP", "day": "Daily", "time": ""}, {"action": "Email received from NHSP to Approve or query - Check Code*", "day": "", "time": "10:00"}, {"action": "Self bill received by NHSP", "day": "", "time": "12:00"}, {"action": "Payroll process payment", "day": "", "time": "18:00"}], "rota": [], "issues": [{"issue": "Incorrect assignment code", "resolution": "Query shift after shift has been approved"}, {"issue": "Incorrect rate paid", "resolution": "Email systems to see if the rate card is active"}, {"issue": "shift not on NHSP", "resolution": "fill out a retrospective form, email to NHSP"}, {"issue": "Candidate does not appear to book", "resolution": "add candidate profile, correct assignment, checklist is in date"}], "roster_link": "", "contacts": [{"name": "Jo Laker", "title": "Matron", "dept": "Main Theatres", "email": "joannelaker@nhs.net", "phone": "07388991383", "lastContacted": ""}, {"name": "Tanya Mcintyre", "title": "Lead ODP", "dept": "Main Theatres", "email": "Tanya.McIntyre@whht.nhs.uk", "phone": "07393870773", "lastContacted": ""}, {"name": "Michael Lewis", "title": "B7 Scrub", "dept": "Obs & Gyane Theatres", "email": "michael.lewis23@nhs.net", "phone": "07703497804", "lastContacted": ""}, {"name": "Jo Mills", "title": "Temporary Staffing Manager", "dept": "Temporary Staffing", "email": "johanna.mills@whht.nhs.uk", "phone": "", "lastContacted": ""}, {"name": "Louise", "title": "B7 Recovery", "dept": "Main Theatres", "email": "", "phone": "07768156526", "lastContacted": ""}], "rates": [{"trust": "West Herfordshire", "hospital": "Watford", "card": "CB6 - The (Care Providers )", "ward": "Main Theatres", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "cs": 41.0, "md": 4.45}], "personalRates": []}, {"name": "Luton & Bedford", "area": "Hertfordshire", "pps": 39.615, "total": 890, "weekly": [13, 23, 20, 6, 16, 23, 17, 19, 22, 18, 29, 34, 37, 35, 48, 0], "processes": [{"action": "Pay by Timesheet", "day": "", "time": ""}, {"action": "Joshua Tanimowo", "day": "", "time": ""}, {"action": "Chris Bwalya", "day": "", "time": ""}, {"action": "Lyn Chiwenga", "day": "", "time": ""}, {"action": "Parmanan Paggo", "day": "", "time": ""}, {"action": "Rachel Ofole", "day": "", "time": ""}, {"action": "Sonny Cas", "day": "", "time": ""}, {"action": "Ritchie Cabural", "day": "", "time": ""}, {"action": "Edward Brooks", "day": "", "time": ""}], "rota": [{"name": "Chris Davies", "spec": "Anae"}, {"name": "Daniel Pakbonyan", "spec": "Anae"}, {"name": "Joshua Tanimowo", "spec": "Anae"}, {"name": "Chris Bwalya", "spec": "Anae"}, {"name": "Lyn Chiwenga", "spec": "Anae"}, {"name": "Edward Brooks", "spec": "Anae/Scrub"}, {"name": "Edward Appiah", "spec": "Anae"}, {"name": "Farzad Sajjad", "spec": "Anae"}, {"name": "Josiah Nyabango", "spec": "Scrub"}, {"name": "Raheela Shraf", "spec": "Scrub"}, {"name": "Aisha Ramadham", "spec": "Scrub"}], "issues": [{"issue": "Jyothi", "resolution": "Jyothi"}, {"issue": "Josiah Nyabango", "resolution": "Josiah Nyabango"}, {"issue": "Raheela Shraf", "resolution": "Raheela Shraf"}, {"issue": "Aisha Ramadham", "resolution": "Aisha Ramadham"}], "roster_link": "https://BEDFT.allocate-cloud.co.uk/BankStaffBEDFTLIVE/", "contacts": [], "rates": [{"trust": "Bedfordshire", "hospital": "Luton", "card": "CB6 - The (Day Webster Ltd)", "ward": "Theatres - L&DH", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "cs": 41.0, "md": 4.45}, {"trust": "Bedfordshire", "hospital": "Bedford", "card": "CB6 - The (Day Webster Ltd)", "ward": "Theatres - Bedford", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "cs": 41.0, "md": 4.45}], "personalRates": []}, {"name": "Royal Berkshire", "area": "Surrey", "pps": 38, "total": 57, "weekly": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], "processes": [{"action": "Release shifts for RBH by NHSP emails", "day": "", "time": ""}, {"action": "If released after 7am that day it will be processed the following day", "day": "", "time": ""}], "rota": [], "issues": [], "roster_link": "", "contacts": [{"name": "Lisa Tinker", "title": "Lead ODP", "dept": "Main Theatres", "email": "lisa.tinker@nhs.net", "phone": "07967730177", "lastContacted": ""}, {"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "rsc-tr.staffbank@nhs.net", "phone": "01493571122", "lastContacted": ""}, {"name": "Khader", "title": "Theatre Manager", "dept": "Main Theatres", "email": "", "phone": "07850932324", "lastContacted": ""}, {"name": "Staff Bank", "title": "General Contact", "dept": "Temporary Staffing", "email": "rf-tr.tsbookings@nhs.net", "phone": "02078302065", "lastContacted": "2026-01-13"}, {"name": "Richard", "title": "Staff Bank Co-ordinator", "dept": "Temporary Staffing", "email": "", "phone": "", "lastContacted": ""}], "rates": [{"trust": "Royal Surrey", "hospital": "Royal Surrey", "card": "CB6 - The (Day Webster Ltd)", "ward": "Theatres - RSCH", "pd": 29.7, "pn": 31.68, "ps": 31.68, "cd": 33.5, "cn": 35.0, "cs": 35.0, "md": 3.8}, {"trust": "Royal Berkshire", "hospital": "Royal Berkshire", "card": "CB6 - The PRC Rate NEW", "ward": "Main Theatres - RBH", "pd": 26.72, "pn": 31.67, "ps": 33.65, "cd": 31.17, "cn": 36.0, "cs": 41.0, "md": 4.45}, {"trust": "Sussex", "hospital": "Princess Royal", "card": "CB6 - The Esc (Day Webster)", "ward": "Theatres - PRH", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "cs": 34.0, "md": 4.3}, {"trust": "Sussex", "hospital": "Royal Sussex County", "card": "CB6 - The Esc (Day Webster)", "ward": "Theatres RSCH", "pd": 29.7, "pn": 29.7, "ps": 29.7, "cd": 34.0, "cn": 34.0, "cs": 34.0, "md": 4.3}, {"trust": "Barts Health", "hospital": "Royal London (Inner)", "card": "CB5 - The (Care Providers)", "ward": "Theatres - Royal London", "pd": 22.76, "pn": 24.74, "ps": 29.69, "cd": 26.94, "cn": 29.45, "cs": 35.11, "md": 4.18}, {"trust": "Barts Health", "hospital": "Royal London (Inner)", "card": "CB6 - Theatres (Care Providers )", "ward": "Theatres - Royal London", "pd": 26.72, "pn": 31.67, "ps": 34.64, "cd": 32.8, "cn": 37.03, "cs": 42.67, "md": 6.08}], "personalRates": [{"name": "Martin Rowan", "spec": "ODP", "rate": 25.0}]}, {"name": "Cromwell", "area": "Private", "pps": 20.33, "total": 90, "weekly": [3, 3, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 2, 4, 0], "processes": [], "rota": [], "issues": [], "roster_link": "", "contacts": [], "rates": [], "personalRates": []}, {"name": "Spa Medica", "area": "Private", "pps": 47.5, "total": 321, "weekly": [1, 0, 5, 0, 0, 23, 24, 25, 20, 20, 19, 19, 16, 10, 9, 0], "processes": [{"action": "Pay by Timesheet", "day": "", "time": ""}], "rota": [], "issues": [{"issue": "No expected issues", "resolution": "Charmain Reis"}, {"issue": "Ruth Magambo", "resolution": "Ruth Magambo"}, {"issue": "Eugene Igwe", "resolution": "Eugene Igwe"}, {"issue": "Catherine Onyeama", "resolution": "Catherine Onyeama"}, {"issue": "Jonathan Montoya", "resolution": "Jonathan Montoya"}, {"issue": "Luigi Donate", "resolution": "Luigi Donate"}, {"issue": "Edward Brooks", "resolution": "Edward Brooks"}], "roster_link": "", "contacts": [{"name": "Brad Sims", "title": "Area Manager - South East", "dept": "Mangment", "email": "brad.sims@spamedica.co.uk", "phone": "07434784522", "lastContacted": ""}, {"name": "Nadine Mckee", "title": "Area Manager - South West", "dept": "Mangment", "email": "nadine.mckee@spamedica.co.uk", "phone": "07749721658", "lastContacted": ""}, {"name": "Shirley", "title": "Hospital Manager - Colchester", "dept": "Theatres", "email": "", "phone": "07947662808", "lastContacted": ""}, {"name": "Natalie Gregory", "title": "Hospital Manager - Chelmsford", "dept": "Theatres", "email": "natalie.gregory@spamedica.co.uk", "phone": "07842403170", "lastContacted": ""}, {"name": "Ken keen", "title": "Hospital Manager - Epsom", "dept": "Theatres", "email": "kenneth.keen@spamedica.co.uk", "phone": "07955439588", "lastContacted": ""}, {"name": "Sarah Mcmanus", "title": "Hospital Director - South East", "dept": "Management", "email": "", "phone": "07874867914", "lastContacted": ""}, {"name": "Emma Tisma", "title": "Director of Actvity", "dept": "Mangment", "email": "emma.tisma@spamedica.co.uk", "phone": "07779097105", "lastContacted": ""}], "rates": [], "personalRates": []}];
var ROTA_DATA={"weeks": {"2026-01-19": {"dates": ["Mon 19 Jan", "Tue 20 Jan", "Wed 21 Jan", "Thu 22 Jan", "Fri 23 Jan", "Sat 24 Jan", "Sun 25 Jan"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["U", "U", "", "", "U", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["U", "U", "U", "U", "", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "U", "U"]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["MSE", "", "MSE", "U", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "U", "MSE", "U", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["", "Lewisham", "Homerton", "Lewisham", "", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Homerton", "Lewisham", "Lewisham", "Lewisham", "Homerton", "", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["Lewisham", "Lewisham", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["", "", "", "Lewisham", "Lewisham", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["Lewisham", "", "", "", "", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "Homerton", "", "", "", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Homerton", "BHT", "BHT", "BHT", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "Homerton", "", "Homerton", "Homerton", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["Homerton", "Homerton", "", "", "Homerton", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["", "Lewisham", "Homerton", "Lewisham", "", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["Homerton", "", "RNOH", "", "RNOH", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Homerton", "Lewisham", "Lewisham", "Lewisham", "Homerton", "", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["", "Homerton", "", "Homerton", "Homerton", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["U", "U", "Homerton", "U", "U", "", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "", "", "Homerton", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["Homerton", "", "", "Homerton", "", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["Homerton", "", "", "", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "Homerton", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["U", "Homerton", "U", "U", "Homerton", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["U", "U", "", "Homerton", "", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Homerton", "BHT", "BHT", "BHT", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "Homerton", "", "Homerton", "Homerton", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["MSE", "", "MSE", "Homerton", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "Homerton", "MSE", "Homerton", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["U", "BHT", "BHT", "BHT", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["U", "U", "U", "U", "U", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["", "", "Royal Surrey", "Royal Surrey", "", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["Royal Surrey", "U", "Royal Surrey", "Royal Surrey", "U", "", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["U", "", "U", "U", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["", "East Surrey", "East Surrey", "", "", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["East Surrey", "East Surrey", "", "U", "", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["", "QVH", "QVH", "QVH", "QVH", "QVH", ""]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["Luton", "Luton", "", "", "", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["Luton", "Luton", "U", "Luton", "Luton", "", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "", "Luton", "Luton", "", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "Luton", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["U", "U", "U", "U", "U", "U", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["Ramsay", "", "", "Ramsay", "Ramsay", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "Spa Medica", "Spa Medica", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}]}}, "2026-01-26": {"dates": ["Mon 26 Jan", "Tue 27 Jan", "Wed 28 Jan", "Thu 29 Jan", "Fri 30 Jan", "Sat 31 Jan", "Sun 01 Feb"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["U", "U", "", "", "", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["U", "", "U", "U", "", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "U", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["MSE", "", "MSE", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "U", "U", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "MSE", "MSE", "", "", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["Lewisham", "Lewisham", "", "", "Homerton", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "Lewisham", "Lewisham", "", "Homerton", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["", "Lewisham", "Lewisham", "Homerton", "Lewisham", "", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["Lewisham", "", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["", "", "", "Lewisham", "", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["Lewisham", "", "", "Lewisham", "", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "Homerton", "Homerton", "", "", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "BHT", "BHT", "", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "Homerton", "Homerton", "Homerton", "", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["Lewisham", "Lewisham", "", "", "Homerton", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["Homerton", "Homerton", "", "", "", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "Lewisham", "Lewisham", "", "Homerton", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["", "Homerton", "", "RNOH", "RNOH", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["", "Lewisham", "Lewisham", "Homerton", "Lewisham", "", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["", "Homerton", "Homerton", "", "Homerton", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["Homerton", "", "", "Homerton", "Homerton", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["", "Homerton", "Homerton", "", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "U", "U", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["U", "U", "Homerton", "Homerton", "U", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "BHT", "BHT", "", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "Homerton", "Homerton", "Homerton", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["MSE", "", "MSE", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "Homerton", "Homerton", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "", "BHT", "U", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["U", "BHT", "BHT", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["U", "U", "", "U", "U", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["", "", "Royal Surrey", "", "", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["", "Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["U", "U", "U", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["U", "", "U", "", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["Crawley", "", "", "East Surrey", "East Surrey", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["", "", "", "", "East Surrey", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["East Surrey", "East Surrey", "U", "U", "East Surrey", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["", "", "", "", "Luton", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "Luton", "Luton", "Luton", "", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "Luton", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["", "Luton", "", "", "Luton", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["U", "U", "U", "U", "U", "", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["U", "", "", "U", "U", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["", "", "", "", "", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}]}}, "2026-02-02": {"dates": ["Mon 02 Feb", "Tue 03 Feb", "Wed 04 Feb", "Thu 05 Feb", "Fri 06 Feb", "Sat 07 Feb", "Sun 08 Feb"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["U", "U", "", "", "", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["U", "U", "", "U", "", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["U", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["U", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Homerton", "Homerton", "Lewisham", "Lewisham", "Lewisham", "", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["Lewisham", "Lewisham", "", "Lewisham", "", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["", "", "", "Lewisham", "", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "Homerton", "", "", "Homerton", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["Lewisham", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Homerton", "", "", "Homerton", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["BHT", "BHT", "", "Homerton", "BHT", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["Homerton", "Homerton", "", "", "", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["RNOH", "", "", "", "", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Homerton", "Homerton", "Lewisham", "Lewisham", "Lewisham", "", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["", "", "U", "U", "Homerton", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "", "Homerton", "", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["", "Homerton", "", "", "", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["Homerton", "", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["", "Homerton", "", "", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "U", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["", "Homerton", "", "Homerton", "", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Homerton", "", "", "Homerton", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["BHT", "BHT", "", "Homerton", "BHT", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["Homerton", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "U", "", "BHT", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["U", "", "", "U", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["U", "U", "U", "U", "Royal Surrey", "", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["U", "", "", "", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["East Surrey", "", "East Surrey", "", "", "", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["", "U", "", "U", "", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["CareF", "QVH", "QVH", "QVH", "QVH", "", "QVH"]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["", "Luton", "", "Luton", "Luton", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "Luton", "Luton", "Luton", "", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["U", "U", "U", "U", "U", "", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["", "", "", "", "", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["BHT", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "BANH", "", "", "", ""]}]}}, "2026-02-09": {"dates": ["Mon 09 Feb", "Tue 10 Feb", "Wed 11 Feb", "Thu 12 Feb", "Fri 13 Feb", "Sat 14 Feb", "Sun 15 Feb"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "U", "", "", "U", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["U", "U", "", "", "", "U", "U"]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["U", "U", "", "U", "U", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "", "U", "", "MSE", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["MSE", "", "", "MSE", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "", "MSE", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "", "", "", "MSE", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "Lewisham", "Lewisham", "", "Lewisham", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "", "Homerton", "", "", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["", "Lewisham", "Lewisham", "Lewisham", "Lewisham", "", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["Lewisham", "Lewisham", "", "Lewisham", "Lewisham", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["Lewisham", "", "", "", "Lewisham", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "", "Lewisham", "", "MSE", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["BHT", "", "BHT", "BHT", "", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["", "Lewisham", "", "", "Lewisham", "", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "Lewisham", "Lewisham", "", "Lewisham", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "Homerton", "", "", "Homerton", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "", "Homerton", "", "", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["Homerton", "", "RNOH", "RNOH", "RNOH", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["", "Lewisham", "Lewisham", "Lewisham", "Lewisham", "", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["U", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["", "Homerton", "Homerton", "", "", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["Homerton", "Homerton", "", "", "Homerton", "", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["", "Homerton", "", "", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["Homerton", "Homerton", "", "Homerton", "Homerton", "", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "U", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["", "U", "U", "", "U", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["BHT", "", "BHT", "BHT", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["MSE", "", "", "MSE", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "", "MSE", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "U", "", "U", "U", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["U", "U", "U", "U", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["U", "U", "", "", "U", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "U", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["", "Royal Surrey", "Royal Surrey", "", "Royal Surrey", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["U", "U", "U", "U", "Royal Surrey", "", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["U", "", "", "U", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["", "East Surrey", "", "East Surrey", "", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["", "U", "U", "U", "U", "U", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["East Surrey", "", "", "", "", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["", "East Surrey", "East Surrey", "", "East Surrey", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["CareF", "QVH", "QVH", "QVH", "CareF", "", "QVH"]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["Luton", "", "Luton", "", "", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "Luton", "Luton", "Luton", "Luton", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["Luton", "", "Luton", "", "", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["U", "U", "", "U", "U", "", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["U", "", "", "", "", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["Ramsay", "Ramsay", "", "", "Ramsay", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "", "", "", "Spa Medica", "Spa Medica"]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["Spa Medica", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}]}}, "2026-02-16": {"dates": ["Mon 16 Feb", "Tue 17 Feb", "Wed 18 Feb", "Thu 19 Feb", "Fri 20 Feb", "Sat 21 Feb", "Sun 22 Feb"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "", "", "U", "U", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["U", "U", "U", "", "U", "U", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "U", "", "U", "QE", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["U", "", "", "", "U", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "U", "", "MSE", "MSE", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "", "", "MSE", "", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "Lewisham", "Lewisham", "", "Lewisham", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "QE", "Homerton", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Lewisham", "Lewisham", "", "Homerton", "", "", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "Lewisham", "", "Lewisham", "QE", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["", "", "", "QE", "", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["Lewisham", "", "", "", "Lewisham", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "", "", "", "Homerton", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "Lewisham", "", "MSE", "MSE", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["Homerton", "", "U", "Homerton", "Homerton", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["QE", "", "", "", "Lewisham", "", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "Lewisham", "Lewisham", "", "Lewisham", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "", "", "Homerton", "Homerton", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "QE", "Homerton", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["", "", "U", "", "", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Lewisham", "Lewisham", "", "Homerton", "", "", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["", "U", "U", "U", "MSE", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["", "U", "U", "U", "U", "", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "U", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "BHT", "", "", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["Homerton", "", "", "", "", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["", "Homerton", "Homerton", "Homerton", "U", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["U", "MSE", "", "MSE", "U", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["Homerton", "", "U", "Homerton", "Homerton", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "U", "U", "U", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["U", "U", "U", "U", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["U", "U", "", "U", "U", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["", "", "Royal Surrey", "Royal Surrey", "", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["", "", "U", "", "", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["", "U", "U", "U", "Royal Surrey", "", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["East Surrey", "", "East Surrey", "", "", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["", "", "East Surrey", "U", "East Surrey", "", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "Crawley", "East Surrey", "", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["East Surrey", "", "", "", "", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["East Surrey", "U", "", "U", "East Surrey", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["CareF", "QVH", "QVH", "", "", "QVH", "QVH"]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["", "U", "U", "U", "U", "", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "U", "U", "", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["Ramsay", "Ramsay", "", "", "Ramsay", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "", "Spa Medica", "Spa Medica", ""]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}]}}, "2026-02-23": {"dates": ["Mon 23 Feb", "Tue 24 Feb", "Wed 25 Feb", "Thu 26 Feb", "Fri 27 Feb", "Sat 28 Feb", "Sun 01 Mar"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["U", "U", "U", "U", "", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["", "U", "U", "", "", "U", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "U", "", "U", "U", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["U", "", "U", "", "U", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "", "", "MSE", "MSE", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Lewisham", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["", "Homerton", "Lewisham", "Homerton", "Homerton", "", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["", "", "", "Lewisham", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "Lewisham", "", "Lewisham", "Lewisham", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["Lewisham", "", "", "", "", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "", "BHT", "Lewisham", "", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "", "", "MSE", "MSE", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "", "Lewisham", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "BHT", "", "BHT", "BHT", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["Lewisham", "", "U", "U", "U", "", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Lewisham", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["", "RNOH", "", "", "RNOH", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["", "Homerton", "Lewisham", "Homerton", "Homerton", "", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["", "U", "U", "U", "U", "", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "", "", "U", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "", "Homerton", "", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "Homerton", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["", "Homerton", "Homerton", "Homerton", "U", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["U", "U", "MSE", "MSE", "U", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "", "Lewisham", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "BHT", "", "BHT", "BHT", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "U", "", "U", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["U", "U", "", "U", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["U", "U", "", "U", "U", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["Royal Surrey", "", "", "", "", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["U", "U", "U", "", "U", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["", "", "Royal Surrey", "Royal Surrey", "", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["", "U", "U", "U", "Royal Surrey", "", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["", "", "", "East Surrey", "", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["Crawley", "Crawley", "Crawley", "U", "East Surrey", "", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "Crawley", "Crawley", "", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["East Surrey", "East Surrey", "U", "U", "East Surrey", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["", "QVH", "QVH", "QVH", "QVH", "QVH", ""]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["Luton", "Luton", "", "Luton", "", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "Luton", "Luton", "Luton", "", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["U", "U", "U", "", "U", "", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["", "", "U", "U", "", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["", "Ramsay", "", "Ramsay", "Ramsay", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["", "Spa Medica", "Spa Medica", "", "", "Spa Medica", ""]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}]}}, "2026-03-02": {"dates": ["Mon 02 Mar", "Tue 03 Mar", "Wed 04 Mar", "Thu 05 Mar", "Fri 06 Mar", "Sat 07 Mar", "Sun 08 Mar"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "U", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "U", "U", "U", "", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "", "U", "U", "MSE", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["", "MSE", "MSE", "", "", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["Homerton", "Lewisham", "", "", "Lewisham", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["", "", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Lewisham", "Homerton", "Homerton", "Homerton", "", "Lewisham", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["", "", "", "Lewisham", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "Lewisham", "Lewisham", "Lewisham", "", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "Homerton", "Homerton", "", "", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "", "Lewisham", "Lewisham", "MSE", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "Lewisham", "Lewisham", "Lewisham", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["Homerton", "Lewisham", "", "", "Lewisham", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["", "", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["RNOH", "", "RNOH", "RNOH", "", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Lewisham", "Homerton", "Homerton", "Homerton", "", "Lewisham", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["MSE", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["U", "U", "U", "U", "U", "U", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "", "U", "", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["", "", "", "Homerton", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["Homerton", "", "Homerton", "Homerton", "", "", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "Homerton", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["U", "U", "MSE", "MSE", "U", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["Lewisham", "Lewisham", "Lewisham", "Lewisham", "Lewisham", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["", "", "Homerton", "Homerton", "Homerton", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["", "MSE", "MSE", "", "", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "U", "", "U", "U", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["", "U", "U", "", "", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["", "", "", "", "OXF", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["U", "U", "", "U", "", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["U", "U", "U", "U", "", "", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["U", "U", "", "U", "U", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["", "East Surrey", "", "East Surrey", "East Surrey", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["East Surrey", "Crawley", "East Surrey", "East Surrey", "Crawley", "", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["East Surrey", "", "East Surrey", "Crawley", "Crawley", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["East Surrey", "East Surrey", "U", "U", "East Surrey", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["", "Luton", "Luton", "Luton", "Luton", "Luton", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["Luton", "Luton", "", "", "", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "Luton", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "Luton", "Luton", "Luton", "", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["U", "", "U", "U", "", "", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["U", "", "U", "U", "U", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["", "", "", "Ramsay", "Ramsay", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["U", "U", "", "U", "U", "", ""]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "Spa Medica", "", "Spa Medica", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}]}}, "2026-03-09": {"dates": ["Mon 09 Mar", "Tue 10 Mar", "Wed 11 Mar", "Thu 12 Mar", "Fri 13 Mar", "Sat 14 Mar", "Sun 15 Mar"], "rotas": {"MSE": [{"n": "Alex Amponsah", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "U", "", "U", "U", "", ""]}, {"n": "Bimbola Oduyemi", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["MSE", "MSE", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "U", "U", "U", "U", "", ""]}, {"n": "Evelyn Josephine kabba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Florah Mudeke", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Gina-Oana Tilvic", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josiah Nyabango", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Melody Mamire", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Phillip Mwaijumba", "s": "Scrub", "c": ["MSE", "MSE", "MSE", "MSE", "MSE", "", ""]}, {"n": "Sandra Maria Duarte-Botello", "s": "Scrub", "c": ["U", "", "", "U", "U", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "MSE", "", "", "MSE", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}, {"n": "Yohannes Adamu", "s": "ODP", "c": ["", "MSE", "MSE", "MSE", "MSE", "", ""]}], "Lewisham & QEH": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Lewisham", "", "", "", "", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Homerton", "", "", "", "", "Homerton", ""]}, {"n": "Blessing Dododawa", "s": "Scrub", "c": ["Lewisham", "", "", "", "", "", ""]}, {"n": "Comfort Raji", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Ikeh", "s": "Scrub", "c": ["", "Lewisham", "Lewisham", "Lewisham", "Lewisham", "", ""]}, {"n": "Isa Makama Muazu", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Maureen Chukwuma", "s": "Recovery", "c": ["", "", "", "Lewisham", "Lewisham", "", ""]}, {"n": "Maxmore Nyazema", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Mercy Afolabi", "s": "Scrub", "c": ["", "", "", "", "Homerton", "", ""]}, {"n": "Novlette Panton", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Sunday Olaniyan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Olutoyin Latinwo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Stephen Alake", "s": "ODP", "c": ["", "MSE", "", "", "MSE", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["", "Lewisham", "QE", "QE", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["U", "", "U", "", "U", "", ""]}, {"n": "Vimbayi Mary Mapolisa", "s": "Recovery", "c": ["", "U", "", "", "U", "U", ""]}], "Homerton": [{"n": "Abidemi Layo Jegede", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Alex Acheampong", "s": "ODP", "c": ["", "Homerton", "", "Homerton", "Homerton", "", ""]}, {"n": "Augustina Akujobi", "s": "Scrub", "c": ["Lewisham", "", "", "", "", "", ""]}, {"n": "Babajide Fasuji", "s": "Scrub", "c": ["", "", "RNOH", "RNOH", "", "", ""]}, {"n": "Bibi Sakilla Jugon", "s": "ODP", "c": ["Homerton", "", "", "", "", "Homerton", ""]}, {"n": "Christopher Bwalya", "s": "ODP", "c": ["", "", "Homerton", "Homerton", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["U", "U", "", "", "", "", ""]}, {"n": "Edward Owusu-Appiah", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ethel Mandega", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Genn Balaaldia Agduyeng", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "John Arthur", "s": "ODP", "c": ["", "Homerton", "Homerton", "Homerton", "Homerton", "Homerton", ""]}, {"n": "Librada Tagelo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Mahir Ahmed", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "Homerton", ""]}, {"n": "Patrick Adutwim", "s": "ODP", "c": ["Homerton", "Homerton", "Homerton", "Homerton", "Homerton", "Homerton", ""]}, {"n": "Rayven-Renee Arboine", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["", "", "MSE", "MSE", "MSE", "Homerton", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["U", "U", "MSE", "MSE", "U", "", ""]}, {"n": "Simon Broughton", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["", "Lewisham", "QE", "QE", "", "", ""]}, {"n": "Tanya Williams", "s": "Scrub", "c": ["U", "", "U", "", "U", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["MSE", "MSE", "", "MSE", "MSE", "", ""]}], "Barts": [{"n": "David Joy", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Janet Balacanao", "s": "Chemo", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["U", "U", "U", "U", "U", "", ""]}, {"n": "Moses Chika Megwaonye", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Raheela Ashraf", "s": "Scrub", "c": ["", "", "U", "", "U", "U", ""]}, {"n": "Tamara Boswell", "s": "Scrub", "c": ["", "U", "QE", "QE", "", "", ""]}, {"n": "Willard Mandaza", "s": "ODP", "c": ["U", "U", "", "U", "U", "", ""]}], "Royal Surrey": [{"n": "Adebukola Akintayo", "s": "ODP", "c": ["", "Royal Surrey", "", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Aleksandra Lacey", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Carl Wheat", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Fanol Gjata", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Josephloid veloso", "s": "Scrub", "c": ["", "Royal Surrey", "Royal Surrey", "Royal Surrey", "Royal Surrey", "", ""]}, {"n": "Kaif Rashid", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lovie Pascual", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Ronan Perez", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Roseline Emmanuel", "s": "Scrub", "c": ["", "", "U", "U", "U", "U", ""]}, {"n": "Tirett Millard", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Uzoma Akosim", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Visshal Roy Issuree", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "East Surrey": [{"n": "Christine Gikurumi", "s": "Scrub", "c": ["East Surrey", "", "East Surrey", "", "", "", ""]}, {"n": "Diosdado B Wagan", "s": "Scrub", "c": ["Crawley", "East Surrey", "Crawley", "East Surrey", "East Surrey", "", ""]}, {"n": "Jovanie Santos", "s": "ODP", "c": ["U", "", "", "", "East Surrey", "", ""]}, {"n": "Marlon Orio", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Paivi Hannele Raulamo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Silvestre Salalima", "s": "Scrub", "c": ["East Surrey", "East Surrey", "U", "U", "East Surrey", "", ""]}], "QVH": [{"n": "Gloria Tawonezvi", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Patrick Mitchell", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Luton & Bedford": [{"n": "Aaron Gascon", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Abdul-Fatau Musah", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "", ""]}, {"n": "Aisha Ramadhan", "s": "scrub", "c": ["Luton", "Luton", "Luton", "", "Luton", "Luton", ""]}, {"n": "Andrew P Crawford", "s": "ODP", "c": ["Luton", "Luton", "", "Luton", "Luton", "", ""]}, {"n": "Christopher Davies", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Daniel Pakbonyan", "s": "ODP", "c": ["Luton", "Luton", "", "", "", "", ""]}, {"n": "Diego Sevilla", "s": "ODP", "c": ["", "", "Luton", "Luton", "Luton", "", ""]}, {"n": "Joshua Tanimowo", "s": "ODP", "c": ["Luton", "Luton", "Luton", "Luton", "Luton", "Luton", ""]}, {"n": "Mohammadreza Mohammadi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}], "Watford": [{"n": "Mahir Ahmed", "s": "ODP", "c": ["U", "U", "U", "U", "U", "U", ""]}], "Ramsay": [{"n": "Jovanie Santos", "s": "ODP", "c": ["U", "", "", "", "U", "", ""]}, {"n": "Manuel Rodriguez", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Maudy Hoyi", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Rinah Bheekharry", "s": "SFA", "c": ["", "", "Ramsay", "Ramsay", "Ramsay", "", ""]}], "Spa Medica": [{"n": "Charmain Yvette Reis", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Eduard Constantin Batog", "s": "Scrub", "c": ["U", "U", "", "", "", "", ""]}, {"n": "Eugene Igwe", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "George Cobbina", "s": "TSW", "c": ["", "", "", "", "", "", ""]}, {"n": "John Gerad Mcdonnell", "s": "Recovery", "c": ["", "", "", "", "", "", ""]}, {"n": "Jonathan Montoya Rendon", "s": "Scrub", "c": ["Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Lena O'Leary", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Leonida Untalan White", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Lydie Gam-mackitta", "s": "Scrub", "c": ["Spa Medica", "", "Spa Medica", "Spa Medica", "Spa Medica", "", ""]}, {"n": "Peninnah Kabura Wairia", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}, {"n": "Ruth Asimwe Magambo", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Royal Berkshire": [{"n": "Benjamin Davis", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Lauren Amy Orgar", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Martin Rowan", "s": "ODP", "c": ["", "", "", "", "", "", ""]}, {"n": "Pamela Nozipo Ncube", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}], "Cromwell": [{"n": "Michelle Lim", "s": "Scrub", "c": ["", "", "", "", "", "", ""]}]}}}, "weekKeys": ["2026-01-19", "2026-01-26", "2026-02-02", "2026-02-09", "2026-02-16", "2026-02-23", "2026-03-02", "2026-03-09"], "trustSites": {"MSE": ["Southend", "Broomfield", "Basildon"], "Lewisham & QEH": ["Lewisham", "QEH"], "Homerton": ["Homerton"], "Barts": ["St Barts", "Royal London", "Whipps Cross", "Newham"], "Royal Surrey": ["Royal Surrey"], "East Surrey": ["East Surrey", "Crawley"], "QVH": ["QVH", "DVH"], "Luton & Bedford": ["Luton", "Bedford"], "Watford": ["Watford", "St Albans"], "Ramsay": ["Ramsay"], "Spa Medica": ["Spa Medica"], "Royal Berkshire": ["Royal Berkshire"], "Cromwell": ["Cromwell"]}}
var TRUST_SITES=ROTA_DATA.trustSites;
var rotaWkIdx=ROTA_DATA.weekKeys.length-1;
function getRotaWkKey(){
// Single source of truth: always matches shift entry week
return wKey(wkOff);
}
function getRotaWk(){
var wk=getRotaWkKey();
ensureWeekInRota(wk);
var data=ROTA_DATA.weeks[wk];
return{dates:data.dates||[],rotas:data.rotas||{}};
}

var DAYS=['Mon','Tue','Wed','Thu','Fri','Sat','Sun'];
var wkOff=0,sd={},ac=null,dfi=-1,dm=[],ddPicking=false,saveT=null;
try{var _s=localStorage.getItem('crm5');if(_s)sd=JSON.parse(_s);}catch(e){}

function esc(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function gMon(o){var d=new Date();d.setHours(0,0,0,0);d.setDate(d.getDate()-((d.getDay()+6)%7)+o*7);return d;}
function wKey(o){return gMon(o).toISOString().slice(0,10);}
function fWk(o){var m=gMon(o),e=new Date(m);e.setDate(m.getDate()+6);var op={day:'numeric',month:'short'};return m.toLocaleDateString('en-GB',op)+'\u2013'+e.toLocaleDateString('en-GB',op);}
function fDH(o,di){var m=gMon(o),d=new Date(m);d.setDate(m.getDate()+di);var t=new Date();t.setHours(0,0,0,0);var col=d.getTime()===t.getTime()?'color:var(--bl)':'';return '<span style="'+col+'">'+DAYS[di]+'</span><br><span style="font-size:10px;color:var(--t3);font-weight:400">'+d.getDate()+'/'+(d.getMonth()+1)+'</span>';}
function gWD(){var k=wKey(wkOff);if(!sd[k])sd[k]={};return sd[k];}
function gI(r,d){return document.querySelector('.ci[data-r="'+r+'"][data-d="'+d+'"]');}

function chWk(dir){
if(dir===0)wkOff=0;else wkOff+=dir;
var lbl=fWk(wkOff);
document.getElementById('wkl').textContent=lbl;
var l2=document.getElementById('wkl2');if(l2)l2.textContent=lbl;
document.getElementById('wb0').classList.toggle('on',wkOff===0);
var w1=document.getElementById('wb1');if(w1)w1.classList.toggle('on',wkOff===0);
rTable();rSum();rDash();
}

function rTable(){
var wd=gWD();
var _sq=(document.getElementById('se-search')||{value:''}).value;
document.getElementById('sth').innerHTML='<tr><th style="width:172px"><div class="thi" style="display:flex;align-items:center;gap:6px">Candidate<input type="text" id="se-search" placeholder="Search\u2026" oninput="rTable()" style="margin-left:auto;padding:3px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--bg);color:var(--tx);outline:none;font-size:11px;width:110px"></div></th>'+
DAYS.map(function(_,i){return '<th style="width:110px"><div class="thi">'+fDH(wkOff,i)+'</div></th>';}).join('')+
'<th style="width:50px"><div class="thi" style="text-align:right">Total</div></th></tr>';
var rows='';
// Restore search value after thead rebuild
var _srch=document.getElementById('se-search');
if(_srch&&_sq){_srch.value=_sq;_srch.focus();_srch.setSelectionRange(_sq.length,_sq.length);}
var _seQ=_sq.toLowerCase().trim();
for(var ri=0;ri<C.length;ri++){if(C[ri]&&C[ri].ac==='Inactive')continue;
if(_seQ&&!(C[ri].n||'').toLowerCase().includes(_seQ))continue;
var c=C[ri],row=wd[ri]||{},tot=0,cells='';
for(var di=0;di<7;di++){
var v=row[di]||'',f=v?' f':'';
tot+=(v?1:0);
cells+='<td><input class="ci'+f+'" data-r="'+ri+'" data-d="'+di+'" value="'+esc(v)+'" placeholder="\u2014" autocomplete="off" spellcheck="false" onfocus="oFoc(event)" oninput="oInp(event)" onkeydown="oKey(event)" onblur="oBlu(event)"></td>';
}
var ts=tot>0?'color:var(--bl);font-weight:500':'color:var(--t3)';
rows+='<tr><td><span class="cn">'+esc(c.n)+'<span class="cs"> '+esc(c.s)+'</span></span></td>'+cells+'<td style="text-align:right;padding-right:8px;font-size:12px;'+ts+'">'+(tot||'')+'</td></tr>';
}
document.getElementById('stb').innerHTML=rows||'<tr><td colspan="9" style="padding:20px;text-align:center;color:var(--t3);font-size:13px">No candidates match &ldquo;'+esc(_seQ)+'&rdquo;</td></tr>';
rFoot();uMet();
}

function rFoot(){
var wd=gWD(),dt=DAYS.map(function(_,di){var t=0;Object.keys(wd).forEach(function(ri){if((wd[ri]||{})[di])t++;});return t;}),g=dt.reduce(function(a,b){return a+b;},0);
document.getElementById('stf').innerHTML='<tr class="trow"><td style="color:var(--t2);font-weight:400;font-size:11px">Shifts/day</td>'+dt.map(function(t){return '<td style="text-align:center">'+(t||'')+'</td>';}).join('')+'<td style="text-align:right;padding-right:8px">'+(g||'')+'</td></tr>';
}

function uMet(){
var wd=gWD(),tot=0,hs=new Set(),cs=new Set(),mg=0;
Object.keys(wd).forEach(function(ri){Object.keys(wd[ri]).forEach(function(di){var h=wd[ri][di];if(!h)return;tot++;hs.add(h);cs.add(ri);mg+=getHospPPS(h);});});
document.getElementById('m0').textContent=tot;
document.getElementById('m1').textContent=hs.size;
document.getElementById('m2').textContent=cs.size;
document.getElementById('m3').textContent=mg>0?'\u00a3'+Math.round(mg).toLocaleString():'\u2014';
}

function oFoc(e){var i=e.target;i.select();openDD(i);}
function oInp(e){openDD(e.target);}

function oBlu(e){
var i=e.target,ri=+i.dataset.r,di=+i.dataset.d;
setTimeout(function(){
if(ddPicking)return;
/* Only commit if the value exactly matches a valid hospital */
var v=i.value.trim();
var valid=v&&A.some(function(h){return h.toLowerCase()===v.toLowerCase();});
if(valid){
/* normalise capitalisation to match canonical name */
var canonical=A.find(function(h){return h.toLowerCase()===v.toLowerCase();});
commit(i,ri,di,canonical);
} else {
/* invalid \u2014 clear the cell and flash the input red briefly */
commit(i,ri,di,'');
if(v){i.style.background='var(--redbg,#faeaea)';setTimeout(function(){i.style.background='';},600);}
}
closeDD();
},160);
}

function oKey(e){
var i=e.target,ri=+i.dataset.r,di=+i.dataset.d;
if(e.key==='ArrowDown'){e.preventDefault();mDF(1);}
else if(e.key==='ArrowUp'){e.preventDefault();mDF(-1);}
else if(e.key==='Enter'||e.key==='Tab'){
e.preventDefault();
var ch=null;
if(dfi>=0&&dm[dfi])ch=dm[dfi]; /* arrowed to a specific item */
else if(dm.length===1)ch=dm[0]; /* only one match \u2014 auto-confirm */
/* else: multiple matches and none selected \u2014 don't commit, let user pick */
if(ch)commit(i,ri,di,ch);
else{
/* not valid \u2014 clear and flash */
var v=i.value.trim();
if(v&&!A.some(function(h){return h.toLowerCase()===v.toLowerCase();})){
commit(i,ri,di,'');
i.style.background='var(--redbg,#faeaea)';setTimeout(function(){i.style.background='';},600);
}
}
closeDD();
var ni=di<6?gI(ri,di+1):gI(Math.min(ri+1,C.length-1),0);
if(ni){ni.focus();ni.scrollIntoView({block:'nearest'});}
} else if(e.key==='Escape'){closeDD();i.blur();}
else if(e.key==='Delete'||(e.key==='Backspace'&&i.value==='')){commit(i,ri,di,'');closeDD();}
}

// \u2500\u2500 SYNC LAYER \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500

function getTrust(val){
if(!val)return null;
var vl=val.toLowerCase().trim();
var allTrusts=Object.keys(TRUST_SITES);
// Direct trust name match first
for(var i=0;i<allTrusts.length;i++){
if(allTrusts[i].toLowerCase()===vl)return allTrusts[i];
}
// Site name match using getSites (includes user-added sites)
for(var i=0;i<allTrusts.length;i++){
var sites=getSites(allTrusts[i]);
for(var j=0;j<sites.length;j++){
if(sites[j].toLowerCase()===vl)return allTrusts[i];
}
}
// Fuzzy match as fallback
for(var i=0;i<allTrusts.length;i++){
var sites=getSites(allTrusts[i]);
for(var j=0;j<sites.length;j++){
var sl=sites[j].toLowerCase();
if(sl.includes(vl)||vl.includes(sl))return allTrusts[i];
}
}
return null;
}

function getCandIdx(candName){
// Return index of candidate in C[] by name
for(var i=0;i<C.length;i++){if(C[i].n===candName)return i;}
return -1;
}

function getRotaIdx(trustName, candName, wk){
// Return index of candidate in a trust's rota for a given week
var rotas=(ROTA_DATA.weeks[wk]&&ROTA_DATA.weeks[wk].rotas)||{};
var trustRota=rotas[trustName]||[];
for(var i=0;i<trustRota.length;i++){
if(trustRota[i].n===candName||trustRota[i].name===candName)return i;
}
return -1;
}

function ensureWeekInRota(wk){
if(ROTA_DATA.weeks[wk])return; // already exists
// Generate date labels
var d=new Date(wk);
var months=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
var dayNames=['Mon','Tue','Wed','Thu','Fri','Sat','Sun'];
var dates=[];
for(var i=0;i<7;i++){
var dd=new Date(d);dd.setDate(d.getDate()+i);
dates.push(dayNames[i]+' '+dd.getDate()+' '+months[dd.getMonth()]);
}
// Build rotas from CURRENT staff on system for each trust (not historical clone)
// This ensures new candidates added via UI are included
var newRotas={};
Object.keys(TRUST_SITES).forEach(function(trust){
var hObj=HC.find(function(x){return x.name===trust;})||{};
var ed=gHE(trust);
// Only show active candidates on rota
var staffList=(hObj.rota||[]).concat(ed.rota||[]).filter(function(w){
var nm=w.name||w.n||'';
var candObj=C.find(function(x){return x.n===nm;});
return !candObj||(candObj.ac!=='Inactive');
});
// Check if we have historical data for this trust to preserve existing entries
var historical=null;
var histKeys=ROTA_DATA.weekKeys.filter(function(k){return ROTA_DATA.weeks[k]&&ROTA_DATA.weeks[k].rotas[trust];});
if(histKeys.length){
historical=ROTA_DATA.weeks[histKeys[histKeys.length-1]].rotas[trust];
}
newRotas[trust]=staffList.map(function(w){
var name=w.name||w.n||'';
var spec=w.spec||w.s||'';
// Check sd for any existing shift data for this person this week
var candIdx=getCandIdx(name);
var cells=[];
for(var di=0;di<7;di++){
var shiftVal=(sd[wk]&&sd[wk][candIdx])?sd[wk][candIdx][di]||'':'';
if(shiftVal){
// Already booked in shift entry \u2014 set correct value
var shiftTrust=getTrust(shiftVal);
if(shiftTrust===trust){cells.push(shiftVal);}
else{cells.push('U');}
} else {
// Check historical rota for this person
var histEntry=historical?historical.find(function(r){return r.n===name;}):null;
cells.push(histEntry&&histEntry.c&&histEntry.c[di]?histEntry.c[di]:'');
}
}
return{n:name,s:spec,c:cells};
});
});
ROTA_DATA.weeks[wk]={dates:dates,rotas:newRotas};
if(ROTA_DATA.weekKeys.indexOf(wk)<0)ROTA_DATA.weekKeys.push(wk);
ROTA_DATA.weekKeys.sort();
}

function checkConflict(candName, wk, dayIdx, targetTrust){
// Returns the trust name if already booked elsewhere that day, else null
var candIdx=getCandIdx(candName);
if(candIdx<0)return null;
// Check shiftData
var wd=sd[wk]||{};
var existing=(wd[candIdx]||{})[dayIdx];
if(existing){
var existTrust=getTrust(existing);
if(existTrust&&existTrust!==targetTrust)return existTrust;
if(!existTrust&&existing!==targetTrust)return existing;
}
return null;
}

function getCellForRota(wk, trustName, candIdx, dayIdx){
// Returns {val, encoded} where val is display value and encoded is 'A'/'U'/site/''
var shiftVal=(sd[wk]&&sd[wk][candIdx])?sd[wk][candIdx][dayIdx]||'':'';
if(shiftVal){
var shiftTrust=getTrust(shiftVal);
if(shiftTrust===trustName){
return{val:shiftVal, encoded:shiftVal}; // booked at this trust
} else {
return{val:'U', encoded:'U'}; // booked elsewhere = unavailable
}
}
// No booking in sd \u2014 check manual rota override
var override=getRO(wk,trustName,candIdx,dayIdx);
return{val:override||'', encoded:override||''};
}


function syncShiftToRota(wk, candIdx, dayIdx, hospVal){
// sd is already updated by commit() before this is called.
// Rota renders live from sd via getCellForRota(), so no ROTA_DATA write needed.
// Just re-render if hospital panel is open on an affected trust.
if(_curRotaHosp&&document.getElementById('pg-hospitals').classList.contains('on')){
openHosp(_curRotaHosp);
}
}

function syncRotaToShift(wk, trustName, candName, dayIdx, rotaVal){
// Called when rota dropdown changes
// rotaVal = 'A','U','T',siteName,'' 
var candIdx=getCandIdx(candName);
if(candIdx<0)return;
var isBooked=(rotaVal&&rotaVal!=='A'&&rotaVal!=='U'&&rotaVal!=='T');
var isCleared=(rotaVal===''||rotaVal==='U');
if(!sd[wk])sd[wk]={};
if(!sd[wk][candIdx])sd[wk][candIdx]={};
if(isBooked){
sd[wk][candIdx][dayIdx]=rotaVal; // site name
} else if(isCleared){
delete sd[wk][candIdx][dayIdx];
}
// Sync unavailable to all other trusts
if(isBooked){
var allTrusts=Object.keys(TRUST_SITES);
ensureWeekInRota(wk);
allTrusts.forEach(function(trust){
if(trust===trustName)return;
var rotaIdx=getRotaIdx(trust,candName,wk);
if(rotaIdx<0)return;
var cells=(ROTA_DATA.weeks[wk].rotas[trust][rotaIdx]||{}).c;
if(!cells)return;
while(cells.length<7)cells.push('');
cells[dayIdx]='U';
});
} else if(isCleared){
// If cleared/unavailable, remove from other rotas too (only if they were auto-set)
var allTrusts=Object.keys(TRUST_SITES);
ensureWeekInRota(wk);
allTrusts.forEach(function(trust){
if(trust===trustName)return;
var rotaIdx=getRotaIdx(trust,candName,wk);
if(rotaIdx<0)return;
var cells=(ROTA_DATA.weeks[wk].rotas[trust][rotaIdx]||{}).c;
if(!cells)return;
// Only clear if it was auto-set as unavailable (not manually set)
if(cells[dayIdx]==='U')cells[dayIdx]='';
});
}
// Refresh shift table if visible
if(document.getElementById('pg-shifts').classList.contains('on'))rTable();
rFoot();uMet();rDash();aS();
try{localStorage.setItem('crm_rotas2',JSON.stringify(ROTA_DATA.weeks));}catch(e){}
}


function commit(i,ri,di,v){
var wd=gWD();if(!wd[ri])wd[ri]={};
v=(v||'').trim();
// Conflict check \u2014 is candidate already booked at a different hospital this day?
if(v){
var wk=wKey(wkOff);
var conflict=checkConflict(C[ri]?C[ri].n:'',wk,di,getTrust(v)||v);
if(conflict){
var candName=C[ri]?C[ri].n:'this candidate';
if(!confirm(candName+' is already booked at '+conflict+' on this day. Book at '+v+' instead?')){
// Revert input
var prev=(wd[ri]||{})[di]||'';
i.value=prev;
if(!prev)i.classList.remove('f');
return;
}
}
}
if(v){wd[ri][di]=v;i.value=v;i.classList.add('f');}
else{delete wd[ri][di];i.value='';i.classList.remove('f');}
// Sync to rota
var wk2=wKey(wkOff);
syncShiftToRota(wk2,ri,di,v);
rFoot();uMet();rDash();aS();
}

function openDD(inp){
var q=(inp.value||'').toLowerCase().trim();
dm=q?A.filter(function(h){return h.toLowerCase().includes(q);}):A;
dfi=-1;
var dd=document.getElementById('dd');
if(!dm.length){dd.classList.remove('open');return;}
dd.innerHTML=dm.slice(0,14).map(function(h,idx){
return '<div class="ddo" data-i="'+idx+'" onmousedown="ddP(event,'+idx+')">'+esc(h)+'</div>';
}).join('');
var rect=inp.getBoundingClientRect();
dd.style.left=rect.left+'px';
dd.style.top=(rect.bottom+2)+'px';
dd.style.width=Math.max(rect.width,190)+'px';
dd.classList.add('open');
ac=inp;
}
function closeDD(){document.getElementById('dd').classList.remove('open');ac=null;dfi=-1;dm=[];}
function mDF(d){
var dd=document.getElementById('dd'),opts=dd.querySelectorAll('.ddo');
if(!opts.length)return;
dfi=Math.max(0,Math.min(dm.length-1,dfi+d));
opts.forEach(function(o,i){o.classList.toggle('hi',i===dfi);});
opts[dfi].scrollIntoView({block:'nearest'});
}
function ddP(e,idx){
/* KEY FIX: set ddPicking=true BEFORE mousedown causes blur on the input */
e.preventDefault();
ddPicking=true;
if(!ac){ddPicking=false;return;}
var ri=+ac.dataset.r,di=+ac.dataset.d,inp=ac;
commit(inp,ri,di,dm[idx]);
closeDD();
ddPicking=false;
var ni=di<6?gI(ri,di+1):gI(Math.min(ri+1,C.length-1),0);
if(ni)setTimeout(function(){ni.focus();},20);
}

document.addEventListener('mousedown',function(e){
if(!e.target.closest('#dd')&&!e.target.closest('.ci'))closeDD();
});

function aS(){clearTimeout(saveT);saveT=setTimeout(function(){try{localStorage.setItem('crm5',JSON.stringify(sd));}catch(e){}},600);}
function saveNow(){
try{localStorage.setItem('crm5',JSON.stringify(sd));}catch(e){}
var el=document.getElementById('smsg');el.textContent='Saved \u2713';el.style.color='var(--grtx)';
setTimeout(function(){el.textContent='Autosaves as you type';el.style.color='';},2000);
}

/* DASHBOARD */
function rDash(){
var wd=gWD(),wkTot=0,wkMg=0,hs=new Set();
// All candidates stat
var _allC=C.length;
var _activeC=C.filter(function(c){return c.ac==='Active';}).length;
var _el1=document.getElementById('dv-activecands');if(_el1)_el1.textContent=_activeC;
var _el2=document.getElementById('dv-allcands');if(_el2)_el2.textContent=_allC+' total';
// Open queries from pay queries
if(!_pqLoaded){loadPQ();_pqLoaded=true;}
var _openQ=_pq.filter(function(q){return q.status==='open';}).length;
var _inprogQ=_pq.filter(function(q){return q.status==='inprogress';}).length;
var _el3=document.getElementById('dv-openq');if(_el3)_el3.textContent=_openQ+_inprogQ;
var _el4=document.getElementById('dv-inprogq');if(_el4)_el4.textContent=_openQ+' open, '+_inprogQ+' in progress';
Object.keys(wd).forEach(function(ri){Object.keys(wd[ri]).forEach(function(di){var h=wd[ri][di];if(!h)return;wkTot++;hs.add(h);wkMg+=getHospPPS(h);});});
document.getElementById('dv-wk').textContent=wkTot||'\u2014';
document.getElementById('dv-mg').textContent=wkMg>0?'\u00a3'+Math.round(wkMg).toLocaleString():'\u2014';

// Hospital shift volume from Div Con
if(!_dcLoaded){loadDC();_dcLoaded=true;}
var _hospsEl=document.getElementById('dv-hosps');
if(_hospsEl){
if(!_dcReports.length){
_hospsEl.innerHTML='<div style="font-size:12px;color:var(--t3);padding:8px 0">No Div Con reports imported yet</div>';
} else {
var _dcHtml='<div style="display:flex;align-items:center;gap:8px;margin-bottom:10px">'
+'<span style="font-size:11px;color:var(--t2);flex-shrink:0">Week:</span>'
+'<select id="dash-dc-sel" onchange="dashDcTab(+this.value)" style="padding:4px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+_dcReports.map(function(r,i){return'<option value="'+i+'">'+esc(r.weekLabel)+'</option>';}).join('')
+'</select></div><div id="dash-dc-bars"></div>';
_hospsEl.innerHTML=_dcHtml;
var _initTab=Math.min(_dashDcActiveTab,_dcReports.length-1);
dashDcTab(_initTab>=0?_initTab:0);
}
}

// Top earners from selected Div Con week
var _avEl=document.getElementById('dv-avail');
if(_avEl){
if(!_dcLoaded){loadDC();_dcLoaded=true;}
var _rep=_dcReports[_dashDcActiveTab>=0?_dashDcActiveTab:0];
if(!_rep){
_avEl.innerHTML='<div style="font-size:12px;color:var(--t3)">No Div Con imported yet</div>';
} else {
// Sum margin by candidate
var _byC={};
_rep.rows.forEach(function(r){
if(!_byC[r.cand])_byC[r.cand]={margin:0,shifts:0};
_byC[r.cand].margin+=r.margin;
_byC[r.cand].shifts++;
});
var _top=Object.keys(_byC).map(function(n){return{name:n,margin:_byC[n].margin,shifts:_byC[n].shifts};})
.sort(function(a,b){return b.margin-a.margin;}).slice(0,8);
var _maxM=_top.length?_top[0].margin:1;
_avEl.innerHTML=_top.map(function(c){
var pct=_maxM>0?Math.round(Math.abs(c.margin)/_maxM*100):0;
var isNeg=c.margin<0;
return'<div style="margin-bottom:8px">'
+'<div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:3px">'
+'<span style="font-size:12px;font-weight:500;color:var(--tx)">'+esc(c.name)+'</span>'
+'<span style="font-size:12px;font-weight:600;color:'+(isNeg?'var(--amtx)':'var(--grtx)')+';\u00a0white-space:nowrap;padding-left:8px">\u00a3'+c.margin.toFixed(0)+'</span>'
+'</div>'
+'<div style="height:4px;background:var(--su2);border-radius:2px;overflow:hidden">'
+'<div style="height:100%;width:'+pct+'%;background:'+(isNeg?'var(--amtx)':'var(--grtx)')+';border-radius:2px"></div>'
+'</div>'
+'</div>';
}).join('')
}
}

var specs=[['ODP',76,'#1558a0'],['Scrub',70,'#157a52'],['Recovery',7,'#a06010'],['Chemo',3,'#921f1f']];
document.getElementById('dv-specs').innerHTML=specs.map(function(sp){
return '<div class="specrow"><span class="specrow-lbl">'+sp[0]+'</span><div class="specrow-bw"><div class="specrow-b" style="width:'+Math.round(sp[1]/76*100)+'%;background:'+sp[2]+'"></div></div><span class="specrow-n">'+sp[1]+'</span></div>';
}).join('');

// \u2500\u2500 Weekly shifts chart \u2014 from shift count (rotas) \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
// Build week-by-week shift counts from gWD across all stored weeks
var _allRotas=[];
try{
var _sr=localStorage.getItem('crm_rotas2');
if(_sr){
var _rd=JSON.parse(_sr);
Object.keys(_rd).forEach(function(dateKey){
var wd=_rd[dateKey];
var cnt=0;
Object.keys(wd).forEach(function(ri){Object.keys(wd[ri]).forEach(function(di){if(wd[ri][di])cnt++;});});
if(cnt>0){
// Convert date to tax week number (UK Apr-Mar, week 1 = first Mon of Apr)
var d=new Date(dateKey);
var yr=d.getFullYear();
var taxStart=new Date(d.getMonth()<3?yr-1:yr,3,1); // Apr 1
// Find first Monday on or after Apr 1
var dow=taxStart.getDay();
if(dow!==1)taxStart.setDate(taxStart.getDate()+(dow===0?1:8-dow));
var diff=Math.floor((d-taxStart)/604800000);
var taxWk=diff+1;
_allRotas.push({dateKey:dateKey,taxWk:taxWk,shifts:cnt});
}
});
}
}catch(e){}
_allRotas.sort(function(a,b){return a.dateKey<b.dateKey?-1:1;});
// Use hardcoded W as fallback if no rotas
var _shiftData=_allRotas.length?_allRotas:W.map(function(w){return{taxWk:w.wk,shifts:w.shifts};});
var maxS=Math.max.apply(null,_shiftData.map(function(w){return w.shifts;}));
document.getElementById('dv-shchart').innerHTML=_shiftData.map(function(w){
var pct=Math.max(Math.round(w.shifts/maxS*100),2);
var wkLabel='Wk '+_wn;
var _wn=w.taxWk||w.wk||'';
return'<div class="bw"><div class="b" style="height:'+pct+'%;background:#378ADD" title="Wk '+_wn+': '+w.shifts+' shifts"></div><div class="blbl">'+_wn+'</div></div>';
}).join('');

// \u2500\u2500 Weekly margin chart \u2014 from all Div Con reports \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
if(!_dcLoaded){loadDC();_dcLoaded=true;}
var _dcByWk=[];
_dcReports.forEach(function(r){
var total=r.rows.reduce(function(s,row){return s+row.margin;},0);
_dcByWk.push({label:r.weekLabel,margin:total});
});
// Sort by week label (WK51 25-26 etc)
_dcByWk.sort(function(a,b){return a.label<b.label?-1:1;});
var _mgData=_dcByWk.length?_dcByWk:W.map(function(w){return{label:'Wk '+w.wk,margin:w.margin};});
var maxM=Math.max.apply(null,_mgData.map(function(w){return Math.abs(w.margin);}));if(!maxM)maxM=1;
document.getElementById('dv-mgchart').innerHTML=_mgData.map(function(w){
var isNeg=w.margin<0;
var pct=Math.max(Math.round(Math.abs(w.margin)/maxM*100),3);
var wn=(w.label||'').replace(/[^\d]/g,'').slice(0,2)||'';
return'<div class="bw"><div class="b" style="height:'+pct+'%;background:'+(isNeg?'var(--amtx)':'#1D9E75')+'" title="'+esc(w.label)+': \u00a3'+Math.round(w.margin).toLocaleString()+'"></div><div class="blbl">'+wn+'</div></div>';
}).join('');
// Margin chart labels - show each div con week number
var _mgLblEl=document.getElementById('dv-mglbls');
if(_mgLblEl){
if(!_mgData.length){_mgLblEl.innerHTML='';}
else{
// Extract just the week number from label e.g. "WK51 25-26" -> "51"
var _mgStep=Math.max(1,Math.floor(_mgData.length/6));
var _mgLbls=[];
_mgData.forEach(function(w,i){
if(i%_mgStep===0||i===_mgData.length-1){
var _wn=(w.label||'').match(/\d+/);
_mgLbls.push('<span class="chartlbl">'+(_wn?_wn[0]:w.label)+'</span>');
}
});
_mgLblEl.innerHTML=_mgLbls.join('');
}
}
}

/* SUMMARY */
function rSum(){
var wd=gWD(),ht={},hc={};
Object.keys(wd).forEach(function(ri){
Object.keys(wd[ri]).forEach(function(di){
var h=wd[ri][di];if(!h)return;
ht[h]=(ht[h]||0)+1;
if(!hc[h])hc[h]=new Set();
hc[h].add(ri);
});
});
var en=Object.keys(ht).sort(function(a,b){return ht[b]-ht[a];});
if(!en.length){
document.getElementById('hgrid').innerHTML='<p style="color:var(--t3);font-size:13px">No shifts entered this week yet.</p>';
document.getElementById('hdet').innerHTML='';
return;
}
var mx=ht[en[0]];
var rows='';
en.forEach(function(nm,i){
var cnt=ht[nm],cc=hc[nm]?hc[nm].size:0;
var ho=H.find(function(x){return x.name===nm;});
var pps=ho&&ho.pps>0?ho.pps:0;
var mg=pps?' \u00b7 est. \u00a3'+Math.round(pps*cnt).toLocaleString():'';
var area=ho?ho.area:'';
var pct=Math.round(cnt/mx*100);
rows+='<div class="hc sumrow" data-nm="'+esc(nm)+'">'
+'<div style="font-size:14px;font-weight:500;margin-bottom:2px">'+esc(nm)+'</div>'
+'<div style="font-size:11px;color:var(--t2);margin-bottom:7px">'+esc(area)+'</div>'
+'<div style="font-size:24px;font-weight:500;color:var(--bl)">'+cnt+'</div>'
+'<div style="font-size:11px;color:var(--t3)">shifts</div>'
+'<div style="height:3px;background:var(--b1);border-radius:2px;margin:7px 0 5px">'
+'<div style="height:3px;border-radius:2px;background:var(--bl);width:'+pct+'%"></div>'
+'</div>'
+'<div style="font-size:11px;color:var(--t2)">'+cc+' candidate'+(cc!==1?'s':'')+mg+'</div>'
+'</div>';
});
document.getElementById('hgrid').innerHTML=rows;
document.getElementById('hgrid').querySelectorAll('.sumrow').forEach(function(el){
el.addEventListener('click',function(){showHD(this.dataset.nm);});
});
}

function showHD(nm){
var wd=gWD(),bd={};
Object.keys(wd).forEach(function(ri){Object.keys(wd[ri]).forEach(function(di){if(wd[ri][di]===nm){var d=DAYS[+di];if(!bd[d])bd[d]=[];bd[d].push(C[+ri]);}});});
var html='<div style="margin-top:16px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px"><div style="font-size:13px;font-weight:500;margin-bottom:11px">'+esc(nm)+'\u2014 this week breakdown</div>';
DAYS.forEach(function(d){if(!bd[d])return;html+='<div style="margin-bottom:9px"><div style="font-size:11px;font-weight:500;color:var(--t2);margin-bottom:4px">'+d+'</div>'+bd[d].map(function(c){return '<div style="display:flex;align-items:center;gap:8px;padding:4px 0;border-bottom:0.5px solid var(--b1)"><span style="flex:1;font-size:13px">'+esc(c.n)+'</span><span style="font-size:11px;color:var(--t2)">'+esc(c.s)+'</span></div>';}).join('')+'</div>';});
html+='</div>';document.getElementById('hdet').innerHTML=html;
}

/* CANDIDATES */
function saveCandEdit(idx){
var fields=['n','s','ac','e','p','av','h','a','r'];
// Read also-works-at checkboxes
var sitesChecked=[];
var awEl=document.getElementById('ce-sites-list');
if(awEl){
awEl.querySelectorAll('input[type=checkbox]:checked').forEach(function(cb){
sitesChecked.push(cb.value);
});
}
var ed={};
fields.forEach(function(f){
var el=document.getElementById('ce-'+f);
if(el){
var val=el.value.trim();
if(f==='r')val=parseFloat(val)||0;
ed[f]=val;
}
});
// Read spec multi-select
ed.s=ceGetSpecs()||'';
ed.subSpec=ceGetSubSpecs()||'';
ed.sites=sitesChecked;
if(!ed.n){alert('Name is required');return;}
if(idx>=0){
// Edit existing
candEdits[idx]=ed;
// Update base C[] too so everything stays in sync
Object.assign(C[idx],ed);
} else {
// New candidate
var newCand=Object.assign({st:'unknown',b:''},ed);
C.push(newCand);
// Add to shift entry dropdown rebuild not needed \u2014 C[] is source
}
saveCE();
// If coming from pipeline, link the new candidate back
if(window._pipeRegisteringId){
var _pid=window._pipeRegisteringId;
window._pipeRegisteringId=null;
var _pp=_pipe.find(function(x){return x.id===_pid;});
if(_pp){_pp.candIdx=C.length-1;savePipe();}
}
closeCandPanel();
rCands();
rebuildDropdown();
}

function addNewCand(){
openCandPanel(-1,{n:'',s:'ODP',ac:'Active',e:'',p:'',av:'',h:'',a:'',r:0});
}

var _editCandIdx=-1;
function openCandPanel(idx,cand){
try{
_editCandIdx=idx;
var panel=document.getElementById('cand-panel');
if(!panel){console.error('cand-panel not found');return;}
var title=document.getElementById('cp-title');
if(title)title.textContent=idx>=0?'Edit candidate':'Add new candidate';
var deact=document.getElementById('cp-deact');
if(deact)deact.style.display=idx>=0?'block':'none';
// Populate main hospital select with all specific sites
var hSel=document.getElementById('ce-h');
if(hSel){
var currentH=cand.h||'';
hSel.innerHTML='<option value="">-- select hospital --</option>';
getAllSitesList().forEach(function(site){
var opt=document.createElement('option');
opt.value=site; opt.textContent=site;
if(site===currentH)opt.selected=true;
hSel.appendChild(opt);
});
}
// Restore spec multi-select
var specDrop=document.getElementById('ce-spec-drop');
if(specDrop){
var savedSpecs=(cand.s||'').split(',').map(function(s){return s.trim();}).filter(Boolean);
var customSpecs=[];
specDrop.querySelectorAll('input[type=checkbox]').forEach(function(cb){
cb.checked=savedSpecs.indexOf(cb.value)>=0;
});
// Handle custom specs (Other free text)
var knownSpecs=['ODP','Scrub','Recovery','Chemo','Anaesthetics','SFA','TSW','Other'];
var otherVals=savedSpecs.filter(function(s){return knownSpecs.indexOf(s)<0;});
var otherCb=specDrop.querySelector('input[value="Other"]');
var otherInput=document.getElementById('ce-s-other');
if(otherVals.length&&otherInput){
if(otherCb)otherCb.checked=true;
otherInput.value=otherVals.join(', ');
otherInput.style.display='block';
} else if(otherInput){
otherInput.style.display='none';
}
ceSpecChanged();
}
// Restore sub-specs
var subWrap=document.getElementById('ce-subspec-wrap');
if(subWrap){
var savedSubSpecs=(cand.subSpec||'').split(',').map(function(s){return s.trim();}).filter(Boolean);
subWrap.querySelectorAll('input[name=ce-subspec]').forEach(function(cb){
cb.checked=savedSubSpecs.indexOf(cb.value)>=0;
});
}
// Populate also-works-at checkboxes
var awEl=document.getElementById('ce-sites-list');
if(awEl){
var currentSites=cand.sites||[];
var allSites=getAllSitesList();
awEl.innerHTML=allSites.map(function(site){
var checked=currentSites.indexOf(site)>=0?' checked':'';
return'<label style="display:flex;align-items:center;gap:6px;padding:4px 0;font-size:12px;cursor:pointer;border-bottom:0.5px solid var(--b1)">'
+'<input type="checkbox" value="'+site+'"'+checked+' style="cursor:pointer"> '+site
+'</label>';
}).join('');
}
// Fill remaining fields
var fields=['n','s','ac','e','p','av','a','r'];
fields.forEach(function(f){
var el=document.getElementById('ce-'+f);
if(!el)return;
var val=cand[f];
if(f==='r')el.value=val>0?val:'';
else el.value=val||'';
});
panel.classList.add('open');
}catch(err){
console.error('openCandPanel error:',err.message);
alert('Panel error: '+err.message);
}
}

function closeCandPanel(){
var panel=document.getElementById('cand-panel');
if(panel)panel.classList.remove('open');
_editCandIdx=-1;
}

function deactivateCand(idx){
if(!confirm('Mark '+C[idx].n+' as Inactive?'))return;
if(!candEdits[idx])candEdits[idx]={};
candEdits[idx].ac='Inactive';
C[idx].ac='Inactive';
C[idx].st='unknown';
saveCE();rCands();
}


function setCF(v,btn){candFilter=v;document.querySelectorAll('#cpills .wb').forEach(function(b){b.classList.remove('on');});btn.classList.add('on');rCands();}
function rCands(){
var q=(document.getElementById('cq').value||'').toLowerCase();
var fl=C.map(function(c,i){return{c:getC(i),i:i};}).filter(function(obj){
var c=obj.c;
if(candFilter==='inactive'&&c.ac!=='Inactive')return false;
if(candFilter==='ODP'&&c.s!=='ODP')return false;
if(candFilter==='Scrub'&&!c.s.toLowerCase().includes('scrub'))return false;
if(candFilter==='active'&&c.ac==='Inactive')return false;
if(q&&!(c.n+c.s+(c.h||'')+(c.a||'')+(c.e||'')).toLowerCase().includes(q))return false;
return true;
});
document.getElementById('cqc').textContent=fl.length+' shown';
var sc={ODP:'var(--bl)',Scrub:'var(--gr)',Recovery:'var(--am)'};
var rows=fl.map(function(obj){
var c=obj.c,idx=obj.i;
var col=sc[c.s]||'var(--t3)';
var inactive=c.ac==='Inactive';
var sb=c.ac==='Inactive'?'tgr':'tg';
var sl=c.ac==='Inactive'?'Inactive':'Active';
return '<tr style="border-bottom:0.5px solid var(--b1);'+(inactive?'opacity:.5':'')+'">'+
'<td style="padding:7px 0;cursor:pointer" class="fw cand-edit-row" data-idx="'+idx+'">'+esc(c.n)+'</td>'+
'<td style="padding:7px 7px;font-size:12px;color:'+col+'">'+esc(c.s||'')+'</td>'+
'<td style="padding:7px 7px;font-size:12px" class="m">'+esc(c.h||'')+(c.sites&&c.sites.length?'<span style="font-size:10px;background:var(--blbg);color:var(--bl);border-radius:10px;padding:1px 5px;margin-left:4px">+'+c.sites.length+' sites</span>':'')+'</td>'+
'<td style="padding:7px 7px;font-size:12px" class="m">'+esc(c.a||'')+'</td>'+
'<td style="padding:7px 7px;font-size:12px" class="m">'+esc(c.e||'')+'</td>'+
'<td style="padding:7px 7px;font-size:12px;font-family:monospace" class="m">'+esc(c.p||'')+'</td>'+
'<td style="padding:7px 0;text-align:right"><span class="tag '+sb+'">'+sl+'</span></td>'+
'<td style="padding:7px 0;text-align:right;font-size:12px" class="m">'+(c.r>0?'\u00a3'+c.r:'\u2014')+'</td>'+
'<td style="padding:7px 0 7px 8px;text-align:right">'+
'<button class="edit-btn cand-edit-btn" data-idx="'+idx+'">Edit</button>'+
'</td>'+
'</tr>';
}).join('');
var tbl=document.getElementById('ctbl');
tbl.innerHTML='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;min-width:800px">'+
'<thead><tr style="border-bottom:0.5px solid var(--b2)">'+
['Name','Spec','Hospital','Area','Email','Phone','Activity','Min rate',''].map(function(h,i){
var align=i>5?'right':'left';
return '<th style="text-align:'+align+';font-size:11px;font-weight:500;color:var(--t2);padding:0 '+(i>5?'0':'7px')+' 8px '+(i===0?'0':'7px')+';text-transform:uppercase;letter-spacing:.05em">'+h+'</th>';
}).join('')+
'</tr></thead><tbody>'+rows+'</tbody></table></div>';
// Event delegation for edit buttons and row clicks
tbl.querySelectorAll('.cand-edit-btn,.cand-edit-row').forEach(function(el){
el.addEventListener('click',function(e){
e.stopPropagation();
try{
var idx=+this.dataset.idx;
openCandPanel(idx,getC(idx));
}catch(err){
console.error('openCandPanel error:',err.message,err.stack);
alert('Error opening candidate: '+err.message);
}
});
});
}

/* HOSPITALS */
var selHosp=null;
function aTag(a){var l=(a||'').toLowerCase();if(l.includes('london'))return'tb';if(l.includes('surrey'))return'tg';if(['private','spa','ramsay','fertility','medica'].some(function(x){return l.includes(x);}))return'ta';return'tgr';}

function addNewTrust(){
var nameEl=document.getElementById('nt-name');
var areaEl=document.getElementById('nt-area');
var sitesEl=document.getElementById('nt-sites');
if(!nameEl||!nameEl.value.trim()){alert('Trust name is required');return;}
var name=nameEl.value.trim();
var area=areaEl?areaEl.value.trim():'';
var sitesRaw=sitesEl?sitesEl.value.trim():'';
// Parse comma-separated sites
var sites=sitesRaw?sitesRaw.split(',').map(function(s){return s.trim();}).filter(Boolean):[name];
// Check not duplicate
if(HC.find(function(h){return h.name.toLowerCase()===name.toLowerCase();})){
alert(name+' already exists');return;
}
// Add to HC and H
var newHC={
name:name, area:area, pps:0, total:0, weekly:[],
processes:[], rota:[], issues:[], roster_link:'',
contacts:[], rates:[], personalRates:[]
};
var newH={name:name, area:area, pps:0, total:0};
HC.push(newHC);
H.push(newH);
// Add to TRUST_SITES
TRUST_SITES[name]=sites;
// Save
trustEdits.push({name:name, area:area, sites:sites});
saveTrustEdits();
// Rebuild dropdown
rebuildDropdown();
// Close form and refresh list
hideEF('nt-form');
if(nameEl)nameEl.value='';
if(areaEl)areaEl.value='';
if(sitesEl)sitesEl.value='';
rHosps();
// Open the new hospital page
openHosp(name);
}

function deleteTrust(name){
if(!confirm('Remove '+name+' from the hospital list? This cannot be undone.'))return;
// Remove from HC and H
HC=HC.filter(function(h){return h.name!==name;});
H=H.filter(function(h){return h.name!==name;});
delete TRUST_SITES[name];
delete hospEdits[name];
trustEdits=trustEdits.filter(function(t){return t.name!==name;});
saveTrustEdits();
saveHE();
rebuildDropdown();
selHosp=null;
document.getElementById('hd-content').style.display='none';
document.getElementById('hd-empty').style.display='block';
rHosps();
}



// \u2500\u2500 HOSPITAL TRUST CARDS \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _hospView='cards'; // 'cards' | 'trust' | 'hospital' | 'split'
var _activeTrust=null;
var _activeHosp=null;

function rHosps(){
if(_hospView==='cards')renderTrustCards();
else if(_hospView==='trust')renderTrustDetail(_activeTrust);
else if(_hospView==='hospital')renderHospDetail(_activeHosp,_activeTrust);
else if(_hospView==='split')renderSplitView();
}

function renderTrustCards(){
var el=document.getElementById('hosp-main');
if(!el)return;

// Build card grid
var html='<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:16px">'
+'<div class="sh">Hospitals &amp; Trusts</div>'
+'<div style="display:flex;gap:8px">'
+'<button onclick="toggleSplitMode()" id="split-btn" style="padding:6px 12px;border:0.5px solid var(--b2);border-radius:var(--r);background:'
+(_splitMode?'var(--bl)':'transparent')+';color:'+(_splitMode?'#fff':'var(--t2)')+';font-size:12px;cursor:pointer">'
+(_splitMode?'&#9135; Split on':'&#9634; Split view')+'</button>'
+'<button onclick="showAddTrustForm()" style="padding:6px 12px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;color:var(--t2);font-size:12px;cursor:pointer">+ Add trust</button>'
+'</div>'
+'</div>';

html+='<div id="trust-card-grid" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:16px">';

TRUST_CARDS.forEach(function(trust){
var hc=HC.find(function(h){return h.name===trust.name;})||{};
var he=(typeof gHE==='function')?gHE(trust.name):{};
// Merge base + edited contacts so primary flag works across both
var _baseCts=hc.contacts||[];
var _editCts=(he&&he.contacts)||[];
var contacts=_baseCts.concat(_editCts);
var rosterLink=(he&&he.rosterLink)||hc.roster_link||'';

var nSites=trust.sites.length;
var sliceWidth=100/nSites;

// Build site slices
var slicesHtml='';
trust.sites.forEach(function(site,si){
var imgUrl=tcImgEdits[trust.name+'|'+site.name]||site.img||'';
var imgOverride=tcImgEdits[trust.name+'|'+site.name]||'';
var finalImg=imgOverride||imgUrl||'';
var bgStyle=finalImg
?'background:url('+finalImg+') center/cover no-repeat;'
:'background:linear-gradient(135deg,'+trust.color+' 0%,'+trust.color+'cc 100%);';
var placeholder=finalImg?''
:'<div style="position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:8px">'
+'<div style="font-size:22px;margin-bottom:4px;opacity:.7">&#127973;</div>'
+'<div style="font-size:12px;font-weight:700;color:#fff;text-align:center;text-shadow:0 1px 3px rgba(0,0,0,.4)">'+esc(site.name)+'</div>'
+'</div>';

slicesHtml+='<div class="tc-slice" data-trust="'+esc(trust.name)+'" data-site="'+esc(site.name)+'" '
+'style="flex:1;transition:flex .3s ease;position:relative;overflow:hidden;cursor:pointer;'+bgStyle+'" '
+'onmouseenter="sliceHover(this,true)" onmouseleave="sliceHover(this,false)" '
+'onclick="onSliceClick(\''+esc(trust.name)+'\',\''+esc(site.name)+'\')">'
+placeholder
// Site name label on hover
+'<div class="slice-label" style="position:absolute;bottom:0;left:0;right:0;padding:8px 10px;background:linear-gradient(transparent,rgba(0,0,0,.65));opacity:0;transition:opacity .25s;pointer-events:none">'
+'<div style="font-size:12px;font-weight:600;color:#fff">'+esc(site.name)+'</div>'
+'</div>'
+'</div>';
});

// Card
html+='<div class="trust-card" style="border-radius:12px;overflow:hidden;background:var(--su);border:0.5px solid var(--b1);box-shadow:0 2px 8px rgba(0,0,0,.06);transition:box-shadow .2s" '
+'onmouseenter="this.style.boxShadow=\'0 6px 20px rgba(0,0,0,.12)\'" onmouseleave="this.style.boxShadow=\'0 2px 8px rgba(0,0,0,.06)\'">'

// Image slices row
+'<div style="display:flex;height:120px;overflow:hidden">'
+slicesHtml
+'</div>'

// Card footer
+'<div style="padding:12px 14px">'
// Trust name \u2014 click for trust overview
+'<div style="display:flex;align-items:flex-start;justify-content:space-between;gap:8px">'
+'<div>'
+'<div class="trust-name-link" onclick="onTrustClick(\''+esc(trust.name)+'\')" '
+'style="font-size:14px;font-weight:600;color:var(--tx);cursor:pointer;line-height:1.3" '
+'onmouseover="this.style.color=\'var(--bl)\'" onmouseout="this.style.color=\'var(--tx)\'">'
+esc(trust.fullName)
+'</div>'
+'<div style="font-size:11px;color:var(--t3);margin-top:2px">'+esc(trust.area)+(nSites>1?' &middot; '+nSites+' sites':'')+'</div>'
+'</div>'
+'<button onclick="toggleMoreInfo(\''+esc(trust.name)+'\')" '
+'style="flex-shrink:0;padding:4px 8px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2);white-space:nowrap">'
+'More info</button>'
+'</div>'

// More info panel (hidden by default)
+'<div id="more-info-'+esc(trust.name).replace(/[^a-z0-9]/gi,'_')+'" style="display:none;margin-top:10px;padding-top:10px;border-top:0.5px solid var(--b1)">'
+(contacts.length?(function(){
// Show primary contact, or first contact if none marked primary
var allCts=contacts;
var primary=allCts.find(function(c){return c.primary===true;})||allCts[0];
return'<div style="font-size:12px;margin-bottom:4px">'
+'<span style="font-size:9px;font-weight:600;color:var(--bl);text-transform:uppercase;letter-spacing:.08em;margin-right:6px">Primary</span>'
+'<strong style="color:var(--tx)">'+esc(primary.name||'')+'</strong>'
+((primary.title||primary.role)?'<span style="color:var(--t3);font-size:11px"> &middot; '+esc(primary.title||primary.role||'')+'</span>':'')
+(primary.email?'<br><a href="mailto:'+esc(primary.email)+'" style="color:var(--bl);font-size:11px">'+esc(primary.email)+'</a>':'')
+(primary.phone?'<br><span style="color:var(--t3);font-size:11px">'+esc(primary.phone)+'</span>':'')
+'</div>'
+(allCts.length>1?'<div style="font-size:10px;color:var(--t3)">+'+( allCts.length-1)+' more contact'+(allCts.length>2?'s':'')+'</div>':'');
})()
:'<div style="font-size:12px;color:var(--t3)">No contacts saved</div>')
+(rosterLink?'<a href="'+esc(rosterLink)+'" target="_blank" style="display:inline-block;margin-top:8px;font-size:11px;color:var(--bl)">&#128279; Open Health Roster</a>':'')
+'</div>'
+'</div>'
+'</div>';
});

html+='</div>';
el.innerHTML=html;
}

function sliceHover(el,entering){
var parent=el.parentNode;
var slices=parent.querySelectorAll('.tc-slice');
var n=slices.length;
if(n<=1)return;
var lbl=el.querySelector('.slice-label');
slices.forEach(function(s){
if(s===el){
s.style.flex=entering?'2.5':'1';
var l=s.querySelector('.slice-label');if(l)l.style.opacity=entering?'1':'0';
} else {
s.style.flex=entering?'0.5':'1';
var l=s.querySelector('.slice-label');if(l)l.style.opacity='0';
}
});
}

function onSliceClick(trustName,siteName){
if(_splitMode){
if(!_splitHospA){_splitHospA={trust:trustName,site:siteName};}
else if(!_splitHospB){_splitHospB={trust:trustName,site:siteName};_hospView='split';rHosps();}
return;
}
_activeTrust=trustName;_activeHosp=siteName;_hospView='hospital';rHosps();
}

function onTrustClick(trustName){
_activeTrust=trustName;_activeHosp=null;_hospView='trust';rHosps();
}

function toggleMoreInfo(trustName){
var id='more-info-'+trustName.replace(/[^a-z0-9]/gi,'_');
var el=document.getElementById(id);
if(!el)return;
var isHidden=el.style.display==='none';
if(!isHidden){el.style.display='none';return;}
// Rebuild content live so primary contact is always current
var hc=HC.find(function(h){return h.name===trustName;})||{};
var he=gHE(trustName);
var contacts=(hc.contacts||[]).concat(he.contacts||[]);
var rosterLink=(he&&he.rosterLink)||hc.roster_link||'';
var primary=contacts.find(function(c){return c.primary===true;})||contacts[0];
var html='';
if(primary){
html+='<div style="font-size:12px;margin-bottom:6px">'
+'<span style="font-size:9px;font-weight:600;color:var(--bl);text-transform:uppercase;letter-spacing:.08em;margin-right:6px">Primary</span>'
+'<strong style="color:var(--tx)">'+esc(primary.name||'')+'</strong>'
+((primary.title||primary.role)?'<span style="color:var(--t3);font-size:11px"> &middot; '+esc(primary.title||primary.role||'')+'</span>':'')
+(primary.email?'<br><a href="mailto:'+esc(primary.email)+'" style="color:var(--bl);font-size:11px">'+esc(primary.email)+'</a>':'')
+(primary.phone?'<br><span style="color:var(--t3);font-size:11px">'+esc(primary.phone)+'</span>':'')
+'</div>'
+(contacts.length>1?'<div style="font-size:10px;color:var(--t3)">+'+(contacts.length-1)+' more contact'+(contacts.length>2?'s':'')+'</div>':'');
} else {
html='<div style="font-size:12px;color:var(--t3)">No contacts saved</div>';
}
if(rosterLink)html+='<a href="'+esc(rosterLink)+'" target="_blank" style="display:inline-block;margin-top:8px;font-size:11px;color:var(--bl)">&#128279; Health Roster</a>';
el.innerHTML=html;
el.style.display='block';
}

function toggleSplitMode(){
_splitMode=!_splitMode;
_splitHospA=null;_splitHospB=null;
if(!_splitMode&&_hospView==='split'){_hospView='cards';}
rHosps();
}

function renderTrustDetail(trustName){
var trust=TRUST_CARDS.find(function(t){return t.name===trustName;})||{name:trustName,fullName:trustName,color:'#1a5276',sites:[]};
var el=document.getElementById('hosp-main');
if(!el)return;

var backHtml='<div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">'
+'<button onclick="_hospView=\'cards\';rHosps()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">\u2190 Hospitals</button>'
+'<div class="sh" style="margin:0">'+esc(trust.fullName)+'</div>'
+'</div>';

// Site cards row
var sitesHtml='<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:10px;margin-bottom:16px">';
trust.sites.forEach(function(site){
var imgUrl=tcImgEdits[trustName+'|'+site.name]||site.img||'';
sitesHtml+='<div onclick="onSliceClick(\''+esc(trustName)+'\',\''+esc(site.name)+'\')" style="border-radius:var(--rl);overflow:hidden;cursor:pointer;border:0.5px solid var(--b1);transition:box-shadow .15s" '
+'onmouseover="this.style.boxShadow=\'0 4px 12px rgba(0,0,0,.12)\'" onmouseout="this.style.boxShadow=\'none\'">'
+'<div style="height:90px;background:'+(imgUrl?'url('+imgUrl+') center/cover':trust.color)+';display:flex;align-items:center;justify-content:center">'
+(imgUrl?'':'<span style="font-size:28px;opacity:.5">&#127973;</span>')
+'</div>'
+'<div style="padding:8px 10px;font-size:13px;font-weight:500;color:var(--tx)">'+esc(site.name)+'</div>'
+'</div>';
});
sitesHtml+='</div>';

el.innerHTML=backHtml+sitesHtml+'<div id="hd-empty" style="display:none"></div><div id="hd-content" class="hosp-view" style="display:block"></div>';
openHosp(trustName);
}


function renderHospDetail(siteName,trustName){
var trust=TRUST_CARDS.find(function(t){return t.name===trustName;})||{name:trustName,fullName:trustName,color:'#1a5276',sites:[]};
var site=trust.sites.find(function(s){return s.name===siteName;})||{name:siteName,img:''};
var imgUrl=tcImgEdits[trustName+'|'+siteName]||site.img||'';
var el=document.getElementById('hosp-main');
if(!el)return;

// Build the page shell with back button + image header + original openHosp content
var backHtml='<div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">'
+'<button onclick="_hospView=\'cards\';rHosps()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">\u2190 Hospitals</button>'
+(trustName&&trust.sites.length>1?'<button onclick="_hospView=\'trust\';renderTrustDetail(_activeTrust)" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">\u2190 '+esc(trustName)+'</button>':'')
+'<label style="margin-left:auto;font-size:11px;color:var(--t3);cursor:pointer" title="Upload new image">'
+'\u{1f4f7} Change image'
+'<input type="file" accept="image/*" onchange="updateTrustImg(\''+esc(trustName)+'\',\''+esc(siteName)+'\',this)" style="display:none">'
+'</label>'
+'</div>'
+(imgUrl?'<div style="height:180px;border-radius:var(--rl);overflow:hidden;margin-bottom:16px;background:url('+imgUrl+') center/cover no-repeat"></div>'
:'<div style="height:100px;border-radius:var(--rl);margin-bottom:16px;background:linear-gradient(135deg,'+trust.color+' 0%,'+trust.color+'bb 100%);display:flex;align-items:center;justify-content:center"><span style="font-size:22px;opacity:.6">&#127973;</span><span style="font-size:20px;font-weight:700;color:#fff;margin-left:10px">'+esc(siteName)+'</span></div>');

el.innerHTML=backHtml+'<div id="hd-empty" style="display:none"></div><div id="hd-content" class="hosp-view" style="display:block"></div>';

// Now call the original openHosp which fills hd-content with all the full detail
openHosp(trustName);
}


function renderSplitView(){
var el=document.getElementById('hosp-main');
if(!el)return;
var html='<div style="display:flex;gap:8px;align-items:center;margin-bottom:12px">'
+'<button onclick="_hospView=\'cards\';_splitMode=false;_splitHospA=null;_splitHospB=null;rHosps()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">\u2190 Back</button>'
+'<span style="font-size:13px;font-weight:500;color:var(--tx)">Split view: '+esc(_splitHospA.site)+' &amp; '+esc(_splitHospB.site)+'</span>'
+'</div>'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;height:calc(100vh - 140px)">';

[_splitHospA,_splitHospB].forEach(function(h,i){
var trust=TRUST_CARDS.find(function(t){return t.name===h.trust;})||{name:h.trust,fullName:h.trust,color:'#1a5276',sites:[]};
var site=trust.sites.find(function(s){return s.name===h.site;})||{name:h.site,img:''};
var hc=HC.find(function(hh){return hh.name===h.trust;})||{};
var he=(typeof gHE==='function')?gHE(h.trust):{};
var imgUrl=tcImgEdits[h.trust+'|'+h.site]||site.img||'';

html+='<div style="overflow-y:auto;border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px">'
+'<div style="height:100px;border-radius:var(--r);overflow:hidden;margin-bottom:10px;background:'+(imgUrl?'url('+imgUrl+') center/cover':trust.color)+';"></div>'
+'<div style="font-size:14px;font-weight:600;color:var(--tx);margin-bottom:4px">'+esc(h.site)+'</div>'
+'<div style="font-size:11px;color:var(--t3);margin-bottom:12px">'+esc(trust.fullName)+'</div>'
+hospHCDetail(hc,he)
+'<div class="sh" style="margin:12px 0 8px">Rota</div>'
+'<div id="split-rota-'+i+'"></div>'
+'</div>';
});
html+='</div>';
el.innerHTML=html;
renderHospRota(_splitHospA.trust,'split-rota-0');
renderHospRota(_splitHospB.trust,'split-rota-1');
}

function hospDetailHeader(title,trustName,imgUrl){
return '<div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">'
+'<button onclick="_hospView=\'cards\';rHosps()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">\u2190 Back</button>'
+(trustName&&_activeTrust&&title!==_activeTrust?'<button onclick="_hospView=\'trust\';rHosps()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">\u2190 '+esc(_activeTrust)+'</button>':'')
+'<div class="sh" style="margin:0">'+esc(title)+'</div>'
+'<label style="margin-left:auto;font-size:11px;color:var(--t3);cursor:pointer" title="Upload new image">'
+'&#128247; Change image'
+'<input type="file" accept="image/*" onchange="updateTrustImg(\''+esc(trustName)+'\',\''+esc(title)+'\',this)" style="display:none">'
+'</label>'
+'</div>'
+(imgUrl?'<div style="height:200px;border-radius:var(--rl);overflow:hidden;margin-bottom:16px;background:url('+imgUrl+') center/cover"></div>':'');
}

function hospHCDetail(hc,he){
// Merge base HC data with user edits
var contacts=(he&&he.contacts&&he.contacts.length?he.contacts:null)||hc.contacts||[];
var processes=(he&&he.processes&&he.processes.length?he.processes:null)||hc.processes||[];
var issues=(he&&he.issues&&he.issues.length?he.issues:null)||hc.issues||[];
var rates=(he&&he.rates&&he.rates.length?he.rates:null)||hc.rates||[];
var personalRates=(he&&he.personalRates&&he.personalRates.length?he.personalRates:null)||hc.personalRates||[];
var rosterLink=(he&&he.rosterLink)||hc.roster_link||'';
var pps=(he&&he.pps)||hc.pps||0;
var total=hc.total||0;

var html='';

// Stats bar
html+='<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:16px">';
if(pps)html+='<div style="padding:8px 16px;background:var(--su2);border-radius:var(--r);text-align:center">'
+'<div style="font-size:20px;font-weight:600;color:var(--bl)">\u00a3'+pps.toFixed(2)+'</div>'
+'<div style="font-size:10px;color:var(--t3);margin-top:1px">PPS rate</div></div>';
if(total)html+='<div style="padding:8px 16px;background:var(--su2);border-radius:var(--r);text-align:center">'
+'<div style="font-size:20px;font-weight:600;color:var(--tx)">'+total+'</div>'
+'<div style="font-size:10px;color:var(--t3);margin-top:1px">total shifts</div></div>';
if(rosterLink)html+='<a href="'+esc(rosterLink)+'" target="_blank" '
+'style="padding:8px 16px;background:var(--blbg);border-radius:var(--r);font-size:12px;color:var(--bl);text-decoration:none;display:flex;align-items:center;gap:6px">'
+'&#128279; Health Roster</a>';
html+='</div>';

// Contacts
if(contacts.length){
html+='<div class="sh" style="font-size:12px;margin-bottom:8px">Contacts</div>';
contacts.forEach(function(c){
html+='<div style="padding:10px 12px;background:var(--su2);border-radius:var(--r);margin-bottom:6px">'
+'<div style="font-size:13px;font-weight:500;color:var(--tx)">'+esc(c.name||c.title||'')+'</div>'
+((c.title||c.role||c.dept)?'<div style="font-size:11px;color:var(--t3);margin-top:1px">'+esc(c.title||c.role||c.dept||'')+'</div>':'')
+(c.email?'<div style="margin-top:4px"><a href="mailto:'+esc(c.email)+'" style="font-size:12px;color:var(--bl)">'+esc(c.email)+'</a></div>':'')
+(c.phone?'<div style="font-size:12px;color:var(--t2);margin-top:2px">&#128222; '+esc(c.phone)+'</div>':'')
+'</div>';
});
}

// Processes
if(processes.length){
html+='<div class="sh" style="font-size:12px;margin:14px 0 8px">Processes</div>';
processes.forEach(function(p){
html+='<div style="display:flex;gap:10px;padding:7px 10px;border-left:2px solid var(--bl);margin-bottom:6px;background:var(--su2);border-radius:0 var(--r) var(--r) 0">'
+'<div style="flex:1;font-size:12px;color:var(--tx)">'+esc(p.action||'')+'</div>'
+(p.day?'<div style="font-size:11px;color:var(--t3);white-space:nowrap">'+esc(p.day)+'</div>':'')
+'</div>';
});
}

// Issues
if(issues.length){
html+='<div class="sh" style="font-size:12px;margin:14px 0 8px">Common issues</div>';
issues.forEach(function(iss){
html+='<div style="padding:8px 12px;background:var(--ambg);border-radius:var(--r);margin-bottom:6px">'
+'<div style="font-size:12px;font-weight:500;color:var(--amtx)">'+esc(iss.issue||'')+'</div>'
+(iss.resolution?'<div style="font-size:11px;color:var(--t2);margin-top:3px">'+esc(iss.resolution)+'</div>':'')
+'</div>';
});
}

// Rate cards
if(rates.length){
html+='<div class="sh" style="font-size:12px;margin:14px 0 8px">Rate cards</div>';
html+='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="text-align:left;padding:4px 8px;color:var(--t2)">Grade</th>'
+'<th style="text-align:right;padding:4px 8px;color:var(--t2)">Pay</th>'
+'<th style="text-align:right;padding:4px 8px;color:var(--t2)">Charge</th>'
+'<th style="text-align:right;padding:4px 8px;color:var(--t2)">Margin</th>'
+'</tr></thead><tbody>';
rates.forEach(function(r){
var margin=r.charge&&r.pay?Math.round((r.charge-r.pay)*100)/100:null;
html+='<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 8px;color:var(--tx)">'+esc(r.grade||r.name||'')+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--t2)">'+(r.pay?'\u00a3'+r.pay:'--')+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--bl)">'+(r.charge?'\u00a3'+r.charge:'--')+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--grtx)">'+(margin!==null?'\u00a3'+margin:'--')+'</td>'
+'</tr>';
});
html+='</tbody></table></div>';
}

// Personal rates
if(personalRates.length){
html+='<div class="sh" style="font-size:12px;margin:14px 0 8px">Personal rates</div>';
html+='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="text-align:left;padding:4px 8px;color:var(--t2)">Candidate</th>'
+'<th style="text-align:right;padding:4px 8px;color:var(--t2)">Pay</th>'
+'<th style="text-align:right;padding:4px 8px;color:var(--t2)">Charge</th>'
+'</tr></thead><tbody>';
personalRates.forEach(function(r){
html+='<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 8px;color:var(--tx)">'+esc(r.cand||r.candidate||'')+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--t2)">'+(r.pay?'\u00a3'+r.pay:'--')+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--bl)">'+(r.charge?'\u00a3'+r.charge:'--')+'</td>'
+'</tr>';
});
html+='</tbody></table></div>';
}

return html;
}

function renderHospRota(trustName,containerId){
var container=document.getElementById(containerId);
if(!container)return;
// Get current week rota data for this trust
var wkKey=getRotaWkKey();
var wkData=ROTA_DATA.weeks&&ROTA_DATA.weeks[wkKey];
if(!wkData||!wkData.rotas||!wkData.rotas[trustName]){
container.innerHTML='<div style="font-size:12px;color:var(--t3);padding:8px">No rota data for this week</div>';
return;
}
var rows=wkData.rotas[trustName];
var dates=wkData.dates||[];
var days=['Mon','Tue','Wed','Thu','Fri','Sat','Sun'];
var html='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px">';
html+='<thead><tr><th style="padding:4px 8px;text-align:left;color:var(--t2);border-bottom:0.5px solid var(--b2)">Candidate</th>';
days.forEach(function(d,i){html+='<th style="padding:4px 6px;text-align:center;color:var(--t2);border-bottom:0.5px solid var(--b2);min-width:70px">'+d+(dates[i]?'<br><span style="color:var(--t3);font-weight:400">'+fmtDateDMY(dates[i]).slice(0,5)+'</span>':'')+'</th>';});
html+='</tr></thead><tbody>';
rows.forEach(function(row){
html+='<tr style="border-bottom:0.5px solid var(--b1)"><td style="padding:4px 8px;font-weight:500;color:var(--tx)">'+esc(row.n||'')+'</td>';
(row.c||[]).forEach(function(cell){
var v=cell||'';
var clr=v==='A'?'var(--grbg)':v==='U'?'var(--ambg)':v?'var(--blbg)':'transparent';
html+='<td style="padding:4px 6px;text-align:center;background:'+clr+';border-radius:3px">'+esc(v)+'</td>';
});
html+='</tr>';
});
html+='</tbody></table></div>';
container.innerHTML=html;
}

function updateTrustImg(trustName,siteName,input){
if(!input.files||!input.files[0])return;
var reader=new FileReader();
reader.onload=function(e){
tcImgEdits[trustName+'|'+siteName]=e.target.result;
saveTCImgs();
rHosps();
};
reader.readAsDataURL(input.files[0]);
}

function showAddTrustForm(){
var el=document.getElementById('hosp-main');
if(!el)return;
el.innerHTML='<div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">'
+'<button onclick="rHosps()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">\u2190 Back</button>'
+'<div class="sh" style="margin:0">Add new trust</div>'
+'</div>'
+'<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:16px;max-width:500px">'
+'<div style="margin-bottom:10px"><div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase">Trust name</div>'
+'<input id="add-trust-name" type="text" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box"></div>'
+'<div style="margin-bottom:10px"><div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase">Full name</div>'
+'<input id="add-trust-full" type="text" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box"></div>'
+'<div style="margin-bottom:10px"><div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase">Area</div>'
+'<input id="add-trust-area" type="text" style="width:100%;padding:7px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none;box-sizing:border-box"></div>'
+'<div style="margin-bottom:10px"><div style="font-size:11px;color:var(--t2);margin-bottom:4px;text-transform:uppercase">Hospital image</div>'
+'<input id="add-trust-img" type="file" accept="image/*" style="font-size:12px"></div>'
+'<button class="ef-save" onclick="confirmAddTrust()">Add trust</button>'
+'</div>';
}

function confirmAddTrust(){
var name=(document.getElementById('add-trust-name')||{}).value||'';
var full=(document.getElementById('add-trust-full')||{}).value||name;
var area=(document.getElementById('add-trust-area')||{}).value||'';
if(!name){alert('Trust name is required');return;}
var fi=document.getElementById('add-trust-img');
function doAdd(imgData){
TRUST_CARDS.push({name:name,fullName:full,area:area,color:'#1a5276',sites:[{name:name,img:imgData||''}]});
if(imgData)tcImgEdits[name+'|'+name]=imgData;
saveTCImgs();
// Also add to HC so new trust works across all CRM pages
if(!HC.find(function(h){return h.name===name;})){
HC.push({name:name,area:area,pps:0,total:0,weekly:[],contacts:[],sites:[name]});
}
if(!H.find(function(h){return h.name===name;})){
H.push({name:name,total:0});
}
// Save to trustEdits for persistence
var existing=trustEdits.find(function(t){return t.name===name;});
if(!existing){trustEdits.push({name:name,fullName:full,area:area,isNew:true});saveTrustEdits();}
rebuildDropdown();
_hospView='cards';rHosps();
}
if(fi&&fi.files&&fi.files[0]){
var r=new FileReader();r.onload=function(e){doAdd(e.target.result);};r.readAsDataURL(fi.files[0]);
} else {doAdd('');}
}


function filterHL(){rHosps();}

function getSites(trustName){
var base=TRUST_SITES[trustName]||[];
var added=(gHE(trustName).sites||[]);
// Deduplicate
var all=base.slice();
added.forEach(function(s){if(all.indexOf(s)<0)all.push(s);});
return all;
}

function getAllSites(){
var sites=[];
var trusts=Object.keys(TRUST_SITES);
trusts.forEach(function(t){
getSites(t).forEach(function(s){
if(sites.indexOf(s)<0)sites.push(s);
});
});
return sites.sort();
}

function getAllSitesList(){
// All specific sites from TRUST_CARDS (the definitive site list)
var sites=[];
TRUST_CARDS.forEach(function(tc){
tc.sites.forEach(function(s){
if(sites.indexOf(s.name)<0)sites.push(s.name);
});
});
// Also add from TRUST_SITES (original data)
Object.keys(TRUST_SITES).forEach(function(t){
(TRUST_SITES[t]||[]).forEach(function(s){
if(sites.indexOf(s)<0)sites.push(s);
});
});
return sites.sort();
}

function getCandSites(cand){
// Returns array of sites the candidate works at
// Uses cand.sites[] if set, otherwise falls back to cand.h
if(cand&&cand.sites&&cand.sites.length)return cand.sites;
if(cand&&cand.h)return[cand.h];
return[];
}

function candWorksAt(cand,siteName){
return getCandSites(cand).indexOf(siteName)>=0||(cand&&cand.h===siteName);
}

function rebuildDropdown(){
// Rebuild the A array (used for shift entry autocomplete)
var newSites=getAllSites();
// Replace contents of A
A.length=0;
newSites.forEach(function(s){A.push(s);});
}

function addSiteToTrust(trustName, siteName){
if(!siteName)return;
siteName=siteName.trim();
if(!siteName)return;
var ed=gHE(trustName);
if(!ed.sites)ed.sites=[];
if(ed.sites.indexOf(siteName)>=0||(TRUST_SITES[trustName]||[]).indexOf(siteName)>=0){
alert(siteName+' is already listed for '+trustName);return;
}
ed.sites.push(siteName);
// Also add to TRUST_SITES so rota dropdowns update
if(!TRUST_SITES[trustName])TRUST_SITES[trustName]=[];
TRUST_SITES[trustName].push(siteName);
saveHE();
rebuildDropdown();
openHosp(trustName);
}

function removeSiteFromTrust(trustName, siteName){
var ed=gHE(trustName);
if(!ed.sites)ed.sites=[];
var idx=ed.sites.indexOf(siteName);
if(idx>=0)ed.sites.splice(idx,1);
// Remove from TRUST_SITES too
var tsIdx=(TRUST_SITES[trustName]||[]).indexOf(siteName);
if(tsIdx>=0)TRUST_SITES[trustName].splice(tsIdx,1);
saveHE();
rebuildDropdown();
openHosp(trustName);
}


function getHospShiftStats(hospName){
// Returns {total, weekly16, marginTotal} from live shiftData
// weekly16 = array of 16 most recent weeks shift counts
var wks=Object.keys(sd).sort();
var weekCounts={};
var total=0;
wks.forEach(function(wk){
var wd=sd[wk]||{};
var cnt=0;
Object.keys(wd).forEach(function(ri){
Object.keys(wd[ri]).forEach(function(di){
if(wd[ri][di]===hospName)cnt++;
});
});
weekCounts[wk]=cnt;
total+=cnt;
});
// Build 16-week array (most recent 16 weeks, fill missing with 0)
var last16=wks.slice(-16);
// Pad to 16
while(last16.length<16){last16.unshift(null);}
var weekly16=last16.map(function(wk){return wk?weekCounts[wk]||0:0;});
var pps=getHospPPS(hospName);
var marginTotal=Math.round(total*pps);
return{total:total,weekly16:weekly16,marginTotal:marginTotal,pps:pps};
}


var hospEditMode=false;
function toggleHospEdit(){
hospEditMode=!hospEditMode;
var panel=document.getElementById('hd-content');
var btn=document.getElementById('hosp-edit-btn');
if(!panel||!btn)return;
if(hospEditMode){
panel.classList.remove('hosp-view');
btn.textContent='Done editing';
btn.style.background='var(--bl)';
btn.style.color='#fff';
btn.style.borderColor='var(--bl)';
} else {
panel.classList.add('hosp-view');
btn.textContent='Edit';
btn.style.background='';
btn.style.color='';
btn.style.borderColor='';
// Close any open forms
document.querySelectorAll('.ef').forEach(function(f){f.style.display='none';});
}
}


function openHosp(name){
selHosp=HC.find(function(h){return h.name===name;});
// Fallback: create a minimal object for user-added trusts
if(!selHosp){
var _tc=TRUST_CARDS.find(function(t){return t.name===name;});
if(_tc){selHosp={name:name,area:_tc.area||'',pps:0,total:0,weekly:[],contacts:[],sites:[name]};}
}
if(!selHosp)return;
_curRotaHosp=name;
_editHosp=name;
document.getElementById('hd-empty').style.display='none';
var c=document.getElementById('hd-content');
c.style.display='block';
// Always start in view mode when switching hospital
hospEditMode=false;
c.classList.add('hosp-view');
var eb=document.getElementById('hosp-edit-btn');
if(eb){eb.textContent='Edit';eb.style.background='';eb.style.color='';eb.style.borderColor='';}

var h=selHosp;
var ed=gHE(h.name);
var processes=h.processes.concat(ed.processes||[]);
var issues=h.issues.concat(ed.issues||[]);
var contacts=h.contacts.concat(ed.contacts||[]);
var rota=h.rota.concat(ed.rota||[]);
var personalRates=h.personalRates.concat(ed.personalRates||[]);
var rosterLink=ed.rosterLink||h.roster_link||'';
var totalMargin=h.pps>0?Math.round(h.pps*(h.total||0)):0;
var _sparkData=_liveTotal>0?_dispWeekly:(h.weekly||[]);
var wklyMax=Math.max.apply(null,_sparkData.concat([1]));
var sparkH=_sparkData.length?'<div style="display:flex;align-items:flex-end;gap:2px;height:44px;margin-top:8px">'+
_sparkData.map(function(v){var pct=Math.max(Math.round(v/wklyMax*100),2);return'<div style="flex:1;height:'+pct+'%;background:var(--bl);border-radius:1px 1px 0 0;min-width:0"></div>';}).join('')+
'</div>':'';


// Header
// PPS calculation
var _ed=gHE(h.name);
var _avgHours=_ed.avgHours||0;
var _selRateIdx=_ed.selectedRate!=null?_ed.selectedRate:-1;
var allRates2=(h.rates||[]).concat(_ed.rates||[]);
var _selRate=_selRateIdx>=0?allRates2[_selRateIdx]:null;
var _ppsResult=calcPPS(h.name,rota,personalRates,_selRate,_avgHours);
var _stdPPS=_ppsResult?_ppsResult.std:h.pps||0;
var _blendedPPS=_ppsResult?_ppsResult.blended:_stdPPS;
// Live shift stats from shift entry
var _liveStats=getHospShiftStats(h.name);
var _liveTotal=_liveStats.total;
var _liveMargin=_liveStats.marginTotal;
var _liveWeekly=_liveStats.weekly16;
// Fall back to spreadsheet data if nothing entered yet
var _dispTotal=_liveTotal>0?_liveTotal:h.total||0;
var _dispMargin=_liveTotal>0?_liveMargin:(_stdPPS>0?Math.round(_stdPPS*(h.total||0)):(h.pps||0)*(h.total||0));
var _dispWeekly=_liveTotal>0?_liveWeekly:(h.weekly||[]);

var html='<div style="display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:18px;flex-wrap:wrap;gap:10px">'
+'<div style="display:flex;align-items:center;gap:10px;margin-bottom:14px;width:100%">'
+'<button id="hosp-edit-btn" onclick="toggleHospEdit()" style="padding:5px 14px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:12px;color:var(--tx)">Edit</button>'
+'</div>'
+'<div>'
+'<div style="display:flex;align-items:center;gap:10px">'
+'<h2 style="font-size:17px;font-weight:500">'+esc(h.name)+'</h2>' 
+(trustEdits.find(function(t){return t.name===h.name;})?'<button class="edit-btn del-trust" style="color:#921f1f;border-color:#921f1f">Remove trust</button>':'')
+'</div>'
+'<div style="display:flex;align-items:center;gap:8px;margin-top:5px;flex-wrap:wrap">'
+'<span class="tag '+aTag(h.area)+'">'+esc(h.area)+'</span>'
+((_stdPPS>0||h.pps>0)?'<span style="font-size:12px;color:var(--t2)">\u00a3'+(_stdPPS>0?_stdPPS.toFixed(2):(h.pps||0).toFixed(2))+'/shift PPS</span>':'')
+(rosterLink?'<a href="'+esc(rosterLink)+'" target="_blank" style="font-size:12px;color:var(--bl);text-decoration:none">Health Roster &#8599;</a>':'')
+'<button class="edit-btn" onclick="showEF(\'ef-roster\')">&#9998; Roster link</button>'
+'</div>'
+'<div id="ef-roster" class="ef" style="display:none;margin-top:8px">'
+'<input id="ef-roster-link" type="text" placeholder="Paste Health Roster URL" value="'+esc(rosterLink)+'">'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="updateRosterLink()">Save</button>'
+'<button class="ef-cancel" onclick="hideEF(\'ef-roster\')">Cancel</button>'
+'</div>'
+'</div>'
+'</div>'
+'<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px">'
+'<div style="background:var(--su2);border-radius:var(--r);padding:9px 12px;text-align:center">'
+'<div style="font-size:18px;font-weight:500;color:var(--bl)">'+_dispTotal+'</div>'
+'<div style="font-size:10px;color:var(--t2);text-transform:uppercase;letter-spacing:.04em">Shifts'+(_liveTotal>0?' (live)':' YTD')+'</div>'
+'</div>'
+'<div style="background:var(--su2);border-radius:var(--r);padding:9px 12px;text-align:center">'
+'<div style="font-size:18px;font-weight:500;color:var(--gr)">'+(_dispMargin>0?'\u00a3'+Math.round(_dispMargin).toLocaleString():'\u2014')+'</div>'
+'<div style="font-size:10px;color:var(--t2);text-transform:uppercase;letter-spacing:.04em">Est. margin</div>'
+'</div>'
+'<div style="background:var(--su2);border-radius:var(--r);padding:9px 12px;text-align:center">'
+'<div style="font-size:18px;font-weight:500">'+rota.length+'</div>'
+'<div style="font-size:10px;color:var(--t2);text-transform:uppercase;letter-spacing:.04em">On rota</div>'
+'</div>'
+'</div>'
+'</div>';

if(sparkH)html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-bottom:12px"><div class="sh">16-week trend</div>'+sparkH+'</div>';


html+='<div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">';

// \\u25002500\u2500 \\\\\\\\u25002500250025002500250025002500ROCESSES \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px">'
+'<div style="display:flex;align-items:center;margin-bottom:10px">'
+'<div class="sh" style="margin-bottom:0;flex:1">Payment process</div>'
+'<button class="edit-btn" onclick="showEF(\'ef-proc\')">+ Add step</button>'
+'</div>';
processes.forEach(function(p,i){
var isNew=i>=(h.processes||[]).length;
html+='<div style="display:flex;gap:9px;align-items:flex-start;padding:5px 0;border-bottom:0.5px solid var(--b1)">'
+'<div style="flex-shrink:0;width:64px;font-size:11px;color:var(--t3);padding-top:1px">'+esc(p.day||'')+(p.time?'<br>'+esc(p.time):'')+'</div>'
+'<div style="font-size:12px;flex:1">'+esc(p.action)+'</div>'
+(isNew?'<button class="delbtn" onclick="delHEItem(\'processes\','+(i-(h.processes||[]).length)+')">&#215;</button>':'')
+'</div>';
});
html+='<div id="ef-proc" class="ef" style="display:none;margin-top:8px">'
+'<textarea id="ef-proc-action" placeholder="Process step description"></textarea>'
+'<div class="ef-g2">'
+'<input id="ef-proc-day" type="text" placeholder="Day (e.g. Monday)">'
+'<input id="ef-proc-time" type="text" placeholder="Time (e.g. 10:00)">'
+'</div>'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="addProcess()">Add step</button>'
+'<button class="ef-cancel" onclick="hideEF(\'ef-proc\')">Cancel</button>'
+'</div>'
+'</div>'
+'</div>';

// \u2500\u2500 ISSUES \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _issTitle=(gHE(h.name).issuesTitle)||'Common issues';
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px">'
+'<div style="display:flex;align-items:center;margin-bottom:10px">'
+'<div class="sh" style="margin-bottom:0;flex:1" id="iss-title-display">'+esc(_issTitle)+'</div>'
+'<button class="edit-btn" onclick="editIssueTitle()" style="margin-right:4px">&#9998; Rename</button>'
+'<button class="edit-btn" onclick="showEF(\'ef-iss\')">+ Add</button>'
+'</div>'
+'<div id="ef-iss-title" class="ef" style="display:none;margin-bottom:10px">'
+'<input id="ef-iss-title-input" type="text" placeholder="Box title e.g. Common issues, Notes, Key info" value="'+esc(_issTitle)+'">'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="saveIssueTitle()">Save</button>'
+'<button class="ef-cancel" onclick="hideEF(\'ef-iss-title\')">Cancel</button>'
+'</div>'
+'</div>';
issues.forEach(function(x,i){
var isNew=i>=(h.issues||[]).length;
html+='<div style="padding:5px 0;border-bottom:0.5px solid var(--b1);display:flex;gap:6px;align-items:flex-start">'
+'<div style="flex:1">'
+'<div style="font-size:12px;font-weight:500">'+esc(x.issue)+'</div>'
+(x.resolution?'<div style="font-size:11px;color:var(--t2);margin-top:2px">'+esc(x.resolution)+'</div>':'')
+'</div>'
+(isNew?'<button class="delbtn" onclick="delHEItem(\'issues\','+(i-(h.issues||[]).length)+')">&#215;</button>':'')
+'</div>';
});
html+='<div id="ef-iss" class="ef" style="display:none;margin-top:8px">'
+'<input id="ef-iss-issue" type="text" placeholder="Issue title">'
+'<textarea id="ef-iss-res" placeholder="Resolution / how to fix it"></textarea>'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="addIssue()">Add issue</button>'
+'<button class="ef-cancel" onclick="hideEF(\'ef-iss\')">Cancel</button>'
+'</div>'
+'</div>'
+'</div>';

html+='</div>'; // end 2-col grid

// \u2500\u2500 STAFF ON SYSTEM \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _excl=rotaExclusions[h.name]||{};
// Staff on system \u2014 filter by specific site being viewed
var _viewSite=_activeHosp||name;
var _isSpecificSite=(_viewSite!==name);
var _staffList;
if(_isSpecificSite){
// Hospital page: only candidates with this specific site in their profile
_staffList=C.filter(function(cand){
return cand.ac!=='Inactive'&&candWorksAt(cand,_viewSite);
}).map(function(cand){return{name:cand.n,spec:cand.s,n:cand.n,s:cand.s};});
} else {
// Trust page: use full rota list
_staffList=rota;
}
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-top:12px">'
+'<div style="display:flex;align-items:center;margin-bottom:4px">'
+'<div class="sh" style="margin-bottom:0;flex:1">Staff on system</div>'
+'<button class="edit-btn" onclick="showEF(\'ef-ro\')">+ Add candidate</button>'
+'</div>'
+'<div class="staff-toggle-hint" style="font-size:11px;color:var(--t3);margin-bottom:10px">Click a name to show/hide them on the rota</div>'
+'<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:5px" id="staff-grid">';
_staffList.forEach(function(w){
var excluded=_excl[w.name||w.n]===true;
var bg=excluded?'var(--su3)':'var(--su2)';
var nc=excluded?'var(--t3)':'var(--tx)';
var dot=excluded?'#ccc':'var(--bl)';
var st=excluded?'text-decoration:line-through;':'';
html+='<div class="staff-toggle" data-cand="'+esc(w.name||w.n)+'" '
+'style="display:flex;align-items:center;gap:7px;padding:5px 8px;background:'+bg+';border-radius:5px;cursor:pointer;user-select:none">'
+'<div style="width:6px;height:6px;border-radius:50%;background:'+dot+';flex-shrink:0"></div>'
+'<span style="font-size:12px;flex:1;min-width:0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;color:'+nc+';'+st+'">'+esc(w.name||w.n)+'</span>'
+'<span style="font-size:10px;color:var(--t3);flex-shrink:0">'+esc(w.spec||w.s||'')+'</span>'
+'</div>';
}); if(!_staffList.length)html+='<div style="font-size:12px;color:var(--t3)">No staff recorded for '+esc(_viewSite)+'</div>';
html+='</div>'
+'<div id="ef-ro" class="ef" style="display:none;margin-top:8px">'
+'<div style="margin-bottom:5px;font-size:12px;color:var(--t2)">Pick from candidate register:</div>'
+'<input type="text" id="ef-ro-search" placeholder="Type to filter candidates..." oninput="filterRotaSel()" style="margin-bottom:5px">'
+'<select id="ef-ro-sel" size="6" style="height:130px;width:100%;padding:0;margin-bottom:6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px">';
C.forEach(function(cand,i){
html+='<option value="'+i+'">'+esc(cand.n)+' \u2014 '+esc(cand.s)+(cand.h?' ('+esc(cand.h)+')':'')+'</option>';
});
html+='</select>'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="addRota()">Add to system</button>'
+'<button class="ef-cancel" data-hide="ef-ro">Cancel</button>'
+'</div>'
+'</div>'
+'</div>';

// \u2500\u2500 ROTA GRID \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
try{
var _rw=getRotaWk();
var _rdates=_rw.dates||[];
var _rawRota=(_rw.rotas&&_rw.rotas[h.name])||[];
var hSites=TRUST_SITES[h.name]||[];
// Sync rota grid to match staff on system exactly
// `rota` is the source of truth (Staff on System list)
var hRota=rota.map(function(w){
// Find existing row in ROTA_DATA for this person
var existing=_rawRota.find(function(r){return r.n===w.name||r.n===(w.name||'');});
if(existing)return existing;
// Not in ROTA_DATA yet - create blank row
return{n:w.name,s:w.spec,c:_rdates.map(function(){return'';})};
});
// Write back to ROTA_DATA so changes persist
if(!_rw.rotas)_rw.rotas={};
_rw.rotas[h.name]=hRota;
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-top:12px" id="rota-section">'
+'<div style="display:flex;align-items:center;gap:8px;margin-bottom:10px">'
+'<button onclick="rotaNav(-1,event)" style="padding:3px 9px;font-size:12px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;color:var(--t2)">&#8592;</button>'
+'<div class="sh" style="margin-bottom:0;flex:1">Rota \u2014 w/c <span id="rota-wk-lbl">'+(_rdates[0]||'')+'</span></div>'
+'<button onclick="rotaNav(1,event)" style="padding:3px 9px;font-size:12px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;color:var(--t2)">&#8594;</button>'
+'<button id="copy-rota-btn" onclick="copyRota(event)" style="padding:3px 10px;font-size:11px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;color:var(--bl)">Copy grid</button>'
+'</div>';
var _excl2=rotaExclusions[h.name]||{};
if(hRota.length){
html+='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;min-width:500px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="text-align:left;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px;min-width:140px">Name</th>'
+'<th style="text-align:left;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;min-width:70px">Skill</th>';
(_rdates||[]).forEach(function(d){
html+='<th style="text-align:center;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px;min-width:88px">'+esc(d)+'</th>';
});
html+='</tr></thead><tbody>';
var _excl2Keys=Object.keys(_excl2);
var _activeRota=(hRota||[]).filter(function(c){return !_excl2[c.n||c.name||''];});
var _wk2=getRotaWkKey();
_activeRota.forEach(function(c,ci){
var candIdx2=getCandIdx(c.n||c.name||'');
html+='<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 0;font-size:12px;font-weight:500;white-space:nowrap">'+esc(c.n||c.name||'')+'</td>'
+'<td style="padding:5px 8px;font-size:11px;color:var(--t2);white-space:nowrap">'+esc(c.s||c.spec||'')+'</td>';
for(var di2=0;di2<(_rdates.length||7);di2++){
var cell=getCellForRota(_wk2,h.name,candIdx2,di2);
var v=cell.encoded;
var bg='transparent',col='var(--t3)';
if(v==='A'){bg='#faf0df';col='#a06010';}
else if(v==='U'){bg='#e8e6e0';col='#5c5b52';}
else if(v==='T'){bg='#e8f0fa';col='#1558a0';}
else if(v){bg='#e2f4ec';col='#157a52';}
html+='<td style="padding:3px 3px;text-align:center">'
+'<select data-ci="'+ci+'" data-di="'+di2+'" data-hn="'+esc(h.name)+'"'
+' onchange="rotaChange(this)"'
+' style="width:100%;padding:3px 4px;font-size:11px;border:0.5px solid var(--b1);border-radius:4px;background:'+bg+';color:'+col+';cursor:pointer;outline:none;font-weight:500">'
+'<option value="">--</option>'
+'<option value="available"'+(v==='A'?' selected':'')+'>Available</option>'
+'<option value="unavailable"'+(v==='U'?' selected':'')+'>Unavailable</option>';
hSites.forEach(function(site){
html+='<option value="'+esc(site)+'"'+(v===site?' selected':'')+'>'+esc(site)+'</option>';
});
html+='<option value="tbc"'+(v==='T'?' selected':'')+'>TBC</option>';
html+='</select></td>';
}
html+='</tr>';
});
html+='</tbody></table></div>';
} else {
html+='<div style="font-size:12px;color:var(--t3)">No rota candidates linked to this hospital</div>';
}
html+='</div>';
}catch(rotaErr){console.error('Rota error:',rotaErr);html+='<div style="color:red;padding:8px;font-size:12px">Rota error: '+rotaErr.message+'</div>';}

// \u2500\u2500 RATE CARDS \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-top:12px">'
+'<div style="display:flex;align-items:center;margin-bottom:10px">'
+'<div class="sh" style="margin-bottom:0;flex:1">Rate cards</div>'
+'<button class="edit-btn" onclick="showEF(\'ef-rc\')">+ Add rate card</button>'
+'</div>';
// Merged rates: base + any added via UI
var allRates=(h.rates||[]).concat(gHE(h.name).rates||[]);
if(allRates.length){
html+='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px"><thead>'
+'<tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px;text-align:left">Ward/grade</th>'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;text-align:right">Pay D</th>'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;text-align:right">Pay N</th>'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;text-align:right">Pay S</th>'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;text-align:right">Charge D</th>'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;text-align:right">Charge N</th>'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;text-align:right">Margin D</th>'
+'<th style="font-size:10px;font-weight:500;color:var(--t2);padding:0 0 7px 8px;text-align:right"></th>'
+'</tr></thead><tbody>'
+allRates.map(function(r,ri){
var isNew=ri>=(h.rates||[]).length;
return '<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 0">'+esc(r.ward||r.hospital||'')+'</td>'
+'<td style="padding:5px 0 5px 8px;text-align:right;font-weight:500">\u00a3'+r.pd+'</td>'
+'<td style="padding:5px 0 5px 8px;text-align:right;color:var(--t2)">\u00a3'+r.pn+'</td>'
+'<td style="padding:5px 0 5px 8px;text-align:right;color:var(--t2)">\u00a3'+r.ps+'</td>'
+'<td style="padding:5px 0 5px 8px;text-align:right;font-weight:500">\u00a3'+r.cd+'</td>'
+'<td style="padding:5px 0 5px 8px;text-align:right;color:var(--t2)">\u00a3'+r.cn+'</td>'
+'<td style="padding:5px 0 5px 8px;text-align:right;font-weight:500;color:var(--grtx)">\u00a3'+r.md+'</td>'
+'<td style="padding:5px 0 5px 8px;text-align:right">'+(isNew?'<button class="delbtn rc-del" data-ridx="'+(ri-(h.rates||[]).length)+'">&#215;</button>':'')+'</td>'+'</tr>';
}).join('')+'</tbody></table></div>';
} else html+='<div style="font-size:12px;color:var(--t3)">No standard rate cards on file</div>';
// Rate card add form
html+='<div id="ef-rc" class="ef" style="display:none;margin-top:8px">'
+'<div style="margin-bottom:6px;font-size:12px;color:var(--t2)">Ward / grade name:</div>'
+'<input id="ef-rc-ward" type="text" placeholder="e.g. Band 6 ODP, CB6 Theatres">'
+'<div style="font-size:12px;color:var(--t2);margin:6px 0 4px">Pay rates:</div>'
+'<div class="ef-g3">'
+'<input id="ef-rc-pd" type="number" step="0.01" placeholder="Pay day (\u00a3)">'
+'<input id="ef-rc-pn" type="number" step="0.01" placeholder="Pay night (\u00a3)">'
+'<input id="ef-rc-ps" type="number" step="0.01" placeholder="Pay Sun (\u00a3)">'
+'</div>'
+'<div style="font-size:12px;color:var(--t2);margin:4px 0">Charge rates:</div>'
+'<div class="ef-g3">'
+'<input id="ef-rc-cd" type="number" step="0.01" placeholder="Charge day (\u00a3)">'
+'<input id="ef-rc-cn" type="number" step="0.01" placeholder="Charge night (\u00a3)">'
+'<input id="ef-rc-cs" type="number" step="0.01" placeholder="Charge Sun (\u00a3)">'
+'</div>'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="addRateCard()">Add rate card</button>'
+'<button class="ef-cancel" data-hide="ef-rc">Cancel</button>'
+'</div>'
+'</div>';

if(personalRates.length){
html+='<div style="margin-top:10px">'
+'<div style="display:flex;align-items:center;margin-bottom:6px">'
+'<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;flex:1">Personalised rates</div>'
+'<button class="edit-btn" onclick="showEF(\'ef-pr\')">+ Add</button>'
+'</div>'
+'<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:5px">';
personalRates.forEach(function(p,i){
var isNew=i>=(h.personalRates||[]).length;
html+='<div style="display:flex;align-items:center;gap:7px;padding:5px 9px;background:var(--ambg);border-radius:5px">'
+'<span style="flex:1;font-size:12px">'+esc(p.name)+'</span>'
+'<span style="font-size:11px;color:var(--t2)">'+esc(p.spec)+'</span>'
+'<span style="font-size:12px;font-weight:500;color:var(--amtx)">\u00a3'+p.rate+'</span>'
+(isNew?'<button class="delbtn" onclick="delHEItem(\'personalRates\','+(i-(h.personalRates||[]).length)+')">&#215;</button>':'')
+'</div>';
});
html+='</div></div>';
} else {
html+='<div style="margin-top:10px">'
+'<div style="display:flex;align-items:center;margin-bottom:6px">'
+'<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;flex:1">Personalised rates</div>'
+'<button class="edit-btn" onclick="showEF(\'ef-pr\')">+ Add</button>'
+'</div>'
+'<div style="font-size:12px;color:var(--t3)">No personalised rates on file</div>'
+'</div>';
}
html+='<div id="ef-pr" class="ef" style="display:none;margin-top:8px">'
+'<div style="margin-bottom:5px;font-size:12px;color:var(--t2)">Select from staff on system:</div>'
+'<select id="ef-pr-sel" style="margin-bottom:6px;width:100%;padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px">'
+'<option value="">-- select --</option>';
rota.forEach(function(w,wi){
html+='<option value="'+wi+'">'+esc(w.name)+' \u2014 '+esc(w.spec)+'</option>';
});
html+='</select>'
+'<input id="ef-pr-rate" type="number" placeholder="Pay rate e.g. 26.50" step="0.01">'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="addPersonalRate()">Add rate</button>'
+'<button class="ef-cancel" data-hide="ef-pr">Cancel</button>'
+'</div>'
+'</div>'
+'</div>';

// \u2500\u2500 CONTACTS \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-top:12px">'
+'<div style="display:flex;align-items:center;margin-bottom:10px">'
+'<div class="sh" style="margin-bottom:0;flex:1">Contacts</div>'
+'<button class="edit-btn" onclick="showEF(\'ef-ct\')">+ Add contact</button>'
+'</div>';
if(contacts.length){
html+='<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(250px,1fr));gap:8px">';
contacts.forEach(function(ct,i){
var isNew=i>=(h.contacts||[]).length;
var isPrimCt=ct.primary===true;
html+='<div style="padding:9px 11px;background:var(--su2);border-radius:var(--r);position:relative;border:'+(isPrimCt?'1.5px solid var(--bl)':'0.5px solid transparent')+'">'
+(isPrimCt?'<span style="position:absolute;top:6px;left:9px;font-size:9px;font-weight:600;color:var(--bl);text-transform:uppercase;letter-spacing:.08em">Primary</span>':'')
+'<div style="display:flex;align-items:flex-start;gap:6px;'+(isPrimCt?'margin-top:14px':'')+'">'
+'<div style="flex:1">'
+'<div style="font-size:13px;font-weight:500">'+esc(ct.name)+'</div>'
+'<div style="font-size:11px;color:var(--t2);margin-top:1px">'+esc(ct.title||'')+'</div>'
+(ct.dept?'<div style="font-size:10px;color:var(--t3)">'+esc(ct.dept)+'</div>':'')
+'<div style="margin-top:6px;display:flex;flex-direction:column;gap:2px">'
+(ct.email?'<a href="mailto:'+esc(ct.email)+'" style="font-size:11px;color:var(--bl);text-decoration:none">'+esc(ct.email)+'</a>':'')
+(ct.phone?'<span style="font-size:11px;color:var(--t2);font-family:monospace">'+esc(ct.phone)+'</span>':'')
+(ct.lastContacted&&ct.lastContacted!='NaT'?'<span style="font-size:10px;color:var(--t3)">Last contacted: '+esc(ct.lastContacted)+'</span>':'')
+'</div>'
+'</div>'
+'<div style="display:flex;flex-direction:column;gap:4px;align-items:flex-end">'
+(!isPrimCt?'<button class="edit-btn set-primary-btn" data-ci="'+i+'" style="font-size:10px;padding:2px 7px">Set primary</button>':'')
+(isNew?'<button class="delbtn" onclick="delHEItem(\'contacts\','+(i-(h.contacts||[]).length)+')">&#215;</button>':'')
+'</div>'
+'</div>'
+'</div>';
});
html+='</div>';
} else html+='<div style="font-size:12px;color:var(--t3)">No contacts on file</div>';
html+='<div id="ef-ct" class="ef" style="display:none;margin-top:10px">'
+'<div class="ef-g2">'
+'<input id="ef-ct-name" type="text" placeholder="Full name">'
+'<input id="ef-ct-title" type="text" placeholder="Job title">'
+'</div>'
+'<div class="ef-g2">'
+'<input id="ef-ct-dept" type="text" placeholder="Department">'
+'<input id="ef-ct-email" type="email" placeholder="Email address">'
+'</div>'
+'<input id="ef-ct-phone" type="tel" placeholder="Phone number">'
+'<label style="display:flex;align-items:center;gap:6px;font-size:12px;color:var(--t2);margin-bottom:6px;cursor:pointer">'
+'<input type="checkbox" id="ef-ct-primary"> Set as primary contact</label>'
+'<div class="ef-btns">'
+'<button class="ef-save" onclick="addContact()">Add contact</button>'
+'<button class="ef-cancel" onclick="hideEF(\'ef-ct\')">Cancel</button>'
+'</div>'
+'</div>'
+'</div>';

// Sites within trust
var trustSitesList=getSites(h.name);
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-top:12px">'
+'<div style="display:flex;align-items:center;margin-bottom:8px">'
+'<div class="sh" style="margin-bottom:0;flex:1">Sites within this trust</div>'
+'<button class="edit-btn" onclick="showEF(\'ef-site\')">+ Add site</button>'
+'</div>'
+'<div style="font-size:11px;color:var(--t3);margin-bottom:8px">These appear in the shift entry dropdown and rota booking options</div>'
+'<div style="display:flex;flex-wrap:wrap;gap:6px">';
trustSitesList.forEach(function(site){
var isUserAdded=(gHE(h.name).sites||[]).indexOf(site)>=0;
html+='<div style="display:flex;align-items:center;gap:4px;padding:4px 10px;background:var(--blbg);border-radius:20px;font-size:12px;color:var(--bltx)">'
+'<span>'+esc(site)+'</span>'
+(isUserAdded?'<button class="delbtn site-del" data-site="'+esc(site)+'">&#215;</button>':'')
+'</div>';
});
if(!trustSitesList.length)html+='<span style="font-size:12px;color:var(--t3)">No sites defined \u2014 add one below</span>';
html+='</div>'
+'<div id="ef-site" class="ef" style="display:none;margin-top:8px">'
+'<div style="display:flex;gap:8px;align-items:center">'
+'<input id="ef-site-name" type="text" placeholder="Site name e.g. Basildon" style="flex:1;margin-bottom:0">'
+'<button class="ef-save site-add">Add</button>'
+'<button class="ef-cancel" data-hide="ef-site">Cancel</button>'
+'</div>'
+'</div>'
+'</div>';


// \u2500\u2500 PPS CONFIG (collapsible) \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var rateOptions='<option value="-1">-- select rate card --</option>';
allRates2.forEach(function(r,ri){
var sel=ri===_selRateIdx?' selected':'';
rateOptions+='<option value="'+ri+'"'+sel+'>'+esc(r.ward||r.hospital||'Rate '+ri)+
' | Pay \u00a3'+r.pd+' Chg \u00a3'+r.cd+'</option>';
});
var ppsConfigured=_selRate&&_avgHours>0;
var ppsSummary=ppsConfigured
?'\u00a3'+_stdPPS.toFixed(2)+' std'+(_ppsResult&&_blendedPPS!==_stdPPS?' \u00b7 \u00a3'+_blendedPPS.toFixed(2)+' blended':'')
:'Not configured';
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);margin-top:12px;overflow:hidden">'
+'<div class="pps-toggle" style="display:flex;align-items:center;padding:13px 15px;cursor:pointer;user-select:none">'
+'<div class="sh" style="margin-bottom:0;flex:1">PPS configuration</div>'
+'<span style="font-size:12px;color:'+(ppsConfigured?'var(--gr)':'var(--t3)')+';margin-right:8px">'+ppsSummary+'</span>'
+'<span class="pps-chevron" style="font-size:12px;color:var(--t3)">&#9660;</span>'
+'</div>'
+'<div class="pps-body" style="display:none;padding:0 15px 15px">'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:12px;align-items:end">'
+'<div>'
+'<div style="font-size:11px;color:var(--t2);margin-bottom:4px">Standard rate card:</div>'
+'<select id="cfg-rate" style="width:100%;padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px">'+rateOptions+'</select>'
+'</div>'
+'<div>'
+'<div style="font-size:11px;color:var(--t2);margin-bottom:4px">Average shift hours:</div>'
+'<div style="display:flex;gap:6px;align-items:center">'
+'<input id="cfg-hours" type="number" step="0.5" min="1" max="24" placeholder="e.g. 10" value="'+(_avgHours||'')+'" style="flex:1;padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px">'
+'<button class="ef-save" onclick="saveHospConfig()">Save</button>'
+'</div>'
+'</div>'
+'</div>';
if(_ppsResult&&_ppsResult.breakdown&&_ppsResult.breakdown.length){
html+='<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:6px">Margin breakdown</div>'
+'<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="text-align:left;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 6px">Candidate</th>'
+'<th style="text-align:left;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 6px 8px">Spec</th>'
+'<th style="text-align:right;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 6px 8px">Pay</th>'
+'<th style="text-align:right;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 6px 8px">Margin/shift</th>'
+'</tr></thead><tbody>';
_ppsResult.breakdown.forEach(function(b){
var ms=b.margin<0?'color:#921f1f':'color:var(--grtx)';
html+='<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:4px 0;'+(b.isPersonal?'color:var(--amtx)':'')+'">'+esc(b.name)+(b.isPersonal?' <span style="font-size:10px;background:var(--ambg);color:var(--amtx);padding:1px 5px;border-radius:10px">personal</span>':'')+'</td>'
+'<td style="padding:4px 0 4px 8px;color:var(--t2)">'+esc(b.spec)+'</td>'
+'<td style="padding:4px 0 4px 8px;text-align:right">\u00a3'+b.pay.toFixed(2)+'</td>'
+'<td style="padding:4px 0 4px 8px;text-align:right;font-weight:500;'+ms+'">\u00a3'+b.margin.toFixed(2)+'</td>'
+'</tr>';
});
html+='</tbody></table></div>'
+'<div style="display:flex;gap:20px;margin-top:8px;padding-top:8px;border-top:0.5px solid var(--b1)">'
+'<span style="font-size:12px;color:var(--t2)">Std PPS: <strong>\u00a3'+_stdPPS.toFixed(2)+'</strong></span>'
+'<span style="font-size:12px;color:var(--t2)">Blended: <strong style="color:var(--gr)">\u00a3'+_blendedPPS.toFixed(2)+'</strong></span>'
+'<span style="font-size:12px;color:var(--t2)">Avg hours: <strong>'+_avgHours+'h</strong></span>'
+'</div>';
} else {
html+='<div style="font-size:12px;color:var(--t3)">'+
(!allRates2.length?'Add a rate card above to enable PPS calculation.':
!_avgHours?'Enter average shift hours and save to calculate PPS.':
'No candidates currently on rota.')+
'</div>';
}
html+='</div></div>';



// Collapsible PPS section
var _allR2=(h.rates||[]).concat(gHE(h.name).rates||[]);
var rateOpts='<option value="-1">-- select rate card --</option>';
_allR2.forEach(function(r,ri){
var sel=ri===_selRateIdx?' selected':'';
rateOpts+='<option value="'+ri+'"'+sel+'>'+esc(r.ward||r.hospital||'Rate '+ri)+' | Pay \u00a3'+r.pd+' Chg \u00a3'+r.cd+'</option>';
});
var _ppsLabel=_ppsResult?'Std \u00a3'+_stdPPS.toFixed(2)+' \u00b7 Blended \u00a3'+_blendedPPS.toFixed(2):'not configured';

// \u2500\u2500 ACTIVITY LOG \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _actLog=(_hospActivity[h.name]||[]);
var _actSafeId=h.name.replace(/[^a-z0-9]/gi,'_');
html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-top:12px">'
+'<div style="display:flex;align-items:center;margin-bottom:10px">'
+'<div class="sh" style="margin-bottom:0;flex:1">Activity log</div>'
+'</div>'
// Add entry form
+'<div style="display:flex;gap:6px;align-items:center;margin-bottom:10px">'
+'<select id="hosp-log-tag-'+_actSafeId+'" style="padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;flex-shrink:0">'
+'<option value="">Tag</option>'
+'<option>Called</option><option>Emailed</option><option>Refurbishment</option>'
+'<option>Planned closure</option><option>Surgeon absent</option>'
+'<option>D&V outbreak</option><option>Seasonal</option><option>Recovered</option><option>Other</option>'
+'</select>'
+'<input id="hosp-log-note-'+_actSafeId+'" type="text" placeholder="Add note e.g. Spoke to Sandra, theatre refurb until Feb\u2026" style="flex:1;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<button onclick="hospAddLog(\''+h.name+'\')" class="ef-save" style="padding:5px 12px;font-size:12px;white-space:nowrap">+ Log</button>'
+'</div>';
if(_actLog.length){
html+='<div>';
_actLog.forEach(function(e){
var tagColors={'Called':'var(--blbg)','Emailed':'#f0ebff','Refurbishment':'var(--ambg)',
'Planned closure':'var(--ambg)','Surgeon absent':'var(--ambg)','D&V outbreak':'#fdf0ee',
'Seasonal':'var(--su2)','Recovered':'var(--grbg)','Other':'var(--su2)'};
var tagTx={'Called':'var(--bl)','Emailed':'#6c3fc5','Refurbishment':'var(--amtx)',
'Planned closure':'var(--amtx)','Surgeon absent':'var(--amtx)','D&V outbreak':'#c0392b',
'Seasonal':'var(--t2)','Recovered':'var(--grtx)','Other':'var(--t2)'};
html+='<div style="display:flex;gap:10px;padding:7px 0;border-bottom:0.5px solid var(--b1);align-items:flex-start">'
+'<span style="font-size:11px;color:var(--t3);white-space:nowrap;flex-shrink:0;padding-top:1px">'+esc(e.date)+'</span>'
+(e.tag?'<span style="flex-shrink:0;padding:2px 8px;border-radius:10px;font-size:10px;font-weight:600;background:'+(tagColors[e.tag]||'var(--su2)')+';color:'+(tagTx[e.tag]||'var(--t2)')+'">'+esc(e.tag)+'</span>':'')
+'<span style="font-size:12px;color:var(--tx);flex:1">'+esc(e.note)+'</span>'
+'<button onclick="hospDeleteLog(\''+h.name+'\',\''+e.id+'\')" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:13px;padding:0;flex-shrink:0">&#215;</button>'
+'</div>';
});
html+='</div>';
} else {
html+='<div style="font-size:12px;color:var(--t3)">No activity logged yet</div>';
}
html+='</div>';



html+='<details style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);margin-top:12px;overflow:hidden">'
+'<summary style="display:flex;align-items:center;padding:11px 15px;cursor:pointer;user-select:none;list-style:none">'
+'<div class="sh" style="margin-bottom:0;flex:1">PPS \u2014 margin configuration</div>'
+'<span style="font-size:12px;color:'+(_ppsResult?'var(--t2)':'var(--t3)')+';margin-right:8px">'+_ppsLabel+'</span>'
+'</summary>'
+'<div style="border-top:0.5px solid var(--b1);padding:14px 15px">'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;align-items:end;margin-bottom:12px">'
+'<div>'
+'<div style="font-size:11px;color:var(--t2);margin-bottom:4px">Rate card to base calculation on:</div>'
+'<select id="cfg-rate" style="width:100%;padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px">'+rateOpts+'</select>'
+'</div>'
+'<div>'
+'<div style="font-size:11px;color:var(--t2);margin-bottom:4px">Average shift length (hours):</div>'
+'<div style="display:flex;gap:6px">'
+'<input id="cfg-hours" type="number" step="0.5" min="1" max="24" placeholder="e.g. 10" value="'+(_avgHours||'')+'" style="flex:1;padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px">'
+'<button class="ef-save" onclick="saveHospConfig()">Save</button>'
+'</div>'
+'</div>'
+'</div>';

if(_ppsResult&&_ppsResult.breakdown&&_ppsResult.breakdown.length){
html+='<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:7px">Margin per booked candidate</div>'
+'<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="text-align:left;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 5px">Candidate</th>'
+'<th style="text-align:left;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 5px 8px">Spec</th>'
+'<th style="text-align:right;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 5px">Pay/hr</th>'
+'<th style="text-align:right;font-size:10px;font-weight:500;color:var(--t2);padding:0 0 5px">Margin/shift</th>'
+'</tr></thead><tbody>';
_ppsResult.breakdown.forEach(function(b){
var ms=b.margin<0?'color:#921f1f':'color:var(--grtx)';
html+='<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:4px 0">'+(b.isPersonal?'<span style="color:var(--amtx)">'+esc(b.name)+'</span> <span style="font-size:10px;background:var(--ambg);color:var(--amtx);padding:1px 5px;border-radius:10px">personal</span>':esc(b.name))+'</td>'
+'<td style="padding:4px 0 4px 8px;color:var(--t2)">'+esc(b.spec)+'</td>'
+'<td style="padding:4px 0;text-align:right">\u00a3'+b.pay.toFixed(2)+'</td>'
+'<td style="padding:4px 0;text-align:right;font-weight:500;'+ms+'">\u00a3'+b.margin.toFixed(2)+'</td>'
+'</tr>';
});
html+='</tbody></table></div>'
+'<div style="display:flex;gap:20px;margin-top:8px;padding-top:8px;border-top:0.5px solid var(--b1)">'
+'<span style="font-size:12px;color:var(--t2)">Standard: <strong>\u00a3'+_stdPPS.toFixed(2)+'/shift</strong></span>'
+'<span style="font-size:12px;color:var(--t2)">Blended: <strong style="color:var(--grtx)">\u00a3'+_blendedPPS.toFixed(2)+'/shift</strong></span>'
+'<span style="font-size:12px;color:var(--t3)">\u00d7 '+_avgHours+'h avg</span>'
+'</div>';
} else {
html+='<div style="font-size:12px;color:var(--t3)">'+(!_allR2.length?'Add a rate card to enable PPS calculation.':!_avgHours?'Enter average shift hours and save to calculate.':'Configure above to see per-candidate margin breakdown.')+'</div>';
}
html+='</div></details>';

c.innerHTML=html;
// Event delegation for staff toggles
renderHospDocs(h.name,'hosp-docs-'+h.name.replace(/\s+/g,'-'));

c.querySelectorAll('.staff-toggle').forEach(function(el){
el.addEventListener('click',function(){toggleRotaCand(_curRotaHosp,this.dataset.cand);});
});
c.querySelectorAll('[data-hide]').forEach(function(el){
el.addEventListener('click',function(){hideEF(this.dataset.hide);});
});
c.querySelectorAll('.rc-del').forEach(function(el){
el.addEventListener('click',function(){delHEItem('rates',+this.dataset.ridx);});
});
c.querySelectorAll('.site-del').forEach(function(el){
el.addEventListener('click',function(){removeSiteFromTrust(_editHosp,this.dataset.site);});
});
c.querySelectorAll('.site-add').forEach(function(el){
el.addEventListener('click',function(){
var val=document.getElementById('ef-site-name');
if(val)addSiteToTrust(_editHosp,val.value);
});
});
c.querySelectorAll('.set-primary-btn').forEach(function(el){
el.addEventListener('click',function(){
var ci=+this.dataset.ci;
var hn=_editHosp;
var hc2=HC.find(function(h){return h.name===hn;})||{};
var baseLen=(hc2.contacts||[]).length;
// Clear all primaries
(hc2.contacts||[]).forEach(function(c){c.primary=false;});
gHE(hn).contacts.forEach(function(c){c.primary=false;});
// Set selected
if(ci<baseLen){(hc2.contacts||[])[ci].primary=true;}
else{var editIdx=ci-baseLen;if(gHE(hn).contacts[editIdx])gHE(hn).contacts[editIdx].primary=true;}
saveHE();openHosp(hn);
});
});
c.querySelectorAll('.del-trust').forEach(function(el){
el.addEventListener('click',function(){deleteTrust(_editHosp);});
});
// PPS collapsible toggle
var ppsToggle=c.querySelector('.pps-toggle');
if(ppsToggle){
ppsToggle.addEventListener('click',function(){
var body=c.querySelector('.pps-body');
var chev=c.querySelector('.pps-chevron');
if(!body)return;
var open=body.style.display!=='none';
body.style.display=open?'none':'block';
if(chev)chev.innerHTML=open?'&#9660;':'&#9650;';
});
}
}

function rRates(){
document.getElementById('rtbl').innerHTML='<table style="border-collapse:collapse;width:100%;min-width:640px"><thead><tr style="border-bottom:0.5px solid var(--b2)">'+
['Trust','Hospital','Ward/grade','Pay D','Pay N','Pay S','Charge D','Charge N','Margin D'].map(function(h,i){return '<th style="text-align:'+(i>2?'right':'left')+';font-size:11px;font-weight:500;color:var(--t2);padding:0 '+(i>2?'0':'7px')+' 8px '+(i===0?'0':'7px')+';text-transform:uppercase;letter-spacing:.05em">'+h+'</th>';}).join('')+
'</tr></thead><tbody>'+
R.map(function(r){return '<tr style="border-bottom:0.5px solid var(--b1)"><td style="padding:6px 0;font-size:12px" class="m">'+esc(r.trust)+'</td><td style="padding:6px 7px" class="fw">'+esc(r.hospital)+'</td><td style="padding:6px 7px;font-size:12px" class="m">'+esc(r.ward||'')+'</td><td style="padding:6px 0;text-align:right" class="fw">\u00a3'+r.pd+'</td><td style="padding:6px 0;text-align:right;font-size:12px" class="m">\u00a3'+r.pn+'</td><td style="padding:6px 0;text-align:right;font-size:12px" class="m">\u00a3'+r.ps+'</td><td style="padding:6px 0;text-align:right" class="fw">\u00a3'+r.cd+'</td><td style="padding:6px 0;text-align:right;font-size:12px" class="m">\u00a3'+r.cn+'</td><td style="padding:6px 0;text-align:right;color:var(--grtx)" class="fw">\u00a3'+r.md+'</td></tr>';}).join('')+
'</tbody></table>';
}

/* NAV */
var _curRotaHosp=null;
var _editHosp=null;
var candEdits={};
var candFilter='active';
try{var _ce=localStorage.getItem('cand_edits');if(_ce)candEdits=JSON.parse(_ce);}catch(e){}
function saveCE(){try{localStorage.setItem('cand_edits',JSON.stringify(candEdits));}catch(e){}}
function getC(idx){
// Returns merged candidate: base C[idx] + any edits
var base=C[idx]||{};
var ed=candEdits[idx]||{};
return Object.assign({},base,ed);
}
var rotaOverrides={};
try{var _ro=localStorage.getItem('rota_overrides');if(_ro)rotaOverrides=JSON.parse(_ro);}catch(e){}
function saveRO(){try{localStorage.setItem('rota_overrides',JSON.stringify(rotaOverrides));}catch(e){}}
function getRO(wk,trust,ci,di){
return((rotaOverrides[wk]||{})[trust]||{})[ci+'_'+di]||'';
}
function setRO(wk,trust,ci,di,val){
if(!rotaOverrides[wk])rotaOverrides[wk]={};
if(!rotaOverrides[wk][trust])rotaOverrides[wk][trust]={};
if(val)rotaOverrides[wk][trust][ci+'_'+di]=val;
else delete rotaOverrides[wk][trust][ci+'_'+di];
saveRO();
}
var rotaExclusions={};
var hospEdits={};
var trustEdits=[];
try{var _te=localStorage.getItem('trust_edits');if(_te)trustEdits=JSON.parse(_te);}catch(e){}
function saveTrustEdits(){try{localStorage.setItem('trust_edits',JSON.stringify(trustEdits));}catch(e){}}
// Restore user-added trusts into HC and TRUST_CARDS on load
trustEdits.forEach(function(t){
if(!t.isNew)return;
if(!HC.find(function(h){return h.name===t.name;}))
HC.push({name:t.name,area:t.area||'',pps:0,total:0,weekly:[],contacts:[],sites:[t.name]});
if(!TRUST_CARDS.find(function(tc){return tc.name===t.name;}))
TRUST_CARDS.push({name:t.name,fullName:t.fullName||t.name,area:t.area||'',color:'#1a5276',sites:[{name:t.name,img:''}]});
});
try{var _he=localStorage.getItem('hosp_edits');if(_he)hospEdits=JSON.parse(_he);}catch(e){}
function saveHE(){try{localStorage.setItem('hosp_edits',JSON.stringify(hospEdits));}catch(e){}}
function gHE(n){if(!hospEdits[n])hospEdits[n]={processes:[],issues:[],contacts:[],rota:[],personalRates:[],rates:[],avgHours:0,selectedRate:-1};return hospEdits[n];}
function delHEItem(section,idx){var hospName=_editHosp;if(!hospName)return;
var e=gHE(hospName);
if(e[section])e[section].splice(idx,1);
saveHE();openHosp(hospName);
}
function showEF(id){
// Hide all open forms first
document.querySelectorAll('.ef').forEach(function(f){f.style.display='none';});
var el=document.getElementById(id);
if(el)el.style.display='block';
}
function hideEF(id){var el=document.getElementById(id);if(el)el.style.display='none';}
function addProcess(){var hn=_editHosp;if(!hn)return;
var a=document.getElementById('ef-proc-action').value.trim();
var d=document.getElementById('ef-proc-day').value.trim();
var t=document.getElementById('ef-proc-time').value.trim();
if(!a)return;
gHE(hn).processes.push({action:a,day:d,time:t});
saveHE();openHosp(hn);
}
function editIssueTitle(){
showEF('ef-iss-title');
var inp=document.getElementById('ef-iss-title-input');
if(inp){inp.focus();inp.select();}
}

function saveIssueTitle(){
var hn=_editHosp;if(!hn)return;
var inp=document.getElementById('ef-iss-title-input');
if(!inp)return;
var val=inp.value.trim()||'Common issues';
gHE(hn).issuesTitle=val;
saveHE();
// Update display inline without full re-render
var disp=document.getElementById('iss-title-display');
if(disp)disp.textContent=val;
hideEF('ef-iss-title');
}


function addIssue(){var hn=_editHosp;if(!hn)return;
var iss=document.getElementById('ef-iss-issue').value.trim();
var res=document.getElementById('ef-iss-res').value.trim();
if(!iss)return;
gHE(hn).issues.push({issue:iss,resolution:res});
saveHE();openHosp(hn);
}
function hospAddLog(hospName){
var safeId=hospName.replace(/[^a-z0-9]/gi,'_');
var tag=(document.getElementById('hosp-log-tag-'+safeId)||{}).value||'';
var note=((document.getElementById('hosp-log-note-'+safeId)||{}).value||'').trim();
if(!note)return;
addHospActivityEntry(hospName,note,tag,false);
openHosp(hospName);
}

function hospDeleteLog(hospName,entryId){
if(!_hospActivity[hospName])return;
_hospActivity[hospName]=_hospActivity[hospName].filter(function(e){return e.id!==entryId;});
saveHospActivity();
openHosp(hospName);
}


function addContact(){var hn=_editHosp;if(!hn)return;
var nm=document.getElementById('ef-ct-name').value.trim();
var ti=document.getElementById('ef-ct-title').value.trim();
var dp=document.getElementById('ef-ct-dept').value.trim();
var em=document.getElementById('ef-ct-email').value.trim();
var ph=document.getElementById('ef-ct-phone').value.trim();
if(!nm)return;
var isPrimary=document.getElementById('ef-ct-primary')&&document.getElementById('ef-ct-primary').checked;
if(isPrimary){
// Clear primary flag from all existing contacts
var allCts=(gHE(hn).contacts||[]).concat([]);
allCts.forEach(function(c){c.primary=false;});
// Also clear from base HC contacts
var hcEntry=HC.find(function(h){return h.name===hn;});
if(hcEntry&&hcEntry.contacts)hcEntry.contacts.forEach(function(c){c.primary=false;});
}
gHE(hn).contacts.push({name:nm,title:ti,dept:dp,email:em,phone:ph,lastContacted:'',primary:!!isPrimary});
saveHE();openHosp(hn);
}
function filterRotaSel(){
var q=(document.getElementById('ef-ro-search').value||'').toLowerCase();
var sel=document.getElementById('ef-ro-sel');
if(!sel)return;
Array.from(sel.options).forEach(function(opt){
var txt=opt.text.toLowerCase();
opt.style.display=(!q||txt.includes(q))?'':'none';
});
}


function addRota(){var hn=_editHosp;if(!hn)return;
var sel=document.getElementById('ef-ro-sel');
if(!sel||sel.selectedIndex<0)return;
var idx=+sel.value;
var cand=C[idx];
if(!cand)return;
gHE(hn).rota.push({name:cand.n,spec:cand.s});
// Add hospital to candidate's sites[]
if(!cand.sites)cand.sites=[];
if(cand.sites.indexOf(hn)<0)cand.sites.push(hn);
if(!candEdits[idx])candEdits[idx]={};
candEdits[idx].sites=cand.sites.slice();
saveCE();
saveHE();openHosp(hn);
}function calcPPS(hospName, rotaList, personalRatesList, selectedRateCard, avgHours){
// Returns {std, blended, breakdown[]}
if(!selectedRateCard||!avgHours||avgHours<=0) return null;
var chargeDay = selectedRateCard.cd||0;
var payDay = selectedRateCard.pd||0;
if(!chargeDay||!payDay) return null;
var stdMargin = Math.round((chargeDay - payDay) * avgHours * 100) / 100;
var stdPPS = stdMargin;

// Blended: for each person on rota, use their personal rate if they have one
var excl = rotaExclusions[hospName]||{};
var activeRota = rotaList.filter(function(w){ return !excl[w.name||w.n]; });
if(!activeRota.length) return {std:stdPPS, blended:stdPPS, breakdown:[]};

var breakdown = [];
var totalMargin = 0;
activeRota.forEach(function(w){
var wName = w.name||w.n||'';
var personalEntry = personalRatesList.find(function(p){ return p.name===wName; });
var effectivePay = personalEntry ? personalEntry.rate : payDay;
var margin = Math.round((chargeDay - effectivePay) * avgHours * 100) / 100;
totalMargin += margin;
breakdown.push({
name: wName,
spec: w.spec||w.s||'',
pay: effectivePay,
isPersonal: !!personalEntry,
margin: margin
});
});
var blendedPPS = Math.round(totalMargin / activeRota.length * 100) / 100;
return {std:stdPPS, blended:blendedPPS, breakdown:breakdown};
}


function saveHospConfig(){
var hn=_editHosp;if(!hn)return;
var hrs=parseFloat(document.getElementById('cfg-hours').value)||0;
var rateIdx=parseInt(document.getElementById('cfg-rate').value);
gHE(hn).avgHours=hrs;
gHE(hn).selectedRate=isNaN(rateIdx)?-1:rateIdx;
saveHE();openHosp(hn);
}


function getHospPPS(hospName){
// Returns the best available PPS: calculated if configured, else hardcoded
var hObj=HC.find(function(x){return x.name===hospName;})||{};
var ed=gHE(hospName);
var avgHours=ed.avgHours||0;
var selIdx=ed.selectedRate!=null?ed.selectedRate:-1;
var allRates=(hObj.rates||[]).concat(ed.rates||[]);
var selRate=selIdx>=0?allRates[selIdx]:null;
if(selRate&&avgHours>0){
// Use calculated blended PPS
var rotaList=(hObj.rota||[]).concat(ed.rota||[]);
var prList=(hObj.personalRates||[]).concat(ed.personalRates||[]);
var result=calcPPS(hospName,rotaList,prList,selRate,avgHours);
if(result)return result.blended;
}
return hObj.pps||0;
}


function addRateCard(){
var hn=_editHosp;if(!hn)return;
var ward=document.getElementById('ef-rc-ward').value.trim();
var pd=parseFloat(document.getElementById('ef-rc-pd').value)||0;
var pn=parseFloat(document.getElementById('ef-rc-pn').value)||0;
var ps=parseFloat(document.getElementById('ef-rc-ps').value)||0;
var cd=parseFloat(document.getElementById('ef-rc-cd').value)||0;
var cn=parseFloat(document.getElementById('ef-rc-cn').value)||0;
var cs=parseFloat(document.getElementById('ef-rc-cs').value)||0;
if(!ward||!pd||!cd){alert('Ward/grade, pay day and charge day are required');return;}
var md=Math.round((cd-pd)*100)/100;
if(!gHE(hn).rates)gHE(hn).rates=[];
gHE(hn).rates.push({ward:ward,hospital:hn,pd:pd,pn:pn,ps:ps,cd:cd,cn:cn,cs:cs,md:md});
saveHE();openHosp(hn);
}


function addPersonalRate(){
var hn=_editHosp;if(!hn)return;
var sel=document.getElementById('ef-pr-sel');
if(!sel||!sel.value&&sel.value!=='0')return;
var wi=+sel.value;
// Get staff on system list for this hospital
var hObj=HC.find(function(x){return x.name===hn;})||{};
var ed=gHE(hn);
var staffList=(hObj.rota||[]).concat(ed.rota||[]);
var w=staffList[wi];
if(!w)return;
var rt=parseFloat(document.getElementById('ef-pr-rate').value)||0;
if(!rt){alert('Please enter a rate');return;}
var allRates=(hObj.personalRates||[]).concat(ed.personalRates||[]);
if(allRates.some(function(p){return p.name===w.name;})){
alert(w.name+' already has a personalised rate for this hospital');return;
}
ed.personalRates.push({name:w.name,spec:w.spec,rate:rt});
saveHE();openHosp(hn);
}
function updateRosterLink(){var hn=_editHosp;if(!hn)return;
var val=document.getElementById('ef-roster-link').value.trim();
gHE(hn).rosterLink=val;
saveHE();openHosp(hn);
}
try{var _re=localStorage.getItem('rota_excl');if(_re)rotaExclusions=JSON.parse(_re);}catch(e){}

function toggleRotaCand(hospName, candName){
if(!hospName||!candName)return;
if(!rotaExclusions[hospName])rotaExclusions[hospName]={};
rotaExclusions[hospName][candName]=!rotaExclusions[hospName][candName];
try{localStorage.setItem('rota_excl',JSON.stringify(rotaExclusions));}catch(e){}
openHosp(hospName);
}


function rotaNav(dir,e){
if(e){e.preventDefault();e.stopPropagation();}
// Rota navigation now moves shift entry week too (single source of truth)
chWk(dir);
if(_curRotaHosp)openHosp(_curRotaHosp);
}

function copyRota(e){
e.preventDefault();e.stopPropagation();
var _rw=getRotaWk();
var dates=_rw.dates||[];
// Use synced rota (staff on system as source of truth)
var _h=HC.find(function(x){return x.name===_curRotaHosp;});
var _ed=gHE(_curRotaHosp);
var _staffList=(_h?_h.rota:[]).concat(_ed.rota||[]);
var _rawRota2=(_rw.rotas&&_rw.rotas[_curRotaHosp])||[];
var hRota=_staffList.map(function(w){
var existing=_rawRota2.find(function(r){return r.n===w.name;});
return existing||{n:w.name,s:w.spec,c:dates.map(function(){return'';})};
});
if(!hRota.length){alert('No rota data to copy');return;}

// Build plain text table for email
var lines=[];
var hdr='Name Skill '+dates.join(' ');
lines.push(hdr);
lines.push(Array(hdr.length+1).join('-'));

var _excl3=rotaExclusions[_curRotaHosp]||{};
hRota.filter(function(c){return !_excl3[c.n];}).forEach(function(c){
var cells=(c.c||[]).map(function(v){
if(!v)return'';
if(v==='A')return'Available';
if(v==='U')return'Unavailable';
if(v==='T')return'TBC';
return v;
});
// Pad name to ~30 chars for alignment
var name=c.n.length>28?c.n.slice(0,27)+'..':c.n;
lines.push(name+' '+c.s+' '+cells.join(' '));
});

// Also build HTML table for rich email clients
var htmlLines=['<table border="1" cellpadding="4" cellspacing="0" style="border-collapse:collapse;font-family:Arial,sans-serif;font-size:12px">'];
htmlLines.push('<tr style="background:#e8f0fa"><th>Name</th><th>Skill</th>'+dates.map(function(d){return'<th>'+d+'</th>';}).join('')+'</tr>');
hRota.filter(function(c){return !_excl3[c.n];}).forEach(function(c){
htmlLines.push('<tr>');
htmlLines.push('<td style="white-space:nowrap;font-weight:500">'+c.n+'</td>');
htmlLines.push('<td style="color:#666">'+c.s+'</td>');
(c.c||[]).forEach(function(v){
var bg='',col='',txt='';
if(!v){bg='';txt='';}
else if(v==='A'){bg='#faf0df';col='#a06010';txt='Available';}
else if(v==='U'){bg='#e8e6e0';col='#5c5b52';txt='Unavailable';}
else if(v==='T'){bg='#e8f0fa';col='#1558a0';txt='TBC';}
else{bg='#e2f4ec';col='#157a52';txt=v;}
htmlLines.push('<td style="background:'+bg+';color:'+col+';text-align:center;white-space:nowrap;font-weight:500">'+txt+'</td>');
});
htmlLines.push('</tr>');
});
htmlLines.push('</table>');

var plainText=lines.join('\n');
var htmlText=htmlLines.join('');

// Copy HTML table - works in Outlook/Gmail via hidden textarea trick
var copyDiv=document.createElement('div');
copyDiv.style.cssText='position:fixed;left:-9999px;top:0;opacity:0';
copyDiv.contentEditable='true';
copyDiv.innerHTML=htmlText;
document.body.appendChild(copyDiv);
var sel=window.getSelection();
var range=document.createRange();
range.selectNodeContents(copyDiv);
sel.removeAllRanges();
sel.addRange(range);
var ok=false;
try{ok=document.execCommand('copy');}catch(ex){}
sel.removeAllRanges();
document.body.removeChild(copyDiv);
var btn=document.getElementById('copy-rota-btn');
if(ok){
if(btn){btn.textContent='Copied \u2713';btn.style.color='var(--grtx)';setTimeout(function(){btn.textContent='Copy grid';btn.style.color='';},2500);}
} else {
// Last resort - plain text via clipboard API
navigator.clipboard.writeText(plainText).catch(function(){});
if(btn){btn.textContent='Copied (plain)';setTimeout(function(){btn.textContent='Copy grid';},2500);}
}
}


function rotaChange(sel){
var val=sel.value;
var ci=+sel.dataset.ci,di=+sel.dataset.di,hn=sel.dataset.hn;
var wk=getRotaWkKey();
// Get candidate from active staff list (same order as rendered)
var hObj=HC.find(function(x){return x.name===hn;})||{};
var ed=gHE(hn);
var staffList=(hObj.rota||[]).concat(ed.rota||[]);
var excl=rotaExclusions[hn]||{};
var activeStaff=staffList.filter(function(w){return !excl[w.name||w.n];});
var candObj=activeStaff[ci];
var candName=candObj?(candObj.name||candObj.n||''):'';
if(!candName)return;
var candIdx=getCandIdx(candName);
var encoded=val===''?'':val==='available'?'A':val==='unavailable'?'U':val==='tbc'?'T':val;
var isBooking=(encoded&&encoded!=='A'&&encoded!=='U'&&encoded!=='T');
if(isBooking){
// Conflict check
var conflict=checkConflict(candName,wk,di,hn);
if(conflict){
if(!confirm(candName+' is already booked at '+conflict+' on '+DAYS[di]+'. Book at '+hn+' ('+val+') instead?')){
sel.value=''; return;
}
}
// Write booking to sd
if(!sd[wk])sd[wk]={};
if(!sd[wk][candIdx])sd[wk][candIdx]={};
sd[wk][candIdx][di]=encoded;
setRO(wk,hn,ci,di,'');
syncRotaToShift(wk,hn,candName,di,encoded);
} else {
// Manual availability \u2014 clear sd booking, store override
if(candIdx>=0&&sd[wk]&&sd[wk][candIdx])delete sd[wk][candIdx][di];
setRO(wk,hn,ci,di,encoded);
syncRotaToShift(wk,hn,candName,di,encoded);
}
// Restyle select
var bg='transparent',col='var(--t3)';
if(encoded==='A'){bg='#faf0df';col='#a06010';}
else if(encoded==='U'){bg='#e8e6e0';col='#5c5b52';}
else if(encoded==='T'){bg='#e8f0fa';col='#1558a0';}
else if(encoded){bg='#e2f4ec';col='#157a52';}
sel.style.background=bg;sel.style.color=col;
rFoot();uMet();rDash();aS();
}


var _bookingPages=['shifts','summary','candidates','hospitals','rates','rostercheck','documents','pipeline'];
var _payrollPages=['timesheets','payonly','selfbill','placement','payqueries','divcon'];

function gp(id){
document.querySelectorAll('.pg').forEach(function(p){p.classList.remove('on');});
document.querySelectorAll('.ntab,.ngrp-item,.ngrp-btn').forEach(function(t){t.classList.remove('on');});
document.getElementById('pg-'+id).classList.add('on');
var tabEl=document.getElementById('tab-'+id);
if(tabEl)tabEl.classList.add('on');
// Highlight parent group button
if(_bookingPages.indexOf(id)>=0){
var btn=document.getElementById('ngrp-bookings-btn');
if(btn)btn.classList.add('on');
}
if(_payrollPages.indexOf(id)>=0){
var btn2=document.getElementById('ngrp-payroll-btn');
if(btn2)btn2.classList.add('on');
}
closeDD();
if(id==='summary')rSum();
if(id==='candidates')rCands();
if(id==='hospitals')rHosps();
if(id==='rates')rRates();
if(id==='timesheets'){rTS();populateTSDatalists();}
if(id==='payonly'){rPO();populatePODatalists();poInitDrop();}
if(id==='rostercheck')rRC();
if(id==='documents')rDocs();
if(id==='pipeline')rPipeline();
if(id==='selfbill'){rSB();populateSBDatalists();sbInitDrop();}
if(id==='placement'){
rLP();
lpInitDrop();
var lc=document.getElementById('lp-cand-list');
if(lc)lc.innerHTML=C.filter(function(c){return c.ac!=='Inactive';}).map(function(c){return'<option value="'+esc(c.n)+'"></option>';}).join('');
var lcl=document.getElementById('lp-client-dlist');
if(lcl)lcl.innerHTML=getAllTrustNames().map(function(n){return'<option value="'+esc(n)+'"></option>';}).join('');
}
if(id==='dashboard')rDash();
if(id==='payqueries')rPQ();
if(id==='divcon')rDivCon();
if(id==='todo'){rTodo();}
}

// Restore user-added trusts
trustEdits.forEach(function(t){
if(!HC.find(function(h){return h.name===t.name;})){
HC.push({name:t.name,area:t.area||'',pps:0,total:0,weekly:[],processes:[],rota:[],issues:[],roster_link:'',contacts:[],rates:[],personalRates:[]});
H.push({name:t.name,area:t.area||'',pps:0,total:0});
}
if(!TRUST_SITES[t.name])TRUST_SITES[t.name]=t.sites||[t.name];
});


// Global data-hide handler for forms outside openHosp
document.addEventListener('click',function(e){
if(e.target.dataset&&e.target.dataset.hide){
var el=document.getElementById(e.target.dataset.hide);
if(el)el.style.display='none';
}
});


var TS_BASE=[]
var tsEdits=[];
try{var _ts=localStorage.getItem('ts_edits');if(_ts)tsEdits=JSON.parse(_ts);}catch(e){}
function saveTS(){try{localStorage.setItem('ts_edits',JSON.stringify(tsEdits));}catch(e){}}
function getAllTS(){return TS_BASE.concat(tsEdits);}

var tsFilter={trust:'',day:'',q:''};

var _tsSel={name:'',spec:'',hosp:''};

function tsSessToday(){
var d=new Date();
var dateEl=document.getElementById('ts-sess-date');
if(dateEl)dateEl.value=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
tsDeriveDay();
}

function tsDeriveDay(){
var dateEl=document.getElementById('ts-sess-date');
var dayEl=document.getElementById('ts-sess-day');
var lbl=document.getElementById('ts-sess-lbl');
if(!dateEl||!dateEl.value)return;
var dayNames=['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
var months=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
var parts=dateEl.value.split('-');
var d=new Date(+parts[0],+parts[1]-1,+parts[2]);
if(dayEl)dayEl.value=dayNames[d.getDay()];
if(lbl)lbl.textContent=dayNames[d.getDay()]+' '+d.getDate()+' '+months[d.getMonth()]+' '+d.getFullYear();
}

function tsUpdateSessLbl(){
tsDeriveDay(); // day always derived from date
}

function tsCandSearch(){
var q=(document.getElementById('ts-q').value||'').toLowerCase().trim();
var drop=document.getElementById('ts-cand-drop');
if(!drop)return;
if(!q){drop.style.display='none';return;}
var matches=C.filter(function(c){
return c.ac!=='Inactive'&&(c.n||'').toLowerCase().includes(q);
}).slice(0,12);
if(!matches.length){drop.style.display='none';return;}
drop.innerHTML=matches.map(function(c,i){
return '<div class="ts-cand-opt" data-idx="'+C.indexOf(c)+'" style="padding:8px 12px;cursor:pointer;font-size:13px;border-bottom:0.5px solid var(--b1)">'
+'<span style="font-weight:500">'+esc(c.n)+'</span>'
+' <span style="font-size:11px;color:var(--t2)">'+esc(c.s||'')+'</span>'
+(c.h?'<span style="font-size:11px;color:var(--t3);float:right">'+esc(c.h)+'</span>':'')
+'</div>';
}).join('');
drop.style.display='block';
drop.querySelectorAll('.ts-cand-opt').forEach(function(el){
el.addEventListener('mousedown',function(e){
e.preventDefault();
var idx=+this.dataset.idx;
var c=C[idx];
if(!c)return;
_tsSel={name:c.n,spec:c.s||'',hosp:c.h||''};
document.getElementById('ts-q').value='';
drop.style.display='none';
document.getElementById('ts-sel-name').textContent=c.n;
document.getElementById('ts-sel-spec').textContent=c.s||'';
document.getElementById('ts-selected-row').style.display='block';
// Auto-fill trust from main hospital
var trustEl=document.getElementById('ts-trust');
if(trustEl&&c.h&&!trustEl.value)trustEl.value=c.h;
// Focus shifts
var shiftsEl=document.getElementById('ts-shifts');
if(shiftsEl)shiftsEl.focus();
});
el.addEventListener('mouseover',function(){this.style.background='var(--su2)';});
el.addEventListener('mouseout',function(){this.style.background='';});
});
}

function tsClearCand(){
_tsSel={name:'',spec:'',hosp:''};
document.getElementById('ts-selected-row').style.display='none';
document.getElementById('ts-q').value='';
document.getElementById('ts-trust').value='';
}

var _tsCalYear=0, _tsCalMonth=0, _tsSelDates=[];

function tsToggleCal(){
var cal=document.getElementById('ts-cal');
if(!cal)return;
if(cal.style.display==='none'){
// Init to session date month or today
var dateEl=document.getElementById('ts-sess-date');
var ref=dateEl&&dateEl.value?new Date(dateEl.value.replace(/-/g,'/')):new Date();
_tsCalYear=ref.getFullYear();
_tsCalMonth=ref.getMonth();
tsRenderCal();
cal.style.display='block';
} else {
cal.style.display='none';
}
}

function tsCalNav(dir){
_tsCalMonth+=dir;
if(_tsCalMonth<0){_tsCalMonth=11;_tsCalYear--;}
if(_tsCalMonth>11){_tsCalMonth=0;_tsCalYear++;}
tsRenderCal();
}

function tsRenderCal(){
var months=['January','February','March','April','May','June','July','August','September','October','November','December'];
var lbl=document.getElementById('ts-cal-lbl');
if(lbl)lbl.textContent=months[_tsCalMonth]+' '+_tsCalYear;
var grid=document.getElementById('ts-cal-grid');
if(!grid)return;
var html='';
// Day headers
['M','T','W','T','F','S','S'].forEach(function(d){
html+='<div style="font-size:10px;font-weight:500;color:var(--t2);padding:2px 0">'+d+'</div>';
});
// First day of month (Mon=0)
var first=new Date(_tsCalYear,_tsCalMonth,1);
var startOffset=(first.getDay()+6)%7; // 0=Mon
for(var i=0;i<startOffset;i++)html+='<div></div>';
var daysInMonth=new Date(_tsCalYear,_tsCalMonth+1,0).getDate();
for(var d2=1;d2<=daysInMonth;d2++){
var dateStr=_tsCalYear+'-'+String(_tsCalMonth+1).padStart(2,'0')+'-'+String(d2).padStart(2,'0');
var sel=_tsSelDates.indexOf(dateStr)>=0;
var style='padding:3px 0;border-radius:4px;cursor:pointer;font-size:12px;'
+(sel?'background:var(--bl);color:#fff;font-weight:500;':'color:var(--tx);');
html+='<div class="ts-cal-day" data-date="'+dateStr+'" style="'+style+'">'+d2+'</div>';
}
grid.innerHTML=html;
grid.querySelectorAll('.ts-cal-day').forEach(function(el){
el.addEventListener('click',function(e){
e.stopPropagation();
var dt=this.dataset.date;
var idx=_tsSelDates.indexOf(dt);
if(idx>=0)_tsSelDates.splice(idx,1);
else _tsSelDates.push(dt);
_tsSelDates.sort();
tsRenderCal();
tsUpdateDatesBtn();
});
});
}

function tsUpdateDatesBtn(){
var btn=document.getElementById('ts-dates-btn');
var inp=document.getElementById('ts-dates');
var shiftsHid=document.getElementById('ts-shifts');
var shiftsLbl=document.getElementById('ts-shifts-lbl');
if(!btn||!inp)return;
if(!_tsSelDates.length){
btn.textContent='Pick dates\u2026';
btn.style.color='var(--t2)';
inp.value='';
if(shiftsHid)shiftsHid.value='0';
if(shiftsLbl)shiftsLbl.textContent='\u2014';
return;
}
var formatted=tsFmtDates(_tsSelDates);
btn.textContent=formatted;
btn.style.color='var(--tx)';
inp.value=formatted;
// Shifts = number of selected dates
var count=_tsSelDates.length;
if(shiftsHid)shiftsHid.value=String(count);
if(shiftsLbl){
shiftsLbl.textContent=count;
shiftsLbl.style.color='var(--tx)';
shiftsLbl.style.fontWeight='500';
}
}

function tsFmtDates(dates){
if(!dates.length)return'';
var fmt=function(s){
var p=s.split('-');
return p[2]+'/'+p[1];
};
if(dates.length===1)return fmt(dates[0]);
// Check if consecutive range
var isRange=true;
for(var i=1;i<dates.length;i++){
var prev=new Date(dates[i-1]);var curr=new Date(dates[i]);
var diff=(curr-prev)/(1000*60*60*24);
if(diff!==1){isRange=false;break;}
}
if(isRange)return fmt(dates[0])+'\u2013'+fmt(dates[dates.length-1]);
return dates.map(fmt).join(', ');
}

function tsClearDates(){
_tsSelDates=[];
tsRenderCal();
tsUpdateDatesBtn();
}

function tsConfirmDates(){
var cal=document.getElementById('ts-cal');
if(cal)cal.style.display='none';
}


function addTimesheet(){
var sub=(document.getElementById('ts-sess-date')||{value:''}).value||'';
var day=(document.getElementById('ts-sess-day')||{value:''}).value||'';
var shifts=parseInt((document.getElementById('ts-shifts')||{value:'0'}).value)||0;
var cand=_tsSel.name;
var dates=(document.getElementById('ts-dates')||{value:''}).value.trim();
var trust=(document.getElementById('ts-trust')||{value:''}).value.trim();
if(!cand){alert('Please select a candidate first');return;}
if(!sub){alert('Please set the session date at the top');return;}
if(!shifts||!dates){alert('Please pick at least one shift date');return;}
tsEdits.push([sub,shifts,cand,dates,trust,day]);
saveTS();
// Clear entry fields but keep session + candidate for fast repeat entry
document.getElementById('ts-shifts').value='';
document.getElementById('ts-dates').value='';
document.getElementById('ts-shifts').value='0';
var shiftsLbl=document.getElementById('ts-shifts-lbl');
if(shiftsLbl){shiftsLbl.textContent='\u2014';shiftsLbl.style.color='';shiftsLbl.style.fontWeight='';}
_tsSelDates=[];
var dBtn=document.getElementById('ts-dates-btn');
if(dBtn){dBtn.textContent='Pick dates\u2026';dBtn.style.color='var(--t2)';}
// Keep trust filled for same-trust batch, clear candidate
tsClearCand();
rTS();
populateTSDatalists();
// Focus back to candidate search
var q=document.getElementById('ts-q');
if(q)q.focus();
}

function deleteTS(idx){
// idx into tsEdits (not TS_BASE)
if(!confirm('Delete this timesheet entry?'))return;
tsEdits.splice(idx,1);
saveTS();
rTS();
}

function rTS(){
var all=getAllTS();
var q=(tsFilter.q||'').toLowerCase();
var tf=(tsFilter.trust||'').toLowerCase();
var df=(tsFilter.day||'').toLowerCase();
var filtered=all.filter(function(r,i){
if(tf&&!(r[4]||'').toLowerCase().includes(tf))return false;
if(df&&!(r[5]||'').toLowerCase().includes(df))return false;
if(q&&!((r[2]||'')+(r[4]||'')+(r[3]||'')).toLowerCase().includes(q))return false;
return true;
});
// Summary stats
var totalShifts=filtered.reduce(function(s,r){return s+(r[1]||0);},0);
var byDay={};
filtered.forEach(function(r){var d=r[5]||'Unknown';byDay[d]=(byDay[d]||0)+(r[1]||0);});
var byTrust={};
filtered.forEach(function(r){var t=r[4]||'Unknown';byTrust[t]=(byTrust[t]||0)+(r[1]||0);});
// Render stats
var statsEl=document.getElementById('ts-stats');
if(statsEl){
statsEl.innerHTML='<span style="font-size:13px;font-weight:500">'+filtered.length+' records &middot; '+totalShifts+' shifts</span>';
}
// Totals panel
var totalsEl=document.getElementById('ts-totals');
var dayTotalsEl=document.getElementById('ts-day-totals');
var weekTotalEl=document.getElementById('ts-week-total');
var entryCountEl=document.getElementById('ts-entry-count');
if(totalsEl){
totalsEl.style.display=tsEdits.length?'block':'none';
var allDays=['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday'];
if(dayTotalsEl){
dayTotalsEl.innerHTML=allDays.map(function(d){
var cnt=byDay[d]||0;
return '<div style="text-align:center;padding:8px 4px;background:var(--su2);border-radius:var(--r)">'
+'<div style="font-size:18px;font-weight:500;color:'+(cnt>0?'var(--bl)':'var(--t3)')+'">'+cnt+'</div>'
+'<div style="font-size:10px;color:var(--t2);text-transform:uppercase;letter-spacing:.04em">'+d.slice(0,3)+'</div>'
+'</div>';
}).join('');
}
if(weekTotalEl)weekTotalEl.textContent=totalShifts;
if(entryCountEl)entryCountEl.textContent=filtered.length;
}
// Render table
var tbody=document.getElementById('ts-tbody');
if(!tbody)return;
if(!filtered.length){
var msg=tsEdits.length===0
?'No timesheets logged yet \u2014 use the form above to add the first one'
:'No records match your filters';
tbody.innerHTML='<tr><td colspan="7" style="padding:24px;text-align:center;color:var(--t3);font-size:13px">'+msg+'</td></tr>';
return;
}
// Show most recent first \u2014 track tsEdits index for delete
var indexedFiltered=[];
for(var _i=0;_i<tsEdits.length;_i++){
var r=tsEdits[_i];
var tf2=(tsFilter.trust||'').toLowerCase();
var df2=(tsFilter.day||'').toLowerCase();
var q2=(tsFilter.q||'').toLowerCase();
if(tf2&&!(r[4]||'').toLowerCase().includes(tf2))continue;
if(df2&&!(r[5]||'').toLowerCase().includes(df2))continue;
if(q2&&!((r[2]||'')+(r[4]||'')+(r[3]||'')).toLowerCase().includes(q2))continue;
indexedFiltered.push({r:r,idx:_i});
}
indexedFiltered.reverse(); // most recent first
var rows=indexedFiltered.map(function(obj){
var r=obj.r;
var newIdx=obj.idx;
var isNew=true;
var si=0; // unused now
return '<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:6px 0;font-size:12px">'+esc(r[0]||'')+'</td>'
+'<td style="padding:6px 8px;font-size:12px;text-align:center;font-weight:500">'+((r[1]||0)||'\u2014')+'</td>'
+'<td style="padding:6px 8px;font-size:12px;font-weight:500">'+esc(r[2]||'')+'</td>'
+'<td style="padding:6px 8px;font-size:12px;color:var(--t2)">'+esc(r[3]||'')+'</td>'
+'<td style="padding:6px 8px;font-size:12px;color:var(--t2)">'+esc(r[4]||'')+'</td>'
+'<td style="padding:6px 8px;font-size:12px;color:var(--t2)">'+esc(r[5]||'')+'</td>'
+'<td style="padding:6px 0;text-align:right">'+(isNew?'<button class="delbtn ts-del-btn" data-ni="'+newIdx+'">&#215;</button>':'')+'</td>'
+'</tr>';
}).join('');
tbody.innerHTML=rows;
// Wire delete buttons
tbody.querySelectorAll('.ts-del-btn').forEach(function(btn){
btn.addEventListener('click',function(){deleteTS(+this.dataset.ni);});
});
}

function tsSetFilter(key,val){
tsFilter[key]=val;
rTS();
}


function populateTSDatalists(){
var tl=document.getElementById('ts-trust-list');
if(tl){tl.innerHTML=getAllTrustNames().map(function(n){return '<option value="'+esc(n)+'"></option>';}).join('');}
var tf=document.getElementById('ts-trust-filter');
if(tf){
var trusts=[];
tsEdits.forEach(function(r){if(r[4]&&trusts.indexOf(r[4])<0)trusts.push(r[4]);});
trusts.sort();
tf.innerHTML='<option value="">All trusts</option>'+
trusts.map(function(t){return '<option value="'+esc(t)+'">'+esc(t)+'</option>';}).join('');
}
tsInitSession();
}

function tsInitSession(){
var dateEl=document.getElementById('ts-sess-date');
if(!dateEl||dateEl.value)return; // already set
var d=new Date();
dateEl.value=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
tsDeriveDay();
}



// Init session bar listeners
document.addEventListener('DOMContentLoaded',function(){
var sd=document.getElementById('ts-sess-date');
var sy=document.getElementById('ts-sess-day');
if(sd)sd.addEventListener('change',tsUpdateSessLbl);
if(sy)sy.addEventListener('change',tsUpdateSessLbl);
// Close candidate dropdown on outside click
document.addEventListener('click',function(e){
var drop=document.getElementById('ts-cand-drop');
var q=document.getElementById('ts-q');
if(drop&&q&&!drop.contains(e.target)&&e.target!==q){
drop.style.display='none';
}
// Close calendar on outside click
var cal=document.getElementById('ts-cal');
var calBtn=document.getElementById('ts-dates-btn');
if(cal&&cal.style.display!=='none'&&!cal.contains(e.target)&&e.target!==calBtn){
cal.style.display='none';
}
});
});


var PO_BASE=[["Philip White", "Darent Valley", "Wednesday", "2023-05-17", "08:00", "18:30", 30.0, 10.0, 30.0, 33.15, "waiting for shifts to come on report", 331.5, 31.5, "Roster"], ["Philip White", "Darent Valley", "Thursday", "2023-05-18", "08:00", "18:00", 30.0, 9.5, 30.0, 33.15, "waiting for shifts to come on report", 314.93, 29.93, "Roster"], ["Philip White", "Darent Valley", "Friday", "2023-05-19", "08:00", "19:00", 30.0, 10.5, 30.0, 33.15, "waiting for shifts to come on report", 348.08, 33.08, "Roster"], ["Jane Pengelly", "Derriford", "Thursday", "2023-05-18", "08:00", "17:30", 30.0, 9.0, 45.0, 54.0, "waiting for shifts to come over on NHSP", 486.0, 81.0, "NHSP"], ["Jane Pengelly", "Derriford", "Friday", "2023-05-19", "08:00", "17:00", 30.0, 9.0, 45.0, 50.0, "waiting for shifts to come over on NHSP", 450.0, 45.0, "NHSP"], ["Nhamo Makamba", "Royal Surrey", "Monday", "2023-05-15", "08:00", "18:00", 30.0, 9.5, 35.0, 40.0, "waiting for shift to come over on NHSP", 380.0, 47.5, "HRoster"], ["Nhamo Makamba", "Royal Surrey", "Tuesday", "2023-05-16", "08:00", "18:00", 30.0, 9.5, 35.0, 40.0, "waiting for shift to come over on NHSP", 380.0, 47.5, "HRoster"], ["Nhamo Makamba", "Royal Surrey", "Wednesday", "2023-05-17", "08:00", "18:00", 30.0, 9.5, 35.0, 40.0, "waiting for shift to come over on NHSP", 380.0, 47.5, "HRoster"], ["Nhamo Makamba", "Royal Surrey", "Thursday", "2023-05-18", "08:00", "18:00", 30.0, 9.5, 35.0, 40.0, "waiting for shift to come over on NHSP", 380.0, 47.5, "HRoster"], ["Nhamo Makamba", "Royal Surrey", "Friday", "2023-05-19", "08:00", "18:00", 30.0, 9.5, 35.0, 40.0, "waiting for shift to come over on NHSP", 380.0, 47.5, "HRoster"], ["Jovanie Santos", "Ramsey North Downs", "Monday", "2023-05-15", "07:30", "18:30", 0, 10.5, 40.0, 43.19, "waiting for shifts to come over on E-Tips", 453.5, 33.5, "ETIPS"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2023-05-17", "07:30", "13:30", 0, 11.5, 40.0, 43.19, "waiting for shifts to come over on E-Tips", 496.69, 36.69, "ETIPS"], ["Buddah Gurung", "Royal Berkshire", "Wednesday", "2023-05-17", "07:30", "18:00", 0, 10.0, 29.5, 40.0, "waiting for shifts to come over on NHSP", 400.0, 105.0, "NHSP"], ["Patrick Gambold", "St. Mary's (IOW)", "Wednesday", "2023-05-10", "08:00", "11:30", 0, 3.5, 32.0, 34.98, "waiting for shift to come over on ID medical report", 122.43, 10.43, "Clairty"], ["Paula Ibanez", "Spire Wellessley", "Monday", "2023-05-22", "07:30", "17:00", 30.0, 9.5, 36.66, 40.3, "waiting for retinue report", 382.85, 34.58, "Spire/Retinue"], ["Olufunke Awotedu", "Derriford", "Monday", "2023-05-08", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over on NHSP", 513.0, 133.0, "NHSP"], ["Olufunke Awotedu", "Derriford", "Tuesday", "2023-05-09", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over on NHSP", 513.0, 133.0, "NHSP"], ["Olufunke Awotedu", "Derriford", "Wednesday", "2023-05-10", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over on NHSP", 513.0, 133.0, "NHSP"], ["Olufunke Awotedu", "Derriford", "Thursday", "2023-05-11", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over on NHSP", 513.0, 133.0, "NHSP"], ["Olufunke Awotedu", "Derriford", "Friday", "2023-05-12", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over on NHSP", 513.0, 133.0, "NHSP"], ["Tanya Williams", "Watford", "Thursday", "2023-05-18", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "awaiting shift to come over on NHSP", 391.0, 46.0, "NHSP"], ["Philip White", "Darent Valley", "Monday", "2023-05-22", "08:00", "20:30", 30.0, 12.0, 30.0, 33.15, "awaiting shift to come over on HRoster", 397.8, 37.8, "HRoster"], ["Philip White", "Darent Valley", "Tuesday", "2023-05-23", "08:00", "18:30", 30.0, 10.0, 30.0, 33.15, "awaiting shift to come over on HRoster", 331.5, 31.5, "HRoster"], ["Philip White", "Darent Valley", "Wednesday", "2023-05-24", "08:00", "18:00", 30.0, 9.5, 30.0, 33.15, "awaiting shift to come over on HRoster", 314.93, 29.93, "HRoster"], ["Philip White", "Darent Valley", "Thursday", "2023-05-25", "08:00", "18:00", 30.0, 9.5, 30.0, 33.15, "awaiting shift to come over on HRoster", 314.93, 29.93, "HRoster"], ["Gary Primmer", "Derriford", "Monday", "2023-05-22", "08:00", "21:00", 30.0, 12.5, 45.0, 54.0, "will come over on NHSP (Plymouth)", 675.0, 112.5, "NHSP"], ["Gary Primmer", "Derriford", "Tuesday", "2023-05-23", "08:00", "18:00", 30.0, 9.5, 45.0, 54.0, "will come over on NHSP (Plymouth)", 513.0, 85.5, "NHSP"], ["Gary Primmer", "Derriford", "Wednesday", "2023-05-24", "08:00", "21:00", 30.0, 12.5, 45.0, 54.0, "will come over on NHSP (Plymouth)", 675.0, 112.5, "NHSP"], ["Gary Primmer", "Derriford", "Thursday", "2023-05-25", "08:00", "18:00", 30.0, 9.5, 45.0, 54.0, "will come over on NHSP (Plymouth)", 513.0, 85.5, "NHSP"], ["Mark Shea", "Derriford", "Tuesday", "2023-05-23", "11:30", "21:00", 30.0, 9.0, 34.1, 54.0, "will come over on NHSP (Plymouth)", 486.0, 179.1, "NHSP"], ["Mark Shea", "Derriford", "Wednesday", "2023-05-24", "08:00", "18:00", 0.0, 10.0, 34.1, 54.0, "will come over on NHSP (Plymouth)", 540.0, 199.0, "NHSP"], ["Mark Shea", "Derriford", "Thursday", "2023-05-25", "08:00", "18:00", 30.0, 9.5, 34.1, 54.0, "will come over on NHSP (Plymouth)", 513.0, 189.05, "NHSP"], ["Mark Shea", "Derriford", "Friday", "2023-05-26", "08:00", "21:00", 60.0, 12.0, 34.1, 54.0, "will come over on NHSP (Plymouth)", 648.0, 238.8, "NHSP"], ["Mark Shea", "Derriford", "Saturday", "2023-05-27", "08:00", "21:00", 60.0, 12.0, 34.1, 54.0, "will come over on NHSP (Plymouth)", 648.0, 238.8, "NHSP"], ["Wayne Mcgeary", "Royal Berkshire", "Monday", "2023-05-22", "07:30", "18:00", 30.0, 10.0, 42.0, 45.0, "awaiting for shift to appear on NHSP", 450.0, 30.0, "NHSP"], ["Wayne Mcgeary", "Royal Berkshire", "Wednesday", "2023-05-24", "07:30", "18:00", 30.0, 10.0, 42.0, 45.0, "awaiting for shift to appear on NHSP", 450.0, 30.0, "NHSP"], ["Wayne Mcgeary", "Royal Berkshire", "Thursday", "2023-05-25", "07:30", "18:00", 30.0, 10.0, 42.0, 45.0, "awaiting for shift to appear on NHSP", 450.0, 30.0, "NHSP"], ["Wayne Mcgeary", "Royal Berkshire", "Friday", "2023-05-26", "07:30", "18:00", 30.0, 10.0, 42.0, 45.0, "awaiting for shift to appear on NHSP", 450.0, 30.0, "NHSP"], ["Jane Pengelly", "Derriford", "Thursday", "2023-05-25", "08:00", "18:15", 30.0, 9.75, 45.0, 54.0, "awaiting for shift to appear on NHSP", 526.5, 87.75, "NHSP"], ["Jane Pengelly", "Derriford", "Friday", "2023-05-26", "08:00", "18:00", 30.0, 9.5, 45.0, 54.0, "awaiting for shift to appear on NHSP", 513.0, 85.5, "NHSP"], ["Patrick Gambold", "Isle Of Wight", "Tuesday", "2023-05-23", "08:00", "11:30", 0, 3.5, 32.0, 34.94, "awaiting id medical report", 122.29, 10.29, "Clairty"], ["Patrick Gambold", "Isle Of Wight", "Wednesday", "2023-05-24", "08:00", "16:15", 30.0, 7.75, 32.0, 34.94, "awaiting id medical report", 270.79, 22.79, "Clairty"], ["Patrick Gambold", "Isle Of Wight", "Thursday", "2023-05-25", "08:00", "18:15", 30.0, 9.75, 32.0, 34.94, "awaiting id medical report", 340.67, 28.67, "Clairty"], ["Patrick Gambold", "Isle Of Wight", "Friday", "2023-05-26", "08:00", "17:15", 30.0, 8.75, 32.0, 34.94, "awaiting id medical report", 305.73, 25.73, "Clairty"], ["Dazia Dawn Moses-Biggs", "Royal Free (Chase Farm)", "Friday", "2023-05-05", "08:00", "20:00", 45.0, 11.25, 30.0, 32.1, "awaiitng HRoster report", 361.13, 23.63, "HRoster"], ["Dazia Dawn Moses-Biggs", "Royal Free (Chase Farm)", "Thursday", "2023-05-25", "08:00", "20:00", 45.0, 9.25, 30.0, 32.1, "awaiitng HRoster report", 296.93, 19.43, "HRoster"], ["Jovanie Santos", "Ramsey North Downs", "Monday", "2023-05-22", "07:30", "18:00", 30.0, 10.0, 40.0, 43.19, "awaiting next etips report", 431.9, 31.9, "ETIPS"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2023-05-31", "09:30", "18:00", 30.0, 8.0, 40.0, 43.19, "awaiting next etips report", 345.52, 25.52, "ETIPS"], ["Marichelle Alvarez", "Cromwell Hospital", "Tuesday", "2023-05-23", "13:00", "21:00", 30.0, 7.5, 38.0, 50.14, "will be on etips report", 376.05, 91.05, "ETIPS"], ["(Jimi) Gemima Redd", "Royal Berkshire", "Monday", "2023-05-22", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "will come over on NHSP", 380.0, 99.75, "NHSP"], ["(Jimi) Gemima Redd", "Royal Berkshire", "Tuesday", "2023-05-23", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "will come over on NHSP", 380.0, 99.75, "NHSP"], ["(Jimi) Gemima Redd", "Royal Berkshire", "Wednesday", "2023-05-24", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "will come over on NHSP", 380.0, 99.75, "NHSP"], ["(Jimi) Gemima Redd", "Royal Berkshire", "Friday", "2023-05-26", "08:00", "15:30", 30.0, 7.0, 29.5, 40.0, "will come over on NHSP", 280.0, 73.5, "NHSP"], ["Petru Suciu", "West Herts", "Friday", "2023-05-26", "08:00", "21:00", 30.0, 12.5, 25.97, 34.0, "will come over next week on NHSP", 425.0, 100.38, "NHSP"], ["Gary Primmer", "Derriford", "Wednesday", "2023-05-31", "08:00", "01:00", 60.0, 14.0, 40.0, 54.0, "Will come over on NHSP", 756.0, 196.0, "NHSP"], ["Gary Primmer", "Derriford", "Thursday", "2023-01-06", "08:00", "21:00", 30.0, 12.5, 40.0, 54.0, "Will come over on NHSP", 675.0, 175.0, "NHSP"], ["Gary Primmer", "Derriford", "Friday", "2023-02-06", "08:00", "21:00", 60.0, 12.0, 40.0, 54.0, "Will come over on NHSP", 648.0, 168.0, "NHSP"], ["Jane Pengelly", "Derriford", "Thursday", "2023-06-01", "08:00", "15:30", 30.0, 7.0, 45.0, 54.0, "will come over on NHSP", 378.0, 63.0, "NHSP"], ["Jane Pengelly", "Derriford", "Friday", "2023-06-02", "08:00", "16:30", 30.0, 8.0, 45.0, 54.0, "will come over on NHSP", 432.0, 72.0, "NHSP"], ["Lydie Gam-Mackitta", "Bristol Infirmary", "Tuesday", "2023-05-30", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "will be on etips report this week", 580.13, 43.88, "Retinue"], ["Lydie Gam-Mackitta", "Bristol Infirmary", "Wednesday", "2023-05-31", "07:45", "18:30", 30.0, 10.25, 55.0, 59.5, "will be on etips report this week", 609.88, 46.13, "Retinue"], ["Lydie Gam-Mackitta", "Bristol Infirmary", "Thursday", "2023-06-01", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "will be on etips report this week", 580.13, 43.88, "Retinue"], ["Lydie Gam-Mackitta", "Bristol Infirmary", "Friday", "2023-06-02", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "will be on etips report this week", 580.13, 43.88, "Retinue"], ["Lydie Gam-Mackitta", "Bristol Infirmary", "Friday", "2023-06-02", "18:00", "08:00", 0.0, 14.0, 22.0, 24.0, "will be on etips report this week", 336.0, 28.0, "Retinue"], ["Lydie Gam-Mackitta", "Bristol Infirmary", "Saturday", "2023-06-03", "08:00", "08:00", 0.0, 24.0, 22.0, 24.0, "will be on etips report this week", 576.0, 48.0, "Retinue"], ["Lydie Gam-Mackitta", "Bristol Infirmary", "Sunday", "2023-06-04", "08:00", "07:40", 0.0, 23.75, 22.0, 24.0, "will be on etips report this week", 570.0, 47.5, "Retinue"], ["Patrick Gambold", "isle Of Wight", "Tuesday", "2023-05-30", "08:00", "15:00", 30.0, 6.5, 32.0, 34.94, "Will come over on ID MED report", 227.11, 19.11, "Clairty"], ["Patrick Gambold", "isle Of Wight", "Wednesday", "2023-05-31", "08:00", "17:45", 30.0, 9.25, 32.0, 34.94, "Will come over on ID MED report", 323.2, 27.2, "Clairty"], ["Patrick Gambold", "isle Of Wight", "Thursday", "2023-06-01", "08:00", "16:45", 30.0, 8.25, 32.0, 34.94, "Will come over on ID MED report", 288.26, 24.26, "Clairty"], ["Patrick Gambold", "isle Of Wight", "Friday", "2023-06-02", "08:00", "16:30", 30.0, 8.0, 32.0, 34.94, "Will come over on ID MED report", 279.52, 23.52, "Clairty"], ["Marichelle Alvarez", "Cromwell Hospital", "Tuesday", "2023-05-30", "13:00", "20:00", 30.0, 6.5, 38.0, 50.14, "will come over on Etips", 325.91, 78.91, "Etips"], ["Marichelle Alvarez", "Cromwell Hospital", "Thursday", "2023-06-01", "13:00", "21:00", 30.0, 7.5, 38.0, 50.14, "will come over on Etips", 376.05, 91.05, "Etips"], ["Mark Shea", "Derriford", "Tuesday", "2023-05-30", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over next week on NHSP", 513.0, 133.0, "NHSP"], ["Mark Shea", "Derriford", "Wednesday", "2023-05-31", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over next week on NHSP", 513.0, 133.0, "NHSP"], ["Mark Shea", "Derriford", "Friday", "2023-06-02", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "will come over next week on NHSP", 513.0, 133.0, "NHSP"], ["Diosdado Wagan", "North Downs", "Tuesday", "2023-01-30", "07:30", "19:30", 30.0, 11.5, 40.0, 43.93, "Submitted TS fot Etips after cutoff", 505.2, 45.2, "Etips"], ["Diosdado Wagan", "North Downs", "Wednesday", "2023-05-31", "07:30", "18:00", 30.0, 10.0, 40.0, 43.93, "Submitted TS fot Etips after cutoff", 439.3, 39.3, "Etips"], ["Diosdado Wagan", "North Downs", "Thursday", "2023-06-01", "07:30", "15:00", 30.0, 7.0, 40.0, 43.93, "Submitted TS fot Etips after cutoff", 307.51, 27.51, "Etips"], ["Diosdado Wagan", "North Downs", "Friday", "2023-06-02", "07:30", "17:30", 30.0, 9.75, 40.0, 43.93, "Submitted TS fot Etips after cutoff", 428.32, 38.32, "Etips"], ["Diosdado Wagan", "North Downs", "Saturday", "2023-06-03", "07:30", "16:30", 30.0, 8.75, 40.0, 43.93, "Submitted TS fot Etips after cutoff", 384.39, 34.39, "Etips"], ["Diosdado Wagan", "North Downs", "Friday", "2023-06-02", "20:00", "08:00", 0.0, 12.0, 50.0, 54.0, "Submitted TS fot Etips after cutoff", 648.0, 48.0, "Etips"], ["Diosdado Wagan", "North Downs", "Sunday", "2023-06-04", "20:00", "08:00", 0.0, 12.0, 50.0, 54.0, "Submitted TS fot Etips after cutoff", 648.0, 48.0, "Etips"], ["Rose Emmanuel", "Rivers Hospital", "Tuesday", "2023-05-30", "07:30", "18:00", 30.0, 10.0, 50.0, 60.0, "Incorrectly Uploaded on Etips", 600.0, 100.0, "Etips"], ["Rose Emmanuel", "Rivers Hospital", "Wednesday", "2023-05-31", "07:30", "17:00", 30.0, 9.0, 50.0, 60.0, "Incorrectly Uploaded on Etips", 540.0, 90.0, "Etips"], ["Rose Emmanuel", "Rivers Hospital", "Friday", "2023-06-02", "07:30", "18:00", 30.0, 10.0, 50.0, 60.0, "Incorrectly Uploaded on Etips", 600.0, 100.0, "Etips"], ["Rose Emmanuel", "Rivers Hospital", "Saturday", "2023-06-03", "07:30", "17:00", 30.0, 9.0, 60.0, 68.0, "Incorrectly Uploaded on Etips", 612.0, 72.0, "Etips"], ["Kate Newman", "Colchester", "Tuesday", "2023-06-06", "08:00", "18:30", 30.0, 10.0, 28.98, 38.0, "Will come over on NHSP", 380.0, 90.2, "NHSP"], ["Chan Ganesh", "Oaks Hospital", "Tuesday", "2023-05-30", "17:30", "18:30", 0.0, 1.0, 55.0, 60.0, "Etips Correction of Hours", 60.0, 5.0, "Etips"], ["Chan Ganesh", "Oaks Hospital", "Wednesday", "2023-05-31", "17:30", "18:30", 0.0, 1.0, 55.0, 60.0, "Etips Correction of Hours", 60.0, 5.0, "Etips"], ["Chan Ganesh", "Oaks Hospital", "Monday", "2023-05-06", "08:00", "18:30", 30.0, 10.0, 55.0, 60.0, "Will be on Etips Report", 600.0, 50.0, "Etips"], ["Chan Ganesh", "Oaks Hospital", "Tuesday", "2023-06-06", "08:00", "18:30", 30.0, 10.0, 55.0, 60.0, "Will be on Etips Report", 600.0, 50.0, "Etips"], ["Chan Ganesh", "Oaks Hospital", "Wednesday", "2023-07-06", "08:00", "19:00", 30.0, 10.5, 55.0, 60.0, "Will be on Etips Report", 630.0, 52.5, "Etips"], ["Chan Ganesh", "Oaks Hospital", "Thursday", "2023-08-06", "08:00", "18:30", 30.0, 10.0, 55.0, 60.0, "Will be on Etips Report", 600.0, 50.0, "Etips"], ["Chan Ganesh", "Oaks Hospital", "Friday", "2023-09-06", "08:00", "18:30", 30.0, 10.0, 55.0, 60.0, "Will be on Etips Report", 600.0, 50.0, "Etips"], ["Chan Ganesh", "Oaks Hospital", "Saturday", "2023-10-06", "08:00", "17:00", 30.0, 8.5, 55.0, 60.0, "Will be on Etips Report", 510.0, 42.5, "Etips"], ["Jane Pengelly", "Derriford", "Wednesday", "2023-07-06", "08:00", "17:15", 30.0, 8.75, 45.0, 54.0, "Will come over on NHSP", 472.5, 78.75, "NHSP"], ["Jane Pengelly", "Derriford", "Thursday", "2023-08-06", "08:00", "18:15", 30.0, 9.75, 45.0, 54.0, "Will come over on NHSP", 526.5, 87.75, "NHSP"], ["Jane Pengelly", "Derriford", "Friday", "2023-09-06", "08:00", "18:00", 0.0, 10.0, 45.0, 54.0, "Will come over on NHSP", 540.0, 90.0, "NHSP"], ["Diosdado Wagan", "North Downs Hosp", "Monday", "2023-05-06", "12:30", "18:30", 0.0, 6.0, 40.0, 43.93, "Awaiting ETIPS Report", 263.58, 23.58, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Tuesday", "2023-06-06", "07:30", "18:00", 30.0, 10.0, 40.0, 43.93, "Awaiting ETIPS Report", 439.3, 39.3, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Wednesday", "2023-07-06", "09:00", "18:45", 30.0, 9.25, 40.0, 43.93, "Awaiting ETIPS Report", 406.35, 36.35, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Thursday", "2023-08-06", "07:30", "19:30", 30.0, 10.5, 40.0, 43.93, "Awaiting ETIPS Report", 461.27, 41.27, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Friday", "2023-09-06", "07:30", "16:15", 30.0, 8.25, 40.0, 43.93, "Awaiting ETIPS Report", 362.42, 32.42, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Saturday", "2023-10-06", "07:30", "17:00", 15.0, 9.25, 45.0, 46.24, "Awaiting ETIPS Report", 427.72, 11.47, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Monday", "2023-05-06", "20:00", "08:00", 0.0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report. 50 = Full Shift", 50.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Tuesday", "2023-06-06", "20:00", "08:00", 0.0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 50.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Wednesday", "2023-07-06", "20:00", "08:00", 0.0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 50.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Thursday", "2023-08-06", "20:00", "08:00", 0.0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 50.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Friday", "2023-09-06", "20:00", "08:00", 0.0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 50.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Saturday", "2023-10-06", "20:00", "08:00", 0.0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 50.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Sunday", "2023-11-06", "20:00", "08:00", 0.0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 50.0, 4.0, "Etips"], ["Martin Rowan", "Royal Berkshire", "Monday", "2023-05-06", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Will be on NHSP this week", 450.0, 70.0, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Wednesday", "2023-07-06", "07:30", "18:30", 30.0, 10.5, 38.0, 45.0, "Will be on NHSP this week", 472.5, 73.5, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Thursday", "2023-09-06", "07:30", "18:30", 30.0, 10.5, 38.0, 45.0, "Will be on NHSP this week", 472.5, 73.5, "NHSP"], ["Wayne Mcgeary", "Royal Berkshire", "Monday", "2023-05-06", "07:30", "18:00", 30.0, 10.0, 42.0, 45.0, "Will be on NHSP this week", 450.0, 30.0, "NHSP"], ["Wayne Mcgeary", "Royal Berkshire", "Wednesday", "2023-07-06", "07:30", "18:00", 30.0, 10.0, 42.0, 45.0, "Will be on NHSP this week", 450.0, 30.0, "NHSP"], ["Wayne Mcgeary", "Royal Berkshire", "Thursday", "2023-09-06", "07:30", "18:00", 30.0, 11.0, 42.0, 45.0, "Will be on NHSP this week", 495.0, 33.0, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Monday", "2023-05-06", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Tuesday", "2023-06-06", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Wednesday", "2023-07-06", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Thursday", "2023-08-06", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Marichelle Alvarez", "Cromwell Hosp (Etips)", "Tuesday", "2023-06-06", "07:45", "21:00", 60.0, 12.25, 38.0, 50.14, "will come over on Etips next week", 614.22, 148.72, "ETIPS"], ["Patrick Gambold", "Isle Of Wight", "Monday", "2023-05-06", "08:00", "16:30", 30.0, 8.0, 32.0, 34.94, "Will be on ID MED reprot this week", 279.52, 23.52, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Tuesday", "2023-06-06", "08:00", "18:00", 30.0, 9.5, 32.0, 34.94, "Will be on ID MED reprot this week", 331.93, 27.93, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Wednesday", "2023-07-06", "08:00", "18:00", 30.0, 9.5, 32.0, 34.94, "Will be on ID MED reprot this week", 331.93, 27.93, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Thursday", "2023-08-06", "08:00", "16:30", 30.0, 8.0, 32.0, 34.94, "Will be on ID MED reprot this week", 279.52, 23.52, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Friday", "2023-09-06", "08:00", "13:45", 30.0, 5.75, 32.0, 34.94, "Will be on ID MED reprot this week", 200.91, 16.91, "Clarity"], ["Asia Ismail", "Nuffield Woking", "Saturday", "2023-10-06", "08:15", "13:30", 0.0, 5.25, 34.0, 43.51, "Will be on next weeks Etips", 228.43, 49.93, "Etips"], ["Rinah Andiappareddi", "Cherwell Hospital", "Friday", "2023-02-06", "08:00", "15:45", 30.0, 7.25, 50.0, 60.0, "Awaiting ETips", 435.0, 72.5, "Etips"], ["Gale Ann Barangan", "Watford/West Herts", "Friday", "2023-02-06", "08:00", "20:30", 30.0, 11.5, 25.79, 34.0, "Awaiting NHSP", 391.0, 94.42, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Monday", "2023-12-06", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Will come over on NHSP", 450.0, 70.0, "NSHP"], ["Martin Rowan", "Royal Berkshire", "Tuesday", "2023-06-13", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Will come over on NHSP", 450.0, 70.0, "NSHP"], ["Martin Rowan", "Royal Berkshire", "Wednesday", "2023-06-14", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Will come over on NHSP", 450.0, 70.0, "NSHP"], ["Madilaya Ndanatsei", "Buckinghamshire", "Monday", "2023-05-06", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Has been relased on NHSP", 332.31, 47.31, "NHSP"], ["Madilaya Ndanatsei", "Buckinghamshire", "Tuesday", "2023-06-06", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Has been relased on NHSP", 332.31, 47.31, "NHSP"], ["Madilaya Ndanatsei", "Buckinghamshire", "Wednesday", "2023-07-06", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Has been relased on NHSP", 332.31, 47.31, "NHSP"], ["Madilaya Ndanatsei", "Buckinghamshire", "Thursday", "2023-08-06", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Has been relased on NHSP", 332.31, 47.31, "NHSP"], ["Madilaya Ndanatsei", "Buckinghamshire", "Friday", "2023-09-06", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Has been relased on NHSP", 332.31, 47.31, "NHSP"], ["Ethel Ikeh", "Watford", "Monday", "2023-03-04", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "Aged Shift re relased on NHSP", 391.0, 46.0, "NHSP"], ["Ethel Ikeh", "Watford", "Tuesday", "2023-04-04", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "Aged Shift re relased on NHSP", 391.0, 46.0, "NHSP"], ["Ethel Ikeh", "Watford", "Wednesday", "2023-05-04", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "Aged Shift re relased on NHSP", 391.0, 46.0, "NHSP"], ["Ethel Ikeh", "Watford", "Thursday", "2023-06-04", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "Aged Shift re relased on NHSP", 391.0, 46.0, "NHSP"], ["Rebecca Shields", "Watford", "Friday", "2023-09-06", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "09/06 awaiting autherisation on NHSP", 391.0, 46.0, "NHSP"], ["Rebecca Shields", "Watford", "Tuesday", "2023-06-13", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "13/06 To be relased next week", 391.0, 46.0, "NHSP"], ["Patrick Gambold", "Isle of Wight", "Monday", "2023-12-06", "08:00", "16:30", 30.0, 8.0, 32.0, 34.94, "Will be on this weeks ID Medical Report", 279.52, 23.52, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Tuesday", "2023-06-13", "08:00", "16:30", 30.0, 8.0, 32.0, 34.94, "Will be on this weeks ID Medical Report", 279.52, 23.52, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Wednesday", "2023-06-14", "08:00", "15:30", 30.0, 7.0, 32.0, 34.94, "Will be on this weeks ID Medical Report", 244.58, 20.58, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Thursday", "2023-06-15", "08:00", "15:00", 30.0, 6.5, 32.0, 34.94, "Will be on this weeks ID Medical Report", 227.11, 19.11, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Friday", "2023-06-16", "08:00", "10:30", 0.0, 2.5, 32.0, 34.94, "Will be on this weeks ID Medical Report", 87.35, 7.35, "Clarity"], ["Gary Primmer", "Derriford", "Monday", "2023-12-06", "08:00", "21:00", 30.0, 12.0, 40.0, 54.0, "Will come over on NHSP", 648.0, 168.0, "NHSP"], ["Gary Primmer", "Derriford", "Tuesday", "2023-06-13", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "Will come over on NHSP", 513.0, 133.0, "NHSP"], ["Gary Primmer", "Derriford", "Wednesday", "2023-06-14", "08:00", "21:00", 60.0, 12.0, 40.0, 54.0, "Will come over on NHSP", 648.0, 168.0, "NHSP"], ["Gary Primmer", "Derriford", "Thursday", "2023-06-15", "08:00", "21;00", 60.0, 12.0, 40.0, 54.0, "Will come over on NHSP", 648.0, 168.0, "NHSP"], ["Gary Primmer", "Derriford", "Friday", "2023-06-16", "08:00", "18:00", 30.0, 9.5, 40.0, 54.0, "Will come over on NHSP", 513.0, 133.0, "NHSP"], ["Diosdado Wagan", "North Downs Hosp", "Monday", "2023-12-06", "07:30", "18:30", 30.0, 10.5, 40.0, 43.19, "Will be on tomorrows ETips Report", 453.5, 33.5, "ETIPS"], ["Diosdado Wagan", "North Downs Hosp", "Tuesday", "2023-06-13", "07:30", "21;00", 30.0, 13.0, 40.0, 43.19, "Will be on tomorrows ETips Report", 561.47, 41.47, "ETIPS"], ["Diosdado Wagan", "North Downs Hosp", "Wednesday", "2023-06-14", "07:00", "18:45", 30.0, 9.25, 40.0, 43.19, "Will be on tomorrows ETips Report", 399.51, 29.51, "ETIPS"], ["Diosdado Wagan", "North Downs Hosp", "Thursday", "2023-06-15", "07:30", "20:00", 15.0, 12.25, 40.0, 43.19, "Will be on tomorrows ETips Report", 529.08, 39.08, "ETIPS"], ["Diosdado Wagan", "North Downs Hosp", "Saturday", "2023-06-17", "07:30", "17;15", 15.0, 9.5, 40.0, 43.19, "Will be on tomorrows ETips Report", 410.31, 30.31, "ETIPS"], ["Diosdado Wagan", "North Downs Hosp", "Friday", "2023-06-16", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 54.0, 4.0, "ETIPS"], ["Diosdado Wagan", "North Downs Hosp", "Saturday", "2023-06-17", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 54.0, 4.0, "ETIPS"], ["Diosdado Wagan", "North Downs Hosp", "Sunday", "2023-06-18", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "(On Call Hours) Awaiting etips report", 54.0, 4.0, "ETIPS"], ["Sandra Maria Duarte-Botello", "Nuffield Oxford", "Saturday", "2023-10-06", "08:00", "19:00", 30.0, 10.5, 48.0, 51.16, "Awaiting Etips report", 537.18, 33.18, "ETIPS"], ["Sandra Maria Duarte-Botello", "The Cherwell Hosp", "Monday", "2023-05-06", "08:00", "16:30", 30.0, 8.0, 55.0, 60.0, "Awaiting Etips report", 480.0, 40.0, "ETIPS"], ["Sandra Maria Duarte-Botello", "The Cherwell Hosp", "Tuesday", "2023-06-06", "08:00", "17:00", 30.0, 8.5, 55.0, 60.0, "Awaiting Etips report", 510.0, 42.5, "ETIPS"], ["Sandra Maria Duarte-Botello", "The Cherwell Hosp", "Wednesday", "2023-07-06", "08:00", "16:00", 30.0, 7.5, 55.0, 60.0, "Awaiting Etips report", 450.0, 37.5, "ETIPS"], ["Sandra Maria Duarte-Botello", "The Cherwell Hosp", "Thursday", "2023-08-06", "08:00", "13:30", 0.0, 5.5, 55.0, 60.0, "Awaiting Etips report", 330.0, 27.5, "ETIPS"], ["Sandra Maria Duarte-Botello", "The Cherwell Hosp", "Friday", "2023-09-06", "08:00", "17:30", 30.0, 9.0, 55.0, 60.0, "Awaiting Etips report", 540.0, 45.0, "ETIPS"], ["Tamara Boswell", "Lewisham & Greenwhich", "Monday", "2023-06-19", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "Awaiting HRoster finalization", 289.66, 23.66, "ETIPS"], ["Robert East", "University Oxford", "Friday", "2023-05-05", "07:45", "17:45", 30.0, 9.5, 30.0, 39.5, "Will be on next weeks NHSP report", 375.25, 90.25, "NHSP"], ["Robert East", "University Oxford", "Tuesday", "2023-05-30", "07:45", "17:45", 30.0, 9.5, 30.0, 39.5, "Will be on next weeks NHSP report", 375.25, 90.25, "NHSP"], ["Robert East", "University Oxford", "Wednesday", "2023-05-31", "07:45", "17:45", 30.0, 9.5, 30.0, 39.5, "Will be on next weeks NHSP report", 375.25, 90.25, "NHSP"], ["Robert East", "University Oxford", "Thursday", "2023-08-06", "07:45", "17:45", 30.0, 9.5, 30.0, 39.5, "Will be on next weeks NHSP report", 375.25, 90.25, "NHSP"], ["Mohammad Mohammadi", "Plymouth Hospital", "Monday", "2023-12-06", "08:00", "16:30", 30.0, 8.0, 40.0, 44.15, "Was not finalized on appoved on this weeks NHSP", 353.2, 33.2, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Friday", "2023-06-16", "08:00", "12:30", 0.0, 4.5, 29.5, 40.0, "Will be on next weeks report", 180.0, 47.25, "NHSP"], ["Gary Primmer", "Derriford", "Monday", "2023-06-19", "07:00", "21:00", 0.0, 14.0, 40.0, 54.0, "Will come on next weeks NHSP report", 756.0, 196.0, "NHSP"], ["Gary Primmer", "Derriford", "Tuesday", "2023-06-20", "07:00", "18:00", 0.0, 11.0, 40.0, 54.0, "Will come on next weeks NHSP report", 594.0, 154.0, "NHSP"], ["Gary Primmer", "Derriford", "Thursday", "2023-06-22", "08:00", "18:00", 0.0, 10.0, 40.0, 54.0, "Will come on next weeks NHSP report", 540.0, 140.0, "NHSP"], ["Mark Shea", "Derriford", "Wednesday", "2023-06-21", "11:00", "21:00", 30.0, 9.5, 34.1, 45.75, "will come over next week on NHSP", 434.63, 110.68, "NHSP"], ["Mark Shea", "Derriford", "Thursday", "2023-06-22", "08:00", "21:00", 0.0, 13.0, 34.1, 45.75, "will come over next week on NHSP", 594.75, 151.45, "NHSP"], ["Mark Shea", "Derriford", "Friday", "2023-06-23", "08:00", "18:00", 30.0, 9.5, 34.1, 45.75, "will come over next week on NHSP", 434.63, 110.68, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Monday", "2023-06-19", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Released on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Tuesday", "2023-06-20", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Released on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Wednesday", "2023-06-21", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Released on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Thursday", "2023-06-22", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Released on NHSP", 380.0, 99.75, "NHSP"], ["Roseline Emmanuel", "Rivers Hospital", "Monday", "2023-06-19", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Will come over on this weeks Etips", 570.0, 95.0, "Etips"], ["Roseline Emmanuel", "Rivers Hospital", "Wednesday", "2023-06-21", "07:30", "18:15", 30.0, 10.25, 50.0, 60.0, "Will come over on this weeks Etips", 615.0, 102.5, "Etips"], ["Roseline Emmanuel", "Rivers Hospital", "Thursday", "2023-06-22", "07:30", "19:00", 30.0, 11.0, 50.0, 60.0, "Will come over on this weeks Etips", 660.0, 110.0, "Etips"], ["Roseline Emmanuel", "Rivers Hospital", "Friday", "2023-06-23", "07:30", "17:00", 30.0, 9.0, 50.0, 60.0, "Will come over on this weeks Etips", 540.0, 90.0, "Etips"], ["Roseline Emmanuel", "Rivers Hospital", "Saturday", "2023-06-24", "07:30", "14:30", 30.0, 6.5, 60.0, 65.0, "Will come over on this weeks Etips", 422.5, 32.5, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Tuesday", "2023-06-20", "07:30", "12:30", 0.0, 5.0, 40.0, 43.93, "Will come over on this weeks Etips", 219.65, 19.65, "Etips"], ["Philip White", "Darent Valley", "Fridat", "2023-06-23", "08:00", "17:30", 30.0, 9.0, 30.0, 33.15, "awaiting shift to come over on HRoster", 298.35, 28.35, "HRoster"], ["Wayne Mcgearey", "Royal Berkshire", "Monday", "2023-06-19", "07:30", "17:30", 30.0, 9.5, 42.0, 45.0, "Awaiting to be relaised this weeks on NHSP", 427.5, 28.5, "NHSP"], ["Wayne Mcgearey", "Royal Berkshire", "Tuesday", "2023-06-20", "07:30", "17:30", 30.0, 9.5, 42.0, 45.0, "Awaiting to be relaised this weeks on NHSP", 427.5, 28.5, "NHSP"], ["Wayne Mcgearey", "Royal Berkshire", "Wedensday", "2023-06-21", "07:30", "17:30", 30.0, 9.5, 42.0, 45.0, "Awaiting to be relaised this weeks on NHSP", 427.5, 28.5, "NHSP"], ["Wayne Mcgearey", "Royal Berkshire", "Friday", "2023-06-23", "07:30", "19:15", 30.0, 11.75, 42.0, 45.0, "Awaiting to be relaised this weeks on NHSP", 528.75, 35.25, "NHSP"], ["Patrick Gambold", "Isle of Wight", "Monday", "2023-06-19", "08:00", "17:15", 30.0, 8.75, 32.0, 34.94, "will be on this weeks ID Med report", 305.73, 25.73, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Tuesday", "2023-06-20", "08:00", "17:00", 30.0, 8.5, 32.0, 34.94, "will be on this weeks ID Med report", 296.99, 24.99, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Thursday", "2023-06-22", "08:00", "17:45", 30.0, 9.25, 32.0, 34.94, "will be on this weeks ID Med report", 323.2, 27.2, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Friday", "2023-06-23", "08:00", "17:45", 30.0, 9.25, 32.0, 34.94, "will be on this weeks ID Med report", 323.2, 27.2, "Clarity"], ["Kate Newman", "Colchester", "Tuesday", "2023-06-20", "08:00", "13:30", 0.0, 5.5, 28.98, 38.0, "Will come over on NHSP", 209.0, 49.61, "NHSP"], ["Marichelle Alvarez", "Cromwell Hospital", "Tuesday", "2023-06-13", "07:45", "21:00", 60.0, 12.25, 38.0, 50.14, "Will be on next weeks Etips", 614.22, 148.72, "E-Tips"], ["Tanya Williams", "Watford", "Monday", "2023-06-19", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "Released on NHSP", 391.0, 46.0, "NHSP"], ["Sasa Jokic", "Oxford Manor", "Wednesday", "2023-06-21", "07:30", "17:30", 30.0, 9.5, 42.0, 48.58, "Uplaoded to Etips, will be on next weeks report", 461.51, 62.51, "ETIPS"], ["Sasa Jokic", "Oxford Manor", "Thursday", "2023-06-22", "07:30", "15:30", 30.0, 7.5, 42.0, 45.58, "Uplaoded to Etips, will be on next weeks report", 341.85, 26.85, "ETIPS"], ["Sasa Jokic", "Oxford Manor", "Friday", "2023-06-23", "07:30", "15:00", 0.0, 7.5, 42.0, 48.58, "Uplaoded to Etips, will be on next weeks report", 364.35, 49.35, "ETIPS"], ["Stephen Roberts", "Wrexham Frimley", "Monday", "2023-06-26", "07:30", "19:00", 30.0, 11.0, 38.0, 42.68, "Hours on Clarity portal, worker needs fund today", 469.48, 51.48, "Clarity"], ["Gemima Redd", "Royal Berkshire", "Tuesday", "2023-06-27", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Wednesday", "2023-06-28", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Thursday", "2023-06-29", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Augstyna Akujobi", "Watford", "Monday", "2023-06-26", "08:00", "21:00", 60.0, 12.0, 25.54, 33.73, "waiting for grades to be changed on NHSP", 404.76, 98.28, "NHSP"], ["Roseline Emmanuel", "Rivers Hospital", "Monday", "2023-06-26", "08:00", "19:30", 30.0, 11.0, 50.0, 60.0, "Will come over on this weeks Etips", 570.0, 95.0, "Etips"], ["Roseline Emmanuel", "Rivers Hospital", "Wednesday", "2023-06-28", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Will come over on this weeks Etips", 615.0, 102.5, "Etips"], ["Roseline Emmanuel", "Rivers Hospital", "Thursday", "2023-06-29", "08:00", "19:30", 30.0, 11.0, 50.0, 60.0, "Will come over on this weeks Etips", 660.0, 110.0, "Etips"], ["Roseline Emmanuel", "Rivers Hospital", "Saturday", "2023-01-07", "07:30", "15:00", 30.0, 7.0, 60.0, 65.0, "Will come over on this weeks Etips", 455.0, 35.0, "Etips"], ["Ana Paggao", "Watford Gen Hospi", "Tuesday", "2023-06-13", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "Will be on this week's NHSP Report", 391.0, 46.0, "NHSP"], ["Jane Pengelly", "Derriford", "Wednesday", "2023-06-29", "08:00", "17:00", 30.0, 8.5, 45.0, 54.0, "Retrospective NHSP Booking", 472.5, 78.75, "NHSP"], ["Jane Pengelly", "Derriford", "Thursday", "2023-06-30", "08:00", "18:00", 0.0, 10.0, 45.0, 54.0, "Retrospective NHSP Booking", 526.5, 87.75, "NHSP"], ["Mark Shea", "Derriford", "Monday", "2023-06-26", "08:00", "18:00", 30.0, 9.5, 34.1, 54.0, "Will be on this week's SB", 513.0, 189.05, "NHSP"], ["Mark Shea", "Derriford", "Tuesday", "2023-06-27", "08:00", "18:00", 0.0, 10.0, 34.1, 54.0, "Will be on this week's SB", 540.0, 199.0, "NHSP"], ["Mark Shea", "Derriford", "Wednesday", "2023-06-28", "08:00", "18:00", 0.0, 10.0, 34.1, 54.0, "Will be on this week's SB", 540.0, 199.0, "NHSP"], ["Mark Shea", "Derriford", "Thursday", "2023-06-29", "08:00", "18:00", 30.0, 9.5, 34.1, 54.0, "Will be on this week's SB", 513.0, 189.05, "NHSP"], ["Mark Shea", "Derriford", "Friday", "2023-06-30", "08:00", "18:00", 0.0, 10.5, 34.1, 54.0, "Will be on this week's SB", 567.0, 208.95, "NHSP"], ["Wayne Mcgearey", "Frimely Park Hosp", "Wednesday", "2023-06-28", "07:30", "18:00", 30.0, 11.0, 40.0, 42.25, "Will come over on Clairty report", 464.75, 24.75, "Clarity"], ["Wayne Mcgearey", "Frimely Park Hosp", "Thursday", "2023-06-29", "07:30", "19:00", 30.0, 10.0, 40.0, 42.25, "Will come over on Clairty report", 422.5, 22.5, "Clarity"], ["Wayne Mcgearey", "Royal Berkshire", "Fridaay", "2023-06-30", "07:30", "17:30", 30.0, 9.5, 42.0, 45.0, "Will come over this week on NHSP", 427.5, 28.5, "NHSP"], ["Gale Ann Barangan", "West Herts", "Friday", "2023-06-16", "08:00", "21:00", 30.0, 12.5, 25.79, 34.0, "", 425.0, 102.63, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth", "Tuesday", "2023-06-06", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "Retrospective NHSP Shift", 425.13, 45.13, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth", "Monday", "2023-12-06", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "Retrospective NHSP Shift", 425.13, 45.13, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth", "Tuesday", "2023-06-13", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "Retrospective NHSP Shift", 425.13, 45.13, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Monday", "2023-03-07", "07:30", "19:00", 30.0, 11.0, 38.0, 45.0, "Released on NHSP", 495.0, 77.0, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Wednesday", "2023-04-07", "07:30", "17:30", 30.0, 9.5, 38.0, 45.0, "Released on NHSP", 427.5, 66.5, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Thursday", "2023-05-07", "07:30", "17:00", 30.0, 9.0, 38.0, 45.0, "Released on NHSP", 405.0, 63.0, "NHSP"], ["Shauna Henderson-Rose", "Ramsay Rivers", "Monday", "2023-06-26", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Hours uploadedto Etips, On next week Report", 600.0, 100.0, "ETIPS"], ["Shauna Henderson-Rose", "Ramsay Rivers", "Tuesday", "2023-06-27", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Hours uploaded to Etips, On next week Report", 570.0, 95.0, "ETIPS"], ["Robert East", "Oxford University", "Wednesday", "2023-06-28", "07:45", "17:45", 30.0, 9.5, 31.5, 39.5, "Raised on NHSP", 375.25, 76.0, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Tuesday", "2023-03-07", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Wednesday", "2023-04-07", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Thursday", "2023-05-07", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Will come over on NHSP", 380.0, 99.75, "NHSP"], ["Tanya Williams", "West Herts", "Tuesday", "2023-06-27", "08:00", "21:00", 30.0, 12.5, 30.0, 34.0, "on NHSP portal", 425.0, 50.0, "NHSP"], ["Tanya Williams", "West Herts", "Wednesday", "2023-06-28", "08:00", "21:00", 30.0, 12.5, 30.0, 34.0, "on NHSP portal", 425.0, 50.0, "NHSP"], ["Ndidi Chidume", "West Herts", "Wednesday", "2023-02-15", "08:00", "21:00", 30.0, 12.5, 30.0, 34.0, "NHSP Retrospective form filled and sent to trust", 425.0, 50.0, "NHSP"], ["Ndidi Chidume", "West Herts", "Thursday", "2023-05-25", "08:00", "19:00", 30.0, 10.5, 30.0, 34.0, "NHSP Retrospective form filled and sent to trust", 357.0, 42.0, "NHSP"], ["Mark Pablico", "North Downs", "Monday", "2023-06-26", "07:45", "18:00", 30.0, 9.75, 40.0, 43.19, "On next etips report", 421.1, 31.1, "ETIPS"], ["Mark Pablico", "North Downs", "Tuesday", "2023-06-27", "07:45", "18:00", 30.0, 9.75, 40.0, 43.19, "On next etips report", 421.1, 31.1, "ETIPS"], ["Mark Pablico", "North Downs", "Thursday", "2023-06-28", "08:30", "16:00", 30.0, 7.0, 40.0, 43.19, "On next etips report", 302.33, 22.33, "ETIPS"], ["Mark Pablico", "North Downs", "Saturday", "2023-01-07", "07:30", "14:00", 15.0, 6.25, 45.0, 46.24, "On next etips report", 289.0, 7.75, "ETIPS"], ["John Arthur", "Chelsea Westminster", "Thursdsy", "2023-06-29", "08:00", "20:30", 30.0, 12.0, 30.0, 33.73, "Profile wasn't complete on Hroster, Needs funds", 404.76, 44.76, "HRoster"], ["Jane Pengelly", "Derriford", "Wednesday", "2023-07-05", "08:00", "18:00", 30.0, 9.5, 34.1, 44.75, "shift will come over tomorrow", 425.13, 101.18, "NHSP"], ["Jane Pengelly", "Derriford", "Thursday", "2023-07-06", "08:00", "18:15", 0.0, 10.25, 34.1, 44.75, "shift will come over tomorrow", 458.69, 109.16, "NHSP"], ["Jane Pengelly", "Derriford", "Friday", "2023-07-07", "08:00", "16:15", 0.0, 8.25, 34.1, 44.75, "shift will come over tomorrow", 369.19, 87.86, "NHSP"], ["Beauty Pangidzwa", "Colchester", "Wednesday", "2023-07-05", "08:00", "18:15", 30.0, 9.75, 34.0, 38.0, "shift coming over on NHSP", 370.5, 39.0, "NHSP"], ["Beauty Pangidzwa", "Colchester", "Thursday", "2023-07-06", "08:00", "18:00", 30.0, 9.5, 34.0, 38.0, "shift coming over on NHSP", 361.0, 38.0, "NHSP"], ["Beauty Pangidzwa", "Colchester", "Friday", "2023-07-07", "08:00", "17:30", 30.0, 9.0, 34.0, 38.0, "shift coming over on NHSP", 342.0, 36.0, "NHSP"], ["Gurprit Kayola", "Moorefields", "Tuesday", "2023-06-27", "08:00", "13:00", 0.0, 5.0, 29.84, 40.0, "timesheet sent to bank to get authorised", 200.0, 50.8, "HR"], ["Ndanatsei Madilaya", "Buckinghamshire", "Monday", "2023-07-03", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Shift will come over tomorrow from NHSP", 332.31, 47.31, "NHSP"], ["Ndanatsei Madilaya", "Buckinghamshire", "Tuesday", "2023-07-04", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Shift will come over tomorrow from NHSP", 332.31, 47.31, "NHSP"], ["Ndanatsei Madilaya", "Buckinghamshire", "Wednesday", "2023-07-05", "08:00", "18:00", 30.0, 9.5, 30.0, 34.98, "Shift will come over tomorrow from NHSP", 332.31, 47.31, "NHSP"], ["Marichelle Alvarez", "Cromwell", "Tuesday", "2023-06-20", "13:00", "21:00", 30.0, 7.5, 38.0, 50.14, "shift will come over on next week report", 376.05, 91.05, "Etips"], ["Myles Roberts", "Plymouth", "Monday", "2023-07-03", "08:00", "18:00", 0.0, 10.0, 34.1, 44.75, "waiting for correct codes to be added to NHSP", 447.5, 106.5, "NHSP"], ["Myles Roberts", "Plymouth", "Wednesday", "2023-07-05", "08:00", "21:00", 60.0, 12.0, 34.1, 44.75, "waiting for correct codes to be added to NHSP", 537.0, 127.8, "NHSP"], ["Myles Roberts", "Plymouth", "Thursday", "2023-07-06", "08:00", "21:00", 30.0, 12.5, 34.1, 44.75, "waiting for correct codes to be added to NHSP", 559.38, 133.13, "NHSP"], ["Stephen Roberts", "Wexham Park", "Monday", "2023-07-10", "07:30", "19:30", 30.0, 11.5, 38.0, 42.68, "Shift will come over on Clarity report next thurs", 490.82, 53.82, "Clarity"], ["Stephen Roberts", "Wexham Park", "Thursday", "2023-07-13", "07:30", "18:30", 30.0, 10.5, 38.0, 42.68, "Shift will come over on Clarity report next thurs", 448.14, 49.14, "Clarity"], ["Sandra Botello", "Nuffield Oxford - The Manor", "Tuesday", "2023-07-04", "08:00", "20:00", 30.0, 11.5, 48.0, 51.16, "Shifts will come over on etips", 588.34, 36.34, "etips"], ["Sandra Botello", "Nuffield Oxford - The Manor", "Fridau", "2023-07-07", "08:00", "17:30", 30.0, 9.0, 48.0, 51.16, "Shifts will come over on etips", 460.44, 28.44, "etips"], ["Sandra Botello", "Nuffield Oxford - The Manor", "Saturday", "2023-07-08", "08:00", "16:30", 0.0, 8.5, 48.0, 51.16, "Shifts will come over on etips", 434.86, 26.86, "etips"], ["Sandra Botello", "Ramsay cherwell", "Monday", "2023-07-03", "08:00", "15:30", 30.0, 7.0, 55.0, 60.0, "Shifts will come over on etips", 420.0, 35.0, "etips"], ["Sandra Botello", "Ramsay cherwell", "Wednesday", "2023-07-05", "08:00", "16:45", 30.0, 8.15, 55.0, 60.0, "Shifts will come over on etips", 489.0, 40.75, "etips"], ["Sandra Botello", "Ramsay cherwell", "Thursday", "2023-07-06", "08:00", "16:00", 30.0, 7.5, 55.0, 60.0, "Shifts will come over on etips", 450.0, 37.5, "etips"], ["Beauty Pangidzwa", "Colchester", "Tuesday", "2023-07-11", "08:00", "18:30", 30.0, 10.0, 34.0, 38.0, "shifts waiting to come over for NHSP", 380.0, 40.0, "NHSP"], ["Beauty Pangidzwa", "Colchester", "Wednesday", "2023-07-12", "08:00", "18:00", 30.0, 9.5, 34.0, 38.0, "shifts waiting to come over for NHSP", 361.0, 38.0, "NHSP"], ["Beauty Pangidzwa", "Colchester", "Thursday", "2023-07-13", "08:00", "18:00", 30.0, 9.5, 34.0, 38.0, "shifts waiting to come over for NHSP", 361.0, 38.0, "NHSP"], ["Rose Emmauel", "Ramsay Rivers", "Monday", "2023-07-10", "07:30", "19:45", 30.0, 11.75, 50.0, 60.0, "Shifts will be on tomorrow's Etips report", 705.0, 117.5, "Etips"], ["Rose Emmauel", "Ramsay Rivers", "Wednesday", "2023-07-12", "07:30", "18:15", 30.0, 10.5, 50.0, 60.0, "Shifts will be on tomorrow's Etips report", 630.0, 105.0, "Etips"], ["Rose Emmauel", "Ramsay Rivers", "Thursday", "2023-07-13", "07:30", "19:00", 30.0, 11.0, 50.0, 60.0, "Shifts will be on tomorrow's Etips report", 660.0, 110.0, "Etips"], ["Rose Emmauel", "Ramsay Rivers", "Friday", "2023-07-14", "07:30", "18:00", 30.0, 10.0, 50.0, 60.0, "Shifts will be on tomorrow's Etips report", 600.0, 100.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Monday", "2023-07-10", "07:30", "18:15", 30.0, 10.25, 40.0, 43.93, "Shifts uploaded to ETIPS portal", 450.28, 40.28, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Tuesday", "2023-07-11", "07:30", "19:00", 30.0, 11.0, 40.0, 43.93, "Shifts uploaded to ETIPS portal", 483.23, 43.23, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Wednesday", "2023-07-12", "07:30", "19:15", 30.0, 11.25, 40.0, 43.93, "Shifts uploaded to ETIPS portal", 494.21, 44.21, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Thursday", "2023-07-13", "07:30", "18:00", 30.0, 10.0, 40.0, 43.93, "Shifts uploaded to ETIPS portal", 439.3, 39.3, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Friday", "2023-07-14", "07:30", "17:30", 30.0, 9.5, 40.0, 43.93, "Shifts uploaded to ETIPS portal", 417.34, 37.34, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Saturday", "2023-07-15", "07:30", "18:00", 15.0, 10.25, 45.0, 46.24, "Shifts uploaded to ETIPS portal", 473.96, 12.71, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Thursday", "2023-07-13", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "(ON CALL HOURS)", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Friday", "2023-07-14", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "(ON CALL HOURS)", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Saturday", "2023-07-15", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "(ON CALL HOURS)", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "North Downs Hosp", "Sunday", "2023-07-16", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "(ON CALL HOURS)", 54.0, 4.0, "Etips"], ["Shauna Henderson-Rose", "Rivers Hospital", "Monday", "2023-07-10", "07:30", "18:00", 30.0, 10.0, 50.0, 60.0, "Will be on Etips tomorrow", 600.0, 100.0, "Etips"], ["Shauna Henderson-Rose", "Rivers Hospital", "Tuesday", "2023-07-11", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Will be on Etips tomorrow", 570.0, 95.0, "Etips"], ["Patrick Gambold", "Isle of Wright", "Monday", "2023-07-10", "08:00", "16:00", 30.0, 7.5, 32.0, 34.94, "Submitted to Clarity Portal", 262.05, 22.05, "Clairty"], ["Patrick Gambold", "Isle of Wright", "Tuesday", "2023-07-11", "08:00", "16:30", 30.0, 8.0, 32.0, 34.94, "Submitted to Clarity Portal", 279.52, 23.52, "Clairty"], ["Patrick Gambold", "Isle of Wright", "Wednesday", "2023-07-12", "08:00", "16:30", 30.0, 8.0, 32.0, 34.94, "Submitted to Clarity Portal", 279.52, 23.52, "Clairty"], ["Patrick Gambold", "Isle of Wright", "Thursday", "2023-07-13", "08:00", "18:00", 30.0, 9.5, 32.0, 34.94, "Submitted to Clarity Portal", 331.93, 27.93, "Clairty"], ["Patrick Gambold", "Isle of Wright", "Friday", "2023-07-14", "08:00", "15:15", 30.0, 6.75, 32.0, 34.94, "Submitted to Clarity Portal", 235.85, 19.85, "Clairty"], ["Shauna Henderson-Rose", "Rivers Hops", "Monday", "2023-07-03", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Should've been paid on last weeks report, uplaoded to etips", 570.0, 95.0, "Etips"], ["Shauna Henderson-Rose", "Rivers Hosp", "Tuesday", "2023-07-04", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Should've been paid on last weeks report, uplaoded to etips", 600.0, 100.0, "Etips"], ["Jovanie Santos", "North Downs Hosp", "Monday", "2023-07-03", "10:00", "18:45", 30.0, 8.25, 40.0, 43.19, "Submitted on ETIPS, Will come over tomorrow", 356.32, 26.32, "Etips"], ["Jovanie Santos", "North Downs Hosp", "Wednesday", "2023-07-05", "07:30", "19:00", 30.0, 11.0, 40.0, 43.19, "Submitted on ETIPS, Will come over tomorrow", 475.09, 35.09, "Etips"], ["Jovanie Santos", "North Downs Hosp", "Thursday", "2023-07-06", "07:30", "18:30", 30.0, 10.5, 40.0, 43.19, "Submitted on ETIPS, Will come over tomorrow", 453.5, 33.5, "Etips"], ["Jovanie Santos", "North Downs Hosp", "Wednesday", "2023-07-12", "07:30", "19:15", 30.0, 11.25, 40.0, 43.19, "Submitted on ETIPS, Will come over tomorrow", 485.89, 35.89, "Etips"], ["Jovanie Santos", "North Downs Hosp", "Thursday", "2023-07-13", "07:30", "18:00", 30.0, 10.0, 40.0, 43.19, "Submitted on ETIPS, Will come over tomorrow", 431.9, 31.9, "Etips"], ["Marichelle Alvarez", "Bupa Cromwell", "Tuesday", "2023-07-11", "07:45", "15:45", 30.0, 7.5, 38.0, 50.14, "Submitted to Etips will come over next week", 376.05, 91.05, "Etips"], ["Mark Shea", "Derriford", "Monday", "2023-07-10", "08:00", "18:00", 30.0, 9.5, 34.1, 54.0, "Released on NHSP", 513.0, 189.05, "NHSP"], ["Mark Shea", "Derriford", "Tuesday", "2023-07-11", "11:00", "21:00", 30.0, 9.5, 34.1, 54.0, "Released on NHSP", 513.0, 189.05, "NHSP"], ["Mark Shea", "Derriford", "Wednesday", "2023-07-12", "08:00", "21:00", 30.0, 12.5, 34.1, 54.0, "Released on NHSP", 675.0, 248.75, "NHSP"], ["Mark Shea", "Derriford", "Thursday", "2023-07-13", "08:00", "18:00", 30.0, 9.5, 34.1, 54.0, "Released on NHSP", 513.0, 189.05, "NHSP"], ["Mark Shea", "Derriford", "Friday", "2023-07-14", "08:00", "19:00", 60.0, 10.0, 34.1, 54.0, "Released on NHSP", 540.0, 199.0, "NHSP"], ["Mark Shea", "Derriford", "Saturday", "2023-07-15", "21:00", "08:00", 60.0, 10.0, 34.1, 54.0, "Released on NHSP", 540.0, 199.0, "NHSP"], ["Mark Shea", "Derriford", "Sunday", "2023-07-16", "21:00", "08:00", 60.0, 10.0, 34.1, 54.0, "Released on NHSP", 540.0, 199.0, "NHSP"], ["Lyn Chiwenga", "Derriford", "Friday", "2023-06-30", "08:00", "19:00", 0.0, 11.0, 40.0, 44.75, "Will be on NHSP next week", 492.25, 52.25, "NHSP"], ["Lyn Chiwenga", "Derriford", "Friday", "2023-07-07", "08:00", "21:30", 30.0, 12.45, 40.0, 44.75, "Will be on NHSP next week", 557.14, 59.14, "NHSP"], ["Katarzyna Szkiladz", "Chelsea & West Mid", "Wednesday", "2023-07-12", "08:00", "18:30", 30.0, 10.0, 30.0, 33.66, "Chased Chelsea all week for references, worker needs Funds", 336.6, 36.6, "VMS"], ["Diosdado Wagan", "North Down Hosp", "Monday", "2023-07-17", "08:00", "18:15", 30.0, 9.75, 40.0, 43.19, "Uploaded TS to Portal", 421.1, 31.1, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Wednesday", "2023-07-19", "09:45", "20:30", 30.0, 10.25, 40.0, 43.19, "Uploaded TS to Portal", 442.7, 32.7, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Thursday", "2023-07-20", "13:00", "17:00", 0.0, 4.0, 40.0, 43.19, "Uploaded TS to Portal", 172.76, 12.76, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Friday", "2023-04-21", "07:30", "14:30", 15.0, 7.25, 40.0, 43.19, "Uploaded TS to Portal", 313.13, 23.13, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Saturday", "2023-04-22", "07:30", "13:00", 15.0, 5.25, 40.0, 43.19, "Uploaded TS to Portal", 226.75, 16.75, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Monday", "2023-07-17", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "Uploaded TS to Portal", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Friday", "2023-07-21", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "Uploaded TS to Portal", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Saturday", "2023-07-22", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "Uploaded TS to Portal", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "North Down Hosp", "Sunday", "2023-07-23", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "Uploaded TS to Portal", 54.0, 4.0, "Etips"], ["Rose Emmanuel", "Ramsay Rivers", "Monday", "2023-07-17", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Uploaded to Etips", 600.0, 100.0, "Etips"], ["Rose Emmanuel", "Ramsay Rivers", "Wednesdat", "2023-07-19", "07:30", "16:00", 30.0, 8.0, 50.0, 60.0, "Uploaded to Etips", 480.0, 80.0, "Etips"], ["Rose Emmanuel", "Ramsay Rivers", "Thursday", "2023-07-20", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Uploaded to Etips", 570.0, 95.0, "Etips"], ["Gloria Tawonezvi", "West Herts", "Monday", "2023-07-10", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "released on NHSP", 391.0, 46.0, "NHSP"], ["Carla Lobato", "Ramsay - Pine Hill", "Wednesday", "2023-07-19", "07:30", "17:45", 30.0, 9.75, 35.1, 60.0, "Uploaded to Etips Portal", 585.0, 242.78, "Etips"], ["Carla Lobato", "Ramsay - Pine Hill", "Thursday", "2023-07-20", "07:30", "18:00", 30.0, 10.0, 35.1, 60.0, "Uploaded to Etips Portal", 600.0, 249.0, "Etips"], ["Carla Lobato", "Ramsay - Pine Hill", "Saturday", "2023-07-22", "07:30", "13:45", 0.0, 6.25, 35.1, 60.0, "Uploaded to Etips Portal", 375.0, 155.63, "Etips"], ["Patrick Gambold", "Isle of Wight", "Monday", "2023-07-17", "08:00", "17:15", 0.0, 9.25, 32.0, 34.94, "will be on this weeks ID Med report", 323.2, 27.2, "Clairty"], ["Patrick Gambold", "Isle of Wight", "Tuesday", "2023-07-18", "08:00", "18:00", 30.0, 9.5, 32.0, 34.94, "will be on this weeks ID Med report", 331.93, 27.93, "Clairty"], ["Patrick Gambold", "Isle of Wight", "Thursday", "2023-07-19", "08:00", "17:00", 30.0, 8.5, 32.0, 34.94, "will be on this weeks ID Med report", 296.99, 24.99, "Clairty"], ["Paula Ibanez", "Spire Wellesley", "Monday", "2023-07-19", "07:45", "20:00", 30.0, 11.75, 36.66, 40.3, "Chasing Retinue to add her bookings", 473.53, 42.77, "Retinue"], ["Tamara Boswell", "Lewisham & QE", "Monday", "2023-07-24", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "Added to Hroster for invoicing next week", 289.66, 23.66, "Hroster"], ["Tamara Boswell", "Lewisham & QE", "Tuesday", "2023-07-25", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "Added to Hroster for invoicing next week", 289.66, 23.66, "Hroster"], ["Tamara Boswell", "Lewisham & QE", "Wednesday", "2023-07-26", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "Added to Hroster for invoicing next week", 289.66, 23.66, "Hroster"], ["Tamara Boswell", "Lewisham & QE", "Thursday", "2023-07-27", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "Added to Hroster for invoicing next week", 289.66, 23.66, "Hroster"], ["Rose Emmanuel", "Ramsay - Rivers", "Monday", "2023-07-24", "13:00", "19:30", 30.0, 6.0, 50.0, 60.0, "Uploaded to Etips", 360.0, 60.0, "Etips"], ["Rose Emmanuel", "Ramsay - Rivers", "Tuesday", "2023-07-25", "13:00", "18:00", 0.0, 5.0, 50.0, 60.0, "Uploaded to Etips", 300.0, 50.0, "Etips"], ["Rose Emmanuel", "Ramsay - Rivers", "Friday", "2023-07-28", "08:00", "17:00", 30.0, 8.5, 50.0, 60.0, "Uploaded to Etips", 510.0, 85.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-07-24", "07:30", "18:30", 30.0, 10.5, 42.0, 43.19, "Uploaded to Etips", 453.5, 12.5, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-07-25", "07:30", "20:15", 30.0, 12.25, 42.0, 43.19, "Uploaded to Etips", 529.08, 14.58, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2023-07-27", "07:30", "17:30", 30.0, 9.5, 42.0, 43.19, "Uploaded to Etips", 410.31, 11.31, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2023-07-28", "07:30", "16:00", 15.0, 8.25, 42.0, 43.19, "Uploaded to Etips", 356.32, 9.82, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2023-07-29", "07:30", "16:30", 15.0, 8.75, 42.0, 43.19, "Uploaded to Etips", 377.91, 10.41, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-07-24", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "On Call Hours", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-07-25", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "On Call Hours", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2023-07-27", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "On Call Hours", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2023-07-28", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "On Call Hours", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2023-07-29", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "On Call Hours", 54.0, 4.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Sunday", "2023-07-30", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "On Call Hours", 54.0, 4.0, "Etips"], ["Jane Pengelly", "Plymouth - Derriford", "Wednesday", "2023-07-26", "08:00", "17:45", 30.0, 9.25, 34.1, 44.75, "Released on NHSP", 413.94, 98.51, "NHSP"], ["Jane Pengelly", "Plymouth - Derriford", "Thursday", "2023-07-27", "08:00", "18:00", 30.0, 9.5, 34.1, 44.75, "Released on NHSP", 425.13, 101.18, "NHSP"], ["Jane Pengelly", "Plymouth - Derriford", "Friday", "2023-07-28", "08:00", "16:50", 0.0, 8.5, 34.1, 44.75, "Released on NHSP", 380.38, 90.53, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth - Derriford", "Monday", "2023-07-24", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "will be on tomorrows NHSP", 425.13, 45.13, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth - Derriford", "Tuesday", "2023-07-25", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "will be on tomorrows NHSP", 425.13, 45.13, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth - Derriford", "Wednesday", "2023-07-26", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "will be on tomorrows NHSP", 425.13, 45.13, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth - Derriford", "Thursday", "2023-07-27", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "will be on tomorrows NHSP", 425.13, 45.13, "NHSP"], ["Iyabo Olufunke Awotedu", "Plymouth - Derriford", "Friday", "2023-07-28", "08:00", "18:00", 30.0, 9.5, 40.0, 44.75, "will be on tomorrows NHSP", 425.13, 45.13, "NHSP"], ["Jovanie Santos", "Ramsay - North Downs", "Monday", "2023-07-24", "07:30", "17:00", 30.0, 9.0, 40.0, 43.19, "Uploaded to Etips", 388.71, 28.71, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2023-07-25", "07:30", "18:00", 30.0, 10.0, 40.0, 43.19, "Uploaded to Etips", 431.9, 31.9, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Monday", "2023-07-31", "07:30", "18:30", 30.0, 10.5, 40.0, 43.19, "Uploaded to Etips", 453.5, 33.5, "Etips"], ["Togy Sebastian", "Royal Berkshire", "Thursday", "2023-07-27", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Released on NHSP", 450.0, 70.0, "nhsp"], ["Togy Sebastian", "Royal Berkshire", "Friday", "2023-07-28", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Released on NHSP", 450.0, 70.0, "nhsp"], ["Wayne Mcgeary", "Royal Berkshire", "Thursday", "2023-07-27", "07:30", "18:00", 30.0, 10.0, 42.0, 45.0, "Released on NHSP", 450.0, 30.0, "NHSP"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-07-31", "10:00", "18:30", 30.0, 9.0, 40.0, 43.19, "Uploaded to Etips", 388.71, 28.71, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-08-01", "07:30", "18:00", 30.0, 10.0, 40.0, 43.19, "Uploaded to Etips", 431.9, 31.9, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-07-31", "20:00", "08:00", 0, 1.0, 50.0, 54.0, "Uploaded to Etips", 54.0, 4.0, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Monday", "2023-07-21", "07:30", "15:30", 15.0, 7.75, 40.0, 43.19, "Uplaoded to etips for invoicing", 334.72, 24.72, "Etips"], ["Florence Rufu", "Ramsay - Blakelands", "Monday", "2023-07-24", "08:00", "19:30", 30.0, 11.0, 35.0, 39.33, "Will come over next weeks report", 432.63, 47.63, "Etips"], ["Florence Rufu", "Ramsay - Blakelands", "Thursday", "2023-07-27", "08:00", "17:00", 30.0, 8.5, 35.0, 39.33, "Will come over next weeks report", 334.31, 36.81, "Etips"], ["Jane Mayhew", "Wrexham", "Tuesday", "2023-08-02", "07:30", "19:30", 30.0, 11.5, 35.0, 42.68, "Missed Clarity cutoff time", 490.82, 88.32, "Clarity"], ["Gemima Redd", "Royal Berkshire", "Monday", "2023-07-24", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Released on NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Tuesday", "2023-07-25", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Released on NHSP", 380.0, 99.75, "NHSP"], ["Ndidi Chidume", "West Herts", "Thursday", "2023-06-15", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "will comeover on NHSP", 391.0, 46.0, "NHSP"], ["Ndidi Chidume", "West Herts", "Thursday", "2023-07-18", "08:00", "17:00", 30.0, 8.5, 30.0, 34.0, "will comeover on NHSP", 289.0, 34.0, "NHSP"], ["Togy Sebastian", "Royal Berkshire", "Friday", "2023-08-04", "07:30", "17:30", 30.0, 9.5, 38.0, 45.0, "Will come over on NHSP this weeK", 427.5, 66.5, "NHSP"], ["Wayne Mcgearey", "Royal Berkshire", "Tuesday", "2023-08-01", "07:30", "18:00", 30.0, 12.5, 42.0, 45.0, "Awaiting to be relaised this weeks on NHSP", 562.5, 37.5, "NHSP"], ["Wayne Mcgearey", "Royal Berkshire", "Wednesday", "2023-08-02", "07:30", "20:00", 30.0, 12.0, 42.0, 45.0, "Awaiting to be relaised this weeks on NHSP", 540.0, 36.0, "NHSP"], ["Wayne Mcgearey", "Royal Berkshire", "Thursday", "2023-08-03", "07:30", "18:30", 30.0, 10.5, 42.0, 45.0, "Awaiting to be relaised this weeks on NHSP", 472.5, 31.5, "NHSP"], ["Rose Emmanuel", "Ramsay Rivers", "Monday", "2023-07-31", "08:00", "18:15", 30.0, 9.75, 50.0, 60.0, "Uploaded to Etips", 600.0, 100.0, "Etips"], ["Rose Emmanuel", "Ramsay Rivers", "Wednesday", "2023-08-02", "07:30", "18:30", 30.0, 10.5, 50.0, 60.0, "Uploaded to Etips", 480.0, 80.0, "Etips"], ["Rose Emmanuel", "Ramsay Rivers", "Thursday", "2023-08-03", "07:30", "18:00", 30.0, 10.0, 50.0, 60.0, "Uploaded to Etips", 570.0, 95.0, "Etips"], ["Rose Emmanuel", "Ramsay Rivers", "Friday", "2023-08-04", "07:30", "18:30", 30.0, 10.5, 50.0, 60.0, "Uploaded to Etips", 570.0, 95.0, "Etips"], ["Sandra Durate Botello", "Ramsay - Cherwell", "Monday", "2023-07-31", "08:00", "14:00", 0.0, 6.0, 55.0, 60.0, "Will appear on Etips Report Tomorrow", 360.0, 30.0, "Etips"], ["Sandra Durate Botello", "Ramsay - Cherwell", "Tuesday", "2023-08-01", "08:00", "13:00", 0.0, 5.0, 55.0, 60.0, "Will appear on Etips Report Tomorrow", 300.0, 25.0, "Etips"], ["Sandra Durate Botello", "Ramsay - Cherwell", "Wednesday", "2023-08-02", "08:00", "16:00", 30.0, 7.5, 55.0, 60.0, "Will appear on Etips Report Tomorrow", 450.0, 37.5, "Etips"], ["Sandra Durate Botello", "Ramsay - Cherwell", "Thursday", "2023-08-03", "08:00", "17:30", 30.0, 9.0, 55.0, 60.0, "Will appear on Etips Report Tomorrow", 540.0, 45.0, "Etips"], ["Jane Mayhew", "Wrexham", "Thursday", "2023-08-03", "07:30", "20:00", 30.0, 12.0, 35.0, 42.68, "Will be on Clairty report (Thursday)", 512.16, 92.16, "Clarity"], ["Jane Mayhew", "Wrexham", "Frirday", "2023-08-04", "07:30", "20:00", 0.0, 10.0, 35.0, 42.68, "Will be on Clairty report (Thursday)", 426.8, 76.8, "Clarity"], ["Biren Chheda", "Wrexham", "Monday", "2023-07-31", "07:30", "18:00", 30.0, 10.0, 30.0, 38.81, "Released on Clarity Portal", 388.1, 88.1, "Clarity"], ["Biren Chheda", "Wrexham", "Wednesday", "2023-08-02", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Released on Clarity Portal", 446.32, 101.32, "Clarity"], ["Biren Chheda", "Wrexham", "Thursday", "2023-08-03", "07:30", "20:30", 30.0, 12.5, 30.0, 38.81, "Released on Clarity Portal", 485.13, 110.13, "Clarity"], ["Biren Chheda", "Wrexham", "Friday", "2023-08-04", "07:30", "00:00", 30.0, 16.0, 30.0, 38.81, "Released on Clarity Portal", 620.96, 140.96, "Clarity"], ["Jane pengelly", "plymouth", "Wednesday", "2023-08-02", "08:00", "18:00", 0.0, 10.0, 34.1, 44.75, "Released from NHSP", 447.5, 106.5, "NHSP"], ["Jane pengelly", "plymouth", "Thursday", "2023-08-03", "08:00", "18:00", 30.0, 9.5, 34.1, 44.75, "Released from NHSP", 425.13, 101.18, "NHSP"], ["Jane pengelly", "plymouth", "Friday", "2023-08-04", "08:00", "17:30", 30.0, 9.0, 34.1, 44.75, "Released from NHSP", 402.75, 95.85, "NHSP"], ["Chandrakumar Ganeshamoorthy", "Ramsay oaks", "Friday", "2023-08-04", "19:30", "20:00", 0.0, 0.5, 55.0, 60.0, "wrong hours inputted to etips - now amended", 30.0, 2.5, "NHSP"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Thursday", "2023-07-27", "08:00", "16:30", 30.0, 8.0, 50.0, 60.0, "Hours Submitted to ETips", 480.0, 80.0, "ETIPS"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Friday", "2023-07-28", "08:00", "17:30", 30.0, 9.0, 50.0, 60.0, "Hours Submitted to ETips", 540.0, 90.0, "ETIPS"], ["Gemima Redd", "Royal Berkshire", "Wednesday", "2023-08-02", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Submitted to NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Thursday", "2023-08-03", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Submitted to NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Monday", "2023-08-07", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Submitted to NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Tuesday", "2023-08-08", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Submitted to NHSP", 380.0, 99.75, "NHSP"], ["Gemima Redd", "Royal Berkshire", "Wednesday", "2023-08-09", "08:00", "18:00", 30.0, 9.5, 29.5, 40.0, "Submitted to NHSP", 380.0, 99.75, "NHSP"], ["Biren Chheda", "Wrexham - Frimley", "Monday", "2023-08-07", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Will be on next week report", 446.32, 101.32, "Clairty"], ["Biren Chheda", "Wrexham - Frimley", "Wednesday", "2023-08-09", "07:30", "18:30", 30.0, 10.5, 30.0, 38.81, "Will be on next week report", 407.51, 92.51, "Clairty"], ["Biren Chedda", "Wrexham - Frimley", "Thursday", "2023-08-10", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Will be on next week report", 446.32, 101.32, "Clairty"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-08-07", "12:30", "18:45", 0.0, 6.25, 42.0, 60.0, "Uploaded to Etips for invoicing", 375.0, 112.5, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-08-08", "07:30", "20:00", 30.0, 12.0, 42.0, 60.0, "Uploaded to Etips for invoicing", 720.0, 216.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2023-08-09", "07:30", "17:00", 30.0, 9.0, 42.0, 60.0, "Uploaded to Etips for invoicing", 540.0, 162.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2023-08-10", "07:30", "17:00", 30.0, 9.0, 42.0, 60.0, "Uploaded to Etips for invoicing", 540.0, 162.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2023-08-11", "07:30", "18:45", 15.0, 11.0, 42.0, 60.0, "Uploaded to Etips for invoicing", 660.0, 198.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2023-08-12", "07:30", "16:30", 15.0, 8.75, 42.0, 60.0, "Uploaded to Etips for invoicing", 525.0, 157.5, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-08-07", "20:00", "08:00", 60.0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-08-08", "20:00", "08:00", 60.0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2023-08-12", "20:00", "08:00", 60.0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Sunday", "2023-08-13", "20:00", "08:00", 60.0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "ETIPS"], ["Rose Emmanuel", "Ramsay - Rivers", "Monday", "2023-08-07", "07:30", "19:00", 30.0, 11.0, 50.0, 60.0, "Uploaded to Etips for invoicing", 660.0, 110.0, "Etips"], ["Rose Emmanuel", "Ramsay - Rivers", "Wednesday", "2023-08-09", "07:30", "18:00", 30.0, 10.0, 50.0, 60.0, "Uploaded to Etips for invoicing", 600.0, 100.0, "Etips"], ["Rose Emmanuel", "Ramsay - Rivers", "Thursday", "2023-08-11", "07:30", "00:00", 30.0, 9.0, 50.0, 60.0, "Uploaded to Etips for invoicing", 540.0, 90.0, "Etips"], ["Rose Emmanuel", "Ramsay - Rivers", "Friday", "2023-08-12", "08:30", "13:30", 0.0, 5.0, 60.0, 68.0, "Uploaded to Etips for invoicing", 340.0, 40.0, "Etips"], ["Ndidi Onyekachi", "West Herts", "Tuesday", "2023-07-26", "08:00", "19:00", 30.0, 10.5, 30.0, 34.0, "Will come over on NHSP", 357.0, 42.0, "NHSP"], ["Jane Pengelly", "Derriford - Plymouth", "Tuesday", "2023-08-08", "08:00", "17:45", 30.0, 9.25, 34.1, 44.75, "Will come over on NHSP this week", 413.94, 98.51, "NHSP"], ["Jane Pengelly", "Derriford - Plymouth", "Wednesdsy", "2023-08-09", "08:00", "17:45", 0.0, 9.25, 34.1, 44.75, "Will come over on NHSP this week", 413.94, 98.51, "NHSP"], ["Jane Pengelly", "Derriford - Plymouth", "Thursday", "2023-08-10", "08:00", "19:00", 0.0, 11.0, 34.1, 44.75, "Will come over on NHSP this week", 492.25, 117.15, "NHSP"], ["Jane Pengelly", "Derriford - Plymouth", "Friday", "2023-08-11", "08:00", "18:00", 30.0, 9.5, 34.1, 44.75, "Will come over on NHSP this week", 425.13, 101.18, "NHSP"], ["Florence Rufu", "Ramsay - Blakelands", "Monday", "2023-07-31", "08:00", "19:00", 30.0, 10.5, 35.0, 39.33, "Will come over on next weeks Etips", 412.97, 45.47, "etips"], ["Florence Rufu", "Ramsay - Blakelands", "Thursday", "2023-08-03", "08:00", "18:00", 30.0, 9.5, 35.0, 39.33, "Will come over on next weeks Etips", 373.64, 41.14, "Etips"], ["Zahra Noor", "Royal London", "Monday", "2023-08-07", "07:30", "18:00", 30.0, 10.0, 35.0, 40.0, "Will get TS countersigned on Thursday", 400.0, 50.0, "HRoster"], ["Zahra Noor", "Royal London", "Tuesday", "2023-08-08", "07:30", "21:30", 60.0, 13.0, 35.0, 40.0, "Will get TS countersigned on Thursday", 520.0, 65.0, "HRoster"], ["Robert East", "NHSP - Oxford Uni", "Thursday", "2023-07-27", "07:45", "17:45", 30.0, 9.5, 31.5, 39.5, "Released for Invoicing", 375.25, 76.0, "NHSP"], ["Robert East", "NHSP - Oxford Uni", "Tuesday", "2023-08-01", "07:45", "18:15", 30.0, 10.0, 31.5, 39.5, "Released for Invoicing", 395.0, 80.0, "NHSP"], ["Togy Sebastian", "NHSP - Royal Berkshire", "Thursday", "2023-08-10", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Ward Manager to release shifts this week", 450.0, 70.0, "NHSP"], ["Togy Sebastian", "NHSP - Royal Berkshire", "Friday", "2023-08-11", "07:30", "18:00", 30.0, 10.0, 38.0, 45.0, "Ward Manager to release shifts this week", 450.0, 70.0, "NHSP"], ["Robert East", "Oxford University", "Wesnesday", "2023-08-09", "07:45", "17:45", 30.0, 9.5, 31.5, 39.5, "Shifts have been Released", 375.25, 76.0, "NHSP"], ["Robert East", "Oxford University", "Thursday", "2023-08-10", "07:45", "17:45", 30.0, 9.5, 31.5, 39.5, "Shifts have been Released", 375.25, 76.0, "NHSP"], ["Mariel Cabading", "Ramsay - North Downs", "Saturday", "2023-07-08", "20:30", "08:00", 60.0, 10.5, 35.0, 43.19, "Submitted to Etips, Off next week", 453.5, 86.0, "Etips"], ["Biren Chheda", "Frimley Hosiptal", "Monday", "2023-08-14", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Shifts were finalized too late on client roster", 446.32, 101.32, "Clarity"], ["Biren Chheda", "Frimley Hosiptal", "Tuesday", "2023-08-15", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Shifts were finalized too late on client roster", 446.32, 101.32, "Clarity"], ["Biren Chheda", "Frimley Hosiptal", "Wednesday", "2023-08-16", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Shifts were finalized too late on client roster", 446.32, 101.32, "Clarity"], ["Biren Chheda", "Frimley Hosiptal", "Thursday", "2023-08-17", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Shifts were finalized too late on client roster", 446.32, 101.32, "Clarity"], ["Biren Chheda", "Frimley Hosiptal", "Friday", "2023-08-18", "07:30", "19:30", 30.0, 11.5, 30.0, 38.81, "Shifts were finalized too late on client roster", 446.32, 101.32, "Clarity"], ["Jane Mayhew", "Frimley Hospital", "Wednesday", "2023-08-23", "07:30", "19:00", 30.0, 11.0, 35.0, 42.68, "Shifts were finalized too late on client roster", 469.48, 84.48, "Clarity"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Tuesday", "2023-08-29", "08:00", "17:30", 30.0, 9.0, 55.0, 60.0, "Submitted too late on Etips", 465.0, 45.0, "Etips"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Friday", "2023-09-01", "08:00", "16:15", 30.0, 7.75, 55.0, 60.0, "Submitted too late on Etips", 465.0, 38.75, "Etips"], ["Sandra Duarte Botello", "Nuffield - Oxford", "Wednesday", "2023-08-30", "08:00", "19:00", 30.0, 10.5, 48.0, 51.16, "Submitted too late on Etips", 537.18, 33.18, "Etips"], ["Sandra Duarte Botello", "Nuffield - Oxford", "Thursday", "2023-08-31", "08:00", "17:00", 30.0, 8.5, 48.0, 51.16, "Submitted too late on Etips", 434.86, 26.86, "Etips"], ["Sandra Duarte Botello", "Nuffield - Oxford", "Saturday", "2023-09-02", "08:00", "18:00", 30.0, 9.5, 50.0, 53.35, "Submitted too late on Etips", 506.83, 31.83, "Etips"], ["Rose Emmanuel", "Ramsay - Rivers", "Friday", "2023-09-01", "12:00", "18:30", 30.0, 6.0, 50.0, 60.0, "Sent to another agency, missed cutoff day/time", 360.0, 60.0, "Etips"], ["Rose Emmanuel", "Ramsay - Rivers", "Saturday", "2023-09-02", "07:30", "14:30", 30.0, 6.5, 60.0, 65.0, "Sent to another agency, missed cutoff day/time", 422.5, 32.5, "Etips"], ["Paula Ibanez", "Spire - Wellesley", "Thursday", "2023-08-31", "07:30", "16:00", 30.0, 8.0, 36.66, 40.3, "Submitted on client portal", 322.4, 29.12, "Bridge"], ["Paula Ibanez", "Spire - Wellesley", "Wednesday", "2023-09-06", "07:30", "20:30", 30.0, 12.5, 36.66, 40.3, "Submitted on client portal", 503.75, 45.5, "Bridge"], ["Patrick Gambold", "Isle of Wight", "Thursday", "2023-09-14", "08:00", "17:00", 30.0, 8.5, 32.0, 34.94, "Candidate needs funds", 296.99, 24.99, "ID MED"], ["Patrick Gambold", "Isle of Wight", "Friday", "2023-09-15", "08:00", "17:15", 30.0, 8.75, 32.0, 34.94, "Candidate needs funds", 305.73, 25.73, "ID MED"], ["Mark Pablico", "Ramsay - North Downs", "Monday", "2023-09-11", "12:30", "18:45", 0.0, 6.25, 40.0, 43.19, "On next etips report", 269.94, 19.94, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Tuesday", "2023-09-12", "08:00", "18:00", 30.0, 9.5, 40.0, 43.19, "On next etips report", 410.31, 30.31, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Wednesday", "2023-09-13", "08:00", "18:45", 30.0, 10.75, 40.0, 43.19, "On next etips report", 464.29, 34.29, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Thursday", "2023-09-14", "07:45", "18:30", 15.0, 10.5, 40.0, 43.19, "On next etips report", 453.5, 33.5, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Friday", "2023-09-15", "08:15", "14:00", 0.0, 5.75, 40.0, 43.19, "On next etips report", 248.34, 18.34, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Saturday", "2023-09-16", "07:30", "16:15", 15.0, 8.5, 40.0, 43.19, "On next etips report", 367.12, 27.12, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Tuesday", "2023-08-29", "08:00", "17:00", 30.0, 8.5, 50.0, 60.0, "Uploaded onto next etips report", 510.0, 85.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Wednesday", "2023-08-31", "00:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Uploaded onto next etips report", 570.0, 95.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Thursday", "2023-09-14", "08:00", "18:30", 30.0, 10.0, 55.0, 60.0, "Uploaded late on to Etips", 600.0, 50.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Friday", "2023-09-15", "08:00", "18:30", 30.0, 10.0, 55.0, 60.0, "Uploaded late on to Etips", 600.0, 50.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Saturday", "2023-09-16", "08:00", "17:00", 30.0, 8.5, 60.0, 65.0, "Uploaded late on to Etips", 552.5, 42.5, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Thursday", "2023-09-07", "07:30", "16:00", 30.0, 8.0, 42.0, 48.33, "Uploaded late on to Etips", 386.64, 50.64, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Saturday", "2023-09-09", "07:30", "17:15", 15.0, 9.5, 42.0, 48.33, "Uploaded late on to Etips", 459.14, 60.14, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2023-09-12", "07:30", "18:00", 30.0, 10.0, 42.0, 48.33, "Uploaded late on to Etips", 483.3, 63.3, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Thursday", "2023-09-14", "07:30", "18:30", 15.0, 10.75, 42.0, 48.33, "Uploaded late on to Etips", 519.55, 68.05, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Friday", "2023-09-15", "07:30", "15:30", 15.0, 7.75, 42.0, 48.33, "Uploaded late on to Etips", 374.56, 49.06, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Monday", "2023-09-18", "07:30", "18:45", 15.0, 11.0, 42.0, 48.33, "Uploaded late on to Etips", 531.63, 69.63, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2023-09-19", "07:30", "18:00", 30.0, 10.0, 42.0, 48.33, "Uploaded late on to Etips", 483.3, 63.3, "Etips"], ["Marian Gbadamosi", "HRoster - Darent Valley", "Tuesday", "2023-08-29", "08:00", "19:00", 30.0, 10.5, 30.0, 33.15, "Trust confirmed they are adding to report", 348.08, 33.08, "HRoster"], ["Gale Ann Barangan", "West Hertfordshire", "Wednesday", "2023-07-26", "08:00", "20:00", 30.0, 11.5, 30.0, 34.0, "waiting for NHSP to approve shift", 391.0, 46.0, "NHSP"], ["Stephen Roberts", "Frimley", "Friday", "2023-09-15", "07:30", "18:00", 30.0, 10.0, 38.0, 42.68, "Was never sent over on a backingreport", 426.8, 46.8, "ID Med"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-09-18", "07:30", "18:45", 15.0, 11.0, 42.0, 50.6, "Uploaded late on etips", 556.6, 94.6, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-09-19", "07:30", "18:00", 30.0, 10.0, 42.0, 50.6, "Uploaded late on etips", 506.0, 86.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2023-09-20", "07:30", "12:30", 0.0, 5.0, 42.0, 50.6, "Uploaded late on etips", 253.0, 43.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2023-09-21", "07:30", "16:45", 30.0, 8.75, 42.0, 50.6, "Uploaded late on etips", 442.75, 75.25, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2023-09-23", "07:30", "16:45", 0.0, 9.25, 42.0, 50.6, "Uploaded late on etips", 468.05, 79.55, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-09-19", "20:00", "08:00", 0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2023-09-20", "20:00", "08:00", 0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2023-09-22", "20:00", "08:00", 0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "Etips"], ["Diosdado Wagan", "Ramsay - North Downs", "Sunday", "2023-09-24", "20:00", "08:00", 0, 1.0, 55.0, 60.0, "On Call Hours", 60.0, 5.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Tuesday", "2023-09-05", "08:00", "13:00", 0.0, 5.0, 50.0, 60.0, "Uploaded after cutoff time", 300.0, 50.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Thursday", "2023-09-05", "08:00", "17:30", 30.0, 9.0, 50.0, 60.0, "Uploaded after cutoff time", 540.0, 90.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Friday", "2023-09-05", "08:00", "15:30", 30.0, 8.5, 50.0, 60.0, "Uploaded after cutoff time", 510.0, 85.0, "Etips"], ["Roseline Emmanuel", "Retinue - Circle Health", "Thursday", "2023-10-05", "08:00", "18:00", 30.0, 9.5, 50.0, 54.99, "", 522.41, 47.41, "Circle"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-10-02", "08:00", "19:00", 15.0, 10.75, 42.0, 50.6, "", 543.95, 92.45, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-10-03", "07:30", "19:30", 30.0, 11.5, 42.0, 50.6, "", 581.9, 98.9, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2023-10-04", "07:30", "19:15", 30.0, 11.25, 42.0, 50.6, "", 569.25, 96.75, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2023-10-05", "07:30", "17:00", 30.0, 9.0, 42.0, 50.6, "", 455.4, 77.4, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2023-10-07", "07:30", "15:45", 15.0, 8.0, 42.0, 50.6, "", 404.8, 68.8, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2023-10-06", "20:00", "08:00", 0, 1.0, 55.0, 60.0, "", 60.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2023-10-07", "20:00", "08:00", 0, 1.0, 55.0, 60.0, "", 60.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Sunday", "203-08-10", "08:00", "08:00", 0, 1.0, 55.0, 60.0, "", 60.0, 5.0, "ETIPS"], ["Paul Reeves", "Lewisham", "Wednesday", "2023-09-13", "08:00", "18:00", 30.0, 9.5, 28.0, 30.0, "shift on HR and approved to be paid next week", 285.0, 19.0, "HRoster"], ["Jovanie Santos", "Ramsay - North Downs", "Monday", "2023-09-10", "07:30", "17:15", 30.0, 9.25, 42.0, 48.33, "Worker in need of Funds ASAP - will be charged tomorrow", 447.05, 58.55, "ETIPS"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2023-10-10", "07:30", "18:00", 30.0, 10.0, 42.0, 48.33, "Worker in need of Funds ASAP - will be charged tomorrow", 483.3, 63.3, "ETIPS"], ["Jovanie Santos", "Ramsay - North Downs", "Wednesday", "2023-11-10", "07:30", "19:15", 30.0, 11.25, 42.0, 48.33, "Worker in need of Funds ASAP - will be charged tomorrow", 543.71, 71.21, "ETIPS"], ["Penelope Piccio", "Circle Reading", "Monday", "2023-02-10", "12:30", "20:00", 0.0, 7.5, 45.5, 55.0, "Worker has been waiting for Funds for a while", 412.5, 71.25, "Circlle"], ["Penelope Piccio", "Circle Reading", "Tuesday", "2023-03-10", "07:30", "18:00", 30.0, 10.0, 45.5, 55.0, "Worker has been waiting for Funds for a while", 550.0, 95.0, "Circlle"], ["Penelope Piccio", "Circle Reading", "Wednesday", "2023-04-10", "07:30", "18:00", 30.0, 10.0, 45.5, 55.0, "Worker has been waiting for Funds for a while", 550.0, 95.0, "Circlle"], ["Penelope Piccio", "Circle Reading", "Thursday", "2023-05-10", "07:30", "18:00", 0.0, 5.0, 45.5, 55.0, "Worker has been waiting for Funds for a while", 275.0, 47.5, "Circlle"], ["Penelope Piccio", "Circle Reading", "Friday", "2023-06-10", "07:30", "12:30", 0.0, 5.0, 45.5, 55.0, "Worker has been waiting for Funds for a while", 275.0, 47.5, "Circlle"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Tuesday", "2023-10-10", "08:00", "18:30", 60.0, 10.0, 50.0, 60.0, "Submitted TS with incorrect Trust", 600.0, 100.0, "Etips"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Thursday", "2023-10-12", "08:00", "18:30", 60.0, 10.0, 50.0, 60.0, "Submitted TS with incorrect Trust", 600.0, 100.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Tuesday", "2023-10-02", "08:00", "16:30", 0.0, 5.0, 50.0, 60.0, "Sumbitted TS too late, Will be on next weeks report", 300.0, 50.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Thursday", "2023-10-05", "08:00", "16:00", 30.0, 9.0, 50.0, 60.0, "Sumbitted TS too late, Will be on next weeks report", 540.0, 90.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Friday", "2023-10-06", "08:00", "15:00", 30.0, 8.5, 50.0, 60.0, "Sumbitted TS too late, Will be on next weeks report", 510.0, 85.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Tuesday", "2023-09-25", "08:00", "17:45", 30.0, 9.25, 50.0, 60.0, "Our fault for shift not being paid - will be charged next week", 555.0, 92.5, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Thursday", "2023-09-28", "08:00", "17:30", 30.0, 9.0, 50.0, 60.0, "Our fault for shift not being paid - will be charged next week", 540.0, 90.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Friday", "2023-09-29", "08:00", "16:30", 30.0, 8.0, 50.0, 60.0, "Our fault for shift not being paid - will be charged next week", 480.0, 80.0, "Etips"], ["Gloria Ibbe", "Lewisham", "MONDAY", "2023-10-16", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "Shift pending finalization, Candiate needs funds for bills due today", 289.66, 23.66, "HRoster"], ["Aleksandra Lacey", "Royal Berkshire", "Monday", "2023-10-09", "08:00", "17:30", 30.0, 9.0, 35.0, 40.0, "Will be be invoiced this week", 360.0, 45.0, "NHSP"], ["Patrick Gambold", "Isle of Wright", "Monday", "2023-10-16", "08:00", "16:45", 30.0, 8.25, 32.0, 34.94, "Will be charged tomorrows report - Worker needs funds", 288.26, 24.26, "ID MED"], ["Patrick Gambold", "Isle of Wright", "Tuesday", "2023-10-17", "08:00", "15:30", 30.0, 7.0, 32.0, 34.94, "Will be charged tomorrows report - Worker needs funds", 244.58, 20.58, "ID MED"], ["Patrick Gambold", "Isle of Wright", "Wednesday", "2023-10-18", "08:00", "19:00", 30.0, 10.5, 32.0, 34.94, "Will be charged tomorrows report - Worker needs funds", 366.87, 30.87, "ID MED"], ["Patrick Gambold", "Isle of Wright", "Friday", "2023-10-20", "08:00", "11:45", 0.0, 3.75, 32.0, 34.94, "Will be charged tomorrows report - Worker needs funds", 131.03, 11.03, "ID MED"], ["Gloria Ibbe", "Lewisham", "Tuesday", "2023-10-24", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "Worker Needs Funds", 289.66, 23.66, "HRoster"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Monday", "2023-10-09", "08:00", "15:00", 30.0, 6.5, 50.0, 60.0, "Submitted TS after trust cutoff time", 390.0, 65.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Tuesday", "2023-10-10", "08:00", "15:30", 30.0, 7.0, 50.0, 60.0, "Submitted TS after trust cutoff time", 420.0, 70.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Wednesday", "2023-10-11", "08:00", "15:30", 30.0, 7.0, 50.0, 60.0, "Submitted TS after trust cutoff time", 420.0, 70.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Thursday", "2023-10-12", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Submitted TS after trust cutoff time", 570.0, 95.0, "Etips"], ["Rinah Andiappareddi", "Ramsay - Cherwell", "Friday", "2023-10-13", "08:00", "15:30", 30.0, 7.0, 50.0, 60.0, "Submitted TS after trust cutoff time", 420.0, 70.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Monday", "2023-10-23", "08:00", "18:45", 30.0, 10.25, 50.0, 60.0, "Submitted TS after trust cutoff time", 615.0, 102.5, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Tuesday", "2023-10-24", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Submitted TS after trust cutoff time", 600.0, 100.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Wednesday", "2023-10-25", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Submitted TS after trust cutoff time", 600.0, 100.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Thursday", "2023-10-26", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Submitted TS after trust cutoff time", 600.0, 100.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Ramsay - Oaks", "Friday", "2023-10-27", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Submitted TS after trust cutoff time", 600.0, 100.0, "Etips"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Monday", "2023-10-30", "08:00", "18:15", 30.0, 9.75, 50.0, 59.5, "Shift wasnt included on today's report", 580.13, 92.63, "Retinue"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Tuesday", "2023-10-31", "08:00", "21:00", 45.0, 12.25, 50.0, 59.5, "Shift wasnt included on today's report", 728.88, 116.38, "Retinue"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Wednesday", "2023-11-01", "08:00", "18:00", 30.0, 9.5, 50.0, 59.5, "Shift wasnt included on today's report", 565.25, 90.25, "Retinue"], ["Victor Provido", "Reading", "Saturday", "2023-10-21", "07:30", "19:00", 30.0, 11.0, 45.0, 55.0, "Submitted TS awile aggo, awaiting action from Bridge portal", 605.0, 110.0, "Circle"], ["Patrick Gambold", "Isle of Wright", "Monday", "2023-10-30", "08:00", "18:00", 0.0, 10.0, 32.0, 34.94, "Candidate forgot to send TS to us", 349.4, 29.4, "Clarity"], ["Patrick Gambold", "Isle of Wright", "Tuesday", "2023-10-31", "08:00", "18:00", 30.0, 9.5, 32.0, 34.94, "Candidate forgot to send TS to us", 331.93, 27.93, "Clarity"], ["Patrick Gambold", "Isle of Wright", "Wednesday", "2023-11-01", "08:00", "17:30", 30.0, 9.0, 32.0, 34.94, "Candidate forgot to send TS to us", 314.46, 26.46, "Clarity"], ["Patrick Gambold", "Isle of Wright", "Thursday", "2023-11-02", "08:00", "17:30", 30.0, 9.0, 32.0, 34.94, "Candidate forgot to send TS to us", 314.46, 26.46, "Clarity"], ["Patrick Gambold", "Isle of Wright", "Friday", "2023-11-03", "08:00", "10:00", 0.0, 2.0, 32.0, 34.94, "Candidate forgot to send TS to us", 69.88, 5.88, "Clarity"], ["Mark Pablico", "Ramsay - North Downs", "Monday", "2023-11-13", "08:00", "18:00", 30.0, 9.5, 40.0, 43.0, "Submitted TS after cutoff", 408.5, 28.5, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Tuesday", "2023-11-14", "08:00", "19:15", 15.0, 11.0, 40.0, 43.0, "Submitted TS after cutoff", 473.0, 33.0, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Thursday", "2023-11-16", "08:00", "18:30", 15.0, 10.25, 40.0, 43.0, "Submitted TS after cutoff", 440.75, 30.75, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Friday", "2023-11-17", "08:00", "16:30", 30.0, 8.0, 40.0, 43.0, "Submitted TS after cutoff", 344.0, 24.0, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Saturday", "2023-11-18", "08:45", "14:30", 0.0, 5.75, 45.0, 46.24, "Submitted TS after cutoff", 265.88, 7.13, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Monday", "2023-11-20", "08:00", "17:15", 15.0, 9.0, 42.0, 48.33, "TS Submitted after cutoff times", 434.97, 56.97, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2023-11-23", "07:30", "17:00", 30.0, 9.0, 42.0, 48.33, "TS Submitted after cutoff times", 434.97, 56.97, "Etips"], ["Fanol Gjata", "Ramsay - North Downs", "Tuesday", "2023-11-21", "07:30", "19:30", 30.0, 11.5, 40.0, 45.27, "TS Submitted after cutoff times", 520.61, 60.61, "Etips"], ["Fanol Gjata", "Ramsay - North Downs", "Wednesday", "2023-11-22", "07:30", "18:00", 30.0, 10.0, 40.0, 45.27, "TS Submitted after cutoff times", 452.7, 52.7, "Etips"], ["Victor Provido", "Spire - Dunedin", "Saturday", "2023-11-15", "07:30", "00:00", 30.0, 10.0, 38.0, 55.0, "Worker in need of funds before Friday", 550.0, 170.0, "Retinue"], ["Angelo Salomeo", "Ramsay - North Downs", "Tuesday", "2023-11-28", "07:30", "20:15", 15.0, 12.5, 46.0, 50.0, "Worker submited TS after cutoff - On System for invoiing", 625.0, 50.0, "Etips"], ["Angelo Salomeo", "Ramsay - North Downs", "Thursday", "2023-11-30", "07:30", "13:00", 0.0, 5.5, 46.0, 50.0, "Worker submited TS after cutoff - On System for invoiing", 275.0, 22.0, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Monday", "2023-11-27", "08:00", "18:00", 30.0, 9.5, 42.0, 45.0, "TS Submitted after cutoff times", 427.5, 28.5, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Tuesday", "2023-11-28", "09:00", "20:15", 30.0, 10.75, 42.0, 45.0, "TS Submitted after cutoff times", 483.75, 32.25, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Thursday", "2023-11-29", "08:00", "16:30", 30.0, 8.0, 42.0, 45.0, "TS Submitted after cutoff times", 360.0, 24.0, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Friday", "2023-11-30", "07:30", "17:30", 30.0, 9.5, 42.0, 45.0, "TS Submitted after cutoff times", 427.5, 28.5, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Saturday", "2023-12-01", "08:30", "17:00", 30.0, 8.0, 48.0, 50.0, "TS Submitted after cutoff times", 400.0, 16.0, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Sunday", "2023-12-02", "08:00", "14:30", 0.0, 6.5, 48.0, 50.0, "TS Submitted after cutoff times", 325.0, 13.0, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Monday", "2023-12-04", "07:30", "18:00", 30.0, 10.0, 42.0, 48.0, "Submitted TS after client cutoff", 480.0, 60.0, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2023-12-05", "07:30", "20:15", 15.0, 12.5, 42.0, 48.0, "Submitted TS after client cutoff", 600.0, 75.0, "Etips"], ["Ana Paggao", "Watford Gen Hospital", "Wednesday", "2023-11-01", "08:00", "19:30", 30.0, 11.0, 30.0, 34.0, "Candidate claiming to leave DW / Complain if not paid", 374.0, 44.0, "NHSP"], ["Rogeilo Jr Albano", "Nuffield - Bournemouth", "Friday", "2023-11-17", "07:15", "15:15", 25.0, 7.75, 30.0, 34.0, "", 263.5, 31.0, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Monday", "2023-12-04", "08:30", "17:00", 15.0, 8.25, 42.0, 45.0, "TS On Etips", 371.25, 24.75, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Tuesday", "2023-12-05", "08:00", "20:30", 15.0, 12.25, 42.0, 45.0, "TS On Etips", 551.25, 36.75, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Wednesday", "2023-12-06", "09:30", "17:45", 30.0, 7.75, 42.0, 45.0, "TS On Etips", 348.75, 23.25, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Thursday", "2023-12-07", "08:00", "15:30", 30.0, 7.0, 42.0, 45.0, "TS On Etips", 315.0, 21.0, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Friday", "2023-12-08", "08:00", "17:00", 15.0, 8.75, 42.0, 45.0, "TS On Etips", 393.75, 26.25, "Etips"], ["Mark Pablico", "Ramsay - North Downs", "Saturday", "2023-12-09", "08:30", "17:00", 15.0, 8.25, 48.0, 50.0, "TS On Etips", 412.5, 16.5, "Etips"], ["Mitchell Balogun", "SABP", "Friday", "2023-12-08", "07:30", "12:30", 0.0, 5.0, 36.0, 38.91, "Shift Queried on NHSP delay in authorisation", 194.55, 14.55, "NHSP"], ["Mitchell Balogun", "SABP", "Tuesday", "2023-12-05", "07:30", "13:30", 0.0, 5.0, 36.0, 38.91, "Shift Queried on NHSP delay in authorisation", 194.55, 14.55, "NHSP"], ["Nyasha Jena", "SABP", "Friday", "2023-12-08", "07:30", "14:30", 0.0, 5.0, 31.72, 38.91, "Shift Queried on NHSP delay in authorisation", 194.55, 35.95, "NHSP"], ["Charren Torralba", "Nuffield - Woking", "Monday", "2023-11-13", "07:30", "17:30", 30.0, 9.5, 39.0, 45.0, "Paying on Behalf of Comfort Healthcare", 427.5, 57.0, "Etips"], ["Victor Provido", "spire dunedin hospital", "Monday", "2023-12-04", "07:30", "14:30", 0.0, 7.0, 40.0, 48.0, "shift is on and approved on Retinue but needs to be paid early", 336.0, 56.0, "Retinue"], ["Victor Provido", "spire dunedin hospital", "Wednesday", "2023-12-06", "07:30", "18:00", 30.0, 10.0, 40.0, 48.0, "shift is on and approved on Retinue but needs to be paid early", 480.0, 80.0, "Retinue"], ["Victor Provido", "spire dunedin hospital", "Thursday", "2023-12-07", "07:30", "19:30", 30.0, 12.5, 40.0, 48.0, "shift is on and approved on Retinue but needs to be paid early", 600.0, 100.0, "Retinue"], ["Victor Provido", "spire dunedin hospital", "Friday", "2023-12-08", "07:30", "18:00", 30.0, 10.0, 40.0, 48.0, "shift is on and approved on Retinue but needs to be paid early", 480.0, 80.0, "Retinue"], ["Jovanie Santos", "Ramsay - North Downs", "Thursday", "2023-12-21", "07:30", "16:45", 15.0, 9.0, 42.0, 48.33, "On Etips portal for invoicing Next Week", 434.97, 56.97, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-12-18", "12:30", "18:30", 0.0, 6.0, 42.0, 50.6, "On Etips portal for invoicing Next Week", 303.6, 51.6, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2023-12-19", "08:30", "18:30", 15.0, 9.75, 42.0, 50.6, "On Etips portal for invoicing Next Week", 493.35, 83.85, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2023-12-20", "07:30", "19:15", 30.0, 11.25, 42.0, 50.6, "On Etips portal for invoicing Next Week", 569.25, 96.75, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2023-12-21", "07:30", "16:45", 15.0, 9.0, 42.0, 50.6, "On Etips portal for invoicing Next Week", 455.4, 77.4, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2023-12-18", "20:00", "08:00", 0.0, 1.0, 55.0, 60.0, "On Etips portal for invoicing Next Week", 60.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2023-12-20", "20:00", "08:00", 0.0, 1.0, 55.0, 60.0, "On Etips portal for invoicing Next Week", 60.0, 5.0, "ETIPS"], ["Patrick Gambold", "ID Medical - Isle Of Wight", "Thursday", "2023-12-14", "08:00", "14:30", 30.0, 6.0, 32.0, 34.94, "On client portal", 209.64, 17.64, "ID Medical"], ["Consuelo Johnson", "Ramsay - Pinehill", "Friday", "2023-12-15", "12:00", "18:00", 0, 6.0, 42.0, 48.33, "Did not realize there was a differnt cuttoff due to bank holidays", 289.98, 37.98, "ETIPS"], ["Patrick Gambold", "Isle Of Wight", "Monday", "2023-12-18", "08:00", "16:15", 30.0, 7.75, 32.0, 34.94, "Consulant request", 270.79, 22.79, "ID Medical"], ["Patrick Gambold", "Isle Of Wight", "Tuesday", "2023-12-19", "08:00", "17:45", 30.0, 9.25, 32.0, 34.94, "Consulant request", 323.2, 27.2, "ID Medical"], ["Patrick Gambold", "Isle Of Wight", "Friday", "2023-12-22", "08:00", "11:30", 0.0, 3.5, 32.0, 34.94, "Consulant request", 122.29, 10.29, "ID Medical"], ["Patrick Gambold", "Isle Of Wight", "Wednesday", "2023-12-27", "08:00", "12:00", 0.0, 4.0, 32.0, 34.94, "On portal to be processed next week", 139.76, 11.76, "ID Medical"], ["Shabana Sultanta", "South London Maudsley", "Friday", "2024-01-02", "07:00", "13:00", 0.0, 6.0, 42.0, 47.0, "PRC rate card yet to be apporved,", 282.0, 30.0, "NHSP"], ["Rogeilo Jr Albano", "Nuffield - Bournemouth", "Wednesday", "2024-01-10", "07:30", "19:00", 30.0, 11.0, 37.0, 51.1, "On Client Portal", 562.1, 155.1, "Etips"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2024-01-10", "07:30", "19:15", 30.0, 11.25, 42.0, 48.33, "", 543.71, 71.21, "Etips"], ["Simon Broughton", "South London Maudsley", "Friday", "2024-01-05", "07:00", "13:00", 0.0, 6.0, 42.0, 47.0, "Consulant Issues Pay Only for First Slam Shift", 282.0, 30.0, "NHSP"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2024-01-08", "07:30", "18:30", 30.0, 10.5, 42.0, 50.6, "Submitted a few mins after client cutoff", 531.3, 90.3, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2024-01-09", "07:30", "19:30", 30.0, 11.5, 42.0, 50.6, "Submitted a few mins after client cutoff", 581.9, 98.9, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2024-01-10", "07:30", "14:15", 15.0, 6.5, 42.0, 50.6, "Submitted a few mins after client cutoff", 328.9, 55.9, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2024-01-11", "07:30", "20:30", 30.0, 12.5, 42.0, 50.6, "Submitted a few mins after client cutoff", 632.5, 107.5, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2024-01-12", "07:30", "17:15", 15.0, 9.5, 42.0, 50.6, "Submitted a few mins after client cutoff", 480.7, 81.7, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2024-01-13", "07:30", "19:15", 15.0, 11.5, 45.0, 50.6, "Submitted a few mins after client cutoff", 581.9, 64.4, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2024-01-09", "20:00", "08:00", 0.0, 1.0, 55.0, 76.87, "On Call Hours", 76.87, 21.87, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2024-01-11", "20:00", "08:00", 0.0, 1.0, 55.0, 76.87, "On Call Hours", 76.87, 21.87, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2024-01-12", "20:00", "08:00", 0.0, 1.0, 55.0, 76.87, "On Call Hours", 76.87, 21.87, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2024-01-13", "20:00", "08:00", 0.0, 1.0, 55.0, 76.87, "On Call Hours", 76.87, 21.87, "ETIPS"], ["Angelo Marco Salomeo", "Ramsay - North Downs", "Tuesday", "2024-01-09", "13:00", "19:00", 0.0, 6.0, 46.0, 50.0, "I forgot to submit on Etips for Payment", 300.0, 24.0, "ETIPS"], ["Angelo Marco Salomeo", "Ramsay - North Downs", "Wednesday", "2024-01-10", "07:30", "19:00", 15.0, 11.25, 46.0, 50.0, "I forgot to submit on Etips for Payment", 562.5, 45.0, "ETIPS"], ["Angelo Marco Salomeo", "Ramsay - North Downs", "Thursday", "2024-01-11", "08:00", "13:30", 0.0, 5.5, 46.0, 50.0, "I forgot to submit on Etips for Payment", 275.0, 22.0, "ETIPS"], ["Sandra Botello", "Oxford Mannor", "Monday", "2024-01-08", "08:00", "19:30", 30.0, 11.0, 48.0, 51.16, "Was sent to remi which we didnt have acess to TS", 562.76, 34.76, "ETIPS"], ["Sandra Botello", "Oxford Mannor", "Tuesday", "2024-01-09", "08:00", "19:30", 30.0, 11.0, 48.0, 51.16, "Was sent to remi which we didnt have acess to TS", 562.76, 34.76, "ETIPS"], ["Sandra Botello", "Oxford Mannor", "Wednesday", "2024-01-10", "08:00", "20:00", 30.0, 11.5, 48.0, 51.16, "Was sent to remi which we didnt have acess to TS", 588.34, 36.34, "ETIPS"], ["Sandra Botello", "Oxford Mannor", "Thursday", "2024-01-11", "08:00", "18:00", 30.0, 9.5, 48.0, 51.16, "Was sent to remi which we didnt have acess to TS", 486.02, 30.02, "ETIPS"], ["Sandra Botello", "Oxford Mannor", "Friday", "2024-01-12", "07:30", "20:30", 30.0, 12.5, 48.0, 51.16, "Was sent to remi which we didnt have acess to TS", 639.5, 39.5, "ETIPS"], ["Sandra Botello", "Oxford Mannor", "Saturday", "2024-01-13", "08:00", "16:00", 0.0, 8.0, 50.0, 53.35, "Was sent to remi which we didnt have acess to TS", 426.8, 26.8, "ETIPS"], ["Penelope Piccio", "Spire - Dunedin", "Thursday", "2024-01-18", "07:30", "18:30", 30.0, 10.5, 36.0, 44.0, "Submitted TS after invoice cutoff", 462.0, 84.0, "SPIRE"], ["Penelope Piccio", "Spire - Dunedin", "Friday", "2024-01-19", "07:30", "13:30", 0.0, 6.0, 36.0, 44.0, "Submitted TS after invoice cutoff", 264.0, 48.0, "SPIRE"], ["Marcia Morris Jackson", "Lewisham", "Monday", "2024-01-15", "08:00", "18:00", 30.0, 9.5, 28.0, 30.49, "", 289.66, 23.66, "HRoster"], ["Marcia Morris Jackson", "Lewisham", "Thursday", "2024-01-18", "09:00", "20:15", 45.0, 10.5, 28.0, 30.49, "", 320.15, 26.15, "HRoster"], ["Kelly Peel", "Spire - Dunedin", "Friday", "2024-01-12", "12:00", "17:30", 0.0, 5.5, 36.0, 44.0, "Submitted TS after cutoff", 242.0, 44.0, "SPIRE"], ["Kelly Peel", "Spire - Dunedin", "Monday", "2024-01-15", "13:00", "19:30", 0.0, 6.5, 36.0, 44.0, "Submitted TS after cutoff", 286.0, 52.0, "SPIRE"], ["Kelly Peel", "Spire - Dunedin", "Tuesday", "2024-01-16", "07:30", "18:00", 30.0, 10.0, 36.0, 44.0, "Submitted TS after cutoff", 440.0, 80.0, "SPIRE"], ["Mark Pablco", "Ramsay - North Downs", "Monday", "2024-01-22", "07:30", "18:15", 30.0, 10.75, 42.0, 50.6, "", 543.95, 92.45, "Etips"], ["Mark Pablco", "Ramsay - North Downs", "Tuesday", "2024-01-27", "08:00", "14:00", 0.0, 6.0, 42.0, 50.6, "", 303.6, 51.6, "Etips"], ["Angelo Marco Salomeo", "Ramsay - North Downs", "Tuesday", "2024-01-23", "12:00", "20:30", 15.0, 8.25, 46.0, 50.0, "I forgot to uplaod TS to client portal", 412.5, 33.0, "Etips"], ["Angelo Marco Salomeo", "Ramsay - North Downs", "Wednesday", "2024-01-24", "13:15", "19:45", 0.0, 6.5, 46.0, 50.0, "I forgot to uplaod TS to client portal", 325.0, 26.0, "Etips"], ["Angelo Marco Salomeo", "Ramsay - North Downs", "Thursday", "2024-01-25", "08:30", "13:00", 0.0, 4.5, 46.0, 50.0, "I forgot to uplaod TS to client portal", 225.0, 18.0, "Etips"], ["Angelo Marco Salomeo", "Ramsay - North Downs", "Saturday", "2024-01-27", "13:30", "19:00", 0.0, 5.5, 50.0, 60.0, "I forgot to uplaod TS to client portal", 330.0, 55.0, "Etips"], ["Chandrakumar Ganeshamoorthy", "Spire - Wellseley Hospital", "Tuesday", "2024-01-23", "07:30", "15:25", 30.0, 7.25, 40.0, 46.0, "Consulant request as candidate needs funds for bills - all hours on portal", 333.5, 43.5, "Bridge"], ["Patrick Gambold", "Isle Of Wight", "Monday", "2024-01-22", "08:00", "16:45", 30.0, 8.25, 32.0, 34.94, "", 288.26, 24.26, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Tuesday", "2024-01-23", "08:00", "14:30", 0.0, 6.5, 32.0, 34.94, "", 227.11, 19.11, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Friday", "2024-01-26", "08:00", "10:45", 0.0, 3.75, 32.0, 34.94, "", 131.03, 11.03, "Clarity"], ["Chandrakruma Ganeshamoorthy", "Circle Kings Oak", "Tuesday", "2024-01-09", "08:00", "21:30", 30.0, 13.0, 38.0, 42.0, "shift is approved late, will be on 9th Feb report", 546.0, 52.0, "Retinue"], ["Chandrakruma Ganeshamoorthy", "Circle Kings Oak", "Thursday", "2024-01-11", "07:30", "18:30", 30.0, 10.5, 50.0, 55.0, "shift is approved late, will be on 9th Feb report", 577.5, 52.5, "Retinue"], ["Chandrakruma Ganeshamoorthy", "Circle Kings Oak", "Friday", "2024-01-12", "07:30", "18:00", 30.0, 10.0, 50.0, 55.0, "shift is approved late, will be on 9th Feb report", 550.0, 50.0, "Retinue"], ["Penelope Piccio", "Spire - Dunedin", "Thursday", "2024-01-31", "09:15", "18:15", 30.0, 8.5, 41.0, 44.41, "Shift will be paid on Friday", 377.49, 28.99, "RETINUE"], ["Mark Pablico", "Ramsay - North Downs", "Wednesday", "2024-01-31", "08:00", "17:30", 30.0, 9.0, 42.0, 50.6, "Sumbitted TS 5 Mins after Etips Cutoff. On Portal for next week", 455.4, 77.4, "ETIPS"], ["Mark Pablico", "Ramsay - North Downs", "Saturday", "2024-02-03", "08:00", "18:00", 15.0, 9.75, 48.0, 54.27, "Sumbitted TS 5 Mins after Etips Cutoff. On Portal for next week", 529.13, 61.13, "ETIPS"], ["Penelope Piccio", "Spire - Dunedin", "Saturday", "2024-01-27", "07:30", "16:30", 30.0, 8.5, 44.0, 46.95, "Shift will be paid charged on Friday's invoice", 399.08, 25.08, "RETINUE"], ["Audrey Daras", "Practice Plus - Portsmouth", "Wednesday", "2024-01-31", "07:30", "14:30", 0.0, 7.0, 40.0, 45.0, "Hours uplaoded to protal, system error with invoiciing. Will be on next weeks report", 315.0, 35.0, "ETIPS"], ["Kelly Peel", "Spire - Dunedin", "Tuesday", "2024-01-30", "07:30", "13:00", 0.0, 5.5, 36.0, 44.0, "TS uploaded to Portal after cutoff", 242.0, 44.0, "Bridge"], ["Mohammadreza Mohammadi", "Bristol & Western", "Thursday", "2024-02-01", "08:00", "17:00", 30.0, 8.5, 50.0, 59.23, "Shift approved on HR will be on Friday Report", 503.46, 78.46, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Western", "Friday", "2024-02-02", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Shift approved on HR will be on Friday Report", 562.69, 87.69, "RETINUE"], ["Mark Pablico", "Ramsay - North Downs", "Monday", "2024-02-05", "08:30", "19:00", 30.0, 10.0, 42.0, 50.6, "Shifts did not pull through to etips report will be charged next week", 506.0, 86.0, "ETIPS"], ["Mark Pablico", "Ramsay - North Downs", "Tuesday", "2024-02-06", "08:00", "18:00", 30.0, 9.5, 42.0, 50.6, "Shifts did not pull through to etips report will be charged next week", 480.7, 81.7, "ETIPS"], ["Mark Pablico", "Ramsay - North Downs", "Wednesday", "2024-02-07", "08:00", "19:45", 30.0, 11.25, 42.0, 50.6, "Shifts did not pull through to etips report will be charged next week", 569.25, 96.75, "ETIPS"], ["Audrey Daras", "Practice Plus", "Monday", "2024-02-12", "08:00", "17:30", 30.0, 9.0, 35.0, 38.95, "Shift coming over on next week report", 350.55, 35.55, "ETIPS"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2024-02-13", "07:30", "17:30", 30.0, 9.5, 44.0, 48.33, "Shift to be paid with her refferal fees which will be paid today.", 459.14, 41.14, "ETIPS"], ["Penelope Piccio", "Circle - Reading", "Monday", "2024-02-12", "07:30", "20:00", 30.0, 12.0, 45.5, 55.09, "Needs to be paid today", 661.08, 115.08, "CIRCLE"], ["Penelope Piccio", "Circle - Reading", "Tuesday", "2024-02-13", "07:30", "18:30", 30.0, 10.5, 45.5, 55.09, "Needs to be paid today", 578.45, 100.7, "CIRCLE"], ["Penelope Piccio", "Circle - Reading", "Wednesday", "2024-02-14", "07:30", "18:00", 30.0, 10.0, 45.5, 55.09, "Needs to be paid today", 550.9, 95.9, "CIRCLE"], ["Penelope Piccio", "Circle - Reading", "Thursday", "2024-02-15", "07:30", "18:30", 30.0, 10.5, 45.5, 55.09, "Needs to be paid today", 578.45, 100.7, "CIRCLE"], ["Mark Pablico", "North Downs", "Monday", "2024-02-19", "12:30", "18:00", 0.0, 5.5, 44.0, 50.6, "Shift uplaoded to Etips, Needs fund immediatley", 278.3, 36.3, "ETIPS"], ["Mark Pablico", "North Downs", "Saturday", "2024-02-24", "08:00", "13:30", 0.0, 5.5, 48.0, 54.27, "Shift uplaoded to Etips, Needs fund immediatley", 298.49, 34.49, "ETIPS"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Thursday", "2024-02-22", "08:00", "15:45", 30.0, 7.25, 50.0, 60.0, "Candidate submitted ts to wrong place", 435.0, 72.5, "ETIPS"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Thursday", "2024-02-29", "08:00", "14:00", 0.0, 6.0, 50.0, 60.0, "Candidate submitted ts to wrong place", 360.0, 60.0, "ETIPS"], ["Sandra Maria Duarte Botello", "Nuffield - Oxford Mannor", "Monday", "2024-02-26", "08:00", "18:30", 30.0, 10.0, 48.0, 51.16, "Missed the timesheet & She\u2019s had to fly home for a bereavement. She needs the funds", 511.6, 31.6, "ETIPS"], ["Sandra Maria Duarte Botello", "Nuffield - Oxford Mannor", "Tuesday", "2024-02-27", "08:00", "19:30", 30.0, 11.0, 48.0, 51.16, "Missed the timesheet & She\u2019s had to fly home for a bereavement. She needs the funds", 562.76, 34.76, "ETIPS"], ["Sandra Maria Duarte Botello", "Nuffield - Oxford Mannor", "Wednesday", "2024-02-28", "08:00", "19:30", 30.0, 11.0, 48.0, 51.16, "Missed the timesheet & She\u2019s had to fly home for a bereavement. She needs the funds", 562.76, 34.76, "ETIPS"], ["Patrick Gambold", "Isle of Wight", "Monday", "2024-02-26", "08:00", "18:00", 30.0, 9.5, 32.0, 34.94, "Submitted TS after trust cutoff. will be charged next week", 331.93, 27.93, "ID MED"], ["Patrick Gambold", "Isle of Wight", "Wednesday", "2024-02-28", "08:00", "17:30", 30.0, 9.0, 32.0, 34.94, "Submitted TS after trust cutoff. will be charged next week", 314.46, 26.46, "ID MED"], ["Patrick Gambold", "Isle of Wight", "Thursday", "2024-02-29", "08:00", "16:15", 30.0, 7.75, 32.0, 34.94, "Submitted TS after trust cutoff. will be charged next week", 270.79, 22.79, "ID MED"], ["Patrick Gambold", "Isle of Wight", "Friday", "2024-03-01", "08:00", "17:45", 30.0, 9.25, 32.0, 34.94, "Submitted TS after trust cutoff. will be charged next week", 323.2, 27.2, "ID MED"], ["Fanol Gjata", "Ramsay - North Downs", "Thursday", "2024-03-07", "07:30", "19:15", 30.0, 11.25, 42.5, 48.33, "Submitted after cutoff", 543.71, 65.59, "ETIPS"], ["Fanol Gjata", "Ramsay - North Downs", "Friday", "2024-03-08", "07:30", "19:00", 30.0, 11.0, 42.5, 48.33, "Submitted after cutoff", 531.63, 64.13, "ETIPS"], ["Fanol Gjata", "Ramsay - North Downs", "Saturday", "2023-03-09", "07:15", "21:00", 15.0, 13.5, 46.5, 48.64, "Submitted after cutoff", 656.64, 28.89, "ETIPS"], ["Consuelo Johnson", "Ramsay - Pinehill Hosp", "Wednesday", "2024-03-06", "08:00", "18:45", 30.0, 10.25, 42.0, 48.33, "Submitted after cutoff", 495.38, 64.88, "ETIPS"], ["Consuelo Johnson", "Ramsay - Pinehill Hosp", "Thursday", "2024-03-07", "08:00", "18:45", 30.0, 10.25, 42.0, 48.33, "Submitted after cutoff", 495.38, 64.88, "ETIPS"], ["Consuelo Johnson", "Ramsay - Pinehill Hosp", "Saturday", "2024-03-09", "08:15", "14:15", 0.0, 6.0, 42.0, 48.33, "Submitted after cutoff", 289.98, 37.98, "ETIPS"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Tuesday", "2024-03-05", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Shift was not sent on report - Candidate needs funds", 562.69, 87.69, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Wednesday", "2024-03-06", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Shift was not sent on report - Candidate needs funds", 562.69, 87.69, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Thursday", "2024-03-07", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Shift was not sent on report - Candidate needs funds", 562.69, 87.69, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Friday", "2024-03-08", "08:00", "18;00", 30.0, 9.5, 50.0, 59.23, "Shift was not sent on report - Candidate needs funds", 562.69, 87.69, "RETINUE"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Thursday", "2024-03-06", "08:00", "16:00", 30.0, 7.5, 50.0, 60.0, "TS submitted late - Needs funds", 450.0, 75.0, "ETIPS"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Thursday", "2024-03-12", "08:00", "17:15", 30.0, 8.75, 50.0, 60.0, "TS submitted late - Needs funds", 525.0, 87.5, "ETIPS"], ["Jovanie Santos", "Ramsay - North Downs", "Friday", "2024-03-22", "07:30", "18:00", 30.0, 10.0, 44.0, 48.33, "TS submitted late - Needs funds", 483.3, 43.3, "ETIPS"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Tuesday", "2024-03-12", "08:00", "18:45", 30.0, 10.25, 50.0, 59.23, "Candidiate needs funds for Bill - Shifts apporved on client portal", 607.11, 94.61, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Wednesday", "2024-03-13", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Candidiate needs funds for Bill - Shifts apporved on client portal", 562.69, 87.69, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Thursday", "2024-03-14", "08:00", "21:15", 30.0, 12.45, 50.0, 59.23, "Candidiate needs funds for Bill - Shifts apporved on client portal", 737.41, 114.91, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Friday", "2024-03-15", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Candidiate needs funds for Bill - Shifts apporved on client portal", 562.69, 87.69, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Thursday", "2024-03-21", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Shift Approved on Portal not on report - Candidiate needs funds", 562.69, 87.69, "RETINUE"], ["Mohammadreza Mohammadi", "Bristol & Weston", "Friday", "2024-03-22", "08:00", "18:00", 30.0, 9.5, 50.0, 59.23, "Shift Approved on Portal not on report - Candidiate needs funds", 562.69, 87.69, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Tuesday", "2024-03-19", "08:00", "21:00", 60.0, 12.0, 50.0, 59.23, "Shift Approved on Portal not on report - Candidiate needs funds", 710.76, 110.76, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2024-03-20", "08:00", "21:00", 60.0, 12.0, 50.0, 59.23, "Shift Approved on Portal not on report - Candidiate needs funds", 710.76, 110.76, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2024-03-21", "08:00", "21:00", 60.0, 12.0, 50.0, 59.23, "Shift Approved on Portal not on report - Candidiate needs funds", 710.76, 110.76, "RETINUE"], ["Rose Emmanuel", "Kings Oak", "Tuesday", "2024-03-26", "07:30", "18:00", 30.0, 10.0, 50.0, 55.0, "Consulant Request - Candidate needs funds", 550.0, 50.0, "RETINUE"], ["Rose Emmanuel", "Kings Oak", "Wednesday", "2024-03-27", "07:30", "15:30", 30.0, 7.5, 50.0, 55.0, "Consulant Request - Candidate needs funds", 412.5, 37.5, "RETINUE"], ["Mark Pablico", "Ramsay - North Downs", "Monday", "2024-03-25", "12:00", "19:00", 15.0, 6.75, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 341.55, 44.55, "ETIPS"], ["Mark Pablico", "Ramsay - North Downs", "Tuesday", "2024-03-26", "08:00", "18:45", 30.0, 9.75, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 493.35, 64.35, "ETIPS"], ["Mark Pablico", "Ramsay - North Downs", "Wednesday", "2024-03-27", "08:30", "20:15", 30.0, 11.25, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 569.25, 74.25, "ETIPS"], ["Mark Pablico", "Ramsay - North Downs", "Thursday", "2024-03-28", "07:45", "20:15", 30.0, 12.0, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 607.2, 79.2, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2024-03-25", "12:00", "19:00", 15.0, 6.75, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 341.55, 44.55, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2024-03-26", "07:30", "17:45", 30.0, 9.75, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 493.35, 64.35, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2024-03-27", "07:30", "19:00", 15.0, 11.25, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 569.25, 74.25, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2024-03-28", "07:30", "19:00", 30.0, 11.0, 44.0, 50.6, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 556.6, 72.6, "ETIPS"], ["Fanol Gjata", "Ramsay - North Downs", "Thursday", "2024-03-21", "07:30", "19:45", 30.0, 11.75, 42.5, 48.33, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 567.88, 68.5, "ETIPS"], ["Fanol Gjata", "Ramsay - North Downs", "Friday", "2024-03-22", "07:15", "16:30", 0.0, 9.25, 42.5, 48.33, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 447.05, 53.93, "ETIPS"], ["Fanol Gjata", "Ramsay - North Downs", "Monday", "2024-03-25", "12:00", "19:00", 0.0, 7.0, 42.5, 48.33, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 338.31, 40.81, "ETIPS"], ["Fanol Gjata", "Ramsay - North Downs", "Thursday", "2024-03-28", "07:30", "19:00", 30.0, 11.0, 42.5, 48.33, "Coud not add hours to Etips due to bank holiday cutoff issue. Hours have now been submitted", 531.63, 64.13, "ETIPS"], ["Rose Emmanuel", "The Chaucer Hospital", "Monday", "2024-03-25", "08:00", "17:00", 30.0, 8.5, 50.0, 55.0, "Consulant Request - Candidate needs funds", 467.5, 42.5, "RETINUE"], ["Rose Emmanuel", "The Chaucer Hospital", "Thursday", "2024-03-28", "08:00", "18:00", 30.0, 9.5, 50.0, 55.0, "Consulant Request - Candidate needs funds", 522.5, 47.5, "RETINUE"], ["Rose Emmanuel", "The Chaucer Hospital", "Tuesday", "2024-04-02", "08:00", "18:00", 30.0, 9.5, 50.0, 55.0, "Consulant Request - Candidate needs funds", 522.5, 47.5, "RETINUE"], ["Rose Emmanuel", "Kings Oak Hospital", "Thursday", "2023-04-04", "07:30", "20:00", 30.0, 12.0, 50.0, 55.0, "Consulant Request - Candidate needs funds", 660.0, 60.0, "BRIDGE"], ["Penelope Piccio", "Circle Reading", "Wednesday", "2024-03-20", "07:30", "18:00", 30.0, 10.0, 45.5, 55.09, "Shifts approved on the portal - did not appear on todays report - candidate needs funds", 550.9, 95.9, "BRIDGE"], ["Penelope Piccio", "Circle Reading", "Thursday", "2024-03-21", "07:30", "18:00", 30.0, 10.0, 45.5, 55.09, "Shifts approved on the portal - did not appear on todays report - candidate needs funds", 550.9, 95.9, "BRIDGE"], ["Penelope Piccio", "Circle Reading", "Saturday", "2024-03-23", "07:30", "17:00", 30.0, 9.0, 48.0, 62.13, "Shifts approved on the portal - did not appear on todays report - candidate needs funds", 559.17, 127.17, "BRIDGE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Monday", "2024-03-18", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Tuesday", "2024-03-19", "07:45", "20:00", 30.0, 11.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 699.13, 52.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Wednesday", "2024-03-20", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Thursday", "2024-03-21", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Friday", "2024-03-22", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Monday", "2024-03-25", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Tuesday", "2024-03-26", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Wednesday", "2024-03-27", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Lydie Gam-Mackitta", "Bristol & Western", "Thursday", "2024-03-28", "07:45", "18:00", 30.0, 9.75, 55.0, 59.5, "On Retinue but delayed by 2 weeks. all shift will come over tomorrow", 580.13, 43.88, "RETINUE"], ["Mark Anthony Pablico", "Ramsay North Downs", "Monday", "2024-04-08", "13:45", "20:15", 0.0, 6.5, 44.0, 50.6, "shifts not added to Etips in time", 328.9, 42.9, "ETIPS"], ["Mark Anthony Pablico", "Ramsay North Downs", "Thursday", "2024-04-11", "09:00", "20:15", 30.0, 10.75, 44.0, 50.6, "shifts not added to Etips in time", 543.95, 70.95, "ETIPS"], ["Mark Anthony Pablico", "Ramsay North Downs", "Saturday", "2024-04-13", "08:00", "13:45", 0.0, 4.75, 48.0, 54.27, "shifts not added to Etips in time", 257.78, 29.78, "ETIPS"], ["Sahana Aravind", "Bristol & Western", "Monday", "2024-04-08", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shift approved on Retinue too ate for this week", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Tuesday", "2024-04-09", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shift approved on Retinue too ate for this week", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Wednesday", "2024-04-10", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shift approved on Retinue too ate for this week", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Thursday", "2024-04-11", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shift approved on Retinue too ate for this week", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Friday", "2024-04-12", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shift approved on Retinue too ate for this week", 527.48, 39.98, "RETINUE"], ["Penelope Piccio", "Spire Dunedin", "Tuesday", "2024-04-09", "13:00", "18:00", 0.0, 5.5, 47.0, 54.52, "Shift Approved after cutoff", 299.86, 41.36, "RETINUE"], ["Penelope Piccio", "Spire Dunedin", "Saturday", "2024-04-13", "07:30", "18:00", 30.0, 10.0, 40.0, 46.95, "Shift Approved after cutoff", 469.5, 69.5, "RETINUE"], ["Penelope Piccio", "Circle Reading", "Saturday", "2024-04-20", "07:30", "16:00", 30.0, 8.0, 51.5, 62.13, "Shift Approved after cutoff", 497.04, 85.04, "RETINUE"], ["Rose Emmanuel", "Kings Oak Hospital", "Wednesday", "2024-04-24", "07:30", "19:30", 30.0, 11.5, 50.0, 55.0, "Shifts approved on portal canidate leaving for holiday today and needs funds", 632.5, 57.5, "BRIDGE"], ["Rose Emmanuel", "Kings Oak Hospital", "Thursday", "2024-04-25", "07:30", "20:30", 60.0, 12.0, 50.0, 55.0, "Shifts approved on portal canidate leaving for holiday today and needs funds", 660.0, 60.0, "BRIDGE"], ["Sahana Aravind", "Bristol & Western", "Friday", "2024-04-19", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shfts approved after payment cutoff. Candidate can't wait for friday", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Monday", "2024-04-22", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shfts approved after payment cutoff. Candidate can't wait for friday", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Tuesday", "2024-04-23", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shfts approved after payment cutoff. Candidate can't wait for friday", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Wednesday", "2024-04-24", "07:45", "19:30", 30.0, 11.25, 50.0, 54.1, "Shfts approved after payment cutoff. Candidate can't wait for friday", 608.63, 46.13, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "thursday", "2024-04-25", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shfts approved after payment cutoff. Candidate can't wait for friday", 527.48, 39.98, "RETINUE"], ["Sahana Aravind", "Bristol & Western", "Friday", "2024-04-26", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Shfts approved after payment cutoff. Candidate can't wait for friday", 527.48, 39.98, "RETINUE"], ["Mark Pablico", "North Downs Hospital", "Monday", "2024-05-13", "10:45", "20:00", 30.0, 8.75, 44.0, 50.6, "Recived timesheet after cutoff. Candidate needs funds", 442.75, 57.75, "ETIPS"], ["Patrick Gambold", "Isle of Wright", "Tuesday", "2024-05-07", "08:00", "17:00", 30.0, 8.5, 32.0, 34.94, "timesheet recived after cutoff. Will be on next week report", 296.99, 24.99, "CLAIRTY"], ["Patrick Gambold", "Isle of Wright", "Wednesday", "2024-05-08", "08:00", "17:45", 30.0, 9.25, 32.0, 34.94, "timesheet recived after cutoff. Will be on next week report", 323.2, 27.2, "CLAIRTY"], ["Patrick Gambold", "Isle of Wright", "Thursday", "2024-05-09", "08:00", "16:15", 30.0, 7.75, 32.0, 34.94, "timesheet recived after cutoff. Will be on next week report", 270.79, 22.79, "CLAIRTY"], ["Patrick Gambold", "Isle of Wright", "Friday", "2024-05-10", "08:00", "18:15", 30.0, 9.75, 32.0, 34.94, "timesheet recived after cutoff. Will be on next week report", 340.67, 28.67, "CLAIRTY"], ["Tamara Boswell", "Broomfield", "Wednesday", "2024-05-22", "08:00", "18:00", 30.0, 9.5, 35.0, 37.0, "Selfbook ticket was accidentally closed", 351.5, 19.0, "MSE"], ["Tamara Boswell", "Broomfield", "Thursday", "2024-05-23", "08:00", "18:00", 30.0, 9.5, 35.0, 37.0, "Selfbook ticket was accidentally closed", 351.5, 19.0, "MSE"], ["Sahana Aravind", "Bristol & Weston", "Friday", "2024-05-10", "07:45", "18:00", 30.0, 9.75, 46.0, 49.02, "Shifts Approved after cutoff period- Candidate is frustrtaed with waiting", 477.95, 29.45, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Tuesday", "2024-05-21", "08:00", "18:15", 30.0, 9.75, 45.0, 54.0, "Shifts all approved yesterday but needs money as it has been 3 weeks since last paid", 526.5, 87.75, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2024-05-22", "08:15", "18:00", 30.0, 9.5, 45.0, 54.0, "Shifts all approved yesterday but needs money as it has been 3 weeks since last paid", 513.0, 85.5, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2024-05-23", "08:00", "19:00", 30.0, 10.5, 45.0, 54.0, "Shifts all approved yesterday but needs money as it has been 3 weeks since last paid", 567.0, 94.5, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Tuesday", "2024-05-28", "08:00", "21:00", 60.0, 12.0, 45.0, 54.0, "Shifts all approved yesterday but needs money as it has been 3 weeks since last paid", 648.0, 108.0, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2024-05-29", "08:00", "19:00", 60.0, 10.0, 45.0, 54.0, "Shifts all approved yesterday but needs money as it has been 3 weeks since last paid", 540.0, 90.0, "RETINUE"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2024-05-30", "08:00", "19:00", 60.0, 10.0, 45.0, 54.0, "Shifts all approved yesterday but needs money as it has been 3 weeks since last paid", 540.0, 90.0, "RETINUE"], ["Paula Ballester", "Spire Wellesley", "Friday", "2024-06-07", "07:30", "19:30", 30.0, 11.5, 36.66, 44.85, "shift on approved on Bridge late", 515.78, 94.19, "BRIDGE"], ["Paula Ballester", "Spire Wellesley", "Wednesday", "2024-06-12", "07:30", "12:30", 30.0, 4.5, 36.66, 48.61, "shift on approved on Bridge late", 218.75, 53.78, "BRIDGE"], ["Rose Emmanuel", "The Kings Oak (Circle)", "Thursday", "2024-06-06", "12:30", "22:00", 30.0, 9.0, 50.0, 55.09, "Approved on Bridge", 495.81, 45.81, "CIRCLE"], ["Rose Emmanuel", "The Kings Oak (Circle)", "Friday", "2024-06-07", "07:30", "15:30", 0.0, 8.0, 50.0, 55.09, "Approved on Bridge", 440.72, 40.72, "CIRCLE"], ["Rose Emmanuel", "The Kings Oak (Circle)", "Monday", "2024-06-10", "13:00", "20:30", 0.0, 7.5, 50.0, 55.09, "Approved on Bridge", 413.18, 38.18, "CIRCLE"], ["Rose Emmanuel", "The Kings Oak (Circle)", "Thursday", "2024-06-13", "07:30", "19:30", 30.0, 11.5, 50.0, 55.09, "Approved on Bridge", 633.54, 58.54, "CIRCLE"], ["Stuart hicks", "St Mary's (Etips)", "Tuesday", "2024-05-14", "09:30", "17:15", 30.0, 7.25, 35.0, 38.95, "Candidates waited over a month for approval", 282.39, 28.64, "ETIPS"], ["Stuart hicks", "St Mary's (Etips)", "Wednesday", "2024-05-15", "07:30", "17:00", 30.0, 9.25, 35.0, 38.95, "Candidates waited over a month for approval", 360.29, 36.54, "ETIPS"], ["Stuart hicks", "St Mary's (Etips)", "Thursday", "2024-05-16", "07:30", "16:30", 30.0, 8.5, 35.0, 38.95, "Candidates waited over a month for approval", 331.08, 33.58, "ETIPS"], ["Stuart hicks", "St Mary's (Etips)", "Tuesday", "2024-05-21", "07:30", "16:30", 30.0, 8.5, 35.0, 38.95, "Candidates waited over a month for approval", 331.08, 33.58, "ETIPS"], ["Stuart hicks", "St Mary's (Etips)", "Wednesday", "2024-05-22", "07:30", "16:00", 30.0, 8.0, 35.0, 38.95, "Candidates waited over a month for approval", 311.6, 31.6, "ETIPS"], ["Iliyana Sokolova", "Spire Cambridge Lea Hospital", "Friday", "2024-06-14", "07:30", "16:45", 30.0, 8.75, 32.59, 44.41, "shift on approved on Bridge late", 388.59, 103.43, "BRIDGE"], ["Rogelio Jr Albano", "Nuffield - Bournemouth", "Monday", "2024-06-24", "07:00", "18:00", 30.0, 10.5, 37.5, 51.16, "Rejoined with DW & not aware of the new bookings - Trust added booking so it will be approved. Goiing forward he follow the new process", 537.18, 143.43, "ETIPS"], ["Rogelio Jr Albano", "Nuffield - Bournemouth", "Wednesday", "2024-06-26", "07:00", "20:00", 30.0, 12.5, 37.5, 51.16, "Rejoined with DW & not aware of the new bookings - Trust added booking so it will be approved. Goiing forward he follow the new process", 639.5, 170.75, "ETIPS"], ["Sahana Aravind", "Bristol & Western", "Monday", "2024-06-24", "07:45", "18:00", 30.0, 9.75, 42.0, 43.15, "Approved on Portal", 420.71, 11.21, "BRIDGE"], ["Sahana Aravind", "Bristol & Western", "Tuesday", "2024-06-25", "07:45", "18:00", 30.0, 9.75, 42.0, 43.15, "Approved on Portal", 420.71, 11.21, "BRIDGE"], ["Sahana Aravind", "Bristol & Western", "Wednesday", "2024-06-26", "07:45", "18:00", 30.0, 9.75, 42.0, 43.15, "Approved on Portal", 420.71, 11.21, "BRIDGE"], ["Sahana Aravind", "Bristol & Western", "thursday", "2024-06-27", "07:45", "18:00", 30.0, 9.75, 42.0, 43.15, "Approved on Portal", 420.71, 11.21, "BRIDGE"], ["Sahana Aravind", "Bristol & Western", "Friday", "2024-06-28", "07:45", "18:00", 30.0, 9.75, 42.0, 43.15, "Approved on Portal", 420.71, 11.21, "BRIDGE"], ["Penelope Piccio", "Circle - Reading", "Thursday", "2024-06-27", "07:30", "18:00", 30.0, 10.0, 45.5, 55.09, "Consualnt Request - Candiate has no money", 550.9, 95.9, "BRIDGE"], ["Penelope Piccio", "Circle - Reading", "Friday", "2024-06-28", "07:30", "17:00", 30.0, 9.0, 45.5, 55.09, "Consualnt Request - Candiate has no money", 495.81, 86.31, "BRIDGE"], ["Penelope Piccio", "Circle - Reading", "Tuesday", "2024-07-02", "07:30", "20:00", 30.0, 12.0, 45.5, 55.09, "Shift approved for 19/7/24 report", 661.08, 115.08, "BRIDGE"], ["Penelope Piccio", "Circle - Reading", "Thursday", "2024-07-04", "07:30", "17:30", 30.0, 9.5, 45.5, 55.09, "Shift approved for 19/7/24 report", 523.36, 91.11, "BRIDGE"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2024-07-09", "10:30", "20:00", 30.0, 9.0, 44.0, 50.6, "Consualnt Request - Candiate has no money", 455.4, 59.4, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2024-07-10", "07:30", "19:15", 30.0, 11.25, 44.0, 50.6, "Consualnt Request - Candiate has no money", 569.25, 74.25, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2024-07-11", "07:30", "20:00", 30.0, 12.0, 44.0, 50.6, "Consualnt Request - Candiate has no money", 607.2, 79.2, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2024-07-12", "07:30", "18:15", 15.0, 10.5, 44.0, 50.6, "Consualnt Request - Candiate has no money", 531.3, 69.3, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2024-07-13", "07:30", "15:00", 15.0, 7.25, 44.0, 50.6, "Consualnt Request - Candiate has no money", 366.85, 47.85, "ETIPS"], ["Sahana Aravind", "Bristol & Western", "Monday", "2024-05-03", "07:45", "18:00", 30.0, 9.75, 50.0, 54.1, "Approved over the weekend - To be charged friday", 527.48, 39.98, "RETINUE"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2024-07-27", "07:30", "16:00", 30.0, 8.25, 48.0, 54.27, "Shift not included on this weeks selfbill - to be charged next week", 447.73, 51.73, "ETIPS"], ["Penelope Piccio", "Circle - Reading", "Friday", "2024-07-19", "07:30", "14:00", 0.0, 6.5, 45.5, 55.09, "Both timesheets approved after cutoff - Will be charged next week", 358.09, 62.34, "BRIDGE"], ["Penelope Piccio", "Circle - Reading", "Monday", "2024-07-22", "07:30", "19:30", 30.0, 11.5, 45.5, 55.09, "Both timesheets approved after cutoff - Will be charged next week", 633.54, 110.29, "BRIDGE"], ["Penelope Piccio", "Circle - Reading", "Thursday", "2024-07-25", "07:30", "18:00", 30.0, 10.0, 45.5, 55.09, "Both timesheets approved after cutoff - Will be charged next week", 550.9, 95.9, "BRIDGE"], ["Angelo Salomeo", "Ramsay - North Downs", "Wednesday", "2024-07-31", "08:15", "12:45", 0.0, 4.5, 46.0, 60.0, "Timesheet was not submitted - Will be on next week", 270.0, 63.0, "ETIPS"], ["Angelo Salomeo", "Ramsay - North Downs", "Saturday", "2024-08-03", "09:00", "17:30", 0.0, 8.5, 50.0, 65.0, "Timesheet was not submitted - Will be on next week", 552.5, 127.5, "ETIPS"], ["Patrick Gambold", "Isle of Wight", "Monday", "2024-07-29", "08:00", "17:30", 30.0, 9.0, 32.0, 34.94, "Approval late on client portal - On next weeks report", 314.46, 26.46, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Thursday", "2024-08-01", "08:00", "17:15", 30.0, 8.75, 32.0, 34.94, "Approval late on client portal - On next weeks report", 305.73, 25.73, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Friday", "2024-08-02", "08:00", "18:00", 30.0, 9.5, 32.0, 34.94, "Approval late on client portal - On next weeks report", 331.93, 27.93, "Clarity"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2024-08-08", "20:00", "08:00", 0.0, 1.0, 45.0, 50.0, "On Call Job Type was approved after TS cutoff", 50.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2024-08-10", "20:00", "08:00", 0.0, 1.0, 45.0, 50.0, "On Call Job Type was approved after TS cutoff", 50.0, 5.0, "ETIPS"], ["Diosdado Wagan", "Ramsay - North Downs", "Sunday", "2024-08-11", "08:00", "20:00", 0.0, 1.0, 45.0, 50.0, "On Call Job Type was approved after TS cutoff", 50.0, 5.0, "ETIPS"], ["Louisa Boateng", "Ramsay - Oaks Hospital", "Monday", "2024-08-05", "08:00", "17:30", 30.0, 9.0, 50.0, 60.0, "Submitted after cutoff", 540.0, 90.0, "ETIPS"], ["Louisa Boateng", "Ramsay - Oaks Hospital", "Tuesday", "2024-08-06", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Submitted after cutoff", 600.0, 100.0, "ETIPS"], ["Louisa Boateng", "Ramsay - Oaks Hospital", "Wednesday", "2024-08-07", "08:00", "19:00", 30.0, 10.5, 50.0, 60.0, "Submitted after cutoff", 630.0, 105.0, "ETIPS"], ["Louisa Boateng", "Ramsay - Oaks Hospital", "Thursday", "2024-08-08", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Submitted after cutoff", 570.0, 95.0, "ETIPS"], ["Louisa Boateng", "Ramsay - Oaks Hospital", "Saturday", "2024-08-10", "08:00", "18:00", 30.0, 9.5, 55.0, 65.0, "Submitted after cutoff", 617.5, 95.0, "ETIPS"], ["Patrick Gambold", "Isle of Wight", "Tuesday", "2024-08-06", "08:00", "12:45", 0.0, 4.75, 32.0, 34.94, "Approved after cutoff", 165.97, 13.97, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Thursday", "2024-08-08", "08:00", "17:45", 30.0, 9.25, 32.0, 34.94, "Approved after cutoff", 323.2, 27.2, "Clarity"], ["Patrick Gambold", "Isle of Wight", "Friday", "2024-08-09", "08:00", "11:45", 0.0, 3.75, 32.0, 34.94, "Approved after cutoff", 131.03, 11.03, "Clarity"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2024-07-17", "08:00", "18:00", 30.0, 9.5, 40.0, 44.0, "Approved after cutoff", 418.0, 38.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2024-07-18", "08:00", "18:00", 30.0, 9.5, 40.0, 44.0, "Approved after cutoff", 418.0, 38.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Tuesday", "2024-07-23", "08:00", "18:00", 30.0, 9.5, 40.0, 44.0, "Approved after cutoff", 418.0, 38.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2024-07-24", "08:00", "18:00", 30.0, 9.5, 40.0, 44.0, "Approved after cutoff", 418.0, 38.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2024-07-25", "08:00", "19:00", 60.0, 10.0, 40.0, 44.0, "Approved after cutoff", 440.0, 40.0, "Retinue"], ["Penelope Piccio", "Spire - Dunedin", "Tuesday", "2024-08-06", "07:30", "18:00", 30.0, 10.0, 38.5, 48.41, "Approved after cutoff", 484.1, 99.1, "Bridge"], ["Penelope Piccio", "Spire - Dunedin", "Friday", "2024-08-09", "07:30", "18:00", 30.0, 10.0, 36.0, 44.85, "Approved after cutoff", 448.5, 88.5, "Bridge"], ["Paul Harris", "Spire - Gatwick Park", "Monday", "2024-08-05", "07:30", "19:00", 30.0, 11.0, 40.0, 48.0, "Consultants Request - Candidate needs to be paid", 528.0, 88.0, "Bridge"], ["Tamara Boswell", "Lewisham", "Monday", "2024-08-19", "08:00", "18:00", 30.0, 9.5, 28.0, 32.0, "Candidate needs funds", 304.0, 38.0, "HROSTER"], ["Tamara Boswell", "Lewisham", "Wednesday", "2024-08-21", "08:00", "18:00", 30.0, 9.5, 28.0, 32.0, "Candidate needs funds", 304.0, 38.0, "HROSTER"], ["Tamara Boswell", "QEH", "Tuesday", "2024-08-20", "08:00", "18:00", 30.0, 9.5, 28.0, 32.0, "Candidate needs funds", 304.0, 38.0, "HROSTER"], ["Tamara Boswell", "Lewisham", "Friday", "2024-08-23", "08:00", "18:00", 30.0, 9.5, 28.0, 32.0, "Candidate needs funds", 304.0, 38.0, "HROSTER"], ["Tamara Boswell", "QEH", "Tuesday", "2024-08-27", "08:00", "18:00", 30.0, 9.5, 28.0, 32.0, "Candidate needs funds", 304.0, 38.0, "HROSTER"], ["Patrick Gambold", "Isle Of Wight", "Monday", "2024-08-19", "08:00", "16:45", 30.0, 8.25, 32.0, 34.94, "Approved after cutoff", 288.26, 24.26, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Tuesday", "2024-08-20", "08:00", "17:00", 30.0, 8.5, 32.0, 34.94, "Approved after cutoff", 296.99, 24.99, "Clarity"], ["Patrick Gambold", "Isle Of Wight", "Thursday", "2024-08-22", "08:00", "18:00", 0.0, 5.0, 32.0, 34.94, "Approved after cutoff", 174.7, 14.7, "Clarity"], ["Paula Ibanez", "Spire - Wellesley", "Wednesday", "2024-08-14", "07:30", "17:00", 30.0, 9.0, 36.66, 40.3, "Approved after cutoff", 362.7, 32.76, "BRIDGE"], ["Lauren Orgar", "Ramsay - Berkshire", "Monday", "2024-08-19", "07:30", "17:30", 30.0, 9.5, 33.0, 38.71, "Approved after cutoff", 367.75, 54.25, "ETIPS"], ["Zoe Hodge", "Watford General Hospital", "Thursday", "2024-08-22", "14:00", "20:00", 0.0, 6.0, 29.0, 31.17, "Candidate needs funds, will be invoiced next week", 187.02, 13.02, "NHSP"], ["Rinah BHEEKHARRY", "Ramsay - Cherwell", "Monday", "2024-09-02", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Timesheet Submitted after client cutoff", 570.0, 95.0, "ETIPS"], ["Rinah BHEEKHARRY", "Ramsay - Cherwell", "Thursday", "2024-09-05", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Timesheet Submitted after client cutoff", 570.0, 95.0, "ETIPS"], ["Rinah BHEEKHARRY", "Ramsay - Cherwell", "Friday", "2024-09-06", "08:00", "16:15", 30.0, 7.75, 50.0, 60.0, "Timesheet Submitted after client cutoff", 465.0, 77.5, "ETIPS"], ["Maria Castro", "Nuffield - Wessex", "Tuesday", "2024-09-10", "07:30", "19:30", 30.0, 11.5, 45.0, 48.58, "Submitted on time - Error on Etips side. Will be on Next week report", 558.67, 41.17, "ETIPS"], ["Maria Castro", "Nuffield - Wessex", "Wednesday", "2024-09-11", "07:30", "17:00", 30.0, 9.0, 45.0, 48.58, "Submitted on time - Error on Etips side. Will be on Next week report", 437.22, 32.22, "ETIPS"], ["Maria Castro", "Nuffield - Wessex", "Friday", "2024-09-13", "07:30", "17:30", 30.0, 9.5, 45.0, 48.58, "Submitted on time - Error on Etips side. Will be on Next week report", 461.51, 34.01, "ETIPS"], ["Patrick Gambold", "Isle of Wight", "Monday", "2024-09-09", "08:00", "15:30", 30.0, 7.0, 32.0, 34.94, "Error with Approval, Will be on this weekes report", 244.58, 20.58, "Clarity"], ["Amara Anadu", "Spire - Dunedin", "Wednesday", "2024-09-11", "12:15", "18:45", 0.0, 6.5, 38.0, 48.78, "Approved after cutoff, will be on Firdays report", 317.07, 70.07, "SPIRE"], ["Amara Anadu", "Spire - Portsmorth", "Friday", "2024-09-13", "08:15", "20:00", 30.0, 11.25, 38.0, 49.51, "Approved after cutoff, will be on Firdays report", 556.99, 129.49, "SPIRE"], ["Roseline Emmanuel", "Medway", "Monday", "2024-09-23", "08:00", "18:00", 30.0, 9.5, 30.0, 32.0, "Candiate going away for a few weeks and will need funds", 304.0, 19.0, "HROSTER"], ["Roseline Emmanuel", "Medway", "Tuesday", "2024-09-24", "08:00", "18:30", 30.0, 10.0, 30.0, 32.0, "Candiate going away for a few weeks and will need funds", 320.0, 20.0, "HROSTER"], ["Roseline Emmanuel", "Medway", "Wednesday", "2024-09-25", "08:00", "18:45", 30.0, 10.25, 30.0, 32.0, "Candiate going away for a few weeks and will need funds", 328.0, 20.5, "HROSTER"], ["Amara Anadu", "Circle - Mt Alvernia", "Wednesday", "2024-09-18", "08:00", "17:30", 30.0, 9.0, 32.0, 54.0, "Approved after cutoff, has bills going out tonight", 486.0, 198.0, "CIRCLE"], ["Amara Anadu", "Circle - Reading", "Thursday", "2024-09-19", "08:00", "20:00", 30.0, 12.0, 32.0, 42.0, "Approved after cutoff, has bills going out tonight", 504.0, 120.0, "CIRCLE"], ["Patrick Gambold", "Isle of Wight", "Monday", "2024-09-23", "08:00", "14:45", 30.0, 6.25, 32.0, 34.94, "Approved after cutoff", 218.38, 18.38, "Clarity"], ["Maria Castro", "Nuffield - Wessex", "Monday", "2024-09-30", "07:30", "21:00", 60.0, 12.5, 45.0, 48.58, "Did not appear on this weeks self-bill. Will be charged next week", 607.25, 44.75, "Etips"], ["Maria Castro", "Nuffield - Wessex", "Tuesday", "2024-10-01", "07:30", "19:00", 30.0, 11.0, 45.0, 48.58, "Did not appear on this weeks self-bill. Will be charged next week", 534.38, 39.38, "Etips"], ["Maria Castro", "Nuffield - Wessex", "Wednesday", "2024-10-02", "07:30", "18:00", 30.0, 10.0, 45.0, 48.58, "Did not appear on this weeks self-bill. Will be charged next week", 485.8, 35.8, "Etips"], ["Maria Castro", "Nuffield - Wessex", "Thursday", "2024-10-03", "07:30", "18:00", 30.0, 10.0, 45.0, 48.58, "Did not appear on this weeks self-bill. Will be charged next week", 485.8, 35.8, "Etips"], ["Maria Castro", "Nuffield - Wessex", "Friday", "2024-10-04", "07:30", "15:45", 30.0, 7.75, 45.0, 48.58, "Did not appear on this weeks self-bill. Will be charged next week", 376.5, 27.75, "Etips"], ["Swapna Fernadez", "Cardiff & Vale", "Monday", "2024-09-30", "07:30", "18:00", 30.0, 10.0, 34.0, 37.46, "bank manager is adding shifts onto the report, but they threated to take us to the framework for not paying the candidate 4", 374.6, 34.6, "SelfBill"], ["Swapna Fernadez", "Cardiff & Vale", "Tuesday", "2024-10-01", "07:30", "18:00", 30.0, 10.0, 34.0, 37.46, "bank manager is adding shifts onto the report, but they threated to take us to the framework for not paying the candidate 4", 374.6, 34.6, "SelfBill"], ["Swapna Fernadez", "Cardiff & Vale", "Wednesday", "2024-10-02", "07:30", "16:30", 30.0, 7.5, 34.0, 37.46, "bank manager is adding shifts onto the report, but they threated to take us to the framework for not paying the candidate 4", 280.95, 25.95, "SelfBill"], ["Swapna Fernadez", "Cardiff & Vale", "Thursday", "2024-10-03", "07:30", "17:00", 30.0, 9.0, 34.0, 37.46, "bank manager is adding shifts onto the report, but they threated to take us to the framework for not paying the candidate 4", 337.14, 31.14, "SelfBill"], ["Consuelo Johnson", "Ramsay Pinehill", "Friday", "2024-10-25", "08:00", "18:00", 30.0, 9.5, 42.0, 48.33, "Shift hours were adjusted on Etips -awaiting the Etips report for payment next week", 459.14, 60.14, "Etips"], ["Penelope Piccio", "Nuffield - Oxford", "Monday", "2024-10-28", "08:00", "17:00", 30.0, 8.5, 41.5, 51.13, "Approved after cutoff", 434.61, 81.86, "Etips"], ["Paula Ibanez", "Spire - Wellesley", "Tuesday", "2024-10-22", "07:30", "13:30", 0.0, 6.0, 36.66, 40.3, "Approved After cutoff funds will be on next weeks report", 241.8, 21.84, "Bridge"], ["Paula Ibanez", "Spire - Wellesley", "Thursday", "2024-10-31", "07:30", "17:30", 30.0, 9.0, 36.66, 40.3, "Approved After cutoff funds will be on next weeks report", 362.7, 32.76, "Bridge"], ["Edward Brooks", "UCLH", "Tuesday", "2024-11-05", "08:00", "18:00", 30.0, 9.5, 30.0, 33.87, "Approved on HR - Will charged", 321.77, 36.77, "Bank Partners"], ["Edward Brooks", "UCLH", "Wednesday", "2024-11-06", "08:00", "16:00", 30.0, 7.5, 30.0, 33.87, "Approved on HR - Will charged", 254.03, 29.03, "Bank Partners"], ["Edward Brooks", "UCLH", "Thursday", "2024-11-07", "08:00", "18:00", 30.0, 9.5, 30.0, 33.87, "Approved on HR - Will charged", 321.77, 36.77, "Bank Partners"], ["Consuelo Johnson", "Ramsay - Pinehill", "Tuesday", "2024-11-05", "12:00", "16:00", 0.0, 4.0, 42.0, 47.55, "Job not on Retinue Portal", 190.2, 22.2, "Bridge"], ["Consuelo Johnson", "Ramsay - Pinehill", "Thursday", "2024-11-07", "08:00", "18:00", 30.0, 9.5, 42.0, 47.55, "Job not on Retinue Portal", 451.73, 52.73, "Bridge"], ["Consuelo Johnson", "Ramsay - Pinehill", "Friday", "2024-11-08", "08:00", "16:30", 30.0, 8.0, 42.0, 47.55, "Job not on Retinue Portal", 380.4, 44.4, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Thursday", "2024-11-07", "12:30", "18:15", 0.0, 5.75, 44.0, 48.33, "Paid Etips yesterday", 277.9, 24.9, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Friday", "2024-11-08", "08:00", "18:00", 30.0, 9.5, 44.0, 48.33, "Paid Etips yesterday", 459.14, 41.14, "Bridge"], ["Sandra Duarte-Botello", "Ramsay Cherwell", "Monday", "2024-11-04", "08:00", "16:45", 30.0, 8.25, 55.0, 60.0, "Approved on Portal, Candidate needs funds asap", 495.0, 41.25, "Bridge"], ["Sandra Duarte-Botello", "Ramsay Cherwell", "Tuesday", "2024-11-05", "08:00", "17:15", 30.0, 8.75, 55.0, 60.0, "Approved on Portal, Candidate needs funds asap", 525.0, 43.75, "Bridge"], ["Sandra Duarte-Botello", "Ramsay Cherwell", "Wednesday", "2024-11-06", "08:00", "16:30", 30.0, 8.0, 55.0, 60.0, "Approved on Portal, Candidate needs funds asap", 480.0, 40.0, "Bridge"], ["Sandra Duarte-Botello", "Ramsay Cherwell", "Thursday", "2024-11-07", "08:00", "18:00", 30.0, 9.5, 55.0, 60.0, "Approved on Portal, Candidate needs funds asap", 570.0, 47.5, "Bridge"], ["Josiah Nybango", "East & North Hertfordshire", "Friday", "2024-11-01", "08:00", "18:00", 30.0, 9.5, 24.0, 28.0, "On previous report, unable to pay via selfbill RWH-565847). Rates will be rectified next week", 266.0, 38.0, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Monday", "2024-11-04", "08:00", "18:15", 30.0, 9.75, 24.0, 28.0, "On previous report, unable to pay via selfbill RWH-565847). Rates will be rectified next week", 273.0, 39.0, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Tuesday", "2024-11-05", "08:00", "18:00", 30.0, 9.5, 24.0, 28.0, "On previous report, unable to pay via selfbill RWH-565847). Rates will be rectified next week", 266.0, 38.0, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Wednesday", "2024-11-06", "08:00", "18:00", 30.0, 9.5, 24.0, 28.0, "On previous report, unable to pay via selfbill RWH-565847). Rates will be rectified next week", 266.0, 38.0, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Thursday", "2024-11-07", "08:00", "21:00", 30.0, 12.5, 24.0, 28.0, "On previous report, unable to pay via selfbill RWH-565847). Rates will be rectified next week", 350.0, 50.0, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Friday", "2024-11-08", "08:00", "17:15", 30.0, 8.75, 24.0, 28.0, "On previous report, unable to pay via selfbill RWH-565847). Rates will be rectified next week", 245.0, 35.0, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Wednesday", "2024-11-06", "07:30", "17:30", 30.0, 9.5, 30.0, 34.0, "Authorised/Released, Charge will come through on Monday", 323.0, 38.0, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Thursday", "2024-11-07", "07:30", "17:30", 30.0, 9.5, 30.0, 34.0, "Authorised/Released, Charge will come through on Monday", 323.0, 38.0, "NHSP"], ["Martin Rowan", "Royal Berkshire", "Friday", "2024-11-08", "07:30", "18:00", 30.0, 9.5, 30.0, 34.0, "Authorised/Released, Charge will come through on Monday", 323.0, 38.0, "NHSP"], ["Hellen Chipudhla", "Lloyds Clinical", "Monday", "2024-11-18", "10:00", "19:00", 0.0, 9.0, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 630.0, 180.0, "Neuven"], ["Hellen Chipudhla", "Lloyds Clinical", "Tuesday", "2024-11-19", "07:30", "16:15", 0.0, 7.75, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 542.5, 155.0, "Neuven"], ["Hellen Chipudhla", "Lloyds Clinical", "Wednesday", "2024-11-20", "09:30", "19:00", 0.0, 8.5, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 595.0, 170.0, "Neuven"], ["Hellen Chipudhla", "Lloyds Clinical", "Thursday", "2024-11-21", "07:30", "18:00", 30.0, 10.0, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 700.0, 200.0, "Neuven"], ["Hellen Chipudhla", "Lloyds Clinical", "Friday", "2024-11-22", "10:00", "18:45", 0.0, 8.75, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 612.5, 175.0, "Neuven"], ["Virginia Ego Amechi", "Lloyds Clinical", "Wednesday", "2024-11-20", "07:00", "17:00", 0, 10.0, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 700.0, 200.0, "Neuven"], ["Virginia Ego Amechi", "Lloyds Clinical", "Thursday", "2024-11-21", "07:45", "15:45", 0, 8.0, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 560.0, 160.0, "Neuven"], ["Virginia Ego Amechi", "Lloyds Clinical", "Friday", "2024-11-22", "07:00", "17:00", 0, 10.0, 50.0, 70.0, "IT issues with Lloyds meant they sent timesheets in 1 day late", 700.0, 200.0, "Neuven"], ["Leonida White", "Cardiff & Vale", "Monday", "2024-09-30", "07:30", "19:30", 30.0, 11.5, 30.0, 37.0, "shift not appeared on self bill yet, should come over next week. candidate has threated leagal action if not paid today", 425.5, 80.5, ""], ["Angelo Salomeo", "North Downs", "Wednesday", "2024-11-20", "07:30", "12:30", 0.0, 5.0, 46.0, 60.0, "Approved on Portal, Needs to money for Bills", 300.0, 70.0, "Bridge"], ["Angelo Salomeo", "North Downs", "Thursday", "2024-11-21", "08:00", "13:30", 0.0, 5.5, 46.0, 60.0, "Approved on Portal, Needs to money for Bills", 330.0, 77.0, "Bridge"], ["Diosdado Wagan", "North Downs", "Monday", "2024-11-18", "09:00", "16:00", 30.0, 6.5, 40.0, 43.46, "Department not authorising shift on time", 282.49, 22.49, "Bridge"], ["Diosdado Wagan", "North Downs", "Tuesday", "2024-11-19", "07:30", "17:15", 15.0, 9.5, 40.0, 43.46, "Department not authorising shift on time", 412.87, 32.87, "Bridge"], ["Diosdado Wagan", "North Downs", "Thursday", "2024-11-21", "07:30", "17:30", 30.0, 9.5, 44.0, 49.29, "Department not authorising shift on time", 468.26, 50.26, "Bridge"], ["Diosdado Wagan", "North Downs", "Friday", "2024-11-22", "08:00", "20:30", 30.0, 12.0, 44.0, 49.29, "Department not authorising shift on time", 591.48, 63.48, "Bridge"], ["Diosdado Wagan", "North Downs", "Monday", "2024-11-25", "08:30", "19:00", 30.0, 10.0, 40.0, 43.46, "Department not authorising shift on time", 434.6, 34.6, "Bridge"], ["Diosdado Wagan", "North Downs", "Tuesday", "2024-11-26", "09:00", "21:00", 30.0, 11.5, 44.0, 49.29, "Department not authorising shift on time", 566.84, 60.84, "Bridge"], ["Diosdado Wagan", "North Downs", "Thursday", "2024-11-28", "07:30", "17:00", 30.0, 9.0, 44.0, 49.29, "Department not authorising shift on time", 443.61, 47.61, "Bridge"], ["Diosdado Wagan", "North Downs", "Saturday", "2024-11-30", "07:30", "18:30", 15.0, 10.75, 44.0, 49.29, "Department not authorising shift on time", 529.87, 56.87, "Bridge"], ["Shauna Henderson-Rose", "Rivers Hospital", "Tuesday", "2024-11-12", "08:00", "17:30", 30.0, 9.0, 50.0, 60.0, "Department not authorising shift on time", 540.0, 90.0, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Monday", "2024-12-02", "07:30", "19:00", 30.0, 11.0, 45.5, 55.09, "Shifts Approved after cutoff - Will be charged next week", 605.99, 105.49, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Tuesday", "2024-12-03", "07:30", "19:00", 30.0, 11.0, 45.5, 55.09, "Shifts Approved after cutoff - Will be charged next week", 605.99, 105.49, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Wednesday", "2024-12-04", "07:30", "18:30", 30.0, 10.5, 45.5, 55.09, "Shifts Approved after cutoff - Will be charged next week", 578.45, 100.7, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Thursday", "2024-12-05", "07:30", "17:00", 30.0, 9.0, 45.5, 55.09, "Shifts Approved after cutoff - Will be charged next week", 495.81, 86.31, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Saturday", "2024-12-07", "07:30", "15:00", 30.0, 7.0, 51.5, 65.19, "Shifts Approved after cutoff - Will be charged next week", 456.33, 95.83, "Bridge"], ["Tamra Boswell", "Broomfield", "Wednesday", "2024-12-11", "08:00", "18:00", 30.0, 9.5, 30.0, 36.0, "Staffbank had issues with the rate card. Sent over low charge. MSE are workign on a resloution now for the next report", 342.0, 57.0, "Litmus"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Monday", "2024-12-02", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and Reissue on LW report, Pay was not issued", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Tuesday", "2024-12-03", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and Reissue on LW report, Pay was not issued", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Wednesday", "2024-12-04", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and Reissue on LW report, Pay was not issued", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Thursday", "2024-12-05", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and Reissue on LW report, Pay was not issued", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Friday", "2024-12-06", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and Reissue on LW report, Pay was not issued", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Monday", "2024-12-09", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and reissue will be on this weeks report, approval below. Needs money today", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Tuesday", "2024-12-10", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and reissue will be on this weeks report, approval below. Needs money today", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Wednesday", "2024-12-11", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and reissue will be on this weeks report, approval below. Needs money today", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Thursday", "2024-12-12", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and reissue will be on this weeks report, approval below. Needs money today", 412.33, 71.08, "Retinue"], ["Lydie Gam-Mackitta", "Bristol & Weston", "Friday", "2024-12-13", "07:45", "18:00", 30.0, 9.75, 35.0, 42.29, "Credit and reissue will be on this weeks report, approval below. Needs money today", 412.33, 71.08, "Retinue"], ["Shauna Henderson-Rose", "Ramsay Rivers", "Tuesday", "2024-11-12", "08:00", "17:30", 30.0, 9.0, 50.0, 59.99, "Candidate has been waiting over a month for payment. Approved for this weeks self-bill", 539.91, 89.91, "Bridge"], ["Shuana Henderson-Rose", "Ramsay Rivers", "Tuesday", "2024-11-19", "08:00", "16:00", 30.0, 7.5, 50.0, 59.99, "Candidate has been waiting over a month for payment. Approved for this weeks self-bill", 449.93, 74.93, "Bridge"], ["Oana Tilvic", "Litmus MSE - Basildon", "Monday", "2024-12-16", "08:00", "17:00", 30.0, 8.5, 30.0, 36.13, "Outstaningin for almost a month, will be on this weeks selfbill - confimred by litmus", 307.11, 52.11, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Tuesday", "2024-12-17", "08:00", "19:00", 30.0, 10.5, 30.0, 36.13, "Outstaningin for almost a month, will be on this weeks selfbill - confimred by litmus", 379.37, 64.37, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Saturday", "2024-12-28", "08:00", "16:00", 30.0, 7.5, 35.0, 36.13, "Outstaningin for almost a month, will be on this weeks selfbill - confimred by litmus", 270.98, 8.48, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Thursday", "2024-12-12", "07:30", "18:00", 30.0, 10.0, 40.0, 44.05, "Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 440.5, 40.5, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Friday", "2024-12-13", "07:30", "18:00", 30.0, 10.0, 40.0, 44.05, "Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 440.5, 40.5, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Monday", "2024-12-16", "07:30", "18:00", 30.0, 10.0, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 440.5, 40.5, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Tuesday", "2024-12-17", "07:30", "18:00", 30.0, 10.0, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 440.5, 40.5, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Wednesday", "2024-12-18", "07:30", "13:00", 0.0, 5.5, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 242.28, 22.28, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Thursday", "2024-12-19", "07:30", "13:00", 0.0, 5.5, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 242.28, 22.28, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Friday", "2024-12-20", "11:00", "18:00", 0.0, 7.0, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 308.35, 28.35, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Tuesday", "2024-12-24", "11:00", "18:00", 0.0, 7.0, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 308.35, 28.35, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Friday", "2024-12-31", "08:00", "15:00", 0.0, 7.0, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 308.35, 28.35, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Sunday", "2025-01-02", "11:00", "18:00", 0.0, 7.0, 40.0, 44.05, "Josh will speak to Graham about this - Outstanding for almost a month, will be on this weeks selfbill - confirmed by litmus", 308.35, 28.35, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Tuesday", "2024-12-31", "08:00", "00:00", 30.0, 9.5, 30.0, 36.13, "Consualnt Request, Finalized on HR WIll be on a SB", 343.24, 58.24, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Thursday", "2024-12-19", "08:00", "18:00", 30.0, 9.5, 30.0, 36.13, "Consultant Request, Shifts on yesterdays report. Unable to pay. Josh Queried with releanvt teams for an amendemtn please pay today", 343.24, 58.24, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Friday", "2024-12-20", "08:00", "18:00", 30.0, 9.5, 30.0, 36.13, "Consultant Request, Shifts on yesterdays report. Unable to pay. Josh Queried with releanvt teams for an amendemtn please pay today", 343.24, 58.24, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Thursday", "2025-01-02", "08:00", "18:00", 30.0, 9.5, 30.0, 36.13, "Consultant Request, Shifts on yesterdays report. Unable to pay. Josh Queried with releanvt teams for an amendemtn please pay today", 343.24, 58.24, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Saturday", "2025-01-04", "09:00", "18:30", 30.0, 10.0, 35.0, 36.13, "Consultant Request, Shifts on yesterdays report. Unable to pay. Josh Queried with releanvt teams for an amendemtn please pay today", 361.3, 11.3, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Tuesday", "2025-01-05", "08:00", "18:00", 30.0, 9.5, 35.0, 36.13, "Approved on client Portal - Candidate needs funds", 343.24, 10.74, "Litmus"], ["Penelope Piccio", "Circle - Reading", "Saturday", "2025-01-11", "07:30", "18:30", 30.0, 10.5, 51.5, 67.11, "Approved after cutoff - canidate needs the funds today", 704.66, 163.91, "Circle"], ["Simba Makaru", "Litmus MSE - Basildon", "Monday", "2024-01-06", "08:00", "20:00", 60.0, 11.0, 30.0, 30.69, "Charge came across as incorrect, canaidate hasnt worked for months and needs money asap", 337.59, 7.59, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Tuesday", "2025-01-07", "08:00", "17:30", 30.0, 9.0, 30.0, 30.69, "Charge came across as incorrect, canaidate hasnt worked for months and needs money asap", 276.21, 6.21, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Wednesday", "2025-01-08", "08:30", "22:00", 30.0, 11.0, 30.0, 30.69, "Charge came across as incorrect, canaidate hasnt worked for months and needs money asap", 337.59, 7.59, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Thursday", "2025-01-09", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "Charge came across as incorrect, canaidate hasnt worked for months and needs money asap", 291.56, 6.56, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Friday", "2025-01-10", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "Charge came across as incorrect, canaidate hasnt worked for months and needs money asap", 291.56, 6.56, "Litmus"], ["Will Mandaza", "Litmus MSE - Broomfield", "Wednesday", "2025-01-08", "07:45", "18:00", 30.0, 9.75, 30.0, 30.69, "Candidate needs funds is unable to pay for bills", 299.23, 6.73, "Litmus"], ["Will Mandaza", "Litmus MSE - Broomfield", "Thursday", "2025-01-09", "07:45", "19:00", 30.0, 10.75, 30.0, 30.69, "Candidate needs funds is unable to pay for bills", 329.92, 7.42, "Litmus"], ["Will Mandaza", "Litmus MSE - Broomfield", "Tuesday", "2025-01-14", "07:45", "18:00", 30.0, 9.75, 27.0, 30.69, "Candidate needs funds is unable to pay for bills", 299.23, 35.98, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Saturday", "2025-01-11", "08:00", "19:30", 30.0, 11.0, 27.0, 30.69, "New MSE Process - Outstanding Payment", 337.59, 40.59, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Monday", "2025-01-13", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 35.06, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Tuesday", "2025-01-14", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 35.06, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Wednesday", "2025-01-15", "08:00", "19:00", 30.0, 10.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 322.25, 38.75, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Thursday", "2025-01-16", "13:00", "18:30", 0.0, 5.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 168.8, 20.3, "Litmus"], ["Simba Makaru", "Litmus MSE - Basildon", "Friday", "2025-01-17", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 35.06, "Litmus"], ["Comfort Raji", "Litmus MSE - Basildon", "Saturday", "2024-12-14", "08:00", "18:00", 30.0, 9.5, 35.0, 37.0, "New MSE Process - Outstanding Payment", 351.5, 19.0, "Litmus"], ["Comfort Raji", "Litmus MSE - Basildon", "Tuesday", "2024-12-17", "08:00", "18:00", 30.0, 9.5, 35.0, 37.0, "New MSE Process - Outstanding Payment", 351.5, 19.0, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Monday", "2025-01-06", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 6.56, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Tuesday", "2025-01-07", "08:00", "17:30", 30.0, 9.0, 30.0, 30.69, "New MSE Process - Outstanding Payment", 276.21, 6.21, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Wednesday", "2025-01-08", "08:00", "18:30", 30.0, 10.0, 30.0, 30.69, "New MSE Process - Outstanding Payment", 306.9, 6.9, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Thursday", "2025-01-09", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 6.56, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Friday", "2025-01-10", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 6.56, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Monday", "2025-01-13", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Tuesday", "2025-01-14", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Wednesday", "2025-01-15", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 35.06, "Litmus"], ["David Joy", "Litmus MSE - Southend", "Tuesday", "2025-01-14", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "New MSE Process - Outstanding Payment", 283.88, 34.13, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Sunday", "2025-01-05", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 6.56, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Monday", "2025-01-06", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 6.56, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Tuesday", "2025-01-07", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 6.56, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Wednesday", "2025-01-08", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 6.56, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Monday", "2025-01-13", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 291.56, 35.06, "Litmus"], ["Oana Tilvic", "Litmus MSE - Basildon", "Tuesday", "2025-01-14", "08:00", "17:00", 30.0, 8.5, 27.0, 30.69, "New MSE Process - Outstanding Payment", 260.87, 31.37, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Thursday", "2025-01-09", "07:30", "14:00", 0.0, 6.0, 30.0, 30.69, "New MSE Process - Outstanding Payment", 184.14, 4.14, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Friday", "2025-01-10", "07:30", "18:00", 30.0, 10.0, 30.0, 30.69, "New MSE Process - Outstanding Payment", 306.9, 6.9, "Litmus"], ["Shivali Bhati", "Litmus MSE - Orset", "Monday", "2025-01-06", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "Outstanding Payment - Candidate requested funds urgently", 291.56, 6.56, "Litmus"], ["Shivali Bhati", "Litmus MSE - Orset", "Wednesday", "2025-01-08", "13:00", "18:30", 0.0, 5.0, 30.0, 30.69, "Outstanding Payment - Candidate requested funds urgently", 153.45, 3.45, "Litmus"], ["Shivali Bhati", "Litmus MSE - Orset", "Friday", "2025-01-10", "08:00", "18:00", 30.0, 9.5, 30.0, 30.69, "Outstanding Payment - Candidate requested funds urgently", 291.56, 6.56, "Litmus"], ["Shivali Bhati", "Litmus MSE - Orset", "Monday", "2025-01-13", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Outstanding Payment - Candidate requested funds urgently", 291.56, 25.56, "Litmus"], ["Shivali Bhati", "Litmus MSE - Orset", "Tuesday", "2025-01-14", "13:00", "18:00", 0.0, 5.0, 28.0, 30.69, "Outstanding Payment - Candidate requested funds urgently", 153.45, 13.45, "Litmus"], ["Shivali Bhati", "Litmus MSE - Orset", "Wednesday", "2025-01-15", "13:00", "18:00", 0.0, 5.0, 28.0, 30.69, "Outstanding Payment - Candidate requested funds urgently", 153.45, 13.45, "Litmus"], ["Shivali Bhati", "Litmus MSE - Orset", "Friday", "2025-01-17", "08:00", "18:00", 0.0, 9.5, 28.0, 30.69, "Outstanding Payment - Candidate requested funds urgently", 291.56, 25.56, "Litmus"], ["David Joy", "Litmus MSE - Southend", "Friday", "2025-01-10", "08:00", "17:00", 45.0, 8.25, 30.0, 30.69, "Not sent via selfbill report", 253.19, 5.69, "Litmus"], ["Virginia Ego Amechi", "Lloyds Pharmacy", "Thursday", "2025-01-09", "07:30", "17:00", 0.0, 9.5, 50.0, 69.44, "(Consulant Request)", 659.68, 184.68, "Neuven"], ["Virginia Ego Amechi", "Lloyds Pharmacy", "Friday", "2025-01-10", "06:30", "16:30", 0.0, 10.0, 50.0, 69.44, "(Consulant Request)", 694.4, 194.4, "Neuven"], ["Virginia Ego Amechi", "Lloyds Pharmacy", "Wednesday", "2025-01-15", "06:30", "16:30", 0.0, 10.0, 50.0, 69.44, "(Consulant Request)", 694.4, 194.4, "Neuven"], ["Virginia Ego Amechi", "Lloyds Pharmacy", "Thursday", "2025-01-16", "07:30", "17:00", 0.0, 9.5, 50.0, 69.44, "(Consulant Request)", 659.68, 184.68, "Neuven"], ["Virginia Ego Amechi", "Lloyds Pharmacy", "Friday", "2025-01-17", "06:30", "15:30", 0.0, 9.0, 50.0, 69.44, "(Consulant Request)", 624.96, 174.96, "Neuven"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2025-01-08", "07:30", "19:15", 30.0, 11.25, 48.0, 51.5, "Approved for tomorrows report. Candidate needs funds", 579.38, 39.38, "Bridge"], ["Simba Makarau", "Litmus MSE - Basildon", "Monday", "2025-01-20", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on Self Bill (Consulant Request)", 291.56, 35.06, "Litmus"], ["Simba Makarau", "Litmus MSE - Basildon", "Wednesday", "2025-01-22", "08:00", "17:00", 30.0, 8.5, 27.0, 30.69, "Not on Self Bill (Consulant Request)", 260.87, 31.37, "Litmus"], ["Simba Makarau", "Litmus MSE - Basildon", "Thursday", "2025-01-23", "08:00", "19:00", 30.0, 10.5, 27.0, 30.69, "Not on Self Bill (Consulant Request)", 322.25, 38.75, "Litmus"], ["Everlyn Kabba", "Litmus MSE - Broomfield", "Monday", "2025-01-20", "08:00", "15:30", 30.0, 7.0, 27.0, 30.69, "Not On a Selfbill", 214.83, 25.83, "Litmus"], ["Everlyn Kabba", "Litmus MSE - Broomfield", "Tuesday", "2025-01-21", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Everlyn Kabba", "Litmus MSE - Broomfield", "Wednesday", "2025-01-22", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Everlyn Kabba", "Litmus MSE - Broomfield", "Thursday", "2025-01-23", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "Litmus MSE - Broomfield", "Monday", "2025-01-20", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "Litmus MSE - Broomfield", "Tuesday", "2025-01-21", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "Litmus MSE - Broomfield", "Thursday", "2025-01-23", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "Litmus MSE - Broomfield", "Friday", "2025-01-24", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Penelope Piccio", "Circle Reading", "Monday", "2025-01-13", "08:00", "18:00", 30.0, 10.0, 45.5, 55.09, "Approved Aftercutoff was not on last weeks self bill", 550.9, 95.9, "Circle"], ["Lena O'Leary", "Litmus MSE - Southend", "Tuesday", "2025-01-21", "13:00", "18:00", 0.0, 5.0, 27.0, 30.69, "Not sent via selfbill", 153.45, 18.45, "Litmus"], ["Lena O'Leary", "Litmus MSE - Southend", "Friday", "2025-01-24", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not sent via selfbill", 291.56, 35.06, "Litmus"], ["Comfort Raji", "Litmus MSE - Basildon", "Tuesday", "2025-01-21", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not sent via selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Monday", "2025-01-20", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Tuesday", "2025-01-21", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Thursday", "2025-01-23", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Friday", "2025-01-24", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not On a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "Litmus MSE - Basildon", "Saturday", "2025-01-25", "08:00", "17:30", 30.0, 9.0, 27.0, 30.69, "Not On a Selfbill", 276.21, 33.21, "Litmus"], ["Shauna Henderson Rose", "Litmus MSE - Southend", "Wednesday", "2025-01-22", "13:00", "18:00", 0.0, 5.0, 30.0, 30.69, "Not on self bill / urgent request", 153.45, 3.45, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Thursday", "2025-01-16", "11:00", "18:00", 0.0, 7.0, 27.0, 30.69, "New MSE Process - Outstanding Payment", 214.83, 25.83, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Friday", "2025-01-17", "07:30", "18:00", 30.0, 10.0, 27.0, 30.69, "New MSE Process - Outstanding Payment", 306.9, 36.9, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Monday", "2025-01-20", "07:30", "18:00", 30.0, 10.0, 27.0, 30.69, "Not on Self Bill", 306.9, 36.9, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Thursday", "2025-01-23", "07:30", "18:00", 30.0, 10.0, 27.0, 30.69, "Not on Self Bill", 306.9, 36.9, "Litmus"], ["Charmaine Reis", "Litmus MSE - Broomfield", "Friday", "2025-01-24", "07:30", "18:00", 30.0, 10.0, 27.0, 30.69, "Not on Self Bill", 306.9, 36.9, "Litmus"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Wednesday", "2025-01-08", "08:00", "19:00", 30.0, 10.5, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 629.9, 104.9, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Thursday", "2025-01-09", "08:00", "18:45", 30.0, 10.25, 50.0, 60.99, "Not On a Selfbill / Consulant Request", 625.15, 112.65, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Friday", "2025-01-10", "08:00", "18:30", 30.0, 10.0, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 599.9, 99.9, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Sunday", "2025-01-12", "08:00", "18:30", 30.0, 7.5, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 449.93, 74.93, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Wednesday", "2025-01-15", "08:00", "17:30", 30.0, 9.0, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 539.91, 89.91, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Rivers", "Tuesday", "2024-12-17", "07:30", "20:00", 30.0, 12.0, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 719.88, 119.88, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Rivers", "Thursday", "2024-12-19", "07:30", "18:00", 30.0, 10.0, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 599.9, 99.9, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Rivers", "Friday", "2024-12-20", "07:30", "18:00", 30.0, 10.0, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 599.9, 99.9, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Rivers", "Friday", "2025-01-03", "09:15", "17:30", 30.0, 7.75, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 464.92, 77.42, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Rivers", "Friday", "2025-01-17", "07:30", "18:00", 30.0, 10.0, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 599.9, 99.9, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Rivers", "Friday", "2025-01-24", "07:30", "18:00", 30.0, 10.0, 50.0, 59.99, "Not On a Selfbill / Consulant Request", 599.9, 99.9, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2025-01-09", "07:30", "17:00", 30.0, 9.0, 44.0, 51.5, "Approved After Todays Cutoff", 463.5, 67.5, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Friday", "2025-01-10", "07:30", "14:30", 30.0, 6.5, 44.0, 51.5, "Approved After Todays Cutoff", 334.75, 48.75, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2025-01-18", "07:30", "17:00", 30.0, 9.0, 48.0, 55.25, "Approved After Todays Cutoff", 497.25, 65.25, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2025-01-21", "08:00", "19:30", 30.0, 11.0, 44.0, 51.5, "Approved After Todays Cutoff", 566.5, 82.5, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Thurday", "2025-01-23", "08:00", "19:00", 30.0, 10.5, 44.0, 51.5, "Approved After Todays Cutoff", 540.75, 78.75, "Bridge"], ["Tanya Williams", "NHSP - Croydon", "Wednesday", "2025-01-22", "08:00", "17:00", 30.0, 8.5, 30.0, 32.76, "Will be on tomorrows report. Tanya needs the funds today forher Mortgage Payment", 278.46, 23.46, "NHSP"], ["Tanya Williams", "NHSP - Croydon", "Thursday", "2025-01-23", "08:00", "17:30", 30.0, 9.0, 30.0, 32.76, "Will be on tomorrows report. Tanya needs the funds today forher Mortgage Payment", 294.84, 24.84, "NHSP"], ["Tanya Williams", "NHSP - Croydon", "Monday", "2025-01-27", "20:00", "08:00", 60.0, 11.0, 34.0, 37.91, "Will be on tomorrows report. Tanya needs the funds today forher Mortgage Payment", 417.01, 43.01, "NHSP"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2025-01-14", "08:30", "17:30", 30.0, 8.5, 43.0, 44.65, "Approved for tomorrow / PO beacuse starlight will send funds on monday", 379.53, 14.03, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Thursday", "2025-01-16", "08:00", "19:00", 30.0, 10.0, 43.0, 44.65, "Approved for tomorrow / PO beacuse starlight will send funds on monday", 446.5, 16.5, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Friday", "2025-01-24", "09:30", "18:00", 30.0, 8.0, 43.0, 44.65, "Approved for tomorrow / PO beacuse starlight will send funds on monday", 357.2, 13.2, "Bridge"], ["Hellen Chipudhia", "Lloyds Pharmacy", "Monday", "2025-01-20", "08:00", "13:25", 60.0, 4.25, 50.0, 69.44, "Not on this weeks selfbill & candidate needs funds for bills due today. Approved for next weeks selfbill.", 295.12, 82.62, "Neuven"], ["Hellen Chipudhia", "Lloyds Pharmacy", "Tuesday", "2025-01-21", "08:00", "15:00", 60.0, 6.0, 50.0, 69.44, "Not on this weeks selfbill & candidate needs funds for bills due today. Approved for next weeks selfbill.", 416.64, 116.64, "Neuven"], ["Hellen Chipudhia", "Lloyds Pharmacy", "Wednesday", "2025-01-23", "08:00", "15:30", 60.0, 6.5, 50.0, 69.44, "Not on this weeks selfbill & candidate needs funds for bills due today. Approved for next weeks selfbill.", 451.36, 126.36, "Neuven"], ["Hellen Chipudhia", "Lloyds Pharmacy", "Thursday", "2025-01-24", "08:00", "20:00", 60.0, 11.0, 50.0, 69.44, "Not on this weeks selfbill & candidate needs funds for bills due today. Approved for next weeks selfbill.", 763.84, 213.84, "Neuven"], ["Penelope Piccio", "Circle - Reading", "Wednesday", "2025-01-22", "07:30", "19:30", 30.0, 11.5, 45.5, 60.0, "Approved after cutoff", 690.0, 166.75, "Bridge"], ["Penlelope Piccio", "Circle - Reading", "Thursday", "2025-01-23", "13:00", "18:00", 0.0, 5.0, 45.5, 60.0, "Approved after cutoff", 300.0, 72.5, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Friday", "2025-01-24", "07:30", "17:00", 30.0, 9.0, 45.5, 60.0, "Approved after cutoff", 540.0, 130.5, "Bridge"], ["Simba Makarau", "MSE - Basildon", "Tuesday", "2025-01-28", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Friday", "2025-01-31", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Oluwamayowa Fabunmi", "MSE - Southend", "Wednesday", "2025-01-22", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Selfbill", 283.88, 34.13, "Litmus"], ["Oluwamayowa Fabunmi", "MSE - Southend", "Friday", "2025-01-31", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Selfbill", 283.88, 34.13, "Litmus"], ["David Joy", "MSE - Southend", "Monday", "2025-01-27", "08:00", "17:15", 45.0, 8.5, 27.0, 30.69, "Not on a Selfbill", 260.87, 31.37, "Litmus"], ["David Joy", "MSE - Southend", "Tuesday", "2025-01-28", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Selfbill", 283.88, 34.13, "Litmus"], ["David Joy", "MSE - Southend", "Wednesday", "2025-01-29", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Selfbill", 283.88, 34.13, "Litmus"], ["David Joy", "MSE - Southend", "Thursday", "2025-01-30", "08:00", "17:30", 45.0, 8.75, 27.0, 30.69, "Not on a Selfbill", 268.54, 32.29, "Litmus"], ["David Joy", "MSE - Southend", "Friday", "2025-01-31", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Selfbill", 283.88, 34.13, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Monday", "2025-01-27", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Tuesday", "2025-01-28", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Wednesday", "2025-01-29", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Thursday", "2025-01-30", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Monday", "2025-01-27", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Tuesday", "2025-01-28", "13:00", "18:00", 0.0, 5.0, 27.0, 30.69, "Not on a Selfbill", 153.45, 18.45, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Wednesday", "2025-01-29", "13:00", "18:00", 0.0, 5.0, 27.0, 30.69, "Not on a Selfbill", 153.45, 18.45, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Thursday", "2025-01-30", "08:00", "13:00", 0.0, 5.0, 27.0, 30.69, "Not on a Selfbill", 153.45, 18.45, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Friday", "2025-05-31", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Tuesday", "2025-01-28", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "MSE Basildon", "Wednesday", "2025-01-29", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Tuesday", "2025-01-28", "08:00", "17:15", 30.0, 8.75, 46.0, 59.99, "Approved for this weeks self bill- Jason to confim", 524.91, 122.41, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Wednesday", "2025-01-29", "08:00", "15:45", 30.0, 7.25, 55.0, 59.99, "Approved for this weeks self bill- Jason to confim", 434.93, 36.18, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Firday", "2025-05-31", "08:00", "15:30", 30.0, 7.0, 55.0, 59.99, "Approved for this weeks self bill- Jason to confim", 419.93, 34.93, "Bridge"], ["Frackson Banda", "MSE - Southend", "Monday", "2025-02-03", "08:00", "18:00", 60.0, 9.0, 27.0, 30.69, "Not on a Selfbill", 276.21, 33.21, "Litmus"], ["David Joy", "MSE - Southend", "Monday", "2025-02-03", "08:00", "17:00", 45.0, 8.25, 27.0, 30.69, "Not on a Selfbill", 253.19, 30.44, "Litmus"], ["David Joy", "MSE - Southend", "Tuesday", "2025-02-04", "08:00", "17:30", 45.0, 8.75, 27.0, 30.69, "Not on a Selfbill", 268.54, 32.29, "Litmus"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Monday", "2025-01-27", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Approved on Bridge / We had rate issues with last weeks shifts so canidate needs these shifts", 570.0, 95.0, "Bridge"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Friday", "2025-01-31", "08:00", "14:00", 0.0, 6.0, 50.0, 60.0, "Approved on Bridge / We had rate issues with last weeks shifts so candidate needs these shifts", 360.0, 60.0, "Bridge"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Tuesday", "2025-01-14", "08:00", "15:30", 30.0, 7.0, 50.0, 60.0, "Came over on last weeks report as incorrect charge rate and could not pay the candiate. the amendmetn has been processed for next weeks reprot. Candidate needs this money for bills.", 420.0, 70.0, "Bridge"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Thursday", "2025-01-16", "08:00", "18:00", 30.0, 9.5, 50.0, 60.0, "Came over on last weeks report as incorrect charge rate and could not pay the candiate. the amendmetn has been processed for next weeks reprot. Candidate needs this money for bills.", 570.0, 95.0, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Thursday", "2025-01-29", "08:30", "18:30", 30.0, 9.5, 40.0, 44.65, "Need to pay today ts today, so the candidate can recive payment tomorrow (Stralight)", 424.18, 44.18, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Friday", "2025-01-30", "08:30", "18:00", 30.0, 9.0, 40.0, 44.65, "Need to pay today ts today, so the candidate can recive payment tomorrow (Stralight)", 401.85, 41.85, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Saturday", "2025-02-02", "07:30", "17:30", 30.0, 9.5, 48.0, 52.88, "Need to pay today ts today, so the candidate can recive payment tomorrow (Stralight)", 502.36, 46.36, "Bridge"], ["Bridie Newton", "MSE - Southend", "Tuesday", "2025-02-04", "08:00", "18:00", 30.0, 9.5, 23.22, 31.5, "Not on a Selfbill", 299.25, 78.66, "Litmus"], ["Bridie Newton", "MSE - Southend", "Wednesday", "2025-02-05", "07:45", "18:00", 30.0, 9.75, 23.22, 31.5, "Not on a Selfbill", 307.13, 80.73, "Litmus"], ["Comfort Raji", "Litmus MSE - Basildon", "Tuesday", "2025-02-06", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Penelope Piccio", "Circle - Reading", "Monday", "2025-01-27", "07:30", "18:30", 30.0, 10.5, 45.5, 60.0, "Approved after cutoff", 630.0, 152.25, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Tuesday", "2025-01-28", "07:30", "18:30", 30.0, 10.5, 45.5, 60.0, "Approved after cutoff", 630.0, 152.25, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Thursday", "2025-01-30", "07:30", "17:00", 30.0, 9.0, 45.5, 60.0, "Approved after cutoff", 540.0, 130.5, "Bridge"], ["Lena O'Leary", "MSE - Southend", "Monday", "2025-02-03", "13:00", "18:00", 0.0, 5.0, 27.0, 30.69, "Not on a Selfbill", 153.45, 18.45, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Tuesday", "2025-02-04", "13:00", "18:00", 0.0, 5.0, 27.0, 30.69, "Not on a Selfbill", 153.45, 18.45, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Thursday", "2025-02-06", "08:00", "13:00", 0.0, 5.0, 27.0, 30.69, "Not on a Selfbill", 153.45, 18.45, "Litmus"], ["Lena O'Leary", "MSE - Southend", "Friday", "2025-02-07", "08:00", "18:30", 30.0, 10.0, 27.0, 30.69, "Not on a Selfbill", 306.9, 36.9, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Monday", "2025-02-03", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Tuesday", "2025-02-04", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Thursday", "2025-02-06", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Friday", "2025-02-07", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Tuesday", "2025-02-04", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Wednesday", "2025-02-05", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Thursday", "2025-02-06", "08:00", "18:30", 30.0, 10.0, 27.0, 30.69, "Not on a Selfbill", 306.9, 36.9, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Friday", "2025-02-07", "08:00", "18:30", 30.0, 10.0, 27.0, 30.69, "Not on a Selfbill", 306.9, 36.9, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Monday", "2025-02-03", "08:00", "20:00", 30.0, 11.5, 27.0, 30.69, "Not on a Selfbill", 352.94, 42.44, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Tuesday", "2025-02-04", "09:00", "17:30", 30.0, 8.0, 27.0, 30.69, "Not on a Selfbill", 245.52, 29.52, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Wednesday", "2025-02-05", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Thursday", "2025-02-06", "08:00", "14:00", 0.0, 6.0, 27.0, 30.69, "Not on a Selfbill", 184.14, 22.14, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Friday", "2025-02-07", "00:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Monday", "2025-02-03", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Tuesday", "2025-02-04", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Wednesday", "2025-02-05", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Thursday", "2025-02-06", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Friday", "2025-02-07", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Willard Mandaza", "MSE - Broomfield", "Thursday", "2025-02-06", "07:45", "18:00", 30.0, 9.75, 27.0, 30.69, "Not on a Selfbill", 299.23, 35.98, "Litmus"], ["Rinah Bheekharry", "Ramsay - Cherwell", "Monday", "2025-01-20", "08:00", "18:45", 30.0, 10.25, 50.0, 59.99, "Came over on last weeks report as incorrect charge rate and could not pay the candiate. the amendment has been processed for this reportweeks reprot", 614.9, 102.4, "Bridge"], ["Oana Tilvic", "MSE - Basildon", "Monday", "2025-02-10", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Oana Tilvic", "MSE - Basildon", "Tuesday", "2025-02-11", "08:00", "18:50", 30.0, 10.2, 27.0, 30.69, "Not on a Selfbill", 313.04, 37.64, "Litmus"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2025-02-04", "07:30", "17:45", 30.0, 9.75, 44.0, 51.51, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 502.22, 73.22, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2025-02-05", "08:00", "18:15", 30.0, 9.75, 44.0, 51.51, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 502.22, 73.22, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Wednesday", "2025-02-06", "07:30", "17:30", 30.0, 9.5, 44.0, 51.51, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 489.35, 71.35, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Wednesday", "2025-02-05", "08:30", "18:15", 30.0, 9.25, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 413.01, 43.01, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Thursday", "2025-02-06", "08:30", "17:30", 30.0, 8.5, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 379.53, 39.53, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Friday", "2025-02-07", "08:30", "17:00", 30.0, 8.0, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 357.2, 37.2, "Bridge"], ["Sandra Duarte-Botello", "Ramsay - Cherwell", "Monday", "2025-02-03", "08:00", "16:30", 30.0, 8.0, 55.0, 59.99, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 479.92, 39.92, "Bridge"], ["Sandra Duarte-Botello", "Ramsay - Cherwell", "Thursday", "2025-02-06", "08:00", "17:00", 30.0, 8.5, 55.0, 59.99, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 509.92, 42.42, "Bridge"], ["Sandra Duarte-Botello", "Ramsay - Cherwell", "Friday", "2025-02-07", "08:00", "17:30", 30.0, 9.0, 55.0, 59.99, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 539.91, 44.91, "Bridge"], ["Maudy Hoyi", "MSE - Basildon", "Monday", "2025-02-10", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Selfbill", 291.56, 25.56, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Tuesday", "2025-02-11", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Selfbill", 291.56, 25.56, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Thursday", "2025-02-13", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Selfbill", 291.56, 25.56, "Litmus"], ["Comfort Raji", "MSE - Basildon", "Thursday", "2025-02-13", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Selfbill", 291.56, 25.56, "Litmus"], ["Comfort Raji", "MSE - Basildon", "Friday", "2025-02-14", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Selfbill", 291.56, 25.56, "Litmus"], ["Oana Tilvic", "MSE - Basildon", "Saturday", "2025-02-15", "08:00", "17:00", 30.0, 8.5, 27.0, 30.69, "Not on a Selfbill", 260.87, 31.37, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Monday", "2025-02-10", "08:00", "20:30", 60.0, 11.5, 27.0, 30.69, "Not on a Selfbill", 352.94, 42.44, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Tuesday", "2025-02-11", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Wednesday", "2025-02-12", "08:00", "19:00", 30.0, 10.5, 27.0, 30.69, "Not on a Selfbill", 322.25, 38.75, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Thursday", "2025-02-13", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Friday", "2025-02-14", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Monday", "2025-02-10", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Wednesday", "2025-02-12", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Thursday", "2025-02-13", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Friday", "2025-02-14", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Sekai Nyamhandu", "NHSP - Buckinghamshire", "Monday", "2025-02-10", "09:00", "17:00", 30.0, 7.5, 35.0, 39.0, "Will be on tomorrows report, but she needs to pay for accomadation so we said we will pay her today", 292.5, 30.0, "NHSP"], ["Sekai Nyamhandu", "NHSP - Buckinghamshire", "Wednesday", "2025-02-12", "09:00", "17:00", 30.0, 7.5, 35.0, 39.0, "Will be on tomorrows report, but she needs to pay for accomadation so we said we will pay her today", 292.5, 30.0, "NHSP"], ["Sekai Nyamhandu", "NHSP - Buckinghamshire", "Thursday", "2025-02-13", "09:00", "17:00", 30.0, 7.5, 35.0, 39.0, "Will be on tomorrows report, but she needs to pay for accomadation so we said we will pay her today", 292.5, 30.0, "NHSP"], ["Florah Mudeke", "MSE - Broomfield", "Monday", "2025-02-10", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Tuesday", "2025-02-11", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Thursday", "2025-02-13", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Friday", "2025-02-14", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["John Arthur", "Circle - Chelsfield Park", "Friday", "2025-01-31", "07:30", "21:00", 60.0, 12.5, 35.0, 40.96, "Due to dipustes the shift was approved after cutoff. Will be charged next week", 512.0, 74.5, "Bridge"], ["Rose Emmanuel", "Watford General Hospital", "Friday", "2024-12-13", "08:00", "20:00", 30.0, 11.5, 30.0, 31.17, "Candiate name not on system yet", 358.46, 13.46, "NHSP"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Wednesday", "2025-01-29", "08:00", "18:30", 30.0, 10.0, 50.0, 60.0, "Candiate complaint - Will be on this weeks report. If this is paid on Friday she wont recive money until monday (Starlight)", 600.0, 100.0, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Thursday", "2025-01-30", "08:00", "19:00", 30.0, 10.5, 50.0, 60.0, "Candiate complaint - Will be on this weeks report. If this is paid on Friday she wont recive money until monday (Starlight)", 630.0, 105.0, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Friday", "2025-01-31", "08:00", "19:30", 30.0, 11.0, 50.0, 60.0, "Candiate complaint - Will be on this weeks report. If this is paid on Friday she wont recive money until monday (Starlight)", 660.0, 110.0, "Bridge"], ["Shauna Henderson Rose", "Ramsay - Oaks", "Sunday", "2025-02-02", "08:00", "16:30", 30.0, 8.0, 60.0, 65.0, "Candiate complaint - Will be on this weeks report. If this is paid on Friday she wont recive money until monday (Starlight)", 520.0, 40.0, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Monday", "2025-02-10", "08:00", "18:15", 30.0, 9.75, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 498.62, 50.12, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Tuesday", "2025-02-11", "08:00", "14:15", 0.0, 6.25, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 319.63, 32.13, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Wednesday", "2025-02-12", "08:00", "16:15", 30.0, 7.75, 55.0, 59.99, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 464.92, 38.67, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Monday", "2025-02-13", "07:30", "16:45", 30.0, 8.75, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 447.48, 62.48, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Wednesday", "2025-02-12", "08:30", "18:15", 30.0, 9.25, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 413.01, 43.01, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Friday", "2025-02-14", "08:30", "17:15", 30.0, 8.25, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 368.36, 38.36, "Bridge"], ["Willard Mandaza", "MSE - Broomfield", "Monday", "2025-02-10", "17:30", "07:45", 60.0, 13.25, 27.0, 30.69, "Not on a Selfbill", 406.64, 48.89, "Litmus"], ["Willard Mandaza", "MSE - Broomfield", "Tuesday", "2025-02-14", "07:45", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Edward Brooks", "Bristol & Weston", "Tuesday", "2025-02-04", "08:00", "19:30", 60.0, 10.5, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 420.0, 52.5, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2025-02-05", "08:00", "20:00", 30.0, 11.5, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 460.0, 57.5, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2025-02-06", "08:00", "21:00", 60.0, 12.0, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 480.0, 60.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Tuesday", "2025-02-11", "08:00", "21:00", 60.0, 12.0, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 480.0, 60.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2025-02-12", "08:00", "21:00", 60.0, 12.0, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 480.0, 60.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2025-02-13", "08:00", "18:00", 30.0, 9.5, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 380.0, 47.5, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Tuesday", "2025-02-18", "08:00", "21:00", 60.0, 12.0, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 480.0, 60.0, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Wednesday", "2025-02-19", "08:00", "18:00", 30.0, 9.5, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 380.0, 47.5, "Retinue"], ["Edward Brooks", "Bristol & Weston", "Thursday", "2025-02-20", "08:00", "21:00", 60.0, 12.0, 35.0, 40.0, "Payment has been outstanding for 2 weeks, candidate needs funds or he will leave the agency", 480.0, 60.0, "Retinue"], ["Bridie Newton", "MSE - Southend", "Thursday", "2025-02-20", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Selfbill", 283.88, 34.13, "Litmus"], ["Bridie Newton", "MSE - Southend", "Friday", "2025-02-21", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Selfbill", 283.88, 34.13, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Tuesday", "2025-02-18", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Selfbill", 291.56, 25.56, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Wedensday", "2025-02-20", "08:00", "19:00", 30.0, 10.5, 28.0, 30.69, "Not on a Selfbill", 322.25, 28.25, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Monday", "2025-02-17", "08:00", "17:30", 30.0, 9.0, 27.0, 30.69, "Not on a Selfbill", 276.21, 33.21, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Tuesday", "2025-02-18", "08:00", "19:00", 30.0, 10.5, 27.0, 30.69, "Not on a Selfbill", 322.25, 38.75, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Wednesday", "2025-02-19", "13:00", "18:00", 0.0, 5.0, 27.0, 30.69, "Not on a Selfbill", 153.45, 18.45, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Thursday", "2025-02-20", "08:00", "20:15", 30.0, 11.75, 27.0, 30.69, "Not on a Selfbill", 360.61, 43.36, "Litmus"], ["David Joy", "MSE - Southend", "Monday", "2025-02-17", "08:00", "17:30", 45.0, 8.75, 27.0, 30.69, "Not on a Selfbill", 268.54, 32.29, "Litmus"], ["David Joy", "MSE - Southend", "Friday", "2025-02-21", "08:00", "13:30", 0.0, 5.5, 27.0, 30.69, "Not on a Selfbill", 168.8, 20.3, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Monday", "2025-02-17", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Tuesday", "2025-02-18", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Thursday", "2025-02-20", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Friday", "2025-02-21", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Selfbill", 291.56, 35.06, "Litmus"], ["Penelope Piccio", "Circle - Reading", "Monday", "2025-02-10", "13:00", "18:00", 0.0, 5.0, 45.5, 60.0, "Should have been paid last Friday. Retinue was messing about with her complaince so tis one shift was not authorised in time.", 300.0, 72.5, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Monday", "2025-02-17", "08:00", "17:30", 30.0, 9.0, 55.0, 60.0, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 540.0, 45.0, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Tuesday", "2025-02-18", "08:00", "16:45", 30.0, 7.75, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 396.34, 39.84, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Friday", "2025-02-21", "08:00", "15:00", 30.0, 6.5, 55.0, 60.0, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 390.0, 32.5, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Tuesday", "2025-02-18", "08:00", "19:00", 30.0, 10.5, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 468.83, 48.83, "Bridge"], ["Jovanie Santos", "Ramsay - North Downs", "Wednesday", "2025-02-21", "08:30", "17:30", 30.0, 8.5, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 379.53, 39.53, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Tuesday", "2025-02-18", "13:00", "19:00", 0.0, 6.0, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 306.84, 42.84, "Bridge"], ["Diosdado Wagan", "Ramsay - North Downs", "Thursday", "2025-02-20", "08:30", "19:00", 30.0, 10.0, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 511.4, 71.4, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Monday", "2025-02-17", "13:00", "18:00", 0.0, 5.0, 45.5, 60.57, "Approved after cutoff - Candidate has upcoming bills. Shfits will be charged next week", 302.85, 75.35, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Wedneday", "2025-02-19", "13:00", "18:00", 0.0, 5.0, 32.5, 42.0, "Approved after cutoff - Candidate has upcoming bills. Shfits will be charged next week", 210.0, 47.5, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Friday", "2025-02-21", "07:30", "12:30", 0.0, 5.0, 45.5, 60.57, "Approved after cutoff - Candidate has upcoming bills. Shfits will be charged next week", 302.85, 75.35, "Bridge"], ["Penelope Piccio", "Circle - Reading", "Saturday", "2025-02-22", "07:30", "15:30", 30.0, 7.5, 51.5, 67.11, "Approved after cutoff - Candidate has upcoming bills. Shfits will be charged next week", 503.33, 117.08, "Bridge"], ["Simba Makarau", "MSE - Basildon", "Tuesday", "2025-02-25", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Wednesday", "2025-02-26", "08:00", "20:00", 30.0, 11.5, 27.0, 30.69, "Not on a Self-bill", 352.94, 42.44, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Thursday", "2025-02-27", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Simba Makarau", "MSE - Basildon", "Friday", "2025-02-28", "08:00", "18;00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Monday", "2025-02-24", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Tuesday", "2025-02-25", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Thursday", "2025-02-27", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Florah Mudeke", "MSE - Broomfield", "Friday", "2025-02-28", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Thursday", "2025-02-27", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Self-bill", 291.56, 25.56, "Litmus"], ["Maudy Hoyi", "MSE - Basildon", "Friday", "2025-02-28", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Self-bill", 291.56, 25.56, "Litmus"], ["David Joy", "MSE - Southend", "Monday", "2025-02-24", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Self-bill", 283.88, 34.13, "Litmus"], ["David Joy", "MSE - Southend", "Tuesday", "2025-02-25", "08:00", "18:00", 45.0, 9.25, 27.0, 30.69, "Not on a Self-bill", 283.88, 34.13, "Litmus"], ["David Joy", "MSE - Southend", "Wednesday", "2025-02-26", "08:00", "13:00", 0.0, 5.0, 27.0, 30.69, "Not on a Self-bill", 153.45, 18.45, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Monday", "2025-02-24", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Tuesday", "2025-02-25", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Wednesday", "2025-02-26", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Thursday", "2025-02-27", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["Evelyn Kabba", "MSE - Broomfield", "Friday", "2025-02-28", "08:00", "18:00", 30.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["David Joy", "MSE - Southend", "Thursday", "2025-02-27", "08:00", "18:15", 45.0, 9.5, 27.0, 30.69, "Not on a Self-bill", 291.56, 35.06, "Litmus"], ["David Joy", "MSE - Southend", "Friday", "2025-02-28", "08:00", "18:30", 45.0, 9.75, 27.0, 30.69, "Not on a Self-bill", 299.23, 35.98, "Litmus"], ["Diosdado Wagan", "North Downs Hospital", "Saturday", "2025-03-01", "08:30", "14:30", 30.0, 5.5, 41.0, 45.92, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 252.56, 27.06, "Bridge"], ["Jovanie Santos", "North Downs Hospital", "Friday", "2025-02-28", "08:30", "20:00", 30.0, 11.0, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 491.15, 51.15, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Monday", "2025-02-24", "08:00", "17:30", 30.0, 9.0, 46.0, 51.15, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 460.35, 46.35, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Tuesday", "2025-02-25", "08:00", "17:00", 30.0, 8.5, 46.0, 51.15, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 434.78, 43.78, "Bridge"], ["Sandra Duarte Botello", "Ramsay - Cherwell", "Friday", "2025-02-28", "08:00", "16:00", 30.0, 7.5, 55.0, 59.99, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 449.93, 37.43, "Bridge"], ["Comfort Raji", "MSE - Basildon", "Thursday", "2025-02-27", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Self-bill", 291.56, 25.56, "Litmus"], ["Comfort Raji", "MSE - Basildon", "Friday", "2025-02-28", "08:00", "18:00", 30.0, 9.5, 28.0, 30.69, "Not on a Self-bill", 291.56, 25.56, "Litmus"], ["Josiah Nybango", "East & North Hertfordshire", "Monday", "2025-02-17", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Tuesday", "2025-02-18", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Wednesday", "2025-02-19", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Thursday", "2025-02-20", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Friday", "2025-02-21", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Monday", "2025-02-24", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Tuesday", "2025-02-25", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Thursday", "2025-02-27", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Friday", "2025-02-28", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Monday", "2025-03-03", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Tuesday", "2025-03-04", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Wednesday", "2025-03-06", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Josiah Nybango", "East & North Hertfordshire", "Thursday", "2025-03-07", "08:00", "18:00", 30.0, 9.5, 24.0, 25.26, "PRC Issue on NHSP - See reason below", 239.97, 11.97, "NHSP"], ["Diosdado Wagan", "North Downs Hospital", "Tuesday", "2025-03-04", "13:00", "19:45", 0.0, 6.75, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 345.2, 48.2, "Bridge"], ["Diosdado Wagan", "North Downs Hospital", "Thursday", "2025-03-06", "07:30", "17:15", 30.0, 9.25, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 473.05, 66.05, "Bridge"], ["Diosdado Wagan", "North Downs Hospital", "Saturday", "2025-03-08", "08:30", "16:45", 30.0, 7.75, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 396.34, 55.34, "Bridge"], ["Jovanie Santos", "North Downs Hospital", "Wednesday", "2025-03-05", "07:30", "13:15", 0.0, 5.75, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 256.74, 26.74, "Bridge"], ["Jovanie Santos", "North Downs Hospital", "Friday", "2025-03-07", "07:30", "16:45", 30.0, 8.75, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 390.69, 40.69, "Bridge"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-03-03", "08:00", "17:30", 30.0, 9.0, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 460.26, 46.26, "Bridge"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-03-04", "08:00", "13:00", 0.0, 5.0, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 255.7, 25.7, "Bridge"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-03-07", "08:00", "16:00", 30.0, 7.5, 55.0, 60.0, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 450.0, 37.5, "Bridge"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Saturday", "2025-03-08", "08:00", "15:30", 30.0, 7.0, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 357.98, 35.98, "Bridge"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-03-12", "08:00", "17:00", 30.0, 8.5, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 434.69, 43.69, "Bridge"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-03-13", "08:00", "18:00", 30.0, 9.5, 46.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 485.83, 48.83, "Bridge"], ["Diosdado Wagan", "North Downs Hospital", "Monday", "2025-03-10", "08:30", "16:30", 30.0, 7.5, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 383.55, 53.55, "Bridge"], ["Diosdado Wagan", "North Downs Hospital", "Thursday", "2025-03-13", "08:30", "21:00", 30.0, 12.0, 44.0, 51.14, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 613.68, 85.68, "Bridge"], ["Jovanie Santos", "North Downs Hospital", "Wednesday", "2025-03-13", "08:30", "18:00", 30.0, 9.0, 40.0, 44.65, "Due Starlight cutoff at 3pm. We need to pay today for the candidate to receive payment tomorrow", 401.85, 41.85, "Bridge"], ["Hector Pablo", "Cromwell", "Monday", "2025-02-10", "07:30", "21:00", 60.0, 12.5, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 625.0, 25.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Wednesday", "2025-02-12", "07:30", "15:30", 30.0, 7.5, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 375.0, 15.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Thursday", "2025-02-13", "07:00", "00:00", 60.0, 16.0, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 800.0, 32.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Friday", "2025-02-14", "07:30", "00:00", 60.0, 15.5, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 775.0, 31.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Monday", "2025-02-24", "07:30", "21:00", 60.0, 12.5, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 625.0, 25.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Friday", "2025-02-28", "07:30", "21:00", 60.0, 12.5, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 625.0, 25.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Monday", "2025-03-03", "07:00", "21:00", 60.0, 13.0, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 650.0, 26.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Tuesday", "2025-03-04", "07:30", "21:00", 60.0, 12.5, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 625.0, 25.0, "ETIPS"], ["Hector Pablo", "Cromwell", "Wednesday", "2025-03-05", "09:15", "21:00", 60.0, 10.75, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 537.5, 21.5, "ETIPS"], ["Hector Pablo", "Cromwell", "Thursday", "2025-03-06", "07:30", "16:30", 30.0, 8.5, 48.0, 50.0, "all shifts uploaded to Etips - Nurse threateneing to leave", 425.0, 17.0, "ETIPS"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-03-19", "07:30", "17:45", 30.0, 9.75, 40.0, 44.65, "Shift approved on retinue Will recieve the funds this week", 435.34, 45.34, "retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-03-21", "08:30", "19:00", 30.0, 10.0, 40.0, 44.65, "Shift approved on retinue Will recieve the funds this week", 446.5, 46.5, "retinue"], ["Jovanie Santos", "Ramsey North Downs", "Monday", "2025-03-24", "07:30", "18:15", 30.0, 10.25, 40.0, 44.65, "Shift approved on retinue Will recieve the funds this week", 457.66, 47.66, "retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-03-28", "08:30", "15:00", 30.0, 6.5, 40.0, 44.65, "Shift approved on retinue Will recieve the funds this week", 290.22, 30.22, "retinue"], ["David Joy", "Royal London Hospital", "Wednesday", "2025-03-26", "08:00", "17:30", 30.0, 9.0, 27.0, 32.8, "the shift has been Authorised but haven't come out on the report", 295.2, 52.2, "HR"], ["Griechelle Manginsay", "Cromwell", "Tuesday", "2025-03-04", "07:30", "21:00", 60.0, 12.5, 48.0, 50.0, "shiftt approved on Etips", 625.0, 25.0, "ETIPS"], ["Griechelle Manginsay", "Cromwell", "Wednesday", "2025-03-05", "07:30", "21:00", 30.0, 13.0, 48.0, 50.0, "shiftt approved on Etips", 650.0, 26.0, "ETIPS"], ["Penelope Piccio", "Circle reading hospital", "Monday", "2025-03-24", "07:30", "19:00", 30.0, 11.0, 45.5, 60.0, "the shift has been Authorised but haven't come out on the report", 660.0, 159.5, "Bridge"], ["Penelope Piccio", "Circle reading hospital", "Tuesday", "2025-03-25", "07:30", "20:30", 30.0, 12.5, 45.5, 60.0, "the shift has been Authorised but haven't come out on the report", 750.0, 181.25, "Bridge"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-03-31", "08:00", "17:00", 30.0, 8.5, 55.0, 60.0, "Shift approved late on retinue, will recieve the funds next week", 510.0, 42.5, "retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-04-01", "08:00", "17:15", 30.0, 8.45, 55.0, 60.0, "Shift approved late on retinue, will recieve the funds next week", 507.0, 42.25, "retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-04-02", "08:00", "18:00", 30.0, 9.5, 46.0, 51.14, "Shift approved late on retinue, will recieve the funds next week", 485.83, 48.83, "retinue"], ["Jovanie Santos", "Ramsey North Downs", "Thursday", "2025-04-03", "08:30", "20:15", 30.0, 11.25, 40.0, 44.65, "Shift approved late on retinue, will recieve the funds next week", 502.31, 52.31, "retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-04-04", "08:30", "17:15", 30.0, 0, 40.0, 44.65, "Shift approved late on retinue, will recieve the funds next week", 15.66, 1.63, "retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-04-03", "07:30", "20:15", 30.0, 12.25, 44.0, 51.14, "Shift approved late on retinue, will recieve the funds next week", 626.47, 87.47, "retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Friday", "2025-04-04", "07:30", "17:15", 30.0, 9.25, 40.0, 44.65, "Shift approved late on retinue, will recieve the funds next week", 413.01, 43.01, "retinue"], ["Penelope Piccio", "Circle reading hospital", "Tuesday", "2025-04-01", "07:30", "18:30", 30.0, 10.5, 45.5, 60.0, "the shift has been Authorised but haven't come out on the report", 630.0, 152.25, "Retinue"], ["Penelope Piccio", "Circle reading hospital", "Thursday", "2025-04-03", "07:30", "18:30", 30.0, 10.5, 45.5, 60.0, "the shift has been Authorised but haven't come out on the report", 630.0, 152.25, "Retinue"], ["Penelope Piccio", "Circle reading hospital", "Friday", "2025-04-04", "07:30", "18:00", 30.0, 10.0, 45.5, 60.0, "the shift has been Authorised but haven't come out on the report", 600.0, 145.0, "Retinue"], ["Penelope Piccio", "Circle reading hospital", "Saturday", "2025-04-05", "07:30", "15:30", 30.0, 7.5, 45.5, 60.0, "the shift has been Authorised but haven't come out on the report", 450.0, 108.75, "Retinue"], ["Penelope Piccio", "Circle reading hospital", "Tuesday", "2025-04-08", "07:30", "18:00", 30.0, 10.5, 45.5, 55.09, "candidate requires funds shiftt approved on Retinue but not on the report", 578.45, 100.7, ""], ["Penelope Piccio", "Circle reading hospital", "Thursday", "2025-04-10", "07:30", "18:00", 30.0, 10.0, 45.5, 55.09, "candidate requires funds shiftt approved on Retinue but not on the report", 550.9, 95.9, ""], ["Penelope Piccio", "Circle reading hospital", "Friday", "2025-04-11", "09:30", "17:00", 30.0, 7.0, 45.5, 55.09, "candidate requires funds shiftt approved on Retinue but not on the report", 385.63, 67.13, ""], ["Penelope Piccio", "Circle reading hospital", "Friday", "2024-04-12", "07:30", "13:30", 0.0, 6.0, 51.5, 60.57, "candidate requires funds shiftt approved on Retinue but not on the report", 0, 0, ""], ["Diosdado B Wagan", "North Downs Hospital", "Tuesday", "2025-04-08", "07:30", "18:00", 30.0, 0, 40.0, 43.46, "candidate requires funds shiftt approved on Retinue but not on the report", 18.11, 1.44, ""], ["Diosdado B Wagan", "North Downs Hospital", "Wednesday", "2025-04-09", "08:00", "15:45", 30.0, 0, 40.0, 43.46, "candidate requires funds shiftt approved on Retinue but not on the report", 13.43, 1.07, ""], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-04-09", "08:00", "15:30", 30.0, 7.0, 50.0, 52.92, "candidate requires funds shiftt approved on Retinue but not on the report", 370.44, 20.44, ""], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-04-10", "08:00", "16:45", 30.0, 0, 50.0, 52.92, "candidate requires funds shiftt approved on Retinue but not on the report", 18.56, 1.02, ""], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-04-14", "08:00", "16:30", 30.0, 8.0, 50.0, 52.92, "candidate requires funds shiftt approved on Retinue but not on the report", 423.36, 23.36, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-04-15", "08:00", "13:15", 0.0, 5.15, 50.0, 52.92, "candidate requires funds shiftt approved on Retinue but not on the report", 272.54, 15.04, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-04-17", "08:00", "15:30", 30.0, 7.0, 46.0, 49.83, "candidate requires funds shiftt approved on Retinue but not on the report", 348.81, 26.81, "Retinue"], ["Diosdado B Wagan", "Ramsey Ashtead", "Monday", "2025-04-14", "07:30", "18:00", 30.0, 10.0, 40.0, 43.46, "candidate requires funds shiftt approved on Retinue but not on the report", 434.6, 34.6, "Retinue"], ["Diosdado B Wagan", "Ramsey Ashtead", "Tuesday", "2025-04-15", "07:30", "16:30", 30.0, 8.5, 40.0, 43.46, "candidate requires funds shiftt approved on Retinue but not on the report", 369.41, 29.41, "Retinue"], ["Diosdado B Wagan", "Ramsey Ashtead", "Wednesday", "2025-04-16", "07:30", "17:45", 30.0, 9.75, 40.0, 43.46, "candidate requires funds shiftt approved on Retinue but not on the report", 423.74, 33.74, "Retinue"], ["David Joy", "Royal London Hospital", "Wednesday", "2025-04-02", "19:30", "08:00", 60.0, 11.5, 31.67, 37.03, "candidate requires funds since its more than two weeks shift approved on HR", 425.85, 61.64, "HR"], ["Edward Brooks", "UHBW - Bristol Royal Infirmary", "Tuesday", "2025-04-01", "08:00", "21:30", 60.0, 12.5, 35.0, 39.08, "Candidate chasing for payment / shifts have come out on the report with incorect rates", 488.5, 51.0, "Clarity"], ["Edward Brooks", "UHBW - Bristol Royal Infirmary", "Wednesday", "2025-04-02", "08:00", "21:30", 60.0, 12.5, 35.0, 39.08, "Candidate chasing for payment / shifts have come out on the report with incorect rates", 488.5, 51.0, "Clarity"], ["Edward Brooks", "UHBW - Bristol Royal Infirmary", "Monday", "2025-04-07", "08:00", "21:30", 60.0, 12.5, 35.0, 39.08, "Candidate chasing for payment / shifts have come out on the report with incorect rates", 488.5, 51.0, "Clarity"], ["Edward Brooks", "UHBW - Bristol Royal Infirmary", "Tuesday", "2025-04-08", "08:00", "21:30", 60.0, 12.5, 35.0, 39.08, "Candidate chasing for payment / shifts have come out on the report with incorect rates", 488.5, 51.0, "Clarity"], ["Edward Brooks", "UHBW - Bristol Royal Infirmary", "Wednesday", "2025-04-09", "08:00", "21:30", 60.0, 12.5, 35.0, 39.08, "Candidate chasing for payment / shifts have come out on the report with incorect rates", 488.5, 51.0, "Clarity"], ["Diosdado B Wagan", "North Downs Hospital", "Tuesday", "2025-04-22", "08:30", "18:45", 30.0, 9.75, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 485.84, 56.84, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-04-24", "07:30", "19:00", 30.0, 11.0, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 548.13, 64.13, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Friday", "2025-04-25", "07:30", "19:45", 30.0, 11.75, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 585.5, 68.5, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Saturday", "2025-04-26", "08:00", "17:00", 30.0, 8.5, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 423.56, 49.56, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-04-25", "08:00", "16:30", 30.0, 8.0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 398.64, 30.64, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-05-01", "08:00", "14:30", 0.0, 6.5, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 323.89, 24.89, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-05-02", "08:00", "16:30", 30.0, 8.0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 398.64, 30.64, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Tuesday", "2025-04-29", "07:30", "20:30", 30.0, 12.5, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 622.88, 72.88, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-05-01", "07:30", "19:30", 30.0, 11.5, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 573.04, 67.04, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Friday", "2025-05-02", "07:30", "17:15", 30.0, 9.25, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 460.93, 53.93, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Saturday", "2025-05-03", "07:30", "18:45", 15.0, 11.0, 48.0, 51.06, "the shift has been authorised but haven't come out on the report", 561.66, 33.66, "Retinue"], ["David Joy", "Royal London Hospital", "Friday", "2025-04-25", "08:00", "18:00", 30.0, 9.5, 26.72, 32.8, "the shift has been authorised but haven't come out on the report", 311.6, 57.76, "HR"], ["David Joy", "Royal London Hospital", "Saturday", "2025-04-26", "08:00", "18:00", 30.0, 9.5, 31.67, 37.03, "the shift has been authorised but haven't come out on the report", 351.79, 50.92, "HR"], ["David Joy", "Royal London Hospital", "Monday", "2025-04-28", "08:00", "18:00", 30.0, 9.5, 26.72, 32.8, "the shift has been authorised but haven't come out on the report", 311.6, 57.76, "HR"], ["David Joy", "Royal London Hospital", "Friday", "2025-05-02", "19:30", "08:30", 60.0, 11.5, 31.67, 37.03, "the shift has been authorised but haven't come out on the report", 425.85, 61.64, "HR"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2024-12-16", "08:00", "17:00", 30.0, 8.5, 55.0, 59.99, "the shift has been authorised but haven't come out on the report", 509.92, 42.42, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2024-12-18", "08:00", "16:30", 30.0, 8.0, 55.0, 59.99, "the shift has been authorised but haven't come out on the report", 479.92, 39.92, "Retinue"], ["Penelope Piccio", "Circle reading hospital", "Thursday", "2025-05-01", "07:30", "18:00", 30.0, 10.0, 45.5, 59.93, "the shift has been authorised but haven't come out on the report", 599.3, 144.3, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Wednesday", "2025-05-07", "07:30", "19:00", 30.0, 11.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 478.06, 38.06, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-05-08", "07:30", "15:00", 30.0, 7.0, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 348.81, 40.81, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Friday", "2025-05-09", "07:30", "17:15", 30.0, 9.25, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 402.0, 32.0, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Saturday", "2025-05-10", "07:30", "19:00", 30.0, 11.0, 48.0, 51.06, "the shift has been authorised but haven't come out on the report", 561.66, 33.66, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-05-06", "08:00", "18:00", 30.0, 9.5, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 473.38, 36.38, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-05-08", "08:00", "17:30", 30.0, 9.0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 448.47, 34.47, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-05-09", "08:00", "16:30", 30.0, 8.0, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 423.36, 23.36, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-05-15", "07:30", "20:15", 30.0, 12.25, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 610.42, 71.42, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Friday", "2025-05-16", "07:30", "16:30", 30.0, 8.5, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 423.56, 49.56, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-05-09", "08:00", "19:15", 30.0, 10.75, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 467.19, 37.19, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-05-16", "08:00", "18:00", 30.0, 9.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 412.87, 32.87, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-05-22", "07:30", "17:30", 30.0, 9.5, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 473.38, 55.38, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Thursday", "2025-05-22", "08:00", "17:30", 30.0, 9.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 412.87, 32.87, "Retinue"], ["Penelope Piccio", "Circle reading hospital", "Monday", "2025-05-12", "12:30", "18:00", 0.0, 5.5, 45.5, 59.93, "the shift has been authorised but haven't come out on the report", 329.62, 79.37, "Retinue"], ["Lydie Gam-mackitta", "ID Medical University Hospitals Bristol and Weston", "Wednesday", "2025-05-21", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "ID Medical University Hospitals Bristol and Weston", "Thursday", "2025-05-22", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "ID Medical University Hospitals Bristol and Weston", "Friday", "2025-05-23", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-05-27", "08:00", "16:30", 30.0, 8.0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 398.64, 30.64, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-05-29", "08:00", "16:30", 30.0, 8.0, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 423.36, 23.36, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-05-29", "10:00", "18:00", 30.0, 7.5, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 373.72, 43.72, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Saturday", "2025-05-31", "07:30", "14:30", 30.0, 6.5, 41.0, 45.95, "the shift has been authorised but haven't come out on the report", 298.68, 32.18, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-05-28", "08:30", "18:00", 30.0, 9.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 391.14, 31.14, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Thursday", "2025-05-29", "10:00", "18:00", 30.0, 7.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 325.95, 25.95, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-05-30", "12:00", "17:45", 0.0, 7.75, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 336.81, 26.81, "Retinue"], ["Penelope Piccio", "Circle reading hospital", "Tuesday", "2025-05-27", "07:30", "19:00", 30.0, 11.0, 45.5, 59.93, "the shift has been authorised but haven't come out on the report", 659.23, 158.73, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-06-02", "08:00", "14:00", 0.0, 6.0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 298.98, 22.98, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-06-05", "08:00", "16:00", 30.0, 7.5, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 373.72, 28.72, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-06-06", "08:00", "17:15", 30.0, 8.45, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 421.06, 32.36, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Wednesday", "2025-06-04", "07:30", "18:15", 30.0, 10.25, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 510.76, 59.76, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-06-06", "08:00", "17:00", 30.0, 8.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 369.41, 29.41, "Retinue"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Monday", "2025-06-02", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Tuesday", "2025-06-03", "09:00", "19:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Wednesday", "2025-06-04", "10:00", "20:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Thursday", "2025-06-05", "11:00", "21:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Friday", "2025-06-06", "12:00", "22:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Maudy Hoyi", "Ramsey Springfield Hospital", "Tuesday", "2025-06-03", "07:30", "19:00", 30.0, 11.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 478.06, 38.06, "Retinue"], ["Maudy Hoyi", "Ramsey Springfield Hospital", "Friday", "2025-06-06", "17:30", "19:30", 30.0, 11.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 499.79, 39.79, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-06-09", "08:00", "18:15", 30.0, 9.45, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 470.89, 36.19, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-06-10", "08:00", "18:30", 30.0, 10.0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 498.3, 38.3, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-06-11", "08:00", "18:00", 30.0, 9.5, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 473.38, 36.38, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Tuesday", "2025-06-10", "13:00", "19:00", 0.0, 6.0, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 298.98, 34.98, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-06-12", "07:30", "18:00", 30.0, 10.0, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 498.3, 58.3, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Saturday", "2025-06-14", "07:30", "15:30", 30.0, 7.5, 41.0, 43.46, "the shift has been authorised but haven't come out on the report", 325.95, 18.45, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Tuesday", "2025-06-10", "08:30", "19:00", 30.0, 10.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 434.6, 34.6, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Thursday", "2025-06-12", "07:45", "18:00", 30.0, 9.75, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 423.74, 33.74, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-06-13", "08:00", "19:00", 30.0, 10.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 456.33, 36.33, "Retinue"], ["Penelope Piccio", "Oxford (The Manor Hospital", "Monday", "2025-06-02", "08:00", "18:00", 30.0, 9.5, 41.0, 51.94, "the shift has been authorised but haven't come out on the report", 493.43, 103.93, "ETIPS"], ["Penelope Piccio", "Oxford (The Manor Hospital", "Saturday", "2025-06-07", "08:00", "17:00", 30.0, 8.5, 42.5, 54.52, "the shift has been authorised but haven't come out on the report", 463.42, 102.17, "ETIPS"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Monday", "2025-06-09", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Tuesday", "2025-06-10", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Wednesday", "2025-06-11", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Thursday", "2025-06-12", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Friday", "2025-06-13", "08:00", "18:00", 30.0, 9.5, 35.0, 39.08, "the shift has been authorised but haven't come out on the report", 371.26, 38.76, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Saturday", "2025-06-14", "08:00", "08:00", 0.0, 24.0, 22.0, 39.08, "the shift has been authorised but haven't come out on the report", 937.92, 409.92, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Sunday", "2025-06-15", "08:00", "07:45", 0.0, 23.45, 22.0, 39.08, "the shift has been authorised but haven't come out on the report", 916.43, 400.53, "Clarity"], ["Maudy Hoyi", "Ramsey Springfield Hospital", "Wednesday", "2025-06-11", "07:30", "19:30", 30.0, 11.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 499.79, 39.79, "Retinue"], ["Maudy Hoyi", "Ramsey Springfield Hospital", "Wednesday", "2025-06-18", "08:30", "19:00", 30.0, 10.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 434.6, 34.6, "Retinue"], ["Maudy Hoyi", "Ramsey Springfield Hospital", "Thursday", "2025-06-19", "07:30", "13:00", 0.0, 5.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 239.03, 19.03, "Retinue"], ["Maudy Hoyi", "Ramsey Springfield Hospital", "Friday", "2025-06-20", "12:00", "20:00", 30.0, 7.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 325.95, 25.95, "Retinue"], ["Maudy Hoyi", "Ramsey Springfield Hospital", "Saturday", "2025-06-21", "07:30", "14:30", 30.0, 6.5, 44.0, 45.95, "the shift has been authorised but haven't come out on the report", 298.68, 12.68, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-06-16", "08:00", "17:30", 30.0, 9.0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 448.47, 34.47, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-06-17", "08:00", "18:00", 30.0, 9.5, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 502.74, 27.74, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-06-20", "08:00", "15:15", 30.0, 8.45, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 447.17, 24.67, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Tuesday", "2025-06-17", "12:30", "18:00", 30.0, 5.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 239.03, 19.03, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Wednesday", "2025-06-18", "07:30", "16:45", 30.0, 8.75, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 436.01, 51.01, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Thursday", "2025-06-19", "07:30", "21:00", 30.0, 13.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 564.98, 44.98, "Retinue"], ["Diosdado B Wagan", "North Downs Hospital", "Friday", "2025-06-20", "07:30", "17:00", 30.0, 9.0, 44.0, 49.83, "the shift has been authorised but haven't come out on the report", 448.47, 52.47, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Monday", "2025-06-16", "09:00", "18:15", 30.0, 8.75, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 380.28, 30.28, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Tuesday", "2025-06-17", "08:30", "18:15", 30.0, 9.25, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 402.0, 32.0, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-06-18", "07:30", "20:45", 60.0, 12.25, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 532.38, 42.38, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-06-20", "07:30", "17:30", 30.0, 9.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 412.87, 32.87, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-06-23", "08:00", "18:45", 30.0, 0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 21.28, 1.64, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-06-26", "08:00", "17:00", 30.0, 0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 19.72, 1.52, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-06-27", "08:00", "16:45", 30.0, 0, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 17.13, 1.32, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Tuesday", "2025-06-24", "07:30", "20:30", 30.0, 12.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 543.25, 43.25, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-06-25", "08:30", "17:30", 30.0, 8.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 369.41, 29.41, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Thursday", "2025-06-26", "08:00", "18:30", 30.0, 10.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 434.6, 34.6, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-06-27", "08:30", "17:15", 30.0, 8.25, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 358.55, 28.55, "Retinue"], ["Willard Mandaza", "Medway", "Wednesday", "2025-06-25", "08:00", "18:00", 30.0, 9.5, 27.0, 32.0, "the shift has been authorised but haven't come out on the report", 304.0, 47.5, "HR"], ["Shauna Henderson-Rose", "Ramsay Rivers hospital", "Saturday", "2025-06-21", "07:30", "14:00", 0.0, 6.5, 52.0, 54.16, "the shift has been authorised but haven't come out on the report", 352.04, 14.04, "Retinue"], ["Shauna Henderson-Rose", "Ramsay Rivers hospital", "Tuesday", "2025-06-24", "07:30", "16:30", 30.0, 8.5, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 449.82, 24.82, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-06-30", "08:00", "13:45", 0.0, 5.45, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 271.57, 20.87, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-07-01", "08:00", "16:00", 30.0, 7.5, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 373.72, 28.72, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-07-02", "08:00", "17:00", 30.0, 8.5, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 449.82, 24.82, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-07-03", "08:00", "17:15", 30.0, 8.45, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 421.06, 32.36, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Monday", "2025-06-30", "08:00", "19:45", 30.0, 11.25, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 488.93, 38.93, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Tuesday", "2025-07-01", "08:45", "20:15", 30.0, 11.0, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 478.06, 38.06, "Retinue"], ["Consuelo Johnson", "Pinehill Hospital", "Monday", "2025-07-07", "12:30", "18:30", 0.0, 6.0, 34.0, 43.46, "the shift has been authorised but haven't come out on the report", 260.76, 56.76, "Retinue"], ["Consuelo Johnson", "Pinehill Hospital", "Friday", "2025-07-11", "08:00", "16:30", 30.0, 8.0, 34.0, 43.46, "the shift has been authorised but haven't come out on the report", 347.68, 75.68, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-07-07", "08:00", "17:45", 30.0, 9.15, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 455.94, 35.04, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-07-10", "08:00", "16:45", 30.0, 8.15, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 406.11, 31.21, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-07-11", "08:00", "17:00", 30.0, 8.5, 46.0, 49.83, "the shift has been authorised but haven't come out on the report", 423.56, 32.56, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Thursday", "2025-07-10", "08:30", "17:30", 30.0, 8.5, 40.0, 43.46, "the shift has been authorised but haven't come out on the report", 369.41, 29.41, "Retinue"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Saturday", "2025-06-21", "00:00", "00:00", 0.0, 24.0, 22.0, 39.08, "the shift has been authorised but haven't come out on the report", 937.92, 409.92, "Clarity"], ["Lydie Gam-mackitta", "UHBW - Bristol Royal Infirmary", "Sunday", "2025-06-22", "00:00", "00:00", 0.0, 24.0, 22.0, 39.08, "the shift has been authorised but haven't come out on the report", 937.92, 409.92, "Clarity"], ["Shauna Henderson-Rose", "Ramsay Rivers hospital", "Thursday", "2024-07-04", "07:30", "18:00", 30.0, 10.0, 45.0, 49.83, "the shift has been authorised but haven't come out on the report", 498.3, 48.3, "Retinue"], ["Shauna Henderson-Rose", "Ramsay Rivers hospital", "Tuesday", "2025-07-08", "07:45", "19:30", 30.0, 11.25, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 595.35, 32.85, "Retinue"], ["Shauna Henderson-Rose", "Ramsay Rivers hospital", "Friday", "2025-07-11", "07:30", "18:00", 30.0, 10.0, 50.0, 52.92, "the shift has been authorised but haven't come out on the report", 529.2, 29.2, "Retinue"], ["Shauna Henderson-Rose", "Ramsay Rivers hospital", "Saturday", "2025-07-12", "07:30", "15:00", 0.0, 7.5, 52.0, 54.16, "the shift has been authorised but haven't come out on the report", 406.2, 16.2, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-07-22", "07:30", "17:30", 30.0, 9.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 482.6, 102.6, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-07-24", "07:30", "19:15", 30.0, 11.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 571.5, 121.5, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Friday", "2025-07-25", "07:30", "19:30", 30.0, 11.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 584.2, 124.2, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-07-26", "07:30", "18:00", 30.0, 10.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 508.0, 108.0, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Friday", "2025-07-25", "20:00", "22:00", 0.0, 2.0, 38.0, 50.54, "the shift has been authorised but haven't come out on the report", 101.08, 25.08, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-07-26", "20:00", "21:00", 0.0, 1.0, 38.0, 50.54, "the shift has been authorised but haven't come out on the report", 50.54, 12.54, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Monday", "2025-07-28", "07:30", "18:30", 30.0, 10.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 533.4, 113.4, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-07-29", "07:30", "10:45", 0.0, 0.03, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 1.27, 0.27, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Wednesday", "2025-07-30", "13:00", "18:00", 0.0, 5.0, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 221.0, 48.5, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-07-31", "07:30", "17:00", 0.0, 9.0, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 397.8, 87.3, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-07-21", "08:00", "16:45", 30.0, 8.15, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 414.02, 88.02, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-07-22", "08:00", "17:45", 30.0, 9.15, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 464.82, 98.82, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-07-23", "08:00", "16:30", 30.0, 8.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 406.4, 86.4, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-07-28", "08:00", "18:15", 30.0, 9.45, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 510.3, 103.95, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-07-29", "08:00", "17:00", 30.0, 8.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 431.8, 91.8, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-07-30", "08:00", "17:15", 30.0, 8.45, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 456.3, 92.95, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-07-18", "07:30", "19:30", 30.0, 11.5, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 508.3, 111.55, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-07-23", "08:30", "18:30", 30.0, 9.5, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 419.9, 92.15, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-07-25", "08:00", "19:30", 30.0, 11.0, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 486.2, 106.7, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-08-01", "08:30", "19:45", 30.0, 0, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 19.8, 4.34, "Retinue"], ["Tamara Boswell", "Royal london hospital", "Friday", "2025-08-01", "08:00", "18:00", 30.0, 9.5, 26.72, 32.8, "the shift has not come over on the report/ followed up with the trust", 311.6, 57.76, "HR"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-08-04", "08:00", "18:15", 30.0, 9.45, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 480.06, 102.06, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-08-05", "08:00", "18:00", 30.0, 9.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 482.6, 102.6, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-08-06", "08:00", "16:45", 30.0, 8.15, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 414.02, 88.02, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-08-07", "08:00", "17:00", 30.0, 8.5, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 459.0, 93.5, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-08-05", "12:30", "20:30", 0.0, 8.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 406.4, 86.4, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-08-06", "08:30", "16:15", 30.0, 7.25, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 320.45, 70.33, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-08-08", "07:30", "17:45", 30.0, 9.75, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 430.95, 94.58, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Monday", "2025-08-04", "07:30", "21:00", 30.0, 13.0, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 592.93, 150.93, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Friday", "2025-08-08", "12:00", "20:30", 0.0, 8.5, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 387.69, 98.69, "Retinue"], ["Penelope Piccio", "Spire Dunedin Hospital", "Saturday", "2025-08-09", "07:30", "19:00", 30.0, 11.0, 8.5, 51.99, "the shift has been authorised but haven't come out on the report", 571.89, 478.39, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-08-11", "08:00", "17:15", 30.0, 8.45, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 429.26, 91.26, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-08-12", "08:00", "17:45", 30.0, 9.15, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 464.82, 98.82, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-08-14", "08:00", "16:00", 30.0, 7.5, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 405.0, 82.5, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-08-15", "08:00", "17:15", 30.0, 8.45, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 429.26, 91.26, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Friday", "2025-08-15", "07:30", "12:45", 0.0, 5.25, 34.5, 42.2, "the shift has been authorised but haven't come out on the report", 221.55, 40.43, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-08-15", "08:00", "12:45", 0.0, 4.75, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 209.95, 46.08, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Saturday", "2025-08-16", "08:30", "14:05", 30.0, 5.5, 35.5, 44.2, "the shift has been authorised but haven't come out on the report", 243.1, 47.85, "Retinue"], ["Shauna Henderson-Rose", "Ramsay Rivers", "Monday", "2025-07-28", "09:30", "19:00", 30.0, 9.0, 43.05, 54.0, "the shift has been authorised but haven't come out on the report", 486.0, 98.55, "Retinue"], ["Shauna Henderson-Rose", "Ramsay Rivers", "Tuesday", "2025-07-29", "07:30", "18:00", 30.0, 10.0, 43.02, 54.0, "the shift has been authorised but haven't come out on the report", 540.0, 109.8, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-08-18", "08:00", "17:30", 30.0, 9.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 457.2, 97.2, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-08-19", "08:00", "17:15", 30.0, 9.15, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 464.82, 98.82, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-08-20", "08:00", "17:30", 30.0, 9.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 457.2, 97.2, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-08-21", "08:00", "15:00", 30.0, 6.5, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 351.0, 71.5, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-08-20", "07:30", "18:15", 30.0, 10.25, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 453.05, 99.43, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Friday", "2025-08-22", "08:00", "17:30", 30.0, 9.0, 35.5, 44.2, "the shift has been authorised but haven't come out on the report", 397.8, 78.3, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Monday", "2025-08-18", "07:30", "20:00", 30.0, 12.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 609.6, 129.6, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-08-19", "07:30", "19:00", 30.0, 11.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 558.8, 118.8, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-08-21", "07:30", "18:30", 30.0, 10.5, 34.5, 42.2, "the shift has been authorised but haven't come out on the report", 443.1, 80.85, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-08-23", "07:30", "17:45", 30.0, 9.75, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 495.3, 105.3, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Tuesday", "2025-08-19", "07:30", "19:30", 30.0, 11.5, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 524.51, 133.51, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Wednesday", "2025-08-20", "07:30", "18:30", 30.0, 10.5, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 478.9, 121.9, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Thursday", "2025-08-21", "07:30", "19:00", 30.0, 11.0, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 501.71, 127.71, "Retinue"], ["Maudy Hoyi", "Ramsay Springfield", "Monday", "2025-08-18", "09:00", "14:00", 0.0, 5.0, 34.5, 44.36, "Shift is due to be paid this week, but should have been paid last week", 221.8, 49.3, "Retinue"], ["Maudy Hoyi", "Ramsay Springfield", "Thursday", "2025-08-07", "12:00", "19:30", 30.0, 7.0, 34.5, 44.36, "Shift is due to be paid this week, but should have been paid last week", 310.52, 69.02, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-08-27", "08:00", "17:00", 30.0, 0, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 18.19, 3.7, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-08-28", "08:00", "16:00", 30.0, 0, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 15.94, 3.25, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-08-29", "08:00", "16:45", 30.0, 0, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 18.56, 3.78, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Wednesday", "2025-08-27", "07:30", "20:00", 30.0, 12.0, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 547.32, 139.32, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Thursday", "2025-08-28", "07:30", "19:30", 30.0, 11.5, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 524.51, 133.51, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-04-09", "08:00", "15:00", 30.0, 6.5, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 351.0, 71.5, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-05-09", "08:00", "17:45", 30.0, 9.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 469.9, 99.9, "Retinue"], ["Roseline Emmanuel", "Royal Surrey", "Saturday", "2025-08-09", "08:00", "18:00", 30.0, 9.5, 30.0, 33.5, "the shift has been authorised but haven't come out on the report", 318.25, 33.25, "Roster"], ["Roseline Emmanuel", "Royal Surrey", "Tuesday", "2025-09-09", "08:00", "18:30", 30.0, 10.0, 30.0, 33.5, "the shift has been authorised but haven't come out on the report", 335.0, 35.0, "Roster"], ["Roseline Emmanuel", "Royal Surrey", "Thursday", "2025-10-09", "08:00", "18:00", 30.0, 9.5, 30.0, 33.5, "the shift has been authorised but haven't come out on the report", 318.25, 33.25, "Roster"], ["Roseline Emmanuel", "Royal Surrey", "Sunday", "2025-11-09", "08:00", "20:45", 45.0, 12.0, 30.0, 33.5, "the shift has been authorised but haven't come out on the report", 402.0, 42.0, "Roster"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-09-08", "08:00", "17:45", 30.0, 9.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 469.9, 99.9, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-09-09", "08:00", "18:00", 30.0, 9.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 482.6, 102.6, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-09-11", "08:00", "17:45", 30.0, 9.25, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 499.5, 101.75, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Wednesday", "2025-09-10", "07:30", "18:15", 30.0, 10.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 520.7, 110.7, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-09-11", "07:30", "20:00", 30.0, 12.0, 34.5, 42.2, "the shift has been authorised but haven't come out on the report", 506.4, 92.4, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Tuesday", "2025-09-09", "07:30", "16:45", 30.0, 8.75, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 386.75, 84.88, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-09-10", "09:00", "17:00", 30.0, 7.5, 35.5, 0, "the shift has been authorised but haven't come out on the report", 331.5, 65.25, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-09-20", "07:30", "18:00", 30.0, 10.0, 35.5, 45.4, "the shift has been authorised but haven't come out on the report", 454.0, 99.0, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-09-16", "08:30", "17:15", 30.0, 8.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 419.1, 89.1, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Wednesday", "2025-09-17", "08:15", "13:30", 0.0, 5.25, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 232.05, 50.93, "Retinue"], ["Consuelo Johnson", "Ramsay pinehill Hospital", "Monday", "2025-09-08", "08:00", "18:30", 30.0, 10.0, 34.0, 44.2, "the shift has been authorised but haven't come out on the report", 442.0, 102.0, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-09-19", "08:00", "16:30", 30.0, 8.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 406.4, 86.4, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-09-22", "08:00", "16:00", 30.0, 7.5, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 405.0, 82.5, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-09-23", "08:00", "18:00", 30.0, 9.5, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 513.0, 104.5, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-09-26", "08:00", "17:45", 30.0, 9.25, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 499.5, 101.75, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-09-27", "07:30", "18:00", 30.0, 10.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 508.0, 108.0, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Monday", "2025-09-22", "07:30", "20:00", 30.0, 12.0, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 547.32, 139.32, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Thursday", "2025-09-25", "07:30", "19:00", 30.0, 11.0, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 501.71, 127.71, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-09-29", "08:00", "15:45", 30.0, 7.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 368.3, 78.3, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-10-03", "08:00", "16:00", 30.0, 7.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 381.0, 81.0, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-10-02", "08:00", "17:00", 30.0, 8.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 431.8, 91.8, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Friday", "2025-10-03", "07:30", "16:15", 30.0, 8.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 419.1, 89.1, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-10-04", "07:30", "13:00", 0.0, 5.5, 42.0, 52.1, "the shift has been authorised but haven't come out on the report", 286.55, 55.55, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Tuesday", "2025-09-30", "07:30", "20:15", 60.0, 11.75, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 615.82, 134.07, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Thursday", "2025-10-02", "07:45", "18:30", 30.0, 10.25, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 537.2, 116.95, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Saturday", "2025-10-04", "07:00", "17:30", 30.0, 10.0, 42.0, 53.7, "the shift has been authorised but haven't come out on the report", 537.0, 117.0, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-10-07", "07:30", "18:30", 30.0, 10.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 533.4, 113.4, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Wednesday", "2025-10-08", "07:30", "18:00", 30.0, 10.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 508.0, 108.0, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-10-09", "07:00", "17:30", 30.0, 10.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 508.0, 108.0, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Friday", "2025-10-10", "07:30", "14:15", 0.0, 6.75, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 342.9, 72.9, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-10-11", "07:30", "16:00", 15.0, 8.25, 42.0, 52.1, "the shift has been authorised but haven't come out on the report", 429.82, 83.32, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-10-06", "08:00", "18:00", 30.0, 9.5, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 513.0, 104.5, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Saturday", "2025-10-11", "07:30", "19:00", 30.0, 11.0, 35.5, 45.72, "the shift has been authorised but haven't come out on the report", 502.92, 112.42, "Retinue"], ["Jovanie Santos", "Ramsey North Downs", "Tuesday", "2025-10-14", "08:30", "18:00", 30.0, 9.0, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 397.8, 87.3, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-10-13", "08:00", "17:45", 30.0, 9.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 469.9, 99.9, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-10-15", "08:00", "17:30", 30.0, 9.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 457.2, 97.2, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-10-16", "08:00", "17:30", 30.0, 9.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 457.2, 97.2, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-10-16", "08:00", "20:30", 30.0, 12.0, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 530.4, 116.4, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-10-18", "07:30", "15:00", 15.0, 7.25, 35.5, 45.4, "the shift has been authorised but haven't come out on the report", 329.15, 71.77, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Friday", "2025-10-17", "07:30", "20:30", 30.0, 12.5, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 570.12, 145.12, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Saturday", "2025-10-18", "07:30", "17:30", 30.0, 9.5, 35.5, 45.72, "the shift has been authorised but haven't come out on the report", 434.34, 97.09, "Retinue"], ["Lena O'Leary", "Spa Medica", "Thursday", "2025-09-25", "07:30", "17:30", 30.0, 9.5, 40.0, 45.0, "the shift has been authorised but haven't come out on the pulse report", 427.5, 47.5, "Pulse"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-10-21", "08:00", "16:45", 30.0, 8.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 419.1, 89.1, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-10-23", "08:00", "17:30", 30.0, 9.0, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 486.0, 99.0, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-10-24", "08:00", "17:15", 30.0, 8.75, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 444.5, 94.5, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-10-23", "07:30", "18:00", 30.0, 10.0, 34.5, 44.2, "the shift has been authorised but haven't come out on the report", 442.0, 97.0, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-10-25", "09:30", "18:45", 30.0, 8.75, 42.0, 52.1, "the shift has been authorised but haven't come out on the report", 455.88, 88.38, "Retinue"], ["Amber Asif", "Spire Gatwick Park Hospital", "Friday", "2025-10-24", "07:30", "17:00", 30.0, 9.0, 34.0, 45.61, "the shift has been authorised but haven't come out on the report", 410.49, 104.49, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Monday", "2025-10-20", "07:30", "20:30", 60.0, 12.0, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 628.92, 136.92, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Tuesday", "2025-10-21", "07:30", "19:00", 30.0, 11.0, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 576.51, 125.51, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Wednesday", "2025-10-22", "07:30", "21:00", 60.0, 12.5, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 655.12, 142.62, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Thursday", "2025-10-23", "13:00", "20:00", 30.0, 6.5, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 340.67, 74.17, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Saturday", "2025-10-25", "07:30", "16:45", 30.0, 8.75, 42.0, 53.7, "the shift has been authorised but haven't come out on the report", 469.88, 102.38, "Retinue"], ["Shauna Henderson rose", "Ramsay oaks hospital", "Sunday", "2025-10-26", "07:30", "19:00", 30.0, 11.0, 44.29, 56.56, "the shift has been authorised but haven't come out on the report", 622.16, 134.97, "Retinue"], ["Maudy Hoyi", "Ramsay Springfield Hospital", "Friday", "2025-10-24", "10:00", "19:00", 30.0, 8.5, 34.5, 44.36, "the shift has been authorised but haven't come out on the report", 377.06, 83.81, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Monday", "2025-10-27", "09:00", "16:00", 30.0, 6.5, 30.5, 44.2, "the shift has been authorised but haven't come out on the report", 287.3, 89.05, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-10-30", "08:00", "19:30", 30.0, 11.0, 30.5, 44.2, "the shift has been authorised but haven't come out on the report", 486.2, 150.7, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-10-27", "08:00", "17:45", 30.0, 9.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 469.9, 99.9, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Tuesday", "2025-10-28", "08:00", "15:00", 0, 7.0, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 378.0, 77.0, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2025-10-29", "08:00", "17:15", 30.0, 8.75, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 444.5, 94.5, "Retinue"], ["Roseline Ogenekevbe Emmanuel", "Royal surrey", "Monday", "2025-11-03", "08:00", "19:30", 30.0, 11.0, 30.0, 32.0, "the shift has been authorised but haven't come out on the report", 352.0, 22.0, "Retinue"], ["Roseline Ogenekevbe Emmanuel", "Royal surrey", "Tuesday", "2025-11-04", "08:00", "18:30", 30.0, 10.0, 30.0, 32.0, "the shift has been authorised but haven't come out on the report", 320.0, 20.0, "Retinue"], ["Roseline Ogenekevbe Emmanuel", "Royal surrey", "Wednesday", "2025-11-05", "08:00", "19:00", 30.0, 10.5, 30.0, 32.0, "the shift has been authorised but haven't come out on the report", 336.0, 21.0, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Thursday", "2025-10-30", "07:30", "13:30", 0.0, 6.0, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 314.46, 68.46, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Saturday", "2025-11-01", "07:00", "18:00", 30.0, 10.5, 42.0, 53.7, "the shift has been authorised but haven't come out on the report", 563.85, 122.85, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-11-04", "07:30", "19:00", 30.0, 11.0, 34.0, 44.58, "the shift has been authorised but haven't come out on the report", 490.38, 116.38, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Thursday", "2025-11-06", "07:30", "20:00", 30.0, 12.0, 34.0, 44.58, "the shift has been authorised but haven't come out on the report", 534.96, 126.96, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-11-08", "07:30", "16:30", 30.0, 8.5, 31.5, 45.95, "the shift has been authorised but haven't come out on the report", 390.58, 122.83, "Retinue"], ["Shauna Henderson rose", "Ramsay oaks hospital", "Wednesday", "2025-10-29", "13:00", "18:00", 0, 5.0, 44.29, 56.5, "the shift has been authorised but haven't come out on the report", 282.5, 61.05, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Monday", "2025-11-03", "07:45", "20:30", 60.0, 11.75, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 615.82, 134.07, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Tuesday", "2025-11-04", "07:30", "18:00", 30.0, 10.0, 41.0, 52.41, "the shift has been authorised but haven't come out on the report", 524.1, 114.1, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2025-11-03", "08:00", "16:30", 30.0, 8.0, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 432.0, 88.0, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2025-11-06", "08:00", "13:00", 0.0, 5.0, 43.0, 54.0, "the shift has been authorised but haven't come out on the report", 270.0, 55.0, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2025-11-07", "08:00", "17:45", 30.0, 9.25, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 469.9, 99.9, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Wednesday", "2025-11-12", "07:30", "19:00", 30.0, 11.0, 34.0, 44.58, "the shift has been authorised but haven't come out on the report", 490.38, 116.38, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-11-15", "07:30", "14:45", 0.0, 7.25, 35.0, 45.87, "the shift has been authorised but haven't come out on the report", 332.56, 78.81, "Retinue"], ["Alex Amponsah", "Southend University hospital", "Tuesday", "2025-11-18", "09:00", "19:20", 30.0, 9.83, 26.0, 23.32, "the shift has been authorised but haven't come out on the report", 229.31, -26.35, "HRoster"], ["Alex Amponsah", "Southend University hospital", "Wednesday", "2025-11-19", "08:00", "18:00", 30.0, 9.5, 26.0, 23.32, "the shift has been authorised but haven't come out on the report", 221.54, -25.46, "HRoster"], ["Alex Amponsah", "Southend University hospital", "Thursday", "2025-11-20", "08:00", "18:00", 30.0, 9.5, 26.0, 23.32, "the shift has been authorised but haven't come out on the report", 221.54, -25.46, "HRoster"], ["Alex Amponsah", "Southend University hospital", "Friday", "2025-11-21", "08:00", "18:00", 30.0, 9.5, 26.0, 23.32, "the shift has been authorised but haven't come out on the report", 221.54, -25.46, "HRoster"], ["Diosdado B Wagan", "Ramsey North Downs", "Wednesday", "2025-11-12", "08:00", "21:30", 30.0, 13.0, 30.5, 44.2, "the shift has been authorised but haven't come out on the report", 574.6, 178.1, "Retinue"], ["Roseline Emmanuel", "Royal surrey", "Monday", "2025-11-24", "08:00", "18:00", 30.0, 9.5, 30.0, 32.0, "the shift has been authorised but haven't come out on the report", 304.0, 19.0, "HRoster"], ["Roseline Emmanuel", "Royal surrey", "Tuesday", "2025-11-25", "08:00", "20:45", 45.0, 12.0, 30.0, 32.0, "the shift has been authorised but haven't come out on the report", 384.0, 24.0, "HRoster"], ["Roseline Emmanuel", "Royal surrey", "Wednesday", "2025-11-26", "08:00", "19:30", 30.0, 11.0, 30.0, 32.0, "the shift has been authorised but haven't come out on the report", 352.0, 22.0, "HRoster"], ["Roseline Emmanuel", "Royal surrey", "Thursday", "2025-11-27", "08:00", "20:45", 45.0, 12.0, 30.0, 32.0, "the shift has been authorised but haven't come out on the report", 384.0, 24.0, "HRoster"], ["Diosdado B Wagan", "Ramsey North Downs", "Tuesday", "2025-12-09", "07:30", "19:45", 30.0, 11.75, 34.0, 44.58, "the shift has been authorised but haven't come out on the report", 523.81, 124.31, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Friday", "2025-12-12", "08:00", "19:00", 30.0, 10.5, 30.5, 44.2, "the shift has been authorised but haven't come out on the report", 464.1, 143.85, "Retinue"], ["Diosdado B Wagan", "Ramsey North Downs", "Saturday", "2025-12-13", "08:00", "17:45", 30.0, 9.25, 31.5, 45.62, "the shift has been authorised but haven't come out on the report", 421.99, 130.61, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Thursday", "2025-12-11", "13:00", "19:30", 30.0, 6.0, 41.0, 52.41, "the shift has been invoiced on the system but haven't come out on the report", 314.46, 68.46, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Friday", "2025-12-12", "07:45", "18:30", 30.0, 10.25, 41.0, 52.41, "the shift has been invoiced on the system but haven't come out on the report", 537.2, 116.95, "Retinue"], ["Dinah Baluyot", "Clementine Churchill Hospital", "Saturday", "2025-12-13", "07:30", "20:30", 60.0, 12.0, 42.0, 53.7, "the shift has been invoiced on the system but haven't come out on the report", 644.4, 140.4, "Retinue"], ["Diosdado Wagan", "Ramsey North Downs", "Friday", "2025-12-19", "07:30", "16:15", 15.0, 8.5, 30.5, 44.2, "the shift has been invoiced on the system but haven't come out on the report", 375.7, 116.45, "Retinue"], ["Diosdado Wagan", "Ramsey North Downs", "Monday", "2025-12-22", "07:30", "19:00", 30.0, 11.0, 34.0, 44.58, "the shift has been authorised but haven't come out on the report", 490.38, 116.38, "Retinue"], ["Joshua Tanimowo", "Ramsey North Downs", "Tuesday", "2025-12-16", "08:00", "13:30", 0.0, 5.5, 30.0, 44.2, "the shift has been authorised but haven't come out on the report", 243.1, 78.1, "Retinue"], ["Joshua Tanimowo", "Ramsey North Downs", "Saturday", "2025-12-20", "07:30", "15:45", 15.0, 8.0, 30.0, 45.62, "the shift has been authorised but haven't come out on the report", 364.96, 124.96, "Retinue"], ["Edward Brooks", "Spa medica", "Monday", "2026-01-05", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Edward Brooks", "Spa medica", "Tuesday", "2026-01-06", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Jovanie Santos", "Ramsey North Downs", "Monday", "2025-01-06", "08:00", "19:45", 30.0, 11.25, 30.5, 44.2, "the shift has been authorised but haven't come out on the report", 497.25, 154.13, "Retinue"], ["Alex Amponsah", "Southend University hospital", "Monday", "2026-01-05", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Tuesday", "2026-01-06", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Wednesday", "2026-01-07", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Thursday", "2026-01-08", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Friday", "2026-01-09", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Monday", "2026-01-05", "08:00", "18:00", 30.0, 9.5, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 482.6, 102.6, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Thursday", "2026-01-08", "08:00", "17:15", 30.0, 8.75, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 444.5, 94.5, "Retinue"], ["Sandra Duarte-Botello", "The Cherwell Hospital", "Friday", "2026-01-09", "08:00", "17:30", 30.0, 9.0, 40.0, 50.8, "the shift has been authorised but haven't come out on the report", 457.2, 97.2, "Retinue"], ["Alex Amponsah", "Southend University hospital", "Monday", "2026-01-12", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Tuesday", "2026-01-13", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Wednesday", "2026-01-14", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Thursday", "2026-01-15", "08:00", "18:00", 45.0, 9.25, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 268.06, 27.56, "H roster"], ["Alex Amponsah", "Southend University hospital", "Friday", "2026-01-16", "08:00", "13:00", 0.0, 5.0, 26.0, 28.98, "the shift has been authorised but haven't come out on the report", 144.9, 14.9, "H roster"], ["Jovanie Santos", "Ramsey North Downs", "Thursday", "2026-01-15", "08:15", "19:15", 30.0, 10.5, 30.5, 44.2, "the shift has been authorised but haven't come out on the report", 464.1, 143.85, "Retinue"], ["Paula Ibanez Ballester", "Spire Wellesley", "Wednesday", "2026-01-28", "12:30", "19:00", 0.0, 6.5, 36.0, 48.52, "the shift has been authorised but haven't come out on the report", 315.38, 81.38, "Retinue"], ["Alex Amponsah", "Southend University hospital", "Tuesday", "2026-02-03", "08:00", "18:00", 45.0, 9.25, 26.0, 28.97, "the shift has been authorised but haven't come out on the report", 267.97, 27.47, "Roster"], ["Lydie Gam-mackitta", "Spa medica", "Tuesday", "2026-02-03", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Lydie Gam-mackitta", "Spa medica", "Monday", "2026-02-09", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Lydie Gam-mackitta", "Spa medica", "Monday", "2026-02-16", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Lydie Gam-mackitta", "Spa medica", "Tuesday", "2026-02-17", "07:30", "19:00", 30.0, 11.0, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 485.1, 110.0, "Pulse"], ["Lydie Gam-mackitta", "Spa medica", "Wednesday", "2026-02-18", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Lydie Gam-mackitta", "Spa medica", "Thursday", "2026-02-19", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Lydie Gam-mackitta", "Spa medica", "Friday", "2026-02-20", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Jonathan Antonio Montoya Rendon", "Spa medica", "Tuesday", "2026-02-17", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Jonathan Antonio Montoya Rendon", "Spa medica", "Wednesday", "2026-02-18", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Jonathan Antonio Montoya Rendon", "Spa medica", "Thursday", "2026-02-19", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Jonathan Antonio Montoya Rendon", "Spa medica", "Friday", "2026-02-20", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Edward Brooks", "Spa medica", "Monday", "2026-02-16", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Edward Brooks", "Spa medica", "Tuesday", "2026-02-17", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Edward Brooks", "Spa medica", "Wednesday", "2026-02-18", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Lydie Gam-mackitta", "Spa medica", "Saturday", "2026-02-21", "07:30", "17:30", 30.0, 9.5, 34.1, 44.1, "the shift has been authorised but haven't come out on the report", 418.95, 95.0, "Pulse"], ["Sandra Maria Duarte-Botello", "The Cherwell Hospital", "Friday", "2026-02-20", "08:00", "18:15", 30.0, 9.75, 31.5, 41.99, "the shift has been authorised but haven't come out on the report", 409.4, 102.28, "Retinue"], ["Christopher Bwalya", "Southend University hospital", "Monday", "2026-02-23", "08:00", "18:00", 30.0, 9.5, 20.0, 23.32, "the shift has been authorised but haven't come out on the report", 221.54, 31.54, "H roster"], ["Christopher Bwalya", "Southend University hospital", "Tuesday", "2026-02-24", "08:00", "18:00", 30.0, 9.5, 20.0, 23.32, "the shift has been authorised but haven't come out on the report", 221.54, 31.54, "H roster"], ["Christopher Bwalya", "Southend University hospital", "Friday", "2026-02-27", "08:00", "18:00", 30.0, 9.5, 20.0, 23.32, "the shift has been authorised but haven't come out on the report", 221.54, 31.54, "H roster"], ["Roseline Ogenekevbe Emmanuel", "Southend University hospital", "Wednesday", "2026-03-11", "08:00", "18:30", 30.0, 10.0, 28.0, 28.98, "the shift has been authorised but haven't come out on the report", 289.8, 9.8, "H roster"], ["Roseline Ogenekevbe Emmanuel", "Southend University hospital", "Thursday", "2026-03-12", "08:00", "18:00", 30.0, 9.5, 28.0, 28.98, "the shift has been authorised but haven't come out on the report", 275.31, 9.31, "H roster"], ["Roseline Ogenekevbe Emmanuel", "Southend University hospital", "Friday", "2026-03-13", "08:00", "18:00", 30.0, 9.5, 28.0, 28.98, "the shift has been authorised but haven't come out on the report", 275.31, 9.31, "H roster"], ["Roseline Ogenekevbe Emmanuel", "Homerton", "Saturday", "2026-03-14", "08:00", "18:00", 30.0, 9.5, 32.0, 37.91, "the shift has been authorised but haven't come out on the report", 360.14, 56.14, "H roster"], ["Sandra Maria Duarte-Botello", "The Cherwell Hospital", "Wednesday", "2026-03-04", "08:00", "18:00", 30.0, 9.5, 38.0, 47.36, "the shift has been authorised but haven't come out on the report", 449.92, 88.92, "Retinue"]];
var poEdits=[];
try{var _po=localStorage.getItem('po_edits');if(_po)poEdits=JSON.parse(_po);}catch(e){}
function savePO(){try{localStorage.setItem('po_edits',JSON.stringify(poEdits));}catch(e){}}
function getAllPO(){return PO_BASE.concat(poEdits);}
var poFilter={hospital:'',day:'',q:'',charged:''};
var poPage=0;
var PO_PAGE_SIZE=50;

function fmtDateDMY(s){
if(!s)return'';
var p=s.split('-');
if(p.length!==3)return s;
return p[2]+'/'+p[1]+'/'+p[0];
}


function poCalc(){
// Calculate total hours from start/end/break, then charge and margin
var start=document.getElementById('po-start').value;
var end=document.getElementById('po-end').value;
var brk=parseFloat(document.getElementById('po-break').value)||0;
var pay=parseFloat(document.getElementById('po-payrate').value)||0;
var chg=parseFloat(document.getElementById('po-chgrate').value)||0;
var hrs=0;
if(start&&end){
var [sh,sm]=start.split(':').map(Number);
var [eh,em]=end.split(':').map(Number);
var totalMins=(eh*60+em)-(sh*60+sm)-brk;
if(totalMins<0)totalMins+=24*60; // overnight
hrs=Math.round(totalMins/60*100)/100;
}
var totalCharge=Math.round(hrs*chg*100)/100;
var margin=Math.round((chg-pay)*hrs*100)/100;
document.getElementById('po-hours-disp').textContent=hrs>0?hrs+'h':'--';
document.getElementById('po-charge-disp').textContent=totalCharge>0?'\u00a3'+totalCharge.toFixed(2):'--';
document.getElementById('po-margin-disp').textContent=margin!==0?'\u00a3'+margin.toFixed(2):'--';
document.getElementById('po-hours').value=hrs;
document.getElementById('po-charge').value=totalCharge;
document.getElementById('po-margin').value=margin;
}
function poCalcCharges(){poCalc();}

function poOnCandChange(){
var nameEl=document.getElementById('po-name');
var hospEl=document.getElementById('po-hospital');
var payEl=document.getElementById('po-payrate');
var chgEl=document.getElementById('po-chgrate');
if(!nameEl||!hospEl)return;
var val=nameEl.value.trim();
if(!val)return;

// Find candidate in C[]
var match=C.find(function(c){return c.n===val&&c.ac!=='Inactive';});
if(!match)return;

// \u2500\u2500 Hospital \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
// c.h may be raw spreadsheet value \u2014 find matching HC trust
var hospName='';
if(match.h){
// Try direct HC name match first
var directMatch=HC.find(function(h){return h.name===match.h;});
if(directMatch){
hospName=directMatch.name;
} else {
// Try getTrust fuzzy match
var trust=getTrust(match.h);
if(trust)hospName=trust;
else hospName=match.h; // fallback to raw value
}
}
if(hospName)hospEl.value=hospName;

// \u2500\u2500 Rates \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var hObj=HC.find(function(h){return h.name===hospName;})||{};
var ed=gHE(hospName);

// 1. Check personalised rate for this candidate at this hospital
var personalRates=(hObj.personalRates||[]).concat(ed.personalRates||[]);
var personal=personalRates.find(function(p){return p.name===match.n;});

if(personal&&personal.rate){
// Personalised pay rate exists \u2014 use it
if(payEl)payEl.value=personal.rate;
} else {
// 2. Use first standard rate card for this hospital (day pay rate)
var allRates=(hObj.rates||[]).concat(ed.rates||[]);
// Use selected rate card if configured, else first available
var selIdx=ed.selectedRate!=null?ed.selectedRate:-1;
var rateCard=selIdx>=0?allRates[selIdx]:allRates[0];
if(rateCard&&rateCard.pd){
if(payEl)payEl.value=rateCard.pd; // rate card
if(chgEl)chgEl.value=rateCard.cd||'';
} else if(match.r>0){
// 3. Fall back to candidate min rate
if(payEl)payEl.value=match.r;
}
}
poCalc();
}


function addPayOnly(){
var name=document.getElementById('po-name').value.trim();
var hosp=document.getElementById('po-hospital').value.trim();
var date=document.getElementById('po-date').value;
var start=document.getElementById('po-start').value;
var end=document.getElementById('po-end').value;
var brk=parseFloat(document.getElementById('po-break').value)||0;
var hrs=parseFloat(document.getElementById('po-hours').value)||0;
var pay=parseFloat(document.getElementById('po-payrate').value)||0;
var chg=parseFloat(document.getElementById('po-chgrate').value)||0;
var reason=document.getElementById('po-reason').value.trim();
var system=document.getElementById('po-system').value.trim();
var reqdate=document.getElementById('po-reqdate').value||'';
var totalCharge=parseFloat(document.getElementById('po-charge').value)||0;
var margin=parseFloat(document.getElementById('po-margin').value)||0;
if(!name){alert('Candidate name is required');return;}
if(!date){alert('Date is required');return;}
if(!hrs){alert('Please enter start and end times');return;}
// Day from date
var dayNames=['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
var parts=date.split('-');
var d=new Date(+parts[0],+parts[1]-1,+parts[2]);
var day=dayNames[d.getDay()];
var newRec=[name,hosp,day,date,start,end,brk,hrs,pay,chg,reason,totalCharge,margin,system,reqdate,''];
poEdits.push(newRec);
savePO();
// Show email button
poShowEmailBtn(newRec);
// Clear entry fields
document.getElementById('po-name').value='';
document.getElementById('po-date').value='';
document.getElementById('po-start').value='';
document.getElementById('po-end').value='';
document.getElementById('po-break').value='';
document.getElementById('po-payrate').value='';
document.getElementById('po-chgrate').value='';
document.getElementById('po-reason').value='';
var _d=new Date();
document.getElementById('po-reqdate').value=_d.getFullYear()+'-'+String(_d.getMonth()+1).padStart(2,'0')+'-'+String(_d.getDate()).padStart(2,'0');
document.getElementById('po-hours').value='';
document.getElementById('po-charge').value='';
document.getElementById('po-margin').value='';
document.getElementById('po-hours-disp').textContent='--';
document.getElementById('po-charge-disp').textContent='--';
document.getElementById('po-margin-disp').textContent='--';
poPage=0;
rPO();
}

function deletePO(idx){
if(!confirm('Delete this entry?'))return;
poEdits.splice(idx,1);
savePO();rPO();
}

function updatePOCharged(editIdx, val){
// val = YYYY-MM-DD or ''
if(editIdx<0||editIdx>=poEdits.length)return;
if(!poEdits[editIdx][15]&&poEdits[editIdx].length<16)poEdits[editIdx].push('');
poEdits[editIdx][15]=val;
savePO();
}


function poShowEmailBtn(rec){
var bar=document.getElementById('po-email-bar');
if(!bar)return;
bar.style.display='flex';
bar.dataset.rec=JSON.stringify(rec);
// Auto-hide after 60 seconds
clearTimeout(bar._hideTimer);
bar._hideTimer=setTimeout(function(){bar.style.display='none';},60000);
}

function poOpenEmail(){
var bar=document.getElementById('po-email-bar');
if(!bar)return;
var rec=JSON.parse(bar.dataset.rec||'[]');
if(!rec.length)return;
var name=rec[0]||'',hosp=rec[1]||'',day=rec[2]||'';
var date=rec[3]?fmtDateDMY(rec[3]):'';
var start=rec[4]||'',end5=rec[5]||'',brk=rec[6]||'',hrs=rec[7]||'';
var payRate=rec[8]||'',chgRate=rec[9]||'',reason=rec[10]||'';
var totalCharge=rec[11]?'\u00a3'+parseFloat(rec[11]).toFixed(2):'';
var margin=rec[12]?'\u00a3'+parseFloat(rec[12]).toFixed(2):'';
var system=rec[13]||'',reqdate=rec[14]?fmtDateDMY(rec[14]):'';
var nl='\n';
var subject='Pay Only Request - '+name+' - '+hosp+' - '+date;
var lines=[
'Pay Only Request',
'========================',
'',
'Candidate: '+name,
'Hospital: '+hosp,
'Date: '+date+' ('+day+')',
'Times: '+start+(end5?' - '+end5:'')+' | Break: '+brk+' mins',
'Hours: '+hrs+'h',
'Pay rate: \u00a3'+payRate+'/hr',
'Charge rate: \u00a3'+chgRate+'/hr',
'Total charge: '+totalCharge,
'Margin: '+margin
];
if(system)lines.push('System: '+system);
if(reqdate)lines.push('Request date: '+reqdate);
if(reason)lines.push('Reason: '+reason);
lines.push('','Please process. Thank you');
var body=lines.join(nl);
poShowEmailModal(subject,body);
}

function poShowEmailModal(subject,body){
var existing=document.getElementById('po-email-modal');
if(existing)existing.remove();
var modal=document.createElement('div');
modal.id='po-email-modal';
modal.style.cssText='position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:9999;display:flex;align-items:center;justify-content:center;padding:20px';
var subj_safe=subject.replace(/'/g,'\u0027');
var body_safe=body.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
modal.innerHTML='<div style="background:var(--su);border-radius:var(--rl);padding:20px;max-width:560px;width:100%;max-height:85vh;overflow-y:auto;box-shadow:0 8px 32px rgba(0,0,0,.25)">'
+'<div style="display:flex;align-items:center;margin-bottom:14px">'
+'<h3 style="flex:1;font-size:15px;font-weight:500">Pay Only Email</h3>'
+'<button id="po-modal-close" style="background:none;border:none;cursor:pointer;font-size:22px;color:var(--t2);line-height:1">&#215;</button>'
+'</div>'
+'<div style="margin-bottom:8px"><span style="font-size:11px;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">To</span>'
+'<div style="font-size:13px;font-weight:500;padding:5px 0">payonlyrequest@daywebster.com</div></div>'
+'<div style="margin-bottom:8px"><span style="font-size:11px;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Subject</span>'
+'<div style="font-size:13px;padding:6px 9px;background:var(--su2);border-radius:var(--r);margin-top:3px">'+subj_safe+'</div></div>'
+'<div style="margin-bottom:10px"><span style="font-size:11px;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Body</span>'
+'<textarea id="po-modal-body" readonly style="width:100%;height:200px;padding:8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su2);color:var(--tx);font-size:12px;font-family:monospace;resize:none;outline:none;box-sizing:border-box;margin-top:3px">'+body+'</textarea></div>'
+'<div style="display:flex;gap:8px">'
+'<button id="po-copy-btn" style="flex:1;padding:8px;background:var(--bl);color:#fff;border:none;border-radius:var(--r);cursor:pointer;font-size:13px;font-weight:500">Copy body</button>'
+'<button id="po-modal-close2" style="padding:8px 16px;background:transparent;border:0.5px solid var(--b2);border-radius:var(--r);cursor:pointer;font-size:13px;color:var(--t2)">Close</button>'
+'</div>'
+'</div>';
document.body.appendChild(modal);
document.getElementById('po-modal-close').onclick=function(){modal.remove();};
document.getElementById('po-modal-close2').onclick=function(){modal.remove();};
document.getElementById('po-copy-btn').onclick=function(){
var ta=document.getElementById('po-modal-body');
ta.select();
var ok=false;
try{ok=document.execCommand('copy');}catch(e){}
if(!ok&&navigator.clipboard)navigator.clipboard.writeText(ta.value).catch(function(){});
this.textContent='Copied \u2713';
this.style.background='var(--gr)';
var btn=this;
setTimeout(function(){btn.textContent='Copy body';btn.style.background='var(--bl)';},2000);
};
}


function rPO(){
var all=getAllPO();
var q=(poFilter.q||'').toLowerCase();
var hf=(poFilter.hospital||'').toLowerCase();
var df=(poFilter.day||'').toLowerCase();
var chf=(poFilter.charged||'');
var filtered=[];
all.forEach(function(r,i){
if(hf&&!(r[1]||'').toLowerCase().includes(hf))return;
if(df&&!(r[2]||'').toLowerCase().includes(df))return;
if(q&&!((r[0]||'')+(r[1]||'')+(r[10]||'')).toLowerCase().includes(q))return;
if(chf==='none'&&(i<PO_BASE.length||(r[15]&&r[15]!=='')))return;
filtered.push({r:r, origIdx:i});
});
// Stats
var totalCharge=filtered.reduce(function(s,o){return s+(o.r[11]||0);},0);
var totalMargin=filtered.reduce(function(s,o){return s+(o.r[12]||0);},0);
var totalHours=filtered.reduce(function(s,o){return s+(o.r[7]||0);},0);
var statsEl=document.getElementById('po-stats');
if(statsEl){
statsEl.innerHTML=
'<span><strong>'+filtered.length+'</strong> records</span>'
+'<span><strong>'+Math.round(totalHours)+'h</strong> total</span>'
+'<span>Charge: <strong style="color:var(--bl)">\u00a3'+totalCharge.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</strong></span>'
+'<span>Margin: <strong style="color:var(--grtx)">\u00a3'+totalMargin.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</strong></span>';
}

// Outstanding: user-added records with no date charged
var outstanding=poEdits.filter(function(r){return !r[15]||r[15]==='';});
var outPay=outstanding.reduce(function(s,r){return s+((r[8]||0)*(r[7]||0));},0);
var outCharge=outstanding.reduce(function(s,r){return s+(r[11]||0);},0);
var outEl=document.getElementById('po-outstanding');
if(outEl){
if(outstanding.length>0){
outEl.style.display='block';
var _isFiltered=poFilter.charged==='none';
var _btnStyle='margin-left:auto;padding:5px 14px;border:0.5px solid var(--am);border-radius:20px;cursor:pointer;font-size:12px;color:var(--amtx)';
outEl.innerHTML='<div style="display:flex;align-items:center;flex-wrap:wrap;gap:20px">'
+'<div><div style="font-size:11px;color:var(--amtx);text-transform:uppercase;letter-spacing:.05em;font-weight:500;margin-bottom:2px">Outstanding</div>'
+'<div style="font-size:12px;color:var(--t2)">'+outstanding.length+' shift'+(outstanding.length!==1?'s':'')+' not yet charged</div></div>'
+'<div style="height:36px;width:0.5px;background:var(--b2)"></div>'
+'<div><div style="font-size:10px;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:2px">Total pay (hrs \u00d7 rate)</div>'
+'<div style="font-size:20px;font-weight:500;color:var(--amtx)">\u00a3'+outPay.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</div></div>'
+'<div style="height:36px;width:0.5px;background:var(--b2)"></div>'
+'<div><div style="font-size:10px;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:2px">Total charge</div>'
+'<div style="font-size:20px;font-weight:500;color:var(--bl)">\u00a3'+outCharge.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</div></div>'
+'</div>';
// Add toggle button separately to avoid quote escaping issues
var _toggleBtn=document.createElement('button');
_toggleBtn.className='po-toggle-outstanding';
_toggleBtn.style.cssText=_btnStyle+';background:'+(_isFiltered?'var(--ambg)':'transparent');
_toggleBtn.textContent=_isFiltered?'\u2713 Showing outstanding \u2014 show all':'View outstanding';
outEl.querySelector('div').appendChild(_toggleBtn);
outEl.querySelectorAll('.po-toggle-outstanding').forEach(function(btn){
btn.addEventListener('click',function(){
poSetFilter('charged', poFilter.charged==='none'?'':'none');
});
});
} else {
outEl.style.display='none';
// Auto-clear the outstanding filter if no more outstanding records
if(poFilter.charged==='none'){
poFilter.charged='';
var cb=document.getElementById('po-clear-filter');
if(cb)cb.style.display='none';
// Re-run without recursion by resetting and letting current render complete
setTimeout(function(){rPO();},0);
}
}
}
// Pagination
// Sort most recent first
filtered.sort(function(a,b){
var da=a.r[3]||''; var db=b.r[3]||'';
return db.localeCompare(da);
});
var totalPages=Math.ceil(filtered.length/PO_PAGE_SIZE)||1;
if(poPage>=totalPages)poPage=totalPages-1;
var page=filtered.slice(poPage*PO_PAGE_SIZE,(poPage+1)*PO_PAGE_SIZE);
// Page controls
var pgEl=document.getElementById('po-pages');
if(pgEl){
pgEl.innerHTML='<span style="font-size:12px;color:var(--t2)">Page '+(poPage+1)+' of '+totalPages+'</span>'
+'<button onclick="if(poPage>0){poPage--;rPO();}" style="padding:3px 9px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">&#8592;</button>'
+'<button onclick="if(poPage<'+totalPages+'-1){poPage++;rPO();}" style="padding:3px 9px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">&#8594;</button>';
}
// Table
var tbody=document.getElementById('po-tbody');
if(!tbody)return;
if(!page.length){
tbody.innerHTML='<tr><td colspan="10" style="padding:24px;text-align:center;color:var(--t3)">No records match</td></tr>';
return;
}
tbody.innerHTML=page.map(function(o,si){
var r=o.r,editIdx=o.editIdx;
// dateCharged: poEdits=r[15], PO_BASE=r[16]
var _dc=editIdx>=0?(r[15]||''):(r[16]||'');
var ts=r[16]&&editIdx>=0?'<td style="padding:5px 4px;text-align:center"><a href="'+r[16]+'" target="_blank" style="font-size:15px;text-decoration:none">&#128196;</a></td>':'<td></td>';
var del=editIdx>=0?'<td style="padding:5px 0;text-align:right"><button class="delbtn po-del-btn" data-ei="'+editIdx+'">\u00d7</button></td>':'<td></td>';
var chgd=editIdx>=0
?'<td style="padding:5px 7px;font-size:12px"><input type="date" value="'+_dc+'" class="po-charged-inp" data-ei="'+editIdx+'" style="border:none;background:transparent;cursor:pointer;font-size:12px;color:var(--t2);outline:none"></td>'
:'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+(_dc?fmtDateDMY(_dc):'--')+'</td>';
return'<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 0;font-size:12px">'+fmtDateDMY(r[3])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;font-weight:500">'+esc(r[0])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+esc(r[1])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+r[2]+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+r[4]+' \u2013 '+r[5]+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right">'+((r[7]||0)+'h')+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right">\u00a3'+(r[8]||0).toFixed(2)+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right;color:var(--bl)">\u00a3'+(r[9]||0).toFixed(2)+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right;color:var(--grtx)">\u00a3'+(r[12]||0).toFixed(2)+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+esc(r[13]||'')+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+esc(r[10]||'')+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+fmtDateDMY(r[14]||'')+'</td>'
+chgd+ts+del
+'</tr>';
}).join('');
tbody.querySelectorAll('.po-del-btn').forEach(function(btn){
btn.addEventListener('click',function(){deletePO(+this.dataset.ei);});
});

}

function poSetFilter(k,v){
poFilter[k]=v;poPage=0;
var cb=document.getElementById('po-clear-filter');
if(cb)cb.style.display=poFilter.charged==='none'?'inline-block':'none';
rPO();
}

function populatePODatalists(){
// Auto-set request date to today
var rdEl=document.getElementById('po-reqdate');
if(rdEl&&!rdEl.value){
var d=new Date();
rdEl.value=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
}
var nl=document.getElementById('po-name-list');
if(nl)nl.innerHTML=C.filter(function(c){return c.ac!=='Inactive';})
.map(function(c){return '<option value="'+esc(c.n)+'"></option>';}).join('');
var hl=document.getElementById('po-hosp-list');
if(hl)hl.innerHTML=getAllTrustNames().map(function(n){return '<option value="'+esc(n)+'"></option>';}).join('');

var phf=document.getElementById('po-hosp-filter');
if(phf){
var hosps=[];
getAllPO().forEach(function(r){if(r[1]&&hosps.indexOf(r[1])<0)hosps.push(r[1]);});
hosps.sort();
phf.innerHTML='<option value="">All hospitals</option>'+
hosps.map(function(h){return '<option value="'+esc(h)+'">'+esc(h)+'</option>';}).join('');
}
}


// \u2500\u2500 ROSTER CHECK \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
// RC_HOSPITALS: [name, system, linkLabel, systemUrl]
var RC_HOSPITALS=[["Barts", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["Royal Surrey", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["East Surrey", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["Luton", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["Lewisham", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["Mid Essex", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["UCLH", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["Homerton", "HR", "Health Roster", "https://healthroster.allocate.cloud/"], ["Sussex", "HR", "", ""], ["Darent Valley", "HR", "", ""], ["RNOH", "HR", "", ""], ["Medway", "HR", "", ""], ["Watford", "NHSP", "NHSP", "https://bank.nhsprofessionals.nhs.uk/"], ["Royal Berkshire", "NHSP", "NHSP", "https://bank.nhsprofessionals.nhs.uk/"], ["East & North Herts", "NHSP", "NHSP", "https://bank.nhsprofessionals.nhs.uk/"], ["Croydon", "NHSP", "NHSP", "https://bank.nhsprofessionals.nhs.uk/"], ["Oxford", "NHSP", "NHSP", "https://bank.nhsprofessionals.nhs.uk/"], ["East Suffolk & North Essex", "NHSP", "", ""], ["Southampton", "NHSP", "NHSP", "https://bank.nhsprofessionals.nhs.uk/"], ["Frimley Health", "ID Medical", "Clarity", "https://clarity.id-medical.co.uk/"], ["Bristol & Western", "ID Medical", "Clarity", "https://clarity.id-medical.co.uk/"], ["Spire", "Retinue", "Bridge", "https://bridge.retinue.com/"], ["Circle", "Retinue", "Bridge", "https://bridge.retinue.com/"], ["Ramsay", "Retinue", "Bridge", "https://bridge.retinue.com/"], ["Spa Medica", "No System", "", ""], ["Medicana", "No System", "", ""], ["Optegra", "No System", "", ""]];

// rcChecks: {hospitalName: {wkKey: {checked: bool, time: 'HH:MM', date: 'YYYY-MM-DD'}}}
var rcChecks={};
try{var _rc=localStorage.getItem('rc_checks');if(_rc)rcChecks=JSON.parse(_rc);}catch(e){}
function saveRC(){try{localStorage.setItem('rc_checks',JSON.stringify(rcChecks));}catch(e){}}

var rcWkOffset=0; // 0 = current week, -1 = last week, etc.

function rcGetMonday(offset){
var d=new Date();
var day=d.getDay()||7;
d.setDate(d.getDate()-day+1+(offset*7));
return d;
}

function rcWkKey(){
var d=rcGetMonday(rcWkOffset);
var y=d.getFullYear(),m=String(d.getMonth()+1).padStart(2,'0'),dd=String(d.getDate()).padStart(2,'0');
return y+'-'+m+'-'+dd;
}

function rcMondayLabel(){
var d=rcGetMonday(rcWkOffset);
var months=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
var label='w/c '+d.getDate()+' '+months[d.getMonth()]+' '+d.getFullYear();
if(rcWkOffset===0)label+=' (this week)';
else if(rcWkOffset===-1)label+=' (last week)';
return label;
}

function rcNavWk(dir){
// Don't allow navigating past current week
if(rcWkOffset+dir>0)return;
rcWkOffset+=dir;
rRC();
}

function rcCheckDays(){return['Monday','Wednesday','Friday'];}

function rcTodayName(){
var days=['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
return days[new Date().getDay()];
}

function rcMarkChecked(name, checkDay){
if(rcWkOffset!==0)return;
var wk=rcWkKey();
if(!rcChecks[name])rcChecks[name]={};
if(!rcChecks[name][wk])rcChecks[name][wk]={};
var now=new Date();
var h=String(now.getHours()).padStart(2,'0'),m=String(now.getMinutes()).padStart(2,'0');
rcChecks[name][wk][checkDay]={checked:true,time:h+':'+m};
saveRC();
rRC();
}

function rcUncheck(name, checkDay){
if(rcWkOffset!==0)return;
var wk=rcWkKey();
if(rcChecks[name]&&rcChecks[name][wk])delete rcChecks[name][wk][checkDay];
saveRC();
rRC();
}

function rRC(){
var el=document.getElementById('rc-grid');
if(!el)return;
var wk=rcWkKey();
var wkLbl=rcMondayLabel();
var checkDays=rcCheckDays();
var todayName=rcTodayName();
var isCurrentWk=rcWkOffset===0;

// Week label with nav arrows
var wlEl=document.getElementById('rc-wk-lbl');
if(wlEl){
var prevBtn='<button onclick="rcNavWk(-1)" style="background:none;border:none;cursor:pointer;font-size:16px;color:var(--t2);padding:0 8px 0 0">&#8592;</button>';
var nextBtn=isCurrentWk?'':'<button onclick="rcNavWk(1)" style="background:none;border:none;cursor:pointer;font-size:16px;color:var(--t2);padding:0 0 0 8px">&#8594;</button>';
wlEl.innerHTML=prevBtn+'<span style="font-size:13px;font-weight:500">'+wkLbl+'</span>'+nextBtn;
}

// Summary \u2014 count hospitals with all 3 checks done
var allDone=RC_HOSPITALS.filter(function(h){
var hWk=(rcChecks[h[0]]||{})[wk]||{};
return checkDays.every(function(d){return hWk[d]&&hWk[d].checked;});
}).length;
var anyDone=RC_HOSPITALS.filter(function(h){
var hWk=(rcChecks[h[0]]||{})[wk]||{};
return checkDays.some(function(d){return hWk[d]&&hWk[d].checked;});
}).length;
var total=RC_HOSPITALS.length;
// Total individual checks done vs possible
var totalChecks=RC_HOSPITALS.reduce(function(s,h){
var hWk=(rcChecks[h[0]]||{})[wk]||{};
return s+checkDays.filter(function(d){return hWk[d]&&hWk[d].checked;}).length;
},0);
var maxChecks=total*3;
var pct=Math.round(totalChecks/maxChecks*100);

var summEl=document.getElementById('rc-summary');
if(summEl){
var col=allDone===total?'var(--grtx)':totalChecks>0?'var(--amtx)':'var(--t2)';
summEl.innerHTML='<span style="font-size:20px;font-weight:500;color:'+col+'">'+totalChecks+'</span>'
+'<span style="font-size:13px;color:var(--t2)"> / '+maxChecks+' checks done</span>'
+'<span style="font-size:12px;color:var(--t3);margin-left:8px">('+allDone+' hospitals fully complete)</span>'
+'<div style="margin-top:6px;height:5px;border-radius:3px;background:var(--b2);overflow:hidden;width:220px">'
+'<div style="height:100%;width:'+pct+'%;background:'+(allDone===total?'var(--gr)':'var(--bl)')+';border-radius:3px;transition:width .3s"></div>'
+'</div>';
}

var sysFilter=document.getElementById('rc-sys-filter');
var activeSys=sysFilter?sysFilter.value:'';
var systems=['HR','NHSP','Retinue','ID Medical','No System'];
var sysLabels={'HR':'Health Roster','NHSP':'NHSP','Retinue':'Retinue / Bridge','ID Medical':'ID Medical','No System':'No Roster System'};
var html='';

systems.forEach(function(sys){
if(activeSys&&activeSys!==sys)return;
var hosps=RC_HOSPITALS.filter(function(h){return h[1]===sys;});
if(!hosps.length)return;
html+='<div style="margin-bottom:20px">'
+'<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.06em;margin-bottom:8px">'+sysLabels[sys]+'</div>'
+'<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:8px">';

hosps.forEach(function(h){
var name=h[0];
var _hObj=HC.find(function(x){return x.name===name;})||{};
var _ed=gHE(name);
var sysUrl=_ed.rosterLink||_hObj.roster_link||h[3];
var hWk=(rcChecks[name]||{})[wk]||{};
var doneCount=checkDays.filter(function(d){return hWk[d]&&hWk[d].checked;}).length;
var allChecked=doneCount===3;
var border=allChecked?'0.5px solid var(--gr)':doneCount>0?'0.5px solid var(--am)':'0.5px solid var(--b2)';

html+='<div style="background:var(--su);border:'+border+';border-radius:var(--rl);padding:11px 12px">'
+'<div style="display:flex;align-items:center;margin-bottom:8px">'
+'<div style="font-size:13px;font-weight:500;flex:1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis">'+esc(name)+'</div>'
+(sysUrl?'<a href="'+esc(sysUrl)+'" target="_blank" style="font-size:11px;color:var(--t2);text-decoration:none;padding:2px 6px;border:0.5px solid var(--b2);border-radius:10px;white-space:nowrap">'+(h[2]||'Open')+' \u2197</a>':'')
+'</div>'
// 3 check day slots
+'<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:5px">';

checkDays.forEach(function(day){
var chk=hWk[day];
var done=chk&&chk.checked;
var isToday=isCurrentWk&&day===todayName;
var shortDay=day.slice(0,3);

if(isCurrentWk){
if(done){
html+='<button class="rc-uncheck-btn" data-name="'+esc(name)+'" data-day="'+day+'"'
+' style="padding:5px 2px;border:0.5px solid var(--gr);border-radius:var(--r);background:var(--su);cursor:pointer;text-align:center">'
+'<div style="font-size:10px;color:var(--grtx);font-weight:500">\u2713 '+shortDay+'</div>'
+'<div style="font-size:10px;color:var(--t3)">'+chk.time+'</div>'
+'</button>';
} else {
html+='<button class="rc-check-btn" data-name="'+esc(name)+'" data-day="'+day+'"'
+' style="padding:5px 2px;border:0.5px solid '+(isToday?'var(--bl)':'var(--b2)')+';border-radius:var(--r);background:'+(isToday?'var(--blbg)':'transparent')+';cursor:pointer;text-align:center">'
+'<div style="font-size:10px;color:'+(isToday?'var(--bltx)':'var(--t2)')+';font-weight:'+(isToday?'500':'400')+'">'+shortDay+'</div>'
+'<div style="font-size:10px;color:var(--t3)">check</div>'
+'</button>';
}
} else {
// Past week \u2014 read only
html+='<div style="padding:5px 2px;border:0.5px solid '+(done?'var(--gr)':'var(--b2)')+';border-radius:var(--r);text-align:center">'
+'<div style="font-size:10px;color:'+(done?'var(--grtx)':'var(--t3)')+';font-weight:'+(done?'500':'400')+'">'+(done?'\u2713':'\u2013')+' '+shortDay+'</div>'
+'<div style="font-size:10px;color:var(--t3)">'+(done?chk.time:'')+'</div>'
+'</div>';
}
});

html+='</div>' // end grid
+'</div>'; // end card
});
html+='</div></div>';
});

el.innerHTML=html;

el.querySelectorAll('.rc-check-btn').forEach(function(btn){
btn.addEventListener('click',function(){rcMarkChecked(this.dataset.name,this.dataset.day);});
});
el.querySelectorAll('.rc-uncheck-btn').forEach(function(btn){
btn.addEventListener('click',function(){rcUncheck(this.dataset.name,this.dataset.day);});
});
}


// \u2500\u2500 SELF BILL \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var SB_BASE=[]
var sbEdits=[];
try{var _sb=localStorage.getItem('sb_edits');if(_sb)sbEdits=JSON.parse(_sb);}catch(e){}
function saveSB(){try{localStorage.setItem('sb_edits',JSON.stringify(sbEdits));}catch(e){}}
function getAllSB(){return SB_BASE.concat(sbEdits);}

var sbFilter={hospital:'',status:'',q:''};
var sbPage=0;
var SB_PAGE_SIZE=50;

function sbDisc(r){
// Returns discrepancy: sb_amount - expected_amount
var exp=r[6]||0;
var sb=r[4]||0;
if(!exp)return null; // no expected set
return Math.round((sb-exp)*100)/100;
}

// \u2500\u2500 SB BULK PASTE \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _sbParsed=[]; // [{cand,shiftDate,ref,amount,raw,matched,selected,candIdx}]
function getAllTrustNames(){
// Returns all trust names from TRUST_CARDS + HC (includes user-added trusts)
var names=[];
TRUST_CARDS.forEach(function(tc){
if(names.indexOf(tc.name)<0)names.push(tc.name);
});
HC.forEach(function(h){
if(names.indexOf(h.name)<0)names.push(h.name);
});
// Also include any user-added trusts from trustEdits
trustEdits.forEach(function(t){
if(t.name&&names.indexOf(t.name)<0)names.push(t.name);
});
return names.sort();
}

function sbFuzzyMatch(name){
if(!name)return{name:'',idx:-1,score:0};
var n=name.toLowerCase().trim();
var nParts=n.split(/\s+/).filter(function(p){return p.length>0;});
if(!nParts.length)return{name:'',idx:-1,score:0};

// Also try reversed: "Emmanuel Roseline" -> ["Roseline","Emmanuel"]
var nPartsRev=nParts.slice().reverse();

var best={name:'',idx:-1,score:0};

function scoreAgainst(parts,c,penalise){
var cn=c.n.toLowerCase();
var cParts=cn.split(/\s+/).filter(function(p){return p.length>0;});
if(!cParts.length)return 0;
if(parts.join(' ')===cn)return penalise?95:100;

var inSurname=parts[parts.length-1];
var inFirstParts=parts.slice(0,-1);
var cSurname=cParts[cParts.length-1];
var cFirstParts=cParts.slice(0,-1);

var surnameExact=inSurname===cSurname;
var surnamePrefix=(inSurname.length>3&&cSurname.startsWith(inSurname))
||(cSurname.length>3&&inSurname.startsWith(cSurname));
if(!surnameExact&&!surnamePrefix)return 0;

if(!inFirstParts.length||!cFirstParts.length)
return surnameExact?(penalise?40:45):(penalise?30:35);

var firstScore=0;
inFirstParts.forEach(function(iw){
if(iw.length<2)return;
cFirstParts.forEach(function(cw){
if(cw.length<2)return;
if(iw===cw)firstScore=Math.max(firstScore,100);
else if(cw.startsWith(iw)&&iw.length>=3)firstScore=Math.max(firstScore,85);
else if(iw.startsWith(cw)&&cw.length>=3)firstScore=Math.max(firstScore,85);
else if(cw.indexOf(iw)>=0&&iw.length>=4)firstScore=Math.max(firstScore,65);
else if(iw.indexOf(cw)>=0&&cw.length>=4)firstScore=Math.max(firstScore,65);
});
});

var score=0;
if(surnameExact&&firstScore>=85)score=92;
else if(surnameExact&&firstScore>=65)score=78;
else if(surnameExact&&firstScore>=40)score=65;
else if(surnameExact)score=45;
else if(surnamePrefix&&firstScore>=85)score=82;
else if(surnamePrefix&&firstScore>=65)score=68;

return penalise?Math.round(score*0.92):score; // small penalty for reversed
}

C.forEach(function(c,i){
if(!c.n)return;
var s1=scoreAgainst(nParts,c,false);
var s2=nParts.length>1?scoreAgainst(nPartsRev,c,true):0;
var score=Math.max(s1,s2);
if(score>best.score)best={name:c.n,idx:i,score:score};
});

return best;
}




function sbDetectCols(headers){
// Auto-detect which column is which from header row
var cols={cand:-1,date:-1,ref:-1,amount:-1};
headers.forEach(function(h,i){
var hl=(h||'').toLowerCase();
if(cols.cand<0&&(hl.includes('name')||hl.includes('worker')||hl.includes('staff')||hl.includes('candidate')))cols.cand=i;
if(cols.date<0&&(hl.includes('shift')||hl.includes('date'))&&!hl.includes('sb')&&!hl.includes('bill'))cols.date=i;
if(cols.ref<0&&(hl.includes('ref')||hl.includes('id')||hl.includes('request')||hl.includes('booking')||hl.includes('number')))cols.ref=i;
if(cols.amount<0&&(hl.includes('amount')||hl.includes('cost')||hl.includes('charge')||hl.includes('net')||hl.includes('total')))cols.amount=i;
});
return cols;
}

function sbParsePaste(){
var raw=document.getElementById('sb-paste-area').value.trim();
if(!raw){alert('Please paste data first');return;}
var hospital=document.getElementById('sb-paste-hosp').value.trim();
var sbDate=document.getElementById('sb-paste-date').value||'';
var lines=raw.split('\n').map(function(l){return l.split('\t');});
if(!lines.length){alert('No data found');return;}

// Try to detect header row
var headerRow=lines[0];
var cols=sbDetectCols(headerRow);
var dataStart=0;
if(cols.cand>=0||cols.amount>=0){
dataStart=1; // first row is header
} else {
// Try second row as header
if(lines.length>1){
cols=sbDetectCols(lines[1]);
if(cols.cand>=0)dataStart=2;
}
}

// If no auto-detect, use positional fallback (name=0, date=1, ref=2, amount=3)
if(cols.cand<0)cols.cand=0;
if(cols.date<0)cols.date=1;
if(cols.ref<0)cols.ref=2;
if(cols.amount<0)cols.amount=3;

_sbParsed=[];
for(var i=dataStart;i<lines.length;i++){
var row=lines[i];
if(row.length<2)continue;
var candRaw=(row[cols.cand]||'').trim();
if(!candRaw)continue;
var shiftDate='';
var dateRaw=(row[cols.date]||'').trim();
if(dateRaw){
// Try to parse various date formats
var d=new Date(dateRaw);
if(!isNaN(d.getTime()))shiftDate=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
else shiftDate=dateRaw;
}
var ref=(row[cols.ref]||'').trim();
var amtRaw=(row[cols.amount]||'').replace(/[\u00a3$,]/g,'').trim();
var amount=parseFloat(amtRaw)||0;
var match=sbFuzzyMatch(candRaw);
_sbParsed.push({
cand:match.score>=70?match.name:candRaw,
candRaw:candRaw,
shiftDate:shiftDate,
ref:ref,
amount:amount,
hospital:hospital,
sbDate:sbDate,
matched:match.score>=60,
matchScore:match.score,
selected:match.score>=60, // auto-select matched candidates
rawRow:row.join('\t')
});
}

if(!_sbParsed.length){alert('Could not parse any rows. Check the data format.');return;}
sbRenderPreview();
document.getElementById('sb-preview-area').style.display='block';
document.getElementById('sb-paste-area').value='';
}

function sbRenderPreview(){
var tbody=document.getElementById('sb-preview-tbody');
if(!tbody)return;
var matched=_sbParsed.filter(function(r){return r.matched;}).length;
var selected=_sbParsed.filter(function(r){return r.selected;}).length;
document.getElementById('sb-preview-summary').innerHTML=
'<strong>'+_sbParsed.length+'</strong> rows parsed &middot; '
+'<span style="color:var(--grtx)"><strong>'+matched+'</strong> matched to candidates</span>'
+' &middot; <strong>'+selected+'</strong> selected to log';
tbody.innerHTML=_sbParsed.map(function(r,i){
var rowBg=r.matched?'':'background:var(--su2)';
var candDisplay=r.matched
?'<span style="color:var(--grtx);font-weight:500">'+esc(r.cand)+'</span>'
:'<span style="color:var(--amtx)">'+esc(r.candRaw)+'</span><div style="font-size:10px;color:var(--t3)">no match</div>';
return '<tr style="border-bottom:0.5px solid var(--b1);'+rowBg+'">'
+'<td style="padding:5px 8px"><input type="checkbox" class="sb-pre-chk" data-i="'+i+'"'+(r.selected?' checked':'')+'></td>'
+'<td style="padding:5px 8px;font-size:12px">'+candDisplay+'</td>'
+'<td style="padding:5px 8px;font-size:12px;color:var(--t2)">'+fmtDateDMY(r.shiftDate)+'</td>'
+'<td style="padding:5px 8px;font-size:12px;color:var(--t2)">'+esc(r.ref)+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right;font-weight:500">'+(r.amount?'\u00a3'+r.amount.toFixed(2):'--')+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right;color:var(--t2)">'+(r.expected?'\u00a3'+r.expected.toFixed(2):'--')+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right;'+(r.diff&&r.diff!==0?'color:var(--amtx);font-weight:500':'color:var(--grtx)')+'">'+(r.expected?(r.diff===0?'\u2713':'\u00a3'+r.diff.toFixed(2)):'--')+'</td>'
+'</tr>';
}).join('');
tbody.querySelectorAll('.sb-pre-chk').forEach(function(chk){
chk.addEventListener('change',function(){_sbParsed[+this.dataset.i].selected=this.checked;sbRenderPreview();});
});
}

function sbSelectAll(val){
_sbParsed.forEach(function(r){r.selected=val;});
sbRenderPreview();
}

function sbConfirmBulk(){
var toLog=_sbParsed.filter(function(r){return r.selected;});
if(!toLog.length){alert('No rows selected');return;}
toLog.forEach(function(r){
sbEdits.push([r.sbDate,r.cand,r.shiftDate,r.ref,r.amount,r.hospital,0,'unreconciled']);
});
saveSB();
_sbParsed=[];
document.getElementById('sb-preview-area').style.display='none';
sbPage=0;
rSB();
alert(toLog.length+' entries logged successfully');
}

function sbCancelBulk(){
_sbParsed=[];
document.getElementById('sb-preview-area').style.display='none';
}


// Shared XLSX loader \u2014 loads SheetJS once, calls callback when ready
function loadXLSX(cb){
if(typeof XLSX!=='undefined'){cb();return;}
if(window._xlsxLoading){window._xlsxQueue=window._xlsxQueue||[];window._xlsxQueue.push(cb);return;}
window._xlsxLoading=true;window._xlsxQueue=[cb];
var s=document.createElement('script');
s.src='https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js';
s.onload=function(){window._xlsxLoading=false;(window._xlsxQueue||[]).forEach(function(fn){fn();});window._xlsxQueue=[];};
s.onerror=function(){window._xlsxLoading=false;alert('Could not load spreadsheet parser. Check internet connection.');};
document.head.appendChild(s);
}


// \u2500\u2500 SB DRAG & DROP IMPORT \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _sbImportParsed=[];

function sbInitDrop(){
var zone=document.getElementById('sb-drop-zone');
if(!zone||zone._init)return;
zone._init=true;
zone.addEventListener('dragover',function(e){e.preventDefault();this.style.borderColor='var(--bl)';this.style.background='var(--blbg)';});
zone.addEventListener('dragleave',function(){this.style.borderColor='var(--b2)';this.style.background='transparent';});
zone.addEventListener('drop',function(e){
e.preventDefault();
this.style.borderColor='var(--b2)';this.style.background='transparent';
var file=e.dataTransfer.files[0];
if(!file)return;
sbReadFile(file);
});
zone.addEventListener('click',function(){document.getElementById('sb-file-input').click();});
var fi=document.getElementById('sb-file-input');
if(fi)fi.addEventListener('change',function(){if(this.files[0])sbReadFile(this.files[0]);});
}

function sbReadFile(file){
var statusEl=document.getElementById('sb-drop-status');
if(statusEl)statusEl.textContent='Reading '+file.name+'...';
var reader=new FileReader();
reader.onload=function(e){
try{sbParseXLSX(e.target.result,file.name);}
catch(err){if(statusEl)statusEl.textContent='Error: '+err.message;}
};
reader.readAsArrayBuffer(file);
}

function sbParseXLSX(buffer,filename){
var statusEl=document.getElementById('sb-drop-status');
var data=new Uint8Array(buffer);
var bstr='';
for(var i=0;i<data.length;i++)bstr+=String.fromCharCode(data[i]);
loadXLSX(function(){sbParseWithXLSX(bstr,filename);});
}

function sbParseWithXLSX(bstr,filename){
var statusEl=document.getElementById('sb-drop-status');
try{
var wb=XLSX.read(bstr,{type:'binary',cellDates:true,raw:false});
var skipWords=['mismatch','error','issue','platform fee','client net'];
var mainSheet=null;
wb.SheetNames.forEach(function(s){
if(!mainSheet&&!skipWords.some(function(w){return s.toLowerCase().includes(w);}))mainSheet=s;
});
if(!mainSheet)mainSheet=wb.SheetNames[0];
var ws=wb.Sheets[mainSheet];
var rows=XLSX.utils.sheet_to_json(ws,{header:1,defval:'',raw:false});
if(!rows||rows.length<2){if(statusEl)statusEl.textContent='No data found in: '+mainSheet;return;}

var headerIdx=0;
for(var h=0;h<Math.min(8,rows.length);h++){
if(rows[h].filter(function(v){return(v||'').toString().trim()!='';}).length>=4){headerIdx=h;break;}
}
var hdrs=rows[headerIdx].map(function(v){return(v||'').toString().toLowerCase().trim();});

function findCol(kws){
for(var k=0;k<kws.length;k++)for(var i=0;i<hdrs.length;i++)if(hdrs[i].includes(kws[k]))return i;
return -1;
}
var nameCol=findCol(['applicant name','worker','candidate','staff']);
var dateCol=findCol(['shift date','tsfrom','date']);
var refCol=findCol(['timesheet id','request id','reference 1','ref 1','ref1','booking']);
var hospCol=findCol(['unit','client','hospital','trust','location']);
var amtCol=findCol(['self-bill net','selfbill net','net chg','net charge','actual charge','actual cost','net','charge','amount','cost','total']);
if(nameCol<0)nameCol=0;
if(dateCol<0)dateCol=1;

var sf=function(v){var s=(v||'').toString().replace(/[\\u00a3$,\\s]/g,'');var n=parseFloat(s);return isNaN(n)?0:Math.round(n*100)/100;};
var parseDate=function(v){
if(!v)return'';
var s=v.toString().trim();
var m=s.match(/^(\d{1,2})\/(\d{1,2})\/(\d{4})$/);if(m)return m[3]+'-'+m[2].padStart(2,'0')+'-'+m[1].padStart(2,'0');
var m2=s.match(/^(\d{4})-(\d{2})-(\d{2})/);if(m2)return m2[1]+'-'+m2[2]+'-'+m2[3];
var d=new Date(s);if(!isNaN(d.getTime()))return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
return'';
};
var hospHint=filename.replace(/^\d{4}_\d{2}_\d{2}_/,'').replace(/_WK\d+.*/i,'').replace(/_UPLOADED.*/i,'').replace(/_Self_Bill.*/i,'').replace(/_Checks.*/i,'').replace(/All_/i,'').replace(/_/g,' ').replace(/\.xlsx?$/i,'').trim();

var parsed=[];
for(var r=headerIdx+1;r<rows.length;r++){
var row=rows[r];
if(!row||!row.length)continue;
var nameRaw=(row[nameCol]||'').toString().trim();
if(!nameRaw)continue;
var amount=amtCol>=0?sf(row[amtCol]):0;
if(amount<=0)continue; // skip zero/reversal rows
var shiftDate=parseDate(dateCol>=0?row[dateCol]||'':'');
var ref=refCol>=0?(row[refCol]||'').toString().trim().replace(/^'/,''):'';
var hospRaw=hospCol>=0?(row[hospCol]||'').toString().trim():'';
var hosp=(hospRaw&&hospRaw.length<60)?hospRaw:hospHint;
var _match=sbFuzzyMatch(nameRaw);
var _matched=_match.score>=60;
parsed.push({name:_matched?_match.name:nameRaw,nameRaw:nameRaw,matched:_matched,candOverride:'',hospital:hosp,shiftDate:shiftDate,ref:ref,amount:amount,expected:0,diff:0,selected:false});
}

if(!parsed.length){if(statusEl)statusEl.textContent='No rows parsed from: '+mainSheet+'. Detected headers: '+hdrs.slice(0,8).join(', ');return;}

var existing=getAllSB();
var existingKeys={};
existing.forEach(function(r){existingKeys[(r[1]||'')+'|'+(r[5]||'')+'|'+(r[2]||'')]=true;});
var newRows=parsed.filter(function(r){return !existingKeys[(r.name||'')+'|'+(r.hospital||'')+'|'+(r.shiftDate||'')];});
var dupes=parsed.length-newRows.length;
var matched=newRows.filter(function(r){return r.matched;}).length;
_sbImportParsed=newRows;
if(statusEl)statusEl.textContent=filename+' \u2014 '+parsed.length+' shifts, '+matched+' matched, '+(newRows.length-matched)+' unmatched, '+dupes+' dupes skipped, '+newRows.length+' new.';
sbRenderImportPreview();
document.getElementById('sb-import-preview').style.display='block';
}catch(err){if(statusEl)statusEl.textContent='Parse error: '+err.message;console.error(err);}
}

function sbRenderImportPreview(){
var tbody=document.getElementById('sb-import-tbody');
var countEl=document.getElementById('sb-import-count');
var hospWrap=document.getElementById('sb-hosp-picker-wrap');
if(!tbody)return;

// \u2500\u2500 Hospital picker at top (build once) \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
if(hospWrap&&!hospWrap._built){
hospWrap._built=true;
var hospOpts='<option value="">-- select hospital --</option>'
+getAllSitesList().map(function(s){return'<option value="'+esc(s)+'">'+esc(s)+'</option>';}).join('');
// Try to pre-select from the first row's hospital hint
var hint=(_sbImportParsed[0]&&_sbImportParsed[0].hospital)||'';
hospOpts=hospOpts.replace('value="'+esc(hint)+'"','value="'+esc(hint)+'" selected');
hospWrap.innerHTML='<div style="display:flex;align-items:center;gap:10px;margin-bottom:12px;padding:10px 12px;background:var(--su2);border-radius:var(--r)">'
+'<div style="font-size:12px;font-weight:500;color:var(--tx);flex-shrink:0">Hospital for all rows:</div>'
+'<select id="sb-hosp-all" style="flex:1;max-width:260px;padding:6px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:13px;outline:none">'
+hospOpts
+'</select>'
+'<div style="font-size:11px;color:var(--t3)">Changes apply to all rows instantly</div>'
+'</div>';
// If hint found, apply it to all rows
if(hint)_sbImportParsed.forEach(function(r){r.hospital=hint;});
document.getElementById('sb-hosp-all').addEventListener('change',function(){
var h=this.value;
_sbImportParsed.forEach(function(r){r.hospital=h;});
// Re-render hospital column only
tbody.querySelectorAll('.sb-hosp-cell').forEach(function(td){td.textContent=h;});
});
}

// Build candidate options for fix dropdowns
var candOpts='<option value="">-- select --</option>'
+C.filter(function(c){return c.ac!=='Inactive';}).map(function(c){
return'<option value="'+esc(c.n)+'">'+esc(c.n)+'</option>';
}).join('');

var sel=_sbImportParsed.filter(function(r){return r.selected;}).length;
var unmatched=_sbImportParsed.filter(function(r){return !r.matched&&!r.candOverride;}).length;
if(countEl)countEl.textContent=_sbImportParsed.length+' rows \u2014 '+sel+' selected'+(unmatched?' \u2014 <span style="color:var(--amtx)">'+unmatched+' unmatched</span>':'');

tbody.innerHTML=_sbImportParsed.map(function(r,i){
var displayName=r.candOverride||r.name;
var isMatched=r.matched||r.candOverride;
var nameCell=
// Name display
'<div style="display:flex;align-items:center;gap:6px">'
+'<span style="font-size:12px;font-weight:500;color:'+(isMatched?'var(--tx)':'var(--amtx)')+'">'+esc(displayName)+'</span>'
+(r.candOverride?'<span style="font-size:10px;color:var(--t3)">(fixed)</span>':'')
+(!isMatched?'<span style="font-size:10px;color:var(--amtx)">no match</span>':'')
+'<button class="sb-fix-btn edit-btn" data-i="'+i+'" style="padding:1px 6px;font-size:10px;margin-left:2px">Fix</button>'
+'</div>'
// Fix dropdown (hidden by default)
+'<div class="sb-fix-wrap" id="sb-fix-'+i+'" style="display:none;margin-top:4px">'
+'<select class="sb-cand-sel" data-i="'+i+'" style="width:100%;padding:4px 6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+candOpts
+'</select>'
+'</div>';

return'<tr style="border-bottom:0.5px solid var(--b1);background:'+(isMatched?'transparent':'var(--ambg)')+'">'
+'<td style="padding:5px 8px"><input type="checkbox" class="sb-imp-chk" data-i="'+i+'"'+(r.selected?' checked':'')+'></td>'
+'<td style="padding:5px 8px;min-width:180px">'+nameCell+'</td>'
+'<td class="sb-hosp-cell" style="padding:5px 8px;font-size:12px;color:var(--t2)">'+esc(r.hospital)+'</td>'
+'<td style="padding:5px 8px;font-size:12px;color:var(--t2)">'+fmtDateDMY(r.shiftDate)+'</td>'
+'<td style="padding:5px 8px;font-size:12px;color:var(--t2)">'+esc(r.ref)+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right;font-weight:500">'+(r.amount?'\u00a3'+r.amount.toFixed(2):'--')+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right;color:var(--t2)">'+(r.expected?'\u00a3'+r.expected.toFixed(2):'--')+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right"></td>'
+'</tr>';
}).join('');

// Wire checkboxes
tbody.querySelectorAll('.sb-imp-chk').forEach(function(chk){
chk.addEventListener('change',function(){
_sbImportParsed[+this.dataset.i].selected=this.checked;
var s=_sbImportParsed.filter(function(r){return r.selected;}).length;
var um=_sbImportParsed.filter(function(r){return !r.matched&&!r.candOverride;}).length;
if(countEl)countEl.innerHTML=_sbImportParsed.length+' rows \u2014 '+s+' selected'+(um?' \u2014 <span style="color:var(--amtx)">'+um+' unmatched</span>':'');
});
});

// Wire fix buttons \u2014 toggle dropdown
tbody.querySelectorAll('.sb-fix-btn').forEach(function(btn){
btn.addEventListener('click',function(){
var wrap=document.getElementById('sb-fix-'+this.dataset.i);
if(wrap)wrap.style.display=wrap.style.display==='none'?'block':'none';
});
});

// Wire candidate fix dropdowns
tbody.querySelectorAll('.sb-cand-sel').forEach(function(sel){
sel.addEventListener('change',function(){
var i=+this.dataset.i;
if(!this.value)return;
_sbImportParsed[i].candOverride=this.value;
_sbImportParsed[i].name=this.value;
_sbImportParsed[i].matched=true;
// Hide fix dropdown and re-render row name
var wrap=document.getElementById('sb-fix-'+i);
if(wrap)wrap.style.display='none';
sbRenderImportPreview();
});
});
}
function sbConfirmImport(){
var toLog=_sbImportParsed.filter(function(r){return r.selected;});
if(!toLog.length){alert('No rows selected');return;}
var today=todayStr();
toLog.forEach(function(r){
var cand=r.candOverride||r.name||r.nameRaw;
sbEdits.push([today,cand,r.shiftDate,r.ref,r.amount,r.hospital,0,'unreconciled']);
});
saveSB();
_sbImportParsed=[];
var prev=document.getElementById('sb-import-preview');
if(prev)prev.style.display='none';
var wrap=document.getElementById('sb-hosp-picker-wrap');
if(wrap){wrap.innerHTML='';wrap._built=false;}
var status=document.getElementById('sb-drop-status');
if(status)status.textContent=toLog.length+' shifts imported.';
rSB();
}


function sbCancelImport(){
_sbImportParsed=[];
document.getElementById('sb-import-preview').style.display='none';
document.getElementById('sb-drop-status').textContent='';
}


function addSelfBill(){
var sbDate=document.getElementById('sb-sbdate').value||'';
var cand=document.getElementById('sb-cand').value.trim();
var shiftDate=document.getElementById('sb-shiftdate').value||'';
var ref=document.getElementById('sb-ref').value.trim();
var sbAmt=parseFloat(document.getElementById('sb-amount').value)||0;
var hosp=document.getElementById('sb-hospital').value.trim();
var expAmt=parseFloat(document.getElementById('sb-expected').value)||0;
if(!cand){alert('Candidate name is required');return;}
if(!sbDate){alert('SB date is required');return;}
sbEdits.push([sbDate,cand,shiftDate,ref,sbAmt,hosp,expAmt,'unreconciled']);
saveSB();
// Clear form except hospital (batch entry)
document.getElementById('sb-cand').value='';
document.getElementById('sb-shiftdate').value='';
document.getElementById('sb-ref').value='';
document.getElementById('sb-amount').value='';
document.getElementById('sb-expected').value='';
sbPage=0;
rSB();
}

function updateSBStatus(editIdx, status){
if(editIdx<0||editIdx>=sbEdits.length)return;
sbEdits[editIdx][7]=status;
saveSB(); rSB();
}

function deleteSB(editIdx){
if(!confirm('Delete this entry?'))return;
sbEdits.splice(editIdx,1);
saveSB(); rSB();
}

function sbSetFilter(k,v){sbFilter[k]=v;sbPage=0;rSB();}

function rSB(){
var all=getAllSB();
var q=(sbFilter.q||'').toLowerCase();
var hf=(sbFilter.hospital||'').toLowerCase();
var sf=(sbFilter.status||'');

var indexed=[];
all.forEach(function(r,i){
if(hf&&!(r[5]||'').toLowerCase().includes(hf))return;
if(q&&!((r[1]||'')+(r[5]||'')+(r[3]||'')).toLowerCase().includes(q))return;
var disc=sbDisc(r);
if(sf==='discrepancy'&&(disc===null||disc===0))return;
if(sf==='unreconciled'&&r[7]!=='unreconciled')return;
if(sf==='reconciled'&&r[7]!=='reconciled')return;
if(sf==='queried'&&r[7]!=='queried')return;
indexed.push({r:r,origIdx:i});
});

// Sort most recent first
indexed.sort(function(a,b){var d=(b.r[0]||'').localeCompare(a.r[0]||'');return d!==0?d:(b.r[2]||'').localeCompare(a.r[2]||'');});

// Summary stats
var totalSB=indexed.reduce(function(s,o){return s+(o.r[4]||0);},0);
var totalExp=indexed.reduce(function(s,o){return s+(o.r[6]||0);},0);
var discCount=indexed.filter(function(o){var d=sbDisc(o.r);return d!==null&&d!==0;}).length;
var unreconCount=indexed.filter(function(o){return o.r[7]==='unreconciled';}).length;

var statsEl=document.getElementById('sb-stats');
if(statsEl){
statsEl.innerHTML=
'<span><strong>'+indexed.length+'</strong> records</span>'
+'<span>SB total: <strong style="color:var(--bl)">\u00a3'+totalSB.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</strong></span>'
+(totalExp?'<span>Expected: <strong>\u00a3'+totalExp.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</strong></span>':'')
+(discCount?'<span style="color:var(--amtx)"><strong>'+discCount+'</strong> discrepanc'+(discCount===1?'y':'ies')+'</span>':'')
+(unreconCount?'<span style="color:var(--t3)"><strong>'+unreconCount+'</strong> unreconciled</span>':'');
}

// Pagination
var totalPages=Math.ceil(indexed.length/SB_PAGE_SIZE)||1;
if(sbPage>=totalPages)sbPage=totalPages-1;
var page=indexed.slice(sbPage*SB_PAGE_SIZE,(sbPage+1)*SB_PAGE_SIZE);
var pgEl=document.getElementById('sb-pages');
if(pgEl){
pgEl.innerHTML='<span style="font-size:12px;color:var(--t2)">Page '+(sbPage+1)+' of '+totalPages+'</span>'
+'<button onclick="if(sbPage>0){sbPage--;rSB();}" style="padding:3px 9px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">\u2190</button>'
+'<button onclick="if(sbPage<'+(totalPages-1)+'){sbPage++;rSB();}" style="padding:3px 9px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">\u2192</button>';
}

// Table
var tbody=document.getElementById('sb-tbody');
if(!tbody)return;
if(!page.length){
tbody.innerHTML='<tr><td colspan="9" style="padding:24px;text-align:center;color:var(--t3)">No records match</td></tr>';
return;
}

tbody.innerHTML=page.map(function(o){
var r=o.r;
var editIdx=o.origIdx>=SB_BASE.length?o.origIdx-SB_BASE.length:-1;
var disc=sbDisc(r);
var discHtml='<span style="color:var(--t3)">--</span>';
if(disc!==null){
if(disc===0)discHtml='<span style="color:var(--grtx)">\u2713 Match</span>';
else discHtml='<span style="color:var(--amtx);font-weight:500">'+(disc>0?'+':'')+'\u00a3'+Math.abs(disc).toFixed(2)+'</span>';
}
var statusCol={unreconciled:'var(--t3)',reconciled:'var(--grtx)',queried:'var(--amtx)'};
var statusDot='<span style="display:inline-block;width:7px;height:7px;border-radius:50%;background:'+(statusCol[r[7]]||'var(--t3)')+';margin-right:4px"></span>';

return '<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 0;font-size:12px">'+fmtDateDMY(r[0])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;font-weight:500">'+esc(r[1])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+esc(r[5])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+fmtDateDMY(r[2])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+esc(r[3])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right;font-weight:500">'+(r[4]?'\u00a3'+r[4].toFixed(2):'--')+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right;color:var(--t2)">'+(r[6]?'\u00a3'+r[6].toFixed(2):'--')+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right">'+discHtml+'</td>'
+'<td style="padding:5px 7px;font-size:12px">'
+statusDot
+(editIdx>=0
?'<select class="sb-status-sel" data-ei="'+editIdx+'" style="border:none;background:transparent;cursor:pointer;font-size:12px;color:'+(statusCol[r[7]]||'var(--t3)')+';">'
+'<option value="unreconciled"'+(r[7]==='unreconciled'?' selected':'')+'>Unreconciled</option>'
+'<option value="reconciled"'+(r[7]==='reconciled'?' selected':'')+'>Reconciled</option>'
+'<option value="queried"'+(r[7]==='queried'?' selected':'')+'>Queried</option>'
+'</select>'
:esc(r[7]||''))
+'</td>'
+'<td style="padding:5px 0;text-align:right">'+(editIdx>=0?'<button class="delbtn sb-del-btn" data-ei="'+editIdx+'">&#215;</button>':'')+'</td>'
+'</tr>';
}).join('');

tbody.querySelectorAll('.sb-status-sel').forEach(function(sel){
sel.addEventListener('change',function(){updateSBStatus(+this.dataset.ei,this.value);});
});
tbody.querySelectorAll('.sb-del-btn').forEach(function(btn){
btn.addEventListener('click',function(){deleteSB(+this.dataset.ei);});
});

// \u2500\u2500 SB WEEK SUMMARY \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
(function(){
var _t=new Date(),_dow=(_t.getDay()+6)%7;
var _mon=new Date(_t);_mon.setDate(_t.getDate()-_dow);_mon.setHours(0,0,0,0);
var _sun=new Date(_mon);_sun.setDate(_mon.getDate()+6);
var _f=function(d){return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');};
var wkS=_f(_mon),wkE=_f(_sun);
var wkData=getAllSB().filter(function(r){var d=r[0]||'';return d&&d>=wkS&&d<=wkE;});
var shiftKeys={};wkData.forEach(function(r){shiftKeys[(r[1]||'')+'|'+(r[2]||'')]=1;});
var wkShifts=Object.keys(shiftKeys).length;
var candKeys={};wkData.forEach(function(r){candKeys[r[1]||'']=1;});
var wkCands=Object.keys(candKeys).length;
var wkAmt=wkData.reduce(function(s,r){return s+(r[4]||0);},0);
var wkExp=wkData.reduce(function(s,r){return s+(r[6]||0);},0);
var wkMargin=Math.round((wkExp-wkAmt)*100)/100;
var hospMap={};
wkData.forEach(function(r){
var h=r[5]||'Unknown',k=(r[1]||'')+'|'+(r[2]||'')+'|'+h;
if(!hospMap[h])hospMap[h]={seen:{},n:0};
if(!hospMap[h].seen[k]){hospMap[h].seen[k]=1;hospMap[h].n++;}
});
var el=document.getElementById('sb-week-summary');
if(!el)return;
var months=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
var lbl=_mon.getDate()+' '+months[_mon.getMonth()]+' \u2013 '+_sun.getDate()+' '+months[_sun.getMonth()];
var hospKeys=Object.keys(hospMap).sort(function(a,b){return hospMap[b].n-hospMap[a].n;});
var hospHtml=hospKeys.length
?hospKeys.map(function(h){return'<div style="display:flex;justify-content:space-between;padding:4px 0;border-bottom:0.5px solid var(--b1)"><span style="font-size:12px;color:var(--t2)">'+esc(h)+'</span><span style="font-size:12px;font-weight:500">'+hospMap[h].n+'</span></div>';}).join('')
:'<div style="font-size:12px;color:var(--t3);padding:8px 0">No SB data this week \u2014 drop a file above.</div>';
el.innerHTML=
'<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:10px">This week <span style="font-weight:400;color:var(--t3);text-transform:none">'+lbl+'</span></div>'
+'<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:14px">'
+'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)"><div style="font-size:28px;font-weight:600;color:var(--tx)">'+wkShifts+'</div><div style="font-size:11px;color:var(--t2);margin-top:2px">shifts paid</div></div>'
+'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)"><div style="font-size:28px;font-weight:600;color:var(--tx)">'+wkCands+'</div><div style="font-size:11px;color:var(--t2);margin-top:2px">candidates</div></div>'
+'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)"><div style="font-size:28px;font-weight:600;color:var(--bl)">\u00a3'+wkAmt.toLocaleString('en-GB',{minimumFractionDigits:0,maximumFractionDigits:0})+'</div><div style="font-size:11px;color:var(--t2);margin-top:2px">SB total</div></div>'
+(wkExp?'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)"><div style="font-size:28px;font-weight:600;color:'+(wkMargin>=0?'var(--grtx)':'var(--amtx)')+';">'+(wkMargin>=0?'+':'')+'\u00a3'+Math.abs(wkMargin).toLocaleString('en-GB',{minimumFractionDigits:0,maximumFractionDigits:0})+'</div><div style="font-size:11px;color:var(--t2);margin-top:2px">margin</div></div>':'')
+'</div>'
+'<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:8px">Shifts by hospital</div>'
+'<div style="column-count:2;column-gap:20px">'+hospHtml+'</div>';
})();
}

function populateSBDatalists(){
var nl=document.getElementById('sb-cand-list');
if(nl)nl.innerHTML=C.filter(function(c){return c.ac!=='Inactive';})
.map(function(c){return '<option value="'+esc(c.n)+'"></option>';}).join('');
var hl=document.getElementById('sb-hosp-list');
if(hl)hl.innerHTML=getAllTrustNames().map(function(n){return '<option value="'+esc(n)+'"></option>';}).join('');
var hl2=document.getElementById('sb-hosp-list2');
if(hl2)hl2.innerHTML=getAllTrustNames().map(function(n){return '<option value="'+esc(n)+'"></option>';}).join('');
// Auto-set paste date to today
var pdEl=document.getElementById('sb-paste-date');
if(pdEl&&!pdEl.value){var _d=new Date();pdEl.value=_d.getFullYear()+'-'+String(_d.getMonth()+1).padStart(2,'0')+'-'+String(_d.getDate()).padStart(2,'0');}
// Populate hospital filter dropdown from all SB data
var hf=document.getElementById('sb-hosp-filter');
if(hf){
var hosps=[];
getAllSB().forEach(function(r){if(r[5]&&hosps.indexOf(r[5])<0)hosps.push(r[5]);});
hosps.sort();
hf.innerHTML='<option value="">All hospitals</option>'+
hosps.map(function(h){return '<option value="'+esc(h)+'">'+esc(h)+'</option>';}).join('');
}
// Auto-set SB date to today
var sdEl=document.getElementById('sb-sbdate');
if(sdEl&&!sdEl.value){
var d=new Date();
sdEl.value=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
}
}


function toggleNGrp(id,e){
if(e)e.stopPropagation();
var grp=document.getElementById('ngrp-'+id);
if(!grp)return;
var wasOpen=grp.classList.contains('open');
closeNGrps();
if(!wasOpen)grp.classList.add('open');
}

function closeNGrps(){
document.querySelectorAll('.ngrp').forEach(function(g){g.classList.remove('open');});
}

// Close dropdowns when clicking outside
document.addEventListener('click',function(e){
if(!e.target.closest('.ngrp'))closeNGrps();
});


// \u2500\u2500 LIVE PLACEMENT \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var LP_BASE=[]
var lpEdits=[];
try{var _lp=localStorage.getItem('lp_edits');if(_lp)lpEdits=JSON.parse(_lp);}catch(e){}
function saveLP(){try{localStorage.setItem('lp_edits',JSON.stringify(lpEdits));}catch(e){}}
function lpClearData(){
if(!confirm('Clear all imported placement data?'))return;
lpEdits=[];
try{localStorage.removeItem('lp_edits');}catch(e){}
try{localStorage.setItem('lp_edits','[]');}catch(e){}
rLP();
alert('Placement data cleared.');
}
function getAllLP(){return LP_BASE.concat(lpEdits);}

var lpFilter={client:'',consultant:'',q:'',dateFrom:'',dateTo:''};
var lpPage=0;
var LP_PAGE_SIZE=50;

// \u2500\u2500 LP DRAG & DROP IMPORT \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _lpImportParsed=[];

function lpInitDrop(){
var zone=document.getElementById('lp-drop-zone');
if(!zone||zone._init)return;
zone._init=true;
zone.addEventListener('dragover',function(e){e.preventDefault();this.style.borderColor='var(--bl)';this.style.background='var(--blbg)';});
zone.addEventListener('dragleave',function(){this.style.borderColor='var(--b2)';this.style.background='transparent';});
zone.addEventListener('drop',function(e){
e.preventDefault();
this.style.borderColor='var(--b2)';this.style.background='transparent';
var file=e.dataTransfer.files[0];
if(!file)return;
lpReadFile(file);
});
zone.addEventListener('click',function(){document.getElementById('lp-file-input').click();});
var fi=document.getElementById('lp-file-input');
if(fi)fi.addEventListener('change',function(){if(this.files[0])lpReadFile(this.files[0]);});

}

function lpReadFile(file){
var statusEl=document.getElementById('lp-drop-status');
if(statusEl)statusEl.textContent='Reading '+file.name+'...';
var reader=new FileReader();
reader.onload=function(e){
try{
lpParseXLSX(e.target.result, file.name);
}catch(err){
if(statusEl)statusEl.textContent='Error: '+err.message;
}
};
reader.readAsArrayBuffer(file);
}

function lpParseXLSX(buffer, filename){
var statusEl=document.getElementById('lp-drop-status');
// Use SheetJS (already available as global XLSX if loaded, else parse manually)
// SheetJS is available via the CRM's included libraries - but this is a plain HTML file
// We'll parse the binary manually for xlsx using a simple approach
// Actually: read as binary string then use the built-in approach

// Convert ArrayBuffer to binary string for SheetJS-style parsing
var data=new Uint8Array(buffer);
var bstr='';
for(var i=0;i<data.length;i++)bstr+=String.fromCharCode(data[i]);

// Load SheetJS dynamically if not already loaded
loadXLSX(function(){lpParseWithXLSX(bstr,filename);});
}

function lpParseWithXLSX(bstr, filename){
var statusEl=document.getElementById('lp-drop-status');
try{
var wb=XLSX.read(bstr,{type:'binary',cellDates:true});
var ws=wb.Sheets[wb.SheetNames[0]];
var rows=XLSX.utils.sheet_to_json(ws,{header:1,defval:''});

if(!rows||rows.length<2){
if(statusEl)statusEl.textContent='No data found in file.';
return;
}

// Find header row \u2014 look for row containing 'Consultant' or 'Candidate'
var headerIdx=-1;
var cols={consultant:-1,candidate:-1,client:-1,shiftDate:-1,paidHrs:-1,chargedHrs:-1,cost:-1,charge:-1,margin:-1,created:-1};
for(var h=0;h<Math.min(5,rows.length);h++){
var row=rows[h];
var found=false;
row.forEach(function(v,i){
var vl=(v||'').toString().toLowerCase().trim();
if(vl.includes('consultant'))cols.consultant=i;
if(vl.includes('candidate'))cols.candidate=i;
if(vl.includes('client'))cols.client=i;
if((vl.includes('shift')&&vl.includes('date'))||(vl==='shift date'))cols.shiftDate=i;
if(vl.includes('paid hrs')||vl==='paid hrs'||vl==='paid hours')cols.paidHrs=i;
if(vl.includes('charged hrs')||vl==='charged hrs'||vl==='charged hours')cols.chargedHrs=i;
if(vl.includes('actual cost')||vl==='cost')cols.cost=i;
if(vl.includes('actual charge')||vl==='charge')cols.charge=i;
if(vl.includes('actual margin')||vl==='margin')cols.margin=i;
if(vl==='c'||vl.includes('created')||vl.includes('paid date'))cols.created=i;
if(vl.includes('consultant')||vl.includes('candidate'))found=true;
});
if(found){headerIdx=h;break;}
}

if(headerIdx<0||cols.candidate<0){
if(statusEl)statusEl.textContent='Could not find column headers. Expected: Consultant Name, Candidate, Client, Shift Date.';
return;
}

// Parse data rows, filter to South Theatres only
var parsed=[];
var skipped=0;
for(var r=headerIdx+1;r<rows.length;r++){
var row=rows[r];
if(!row||!row.length)continue;
var consultant=(row[cols.consultant]||'').toString().trim();
var candidate=(row[cols.candidate]||'').toString().trim();
if(!candidate)continue;
// FILTER: only South Theatres consultant
if(consultant.toLowerCase()!=='south theatres'){skipped++;continue;}

// Parse shift date
var sdRaw=row[cols.shiftDate];
var shiftDate='';
if(sdRaw){
if(sdRaw instanceof Date){
shiftDate=sdRaw.getFullYear()+'-'+String(sdRaw.getMonth()+1).padStart(2,'0')+'-'+String(sdRaw.getDate()).padStart(2,'0');
} else {
var d=new Date(sdRaw);
if(!isNaN(d.getTime()))shiftDate=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
else shiftDate=sdRaw.toString().slice(0,10);
}
}

var sf=function(v){try{return Math.round(parseFloat((v||0).toString().replace(/[,\u00a3$]/g,''))*100)/100||0;}catch(e){return 0;}};
// Parse created date
var createdDate='';
if(cols.created>=0){
var cdRaw=row[cols.created];
if(cdRaw){
if(cdRaw instanceof Date){
createdDate=cdRaw.getFullYear()+'-'+String(cdRaw.getMonth()+1).padStart(2,'0')+'-'+String(cdRaw.getDate()).padStart(2,'0');
} else {
var cd=new Date(cdRaw);
if(!isNaN(cd.getTime()))createdDate=cd.getFullYear()+'-'+String(cd.getMonth()+1).padStart(2,'0')+'-'+String(cd.getDate()).padStart(2,'0');
}
}
}
parsed.push([
consultant,
candidate,
(row[cols.client]||'').toString().trim(),
shiftDate,
sf(row[cols.paidHrs]),
sf(row[cols.chargedHrs]),
sf(row[cols.cost]),
sf(row[cols.charge]),
sf(row[cols.margin]),
createdDate
]);
}

if(!parsed.length){
if(statusEl)statusEl.textContent='No South Theatres shifts found in file ('+skipped+' other consultants skipped).';
return;
}

// Deduplicate against existing LP data (candidate + shiftDate + charge)
var existing=getAllLP();
var existingKeys={};
existing.forEach(function(r){existingKeys[(r[1]||'')+'|'+(r[3]||'')+'|'+(r[7]||0)]=true;});

var newRows=parsed.filter(function(r){
return !existingKeys[(r[1]||'')+'|'+(r[3]||'')+'|'+(r[7]||0)];
});
var dupes=parsed.length-newRows.length;

_lpImportParsed=newRows;

if(statusEl)statusEl.textContent=filename+': '+parsed.length+' South Theatres shifts found, '+dupes+' already in system, '+newRows.length+' new.';

lpRenderImportPreview();
document.getElementById('lp-import-preview').style.display='block';

}catch(err){
if(statusEl)statusEl.textContent='Parse error: '+err.message;
console.error(err);
}
}

function lpRenderImportPreview(){
var tbody=document.getElementById('lp-import-tbody');
var countEl=document.getElementById('lp-import-count');
if(!tbody)return;
if(countEl)countEl.textContent=_lpImportParsed.length+' new shifts to add';
if(!_lpImportParsed.length){
tbody.innerHTML='<tr><td colspan="6" style="padding:16px;text-align:center;color:var(--grtx)">All shifts already in the system \u2014 nothing new to import.</td></tr>';
return;
}
tbody.innerHTML=_lpImportParsed.map(function(r,i){
return'<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 8px;font-size:12px;font-weight:500">'+esc(r[1])+'</td>'
+'<td style="padding:5px 8px;font-size:12px;color:var(--t2)">'+esc(r[2])+'</td>'
+'<td style="padding:5px 8px;font-size:12px;color:var(--t2)">'+fmtDateDMY(r[3])+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right">'+((r[4]||0)+'h')+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right;color:var(--bl);font-weight:500">\u00a3'+(r[7]||0).toFixed(2)+'</td>'
+'<td style="padding:5px 8px;font-size:12px;text-align:right;color:var(--grtx)">\u00a3'+(r[8]||0).toFixed(2)+'</td>'
+'</tr>';
}).join('');
}

function lpConfirmImport(){
if(!_lpImportParsed.length)return;
_lpImportParsed.forEach(function(r){lpEdits.push(r);});
saveLP();
var count=_lpImportParsed.length;
_lpImportParsed=[];
document.getElementById('lp-import-preview').style.display='none';
document.getElementById('lp-drop-status').textContent='';
lpPage=0;
rLP();
alert(count+' shifts imported successfully.');
}

function lpCancelImport(){
_lpImportParsed=[];
document.getElementById('lp-import-preview').style.display='none';
document.getElementById('lp-drop-status').textContent='';
}


function addPlacement(){
var consultant=document.getElementById('lp-consultant').value.trim();
var candidate=document.getElementById('lp-candidate').value.trim();
var client=document.getElementById('lp-client').value.trim();
var shiftDate=document.getElementById('lp-shiftdate').value||'';
var paidHrs=parseFloat(document.getElementById('lp-paidhrs').value)||0;
var chargedHrs=parseFloat(document.getElementById('lp-chargedhrs').value)||0;
var cost=parseFloat(document.getElementById('lp-cost').value)||0;
var charge=parseFloat(document.getElementById('lp-charge').value)||0;
var margin=Math.round((charge-cost)*100)/100;
if(!candidate){alert('Candidate is required');return;}
if(!shiftDate){alert('Shift date is required');return;}
lpEdits.push([consultant,candidate,client,shiftDate,paidHrs,chargedHrs,cost,charge,margin]);
saveLP();
document.getElementById('lp-candidate').value='';
document.getElementById('lp-shiftdate').value='';
document.getElementById('lp-paidhrs').value='';
document.getElementById('lp-chargedhrs').value='';
document.getElementById('lp-cost').value='';
document.getElementById('lp-charge').value='';
lpPage=0;
rLP();
}

function deleteLP(editIdx){
if(!confirm('Delete this entry?'))return;
lpEdits.splice(editIdx,1);
saveLP();rLP();
}

function lpSetFilter(k,v){lpFilter[k]=v;lpPage=0;rLP();}

function rLP(){
var all=getAllLP();
var q=(lpFilter.q||'').toLowerCase();
var cf=(lpFilter.client||'').toLowerCase();
var consf=(lpFilter.consultant||'').toLowerCase();
var df=lpFilter.dateFrom||'';
var dt=lpFilter.dateTo||'';

var indexed=[];
all.forEach(function(r,i){
if(cf&&!(r[2]||'').toLowerCase().includes(cf))return;
if(consf&&!(r[0]||'').toLowerCase().includes(consf))return;
if(q&&!((r[1]||'')+(r[2]||'')).toLowerCase().includes(q))return;
if(df&&(r[3]||'')<df)return;
if(dt&&(r[3]||'')>dt)return;
indexed.push({r:r,origIdx:i});
});

// Sort most recent first
indexed.sort(function(a,b){return(b.r[3]||'').localeCompare(a.r[3]||'');});

// Stats \u2014 all filtered data, deduplicate shifts by candidate+shiftDate
var totCost=indexed.reduce(function(s,o){return s+(o.r[6]||0);},0);
var totCharge=indexed.reduce(function(s,o){return s+(o.r[7]||0);},0);
var totMargin=indexed.reduce(function(s,o){return s+(o.r[8]||0);},0);
var totHrs=indexed.reduce(function(s,o){return s+(o.r[4]||0);},0);
var mPct=totCharge>0?Math.round(totMargin/totCharge*100):0;
// Shift count: deduplicate ALL data by candidate+shiftDate (not affected by filters)
var _allKeys={};
getAllLP().forEach(function(r){_allKeys[(r[1]||'')+'|'+(r[3]||'')]=1;});
var wkShiftCount=Object.keys(_allKeys).length;

var statsEl=document.getElementById('lp-stats');
if(statsEl){
statsEl.innerHTML=
'<span><strong>'+wkShiftCount+'</strong> shifts (deduplicated)</span>'
+'<span><strong>'+totHrs.toLocaleString('en-GB',{maximumFractionDigits:1})+'h</strong></span>'
+'<span>Cost: <strong>\u00a3'+totCost.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</strong></span>'
+'<span>Charge: <strong style="color:var(--bl)">\u00a3'+totCharge.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+'</strong></span>'
+'<span>Margin: <strong style="color:var(--grtx)">\u00a3'+totMargin.toLocaleString('en-GB',{minimumFractionDigits:2,maximumFractionDigits:2})+' ('+mPct+'%)</strong></span>'
;
}

// Current week summary (Mon-Sun)
var _today=new Date();
var _dow=(_today.getDay()+6)%7;
var _wkMon=new Date(_today);_wkMon.setDate(_today.getDate()-_dow);_wkMon.setHours(0,0,0,0);
var _wkSun=new Date(_wkMon);_wkSun.setDate(_wkMon.getDate()+6);
var _fmt=function(d){return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');};
var _wkStart=_fmt(_wkMon);var _wkEnd=_fmt(_wkSun);
var wkData=getAllLP().filter(function(r){
var d=r[9]||r[3]||''; // use created date, fall back to shift date
return d&&d>=_wkStart&&d<=_wkEnd;
});
// Deduplicate shifts by candidate + shift date
var wkShiftKeys2={};
wkData.forEach(function(r){wkShiftKeys2[(r[1]||'')+'|'+(r[3]||'')]=1;});
var wkShifts=Object.keys(wkShiftKeys2).length;
var wkCands={};wkData.forEach(function(r){wkCands[r[1]]=1;});
var wkCandCount=Object.keys(wkCands).length;
var wkMargin=wkData.reduce(function(s,r){return s+(r[8]||0);},0);
var wkCharge=wkData.reduce(function(s,r){return s+(r[7]||0);},0);
var wkEl=document.getElementById('lp-week-summary');
if(wkEl){
var _months=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
var wkLbl=_wkMon.getDate()+' '+_months[_wkMon.getMonth()]+' \u2013 '+_wkSun.getDate()+' '+_months[_wkSun.getMonth()];
wkEl.innerHTML=
'<div style="font-size:11px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:10px">This week <span style="font-weight:400;color:var(--t3);text-transform:none">'+wkLbl+'</span></div>'
+'<div style="display:flex;gap:12px;flex-wrap:wrap">'
+'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)">'
+'<div style="font-size:28px;font-weight:600;color:var(--tx)">'+wkShifts+'</div>'
+'<div style="font-size:11px;color:var(--t2);margin-top:2px">shifts paid</div>'
+'</div>'
+'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)">'
+'<div style="font-size:28px;font-weight:600;color:var(--tx)">'+wkCandCount+'</div>'
+'<div style="font-size:11px;color:var(--t2);margin-top:2px">candidates</div>'
+'</div>'
+'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)">'
+'<div style="font-size:28px;font-weight:600;color:var(--bl)">\u00a3'+wkCharge.toLocaleString('en-GB',{minimumFractionDigits:0,maximumFractionDigits:0})+'</div>'
+'<div style="font-size:11px;color:var(--t2);margin-top:2px">charged</div>'
+'</div>'
+'<div style="text-align:center;padding:10px 20px;background:var(--su2);border-radius:var(--r)">'
+'<div style="font-size:28px;font-weight:600;color:var(--grtx)">\u00a3'+wkMargin.toLocaleString('en-GB',{minimumFractionDigits:0,maximumFractionDigits:0})+'</div>'
+'<div style="font-size:11px;color:var(--t2);margin-top:2px">margin</div>'
+'</div>'
+'</div>'
+(wkShifts===0?'<div style="margin-top:8px;font-size:12px;color:var(--t3)">No placement data for this week yet \u2014 drop the latest report above.</div>':'');
}

// Populate client filter
var clf=document.getElementById('lp-client-filter');
if(clf&&clf.options.length<=1){
var clients=[];
all.forEach(function(r){if(r[2]&&clients.indexOf(r[2])<0)clients.push(r[2]);});
clients.sort();
clf.innerHTML='<option value="">All clients</option>'+
clients.map(function(c){return'<option value="'+esc(c)+'">'+esc(c)+'</option>';}).join('');
}

// Pagination
var totalPages=Math.ceil(indexed.length/LP_PAGE_SIZE)||1;
if(lpPage>=totalPages)lpPage=totalPages-1;
var page=indexed.slice(lpPage*LP_PAGE_SIZE,(lpPage+1)*LP_PAGE_SIZE);
var pgEl=document.getElementById('lp-pages');
if(pgEl){
pgEl.innerHTML='<span style="font-size:12px;color:var(--t2)">Page '+(lpPage+1)+' of '+totalPages+'</span>'
+'<button onclick="if(lpPage>0){lpPage--;rLP();}" style="padding:3px 9px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">\u2190</button>'
+'<button onclick="if(lpPage<'+(totalPages-1)+'){lpPage++;rLP();}" style="padding:3px 9px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">\u2192</button>'
+'<span style="font-size:11px;color:var(--t3)">Showing 600 most recent. Add new entries below.</span>';
}

var tbody=document.getElementById('lp-tbody');
if(!tbody)return;
if(!page.length){
tbody.innerHTML='<tr><td colspan="9" style="padding:24px;text-align:center;color:var(--t3)">No records match</td></tr>';
return;
}
tbody.innerHTML=page.map(function(o){
var r=o.r;
var editIdx=o.origIdx>=LP_BASE.length?o.origIdx-LP_BASE.length:-1;
var mPctRow=r[7]>0?Math.round((r[8]||0)/r[7]*100):0;
return'<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:5px 0;font-size:12px">'+fmtDateDMY(r[3])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;font-weight:500">'+esc(r[1])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+esc(r[2])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+esc(r[0])+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right">'+((r[4]||0)+'h')+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right;color:var(--t2)">\u00a3'+(r[6]||0).toFixed(2)+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right;font-weight:500;color:var(--bl)">\u00a3'+(r[7]||0).toFixed(2)+'</td>'
+'<td style="padding:5px 7px;font-size:12px;text-align:right;color:var(--grtx);font-weight:500">\u00a3'+(r[8]||0).toFixed(2)+(mPctRow?' <span style="font-size:10px;font-weight:400">('+mPctRow+'%)</span>':'')+'</td>'
+'<td style="padding:5px 7px;font-size:12px;color:var(--t2)">'+fmtDateDMY(r[9]||'')+'</td>'
+'<td style="padding:5px 0;text-align:right">'+(editIdx>=0?'<button class="delbtn lp-del-btn" data-ei="'+editIdx+'">&#215;</button>':'')+'</td>'
+'</tr>';
}).join('');
tbody.querySelectorAll('.lp-del-btn').forEach(function(btn){
btn.addEventListener('click',function(){deleteLP(+this.dataset.ei);});
});
}

function lpCalcMargin(){
var cost=parseFloat(document.getElementById('lp-cost').value)||0;
var charge=parseFloat(document.getElementById('lp-charge').value)||0;
var mEl=document.getElementById('lp-margin-disp');
if(mEl){
var m=charge-cost;
mEl.textContent=m!==0?'\u00a3'+m.toFixed(2):'--';
mEl.style.color=m>0?'var(--grtx)':m<0?'#921f1f':'var(--t2)';
}
}


// Live clock
function startClock(){
function tick(){
var now=new Date();
var h=String(now.getHours()).padStart(2,'0');
var m=String(now.getMinutes()).padStart(2,'0');
var s=String(now.getSeconds()).padStart(2,'0');
var el=document.getElementById('nav-clock');
if(el)el.textContent=h+':'+m+':'+s;
}
tick();
setInterval(tick,1000);
}
startClock();


// \u2500\u2500 PAY ONLY TIMESHEET DROP \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _poAttachedFile=null; // {name, type, dataUrl}

function poInitDrop(){
var zone=document.getElementById('po-ts-drop');
if(!zone||zone._init)return;
zone._init=true;
zone.addEventListener('dragover',function(e){e.preventDefault();this.style.borderColor='var(--bl)';this.style.background='var(--blbg)';});
zone.addEventListener('dragleave',function(){this.style.borderColor='var(--b2)';this.style.background='transparent';});
zone.addEventListener('drop',function(e){
e.preventDefault();
this.style.borderColor='var(--b2)';this.style.background='transparent';
var file=e.dataTransfer.files[0];
if(!file)return;
poReadTS(file);
});
zone.addEventListener('click',function(){document.getElementById('po-ts-input').click();});
var fi=document.getElementById('po-ts-input');
if(fi)fi.addEventListener('change',function(){if(this.files[0])poReadTS(this.files[0]);});
}

function poReadTS(file){
var reader=new FileReader();
reader.onload=function(e){
_poAttachedFile={name:file.name};
var isPdf=file.name.toLowerCase().endsWith('.pdf');
var byteStr=atob(e.target.result.split(',')[1]);
var ab=new ArrayBuffer(byteStr.length);
var ia=new Uint8Array(ab);
for(var i=0;i<byteStr.length;i++)ia[i]=byteStr.charCodeAt(i);
var mtype=isPdf?'application/pdf':'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet';
var blobUrl=URL.createObjectURL(new Blob([ab],{type:mtype}));
_poTsUrl=blobUrl;
var prev=document.getElementById('po-ts-preview');
if(!prev)return;
prev.style.display='block';
if(isPdf){
prev.innerHTML=
'<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:8px">'
+'<span style="font-size:12px;font-weight:500;color:var(--tx)">&#128196; '+esc(file.name)+'</span>'
+'<a href="'+blobUrl+'" target="_blank" style="font-size:11px;color:var(--bl);text-decoration:none">Open full size &#8599;</a>'
+'</div>'
+'<object data="'+blobUrl+'" type="application/pdf" style="width:100%;height:480px;border:0.5px solid var(--b2);border-radius:var(--r);background:#f8f8f8">'
+'<div style="padding:24px;text-align:center;color:var(--t2)">PDF preview not supported in this browser. '
+'<a href="'+blobUrl+'" target="_blank" style="color:var(--bl)">Open PDF &#8599;</a>'
+'</div>'
+'</object>';
} else {
prev.innerHTML='<div style="padding:8px 10px;background:var(--su2);border-radius:var(--r);font-size:12px;color:var(--tx)">&#128196; '+esc(file.name)+' attached</div>';
}
// Update drop zone label
var lbl=document.getElementById('po-ts-label');
if(lbl)lbl.textContent=file.name.length>15?file.name.slice(0,13)+'...':file.name;
};
reader.readAsDataURL(file);
}



function poClearTS(){
_poAttachedFile=null;
var prev=document.getElementById('po-ts-preview');
if(prev){prev.innerHTML='';prev.style.display='none';}
var si=document.getElementById('po-ts-input');if(si)si.value='';
var z=document.getElementById('po-ts-drop');if(z){z._init=false;}
poInitDrop();
}


// \u2500\u2500 TRUST CARDS \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var TRUST_CARDS=[
{name:'MSE',fullName:'Mid & South Essex NHS Foundation Trust',area:'Essex',
color:'#1a5276',
sites:[
{name:'Broomfield',img:''},
{name:'Southend',img:''},
{name:'Basildon',img:''}
]},
{name:'Barts',fullName:'Barts Health NHS Trust',area:'London',
color:'#002060',
sites:[
{name:'St Barts',img:''},
{name:'Royal London',img:'https://www.bartshealth.nhs.uk/application/files/cache/thumbnails/5e8e1c2f8a3d4.jpg'},
{name:'Whipps Cross',img:''},
{name:'Newham',img:''}
]},
{name:'Lewisham & QEH',fullName:'Lewisham and Greenwich NHS Trust',area:'London',
color:'#1b6ca8',
sites:[
{name:'Lewisham',img:''},
{name:'QEH',img:''}
]},
{name:'Homerton',fullName:'Homerton University Hospital NHS Foundation Trust',area:'London',
color:'#145a32',
sites:[
{name:'Homerton',img:'https://www.homerton.nhs.uk/application/files/cache/thumbnails/homerton-building.jpg'}
]},
{name:'Royal Surrey',fullName:'Royal Surrey NHS Foundation Trust',area:'Surrey',
color:'#154360',
sites:[
{name:'Royal Surrey',img:''}
]},
{name:'East Surrey',fullName:'Surrey and Sussex Healthcare NHS Trust',area:'Surrey',
color:'#4a235a',
sites:[
{name:'East Surrey',img:''},
{name:'Crawley',img:''}
]},
{name:'QVH',fullName:'Queen Victoria Hospital NHS Foundation Trust',area:'East Grinstead',
color:'#1a5276',
sites:[
{name:'QVH',img:'https://www.qvh.nhs.uk/application/files/cache/thumbnails/qvh-building.jpg'},
{name:'DVH',img:''}
]},
{name:'Luton & Bedford',fullName:'Bedfordshire Hospitals NHS Foundation Trust',area:'Bedfordshire',
color:'#154360',
sites:[
{name:'Luton',img:''},
{name:'Bedford',img:''}
]},
{name:'Watford',fullName:'West Hertfordshire Teaching Hospitals NHS Trust',area:'Hertfordshire',
color:'#1b4f72',
sites:[
{name:'Watford',img:''},
{name:'St Albans',img:''}
]},
{name:'Royal Berkshire',fullName:'Royal Berkshire NHS Foundation Trust',area:'Reading',
color:'#1a5276',
sites:[
{name:'Royal Berkshire',img:''}
]},
{name:'Ramsay',fullName:'Ramsay Health Care UK',area:'Private',
color:'#c0392b',
sites:[
{name:'Ramsay',img:''}
]},
{name:'Cromwell',fullName:'Cromwell Hospital',area:'London',
color:'#1a3a5c',
sites:[
{name:'Cromwell',img:''}
]},
{name:'Spa Medica',fullName:'Spa Medica',area:'Private',
color:'#117a65',
sites:[
{name:'Spa Medica',img:''}
]}
];

// Trust card image overrides from localStorage
var tcImgEdits={};
try{var _tci=localStorage.getItem('tc_imgs');if(_tci)tcImgEdits=JSON.parse(_tci);}catch(e){}
function saveTCImgs(){try{localStorage.setItem('tc_imgs',JSON.stringify(tcImgEdits));}catch(e){}}
var tcGeoEdits={};
try{var _tg=localStorage.getItem('tc_geo');if(_tg)tcGeoEdits=JSON.parse(_tg);}catch(e){}
function saveTCGeo(){try{localStorage.setItem('tc_geo',JSON.stringify(tcGeoEdits));}catch(e){}}

// Split view state
var _splitMode=false;
var _splitHospA=null,_splitHospB=null;


// \u2500\u2500 TODO / TASK MANAGER \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _tasks=[];
var _recurring=[];
var _todoLoaded=false;

function loadTasks(){
try{var t=localStorage.getItem('dw_tasks');if(t)_tasks=JSON.parse(t);}catch(e){}
try{var r=localStorage.getItem('dw_recurring');if(r)_recurring=JSON.parse(r);}catch(e){}
}

function saveTasks(){
try{localStorage.setItem('dw_tasks',JSON.stringify(_tasks));}catch(e){}
}

function saveRecurring(){
try{localStorage.setItem('dw_recurring',JSON.stringify(_recurring));}catch(e){}
}

function todayStr(){
var d=new Date();
return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
}

function todoRollover(){
// Bump incomplete past tasks to today
var today=todayStr();
var changed=false;
_tasks.forEach(function(t){
if(!t.done&&t.due&&t.due<today){t.due=today;changed=true;}
});
if(changed)saveTasks();
}

function todoGenerateRecurring(){
// Generate tasks from recurring templates for today if not already generated
var today=todayStr();
var d=new Date();
var dayOfWeek=d.getDay(); // 0=Sun,1=Mon...6=Sat
var dayNames=['sunday','monday','tuesday','wednesday','thursday','friday','saturday'];
_recurring.forEach(function(tmpl){
if(tmpl.paused)return;
var shouldGenerate=false;
if(tmpl.freq==='daily')shouldGenerate=true;
else if(tmpl.freq==='weekdays')shouldGenerate=(dayOfWeek>=1&&dayOfWeek<=5);
else if(tmpl.freq==='weekly')shouldGenerate=(tmpl.day===dayNames[dayOfWeek]);
else if(tmpl.freq==='monthly')shouldGenerate=(d.getDate()===parseInt(tmpl.dayOfMonth||1));
if(!shouldGenerate)return;
// Check not already generated today
var exists=_tasks.some(function(t){return t.recurringId===tmpl.id&&t.due===today;});
if(!exists){
_tasks.push({
id:'t'+Date.now()+Math.random(),
type:tmpl.type,
note:tmpl.note,
cand:tmpl.cand||'',
hosp:tmpl.hosp||'',
due:today,
done:false,
recurringId:tmpl.id,
created:today
});
}
});
saveTasks();
}

function rTodo(){
if(!_todoLoaded){loadTasks();_todoLoaded=true;}
todoRollover();
todoGenerateRecurring();

var el=document.getElementById('todo-main');
if(!el)return;

var today=todayStr();
var typeColors={
'Call':'var(--bl)','Email':'#6c3fc5','Chase':'var(--amtx)','Admin':'var(--t2)'
};
var typeBg={
'Call':'var(--blbg)','Email':'#f0ebff','Chase':'var(--ambg)','Admin':'var(--su2)'
};

var todayTasks=_tasks.filter(function(t){return t.due===today&&!t.done;});
var doneTodayTasks=_tasks.filter(function(t){return t.due===today&&t.done;});
var upcomingTasks=_tasks.filter(function(t){return t.due>today&&!t.done;}).sort(function(a,b){return a.due<b.due?-1:1;});

// Group today by type
var types=['Call','Email','Chase','Admin'];

var html='';

// \u2500\u2500 Quick add bar \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var candOpts=C.filter(function(c){return c.ac!=='Inactive';}).map(function(c){
return'<option value="'+esc(c.n)+'">'+esc(c.n)+'</option>';
}).join('');
var hospOpts=getAllSitesList().map(function(s){
return'<option value="'+esc(s)+'">'+esc(s)+'</option>';
}).join('');

html+='<div style="display:grid;grid-template-columns:340px 1fr;gap:16px;align-items:start;margin-bottom:16px">'
// Add task form - compact left column
+'<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px">'
+'<div class="sh" style="margin-bottom:10px">Add task</div>'
+'<div style="display:flex;flex-direction:column;gap:8px">'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase;letter-spacing:.05em">Type</div>'
+'<select id="todo-type" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option>Call</option><option>Email</option><option>Chase</option><option>Admin</option>'
+'</select>'
+'</div>'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase;letter-spacing:.05em">Due date</div>'
+'<input id="todo-due" type="date" value="'+today+'" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box">'
+'</div>'
+'</div>'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase;letter-spacing:.05em">Task</div>'
+'<input id="todo-note" type="text" placeholder="What needs doing?" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box">'
+'</div>'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase;letter-spacing:.05em">Candidate</div>'
+'<select id="todo-cand" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">-- none --</option>'+candOpts
+'</select>'
+'</div>'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase;letter-spacing:.05em">Hospital</div>'
+'<select id="todo-hosp" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">-- none --</option>'+hospOpts
+'</select>'
+'</div>'
+'<button onclick="todoAdd()" class="ef-save" style="width:100%;padding:7px 14px">+ Add task</button>'
+'</div>'
+'</div>'
// Today + Upcoming - right column 
+'<div id="todo-right-col">'
+'</div>'
+'</div>';

// \u2500\u2500 Today \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
// Close the grid wrapper and inject right column content via innerHTML after render
// Actually build right col content as separate var then inject
var rightHtml='';
rightHtml+='<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px">'
+'<div class="sh" style="margin:0">Today</div>'
+'<div style="font-size:12px;color:var(--t3)">'+new Date().toLocaleDateString('en-GB',{weekday:'long',day:'numeric',month:'long'})+'</div>'
+'</div>';

if(!todayTasks.length&&!doneTodayTasks.length){
rightHtml+='<div style="padding:24px;text-align:center;color:var(--t3);font-size:13px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);margin-bottom:16px">&#10003; Nothing due today</div>';
} else {
// Group by type
var hasAny=false;
types.forEach(function(type){
var typeTasks=todayTasks.filter(function(t){return t.type===type;});
if(!typeTasks.length)return;
hasAny=true;
rightHtml+='<div style="margin-bottom:12px">'
+'<div style="font-size:11px;font-weight:600;color:'+typeColors[type]+';text-transform:uppercase;letter-spacing:.08em;margin-bottom:6px;display:flex;align-items:center;gap:6px">'
+'<span style="display:inline-block;width:8px;height:8px;border-radius:50%;background:'+typeColors[type]+'"></span>'+type
+'</div>';
typeTasks.forEach(function(t){rightHtml+=todoCard(t,typeColors,typeBg);});
rightHtml+='</div>';
});
if(!hasAny)rightHtml+='<div style="padding:16px;text-align:center;color:var(--t3);font-size:13px">All done!</div>';
}

// \u2500\u2500 Upcoming \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
if(upcomingTasks.length){
rightHtml+='<div class="sh" style="margin:16px 0 10px">Upcoming</div>';
var upDates=[...new Set(upcomingTasks.map(function(t){return t.due;}))];
upDates.slice(0,14).forEach(function(date){
var dateTasks=upcomingTasks.filter(function(t){return t.due===date;});
var d=new Date(date+'T12:00:00');
var label=d.toLocaleDateString('en-GB',{weekday:'short',day:'numeric',month:'short'});
rightHtml+='<div style="margin-bottom:10px">'
+'<div style="font-size:11px;font-weight:500;color:var(--t2);margin-bottom:5px;padding-bottom:4px;border-bottom:0.5px solid var(--b1)">'+label+'</div>';
dateTasks.forEach(function(t){rightHtml+=todoCard(t,typeColors,typeBg);});
rightHtml+='</div>';
});
}

// \u2500\u2500 Done today (collapsed) \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
if(doneTodayTasks.length){
rightHtml+='<details style="margin-top:16px">'
+'<summary style="font-size:12px;color:var(--t3);cursor:pointer;padding:6px 0;list-style:none">\u2713 '+doneTodayTasks.length+' completed today</summary>'
+'<div style="margin-top:6px;opacity:.6">';
doneTodayTasks.forEach(function(t){rightHtml+=todoCard(t,typeColors,typeBg);});
rightHtml+='</div></details>';
}

// \u2500\u2500 Recurring templates \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
html+='<div style="margin-top:24px;border-top:0.5px solid var(--b1);padding-top:16px">'
+'<div style="display:flex;align-items:center;margin-bottom:10px">'
+'<div class="sh" style="margin:0;flex:1">Recurring tasks</div>'
+'<button onclick="todoShowRecurringForm()" class="edit-btn">+ Add recurring</button>'
+'</div>'
+'<div id="todo-recurring-form" style="display:none;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:12px 14px;margin-bottom:12px">'
+'<div style="display:grid;grid-template-columns:110px 1fr 130px 1fr;gap:8px;margin-bottom:8px">'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Type</div>'
+'<select id="rec-type" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option>Call</option><option>Email</option><option>Chase</option><option>Admin</option>'
+'</select>'
+'</div>'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Task</div>'
+'<input id="rec-note" type="text" placeholder="e.g. Chase self-bills" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box">'
+'</div>'
+'<div>'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Repeat</div>'
+'<select id="rec-freq" onchange="todoFreqChange()" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="daily">Every day</option>'
+'<option value="weekdays">Weekdays only</option>'
+'<option value="weekly">Weekly on...</option>'
+'<option value="monthly">Monthly on day...</option>'
+'</select>'
+'</div>'
+'<div id="rec-day-wrap">'
+'<div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Day</div>'
+'<select id="rec-day" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="monday">Monday</option><option value="tuesday">Tuesday</option>'
+'<option value="wednesday">Wednesday</option><option value="thursday">Thursday</option>'
+'<option value="friday">Friday</option><option value="saturday">Saturday</option>'
+'<option value="sunday">Sunday</option>'
+'</select>'
+'</div>'
+'</div>'
+'<div style="display:flex;gap:8px;align-items:center">'
+'<select id="rec-cand" style="flex:1;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">No candidate</option>'+candOpts
+'</select>'
+'<select id="rec-hosp" style="flex:1;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">No hospital</option>'+hospOpts
+'</select>'
+'<button onclick="todoAddRecurring()" class="ef-save" style="padding:6px 14px">Save</button>'
+'<button onclick="document.getElementById(\'todo-recurring-form\').style.display=\'none\'" style="padding:6px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>'
+'</div>'
+'</div>';

if(_recurring.length){
_recurring.forEach(function(tmpl){
var freqLabel={daily:'Every day',weekdays:'Weekdays',weekly:'Every '+tmpl.day,monthly:'Monthly day '+tmpl.dayOfMonth}[tmpl.freq]||tmpl.freq;
html+='<div style="display:flex;align-items:center;gap:10px;padding:8px 10px;background:var(--su2);border-radius:var(--r);margin-bottom:5px">'
+'<span style="font-size:10px;font-weight:600;padding:2px 7px;border-radius:10px;background:'+typeBg[tmpl.type]+';color:'+typeColors[tmpl.type]+'">'+tmpl.type+'</span>'
+'<span style="font-size:12px;flex:1;color:var(--tx)">'+esc(tmpl.note)+'</span>'
+(tmpl.cand?'<span style="font-size:11px;color:var(--t2)">'+esc(tmpl.cand)+'</span>':'')
+(tmpl.hosp?'<span style="font-size:11px;color:var(--t2)">'+esc(tmpl.hosp)+'</span>':'')
+'<span style="font-size:11px;color:var(--t3)">'+freqLabel+'</span>'
+'<button onclick="todoToggleRecurring(\''+tmpl.id+'\')" style="font-size:10px;padding:2px 7px;border:0.5px solid var(--b2);border-radius:10px;background:transparent;cursor:pointer;color:var(--t2)">'+(tmpl.paused?'Resume':'Pause')+'</button>'
+'<button onclick="todoDeleteRecurring(\''+tmpl.id+'\')" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:14px;padding:0 2px">&#215;</button>'
+'</div>';
});
} else {
html+='<div style="font-size:12px;color:var(--t3);padding:8px 0">No recurring tasks set up yet</div>';
}
html+='</div>';

el.innerHTML=html;
// Append quiet clients panel to right col
var rc2=document.getElementById('todo-right-col');
if(rc2){
rc2.innerHTML=rightHtml;
var qcWrap=document.createElement('div');
qcWrap.id='todo-quiet-clients';
qcWrap.style.cssText='background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-top:14px';
rc2.appendChild(qcWrap);
}
loadHospActivity();
renderQuietClients();
renderPipelineOverdue();
}

function todoCard(t,typeColors,typeBg){
var tc=typeColors[t.type]||'var(--t2)';
var tb=typeBg[t.type]||'var(--su2)';
return'<div style="display:flex;align-items:flex-start;gap:10px;padding:9px 12px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--r);margin-bottom:5px;'+(t.done?'opacity:.5':'')+'">'
+'<input type="checkbox"'+(t.done?' checked':'')+' onchange="todoToggle(\''+t.id+'\')" style="margin-top:2px;cursor:pointer;flex-shrink:0">'
+'<div style="flex:1;min-width:0">'
+'<div style="display:flex;align-items:center;gap:6px;flex-wrap:wrap">'
+'<span style="font-size:10px;font-weight:600;padding:2px 7px;border-radius:10px;background:'+tb+';color:'+tc+'">'+t.type+'</span>'
+(t.recurringId?'<span style="font-size:9px;color:var(--t3)" title="Recurring task">&#8635;</span>':'')
+(t.cand?'<span style="font-size:11px;color:var(--bl);cursor:pointer" onclick="gp(\'candidates\')">'+esc(t.cand)+'</span>':'')
+(t.hosp?'<span style="font-size:11px;color:var(--t2)">'+esc(t.hosp)+'</span>':'')
+'</div>'
+'<div style="font-size:13px;color:var(--tx);margin-top:3px;'+(t.done?'text-decoration:line-through':'')+'">'+esc(t.note)+'</div>'
+'</div>'
+'<button onclick="todoDelete(\''+t.id+'\')" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:14px;padding:0;flex-shrink:0;opacity:.5" onmouseover="this.style.opacity=1" onmouseout="this.style.opacity=.5">&#215;</button>'
+'</div>';
}

function todoAdd(){
var type=(document.getElementById('todo-type')||{}).value||'Call';
var note=((document.getElementById('todo-note')||{}).value||'').trim();
var cand=(document.getElementById('todo-cand')||{}).value||'';
var hosp=(document.getElementById('todo-hosp')||{}).value||'';
var due=(document.getElementById('todo-due')||{}).value||todayStr();
if(!note){alert('Please enter a task description');return;}
_tasks.push({id:'t'+Date.now(),type:type,note:note,cand:cand,hosp:hosp,due:due,done:false,created:todayStr()});
saveTasks();
rTodo();
}

function todoToggle(id){
var t=_tasks.find(function(t){return t.id===id;});
if(t)t.done=!t.done;
saveTasks();rTodo();
}

function todoDelete(id){
_tasks=_tasks.filter(function(t){return t.id!==id;});
saveTasks();rTodo();
}

function todoShowRecurringForm(){
var f=document.getElementById('todo-recurring-form');
if(f)f.style.display=f.style.display==='none'?'block':'none';
}

function todoFreqChange(){
var freq=(document.getElementById('rec-freq')||{}).value;
var wrap=document.getElementById('rec-day-wrap');
if(wrap)wrap.style.display=(freq==='weekly')?'block':'none';
}

function todoAddRecurring(){
var type=(document.getElementById('rec-type')||{}).value||'Call';
var note=((document.getElementById('rec-note')||{}).value||'').trim();
var freq=(document.getElementById('rec-freq')||{}).value||'daily';
var day=(document.getElementById('rec-day')||{}).value||'monday';
var cand=(document.getElementById('rec-cand')||{}).value||'';
var hosp=(document.getElementById('rec-hosp')||{}).value||'';
if(!note){alert('Please enter a task description');return;}
_recurring.push({id:'r'+Date.now(),type:type,note:note,freq:freq,day:day,cand:cand,hosp:hosp,paused:false});
saveRecurring();rTodo();
}

function todoToggleRecurring(id){
var t=_recurring.find(function(r){return r.id===id;});
if(t)t.paused=!t.paused;
saveRecurring();rTodo();
}

function todoDeleteRecurring(id){
_recurring=_recurring.filter(function(r){return r.id!==id;});
saveRecurring();rTodo();
}


// \u2500\u2500 HOSPITAL ACTIVITY LOG \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _hospActivity={}; // {hospName: [{date,note,tag,auto}]}
var _hospSnooze={}; // {hospName: {until,reason}}

function loadHospActivity(){
try{var a=localStorage.getItem('hosp_activity');if(a)_hospActivity=JSON.parse(a);}catch(e){}
try{var s=localStorage.getItem('hosp_snooze');if(s)_hospSnooze=JSON.parse(s);}catch(e){}
}

function saveHospActivity(){
try{localStorage.setItem('hosp_activity',JSON.stringify(_hospActivity));}catch(e){}
}

function saveHospSnooze(){
try{localStorage.setItem('hosp_snooze',JSON.stringify(_hospSnooze));}catch(e){}
}

function addHospActivityEntry(hospName,note,tag,auto){
if(!_hospActivity[hospName])_hospActivity[hospName]=[];
_hospActivity[hospName].unshift({
date:todayStr(),
note:note,
tag:tag||'',
auto:!!auto,
id:'a'+Date.now()
});
saveHospActivity();
}

function getQuietClients(){
var today=new Date();
var todayS=todayStr();
var dayOfWeek=today.getDay();

// Get all LP + PO records to count recent shifts per hospital
var allLP=getAllLP();
var allPO=(PO_BASE||[]).concat(poEdits||[]);

function getWeekStart(d){
var day=d.getDay();
var diff=d.getDate()-(day===0?6:day-1);
var mon=new Date(d);mon.setDate(diff);
return mon.toISOString().slice(0,10);
}
var thisWeekStart=getWeekStart(today);
var lastWeekDate=new Date(today);lastWeekDate.setDate(today.getDate()-7);
var lastWeekStart=getWeekStart(lastWeekDate);

function countLiveShifts(hospName,weekStart){
var weekEnd=new Date(weekStart);weekEnd.setDate(weekEnd.getDate()+7);
var weE=weekEnd.toISOString().slice(0,10);
var count=0;
allLP.forEach(function(r){
var client=(r[2]||'').toString().toLowerCase();
var date=(r[3]||'').toString().slice(0,10);
if(client.includes(hospName.toLowerCase())&&date>=weekStart&&date<weE)count++;
});
allPO.forEach(function(r){
var hosp=(r[1]||'').toString().toLowerCase();
var date=(r[3]||'').toString().slice(0,10);
if(hosp.toLowerCase().includes(hospName.toLowerCase())&&date>=weekStart&&date<weE)count++;
});
return count;
}

var results=[];
HC.forEach(function(hc){
// Skip if snoozed
var snooze=_hospSnooze[hc.name];
if(snooze&&snooze.until>=todayS)return;

var weekly=hc.weekly||[];
var nonZero=weekly.filter(function(v){return v>0;});
if(!nonZero.length)return;
var avg=nonZero.reduce(function(a,b){return a+b;},0)/nonZero.length;
if(avg<1)return;

// Check for known reasons in activity log
var recentLog=(_hospActivity[hc.name]||[]).find(function(e){
return e.date>=lastWeekStart&&(e.tag==='Refurbishment'||e.tag==='Planned closure'||e.tag==='Seasonal');
});
if(recentLog)return;
// Dismiss for today if a note was logged today (any tag)
var loggedToday=(_hospActivity[hc.name]||[]).find(function(e){return e.date===todayS;});
if(loggedToday)return;

// Use live LP/PO data if available, otherwise fall back to weekly[] tail
var hasLiveData=allLP.length>0||allPO.length>0;
var thisWeek,lastWeek;
if(hasLiveData){
thisWeek=countLiveShifts(hc.name,thisWeekStart);
lastWeek=countLiveShifts(hc.name,lastWeekStart);
} else {
// Fall back to weekly[] \u2014 last two entries
var len=weekly.length;
thisWeek=weekly[len-1]||0;
lastWeek=weekly[len-2]||0;
}

var alert=null;
if(avg>=3&&thisWeek===0&&lastWeek===0){
alert={level:'red',msg:'Usually '+Math.round(avg)+' shifts/wk \u2014 nothing in 2 weeks'};
} else if(avg>=2&&(thisWeek+lastWeek)<avg*0.5){
alert={level:'amber',msg:'Below average \u2014 '+thisWeek+' this wk, '+lastWeek+' last wk (avg '+Math.round(avg)+')'};
} else if(avg>=1&&thisWeek===0&&lastWeek===0){
if(dayOfWeek!==1)return;
alert={level:'grey',msg:'Quiet this week \u2014 worth a check (avg '+avg.toFixed(1)+'/wk)'};
}

if(alert){
results.push({
name:hc.name,
alert:alert,
avg:avg,
thisWeek:thisWeek,
lastWeek:lastWeek,
log:(_hospActivity[hc.name]||[]).slice(0,3),
contact:(function(){
var allCts=(hc.contacts||[]).concat(gHE(hc.name).contacts||[]);
return allCts.find(function(c){return c.primary===true;})||allCts[0]||null;
})()
});
}
});

var order={red:0,amber:1,grey:2};
results.sort(function(a,b){return order[a.alert.level]-order[b.alert.level];});
return results;
}

function renderQuietClients(){
var el=document.getElementById('todo-quiet-clients');
if(!el)return;
if(!Object.keys(_hospActivity).length&&!Object.keys(_hospSnooze).length){
loadHospActivity();
}

var clients=getQuietClients();
var levelColor={red:'#c0392b',amber:'var(--amtx)',grey:'var(--t3)'};
var levelBg={red:'#fdf0ee',amber:'var(--ambg)',grey:'var(--su2)'};

var html='<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px">'
+'<div class="sh" style="margin:0">Quiet clients</div>'
+'<span style="font-size:11px;color:var(--t3)">'+clients.length+' flagged</span>'
+'</div>';

if(!clients.length){
html+='<div style="padding:16px;text-align:center;color:var(--t3);font-size:12px;background:var(--su2);border-radius:var(--r)">All clients active &#10003;</div>';
el.innerHTML=html;return;
}

clients.forEach(function(c){
var lc=levelColor[c.alert.level];
var lb=levelBg[c.alert.level];
var logId='qc-log-'+c.name.replace(/[^a-z0-9]/gi,'_');
var lastEntry=c.log[0];

html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--r);margin-bottom:8px;overflow:hidden">'
// Header
+'<div style="display:flex;align-items:flex-start;gap:8px;padding:10px 12px">'
+'<div style="width:8px;height:8px;border-radius:50%;background:'+lc+';flex-shrink:0;margin-top:4px"></div>'
+'<div style="flex:1;min-width:0">'
+'<div style="font-size:13px;font-weight:500;color:var(--tx)">'+esc(c.name)+'</div>'
+'<div style="font-size:11px;color:'+lc+';margin-top:1px">'+esc(c.alert.msg)+'</div>'
+(lastEntry?'<div style="font-size:10px;color:var(--t3);margin-top:3px">Last note: '+esc(lastEntry.note.slice(0,50))+(lastEntry.note.length>50?'\u2026':'')+'</div>':'')
+'</div>'
// Action buttons
+'<div style="display:flex;flex-direction:column;gap:4px;align-items:flex-end">'
+'<div style="display:flex;gap:4px">'
+(c.contact&&(c.contact.email||c.contact.phone)?'<a href="'+(c.contact.email?'mailto:'+esc(c.contact.email):'tel:'+esc(c.contact.phone||''))+'" style="padding:3px 8px;background:var(--blbg);color:var(--bl);border-radius:20px;font-size:10px;font-weight:600;text-decoration:none;white-space:nowrap">&#9993; '+(c.contact.email?'Email':'Call')+'</a>':'')
+'<button onclick="qcShowLog(\''+c.name+'\')" style="padding:3px 8px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:10px;color:var(--t2)">Log</button>'
+'<button onclick="qcSnooze(\''+c.name+'\')" style="padding:3px 8px;border:0.5px solid var(--b2);border-radius:20px;background:transparent;cursor:pointer;font-size:10px;color:var(--t2)">Snooze</button>'
+'</div>'
+'</div>'
+'</div>'
// Expandable log + add entry
+'<div id="'+logId+'" style="display:none;border-top:0.5px solid var(--b1);padding:10px 12px;background:var(--su2)">'
+'<div style="font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.06em;margin-bottom:7px">Activity log</div>'
+(c.log.length?c.log.map(function(e){
return'<div style="display:flex;gap:8px;padding:5px 0;border-bottom:0.5px solid var(--b1);font-size:11px">'
+'<span style="color:var(--t3);white-space:nowrap;flex-shrink:0">'+e.date+'</span>'
+(e.tag?'<span style="padding:1px 6px;border-radius:10px;background:var(--su);font-size:10px;color:var(--t2);flex-shrink:0">'+esc(e.tag)+'</span>':'')
+'<span style="color:var(--tx)">'+esc(e.note)+'</span>'
+'</div>';
}).join(''):'<div style="font-size:11px;color:var(--t3);padding:4px 0">No entries yet</div>')
// Add entry form
+'<div style="margin-top:8px;display:flex;gap:6px;align-items:center">'
+'<select id="log-tag-'+c.name.replace(/[^a-z0-9]/gi,'_')+'" style="padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+'<option value="">Tag</option>'
+'<option>Called</option><option>Emailed</option><option>Refurbishment</option>'
+'<option>Planned closure</option><option>Surgeon absent</option>'
+'<option>D&amp;V outbreak</option><option>Seasonal</option><option>Recovered</option><option>Other</option>'
+'</select>'
+'<input id="log-note-'+c.name.replace(/[^a-z0-9]/gi,'_')+'" type="text" placeholder="Add note\u2026" style="flex:1;padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+'<button onclick="qcAddLog(\''+c.name+'\')" class="ef-save" style="padding:4px 10px;font-size:11px;white-space:nowrap">Save</button>'
+'</div>'
+'</div>'
+'</div>';
});

el.innerHTML=html;
}

function qcShowLog(name){
var id='qc-log-'+name.replace(/[^a-z0-9]/gi,'_');
var el=document.getElementById(id);
if(el)el.style.display=el.style.display==='none'?'block':'none';
}

function qcAddLog(name){
var safeId=name.replace(/[^a-z0-9]/gi,'_');
var tag=(document.getElementById('log-tag-'+safeId)||{}).value||'';
var note=((document.getElementById('log-note-'+safeId)||{}).value||'').trim();
if(!note)return;
addHospActivityEntry(name,note,tag,false);
renderQuietClients();
}

function qcSnooze(name){
var safeId=name.replace(/[^a-z0-9]/gi,'_');
var logDiv=document.getElementById('qc-log-'+safeId);
if(!logDiv)return;
// Toggle existing snooze form
var existingForm=logDiv.querySelector('.snooze-form');
if(existingForm){existingForm.remove();return;}
logDiv.style.display='block';
var form=document.createElement('div');
form.className='snooze-form';
form.style.cssText='padding:8px 0;border-top:0.5px solid var(--b1);margin-top:8px';
form.innerHTML='<div style="font-size:11px;font-weight:600;color:var(--t2);margin-bottom:6px">Snooze for 7 days \u2014 reason:</div>'
+'<div style="display:flex;gap:6px;align-items:center">'
+'<select class="snooze-reason-sel" style="flex:1;padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+'<option>Spoke to them</option><option>Emailed</option><option>Known closure</option><option>Seasonal</option><option>Other</option>'
+'</select>'
+'<button class="ef-save snooze-confirm" data-name="'+name+'" style="padding:4px 10px;font-size:11px">Snooze</button>'
+'<button class="snooze-cancel" style="padding:4px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">Cancel</button>'
+'</div>';
logDiv.appendChild(form);
form.querySelector('.snooze-confirm').addEventListener('click',function(){
var reason=form.querySelector('.snooze-reason-sel').value;
qcConfirmSnooze(name,reason);
});
form.querySelector('.snooze-cancel').addEventListener('click',function(){form.remove();});
}

function qcConfirmSnooze(name,reason){
var until=new Date();until.setDate(until.getDate()+7);
_hospSnooze[name]={until:until.toISOString().slice(0,10),reason:reason||'Spoke to them'};
saveHospSnooze();
addHospActivityEntry(name,'Snoozed 7 days: '+(reason||'Spoke to them'),'Called',false);
renderQuietClients();
}

function qcConfirmSnooze(name){
var safeId=name.replace(/[^a-z0-9]/gi,'_');
var reason=(document.getElementById('snooze-reason-'+safeId)||{}).value||'Spoke to them';
var until=new Date();until.setDate(until.getDate()+7);
_hospSnooze[name]={until:until.toISOString().slice(0,10),reason:reason};
saveHospSnooze();
addHospActivityEntry(name,'Snoozed 7 days: '+reason,'Called',false);
renderQuietClients();
}


// \u2500\u2500 DOCUMENTS \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
// Each doc: {id, name, type, tag, hospital, data, size, uploaded}
// type: 'general' | 'hospital'
// tag: 'Timesheet' | 'Checklist' | 'Rate confirmation' | 'Other'

var _docs=[];
function loadDocs(){try{var d=localStorage.getItem('dw_docs');if(d)_docs=JSON.parse(d);}catch(e){}}
function saveDocs(){try{localStorage.setItem('dw_docs',JSON.stringify(_docs));}catch(e){alert('Storage full \u2014 try removing old documents first.');}}
var _docsLoaded=false;
var _docsHospFilter='';

function rDocs(){
if(!_docsLoaded){loadDocs();_docsLoaded=true;}
var el=document.getElementById('docs-main');
if(!el)return;

var hospOpts='<option value="">All hospitals</option>'
+getAllSitesList().map(function(s){return'<option value="'+esc(s)+'"'+(s===_docsHospFilter?' selected':'')+'>'+esc(s)+'</option>';}).join('');

var tagColors={
'Timesheet':'var(--blbg)','Checklist':'#f0ebff',
'Rate confirmation':'var(--ambg)','Other':'var(--su2)'
};
var tagTx={
'Timesheet':'var(--bl)','Checklist':'#6c3fc5',
'Rate confirmation':'var(--amtx)','Other':'var(--t2)'
};
var tagAccept={
'Timesheet':'.pdf','Checklist':'.doc,.docx',
'Rate confirmation':'.pdf,.eml,.msg,.png,.jpg,.jpeg','Other':'*'
};

var html='<div style="display:grid;grid-template-columns:1fr 1fr;gap:20px">';

// \u2500\u2500 LEFT: General docs \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
html+='<div>'
+'<div style="display:flex;align-items:center;margin-bottom:12px">'
+'<div class="sh" style="margin:0;flex:1">General documents</div>'
+'<button onclick="docsShowUpload(\'general\')" class="edit-btn">+ Upload</button>'
+'</div>'
+'<div id="docs-upload-general" style="display:none;background:var(--su2);border-radius:var(--r);padding:12px;margin-bottom:12px">'+docsUploadForm('general')+'</div>';

var generalDocs=_docs.filter(function(d){return d.type==='general';});
if(generalDocs.length){
generalDocs.forEach(function(d){html+=docsCard(d,tagColors,tagTx);});
} else {
html+='<div style="padding:24px;text-align:center;color:var(--t3);font-size:12px;background:var(--su2);border-radius:var(--r)">No general documents yet</div>';
}
html+='</div>';

// \u2500\u2500 RIGHT: Hospital docs \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
html+='<div>'
+'<div style="display:flex;align-items:center;gap:8px;margin-bottom:12px">'
+'<div class="sh" style="margin:0;flex:1">Hospital documents</div>'
+'<select onchange="_docsHospFilter=this.value;rDocs()" style="padding:5px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'+hospOpts+'</select>'
+'<button onclick="docsShowUpload(\'hospital\')" class="edit-btn">+ Upload</button>'
+'</div>'
+'<div id="docs-upload-hospital" style="display:none;background:var(--su2);border-radius:var(--r);padding:12px;margin-bottom:12px">'+docsUploadForm('hospital')+'</div>';

var hospDocs=_docs.filter(function(d){
return d.type==='hospital'&&(!_docsHospFilter||d.hospital===_docsHospFilter);
});

if(hospDocs.length){
// Group by hospital
var hospGroups={};
hospDocs.forEach(function(d){
if(!hospGroups[d.hospital])hospGroups[d.hospital]=[];
hospGroups[d.hospital].push(d);
});
Object.keys(hospGroups).sort().forEach(function(hosp){
html+='<div style="margin-bottom:14px">'
+'<div style="font-size:11px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.06em;margin-bottom:6px;padding-bottom:4px;border-bottom:0.5px solid var(--b1)">'+esc(hosp)+'</div>';
hospGroups[hosp].forEach(function(d){html+=docsCard(d,tagColors,tagTx);});
html+='</div>';
});
} else {
html+='<div style="padding:24px;text-align:center;color:var(--t3);font-size:12px;background:var(--su2);border-radius:var(--r)">'
+(_docsHospFilter?'No documents for '+esc(_docsHospFilter):'No hospital documents yet')+'</div>';
}
html+='</div>';

html+='</div>';
el.innerHTML=html;
}

function docsUploadForm(type){
var hospSel=type==='hospital'
?'<div style="margin-bottom:8px"><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Hospital</div>'
+'<select id="docs-up-hosp-'+type+'" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">-- select hospital --</option>'
+getAllSitesList().map(function(s){return'<option value="'+esc(s)+'">'+esc(s)+'</option>';}).join('')
+'</select></div>'
:'';
return hospSel
+'<div style="margin-bottom:8px;display:grid;grid-template-columns:1fr 1fr;gap:8px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Document name</div>'
+'<input id="docs-up-name-'+type+'" type="text" placeholder="e.g. Homerton Checklist Jan 2026" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Type</div>'
+'<select id="docs-up-tag-'+type+'" onchange="docsTagChange(\''+type+'\')" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option>Timesheet</option><option>Checklist</option><option>Rate confirmation</option><option>Other</option>'
+'</select></div>'
+'</div>'
// Rate confirmation date fields (hidden by default)
+'<div id="docs-up-dates-'+type+'" style="display:none;margin-bottom:8px;display:none">'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Rate start date *</div>'
+'<input id="docs-up-start-'+type+'" type="date" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Rate end date <span style="color:var(--t3)">(optional)</span></div>'
+'<input id="docs-up-end-'+type+'" type="date" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'</div>'
+'</div>'
+'<div style="margin-bottom:8px"><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">File</div>'
+'<input id="docs-up-file-'+type+'" type="file" accept=".pdf,.doc,.docx,.eml,.msg,.png,.jpg,.jpeg" style="font-size:12px;color:var(--t2)"></div>'
+'<div style="display:flex;gap:6px">'
+'<button onclick="docsUpload(\''+type+'\')" class="ef-save" style="padding:5px 14px">Upload</button>'
+'<button onclick="docsShowUpload(\''+type+'\')" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>'
+'</div>';
}

function docsTagChange(type){
var tag=(document.getElementById('docs-up-tag-'+type)||{}).value||'';
var datesEl=document.getElementById('docs-up-dates-'+type);
if(datesEl)datesEl.style.display=tag==='Rate confirmation'?'block':'none';
}



function docsCard(d,tagColors,tagTx){
var initials=d.name.replace(/\.[^.]+$/,'').split(/\s+/).filter(function(w){return w.length>0;}).map(function(w){return w[0].toUpperCase();}).join('').slice(0,3);
var sizeFmt=d.size>1024*1024?(d.size/1024/1024).toFixed(1)+'MB':(d.size/1024).toFixed(0)+'KB';
var _tb=(tagColors&&tagColors[d.tag])||'var(--blbg)';
var _tc=(tagTx&&tagTx[d.tag])||'var(--bl)';
return'<div style="display:flex;align-items:center;gap:10px;padding:10px 12px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--r);margin-bottom:6px">' +'<div style="width:36px;height:36px;border-radius:var(--r);background:'+_tb+';color:'+_tc+';display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0;letter-spacing:.02em">'+initials+'</div>'+'<div style="flex:1;min-width:0">'
+'<div style="font-size:13px;font-weight:500;color:var(--tx);white-space:nowrap;overflow:hidden;text-overflow:ellipsis">'+esc(d.name)+'</div>'
+'<div style="display:flex;gap:8px;margin-top:2px;align-items:center">'
+'<span style="font-size:10px;font-weight:600;padding:1px 7px;border-radius:10px;background:'+(tagColors[d.tag]||'var(--su2)')+';color:'+(tagTx[d.tag]||'var(--t2)')+'">'+esc(d.tag)+'</span>'
+'<span style="font-size:10px;color:var(--t3)">'+sizeFmt+'</span>'
+'<span style="font-size:10px;color:var(--t3)">'+esc(d.uploaded)+'</span>'+(d.rateStart?'<span style="font-size:10px;color:var(--amtx);margin-left:4px">'+fmtDateDMY(d.rateStart)+(d.rateEnd?' \u2192 '+fmtDateDMY(d.rateEnd):' \u2192 ongoing')+'</span>':'')
+'</div>'
+'</div>'
+'<a href="'+d.data+'" download="'+esc(d.name)+'" style="padding:4px 10px;background:var(--blbg);color:var(--bl);border-radius:20px;font-size:11px;font-weight:600;text-decoration:none;white-space:nowrap;flex-shrink:0">&#8595; Download</a>'
+'<button onclick="docsDelete(\''+d.id+'\')" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:16px;padding:0 2px;flex-shrink:0">&#215;</button>'
+'</div>';
}

function docsShowUpload(type){
var el=document.getElementById('docs-upload-'+type);
if(!el)return;
el.style.display=el.style.display==='none'?'block':'none';
var ni=document.getElementById('docs-up-name-'+type);if(ni)ni.value='';
var fi=document.getElementById('docs-up-file-'+type);if(fi)fi.value='';
}

function docsUpload(type){
var name=(document.getElementById('docs-up-name-'+type)||{}).value||'';
var tag=(document.getElementById('docs-up-tag-'+type)||{}).value||'Other';
var hosp=type==='hospital'?((document.getElementById('docs-up-hosp-'+type)||{}).value||''):'';
var rateStart=(document.getElementById('docs-up-start-'+type)||{}).value||'';
var rateEnd=(document.getElementById('docs-up-end-'+type)||{}).value||'';
var fi=document.getElementById('docs-up-file-'+type);
if(!fi||!fi.files||!fi.files[0]){alert('Please select a file');return;}
if(type==='hospital'&&!hosp){alert('Please select a hospital');return;}
if(tag==='Rate confirmation'&&!rateStart){alert('Please enter a rate start date');return;}
var file=fi.files[0];
if(!name)name=file.name;
if(file.size>3*1024*1024){alert('File too large (max 3MB). Try compressing it first.');return;}
var reader=new FileReader();
reader.onload=function(e){
_docs.push({
id:'doc'+Date.now(),
name:name,
type:type,
tag:tag,
hospital:hosp,
rateStart:rateStart||'',
rateEnd:rateEnd||'',
data:e.target.result,
size:file.size,
uploaded:todayStr()
});
saveDocs();
_docsLoaded=true;
rDocs();
};
reader.readAsDataURL(file);
}



function docsDelete(id){
if(!confirm('Remove this document?'))return;
_docs=_docs.filter(function(d){return d.id!==id;});
saveDocs();
rDocs();
}

// Render hospital docs inline on hospital detail page
function renderHospDocs(hospName,containerId){
var el=document.getElementById(containerId);
if(!el)return;
if(!_docsLoaded){loadDocs();_docsLoaded=true;}
var hospDocs=_docs.filter(function(d){return d.type==='hospital'&&d.hospital===hospName;});
var tagColors={'Timesheet':'var(--blbg)','Checklist':'#f0ebff','Rate confirmation':'var(--ambg)','Other':'var(--su2)'};
var tagTx={'Timesheet':'var(--bl)','Checklist':'#6c3fc5','Rate confirmation':'var(--amtx)','Other':'var(--t2)'};
var html='';
hospDocs.forEach(function(d){html+=docsCard(d,tagColors,tagTx);});
if(!hospDocs.length)html='<div style="font-size:12px;color:var(--t3);margin-bottom:8px">No documents attached yet</div>';
// Add upload button
html+='<button class="edit-btn docs-hosp-upload-btn" data-hosp="'+esc(hospName)+'">+ Attach document</button>'
+'<div class="docs-hosp-upload-form" style="display:none;margin-top:8px;padding:10px;background:var(--su2);border-radius:var(--r)">'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:8px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Name</div>'
+'<input class="docs-hi-name" type="text" placeholder="Document name" style="width:100%;padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Type</div>'
+'<select class="docs-hi-tag" style="width:100%;padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option>Checklist</option><option>Rate confirmation</option><option>Timesheet</option><option>Other</option>'
+'</select></div>'
+'</div>'
+'<div style="margin-bottom:8px"><input class="docs-hi-file" type="file" accept=".pdf,.doc,.docx,.eml,.msg,.png,.jpg,.jpeg" style="font-size:11px;color:var(--t2)"></div>'
+'<div style="display:flex;gap:6px">'
+'<button class="ef-save docs-hi-submit" data-hosp="'+esc(hospName)+'" style="padding:4px 12px;font-size:12px">Upload</button>'
+'<button class="docs-hi-cancel" style="padding:4px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>'
+'</div>'
+'</div>';
el.innerHTML=html;
// Wire upload toggle
var uploadBtn=el.querySelector('.docs-hosp-upload-btn');
var uploadForm=el.querySelector('.docs-hosp-upload-form');
if(uploadBtn&&uploadForm){
uploadBtn.addEventListener('click',function(){uploadForm.style.display=uploadForm.style.display==='none'?'block':'none';});
}
var cancelBtn=el.querySelector('.docs-hi-cancel');
if(cancelBtn&&uploadForm)cancelBtn.addEventListener('click',function(){uploadForm.style.display='none';});
// Wire submit
var submitBtn=el.querySelector('.docs-hi-submit');
if(submitBtn){
submitBtn.addEventListener('click',function(){
var form=el.querySelector('.docs-hosp-upload-form');
var nameEl=el.querySelector('.docs-hi-name');
var tagEl=el.querySelector('.docs-hi-tag');
var fileEl=el.querySelector('.docs-hi-file');
if(!fileEl||!fileEl.files||!fileEl.files[0]){alert('Please select a file');return;}
var file=fileEl.files[0];
if(file.size>3*1024*1024){alert('File too large (max 3MB)');return;}
var docName=nameEl?nameEl.value.trim()||file.name:file.name;
var tag=tagEl?tagEl.value:'Other';
var reader=new FileReader();
reader.onload=function(e){
_docs.push({id:'doc'+Date.now(),name:docName,type:'hospital',tag:tag,hospital:hospName,data:e.target.result,size:file.size,uploaded:todayStr()});
saveDocs();_docsLoaded=true;
openHosp(hospName);
};
reader.readAsDataURL(file);
});
}
}


function docsShowHospUpload(hospName){
var safeId=hospName.replace(/[^a-z0-9]/gi,'_');
var el=document.getElementById('docs-hosp-up-'+safeId);
if(el)el.style.display=el.style.display==='none'?'block':'none';
}

function docsUploadHosp(hospName){
var safeId=hospName.replace(/[^a-z0-9]/gi,'_');
var name=(document.getElementById('docs-hi-name-'+safeId)||{}).value||'';
var tag=(document.getElementById('docs-hi-tag-'+safeId)||{}).value||'Other';
var fi=document.getElementById('docs-hi-file-'+safeId);
if(!fi||!fi.files||!fi.files[0]){alert('Please select a file');return;}
var file=fi.files[0];
if(!name)name=file.name;
if(file.size>3*1024*1024){alert('File too large (max 3MB)');return;}
var reader=new FileReader();
reader.onload=function(e){
_docs.push({id:'doc'+Date.now(),name:name,type:'hospital',tag:tag,hospital:hospName,data:e.target.result,size:file.size,uploaded:todayStr()});
saveDocs();_docsLoaded=true;
openHosp(hospName);
};
reader.readAsDataURL(file);
}


// \u2500\u2500 PAY QUERIES \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
// Record: {id,cand,shiftDate,client,problem,resolution,latestUpdate,nextActionFor,status,agent,created}
// status: 'open' | 'inprogress' | 'completed'
// nextActionFor: 'Consultant'|'Client'|'Payroll'|'Sales Support'|'Candidate'|'Self-bill'|'Compliance'

var _pq=[];
var _pqLoaded=false;
var _pqFilter={status:'inprogress',actionFor:'',agent:'',q:''};

function loadPQ(){try{var d=localStorage.getItem('dw_pq');if(d)_pq=JSON.parse(d);}catch(e){}}
function savePQ(){try{localStorage.setItem('dw_pq',JSON.stringify(_pq));}catch(e){}}

var _pqAgents=['Rachel','Josh','Jason','Other'];
var _pqActionFor=['Consultant','Client','Payroll','Sales Support','Candidate','Self-bill','Compliance'];
var _pqStatuses={open:'Open',inprogress:'In progress',completed:'Completed'};
var _pqStatusColors={open:'var(--amtx)',inprogress:'var(--bl)',completed:'var(--grtx)'};
var _pqStatusBg={open:'var(--ambg)',inprogress:'var(--blbg)',completed:'var(--grbg)'};

function rPQ(){
if(!_pqLoaded){loadPQ();_pqLoaded=true;}
var el=document.getElementById('pq-main');
if(!el)return;

var candOpts=C.filter(function(c){return c.ac!=='Inactive';}).map(function(c){
return'<option value="'+esc(c.n)+'">'+esc(c.n)+'</option>';
}).join('');
var hospOpts=getAllSitesList().map(function(s){
return'<option value="'+esc(s)+'">'+esc(s)+'</option>';
}).join('');

var openCount=_pq.filter(function(q){return q.status==='open';}).length;
var inProgCount=_pq.filter(function(q){return q.status==='inprogress';}).length;
var compCount=_pq.filter(function(q){return q.status==='completed';}).length;

var html='';

// Stats bar
html+='<div style="display:flex;gap:8px;margin-bottom:14px;align-items:center;flex-wrap:wrap">';
html+='<div onclick="pqSetFilter(\'status\',\'open\')" style="padding:8px 16px;background:var(--ambg);border-radius:var(--r);text-align:center;cursor:pointer;'+((_pqFilter.status==='open')?'outline:2px solid var(--amtx)':'')+'">'
+'<div style="font-size:18px;font-weight:600;color:var(--amtx)">'+openCount+'</div>'
+'<div style="font-size:10px;color:var(--amtx);text-transform:uppercase;letter-spacing:.05em">Open</div>'
+'</div>';
html+='<div onclick="pqSetFilter(\'status\',\'inprogress\')" style="padding:8px 16px;background:var(--blbg);border-radius:var(--r);text-align:center;cursor:pointer;'+((_pqFilter.status==='inprogress')?'outline:2px solid var(--bl)':'')+'">'
+'<div style="font-size:18px;font-weight:600;color:var(--bl)">'+inProgCount+'</div>'
+'<div style="font-size:10px;color:var(--bl);text-transform:uppercase;letter-spacing:.05em">In progress</div>'
+'</div>';
html+='<div onclick="pqSetFilter(\'status\',\'completed\')" style="padding:8px 16px;background:var(--grbg);border-radius:var(--r);text-align:center;cursor:pointer;'+((_pqFilter.status==='completed')?'outline:2px solid var(--grtx)':'')+'">'
+'<div style="font-size:18px;font-weight:600;color:var(--grtx)">'+compCount+'</div>'
+'<div style="font-size:10px;color:var(--grtx);text-transform:uppercase;letter-spacing:.05em">Completed</div>'
+'</div>';
html+='<button onclick="pqShowAll()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">Show all</button>';
html+='<div style="display:flex;gap:6px;margin-left:auto;align-items:center;flex-wrap:wrap">'
+'<input id="pq-search" type="text" placeholder="Search\u2026" value="'+esc(_pqFilter.q)+'" oninput="_pqFilter.q=this.value;rPQ()" style="padding:5px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;width:160px">'
+'<select onchange="pqSetFilter(\'actionFor\',this.value)" style="padding:5px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">All action for</option>'
+_pqActionFor.map(function(a){return'<option value="'+a+'"'+(_pqFilter.actionFor===a?' selected':'')+'>'+a+'</option>';}).join('')
+'</select>'
+'<select onchange="pqSetFilter(\'agent\',this.value)" style="padding:5px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">All agents</option>'
+_pqAgents.map(function(a){return'<option value="'+a+'"'+(_pqFilter.agent===a?' selected':'')+'>'+a+'</option>';}).join('')
+'</select>'
+'<button onclick="pqShowAdd()" class="ef-save" style="padding:5px 14px">+ New query</button>'
+'</div>';
html+='</div>';

// Add form
html+='<div id="pq-add-form" style="display:none;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:14px">'
+'<div class="sh" style="margin-bottom:10px">New pay query</div>'
+'<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:8px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Candidate *</div>'
+'<input id="pq-cand" type="text" list="pq-cand-list" placeholder="Candidate name" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box">'
+'<datalist id="pq-cand-list">'+candOpts+'</datalist></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Shift date(s)</div>'
+'<div style="display:flex;flex-direction:column;gap:4px">'
+'<div id="pq-date-chips" style="display:flex;flex-wrap:wrap;gap:4px;min-height:20px"></div>'
+'<div style="display:flex;gap:4px;align-items:center">'
+'<input id="pq-date-pick" type="date" style="flex:1;padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+'<button onclick="pqAddDateChip()" style="padding:4px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">+ Add</button>'
+'<button onclick="pqAddDateRange()" style="padding:4px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:11px;color:var(--t2)">Range</button>'
+'</div>'
// Range row (hidden by default)
+'<div id="pq-range-row" style="display:none;gap:4px;align-items:center">'
+'<input id="pq-date-from" type="date" style="flex:1;padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+'<span style="font-size:11px;color:var(--t3)">\u2192</span>'
+'<input id="pq-date-to" type="date" style="flex:1;padding:5px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+'<button onclick="pqConfirmRange()" style="padding:4px 8px;border:0.5px solid var(--bl);border-radius:var(--r);background:var(--blbg);cursor:pointer;font-size:11px;color:var(--bl)">\u2713</button>'
+'</div>'
+'<input type="hidden" id="pq-date" value="">'
+'</div>'
+'</div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Client</div>'
+'<input id="pq-client" type="text" list="pq-hosp-list" placeholder="Hospital / trust" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box">'
+'<datalist id="pq-hosp-list">'+hospOpts+'</datalist></div>'
+'</div>'
+'<div style="margin-bottom:8px"><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Problem *</div>'
+'<input id="pq-problem" type="text" placeholder="Describe the pay issue" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:8px;margin-bottom:10px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Resolution</div>'
+'<input id="pq-resolution" type="text" placeholder="Steps being taken" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Next action for</div>'
+'<select id="pq-actionfor" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">-- select --</option>'
+_pqActionFor.map(function(a){return'<option>'+a+'</option>';}).join('')
+'</select></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Agent</div>'
+'<select id="pq-agent" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+'<option value="">-- select --</option>'
+_pqAgents.map(function(a){return'<option>'+a+'</option>';}).join('')
+'</select></div>'
+'<div style="display:flex;align-items:flex-end;gap:6px">'
+'<button onclick="pqAdd()" class="ef-save" style="flex:1;padding:7px">Save</button>'
+'<button onclick="pqShowAdd()" style="padding:7px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>'
+'</div>'
+'</div>'
+'</div>';

// Filter queries
var filtered=_pq.filter(function(q){
if(_pqFilter.status&&q.status!==_pqFilter.status)return false;
if(_pqFilter.actionFor&&q.nextActionFor!==_pqFilter.actionFor)return false;
if(_pqFilter.agent&&q.agent!==_pqFilter.agent)return false;
if(_pqFilter.q){
var s=_pqFilter.q.toLowerCase();
if(!((q.cand||'')+(q.client||'')+(q.problem||'')+(q.resolution||'')).toLowerCase().includes(s))return false;
}
return true;
});

if(!filtered.length){
html+='<div style="padding:32px;text-align:center;color:var(--t3);font-size:13px;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl)">'
+'No '+(_pqFilter.status?(_pqStatuses[_pqFilter.status]||'').toLowerCase()+' ':'')+' pay queries'
+'</div>';
el.innerHTML=html;return;
}

html+='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;white-space:nowrap">Status</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Candidate</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;white-space:nowrap">Shift date</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Client</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Problem</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Resolution</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;white-space:nowrap">Latest update</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;white-space:nowrap">Action for</th>'
+'<th style="padding:6px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Agent</th>'
+'<th></th>'
+'</tr></thead><tbody>';

filtered.forEach(function(q){
var sc=_pqStatusColors[q.status]||'var(--t2)';
var sb=_pqStatusBg[q.status]||'var(--su2)';
html+='<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:6px 8px;white-space:nowrap">'
+'<span style="display:inline-block;padding:2px 8px;border-radius:20px;font-size:10px;font-weight:600;background:'+sb+';color:'+sc+';cursor:pointer" '
+'onclick="pqCycleStatus(\''+q.id+'\')" title="Click to advance status">'+esc(_pqStatuses[q.status]||q.status)+'</span>'
+'</td>'
+'<td style="padding:6px 8px;font-weight:500;color:var(--tx);white-space:nowrap">'+esc(q.cand||'')+'</td>'
+'<td style="padding:6px 8px;color:var(--t2);white-space:nowrap">'+esc(q.shiftDate||'')+'</td>'
+'<td style="padding:6px 8px;color:var(--t2);white-space:nowrap">'+esc(q.client||'')+'</td>'
+'<td style="padding:6px 8px;color:var(--tx);max-width:200px">'+esc(q.problem||'')+'</td>'
+'<td style="padding:6px 8px;color:var(--t2);max-width:180px">'+esc(q.resolution||'')+'</td>'
+'<td style="padding:4px 8px;max-width:180px">'
+'<input type="text" value="'+esc(q.latestUpdate||'')+'" placeholder="Add update\u2026" '
+'onblur="pqUpdateField(\''+q.id+'\',\'latestUpdate\',this.value)" '
+'onkeydown="if(event.key===\'Enter\')this.blur()" '
+'style="width:100%;padding:3px 6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none;box-sizing:border-box">'
+'</td>'
+'<td style="padding:4px 8px;white-space:nowrap">'
+'<select onchange="pqUpdateField(\''+q.id+'\',\'nextActionFor\',this.value)" '
+'style="padding:3px 6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none">'
+'<option value="">--</option>'
+_pqActionFor.map(function(a){return'<option'+(q.nextActionFor===a?' selected':'')+'>'+a+'</option>';}).join('')
+'</select>'
+'</td>'
+'<td style="padding:6px 8px;color:var(--t2);white-space:nowrap">'+esc(q.agent||'')+'</td>'
+'<td style="padding:6px 4px;text-align:right;white-space:nowrap">'
+'<button onclick="pqExpand(\''+q.id+'\')" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:11px;padding:2px 4px" title="Edit">\u270e</button>'
+'<button onclick="pqDelete(\''+q.id+'\')" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:14px;padding:2px 4px">&times;</button>'
+'</td>'
+'</tr>'
+'<tr id="pq-expand-'+q.id+'" style="display:none;background:var(--su2)">'
+'<td colspan="10" style="padding:10px 12px">'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Problem</div>'
+'<input type="text" value="'+esc(q.problem||'')+'" onblur="pqUpdateField(\''+q.id+'\',\'problem\',this.value)" style="width:100%;padding:5px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Resolution</div>'
+'<input type="text" value="'+esc(q.resolution||'')+'" onblur="pqUpdateField(\''+q.id+'\',\'resolution\',this.value)" style="width:100%;padding:5px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'</div>'
+'</td>'
+'</tr>';
});
html+='</tbody></table></div>';
el.innerHTML=html;
}



function dashGoTrust(el){
var trust=el.getAttribute('data-trust');
if(!trust)return;
// Find matching trust card
var tc=TRUST_CARDS.find(function(t){
return t.name===trust||t.name.toLowerCase()===trust.toLowerCase();
});
if(!tc){
// Fuzzy fallback
tc=TRUST_CARDS.find(function(t){
return t.name.toLowerCase().includes(trust.toLowerCase())||
trust.toLowerCase().includes(t.name.toLowerCase());
});
}
if(!tc){alert('Could not find "'+trust+'" in your trust register.');return;}
// Use the same navigation as clicking a trust card
var siteName=tc.sites&&tc.sites[0]?tc.sites[0].name:tc.name;
_activeTrust=tc.name;
_activeHosp=siteName;
_hospView='hospital';
gp('hospitals');
}


function dashDcTab(i){
loadDCMap();
_dashDcActiveTab=i;
// Update tab styles
var sel=document.getElementById('dash-dc-sel');
if(sel)sel.value=i;
var barsEl=document.getElementById('dash-dc-bars');
if(!barsEl||!_dcReports[i])return;
var rows=_dcReports[i].rows;
// Group by client
var byClient={};
rows.forEach(function(r){
var k=_dcMap[r.client]||r.client.replace(/^SB\s*-\s*\w+\s*-\s*/i,'').replace('NHS Foundation Trust','NHS FT').replace(' NHS Trust','').trim();
if(!byClient[k])byClient[k]={shifts:0,margin:0};
byClient[k].shifts++;
byClient[k].margin+=r.margin;
});
var clientList=Object.keys(byClient).sort(function(a,b){return byClient[b].shifts-byClient[a].shifts;});
var maxS=Math.max.apply(null,clientList.map(function(k){return byClient[k].shifts;}));
barsEl.innerHTML=clientList.map(function(k){
var d=byClient[k];
var pct=maxS>0?Math.round(d.shifts/maxS*100):0;
var isNeg=d.margin<0;
return'<div class="hrow">'
+'<span class="hrow-name" onclick="dashGoTrust(this)" data-trust="'+esc(k)+'" style="cursor:pointer;color:var(--tx)">'+esc(k)+'</span>'
+'<div class="hrow-bar-w"><div class="hrow-bar" style="width:'+pct+'%"></div></div>'
+'<span class="hrow-n">'+d.shifts+'</span>'
+'<span class="hrow-m" style="color:'+(isNeg?'var(--amtx)':'var(--grtx)')+'">'+'\u00a3'+(d.margin<0?'-':'')+Math.abs(Math.round(d.margin))+'</span>'
+'</div>';
}).join('');
}

function pqShowAll(){_pqFilter.status='';rPQ();}

function pqSetFilter(key,val){
_pqFilter[key]=_pqFilter[key]===val?'':val;
rPQ();
}

function pqShowAdd(){
var f=document.getElementById('pq-add-form');
if(f)f.style.display=f.style.display==='none'?'block':'none';
}

var _pqDateChips=[]; // array of {type:'single'|'range', from, to, label}

function pqAddDateChip(){
var d=(document.getElementById('pq-date-pick')||{}).value||'';
if(!d)return;
var parts=d.split('-');
var label=parts[2]+'/'+parts[1]+(parts[0]!==new Date().getFullYear().toString()?'/'+parts[0].slice(2):'');
_pqDateChips.push({type:'single',from:d,to:d,label:label});
pqRenderChips();
var dp=document.getElementById('pq-date-pick');if(dp)dp.value='';
}

function pqAddDateRange(){
var row=document.getElementById('pq-range-row');
if(row)row.style.display=row.style.display==='none'?'flex':'none';
}

function pqConfirmRange(){
var f=(document.getElementById('pq-date-from')||{}).value||'';
var t=(document.getElementById('pq-date-to')||{}).value||'';
if(!f){alert('Please select a start date');return;}
var fmtDate=function(d){var p=d.split('-');return p[2]+'/'+p[1];};
var label=fmtDate(f)+(t&&t!==f?' \u2013 '+fmtDate(t):'');
_pqDateChips.push({type:'range',from:f,to:t||f,label:label});
pqRenderChips();
var row=document.getElementById('pq-range-row');if(row)row.style.display='none';
var ff=document.getElementById('pq-date-from');if(ff)ff.value='';
var ft=document.getElementById('pq-date-to');if(ft)ft.value='';
}

function pqRenderChips(){
var el=document.getElementById('pq-date-chips');
if(!el)return;
el.innerHTML=_pqDateChips.map(function(c,i){
return'<span style="display:inline-flex;align-items:center;gap:4px;padding:2px 8px;background:var(--blbg);color:var(--bl);border-radius:20px;font-size:11px;font-weight:500">'
+c.label
+'<button onclick="pqRemoveChip('+i+')" style="background:none;border:none;cursor:pointer;color:var(--bl);font-size:12px;padding:0;line-height:1">&times;</button>'
+'</span>';
}).join('');
// Update hidden input
var hid=document.getElementById('pq-date');
if(hid)hid.value=_pqDateChips.map(function(c){return c.label;}).join(', ');
}

function pqRemoveChip(i){
_pqDateChips.splice(i,1);
pqRenderChips();
}

function pqResetDateChips(){
_pqDateChips=[];
pqRenderChips();
var row=document.getElementById('pq-range-row');
if(row)row.style.display='none';
}


function pqAdd(){
var cand=(document.getElementById('pq-cand')||{}).value||'';
var date=(document.getElementById('pq-date')||{}).value||'';
var client=(document.getElementById('pq-client')||{}).value||'';
var problem=(document.getElementById('pq-problem')||{}).value||'';
var resolution=(document.getElementById('pq-resolution')||{}).value||'';
var actionFor=(document.getElementById('pq-actionfor')||{}).value||'';
var agent=(document.getElementById('pq-agent')||{}).value||'';
if(!cand){alert('Candidate is required');return;}
if(!problem){alert('Problem description is required');return;}
_pq.unshift({
id:'pq'+Date.now(),
cand:cand,shiftDate:date,client:client,
problem:problem,resolution:resolution,
latestUpdate:'',nextActionFor:actionFor,
status:'open',agent:agent,
created:todayStr()
});
savePQ();
_pqFilter.status='open';
pqResetDateChips();
pqShowAdd();
rPQ();
}

function pqCycleStatus(id){
var q=_pq.find(function(q){return q.id===id;});
if(!q)return;
var cycle={open:'inprogress',inprogress:'completed',completed:'open'};
q.status=cycle[q.status]||'open';
savePQ();rPQ();
}

function pqUpdateField(id,field,val){
var q=_pq.find(function(q){return q.id===id;});
if(!q)return;
q[field]=val;
savePQ();
// Re-render only if status filter changed significantly
}

function pqExpand(id){
var row=document.getElementById('pq-expand-'+id);
if(row)row.style.display=row.style.display==='none'?'table-row':'none';
}

function pqDelete(id){
if(!confirm('Remove this pay query?'))return;
_pq=_pq.filter(function(q){return q.id!==id;});
savePQ();rPQ();
}


// \u2500\u2500 DIV CON \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
var _dcReports=[]; // [{weekLabel, imported, rows:[{cand,client,date,hrs,pay,charge,margin,cons}]}]
var _dcLoaded=false;
var _dcActiveIdx=-1; // index of currently viewed report
var _dcFilter={q:'',client:'',showNeg:false};



function loadDC(){try{var d=localStorage.getItem('dw_divcon');if(d)_dcReports=JSON.parse(d);}catch(e){}}
function saveDC(){try{localStorage.setItem('dw_divcon',JSON.stringify(_dcReports));}catch(e){alert('Storage full \u2014 try removing older reports.');}}

function rDivCon(){
if(!_dcLoaded){loadDC();_dcLoaded=true;}
var el=document.getElementById('divcon-main');
if(!el)return;
var html='';

// Header + import
html+='<div style="display:flex;align-items:center;gap:10px;margin-bottom:16px;flex-wrap:wrap">'
+'<div class="sh" style="margin:0;flex:1">Div Con</div>'
+'<button onclick="dcShowMapping()" style="padding:5px 12px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Map trusts</button>'
+'<label style="padding:5px 14px;background:var(--bl);color:#fff;border-radius:var(--r);cursor:pointer;font-size:12px;font-weight:500">'
+'&#8679; Import report'
+'<input type="file" accept=".xlsx,.xls" onchange="dcImport(this)" style="display:none">'
+'</label>'
+'</div>';

// Report tabs
if(_dcReports.length){
html+='<div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:14px">';
_dcReports.forEach(function(r,i){
var active=i===_dcActiveIdx;
html+='<div style="display:flex;align-items:center;gap:0">'
+'<button onclick="dcViewReport('+i+')" style="padding:5px 12px;border:0.5px solid '+(active?'var(--bl)':'var(--b2)')+';border-radius:var(--r) 0 0 var(--r);background:'+(active?'var(--bl)':'transparent')+';color:'+(active?'#fff':'var(--t2)')+';cursor:pointer;font-size:12px">'+esc(r.weekLabel)+'</button>'
+'<button onclick="dcDeleteReport('+i+')" style="padding:5px 7px;border:0.5px solid var(--b2);border-left:none;border-radius:0 var(--r) var(--r) 0;background:transparent;cursor:pointer;font-size:11px;color:var(--t3)">&times;</button>'
+'</div>';
});
html+='</div>';
}

if(_dcActiveIdx<0||!_dcReports[_dcActiveIdx]){
html+='<div style="padding:48px;text-align:center;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl)">'
+'<div style="font-size:32px;margin-bottom:8px">&#128202;</div>'
+'<div style="font-size:14px;color:var(--t2);margin-bottom:4px">No report loaded</div>'
+'<div style="font-size:12px;color:var(--t3)">Import a Div Con spreadsheet to get started</div>'
+'</div>';
el.innerHTML=html;return;
}

var rep=_dcReports[_dcActiveIdx];
var rows=rep.rows;

// Apply filters
var filtered=rows.filter(function(r){
if(_dcFilter.showNeg&&r.margin>=0)return false;
if(_dcFilter.client&&!r.client.toLowerCase().includes(_dcFilter.client.toLowerCase()))return false;
if(_dcFilter.q){
var s=_dcFilter.q.toLowerCase();
if(!(r.cand+r.client).toLowerCase().includes(s))return false;
}
return true;
});

// Summary cards
var totalMargin=rows.reduce(function(s,r){return s+r.margin;},0);
var totalPay=rows.reduce(function(s,r){return s+r.pay;},0);
var totalCharge=rows.reduce(function(s,r){return s+r.charge;},0);
var totalHrs=rows.reduce(function(s,r){return s+r.hrs;},0);
var negCount=rows.filter(function(r){return r.margin<0;}).length;

// Check returning shifts vs previous reports
var prevKeys={};
_dcReports.forEach(function(r,i){
if(i===_dcActiveIdx)return;
r.rows.forEach(function(row){
prevKeys[row.cand+'|'+row.date+'|'+row.client]=true;
});
});
var returningCount=rows.filter(function(r){return prevKeys[r.cand+'|'+r.date+'|'+r.client];}).length;

html+='<div style="display:grid;grid-template-columns:repeat(5,1fr);gap:8px;margin-bottom:14px">'
+'<div style="background:var(--su2);border-radius:var(--r);padding:10px 12px;text-align:center">'
+'<div style="font-size:20px;font-weight:600;color:var(--grtx)">\u00a3'+Math.round(totalMargin).toLocaleString()+'</div>'
+'<div style="font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.05em">Total margin</div>'
+'</div>'
+'<div style="background:var(--su2);border-radius:var(--r);padding:10px 12px;text-align:center">'
+'<div style="font-size:20px;font-weight:600;color:var(--bl)">\u00a3'+Math.round(totalCharge).toLocaleString()+'</div>'
+'<div style="font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.05em">Total charge</div>'
+'</div>'
+'<div style="background:var(--su2);border-radius:var(--r);padding:10px 12px;text-align:center">'
+'<div style="font-size:20px;font-weight:600;color:var(--tx)">'+Math.round(totalHrs)+'h</div>'
+'<div style="font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.05em">Hours</div>'
+'</div>'
+'<div style="background:'+(negCount?'var(--ambg)':'var(--su2)')+';border-radius:var(--r);padding:10px 12px;text-align:center;cursor:'+(negCount?'pointer':'default')+'" onclick="'+(negCount?'_dcFilter.showNeg=!_dcFilter.showNeg;rDivCon()':'')+'">'
+'<div style="font-size:20px;font-weight:600;color:'+(negCount?'var(--amtx)':'var(--t3)')+'">'+negCount+'</div>'
+'<div style="font-size:10px;color:'+(negCount?'var(--amtx)':'var(--t3)')+';text-transform:uppercase;letter-spacing:.05em">Negatives</div>'
+'</div>'
+'<div style="background:'+(returningCount?'var(--blbg)':'var(--su2)')+';border-radius:var(--r);padding:10px 12px;text-align:center">'
+'<div style="font-size:20px;font-weight:600;color:'+(returningCount?'var(--bl)':'var(--t3)')+'">'+returningCount+'</div>'
+'<div style="font-size:10px;color:'+(returningCount?'var(--bl)':'var(--t3)')+';text-transform:uppercase;letter-spacing:.05em">Returning</div>'
+'</div>'
+'</div>';

// Per-trust margin breakdown
var byClient={};
rows.forEach(function(r){
var k=r.client;
if(!byClient[k])byClient[k]={margin:0,hrs:0,rows:0};
byClient[k].margin+=r.margin;
byClient[k].hrs+=r.hrs;
byClient[k].rows++;
});
var clientList=Object.keys(byClient).sort(function(a,b){return byClient[b].margin-byClient[a].margin;});

html+='<div style="background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:13px 15px;margin-bottom:14px">'
+'<div class="sh" style="margin-bottom:10px">Margin by trust</div>'
+'<div style="display:flex;flex-direction:column;gap:4px">';

var maxM=Math.max.apply(null,clientList.map(function(k){return Math.abs(byClient[k].margin);}));
clientList.forEach(function(k){
var m=byClient[k].margin;
var pct=maxM>0?Math.abs(m)/maxM*100:0;
var isNeg=m<0;
var shortName=k.replace(/^SB\s*-\s*\w+\s*-\s*/i,'').replace('NHS Foundation Trust','NHS FT').replace('NHS Trust','').trim();
html+='<div style="display:flex;align-items:center;gap:8px;font-size:12px">'
+'<div style="width:160px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;color:var(--tx);flex-shrink:0" title="'+esc(k)+'">'+esc(shortName)+'</div>'
+'<div style="flex:1;height:8px;background:var(--su2);border-radius:4px;overflow:hidden">'
+'<div style="height:100%;width:'+pct.toFixed(1)+'%;background:'+(isNeg?'var(--amtx)':'var(--grtx)')+';border-radius:4px;transition:width .3s"></div>'
+'</div>'
+'<div style="width:70px;text-align:right;font-weight:500;color:'+(isNeg?'var(--amtx)':'var(--grtx)')+'">'+'\u00a3'+(m<0?'-':'')+Math.abs(m).toFixed(0)+'</div>'
+'</div>';
});
html+='</div></div>';

// Filters bar
html+='<div style="display:flex;gap:8px;margin-bottom:10px;align-items:center;flex-wrap:wrap">'
+'<input id="dc-search" type="text" placeholder="Search candidate or client\u2026" value="'+esc(_dcFilter.q)+'" oninput="_dcFilter.q=this.value;rDivCon()" style="flex:1;padding:5px 9px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;min-width:180px">'
+'<button onclick="_dcFilter.showNeg=!_dcFilter.showNeg;rDivCon()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:'+(_dcFilter.showNeg?'var(--ambg)':'transparent')+';cursor:pointer;font-size:12px;color:'+(_dcFilter.showNeg?'var(--amtx)':'var(--t2)')+'">'
+(_dcFilter.showNeg?'Show all':'Show negatives only')
+'</button>'
+'<span style="font-size:12px;color:var(--t3)">'+filtered.length+' of '+rows.length+' shifts</span>'
+'</div>';

// Table
html+='<div style="overflow-x:auto"><table style="border-collapse:collapse;width:100%;font-size:12px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="padding:5px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Candidate</th>'
+'<th style="padding:5px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em;white-space:nowrap">Shift date</th>'
+'<th style="padding:5px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Client</th>'
+'<th style="padding:5px 8px;text-align:right;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Hrs</th>'
+'<th style="padding:5px 8px;text-align:right;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Pay</th>'
+'<th style="padding:5px 8px;text-align:right;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Charge</th>'
+'<th style="padding:5px 8px;text-align:right;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Margin</th>'
+'<th style="padding:5px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em">Consultant</th>'
+'<th style="padding:5px 4px;text-align:center;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase;letter-spacing:.05em" title="Appeared in previous report">&#8635;</th>'
+'</tr></thead><tbody>';

filtered.forEach(function(r){
var isNeg=r.margin<0;
var isReturn=!!prevKeys[r.cand+'|'+r.date+'|'+r.client];
html+='<tr style="border-bottom:0.5px solid var(--b1);background:'+(isNeg?'var(--ambg)':'transparent')+'">'
+'<td style="padding:5px 8px;font-weight:500;color:var(--tx)">'+esc(r.cand)+'</td>'
+'<td style="padding:5px 8px;color:var(--t2);white-space:nowrap">'+esc(r.date)+'</td>'
+'<td style="padding:5px 8px;color:var(--t2);max-width:220px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap" title="'+esc(r.client)+'">'+esc(r.client.replace(/^SB\s*-\s*\w+\s*-\s*/i,''))+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--t2)">'+r.hrs+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--t2)">\u00a3'+r.pay.toFixed(2)+'</td>'
+'<td style="padding:5px 8px;text-align:right;color:var(--bl)">\u00a3'+r.charge.toFixed(2)+'</td>'
+'<td style="padding:5px 8px;text-align:right;font-weight:500;color:'+(isNeg?'var(--amtx)':'var(--grtx)')+'">'+'\u00a3'+(r.margin<0?'':'')+(r.margin).toFixed(2)+'</td>'
+'<td style="padding:5px 8px;color:var(--t3);font-size:11px">'+esc(r.cons||'')+'</td>'
+'<td style="padding:5px 4px;text-align:center">'+(isReturn?'<span style="color:var(--bl);font-size:12px" title="Appeared in previous report">\u21ba</span>':'')+'</td>'
+'</tr>';
});

html+='</tbody></table></div>';
el.innerHTML=html;
}

function dcImport(input){
if(!input.files||!input.files[0])return;
var file=input.files[0];
var reader=new FileReader();
reader.onload=function(e){
var data=new Uint8Array(e.target.result);
var bstr='';for(var i=0;i<data.length;i++)bstr+=String.fromCharCode(data[i]);
loadXLSX(function(){dcParseXLSX(bstr,file.name);});
};
reader.readAsArrayBuffer(file);
input.value='';
}

function dcParseXLSX(bstr,filename){
try{
var wb=XLSX.read(bstr,{type:'binary',cellDates:true,raw:false});
var ws=wb.Sheets['Data']||wb.Sheets[wb.SheetNames[0]];
var rawRows=XLSX.utils.sheet_to_json(ws,{header:1,defval:'',raw:false});
if(!rawRows||rawRows.length<2){alert('No data found in spreadsheet');return;}

var hdrs=rawRows[0].map(function(v){return(v||'').toString().toLowerCase().trim();});
function col(name){return hdrs.indexOf(name);}

var teamCol=col('team'), consCol=col('consultant name');
var candCol=col('candidate'), clientCol=col('client');
var dateCol=col('shift date'), hrsCol=col('paid hrs');
var payCol=col('pay'), chargeCol=col('charge');
var marginCol=col('actual margin');
var cons1Col=col('cons 1 name');

var rows=[];
rawRows.slice(1).forEach(function(row){
var team=(row[teamCol]||'').toString().trim();
var cons=(row[consCol]||'').toString().trim();
if(team!=='Theatres'||cons!=='South Theatres')return;

var dateVal=row[dateCol]||'';
var dateStr='';
if(dateVal){
var d=new Date(dateVal);
if(!isNaN(d.getTime()))dateStr=String(d.getDate()).padStart(2,'0')+'/'+String(d.getMonth()+1).padStart(2,'0')+'/'+d.getFullYear();
else dateStr=dateVal.toString().slice(0,10);
}

var sf=function(v){var n=parseFloat((v||'').toString().replace(/[^0-9.\-]/g,''));return isNaN(n)?0:Math.round(n*100)/100;};

rows.push({
cand:(row[candCol]||'').toString().trim(),
client:(row[clientCol]||'').toString().trim(),
date:dateStr,
hrs:sf(row[hrsCol]),
pay:sf(row[payCol]),
charge:sf(row[chargeCol]),
margin:sf(row[marginCol]),
cons:(row[cons1Col]||'').toString().trim()
});
});

if(!rows.length){alert('No South Theatres rows found in this file.');return;}

// Week label from filename e.g. WK51_DIVCON_2025-2026.xlsx -> WK51 2025-26
var wkMatch=filename.match(/WK(\d+)/i);
var yearMatch=filename.match(/(\d{4})-(\d{4})/);
var weekLabel=wkMatch?'WK'+wkMatch[1]:'Week';
if(yearMatch)weekLabel+='\u00a0'+yearMatch[1].slice(2)+'-'+yearMatch[2].slice(2);
else weekLabel+='\u00a0'+new Date().getFullYear();

// Check for duplicate week label
var existing=_dcReports.findIndex(function(r){return r.weekLabel===weekLabel;});
if(existing>=0){
if(!confirm('A report for '+weekLabel+' already exists. Replace it?'))return;
_dcReports.splice(existing,1,{weekLabel:weekLabel,imported:todayStr(),rows:rows});
_dcActiveIdx=existing;
} else {
_dcReports.unshift({weekLabel:weekLabel,imported:todayStr(),rows:rows});
_dcActiveIdx=0;
}
_dcFilter={q:'',client:'',showNeg:false};
saveDC();
rDivCon();
}catch(err){alert('Parse error: '+err.message);console.error(err);}
}

function dcViewReport(i){
_dcActiveIdx=i;
_dcFilter={q:'',client:'',showNeg:false};
rDivCon();
}

function dcDeleteReport(i){
if(!confirm('Remove this report?'))return;
_dcReports.splice(i,1);
if(_dcActiveIdx>=_dcReports.length)_dcActiveIdx=_dcReports.length-1;
saveDC();
rDivCon();
}


// \u2500\u2500 DIV CON TRUST MAPPING \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500
// _dcMap: {clientName -> trustName in HC}
var _dcMap={};
var _dashDcActiveTab=0;
function loadDCMap(){try{var d=localStorage.getItem('dw_dcmap');if(d)_dcMap=JSON.parse(d);}catch(e){}}
function saveDCMap(){try{localStorage.setItem('dw_dcmap',JSON.stringify(_dcMap));}catch(e){}}

function dcShowMapping(){
if(!_dcLoaded){loadDC();_dcLoaded=true;}
loadDCMap();
// Collect all unique client names across all reports
var allClients={};
_dcReports.forEach(function(r){
r.rows.forEach(function(row){if(row.client)allClients[row.client]=true;});
});
var clients=Object.keys(allClients).sort();
if(!clients.length){alert('No reports imported yet.');return;}

var hospOpts='<option value="">-- no match --</option>'
+getAllTrustNames().map(function(n){return'<option value="'+esc(n)+'">'+esc(n)+'</option>';}).join('');

var html='<div style="position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(0,0,0,.4);z-index:9999;display:flex;align-items:center;justify-content:center">'
+'<div style="background:var(--su);border-radius:var(--rl);padding:20px 24px;width:640px;max-height:80vh;overflow-y:auto;box-shadow:0 8px 32px rgba(0,0,0,.2)">'
+'<div style="display:flex;align-items:center;margin-bottom:14px">'
+'<div class="sh" style="margin:0;flex:1">Map Div Con clients to trusts</div>'
+'<button onclick="document.getElementById(\'dc-map-modal\').remove()" style="background:none;border:none;cursor:pointer;font-size:20px;color:var(--t3)">&times;</button>'
+'</div>'
+'<div style="font-size:12px;color:var(--t3);margin-bottom:12px">Match each billing client name to a trust in your register. Saved permanently.</div>'
+'<table style="width:100%;border-collapse:collapse;font-size:12px">'
+'<thead><tr style="border-bottom:0.5px solid var(--b2)">'
+'<th style="padding:5px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase">Client name (Div Con)</th>'
+'<th style="padding:5px 8px;text-align:left;font-size:10px;font-weight:600;color:var(--t2);text-transform:uppercase">Maps to trust</th>'
+'</tr></thead><tbody>';

clients.forEach(function(c){
var shortName=c.replace(/^SB\s*-\s*\w+\s*-\s*/i,'').trim();
var cur=_dcMap[c]||'';
// Auto-suggest: find closest trust name
if(!cur){
var best='',bestScore=0;
getAllTrustNames().forEach(function(tn){
var hn=tn.toLowerCase();
var cn=c.toLowerCase();
if(cn.includes(hn)||hn.includes(cn.replace(/^sb\s*-\s*\w+\s*-\s*/i,'').trim())){
var score=tn.length;
if(score>bestScore){best=tn;bestScore=score;}
}
});
if(best)cur=best;
}
var opts=hospOpts.replace('value="'+esc(cur)+'"','value="'+esc(cur)+'" selected');
html+='<tr style="border-bottom:0.5px solid var(--b1)">'
+'<td style="padding:6px 8px;color:var(--tx)" title="'+esc(c)+'">'+esc(shortName)+'</td>'
+'<td style="padding:4px 8px">'
+'<select class="dc-map-sel" data-client="'+esc(c)+'" style="width:100%;padding:4px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'
+opts
+'</select>'
+'</td>'
+'</tr>';
});

html+='</tbody></table>'
+'<div style="display:flex;gap:8px;margin-top:14px;justify-content:flex-end">'
+'<button onclick="document.getElementById(\'dc-map-modal\').remove()" style="padding:6px 14px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>'
+'<button onclick="dcSaveMapping()" class="ef-save" style="padding:6px 14px">Save mapping</button>'
+'</div>'
+'</div>'
+'</div>';

var modal=document.createElement('div');
modal.id='dc-map-modal';
modal.innerHTML=html;
document.body.appendChild(modal);
}

function dcSaveMapping(){
document.querySelectorAll('.dc-map-sel').forEach(function(sel){
var client=sel.getAttribute('data-client');
if(sel.value)_dcMap[client]=sel.value;
else delete _dcMap[client];
});
saveDCMap();
document.getElementById('dc-map-modal').remove();
alert('Trust mapping saved.');
}


// \u2500\u2500 MAP \u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500\u2500

// postcode -> {lat,lng}



// {type,name,lat,lng}




// PIPELINE
var _pipe=[];
var _pipeLoaded=false;
var _PIPE_STAGES=[
{id:'contacted',label:'First Contacted',color:'var(--bl)',bg:'var(--blbg)'},
{id:'portal',label:'Added to Portal',color:'#7c3fc5',bg:'#f0ebff'},
{id:'compliance',label:'Sent to Compliance',color:'var(--amtx)',bg:'var(--ambg)'},
{id:'signedoff',label:'Signed Off',color:'var(--grtx)',bg:'var(--grbg)'}
];
var _CONSULTANTS=['Rachel','Josh','Jason'];
function loadPipe(){try{var d=localStorage.getItem('dw_pipeline');if(d)_pipe=JSON.parse(d);}catch(e){}}
function savePipe(){try{localStorage.setItem('dw_pipeline',JSON.stringify(_pipe));}catch(e){}}
function rPipeline(){
if(!_pipeLoaded){loadPipe();_pipeLoaded=true;}
var el=document.getElementById('pipeline-main');if(!el)return;
var today=todayStr();
var overdue=_pipe.filter(function(p){return p.stage!=='signedoff'&&p.followUp&&p.followUp<today;}).length;
var html='<div style="display:flex;align-items:center;gap:10px;margin-bottom:14px;flex-wrap:wrap">'
+'<div class="sh" style="margin:0;flex:1">Candidate Pipeline</div>'
+(overdue?'<span style="padding:4px 10px;background:var(--ambg);color:var(--amtx);border-radius:20px;font-size:11px;font-weight:600">'+overdue+' overdue</span>':'')
+'<button onclick="pipeShowAdd()" class="ef-save" style="padding:5px 14px">+ Add candidate</button>'
+'</div>'
+'<div id="pipe-add-form" style="display:none;background:var(--su);border:0.5px solid var(--b1);border-radius:var(--rl);padding:14px 16px;margin-bottom:14px">'
+'<div class="sh" style="margin-bottom:10px">New pipeline candidate</div>'
+'<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:8px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Name *</div><input id="pipe-name" type="text" placeholder="Candidate name" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Role</div><input id="pipe-role" type="text" placeholder="ODP, Scrub..." style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Consultant</div><select id="pipe-cons" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none"><option value="">-- select --</option>'+_CONSULTANTS.map(function(c){return'<option>'+c+'</option>';}).join('')+'</select></div>'
+'</div>'
+'<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:10px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Phone</div><input id="pipe-phone" type="tel" placeholder="07..." style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Email</div><input id="pipe-email" type="email" placeholder="email@..." style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:3px;text-transform:uppercase">Compliance %</div><input id="pipe-comp" type="number" min="0" max="100" placeholder="0" style="width:100%;padding:6px 8px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'</div>'
+'<div style="display:flex;gap:6px">'
+'<button onclick="pipeAdd()" class="ef-save" style="padding:5px 14px">Add to pipeline</button>'
+'<button onclick="pipeShowAdd()" style="padding:5px 10px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:12px;color:var(--t2)">Cancel</button>'
+'</div>'
+'</div>'
+'<div style="display:grid;grid-template-columns:repeat(4,1fr);gap:10px;align-items:start">';
_PIPE_STAGES.forEach(function(stage){
var cards=_pipe.filter(function(p){return p.stage===stage.id;});
html+='<div style="background:var(--su2);border-radius:var(--rl);padding:10px">'
+'<div style="display:flex;align-items:center;gap:6px;margin-bottom:10px">'
+'<div style="width:8px;height:8px;border-radius:50%;background:'+stage.color+';flex-shrink:0"></div>'
+'<div style="font-size:11px;font-weight:600;color:'+stage.color+';text-transform:uppercase;letter-spacing:.05em">'+stage.label+'</div>'
+'<div style="margin-left:auto;font-size:11px;color:var(--t3)">'+cards.length+'</div>'
+'</div>';
if(!cards.length){
html+='<div style="font-size:11px;color:var(--t3);text-align:center;padding:16px 0">Empty</div>';
} else {
cards.forEach(function(p){
var daysInStage=Math.floor((new Date(today)-new Date(p.stageDate||p.addedDate))/(86400000));
var ageColor=daysInStage>=7?'var(--amtx)':daysInStage>=3?'#c08000':'var(--t3)';
var isOverdue=p.followUp&&p.followUp<today;
var nextStage=_PIPE_STAGES[_PIPE_STAGES.findIndex(function(s){return s.id===stage.id;})+1];
html+='<div style="background:var(--su);border:0.5px solid '+(isOverdue?'var(--amtx)':'var(--b1)')+';border-radius:var(--r);padding:10px;margin-bottom:8px">'
+'<div style="display:flex;align-items:flex-start;justify-content:space-between;gap:4px;margin-bottom:4px">'
+'<div>'
+'<div style="font-size:13px;font-weight:500;color:var(--tx)">'+esc(p.name)+'</div>'
+(p.role?'<div style="font-size:10px;color:var(--t2)">'+esc(p.role)+'</div>':'')
+(p.phone||p.email?'<div style="font-size:10px;color:var(--t3)">'+(p.phone?'\u260e '+esc(p.phone):'')+(p.phone&&p.email?' \u00b7 ':'')+( p.email?esc(p.email):'')+'</div>':'')
+'</div>'
+'<button class="pipe-del-btn" data-pid="'+p.id+'" style="background:none;border:none;cursor:pointer;color:var(--t3);font-size:14px;padding:0">&times;</button>'
+'</div>'
+'<div style="margin-bottom:6px">'
+'<div style="display:flex;justify-content:space-between;font-size:10px;color:var(--t3);margin-bottom:2px"><span>Compliance</span><span style="font-weight:500;color:var(--tx)">'+(p.compliance||0)+'%</span></div>'
+'<div style="height:4px;background:var(--su2);border-radius:2px;overflow:hidden"><div style="height:100%;width:'+(p.compliance||0)+'%;background:'+(p.compliance>=100?'var(--grtx)':p.compliance>=50?'var(--bl)':'var(--amtx)')+';border-radius:2px"></div></div>'
+'</div>'
+'<div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:6px;align-items:center">'
+(p.consultant?'<span style="font-size:10px;background:var(--su2);padding:1px 6px;border-radius:10px;color:var(--t2)">'+esc(p.consultant)+'</span>':'')
+'<span style="font-size:10px;color:'+ageColor+'">'+daysInStage+'d in stage</span>'
+(isOverdue?'<span style="font-size:10px;color:var(--amtx);font-weight:600">\u26a0 Overdue</span>':'')
+(p.followUp&&p.followUp>=today?'<span style="font-size:10px;color:var(--t3)">\ud83d\udcc5 '+fmtDateDMY(p.followUp)+'</span>':'')
+'</div>'
+(p.notes&&p.notes.length?'<div style="margin-bottom:6px">'+p.notes.map(function(n){return'<div style="font-size:10px;padding:3px 6px;background:var(--su2);border-radius:var(--r);margin-bottom:2px;border-left:2px solid var(--b2)"><span style="color:var(--t3)">'+esc(n.date)+(n.consultant?' \u00b7 '+esc(n.consultant):'')+'</span> <span style="color:var(--tx)">'+esc(n.text)+'</span></div>';}).join('')+'</div>':'')
+'<div style="display:flex;gap:4px;flex-wrap:wrap">'
+'<button class="pipe-log-btn" data-pid="'+p.id+'" style="flex:1;padding:4px 6px;background:var(--blbg);color:var(--bl);border:0.5px solid var(--bl);border-radius:var(--r);cursor:pointer;font-size:10px;font-weight:600">\u270e Log note</button>'
+'<button class="pipe-edit-btn" data-pid="'+p.id+'" style="padding:4px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:transparent;cursor:pointer;font-size:10px;color:var(--t2)">Edit</button>'
+'</div>'
+'<div id="pipe-qnote-'+p.id+'" style="display:none;margin-top:6px">'
+'<div style="display:flex;gap:4px"><input id="pipe-note-'+p.id+'" type="text" placeholder="Log a note...\u2026" style="flex:1;padding:4px 7px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:11px;outline:none"><button class="pipe-log-submit" data-pid="'+p.id+'" style="padding:4px 10px;background:var(--bl);color:#fff;border:none;border-radius:var(--r);cursor:pointer;font-size:11px">Log</button></div>'
+'</div>'
+'<div id="pipe-exp-'+p.id+'" style="display:none;margin-top:8px;padding-top:8px;border-top:0.5px solid var(--b1)">'
+'<div style="display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:8px">'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:2px;text-transform:uppercase">Compliance %</div><input type="number" min="0" max="100" value="'+(p.compliance||0)+'" class="pipe-comp-input" data-pid="'+p.id+'" style="width:100%;padding:4px 6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:2px;text-transform:uppercase">Follow-up date</div><input type="date" value="'+(p.followUp||'')+'" class="pipe-date-input" data-pid="'+p.id+'" style="width:100%;padding:4px 6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:2px;text-transform:uppercase">Consultant</div><select class="pipe-cons-sel" data-pid="'+p.id+'" style="width:100%;padding:4px 6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none">'+_CONSULTANTS.map(function(c){return'<option'+(p.consultant===c?' selected':'')+'>'+c+'</option>';}).join('')+'</select></div>'
+'<div><div style="font-size:10px;color:var(--t2);margin-bottom:2px;text-transform:uppercase">Role</div><input type="text" value="'+esc(p.role||'')+'" class="pipe-role-input" data-pid="'+p.id+'" style="width:100%;padding:4px 6px;border:0.5px solid var(--b2);border-radius:var(--r);background:var(--su);color:var(--tx);font-size:12px;outline:none;box-sizing:border-box"></div>'
+'</div>'
+(nextStage?'<button class="pipe-adv-btn" data-pid="'+p.id+'" style="width:100%;padding:5px;background:'+stage.bg+';color:'+stage.color+';border:0.5px solid '+stage.color+';border-radius:var(--r);cursor:pointer;font-size:11px;font-weight:600;margin-bottom:4px">\u2192 Move to '+nextStage.label+'</button>':'')
+(stage.id==='signedoff'?(p.candIdx>=0?'<button class="pipe-reg-btn" data-pid="'+p.id+'" style="width:100%;padding:5px;background:var(--su2);color:var(--grtx);border:0.5px solid var(--grtx);border-radius:var(--r);cursor:pointer;font-size:11px">\u2713 Added \u2192 View profile</button>':'<button class="pipe-reg-btn" data-pid="'+p.id+'" style="width:100%;padding:5px;background:var(--grbg);color:var(--grtx);border:0.5px solid var(--grtx);border-radius:var(--r);cursor:pointer;font-size:11px;font-weight:600">\u2713 Add to register</button>'):'')
+'</div>'
+'</div>';
});
}
html+='</div>';
});
html+='</div>';
el.innerHTML=html;
el.querySelectorAll('.pipe-log-btn').forEach(function(b){b.addEventListener('click',function(){pipeExpandNote(this.dataset.pid);});});
el.querySelectorAll('.pipe-edit-btn').forEach(function(b){b.addEventListener('click',function(){pipeExpand(this.dataset.pid);});});
el.querySelectorAll('.pipe-log-submit').forEach(function(b){b.addEventListener('click',function(){pipeAddNote(this.dataset.pid);});});
el.querySelectorAll('.pipe-del-btn').forEach(function(b){b.addEventListener('click',function(){pipeDelete(this.dataset.pid);});});
el.querySelectorAll('.pipe-adv-btn').forEach(function(b){b.addEventListener('click',function(){pipeAdvance(this.dataset.pid);});});
el.querySelectorAll('.pipe-reg-btn').forEach(function(b){b.addEventListener('click',function(){pipeToRegister(this.dataset.pid);});});
el.querySelectorAll('.pipe-comp-input').forEach(function(i){i.addEventListener('change',function(){pipeUpdate(this.dataset.pid,'compliance',+this.value);rPipeline();});});
el.querySelectorAll('.pipe-date-input').forEach(function(i){i.addEventListener('change',function(){pipeUpdate(this.dataset.pid,'followUp',this.value);rPipeline();});});
el.querySelectorAll('.pipe-cons-sel').forEach(function(s){s.addEventListener('change',function(){pipeUpdate(this.dataset.pid,'consultant',this.value);});});
el.querySelectorAll('.pipe-role-input').forEach(function(i){i.addEventListener('change',function(){pipeUpdate(this.dataset.pid,'role',this.value);});});
}
function pipeShowAdd(){var f=document.getElementById('pipe-add-form');if(f)f.style.display=f.style.display==='none'?'block':'none';}
function pipeAdd(){
var name=(document.getElementById('pipe-name')||{}).value||'';
if(!name.trim()){alert('Name required');return;}
var phone=(document.getElementById('pipe-phone')||{}).value||'';
var email=(document.getElementById('pipe-email')||{}).value||'';
var comp=+(document.getElementById('pipe-comp')||{value:0}).value||0;
_pipe.unshift({id:'pip'+Date.now(),name:name.trim(),role:((document.getElementById('pipe-role')||{}).value||'').trim(),
consultant:(document.getElementById('pipe-cons')||{}).value||'',phone:phone.trim(),email:email.trim(),
stage:'contacted',compliance:comp,addedDate:todayStr(),stageDate:todayStr(),followUp:'',notes:[],candIdx:-1});
savePipe();pipeShowAdd();rPipeline();
}
function pipeAdvance(id){var p=_pipe.find(function(x){return x.id===id;});if(!p)return;var stages=_PIPE_STAGES.map(function(s){return s.id;});var idx=stages.indexOf(p.stage);if(idx<stages.length-1){p.stage=stages[idx+1];p.stageDate=todayStr();}savePipe();rPipeline();}
function pipeUpdate(id,field,val){var p=_pipe.find(function(x){return x.id===id;});if(!p)return;p[field]=val;savePipe();}
function pipeExpandNote(id){var el=document.getElementById('pipe-qnote-'+id);if(!el)return;el.style.display=el.style.display==='none'?'block':'none';if(el.style.display==='block'){var inp=document.getElementById('pipe-note-'+id);if(inp)inp.focus();}}
function pipeExpand(id){var el=document.getElementById('pipe-exp-'+id);if(el)el.style.display=el.style.display==='none'?'block':'none';}
function pipeAddNote(id){var p=_pipe.find(function(x){return x.id===id;});var el=document.getElementById('pipe-note-'+id);if(!p||!el||!el.value.trim())return;if(!p.notes)p.notes=[];p.notes.push({date:todayStr(),consultant:p.consultant||'',text:el.value.trim()});savePipe();rPipeline();}
function pipeDelete(id){if(!confirm('Remove from pipeline?'))return;_pipe=_pipe.filter(function(x){return x.id!==id;});savePipe();rPipeline();}
function pipeToRegister(id){
var p=_pipe.find(function(x){return x.id===id;});if(!p)return;
if(p.candIdx>=0&&C[p.candIdx]){
gp('candidates');
setTimeout(function(){openCandPanel(p.candIdx,C[p.candIdx]);},150);
return;
}
var ex=C.findIndex(function(c){return c.n.toLowerCase()===p.name.toLowerCase();});
if(ex>=0){
if(!confirm(p.name+' already exists. Open their profile?'))return;
p.candIdx=ex;savePipe();
gp('candidates');
setTimeout(function(){openCandPanel(ex,C[ex]);},150);
return;
}
// Store pipeline id so saveCandEdit can link back
window._pipeRegisteringId=id;
// Build partial candidate from pipeline data
var nc={n:p.name,s:p.role||'',ac:'Active',e:p.email||'',p:p.phone||'',av:'',h:'',a:'',r:0,st:'available',b:''};
// Navigate then open panel pre-filled
gp('candidates');
setTimeout(function(){openCandPanel(-1,nc);},150);
}
function getPipelineOverdue(){if(!_pipeLoaded){loadPipe();_pipeLoaded=true;}var today=todayStr();return _pipe.filter(function(p){return p.stage!=='signedoff'&&p.followUp&&p.followUp<=today;});}
function renderPipelineOverdue(){
var overdue=getPipelineOverdue();var el=document.getElementById('todo-right-col');if(!el)return;
var ex=document.getElementById('pipe-overdue-panel');if(ex)ex.remove();if(!overdue.length)return;
var panel=document.createElement('div');panel.id='pipe-overdue-panel';panel.style.cssText='margin-top:16px';
var html='<div style="font-size:11px;font-weight:600;color:var(--amtx);text-transform:uppercase;letter-spacing:.06em;margin-bottom:8px">\u26a0 Pipeline follow-ups overdue ('+overdue.length+')</div>';
overdue.forEach(function(p){html+='<div style="display:flex;align-items:center;gap:8px;padding:8px 10px;background:var(--su);border:0.5px solid var(--amtx);border-radius:var(--r);margin-bottom:6px"><div style="flex:1;min-width:0"><div style="font-size:12px;font-weight:500;color:var(--tx)">'+esc(p.name)+'</div><div style="font-size:10px;color:var(--amtx)">Due: '+fmtDateDMY(p.followUp)+(p.consultant?' \u2022 '+esc(p.consultant):'')+'</div></div><button onclick="gp(\'pipeline\')" style="padding:3px 8px;border:0.5px solid var(--bl);border-radius:var(--r);background:var(--blbg);color:var(--bl);cursor:pointer;font-size:10px">View</button></div>';});
panel.innerHTML=html;el.appendChild(panel);
}


// ── SPEC MULTI-SELECT ─────────────────────────────────────────────────────────
function ceToggleSpecDrop(){
var drop=document.getElementById('ce-spec-drop');
if(!drop)return;
var isOpen=drop.style.display==='block';
drop.style.display=isOpen?'none':'block';
if(!isOpen){
// Close on outside click
setTimeout(function(){
document.addEventListener('click',function handler(e){
var widget=document.getElementById('ce-spec-widget');
if(widget&&!widget.contains(e.target)){
drop.style.display='none';
document.removeEventListener('click',handler);
}
});
},10);
}
}

function ceSpecChanged(){
var drop=document.getElementById('ce-spec-drop');
if(!drop)return;
var checked=Array.from(drop.querySelectorAll('input[type=checkbox]:checked')).map(function(c){return c.value;});
// Update label
var label=document.getElementById('ce-spec-label');
if(label){
if(checked.length===0){label.textContent='Select spec(s)...';label.style.color='var(--t3)';}
else{label.textContent=checked.join(', ');label.style.color='var(--tx)';}
}
// Show/hide Other text field
var otherInput=document.getElementById('ce-s-other');
if(otherInput)otherInput.style.display=checked.indexOf('Other')>=0?'block':'none';
// Show/hide sub-spec
var subWrap=document.getElementById('ce-subspec-wrap');
if(subWrap)subWrap.style.display=checked.indexOf('Scrub')>=0?'block':'none';
}

function ceGetSpecs(){
var drop=document.getElementById('ce-spec-drop');
if(!drop)return'';
var checked=Array.from(drop.querySelectorAll('input[type=checkbox]:checked')).map(function(c){return c.value;});
// Replace Other with the free text value
var otherInput=document.getElementById('ce-s-other');
if(otherInput&&otherInput.value.trim()){
var idx=checked.indexOf('Other');
if(idx>=0)checked[idx]=otherInput.value.trim();
}
return checked.join(', ');
}

function ceGetSubSpecs(){
var wrap=document.getElementById('ce-subspec-wrap');
if(!wrap||wrap.style.display==='none')return'';
var checked=Array.from(wrap.querySelectorAll('input[name=ce-subspec]:checked')).map(function(c){return c.value;});
return checked.join(', ');
}

function ceSetSpecs(specStr, subSpecStr){
var drop=document.getElementById('ce-spec-drop');
if(!drop)return;
var specs=(specStr||'').split(',').map(function(s){return s.trim();}).filter(Boolean);
// Reset all checkboxes
drop.querySelectorAll('input[type=checkbox]').forEach(function(cb){cb.checked=false;});
var otherInput=document.getElementById('ce-s-other');
if(otherInput){otherInput.value='';otherInput.style.display='none';}
var subWrap=document.getElementById('ce-subspec-wrap');
if(subWrap){
subWrap.style.display='none';
subWrap.querySelectorAll('input[name=ce-subspec]').forEach(function(cb){cb.checked=false;});
}

var knownSpecs=['ODP','Scrub','Recovery','Chemo','Anaesthetics','SFA','TSW'];
specs.forEach(function(s){
var cb=drop.querySelector('input[value="'+s+'"]');
if(cb){cb.checked=true;}
else if(knownSpecs.indexOf(s)<0&&otherInput){
// Unknown spec = Other
var otherCb=drop.querySelector('input[value="Other"]');
if(otherCb)otherCb.checked=true;
otherInput.value=s;
otherInput.style.display='block';
}
});
// Sub-specs
if(subSpecStr&&specs.indexOf('Scrub')>=0){
var subSpecs=subSpecStr.split(',').map(function(s){return s.trim();});
if(subWrap){
subWrap.style.display='block';
subSpecs.forEach(function(ss){
var cb=subWrap.querySelector('input[value="'+ss+'"]');
if(cb)cb.checked=true;
});
}
}
// Update label
ceSpecChanged();
}


chWk(0);
// Restore any user-added sites to TRUST_SITES
try{
var _allHE=JSON.parse(localStorage.getItem('hosp_edits')||'{}');
Object.keys(_allHE).forEach(function(hn){
if(_allHE[hn].sites&&_allHE[hn].sites.length){
if(!TRUST_SITES[hn])TRUST_SITES[hn]=[];
_allHE[hn].sites.forEach(function(s){
if(TRUST_SITES[hn].indexOf(s)<0)TRUST_SITES[hn].push(s);
});
}
});
// Rebuild A[] with all sites including user-added
rebuildDropdown();
}catch(e){}
try{var _sr=localStorage.getItem('crm_rotas2');if(_sr){var _rd2=JSON.parse(_sr);Object.keys(_rd2).forEach(function(k){if(ROTA_DATA.weeks[k])ROTA_DATA.weeks[k]=_rd2[k];});}}catch(e){}</script>
</body>
</html>

