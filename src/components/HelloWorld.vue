<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>Here is a pretty looking integral for you:</p>
    <div>\[ \int^{1}_{0} x^2 \textrm{d}x = \frac{1}{3}. \]</div>
    <p>And here is a tidy graph of the same integral for you:</p>
    <div class="chart_container">
      <canvas id="myChart"></canvas>
    </div>
    <p>Hope you like!</p>
    <p>Copyright &copy; {{year}} F.A. Lichtenstein</p>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'HelloWorld',
  my_chart: '',
  props: {
    msg: String
  },
  setup(){
    const chart_data = ref([])
    const Chart = window.Chart
    const date = new Date()
    const year = date.getFullYear()

    for(var i = 0; i<=100; i++){
      chart_data.value.push(
        {x: (i/100), y: Math.pow((i/100),2).toFixed(4) }
      )
    }
    return {chart_data, Chart, year}
  },
  mounted(){
    if(typeof(window.renderMathInElement)==='function'){
        window.renderMathInElement(document.body)
      }
    var ctx = document.getElementById('myChart').getContext('2d');
    this.my_chart = new Chart(ctx, {
        type: 'scatter',
        data: {
          datasets: [{
            data: this.chart_data,
            backgroundColor: 'rgba(44, 62, 80, 0.25)',
            borderColor: 'rgba(44, 62, 80, 0.5)',
            showLine: true,
            fill: true,
            pointRadius: 0,
            pointHoverRadius: 0,
            tension: 0.5
          }],
          
        },
        options: {
          plugins: {
              legend: {
                display: false
            },
            title: {
              display: true,
              text: 'Definite integral of x^2 from 0 to 1'
            }
          },
          scales: {
            x: {
              title: {
                display:true,
                text:'x'
              },
              type: 'linear',
              position: 'bottom'
            },
            y: {
              title: {
                display:true,
                text:'x^2'
              },
            }
          },
          responsive: true
        }
    })
  }
}
</script>

<style>
.chart_container{
  display: inline-flex;
  position: relative;
  width:95vw;
  max-width: 600px;
}
</style>
