<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <div class="text-xs-center">
        <h1>Madkudu Antelope Analysis</h1>
        <h2>Antelope Locations</h2>
        <pie-chart :data="analysis[0].locationData"/>
        <h2>Antelope Horn Shape</h2>
        <pie-chart :data="analysis[1].hornData"/>
        <h1>Antelope Data</h1>
        <div v-for="antelope in antelopeData" :key ="antelope.name">
          <card
            :names="antelope.name"
            :continents="antelope.continent"
            :weights="antelope.weight"
            :heights="antelope.height"
            :horn="antelope.horns"
            :pictures="antelope.picture"
            
          />
        </div>
      </div>
     </v-flex>
  </v-layout>
  
</template>

<script>
import axios from 'axios'
import card from '~/components/card.vue'
import pieChart from '~/components/pieChart.vue'

export default {
  asyncData(){
      return axios.get(`https://s3-us-west-2.amazonaws.com/team.madkudu.com/species.json`)
      .then((response) => {
        return {antelopeData: response.data}
      })
  },
  data: function(){
    return {
    analysis: [  
      {
    locationData: {
        labels: [],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ["#41B883", "#E46651", "#00D8FF"],
            data: []
          }
        ]
      }
      },
      {
    hornData: {
        labels: [],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ["#41B883", "#E46651", "#00D8FF",'#FF0000','#5E0DFF','#2CA3E8'],
            data: []
          }
        ]
      }
      },
    ]
    }
  },
  methods: {
    antelopeLocation: function(){
      var i;
      var j;
      var k;
      var arr =[]
      for( i =0; i < this.antelopeData.length; i++){
        if(this.analysis[0].locationData.labels.includes(this.antelopeData[i].continent)){
          continue;
        }else{
          this.analysis[0].locationData.labels.push(this.antelopeData[i].continent)
          arr.push(0)
        }
      }

      for(j=0; j< this.analysis[0].locationData.labels.length; j++){
        for(k=0; k<this.antelopeData.length; k++){
          if(this.analysis[0].locationData.labels[j] === this.antelopeData[k].continent){
            arr[j] = arr[j] +1
          }
        }        
      }
      this.analysis[0].locationData.datasets[0].data = arr
    },
    antelopeHornTypes: function(){
      var i;
      var j;
      var k;
      var arr =[]
      for( i =0; i < this.antelopeData.length; i++){
        if(this.analysis[1].hornData.labels.includes(this.antelopeData[i].horns)){
          continue;
        }else{
          this.analysis[1].hornData.labels.push(this.antelopeData[i].horns)
          arr.push(0)
        }
      }

      for(j=0; j< this.analysis[1].hornData.labels.length; j++){
        for(k=0; k<this.antelopeData.length; k++){
          if(this.analysis[1].hornData.labels[j] === this.antelopeData[k].horns){
            arr[j] = arr[j] +1
          }
        }        
      }
      this.analysis[1].hornData.datasets[0].data = arr
    }
  },
  created(){
    this.antelopeLocation()
    this.antelopeHornTypes()
  },
  components: {
    card,
    pieChart
  }
}
</script>
