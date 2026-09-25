<template>
  <div>
    <!-- Barra de navegação simples -->
    <nav style="padding: 1rem; background: #e0e0e0; display: flex; gap: 1.5rem; font-family: sans-serif;">
      <NuxtLink to="/">Início</NuxtLink>
      <NuxtLink to="/cadastro">Cadastrar Membro</NuxtLink>
    </nav>

    <!-- ESTA TAG É OBRIGATÓRIA PARA CARREGAR AS PÁGINAS -->
    <NuxtPage />
  </div>
</template>