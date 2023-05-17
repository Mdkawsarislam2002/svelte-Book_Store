<script>
  import { onMount } from "svelte";
  import axiosInstance from "../utils/AxiosInstance";
  import SingleBooks from "./SingleBooks.svelte";
  import { filterValues, searchValue } from "../store";
  let bookData = [];
  let _searchValue;
  let _filterValues;

  function getUserAccount({ filter, searchQuery }) {
    let res;
    let checkFeature = filter === "featured";
    if (checkFeature) {
      res = `books?featured=${checkFeature}&name_like=${searchQuery}`;
    } else {
      res = `books?name_like=${searchQuery}`;
    }
    return axiosInstance.get(res);
  }

  onMount(async () => {
    const response = await getUserAccount({
      filter: _filterValues,
      searchQuery: _searchValue,
    });
    bookData = response.data;
  });

  searchValue.subscribe((value) => {
    _searchValue = value;
  });
  filterValues.subscribe((value) => {
    _filterValues = value;
  });
</script>

<main class="py-12 px-6 2xl:px-6 container">
  <div class="order-2 xl:-order-1">
    <div class="flex items-center justify-between mb-12">
      <h4 class="mt-2 text-xl font-bold">Book List</h4>

      <div class="flex items-center space-x-4">
        <button
          on:click={(e) => filterValues.set("all")}
          class="lws-filter-btn active-filter">All</button
        >
        <button
          on:click={(e) => filterValues.set("featured")}
          class="lws-filter-btn">Featured</button
        >
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
