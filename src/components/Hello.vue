<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Todo List</h2>
    <p v-if="items.length === 0">No item</p>
    <ul>
      <li v-for="item in items" :key="item">{{item}} - <a href="#" v-on:click="removeItem(item)">remove</a></li>
    </ul>

    <input type="text" v-model="item">
    <input type="button" value="Add item" v-on:click="addItem">
   
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Todo App',
      items: [],
      item: ''
    }
  },
  methods: {
    addItem(){
      this.items.push(this.item)
      localStorage.setItem('items', JSON.stringify(this.items))
      this.item = ''
    },
    removeItem(item){
      const index = this.items.indexOf(item)
      this.items.splice(index, 1)
      localStorage.setItem('items', JSON.stringify(this.items))
    }
  },
  created(){
    this.items = JSON.parse(localStorage.getItem('items')) || []
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}

a {
  color: #35495E;
}
</style>
