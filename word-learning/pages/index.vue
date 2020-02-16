<template>
  <main class="backcolor flex2">
    <div id="ch" class="item1 flex">
      <div class="theme item1">
        <p>見習い魔女、</p>
        <p>初めてのおつかい編</p>
      </div>
      <div class="item2">
        <img src="~/assets/chara.png" alt="">
      </div>
    </div>
    <div class="flex item2">
      <div class="center">
        <button class="button-img" v-on:click="$router.push('/battle')">初級</button>
      </div>
      <div class="center">
        <button class="button-img" v-on:click="$router.push('/battle2')">中級</button>
      </div>
      <div class="center">
        <button class="button-img" v-on:click="$router.push('/battle3')">上級</button>
      </div>
    </div>
  </main>
</template>

<script>
import anime from 'animejs'

export default {
  name: 'app',

  beforeRouteEnter(to, from, next) {
    next(vm => {
      vm.initialize();
      next();
    });
  },
  data () {
    return {

    }
  },

  methods: {
    initialize: function () {
      anime.timeline()
          .add({
            targets: '#ch',
            translateX: 50,
      })
    }
  }
}
</script>

<style>
button{
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  padding: 0;
  appearance: none;
}
p {
  font-family: Times New Roman;
}
.center {
  text-align: center;
}
.backcolor {
  background-image: url("~@/assets/mori01.jpg");
  background-size: cover;
  height: 100vh;
  width: 100vw;
}
.button-img {
  background-image: url("~@/assets/004.png");
  background-size: 20vw 12vh;
  width: 20vw;
  height: 12vh;
  font-size: 1.2em;
  color: chartreuse;
}
.flex {
  display: flex;
  justify-content: space-around;
  flex-direction: column;
}
.flex2 {
  display: flex;
  flex-direction: row;
}
.item1 {
  flex: 1;
  margin-left: 10%;
}
.item2 {
  flex: 2;
}
.theme {
  margin-top: 10%;
  font-size: 2.2em;
  font-weight: bold;
  color: rgb(255, 208, 0);

}
</style>

