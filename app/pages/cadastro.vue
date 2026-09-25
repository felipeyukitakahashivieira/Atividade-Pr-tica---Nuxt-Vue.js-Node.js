<template>
  <main class="container">
    <h1>Formulário de Cadastro</h1>

    <div v-if="successMessage" class="alert-success">
      {{ successMessage }}
    </div>

    <form @submit.prevent="handleSubmit" class="form">
      <div class="form-group">
        <label for="nome">Nome Completo *</label>
        <input id="nome" v-model="form.nome" type="text" placeholder="Digite seu nome completo" />
        <span v-if="errors.nome" class="error">{{ errors.nome }}</span>
      </div>

      <div class="form-group">
        <label for="email">E-mail *</label>
        <input id="email" v-model="form.email" type="email" placeholder="seuemail@exemplo.com" />
        <span v-if="errors.email" class="error">{{ errors.email }}</span>
      </div>

      <div class="form-group">
        <label for="curso">Curso / Área de Atuação</label>
        <select id="curso" v-model="form.curso">
          <option value="">Selecione uma opção...</option>
          <option value="Engenharia de Software">Engenharia de Software</option>
          <option value="Ciência da Computação">Ciência da Computação</option>
          <option value="Sistemas de Informação">Sistemas de Informação</option>
        </select>
      </div>

      <div class="form-group">
        <label for="semestre">Semestre / Período</label>
        <input id="semestre" v-model.number="form.semestre" type="number" min="1" max="12" />
      </div>

      <div class="form-group">
        <label>Interesses / Habilidades</label>
        <div class="checkbox-group">
          <label><input type="checkbox" value="Front-end" v-model="form.interesses" /> Front-end</label>
          <label><input type="checkbox" value="Back-end" v-model="form.interesses" /> Back-end</label>
          <label><input type="checkbox" value="Mobile" v-model="form.interesses" /> Mobile</label>
          <label><input type="checkbox" value="UI/UX" v-model="form.interesses" /> UI/UX</label>
        </div>
      </div>

      <div class="form-group">
        <label for="bio">Mensagem / Bio curta</label>
        <textarea id="bio" v-model="form.bio" maxlength="200" rows="4" placeholder="Escreva uma breve apresentação..."></textarea>
        <small>{{ 200 - form.bio.length }} caracteres restantes</small>
      </div>

      <button type="submit" class="btn-submit">Cadastrar</button>
    </form>
  </main>
</template>

<script setup>
import { reactive, ref } from 'vue'

const form = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: 1,
  interesses: [],
  bio: ''
})

const errors = reactive({
  nome: '',
  email: ''
})

const successMessage = ref('')

function validateEmail(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

function handleSubmit() {
  errors.nome = ''
  errors.email = ''
  successMessage.value = ''

  let isValid = true

  if (!form.nome.trim()) {
    errors.nome = 'O nome completo é obrigatório.'
    isValid = false
  }

  if (!form.email.trim()) {
    errors.email = 'O e-mail é obrigatório.'
    isValid = false
  } else if (!validateEmail(form.email)) {
    errors.email = 'Informe um e-mail válido.'
    isValid = false
  }

  if (isValid) {
    console.log('✅ Dados Enviados com Sucesso:', JSON.parse(JSON.stringify(form)))
    successMessage.value = 'Cadastro realizado com sucesso!'
    
    form.nome = ''
    form.email = ''
    form.curso = ''
    form.semestre = 1
    form.interesses = []
    form.bio = ''
  }
}
</script>

<style scoped>
.container { max-width: 500px; margin: 2rem auto; padding: 1.5rem; font-family: sans-serif; border: 1px solid #ddd; border-radius: 8px; }
.form-group { margin-bottom: 1rem; display: flex; flex-direction: column; }
.form-group label { font-weight: bold; margin-bottom: 0.3rem; }
.checkbox-group { display: flex; gap: 0.5rem; flex-wrap: wrap; }
.error { color: red; font-size: 0.85rem; margin-top: 0.2rem; }
.alert-success { background: #d4edda; color: #155724; padding: 1rem; margin-bottom: 1rem; border-radius: 4px; }
.btn-submit { background: #00dc82; color: white; border: none; padding: 0.75rem; cursor: pointer; font-weight: bold; border-radius: 4px; }
</style>