<template>
    <div class="container">
        <div class="login-card">
            <form @submit.prevent="handleSubmit">
                <input type="text" placeholder="Name" id="name" v-model="name" />
                <input type="email" placeholder="Email" id="email" v-model="email" />
                <div class="password-wrapper">
                    <input :type="showIcon ? 'text' : 'password'" placeholder="Password" id="password"
                        v-model="password" />
                    <i :class="showIcon ? 'fas fa-eye' : 'fas fa-eye-slash'" @click="togglePassword"></i>
                </div>
                <button type="submit">Sign Up</button>
            </form>
        </div>
    </div>
</template>

<script>
import axios from '../plugins/axios';
export default {
    name: 'HomeView',
    data() {
        return {
            showIcon: false,
            name: '',
            email: '',
            password: ''
        };
    },
    methods: {
        handleSubmit() {
            const userData = {
                name: this.name,
                email: this.email,
                password: this.password
            };
            localStorage.setItem('user', JSON.stringify(userData));
            this.sendEmail(this.email);
        },
        togglePassword() {
            this.showIcon = !this.showIcon;
        },
        async sendEmail(email) {
            try {
                const response = await axios.post('/api/emailsender', { email });
                if (response.status === 200) {
                    console.log('Email sent successfully');
                } else {
                    console.error('Failed to send email');
                }
            } catch (error) {
                console.error('Error sending email:', error);
            }
        }
    }
};
</script>

<style scoped>
.container {
    display: flex;
    position: absolute;
    top: 0;
    left: 0;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;
    background-color: #17212b;
}

.login-card {
    width: 30%;
    border-radius: 10px;
    height: auto;
    background-color: aliceblue;
    padding: 30px;
}

.login-card form {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 30px;
}

.password-wrapper {
    position: relative;
    width: 100%;
}

.password-wrapper input {
    width: 100%;
    padding-right: 30px;
    box-sizing: border-box;
}

.password-wrapper i {
    position: absolute;
    right: 10px;
    top: 50%;
    transform: translateY(-50%);
    cursor: pointer;
}

form input,
form button {
    padding: 10px;
    outline: none;
    border: 0px;
    width: 100%;
    box-sizing: border-box;
}

form button {
    background-color: #007bff;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 5px;
}

form button:hover {
    background-color: #0056b3;
}
</style>