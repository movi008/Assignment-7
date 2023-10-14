<script setup>
import { RouterView } from 'vue-router';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';

</script>
<template>
    <div>
        <Header />
        <div class="flex">
            <router-view class="flex-1 p-4" />
        </div>
        <Footer />
    </div>
</template>
