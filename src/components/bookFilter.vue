
<template>
        <div>
      <button @click="sortByPrice" >By price</button>
      <button @click="sortByAlphabet" >By ABC</button>
      </div>
</template>
<script>
    export default {
        props: ['book'],
        methods: {
            sortByPrice(){
                console.log("TODO: log by price");
                $emit('byPrice');
            },
            sortByAlphabet(){
                console.log("TODO: log by price");
            }
        }
    }
</script>
    
     
   
