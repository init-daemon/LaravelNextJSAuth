<template>
    <v-row>
        <v-col class="mx-auto rounded-xl" cols="12" md="6">
            <v-card>
                <v-card-text>
                    <v-form>
                        <v-text-field v-model="email" type="email" label="Email" id="email"></v-text-field>
                        <v-text-field v-model="password" type="password" label="Password" id="password"></v-text-field>
                        <v-btn color="success" @click="login">S'authentifier</v-btn>
                    </v-form>
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
</template>
<script>

export default {
    layout: "auth",
    data() {
        return {
            email: 'test@example.com',
            password: 'password'
        }
    },
    methods: {
        login() {
            this.$auth.loginWith('laravelSanctum', {
                data: {
                    email: this.email,
                    password: this.password
                }
            })
        }
    }
}

</script>
