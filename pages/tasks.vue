<template>
  <div>
    <h2>Tasks</h2>
    <form>
      <label id="taskIdLabel" for="taskId">Enter task #:</label>
      <input id="taskId" v-model="taskNumber" type="text"/>
      <button @click.prevent="submit">Submit</button>
    </form>
    <ul>
      <li v-for="task in tasks">{{task.id}}</li>
    </ul>
  </div>
</template>

<style>
  #taskIdLabel {
    padding-right: 5px;
  }
</style>

<script>
  export default {
    async asyncData ({ app }) {
      const tasks = await app.$axios.$get('http://localhost:53856/api/tasks')
      return { tasks }
    },
    data () {
      return {
        taskNumber: 0
      }
    },
    methods: {
      submit () {
        let newTask = { id: this.taskNumber }
        this.$axios.$post('http://localhost:53856/api/tasks', newTask).then((response) => {
          this.tasks.push(newTask)
        })
      }
    }
  }
</script>
