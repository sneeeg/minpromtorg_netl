<script>
import {Doughnut} from 'vue-chartjs'
import 'chartjs-plugin-labels'

export default {
  extends: Doughnut,
  props:['data'],
  watch: {
    data() {
      this.getInitialState()
    }
  },
  methods: {
    getInitialState() {
      this.renderChart({
      
        labels: this.data.map(a => a.production_size_name),
        // labels: ['label-1', 'label-2', 'label-3', 'label-4'],
          datasets: [
            {
              backgroundColor: ['#2E1CE8', '#1b108b', '#040217', '#808080'],
              borderWidth: 0,
              data: this.data.map(a => a.id_count)
            }
          ]
      }, {
        legend: {
          display: false
        },
          plugins: {
            labels: {
              render: 'percentage',
              position: 'outside',
              fontColor: '#2E1CE8',
              fontFamily: "'Bahnschrift'",
              fontSize: 20,
              outsidePadding: 40,
              textMargin: 8
            }
          },
          cutoutPercentage: 80
      })
    }
  },
  mounted () {
    this.getInitialState()
    // Overwriting base render method with actual data.
    
  }
}
</script>
