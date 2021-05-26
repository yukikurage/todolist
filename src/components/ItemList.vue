<!--
task {
  name : タスク名
  isFinished : 完了したか
}
-->

<template>
  <div>
    <div>タスク一覧</div>
    <div v-for="task in tasks" :key="task.name">
      <div class="task">
        <span class="name" :class="{ finished: task.isFinished }">{{ task.name }} </span>
        <button v-if="!task.isFinished" @click="finishTask(task)">完了</button>
      </div>
    </div>
    <div>
      <label>
        タスク名
        <input v-model="newTaskName" type="text" />
      </label>
      <button @click="addTask">追加</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const tasks = ref([]);
    const newTaskName = ref("");

    const addTask = () => {
      tasks.value.push({ name: newTaskName.value, isFinished: false });
      newTaskName.value = ""
    };

    const finishTask = task => {
      task.isFinished = true
    }

    return { tasks, newTaskName, addTask, finishTask };
  },
};
</script>

<style>
.finished {
  text-decoration: line-through
}
</style>