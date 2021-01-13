<script lang="ts">
  import { onMount } from "svelte";
  import axios from "axios";
  export let date;

  onMount(async () => {
    const rest = await axios.get(
      "https://testthathinhdao.azurewebsites.net/api/caption?type=both"
    );
     date = rest.data.quote;
  });
</script>

<main>
  <h1>Capthathinhdao</h1>
  <br />
  <h2>The date according to Node.js is:</h2>
  <p>{date ? date : "Loading date..."}</p>
</main>
