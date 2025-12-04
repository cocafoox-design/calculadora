<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Calculadora Bennys</title>
<style>
:root{
  --bg1:#000;
  --bg2:#2a0000;
  --panel:rgba(0,0,0,0.6);
  --accent:#ff2b2b;
  --muted:#ddd;
}
*{box-sizing:border-box}
body{ margin:0; font-family:Arial,Helvetica,sans-serif; background:linear-gradient(180deg,var(--bg1),var(--bg2)); color:#fff; -webkit-font-smoothing:antialiased; }
.wrap{ max-width:1200px; margin:18px auto; padding:12px; }
.logo{ width:100%; max-height:160px; object-fit:contain; border-radius:8px; display:block; margin:0 auto 14px; }
.grid{ display:grid; grid-template-columns: 1fr 380px; gap:18px; align-items:start; }
@media(max-width:980px){ .grid{ grid-template-columns: 1fr; } .right{ order:2 } }
.panel{ background:var(--panel); padding:14px; border-radius:10px; box-shadow:0 8px 30px rgba(0,0,0,0.6); border:1px solid rgba(255,0,0,0.06); }
h2{ color:var(--accent); margin:6px 0 12px 0; font-size:18px; letter-spacing:0.6px; text-transform:uppercase; }
.btn{ display:inline-block; width:calc(50% - 12px); min-width:160px; margin:6px; padding:10px 12px; background:#191919; border-radius:8px; color:#fff; border:1px solid rgba(255,255,255,0.04); text-align:left; cursor:pointer; }
.btn.small{ width:calc(33.33% - 12px); }
.controls{ display:flex; flex-wrap:wrap; gap:6px; }
.totalBox{ background:linear-gradient(90deg,#3a0000, rgba(0,0,0,0.6)); padding:12px; border-radius:10px; text-align:center; margin-bottom:8px; border:2px solid #600; }
.totalVal{ font-size:28px; font-weight:700; color:#ffdede; margin-top:6px; }
.reset{ background:#222; border:none; padding:10px 12px; color:#fff; border-radius:8px; cursor:pointer; margin-top:10px; }
.kit-input{ width:80px; padding:8px; border-radius:6px; border:1px solid rgba(255,255,255,0.06); background:#111; color:var(--muted); }
.hint{ font-size:13px; color:#ddd; opacity:0.95; margin-top:8px; }

.items-list{ list-style:none; margin:0; padding:0; max-height:260px; overflow:auto; }
.items-list li{ display:flex; justify-content:space-between; gap:8px; padding:8px; border-bottom:1px solid rgba(255,255,255,0.03); align-items:center; }
.items-list .lbl{ flex:1; color:var(--muted) }
.items-list .price{ min-width:120px; text-align:right; font-weight:700; color:#ffdede }
.items-list button.remove{ margin-left:8px; background:#2b0000; border:0; padding:6px 8px; border-radius:6px; color:#fff; cursor:pointer; }

@media(max-width:600px){
  .btn{ width:calc(50% - 12px); min-width:140px }
  .btn.small{ width:calc(50% - 12px); }
  .totalVal{ font-size:22px }
}
</style>
</head>
<body>
<div class="wrap">
  <!-- coloque a imagem Prancheta_3.png na mesma pasta (ou atualize o src) -->
  <img class="logo" src="Prancheta_3.png" alt="Mecânica Bennys">

  <div class="grid">
    <div class="panel left">
      <h2>Full Tuning</h2>
      <div class="controls">
        <button class="btn" data-price="100000" data-group="full" data-label="Carro + Blindagem">Carro + Blindagem — R$ 100.000</button>
        <button class="btn" data-price="75000" data-group="full" data-label="Carro sem Blindagem">Carro sem Blindagem — R$ 75.000</button>
        <button class="btn" data-price="85000" data-group="full" data-label="Moto + Blindagem">Moto + Blindagem — R$ 85.000</button>
        <button class="btn" data-price="60000" data-group="full" data-label="Moto sem Blindagem">Moto sem Blindagem — R$ 60.000</button>

        <button class="btn" id="parceriaToggle" title="Aplica 20% de desconto retroativo para itens Full Tuning">
          <input type="checkbox" id="parceriaCheckbox"> Parceria (20% OFF Full Tuning)
        </button>
      </div>

      <h2 style="margin-top:18px">Modificações — R$ 2.500 cada</h2>
      <div class="controls" id="mods">
        <button class="btn" data-price="2500" data-label="Aerofólio">Aerofólio — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Buzinas">Buzinas — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Enfeites">Enfeites — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Ponteiros">Ponteiros — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Fumaça">Fumaça — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Placa Design">Placa Design — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Vidro">Vidro — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Filtro de Ar">Filtro de Ar — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Escapamento">Escapamento — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Gaiola">Gaiola — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Grelha">Grelha — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Capô">Capô — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Bloco do Motor">Bloco do Motor — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Parachoque F/T">Parachoque F/T — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Placas (interior)">Placas (interior) — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Design">Design — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Volante">Volante — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Câmbio">Câmbio — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Som">Som — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Porta-Malas">Porta-Malas — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Rodas Custom">Rodas Custom — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Rodas Drift">Rodas Drift — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Placa Custom">Placa Custom — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Kit Neon">Kit Neon — R$ 2.500</button>
        <button class="btn" data-price="2500" data-label="Extras">Extras — R$ 2.500</button>
      </div>

      <h2 style="margin-top:18px">Cores — R$ 4.000 cada</h2>
      <div class="controls">
        <button class="btn" data-price="4000" data-label="Metálica">Metálica — R$ 4.000</button>
        <button class="btn" data-price="4000" data-label="Perolado">Perolado — R$ 4.000</button>
        <button class="btn" data-price="4000" data-label="Cromado">Cromado — R$ 4.000</button>
        <button class="btn" data-price="4000" data-label="Fosco">Fosco — R$ 4.000</button>
        <button class="btn" data-price="4000" data-label="Metal">Metal — R$ 4.000</button>
      </div>
    </div>

    <div class="panel right">
      <h2>Diversos</h2>
      <div class="controls">
        <button class="btn small" data-price="2000" data-label="Interno">Interno — R$ 2.000</button>
        <div style="display:flex;align-items:center;gap:8px;">
          <input id="kitQty" class="kit-input" type="number" min="0" value="0" aria-label="Quantidade Kit Reparo">
          <button class="btn small" id="addKit" data-price="2250" data-label="Kit Reparo">Adicionar Kit Reparo (R$ 2.250)</button>
        </div>
        <button class="btn small" data-price="7500" data-label="Xenon">Xenon — R$ 7.500</button>
        <button class="btn small" data-price="7500" data-label="Decal">Decal — R$ 7.500</button>
        <button class="btn small" data-price="7500" data-label="Rodas">Rodas — R$ 7.500</button>
      </div>

      <div style="margin-top:14px" class="totalBox">
        <div class="hint">TOTAL ATUAL</div>
        <div class="totalVal" id="totalDisplay">R$ 0,00</div>
        <div class="hint" id="countDisplay">0 itens</div>
        <button class="reset" id="resetBtn">Resetar</button>
        <button class="reset" id="exportBtn" title="Baixar resumo CSV" style="margin-left:8px">Exportar CSV</button>

        <div class="hint" style="margin-top:8px">Clique nos itens para somar. Você pode remover itens individuais na lista.</div>
      </div>

      <div class="panel" style="margin-top:12px">
        <h2>Itens adicionados</h2>
        <ul id="itemsList" class="items-list" aria-live="polite"></ul>
      </div>
    </div>
  </div>

  <div style="text-align:center; margin-top:18px; color:#ddd; font-size:13px">
    Salve o arquivo e abra no navegador. Se quiser, eu hospedo no CodePen para facilitar o teste.
  </div>
</div>

<script>
(() => {
  const items = []; // { id, label, basePrice, group }
  let nextId = 1;

  const totalDisplay = document.getElementById('totalDisplay');
  const itemsList = document.getElementById('itemsList');
  const countDisplay = document.getElementById('countDisplay');
  const parceriaCheckbox = document.getElementById('parceriaCheckbox');
  const resetBtn = document.getElementById('resetBtn');
  const exportBtn = document.getElementById('exportBtn');
  const kitQtyInput = document.getElementById('kitQty');
  const addKitBtn = document.getElementById('addKit');

  // Helpers
  const fmt = (v) => Number(v).toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
  const isFullGroup = g => g === 'full';

  function calculateTotal() {
    const parceria = parceriaCheckbox.checked;
    let total = 0;
    items.forEach(it => {
      let price = Number(it.basePrice) || 0;
      if (parceria && isFullGroup(it.group)) price = price * 0.8; // aplica 20%
      total += price;
    });
    return total;
  }

  function render() {
    const parceria = parceriaCheckbox.checked;
    // total
    const total = calculateTotal();
    totalDisplay.innerText = 'R$ ' + fmt(total);
    countDisplay.innerText = `${items.length} ${items.length === 1 ? 'item' : 'itens'}`;

    // items list
    itemsList.innerHTML = '';
    items.forEach(it => {
      const li = document.createElement('li');

      const lbl = document.createElement('div');
      lbl.className = 'lbl';
      lbl.textContent = it.label + (it.group ? ` ${it.group === 'full' ? '(Full)' : ''}` : '');

      const priceDiv = document.createElement('div');
      priceDiv.className = 'price';
      let price = Number(it.basePrice) || 0;
      if (parceria && isFullGroup(it.group)) {
        const disc = price * 0.8;
        priceDiv.innerHTML = `<span style="text-decoration:line-through; opacity:0.6; margin-right:8px">R$ ${fmt(price)}</span><strong>R$ ${fmt(disc)}</strong>`;
      } else {
        priceDiv.innerHTML = `<strong>R$ ${fmt(price)}</strong>`;
      }

      const rm = document.createElement('button');
      rm.className = 'remove';
      rm.textContent = 'Remover';
      rm.title = 'Remover item';
      rm.addEventListener('click', () => {
        removeItem(it.id);
      });

      li.appendChild(lbl);
      li.appendChild(priceDiv);
      li.appendChild(rm);
      itemsList.appendChild(li);
    });
  }

  function addItem(basePrice, label, group) {
    items.push({ id: nextId++, label: label || 'Item', basePrice: Number(basePrice) || 0, group: group || '' });
    render();
  }

  function removeItem(id) {
    const idx = items.findIndex(i => i.id === id);
    if (idx >= 0) items.splice(idx, 1);
    render();
  }

  function resetAll() {
    items.length = 0;
    nextId = 1;
    parceriaCheckbox.checked = false;
    kitQtyInput.value = 0;
    render();
  }

  // attach click handlers for all .btn that have data-price
  document.querySelectorAll('.btn').forEach(btn => {
    const price = btn.dataset.price;
    const label = btn.dataset.label || btn.innerText.trim();
    const group = btn.dataset.group || '';
    // add special behavior for partnership toggle button (contains checkbox)
    if (btn.id === 'parceriaToggle') {
      btn.addEventListener('click', (e) => {
        if (e.target.tagName.toLowerCase() === 'input') return;
        parceriaCheckbox.checked = !parceriaCheckbox.checked;
        render();
      });
      return;
    }

    // normal item buttons
    if (price !== undefined) {
      btn.addEventListener('click', () => addItem(Number(price), label, group));
    }
  });

  // kit add button uses quantity input
  addKitBtn.addEventListener('click', () => {
    const qty = Math.max(0, parseInt(kitQtyInput.value || '0', 10));
    const unit = Number(addKitBtn.dataset.price) || 2250;
    for (let i = 0; i < qty; i++) {
      addItem(unit, addKitBtn.dataset.label || 'Kit Reparo');
    }
    kitQtyInput.value = 0;
  });

  // also allow Enter key on qty to add one
  kitQtyInput.addEventListener('keydown', (e) => {
    if (e.key === 'Enter') addKitBtn.click();
  });

  // partnership checkbox change -> re-render (aplica retroativo)
  parceriaCheckbox.addEventListener('change', render);

  // reset
  resetBtn.addEventListener('click', resetAll);

  // export CSV summary
  exportBtn.addEventListener('click', () => {
    const parceria = parceriaCheckbox.checked;
    const rows = [['Label','Preço base','Preço aplicado']];
    items.forEach(it => {
      const base = Number(it.basePrice) || 0;
      const applied = (parceria && isFullGroup(it.group)) ? base * 0.8 : base;
      rows.push([it.label, base.toFixed(2), applied.toFixed(2)]);
    });
    rows.push([]);
    rows.push(['Total', '', calculateTotal().toFixed(2)]);
    const csv = rows.map(r => r.map(cell => `"${String(cell).replace(/"/g,'""')}"`).join(',')).join('\n');
    const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `resumo_modificacoes_${new Date().toISOString().slice(0,10)}.csv`;
    document.body.appendChild(a);
    a.click();
    a.remove();
    URL.revokeObjectURL(url);
  });

  // initialize
  render();

  // Expose addItem for possible external use (not required)
  window.addItem = addItem;
})();
</script>
</body>
</html>
