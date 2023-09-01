<!-- 3. Reactivity Fundamentals: Use of <script setup> tag -->
<script setup>
/* 11. Router */
import { RouterView } from 'vue-router'

import PageHeader from './components/PageHeader.vue'
import PageNavbar from './components/PageNavbar.vue'
import PageFooter from './components/PageFooter.vue'
</script>

<template>
  <PageHeader title="Exploring Vue 3 (part 2)" subtitle="Created for the SIT120 2.3C task"/>
  <PageNavbar/>
  <RouterView/>
  <PageFooter/>
</template>