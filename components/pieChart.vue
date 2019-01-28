<script>
import {Pie} from 'vue-chartjs'

export default {
    extends: Pie,
    props: ['data', 'options'],
    mounted() {
        this.renderChart(this.data, this.options)
    },
    data: function(){
    return {
    locationData: {
        labels: ['hello','me','you'],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ["#41B883", "#E46651", "#00D8FF"],
            data: [30, 10, 30]
          }
        ]
      }
    }
  },
    methods: {


    }
}
</script>