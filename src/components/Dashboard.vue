<template>
  <v-container>
    <v-row>
      <v-col cols="4">
        <v-card>
          <v-container>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>Unique Users:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>{{uniqueUsers}}</h2>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card>
          <v-container>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>Total Page Visits:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>{{dummyData.pageVisits}}</h2>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card>
          <v-container>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>Average Time on Page:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>{{Math.floor(Math.random() * 6) + 2  }} Minutes</h2>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="4">
        <v-card>
          <radar-chart :chart-data="dummyData.radarChart.data"></radar-chart>
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card>
          <bar-chart :chart-data="dummyData.barChart.data"></bar-chart>
        </v-card>
      </v-col>
      <v-col cols="4">
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
import RadarChart from "../lib/charts/RadarChart";
import colors from '../lib/constants/colors';
  export default {
    name: 'Dashboard',
    components: {BarChart, PieChart, LineChart, RadarChart},

    data: () => ({
      dummyData: {
        pageVisits: Math.floor(Math.random() * 1756) + 976,
        timeOnPage: Math.floor(Math.random() * 6) + 2,

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
        radarChart: {
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
    computed: {
      uniqueUsers: function() {
        return this.dummyData.pageVisits - (Math.floor(Math.random() * 460) + 201)
      }
    },
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

      this.dummyData.radarChart.data = {
			labels: ['1', '2', '3', '4', '5', '6', '7'],
			datasets: [{
				label: 'Dataset 1',
				pointBackgroundColor: colors.red,
				backgroundColor: this.changeColorAlpha(colors.red, "0.2"),
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
				pointBackgroundColor: colors.blue,
				backgroundColor: this.changeColorAlpha(colors.blue, "0.2"),
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
      changeColorAlpha(rgbaString, alpha){
        let match = rgbaString.match(/rgba\((\s*\d+\s*,\s*\d+\s*,\s*\d+\s*),\s*(\d+\.?\d*)\)/)[1]
        let newColor = "rgba("+match+","+alpha+")"
        return newColor
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