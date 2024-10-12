<template>
  <form>
    <input type="text" placeholder="Search for a cryptocurrency" />
  </form>
</template>

<script setup></script>

<style lang="css" scoped>
form {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 20px;
  height: 100px;
  width: 100vw;
  background-color: #011b0f;
  position: absolute;
  top:0;
}
input {
    display: block;
    width: 700px;
    max-width: 700px;
    height: 70px;
    margin: 0 20px 0 0;
    padding: 0;
    background-color:#f0f0f0;
    color: #011b0f;
    background-image: url("../assets/icons/search.svg") ;
    background-repeat: no-repeat;
    background-position: right 20px center;
    background-size: 37.5px 37.5px;
    border-radius: 25px;
    font-size: 16px;
    border: none;
    padding-left: 20px;
    
}
input::placeholder {
    color: #011b0f;
    font-size: 16px;
    
}
</style>
