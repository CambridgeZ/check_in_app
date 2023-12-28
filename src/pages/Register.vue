<template>
    <div class="register">
        <h1>注册页面</h1>
        <form @submit="submitForm">
            <label for="username">用户名:</label>
            <input type="text" id="username" v-model="username" required>
            
            <label for="password">密码:</label>
            <input type="password" id="password" v-model="password" required>
            
            <label for="confirmPassword">确认密码:</label>
            <input type="password" id="confirmPassword" v-model="confirmPassword" required>
            
            <button type="submit">注册</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            username: '',
            password: '',
            confirmPassword: ''
        };
    },
    methods: {
        submitForm() {
            // 在这里处理表单提交逻辑
            // 可以使用 this.username, this.password 和 this.confirmPassword 来访问表单数据
        }
    }
};
</script>

<style scoped>
.register {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 4px;
}
</style>
