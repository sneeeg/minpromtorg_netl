<script>
import {HorizontalBar} from 'vue-chartjs'

export default {
  extends: HorizontalBar,
  props:['labels', 'values'],
  mounted () {
    this.gradient = this.$refs.canvas.getContext('2d').createLinearGradient(0, 0, 0, 300)
    this.gradient.addColorStop(0, '#2E1CE8')
    this.gradient.addColorStop(0.5, '#1b108b');
    this.gradient.addColorStop(1, '#040217');


    this.renderChart({
      labels: this.labels,
      responsive: true,
      datasets: [
        {
          label: '',
          backgroundColor: this.gradient,
          borderColor: this.gradient,
          borderWidth: 5,
          tension: 0.04,
          data: this.values,
          capBezierPoints: false
        }
      ]
    }, {
      responsive: true,
      plugins: {
        legend: false
      },
      elements: {
        point:{
          radius: 0
        }
      },
      scales: {
        xAxes: [{
          gridLines: {
            display: false
          },
          ticks: {
            beginAtZero: true
          }
        }],
        yAxes: [{
          gridLines: {
            display: false
          },
        }]
      }
    })
  }
}
</script>
