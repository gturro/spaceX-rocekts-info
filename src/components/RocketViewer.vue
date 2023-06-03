<template>
  <div id="rocket-viewer">
    <button id="returnBtn" @click="showGarden">BACK</button>
    <div class="card">
      <div class="img-container">
        <div class="carrousel-container">
          <img-carousel :imgSources="rocket.flickr_images"></img-carousel>
        </div>
        <div class="footer mt-4">
          <h3>{{ rocket.name }}</h3>
          <div class="text-start px-4">
            <p>{{ rocket.description }}</p>
            <p>Cost per launch: {{ formatedPriceWithDots }}$</p>
            <p>Sucess rate: {{ rocket.success_rate_pct }}%</p>
          </div>
        </div>
      </div>
      <div class="rocket-data">
        <div class="specs">
          <div class="dimensions">
            <h5 class="text-start">Dimensions and mass</h5>
            <div class="content">
              <p class="me-4">Height: {{ rocket.height.meters }}m</p>
              <p class="me-4">Width: {{ rocket.diameter.meters }}m</p>
              <p class="me-4">Mass: {{ rocket.mass.kg }}kg</p>
            </div>
          </div>
          <div class="payloads">
            <h5 class="text-start">Payloads</h5>
            <div class="content">
              <div v-for="(orbit, index) in rocket.payload_weights" :key="index" class="me-4">
                <p>ID: {{ orbit.id }}</p>
                <p>Mass: {{orbit.kg}}kg</p>
              </div>
            </div>
          </div>
          <div class="engines">
            <h5 class="text-start">Engines</h5>
            <div class="content">
              <p>Type: {{ rocket.engines.type }} <span v-if="rocket.engines.version">v.{{ rocket.engines.version }}</span></p>
              <div>
                <p>Isp</p>
                <p>Sea level: {{ rocket.engines.isp.sea_level }}</p>
                <p>Vacuum: {{ rocket.engines.isp.vacuum }}</p>
              </div>
              <div>
                <p>Thrust</p>
                <p>Sea level: {{ rocket.engines.thrust_sea_level.kN }}kN</p>
                <p>Vacuum: {{ rocket.engines.thrust_vacuum.kN }}kN</p>
              </div>
              <div>
                <p>Propellant 1: {{ rocket.engines.propellant_1 }}</p>
                <p>Propellant 2: {{ rocket.engines.propellant_2 }}</p>
              </div>
              <p>Thrust to weight ratio: {{ rocket.engines.thrust_to_weight }}</p>
            </div>
          </div>
          <div class="stages">
            <div class="content">
              <div class="stage">
                  <table class="table table-dark">
                    <tbody>
                      <tr>
                        <th><h6>First stage</h6></th>
                      </tr>
                      <tr>
                        <td>Is reusable: {{ rocket.first_stage.reusable ? 'Yes' : 'No' }}</td>
                      </tr>
                      <tr>
                        <td>Thrust sea level: {{ rocket.first_stage.thrust_sea_level.kN }}kN</td>
                      </tr>
                      <tr>
                        <td>Thrust vacuum: {{ rocket.first_stage.thrust_vacuum.kN }}kN</td>
                      </tr>
                      <tr>
                        <td>Engines: {{ rocket.first_stage.engines }}</td>
                      </tr>
                      <tr>
                        <td>Fuel capacity: {{ rocket.first_stage.fuel_amount_tons }}T</td>
                      </tr>
                      <tr>
                        <td v-if="rocket.first_stage.burn_time_sec">Burn time: {{ rocket.first_stage.burn_time_sec }}s</td>
                      </tr>
                    </tbody>
                  </table>
                  
              </div>
              <div class="stage">
                  <table class="table table-dark">
                    <tbody>
                      <tr>
                        <th><h6>Second stage</h6></th>
                      </tr>
                      <tr>
                        <td>Is reusable: {{ rocket.second_stage.reusable ? 'Yes' : 'No' }}</td>
                      </tr>
                      <tr>
                        <td>Thrust {{ rocket.second_stage.thrust.kN }}kN</td>
                      </tr>
                      <tr><td><br></td></tr>
                      <tr>
                        <td>Engines: {{ rocket.second_stage.engines }}</td>
                      </tr>
                      <tr>
                        <td>Fuel capacity: {{ rocket.first_stage.fuel_amount_tons }}T</td>
                      </tr>
                      <tr>
                        <td v-if="rocket.first_stage.burn_time_sec">Burn time: {{ rocket.first_stage.burn_time_sec }}s</td>
                      </tr>
                    </tbody>
                  </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    </div>
    
</template>

<script>
import ImgCarousel from './ImgCarrousel.vue'
export default {
  name: 'RocketViewer',
  emits: [
    'show-garden'
  ],
  components: {
    ImgCarousel
  }, 
  props: {
    rocket: Object,
  },
  data() {
    return {

    }
  },
  computed: {
    formatedPriceWithDots() {
      let price = this.rocket.cost_per_launch
      let priceStr = price.toString()
      let result = ''
      for (let i = priceStr.length - 1, j = 1; i >= 0; i--, j++) {
        result = priceStr[i] + result
        if (j % 3 === 0 && i !== 0) {
          result = '.'+result
        } 
      }
      return result
    }
  },
  methods: {
    showGarden() {
      this.$emit('show-garden')
    }
  },
  mounted () {

  }

}
</script>

<style lang="css" scoped>
  #rocket-viewer {
    position: relative;
    width: 80%;
    height: 80vh;
    margin: auto;
    margin-top: 20px;
  }
  #returnBtn {
    width: 60px;
    position: absolute;
    left: -80px;
    top: 40px;
  }
  #rocket-viewer .card {
    display: flex;
    flex-direction: row;
  }
  .img-container{
    width: 40%;
    display: flex;
    flex-direction: column;
  }
  .rocket-data {
    flex-grow: 1;
    padding: 20px;
    background-color: aquamarine;
  }
  .carrousel-container {
    flex-grow: 1;
  }
  .specs {
    height: 100%;
    display: flex;
    flex-direction: column;
  }
  .content {
    display: flex;
    flex-grow: 1;
    text-align: start;
  }
  .stages {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
  }
  .stages .content .stage {
    flex-grow: 1;
  }
  p {
    margin-bottom: 10px
  }
  .table-dark {
    color: #fff;
    background-color: #343a40;
  }
  .table tbody th, .table tbody td {
    border: none;
    border-bottom: 3px solid #2b3035;
    font-size: 14px;
  }
</style>
