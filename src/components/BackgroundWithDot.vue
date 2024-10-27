<template>
  <canvas id="dots-canvas"></canvas>
</template>
<script setup>
import { onMounted } from 'vue';

onMounted(() => {
  const canvas = document.getElementById('dots-canvas');
  canvas.width = canvas.offsetWidth;
  canvas.height = canvas.offsetHeight;
  const ctx = canvas.getContext('2d');

  document.addEventListener('mousemove', onmousemove);
  document.addEventListener('mouseleave', onmouseleave);

  const circleProperties = {
    minRadius: 5,
    maxRadius: 8,
    colors: ['#eee', '#596d91', '#545454', '#bb5a68', '#696541'],
  };

  const circles = [];
  for (let i = 0; i < 50; i++) {
    const circle = {
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      radius:
        Math.random() *
          (circleProperties.maxRadius - circleProperties.minRadius) +
        circleProperties.minRadius,
      color:
        circleProperties.colors[
          Math.floor(Math.random() * circleProperties.colors.length)
        ],
    };
    circles.push(circle);
  }

  function drawCircles() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for (const circle of circles) {
      ctx.fillStyle = circle.color;
      ctx.beginPath();
      ctx.arc(circle.x, circle.y, circle.radius, 0, 2 * Math.PI);
      ctx.fill();
    }
  }
  drawCircles();

  function drawLines(mouseX, mouseY) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawCircles();

    for (const circle of circles) {
      const distance = Math.sqrt(
        (circle.x - mouseX) ** 2 + (circle.y - mouseY) ** 2
      );
      if (distance < 300) {
        ctx.strokeStyle = circle.color;
        ctx.lineWidth = 1;
        ctx.beginPath();
        ctx.moveTo(circle.x, circle.y);
        ctx.lineTo(mouseX, mouseY);
        ctx.stroke();
      }
    }
  }

  function onmousemove(e) {
    const mouseX = e.clientX;
    const mouseY = e.clientY;
    drawLines(mouseX, mouseY);
  }

  function onmouseleave(e) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawCircles();
  }
});
</script>
