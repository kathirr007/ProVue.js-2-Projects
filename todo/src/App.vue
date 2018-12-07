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
      tasks: [
        {action: "Buy Vegetables", done: true},
        {action: "Buy Medicines", done: false},
        {action: "Buy Books", done: true},
        {action: "Driving class training", done: false},
        {action: "Cook Non-veg", done: false}
      ],
      hideCompleted: true,
    }
  },
  computed: {
    filteredTasks() {
      return this.hideCompleted ?
        this.tasks.filter(task => !task.done) : this.tasks;
    }
  }
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
