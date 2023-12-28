<template>
    <div class="startup-page">
        <h1 style="color: navy;">Welcome!</h1>
        <button @click="goToLoginPage">登录</button> 
    </div>
</template>

<script>
export default {
    name: "StartupPage",
    methods: {
        goToLoginPage() {
            uni.navigateTo({
                url: '/pages/login' 
            });
        }
    },
};
</script>

<style scoped>
.startup-page {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-size: 36px;
    font-weight: bolder;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    background-color: antiquewhite;
}
</style>
