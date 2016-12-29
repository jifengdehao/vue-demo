<template>
		<div id="first">
				{{msg}}
				<p>{{msgfromfather}}</p>				
				<a href="javascrpt:;" v-on:click='dosomething()'>弹出</a>
				<button v-on:click='onClickme'>click!</button>
		</div>
</template>

<script>

export default {
  name: 'first',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
    }
  },
  props:['msgfromfather'],
  methods:{
  	dosomething:function(){
  		alert(1230);
  	},
  	onClickme:function(){
  		console.log(this.msgfromfather);
  		this.$emit('child-tell-me-something',this.msg);
  		
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	#first{
		color:red;
	}
</style>
