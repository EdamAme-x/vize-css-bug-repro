<template>
  <main class="box">
    <h1>Vize CSS repro</h1>
    <p>If scoped CSS is loaded, this page has a black background.</p>
  </main>
</template>

<style scoped>
.box {
  min-height: 100vh;
  display: grid;
  place-content: center;
  gap: 1rem;
  margin: 0;
  background: black;
  color: white;
  text-align: center;
  font-family: system-ui, sans-serif;
}

h1,
p {
  margin: 0;
}
</style>
