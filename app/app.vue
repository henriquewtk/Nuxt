<template>
  <div>
    <header class="navbar">
      <div class="container nav-content">
        <h1>Projeto Nuxt</h1>

        <nav>
          <NuxtLink to="/">Início</NuxtLink>
          <NuxtLink to="/cadastro">Cadastro</NuxtLink>
        </nav>
      </div>
    </header>

    <main>
      <NuxtPage />
    </main>

    <footer>
      <p>Projeto desenvolvido com Nuxt.js</p>
    </footer>
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f6f8;
  color: #222;
}

.navbar {
  background: #111827;
  color: white;
  padding: 18px 0;
}

.container {
  width: 90%;
  max-width: 1100px;
  margin: auto;
}

.nav-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-content h1 {
  margin: 0;
}

nav {
  display: flex;
  gap: 20px;
}

nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

nav a:hover {
  color: #60a5fa;
}

main {
  min-height: calc(100vh - 130px);
}

footer {
  text-align: center;
  padding: 20px;
  background: #111827;
  color: white;
}
</style>