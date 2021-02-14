<template>
<div>  
  <p>
    My name is <input v-model="name">
    and I am <input v-model="age"> years old.
  </p>
  <p>
    <button @click="persist">Save</button>
  </p>
</div>
</template>



<script>
export default {
    data() {
        return {
            name: '',
            age: 0,
        }
    },
    mounted() {
      if (localStorage.name) {
        this.name = localStorage.name;
      }
      if(localStorage.age){
          this.age = localStorage.age;
      }
    },
    methods:{
        persist(){
            localStorage.name = this.name;
            localStorage.age = this.age;
            console.log('now pretend I did more stuff...');

        }
    }
}
</script>



<style lang="scss">

</style>