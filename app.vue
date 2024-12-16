<script
	setup
	lang="ts"
>
import Toaster from '@/components/ui-kit/toast/Toaster.vue';
</script>

<template>
	<div>
		<NuxtRouteAnnouncer />
		<NuxtLayout>
			<NuxtPage />
		</NuxtLayout>
		<Toaster />
	</div>
</template>

<style lang="scss">
	.show
	{
		display: none;
		color: $main;
		font-size: 32px;

		@include mq($desktop)
		{
			display: block;
		}
	}
</style>
