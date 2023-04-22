<template>
  <div>
    <div class="introduction">
      <div class="logo">
        <img src="../assets/logo.png">
      </div>
      <div class="attention_title">TIPS:</div>
      <div class="text">1.将要分析的程序输入最左边的框内<br>2.点击下方箭头得到输出和符号表<br>3.点击下方“×”可清空输入框
      </div>
    </div>
    <div class="title">
      <div class="title_1">输入guess.in</div>
      <div class="title_x">
        <img src="@/assets/images/off.png" @click="inputClear()" value="清空input输入框">
      </div>
      <div class="title_blank"></div>
      <div class="title_1">输出guess.out</div>
      <div class="title_1">符号表guess.sym</div>
    </div>
    <div class="contents">
      <div class="inputbox_content">
        <textarea id="inputbox_primary" v-model="inputtext" placeholder="请在此处输入源程序" cols="20"
          class="inputbox_text"></textarea>
      </div>
      <div class="running">
        <img src="@/assets/images/running.png" class="play" @click="motivate()">
      </div>
      <div class="outputbox_content">
        <div class="outputbox_text">
          <textarea id="outputbox_primary" v-model="outputtext" cols="20" readonly class="outputbox_text"></textarea>
        </div>
      </div>
      <div class="guessbox_content">
        <div class="guessbox_text">
          <textarea id="guessbox_primary" v-model="guesstext" cols="20" readonly class="guessbox_text"></textarea>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="js">
import axios from 'axios'
export default {
  name: 'hello',
  data() {
    return {
      inputtext: "",//输入
      guesstext: "",//输出
      outputtext: ""//符号表
    };
  },
  methods: {
    motivate() {
      window.console.log(this.inputtext)
      if (this.inputtext == "") {
        alert("您还未填入要分析的程序，请在左框内填入后再次点击此按钮。")
      }
      else {
        var string = this.inputtext;
        axios({
          url: "http://localhost:8080/analyzer",
          data: { string },
          method: "POST",
          headers: {
            'Content-Type': 'application/json'
          }
        }).then(res => {
          console.log(res.data);
          console.log('POST请求成功');
        })

        alert("已生成输出和符号表。")
      }
    },
    inputClear() {
      this.inputtext = JSON.stringify(this.inputtext);
    },
  },
  components: {

  }


}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
body {
  height: 100%;
}

.introduction {

  width: 100%;
  height: 120px;
  background-color: rgba(0, 0, 0, 0.244);

}

.logo {
  padding-left: 15px;
  padding-top: 10px;
  height: 110px;
  float: left;
}

.attention_title {
  font-family: HarmonyOS;
  font-size: 50px;
  float: left;
  width: 100px;
  padding: 20px;
}

.text {
  float: left;
  height: 100px;
  font-family: MaiYuan;
  font-size: 30px;

  text-align: center;
  vertical-align: middle;
  padding-left: 30px;
  padding-top: 15px;
}

.title {
  width: 100%;
  height: 50px;
  background-color: rgba(188, 182, 182, 0.244);
}

.title_1 {
  width: 28%;
  height: 50px;
  background-color: rgba(222, 218, 218, 0.244);
  float: left;
  text-align: center;
  font-family: MaiYuan;
  font-size: 30px;
  border-radius: 10%;
  border: 5px dashed rgba(70, 68, 68, 0.244);
  background:
    linear-gradient(to top, rgba(188, 182, 182, 0.244), 10px, transparent 10px),
    linear-gradient(to right, rgba(188, 182, 182, 0.244), 10px, transparent 10px),
    linear-gradient(to bottom, rgba(188, 182, 182, 0.244), 10px, transparent 10px),
    linear-gradient(to left, rgba(188, 182, 182, 0.244), 10px, transparent 10px);
  background-origin: border-box;

}

.title_x {
  height: 50px;
  float: left;
  width: auto;
  border: 5px dashed rgba(70, 68, 68, 0.244);
}

.title_blank {
  width: 8%;
  height: 50px;
  float: left;

}

.contents {
  padding-top: 15px;
  width: 100%;
  height: 620px;
  background-color: rgba(188, 182, 182, 0.244);

}



.inputbox_content {
  float: left;
  width: 29%;
  height: 600px;
  background-color: rgba(245, 242, 242, 0.796);
  border-top: 1px solid #ffffff;
  box-shadow: darkgrey 10px 10px 30px 5px; //边框阴影
}


.inputbox_text {
  height: 600px;
  width: 100%;
  background-color: rgba(245, 242, 242, 0.796);
}

.running {
  float: left;
  width: 11%;
  height: 600px;
}

.play {
  padding-top: 210px;
  padding-left: 20px;
  float: left;
  vertical-align: middle;
  -webkit-transform: perspective(1px) translateZ(0);
  transform: perspective(1px) translateZ(0);
  box-shadow: 0 0 1px rgba(0, 0, 0, 0);
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: box-shadow, transform;
  transition-property: box-shadow, transform;

}

.play:hover,
.play:focus,
.play:active {
  box-shadow: 0 10px 10px -10px rgba(0, 0, 0, 0.5);
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

.outputbox_content {
  float: left;
  width: 30%;
  height: 600px;
  background-color: rgba(245, 242, 242, 0.796);
  border-top: 1px solid #ffffff;
  box-shadow: darkgrey 10px 10px 30px 5px; //边框阴影
}

.outputbox_content::-webkit-scrollbar {
  background-color: #f8f8f800;
}

.outputbox_content::-webkit-scrollbar-thumb {
  background-color: #bebebe;
  border-radius: 100px;
}

.outputbox_content::-webkit-scrollbar-thumb:hover {
  background-color: #bbb;
}

.outputbox_content::-webkit-scrollbar-corner {
  background-color: rgba(255, 255, 255, 0);
}


.outputbox_text {
  height: 600px;
  width: 100%;
  background-color: rgba(245, 242, 242, 0.796);
}

.guessbox_content {
  float: left;
  width: 30%;
  height: 600px;
  background-color: rgba(245, 242, 242, 0.796);
  border-top: 1px solid #ffffff;
  box-shadow: darkgrey 10px 10px 30px 5px; //边框阴影
}

.guessbox_content::-webkit-scrollbar {
  background-color: #f8f8f800;
}

.guessbox_content::-webkit-scrollbar-thumb {
  background-color: #bebebe;
  border-radius: 100px;
}

.guessbox_content::-webkit-scrollbar-thumb:hover {
  background-color: #bbb;
}

.guessbox_content::-webkit-scrollbar-corner {
  background-color: rgba(255, 255, 255, 0);
}


.guessbox_text {
  height: 600px;
  width: 100%;
  background-color: rgba(245, 242, 242, 0.796);
}
</style>
