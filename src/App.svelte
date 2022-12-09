<script lang="ts">
  import { Client } from "tcore.js";

  const tcore = new Client();

  let name = "";

  async function getName() {
    await tcore.InitRest();

    const res = await tcore.sendRequest({
      hook: "name",
      function: "read_name",
      action: "null",
      params: [],
    });

    const data = await res.json();

    name = data.data.msg;
  }

  getName();
</script>

<main>
  <h1>
    Hello <span class="gradient">{name}</span>
  </h1>
</main>

<style>
  span.gradient {
    background: -webkit-linear-gradient(rgb(183, 61, 61), rgb(12, 76, 153));
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
</style>
