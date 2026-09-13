<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">

<title>cloudasic</title>

<style>
:root {
    --bg: #050505;
    --card: #0b0b0d;
    --text: #f5f5f5;
    --muted: #929292;
    --line: rgba(255,255,255,.14);

    --poster-w: min(80vw, 320px);
    --poster-h: 350px;
}

@media (max-height: 760px) {
    :root {
        --poster-w: min(78vw, 305px);
        --poster-h: 325px;
    }
}

@media (max-height: 670px) {
    :root {
        --poster-w: min(76vw, 292px);
        --poster-h: 305px;
    }
}

@media (max-height: 600px) {
    :root {
        --poster-w: min(74vw, 280px);
        --poster-h: 285px;
    }
}

* {
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
}

html {
    background: var(--bg);
}

body {
    width: 100%;
    min-height: 100dvh;
    margin: 0;
    background: var(--bg);
    color: var(--text);

    font-family:
        Inter,
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        sans-serif;

    overflow-x: hidden;
    overflow-y: auto;
}

.page {
    width: 100%;
    min-height: 100dvh;

    display: flex;
    flex-direction: column;

    padding:
        0
        18px
        calc(20px + env(safe-area-inset-bottom));
}

/* HEADER */

.header {
    flex-shrink: 0;
    padding: 17px 2px 8px;
    text-align: center;
}

.logo {
    font-size: 24px;
    font-weight: 700;
    letter-spacing: .4px;

    text-shadow:
        0 0 10px rgba(255,255,255,.2),
        0 0 28px rgba(255,255,255,.07);

    animation: logoGlow 3.5s ease-in-out infinite;
}

@keyframes logoGlow {
    0%,100% {
        text-shadow:
            0 0 10px rgba(255,255,255,.18),
            0 0 25px rgba(255,255,255,.05);
    }

    50% {
        text-shadow:
            0 0 14px rgba(255,255,255,.32),
            0 0 32px rgba(255,255,255,.10);
    }
}

.line {
    width: 100%;
    height: 1px;
    margin-top: 11px;

    background:
        linear-gradient(
            90deg,
            transparent,
            rgba(255,255,255,.2),
            transparent
        );
}

/* CAROUSEL */

.carousel-area {
    flex-shrink: 0;

    height: 380px;

    display: grid;
    place-items: center;

    overflow: hidden;

    perspective: 1300px;
}

.carousel {
    position: relative;

    width: var(--poster-w);
    height: var(--poster-h);

    transform-style: preserve-3d;
}

/* POSTER */

.poster {
    position: absolute;
    inset: 0;

    width: 100%;
    height: 100%;

    padding: 20px;

    border-radius: 24px;

    background:
        linear-gradient(
            145deg,
            rgba(255,255,255,.075),
            rgba(255,255,255,.018) 45%,
            rgba(0,0,0,.45)
        );

    border: 1px solid rgba(255,255,255,.18);

    box-shadow:
        0 0 14px rgba(255,255,255,.07),
        0 0 40px rgba(255,255,255,.035),
        inset 0 0 30px rgba(255,255,255,.025);

    overflow: hidden;

    opacity: 0;
    pointer-events: none;

    transform:
        translate3d(0,0,0)
        rotateY(0)
        rotateZ(0)
        scale(1);

    transition:
        transform .7s cubic-bezier(.16,1,.3,1),
        opacity .45s ease;

    transform-style: preserve-3d;
}

.poster.active {
    opacity: 1;
    pointer-events: auto;

    animation: posterFloat 4s ease-in-out infinite,
               posterGlow 4s ease-in-out infinite;
}

/* Внутреннее свечение */

.poster::before {
    content: "";

    position: absolute;
    inset: -45%;

    background:
        radial-gradient(
            circle at 50% 35%,
            rgba(255,255,255,.15),
            transparent 40%
        );

    pointer-events: none;

    animation: glowMove 5s ease-in-out infinite;
}

/* Движущийся блик */

.poster::after {
    content: "";

    position: absolute;

    top: -80%;
    left: -100%;

    width: 70%;
    height: 240%;

    background:
        linear-gradient(
            90deg,
            transparent,
            rgba(255,255,255,.075),
            transparent
        );

    transform: rotate(18deg);

    pointer-events: none;

    animation: shine 5s ease-in-out infinite;
}

@keyframes posterFloat {
    0%,100% {
        transform:
            translateY(0)
            rotateX(0deg)
            rotateZ(0deg);
    }

    50% {
        transform:
            translateY(-4px)
            rotateX(.7deg)
            rotateZ(.15deg);
    }
}

@keyframes posterGlow {
    0%,100% {
        box-shadow:
            0 0 14px rgba(255,255,255,.07),
            0 0 40px rgba(255,255,255,.035),
            inset 0 0 30px rgba(255,255,255,.025);
    }

    50% {
        box-shadow:
            0 0 18px rgba(255,255,255,.11),
            0 0 55px rgba(255,255,255,.055),
            inset 0 0 35px rgba(255,255,255,.035);
    }
}

@keyframes glowMove {
    0%,100% {
        transform: translate3d(-4%,0,0);
        opacity: .55;
    }

    50% {
        transform: translate3d(4%,2%,0);
        opacity: .9;
    }
}

@keyframes shine {
    0% {
        left: -110%;
    }

    55%,100% {
        left: 160%;
    }
}

/* CONTENT */

.poster-content {
    position: relative;
    z-index: 2;

    height: 100%;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.poster-top {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.poster-number {
    color: #777;
    font-size: 10px;
    letter-spacing: 2px;
}

.poster-tag {
    color: #999;
    font-size: 9px;
    letter-spacing: 1.5px;
}

.poster-title {
    margin-top: 10px;

    font-size: 29px;
    line-height: 1.05;

    font-weight: 700;
    letter-spacing: -.7px;

    text-shadow:
        0 0 12px rgba(255,255,255,.13);
}

.poster-subtitle {
    margin-top: 9px;

    color: #999;

    font-size: 11px;
    line-height: 1.4;
}

/* INFO */

.info-list {
    display: flex;
    flex-direction: column;

    gap: 7px;

    margin-top: 15px;
}

.info-item {
    display: flex;
    align-items: center;
    justify-content: space-between;

    padding: 9px 11px;

    border-radius: 10px;

    background:
        linear-gradient(
            90deg,
            rgba(255,255,255,.045),
            rgba(255,255,255,.018)
        );

    border: 1px solid rgba(255,255,255,.08);

    color: #c2c2c2;

    font-size: 10px;

    transition:
        transform .25s ease,
        border-color .25s ease,
        box-shadow .25s ease;
}

.info-item:hover {
    transform: translateX(3px);

    border-color: rgba(255,255,255,.2);

    box-shadow:
        0 0 14px rgba(255,255,255,.05);
}

.info-item span:last-child {
    color: #666;
    font-size: 8px;
}

/* WALLET */

.wallet {
    margin-top: 15px;

    padding: 12px;

    border-radius: 13px;

    background: rgba(255,255,255,.035);

    border: 1px solid rgba(255,255,255,.1);

    font-family: monospace;

    font-size: 9px;
    line-height: 1.4;

    word-break: break-all;

    color: #cfcfcf;

    box-shadow:
        0 0 18px rgba(255,255,255,.025),
        inset 0 0 20px rgba(255,255,255,.015);
}

.wallet-label {
    display: block;

    margin-bottom: 6px;

    color: #666;

    font-size: 8px;
    letter-spacing: 1.5px;
}

/* TAGS */

.tags {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
}

.tag {
    padding: 6px 9px;

    border: 1px solid rgba(255,255,255,.11);

    border-radius: 8px;

    color: #aaa;

    font-size: 8px;
    letter-spacing: 1px;

    background: rgba(255,255,255,.025);

    transition:
        transform .25s ease,
        box-shadow .25s ease;
}

.tag:hover {
    transform: translateY(-2px);

    box-shadow:
        0 0 12px rgba(255,255,255,.08);
}

/* TELEGRAM BUTTONS */

.poster-buttons {
    display: flex;
    flex-direction: column;

    gap: 8px;

    margin-top: 18px;
}

.poster-btn {
    position: relative;

    display: flex;
    align-items: center;
    justify-content: space-between;

    width: 100%;
    min-height: 43px;

    padding: 9px 12px;

    color: #fff;
    text-decoration: none;

    border-radius: 12px;

    background:
        linear-gradient(
            135deg,
            rgba(255,255,255,.09),
            rgba(255,255,255,.025)
        );

    border: 1px solid rgba(255,255,255,.2);

    overflow: hidden;

    transition:
        transform .2s ease,
        border-color .2s ease,
        box-shadow .2s ease;
}

.poster-btn::before,
.bottom-btn::before {
    content: "";

    position: absolute;

    top: -100%;
    left: -80%;

    width: 45%;
    height: 300%;

    background:
        linear-gradient(
            90deg,
            transparent,
            rgba(255,255,255,.2),
            transparent
        );

    transform: rotate(20deg);

    animation: buttonShine 3.8s ease-in-out infinite;
}

.poster-btn::after,
.bottom-btn::after {
    content: "";

    position: absolute;

    inset: 0;

    border-radius: inherit;

    box-shadow:
        inset 0 0 20px rgba(255,255,255,.025);

    pointer-events: none;
}

@keyframes buttonShine {
    0%,40% {
        left: -80%;
    }

    68%,100% {
        left: 150%;
    }
}

.poster-btn:hover {
    transform:
        translateY(-2px)
        scale(1.015);

    border-color: rgba(255,255,255,.42);

    box-shadow:
        0 0 20px rgba(255,255,255,.11),
        0 8px 22px rgba(0,0,0,.3);
}

.poster-btn:active {
    transform: scale(.95);
}

.poster-btn-left {
    position: relative;
    z-index: 2;

    display: flex;
    align-items: center;
    gap: 9px;
}

.poster-icon {
    width: 25px;
    height: 25px;

    display: grid;
    place-items: center;

    border-radius: 7px;

    background: rgba(255,255,255,.08);

    font-size: 11px;

    transition:
        transform .3s ease,
        box-shadow .3s ease;
}

.poster-btn:hover .poster-icon {
    transform: rotate(-5deg) scale(1.08);

    box-shadow:
        0 0 12px rgba(255,255,255,.1);
}

.poster-btn-text {
    display: flex;
    flex-direction: column;
    gap: 2px;
}

.poster-btn-title {
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 1px;
}

.poster-btn-user {
    color: #777;
    font-size: 8px;
}

.poster-btn-arrow {
    position: relative;
    z-index: 2;

    color: #aaa;
    font-size: 15px;

    transition:
        transform .3s ease,
        color .3s ease;
}

.poster-btn:hover .poster-btn-arrow {
    transform: translate(3px,-3px);
    color: #fff;
}

/* BOTTOM */

.bottom {
    flex-shrink: 0;

    padding:
        8px
        0
        10px;
}

.bottom-line {
    width: 100%;
    height: 1px;

    margin-bottom: 11px;

    background:
        linear-gradient(
            90deg,
            transparent,
            rgba(255,255,255,.18),
            transparent
        );
}

.bottom-title {
    font-size: 13px;

    font-weight: 700;

    letter-spacing: .7px;

    margin-bottom: 6px;
}

.bottom-text {
    color: #8e8e8e;

    font-size: 9.5px;

    line-height: 1.34;
}

.bottom-text p {
    margin: 0 0 6px;
}

.bottom-text ul {
    margin: 0 0 7px;

    padding-left: 16px;
}

.bottom-text li {
    margin: 2px 0;
}

/* BOTTOM BUTTONS */

.bottom-buttons {
    display: flex;

    gap: 9px;

    margin-top: 10px;
}

.bottom-btn {
    position: relative;

    flex: 1;

    min-height: 50px;

    display: flex;

    align-items: center;
    justify-content: space-between;

    padding: 9px 12px;

    color: white;

    text-decoration: none;

    border-radius: 14px;

    overflow: hidden;

    background:
        linear-gradient(
            135deg,
            rgba(255,255,255,.095),
            rgba(255,255,255,.025)
        );

    border: 1px solid rgba(255,255,255,.22);

    box-shadow:
        0 0 12px rgba(255,255,255,.05),
        inset 0 0 15px rgba(255,255,255,.025);

    transition:
        transform .2s ease,
        box-shadow .2s ease,
        border-color .2s ease;
}

.bottom-btn:hover {
    transform:
        translateY(-3px)
        scale(1.015);

    border-color: rgba(255,255,255,.45);

    box-shadow:
        0 0 24px rgba(255,255,255,.13),
        0 10px 28px rgba(0,0,0,.35);
}

.bottom-btn:active {
    transform: scale(.95);
}

.btn-left {
    position: relative;
    z-index: 2;

    display: flex;

    align-items: center;

    gap: 9px;
}

.btn-icon {
    width: 28px;
    height: 28px;

    display: grid;
    place-items: center;

    border-radius: 8px;

    background: rgba(255,255,255,.08);

    font-size: 12px;

    transition:
        transform .3s ease,
        box-shadow .3s ease;
}

.bottom-btn:hover .btn-icon {
    transform: scale(1.08) rotate(-4deg);

    box-shadow:
        0 0 14px rgba(255,255,255,.1);
}

.btn-info {
    display: flex;
    flex-direction: column;

    gap: 2px;
}

.btn-title {
    font-size: 9px;

    font-weight: 700;

    letter-spacing: 1px;
}

.btn-user {
    color: #777;

    font-size: 8px;
}

.btn-arrow {
    position: relative;
    z-index: 2;

    color: #aaa;

    font-size: 15px;

    transition:
        transform .3s ease,
        color .3s ease;
}

.bottom-btn:hover .btn-arrow {
    transform: translate(3px,-3px);
    color: #fff;
}

/* SWIPE */

.poster.dragging {
    transition: none !important;
    animation: none !important;
}

.poster.leaving {
    animation: none !important;

    transition:
        transform .72s cubic-bezier(.15,.85,.25,1),
        opacity .55s ease !important;
}

.poster.entering {
    animation: none !important;

    transition:
        transform .72s cubic-bezier(.15,.85,.25,1),
        opacity .6s ease !important;
}

/* SMALL PHONE */

@media (max-width: 360px) {

    .page {
        padding-left: 14px;
        padding-right: 14px;
    }

    .carousel-area {
        height: 350px;
    }

    .poster {
        padding: 17px;
        border-radius: 21px;
    }

    .poster-title {
        font-size: 26px;
    }

    .bottom-text {
        font-size: 9px;
    }

    .bottom-buttons {
        gap: 6px;
    }

    .bottom-btn {
        min-height: 46px;
        padding: 8px;
    }

    .btn-title {
        font-size: 8px;
    }
}
</style>
</head>

<body>

<div class="page">

<header class="header">
    <div class="logo">cloudasic</div>
    <div class="line"></div>
</header>


<main class="carousel-area">

<div class="carousel" id="carousel">


<!-- POSTER 1 -->

<article class="poster active">

<div class="poster-content">

<div>

<div class="poster-top">
    <span class="poster-number">01 / 04</span>
    <span class="poster-tag">CRYPTO</span>
</div>

<div class="poster-title">
    Мой<br>кошелек
</div>

<div class="poster-subtitle">
    Мой основной крипто-кошелек
    для TON и NFT.
</div>

<div class="wallet">

<span class="wallet-label">
    WALLET ADDRESS
</span>

UQDjMXuHT4gYTMj-K-ekvpaJaOiSPmt7Pg9bCI65OdaVdPG1

</div>

</div>

<div class="tags">
    <span class="tag">CRYPTO</span>
    <span class="tag">TON</span>
    <span class="tag">NFT</span>
</div>

</div>

</article>


<!-- POSTER 2 -->

<article class="poster">

<div class="poster-content">

<div>

<div class="poster-top">
    <span class="poster-number">02 / 04</span>
    <span class="poster-tag">ABOUT</span>
</div>

<div class="poster-title">
    Обо<br>мне
</div>

<div class="poster-subtitle">
    Немного информации обо мне
    и том, чем я занимаюсь.
</div>

<div class="info-list">

<div class="info-item">
    <span>16 лет</span>
    <span>AGE</span>
</div>

<div class="info-item">
    <span>Создаю сайты</span>
    <span>WEB</span>
</div>

<div class="info-item">
    <span>NFT / Crypto</span>
    <span>DIGITAL</span>
</div>

<div class="info-item">
    <span>Telegram-проекты</span>
    <span>PROJECTS</span>
</div>

</div>

</div>

</div>

</article>


<!-- POSTER 3 -->

<article class="poster">

<div class="poster-content">

<div>

<div class="poster-top">
    <span class="poster-number">03 / 04</span>
    <span class="poster-tag">TELEGRAM</span>
</div>

<div class="poster-title">
    Мой<br>Telegram
</div>

<div class="poster-subtitle">
    Мой Telegram-канал
    и связь со мной.
</div>

<div class="poster-buttons">

<a
    class="poster-btn"
    href="https://t.me/loffi_NFT"
    target="_blank"
>

<div class="poster-btn-left">

<div class="poster-icon">
    ✈
</div>

<div class="poster-btn-text">

<span class="poster-btn-title">
    МОЙ КАНАЛ
</span>

<span class="poster-btn-user">
    loffi_NFT
</span>

</div>

</div>

<span class="poster-btn-arrow">
    ↗
</span>

</a>


<a
    class="poster-btn"
    href="https://t.me/cloudasic"
    target="_blank"
>

<div class="poster-btn-left">

<div class="poster-icon">
    @
</div>

<div class="poster-btn-text">

<span class="poster-btn-title">
    СВЯЗЬ СО МНОЙ
</span>

<span class="poster-btn-user">
    @cloudasic
</span>

</div>

</div>

<span class="poster-btn-arrow">
    ↗
</span>

</a>

</div>

</div>

<div class="tags">
    <span class="tag">CHANNEL</span>
    <span class="tag">CONTACT</span>
</div>

</div>

</article>


<!-- POSTER 4 -->

<article class="poster">

<div class="poster-content">

<div>

<div class="poster-top">
    <span class="poster-number">04 / 04</span>
    <span class="poster-tag">PROJECTS</span>
</div>

<div class="poster-title">
    Мои<br>проекты
</div>

<div class="poster-subtitle">
    Создаю и развиваю digital-проекты.
</div>

<div class="info-list">

<div class="info-item">
    <span>Websites</span>
    <span>01</span>
</div>

<div class="info-item">
    <span>Telegram</span>
    <span>02</span>
</div>

<div class="info-item">
    <span>NFT</span>
    <span>03</span>
</div>

<div class="info-item">
    <span>Design</span>
    <span>04</span>
</div>

</div>

</div>

</div>

</article>

</div>

</main>


<!-- BOTTOM -->

<section class="bottom">

<div class="bottom-line"></div>

<div class="bottom-title">
    ПЕРСОНАЛЬНЫЙ САЙТ
</div>

<div class="bottom-text">

<p>
Создам для вас персональный сайт с уникальным дизайном
и современными 3D-эффектами.
</p>

<p>
Сайт может подойти для:
</p>

<ul>

<li>приглашения в Telegram-канал или проект</li>

<li>презентации себя или своей команды</li>

<li>информации о проекте, бренде или услуге</li>

<li>портфолио и личной страницы</li>

<li>рекламы и продвижения</li>

<li>любой другой идеи, которую вы хотите реализовать</li>

</ul>

<p>
Стоимость — от ★ 100
</p>

<p>
Связь со мной — @cloudasic
</p>

<p>
Пример такого сайта вы можете наблюдать прямо сейчас.
</p>

</div>


<div class="bottom-buttons">

<a
    class="bottom-btn"
    href="https://t.me/loffi_NFT"
    target="_blank"
>

<div class="btn-left">

<div class="btn-icon">
    ✈
</div>

<div class="btn-info">

<span class="btn-title">
    МОЙ КАНАЛ
</span>

<span class="btn-user">
    loffi_NFT
</span>

</div>

</div>

<span class="btn-arrow">
    ↗
</span>

</a>


<a
    class="bottom-btn"
    href="https://t.me/cloudasic"
    target="_blank"
>

<div class="btn-left">

<div class="btn-icon">
    @
</div>

<div class="btn-info">

<span class="btn-title">
    СВЯЗЬ СО МНОЙ
</span>

<span class="btn-user">
    @cloudasic
</span>

</div>

</div>

<span class="btn-arrow">
    ↗
</span>

</a>

</div>

</section>

</div>


<script>

const posters = document.querySelectorAll(".poster");

let current = 0;

let startX = 0;
let startY = 0;

let deltaX = 0;
let deltaY = 0;

let dragging = false;
let changing = false;


/* START */

function startDrag(e) {

    if (changing) return;

    const point =
        e.touches ? e.touches[0] : e;

    startX = point.clientX;
    startY = point.clientY;

    deltaX = 0;
    deltaY = 0;

    dragging = true;

    posters[current].classList.add("dragging");
}


/* MOVE */

function moveDrag(e) {

    if (!dragging || changing) return;

    const point =
        e.touches ? e.touches[0] : e;

    deltaX = point.clientX - startX;
    deltaY = point.clientY - startY;

    if (
        Math.abs(deltaY) >
        Math.abs(deltaX) * 1.2
    ) {
        return;
    }

    const card = posters[current];

    const rotateY = deltaX * .075;
    const rotateZ = deltaX * .018;

    const lift =
        Math.abs(deltaX) * -.018;

    const scale =
        1 -
        Math.min(
            Math.abs(deltaX) / 1500,
            .08
        );

    card.style.transform = `
        translate3d(
            ${deltaX}px,
            ${lift}px,
            0
        )
        rotateY(${rotateY}deg)
        rotateZ(${rotateZ}deg)
        scale(${scale})
    `;

    card.style.opacity =
        1 -
        Math.min(
            Math.abs(deltaX) / 650,
            .42
        );
}


/* END */

function endDrag() {

    if (!dragging || changing) return;

    dragging = false;

    const card = posters[current];

    card.classList.remove("dragging");

    if (Math.abs(deltaX) < 80) {

        card.style.transition =
            "transform .45s cubic-bezier(.2,1.4,.4,1), opacity .35s ease";

        card.style.transform =
            "translate3d(0,0,0) rotateY(0) rotateZ(0) scale(1)";

        card.style.opacity = "1";

        return;
    }

    changePoster(
        deltaX > 0 ? 1 : -1
    );
}


/* CHANGE POSTER */

function changePoster(direction) {

    if (changing) return;

    changing = true;

    const oldIndex = current;

    let nextIndex =
        current + direction;

    if (nextIndex < 0)
        nextIndex = posters.length - 1;

    if (nextIndex >= posters.length)
        nextIndex = 0;

    const oldCard =
        posters[oldIndex];

    const nextCard =
        posters[nextIndex];


    nextCard.classList.remove("active");
    nextCard.classList.add("entering");

    nextCard.style.transition = "none";

    nextCard.style.opacity = "0";

    nextCard.style.transform = `
        translate3d(
            ${direction * -100}vw,
            ${direction * -8}vh,
            -100px
        )
        rotateY(${direction * -50}deg)
        rotateZ(${direction * -10}deg)
        scale(.76)
    `;


    oldCard.classList.add("leaving");

    oldCard.style.transition =
        "transform .72s cubic-bezier(.15,.85,.25,1), opacity .55s ease";

    oldCard.style.transform = `
        translate3d(
            ${direction * 125}vw,
            ${direction * -12}vh,
            0
        )
        rotateY(${direction * 55}deg)
        rotateZ(${direction * 13}deg)
        scale(.72)
    `;

    oldCard.style.opacity = "0";


    setTimeout(() => {

        nextCard.classList.add("active");

        requestAnimationFrame(() => {

            requestAnimationFrame(() => {

                nextCard.style.transition =
                    "transform .72s cubic-bezier(.15,.85,.25,1), opacity .6s ease";

                nextCard.style.transform = `
                    translate3d(0,0,0)
                    rotateY(0)
                    rotateZ(0)
                    scale(1)
                `;

                nextCard.style.opacity = "1";

            });

        });

    }, 35);


    setTimeout(() => {

        oldCard.classList.remove(
            "active",
            "leaving"
        );

        oldCard.style.transition = "none";

        oldCard.style.transform =
            "translate3d(0,0,0) rotateY(0) rotateZ(0) scale(1)";

        oldCard.style.opacity = "0";

        nextCard.classList.remove("entering");

        current = nextIndex;

        changing = false;

    }, 800);
}


/* TOUCH */

const carousel =
    document.getElementById("carousel");

carousel.addEventListener(
    "touchstart",
    startDrag,
    { passive: true }
);

carousel.addEventListener(
    "touchmove",
    moveDrag,
    { passive: true }
);

carousel.addEventListener(
    "touchend",
    endDrag,
    { passive: true }
);


/* MOUSE */

carousel.addEventListener(
    "mousedown",
    startDrag
);

window.addEventListener(
    "mousemove",
    moveDrag
);

window.addEventListener(
    "mouseup",
    endDrag
);

</script>

</body>
</html>
