<script context="module" lang="ts">
  import { writable, type Writable } from "svelte/store";

  export interface TabCtxType {
    selected: Writable<HTMLElement>;
  }
</script>

<script lang="ts">
  import { setContext } from "svelte";

  const ctx: TabCtxType = {
    selected: writable<HTMLElement>()
  };

  setContext("ctx", ctx);

  function init(node: HTMLElement) {
    const destroy = ctx.selected.subscribe((x: HTMLElement) => {
      if (x) node.replaceChildren(x);
    });

    return { destroy };
  }
</script>
<div class="dark:bg-main-300 bg-contrast-100 rounded-2xl border-t-8 border-highlight 
dark:border-highlight-dark overflow-clip outline outline-2 outline-neutral-500/10 shadow-lg">
	<ul class="flex !list-none w-full !m-0 md:px-2">
	  	<slot />
	</ul>
	<div class="md:p-4 p-2 !mt-0 duration-300 tab-body text-[15px] md:text-lg" role="tabpanel" aria-labelledby="id-tab" use:init />
</div>