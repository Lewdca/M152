<template>
  <router-view />
</template>

<style lang="scss">
.grid-container {
  display: grid;
  grid-template-columns: auto;
  padding: 10px;
}

.grid-top-container {
  display: grid;
  grid-template-columns: auto auto;
  padding: 10px;
}

.flex-container {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: nowrap;
}

.flex-container > div {
  text-align: center;
  margin-bottom: 50px;
}

.grid-item {
  margin-bottom: 20px;
  background-color: #d4d6d4;
}

body{
  background-color: #e3e6e3;
}


@media only screen and (max-width: 680px) {
  .flex-container{
    flex-direction: column;
    margin-bottom: 20px;
  }
}

@import'~bootstrap/dist/css/bootstrap.css'
</style>
