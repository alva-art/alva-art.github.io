<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>ALV/ART – My Little Museum of Creative Stuff</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Jost:wght@300;400;800&display=swap" rel="stylesheet">
<style>
  :root {
    --orange: #ff7a00;
    --rust: #c0390b;
    --olive: #8c8a2e;
    --brown: #52251c;
    --green: #17352c;
    --sand: #e8e2df;
    --ink: #1a1a1a;
    --text: #3d3d3d;
  }
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body { margin: 0; font-family: "Jost", "Futura", sans-serif; color: var(--text); background: #fff; line-height: 1.5; }
  a { color: inherit; text-decoration: none; }
  a:focus-visible, label:focus-visible { outline: 3px solid var(--orange); outline-offset: 3px; }

  /* Burger menu (works without JavaScript) */
  #menu-toggle { position: absolute; opacity: 0; pointer-events: none; }
  .burger { position: fixed; top: 16px; left: 16px; z-index: 30; width: 46px; height: 46px; background: var(--orange); border-radius: 50%; display: flex; flex-direction: column; justify-content: center; align-items: center; gap: 5px; cursor: pointer; }
  .burger span { display: block; width: 20px; height: 3px; background: #000; border-radius: 2px; }
  #menu-toggle:focus-visible + .burger { outline: 3px solid #fff; outline-offset: 3px; }
  .menu { position: fixed; inset: 0; z-index: 20; background: var(--brown); display: none; flex-direction: column; justify-content: center; padding: 0 12vw; gap: 18px; }
  #menu-toggle:checked ~ .menu { display: flex; }
  .menu a { font-weight: 800; font-size: clamp(2rem, 7vw, 3.5rem); color: var(--orange); text-transform: uppercase; }
  .menu a:hover { color: #fff; }

  /* Header */
  .hero { background: #000; color: #fff; }
  .hero-photo { height: 200px; background: linear-gradient(120deg, #0b1d1f, #1d5c5a 55%, #0b1d1f); display: flex; align-items: center; justify-content: center; color: rgba(255,255,255,.35); font-size: .9rem; }
  .hero-body { display: flex; flex-wrap: wrap; gap: 28px; padding: 0 6vw 40px; max-width: 1100px; margin: 0 auto; }
  .logo { margin-top: -90px; width: 190px; height: 190px; flex: none; background: linear-gradient(160deg, #7a1f06, #d44a10); display: flex; align-items: flex-end; padding: 14px; }
  .logo span { font-weight: 800; font-size: 2.2rem; color: var(--orange); line-height: 1; }
  .intro { flex: 1 1 320px; padding-top: 22px; }
  .intro h1 { margin: 0 0 8px; font-weight: 400; font-size: 1.4rem; }
  .intro p { margin: 0 0 12px; font-weight: 300; color: #d6d6d6; max-width: 62ch; }
  .intro .driven { color: var(--orange); font-weight: 800; }

  /* Quarter-circle navigation tiles */
  .tiles { background: var(--sand); padding: 48px 6vw; }
  .tiles-grid { max-width: 1100px; margin: 0 auto; display: grid; grid-template-columns: repeat(4, 1fr); gap: 0; }
  .tile { display: block; position: relative; transition: transform .25s ease, filter .25s ease; }
  .tile .pic { aspect-ratio: 1 / 1; border-radius: 100% 0 0 0; display: flex; align-items: center; justify-content: center; color: rgba(255,255,255,.7); font-size: .85rem; }
  .tile .name { height: 50%; min-height: 70px; border-radius: 0 0 100% 0; padding: 14px 18px 0 18px; display: flex; align-items: flex-start; font-weight: 800; color: #fff; text-transform: uppercase; font-size: 1.05rem; }
  .tile:hover, .tile:focus-visible { transform: scale(1.05); filter: drop-shadow(0 10px 14px rgba(0,0,0,.3)); z-index: 2; }
  .tile.travel .pic { background: linear-gradient(160deg, #5a8f4a, #cfa43a); }
  .tile.travel .name { background: var(--olive); }
  .tile.photo .pic { background: linear-gradient(160deg, #f0a24a, #4b4a6b); }
  .tile.photo .name { background: var(--brown); }
  .tile.art .pic { background: linear-gradient(160deg, #6fa8c9, #e9b98a); }
  .tile.art .name { background: var(--rust); }
  .tile.moto .pic { background: linear-gradient(160deg, #1f6e8c, #d9b13b); }
  .tile.moto .name { background: var(--green); }
  .tile .name::after { content: ""; margin: 6px 0 0 8px; border-left: 9px solid var(--orange); border-top: 6px solid transparent; border-bottom: 6px solid transparent; }

  /* Museum rows */
  .museum { max-width: 1100px; margin: 0 auto; padding: 56px 6vw 24px; }
  .museum h2 { font-weight: 300; font-size: clamp(1.6rem, 4vw, 2.4rem); text-transform: uppercase; margin: 0 0 12px; color: var(--ink); }
  .freebie { display: inline-block; margin-bottom: 36px; background: var(--orange); color: #000; font-weight: 800; padding: 10px 22px; border-radius: 999px; }
  .freebie:hover { background: var(--brown); color: var(--orange); }
  .row { margin-bottom: 44px; scroll-margin-top: 20px; }
  .row h3 { margin: 0; font-weight: 800; font-size: 1.15rem; text-transform: uppercase; color: #000; display: inline-flex; align-items: center; gap: 8px; }
  .row h3::after { content: ""; border-left: 9px solid var(--orange); border-top: 6px solid transparent; border-bottom: 6px solid transparent; }
  .row p { margin: 6px 0 16px; max-width: 80ch; color: var(--text); font-size: 1rem; }
  .strip { display: grid; grid-template-columns: repeat(5, 1fr); gap: 14px; }
  .strip a { aspect-ratio: 3 / 4; display: flex; align-items: center; justify-content: center; color: rgba(255,255,255,.75); font-size: .8rem; transition: transform .2s ease; }
  .strip a:hover { transform: translateY(-4px); }
  .strip a:nth-child(1) { background: #c98b3d; }
  .strip a:nth-child(2) { background: #6b6b4a; }
  .strip a:nth-child(3) { background: #3f7a8c; }
  .strip a:nth-child(4) { background: #8a4b3a; }
  .strip a:nth-child(5) { background: #7fa6a3; }

  footer { background: var(--brown); color: var(--orange); font-weight: 800; padding: 16px 6vw; display: flex; justify-content: space-between; }
  footer a:hover { color: #fff; }

  @media (max-width: 760px) {
    .tiles-grid { grid-template-columns: repeat(2, 1fr); row-gap: 18px; }
    .strip { grid-template-columns: repeat(2, 1fr); }
    .logo { margin-top: -60px; width: 150px; height: 150px; }
  }
  @media (prefers-reduced-motion: reduce) { * { transition: none !important; scroll-behavior: auto !important; } }
</style>
</head>
<body>

<input type="checkbox" id="menu-toggle" aria-label="Open menu">
<label class="burger" for="menu-toggle" aria-hidden="true"><span></span><span></span><span></span></label>
<nav class="menu" aria-label="Main menu">
  <a href="#travel">Travel</a>
  <a href="#photography">Photography</a>
  <a href="#art">Art</a>
  <a href="#motorcycling">Motorcycling</a>
  <a href="#freebies">Free templates</a>
</nav>

<header class="hero">
  <div class="hero-photo">header photo (placeholder)</div>
  <div class="hero-body">
    <div class="logo"><span>ALV/<br>ART</span></div>
    <div class="intro">
      <p>My Little Museum of Creative Stuff</p>
      <h1>Hi, I am Alva</h1>
      <p>I love creating things &amp; collecting perspectives.<br>Exploring different bubbles, questioning what I think I know, learning, unlearning and trying to see the world through different eyes.</p>
      <p class="driven">Driven by curiosity, empathy, dopamine, creativity and a feminist mindset.</p>
    </div>
  </div>
</header>

<section class="tiles" aria-label="Topics">
  <div class="tiles-grid">
    <a class="tile travel" href="#travel"><div class="pic">photo</div><div class="name">Travel</div></a>
    <a class="tile photo" href="#photography"><div class="pic">photo</div><div class="name">Photography</div></a>
    <a class="tile art" href="#art"><div class="pic">photo</div><div class="name">Art</div></a>
    <a class="tile moto" href="#motorcycling"><div class="pic">photo</div><div class="name">Motorcycling</div></a>
  </div>
</section>

<main class="museum">
  <h2>My Little Museum of Creative Stuff</h2>
  <a class="freebie" id="freebies" href="#">Free templates</a>

  <section class="row" id="travel">
    <h3>Travel</h3>
    <p>I plan by getting lost in rabbit holes: the perfect spot to sleep, the perfect route, that one hidden place nobody talks about. I share the spots I find here, and if you’re curious, feel free to get inspired :D</p>
    <div class="strip"><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a></div>
  </section>

  <section class="row" id="photography">
    <h3>Photography</h3>
    <p>Shot on my iPhone. People keep asking what camera I use, and the answer is: the one in my pocket. I’m still flirting with a “real” camera, but for now phone photography is fun and honestly enough for me.</p>
    <div class="strip"><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a></div>
  </section>

  <section class="row" id="art">
    <h3>Art</h3>
    <p>Postcards, posters, little designs for my motorcycle: I love to illustrate. Lately I’m also drifting back to paint and canvas, trading pixels for brushes again.</p>
    <div class="strip"><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a></div>
  </section>

  <section class="row" id="motorcycling">
    <h3>Motorcycling</h3>
    <p>Here you can find some of my trips. I love riding through the mountains and catching every curve. With a naked bike I keep the trips doable, because there’s a limit until you’d probably need a proper touring bike, haha. But I love it and like to share our stories here. Feel free to get inspired by them!</p>
    <div class="strip"><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a><a href="#">image</a></div>
  </section>
</main>

<footer>
  <span>© 2026 ALV/ART</span>
  <a href="https://www.pinterest.com/" rel="noopener">Pinterest</a>
</footer>

</body>
</html>
