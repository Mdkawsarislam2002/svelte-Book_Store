<script>
  import { page } from "$app/stores";
  import { onMount } from "svelte";
  import axiosInstance from "../utils/AxiosInstance";

  //    logics
  let bookId = $page.params.edit;

  let name = "";
  let author = "";
  let thumbnail = "";
  let price = "";
  let rating = "";
  let featured = false;

  const getSingleBookData = async () => {
    let res = await axiosInstance.get(`/books/${bookId}`);
    return await res.data;
  };
  const postNewBook = async () => {
    try {
      let res = await axiosInstance.patch(`/books/${bookId}`, {
        name,
        author,
        thumbnail,
        price,
        rating,
        featured,
      });

      return await res.data;
    } catch (error) {
      console.warn(error);
    }
  };

  onMount(async () => {
    let data = await getSingleBookData();
    name = data.name; 
    author = data.author;
    thumbnail = data.thumbnail;
    price = data.price;
    rating = data.rating;
    featured = data.featured;
  });

  const formHandler = (e) => {
    e.preventDefault();
    postNewBook();
  };
</script>

<form class="book-form" on:submit={formHandler}>
  <div class="space-y-2">
    <label for="lws-bookName">Book Name</label>
    <input
      required
      class="text-input"
      type="text"
      id="lws-bookName"
      name="name"
      bind:value={name}
    />
  </div>

  <div class="space-y-2">
    <label for="lws-author">Author</label>
    <input
      required
      class="text-input"
      type="text"
      id="lws-author"
      name="author"
      bind:value={author}
    />
  </div>

  <div class="space-y-2">
    <label for="lws-thumbnail">Image Url</label>
    <input
      required
      class="text-input"
      type="text"
      id="lws-thumbnail"
      name="thumbnail"
      bind:value={thumbnail}
    />
  </div>

  <div class="grid grid-cols-2 gap-8 pb-4">
    <div class="space-y-2">
      <label for="lws-price">Price</label>
      <input
        required
        class="text-input"
        type="number"
        id="lws-price"
        name="price"
        bind:value={price}
      />
    </div>

    <div class="space-y-2">
      <label for="lws-rating">Rating</label>
      <input
        required
        class="text-input"
        type="number"
        id="lws-rating"
        name="rating"
        min="1"
        max="5"
        bind:value={rating}
      />
    </div>
  </div>

  <div class="flex items-center">
    <input
      id="lws-featured"
      type="checkbox"
      name="featured"
      class="w-4 h-4"
      bind:checked={featured}
    />
    <label for="lws-featured" class="ml-2 text-sm">
      This is a featured book
    </label>
  </div>

  <button type="submit" class="submit" id="lws-submit">Edit Book</button>
</form>
