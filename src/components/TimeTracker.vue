<template>
  <div>

  <div>
    <form  @submit.prevent="OnCreateTemps()">
      <input v-model="date" class="btn_date" type="date">
      <input v-model="period" class="text_period" placeholder="name period" type="text">
      <button @click="submitStop" class="btn_stop"> stop </button>
      <button @click="submitStart" class="btn_start"> start new </button>
      <input v-model="detail" class="btn_time" type="time">
    </form>
  </div>

  <div>
    <table >
  <tbody>
    <tr v-for="(detail,index) in details" :key="index">
      <td>{{detail.period}}</td>
      <td>{{detail.temps_deb}}</td>
      <td>{{detail.temps_fin}}</td>
    </tr>
  </tbody>
 </table>
  </div>
   
  </div>
</template>

<script>
  import axios from 'axios';
  export default { 
  name: 'TimeTracker',
  
data(){
return{
  date:null,
  detail:'null',
  period:null,
  details:[
    {
      period:'period1',
      temps_deb:'10:00',
      temps_fin:'12:00'
  },
  {
      period:'period2',
      temps_deb:'12:00',
      temps_fin:'14:00'
  }
]
}
},
  methods:{
    OnCreateTemps(){
    axios.post('http://localhost:3000/temps',{
      nom_period: this.period,
      date: this.date,
      temps_deb: this.temps_deb,
      temps_fin: this.temps_fin
    }).then(response =>{
      console.log(response);
     // this.$router.push('/temps');
    })
    },
    submitStart(){
      if(this.detail.length ===0)  return;
      this.details.push({
        temps_deb:this.detail,
        period:this.period

      })
      /* console.log(this.detail) */
    },
    submitStop(){
      if(this.detail.length ===0)  return;
      this.details.push({
        temps_fin:this.detail,
        period:this.period
      })
      /* console.log(this.detail) */
    }
  }
 
}
</script>

<style lang="scss">
  
html, body {
  padding: 80px;
}

table {
    border-collapse: collapse;
    width: 100%;
}

th, td {
    padding: 10px;
    text-align: left;
    border-bottom: 3px solid #ddd;

}

.btn_stop {
    background-color: white;
    color: black;
    border: 2px solid #ff1313a6;
    margin-left: 100px;
    border-radius: 12px;
    cursor: pointer;
}
.btn_start {
    background-color: white;
    color: black;
    border: 2px solid #4CAF50;
    margin-left: 10px;
    border-radius: 12px; 
    cursor: pointer;
}
.btn_time{
  margin-left: 5px;
}
.text_period{
  width: 100px;
  height: 15px;
  margin-left: 10px;
}

</style>