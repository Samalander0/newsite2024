<script>
  export let title = 'Sam Cheng';
  export let description = "Hey, I'm Sam. I tell stories on the web, and I'd love to tell yours.";
  export let image = 'https://www.samalander.dev/card.png';
</script>

<svelte:head>
	<title>{title}</title>
  <meta name="description" content={description}/>
    
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:site" content="www.samalander.dev" />
  <meta name="twitter:title" content={title} />
  <meta name="twitter:description" content={description} />
  <meta name="twitter:image" content={image} />

  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
  <meta property="og:image" content={image} />

  <link rel="icon" href="https://www.samalander.dev/favicon.ico" type="image/x-icon"/>
</svelte:head>