<template>
  <div id="app">
    <Menu />
    <router-view/>
  </div>
</template>

<script>
import Menu from "./components/Menu";
export default {
  components: {Menu}
}
</script>


<style lang="scss">
@font-face {
    font-family: "Bahnschrift";
    src: url("/font/Bahnschrift.ttf") format("truetype"),
    url(/font/Bahnschrift.ttf) format("woff");
  }
html, body {

  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

div {
  box-sizing: border-box;
}

button {
  font-family: Bahnschrift, Helvetica, Arial, sans-serif;
  cursor: pointer;
  background: none;
  border: none;
}

h1,h2,h3,h4,h5,p {
  margin: 0;
  padding: 0;
}

#app {
  @font-face {
    font-family: "Bahnschrift";
    src: url("/font/Bahnschrift.ttf") format("truetype"),
    url(/font/Bahnschrift.ttf) format("woff");
  }
  font-family: Bahnschrift;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: start;
  color: #000;
  background: #F6F5FA;
  width: 100%;
  display: flex;

}

.flex_row {
  display: flex;
  align-items: center;
}

</style>
