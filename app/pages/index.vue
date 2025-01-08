<template>
    <v-container class="container" :style="{
        transform: `translateX(-${translatedCont}px)`,
    }">
        <HeaderApp @nextClicked="onNextClicked" />
        <UsingTechnologies />
    </v-container>
</template>


<script setup>
import { ref } from 'vue';

const translatedCont = ref(0);
function onNextClicked() {

    translatedCont.value += window.innerWidth; 
}
</script>


<style scoped>
.container {
    display: flex;
    padding: 0;
    margin: 0;
    height: 100% !important;
    min-width: 100% !important;
    transition: all 0.3s cubic-bezier(0.075, 0.82, 0.165, 1);
    transition-delay: 0.2s;
}

@media (max-width: 1130px) {
    .container {
        flex-direction: column;
    }
}
@media (min-width: 501px) {
    .container {
        flex-direction: column;
    }
}
@media (max-width: 500px) {
    .container {
        flex-direction: row;
    }
}
</style>
