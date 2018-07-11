<template>
    <div class="users">
        <div class="loading" v-if="loading">
            Loading...
        </div>

        <div v-if="error" class="error">
            {{ error }}
        </div>

        <ul v-if="users">
            <li v-for="( name, index) in users" :key="index">
                <strong>Name:</strong> {{ name.name }},
                <strong>Email:</strong> {{ name.email }}
            </li>
        </ul>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    data() {
        return {
            loading: false,
            users: null,
            error: null,
        };
    },
    created() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            this.error = this.users = null;
            this.loading = true;
            axios
                .get('/api/users')
                .then(response => {
                    this.loading = false;
                    console.log(response.data.data);
                    this.users = response.data.data;
                }).catch(error =>{
                    this.loading = false;
                    this.error = error.response.data.message || error.message;
                });
        }
    }, 
    

}

</script>