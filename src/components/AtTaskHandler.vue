<template>
  <div class="flex justify-center px-6 py-40">
    <div>
      <div>
        <h2>Nueva Tarea:</h2>
        <div class="flex flex-col">
          <input
            class="rounded mb-2 text-gray-900 px-2"
            type="text"
            v-model="newTask.title"
            placeholder="Tarea"
          />
          <input
            class="rounded text-gray-900 px-2"
            type="number"
            v-model="newTask.time"
            placeholder="Tiempo"
          />
        </div>
        <div class="mt-2">
          <button @click="addTask" class="bg-green-600 rounded px-1 mr-1">
            Agregar
          </button>
          <button @click="cancelTask" class="bg-red-500 rounded px-1">
            Cancelar
          </button>
        </div>
      </div>
      <div>
        <p v-if="noTaskEntry">Ingrese una tarea</p>
        <table v-if="totalTime">
          <tr class="border-b-2">
            <th>Tarea</th>
            <th>Horas</th>
            <th></th>
          </tr>
          <tr v-for="(task, index) in tasks" :key="index" class="border-b">
            <td class="px-1 border-r">{{ task.title }}</td>
            <td class="text-right px-2">{{ task.time }} hs</td>
            <td
              class="rounded px-1 bg-red-500 cursor-pointer"
              @click="removeTask(index)"
            >
              X
            </td>
          </tr>
        </table>
      </div>
      <p v-if="totalTime"><strong>Horas totales:</strong> {{ totalTime }} Hs</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      noTaskEntry: false,
      tasks: [],
      newTask: {
        title: "",
        time: ""
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
        this.newTask.time = "";
      } else {
        this.noTaskEntry = true;
      }
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    cancelTask() {
      this.newTask.title = "";
      this.newTask.time = "";
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
<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type="number"] {
  -moz-appearance: textfield;
}
</style>
