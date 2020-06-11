<template>
  <v-container>
    <v-row>
      <v-col cols="4">
        <v-card>

        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card>
          
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card>
          
        </v-card>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="6">
        <v-card>
          <bar-chart :chart-data="dummyData.barChart.data"></bar-chart>
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card>
          <pie-chart :chart-data="dummyData.pieChart.data"></pie-chart>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-card>
          <line-chart :chart-data="dummyData.lineChart.data" :options="dummyData.lineChart.options"></line-chart>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import BarChart from "../lib/charts/BarChart";
import PieChart from "../lib/charts/PieChart";
import LineChart from "../lib/charts/LineChart";
import colors from '../lib/constants/colors';
  export default {
    name: 'Dashboard',
    components: {BarChart, PieChart, LineChart},

    data: () => ({
      dummyData: {
        barChart: {
          data: {},
          options: {
            responsive: true,
            scales: {
              yAxes: [
                {
                  ticks: {
                    beginAtZero: true
                  }
                }
              ]
            }
          }
        },
        pieChart: {
          data: {},
          options: {}
        },
        lineChart: {
          data: {},
          options: {
            responsive: true,
            title: {
              display: true,
              text: 'Chart.js Line Chart'
            },
            tooltips: {
              mode: 'index',
              intersect: false,
            },
            hover: {
              mode: 'nearest',
              intersect: false
            },
            scales: {
              xAxes: [{
                display: true,
                scaleLabel: {
                  display: true,
                  labelString: 'X'
                }
              }],
              yAxes: [{
                display: true,
                scaleLabel: {
                  display: true,
                  labelString: 'Y'
                }
              }]
            }
          }
        },
      }
    }),
    mounted () {
      this.fillData()
    },
    methods: {
      fillData () {
        this.dummyData.lineChart.data = {
          labels: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()],
          datasets: [
            {
              label: 'First Data Set',
              fill: false,
              borderColor: colors.blue,
              data: [this.getRandomInt(), this.getRandomInt(),this.getRandomInt(),this.getRandomInt(),this.getRandomInt()]
            }, {
              label: 'Second Data Set',
              fill: false,
              borderColor: colors.red,
              data: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
            }
          ]
        }

        this.dummyData.pieChart.data = {
          datasets: [{
            data: [
              this.getRandomScalingFactor(),
              this.getRandomScalingFactor(),
              this.getRandomScalingFactor(),
              this.getRandomScalingFactor(),
              this.getRandomScalingFactor(),
            ],
            backgroundColor: [
              colors.red,
              colors.orange,
              colors.yellow,
              colors.green,
              colors.blue,
            ],
            label: 'Dataset 1'
          }],
          labels: [
            'Red',
            'Orange',
            'Yellow',
            'Green',
            'Blue'
          ]}
        
        this.dummyData.barChart.data = {
			labels: ['1', '2', '3', '4', '5', '6', '7'],
			datasets: [{
				label: 'Dataset 1',
				backgroundColor: colors.red,
				borderColor: colors.red,
				borderWidth: 1,
				data: [
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor()
				]
			}, {
				label: 'Dataset 2',
				backgroundColor: colors.blue,
				borderColor: colors.blue,
				borderWidth: 1,
				data: [
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
					this.getRandomScalingFactor(),
				]
			}]

		};
      },
      getRandomInt () {
        return Math.floor(Math.random() * (50 - 5 + 1)) + 5
      },
      getRandomScalingFactor () {
        return Math.round(Math.random() * 100);
      }
    }
  }
</script>

<style>
</style>