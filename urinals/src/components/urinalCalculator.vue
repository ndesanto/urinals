<template>
  <div >
    <h2> Urinal Saving Calculator </h2>
    <hr>

    <p> Input the number of people who use your urinals per year: </p> 
    <input v-model="numPeople" value="8000000" placeholder="800000" type="number" />
    <p> Input the number of urinals you have: </p> 

    <input v-model="numUrinals" placeholder="1" value="1" type="number" />
    <button v-show="false" v-submit="calculateOldUrinals(numPeople,numUrinals)">s</button>

    <p>{{fixNumber(resultUrinals)}} per year using current urinals </p>
    <p>{{fixNumber(initialFee)}} initial fee +  {{fixNumber(newUrinals)}} per year using our urinals </p>
    <table>
      <tr>
      <th>Total Cost after Year</th>
      <th>Normal Urinals</th>
      <th>Our Urinals</th>
      <th>ROI</th>
      </tr>

      <tr v-for="(item, index) in calculateNewUrinals()" v-bind:key="index"> 
        <td>{{index + 1}}</td> <td>${{fixNumber(resultUrinals* (index+1))}}</td> <td>${{fixNumber(item)}}</td> <td>${{fixNumber((resultUrinals* (index+1)) - item)}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'urinalCalculator',

  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      numPeople: 8000000,
      numUrinals: 30,
      resultUrinals: 0,
      newUrinals: 0,
      initialFee: 0
    }
  },
  methods: {
    calculateOldUrinals(people, urinals) {
      this.resultUrinals = ((((people/2) * 3.8)/1000) * 5);
      this.newUrinals = (190*(people/10000)/urinals);
      this.initialFee = ((54970/30) * this.numUrinals);
    },
    calculateNewUrinals() {
      return [this.initialFee + this.newUrinals, this.initialFee + this.newUrinals + (190*(this.numPeople/10000)/this.numUrinals), this.initialFee + this.newUrinals + 2*(190*(this.numPeople/10000)/this.numUrinals), this.initialFee + this.newUrinals + 3*(190*(this.numPeople/10000)/this.numUrinals), this.initialFee + this.newUrinals + 4*(190*(this.numPeople/10000)/this.numUrinals)];
    },
    fixNumber(num) {
      return parseFloat(num).toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
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
}

input {
  height: 30px;
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

}

tr:nth-child(even) {
  background-color: #f0efef;
}
</style>
