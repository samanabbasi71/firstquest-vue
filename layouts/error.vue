<template>
        <div class="error">
            <h1 class="error-h1">Page Not found</h1>
            <a href='/' class="error-btn">
                back to home
            </a>
        </div>
</template>

<script>
export default {

}
</script>

<style scoped>
    .error {
    min-height: calc(100vh);
    background-image: url('~@/assets/img/1.png');
    /* background: linear-gradient(rgba(0,0,0,0.05), rgba(0,0,0,0.05)); */
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    transition: all 0.3s ease-in-out;
    text-align: center;
    padding: 8rem;
}
.error-h1 {
    text-transform: capitalize;
    margin-bottom: 2rem;
    }
.error-btn {
        text-decoration: none;
        margin: 0 auto 1rem auto;
        text-transform: capitalize;
        padding: 8px 20px;
        border-radius: 5px;
        font-size: 16px;
        background-color: orangered;
        border: none;
        outline: none !important;
        box-shadow: none;
        color: #fff;
        cursor: pointer;
    }
</style>