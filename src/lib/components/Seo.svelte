<script>
  export let title = undefined;
  export let noindex = false;
  export let nofollow = false;
  export let description = undefined;
  export let keywords = undefined;
  export let canonical = undefined;
  export let openGraph = undefined;
  export let twitter = undefined;
  export let image = undefined;
</script>

<svelte:head>
  {#if title}
    <title>{title}</title>
  {/if}

  <meta
    name="robots"
    content={`${noindex ? "noindex" : "index"},${
      nofollow ? "nofollow" : "follow"
    }`}
  />
  <meta
    name="googlebot"
    content={`${noindex ? "noindex" : "index"},${
      nofollow ? "nofollow" : "follow"
    }`}
  />

  {#if description}
    <meta name="description" content={description} />
  {/if}

  {#if image}
    <meta property="og:image" content={image} />
    <meta property="og:image:alt" content={title} />
  {/if}

  {#if canonical}
    <link rel="canonical" href={canonical} />
  {/if}

  {#if keywords}
    <meta name="keywords" content={keywords} />
  {/if}

  {#if openGraph}
    {#if openGraph.title}
      <meta property="og:title" content={openGraph.title} />
    {/if}

    {#if openGraph.description}
      <meta property="og:description" content={openGraph.description} />
    {/if}

    {#if openGraph.url || canonical}
      <meta property="og:url" content={openGraph.url || canonical} />
    {/if}

    {#if openGraph.type}
      <meta property="og:type" content={openGraph.type.toLowerCase()} />
    {/if}

    {#if openGraph.article}
      {#if openGraph.article.publishedTime}
        <meta
          property="article:published_time"
          content={openGraph.article.publishedTime}
        />
      {/if}

      {#if openGraph.article.modifiedTime}
        <meta
          property="article:modified_time"
          content={openGraph.article.modifiedTime}
        />
      {/if}

      {#if openGraph.article.expirationTime}
        <meta
          property="article:expiration_time"
          content={openGraph.article.expirationTime}
        />
      {/if}

      {#if openGraph.article.section}
        <meta property="article:section" content={openGraph.article.section} />
      {/if}

      {#if openGraph.article.authors && openGraph.article.authors.length}
        {#each openGraph.article.authors as author}
          <meta property="article:author" content={author} />
        {/each}
      {/if}

      {#if openGraph.article.tags && openGraph.article.tags.length}
        {#each openGraph.article.tags as tag}
          <meta property="article:tag" content={tag} />
        {/each}
      {/if}
    {/if}
  {/if}

  {#if twitter}
    <meta name="twitter:card" content={twitter.card || "summary_large_image"} />
    {#if twitter.site}
      <meta name="twitter:site" content={twitter.site} />
    {/if}
    {#if twitter.title}
      <meta name="twitter:title" content={twitter.title} />
    {/if}
    {#if twitter.description}
      <meta name="twitter:description" content={twitter.description} />
    {/if}
    {#if twitter.image}
      <meta name="twitter:image" content={twitter.image} />
    {/if}
    {#if twitter.imageAlt}
      <meta name="twitter:image:alt" content={twitter.imageAlt} />
    {/if}
    {#if twitter.player}
      <meta name="twitter:player" content={twitter.player} />
    {/if}
    {#if twitter.playerWidth}
      <meta name="twitter:player:width" content={twitter.playerWidth} />
    {/if}
    {#if twitter.playerHeight}
      <meta name="twitter:player:height" content={twitter.playerHeight} />
    {/if}
  {/if}

  <slot />
</svelte:head>
