<template>
<header>
  <router-link to="/">
    <h1><span>What</span>Movie</h1>
  </router-link>
</header>
<main>
  <router-view/>
</main>
    
</template>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

body {
  background-color: darkslateblue;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color:darkslateblue;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
}

span {
    color: #8b0000;
    font-size: 28px;
  }
h1 {
    color: #fff;
    font-size: 28px;
  }
</style>
