<template>
  <div id="app">
    <h1>Ableitungsrechner</h1>
    f(x)=<input v-model="funktion" placeholder="a*x^2+b*x+c"/><br><br>
    <span v-if="funktion.length === 0">
      f'(x)=2*a*x+b
    </span>
    <span v-else>
      f'(x)={{ableiten()}}
    </span><br>
    <ul>
      <li v-for="regel in regelnUsed" v-bind:key="regel.id">{{regel.name}}</li>
    </ul>
  </div>
</template>
<script>
import { derivative } from "mathjs";

export default {
  name: 'App',
  data: () => ({
    funktion: '',
    regeln: [
      {id: 1, name: "Potenzregel (Beta)"},
      {id: 2, name: "Faktorregel (Beta)"},
      {id: 3, name: "Summenregel (Alpha)"},
      {id: 4, name: "Differenzregel (Alpha)"},
      {id: 5, name: "Produktregel (Alpha)"},
      {id: 6, name: "Quotientenregel (Alpha)"},
      {id: 7, name: "Kettenregel (Alpha)"}
    ],
    regelnUsed: [{id:0, name:"Keine Ableitungsregel benutzt (Coming soon)"}]
  }),
  methods: {
    ableiten() {
      return derivative(this.funktion, 'x', { simplify: true });
    }
  }
}
</script>

<style>
body {
  background: rgb(2,0,36);
  background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(9,9,121,1) 23%, rgba(0,212,255,1) 100%);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #f1f1f1;
  position: fixed;
  top: 50%;
  left: 50%;
  width: 50%;
  height: 60%;
  transform: translate(-50%, -50%);
}
</style>
