<script lang="ts">
	import { attach, draggable } from 'animejs';
	import { onMount } from 'svelte';

	let box_style = 'h-[600px] w-[300px] border-2 border-solid border-black p-5 relative';
	let draggableBoxRef: HTMLDivElement;
	let column1Ref: HTMLDivElement;
	let column2Ref: HTMLDivElement;
	let column3Ref: HTMLDivElement;

	onMount(() => {
		// Create draggable instance for the box
		const dragInstance = draggable({
			targets: draggableBoxRef,
			dragOver: true,
			drop: (droppable) => {
				droppable?.appendChild(draggableBoxRef);
			}
		});

		// Make columns droppable
		const attachColumns = () => {
			attach(draggableBoxRef, [column1Ref, column2Ref, column3Ref]);
		};

		attachColumns();

		return () => {
			dragInstance.destroy();
		};
	});
</script>

<div class="mega-container flex h-screen w-screen items-center justify-center gap-5">
	<div class={box_style} ref={column1Ref}>
		<div
			ref={draggableBoxRef}
			class="h-[100px] w-full border-2 border-solid border-black bg-blue-200 cursor-move"
		></div>
	</div>
	<div class={box_style} ref={column2Ref}></div>
	<div class={box_style} ref={column3Ref}></div>
</div>
