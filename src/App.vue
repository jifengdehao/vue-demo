<template>
  <div id="app">
  	<h1>{{title}}</h1>
  	<input v-model="newItem"  v-on:keyup.enter="addNew"/>
  	<ul>
  		<li v-for='item in items' v-bind:class='{finished :item.isFinished}' v-on:click="toggleFinish(item)">{{item.label}}</li>
  	</ul>
  	<hello></hello>
  	<p>child tells me: {{ childWorld }}</p>
  	<first msgfromfather="msg from father" v-on:child-tell-me-something='listenToMyBoy'></first>
  </div>
</template>

<script>
import Hello from './components/Hello'
import First from './components/First'
import Store from './store'
//console.log(Store);
export default {
  name: 'app',
  components: {
    Hello,First
  },
  data(){
  	return{
  			title:"this is a todo list",
  			items:Store.fetch(),
  			newItem:'',
  			childWorld:''
  	}
  },
  watch:{
  	items:{
  		handler:function(items){
  			Store.save(items);
  		},
  		deep:true
  	}
  },
  methods:{
			toggleFinish:function(item){
		  		item.isFinished = ! item.isFinished;
		  },
		  addNew:function(){
		  	this.items.push({
		  		label:this.newItem,
  				isFinished:false
		  	})
		  	this.newItem="";  	
		  },	  
		  listenToMyBoy:function(msg){
  			this.childWorld=msg;
  		}
  
  }
  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul{
	list-style-type: none;
	padding: 0;
	margin: 0;
}
.finished{
	text-decoration: underline;
}
</style>
