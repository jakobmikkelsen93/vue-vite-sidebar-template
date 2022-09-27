<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Sidebar from './components/Sidebar.vue'
</script>

<template>
	<div class="app">
		<!-- Sidebar -->
		<Sidebar />

		<!-- Content -->
    <div class="content">
      		<router-view />
    </div>
	</div>
</template>

<style scoped>
.content{margin: 1rem;

}

</style>
