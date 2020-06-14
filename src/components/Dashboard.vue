<template>
  <v-container>
    <v-row>
      <v-container>
        <v-row>
          <v-col cols="12">
            <v-progress-linear height="40px" :value="(dummyData.overallECTS/180)*100">
              <strong style="color: #fefefe">Overall ECTS: {{dummyData.overallECTS}}/180</strong>
            </v-progress-linear>
          </v-col>
        </v-row>
      </v-container>
    </v-row>
    <v-row>
      <v-col cols="4">
        <v-card>
          <v-container>
            <v-row>
              <v-col cols="12" class="text-center" :style="{dummyData}">
                <h2>Semester:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>7</h2>
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
                <h2>Current Average:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" class="text-center" :style="{color: getColorForAverage}">
                <h2>{{dummyData.average}}</h2>
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
                <h2>Average ECTS per Semester:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>{{Math.floor(Math.random() * 28) + 12  }}</h2>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <v-card>
          <v-container>
            <v-row>
              <v-col class="text-center">
                <h2>Required ECTS:</h2>
              </v-col>
            </v-row>
            <v-row v-for="item of dummyData.progressBars" v-bind:key="item.index">
              <v-col cols="12">
                <v-progress-linear height="20px" :value="(item.current/item.max)*100">
                  <strong style="color: #fefefe">{{item.label}}: {{item.current}}/{{item.max}}</strong>
                </v-progress-linear>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card>
          <v-container>
            <v-row>
              <v-col class="text-center">
                <h2>Required Activities:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-list style="width: 100%">
                <template v-for="item in dummyData.listItems">
                  <v-divider v-if="item.divider" :key="item.index"></v-divider>
                  <v-list-item v-else :key="item.text">
                    <v-list-item-avatar>
                      <template v-if="item.done">
                        &#10004;&#65039;
                      </template>
                      <template v-else>
                        &#10060;
                      </template>
                    </v-list-item-avatar>
                    <v-list-item-content>
                      <v-list-item-title v-html="item.text"></v-list-item-title>
                      <v-list-item-subtitle v-html="item.subText"></v-list-item-subtitle>
                    </v-list-item-content>
                  </v-list-item>
                </template>
              </v-list>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <v-card>
          <v-container>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>Workload vs Performance:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12">
                <bar-chart :chart-data="dummyData.barChart.data" :options="dummyData.barChart.options"></bar-chart>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card>
          <v-container>
            <v-row>
              <v-col cols="12" class="text-center">
                <h2>Specializations:</h2>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12">
                <radar-chart :chart-data="dummyData.radarChart.data"></radar-chart>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import BarChart from "../lib/charts/BarChart";
import RadarChart from "../lib/charts/RadarChart";
import colors from '../lib/constants/colors';
  export default {
    name: 'Dashboard',
    components: {BarChart, RadarChart},
    data: () => ({
      dummyData: {
        overallECTS: Math.floor(Math.random() * 150) + 1,
        average: ((Math.random() * 4) + 1).toFixed(2),
        semester: Math.floor(Math.random() * 12) + 1,
        timeOnPage: Math.floor(Math.random() * 6) + 2,
        radarChartValues: {
          appliedCS: 0,
          theoreticalCS: 0,
          harwareSystems: 0,
          greenIT: 0,
          ai: 0,
        },
        progressBars: [
          {
            label: "Applied CS",
            current: 12,
            max: 15
          },
          {
            label: "Theoretical CS",
            current: 8,
            max: 15
          },
          {
            label: "Hardware & Systems",
            current: 5,
            max: 15
          },
          {
            label: "Green IT",
            current: 15,
            max: 15
          },
          {
            label: "AI",
            current: 11,
            max: 15
          }
        ],

        listItems: [
          {
            text: "Practical course",
            subText: "Take 1 practical course in any specialization",
            done: true
          },
          {divider: true},
          {
            text: "Seminar 1",
            subText: "Take first seminar in any specialization",
            done: true
          },
          {divider: true},
          {
            text: "Seminar 2",
            subText: "Take second seminar in any specialization",
            done: true
          },
          {divider: true},
          {
            text: "Thesis",
            subText: "Write your final thesis",
            done: false
          },
        ],
        
        barChart: {
          data: {},
          options: {
            responsive: true,
            scales: {
              yAxes: [
                {
                  type: 'linear', // only linear but allow scale type registration. This allows extensions to exist solely for log scale for instance
                  display: true,
                  position: 'left',
                  id: 'y-axis-1',
                  scaleLabel: {
                    labelString: "ECTS",
                    display: true
                  },
                  ticks: {
                    beginAtZero: true
                  }
                },
              ],
              xAxes: [
                {
                  display: true,
                  scaleLabel: {
                    labelString: "Semester",
                    display: true
                  },
                  ticks: {
                    beginAtZero: true
                  }
                },
              ]
            }
          }
        },
        radarChart: {
          data: {},
          options: {
            responsive: true,
          }
        },
        doughnutChart: {
          data: {},
          options: {}
        },
      }
    }),
    computed: {
      uniqueUsers: function() {
        return this.dummyData.pageVisits - (Math.floor(Math.random() * 460) + 201)
      },
      getColorForAverage: function () {
        if(this.dummyData.average < 2) {
          return colors.green
        } else if (this.dummyData.average > 3){
          return colors.red
        }else {
          return colors.orange
        }
      }
    },
    mounted () {
      this.fillData()
    },
    methods: {
      fillData () {
      this.dummyData.barChart.data = {
			labels: ['1', '2', '3', '4', '5', '6', '7'],
			datasets: [{
        label: 'ECTS',
        yAxisID: 'y-axis-1',
				backgroundColor: colors.red,
				borderColor: colors.red,
				borderWidth: 1,
				data: [
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3
				]
			}, {
        label: 'Avg. Performance',
				backgroundColor: colors.blue,
				borderColor: colors.blue,
				borderWidth: 1,
				data: [
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
					this.getRandomScalingFactor()*0.3,
				]
			}]
      };
      this.dummyData.radarChartValues.appliedCS = this.getRandomScalingFactor()
      this.dummyData.radarChartValues.theoreticalCS = this.getRandomScalingFactor()
      this.dummyData.radarChartValues.harwareSystems = this.getRandomScalingFactor()
      this.dummyData.radarChartValues.greenIT = this.getRandomScalingFactor()
      this.dummyData.radarChartValues.ai = this.getRandomScalingFactor()
      this.dummyData.radarChart.data = {
      labels: [['Applied CS ',this.dummyData.radarChartValues.appliedCS], ['Theoretical CS',this.dummyData.radarChartValues.theoreticalCS] , 
        ['Hardware & Systems',this.dummyData.radarChartValues.harwareSystems], ['Green IT',this.dummyData.radarChartValues.greenIT],
        ['AI',this.dummyData.radarChartValues.ai]],
			datasets: [{
				label: 'Total number of ECTS',
        pointBackgroundColor: colors.blue,
        borderColor: colors.blue,
        //transparent area as to not imply quadratic relationships of linear data
				backgroundColor: this.changeColorAlpha(colors.blue, "0"),
				borderWidth: 4,
				data: [
          this.dummyData.radarChartValues.appliedCS,
					this.dummyData.radarChartValues.theoreticalCS,
					this.dummyData.radarChartValues.harwareSystems,
					this.dummyData.radarChartValues.greenIT,
					this.dummyData.radarChartValues.ai
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