<template>
	<div class="weather">
		<span class="city">{{city}}</span>：
		<span class="temperature">{{temperature}}&#8451;</span>
		<span class="state" v-bind:class="{fine:isFine,cloudy:isCloudy}">{{state}}</span>
	</div>
</template>
<script>
	import weatherMsg from '../api/getWeather.js'
	export default{
		data: ()=>{
			return {
				city: '',
				temperature: '',
				state: '',
			}
		},
		created(){
			// 请求天气信息
			weatherMsg().then(str=>{
				let weatherMsg = JSON.parse(str);
				// 城市
				this.city = weatherMsg.data.weather.city;
				// 温度
				this.temperature = weatherMsg.data.weather.tem;
				// 天气状况
				this.state = weatherMsg.data.weather.weather;
			},err=>{
				window.alert(err);
			});
		},
		computed: {
			isFine(){
				return (this.state == '晴' || this.state == '多云');
			},
			isCloudy(){
				return (this.state == '阴');
			}
		}
	};
</script>
<style scoped>
	.state{
		color: white;
		background-color: blue;
	}
	.state.fine{
		color: black;
		background-color: orange;
	}
	.state.cloudy{
		color: white;
		background-color: gray;
	}
</style>