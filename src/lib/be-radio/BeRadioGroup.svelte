<script lang="ts">
	// 选中的列表
	import { createEventDispatcher, setContext } from 'svelte';
	import RadioStore from './radio'
	import { debounce } from '../utils/throttle';
	const dispatch = createEventDispatcher();
	export let checked: string = '';
	const store = new RadioStore({ checked })
	setContext('radioStore', store)

	// 设置选中数据
	export const setChecked = item => {
		if (store.current !== item) {
			store.setChecked(item)
			dispatch('change', item)
		}
	}
	export const clear = () => store.clear()

	const subscribeHandle = debounce(current => {
		if (checked !== current) {
			checked = current
			dispatch('change', current)
		}
		dispatch('clickRadio', current)
	}, 60)
	store.subscribe.push(subscribeHandle)

	let _class: $$props["class"] = "";
	export {_class as class};

	$: if (checked) setChecked(checked)
</script>
<div role="group" aria-label="checkbox-group" class='be-radio-group {_class}' style={$$props.style}>
	<slot></slot>
</div>
