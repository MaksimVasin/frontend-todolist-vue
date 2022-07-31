<template>
  <form @submit.prevent="onSubmit">
    <input type="text" placeholder="Todo item" v-model="title">
    <button type="submit">+</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: ''
    }
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        }

        this.$emit('add-todo', newTodo)
        this.title=''
      }
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
    margin-bottom: 1rem;
    position: relative;
  }

  input {
    width: 100%;
    padding: 0.5rem 5rem 0.5rem 2rem;
    border: 1px solid rgb(0, 0, 0);
    outline: none;
    font-size: 1.2rem;
  }

  input:focus {
    outline: 1px solid rgb(0, 182, 30);
  }

  button {
    width: 2rem;
    height: 2rem;
    font-size: 1.5rem;
    font-weight: bold;
    color: #fff;
    background-color: rgb(0, 182, 30);
    border: none;
    border-radius: 50%;

    position: absolute;
    right: 1.75rem;
    top: 0.25rem;

    transition: background-color .3s linear;
  }

  button:hover {
    background-color: rgb(0, 145, 24);
    cursor: pointer;
  }

</style>