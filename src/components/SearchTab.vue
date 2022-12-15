<template>
  <div class="search-element">
    <label for="search">Type here to Search</label>
    <input
      type="text"
      placeholder="Search"
      v-model="search"
      @input="handleChange($event)"
    />
  </div>
  <div>
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
  name: "SearchTab",
  props: ["filtered"],
  components: {
    Card,
  },
  data() {
    return {
      search: "",
      array: this.filtered,
    };
  },
  methods: {
    handleChange(event) {
      this.array = this.filtered.filter((todo) =>
        todo.name.includes(event.target.value)
      );
    },
  },
};
</script>

<style scoped>
.search-element {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  margin: 15px;
}

#status {
  margin: 10px;
  margin-bottom: 20px;
}
</style>