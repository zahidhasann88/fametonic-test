
<!-- Header.svelte -->
<script lang="ts">
  import { onMount } from "svelte";
  import { showSignIn } from "../../../lib/stores/showSignIn";

  let isMenuOpen = false;
  let windowWidth = 0;
  let showSignInLink = false;

  // Subscribe to the showSignIn store
  showSignIn.subscribe(value => {
    showSignInLink = value;
  });

  const toggleMenu = () => {
    isMenuOpen = !isMenuOpen;
  };

  const handleResize = () => {
    windowWidth = window.innerWidth;
    if (windowWidth >= 768) {
      isMenuOpen = false;
    }
  };

  onMount(() => {
    windowWidth = window.innerWidth;
    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  });
</script>

<header class="w-full relative z-30">
  <!-- Top promo bar -->
  <div
    class="text-white py-2.5 px-4 sm:px-6 lg:px-8 xl:px-[250px] h-auto flex items-center justify-center [background:linear-gradient(to_right,_#FC004E,_#10CBE0)]"
  >
    <p class="text-center py-2 sm:py-0">
      <span class="inline-flex items-center vertical-align-middle">
        <span class="mr-1 sm:mr-2">🚀</span>
        <span
          class="font-[800] text-[14px] xs:text-[16px] sm:text-[22px] leading-[100%] bg-[#00E7F9] bg-clip-text text-transparent"
        >
          FRESH BEGINNINGS SALE:
        </span>
      </span>
      <span
        class="font-[600] text-[14px] xs:text-[16px] sm:text-[22px] leading-[100%]"
      >
        Extra 25% OFF, Limited Spots - start your journey today!
      </span>
    </p>
  </div>

  <!-- Main header -->
  <div
    class="bg-black text-white p-4 sm:px-6 lg:px-8 xl:px-[250px] flex justify-between items-center"
  >
    <!-- empty spacer for alignment -->
    <div class="md:hidden w-8"></div>

    <!-- Logo -->
    <div class="flex justify-center md:justify-start md:flex-grow">
      <a href="/" class="no-underline">
        <img
          src="/logo.png"
          alt="Fame Tonic Logo"
          class="relative z-20 w-[120px] md:w-[150px] h-auto"
        />
      </a>
    </div>

    <!-- Mobile menu button -->
    <button
      class="md:hidden text-white"
      on:click={toggleMenu}
      title="Menu"
      aria-label="Menu"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width={2}
          d="M4 6h16M4 12h16M4 18h16"
        />
      </svg>
    </button>

    <!-- Desktop nav -->
    <nav
      class="hidden md:flex space-x-8 font-semibold text-[18px] text-center align-middle"
    >
      <a
        href="/about-us"
        class="text-[#A9A9A9] hover:text-pink-300 transition-colors"
      >
        About us
      </a>
      <a
        href="/contact"
        class="text-[#A9A9A9] hover:text-pink-300 transition-colors"
      >
        Contact
      </a>
      {#if showSignInLink}
        <a
          href="/sign-in"
          class="text-[#A9A9A9] hover:text-pink-300 transition-colors"
        >
          Sign In
        </a>
      {/if}
    </nav>
  </div>

  <!-- Mobile menu -->
  {#if isMenuOpen}
    <div
      class="md:hidden bg-black text-gray-400 py-4 px-6 absolute w-full z-40"
    >
      <nav class="flex flex-col space-y-4">
        <a
          href="/about-us"
          class="text-gray-400 hover:text-pink-300 transition-colors"
          on:click={() => (isMenuOpen = false)}
        >
          About us
        </a>
        <a
          href="/contact"
          class="text-gray-400 hover:text-pink-300 transition-colors"
          on:click={() => (isMenuOpen = false)}
        >
          Contact
        </a>
        {#if showSignInLink}
          <a
            href="/sign-in"
            class="text-gray-400 hover:text-pink-300 transition-colors"
            on:click={() => (isMenuOpen = false)}
          >
            Sign In
          </a>
        {/if}
      </nav>
    </div>
  {/if}
</header>