<template>
    <div class="login-container">
        <div class="login-box">
            <h2>Login</h2>
            <form @submit.prevent="handleSubmit">
                <div class="input-group">
                    <label for="username">Username:</label>
                    <input type="text" id="username" placeholder="Username" v-model="username" required />
                </div>
                <div class="input-group">
                    <label for="password">Password:</label>
                    <input type="password" id="password" placeholder="Password" v-model="password" required />
                </div>
                <button type="submit">Submit</button>
            </form>
        </div>
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
        handleSubmit() {
            // Handle login logic here
            console.log('Username:', this.username);
            console.log('Password:', this.password);

            this.$router.push("/dashboard");
        }
    }
};
</script>

<style scoped>
.login-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    /* Add the following line to center horizontally */
    margin: 0 auto;

}

.login-box {
    width: 300px;
    padding: 20px;
    background-color: var(--vt-c-background-lighter);
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
}

.input-group {
    margin-bottom: 15px;
    display: flex;
    flex-direction: row;
    line-height: 2;
}

h2 {
    color: var(--color-heading);
    margin-bottom: 20px;
}

label {
    display: none;
    width: 100px;
    text-align: right;
    margin-right: 10px;
}

input {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
}

button {
    padding: 10px;
    background-color: var(--color-blue);
    color: var(--color-text-dark);
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, color 0.3s ease;
}

button:hover {
    background-color: var(--color-blue-dark);
    color: var(--color-text);
}
</style>