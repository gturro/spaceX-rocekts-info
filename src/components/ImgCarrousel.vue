<template>
    <div id="rocketImages" class="carousel slide">
        <div class="carousel-indicators">
            <button type="button" data-bs-target="#rocketImages" v-for="(item, index) in imgSources" :key="index" :class="index == 0 ? 'active' : '' " :data-bs-slide-to="index" aria-current="true" :aria-label=" 'Slide ' + index"></button>
        </div>
        <div class="carousel-inner">
            <div class="carousel-item" v-for="(img, index) in imgSources" :key="index" :class="index == 0 ? 'active' : '' ">
                <img :src="img" class="d-block w-100">
            </div>
        </div>
        <button class="carousel-control-prev" type="button" data-bs-target="#rocketImages" data-bs-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#rocketImages" data-bs-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Next</span>
        </button>
    </div>
</template>
<script>
export default {
    props: {
        imgSources: Array
    }
}
</script>
<style lang="css" scoped>
    #rocketImages, .carousel-inner, .carousel-item, img {
        height: 100%;
    }
    img {
        object-fit: cover;
        object-position: center;
    }
</style>