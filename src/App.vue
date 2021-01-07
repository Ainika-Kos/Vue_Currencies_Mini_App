<template>
  <div class="todoApp">
    <h1 v-if="!todo.length" class="heading">
      You don't have any task!
    </h1>
    <h1 v-else-if="todo.length < 2" class="heading">
      You have {{ todo.length }} task
    </h1>
    <h1 v-else class="heading">
      You have {{ todo.length }} tasks
    </h1>
    <p class="action-text">Add new task:</p>
    <div class="action-wrapper">
      <input
        type="text"
        v-model="newTask"
        placeholder="Enter your task"
        @keyup.enter="addTask(newTask)"
        class="inputTask"
      />
      <Button label="Add task" @onClick="addTask(newTask)" />
    </div>
    <p class="action-text">Filter tasks:</p>
    <div class="action-wrapper">
      <Button label="All tasks"  @onClick="showAllTasks()" />
      <Button label="Active tasks"  @onClick="showActiveTasks()" />
      <Button label="Completed tasks" @onClick="showDoneTasks()" />
    </div>
    <div class="task-wrapper">
      <div v-for="task in filteredList" :key="task.id" class="task">
        <div>
          <input type="checkbox" :id="task.id" v-model="task.completed" />
          <label
            :for="task.id"
            class="task__text"
            :class="{ finished: task.completed }"
          >
            {{ task.name }}
          </label>
        </div>
        <Button label="Delete task" @onClick="removeTask(task.id)" />
      </div>
    </div>
    <p v-show="todo.length" class="action-text">Actions with all tasks:</p>
    <div v-show="todo.length" class="action-wrapper">
      <Button label="Remove all" @onClick="removeAllTasks()" />
      <Button label="All done" @onClick="finishAllTasks()" />
      <Button label="All active" @onClick="unFinishAllTasks()" />
    </div>
  </div>
</template>

<style src="./app.scss" lang="scss" scoped></style>
<style src="vue-flexboxgrid/dist/vue-flexboxgrid.css"/>

<script lang="ts">
import { defineComponent } from 'vue';
/* import flexboxgrid from 'flexboxgrid'; */
import Button from './components/button/button.vue';
/* import Input from './components/input/input.vue'; */

type Data = {
  header: string;
  newTask: string;
  showTask: 'all' | 'active' | 'done';
};

type Todo = {
  id: number;
  name: string;
  completed: boolean;
};

const Component = defineComponent({
  components: {
    Button,
    // Input,
  },
  data() {
    return {
      header: 'ToDo list',
      newTask: '',
      showTask: 'all',
      todo: [
        {
          id: 0,
          name: 'Buy milk',
          completed: false,
        },
        {
          id: 1,
          name: 'Buy bread',
          completed: false,
        },
        {
          id: 2,
          name: 'Buy banana',
          completed: false,
        },
      ],
    };
  },
  computed: {
    filteredList(): Todo[] {
      let filteredTodo = [...this.todo];
      if (this.showTask === 'active') {
        filteredTodo = this.todo.filter((item) => item.completed === false);
      } else if (this.showTask === 'done') {
        filteredTodo = this.todo.filter((item) => item.completed === true);
      }
      return filteredTodo;
    },
  },
  methods: {
    removeTask(id: number) {
      const index = this.todo.findIndex((item) => item.id === id);
      this.todo.splice(index, 1);
    },
    finishTask(id: number) {
      const index = this.todo.findIndex((item) => item.id === id);
      this.todo[index].completed = !this.todo[index].completed;
    },
    addTask(newTask: string) {
      if (newTask) {
        const newTodoTask = {
          id: this.todo.length + 1,
          name: newTask,
          completed: false,
        };
        this.todo.push(newTodoTask);
        this.newTask = '';
      }
    },
    showAllTasks() {
      this.showTask = 'all';
    },
    showActiveTasks() {
      this.showTask = 'active';
    },
    showDoneTasks() {
      this.showTask = 'done';
    },
    removeAllTasks() {
      this.todo = [];
    },
    finishAllTasks() {
      for (let i = 0; i < this.todo.length; i += 1) {
        this.todo[i].completed = true;
      }
    },
    unFinishAllTasks() {
      for (let i = 0; i < this.todo.length; i += 1) {
        this.todo[i].completed = false;
      }
    },
  },
});

export default Component;
</script>
