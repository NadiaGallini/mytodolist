<template>
  <q-page class="bg-grey-3 column">
    <q-list separator bordered>
      <q-item
        @click="toggleTaskDone(index)"
        clickable
        :class="{'done bg-green-3': task.done }"
        v-for="(task, index) in tasks" 
        :key="task.title" 
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox class="no-pointer-event" v-model="task.done" val="teal" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn @click.stop="deleteTask(index)" dense flat round color="primary" icon="delete" />       
        </q-item-section>
      </q-item>
    </q-list>

    <!-- Форма для добавления новой задачи -->
    <q-input outlined v-model="newTaskTitle" label="Новая задача" />
    <q-btn @click="addTask" color="primary" label="Добавить задачу" />
  </q-page>
</template>

<script>
export default { 
  data() {
    return {
      tasks: [
        {
          title: "hello",
          done: true,
        },
        {
          title: "hello2",
          done: false,
        },
        {
          title: "hello3",
          done: false,
        },
      ],
      newTaskTitle: '', // Название новой задачи
    };
  },
  methods: {
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTaskDone(index) {
      this.tasks[index].done = !this.tasks[index].done;
    },
    addTask() {
      if (this.newTaskTitle.trim() !== '') {
        this.tasks.push({
          title: this.newTaskTitle.trim(),
          done: false,
        });
        this.newTaskTitle = ''; // Очистить поле ввода после добавления задачи
      }
    },
  },
};
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: grey;
  }
}
</style>
