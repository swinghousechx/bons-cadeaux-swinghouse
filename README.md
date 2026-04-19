<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="apple-mobile-web-app-title" content="Bons Cadeaux">
  <meta name="theme-color" content="#005235">
  <title>Bons Cadeaux — Swing House</title>
  <!-- Icône app écran d'accueil -->
  <link rel="apple-touch-icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 180 180'%3E%3Crect width='180' height='180' rx='40' fill='%23005235'/%3E%3Crect x='0' y='153' width='180' height='8' rx='0' fill='%23e8562a'/%3E%3Ctext x='90' y='80' font-family='Arial' font-weight='900' font-size='52' fill='%23f0ece5' text-anchor='middle'%3ESH%3C/text%3E%3Ctext x='90' y='130' font-family='Arial' font-weight='500' font-size='22' fill='%23aeae8b' text-anchor='middle'%3EBONS%3C/text%3E%3C/svg%3E">
  <link rel="manifest" href="data:application/json,%7B%22name%22%3A%22Bons%20Cadeaux%20%E2%80%94%20Swing%20House%22%2C%22short_name%22%3A%22Bons%20Cadeaux%22%2C%22display%22%3A%22standalone%22%2C%22background_color%22%3A%22%23005235%22%2C%22theme_color%22%3A%22%23005235%22%2C%22start_url%22%3A%22.%22%7D">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;900&family=Montserrat+Alternates:wght@500;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --sh-dark-green:  #005235;
      --sh-beige:       #f0ece5;
      --sh-light-green: #6a714a;
      --sh-pale-green:  #aeae8b;
      --sh-orange:      #e8562a;
      --safe-top: env(safe-area-inset-top, 0px);
      --safe-bottom: env(safe-area-inset-bottom, 0px);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

    html, body {
      height: 100%;
      font-family: 'Montserrat', Arial, sans-serif;
      background-color: var(--sh-beige);
      color: var(--sh-dark-green);
      overflow-x: hidden;
    }

    /* ── HEADER ── */
    header {
      background-color: var(--sh-dark-green);
      color: var(--sh-beige);
      padding: calc(16px + var(--safe-top)) 20px 16px;
      border-bottom: 3px solid var(--sh-orange);
      position: sticky;
      top: 0;
      z-index: 50;
    }
    .header-top {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 12px;
    }
    .logo-text {
      font-weight: 900;
      font-size: 20px;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--sh-beige);
    }
    .logo-text span { color: var(--sh-orange); }
    .header-actions { display: flex; gap: 10px; }

    /* ── STATS STRIP ── */
    .stats-strip {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0;
      border-top: 1px solid rgba(240,236,229,0.12);
    }
    .stat-item {
      padding: 10px 12px;
      text-align: center;
      border-right: 1px solid rgba(240,236,229,0.12);
    }
    .stat-item:last-child { border-right: none; }
    .stat-item .sv { font-size: 18px; font-weight: 900; color: var(--sh-beige); line-height: 1; }
    .stat-item .sl { font-size: 9px; font-family: 'Montserrat Alternates', sans-serif; font-weight: 500; text-transform: uppercase; letter-spacing: 0.08em; color: var(--sh-pale-green); margin-top: 3px; }
    .stat-item.accent .sv { color: var(--sh-orange); }

    /* ── FILTER BAR ── */
    .filter-bar {
      background: white;
      border-bottom: 1px solid #e8e4dd;
      padding: 12px 16px;
      display: flex;
      gap: 8px;
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
      scrollbar-width: none;
    }
    .filter-bar::-webkit-scrollbar { display: none; }

    .filter-chip {
      flex-shrink: 0;
      background: transparent;
      border: 1.5px solid #d5d0c8;
      color: var(--sh-light-green);
      font-family: 'Montserrat Alternates', sans-serif;
      font-size: 12px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.07em;
      padding: 7px 14px;
      border-radius: 20px;
      cursor: pointer;
      transition: all 0.15s;
      white-space: nowrap;
    }
    .filter-chip.active {
      background: var(--sh-dark-green);
      border-color: var(--sh-dark-green);
      color: var(--sh-beige);
    }

    /* ── SEARCH ── */
    .search-wrap {
      padding: 12px 16px;
      background: white;
      border-bottom: 1px solid #e8e4dd;
    }
    .search-input {
      width: 100%;
      padding: 11px 16px;
      border: 1.5px solid #d5d0c8;
      border-radius: 10px;
      font-family: 'Montserrat', sans-serif;
      font-size: 15px;
      background: var(--sh-beige);
      color: var(--sh-dark-green);
      outline: none;
    }
    .search-input:focus { border-color: var(--sh-dark-green); }

    /* ── CARD LIST ── */
    .card-list {
      padding: 12px 16px;
      display: flex;
      flex-direction: column;
      gap: 10px;
      padding-bottom: calc(90px + var(--safe-bottom));
    }

    .voucher-card {
      background: white;
      border-radius: 10px;
      box-shadow: 0 1px 6px rgba(0,82,53,0.07);
      overflow: hidden;
      transition: box-shadow 0.15s;
    }
    .voucher-card:active { box-shadow: 0 2px 12px rgba(0,82,53,0.14); }

    .card-main {
      padding: 14px 16px 10px;
      cursor: pointer;
    }
    .card-top {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      margin-bottom: 10px;
    }
    .card-client { font-weight: 700; font-size: 16px; }
    .card-ref {
      font-family: 'Montserrat Alternates', sans-serif;
      font-size: 11px;
      font-weight: 600;
      color: var(--sh-pale-green);
      letter-spacing: 0.08em;
      margin-top: 2px;
    }
    .card-note { font-size: 12px; color: var(--sh-pale-green); margin-top: 2px; }

    .card-amounts {
      display: flex;
      gap: 0;
      align-items: stretch;
    }
    .amount-block {
      flex: 1;
      text-align: center;
    }
    .amount-block + .amount-block { border-left: 1px solid #f0ece5; }
    .ab-label { font-size: 10px; font-family: 'Montserrat Alternates', sans-serif; text-transform: uppercase; letter-spacing: 0.08em; color: var(--sh-pale-green); margin-bottom: 2px; }
    .ab-value { font-size: 17px; font-weight: 800; color: var(--sh-dark-green); }
    .ab-value.used { color: var(--sh-light-green); }
    .ab-value.zero { color: var(--sh-pale-green); text-decoration: line-through; font-size: 14px; }

    /* PROGRESS */
    .card-progress { margin: 10px 16px 0; }
    .progress-track { background: #f0ece5; border-radius: 3px; height: 5px; }
    .progress-fill { background: var(--sh-dark-green); height: 5px; border-radius: 3px; transition: width 0.3s; }
    .progress-fill.warn { background: var(--sh-orange); }

    /* CARD FOOTER */
    .card-footer {
      display: flex;
      border-top: 1px solid #f0ece5;
      margin-top: 10px;
    }
    .card-footer-btn {
      flex: 1;
      padding: 11px 8px;
      border: none;
      background: transparent;
      font-family: 'Montserrat', sans-serif;
      font-size: 13px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      cursor: pointer;
      color: var(--sh-light-green);
      transition: background 0.15s;
    }
    .card-footer-btn:active { background: #f0ece5; }
    .card-footer-btn.use-btn {
      color: var(--sh-dark-green);
      border-right: 1px solid #f0ece5;
    }
    .card-footer-btn.use-btn:disabled { color: var(--sh-pale-green); cursor: default; }
    .card-footer-btn.del-btn { color: #c0392b; }

    /* BADGE */
    .badge { display: inline-block; font-family: 'Montserrat Alternates', sans-serif; font-weight: 600; text-transform: uppercase; letter-spacing: 0.08em; font-size: 10px; padding: 3px 9px; border-radius: 12px; }
    .badge-active { background: rgba(0,82,53,0.1); color: var(--sh-dark-green); }
    .badge-partial { background: rgba(106,113,74,0.15); color: var(--sh-light-green); }
    .badge-used { background: #f0ece5; color: var(--sh-pale-green); }

    /* EMPTY */
    .empty-state { padding: 60px 20px; text-align: center; color: var(--sh-pale-green); }
    .empty-state p { font-size: 13px; font-weight: 500; text-transform: uppercase; letter-spacing: 0.08em; line-height: 1.8; }

    /* FAB */
    .fab {
      position: fixed;
      bottom: calc(24px + var(--safe-bottom));
      right: 24px;
      width: 60px;
      height: 60px;
      background: var(--sh-orange);
      color: var(--sh-beige);
      border: none;
      border-radius: 50%;
      font-size: 28px;
      cursor: pointer;
      box-shadow: 0 4px 16px rgba(232,86,42,0.45);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 40;
      transition: transform 0.15s, box-shadow 0.15s;
    }
    .fab:active { transform: scale(0.93); box-shadow: 0 2px 8px rgba(232,86,42,0.35); }

    /* MODAL */
    .modal-overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.5);
      z-index: 200;
      align-items: flex-end;
      justify-content: center;
    }
    .modal-overlay.open { display: flex; }

    /* Sheet style (bottom sheet sur iPad) */
    .modal {
      background: var(--sh-beige);
      border-radius: 16px 16px 0 0;
      padding: 20px 20px calc(20px + var(--safe-bottom));
      width: 100%;
      max-width: 600px;
      box-shadow: 0 -4px 30px rgba(0,0,0,0.2);
      position: relative;
      max-height: 92vh;
      overflow-y: auto;
      -webkit-overflow-scrolling: touch;
    }
    .sheet-handle {
      width: 40px;
      height: 4px;
      background: var(--sh-pale-green);
      border-radius: 2px;
      margin: 0 auto 20px;
    }
    .modal h3 {
      font-size: 17px;
      font-weight: 900;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      color: var(--sh-dark-green);
      margin-bottom: 20px;
      padding-bottom: 12px;
      border-bottom: 2px solid var(--sh-pale-green);
    }

    /* FORM */
    .form-group { margin-bottom: 14px; }
    .form-group label {
      display: block;
      font-family: 'Montserrat Alternates', sans-serif;
      font-size: 11px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--sh-light-green);
      margin-bottom: 6px;
    }
    .form-group input, .form-group select {
      width: 100%;
      padding: 13px 16px;
      border: 1.5px solid #d5d0c8;
      border-radius: 8px;
      font-family: 'Montserrat', sans-serif;
      font-size: 16px; /* prevent zoom on iOS */
      background: white;
      color: var(--sh-dark-green);
      outline: none;
      -webkit-appearance: none;
    }
    .form-group input:focus { border-color: var(--sh-dark-green); }
    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
    .form-actions { display: flex; gap: 10px; margin-top: 20px; }
    .form-actions .btn-primary { flex: 2; padding: 15px; font-size: 15px; border-radius: 8px; text-align: center; }
    .form-actions .btn-cancel { flex: 1; padding: 15px; font-size: 15px; border-radius: 8px; background: #e8e4dd; border: none; color: var(--sh-light-green); font-family: 'Montserrat', sans-serif; font-weight: 700; text-transform: uppercase; letter-spacing: 0.05em; cursor: pointer; }

    /* DETAIL SHEET */
    .detail-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 16px; }
    .detail-field .dl { font-family: 'Montserrat Alternates', sans-serif; font-size: 10px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.1em; color: var(--sh-pale-green); margin-bottom: 2px; }
    .detail-field .dv { font-size: 16px; font-weight: 700; color: var(--sh-dark-green); }
    .usage-history { border-top: 1px solid var(--sh-pale-green); padding-top: 14px; margin-top: 4px; }
    .usage-history h4 { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; color: var(--sh-pale-green); margin-bottom: 10px; }
    .usage-item { display: flex; justify-content: space-between; align-items: center; font-size: 13px; padding: 8px 0; border-bottom: 1px solid #e8e4dd; color: var(--sh-light-green); }
    .usage-item:last-child { border-bottom: none; }
    .usage-item strong { color: var(--sh-dark-green); font-weight: 700; font-size: 14px; }

    /* TOAST */
    #toast {
      position: fixed;
      bottom: calc(100px + var(--safe-bottom));
      left: 50%;
      transform: translateX(-50%);
      background: var(--sh-dark-green);
      color: var(--sh-beige);
      padding: 12px 22px;
      border-radius: 24px;
      font-size: 13px;
      font-weight: 600;
      z-index: 9999;
      box-shadow: 0 4px 20px rgba(0,0,0,0.25);
      opacity: 0;
      transition: opacity 0.3s;
      white-space: nowrap;
      pointer-events: none;
    }

    footer {
      text-align: center;
      padding: 16px;
      color: var(--sh-pale-green);
      font-size: 10px;
      font-family: 'Montserrat Alternates', sans-serif;
      text-transform: uppercase;
      letter-spacing: 0.1em;
    }
  </style>
</head>
<body>

<header>
  <div class="header-top">
    <div>
      <div class="logo-text">SWING<span>HOUSE</span></div>
    </div>
    <div class="header-actions">
      <button onclick="exportCSV()" style="background:transparent;border:1.5px solid rgba(240,236,229,0.35);color:var(--sh-beige);font-family:'Montserrat',sans-serif;font-size:12px;font-weight:600;text-transform:uppercase;letter-spacing:0.06em;padding:8px 14px;border-radius:8px;cursor:pointer">Export CSV</button>
    </div>
  </div>
  <div class="stats-strip" id="statsStrip"></div>
</header>

<div class="filter-bar">
  <button class="filter-chip active" id="fc-all" onclick="setFilter('all')">Tous</button>
  <button class="filter-chip" id="fc-active" onclick="setFilter('active')">Actifs</button>
  <button class="filter-chip" id="fc-partial" onclick="setFilter('partial')">Partiels</button>
  <button class="filter-chip" id="fc-used" onclick="setFilter('used')">Utilisés</button>
</div>

<div class="search-wrap">
  <input class="search-input" type="search" id="searchInput" placeholder="🔍  Rechercher un client…" oninput="renderList()" autocapitalize="none" autocorrect="off">
</div>

<div class="card-list" id="cardList"></div>

<div class="empty-state" id="emptyState" style="display:none">
  <p>Aucun bon cadeau<br>Appuyez sur + pour en ajouter un</p>
</div>

<footer>Swing House Chamonix — @swinghouse.chx</footer>

<!-- FAB -->
<button class="fab" onclick="openAddModal()" title="Nouveau bon cadeau">+</button>

<!-- TOAST -->
<div id="toast"></div>

<!-- ════════ MODAL : AJOUTER ════════ -->
<div class="modal-overlay" id="addModal" onclick="if(event.target===this)closeModal('addModal')">
  <div class="modal">
    <div class="sheet-handle"></div>
    <h3>Nouveau bon cadeau</h3>
    <div class="form-group">
      <label>Nom du client *</label>
      <input type="text" id="add_client" placeholder="Jean Dupont" autocapitalize="words">
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Montant (€) *</label>
        <input type="number" id="add_amount" placeholder="150" min="1" step="0.01" inputmode="decimal">
      </div>
      <div class="form-group">
        <label>Date de vente *</label>
        <input type="date" id="add_date">
      </div>
    </div>
    <div class="form-group">
      <label>Note (optionnel)</label>
      <input type="text" id="add_note" placeholder="Ex: Anniversaire, offert par…" autocapitalize="sentences">
    </div>
    <div class="form-actions">
      <button class="btn-cancel" onclick="closeModal('addModal')">Annuler</button>
      <button class="btn-primary" onclick="addVoucher()">Créer le bon</button>
    </div>
  </div>
</div>

<!-- ════════ MODAL : UTILISER ════════ -->
<div class="modal-overlay" id="useModal" onclick="if(event.target===this)closeModal('useModal')">
  <div class="modal">
    <div class="sheet-handle"></div>
    <h3 id="useModalTitle">Utiliser le bon</h3>
    <div class="form-row">
      <div class="form-group">
        <label>Montant utilisé (€) *</label>
        <input type="number" id="use_amount" placeholder="0" min="0.01" step="0.01" inputmode="decimal">
      </div>
      <div class="form-group">
        <label>Date *</label>
        <input type="date" id="use_date">
      </div>
    </div>
    <div class="form-group">
      <label>Note (optionnel)</label>
      <input type="text" id="use_note" placeholder="Séance simulation 1h…" autocapitalize="sentences">
    </div>
    <div class="form-actions">
      <button class="btn-cancel" onclick="closeModal('useModal')">Annuler</button>
      <button class="btn-primary" onclick="recordUsage()">Enregistrer</button>
    </div>
  </div>
</div>

<!-- ════════ MODAL : DÉTAIL ════════ -->
<div class="modal-overlay" id="detailModal" onclick="if(event.target===this)closeModal('detailModal')">
  <div class="modal" style="max-width:600px">
    <div class="sheet-handle"></div>
    <h3 id="detailTitle"></h3>
    <div id="detailContent"></div>
    <div style="margin-top:16px">
      <button id="detailUseBtn" class="btn-primary" style="width:100%;padding:14px;font-size:15px;border-radius:8px" onclick="openUseFromDetail()">Enregistrer une utilisation</button>
    </div>
  </div>
</div>

<script>
// ══════════════════════════════════
//  STORAGE — localStorage (iPad Safari)
// ══════════════════════════════════
const STORAGE_KEY = 'sh_bons_cadeaux_v2';

function save() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(vouchers));
}
function load() {
  try { return JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'); }
  catch(e) { return []; }
}

let vouchers = load();
let currentFilter = 'all';
let activeVoucherId = null;
let detailVoucherId = null;

// ══════════════════════════════════
//  UTILS
// ══════════════════════════════════
function genRef() {
  const alpha = 'ABCDEFGHJKLMNPQRSTUVWXYZ';
  const r = () => alpha[Math.floor(Math.random()*alpha.length)];
  const n = () => Math.floor(Math.random()*10);
  return `SH-${r()}${r()}${n()}${n()}${n()}`;
}
function today() { return new Date().toISOString().split('T')[0]; }
function fmtDate(d) { if(!d) return '—'; const[y,m,day]=d.split('-'); return `${day}/${m}/${y}`; }
function fmtEur(n) { return Number(n).toLocaleString('fr-FR',{minimumFractionDigits:2,maximumFractionDigits:2})+' €'; }

function getStatus(v) {
  const u = getTotalUsed(v);
  if (u >= v.amount) return 'used';
  if (u > 0) return 'partial';
  return 'active';
}
function getRemaining(v) { return Math.max(0, v.amount - getTotalUsed(v)); }
function getTotalUsed(v) { return v.usages.reduce((s,u)=>s+u.amount, 0); }

const SL = { active:'Actif', partial:'Partiel', used:'Utilisé' };
const SB = { active:'badge-active', partial:'badge-partial', used:'badge-used' };

// ══════════════════════════════════
//  TOAST
// ══════════════════════════════════
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.style.opacity = '1';
  clearTimeout(t._t);
  t._t = setTimeout(()=>{t.style.opacity='0';}, 2500);
}

// ══════════════════════════════════
//  EXPORT CSV
// ══════════════════════════════════
function exportCSV() {
  if (!vouchers.length) { alert('Aucun bon à exporter.'); return; }
  const rows = [['Référence','Client','Date vente','Montant €','Utilisé €','Restant €','Statut','Note']];
  vouchers.forEach(v => {
    rows.push([v.ref, v.client, fmtDate(v.date), v.amount.toFixed(2), getTotalUsed(v).toFixed(2), getRemaining(v).toFixed(2), SL[getStatus(v)], v.note||'']);
    v.usages.forEach(u => rows.push(['','  → '+(u.note||'Utilisation'), fmtDate(u.date),'',u.amount.toFixed(2),'','','']));
  });
  const csv = rows.map(r=>r.map(c=>`"${String(c).replace(/"/g,'""')}"`).join(',')).join('\n');
  const blob = new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8'});
  const url = URL.createObjectURL(blob);
  // Sur iPad : tenter Web Share API, sinon ouvrir dans nouvel onglet
  if (navigator.share) {
    const file = new File([blob], `bons-cadeaux-${today()}.csv`, {type:'text/csv'});
    if (navigator.canShare && navigator.canShare({files:[file]})) {
      navigator.share({files:[file], title:'Bons Cadeaux Swing House'});
      return;
    }
  }
  window.open(url, '_blank');
}

// ══════════════════════════════════
//  STATS
// ══════════════════════════════════
function renderStats() {
  const total = vouchers.length;
  const totalVal = vouchers.reduce((s,v)=>s+v.amount, 0);
  const remaining = vouchers.reduce((s,v)=>s+getRemaining(v), 0);
  const active = vouchers.filter(v=>getStatus(v)!=='used').length;
  document.getElementById('statsStrip').innerHTML = `
    <div class="stat-item accent"><div class="sv">${total}</div><div class="sl">Vendus</div></div>
    <div class="stat-item"><div class="sv">${active}</div><div class="sl">Actifs</div></div>
    <div class="stat-item"><div class="sv">${Math.round(totalVal)}€</div><div class="sl">Total</div></div>
    <div class="stat-item"><div class="sv">${Math.round(remaining)}€</div><div class="sl">Restant</div></div>`;
}

// ══════════════════════════════════
//  FILTER & LIST
// ══════════════════════════════════
function setFilter(f) {
  currentFilter = f;
  document.querySelectorAll('.filter-chip').forEach(b=>b.classList.remove('active'));
  document.getElementById('fc-'+f).classList.add('active');
  renderList();
}

function renderList() {
  const search = document.getElementById('searchInput').value.toLowerCase().trim();
  let list = vouchers.filter(v => {
    if (search && !v.client.toLowerCase().includes(search) && !v.ref.toLowerCase().includes(search)) return false;
    if (currentFilter==='all') return true;
    return getStatus(v)===currentFilter;
  }).sort((a,b)=>b.date.localeCompare(a.date));

  const container = document.getElementById('cardList');
  const empty = document.getElementById('emptyState');

  if (list.length===0) { container.innerHTML=''; empty.style.display='block'; renderStats(); return; }
  empty.style.display = 'none';

  container.innerHTML = list.map(v => {
    const status = getStatus(v);
    const remaining = getRemaining(v);
    const used = getTotalUsed(v);
    const pct = Math.min(100, Math.round((used/v.amount)*100));
    const isUsed = status==='used';
    return `
    <div class="voucher-card">
      <div class="card-main" onclick="openDetail('${v.id}')">
        <div class="card-top">
          <div>
            <div class="card-client">${v.client}</div>
            <div class="card-ref">${v.ref} · ${fmtDate(v.date)}</div>
            ${v.note?`<div class="card-note">${v.note}</div>`:''}
          </div>
          <span class="badge ${SB[status]}">${SL[status]}</span>
        </div>
        <div class="card-amounts">
          <div class="amount-block">
            <div class="ab-label">Montant</div>
            <div class="ab-value">${fmtEur(v.amount)}</div>
          </div>
          <div class="amount-block">
            <div class="ab-label">Utilisé</div>
            <div class="ab-value used">${fmtEur(used)}</div>
          </div>
          <div class="amount-block">
            <div class="ab-label">Restant</div>
            <div class="ab-value ${remaining===0?'zero':''}">${fmtEur(remaining)}</div>
          </div>
        </div>
        ${pct>0?`<div class="card-progress"><div class="progress-track"><div class="progress-fill ${pct>80?'warn':''}" style="width:${pct}%"></div></div></div>`:''}
      </div>
      <div class="card-footer">
        <button class="card-footer-btn use-btn" onclick="openUseModal('${v.id}')" ${isUsed?'disabled':''}>
          ${isUsed?'✓ Soldé':'Utiliser'}
        </button>
        <button class="card-footer-btn" onclick="openDetail('${v.id}')">Détail</button>
        <button class="card-footer-btn del-btn" onclick="deleteVoucher('${v.id}')">Supprimer</button>
      </div>
    </div>`;
  }).join('');
  renderStats();
}

// ══════════════════════════════════
//  MODALS
// ══════════════════════════════════
function openAddModal() {
  document.getElementById('add_client').value='';
  document.getElementById('add_amount').value='';
  document.getElementById('add_date').value=today();
  document.getElementById('add_note').value='';
  document.getElementById('addModal').classList.add('open');
  setTimeout(()=>document.getElementById('add_client').focus(),300);
}

function openUseModal(id) {
  const v = vouchers.find(x=>x.id===id);
  if(!v) return;
  activeVoucherId=id;
  document.getElementById('useModalTitle').textContent=`${v.client} — ${fmtEur(getRemaining(v))} restant`;
  document.getElementById('use_amount').value='';
  document.getElementById('use_amount').max=getRemaining(v);
  document.getElementById('use_date').value=today();
  document.getElementById('use_note').value='';
  closeModal('detailModal');
  document.getElementById('useModal').classList.add('open');
  setTimeout(()=>document.getElementById('use_amount').focus(),300);
}

function openUseFromDetail() {
  openUseModal(detailVoucherId);
}

function openDetail(id) {
  const v = vouchers.find(x=>x.id===id);
  if(!v) return;
  detailVoucherId = id;
  const status=getStatus(v), remaining=getRemaining(v), used=getTotalUsed(v);
  const usageRows = v.usages.length===0
    ? '<p style="color:var(--sh-pale-green);font-size:13px;padding:8px 0">Aucune utilisation enregistrée.</p>'
    : v.usages.map(u=>`<div class="usage-item"><div><div>${fmtDate(u.date)}</div>${u.note?`<div style="font-size:11px;color:var(--sh-pale-green)">${u.note}</div>`:''}</div><strong>-${fmtEur(u.amount)}</strong></div>`).join('');
  document.getElementById('detailTitle').textContent=`${v.client}`;
  document.getElementById('detailContent').innerHTML=`
    <div class="detail-grid">
      <div class="detail-field"><div class="dl">Référence</div><div class="dv" style="font-size:14px;font-family:'Montserrat Alternates'">${v.ref}</div></div>
      <div class="detail-field"><div class="dl">Statut</div><div class="dv"><span class="badge ${SB[status]}">${SL[status]}</span></div></div>
      <div class="detail-field"><div class="dl">Date de vente</div><div class="dv">${fmtDate(v.date)}</div></div>
      <div class="detail-field"><div class="dl">Montant initial</div><div class="dv">${fmtEur(v.amount)}</div></div>
      <div class="detail-field"><div class="dl">Montant utilisé</div><div class="dv" style="color:var(--sh-light-green)">${fmtEur(used)}</div></div>
      <div class="detail-field"><div class="dl">Solde restant</div><div class="dv" style="color:var(--sh-orange)">${fmtEur(remaining)}</div></div>
    </div>
    ${v.note?`<div style="padding:10px 0;color:var(--sh-pale-green);font-size:13px;border-top:1px solid #e8e4dd;margin-top:4px">📝 ${v.note}</div>`:''}
    <div class="usage-history">
      <h4>Historique (${v.usages.length} utilisation${v.usages.length!==1?'s':''})</h4>
      ${usageRows}
    </div>`;
  const useBtn = document.getElementById('detailUseBtn');
  useBtn.style.display = status==='used' ? 'none' : 'block';
  document.getElementById('detailModal').classList.add('open');
}

function closeModal(id) { document.getElementById(id).classList.remove('open'); }

// ══════════════════════════════════
//  CRUD
// ══════════════════════════════════
function addVoucher() {
  const client = document.getElementById('add_client').value.trim();
  const amount = parseFloat(document.getElementById('add_amount').value);
  const date = document.getElementById('add_date').value;
  const note = document.getElementById('add_note').value.trim();
  if (!client) { showToast('⚠ Saisissez le nom du client'); return; }
  if (!amount || amount<=0) { showToast('⚠ Montant invalide'); return; }
  if (!date) { showToast('⚠ Sélectionnez une date'); return; }
  let ref; do { ref=genRef(); } while (vouchers.find(v=>v.ref===ref));
  vouchers.push({id:Date.now().toString(), ref, client, amount, date, note, usages:[]});
  save();
  closeModal('addModal');
  renderList();
  showToast(`✓ Bon ${ref} créé`);
}

function recordUsage() {
  const v = vouchers.find(x=>x.id===activeVoucherId);
  if(!v) return;
  const amount = parseFloat(document.getElementById('use_amount').value);
  const date = document.getElementById('use_date').value;
  const note = document.getElementById('use_note').value.trim();
  const remaining = getRemaining(v);
  if (!amount||amount<=0) { showToast('⚠ Montant invalide'); return; }
  if (amount>remaining+0.001) { showToast(`⚠ Dépasse le solde (${fmtEur(remaining)})`); return; }
  if (!date) { showToast('⚠ Sélectionnez une date'); return; }
  v.usages.push({id:Date.now().toString(), amount, date, note});
  save();
  closeModal('useModal');
  renderList();
  showToast(`✓ ${fmtEur(amount)} enregistré`);
}

function deleteVoucher(id) {
  const v = vouchers.find(x=>x.id===id);
  if(!v) return;
  if(!confirm(`Supprimer le bon de ${v.client} (${v.ref}) ?`)) return;
  vouchers = vouchers.filter(x=>x.id!==id);
  save();
  closeModal('detailModal');
  renderList();
  showToast('Bon supprimé');
}

// ══════════════════════════════════
//  INIT
// ══════════════════════════════════
renderList();
</script>
</body>
</html>
