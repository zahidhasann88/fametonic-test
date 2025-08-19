<script lang="ts">
  export let href: string | undefined = undefined;
  export let onClick: (() => void) | undefined = undefined;
  export let className: string = "";
  export let fullWidth: boolean = false;

  // combine base classes
  $: baseClasses = `
    ${fullWidth ? "w-full" : "w-full md:w-auto"} 
    bg-[#FC004E] hover:bg-[#e0003d] 
    text-white font-bold 
    py-1 sm:py-1.5 md:py-2 
    px-6 sm:px-12 md:px-20 lg:px-28 
    rounded-xl 
    text-sm sm:text-base md:text-lg 
    uppercase 
    flex items-center justify-center 
    shadow-[3px_3px_10px_0px_#00f2ff] 
    transition duration-300 
    ${className}
  `.trim();
</script>

{#if href}
  <a {href} class={fullWidth ? "w-full" : "w-full md:w-auto"}>
    <button class={baseClasses} on:click={onClick}>
      <slot />
    </button>
  </a>
{:else}
  <button class={baseClasses} on:click={onClick}>
    <slot />
  </button>
{/if}
