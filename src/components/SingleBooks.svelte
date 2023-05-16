<script>
  import EditeOrDelete from "./EditeOrDelete.svelte";

  export let data;
  const { name, author, thumbnail, price, rating, featured, id } = data;
</script>

<div class="book-card">
  <img class="h-[240px] w-[170px] object-cover" src={thumbnail} alt="book" />
  <div class="flex-1 h-full pr-2 pt-2 flex flex-col">
    <div class="flex items-center justify-between">
      {#if featured}
        <span class="lws-badge">featured</span>
      {:else}
        <span />
      {/if}

      <div class="text-gray-500 space-x-2">
        <EditeOrDelete {id} />
      </div>
    </div>

    <div class="space-y-2 mt-4 h-full">
      <h4 class="lws-book-name">
        {name}
      </h4>
      <p class="lws-author">{author}</p>
      <div class="lws-stars">
        <p class="text-red-500">
          {rating}
        </p>
        <svg viewBox="0 0 20 20" fill="currentColor" class="star">
          <path
            fill-rule="evenodd"
            d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
            clip-rule="evenodd"
          />
        </svg>
      </div>
      <p class="lws-price">BDT {price}</p>
    </div>
  </div>
</div>
