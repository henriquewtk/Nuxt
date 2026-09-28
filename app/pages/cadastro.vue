<script setup lang="ts">
import { reactive, ref } from 'vue'

const enviado = ref(false)

const formulario = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: '',
  interesses: [] as string[],
  bio: ''
})

const erros = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: '',
  interesses: '',
  bio: ''
})

const interessesDisponiveis = [
  'Front-end',
  'Back-end',
  'Mobile',
  'UI/UX',
  'Banco de Dados',
  'Redes'
]

function validarEmail(email: string) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

function validarFormulario() {
  erros.nome = ''
  erros.email = ''
  erros.curso = ''
  erros.semestre = ''
  erros.interesses = ''
  erros.bio = ''

  let valido = true

  if (!formulario.nome.trim()) {
    erros.nome = 'Informe seu nome completo.'
    valido = false
  }

  if (!formulario.email.trim()) {
    erros.email = 'Informe seu e-mail.'
    valido = false
  } else if (!validarEmail(formulario.email)) {
    erros.email = 'Informe um e-mail válido.'
    valido = false
  }

  if (!formulario.curso) {
    erros.curso = 'Selecione seu curso ou área.'
    valido = false
  }

  if (!formulario.semestre) {
    erros.semestre = 'Informe seu semestre.'
    valido = false
  }

  if (formulario.interesses.length === 0) {
    erros.interesses = 'Selecione pelo menos um interesse.'
    valido = false
  }

  if (formulario.bio.length > 300) {
    erros.bio = 'A bio deve possuir no máximo 300 caracteres.'
    valido = false
  }

  return valido
}

function enviarFormulario() {
  enviado.value = false

  if (!validarFormulario()) {
    return
  }

  console.log('Dados cadastrados:', {
    nome: formulario.nome,
    email: formulario.email,
    curso: formulario.curso,
    semestre: formulario.semestre,
    interesses: formulario.interesses,
    bio: formulario.bio
  })

  enviado.value = true

  formulario.nome = ''
  formulario.email = ''
  formulario.curso = ''
  formulario.semestre = ''
  formulario.interesses = []
  formulario.bio = ''
}
</script>

<template>
  <div class="pagina">
    <div class="container">
      <div class="titulo">
        <h2>Cadastro de Membro</h2>

        <p>
          Preencha os dados abaixo para realizar seu cadastro.
        </p>
      </div>

      <form @submit.prevent="enviarFormulario" class="formulario">

        <div class="campo">
          <label for="nome">Nome completo</label>

          <input
            id="nome"
            v-model="formulario.nome"
            type="text"
            placeholder="Digite seu nome completo"
          />

          <span v-if="erros.nome" class="erro">
            {{ erros.nome }}
          </span>
        </div>

        <div class="campo">
          <label for="email">E-mail</label>

          <input
            id="email"
            v-model="formulario.email"
            type="email"
            placeholder="exemplo@email.com"
          />

          <span v-if="erros.email" class="erro">
            {{ erros.email }}
          </span>
        </div>

        <div class="campo">
          <label for="curso">Curso / Área de atuação</label>

          <select id="curso" v-model="formulario.curso">
            <option value="">Selecione uma opção</option>
            <option value="Engenharia de Software">
              Engenharia de Software
            </option>
            <option value="Sistemas de Informação">
              Sistemas de Informação
            </option>
            <option value="Ciência da Computação">
              Ciência da Computação
            </option>
            <option value="Desenvolvimento Web">
              Desenvolvimento Web
            </option>
            <option value="Redes de Computadores">
              Redes de Computadores
            </option>
          </select>

          <span v-if="erros.curso" class="erro">
            {{ erros.curso }}
          </span>
        </div>

        <div class="campo">
          <label for="semestre">Semestre / Período</label>

          <input
            id="semestre"
            v-model="formulario.semestre"
            type="number"
            min="1"
            max="20"
            placeholder="Ex: 6"
          />

          <span v-if="erros.semestre" class="erro">
            {{ erros.semestre }}
          </span>
        </div>

        <div class="campo">
          <label>Interesses / Habilidades</label>

          <div class="checkboxes">
            <label
              v-for="interesse in interessesDisponiveis"
              :key="interesse"
              class="checkbox"
            >
              <input
                v-model="formulario.interesses"
                type="checkbox"
                :value="interesse"
              />

              {{ interesse }}
            </label>
          </div>

          <span v-if="erros.interesses" class="erro">
            {{ erros.interesses }}
          </span>
        </div>

        <div class="campo">
          <label for="bio">
            Mensagem / Bio curta
          </label>

          <textarea
            id="bio"
            v-model="formulario.bio"
            maxlength="300"
            rows="5"
            placeholder="Escreva uma breve apresentação..."
          ></textarea>

          <small>
            {{ formulario.bio.length }}/300 caracteres
          </small>

          <span v-if="erros.bio" class="erro">
            {{ erros.bio }}
          </span>
        </div>

        <button type="submit">
          Cadastrar
        </button>

        <div v-if="enviado" class="sucesso">
          Cadastro realizado com sucesso!
        </div>

      </form>
    </div>
  </div>
</template>

<style scoped>
.pagina {
  padding: 50px 0;
}

.titulo {
  text-align: center;
  margin-bottom: 30px;
}

.titulo h2 {
  font-size: 32px;
  margin-bottom: 10px;
}

.formulario {
  max-width: 700px;
  margin: auto;
  background: white;
  padding: 35px;
  border-radius: 12px;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.08);
}

.campo {
  margin-bottom: 22px;
}

.campo > label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
}

input,
select,
textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 15px;
}

input:focus,
select:focus,
textarea:focus {
  outline: none;
  border-color: #2563eb;
}

.checkboxes {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 10px;
}

.checkbox {
  font-weight: normal !important;
  display: flex !important;
  align-items: center;
  gap: 8px;
}

.checkbox input {
  width: auto;
}

button {
  width: 100%;
  padding: 14px;
  border: none;
  border-radius: 6px;
  background: #2563eb;
  color: white;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

button:hover {
  background: #1d4ed8;
}

.erro {
  display: block;
  color: #dc2626;
  margin-top: 6px;
  font-size: 14px;
}

.sucesso {
  margin-top: 20px;
  padding: 15px;
  border-radius: 6px;
  background: #dcfce7;
  color: #166534;
  text-align: center;
}

small {
  display: block;
  margin-top: 5px;
  color: #6b7280;
}

@media (max-width: 600px) {
  .formulario {
    padding: 20px;
  }

  .checkboxes {
    grid-template-columns: 1fr;
  }
}
</style>