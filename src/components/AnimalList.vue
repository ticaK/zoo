<template>
  <div>
    
     <form name="myForm" @submit.prevent="addAnimal()">
     Species: <select name="sp">
                  <option v-for="sector in sectors" :key="sector" :value="sector">{{sector}}</option><br>
              </select><br>
   
        Name:<input type="name" name="nm"><br>
        Date:<input type="name" name="dt"><br>
        <button type="submit">Add</button>
      </form>

    <table>
      <tr v-for="(animal,index) in animals" :key="index">
      <th>{{animal.species}}</th>
      <th>{{animal.name}}</th>
      <th>{{animal.date ? animal.date : "nepoznat"}}</th>
      <button @click="removeAnimal(index)">Remove</button>
      <button @click="moveToTop(index)">Move to top </button>
      
      </tr> 
  </table> <br>

  <table>
    <tr v-for="(sector,index) in sectors" :key="sector">
      <th>{{sector}}</th>
      <button @click="showAll(sector)">ShowAll</button>
    </tr>
  </table>
  

 

  </div>
</template>

<script>
export default {
  data(){
    return {
      animals:[
        {species:"cat",name:"Garfild",date:('01.01.2015.')},
        {species:"dog",name:"Lesi",date:('11.01.2015.')},
        {species:"elephant",name:"Bobi",date:('01.25.2015.')},
        {species:"fish",name:"Fish2",date:('10.01.2018.')},
        {species:"bird",name:"Bird1"}
      ],
      sectors:[
    "cat", "dog", "elephant", "fish", "bird"
      ]
    }
  },
  

  methods:{
    removeAnimal(index){
      this.animals.splice(index,1);
    },
    moveToTop(index){
      const animal = this.animals[index];
      this.animals.splice(index,1);
      this.animals.unshift(animal);
    },
    addAnimal(){
      this.animals.push({species:document.forms["myForm"]["sp"].value,
                         name:document.forms["myForm"]["nm"].value,
                         date:document.forms["myForm"]["dt"].value});
    },
    showAll(sector){
          let an = [];      
        for(let i = 0; i<this.animals.length;i++){
           if(this.animals[i].species==sector){
             an.push(this.animals[i]);
          }                  
        }
       alert(JSON.stringify(an));
                  

        
  }

}
}
</script>

<style>
table, th, td {
  border: 1px solid black;
}
</style>
