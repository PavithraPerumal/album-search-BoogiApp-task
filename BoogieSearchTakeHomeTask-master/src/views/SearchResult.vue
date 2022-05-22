<template>
    <div>
        <h1>List of album</h1>
    </div>
</template>
<script>
import axios from 'axios'
export default{
    name:"searchresult",
    mounted(){
        axios.get(`theaudiodb.com/api/v1/json/2/search.php?s=coldplay`)
        .then(response=>console.log(response));
    }
}
</script>
<style>
</style>