<script>
import axios from 'axios';

export default {
    components: {
    },

    data() {
        return {
            profile:{},
            user:{}
        };
    },

    methods: {
        fetchData(){
            axios
            .get('http://127.0.0.1:8000/api/profile/' + this.$route.params.id)
            .then((response)=>{
                this.user = response.data.users.data
                this.profile = response.data.profiles.data
            })
        },
        getImageUrl(profile) {
            return `http://127.0.0.1:8000/storage/${profile.photo}`;
        },

    },

    mounted() {
        this.fetchData()
    },
};
</script>


<template>
    <div class="container">
        <h1>Show</h1>

        <ul>
            <li>{{user[0]?.name}}</li>
            <li>{{user[0]?.surname}}</li>
            <li>{{user[0]?.email}}</li>
            <li>{{profile[0]?.photo}}</li>
            <li>{{profile[0]?.phone}}</li>
            <li>{{profile[0]?.location}}</li>  
            <li>{{user[0]?.specializations.map(specializations => specializations.name).join(', ') }}</li>  
            <li>{{profile[0]?.description}}</li>
        </ul >
    </div>
</template>

<style lang="scss" scoped></style>