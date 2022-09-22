<template>
  <div class="card" :style="{ 'background': `url(./${props.name}.jpg` }" @mouseenter="hover = true"
		@mouseleave="hover = false">
		<div class="card-filter"></div>
		<transition-group name="info" tag="div" v-if="loaded" class="text">
			<span class="country">{{ info.name.common }}</span>
			<span class="capital">{{ info.capital[0] }}</span>
			<template v-if="hover">
				<span class="about">Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsa minima
					aliquam
					amet inventore officiis nostrum exercitationem, qui alias voluptate harum.</span>
				<button class="explorebtn">Explore now</button>
			</template>
		</transition-group>
	</div>
</template>

<script setup>
  import { defineProps, onMounted, ref } from 'vue';
  const props = defineProps({
    name: {
      type: String,
      required: true
    }
  })
  const info = ref({})
  const loaded = ref(false)
  const hover = ref(false)

  onMounted(async () => {
    info.value = (await (await fetch(`https://restcountries.com/v3.1/capital/${props.name}`)).json())[0]
    console.log(info.value)
    loaded.value = true
  })
</script>

<style scoped>
/* CARD */
.card {
	background-position: center !important;
	width: 100%;
	height: 400px;
	background-size: cover !important;
	background-origin: border-box !important;
	background-repeat: no-repeat;
	border-radius: 10px;
	position: relative;
	box-shadow: inset 0 0 50px 0 black;
	display: grid;
	place-items: center;
	overflow: hidden
}
.card-filter {
	backdrop-filter: brightness(0.6);
	transition: all 0.5s ease;
	position: absolute;
	inset: 0;
}
.card:hover .card-filter {
	backdrop-filter: brightness(0.6) saturate(0.5);
}
/* CARD CONTENT */
.country {
	text-transform: uppercase;
	font-size: 1.2em;
	font-weight: 300;
}
.capital { 
	text-transform: uppercase;
	font-size: 2em;
	font-weight: bold
}
.text {
	display: grid;
	gap: 2em;
	place-items: center;
	color: white;
	position: relative;
	z-index: 1;
}
.explorebtn {
	all: unset;
	padding: 0.5em 1em;
	border: solid 1px white;
	border-radius: 0.2em;
	cursor: pointer;
	transition: all 0.2s ease;
	white-space: nowrap;
	margin: auto;
}
.explorebtn:hover {
	background: hsla(0, 0%, 0%, 0.5);
	box-shadow: 0 0 10px 0 hsl(0, 0%, 0%, 0.5);
}
.about {
	font-size: 0.8em;
	text-align: center;
	width: 200px;
}
/* TRANSITIONS */
.info-move,
.info-enter-active,
.info-leave-active {
	transition: all 0.5s ease;
}
.info-leave-active {
	position: absolute;
}
.info-enter-from,
.info-leave-to {
	opacity: 0;
	transform: translate(0%, 50px);
}
.info-enter-to,
.info-leave-from {
	opacity: 1;
	transform: translate(0%, 0%);
}
</style>