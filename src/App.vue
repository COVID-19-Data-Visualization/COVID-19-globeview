<template>
  <div id="app">
    <v-chart :options="globe"/>
  </div>
</template>

<style>
  /**
   * The default size is 600px×400px, for responsive charts
   * you may need to set percentage values as follows (also
   * don't forget to provide a size for the container).
   */
  body {
    margin: 0;
  }

  #app {
    height: 100vh;
    width: 100%;
  }

  .selectable:hover {
    border: 1px;
    height: 30px;
  }

  h4 {
    font-family: sans-serif;
    color: white;
    margin: 0 10px;
  }

  .content {
    margin: 0 10px;
    font-family: sans-serif;
  }

  .content > .content-line {
    display: flex;
    justify-content: space-between;
  }

  .content-line > .right-item {
    margin-left: 10px;
  }

  #about {
    position: absolute;
    bottom: 0;
    left: 40%;
    margin: 0 10px;
    background-color: transparent;
    color: lightgrey;
    border: 1px solid lightgrey;
    border-radius: 4px 4px 0 0;
    cursor: pointer !important;
  }

  #data-box {
    position: absolute;
    top: 5%;
    left: 0;
    margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    color: #fff;
    background: transparent;
  }

  #stats {
    width: 200px;
    padding: 5px 0;
    margin-bottom: 10px;
    color: white;
    border: 1px solid white;
    border-radius: 4px;
    background-color: transparent;
  }

  #controls {
    width: 200px;
    /*background-color: transparent;*/
    color: white;
    border: 1px solid white;
    border-radius: 4px;
  }

  #controls-section {
    font-size: 15px;
    margin: 4px;
    padding: 4px;
    display: flex;
    flex-direction: column;
  }

  button {
    margin-top: 4px;
    background-color: transparent;
    border: 1px solid white;
    border-radius: 4px;
    cursor: pointer !important;
    color: white;
  }

  button:hover {
    color: black;
    background-color: white;
  }

  button:active {
    color: black;
  }

  a {
    margin-left: 5px;
  }

  .echarts {
    width: 100%;
    height: 100vh;
  }
</style>

<script>
    import ECharts from 'vue-echarts'
    import 'echarts/lib/chart/line'
    import 'echarts/lib/component/polar'
    // import axios from 'axios'
    import world from './assets/world.topo.bathy.200401.jpg'
    import starfield from './assets/starfield.jpg'
    // import papa from "papaparse";

    export default {
        created() {
           //TODO change window.onload code to here
        },
        name: 'App',
        components: {
            'v-chart': ECharts
        },
        data() {
            return {
                daily_reports: "https://api.github.com/repos/CSSEGISandData/COVID-19/contents/csse_covid_19_data/csse_covid_19_daily_reports/"
            }
        },
        computed: {
            globe: () => {
                return {
                    globe: {
                        baseTexture: world,
                        heightTexture: world,
                        environment: starfield,
                        displacementScale: 0.03,
                        displacementQuality: 'high',
                        // globeRadius: 200,
                        // globeOuterRadius: 110,
                        // baseColor: '#ccc',
                        shading: 'color',
                        viewControl: {
                            autoRotate: true,
                            autoRotateAfterStill: 30,
                            distance: 300
                        }
                    },
                    series: {
                        type: "scatter3D",
                        coordinateSystem: "globe",
                        // symbolSize: data => dataScaleCalculation(data[3]),
                        label: {
                            show: false,
                            formatter: () => ""
                        },
                        itemStyle: {
                            color: "darkred",
                            opacity: 1
                        },
                        animation: false,
                        blendMode: "source-over",
                        //TODO data here
                        data:[[112.2707, 30.9756, 0, 101204]]
                    }
                }
            }

        },

        methods: {
            // getData(dataType) {
            // getData: async function (dataType) {
            //     let data = await axios({
            //         method: 'get',
            //         url: `https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_19-covid-${dataType}.csv`
            //     })
            //     console.log(data)
            // },

        }
    }
</script>