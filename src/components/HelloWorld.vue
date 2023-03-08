<script>
  import { ref, defineComponent } from 'vue'

  const count = ref(0);
  const message = ref("Hello world");
  const rawHtml = "change";
  message.value = 'changed';
  // const data =
  let id = 1;
  let newTodo = '';
export default defineComponent ({
  data(){
    return {
      count: 5,
      hideCompleted: false,
      todos: [
        { id: id++, text: 'Learn HTML', done: false },
        { id: id++, text: 'Learn HTML', done: true },
        { id: id++, text: 'Learn HTML', done: false }
      ]
    }
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted ? this.todos.filter((t) => !t.done) : this.todos;
    }
  },
  methods: {
    addFruit() {
      this.todos.push({ id: id++, text: this.newTodo, done: false })
      this.newTodo = '';
    },
    removeTodo(toda) {
      this.todos = this.todos.filter((t) => t !== toda);
    },
    // hideCompleted() {

    // }
  }
});
</script>

<template>
  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <h2>{{ message }}</h2>
    <p>Using text interpolation: {{ rawHtml }}</p>
    <p>Using v-html directive: <span v-html="rawHtml"></span></p>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
    <input v-model="newTodo" type="text">
    <button @click="addFruit()">new fruit</button> 
    <ul>
      <li v-for="toda in filteredTodos" :key="toda.id">
        <input type="checkbox" v-model="toda.done">
        <span :class="{ done : toda.done }">{{ toda.text }}</span>
        <button @click="removeTodo(toda)">X</button>
      </li>
      <button @click="hideCompleted = !hideCompleted">
        {{ hideCompleted ? 'Show all' : 'Hide completed' }}
      </button>
    </ul>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
.done {
  text-decoration: line-through;
}

</style>
