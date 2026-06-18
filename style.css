// ─── CONFIG ───────────────────────────────────────────────────
const GAMES = {
  simpsons: {
    title: 'The Simpsons Arcade',
    icon: '🍩',
    type: 'mame',
    rom: 'roms/mame/simpsons.zip',
    width: 800, height: 620
  },
  mk: {
    title: 'Mortal Kombat',
    icon: '⚔️',
    type: 'mame',
    rom: 'roms/mame/mk.zip',
    width: 800, height: 620
  },
  mkla2: {
    title: 'Mortal Kombat (LA)',
    icon: '⚔️',
    type: 'mame',
    rom: 'roms/mame/mkla2.zip',
    width: 800, height: 620
  },
  bublbobl: {
    title: 'Bubble Bobble',
    icon: '🫧',
    type: 'mame',
    rom: 'roms/mame/bublbobl.zip',
    width: 800, height: 580
  },
  wboy: {
    title: 'Wonder Boy',
    icon: '🧙',
    type: 'mame',
    rom: 'roms/mame/wboy.zip',
    width: 800, height: 580
  },
  dbz2: {
    title: 'Dragon Ball Z 2',
    icon: '🐉',
    type: 'mame',
    rom: 'roms/mame/dbz2.zip',
    width: 800, height: 620
  },
  mvscur1: {
    title: 'Marvel vs Capcom',
    icon: '🦸',
    type: 'mame',
    rom: 'roms/mame/mvscur1.zip',
    width: 800, height: 620
  },
  xmcotahr1: {
    title: 'X-Men: Children of the Atom',
    icon: '🧬',
    type: 'mame',
    rom: 'roms/mame/xmcotahr1.zip',
    width: 800, height: 620
  },
  xmvsfu1d: {
    title: 'X-Men vs Street Fighter',
    icon: '👊',
    type: 'mame',
    rom: 'roms/mame/xmvsfu1d.zip',
    width: 800, height: 620
  },
  flash1: {
    title: 'Flash Game',
    icon: '⚡',
    type: 'flash',
    rom: 'roms/flash/game.swf',
    width: 800, height: 600,
    desc: 'Un juego Flash clásico de los 2000s.',
    category: 'Acción',
    controls: 'Mouse / Teclado',
    stars: 4,
    preview: ''   // ruta a imagen de preview, ej: 'roms/flash/previews/game.jpg'
  }
};

const FOLDERS = {
  mame: {
    title: 'MAME',
    icon: '📁',
    type: 'mame',
    romPath: 'roms/mame/',
    indexJson: 'roms/mame/index.json'
  },
  flash: {
    title: 'Flash Games',
    icon: '⚡',
    type: 'flash',
    romPath: 'roms/flash/',
    indexJson: 'roms/flash/index.json'
  }
};

const PATHS = {
  emulatorjs: 'emulatorjs/',
  ruffle: 'ruffle/'
};

// ─── WEB APPS ─────────────────────────────────────────────────
const WEBAPPS = {
  paint: {
    title: 'Paint',
    icon: '🎨',
    url: 'https://jspaint.app',
    width: 900, height: 650
  },
  minesweeper: {
    title: 'Buscaminas',
    icon: '💣',
    url: 'https://minesweeper.online',
    width: 600, height: 520
  },
  cs: {
    title: 'Counter-Strike 1.6',
    icon: '🔫',
    url: 'https://dos.zone/mp/?lobby=cs16',
    width: 1024, height: 700
  }
};

function openWebApp(appId) {
  const app = WEBAPPS[appId];
  if (!app) return;
  if (windows[appId]) { restoreWindow(appId); focusWindow(appId); return; }

  const win = document.createElement('div');
  win.className = 'window active';
  win.id = 'win-' + appId;
  win.style.width = app.width + 'px';
  win.style.height = (app.height + 56) + 'px';
  win.style.left = (Math.random() * 80 + 40) + 'px';
  win.style.top = (Math.random() * 60 + 20) + 'px';

  win.innerHTML = `
    <div class="window-titlebar" onmousedown="startDrag(event, '${appId}')">
      <span class="window-title-icon">${app.icon}</span>
      <span class="window-title-text">${app.title}</span>
      <div class="window-controls">
        <button class="win-btn btn-min" onclick="minimizeWindow('${appId}')">─</button>
        <button class="win-btn btn-max" onclick="maximizeWindow('${appId}')">□</button>
        <button class="win-btn btn-close" onclick="closeWindow('${appId}')">✕</button>
      </div>
    </div>
    <div class="window-menubar">
      <span class="menu-item">Archivo</span>
      <span class="menu-item">Ver</span>
      <span class="menu-item">Ayuda</span>
    </div>
    <div class="window-content">
      <iframe src="${app.url}" style="width:100%;height:100%;border:none;" allowfullscreen></iframe>
    </div>
    <div class="resize-handle" onmousedown="startResize(event, '${appId}')"></div>
  `;

  win.addEventListener('mousedown', () => focusWindow(appId));
  document.body.appendChild(win);
  windows[appId] = win;
  addTaskbarItem(appId, app);
  focusWindow(appId);
}

// ─── WINDOW MANAGER ───────────────────────────────────────────
let windowZ = 200;
let windows = {};
let activeWindow = null;

function openGame(gameId) {
  if (windows[gameId]) { restoreWindow(gameId); focusWindow(gameId); return; }
  const game = GAMES[gameId];
  if (!game) return;
  const win = createWindow(gameId, game);
  document.body.appendChild(win);
  windows[gameId] = win;
  addTaskbarItem(gameId, game);
  focusWindow(gameId);
  setTimeout(() => loadEmulator(gameId, game), 100);
}

function createWindow(id, game) {
  const win = document.createElement('div');
  win.className = 'window active';
  win.id = 'win-' + id;
  const isFlash = game.type === 'flash';
  win.style.width = game.width + 'px';
  win.style.height = (game.height + (isFlash ? 86 : 56)) + 'px';
  win.style.left = (Math.random() * 100 + 50) + 'px';
  win.style.top = (Math.random() * 80 + 30) + 'px';

  const toolbar = isFlash ? `
    <div class="ie-toolbar">
      <div class="ie-nav-btns">
        <button class="ie-btn">◀</button>
        <button class="ie-btn">▶</button>
        <button class="ie-btn">✕</button>
        <button class="ie-btn">↻</button>
        <button class="ie-btn">🏠</button>
      </div>
      <div class="ie-address-bar">
        <span class="ie-address-label">Dirección</span>
        <div class="ie-address-input">🌐 http://www.atempo-juegos.com</div>
        <button class="ie-go-btn">Ir</button>
      </div>
    </div>
    <div class="ie-menubar">
      <span class="menu-item">Archivo</span>
      <span class="menu-item">Edición</span>
      <span class="menu-item">Ver</span>
      <span class="menu-item">Favoritos</span>
      <span class="menu-item">Herramientas</span>
      <span class="menu-item">Ayuda</span>
    </div>` : `
    <div class="window-menubar">
      <span class="menu-item">Archivo</span>
      <span class="menu-item">Ver</span>
      <span class="menu-item">Ayuda</span>
    </div>`;

  win.innerHTML = `
    <div class="window-titlebar" onmousedown="startDrag(event, '${id}')">
      <span class="window-title-icon">${isFlash ? '🌐' : game.icon}</span>
      <span class="window-title-text">${isFlash ? 'atempo-juegos.com - Microsoft Internet Explorer' : game.title}</span>
      <div class="window-controls">
        <button class="win-btn btn-min" onclick="minimizeWindow('${id}')">─</button>
        <button class="win-btn btn-max" onclick="maximizeWindow('${id}')">□</button>
        <button class="win-btn btn-close" onclick="closeWindow('${id}')">✕</button>
      </div>
    </div>
    ${toolbar}
    <div class="window-content" id="content-${id}">
      <div class="emu-loading">
        <span class="spinner">⚙️</span>
        Cargando ${game.title}...
      </div>
    </div>
    ${isFlash ? '<div class="ie-statusbar"><span>🔒 Internet</span></div>' : ''}
    <div class="resize-handle" onmousedown="startResize(event, '${id}')"></div>
  `;
  win.addEventListener('mousedown', () => focusWindow(id));
  return win;
}

// ─── EMULATOR LOADER ──────────────────────────────────────────
function loadEmulator(gameId, game) {
  const content = document.getElementById('content-' + gameId);
  if (game.type === 'flash') {
    loadRuffle(content, game);
  } else {
    loadEmulatorJS(content, game);
  }
}

function showFlashPreview(container, game, gameId) {
  const stars = '★'.repeat(game.stars || 4) + '☆'.repeat(5 - (game.stars || 4));
  container.innerHTML = `
    <div class="flash-preview">
      <div class="flash-preview-left">
        <div class="flash-preview-img">
          ${game.preview
            ? `<img src="${game.preview}" alt="${game.title}" style="width:100%;height:100%;object-fit:cover;border-radius:2px">`
            : `<div class="flash-preview-noimg">${game.icon}<br><small>Sin preview</small></div>`}
        </div>
        <div class="flash-rating">${stars}</div>
        <div class="flash-category">${game.category || 'Acción'}</div>
      </div>
      <div class="flash-preview-right">
        <h2 class="flash-title">${game.title}</h2>
        <p class="flash-desc">${game.desc || 'Juego Flash clásico de los 2000s.'}</p>
        <div class="flash-info">
          <span>🎮 ${game.controls || 'Mouse / Teclado'}</span>
        </div>
        <button class="flash-play-btn" onclick="startFlash('${gameId}')">
          ▶ JUGAR AHORA
        </button>
      </div>
    </div>
  `;
}

// Guarda temporal de juegos flash abiertos desde carpeta
const FLASH_TEMP = {};

function startFlash(gameId) {
  console.log('startFlash llamado con:', gameId);
  console.log('FLASH_TEMP:', JSON.stringify(Object.keys(FLASH_TEMP)));
  const game = GAMES[gameId] || FLASH_TEMP[gameId];
  console.log('game encontrado:', game);
  const content = document.getElementById('content-' + gameId);
  console.log('content element:', content);
  if (!game || !content) { 
    console.error('game o content no encontrado');
    if (content) content.innerHTML = '<div class="emu-error">❌ No se encontró el juego</div>'; 
    return; 
  }
  content.innerHTML = '<div class="emu-loading"><span class="spinner">⚙️</span> Cargando...</div>';
  loadRuffle(content, game);
}

function loadEmulatorJS(container, game) {
  const iframe = document.createElement('iframe');
  iframe.style.width = '100%';
  iframe.style.height = '100%';
  iframe.style.border = 'none';
  iframe.style.background = '#000';

  const coreMap = {
    mame: 'arcade',
    n64: 'n64',
    snes: 'snes',
    nes: 'nes',
    genesis: 'segaMD',
    flash: 'flash'
  };
  const core = coreMap[game.type] || game.type;

  const html = `<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta http-equiv="Content-Security-Policy" content="default-src * 'unsafe-inline' 'unsafe-eval' data: blob:;">
<style>* {margin:0;padding:0;} body {background:#000;overflow:hidden;} #game {width:100vw;height:100vh;}</style>
</head>
<body>
<div id="game"></div>
<script>
  EJS_player = '#game';
  EJS_core = '${core}';
  EJS_gameUrl = '${window.location.href.replace(/\/[^\/]*$/, '')}/${game.rom}';
  EJS_pathtodata = '${window.location.href.replace(/\/[^\/]*$/, '')}/${PATHS.emulatorjs}data/';
  EJS_startOnLoaded = true;
  EJS_color = '#316AC5';
  EJS_backgroundColor = '#000000';
  EJS_Buttons = { playPause:true, restart:true, mute:true, settings:true, fullscreen:true, saveState:true, loadState:true, screenRecord:false, gamepad:true, cheat:false };
<\/script>
<script src="${window.location.href.replace(/\/[^\/]*$/, '')}/${PATHS.emulatorjs}data/loader.js"><\/script>
</body>
</html>`;

  container.innerHTML = '';
  iframe.srcdoc = html;
  container.appendChild(iframe);
}

function loadRuffle(container, game) {
  function startPlayer() {
    const ruffle = window.RufflePlayer.newest();
    const player = ruffle.createPlayer();
    player.style.width = '100%';
    player.style.height = '100%';
    player.style.display = 'block';
    player.style.position = 'absolute';
    player.style.top = '0';
    player.style.left = '0';
    container.style.position = 'relative';
    container.innerHTML = '';
    container.appendChild(player);
    player.load(game.rom);
  }

  // Si Ruffle ya está cargado, usarlo directamente
  if (window.RufflePlayer) {
    startPlayer();
    return;
  }

  const script = document.createElement('script');
  script.src = PATHS.ruffle + 'ruffle.js';
  script.onload = startPlayer;
  script.onerror = () => {
    container.innerHTML = `<div class="emu-error">❌ No se encontró ruffle.js en /ruffle/</div>`;
  };
  document.head.appendChild(script);
}

// ─── FOLDERS ──────────────────────────────────────────────────
function openFolder(folderId) {
  const folder = FOLDERS[folderId];
  if (!folder) return;
  const winId = 'folder-' + folderId;
  if (windows[winId]) { restoreWindow(winId); focusWindow(winId); return; }

  const win = document.createElement('div');
  win.className = 'window active';
  win.id = 'win-' + winId;

  const isFlash = folderId === 'flash';

  if (isFlash) {
    win.style.width = '900px';
    win.style.height = '620px';
  } else {
    win.style.width = '560px';
    win.style.height = '420px';
  }
  win.style.left = '60px';
  win.style.top = '40px';

  const titlebarContent = isFlash ? `
    <div class="ie-toolbar">
      <div class="ie-nav-btns">
        <button class="ie-btn">◀</button>
        <button class="ie-btn">▶</button>
        <button class="ie-btn">✕</button>
        <button class="ie-btn">↻</button>
        <button class="ie-btn">🏠</button>
      </div>
      <div class="ie-address-bar">
        <span class="ie-address-label">Dirección</span>
        <div class="ie-address-input">🌐 http://www.atempo-juegos.com/flash</div>
        <button class="ie-go-btn">Ir</button>
      </div>
    </div>
    <div class="ie-menubar">
      <span class="menu-item">Archivo</span>
      <span class="menu-item">Edición</span>
      <span class="menu-item">Ver</span>
      <span class="menu-item">Favoritos</span>
      <span class="menu-item">Herramientas</span>
      <span class="menu-item">Ayuda</span>
    </div>` : `
    <div class="window-menubar">
      <span class="menu-item">Archivo</span>
      <span class="menu-item">Edición</span>
      <span class="menu-item">Ver</span>
    </div>`;

  win.innerHTML = `
    <div class="window-titlebar" onmousedown="startDrag(event, '${winId}')">
      <span class="window-title-icon">${isFlash ? '🌐' : '📁'}</span>
      <span class="window-title-text">${isFlash ? 'atempo-juegos.com - Microsoft Internet Explorer' : folder.title}</span>
      <div class="window-controls">
        <button class="win-btn btn-min" onclick="minimizeWindow('${winId}')">─</button>
        <button class="win-btn btn-max" onclick="maximizeWindow('${winId}')">□</button>
        <button class="win-btn btn-close" onclick="closeWindow('${winId}')">✕</button>
      </div>
    </div>
    ${titlebarContent}
    <div id="folder-content-${winId}" class="${isFlash ? 'juegos-grid-container' : ''}" style="${isFlash ? '' : 'background:#fff;flex:1;padding:12px;display:flex;flex-wrap:wrap;gap:8px;align-content:flex-start;overflow-y:auto;border-radius:0 0 3px 3px'}">
      <div style="color:#888;font-size:11px;padding:20px">Cargando...</div>
    </div>
    ${isFlash ? '<div class="ie-statusbar"><span>🔒 Internet</span></div>' : ''}
    <div id="folder-status-${winId}" style="background:#ece9d8;border-top:1px solid #aca899;padding:3px 8px;font-size:10px;color:#444;${isFlash ? 'display:none' : ''}">
      ...
    </div>
    <div class="resize-handle" onmousedown="startResize(event, '${winId}')"></div>
  `;

  win.addEventListener('mousedown', () => focusWindow(winId));
  document.body.appendChild(win);
  windows[winId] = win;
  addTaskbarItem(winId, { icon: folder.icon, title: folder.title });
  focusWindow(winId);

  // Cargar ROMs desde index.json
  fetch(folder.indexJson)
    .then(r => r.json())
    .then(roms => {
      const contentEl = document.getElementById('folder-content-' + winId);
      const statusEl = document.getElementById('folder-status-' + winId);
      const isFlash = folder.type === 'flash';
      if (isFlash) {
        // Juegos.com style grid
        const header = `<div class="juegos-header">
          <div class="juegos-logo">⚡ atempo-juegos.com</div>
          <div class="juegos-nav">
            <span class="juegos-nav-item">Inicio</span>
            <span class="juegos-nav-item">Juegos nuevos</span>
            <span class="juegos-nav-item">Populares</span>
          </div>
        </div>
        <div class="juegos-sidebar">
          <div class="juegos-section-title">CATEGORÍAS</div>
          <div class="juegos-cat-item">⚡ Acción</div>
          <div class="juegos-cat-item">🎮 Aventura</div>
          <div class="juegos-cat-item">🧩 Puzzle</div>
          <div class="juegos-cat-item">🏎️ Carreras</div>
          <div class="juegos-cat-item">👗 Vestir</div>
          <div class="juegos-cat-item">🍕 Cocina</div>
        </div>
        <div class="juegos-main">
          <div class="juegos-section-title">JUEGOS FLASH</div>
          <div class="juegos-grid">`;
        
        const cards = roms.map(filename => {
          const basename = filename.split('/').pop();
          const name = basename.replace('.zip','').replace('.swf','').replace(/_/g,' ');
          const gid = Object.keys(GAMES).find(k => GAMES[k].rom && (GAMES[k].rom.endsWith(filename) || GAMES[k].rom.endsWith(basename)));
          const label = gid ? GAMES[gid].title : name;
          const icon = gid ? GAMES[gid].icon : '⚡';
          const preview = gid && GAMES[gid].preview ? `<img src="${GAMES[gid].preview}" style="width:100%;height:100%;object-fit:cover">` : `<div style="font-size:40px;display:flex;align-items:center;justify-content:center;height:100%;background:#1a1a2e">${icon}</div>`;
          return `<div class="juegos-card" onclick="openRom('${filename}','${folder.type}','${folder.romPath}')">
            <div class="juegos-thumb">${preview}</div>
            <div class="juegos-card-name">${label}</div>
          </div>`;
        }).join('');

        contentEl.innerHTML = header + cards + `</div></div>`;
      } else {
        const icons = roms.map(filename => {
          const basename = filename.split('/').pop();
          const name = basename.replace('.zip','').replace('.swf','').replace(/_/g,' ');
          const gid = Object.keys(GAMES).find(k => GAMES[k].rom && GAMES[k].rom.endsWith(filename));
          const label = gid ? GAMES[gid].title : name;
          const icon = gid ? GAMES[gid].icon : '🕹️';
          const c = iconColor(folder.type || 'mame');
          return `<div class="icon" ondblclick="openRom('${filename}','${folder.type || 'mame'}','${folder.romPath}')" onclick="selectIcon(this)" style="width:80px">
            <div class="icon-img" style="--ic1:${c.c1};--ic2:${c.c2};width:48px;height:48px;font-size:28px">${icon}</div>
            <div class="icon-label" style="color:#000;text-shadow:none;font-size:9px">${label}</div>
          </div>`;
        }).join('');
        contentEl.innerHTML = icons;
        statusEl.textContent = roms.length + ' objeto(s)';
      }
    })
    .catch(() => {
      document.getElementById('folder-content-' + winId).innerHTML =
        '<div style="color:red;font-size:11px;padding:20px">❌ No se encontró index.json</div>';
    });
}

function openRom(filename, type, romPath) {
  // ID seguro sin puntos ni caracteres especiales
  const id = filename.replace(/[^a-zA-Z0-9]/g, '_').replace(/_+/g, '_');
  if (windows[id]) { restoreWindow(id); focusWindow(id); return; }

  // Buscar si ya está configurado en GAMES
  const gid = Object.keys(GAMES).find(k => GAMES[k].rom && GAMES[k].rom.endsWith(filename));
  const game = gid ? GAMES[gid] : {
    title: filename.replace('.zip','').replace('.swf','').replace(/_/g,' '),
    icon: type === 'flash' ? '⚡' : '🕹️',
    type: type,
    rom: romPath + filename,
    width: 800, height: 620
  };

  // Guardar en FLASH_TEMP si es flash y no está en GAMES
  if (!gid && type === 'flash') FLASH_TEMP[id] = game;

  const win = createWindow(id, game);
  document.body.appendChild(win);
  windows[id] = win;
  addTaskbarItem(id, game);
  focusWindow(id);
  setTimeout(() => loadEmulator(id, game), 100);
}

function iconColor(type) {
  const map = {
    mame:  { c1: '#1a1a1a', c2: '#8B0000' },
    flash: { c1: '#e63946', c2: '#c1121f' }
  };
  return map[type] || { c1: '#444', c2: '#222' };
}

// ─── DRAG & RESIZE ────────────────────────────────────────────
let dragging = null, dragOX = 0, dragOY = 0;
let resizing = null, resizeOX = 0, resizeOY = 0, resizeW = 0, resizeH = 0;

function startDrag(e, id) {
  if (e.target.classList.contains('win-btn')) return;
  const win = document.getElementById('win-' + id);
  dragging = win;
  dragOX = e.clientX - win.offsetLeft;
  dragOY = e.clientY - win.offsetTop;
  e.preventDefault();
}

function startResize(e, id) {
  const win = document.getElementById('win-' + id);
  resizing = win;
  resizeOX = e.clientX;
  resizeOY = e.clientY;
  resizeW = win.offsetWidth;
  resizeH = win.offsetHeight;
  e.preventDefault();
  e.stopPropagation();
}

document.addEventListener('mousemove', e => {
  if (dragging) {
    dragging.style.left = (e.clientX - dragOX) + 'px';
    dragging.style.top = Math.max(0, e.clientY - dragOY) + 'px';
  }
  if (resizing) {
    resizing.style.width = Math.max(400, resizeW + (e.clientX - resizeOX)) + 'px';
    resizing.style.height = Math.max(300, resizeH + (e.clientY - resizeOY)) + 'px';
  }
});

document.addEventListener('mouseup', () => { dragging = null; resizing = null; });

// ─── WINDOW ACTIONS ───────────────────────────────────────────
function focusWindow(id) {
  Object.keys(windows).forEach(k => {
    const w = windows[k];
    if (w) { w.classList.remove('active'); w.style.zIndex = 100; }
  });
  const win = windows[id];
  if (win) { win.classList.add('active'); win.style.zIndex = ++windowZ; }
  document.querySelectorAll('.taskbar-item').forEach(el => el.classList.remove('active'));
  const tb = document.getElementById('tb-' + id);
  if (tb) tb.classList.add('active');
  activeWindow = id;
}

function minimizeWindow(id) {
  const win = windows[id];
  if (win) win.classList.add('minimized');
  const tb = document.getElementById('tb-' + id);
  if (tb) tb.classList.remove('active');
}

function restoreWindow(id) {
  const win = windows[id];
  if (win) win.classList.remove('minimized');
}

let maximized = {};
function maximizeWindow(id) {
  const win = windows[id];
  if (!win) return;
  if (maximized[id]) {
    Object.assign(win.style, maximized[id]);
    delete maximized[id];
  } else {
    maximized[id] = { left: win.style.left, top: win.style.top, width: win.style.width, height: win.style.height };
    win.style.left = '0';
    win.style.top = '0';
    win.style.width = '100vw';
    win.style.height = 'calc(100vh - 30px)';
  }
}

function closeWindow(id) {
  const win = windows[id];
  if (win) { win.remove(); delete windows[id]; }
  const tb = document.getElementById('tb-' + id);
  if (tb) tb.remove();
  delete maximized[id];
}

// ─── TASKBAR ──────────────────────────────────────────────────
function addTaskbarItem(id, game) {
  const items = document.getElementById('taskbar-items');
  const item = document.createElement('div');
  item.className = 'taskbar-item active';
  item.id = 'tb-' + id;
  item.innerHTML = game.icon + ' ' + game.title;
  item.onclick = () => {
    const win = windows[id];
    if (!win) return;
    if (win.classList.contains('minimized')) { restoreWindow(id); focusWindow(id); }
    else if (activeWindow === id) { minimizeWindow(id); }
    else { focusWindow(id); }
  };
  items.appendChild(item);
}

// ─── CLOCK ────────────────────────────────────────────────────
function updateClock() {
  const now = new Date();
  const h = String(now.getHours()).padStart(2, '0');
  const m = String(now.getMinutes()).padStart(2, '0');
  document.getElementById('clock').textContent = h + ':' + m;
}
updateClock();
setInterval(updateClock, 10000);

// ─── ICON SELECT ──────────────────────────────────────────────
function selectIcon(el) {
  document.querySelectorAll('.icon').forEach(i => i.classList.remove('selected'));
  el.classList.add('selected');
}

// ─── CONTEXT MENU ─────────────────────────────────────────────
document.getElementById('desktop').addEventListener('contextmenu', e => {
  e.preventDefault();
  const menu = document.getElementById('ctx-menu');
  menu.style.display = 'block';
  menu.style.left = e.clientX + 'px';
  menu.style.top = e.clientY + 'px';
});
document.addEventListener('click', () => {
  document.getElementById('ctx-menu').style.display = 'none';
  document.querySelectorAll('.icon').forEach(i => i.classList.remove('selected'));
});
