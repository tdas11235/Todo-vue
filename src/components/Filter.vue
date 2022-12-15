<template>
  <div>
    <h1>Filter Component</h1>
    <div>
      <form @submit="handleSubmit($event)">
        <label for="filter">Filter Options</label>
        <select id="filter" v-model="filterValue">
          <option value="completed">Completed</option>
          <option value="pending">Pending</option>
        </select>
        <button type="submit">Apply Filter</button>
      </form>
    </div>
    <Card v-for="(todo, index) in array" :key="index">
      <template v-slot:header>
        <h3 class="heading">{{ todo.name }}</h3>
      </template>
      <template v-slot:default>
        <div v-if="todo.pending === true" id="status">Status: Incomplete</div>
        <div v-else id="status">Status: Completed</div>
      </template>
    </Card>
  </div>
</template>

<script>
import Card from "./Card.vue";

export default {
  name: "FiterComp",
  props: ["todos"],
  components: {
    Card,
  },
  data() {
    return {
      filterValue: "",
      array: this.todos,
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      if (this.filterValue === "pending") {
        this.array = this.todos.filter((todo) => todo.pending === true);
      } else {
        this.array = this.todos.filter((todo) => todo.pending === false);
      }
    },
  },
};
</script>

<style scoped>
#status {
  margin: 10px;
  margin-bottom: 20px;
}
</style>