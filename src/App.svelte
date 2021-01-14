<script lang="ts">
  import { onMount } from "svelte";
  import axios from "axios";
  import TealButton from "./common/button/TealButton.svelte";
  import { Router, Link, Route } from "svelte-routing";
  import AddQuote from "./add-quote/AddQuote.svelte";
  import Tailwindcss from "./Tailwind.svelte";
  import { Moon } from "svelte-loading-spinners";
  import Caption from "./common/text/Caption.svelte";
  import { LottiePlayer } from "@lottiefiles/svelte-lottie-player";
  import { Azurefunctions, Svelte, Mongodb } from "@icons-pack/svelte-simple-icons";

  export let url = "";

  type quoteType = "male" | "female" | "both";
  let type: quoteType = "both";
  export let date;
  let loading: boolean = true;

  onMount(async () => {
    const rest = await axios.get(
      "https://testthathinhdao.azurewebsites.net/api/caption?type=both"
    );
    date = rest.data.quote;
    loading = false;
  });

  const select = (_type: quoteType) => async () => {
    type = _type;
    loading = true;
    date = (
      await axios.get(
        `https://testthathinhdao.azurewebsites.net/api/caption?type=${_type}`
      )
    ).data.quote;
    loading = false;
  };
</script>

<main class="flex flex-col min-h-screen">
  <body class="">
    <Router {url}>
      <Route path="/add">
        <AddQuote />
      </Route>
      <Route path="/">
        <h1 class="text-2xl text-teal-500 font-semibold mt-12">Capthathinhdao</h1>
        <br />
        <TealButton disabled={loading} on:click={select("male")} text="Nam" />
        <TealButton disabled={loading} on:click={select("female")} text="Nữ" />
        <TealButton disabled={loading} on:click={select("both")} text="Chung" />
        <div class="mt-8">
          {#if loading}
            <div class="flex justify-center">
              <Moon color="#16BDCA" class="mx-auto" />
            </div>
          {:else}
            <Caption text={date} {type} />
          {/if}
        </div>
      </Route>
    </Router>
  </body>
  <footer class="mt-auto p-3 text-teal-400 text-xs sm:text-sm">Built with <Mongodb /> MongoDB  - <Azurefunctions class="inline"/> Azure Function -   <Svelte class="inline"/> Svelte</footer>
</main>
