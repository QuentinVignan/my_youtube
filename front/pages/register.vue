<template>
    <div>
        <div>
            <Header />
        </div>
        <br>
        <br>
        <br>
        <br>
        <div class="container container-table">
            <form class="col-xs-4 col-xs-offset-4" onsubmit="return false">
                <div class="form-group">
                    <label for="username">Username</label>
                    <input type="text" class="form-control" id="user" v-model="userName" placeholder="Username">
                </div>
                <div class="form-group">
                    <label for="username">Pseudo</label>
                    <input type="text" class="form-control" id="pseudo" v-model="pseudo" placeholder="Pseudo">
                </div>
                <div class="form-group">
                    <label for="email">Email</label>
                    <input type="email" class="form-control" id="email" aria-describedby="emailHelp" v-model="mail" placeholder="Enter email">
                </div>
                <div class="form-group">
                    <label for="userPassword">Password</label>
                    <input type="password" class="form-control" id="password" v-model="password" placeholder="Password">
                </div>
                <button class="btn btn-primary" v-on:click="registerCall">Submit</button>
            </form>
        </div>
    </div>
    
</template>


<script>
export default {
    data() {
        return {
            apiUrl: process.env.apiUrl,
            userName: "",
            password: "",
            mail: "",
            pseudo: "",
        }
    },
    methods: {
            async registerCall(e) {
                try {
                    const responseR = await this.$axios.$post(this.apiUrl + '/user?username=' + this.userName + '&password=' + this.password + '&pseudo=' + this.pseudo + '&email=' + this.mail);
                    this.responseR = responseR;
                } catch (error) {
                    alert("please enter/check all credantials or user already exist");
                    location.reload();
                }
                try {
                    const response = await this.$axios.$post(this.apiUrl + '/auth?login=' + this.userName + '&password=' + this.password);
                    this.response = response;
                    sessionStorage.setItem("username" , this.response ["data"]["user"]["username"]);
                    sessionStorage.setItem("id" , this.response ["data"]["user"]["id"]);
                    sessionStorage.setItem("token" , this.response ["data"]["token"]);
                    this.$router.push({path: "/"})
                } catch (error) {
                    
                }
                    
            }
        }
}
</script>