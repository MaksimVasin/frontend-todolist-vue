<template>
  <li>
    <span class="title index">
      <input type="checkbox" v-on:change="todo.completed=!todo.completed">
      <strong>{{ index + 1 }}</strong>
    </span>
    <span class="title" v-bind:class="{done: todo.completed}">{{ uppercase(todo.title) }}</span>
    <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  computed:{
    uppercase(){
      return (value)=>{
        return value[0].toUpperCase() + value.slice(1);
      }
    }
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #000;
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 2rem;
    margin-bottom: 1rem;
  }

  .rm {
    color: #fff;
    background-color: rgb(219, 0, 0);
    border: none;
    border-radius: 50%;
    font-weight: bold;
    font-size: 1.2rem;
    max-height: 1.5rem;

    transition: all .2s linear;
  }

  .rm:hover {
    background-color: rgb(179, 0, 0);
    cursor: pointer;
  }

  .done {
    text-decoration: line-through;
    font-weight: normal;
    color: rgb(139, 139, 139);
  }

  input {
    margin-right: 1rem;
  }

  .title {
    padding-top: 0.15rem;
    padding-right: 1rem;
    font-weight: bold;
  }

  .index {
    min-width: 3rem;
  }
</style>
