<script>
import axios from 'axios';

export default {
    components: {
    },

    data() {
        return {
            profile:{}
        };
    },

    methods: {
        fetchData(){
            axios
            .get('http://127.0.0.1:8000/api/profile/' + this.$route.params.id)
            .then((response)=>{
                this.profile = response.data.data
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
        <h1>Show</h1>

        <ul>
            <li>{{ profile.location}}</li>
        </ul>
        
    </div>
</template>

<style lang="scss" scoped></style>