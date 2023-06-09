<template>
  <div class="main d-flex flex-column align-items-center">
    <h1 class="mb-3">Список дел</h1>
    <div class="col-2">
      <input v-model.trim="taskText" type="text" class="form-control" placeholder="Задание" aria-label="Задание">
    </div>
    <br>
    <div class="buttons mb-3">
      <button @click="addTask" class="btn btn-danger rounded-pill mx-2">Добавить</button>
      <button @click="toggleTasks" class="btn btn-danger rounded-pill mx-2">{{ showTasks ? 'Скрыть' : 'Отобразить' }}</button>
    </div>
    <div v-if="showSuccessMessage" id="success-of-adding-element" class="p-3 border rounded-3 border-3 border-opacity-100 text-center text-bg-secondary">
      Элемент был добавлен
    </div>
    <ol id="task-list" v-show="showTasks">
      <li v-for="task in tasks" :key="task.id">
        <span>{{ task.text }}</span>
        <button @click="deleteTask(task.id)" class="btn btn-danger rounded-pill mx-2">Удалить</button>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  data() {
    return {
      taskText: "",
      tasks: [],
      showSuccessMessage: false,
      showTasks: false,
    };
  },
  methods: {
    addTask() {
      const trimmedText = this.taskText.trim();
      if (trimmedText !== "") {
        const task = {
          id: Date.now(),
          text: trimmedText,
        };
        this.tasks.push(task);
        this.taskText = "";
        this.showSuccessMessage = true;
        setTimeout(() => {
          this.showSuccessMessage = false;
        }, 2000);
      }
    },
    toggleTasks() {
      this.showTasks = !this.showTasks;
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter((task) => task.id !== taskId);
    },
  },
};
</script>

<style>

</style>
