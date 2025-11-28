<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Nexus Games — организация по созданию игр</title>
<style>
  :root{--bg:#0f1724;--card:#0b1220;--accent:#7dd3fc;--muted:#94a3b8;--glass:rgba(255,255,255,0.03)}
  html,body{height:100%;margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,'Helvetica Neue',Arial}
  body{background:linear-gradient(180deg,#071023 0%, #07132a 60%);color:#e6eef8;display:flex;align-items:center;justify-content:center;padding:24px}
  .wrap{width:100%;max-width:900px}
  header{display:flex;align-items:center;gap:16px;margin-bottom:18px}
  .logo{width:56px;height:56px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#4ade80);display:flex;align-items:center;justify-content:center;font-weight:700;color:#002;box-shadow:0 6px 18px rgba(0,0,0,.6)}
  h1{font-size:20px;margin:0}
  p.lead{margin:0;color:var(--muted);font-size:13px}
  .card{background:var(--card);border-radius:12px;padding:16px;margin-bottom:12px;box-shadow:0 6px 24px rgba(2,6,23,.6);backdrop-filter: blur(6px)}
  .grid{display:grid;grid-template-columns:1fr 320px;gap:12px}
  @media (max-width:760px){.grid{grid-template-columns:1fr}}
  .meta{font-size:13px;color:var(--muted);margin-top:8px}
  .games-list{display:flex;flex-direction:column;gap:8px;margin-top:12px}
  .game{padding:10px;border-radius:8px;background:var(--glass);display:flex;justify-content:space-between;align-items:center}
  .game h3{margin:0;font-size:15px}
  .game small{display:block;color:var(--muted);font-size:12px;margin-top:4px}
  .btn{background:transparent;border:1px solid rgba(255,255,255,0.07);padding:8px 10px;border-radius:8px;cursor:pointer;color:inherit;font-weight:600}
  .btn.primary{background:linear-gradient(90deg,var(--accent),#a78bfa);color:#022;padding:8px 12px;border:none}
  .controls{display:flex;gap:8px;align-items:center}
  .edit-mode{border:1px dashed rgba(255,255,255,0.06);padding:8px;border-radius:8px}
  label{font-size:13px;color:var(--muted)}
  input[type="text"],textarea{width:100%;padding:8px;border-radius:8px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit;margin-top:6px}
  textarea{min-height:80px;resize:vertical}
  footer{color:var(--muted);font-size:13px;margin-top:8px;text-align:center}
  .small{font-size:12px;color:var(--muted)}
  .game-actions{display:flex;gap:6px}
  .danger{background:transparent;border:1px solid rgba(255,60,60,0.15);color:#ff9fa0}
</style>
</head>
<body>
<main class="wrap" role="main">
  <header>
    <div class="logo" aria-hidden>NG</div>
    <div>
      <h1 id="orgName">Nexus Games</h1>
      <p class="lead" id="orgTag">Команда разработчиков инди-игр — от простых аркад до учебных симуляторов.</p>
      <div class="meta small" id="orgMeta">Контакт: hello@nexus.example · г. Запорожье</div>
    </div>
  </header>

  <div class="grid">
    <section class="card" aria-labelledby="aboutTitle">
      <h2 id="aboutTitle">О нас</h2>
      <p id="aboutText">Мы создаём небольшие, но увлекательные игры — обучающие проекты, аркады и симуляции. Наша цель — дать людям возможность учиться и развлекаться одновременно.</p>

      <div style="margin-top:12px;display:flex;gap:12px;align-items:center">
        <div>
          <strong>Доступные игры</strong>
          <div class="games-list" id="gamesList"></div>
        </div>
      </div>
    </section>

    <aside class="card" aria-labelledby="adminTitle">
      <h2 id="adminTitle">Управление</h2>

      <div id="authBox" class="small">
        <button class="btn" id="loginBtn">Войти (локально)</button>
        <span class="small" style="margin-left:8px;color:var(--muted)">Пароль клиент-стор: <code>admin</code> (не безопасно)</span>
      </div>

      <div id="editor" style="display:none;margin-top:12px">
        <div class="edit-mode">
          <label>Название организации</label>
          <input id="inpName" type="text" />
          <label style="margin-top:8px">Короткое описание</label>
          <input id="inpTag" type="text" />
          <label style="margin-top:8px">Контакт / место</label>
          <input id="inpMeta" type="text" />
          <label style="margin-top:8px">Блок "О нас"</label>
          <textarea id="inpAbout"></textarea>
        </div>

        <details style="margin-top:10px">
          <summary style="cursor:pointer">Добавить новую игру</summary>
          <div style="margin-top:8px">
            <label>Название игры</label>
            <input id="newGameName" type="text" placeholder="Candy Jump" />
            <label>Короткое описание</label>
            <input id="newGameDesc" type="text" placeholder="Аркада на реакцию" />
            <label>Ссылка (опционально)</label>
            <input id="newGameLink" type="text" placeholder="https://example.com/play/candy" />
            <div style="margin-top:8px;display:flex;gap:8px">
              <button class="btn primary" id="addGameBtn">Добавить игру</button>
              <button class="btn danger" id="clearBtn">Сбросить всё</button>
            </div>
          </div>
        </details>

        <div style="margin-top:10px">
          <button class="btn primary" id="saveBtn">Сохранить изменения</button>
          <button class="btn" id="logoutBtn">Выйти</button>
        </div>
        <p class="small" style="margin-top:8px">Изменения сохраняются в вашем браузере (localStorage). Чтобы редактировать с другого устройства — загрузите файл и распишите содержимое вручную или используйте GitHub Pages (см. инструкции ниже).</p>
      </div>
    </aside>
  </div>

  <footer>
    <div class="small">Подсказка: чтобы быстро править содержимое в коде — открой <code>index.html</code> в любом редакторе и правь данные в блоке <code>initialData</code> (внизу файла).</div>
  </footer>
</main>

<script>
/* --- Простейшее хранилище данных --- 
   Можно править initialData в файле или использовать встроенный редактор.
*/
const initialData = {
  orgName: "Nexus Games",
  orgTag: "Команда разработчиков инди-игр — от простых аркад до учебных симуляторов.",
  orgMeta: "Контакт: hello@nexus.example · г. Запорожье",
  about: "Мы создаём небольшие, но увлекательные игры — обучающие проекты, аркады и симуляции. Наша цель — дать людям возможность учиться и развлекаться одновременно.",
  games: [
    { name: "Pixel Runner", desc: "Беговая аркада с изучением физмеханики", link: "" },
    { name: "Math Quest", desc: "Обучающая игра по математике для 5-7 классов", link: "" }
  ]
};

function loadData(){
  try{
    const saved = localStorage.getItem('siteData_v1');
    return saved ? JSON.parse(saved) : initialData;
  } catch(e){ return initialData; }
}

function saveData(d){
  localStorage.setItem('siteData_v1', JSON.stringify(d));
}

/* --- UI rendering --- */
const data = loadData();
const el = id => document.getElementById(id);

function render(){
  el('orgName').textContent = data.orgName;
  el('orgTag').textContent = data.orgTag;
  el('orgMeta').textContent = data.orgMeta;
  el('aboutText').textContent = data.about;

  const list = el('gamesList');
  list.innerHTML = '';
  if(!data.games || data.games.length===0){ list.innerHTML = '<div class="small" style="color:var(--muted)">Игры пока не добавлены.</div>'; return; }
  data.games.forEach((g, i) => {
    const item = document.createElement('div'); item.className='game';
    const left = document.createElement('div');
    const h = document.createElement('h3'); h.textContent = g.name;
    const sm = document.createElement('small'); sm.textContent = g.desc;
    left.appendChild(h); left.appendChild(sm);
    const actions = document.createElement('div'); actions.className='game-actions';
    if(g.link){
      const a = document.createElement('a'); a.href = g.link; a.textContent = 'Играть'; a.className='btn'; a.target='_blank'; actions.appendChild(a);
    }
    const edit = document.createElement('button'); edit.textContent='✎'; edit.className='btn'; edit.title='Редактировать'; edit.onclick = ()=> openEditGame(i);
    const del = document.createElement('button'); del.textContent='🗑'; del.className='btn danger'; del.title='Удалить'; del.onclick = ()=> { if(confirm('Удалить игру?')){ data.games.splice(i,1); saveData(data); render(); } };
    actions.appendChild(edit); actions.appendChild(del);

    item.appendChild(left);
    item.appendChild(actions);
    list.appendChild(item);
  });
}

/* --- Простая форма редактирования игры (модально простым prompt) --- */
function openEditGame(index){
  const g = data.games[index];
  const newName = prompt('Название игры:', g.name);
  if(newName===null) return;
  const newDesc = prompt('Короткое описание:', g.desc);
  if(newDesc===null) return;
  const newLink = prompt('Ссылка (оставьте пустой, если нет):', g.link||'');
  data.games[index] = { name: newName.trim()||g.name, desc: newDesc.trim()||g.desc, link: newLink.trim()||'' };
  saveData(data); render();
}

/* --- Авторизация (локально, клиент-стор) --- */
let logged = false;
el('loginBtn').addEventListener('click', ()=>{
  const p = prompt('Введите локальный пароль:','');
  if(p === 'admin'){ // клиент-side only
    logged = true; showEditor(true);
  } else alert('Неверный пароль.');
});

el('logoutBtn').addEventListener('click', ()=>{
  logged = false; showEditor(false);
});

function showEditor(on){
  el('editor').style.display = on ? 'block' : 'none';
  el('authBox').style.display = on ? 'none' : 'block';
  if(on){ // populate fields
    el('inpName').value = data.orgName;
    el('inpTag').value = data.orgTag;
    el('inpMeta').value = data.orgMeta;
    el('inpAbout').value = data.about;
  }
}

/* --- add / save --- */
el('addGameBtn').addEventListener('click', ()=>{
  const name = el('newGameName').value.trim();
  if(!name){ alert('Введите название игры.'); return; }
  const desc = el('newGameDesc').value.trim();
  const link = el('newGameLink').value.trim();
  data.games.push({name, desc, link});
  saveData(data); render();
  el('newGameName').value=''; el('newGameDesc').value=''; el('newGameLink').value='';
});

el('saveBtn').addEventListener('click', ()=>{
  data.orgName = el('inpName').value.trim() || data.orgName;
  data.orgTag = el('inpTag').value.trim() || data.orgTag;
  data.orgMeta = el('inpMeta').value.trim() || data.orgMeta;
  data.about = el('inpAbout').value.trim() || data.about;
  saveData(data);
  alert('Сохранено локально в этом браузере.');
  render();
});

el('clearBtn').addEventListener('click', ()=>{
  if(confirm('Сбросить все данные сайта (включая список игр) к изначальным?')) {
    localStorage.removeItem('siteData_v1');
    location.reload();
  }
});

/* initial render */
render();
</script>
</body>
</html>
