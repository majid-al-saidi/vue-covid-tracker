<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{title}}</h2>
        <div class="text2xl mt-4 mb-10">{{timestamp}}</div>
    </div>
</template>

<script>
import moment from 'moment';
export default{
    name:'DateTitle',
    props:['title' , 'date'],
    computed:{
        timestamp: function(){
            return moment(this.date).format('MMMM Do YYYY, h:mm:ss a');
        },
    },
}
</script>