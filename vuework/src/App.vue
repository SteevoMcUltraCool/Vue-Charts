<script setup>
import point from './components/point.vue';
import barGraph from './components/barGraph.vue'
import pieChart from './components/pieChart.vue';
import { nextTick,ref } from 'vue';
import {dataBIG} from './components/getAPI.vue'
let year = 2019
let renderComponent = ref(false)
let data 
async function name() {
	data = await dataBIG()
	data = await data.json()
	renderComponent.value = true
}
name()
const forceRerender = async () => {
  renderComponent.value = false;
	await nextTick();
  renderComponent.value = true;
}
let changeyear = function(x){
  year+=x
  console.log(year)
  forceRerender()
  
}
</script>
<template>
  <point @click="changeyear(-1)" :text="'Previous Year'" v-if="renderComponent"></point>
  <point @click="changeyear(1)" :text="'Next Year'" v-if="renderComponent"></point>
  <div class="cont">
  <h2  v-if="renderComponent">Miscarriage Rates in {{ year }}</h2>
  <p> <i>by Steve and Ness</i> </p>
  </div>
  <div class="cont">
  	<barGraph :year="year" v-if="renderComponent" :data="data"></barGraph>
  	<pieChart :year="year" v-if="renderComponent"></pieChart>
  </div>
  <h3 v-if="year=='2018' || Number(year)<2007 || Number(year)>2019">No data for this year</h3>
</template>

<style scoped>
	.cont {
		display: flex
	}
</style>




