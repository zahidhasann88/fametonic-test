<script lang="ts">
  import { onMount } from "svelte";
  import { showSignIn } from "../../../lib/stores/showSignIn";

  let isMenuOpen = false;
  let windowWidth = 0;
  let showSignInLink = false;

  showSignIn.subscribe((value) => {
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

<header class="relative z-30 w-full">
  <!-- Top promo bar -->
  <div
    class="text-white py-2.5 w-full h-auto flex items-center justify-center [background:linear-gradient(to_right,_#FC004E,_#10CBE0)]"
  >
    <div
      class="w-full max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 xl:px-[250px]"
    >
      <p class="py-2 text-center sm:py-0">
        <span class="inline-flex items-center vertical-align-middle">
          <span class="mr-1 sm:mr-2">🚀</span>
          <span
            class="font-[700] text-[14px] xs:text-[16px] sm:text-[22px] leading-[100%] bg-[#00E7F9] bg-clip-text text-transparent"
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
  </div>

  <!-- Main header -->
  <div class="flex items-center justify-between w-full text-white bg-black">
    <div
      class="w-full max-w-[1440px] mx-auto flex justify-between items-center p-4 sm:px-6 lg:px-8 xl:px-[220px]"
    >
      <!-- empty spacer for alignment -->
      <div class="w-8 md:hidden"></div>

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
        class="text-white md:hidden"
        on:click={toggleMenu}
        title="Menu"
        aria-label="Menu"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="w-6 h-6"
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
  </div>

  <!-- Mobile menu -->
  {#if isMenuOpen}
    <div
      class="absolute z-40 w-full px-6 py-4 text-gray-400 bg-black md:hidden"
    >
      <nav class="flex flex-col space-y-4">
        <a
          href="/about-us"
          class="text-gray-400 transition-colors hover:text-pink-300"
          on:click={() => (isMenuOpen = false)}
        >
          About us
        </a>
        <a
          href="/contact"
          class="text-gray-400 transition-colors hover:text-pink-300"
          on:click={() => (isMenuOpen = false)}
        >
          Contact
        </a>
        {#if showSignInLink}
          <a
            href="/sign-in"
            class="text-gray-400 transition-colors hover:text-pink-300"
            on:click={() => (isMenuOpen = false)}
          >
            Sign In
          </a>
        {/if}
      </nav>
    </div>
  {/if}
</header>
