<template>
        <header class="main-header">
            <h3 class="header-title">
                iran trip planer
            </h3>
            <div class="home-header-about">
            <h1 >
                Plan your trip iran
            </h1>
            <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sed laboriosam corrupti ex id rem temporibus, ipsa repellat nam fuga molestiae saepe nemo officia reprehenderit aliquid accusamus officiis, rerum illum obcaecati quasi esse debitis dolore doloribus quae autem?
            </p>
            </div>
        </header>
</template>

<script>
export default {

}
</script>

<style scoped>
.main-header {
    min-height: calc(30vh);
    background-image: url('~@/assets/img/1.png');
    /* background: linear-gradient(rgba(0,0,0,0.05), rgba(0,0,0,0.05)); */
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    transition: all 0.3s ease-in-out;
    color: #fff;
    text-transform: capitalize;
    padding: 1.5rem 1.5rem 4rem;
    font-size: 1.3rem;
    line-height: 35px;
}

@media screen and (min-width: 768px) {
    .main-header {
        min-height: calc(50vh);
    }
}

</style>