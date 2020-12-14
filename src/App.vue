<template>
  <div id="app">
    <header>
      Minhas tarefas
    </header>
    <Task/>
    <Nutri/>
  </div>
</template>

<script>
import Task from "./components/Task"
import Nutri from "./components/Nutri"

export default {
  name: 'App',
  components: {
    Task, Nutri
  }
}
</script>

<style scoped>
  header {
   display: flex;
   flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 80px;
    font-size: 40px;
    color: #fff;
  }

</style>
