<template>
  <div id="app">
    <h4 class="bg-primary p-2 text-white text-center">
      {{name}}'s' To do list
    </h4>
    <div class="container-fluid p-4">
      <div class="row">
        <div class="col font-weight-bold">Task</div>
        <div class="col-2 font-weight-bold">Done</div>
      </div>
      <div class="row" v-for="task in filteredTasks" v-bind:key="task.action">
        <div class="col">{{task.action}}</div>
        <div class="col-2">
          <input type="checkbox" class="form-check-input" v-model="task.done" />
          {{task.done}}
        </div>
      </div>
      <form v-on:submit.prevent class="form">
        <div class="row py-2">
          <div class="col">
            <input reqiured v-model="newItemText" class="form-control" />
          </div>
          <div class="col-2">
            <button class="btn btn-primary" type="submit" v-on:click="addNewTodo">Add</button>
          </div>
        </div>
      </form>
      <div class="row bg-secondary py-2 mt-2 text-white">
        <div class="col text-center">
          <input id="hideCompleted" type="checkbox" v-model="hideCompleted" class="form-check-input" />
          <label for="hideCompleted" class="form-check-label font-weight-bold">
            Hide completed tasks
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      name: "Kathirr007",
      tasks: [],
      hideCompleted: true,
      newItemText: '',
    }
  },
  computed: {
    filteredTasks() {
      return this.hideCompleted ?
        this.tasks.filter(task => !task.done) : this.tasks;
    }
  },
  methods: {
    addNewTodo() {
      if(this.newItemText) {
        this.tasks.push({
          action: this.newItemText,
          done: false
        });
      }
      localStorage.setItem('todos', JSON.stringify(this.tasks));
      this.newItemText = '';
    }
  },
  created() {
    let todos = localStorage.getItem('todos');
    if (todos != null) {
      this.tasks = JSON.parse(todos);
    }
  },
}
</script>

<style lang="scss" scoped>
  input[type="checkbox"]{
    cursor: pointer;
    + label {
      cursor: pointer;
    }
  }
</style>
