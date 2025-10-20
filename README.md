# test2
<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Liquid Ether Background</title>
<style>
  html, body {
    margin: 0;
    height: 100%;
    overflow: hidden;
    background: #0a0a0a;
  }

  canvas {
    width: 100%;
    height: 100%;
    display: block;
  }
</style>
</head>
<body>
<canvas id="liquid"></canvas>

<script>
const canvas = document.getElementById("liquid");
const ctx = canvas.getContext("2d");
let w, h, t = 0;
let mouseX = 0.5, mouseY = 0.5;

function resize() {
  w = canvas.width = window.innerWidth;
  h = canvas.height = window.innerHeight;
}
resize();
window.addEventListener("resize", resize);
window.addEventListener("mousemove", e => {
  mouseX = e.clientX / w;
  mouseY = e.clientY / h;
});

function draw() {
  t += 0.015;
  const img = ctx.createImageData(w, h);
  for (let i = 0; i < img.data.length; i += 4) {
    const x = (i / 4) % w;
    const y = Math.floor(i / 4 / w);
    const v =
      Math.sin(x * 0.012 + t + mouseX * 2) +
      Math.cos(y * 0.012 + t + mouseY * 2);
    const c = 128 + v * 64;
    img.data[i] = c * 0.5;
    img.data[i + 1] = c * 0.8;
    img.data[i + 2] = 255 - c * 0.3;
    img.data[i + 3] = 255;
  }
  ctx.putImageData(img, 0, 0);
  requestAnimationFrame(draw);
}
draw();
</script>
</body>
</html>
