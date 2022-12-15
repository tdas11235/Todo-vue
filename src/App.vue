<template>
  <div id="tab-group">
    <button @click="activeTab = 'AddTab'">Add Tab</button>
    <button @click="activeTab = 'SearchTab'">Search Tab</button>
    <button @click="activeTab = 'FilterTab'">Filter Tab</button>
  </div>
  <AddTab v-if="activeTab === 'AddTab'">
    <div class="main-container">
      <form @submit="handleSubmit($event)" class="add-form">
        <label for="add-todo">Type here to add Todo</label>
        <div>
          <input id="add-todo" type="text" v-model.lazy="addForm.name" />
          <button type="submit">Add</button>
        </div>
      </form>
      <div>
        <Card v-for="(todo, index) in todos" :key="index">
          <template v-slot:header>
            <h3 class="heading">{{ todo.name }}</h3>
          </template>
          <template v-slot:edit>
            <div v-if="todo.edit === true" class="edit">
              <form @submit="handleEdit($event, index)">
                <input type="text" v-model="name" />
                <button type="submit">Confirm Edit</button>
              </form>
            </div>
          </template>
          <template v-slot:default>
            <div v-if="todo.pending === true">Incomplete</div>
            <div v-else>Completed</div>
          </template>
          <template v-slot:footer>
            <div id="button-group">
              <button @click="todo.pending = false">Completed</button>
              <button @click="handleDelete(index)">Delete</button>
              <button @click="todo.edit = true">Edit</button>
            </div>
          </template>
        </Card>
      </div>
    </div>
  </AddTab>
  <SearchTab v-if="activeTab === 'SearchTab'" :filtered="todos" />
  <FilterTab v-if="activeTab === 'FilterTab'" :todos="todos" />
</template>

<script>
import Card from "./components/Card.vue";
import AddTab from "./components/AddTab.vue";
import SearchTab from "./components/SearchTab.vue";
import FilterTab from "./components/Filter.vue";

export default {
  name: "App",
  components: {
    Card,
    AddTab,
    SearchTab,
    FilterTab,
  },
  data() {
    return {
      addForm: {
        name: "",
        pending: true,
        edit: false,
      },
      name: "",
      todos: [],
      activeTab: "AddTab",
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      //console.log(this.name);
      //makes a shallow copy
      this.todos.push({ ...this.addForm });
      this.addForm.name = "";
    },
    handleDelete(index) {
      this.todos.splice(index, 1);
    },
    handleEdit(event, index) {
      event.preventDefault();
      this.todos[index].name = this.name;
      this.name = "";
      this.todos[index].edit = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.add-form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

button {
  margin: 15px;
}

button [type="submit"] {
  margin-left: 15px;
  margin-top: 15px;
  margin-bottom: 15px;
}

#button-group {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-bottom: 10px;
}
.heading {
  text-transform: uppercase;
}
.edit {
  margin: 15px;
}
input[type="text"],
textarea,
select {
  width: 400px;
  margin-top: 2px;
  margin-bottom: 20px;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  color: #555;
  background-color: #fff;
  background-image: none;
}
</style>
