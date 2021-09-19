<template>
  <div id="container">
    <h1>Items:</h1>
    <button @click="toggleShowList">
      {{ showList? 'Hide list' : 'Show list' }} 
    </button>
    <div id="listWrapper">
      <ul id="list">
        <li v-for="(item, index) in items" :key={index}>
          {{item}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemsList',
  props: {
    items: Array
  },
  data() {
    return {
      showList: false
    }
  },
  methods: {
    toggleShowList() {
     this.showList = !this.showList
    },
    listEndReachedHandler() {
      this.$emit('loadMore');
    }
  },
  mounted() {
    const listWrapper = document.querySelector('#list');
     listWrapper.addEventListener('scroll', () => {
      if(listWrapper.scrollTop + listWrapper.clientHeight >= listWrapper.scrollHeight) {
        this.listEndReachedHandler()
      }
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#container {
  width: 100%;
}
#listWrapper {
  padding: 0 32px;
}
ul {
  overflow: auto;
  height: 500px;
  border: 2px solid #dce4ec;
  border-radius: 5px;
  margin-top: 20px;
  padding: 0;
  list-style: none;
}
li {
  border: 1px solid gray;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
}
a {
  color: #42b983;
}
</style>
