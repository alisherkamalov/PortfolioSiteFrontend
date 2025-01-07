<template>
    <v-container class="container">
        <HeaderApp></HeaderApp>
    </v-container>
</template>

<script>
import HeaderApp from '~/components/HeaderApp.vue';

</script>
<style scoped>
.container {
    display: flex;
    padding: 0;
    margin: 0;
    height: 100% !important;
    min-width: 100% !important;
}
@media (max-width: 1130px) {
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