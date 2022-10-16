<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: {
    Game,
  },
};
</script>


<style>
body {
  font: 14px "Century Gothic", Futura, sans-serif;
  margin: 20px;
}
ol, ul {
  padding-left: 30px;
}
.board-row:after {
  clear: both;
  content: "";
  display: table;
}
.status {
  margin-bottom: 10px;
}
.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 8rem;
  font-weight: bold;
  line-height: 10rem;
  height: 10rem;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 10rem;
}
.square:focus {
  outline: none;
}
.kbd-navigation .square:focus {
  background: #ddd;
}
.game {
  display: flex;
  flex-direction: column;
}
.game-info {
  margin-left: 20px;
}
.game-info button{
  outline: none;
  border-radius: 5px;
}
.game-info button:hover{
  border-color: #666;
}
.move-on button{
  border-color: #000;
}
</style>