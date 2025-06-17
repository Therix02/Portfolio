<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Asier Angulo | Portfolio</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <header>Asier Angulo</header>

  <div id="icon-container"></div>

  <div id="modal" class="modal">
    <div class="modal-content">
      <span id="modal-close" class="modal-close">&times;</span>
      <img id="modal-img" src="" alt="Trabajo completo" />
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>
:root {
  --bg-color: #2E2E2E;
  --text-color: #111111;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html, body {
  height: 100%;
  font-family: Arial, Helvetica, sans-serif;
  background: var(--bg-color);
  overflow: hidden;
}

header {
  position: fixed;
  top: 1rem;
  left: 1rem;
  font-family: "Arial Black", Arial, sans-serif;
  font-size: 1.8rem;
  letter-spacing: 0.5px;
  color: var(--text-color);
  user-select: none;
  z-index: 1000;
}

#icon-container {
  position: relative;
  width: 100vw;
  height: 100vh;
}

.icon {
  width: 90px;
  height: 90px;
  cursor: pointer;
  position: absolute;
  object-fit: contain;
  transition: transform 0.25s ease-in-out;
  user-select: none;
  background-color: transparent;
}

.icon:hover {
  transform: scale(1.2) rotate(5deg);
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0,0,0,0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease;
  z-index: 1500;
}

.modal.open {
  opacity: 1;
  visibility: visible;
}

.modal-content {
  max-width: 85%;
  max-height: 85%;
  position: relative;
}

.modal-content img {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 6px;
}

.modal-close {
  position: absolute;
  top: -2rem;
  right: -2rem;
  font-size: 3rem;
  color: #fff;
  cursor: pointer;
}
const works = [
  {
    thumb: "https://github.com/Therix02/Portfolio/blob/main/11.png?raw=true",
    hover: "https://github.com/Therix02/Portfolio/blob/main/22.png?raw=true",
    full: "https://raw.githubusercontent.com/Therix02/Portfolio/797e69409ce70996eec520649a12e8ffc0176bcc/Mesa%20de%20trabajo%201.svg",
    alt: "Trabajo 1",
  },
  {
    thumb: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Markdown-mark.svg/120px-Markdown-mark.svg.png",
    hover: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Markdown-mark.svg/120px-Markdown-mark.svg.png",
    full: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Markdown-mark.svg/120px-Markdown-mark.svg.png",
    alt: "Trabajo 2",
  },
  {
    thumb: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/JavaScript-logo.png/120px-JavaScript-logo.png",
    hover: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/JavaScript-logo.png/120px-JavaScript-logo.png",
    full: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/JavaScript-logo.png/120px-JavaScript-logo.png",
    alt: "Trabajo 3",
  },
  {
    thumb: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/CSS3_logo_and_wordmark.svg/120px-CSS3_logo_and_wordmark.svg.png",
    hover: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/CSS3_logo_and_wordmark.svg/120px-CSS3_logo_and_wordmark.svg.png",
    full: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/CSS3_logo_and_wordmark.svg/120px-CSS3_logo_and_wordmark.svg.png",
    alt: "Trabajo 4",
  },
];

const container = document.getElementById("icon-container");

works.forEach((work, i) => {
  const img = document.createElement("img");
  img.className = "icon";
  img.src = work.thumb;
  img.dataset.thumb = work.thumb;
  img.dataset.hover = work.hover;
  img.dataset.full = work.full;
  img.alt = work.alt;

  let savedPos = localStorage.getItem(`iconPos${i}`);

  if (savedPos) {
    const pos = JSON.parse(savedPos);
    img.style.left = pos.left;
    img.style.top = pos.top;
  } else {
    const randomX = Math.random() * 80 + 10;
    const randomY = Math.random() * 80 + 10;
    img.style.left = `${randomX}vw`;
    img.style.top = `${randomY}vh`;
    localStorage.setItem(
      `iconPos${i}`,
      JSON.stringify({ left: img.style.left, top: img.style.top })
    );
  }

  img.addEventListener("mouseenter", () => {
    img.src = work.hover || work.thumb;
  });
  img.addEventListener("mouseleave", () => {
    img.src = work.thumb;
  });
  img.addEventListener("click", () => openModal(work.full, work.alt));

  container.appendChild(img);
});

const modal = document.getElementById("modal");
const modalImg = document.getElementById("modal-img");
const modalClose = document.getElementById("modal-close");

function openModal(src, alt) {
  modalImg.src = src;
  modalImg.alt = alt;
  modal.classList.add("open");
}

function closeModal() {
  modal.classList.remove("open");
  modalImg.src = "";
}

modalClose.addEventListener("click", closeModal);
modal.addEventListener("click", (e) => {
  if (e.target === modal) closeModal();
});
