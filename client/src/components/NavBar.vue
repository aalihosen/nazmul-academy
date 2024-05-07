<template>
    <nav class="bg-dark-blue w-full xs:h-16 h-14">
        <ul class="w-full h-full flex items-center justify-end xs:px-10 px-5 xs:gap-6 gap-3 xs:text-xl text-md">
            <li class="nav-link mr-auto xs:text-2xl text-lg">
                <router-link to="/" title="Home">Blog</router-link>
            </li>
            <li class="nav-link">
                <router-link to="/explore" title="Explore">Explore</router-link>
            </li>
            <li class="nav-link">
                <router-link to="/login" title="Login" v-if="!loggedIn">Login</router-link>
                <button to="/logout" v-else @click.prevent="logOut()">Log Out</button>
            </li>
            <li class="nav-link">
                <a class="hover:underline" href="https://www.linkedin.com/in/nazmul-hasan-260a14231/">
                    <img class="fill-light-blue xs:w-8 w-6 transition hover:fill-blue" role="img" viewBox="0 0 24 24" src="../assets/nazmul.svg" alt="404 Not Found">
                </a>
            </li>
        </ul>
    </nav>
</template>

<script>
    export default {
        name: "NavBar",
        data(){
            return {
                loggedIn: false
            }
        },
        watch: {
            "$route": "checkLogin"
        },
        created(){
            this.checkLogin();
        },
        methods: {
            checkLogin(){
                const loggedIn = JSON.parse(window.localStorage.getItem("login"))?.loggedIn || false;

                if (loggedIn === true){
                    this.loggedIn = true
                }
            },
            logOut(){
                window.localStorage.setItem("login", JSON.stringify(false));
                this.$router.push("/login")
            }
        }
    }
</script>