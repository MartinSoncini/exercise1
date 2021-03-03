<template>
  <div id="app">
    <h1>Administrador de tareas</h1>
    <div style="text-align: left; padding: 2rem">
      <h2 style="">Nueva Tarea:</h2>
      <div style="width: 100%; margin-bottom: 2rem">
        <input
          style="border: 0; background: #CCCACA; margin-right: 2rem; padding: 0.5rem; padding-left: 0.5rem; width:45%"
          type="text"
          v-model="newTask.title"
          placeholder="Tarea"
        />
        <input
          style="border: 0; background: #CCCACA; padding: 0.5rem; padding-left: 0.5rem"
          type="number"
          v-model="newTask.time"
          placeholder="Tiempo"
        />
      </div>
      <div>
        <button
          style="border: 0; border-radius: 10px; background: #7EB9B7; padding: 0.5rem; cursor: pointer; margin-right: 1rem;"
          @click="addTask"
        >
          Agregar
        </button>
        <button
          style="border: 0; border-radius: 10px; background: #CCCACA; padding: 0.5rem; cursor: pointer; :focus: outline: none"
          @click="cancelTask"
        >
          Cancelar
        </button>
      </div>
    </div>
    <div>
      <table style="margin: auto; width: 50%">
        <tr>
          <th>Tarea</th>
          <th>Horas</th>
          <th></th>
        </tr>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.title }}</td>
          <td>{{ task.time }}</td>
          <td style="text-align:center">
            <button
              @click="removeTask(index)"
              style="border: 0; border-radius: 10px; background: #EF6666; padding: 0.5rem; cursor: pointer; :focus: outline: none"
            >
              Borrar
            </button>
          </td>
        </tr>
      </table>
    </div>
    <p v-if="totalTime"><strong>Horas totales:</strong> {{ totalTime }} Hs</p>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      tasks: [],
      newTask: {
        title: "",
        time: 0
      }
    };
  },
  computed: {
    totalTime() {
      let total = 0;
      this.tasks.forEach(task => {
        total += Number(task.time);
      });
      return total;
    }
  },
  methods: {
    addTask() {
      if (this.newTask.title && this.newTask.time) {
        this.tasks.push({ title: this.newTask.title, time: this.newTask.time });
        this.newTask.title = "";
        this.newTask.time = 0;
      }
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    cancelTask() {
      this.newTask.title = "";
      this.newTask.time = 0;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    }
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
td {
  text-align: left;
  border-bottom: 1px solid black;
}
</style>
