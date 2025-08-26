<template>
  <div class="results-time" v-if="formattedTime">現地日時：{{ formattedTime }}</div>
  <div class="results-country" v-if="country">{{ country }}</div>
  <div class="results-city" v-if="cityName">{{ cityName }}</div>
  <div class="results-temp" v-if="temperature">{{ temperature }}</div>
  <div class="results-condition" v-if="icon">
    <img :src="icon" alt="icon">
    <span>{{ conditionText }}</span>
  </div>
</template>

<script setup>
import { toRefs, computed } from 'vue'

const props = defineProps({
  results: Object
})

const { localtime, country, cityName, temperature, icon, conditionText } = toRefs(props.results)

const formattedTime = computed(() => {
  if (!localtime.value) return ''
  const date = new Date(localtime.value)
  const yyyy = date.getFullYear()
  const mm = String(date.getMonth() + 1).padStart(2, '0')
  const dd = String(date.getDate()).padStart(2, '0')
  const hh = String(date.getHours()).padStart(2, '0')
  const min = String(date.getMinutes()).padStart(2, '0')
  return `${yyyy}年${mm}月${dd}日 ${hh}:${min}`
})
</script>