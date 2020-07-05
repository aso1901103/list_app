<template>
    <div>
        <h1>{{msg}}</h1>
        <input type="text" v-model="input">
        <button v-on:click='doAct'>クリック</button>
    </div>
</template>

<script>
export default {
  name: 'Mylist',
  props: {
    msg: String,
  },
  data:function(){
    return {
      input: '',
    };
  },
  methods:{
      doAct(){
          this.$emit('result-event',this.input);
      }
  }
}
</script>