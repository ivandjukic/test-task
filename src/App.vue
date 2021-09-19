<template>
  <div id="content">
    <ItemsList :items="items" @loadMore="loadMore" />
  </div>
</template>

<script>
import ItemsList from './components/ItemsList.vue'

export default {
  name: 'App',
  components: {
    ItemsList
  },
  data() {
    return {
      page: 0,
      items: []
    }
  },
  beforeMount() {
    this.loadMore()
  },
  methods: {
    loadMore() {
     this.page ++;
     const results = this.range((this.page - 1) * 20 + 1, this.page * 20)
     this.items = [...this.items, ...results];
    },
    range(start, end) {
      return Array(end - start + 1).fill().map((_, idx) => `Item${start + idx}`)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #7fc7bb;
  height: 100vh;
  display: flex;
  justify-content: center;
}
#content {
  width: 600px;
  margin-top: 60px;
  display: flex;
  justify-content: center;
}
</style>
