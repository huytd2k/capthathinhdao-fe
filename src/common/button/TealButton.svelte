<script lang="ts">
  export let text: string;
  export let hidden: boolean;
  export let disabled: boolean;
</script>

<button
  {disabled}
  on:click
  class:hidden
  class="bg-teal-400 w-20 px-4 py-2 text-white font-medium rounded-lg focus:outline-none focus:ring-2 hover:bg-teal-500 transition duration-300 ease-in-out">
  {text}
</button>

<style>
  .hidden {
    visibility: hidden;
  }
</style>
