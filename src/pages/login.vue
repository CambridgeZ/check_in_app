<template>
    <div class="login">
        <h1>Login</h1>
        <form @submit.prevent="login">
            <input type="text" v-model="username" placeholder="Username" required>
            <input type="password" v-model="password" placeholder="Password" required>
            <button type="submit">Login</button>
            <a @click="goToRegisterPage">Register</a> 
        </form>
    </div>
</template>

<script>

export default {
    data() {
        return {
            username: '',
            password: ''
        };
    },
    methods: {
        async login() {
            const encoder = new TextEncoder();
            const data = encoder.encode(this.password);
            const hash = await window.crypto.subtle.digest('SHA-256', data);
            const hashedPassword = Array.from(new Uint8Array(hash)).map(b => b.toString(16).padStart(2, '0')).join('');

            fetch('http://localhost:3000/login', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    username: this.username,
                    password: hashedPassword
                })
            }).then(res => res.json())
                .then(res => {
                    if (res.success) {
                        uni.setStorageSync('token', res.token);
                        uni.setStorageSync('username', this.username);
                        uni.switchTab({
                            url: '/pages/index/index'
                        });
                    } else {
                        uni.showToast({
                            title: res.message,
                            icon: 'none'
                        });
                    }
                })
                .catch(err => {
                    console.error(err);
                    uni.showToast({
                        title: 'Login failed',
                        icon: 'none'
                    });
                });
        },
        goToRegisterPage() {
            uni.navigateTo({
                url: '/pages/Register' 
            });
        }
    }
};
</script>

<style scoped>
.login {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

h1 {
    margin-bottom: 2rem;
}

form {
    display: flex;
    flex-direction: column;
    align-items: center;
}

input {
    margin-bottom: 1rem;
    padding: 0.5rem;
    width: 15rem;
}

button {
    padding: 0.5rem 1rem;
    background-color: #007bff;
    color: #fff;
    border: none;
    cursor: pointer;
}

a{
    color: #007bff;
     text-align: center;
}
</style>
