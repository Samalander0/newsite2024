<script>
  import { marked } from 'marked'
  import Metatags from '$lib/components/Metatags.svelte';
  import "$lib/styles/styles.scss";
  import "$lib/styles/case-study.scss";

  const text = `
# Case Study - Classmate
<span class="subtitle">07/07/2025</span>

Lorem ipsum dolor sit amet, **consectetur** adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in **reprehenderit in voluptate velit** esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non *proident*, sunt in culpa qui officia deserunt mollit anim id est laborum.

![image](//unsplash.it/900/600)

Lorem ipsum dolor sit amet consectetur adipiscing elit. Quisque faucibus ex sapien vitae pellentesque sem placerat. In id cursus mi pretium tellus duis convallis. Tempus leo eu aenean sed diam urna tempor. Pulvinar vivamus fringilla lacus nec metus bibendum egestas. Iaculis massa nisl malesuada lacinia integer nunc posuere. Ut hendrerit semper vel class aptent taciti sociosqu. Ad litora torquent per conubia nostra inceptos himenaeos.

## Sub-heading

Lorem ipsum dolor sit amet consectetur adipiscing elit. Quisque faucibus ex sapien vitae pellentesque sem placerat. In id cursus mi pretium tellus duis convallis. Tempus leo eu aenean sed diam urna tempor. Pulvinar vivamus fringilla lacus nec metus bibendum egestas. Iaculis massa nisl malesuada lacinia integer nunc posuere. Ut hendrerit semper vel class aptent taciti sociosqu. Ad litora torquent per conubia nostra inceptos himenaeos.
  `
</script>

<Metatags title="Classmate"/>

<main class="page-main">
  <div class="page-content">
    {@html marked(text)}
  </div>
</main>