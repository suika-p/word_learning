<template>
  <main class="backcolor block">
    <div class="flexbox center paddingtop10">
      <section class="flexitem">
        <img class="monster" v-bind:src="img_list[img_ind]" alt="">
      </section>
    </div>
    <div class="mespad text-image">
      <img src="~/assets/mes.png" alt="">
      <p class="mesfont monster">{{ja_word[tmp_ind]}}</p>
    </div>
    <div class="text-image">
      <img src="~/assets/mesinput.png" alt="">
      <input v-model="myText" v-on:keyup.enter="confirmWord" class="inputfont">
    </div>
    <section class="flexbox2">
      <div class="paddingleft10">
        <img v-for="(_, key) in myPoint" :key="key" src="~/assets/heart.png">
      </div>
    </section>
    <p id="over" style="z-index:-1" v-on:click="$router.push('/')">{{gameover}}</p>
    <p id="over2" style="z-index:-1" v-on:click="$router.push('/')">クリックでタイトルへ戻る</p>
    <p id="money">Score: {{moneyP}}G</p>
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
      en_word: [
        "point out", "work out", "have something in mind", "as to", "so far", "to some/extent", 
        "look forward to", "follow up on", "in general", "make sence"
      ],
      ja_word: [
        "〜を指し示す", "〜を解決する", "何か考えがある", "〜については", "今までのところ", "ある程度は",
         "〜を楽しみにする", "〜を実施する", "一般に",
        "意味を成す",
      ],
      img_list: [
        require("~/assets/mon01.png"), 
        require("~/assets/mon02.png"), require("~/assets/mon03.png"), require("~/assets/mon04.png"), 
        require("~/assets/mon05.png"), require("~/assets/mon06.png"), require("~/assets/mon07.png"),
      ],
      tmp_ind: 0,
      img_ind: 0,
      myText: "",
      myPoint: 3,
      moneyP: 0,
      gameover: "GAME OVER",
    }
  },

  methods: {
    chind: function (i) {
      this.tmp_ind = i;
    },
    separate: function (str) {
      var s = "";
      var hako = [];
      for (var i = 0; i < str.length; i++) {
        if (str[i] == ' ' && s != "") {
          hako.push(s);
          s = "";
        } else {
          if (str[i] != ' ') s += str[i];
        }
      }
      if (s != "") hako.push(s);
      return hako;
    },
    confirmWord: function () {
      if (this.myPoint <= 0) {
        return;
      }
      var enword_list = this.separate(this.en_word[this.tmp_ind]);
      var myText_list = this.separate(this.myText);
      var flag = true;
      for (var i = 0; i < enword_list.length; i++) {
        if (enword_list[i] != myText_list[i]) {
          var hint = "";
          for (var j = 0; j <= i; j++) {
            hint += enword_list[j];
            hint += ' ';
          }
          this.myText = hint;
          flag = false;
          if (this.myPoint <= 1) {
            this.myPoint--;
            anime.timeline()
              .add({
                targets: ["#over", "#over2"],
                opacity: 1,
            }) 
            over.style.zIndex = 0;
            over2.style.zIndex = 0;
            break;
          }
          this.myPoint--;
          break;
        }
      }
      if (flag) {
        anime.timeline()
          .add({
            targets: ".monster",
            opacity: 0,
            duration: 500,
          }) 
          .add({
            targets: ".monster",
            opacity: 1,
            duration: 2000,
          })  
        this.myText = "";
        this.search();
        var ind = Math.floor( Math.random() * this.img_list.length);
        this.img_ind = ind;
        this.moneyP += 200;
      }
      return 0;
    },
    search: function () {
      var ind = Math.floor( Math.random() * this.ja_word.length);
      this.chind(ind);
    },

    initialize: function () {
      var ind = Math.floor( Math.random() * this.ja_word.length);
      this.chind(ind);
      ind = Math.floor( Math.random() * this.img_list.length);
      this.img_ind = ind;
      
    }
  }
}
</script>

<style>

p {
  font-family: Times New Roman;
}
.backcolor {
  background-image: url("~@/assets/mori01.jpg");
  background-size: cover;
  height: 100vh;
}
.block {
  display: block;
}
.flexbox {
  display: flex;
  justify-content: space-around;
}
.flexbox2 {
  display: flex;
}

.flexitem {
  flex-grow: 2;
}
.center {
  text-align: center;
}
.mespad {
  padding-top: 3%;
  padding-bottom: 5%;
}
.text-image {
  position: relative;
  text-align: center;
}

.mesfont {
  position: absolute;
  top: 27%;
  left: 42%;
  font-size: 2em;
  font-style: italic;
  color: #df0a0a;
}
.inputfont {
  position: absolute;
  top: 30%;
  left: 28%;
  font-size: 4em;
  font-style: italic;
  color: #df950a;
  border:none;
  background:none;
}
.paddingtop10 {
  padding-top: 5%;
}
.paddingleft10 {
  padding-left: 10%;
}
#over {
  position: absolute;
  left: 35%;
  top: 40%;
  opacity: 0;
  font-size: 5em;
  color: #df0a0a;
  cursor : pointer;
}
#over2 {
  position: absolute;
  left: 40%;
  top: 55%;
  opacity: 0;
  font-size: 1.5em;
  color: #df350a;
  cursor : pointer;
}
#money {
  position: absolute;
  font-size: 3.5em;
  color: #e2fa07;
  left: 5%;
  top: 0%;
}
</style>

