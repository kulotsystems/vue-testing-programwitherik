<template>
    <div>
        Logged in
        <span v-if="loggedIn">Yes</span>
        <span v-else>No</span>
        <div>
            <button @click="signOut">Sign out</button>
        </div>
    </div>
</template>

<script>
    import firebase from 'firebase/app';
    import 'firebase/auth';

    export default {
        name: 'TopHeader',
        data() {
            return {
                loggedIn: false
            }
        },
        methods: {
            async signOut() {
                try {
                    const data = await firebase.auth().signOut();
                    console.log(data);
                    await this.$router.replace({name: 'login'});
                }
                catch (err) {
                    console.log(err);
                }
            }
        },
        created() {
            firebase.auth().onAuthStateChanged(user => {
                if(user) {
                    this.loggedIn = true;
                }
                else {
                    this.loggedIn = false;
                }
            });
        }
    }
</script>

<style scoped>

</style>