<template>
  <div class="container">
    <SwipedButton
      ref="swipeButton"
      class="swipe-button"
      @actionConfirmed="onActionConfirmed"
    />
    <BarChart
      v-if="loaded"
      :chartdata="chartdata"
      :options="options"/>
  </div>
</template>

<script>
import SwipedButton from 'vue-swipe-button'
import 'vue-swipe-button/dist/swipeButton.css'
import axios from 'axios'
import BarChart from './BarChart'

export default {
  name: 'Chart',
  components: { SwipedButton, BarChart },
  data: () => ({
    loaded: false,
    chartdata: {
      labels: ['15 a 19 años', '20 29 años', '30-49 años', '50-64 años', 'Más de 65'],
      datasets: null
    },
    options: {
      scales: {
        yAxes: [{
          ticks: {
            beginAtZero: true
          },
          gridLines: {
            display: true
          }
        }],
        xAxes: [ {
          gridLines: {
            display: false
          }
        }]
      },
      legend: {
        display: true
      },
      responsive: true,
      maintainAspectRatio: false
    }
  }),
  mounted () {
    this.loaded = false
    axios.get('http://www.mocky.io/v2/5dca723f33000073003ded0c')
      .then((response) => {
        const responseData = response.data.data
        this.chartdata.datasets = //{
          //labels: responseData.map(item => item.age_range),
          [
            {
              label: 'Aprobados',
              backgroundColor: '#3498DB',
              pointBackgroundColor: 'white',
              borderWidth: 1,
              pointBorderColor: '#249EBF',
              data: responseData.map(item => item.count.total_approved)
            },
            {
              label: 'Reprobados',
              backgroundColor: '#f87979',
              pointBackgroundColor: 'white',
              borderWidth: 1,
              pointBorderColor: '#249EBF',
              data: responseData.map(item => item.count.total_disapproved)
            }
          ]
        //}
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  methods: {
    onActionConfirmed() {
      this.loaded = false
      setTimeout(() => {
        this.loaded = true
        this.$refs.swipeButton.reset();
      }, 1000);
    },
  }
}
</script>

<style>
  .swipe-button {
    margin-top: 2rem;
    margin-bottom: 2rem;
    width: 100%;
    background-color: #17255A;
    border: 1px solid #17255A;
  }
</style>
