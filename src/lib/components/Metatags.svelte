<script>
  export let title = 'Sam Cheng';
  export let description = "Hey, I'm Sam, a digital designer and web developer";
  export let image = 'https://www.samcheng.co/card.png';
</script>

<svelte:head>
	<title>{title}</title>
  <meta name="description" content={description}/>
    
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:site" content="www.samcheng.co" />
  <meta name="twitter:title" content={title} />
  <meta name="twitter:description" content={description} />
  <meta name="twitter:image" content={image} />

  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
  <meta property="og:image" content={image} />

  <link rel="icon" href="https://www.samcheng.co/favicon.ico" type="image/x-icon"/>
</svelte:head>