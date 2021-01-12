<template>
<div class="entry">
  
  <div class="main-entry">
    <div class="text-container">
      <p>
      {{item.text}}
      </p>
    </div>

    <div class="button-container">
      <button @click="$emit('remove', item)">X</button>
    </div>


  <div v-if="!subEntry" class="input-sub-entry-container">
    <input class="input-sub-entry" type="text" v-on:change="addEntry" autofocus>
  </div>

  <div class="sub-entries-container">
  <entry class="sub-entry"
    subEntry=true
    v-for="(item, index) in items"
    :item="item"
    :index="index"
    :key="item.id"
    :text="item.text"
    @remove="removeTodo"
  ></entry>
</div>
  </div>
</div>

</template>

<script>
let nextId = 1

const createTest = text => ({
  text,
  id: nextId++
  
})

export default {
  name: 'Entry',
  props: {
        text: String,
        item: Object,
        subEntry: Boolean
      
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.entry
{
  display: flex;
  flex-direction: column;
  width: 100%;
  padding-bottom: .5em;


  margin-bottom: 1em;
  border-radius: 5px;

  -webkit-box-shadow: 3px 3px 5px 1px rgba(13,39,80,0.16), -2px -2px 5px 1px #ffffff; 
box-shadow: 3px 3px 5px 1px rgba(13,39,80,0.16), -2px -2px 5px 1px #ffffff;
background: #E8eaec;
color: darkgray;

  align-items: center;
}

.sub-entries-container
{
  grid-column: 1/13;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  padding: 0em 0em;
  margin: 0em 0em;
  user-select: none;






}

.sub-entry
{
  grid-column: 1/13;
  padding: 0em;
  -webkit-box-shadow: none;
  box-shadow: none;
  border-bottom: lightgray 1px solid;
  margin-bottom: 0em;
  padding-bottom: 0em;
  

 
}

.main-entry
{
  display: grid;
  grid-template-columns: repeat(12,1fr);
  width: 100%;
}

.text-container
{
  grid-column: 1/12;
  padding: 0em .5em;
  width: 90%;
  height: 100%;
  overflow-wrap: break-word;
}

.button-container
{
  grid-column: 12/13;
  display: flex;
  justify-content: flex-end;
  align-items: flex-start;
  margin: .5em .5em 0em 0em;
  height: 100%;
}



button
{
  grid-column: 12/13;
  height: 1.5em;

    -webkit-box-shadow: 3px 3px 5px 1px rgba(13,39,80,0.16), -2px -2px 5px 1px #ffffff; 
  box-shadow: 3px 3px 5px 1px rgba(13,39,80,0.16), -2px -2px 5px 1px #ffffff;
  background: #E8eaec;
  border: none;
  border-radius: .25em;
  color: darkgray;
  cursor: pointer;
}

button:hover
{
  -webkit-box-shadow: none;
  box-shadow: none;
  border: 1px lightgrey solid;
  outline-color: #E8eaec;
}

.input-sub-entry-container
{

  grid-column: 1/13;
  display: flex;
  justify-content: center;
  justify-self: center;
  width: 98%;
  margin: 0em 0em;

  user-select: none;
}

.input-sub-entry {
  width: 100%;
  height: 30px;
  margin: 0em 0em;
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
