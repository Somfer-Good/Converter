<template>
  <div class="body">
    <h1 class="heading">Курс валют на {{ date.slice(0, 10) }} {{ date.slice(11, 30) }}</h1>
    <h1 class="tableName1">Валюта</h1>
    <h1 class="tableName2">Курс</h1>
    <div class="tableName2dop">(по отношению к ₽)</div>
    <table class="table" border="1">
      <tbody>
      <tr v-for="currency in valute">
        <td class="namevalue">{{ currency.Name }}</td>
        <td class="namevalue" v-if="currency.NumCode>0" style="color:greenyellow">
          {{ Math.floor(((currency.Value/currency.Nominal)*100))/100 + " +" + Math.floor(((currency.NumCode/currency.Nominal)*100))/100 }}
        </td>
        <td class="namevalue" v-if="currency.NumCode<0" style="color:red">
          {{ Math.floor(((currency.Value/currency.Nominal)*100))/100 + " " + Math.floor(((currency.NumCode/currency.Nominal)*100))/100 }}
        </td>
      </tr>
      </tbody>
    </table>
    <button class="buttonRenovarData" @click="RenovarData(), $emit('changeData');">Обновить данные</button>
    <button class="buttongotopage2" @click="$emit('changePage1')">Перейти к конвертеру</button>
  </div>
</template>

<script>
export default {
  props: ['valute', 'date'],
  name: "PageTable",
  methods:
      {
        RenovarData: function (event) {
          alert('Хотите обновить данные?');
          alert('Данные успешно загружены с сервера');
        }
      }
}
</script>

<style scoped>
.body {
  position: absolute;
  width: 100%;
  height: 120%;
  top: 0;
  left: 0;
  background: radial-gradient(122.19% 312.8% at 55.59% 50%, rgba(16, 111, 19, 0.5) 0%, rgba(209, 212, 20, 0.37) 100%);
}

.heading {
  position: absolute;
  width: 1000px;
  height: 45px;
  top: 10px;
  left: 300px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 600;
  font-size: 40px;
  line-height: 49px;
  text-align: center;
  letter-spacing: 0.13em;
  color: #FFFFFF;
}

.table {
  position: absolute;
  width: 600px;
  height: 586px;
  left: 390px;
  top: 200px;
  background: radial-gradient(171.46% 171.46% at 49.81% 144.29%, rgba(209, 212, 20, 0.35) 0%, rgba(49, 134, 48, 0) 100%);
}

.tableName1 {
  position: absolute;
  width: 222px;
  height: 45px;
  left: 500px;
  top: 93px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 300;
  font-size: 40px;
  line-height: 49px;
  text-align: center;
  letter-spacing: 0.13em;
  color: #FFFFFF;
}

.tableName2 {
  position: absolute;
  width: 350px;
  height: 68px;
  left: 740px;
  top: 93px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 500;
  font-size: 40px;
  line-height: 49px;
  text-align: center;
  letter-spacing: 0.13em;
  color: #FFFFFF;

}

.tableName2dop {
  position: absolute;
  width: 249px;
  height: 68px;
  left: 790px;
  top: 160px;
  font-family: Montserrat, serif;
  font-style: normal;
  font-weight: 500;
  font-size: 13px;
  line-height: 49px;
  text-align: center;
  letter-spacing: 0.13em;

  color: #FFFFFF;
}

.namevalue {

  font-family: Montserrat;
  font-style: normal;
  font-weight: 500;
  font-size: 17px;
  line-height: 21px;
  text-align: center;
  letter-spacing: 0.05em;
  color: #FFFFFF;
}

.buttonRenovarData {
  position: absolute;
  width: 275px;
  height: 59px;
  left: 1100px;
  top: 200px;
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
  color: #FFFFFF;
  cursor: pointer;
}

.buttongotopage2 {
  position: absolute;
  width: 275px;
  height: 59px;
  left: 1100px;
  top: 300px;
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
  color: #FFFFFF;
  cursor: pointer;
}
</style>