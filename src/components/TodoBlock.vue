<script>
export default {
  data() {
    return {
      title: 'Todo',  
      todo: '',
      todos: [],
      isDone: false,
      id: 0,
    }
  },

  async mounted() {
    const data = await localStorage.getItem('todos')
    if (data) {
      this.todos = JSON.parse(data);
    }
  },

  methods: {
    addTodo() {
      if (this.todo != '') {
        this.todos.push({
          id: this.id,
          text: this.todo,
          isComplete: this.isDone,
        });
        localStorage.setItem('todos', JSON.stringify(this.todos))
      }
      this.todo = '';
    },
    // deleted(id) {
    //   this.todos = this.todos.filter(todo => todo.id !== id);
    // }
    removeTodo(id) {
      this.todos.splice(id, 1);
      localStorage.setItem('todos', JSON.stringify(this.todos))

        // this.todos = this.todos.filter(todo => todo.id !== id);
    },
    // isDone() {

    // }
  }
};
</script>

<template>
<h1 class="title"> {{ title }}</h1>
<div class="todo">
  <!-- <form v-on:submit.prevent="addTodo"> -->
  <input v-model="todo" type="text" placeholder="Text..." />
  <button v-on:click="addTodo(id++)">add todo</button>
  <div class="block__counter"> Кол-во залач на сегодня {{ todos.length }} </div>
  <hr>
  <div v-for="(todo, index ) in todos" :key="todo.id">
    <div class="todo__block">
      <span class="todo__id">{{ index + 1 }}. </span>
      <span class="todo__text" :class="{ todo__text_isShow: todo.isComplete }" @dblclick="removeTodo(index)">
        {{ todo.text }}
      </span>
      <input v-model="todo.isComplete" class="todo__check" type="checkbox">
    </div>
  </div>
  <!-- </form> -->
</div>
</template>

<style lang="scss">
.block__counter {
  padding: 5px 0px;
}
.todo {
  width: 300px;
  height: 100%;
  background-color: #fff2f2;
  padding: 30px;
  outline: 1px solid #000;
  min-height: 500px;

  &__block {
    padding: 5px 0px;
  }

  &__id {
  color: red;
  font-weight: bold;
  }

  &__text {
    font-size: 1rem;
    color: #444;
    text-transform: capitalize;
    cursor: pointer;

    &_isShow {
      color: rgb(23, 22, 22);
      text-decoration: line-through;
      cursor: pointer;
      }
  }
  &__check {
    display: inline-block;
    margin-left: 10px;
  }

}
</style>


