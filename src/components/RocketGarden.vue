<template>
  <div>
    <section class="py-1 text-center container">
      <div class="row py-lg-5">
        <div class="col-lg-6 col-md-8 mx-auto">
          <h1 class="fw-light">Space X rocket data</h1>
          <p class="lead text-body-secondary">All technical information about all the different rockets that Space X operates</p>
        </div>
      </div>
    </section>
    <div class="album bg-body-tertiary">
      <div class="container">
        <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 g-3">
          <div v-for="rocket in rockets" :key="rocket.id" class="col">
            <div class="card shadow-sm">
              <img class="card-img-top" :src="rocket.flickr_images[0]" width="100%" height="225">
              <div class="card-body">
                <p class="card-title">{{ rocket.name }}</p>
                <div class="d-flex justify-content-between align-items-center">
                  <div class="btn-group">
                    <button type="button" class="btn btn-sm btn-outline-secondary" @click="showRocket(rocket)">View</button>
                  </div>
                  <small class="text-body-secondary">First flight: {{ rocket.first_flight }}</small>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RocketGarden',
  emits: [
    'show-rocket'
  ],
  props: {
    rockets: Object,
  },
  data() {
    return {
    }
  },
  computed () {

  },
  methods: {
    showRocket (rocket) {
      this.$emit('show-rocket', rocket)
    }
  },
  mounted () {

  }

}
</script>

<style scoped>

</style>
