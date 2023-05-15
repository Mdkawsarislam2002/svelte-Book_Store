<script>
  import { onMount } from "svelte";
  import axiosInstance from "../utils/AxiosInstance";
  import SingleBooks from "./SingleBooks.svelte";
  let bookData = [];

  function getUserAccount() {
    return axiosInstance.get("/books");
  }

  onMount(async () => {
    const response = await getUserAccount();
    bookData = response.data;
  });
</script>

<main class="py-12 px-6 2xl:px-6 container">
  <div class="order-2 xl:-order-1">
    <div class="flex items-center justify-between mb-12">
      <h4 class="mt-2 text-xl font-bold">Book List</h4>

      <div class="flex items-center space-x-4">
        <button class="lws-filter-btn active-filter">All</button>
        <button class="lws-filter-btn">Featured</button>
      </div>
    </div>
    <div
      class="space-y-6 md:space-y-0 md:grid grid-cols-1 lg:grid-cols-3 gap-6"
    >
      {#each bookData as data}
        <SingleBooks {data} />
      {/each}
    </div>
  </div>
</main>
