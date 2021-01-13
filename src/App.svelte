<script lang="ts">
  import { onMount } from "svelte";
  import axios from "axios";
  import { Button } from "svelte-materialify";
  export type quoteType = "male" | "female" | "both";
  export let date;
  export let type: quoteType;
  let loading: boolean = true;

  onMount(async () => {
    const rest = await axios.get(
      "https://testthathinhdao.azurewebsites.net/api/caption?type=both"
    );
    date = rest.data.quote;
    loading = false;
  });

  const select = (_type: quoteType) => async () => {
    loading = true;
    date = (
      await axios.get(
        `https://testthathinhdao.azurewebsites.net/api/caption?type=${_type}`
      )
    ).data.quote;
    loading = false;
  };
</script>

<main>
  <h1>Capthathinhdao</h1>
  <br />
  {#if !loading}
    <Button
      on:click={select("male")}
      disabled={loading}
      class="teal white-text"
      depressed
    >Nam</Button
    >
    <Button
      on:click={select("female")}
      class={!loading && "teal white-text"}
      depressed
    >Nữ</Button
    >
    <Button
      on:click={select("both")}
      disabled={loading}
      class={!loading && "teal white-text"}
      depressed
    >Chung</Button
    >
  {/if}

  <p>{loading ? "Loading...." : date}</p>
</main>

