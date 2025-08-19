<script lang="ts">
  import { onMount } from "svelte";
  import { buttonClickCount } from "../../lib/stores/buttonClickCount";
  import { showSignIn } from "../../lib/stores/showSignIn";

  let isMobile = false;
  let clickCount = 0;
  let buttonText = "GET STARTED";

  // Subscribe to the click count store
  buttonClickCount.subscribe((value) => {
    clickCount = value;
    if (clickCount > 0) {
      buttonText =
        clickCount === 1 ? "CLICKED 1 TIME" : `CLICKED ${clickCount} TIMES`;
    }
  });

  const updateIsMobile = () => {
    isMobile = window.innerWidth < 768;
  };

  const handleGetStartedClick = (event: Event) => {
    event.preventDefault();

    // Increment click count
    clickCount += 1;
    buttonClickCount.set(clickCount);

    // On first click, show the Sign In link
    if (clickCount === 1) {
      showSignIn.set(true);
    }
  };

  onMount(() => {
    updateIsMobile();
    window.addEventListener("resize", updateIsMobile);
    return () => window.removeEventListener("resize", updateIsMobile);
  });
</script>

<div
  class="bg-black text-white p-6 sm:px-6 md:px-8 lg:px-12 xl:px-[250px] relative overflow-hidden pb-12 sm:pb-16 md:pb-24 lg:pb-32"
>
  <div class="flex flex-col items-start justify-between md:flex-row">
    <!-- Hero Content -->
    <div
      class="relative z-20 w-full px-2 mb-8 text-center md:w-1/2 md:mb-0 md:text-left sm:px-0"
    >
      <h1
        class="text-[25px] sm:text-[25px] md:text-[28px] lg:text-[35px] font-[600] mb-[8px] text-white leading-[110%] md:leading-[100%]"
      >
        Want to Turn Social Media Into a Profitable Career?
      </h1>
      <h2
        class="text-[25px] sm:text-[25px] md:text-[28px] lg:text-[35px] font-[600] mb-[20px] md:mb-[27px] leading-[110%] md:leading-[100%] text-[#00E7F9] [text-shadow:2px_2px_6px_rgba(255,20,147,1)]"
      >
        Discover your way to success with Fametonic:
      </h2>
      <ul class="mb-6 space-y-3 text-left md:space-y-4 md:mb-8">
        <li class="flex items-start">
          <span class="flex-shrink-0 mr-2 text-yellow-400">✨</span>
          <span class="font-[600] text-[16px] leading-[22px] align-middle">
            Start growing your influence right away—no waiting required!
          </span>
        </li>
        <li class="flex items-start">
          <span class="flex-shrink-0 mr-2 text-yellow-400">✨</span>
          <span class="font-[600] text-[16px] leading-[22px] align-middle">
            Create viral TikToks and Reels step by step with easy-to-follow
            lessons
          </span>
        </li>
        <li class="flex items-start">
          <span class="flex-shrink-0 mr-2 text-yellow-400">✨</span>
          <span class="font-[600] text-[16px] leading-[22px] align-middle">
            Use a Personal AI Worker to boost your content
          </span>
        </li>
        <li class="flex items-start">
          <span class="flex-shrink-0 mr-2 text-yellow-400">✨</span>
          <span class="font-[600] text-[16px] leading-[22px] align-middle">
            Learn from expert-led courses designed for aspiring influencers
          </span>
        </li>
      </ul>

      <div class="block w-full">
        <!-- Mobile View Button -->
        <div class="block mb-4 text-center md:hidden">
          <p
            class="text-[12px] leading-[16px] font-[500] text-[#ABABAB] ml-[26px]"
          >
            By clicking "Get Started", you agree with Terms and Conditions,
            Privacy Policy, Subscription Terms
          </p>
          <div
            class="text-[10px] leading-[100%] font-[500] align-middle text-[#ABABAB] mt-[40px] mb-[40px] text-center"
          >
            Fametonic 2025 ©All Rights Reserved.
          </div>
        </div>

        <div class="block w-full md:hidden">
          <button
            class="w-full bg-[#FC004E] hover:bg-[#e0003d] text-white font-bold py-2 px-16 lg:px-28 rounded-xl text-base lg:text-lg uppercase flex items-center justify-center shadow-[3px_3px_10px_0px_#00f2ff] transition duration-300"
            on:click={handleGetStartedClick}
          >
            {buttonText}
            <img
              src="/arrow.svg"
              alt="Arrow"
              class="w-3 h-3 ml-1 sm:w-4 sm:h-4"
            />
          </button>
          <p
            class="text-[12px] leading-[16px] text-center font-[400] align-middle text-gray-300 mt-3"
          >
            1-minute quiz for personalized insights
          </p>
        </div>

        <!-- Desktop View Button -->
        <div class="hidden md:block md:text-left">
          <div class="inline-block">
            <button
              class="bg-[#FC004E] hover:bg-[#e0003d] text-white font-bold py-1.5 md:py-2 px-15 md:px-19 lg:px-23 rounded-xl text-base lg:text-lg uppercase flex items-center justify-center shadow-[3px_3px_10px_0px_#00f2ff] transition duration-300"
              on:click={handleGetStartedClick}
            >
              {buttonText}
              <img
                src="/arrow.svg"
                alt="Arrow"
                class="w-3 h-3 ml-1 sm:w-4 sm:h-4"
              />
            </button>
            <p
              class="text-[12px] leading-[16px] text-center font-[400] align-middle text-gray-300 mt-3"
            >
              1-minute quiz for personalized insights
            </p>
          </div>
        </div>

        <div class="hidden md:block">
          <p
            class="text-[12px] leading-[16px] font-[500] align-middle text-[#ABABAB] mt-6 md:mt-8"
          >
            By clicking "Get Started", you agree with Terms and Conditions,
            Privacy Policy, Subscription Terms
          </p>

          <div
            class="text-[10px] leading-[100%] font-[500] align-middle text-[#ABABAB] mt-4"
          >
            Fametonic 2025 ©All Rights Reserved.
          </div>
        </div>
      </div>
    </div>

    <!-- Hero Image -->
    <div
      class="relative flex items-start justify-center order-first w-full md:w-1/2 md:justify-start md:order-last"
    >
      <div
        class={`relative ${isMobile ? "" : "md:absolute md:-left-14 md:top-0"}`}
      >
        <img
          src="/Influe_mobile_mockup.png"
          alt="Fametonic mobile app"
          class="relative w-[290px] sm:w-[410px] md:w-[600px] lg:w-[700px] ml-[1px] scale-105 md:scale-115 md:translate-x-6 lg:translate-x-10"
        />
        <div
          class="absolute top-0 left-1/2 transform -translate-x-1/2 w-[128%] h-[80%] rounded-full bg-gradient-to-r from-[#FC004E] to-[#10CBE0] opacity-50 blur-2xl -z-10"
        ></div>
      </div>
    </div>
  </div>
</div>