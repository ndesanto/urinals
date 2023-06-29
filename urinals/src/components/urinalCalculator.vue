<template>
  <div>
    <h2>URIMAT Urinal Saving Calculator  </h2>
    <hr>
    <p>Input the number of urinals you have: </p>

    <input v-model="numUrinals" placeholder="1" value="1" type="number" />
    <button v-show="false" v-submit="calculateCO2()">s</button>
    <div class="table">
      <table>
        <tr>
          <th>kg less of CO2 Emissions</th>
          <th>Liters of Water Saved</th>
          <th>Cubic Meters of Water Saved</th>
          <th>Olympic Swimming pools of water saved</th>
          <th>Water Saving Dollars*</th>
        </tr>
        <tr>
          <td>{{this.calculateNewUrinals()[0].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}} kg</td>
          <td>{{this.calculateNewUrinals()[1].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}} L</td>
          <td>{{this.calculateNewUrinals()[2].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}} m<sup>3</sup></td>
          <td>{{this.calculateNewUrinals()[3].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</td>
          <td>${{this.calculateNewUrinals()[4].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</td>
        </tr>
        <tr>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
          <td><p class="smalltext">*$5/cubic-meter</p></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'urinalCalculator',

  data () {
    return {
      msg: '',
      numUrinals: 1,
      resultUrinals: 0,
      newUrinals: 0,
      initialFee: 0
    }
  },
  methods: {
    calculateWaterSaved () {
      return (this.numUrinals * 100000)
    },
    calculateCO2 () {
      return this.numUrinals * 17.5
    },
    calculatePools () {
      return this.numUrinals * 2.5
    },
    calculateNewUrinals () {
      return [this.calculateCO2(), this.calculateWaterSaved(), this.calculateWaterSaved() / 1000, this.calculatePools(), (this.calculateWaterSaved() / 1000) * 5]
    },
    fixNumber (num) {
      return parseFloat(num).toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

table {

  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: fit-content;
  margin: 0 auto;
  max-width: 800px;
  overflow: scroll;

}

input {
  height: 30px;
  margin-bottom: 3em;
}
th {
  border: 1px solid #dddddd;
  text-align: center;
  padding: 8px;

}

td:first-child {
  border: 0px solid #dddddd;
  text-align: center;
  padding: 8px;

}
td {
  border: 0px solid #dddddd;
  text-align: right;
  padding: 8px;
  overflow: scroll;

}

tr:nth-child(even) {
  background-color: #f0efef;
}
.smalltext {
  font-size:10px;
}

div.table {
  max-width: 800px;
  overflow: scroll;
  margin: 0 auto;
}
</style>
