<template>
  <div id="app">
    <Header/>
    <List :list="getList()"/>
  </div>
</template>

<script>
import './App.css'
import Header from './components/Header.vue'
import List from './components/List'

export default {
  name: 'App',
  components: {
    Header,
    List
  }, 
  data() {
    return {
      list: [
        [
          {id: 0, description: 'hello'},
          {id: 2, description: 'hi'}
        ], 
        [
          {id: 1, description: 'haha'}
        ]
      ],
      currentList: 0,
      currentId: 0
    };
  },
  methods: {
    getList() {
      console.log(this.list[this.currentList]);
      return this.list[this.currentList];
    }
  }
}
</script>

