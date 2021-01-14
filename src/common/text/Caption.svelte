<script lang="ts">
  import { fly } from "svelte/transition";
  import { LottiePlayer } from "@lottiefiles/svelte-lottie-player";

  export let text: string;
  export let type: "female" | "male" | "both";
</script>

<div>
  <p
    class="font-semibold text-3xl lg:text-3xl sm:text-2xl"
    class:female={type === "female"}
    class:male={type === "male"}
    class:both={type === "both"}
    in:fly={{ x: -200, duration: 3000 }}
  >{text}</p>
  <div class=" flex justify-center ">
    <LottiePlayer
      control={true}
      height={400}
      width={400}
      autoplay={true}
      renderer="svg"
      src="https://assets4.lottiefiles.com/datafiles/d9bc9kYC2VttaKb/data.json"
    />
  </div>
</div>

<style>
  .female {
    @apply text-pink-500;
  }
  .male {
    @apply text-indigo-500;
  }
  .both {
    @apply text-teal-500;
  }
</style>
