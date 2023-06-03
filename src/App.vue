<template>
  <Transition name="fade" mode="out-in">
    <rocket-garden v-if="currentComp == 'garden'"
      :rockets="rocketData"
      @show-rocket="showRocket">
    </rocket-garden>
    <rocket-viewer v-else :rocket="rocketSelected" @show-garden="showGarden"></rocket-viewer>
  </Transition>
  
</template>

<script>
import RocketGarden from './components/RocketGarden.vue';
import RocketViewer from './components/RocketViewer.vue';

export default {
  name: 'App',
  components: {
    RocketGarden,
    RocketViewer
  },
  data() { 
        return {
            rocketData: {},
            rocketSelected: {},
            comp: ['garden', 'viewer'],
            currentComp: 'garden',
        };
  },
  methods: {
    showRocket(rocket){
      console.log("reading from app")
      this.currentComp = this.comp[1]
      this.rocketSelected = rocket
    },
    showGarden() {
      this.currentComp = this.comp[0]
    }
  },
  mounted() {
    fetch('https://api.spacexdata.com/v4/rockets/')
      .then(response => response.json())
      .then(data => {
        this.rocketData = data
        console.log(data)
      })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
