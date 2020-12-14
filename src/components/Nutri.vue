<template>
  <div id="nutri">
    <header>
      <strong>Nutricao</strong>
    </header>
      <div v-if="loading">
        <h1>Carregando</h1>
      </div>
      <article v-else v-for="item in nutri" :key="item.id" class="post">
        <h1 class="titulo">{{item.titulo}}</h1>
        <img :src="item.capa" :alt="item.titulo">
        <span class="categoria">Categoria: {{item.categoria}}</span>
        <p class="subtitulo">{{item.subtitulo}}</p>
        <a class="botao" href="#">Acessar</a>
      </article>
  </div>
</template>

<script>
import api from "./../services/api"

export default {
  name: 'Nutri',
  data() {
    return {
      nutri: [],
      loading: true
    }
  },
  async created() {
    const response = await api.get("?api-posts")
    this.nutri = response.data
    this.loading = false
  }
}
</script>

<style scoped>
#nutri {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 100%;
  background: #DDD;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 35px;
  width: 100%;
  height: 60px;
  background: #4c89c3;
  color: #fff;
}

.post {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 700px;
  background: #fff;
  border-radius: 7px;
  margin: 8px;
  padding: 10px;
}

.titulo {
  font-size: 25px;
  margin-bottom: 25px;
  margin-top: 10px;
}

.categoria {
  padding-top: 15px;
  font-weight: bold;
}

.botao {
  height: 40px;
  background: none;
  border-radius: 5px;
  border: 2px solid #4c89c3;
  color: #4c89c3;
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;
  font-size: 18px;
  transition: all 0.5s;
}

.botao:hover {
  background: #4c89c3;
  color: #fff;
}
</style>