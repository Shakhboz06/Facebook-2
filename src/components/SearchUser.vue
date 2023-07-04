<template>
  <div id="search">
    <input type="text" placeholder="Name" @keyup="SearchUser()"/>
    <button @click="Clear()">Clear</button>
  </div>
</template>

<script>
export default {
  data(){
    return{
    inputValue: "",

    }
  },
  methods:{
    SearchUser: function(){
       this.$emit("Search", this.inputValue)
    },
  }
  
};
</script>

<style>
#search{
  display: flex;
  justify-content: center;
  align-items: center;
  grid-gap: 20px;
  transition: 0.3s ease;
}
#search:hover{
   transform: scale(1.025);
}
#search input{
  width: 230px;
  height: 30px;
  border: 2px solid blue;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 700;
  padding: 0 10px;
}
input:focus {
  outline-offset: 0.7px;
  outline: 1px solid #007fff;
  border: 1px solid #007fff !important;
}
#search button{
  width: 120px;
  height: 35px;
  font-size: 16px;
  font-family: inherit;
  background-color: blue;
  color: #fff;
  font-weight: 700;
  border: 1px solid blue;
  border-radius: 10px;
}
</style>
