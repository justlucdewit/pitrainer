<template>
  <div id="app">
    <Displaybar :pi="pi"/>
    <div id="numpad">
      <div class="numpad-row">
        <Touchbutton label="7" @click.native="typeCharacter('7')"/>
        <Touchbutton label="8" @click.native="typeCharacter('8')"/>
        <Touchbutton label="9" @click.native="typeCharacter('9')"/>
      </div>

      <div class="numpad-row">
        <Touchbutton label="4" @click.native="typeCharacter('4')"/>
        <Touchbutton label="5" @click.native="typeCharacter('5')"/>
        <Touchbutton label="6" @click.native="typeCharacter('6')"/>
      </div>

      <div class="numpad-row">
        <Touchbutton label="1" @click.native="typeCharacter('1')"/>
        <Touchbutton label="2" @click.native="typeCharacter('2')"/>
        <Touchbutton label="3" @click.native="typeCharacter('3')"/>
      </div>

      <div class="numpad-row">
        <Touchbutton label="." @click.native="typeCharacter('.')"/>
        <Touchbutton label="0" @click.native="typeCharacter('0')"/>
        <Touchbutton label="reset" @click.native="reset()"/>
      </div>
    </div>
    <Result v-if="results" :digits="digits" :retry="retry" :startTime="started"/>
  </div>
</template>
<script>
import Displaybar from './components/Displaybar.vue'
import Touchbutton from './components/Touchbutton.vue'
import Result from './components/Result.vue'

export default {
  data(){
    return {
      realpi: "3.1415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679 8214808651328230664709384460955058223172535940812848111745028410270193852110555964462294895493038196 4428810975665933446128475648233786783165271201909145648566923460348610454326648213393607260249141273 7245870066063155881748815209209628292540917153643678925903600113305305488204665213841469519415116094 3305727036575959195309218611738193261179310511854807446237996274956735188575272489122793818301194912 9833673362440656643086021394946395224737190702179860943702770539217176293176752384674818467669405132 0005681271452635608277857713427577896091736371787214684409012249534301465495853710507922796892589235 4201995611212902196086403441815981362977477130996051870721134999999837297804995105973173281609631859 5024459455346908302642522308253344685035261931188171010003137838752886587533208381420617177669147303 5982534904287554687311595628638823537875937519577818577805321712268066130019278766111959092164201989",
      pi: "3.",
      digits: 2,
      results: false,
      started: new Date().getTime()
    }
  },

  methods: {
    retry(){
      this.results = false;
      this.digits = 2;
      this.pi = "3.";
      this.started = new Date().getTime();
    },

    reset(){
      if (!this.results){
        this.pi = "3.";
        this.digits = 2;
      }
    },

    typeCharacter(char=''){
      if (char == this.realpi[this.digits] && !this.results){
        this.digits++;
        this.pi += char;
      }else{
        this.results = true
      }
    },
  },

  mounted(){
    const allowed = new Set('.0123456789')

    window.addEventListener('keyup', ({ key }) => {
      if (allowed.has(key)) {
        this.typeCharacter(key)
      }
    });
  },

  name: 'App',

  components: {
    Displaybar,
    Touchbutton,
    Result
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Open+Sans|Roboto&display=swap');
  #app {
    font-family: 'Open Sans', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  *::selection { background: transparent; } 
  *::-moz-selection { background: transparent; }

  #numpad{
    margin-top: 5px;
  }

  .numpad-row {
    display: flex;
    justify-content: center;
  }
</style>
