<template>
  <div class="body">
    <h1 class="NamePage">Конвертер валют</h1>
    <input class="inputpole" v-model="inputed1" placeholder="0">
    <select class="select1" v-model="selectedval1">
      <option v-for="c in countries" v-bind:value="c">{{ c }}</option>
    </select>
    <span v-if="selectedval1!==null">{{ changeval1(selectedval1) }}</span>
    <img src="@/assets/Swap.png" class="buttonswap"/>
    <button class="buttonswap" @click="buttonswap()"></button>
    <output class="outputpole">{{ outputed }}</output>
    <select class="select2" v-model="selectedval2">
      <option v-for="c in countries" v-bind:value="c">{{ c }}</option>
    </select>
    <span v-if="selectedval2!==null">{{ changeval2(selectedval2) }}</span>
    <button class="buttongotopage1" @click="$emit('changePage2')">Перейти к таблице</button>
  </div>
</template>

<script>
export default {
  name: "PageConverter",
  props: ['valute', 'countries'],
  data() {
    return {
      inputed1: "",
      inputed2: "",
      outputed: "",
      selectedval1: 'RUB',
      selectedval2: 'USD',
      selected: ['RUB', 'USD'],
    }
  },

  watch: {
    inputed1: function () {
      if (this.inputed1 !== this.inputed2) {
        if (this.inputed1 === "") {
          this.outputed = ""
        } else if (this.inputed1 > 0 && this.inputed1[0] > 0 && this.inputed1[0] < 10) {
          this.result();
        } else {
          this.outputed = NaN
        }
        this.inputed2 = this.inputed1
      }
      if (this.inputed1.length > 20) {
        this.inputed1 = "У Вас столько нет)))"
      }

    },
  },

  methods: {
    changeval1(val) {
      if (val !== this.selected[0]) {
        this.selected[0] = val;
        if (this.inputed1 === "") {
          this.outputed = ""
        } else {
          this.result();
        }
      }
    },
    changeval2(val) {
      if (val !== this.selected[1]) {
        this.selected[1] = val;
      }
      this.result();
    },
    result() {
      let select1 = this.valute[this.selected[0]];
      let num1;
      let num2;
      let select1v;
      let select2v;
      if (select1 === undefined) {
        select1v = 1
        num1=1;
      } else {
        select1v = this.valute[this.selected[0]].Value;
        num1=this.valute[this.selected[0]].Nominal;
      }
      let select2 = this.valute[this.selected[1]];
      if (select2 === undefined) {
        select2v = 1
        num2=1
      } else {
        select2v = this.valute[this.selected[1]].Value;
        num2=this.valute[this.selected[1]].Nominal;
      }
      let inp = this.inputed1;
      this.outputed = Math.floor((inp*select1v*num2) / (select2v*num1) * 100) / 100
      this.inputed2 = this.inputed1;
    },
    buttonswap() {
      let tmp = this.selected[0];
      this.selectedval1 = this.selected[1];
      this.changeval1(this.selected[1])
      this.changeval2(tmp)
      this.selectedval2 = tmp;
    },
  }
}
</script>

<style scoped>

.body {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background: radial-gradient(122.19% 312.8% at 55.59% 50%, rgba(16, 111, 19, 0.5) 0%, rgba(209, 212, 20, 0.37) 100%);
}

.NamePage {
  position: absolute;
  width: 1440px;
  height: 45px;
  top: 28px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 500;
  font-size: 40px;
  line-height: 49px;
  text-align: center;
  letter-spacing: 0.13em;

  color: #FFFFFF;
}

.inputpole {
  position: absolute;
  width: 370px;
  height: 75px;
  left: 176px;
  top: 402px;
  background: radial-gradient(171.46% 171.46% at 49.81% 144.29%, rgba(209, 212, 20, 0.3) 0%, rgba(49, 134, 48, 0.3) 100%);
  border: 2px solid rgba(255, 255, 255, 0.3);
  box-sizing: border-box;
  border-radius: 4px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 500;
  font-size: 30px;
  line-height: 37px;
  text-align: center;
  letter-spacing: 0.05em;
  color: rgba(38, 34, 34, 0.8);

}

.select1 {
  position: absolute;
  width: 90px;
  height: 75px;
  left: 547px;
  top: 402px;
  background: radial-gradient(171.46% 171.46% at 49.81% 144.29%, rgba(209, 212, 20, 0.3) 0%, rgba(49, 134, 48, 0.3) 100%);
  border: 2px solid rgba(255, 255, 255, 0.3);
  box-sizing: border-box;
  border-radius: 4px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 37px;
  text-align: center;
  letter-spacing: 0.05em;
  cursor: pointer;
  color: rgba(38, 34, 34, 0.8);

}

.outputpole {
  position: absolute;
  width: 370px;
  height: 75px;
  left: 811px;
  top: 403px;
  background: radial-gradient(171.46% 171.46% at 49.81% 144.29%, rgba(209, 212, 20, 0.3) 0%, rgba(49, 134, 48, 0.3) 100%);
  border: 2px solid rgba(255, 255, 255, 0.3);
  box-sizing: border-box;
  border-radius: 4px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 500;
  font-size: 30px;
  line-height: 65px;
  text-align: center;
  letter-spacing: 0.05em;
  color: rgba(38, 34, 34, 0.8);
}

.select2 {
  position: absolute;
  width: 90px;
  height: 75px;
  left: 1182px;
  top: 403px;
  background: radial-gradient(171.46% 171.46% at 49.81% 144.29%, rgba(209, 212, 20, 0.3) 0%, rgba(49, 134, 48, 0.3) 100%);
  border: 2px solid rgba(255, 255, 255, 0.3);
  box-sizing: border-box;
  border-radius: 4px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 37px;
  text-align: center;
  letter-spacing: 0.05em;
  color: rgba(38, 34, 34, 0.8);
  cursor: pointer;
}

.buttongotopage1 {
  position: absolute;
  width: 275px;
  height: 59px;
  left: 589px;
  top: 523px;
  background: radial-gradient(100% 2172.51% at 100% 50.85%, rgba(49, 134, 48, 0.55) 0%, rgba(209, 213, 20, 0.43) 100%);
  border: 2px solid rgba(255, 255, 255, 0.4);
  box-sizing: border-box;
  border-radius: 4px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: bold;
  font-size: 20px;
  line-height: 24px;
  text-align: center;
  letter-spacing: 0.05em;
  cursor: pointer;
  color: #FFFFFF;

}

.buttonswap {
  position: absolute;
  width: 102px;
  height: 75px;
  left: 676px;
  top: 403px;
  border: medium none;
  background-image: none;
  background: transparent;
  float: left;
  background-color: transparent;
  cursor: pointer;
}

</style>