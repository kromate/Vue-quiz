<template>
  <div>
    <nav>
      <ul>
        <li class="nav-item"> <b> Just a Quiz App</b></li>
        <li class="nav-item counter"> <b>Counter: {{numCorrect}}/{{numTotal}}</b> </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
name:'Header',
props:[
  'numCorrect',
  'numTotal'
]
}
</script>

<style scoped>
.counter{
color: grey;
}
nav{
  display: flex;
  float: left;
}
ul{
  list-style: none;
  display: flex;

}
b{
  font-size: 20px;
}
li{
  margin: 0px 10px;
}
</style>