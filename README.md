<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>RectaPlus – Áreas más fáciles, pasos más simples</title>
<style>
  :root {
    --navy: #0f1f4a;
    --navy-2: #14275a;
    --blue: #2563eb;
    --blue-soft: #e8f0fd;
    --blue-line: #cfdcf5;
    --text: #0f1f4a;
    --muted: #4b5b80;
    --bg: #f5f8fe;
    --card: #ffffff;
    --red: #ef4444;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: "Segoe UI", "Helvetica Neue", Arial, sans-serif;
    color: var(--text);
    background: var(--bg);
    min-height: 100vh;
    display: grid;
    grid-template-columns: 250px 1fr;
    grid-template-rows: 105px 1fr;
    grid-template-areas: "top top" "side main";
  }
  button { font: inherit; cursor: pointer; border: 0; }
  :focus-visible { outline: 3px solid #93b4f8; outline-offset: 2px; }

  /* Barra superior */
  .top {
    grid-area: top; background: var(--navy); color: #fff;
    display: flex; align-items: center; justify-content: space-between;
    padding: 0 32px;
  }
  .brand { display: flex; align-items: center; gap: 20px; }
  .logo {
    width: 76px; height: 66px; border-radius: 14px; background: var(--blue);
    display: grid; place-items: center;
  }
  .logo span { width: 44px; height: 30px; border: 4px solid #fff; border-radius: 4px; }
  .brand h1 { font-size: 40px; line-height: 1; font-weight: 600; }
  .brand h1 b { color: #4f8cff; font-weight: 600; }
  .brand p { color: #c9d6f5; font-size: 18px; margin-top: 6px; }
  .account { display: flex; align-items: center; gap: 12px; color: #dbe5fb; font-size: 18px; }
  .avatar { width: 38px; height: 38px; border-radius: 50%; background: #dbe5fb; display: grid; place-items: center; }
  .avatar svg { width: 22px; height: 22px; fill: var(--navy); }

  /* Menú lateral */
  .side {
    grid-area: side; background: var(--navy-2); color: #dbe5fb;
    padding: 22px 12px; display: flex; flex-direction: column;
  }
  .side nav { display: flex; flex-direction: column; gap: 8px; }
  .side a {
    display: flex; align-items: center; gap: 18px; padding: 16px 14px;
    border-radius: 12px; color: inherit; text-decoration: none; font-size: 18px;
  }
  .side a svg { width: 26px; height: 26px; fill: none; stroke: currentColor; stroke-width: 1.8; stroke-linecap: round; stroke-linejoin: round; }
  .side a.active { background: linear-gradient(90deg, #2563eb, #3b6fe0); color: #fff; }
  .side a:hover:not(.active) { background: rgba(255,255,255,.07); }
  .tip { margin-top: auto; display: flex; gap: 14px; padding: 12px; font-size: 16px; line-height: 1.35; }
  .tip svg { width: 28px; height: 28px; flex: none; fill: none; stroke: #dbe5fb; stroke-width: 1.6; }
  .tip i { display: block; width: 36px; height: 3px; background: var(--blue); margin-top: 10px; }

  /* Contenido */
  main {
    grid-area: main; padding: 40px 36px 0; background: #fbfdff;
    display: grid; grid-template-columns: 1fr 530px; gap: 20px 20px;
    grid-template-rows: 1fr auto; align-items: start;
  }
  .left h2 { font-size: 38px; font-weight: 700; }
  .left > p { color: var(--muted); font-size: 20px; margin: 10px 0 28px; }
  .card { background: var(--card); border: 1px solid var(--blue-line); border-radius: 14px; }

  .calc { display: grid; grid-template-columns: 1fr 1fr; gap: 26px; padding: 22px 28px 40px 28px; }
  .calc label { display: block; font-weight: 700; font-size: 20px; margin: 10px 0 8px; }
  .field { display: flex; border: 1px solid var(--blue-line); border-radius: 6px; overflow: hidden; }
  .field input {
    flex: 1; min-width: 0; border: 0; padding: 12px 14px; font-size: 20px; color: var(--text); background: #fff;
  }
  .field input:focus { outline: none; }
  .field:focus-within { border-color: var(--blue); box-shadow: 0 0 0 3px #bcd1fa; }
  .field span { background: #f0f3f8; padding: 12px 18px; font-size: 20px; color: var(--muted); border-left: 1px solid var(--blue-line); }
  .btn-calc {
    width: 100%; margin-top: 22px; background: var(--blue); color: #fff; font-size: 20px; font-weight: 600;
    padding: 12px; border-radius: 6px; display: flex; align-items: center; justify-content: center; gap: 12px;
  }
  .btn-calc:hover { background: #1d52c9; }
  .btn-calc svg { width: 26px; height: 26px; fill: none; stroke: #fff; stroke-width: 1.8; }
  .error { color: var(--red); font-size: 15px; margin-top: 8px; min-height: 20px; }

  .result { background: var(--blue-soft); border-radius: 12px; padding: 20px 26px; text-align: center; }
  .result h3 { color: var(--blue); text-align: left; font-size: 21px; margin-bottom: 18px; }
  .math { font-family: "Cambria Math", "STIX Two Text", Georgia, serif; font-size: 27px; }
  .math i { font-style: italic; }
  .result .math + .math { margin-top: 16px; }
  .result .final { background: #dbe8fc; border-radius: 8px; padding: 16px; margin-top: 22px; font-size: 29px; }

  .explain { display: grid; grid-template-columns: 310px 1fr; gap: 28px; padding: 18px; margin-top: 16px; }
  .diagram { background: #f6f9fe; padding: 16px 8px 8px; text-align: center; border-radius: 8px; }
  .diagram h4 { font-size: 19px; margin-bottom: 14px; }
  .explain h4.q { font-size: 19px; margin-top: 4px; }
  .explain p { color: var(--muted); font-size: 18px; line-height: 1.4; margin: 8px 0 12px; }
  .formula { background: var(--blue-soft); border-radius: 8px; text-align: center; padding: 10px; font-size: 28px; }
  .legend { color: var(--muted); font-size: 16px; line-height: 1.6; margin-top: 12px; font-family: "Cambria Math", Georgia, serif; }
  .legend i { font-style: italic; margin-right: 4px; }

  /* Lista de tareas */
  .tasks { padding: 22px 18px; }
  .tasks header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 20px; padding: 0 4px; }
  .tasks h3 { display: flex; align-items: center; gap: 16px; font-size: 24px; }
  .tasks h3 svg { width: 36px; height: 36px; fill: none; stroke: var(--blue); stroke-width: 2; }
  .btn-new {
    background: var(--blue); color: #fff; font-size: 18px; padding: 12px 22px; border-radius: 6px;
    display: flex; align-items: center; gap: 12px;
  }
  .btn-new:hover { background: #1d52c9; }
  .btn-new b { font-size: 28px; font-weight: 400; line-height: 1; }
  #list { list-style: none; display: flex; flex-direction: column; gap: 14px; }
  .task {
    display: flex; align-items: center; gap: 14px; padding: 16px 20px 16px 16px;
    border: 1px solid #e3eaf7; border-radius: 8px; background: #fff;
  }
  .task input[type=checkbox] { width: 26px; height: 26px; accent-color: var(--blue); flex: none; cursor: pointer; }
  .task .info { flex: 1; min-width: 0; }
  .task .name { font-size: 18px; line-height: 1.3; }
  .task.done .name { color: var(--muted); }
  .task .date { display: flex; align-items: center; gap: 8px; color: var(--muted); font-size: 16px; margin-top: 8px; }
  .task .date svg { width: 18px; height: 18px; fill: none; stroke: var(--muted); stroke-width: 1.6; }
  .icon-btn { width: 34px; height: 34px; border-radius: 6px; display: grid; place-items: center; flex: none; }
  .icon-btn svg { width: 18px; height: 18px; fill: none; stroke: #fff; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; }
  .edit { background: var(--blue); margin-left: 8px; }
  .del { background: var(--red); margin-left: 12px; }
  .icon-btn:hover { filter: brightness(.9); }
  .empty { text-align: center; color: var(--muted); padding: 30px 10px; font-size: 17px; }

  /* Pie */
  footer {
    grid-column: 1 / -1; border-top: 1px solid #e3eaf7; margin: 28px -36px 0; padding: 22px 36px;
    display: flex; align-items: center; gap: 16px; color: var(--muted); font-size: 16px;
  }
  footer .mini { width: 34px; height: 26px; border: 3px solid var(--navy); border-radius: 3px; }
  footer strong { color: var(--navy); }
  footer .lema { margin-left: auto; font-family: "Segoe Script", "Brush Script MT", cursive; font-style: italic; color: var(--navy); transform: rotate(-3deg); }

  @media (max-width: 1200px) { main { grid-template-columns: 1fr; } }
  @media (max-width: 800px) {
    body { grid-template-columns: 1fr; grid-template-rows: auto auto 1fr; grid-template-areas: "top" "side" "main"; }
    .top { padding: 16px; } .brand h1 { font-size: 28px; } .brand p { font-size: 14px; } .logo { width: 56px; height: 50px; }
    .side { padding: 8px; } .side nav { flex-direction: row; overflow-x: auto; } .side a { white-space: nowrap; padding: 10px 14px; font-size: 16px; } .tip { display: none; }
    main { padding: 24px 16px 0; } .calc, .explain { grid-template-columns: 1fr; } footer { margin: 24px -16px 0; padding: 18px 16px; flex-wrap: wrap; }
  }
</style>
</head>
<body>

<header class="top">
  <div class="brand">
    <div class="logo"><span></span></div>
    <div>
      <h1>Recta<b>Plus</b></h1>
      <p>Áreas más fáciles, pasos más simples</p>
    </div>
  </div>
  <div class="account">
    <div class="avatar"><svg viewBox="0 0 24 24"><circle cx="12" cy="8" r="4.5"/><path d="M3.5 21c0-5 4-7.5 8.5-7.5s8.5 2.500 8.500 7.500z"/></svg></div>
    Mi cuenta ⌄
  </div>
</header>

<aside class="side">
  <nav>
    <a href="#inicio" class="active"><svg viewBox="0 0 24 24" style="fill:#fff;stroke:#fff"><path d="M3 11.500 12 4l9 7.500V21h-6v-6H9v6H3z"/></svg>Inicio</a>
    <a href="#calculadora"><svg viewBox="0 0 24 24"><rect x="5" y="3" width="14" height="18" rx="2"/><path d="M8 7h8M8 12h.01M12 12h.01M16 12h.01M8 16h.01M12 16h.01M16 16h.01"/></svg>Calcular Área</a>
    <a href="#tareas"><svg viewBox="0 0 24 24"><path d="m3 6 1.500 1.500L7 5M3 12l1.500 1.500L7 11M3 18l1.500 1.500L7 17M11 6h10M11 12h10M11 18h10"/></svg>Mis Tareas</a>
    <a href="#config"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3.500"/><path d="M19.400 15a1.700 1.700 0 0 0 .3 1.800l.1.100a2 2 0 1 1-2.800 2.800l-.1-.1a1.700 1.700 0 0 0-1.800-.3 1.700 1.700 0 0 0-1 1.500V21a2 2 0 1 1-4 0v-.1a1.700 1.700 0 0 0-1.100-1.500 1.700 1.700 0 0 0-1.800.3l-.1.1a2 2 0 1 1-2.800-2.800l.1-.1a1.700 1.700 0 0 0 .3-1.800 1.700 1.700 0 0 0-1.500-1H3a2 2 0 1 1 0-4h.1a1.700 1.700 0 0 0 1.500-1.100 1.700 1.700 0 0 0-.3-1.800l-.1-.1a2 2 0 1 1 2.800-2.800l.1.1a1.700 1.700 0 0 0 1.800.3H9a1.700 1.700 0 0 0 1-1.500V3a2 2 0 1 1 4 0v.1a1.700 1.700 0 0 0 1 1.500 1.700 1.700 0 0 0 1.800-.3l.1-.1a2 2 0 1 1 2.800 2.800l-.1.1a1.700 1.700 0 0 0-.3 1.800V9a1.700 1.700 0 0 0 1.500 1H21a2 2 0 1 1 0 4h-.1a1.700 1.700 0 0 0-1.500 1z"/></svg>Configuración</a>
  </nav>
  <div class="tip">
    <svg viewBox="0 0 24 24"><path d="M9 18h6M10 21h4M12 3a6 6 0 0 0-3.500 10.900c.6.500 1 1.200 1 2V16h5v-.1c0-.8.400-1.500 1-2A6 6 0 0 0 12 3z"/></svg>
    <div>La práctica también construye resultados<i></i></div>
  </div>
</aside>

<main id="inicio">
  <section class="left" id="calculadora">
    <h2>Calcula el área de un rectángulo</h2>
    <p>Ingresa la base y la altura del rectángulo para obtener su área.</p>

    <div class="card calc">
      <div>
        <label for="base">Base (b)</label>
        <div class="field"><input id="base" type="number" min="0" step="any" value="8" inputmode="decimal"><span>cm</span></div>
        <label for="altura" style="margin-top:22px">Altura (h)</label>
        <div class="field"><input id="altura" type="number" min="0" step="any" value="5" inputmode="decimal"><span>cm</span></div>
        <button class="btn-calc" id="btnCalc" type="button">
          <svg viewBox="0 0 24 24"><rect x="5" y="3" width="14" height="18" rx="2"/><path d="M8 7h8M8 12h.01M12 12h.01M16 12h.01M8 16h.01M12 16h.01M16 16h.01"/></svg>
          Calcular Área
        </button>
        <div class="error" id="error" role="alert"></div>
      </div>
      <div class="result" aria-live="polite">
        <h3>Resultado</h3>
        <div class="math"><i>Área</i> = <i>b</i> × <i>h</i></div>
        <div class="math" id="paso"><i>Área</i> = 8 × 5</div>
        <div class="math final" id="final"><i>Área</i> = 40 cm²</div>
      </div>
    </div>

    <div class="card explain">
      <div class="diagram">
        <h4>Rectángulo</h4>
        <svg viewBox="0 0 290 200" width="100%" role="img" aria-label="Rectángulo con base b y altura h">
          <rect x="20" y="10" width="215" height="122" fill="#a9c9fb" stroke="#0f2a78" stroke-width="3"/>
          <path d="M252 10v122M246 10h12M246 132h12" stroke="#0f1f4a" stroke-width="1.500" fill="none"/>
          <text x="262" y="76" font-size="16" fill="#0f1f4a">h</text>
          <text x="252" y="100" font-size="13" fill="#0f1f4a" text-anchor="start" transform="translate(-2,0)">(altura)</text>
          <path d="M20 152h215M20 146v12M235 146v12" stroke="#0f1f4a" stroke-width="1.500" fill="none"/>
          <text x="127" y="178" font-size="16" fill="#0f1f4a" text-anchor="middle"><tspan font-style="italic">b</tspan> (base)</text>
        </svg>
      </div>
      <div>
        <h4 class="q">¿Cómo se calcula?</h4>
        <p>El área de un rectángulo se obtiene multiplicando la base por la altura.</p>
        <div class="formula math"><i>A</i> = <i>b</i> × <i>h</i></div>
        <div class="legend">
          <div><i>A</i> = área</div>
          <div><i>b</i> = base</div>
          <div><i>h</i> = altura</div>
        </div>
      </div>
    </div>
  </section>

  <section class="card tasks" id="tareas">
    <header>
      <h3>
        <svg viewBox="0 0 24 24"><rect x="5" y="4" width="14" height="17" rx="2"/><path d="M9 4V3h6v1M8.500 10h7M8.500 14h7M8.500 18h4"/></svg>
        Lista de Tareas
      </h3>
      <button class="btn-new" id="btnNew" type="button"><b>+</b> Nueva Tarea</button>
    </header>
    <ul id="list"></ul>
  </section>

  <footer>
    <div class="mini"></div>
    <strong>RectaPlus</strong> <span>|</span> <span>Tu aliado en matemáticas</span>
    <span class="lema">¡Pequeños cálculos, grandes logros!</span>
  </footer>
</main>

<script>
  /* ---------- Calculadora ---------- */
  const $ = (id) => document.getElementById(id);
  const fmt = (n) => Number.isInteger(n) ? String(n) : String(+n.toFixed(4)).replace('.', ',');

  function calcular() {
    const b = parseFloat($('base').value);
    const h = parseFloat($('altura').value);
    if (!(b >= 0) || !(h >= 0) || isNaN(b) || isNaN(h)) {
      $('error').textContent = 'Escribe números válidos (0 o mayores) en la base y la altura.';
      return;
    }
    $('error').textContent = '';
    $('paso').innerHTML = '<i>Área</i> = ' + fmt(b) + ' × ' + fmt(h);
    $('final').innerHTML = '<i>Área</i> = ' + fmt(b * h) + ' cm²';
  }
  $('btnCalc').addEventListener('click', calcular);
  ['base', 'altura'].forEach((id) =>
    $(id).addEventListener('keydown', (e) => { if (e.key === 'Enter') calcular(); })
  );

  /* ---------- Lista de tareas ---------- */
  const meses = ['ene','feb','mar','abr','may','jun','jul','ago','sep','oct','nov','dic'];
  const hoy = () => { const d = new Date(); return d.getDate() + ' ' + meses[d.getMonth()] + ' ' + d.getFullYear(); };

  let tareas = [
    { id: 1, texto: 'Calcular el área de un rectángulo (base 7, altura 4)', fecha: '15 oct 2026', hecha: true },
    { id: 2, texto: 'Ejercicio 2 (base 12, altura 6)', fecha: '16 oct 2026', hecha: false },
    { id: 3, texto: 'Tarea de geometría', fecha: '17 oct 2026', hecha: false },
    { id: 4, texto: 'Calcular área (base 9, altura 3)', fecha: '18 oct 2026', hecha: false },
    { id: 5, texto: 'Repasar fórmulas', fecha: '20 oct 2026', hecha: false }
  ];
  let siguienteId = 6;

  try {
    const guardado = JSON.parse(localStorage.getItem('rectaplus.tareas'));
    if (Array.isArray(guardado)) {
      tareas = guardado;
      siguienteId = tareas.reduce((m, t) => Math.max(m, t.id), 0) + 1;
    }
  } catch (e) { /* sin almacenamiento: se usan las tareas de ejemplo */ }

  const guardar = () => { try { localStorage.setItem('rectaplus.tareas', JSON.stringify(tareas)); } catch (e) {} };
  const esc = (s) => s.replace(/[&<>"']/g, (c) => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));

  const iconoCal = '<svg viewBox="0 0 24 24"><rect x="3.500" y="5" width="17" height="15" rx="2"/><path d="M3.500 10h17M8 3v4M16 3v4"/></svg>';
  const iconoEditar = '<svg viewBox="0 0 24 24"><path d="M4 20h4L19 9l-4-4L4 16zM13.500 6.500l4 4"/></svg>';
  const iconoBorrar = '<svg viewBox="0 0 24 24"><path d="M4 7h16M10 11v6M14 11v6M6 7l1 13h10l1-13M9 7V4h6v3"/></svg>';

  function dibujar() {
    const ul = $('list');
    if (!tareas.length) { ul.innerHTML = '<li class="empty">No tienes tareas. Pulsa “Nueva Tarea” para crear la primera.</li>'; return; }
    ul.innerHTML = tareas.map((t) => `
      <li class="task ${t.hecha ? 'done' : ''}" data-id="${t.id}">
        <input type="checkbox" ${t.hecha ? 'checked' : ''} aria-label="Marcar como completada">
        <div class="info">
          <div class="name">${esc(t.texto)}</div>
          <div class="date">${iconoCal}${esc(t.fecha)}</div>
        </div>
        <button class="icon-btn edit" data-accion="editar" aria-label="Editar tarea">${iconoEditar}</button>
        <button class="icon-btn del" data-accion="borrar" aria-label="Eliminar tarea">${iconoBorrar}</button>
      </li>`).join('');
  }

  $('list').addEventListener('click', (e) => {
    const li = e.target.closest('.task'); if (!li) return;
    const t = tareas.find((x) => x.id === +li.dataset.id);
    const btn = e.target.closest('button');
    if (e.target.matches('input[type=checkbox]')) { t.hecha = e.target.checked; }
    else if (btn && btn.dataset.accion === 'editar') {
      const nuevo = prompt('Editar tarea:', t.texto);
      if (nuevo && nuevo.trim()) t.texto = nuevo.trim(); else return;
    } else if (btn && btn.dataset.accion === 'borrar') {
      if (!confirm('¿Eliminar esta tarea?')) return;
      tareas = tareas.filter((x) => x.id !== t.id);
    } else return;
    guardar(); dibujar();
  });

  $('btnNew').addEventListener('click', () => {
    const texto = prompt('Escribe la nueva tarea:');
    if (!texto || !texto.trim()) return;
    tareas.push({ id: siguienteId++, texto: texto.trim(), fecha: hoy(), hecha: false });
    guardar(); dibujar();
  });

  dibujar();
</script>
</body>
</html>
