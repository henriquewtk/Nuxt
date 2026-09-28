<template>
  <div class="home">
    <section class="hero">
      <div class="container">
        <h2>Bem-vindo ao Projeto Nuxt</h2>

        <p>
          Aplicação desenvolvida utilizando Node.js, Vue.js e Nuxt.js.
        </p>

        <NuxtLink to="/cadastro" class="button">
          Ir para cadastro
        </NuxtLink>
      </div>
    </section>

    <section class="container cards">
      <div class="card">
        <h3>Node.js</h3>
        <p>
          Ambiente de execução utilizado no ecossistema JavaScript.
        </p>
      </div>

      <div class="card">
        <h3>Vue.js</h3>
        <p>
          Framework utilizado para construção da interface.
        </p>
      </div>

      <div class="card">
        <h3>Nuxt</h3>
        <p>
          Framework baseado em Vue para aplicações web modernas.
        </p>
      </div>
    </section>
  </div>
</template>

<style scoped>
.home {
  padding-bottom: 40px;
}

.hero {
  padding: 80px 0;
  background: #dbeafe;
  text-align: center;
}

.hero h2 {
  font-size: 40px;
  margin-bottom: 15px;
}

.hero p {
  font-size: 18px;
  margin-bottom: 30px;
}

.button {
  display: inline-block;
  padding: 12px 22px;
  background: #2563eb;
  color: white;
  text-decoration: none;
  border-radius: 6px;
}

.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-top: 40px;
}

.card {
  background: white;
  padding: 25px;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

@media (max-width: 700px) {
  .nav-content {
    flex-direction: column;
    gap: 15px;
  }

  .cards {
    grid-template-columns: 1fr;
  }
}
</style>