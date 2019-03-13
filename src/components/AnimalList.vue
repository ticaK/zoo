<template>

  <div>
    
    <h1>Welcome To My Zoo</h1>

    <form @submit.prevent="addAnimal()">

        <div class="form-group">
          <label>Sector:</label>
            <select class="form-control" v-model="animal.sector">
                <option v-for="sector in sectors" :key="sector" :value="sector">{{sector}}</option><br>
            </select><br>
        </div>

        <div class="form-group"> 
          <label>Species:</label>
          <input type="text" class="form-control" v-model="animal.species">
        </div>

        <div class="form-group"> 
          <label>Name:</label>
          <input type="text" class="form-control" v-model="animal.name">
        </div>

        <div class="form-group">
          <label>Date of birth:</label>
          <input type="date" class="form-control"  v-model="animal.date"><br>
        </div>

        <button class="btn btn-primaty btn-block" type="submit">Add animal</button>
        
    </form>

    <table>

      <caption>All animals</caption>

      <tr>
        <th>Sector</th>
        <th>Species</th>
        <th>Name</th>
        <th>Date of birth</th>
        <th>Remove</th>
        <th>Move to top</th>
      </tr>

      <tr v-for="(animal,index) in animals" :key="index">
        <td>{{animal.sector}}</td>
        <td>{{animal.species}}</td>
        <td>{{animal.name}}</td>
        <td>{{animal.date ? moment(animal.date) : "Unknown"}}</td> 

        <td><button class="btn-warning btn-block" @click="removeAnimal(index)">Remove</button></td>
        <td><button class="btn-success btn-block" @click="moveToTop(index)">Move to top </button></td>
      </tr> 

    </table> 


    <table>
      <caption>Animals by sectors</caption>

      <tr v-for="sector in sectors" :key="sector">
        <td>{{sector}}</td>
        <td><button class="btn btn-block" @click="showAll(sector)">Show all</button></td>
      </tr>

    </table>
  
  </div>

</template>

<script>
import moment from 'moment'
export default {
  data() {
    return {

      animals:[
        {sector:"birds", species:"Penguin", name:"Pecky", date: moment('2017-12-04')},
        {sector:"fish", species:"Dolphin", name:"Sandy", date: moment('2015-11-03')},
        {sector:"insects", species:"Butterfly", name:"Brimstone", date: moment('2019-02-11')},
        {sector:"spiders", species:"Black Widow", name:"Killer", date: moment('2019-01-04')},
        {sector:"mammals", species:"Chinchilla", name:"Avalon"},   
      ],

      sectors: [
          "birds", "fish", "insects", "spiders","mammals"
      ],

      animal: {sector: "", species: "", name:"", date: ""}

  }
},
  

  methods: {

    moment(date) {
      return moment(date).format('LL');
    },

    removeAnimal(index) {
      this.animals.splice(index,1);
    },
    
    moveToTop(index) {
      const animal = this.animals[index];
      this.animals.splice(index,1);
      this.animals.unshift(animal);
    },

    addAnimal() {
      this.animals.push({...this.animal});
    },

    showAll(sector) {
        let sectorAnimals = "All animals from this sector: \n "; 
        let animals = this.animals.filter(animal=>animal.sector==sector);
        animals.forEach(function(animal){
            let dateStr = moment(animal.date).format('LL').toString();
            sectorAnimals += animal.species+", "+ animal.name + ", "+ dateStr +"\n"
        });
        alert(sectorAnimals);
    }
  
  }
}
</script>

<style>

table, th, td {
  text-align: center;
  border: 1px solid black;
  font-weight: bold;
}

table, form {
  margin:50px 0;
}

table {
  width: 100%;
}

th {
  background-color: #cec7c7;
}






</style>
