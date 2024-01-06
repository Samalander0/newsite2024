<script>
  let slide = 1;

  function previous() {
    slide--;
    if (slide < 1) {
      slide = 3;
    }
  }
  function next() {
    slide++;
    if (slide > 3) {
      slide = 1;
    }
  }
</script>

<div class="carousel">
  <div class="carousel-content" data-slide={slide}>
    <slot />
  </div>
  <div class="carousel-indicators">
    <button class={slide == 1 ? "active" : null} on:click={() => {slide = 1}} aria-label="first carousel slide"></button>
    <button class={slide == 2 ? "active" : null} on:click={() => {slide = 2}} aria-label="second carousel slide"></button>
    <button class={slide == 3 ? "active" : null} on:click={() => {slide = 3}} aria-label="third carousel slide"></button>
  </div>
  <button aria-label="previous carousel slide" class="carousel-control carousel-previous" on:click={previous}>
    <img src="/assets/arrow-left.svg" alt="left arrow"/>
  </button>
  <button aria-label="next carousel slide" class="carousel-control carousel-next" on:click={next}>
    <img src="/assets/arrow-right.svg" alt="right arrow"/>
  </button>
</div>