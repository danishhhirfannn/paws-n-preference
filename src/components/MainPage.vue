<script setup>
import Card from '@/volt/Card.vue'
import Button from '@/volt/Button.vue'
</script>

<template>
    <div class="flex flex-col items-center flex-1 pb-6">
        <Card 
        class="w-95 h-full"
        style="overflow: hidden; background-image: url('https://primefaces.org/cdn/primevue/images/card-vue.jpg'); background-size: cover; background-position: center; background-repeat: no-repeat;">
        </Card>
        <div class="card flex grow justify-between items-center absolute bottom-30 gap-4">
            <Button 
                class="!w-20 !h-20 !text-4xl bg-opacity-90 !outline-none !ring-0 !border-0" 
                icon="pi pi-times" 
                raised 
                rounded 
                size="large"
                style="outline: none !important; box-shadow: none !important;"
            ></Button>
            <Button 
                class="!w-20 !h-20 !text-4xl bg-red-500 bg-opacity-90 !outline-none !ring-0 !border-0" 
                icon="pi pi-heart" 
                raised 
                rounded 
                size="large"
                style="outline: none !important; box-shadow: none !important;"
            ></Button>
        </div>
    </div>
   
</template>

<style scoped>

</style>