<script lang="ts">
  import { Client } from "tcore.js";

  const tcore = new Client();

  async function getName(): Promise<string> {
    let name = "";
    try {
      await tcore.InitRest();
      const res = await tcore.sendRequest({
        hook: "name",
        function: "read_name",
        action: "null",
        params: [],
      });

      const data = await res.json();

      name = data.data.msg;
    } catch (e) {
      throw e;
    }

    return name;
  }
</script>

<main>
  {#await getName()}
    <p>TCore is loading...</p>
  {:then name}
    <h1>Hello <span class="gradient">{name}</span></h1>
  {:catch}
    <h2>Error connecting to TCore. Make sure TCore service is enabled</h2>
  {/await}
</main>

<style>
  span.gradient {
    background: -webkit-linear-gradient(rgb(183, 61, 61), rgb(12, 76, 153));
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
</style>
