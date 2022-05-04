<template>
    <div>
        <form @submit.prevent="pressed">
            Register
            <div class="email">
                <input type="email" v-model="email" placeholder="email">
            </div>
            <div class="password">
                <input type="password" v-model="password" placeholder="password">
            </div>
            <button type="submit">Register</button>
        </form>
        <div class="error">{{ error.message }}</div>
        <span>Already have an account? Click here to <router-link :to="{ name: 'login' }">Login</router-link>.</span>
    </div>
</template>

<script>
    import firebase from 'firebase/app';
    import 'firebase/auth';

    export default {
        name: 'AppRegister',
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
                    const user = await firebase.auth().createUserWithEmailAndPassword(this.email, this.password);
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