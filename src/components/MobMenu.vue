<template>
	<div class="mob-menu" :class="{ active: isActive }">
		<a href="#"> <jobs-svg /> ვაკანსიები </a>
		<a href="#"> <companies-svg /> კომპანიები </a>
		<a v-if="user" href="#">
			პროფილი
		</a>
		<a v-if="user" href="#" @click="emitLogoutEvent()">
			გასვლა
		</a>
		<a v-if="!user" href="#" @click="routeToRegistration()">
			დარეგისტრირება
		</a>
		<a v-if="!user" href="#" @click="routeToLogin()">
			შესვლა
		</a>
	</div>
</template>

<script>
import CompaniesSvg from './svgs/companiesSvg.vue';
import JobsSvg from './svgs/JobsSvg.vue';
import { mapState } from 'vuex';
export default {
	name: 'MobMenu',
	emits: ['logout', 'close'],
	components: {
		JobsSvg,
		CompaniesSvg,
	},
	props: {
		isActive: Boolean,
	},
	methods: {
		routeToRegistration() {
			this.$router.push({ name: 'register' });
			this.emitDropdownCloseEvent();
		},
		routeToLogin() {
			this.$router.push({ name: 'login' });
			this.emitDropdownCloseEvent();
		},
		emitDropdownCloseEvent() {
			this.$emit('close');
		},
		emitLogoutEvent() {
			this.$emit('logout');
		},
	},
	computed: {
		...mapState(['user']),
	},
};
</script>

<style>
.mob-menu {
	position: absolute;
	display: none;
	flex-direction: column;
	background: #fff;
	left: 0;
	right: 0;
	top: 100%;
	z-index: 10;
}

.mob-menu.active {
	display: flex;
}

.mob-menu a {
	padding: 1rem 1.2rem;
	/* background: rgb(0 0 0 / 5%); */
	display: block;
	text-decoration: none;
	font-size: 18px;
	border-top: 1px solid #dcdcdc;
}
</style>
