<template>
    <div>Hello world
        <v-btn @click="login">Login</v-btn>
    </div>
</template>
<script>

export default {
    methods: {
        login() {
            this.$auth.loginWith('laravelSanctum', {
                data: {
                    email: 'test@example.com',
                    password: "password"
                }
            })
        }
    }
}

</script>
