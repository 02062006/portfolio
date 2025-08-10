<html lang="fr">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Portfolio — Mon site photo</title>
<style>
  :root{
    --bg:#0b0b0c; --panel:#0f1720; --muted:#9aa4b2; --accent:#e0a400;
    --card:#11131a; --glass: rgba(255,255,255,0.03);
  }
  *{box-sizing:border-box}
  html,body{height:100%}
  body{
    margin:0; font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    background:linear-gradient(180deg,var(--bg) 0%, #071017 100%); color:#fff;
    -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;
  }

  /* HEADER */
  header{display:flex;align-items:center;justify-content:space-between;padding:18px 22px;border-bottom:1px solid rgba(255,255,255,0.03);backdrop-filter: blur(4px)}
  .brand{display:flex;gap:14px;align-items:center}
  .logo{width:44px;height:44px;border-radius:8px;background:linear-gradient(135deg,var(--accent), #ffb86b);display:flex;align-items:center;justify-content:center;font-weight:700;color:#08121a}
  h1{font-size:18px;margin:0}
  nav a{color:var(--muted);text-decoration:none;margin-left:16px;font-size:14px}
  nav a:hover{color:#fff}

  /* HERO */
  .hero{padding:40px 22px 18px; text-align:center}
  .hero h2{margin:0;font-size:28px; letter-spacing:-0.4px}
  .hero p{color:var(--muted);margin-top:8px}

  /* TOOLS */
  .tools{display:flex;gap:12px;flex-wrap:wrap;justify-content:center;padding:16px 22px}
  .categories{display:flex;gap:8px;flex-wrap:wrap;justify-content:center}
  .cat-btn{
    background:var(--glass);border:1px solid rgba(255,255,255,0.04);color:var(--muted);
    padding:8px 12px;border-radius:8px;font-size:14px;cursor:pointer;
  }
  .cat-btn.active{background:linear-gradient(90deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01)); color:#fff; box-shadow:0 6px 18px rgba(0,0,0,0.5)}
  .uploader{display:flex;gap:8px;align-items:center}
  select, input[type="file"]{background:transparent;color:var(--muted);border:1px dashed rgba(255,255,255,0.04);padding:8px;border-radius:8px}
  .primary{background:linear-gradient(90deg,var(--accent), #ffb86b); color:#07121a;border:none;padding:9px 14px;border-radius:8px;cursor:pointer;font-weight:600}

  /* GALLERY GRID */
  .gallery{padding:18px;display:grid;grid-template-columns:repeat(3,1fr);gap:14px;max-width:1200px;margin:0 auto}
  .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:12px;overflow:hidden;position:relative}
  .card img{width:100%;height:220px;object-fit:cover;display:block;transition:transform .35s ease}
  .card:hover img{transform:scale(1.03)}
  .tag{position:absolute;left:10px;bottom:10px;background:rgba(0,0,0,0.45);backdrop-filter: blur(4px);padding:6px 10px;border-radius:999px;font-size:13px;color:var(--muted)}
  .caption{padding:10px 12px;color:var(--muted);font-size:13px}

  /* LIGHTBOX */
  .lightbox{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(2,6,10,0.8);z-index:60;padding:20px}
  .lightbox.open{display:flex}
  .lightbox img{max-width:95%;max-height:85%;border-radius:10px;box-shadow:0 20px 60px rgba(0,0,0,0.6)}
  .lb-close{position:absolute;top:18px;right:18px;background:rgba(255,255,255,0.04);border-radius:8px;padding:8px;color:var(--muted);cursor:pointer}

  /* RESPONSIVE */
  @media (max-width:1000px){ .gallery{grid-template-columns:repeat(2,1fr)} .card img{height:200px} }
  @media (max-width:640px){ header{padding:12px} .hero{padding:24px 12px} .gallery{grid-template-columns:repeat(1,1fr)} .card img{height:260px} .tools{padding:10px 12px} }

  /* small footer */
  footer{padding:22px;text-align:center;color:var(--muted);font-size:13px}
</style>
</head>
<body>

<header>
  <div class="brand">
    <div class="logo">PH</div>
    <div>
      <h1>Arthur — Photographie</h1>
      <div style="font-size:12px;color:var(--muted)">Portfolio — style sombre</div>
    </div>
  </div>
  <nav>
    <a href="#galerie">Galerie</a>
    <a href="#contact">Contact</a>
  </nav>
</header>

<section class="hero">
  <h2>Bienvenue dans mon portfolio</h2>
  <p>Site sombre, responsive — ajoute tes photos en un clic, filtre par catégorie et montre-les en grand.</p>
</section>

<section class="tools" aria-hidden="false">
  <div class="categories" role="tablist" aria-label="Catégories">
    <!-- boutons ajoutés par JS -->
  </div>

  <div style="width:14px"></div>

  <div class="uploader" aria-hidden="false">
    <select id="categorySelect" title="Choisis une catégorie">
      <!-- options ajoutées par JS -->
    </select>
    <input id="fileInput" type="file" accept="image/*" multiple />
    <button id="addBtn" class="primary">Ajouter</button>
  </div>
</section>

<main id="galerie">
  <div class="gallery" id="galleryGrid" aria-live="polite">
    <!-- cartes ajoutées par JS -->
  </div>
</main>

<!-- LIGHTBOX -->
<div id="lightbox" class="lightbox" role="dialog" aria-modal="true">
  <button class="lb-close" id="lbClose" aria-label="Fermer">✕</button>
  <img id="lbImg" src="" alt="Agrandissement photo" />
</div>

<section id="contact" style="padding:28px 22px">
  <div style="max-width:720px;margin:0 auto;background:var(--card);padding:18px;border-radius:12px">
    <h3 style="margin-top:0">Contact</h3>
    <p style="color:var(--muted)">Tu peux mettre ici ton email, Instagram ou autre. Le formulaire ci-dessous ouvre ton client mail.</p>
    <form id="contactForm" onsubmit="sendMail(event)">
      <input id="nameField" placeholder="Ton nom" style="width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:#fff;margin-bottom:10px" required>
      <input id="emailField" type="email" placeholder="Ton email" style="width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:#fff;margin-bottom:10px" required>
      <textarea id="msgField" placeholder="Ton message" style="width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:#fff;margin-bottom:10px" rows="4" required></textarea>
      <div style="display:flex;gap:8px">
        <button class="primary" type="submit">Envoyer</button>
        <a href="mailto:ton.email@exemple.com" style="align-self:center;color:var(--muted)">Ou utilise ton client mail</a>
      </div>
    </form>
  </div>
</section>

<footer>
  © <span id="year"></span> Arthur — Portfolio • Construit avec ❤️
</footer>

<script>
/* ====== CONFIG : catégories initiales et images (modifie ici si tu veux) ====== */
const CATEGORIES = [
  { id: 'all', label: 'Tout' },
  { id: 'voyage', label: 'Voyage' },
  { id: 'voiture', label: 'Voiture' },
  { id: 'portrait', label: 'Portrait' }
];

/* Exemple d'images par défaut (pour voir le rendu).
   Remplace ces src par "images/voyage/..." si tu as des images locales dans le même dossier que index.html.
*/
const INITIAL_PHOTOS = [
  { src: 'data:image/svg+xml;utf8,' + encodeURIComponent(sampleSVG('#3498db','Voyage 1')), caption:'Voyage 1', category:'voyage' },
  { src: 'data:image/svg+xml;utf8,' + encodeURIComponent(sampleSVG('#2980b9','Voyage 2')), caption:'Voyage 2', category:'voyage' },
  { src: 'data:image/svg+xml;utf8,' + encodeURIComponent(sampleSVG('#e74c3c','Voiture 1')), caption:'Voiture 1', category:'voiture' },
  { src: 'data:image/svg+xml;utf8,' + encodeURIComponent(sampleSVG('#c0392b','Voiture 2')), caption:'Voiture 2', category:'voiture' },
  { src: 'data:image/svg+xml;utf8,' + encodeURIComponent(sampleSVG('#2ecc71','Portrait 1')), caption:'Portrait 1', category:'portrait' },
  { src: 'data:image/svg+xml;utf8,' + encodeURIComponent(sampleSVG('#27ae60','Portrait 2')), caption:'Portrait 2', category:'portrait' },
];

function sampleSVG(color, text){
  const escaped = text.replace(/&/g,'&amp;').replace(/"/g,'&quot;');
  return `<svg xmlns='http://www.w3.org/2000/svg' width='1200' height='800'>
    <rect width='100%' height='100%' fill='${color}' />
    <g font-family='Arial' font-size='96' fill='white' text-anchor='middle'>
      <text x='50%' y='50%'>${escaped}</text>
    </g>
  </svg>`;
}

/* ====== UI initialisation ====== */
const categoriesEl = document.querySelector('.categories');
const galleryGrid = document.getElementById('galleryGrid');
const categorySelect = document.getElementById('categorySelect');
const fileInput = document.getElementById('fileInput');
const addBtn = document.getElementById('addBtn');
const yearEl = document.getElementById('year');

yearEl.textContent = new Date().getFullYear();

/* Crée boutons et select */
CATEGORIES.forEach((c,i)=>{
  const btn = document.createElement('button');
  btn.className = 'cat-btn' + (c.id==='all' ? ' active':'' );
  btn.textContent = c.label;
  btn.dataset.cat = c.id;
  btn.addEventListener('click',()=>{ setActiveCategory(c.id); });
  categoriesEl.appendChild(btn);

  // select ignore 'all'
  if(c.id!=='all'){
    const opt = document.createElement('option');
    opt.value = c.id; opt.textContent = c.label;
    categorySelect.appendChild(opt);
  }
});

/* données en mémoire (client-side) */
let photos = [...INITIAL_PHOTOS];

/* Render galerie */
function renderGallery(filter='all'){
  galleryGrid.innerHTML = '';
  const list = photos.filter(p => filter === 'all' ? true : p.category === filter);
  if(list.length===0){
    galleryGrid.innerHTML = `<div style="grid-column:1/-1;color:var(--muted);text-align:center;padding:28px;background:transparent;border-radius:8px">Aucune photo dans cette catégorie.</div>`;
    return;
  }
  list.forEach((p, idx)=>{
    const card = document.createElement('figure');
    card.className = 'card';
    card.innerHTML = `
      <img loading="lazy" src="${p.src}" data-idx="${idx}" alt="${escapeHtml(p.caption)}" />
      <figcaption class="caption">${escapeHtml(p.caption)}</figcaption>
      <div class="tag">${escapeHtml(capitalize(p.category))}</div>
    `;
    // click -> open lightbox
    card.querySelector('img').addEventListener('click', (ev) => openLightbox(ev.currentTarget.src, p.caption));
    galleryGrid.appendChild(card);
  });
}

/* Active category visuel + render */
function setActiveCategory(cat){
  document.querySelectorAll('.cat-btn').forEach(b=>{
    b.classList.toggle('active', b.dataset.cat === cat);
  });
  renderGallery(cat);
}

/* Ajouter images depuis le file input */
addBtn.addEventListener('click', ()=>{
  const files = Array.from(fileInput.files);
  if(files.length===0){ alert('Choisis au moins une image.'); return; }
  const cat = categorySelect.value || 'voyage';
  files.forEach(f=>{
    // createObjectURL pour affichage immédiat
    const url = URL.createObjectURL(f);
    photos.unshift({ src: url, caption: f.name, category: cat, isObjectURL:true });
  });
  // effacer input
  fileInput.value = '';
  // montrer catégorie
  setActiveCategory(cat);
});

/* LIGHTBOX */
const lightbox = document.getElementById('lightbox');
const lbImg = document.getElementById('lbImg');
const lbClose = document.getElementById('lbClose');
function openLightbox(src, caption){
  lbImg.src = src;
  lbImg.alt = caption || 'Photo';
  lightbox.classList.add('open');
  document.body.style.overflow = 'hidden';
}
function closeLightbox(){
  lightbox.classList.remove('open');
  lbImg.src = '';
  document.body.style.overflow = '';
}
lbClose.addEventListener('click', closeLightbox);
lightbox.addEventListener('click', (e)=>{
  if(e.target === lightbox) closeLightbox();
});
document.addEventListener('keydown',(e)=>{ if(e.key === 'Escape') closeLightbox(); });

/* Contact form -> ouvre mailto avec sujet */
function sendMail(e){
  e.preventDefault();
  const name = document.getElementById('nameField').value.trim();
  const email = document.getElementById('emailField').value.trim();
  const msg = document.getElementById('msgField').value.trim();
  const mail = 'ton.email@exemple.com'; // modifie ici vers ton email
  const subject = encodeURIComponent(`Contact portfolio — ${name}`);
  const body = encodeURIComponent(`Nom: ${name}\nEmail: ${email}\n\n${msg}`);
  window.location.href = `mailto:${mail}?subject=${subject}&body=${body}`;
}

/* Helpers */
function capitalize(s){ return s && (s[0].toUpperCase()+s.slice(1)); }
function escapeHtml(s){ return String(s).replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;'); }

/* initial render */
renderGallery('all');

/* small note: if you add objectURL images and later want to free memory, you can call URL.revokeObjectURL(url) when removed. */
</script>
</body>
</html>
