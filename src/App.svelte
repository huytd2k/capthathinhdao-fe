<script lang="ts">
  import { onMount } from "svelte";
  import axios from "axios";
  export type quoteType = "male" | "female" | "both";
  import { Button } from "svelte-materialify";
  export let date;
  export let type: quoteType;
  onMount(async () => {
    const rest = await axios.get(
      "https://testthathinhdao.azurewebsites.net/api/caption?type=both"
    );
    date = rest.data.quote;
  });

  const select = (_type: quoteType) => async () => {
    date = undefined;
    date = (
      await axios.get(
        `https://testthathinhdao.azurewebsites.net/api/caption?type=${_type}`
      )
    ).data.quote;
  };
  $: console.log(type);
</script>

<main>
  <h1>Capthathinhdao</h1>
  <br />
  <Button on:click={select("male")} class="teal white-text" depressed
    >Nam</Button
  >
  <Button on:click={select("female")} class="teal white-text" depressed
    >Nữ</Button
  >
  <Button on:click={select("both")} class="teal white-text" depressed
    >Chung</Button
  >
  <p>{date ? date : "Dang tai caption cho cung ne..."}</p>
</main>
