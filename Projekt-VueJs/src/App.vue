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

.form-popup {
  display: none;
  position: fixed;
  bottom: 0;
  right: 15px;
  border: 3px solid #f1f1f1;
  z-index: 9;
}

.form-container {
  max-width: 300px;
  padding: 10px;
  background-color: white;
}

.form-container input[type=text], .form-container input[type=password] {
  width: 100%;
  padding: 15px;
  margin: 5px 0 22px 0;
  border: none;
  background: #f1f1f1;
}

.form-container input[type=text]:focus, .form-container input[type=password]:focus {
  background-color: #ddd;
  outline: none;
}

.form-container .btn {
  background-color: #04AA6D;
  color: white;
  border: none;
  margin-bottom:10px;
}

.form-container .cancel {
  background-color: red;
}

.form-container .btn:hover, .open-button:hover {
  opacity: 1;
}


@media only screen and (max-width: 680px) {
  .flex-container{
    flex-direction: column;
    margin-bottom: 20px;
  }
}

@import'~bootstrap/dist/css/bootstrap.css'
</style>
