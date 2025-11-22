<script>
  import Layout from "./Layout.svelte";
  import { onMount } from "svelte";

  let blog = $state({
    title: "",
    content: "",
    footer: "",
  });

  onMount(async () => {
    const response = await fetch("/blog.json");
    blog = await response.json();
  });
</script>

<Layout title={blog.title} footer={blog.footer}>
  {#snippet content()}
    {@html blog.content}
  {/snippet}
</Layout>
