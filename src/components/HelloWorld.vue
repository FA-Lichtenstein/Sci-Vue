<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>Here is a pretty looking integral for you:</p>
    <div>\[ \int^{1}_{0} x^2 \ \textrm{d}x = \frac{1}{3}. \]</div>
    <p>And here is a tidy graph of the same integral for you:</p>
    <div class="figure_container">
      <h2 class="chart_title">Figure 1: Graph of \( \displaystyle{ \int^{1}_{0} x^2 \ \textrm{d}x }\)</h2>
      <h3 class="chart_ylabel">\( x^2 \)</h3>
      <div class="chart_container">
        <canvas id="myChart"></canvas>
      </div>
      <h3 class="chart_xlabel">\( x \)</h3>
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
    const Chart = window.Chart
    const data = ref({})
    const chart_data = ref([])
    const date = new Date()
    const year = date.getFullYear()

    for(var i = 0; i<=100; i++){
      chart_data.value.push(
        {x: (i/100), y: Math.pow((i/100),2).toFixed(4) }
      )
    }

    data.value = {
          datasets: [{
            data: chart_data.value,
            backgroundColor: 'rgba(44, 62, 80, 0.25)',
            borderColor: 'rgba(44, 62, 80, 0.5)',
            showLine: true,
            fill: true,
            pointRadius: 0,
            pointHoverRadius: 0,
            tension: 0.5
          }],
        }

    const options = {
          plugins: {
              legend: {
                display: false
            },
            title: {
              display: false,
            }
          },
          scales: {
            x: {
              title: {
                display:false,
              },
              type: 'linear',
              position: 'bottom'
            },
            y: {
              title: {
                display:true,
              },
            }
          },
          responsive: true,
          layout: {
            padding: {
                left: 0
            }
          }
        }

    return {chart_data, data, options, Chart, year}
  },
  mounted(){
    if(typeof(window.renderMathInElement)==='function'){
        window.renderMathInElement(document.body)
      }
    var ctx = document.getElementById('myChart').getContext('2d');
    this.my_chart = new Chart(ctx, {
        type: 'scatter',
        data: this.data,
        options: this.options
    })
  }
}
</script>

<style>
.figure_container{
  display: inline-flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  max-width: 800px;
  min-width: 90vw;
  margin: auto;
}

.chart_title{
  min-width: 100vw;
  margin: 0px 0px 0px 0px;
  font-size: 1em;
}
.chart_ylabel{
  display: inline;
  margin: 0px 0px 0px 0px;
  font-size: 0.9em;
}
.chart_container{
  display: block;
  flex-wrap: wrap;
  justify-content: center;
  width: 80vw;
  max-width: 600px;
}
.myChart{
  flex: 1 0 100%;
  max-width: 600px;
}
.chart_xlabel{
  margin: 0px 0px 0px 0px;
  min-width: 100vw;
  font-size: 0.9em;
}
</style>
