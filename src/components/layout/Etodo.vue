<template>
  <div class="Etodo">
  <h3>EtodoList (this one is online and todos are stored on firestore)</h3>
  <input placeholder="new todo" type="text" v-model="newTodo">
  <Button @click="addETodo(newTodo)">Add lodo</Button>
  <button @click="shuffle(todoList)">shuffle</button>
  <ul>
    <li v-for="(item, key) in todoList" :key="key"  class="list todoN">
    <span>{{item}}</span>
    <i class="material-icons" v-on:click="removeETodo(item)" >clear</i>
    </li>
  </ul>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import shuffle from '../../mixins/shuffleMixin'
export default {
  name: 'Etodo',
  mixins: [shuffle],
  data () {
    return {
      newTodo: null // string
    }
  },
  // TODO: create component toast to display all state 'success','error,'pending etc
  // TODO: add loader => before update => uodated to each dispatch call
  methods: {
    addETodo: function (newTodo) {
      this.$store.dispatch('addETodo', newTodo)
    },
    removeETodo: function (todo) {
      this.$store.dispatch('removeETodo', todo)
    }
  },
  mounted () {
    this.$store.dispatch('getETodos')
    // console.log(this.$store.getters.Users)
  },
  computed: {
    ...mapGetters({
      todoList: 'getTodolist'
    })
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Etodo{
  width:90%;
  border:1px solid yellow;
  margin:0 auto;
}
i{
  vertical-align:bottom;
  float:right;
}
.list{
  text-align:left;
  clear:both
}
.list span{
  padding-left:10px;
}
.todoN:nth-child(even){
  background-color:#efefef;

}
.todoN:nth-child(odd){
  background-color:#efe;

}
.done{
  background-color: #42b983
}

</style>
