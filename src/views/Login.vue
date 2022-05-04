<template>
    <div>
        <form @submit.prevent="pressed">
            Login
            <div class="email">
                <input type="email" v-model="email" placeholder="email">
            </div>
            <div class="password">
                <input type="password" v-model="password" placeholder="password">
            </div>
            <button type="submit">Login</button>
        </form>
        <div class="error">{{ error.message }}</div>
        <span>Need an account? Click here to <router-link :to="{ name: 'register' }">Register</router-link>.</span>
    </div>
</template>

<script>
    import firebase from 'firebase';

    export default {
        name: 'AppLogin',
        data() {
            return {
                email: '',
                password: '',
                error: {
                    message: ''
                }
            }
        },
        methods: {
            async pressed() {
                try {
                    const user = await firebase.auth().signInWithEmailAndPassword(this.email, this.password);
                    console.log(user);
                    await this.$router.replace({name: 'secret'});
                }
                catch(err) {
                    this.error = err;
                    console.log(err);
                }
            }
        }
    }
</script>

<style scoped>
    .error {
        color: red;
        font-size: 18px;
    }
    input {
        width: 400px;
        padding: 30px;
        margin: 20px;
        font-size: 21px;
    }
    button {
        width: 400px;
        height: 75px;
        font-size: 100%;
    }
</style>