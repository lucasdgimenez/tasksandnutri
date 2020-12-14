<template>
  <div id="task">
    <form @submit.prevent="addTask">
      <input 
        type="text"
        placeholder="Tarefa de hoje?"
        v-model="tarefa"
      />
      <button type="submit">Adicionar</button>
    </form>
    <Item :lista="list" :delete="deleteTask"/>

    <span v-show="list.length > 0">
      Você tem <strong :class="{pend: pendente}"> {{list.length}} </strong> tarefas pendentes
    </span>
  </div>
</template>

<script>
import Item from "./Item"
export default {
  name: 'Task',
  components: {
    Item
  },
  data() {
    return {
      tarefa: '',
      list: [],
      pendente: false
    }
  },
  methods: {
    addTask() {
      if(this.tarefa != "") {
        this.list.push({
          text: this.tarefa,
          key: Date.now(),
        });
        
      } else {
        alert("Digite uma tarefa...")
        return;
      }
      console.log(this.list)
      this.tarefa = "";
    },
    deleteTask(key) {
      console.log("deletou" + key)
      let filtro = this.list.filter((item) => {
        return (item.key !== key)
      })
      return this.list = filtro
    }
  },
  watch: {
    list: {
      deep: true,
      handler() {
        //salvar no localstorage
      localStorage.setItem('tasks', JSON.stringify(this.list))
      this.list.length > 4 ? this.pendente = true : this.pendente = false
      }
    }
  },
  created() {
    const json = localStorage.getItem('tasks')
    this.list = JSON.parse(json) || []
  }
}
</script>

<style scoped>
#task {
  max-width: 700px;
  background: #fff;
  border-radius: 4px;
  padding: 20px;
  margin: 20px auto;
  box-shadow: 0 0 20px rgba(0,0,0,0.2);
}
form {
  margin-top: 20px;
  display: flex;
  flex-direction: row;
}

form button {
  cursor: pointer;
  background: #0f5959;
  border: 0;
  border-radius: 4px;
  margin-left: 10px;
  padding: 0 15px;
  display: flex;
  justify-content: center;
  align-items: center; color: #fff;
}

input {
  flex: 1;
  border: 1px solid #eee;
  padding: 6px 10px;
  border-radius: 4px;
  font-size: 14px;
}

.pend {
  color: #ff0000;
}
</style>