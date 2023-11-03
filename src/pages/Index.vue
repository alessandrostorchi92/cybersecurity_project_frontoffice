<script>
import axios from 'axios';

export default {
    components: {
    },

    data() {
        return {
            users:[]
        };
    },
    methods: {
        fetchData(){
            axios
            .get('http://127.0.0.1:8000/api/users')
            .then((response)=>{
                this.users = response.data.data;
            })

        }

    },

    mounted() {
        this.fetchData()
    },
};
</script>


<template>
    <div class="container">
        <h1>Index</h1>
    </div>

<ul v-for="user in users">
    <li><router-link :to="{name:'show', params: {id: user.id}}">{{ user.name}}</router-link></li>
</ul>

</template>

<style lang="scss" scoped></style>