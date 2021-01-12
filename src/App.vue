<template>
<div class="input-entry-container">
  <input class="input-entry" type="text" v-on:change="addEntry" autofocus>
</div>

<div class="entries-container">
  <entry
    v-for="(item, index) in items"
    :item="item"
    :index="index"
    :key="item.id"
    :text="item.text"
    @remove="removeTodo"
  ></entry>
</div>

</template>

<script>
import Entry from './components/Entry'

let nextId = 1

const createTest = text => ({
  text,
  id: nextId++
  
})

export default {
  name: 'App',
  components: {
    Entry
  },
  data(){
    return{
      items: []
    }
  },
  methods: {
    addEntry(event){
      this.items.push(createTest(event.target.value))
      event.target.value = "";
    },
    
    removeTodo(e) {
      this.items = this.items.filter(item => item.id != e.id)
      
    }
  }
}
</script>

<style>
body
{
  background: #E8eaec;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;


  margin: auto;
  margin-top: 2em;
  justify-content: center;

  width: 500px;
  box-sizing: border-box;
  padding: 1em;


  border-radius: 2em;


background: #E8eaec;





}

.entries-container
{

  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  padding: 2em 0em;
  user-select: none;

}

.input-entry-container
{

  grid-column: 2/12;
  width: 100%;
  display: flex;
  justify-content: center;
  user-select: none;
}

.input-entry {
  width: 100%;
  height: 30px;

  background: lightgrey;
  border: none;
  border-radius: .5em;
  color: darkgrey;
  font-style: italic;
  outline: none;
  user-select: all;

-webkit-box-shadow: inset -3px -3px 4px 1px rgba(255,255,255,0.64), inset 2px 2px 4px 1px rgba(13,39,80,0.16); 
box-shadow: inset -3px -3px 4px 1px rgba(255,255,255,0.64), inset 2px 2px 4px 1px rgba(13,39,80,0.16);
background: #E8eaec;
}
</style>
