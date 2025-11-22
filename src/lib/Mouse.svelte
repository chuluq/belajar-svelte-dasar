<script>
  const mouse = $state({
    x: 0,
    y: 0,
  });

  function handleMouseMove(event) {
    mouse.x = event.clientX;
    mouse.y = event.clientY;
  }
</script>

<svelte:body onmousemove={handleMouseMove} />

<h1>Mouse position: {mouse.x}, {mouse.y}</h1>
