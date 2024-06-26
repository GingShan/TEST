<script setup>
    import { useRoute, useRouter } from 'vue-router'
    import { ref } from 'vue'

    const route = useRoute()
    console.log(route);
    const id = route.params.id
    const detailItem = ref([])

    const apiHandler = async () => {
        try {
            const response = await fetch(`https://min-api.cryptocompare.com/data/top/totalvolfull?limit=10&tsym=USD/${id}`)
            const data = await response.json()
            console.log(data);
            detailItem.value = data
        } catch (error) {
            console.log(error);
        }
    }
    apiHandler()
</script>

<template>
        
</template>
    
<style>
    
</style>