<script lang="ts">
	import { getContext } from "svelte";

    export let path: string = ''            // 地址
    export let prefetch: boolean = false    // 开启预加载 false/true
    let separator = getContext('BeBreadcrumbSeparator')
</script>
<span class="be-breadcrumb__item">
	<span role="link" class="be-breadcrumb__inner is-link">
		{#if path}
			{#if prefetch}
			<a href={path} sveltekit:prefetch>
				<slot></slot>
			</a>
			{:else}
			<a href={path}>
				<slot></slot>
			</a>
			{/if}
		{:else}
			<slot></slot>
		{/if}
	</span>
	<span role="presentation" class="be-breadcrumb__separator">{separator}</span>
</span>
