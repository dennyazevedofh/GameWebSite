# 📚 Guia de Estudo - CSS do Projeto Gamics

## Introdução

Este documento foi criado para ajudar você a entender como funciona o arquivo `style.css` do projeto Gamics. Vamos explicar cada seção do código CSS de forma clara e objetiva, mostrando como ele se conecta com o HTML e JavaScript.

**Público-alvo**: Alunos do curso de Análise e Desenvolvimento de Sistemas iniciando em desenvolvimento web.

---

## 📑 Índice

1. [Propriedades Personalizadas (Custom Properties)](#1-propriedades-personalizadas-custom-properties)
2. [Reset CSS](#2-reset-css)
3. [Estilos Reutilizáveis](#3-estilos-reutilizáveis)
4. [Cabeçalho (Header)](#4-cabeçalho-header)
5. [Caixa de Busca (Search Box)](#5-caixa-de-busca-search-box)
6. [Seção Hero](#6-seção-hero)
7. [Seção Brand (Marcas)](#7-seção-brand-marcas)
8. [Seção Latest Game](#8-seção-latest-game)
9. [Seção Live Match](#9-seção-live-match)
10. [Seção Featured Game](#10-seção-featured-game)
11. [Seção Shop (Loja)](#11-seção-shop-loja)
12. [Seção Blog](#12-seção-blog)
13. [Newsletter](#13-newsletter)
14. [Footer (Rodapé)](#14-footer-rodapé)
15. [Botão Voltar ao Topo](#15-botão-voltar-ao-topo)
16. [Media Queries (Responsividade)](#16-media-queries-responsividade)

---

## 1. Propriedades Personalizadas (Custom Properties)

### O que são?

Propriedades personalizadas (também chamadas de variáveis CSS) permitem armazenar valores que você quer reutilizar em todo o documento. Elas começam com `--` e são definidas dentro de `:root`.

### Código:

```css
:root {
  /* Cores */
  --rich-black-fogra-29_95: hsla(222, 18%, 11%, 0.95);
  --marigold: hsl(42, 99%, 46%);
  --white: hsl(0, 0%, 100%);
  
  /* Tipografia */
  --ff-oxanium: 'Oxanium', cursive;
  --ff-poppins: 'Poppins', sans-serif;
  
  --fs-1: 7rem;
  --fs-2: 4.5rem;
  
  /* Espaçamento */
  --section-padding: 120px;
  
  /* Transições */
  --transition: 0.25s ease;
}
```

### Explicação:

- **`:root`**: Representa o elemento raiz do documento (HTML). Variáveis definidas aqui ficam disponíveis em todo o site.
- **Cores**: Usa `hsl()` e `hsla()` para definir cores. O último número em `hsla()` é a opacidade (0 a 1).
- **Tipografia**: 
  - `--ff-` (font-family): Define as fontes do projeto
  - `--fs-` (font-size): Define os tamanhos de fonte em `rem` (unidade relativa)
  - `--fw-` (font-weight): Define o peso da fonte (negrito, normal, etc)

### Como usar:

```css
.titulo {
  color: var(--marigold); /* Usa a cor amarela definida */
  font-family: var(--ff-oxanium); /* Usa a fonte Oxanium */
  font-size: var(--fs-1); /* Usa o tamanho 7rem */
}
```

### Por que isso é útil?

Imagine que você precise mudar a cor principal do site. Em vez de procurar em centenas de linhas, você muda apenas uma vez em `:root`!

---

## 2. Reset CSS

### O que é?

Navegadores aplicam estilos padrão diferentes aos elementos HTML. O Reset CSS "reseta" esses estilos para que todos os navegadores comecem do mesmo ponto.

### Código:

```css
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

li { list-style: none; }

a {
  text-decoration: none;
  color: inherit;
}
```

### Explicação:

- **`*`**: Seleciona TODOS os elementos da página
- **`*::before` e `*::after`**: Seleciona pseudo-elementos (conteúdo gerado via CSS)
- **`margin: 0; padding: 0;`**: Remove espaçamentos padrão de todos os elementos
- **`box-sizing: border-box;`**: Faz com que `padding` e `border` sejam incluídos na largura/altura total do elemento
- **`li { list-style: none; }`**: Remove os marcadores (bolinhas) das listas
- **`a { text-decoration: none; }`**: Remove o sublinhado dos links

### Exemplo prático:

**Sem reset:**
```html
<h1>Título</h1>
<p>Parágrafo</p>
```
O navegador adiciona margens automáticas entre o h1 e p.

**Com reset:**
Não há margens automáticas, você controla tudo!

---

## 3. Estilos Reutilizáveis

### 3.1. Container

```css
.container { 
  padding-inline: 15px; 
}
```

**Onde é usado no HTML:**
```html
<div class="container">
  <!-- Conteúdo aqui -->
</div>
```

**Explicação:**
- `padding-inline`: Adiciona espaçamento nas laterais (esquerda e direita)
- Usado em quase todas as seções para garantir que o conteúdo não grude nas bordas da tela

---

### 3.2. Títulos (h1, h2, h3)

```css
.h1,
.h2,
.h3 {
  color: var(--white);
  font-family: var(--ff-oxanium);
  font-weight: var(--fw-800);
  line-height: 1;
}

.h1 {
  font-size: var(--fs-2);
  letter-spacing: -3px;
}
```

**Onde é usado no HTML:**
```html
<h1 class="h1 hero-title">
  Crie e <span class="span">Gerencie</span> Partidas
</h1>
```

**Explicação:**
- Define estilos para títulos
- `line-height: 1`: Altura da linha igual ao tamanho da fonte (sem espaço extra)
- `letter-spacing: -3px`: Aproxima as letras (espaçamento negativo)
- `.span`: Destaca palavras em amarelo (`--marigold`)

---

### 3.3. Botões com Efeito "Skew"

```css
.btn {
  margin-inline: auto;
  color: var(--eerie-black-1);
  font-size: var(--fs-8);
  text-transform: uppercase;
  font-weight: var(--fw-700);
  min-height: 55px;
  padding-inline: 35px;
}

.skewBg {
  position: relative;
  z-index: 1;
}

.skewBg::before {
  content: "";
  position: absolute;
  inset: 0;
  transform: skewX(var(--skewX, -16deg));
  background-color: var(--bg, var(--marigold));
  z-index: -1;
}
```

**Onde é usado no HTML:**
```html
<button class="btn skewBg">
  Leia Mais
</button>
```

**Explicação:**
- **`position: relative`**: Cria um contexto de posicionamento para o pseudo-elemento
- **`::before`**: Cria um elemento "fantasma" ANTES do conteúdo do botão
- **`inset: 0`**: Atalho para `top: 0; right: 0; bottom: 0; left: 0;` (preenche todo o espaço)
- **`transform: skewX(-16deg)`**: Inclina o fundo horizontalmente
- **`z-index: -1`**: Coloca o fundo atrás do texto

**Resultado visual:**
```
┌──────────────┐
│  LEIA MAIS   │  ← Texto reto
└──────────────┘
  ╲          ╱    ← Fundo inclinado
```

---

### 3.4. Scrollbar Horizontal Personalizada

```css
.has-scrollbar {
  display: flex;
  gap: 30px;
  overflow-x: auto;
  padding-block-end: 30px;
  scroll-snap-type: inline mandatory;
}

.has-scrollbar::-webkit-scrollbar { 
  height: 10px; 
}

.has-scrollbar::-webkit-scrollbar-track { 
  outline: 3px solid var(--marigold); 
}

.has-scrollbar::-webkit-scrollbar-thumb { 
  background-color: var(--marigold); 
}
```

**Onde é usado no HTML:**
```html
<ul class="has-scrollbar">
  <li class="scrollbar-item">Item 1</li>
  <li class="scrollbar-item">Item 2</li>
  <li class="scrollbar-item">Item 3</li>
</ul>
```

**Explicação:**
- **`display: flex`**: Coloca itens lado a lado
- **`overflow-x: auto`**: Adiciona rolagem horizontal se necessário
- **`scroll-snap-type: inline mandatory`**: Faz os itens "encaixarem" ao rolar
- **`::-webkit-scrollbar`**: Estiliza a barra de rolagem (funciona no Chrome/Safari)
- **`::-webkit-scrollbar-thumb`**: A parte que você arrasta

**Resultado**: Uma galeria horizontal com rolagem suave e personalizada.

---

## 4. Cabeçalho (Header)

### 4.1. Estrutura do Header

```css
.header-bottom {
  position: absolute;
  top: calc(100% - 1px);
  left: 0;
  width: 100%;
  background-color: var(--raisin-black-2);
  padding-block: 20px;
  z-index: 4;
}

.header-bottom.active {
  position: fixed;
  top: -85px;
  animation: slideIn 0.5s var(--cubic-out) forwards;
}

@keyframes slideIn {
  0% { transform: translateY(0); }
  100% { transform: translateY(100%); }
}
```

**Conexão com JavaScript** (`script.js`):

```javascript
const header = document.querySelector("[data-header]");

window.addEventListener("scroll", function () {
  if (window.scrollY >= 200) {
    header.classList.add("active");
  } else {
    header.classList.remove("active");
  }
});
```

**Explicação:**

1. **Estado inicial**: Header fica posicionado normalmente no topo
2. **Quando você rola 200px**: JavaScript adiciona a classe `.active`
3. **Com `.active`**: 
   - `position: fixed` → Header fica fixo na tela
   - `top: -85px` → Header sobe para fora da tela
   - `animation: slideIn` → Header desce suavemente de volta

**Resultado**: Header que "gruda" no topo ao rolar a página!

---

### 4.2. Menu de Navegação Mobile

```css
.navbar {
  background-color: var(--eerie-black-1);
  color: var(--white);
  position: absolute;
  top: 100%;
  right: 0;
  width: 100%;
  max-width: 350px;
  visibility: hidden;
  max-height: 0;
  transition: 0.25s var(--cubic-out);
  overflow: hidden;
}

.navbar.active {
  visibility: visible;
  max-height: 275px;
  transition-duration: 0.5s;
}
```

**Conexão com JavaScript**:

```javascript
const navbar = document.querySelector("[data-navbar]");
const navbarToggler = document.querySelector("[data-nav-toggler]");

navbarToggler.addEventListener("click", function () {
  navbar.classList.toggle("active");
  this.classList.toggle("active");
});
```

**Explicação:**

1. **Estado inicial**: Menu oculto (`visibility: hidden`, `max-height: 0`)
2. **Ao clicar no botão**: JavaScript adiciona/remove `.active`
3. **Com `.active`**: Menu aparece expandindo de 0 para 275px de altura

**HTML correspondente**:
```html
<button class="nav-toggle-btn" data-nav-toggler>
  <ion-icon name="menu-outline" class="menu"></ion-icon>
  <ion-icon name="close-outline" class="close"></ion-icon>
</button>

<nav class="navbar" data-navbar>
  <ul class="navbar-list">
    <li class="navbar-item">
      <a href="#home" class="navbar-link">Início</a>
    </li>
    <!-- Mais itens... -->
  </ul>
</nav>
```

---

### 4.3. Botão de Alternância de Ícones

```css
.nav-toggle-btn.active .menu,
.nav-toggle-btn .close { 
  display: none; 
}

.nav-toggle-btn .menu,
.nav-toggle-btn.active .close { 
  display: block; 
}
```

**Explicação:**

- **Sem `.active`**: Mostra ícone de menu (☰), esconde ícone de fechar (✕)
- **Com `.active`**: Mostra ícone de fechar (✕), esconde ícone de menu (☰)

**Lógica visual**:
```
Menu fechado: [☰] ← Mostra "menu"
Menu aberto:  [✕] ← Mostra "close"
```

---

## 5. Caixa de Busca (Search Box)

### Código:

```css
.search-container {
  background-color: var(--rich-black-fogra-29_95);
  position: fixed;
  inset: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-inline: 40px;
  z-index: 6;
  visibility: hidden;
  opacity: 0;
  transition: var(--transition);
}

.search-container.active {
  visibility: visible;
  opacity: 1;
}
```

**Conexão com JavaScript**:

```javascript
const searchTogglers = document.querySelectorAll("[data-search-toggler]");
const searchBox = document.querySelector("[data-search-box]");

for (let i = 0; i < searchTogglers.length; i++) {
  searchTogglers[i].addEventListener("click", function () {
    searchBox.classList.toggle("active");
  });
}
```

**Explicação:**

1. **`position: fixed; inset: 0;`**: Ocupa toda a tela
2. **`display: flex; justify-content: center; align-items: center;`**: Centraliza o conteúdo
3. **`visibility: hidden; opacity: 0;`**: Esconde completamente
4. **`.active`**: Torna visível com transição suave

**HTML correspondente**:
```html
<!-- Botão que abre a busca -->
<button class="search-btn" data-search-toggler>
  <ion-icon name="search-outline"></ion-icon>
</button>

<!-- Overlay de busca -->
<div class="search-container" data-search-box>
  <div class="input-wrapper">
    <input type="search" class="search-field" placeholder="Busque aqui...">
    <button class="search-submit" data-search-toggler>
      <ion-icon name="search-outline"></ion-icon>
    </button>
  </div>
</div>
```

**Resultado**: Ao clicar no ícone de busca, uma tela preta semitransparente cobre tudo, mostrando um campo de busca centralizado.

---

## 6. Seção Hero

### Código:

```css
.hero {
  --section-padding: 60px;
  margin-block-start: 84px;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  text-align: center;
  min-height: 100vh;
  display: grid;
  align-items: center;
}
```

**Onde é usado no HTML**:
```html
<section 
  class="section hero" 
  id="home" 
  style="background-image: url('./assets/images/hero-bg.jpg')"
>
  <div class="container">
    <div class="hero-content">
      <p class="hero-subtitle">Mundo dos Games</p>
      <h1 class="h1 hero-title">
        Crie e <span class="span">Gerencie</span> Partidas
      </h1>
      <p class="hero-text">
        Encontre tecnologia ou pessoas...
      </p>
      <button class="btn skewBg">Leia Mais</button>
    </div>
    <figure class="hero-banner">
      <img src="./assets/images/hero-banner.png" alt="Banner principal">
    </figure>
  </div>
</section>
```

**Explicação:**

- **`min-height: 100vh;`**: Altura mínima de 100% da viewport (tela visível)
- **`display: grid; align-items: center;`**: Centraliza o conteúdo verticalmente
- **`background-size: cover;`**: Imagem de fundo cobre toda a área
- **`margin-block-start: 84px;`**: Espaço no topo para não ficar atrás do header

**Resultado**: Uma seção de destaque que ocupa a tela inteira com imagem de fundo.

---

## 7. Seção Brand (Marcas)

### Código:

```css
.brand {
  --section-padding: 60px;
  background-image: var(--gradient);
}

.brand .has-scrollbar { 
  padding-block-end: 0; 
}

.brand .has-scrollbar::-webkit-scrollbar { 
  display: none; 
}

.brand-item {
  min-width: calc(50% - 10px);
  scroll-snap-align: start;
}

.brand-item > img { 
  margin-inline: auto; 
}
```

**HTML correspondente**:
```html
<section class="section brand">
  <div class="container">
    <ul class="has-scrollbar">
      <li class="brand-item">
        <img src="./assets/images/brand-1.png" alt="Logo da Marca">
      </li>
      <li class="brand-item">
        <img src="./assets/images/brand-2.png" alt="Logo da Marca">
      </li>
      <!-- Mais marcas... -->
    </ul>
  </div>
</section>
```

**Explicação:**

- **`min-width: calc(50% - 10px)`**: Cada item ocupa metade da largura (menos 10px de gap)
- **`scroll-snap-align: start`**: Itens "encaixam" no início ao rolar
- **`::-webkit-scrollbar { display: none; }`**: Esconde a barra de rolagem
- **`margin-inline: auto`**: Centraliza as imagens

**Resultado**: Galeria horizontal de logos que você pode arrastar, sem barra de rolagem visível.

---

## 8. Seção Latest Game

### 8.1. Wrapper com Background

```css
.section-wrapper {
  position: relative;
  background-color: var(--white);
  z-index: 1;
}

.section-wrapper::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 57%;
  background-image: url("../images/section-wrapper-bg.png");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  z-index: -1;
}
```

**Explicação:**

- **`::before`**: Cria uma imagem de fundo decorativa
- **`height: 57%`**: Cobre apenas parte da seção
- **`z-index: -1`**: Fica atrás do conteúdo

---

### 8.2. Cards de Jogos

```css
.latest-game-card {
  position: relative;
  box-shadow: var(--shadow-2);
}

.latest-game-card .card-content {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: var(--xiketic_90);
  padding: 35px 25px;
}

.latest-game-card .card-badge {
  position: absolute;
  bottom: 100%;
  left: 25px;
}
```

**HTML correspondente**:
```html
<div class="latest-game-card">
  <figure class="card-banner">
    <img src="./assets/images/latest-game-1.jpg" alt="White Walker Daily">
  </figure>
  <div class="card-content">
    <a href="#" class="card-badge skewBg">Zumbi</a>
    <h3 class="h3">
      <a href="#" class="card-title">
        White Walker <span class="span">Daily</span>
      </a>
    </h3>
    <p class="card-price">
      Taxa de Inscrição: <span class="span">Grátis</span>
    </p>
  </div>
</div>
```

**Explicação:**

- **`position: absolute; bottom: 0;`**: Conteúdo fica fixo na parte inferior da imagem
- **`bottom: 100%;`**: Badge fica logo acima do card-content
- **Layout em camadas**:
  ```
  ┌─────────────────┐
  │                 │
  │   [IMAGEM]      │
  │                 │
  │  [BADGE]        │ ← bottom: 100% do card-content
  ├─────────────────┤
  │ Título          │ ← card-content
  │ Preço           │
  └─────────────────┘
  ```

---

## 9. Seção Live Match

### 9.1. Banner com Botão de Play

```css
.live-match-banner {
  position: relative;
  background-color: var(--light-gray-1);
  border-radius: 6px;
  overflow: hidden;
  box-shadow: var(--shadow-3);
}

.live-match-banner .play-btn {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: var(--marigold);
  font-size: 60px;
}
```

**Explicação:**

- **`position: absolute; top: 50%; left: 50%;`**: Posiciona no centro
- **`transform: translate(-50%, -50%);`**: Ajuste fino para centralização perfeita
  - Move o elemento 50% do seu próprio tamanho para cima e para esquerda

---

### 9.2. Texto "LIVE" em Background

```css
.live-match-player {
  position: relative;
  padding-block-start: var(--section-padding);
}

.live-match-player::after {
  content: "LIVE";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -40%);
  font-size: 15rem;
  font-weight: var(--fw-600);
  color: var(--cultured-2);
  z-index: -1;
}
```

**Explicação:**

- **`content: "LIVE"`**: Texto gerado via CSS
- **`font-size: 15rem`**: Tamanho gigante (150px)
- **`color: var(--cultured-2)`**: Cor bem clara (quase branca)
- **`z-index: -1`**: Fica atrás das imagens dos jogadores

**Resultado**: Palavra "LIVE" gigante e desbotada ao fundo, criando um efeito visual interessante.

---

## 10. Seção Featured Game

### Cards com Overlay ao Passar o Mouse

```css
.featured-game-card {
  position: relative;
}

.featured-game-card .card-content {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 30px 35px;
  transition: var(--transition);
}

.featured-game-card .card-content-overlay {
  position: absolute;
  inset: 0;
  background-color: var(--marigold_75);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transition: var(--transition);
}

.featured-game-card:is(:hover, :focus-within) .card-content {
  opacity: 0;
}

.featured-game-card:is(:hover, :focus-within) .card-content-overlay {
  opacity: 1;
}
```

**HTML correspondente**:
```html
<div class="featured-game-card">
  <figure class="card-banner">
    <img src="./assets/images/featured-game-1.jpg" alt="Jogo">
  </figure>
  
  <!-- Conteúdo normal (visível) -->
  <div class="card-content">
    <h3><a href="#">Título do Jogo</a></h3>
    <span class="card-meta">Playstation 5, Xbox</span>
  </div>
  
  <!-- Overlay (aparece no hover) -->
  <div class="card-content-overlay">
    <img src="./assets/images/featured-game-icon.png" class="card-icon">
    <h3><a href="#">Título do Jogo</a></h3>
    <span class="card-meta">Playstation 5, Xbox</span>
  </div>
</div>
```

**Explicação:**

1. **Estado normal**: `card-content` visível, `card-content-overlay` invisível (opacity: 0)
2. **Ao passar o mouse (`:hover`)**: 
   - `card-content` desaparece (opacity: 0)
   - `card-content-overlay` aparece (opacity: 1)
3. **`:focus-within`**: Também funciona quando você navega com teclado (acessibilidade!)

**Efeito visual**:
```
Normal:     Hover:
┌──────┐     ┌──────┐
│      │     │      │
│      │     │ [🎮] │ ← Ícone
├──────┤     │      │
│Título│     │Título│ ← Centralizado
│Info  │     │Info  │
└──────┘     └──────┘
```

---

## 11. Seção Shop (Loja)

### Cards de Produtos

```css
.shop-card .card-content {
  position: relative;
  padding: 25px;
  padding-block-start: 40px;
}

.shop-card .card-badge {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translate(-50%, -50%);
}

.shop-card .card-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: var(--marigold);
}

.shop-card .card-btn {
  color: inherit;
  font-size: 18px;
  padding: 7px;
  border: 1px solid var(--english-violet);
  border-radius: 4px;
  transition: var(--transition);
}

.shop-card .card-btn:is(:hover, :focus) {
  background-color: var(--marigold);
  color: var(--xiketic);
  border-color: var(--marigold);
}
```

**HTML correspondente**:
```html
<div class="shop-card">
  <figure class="card-banner">
    <img src="./assets/images/product-1.jpg" alt="Produto">
  </figure>
  <div class="card-content">
    <a href="#" class="card-badge skewBg">-20%</a>
    <h3><a href="#" class="card-title">Nome do Produto</a></h3>
    <div class="card-wrapper">
      <p class="card-price">$29.00</p>
      <button class="card-btn">
        <ion-icon name="cart-outline"></ion-icon>
      </button>
    </div>
  </div>
</div>
```

**Explicação:**

- **`transform: translate(-50%, -50%)`**: Badge fica pendurado no topo do card
- **`justify-content: space-between`**: Preço na esquerda, botão na direita
- **Hover do botão**: Inverte as cores (fundo amarelo, texto escuro)

---

## 12. Seção Blog

### Cards de Artigos

```css
.blog-list {
  display: grid;
  gap: 50px;
}

.blog-card .card-meta-list {
  display: flex;
  align-items: center;
  gap: 20px;
}

.blog-card .card-meta-item {
  display: flex;
  align-items: center;
  gap: 5px;
  color: var(--quick-silver);
  font-size: var(--fs-11);
  font-weight: var(--fw-600);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.blog-card .card-meta-item ion-icon {
  --ionicon-stroke-width: 50px;
  color: var(--marigold);
}
```

**HTML correspondente**:
```html
<div class="blog-card">
  <figure class="card-banner">
    <img src="./assets/images/blog-1.jpg" alt="Artigo">
  </figure>
  <div class="card-content">
    <ul class="card-meta-list">
      <li class="card-meta-item">
        <ion-icon name="person-outline"></ion-icon>
        <a href="#" class="item-text">Admin</a>
      </li>
      <li class="card-meta-item">
        <ion-icon name="calendar-outline"></ion-icon>
        <time class="item-text" datetime="2022-09-19">19 Set 2022</time>
      </li>
    </ul>
    <h3 class="card-title">
      <a href="#">Título do Artigo</a>
    </h3>
    <p class="card-text">Resumo do artigo...</p>
    <a href="#" class="card-link">
      Leia Mais
      <ion-icon name="arrow-forward"></ion-icon>
    </a>
  </div>
</div>
```

**Explicação:**

- **`display: grid; gap: 50px;`**: Cards empilhados verticalmente com espaço entre eles
- **Meta informações**: Autor e data ficam lado a lado com ícones
- **`--ionicon-stroke-width: 50px`**: Controla a espessura dos ícones

---

## 13. Newsletter

### Formulário de Inscrição

```css
.newsletter-card {
  background-color: var(--raisin-black-3);
  padding: 40px 15px;
  margin-block-start: -55px;
  border-radius: 80px;
}

.newsletter .input-wrapper {
  max-width: 300px;
  margin-inline: auto;
  margin-block-end: 10px;
}

.newsletter .email-field {
  font-size: var(--fs-9);
  color: var(--white);
  font-weight: var(--fw-500);
  padding: 17px 45px;
  padding-inline-end: 20px;
  outline: none;
}

.newsletter .input-wrapper ion-icon {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  left: 20px;
  color: var(--marigold);
  --ionicon-stroke-width: 50px;
}
```

**HTML correspondente**:
```html
<section class="newsletter">
  <div class="container">
    <div class="newsletter-card">
      <h2 class="h2">Nossa <span class="span">Newsletter</span></h2>
      <form class="newsletter-form">
        <div class="input-wrapper skewBg">
          <input 
            type="email" 
            placeholder="Digite seu e-mail..." 
            class="email-field"
          >
          <ion-icon name="mail-outline"></ion-icon>
        </div>
        <button type="submit" class="btn newsletter-btn skewBg">
          <span>Inscrever-se</span>
          <ion-icon name="paper-plane"></ion-icon>
        </button>
      </form>
    </div>
  </div>
</section>
```

**Explicação:**

- **`margin-block-start: -55px`**: "Puxa" o card para cima, sobrepondo a seção anterior
- **`border-radius: 80px`**: Cantos bem arredondados
- **Ícone no input**: Posicionado absolutamente à esquerda, alinhado verticalmente ao centro

---

## 14. Footer (Rodapé)

### 14.1. Estrutura em Grid

```css
.footer-top .container {
  display: grid;
  gap: 50px;
}
```

**Explicação**: No mobile, tudo fica empilhado verticalmente. Em telas maiores, usa colunas (veja Media Queries).

---

### 14.2. Listas de Links

```css
.footer-list-title {
  position: relative;
  color: var(--silver);
  font-family: var(--ff-oxanium);
  text-transform: uppercase;
  font-weight: var(--fw-800);
  padding-block-end: 20px;
  margin-block-end: 35px;
}

.footer-list-title::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 30px;
  height: 3px;
  background-color: var(--marigold);
}

.footer-link {
  font-size: var(--fs-9);
  max-width: max-content;
  transition: var(--transition);
  padding-block: 8px;
  font-weight: var(--fw-500);
}

.footer-link:is(:hover, :focus) {
  color: var(--marigold);
  transform: translateX(5px);
}
```

**HTML correspondente**:
```html
<ul class="footer-list">
  <li>
    <p class="footer-list-title">Produtos</p>
  </li>
  <li>
    <a href="#" class="footer-link">Placas Gráficas (26)</a>
  </li>
  <li>
    <a href="#" class="footer-link">Planos de Fundo (11)</a>
  </li>
  <!-- Mais links... -->
</ul>
```

**Explicação:**

- **`::after`**: Linha amarela decorativa abaixo do título
- **Hover dos links**: Muda cor para amarelo e desliza 5px para direita
  ```
  Normal:  Produtos
  Hover:   → Produtos  (amarelo e deslocado)
  ```

---

### 14.3. Botão de Newsletter no Footer

```css
.footer-newsletter {
  position: relative;
}

.footer-newsletter .email-field {
  background-color: var(--raisin-black-4);
  padding: 12px 20px;
  padding-inline-end: 60px;
  font-size: var(--fs-9);
  color: var(--white);
}

.footer-btn {
  position: absolute;
  top: 0;
  right: 0;
  height: 100%;
  width: 53px;
  background-color: var(--marigold);
  color: var(--xiketic);
  display: grid;
  place-content: center;
}
```

**Explicação:**

- **`position: relative`**: Container cria contexto para o botão absoluto
- **`position: absolute; right: 0;`**: Botão fica "grudado" na direita do input
- **`display: grid; place-content: center;`**: Centraliza o ícone perfeitamente

**Layout visual**:
```
┌────────────────────────┬────┐
│ Digite seu e-mail...   │ 🚀 │
└────────────────────────┴────┘
```

---

## 15. Botão Voltar ao Topo

### Código:

```css
.back-top-btn {
  position: fixed;
  bottom: 10px;
  right: 15px;
  background-color: var(--marigold);
  padding: 12px;
  z-index: 4;
  transition: var(--transition);
  opacity: 0;
  visibility: hidden;
}

.back-top-btn.active {
  opacity: 1;
  visibility: visible;
  transform: translateY(-10px);
}
```

**Conexão com JavaScript**:

```javascript
const backTopBtn = document.querySelector("[data-back-top-btn]");

window.addEventListener("scroll", function () {
  if (window.scrollY >= 200) {
    backTopBtn.classList.add("active");
  } else {
    backTopBtn.classList.remove("active");
  }
});
```

**HTML correspondente**:
```html
<a href="#top" class="back-top-btn" data-back-top-btn>
  <ion-icon name="caret-up"></ion-icon>
</a>
```

**Explicação:**

1. **Estado inicial**: Invisível (`opacity: 0; visibility: hidden`)
2. **Quando rola 200px**: JavaScript adiciona `.active`
3. **Com `.active`**: 
   - Fica visível
   - Sobe 10px (`translateY(-10px)`) criando efeito de "flutuação"

**Resultado**: Botão que aparece no canto inferior direito quando você rola a página, facilitando voltar ao topo.

---

## 16. Media Queries (Responsividade)

### O que são Media Queries?

Media Queries permitem aplicar estilos diferentes dependendo do tamanho da tela. Isso torna o site **responsivo** (funciona bem em celular, tablet e desktop).

---

### 16.1. Telas Maiores que 576px (Tablets Pequenos)

```css
@media (min-width: 576px) {
  .container {
    max-width: 540px;
    width: 100%;
    margin-inline: auto;
  }
  
  .h1 { --fs-2: 7rem; }
  
  .cart-btn {
    display: block;
    position: relative;
    color: var(--white);
    font-size: 20px;
  }
  
  .cart-badge {
    position: absolute;
    top: -6px;
    right: -10px;
    background-color: var(--marigold);
    color: var(--eerie-black-1);
    font-size: var(--fs-11);
    border-radius: 20px;
    padding: 3px 5px;
    line-height: 1;
    font-weight: var(--fw-800);
  }
}
```

**Explicação:**

- **`max-width: 540px; margin-inline: auto;`**: Container centralizado com largura limitada
- **Botão do carrinho aparece**: Antes estava oculto em telas muito pequenas
- **Cart badge**: Bolinha vermelha com número de itens no carrinho

**HTML do carrinho**:
```html
<button class="cart-btn">
  <ion-icon name="cart"></ion-icon>
  <span class="cart-badge">0</span>
</button>
```

---

### 16.2. Telas Maiores que 768px (Tablets)

```css
@media (min-width: 768px) {
  .container { max-width: 720px; }
  
  .scrollbar-item { 
    min-width: calc(50% - 15px); 
  }
  
  .blog-list { 
    grid-template-columns: 1fr 1fr; 
  }
  
  .newsletter-form {
    display: flex;
    gap: 10px;
    max-width: 500px;
    width: 100%;
    margin-inline: auto;
  }
}
```

**Explicação:**

- **Scrollbar items**: Antes ocupavam 100%, agora ocupam 50% (2 por vez)
- **Blog**: Muda de 1 coluna para 2 colunas
- **Newsletter**: Input e botão ficam lado a lado

**Antes e depois**:
```
Mobile (< 768px):     Tablet (>= 768px):
┌──────────┐          ┌─────┬─────┐
│ Blog 1   │          │Blog1│Blog2│
├──────────┤          ├─────┼─────┤
│ Blog 2   │          │Blog3│Blog4│
├──────────┤          └─────┴─────┘
│ Blog 3   │
└──────────┘
```

---

### 16.3. Telas Maiores que 992px (Desktops)

```css
@media (min-width: 992px) {
  .container { max-width: 960px; }
  
  .header-top {
    display: block;
    background-image: url("../images/header-top-bg.jpg");
    padding-block: 20px;
  }
  
  .countdown-text {
    color: var(--quick-silver);
    font-size: var(--fs-10);
    font-weight: var(--fw-600);
  }
  
  .nav-toggle-btn { display: none; }
  
  .navbar,
  .navbar.active {
    all: unset;
    margin-inline: auto 15px;
  }
  
  .navbar-list { display: flex; }
  
  .navbar-link {
    color: var(--white);
    font-family: var(--ff-oxanium);
    font-size: var(--fs-11);
    text-transform: uppercase;
    font-weight: var(--fw-700);
    padding: 10px 20px;
  }
}
```

**Explicação:**

- **Header-top aparece**: Mostra banner de oferta e redes sociais
- **Botão do menu desaparece**: `display: none;`
- **Menu vira horizontal**: `display: flex;` nos itens
- **`all: unset`**: Remove TODOS os estilos anteriores do menu mobile

**Transformação do menu**:
```
Mobile:           Desktop:
┌─────────┐       ┌──────────────────────────────────┐
│ [☰]     │       │ Logo  [Início] [Ao Vivo] [Blog] │
│         │       └──────────────────────────────────┘
│ Menu    │
│ ├Início │
│ ├Ao Vivo│
│ └Blog   │
└─────────┘
```

---

### 16.4. Hero em Desktop

```css
@media (min-width: 992px) {
  .hero { text-align: left; }
  
  .hero-banner { display: block; }
  
  .hero .container {
    display: grid;
    grid-template-columns: 1fr 0.9fr;
    align-items: center;
    gap: 50px;
  }
}
```

**Explicação:**

- **`text-align: left`**: Texto alinha à esquerda (antes estava centralizado)
- **Banner aparece**: Imagem que estava oculta em mobile
- **Grid de 2 colunas**: Texto à esquerda (60%), imagem à direita (40%)

**Layout visual**:
```
Mobile:                Desktop:
┌──────────┐          ┌────────────┬──────────┐
│  Título  │          │  Título    │          │
│  Texto   │          │  Texto     │  [IMG]   │
│  Botão   │          │  Botão     │          │
└──────────┘          └────────────┴──────────┘
```

---

### 16.5. Telas Maiores que 1200px (Desktops Grandes)

```css
@media (min-width: 1200px) {
  .container { max-width: 1230px; }
  
  .h1 { --fs-2: 7.5rem; }
  
  .scrollbar-item { 
    min-width: calc(25% - 22.5px); 
  }
  
  .newsletter-card {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-inline: 70px;
  }
  
  .newsletter .h2 { 
    margin-block-end: 0; 
  }
}
```

**Explicação:**

- **Títulos maiores**: `7.5rem` (120px)
- **Scrollbar items**: Agora 4 por vez (25% cada)
- **Newsletter horizontal**: Título à esquerda, formulário à direita

**Newsletter em telas grandes**:
```
┌────────────────────────────────────────┐
│  Nossa Newsletter  [Email...] [Botão]  │
└────────────────────────────────────────┘
```

---

## 🎯 Resumo de Conceitos Importantes

### 1. **Box Model**
Todo elemento HTML é uma "caixa" com:
- **Content**: Conteúdo (texto, imagem)
- **Padding**: Espaço interno
- **Border**: Borda
- **Margin**: Espaço externo

```
┌─────────────────────┐
│      MARGIN         │
│  ┌───────────────┐  │
│  │   BORDER      │  │
│  │ ┌───────────┐ │  │
│  │ │  PADDING  │ │  │
│  │ │ ┌───────┐ │ │  │
│  │ │ │CONTENT│ │ │  │
│  │ │ └───────┘ │ │  │
│  │ └───────────┘ │  │
│  └───────────────┘  │
└─────────────────────┘
```

---

### 2. **Position**

```css
/* Valores principais: */
position: static;    /* Padrão, fluxo normal */
position: relative;  /* Relativo à sua posição original */
position: absolute;  /* Relativo ao pai mais próximo com position */
position: fixed;     /* Fixo na tela, não rola */
position: sticky;    /* Gruda ao rolar até certo ponto */
```

---

### 3. **Flexbox**

Sistema de layout unidimensional (linha OU coluna):

```css
.container {
  display: flex;
  justify-content: center;  /* Alinhamento horizontal */
  align-items: center;      /* Alinhamento vertical */
  gap: 20px;                /* Espaço entre itens */
}
```

---

### 4. **Grid**

Sistema de layout bidimensional (linhas E colunas):

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;  /* 3 colunas iguais */
  gap: 30px;
}
```

---

### 5. **Pseudo-elementos**

Criam elementos "virtuais":

```css
.elemento::before { 
  content: "Antes"; 
}  /* Adiciona conteúdo ANTES */

.elemento::after { 
  content: "Depois"; 
}  /* Adiciona conteúdo DEPOIS */
```

---

### 6. **Pseudo-classes**

Estilos baseados em estado:

```css
.link:hover { }        /* Ao passar o mouse */
.input:focus { }       /* Ao focar (clicar) */
.item:first-child { }  /* Primeiro filho */
.elemento:is(:hover, :focus) { }  /* Hover OU focus */
```

---

## 🔗 Conexões CSS ↔ HTML ↔ JavaScript

### Exemplo Completo: Menu Mobile

**HTML**:
```html
<button class="nav-toggle-btn" data-nav-toggler>
  <ion-icon name="menu-outline" class="menu"></ion-icon>
</button>

<nav class="navbar" data-navbar>
  <ul class="navbar-list">
    <li><a href="#home">Início</a></li>
  </ul>
</nav>
```

**CSS**:
```css
.navbar {
  max-height: 0;
  visibility: hidden;
  transition: 0.25s;
}

.navbar.active {
  max-height: 275px;
  visibility: visible;
}
```

**JavaScript**:
```javascript
const toggler = document.querySelector("[data-nav-toggler]");
const navbar = document.querySelector("[data-navbar]");

toggler.addEventListener("click", function() {
  navbar.classList.toggle("active");
});
```

**Fluxo**:
1. Usuário clica no botão
2. JavaScript adiciona/remove classe `.active`
3. CSS detecta `.active` e anima o menu

---

## 📝 Dicas de Estudo

### 1. **Inspecione no Navegador**
- Abra o site no Chrome
- Clique com botão direito → "Inspecionar"
- Veja os estilos aplicados em tempo real
- Teste mudanças diretamente no navegador!

### 2. **Teste Responsividade**
- No DevTools, clique no ícone de celular
- Escolha diferentes tamanhos de tela
- Veja as Media Queries em ação

### 3. **Experimente**
- Mude cores nas variáveis CSS
- Altere tamanhos de fonte
- Teste diferentes valores de `gap`, `padding`, etc.
- **Quebre o código** para entender como funciona!

### 4. **Pratique Cada Conceito**
- Crie um card simples
- Adicione hover effects
- Faça um menu mobile
- Cada pequeno projeto reforça o aprendizado

---

## 🎓 Exercícios Sugeridos

### Nível Iniciante
1. Mude a cor principal (`--marigold`) para azul
2. Aumente o tamanho dos títulos
3. Adicione mais um item no menu

### Nível Intermediário
1. Crie um novo card de jogo com overlay
2. Adicione uma animação ao botão "Leia Mais"
3. Faça o header mudar de cor ao rolar

### Nível Avançado
1. Crie uma nova seção com grid de 4 colunas
2. Implemente um menu dropdown
3. Adicione modo escuro/claro com variáveis CSS

---

## 📚 Recursos Adicionais

- [MDN Web Docs](https://developer.mozilla.org/pt-BR/) - Documentação completa de CSS
- [CSS-Tricks](https://css-tricks.com/) - Tutoriais e truques
- [Flexbox Froggy](https://flexboxfroggy.com/) - Jogo para aprender Flexbox
- [Grid Garden](https://cssgridgarden.com/) - Jogo para aprender Grid

---

## ❓ Dúvidas Frequentes

**P: Por que usar `rem` em vez de `px`?**
R: `rem` é relativo ao tamanho da fonte raiz (html), facilitando acessibilidade e responsividade.

**P: Qual a diferença entre `display: none` e `visibility: hidden`?**
R: 
- `display: none` → Remove o elemento completamente (não ocupa espaço)
- `visibility: hidden` → Esconde o elemento mas mantém o espaço

**P: Quando usar Flexbox vs Grid?**
R:
- **Flexbox**: Layouts unidimensionais (menus, cards em linha)
- **Grid**: Layouts bidimensionais (galerias, páginas inteiras)

**P: Como funcionam as transições?**
R: `transition: propriedade duração tipo-de-animação;`
Exemplo: `transition: all 0.3s ease;` → Anima TODAS as propriedades em 0.3 segundos.

---

## 🎉 Conclusão

Este guia apresentou todos os conceitos do CSS do projeto Gamics. Lembre-se:

1. **Prática é essencial** - Leia o código, mas principalmente **escreva código**
2. **Erros são aprendizado** - Quebre coisas, experimente, veja o que acontece
3. **Pergunte sempre** - Não entendeu algo? Pesquise, pergunte ao professor
4. **Um passo de cada vez** - Não precisa entender tudo de uma vez

**Boa sorte nos estudos! 🚀**

---

*Material desenvolvido para o curso de Análise e Desenvolvimento de Sistemas*
*Versão 1.0 - 2025*
