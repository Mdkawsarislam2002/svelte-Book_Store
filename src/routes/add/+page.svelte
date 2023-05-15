<script>
  import axiosInstance from "../../utils/AxiosInstance";

  let title = "";
  let author = "";
  let imgUrl = "";
  let price = "";
  let rating = "";
  let IsFeatured = "";

  const addBookHandler = async () => {
    try {
      let res = await axiosInstance.post(`/books`, {
        name: title,
        author: author,
        thumbnail: imgUrl,
        price: price,
        rating: rating,
        featured: IsFeatured,
      });
      return await res.data;
    } catch (error) {
      console.warn(error.message);
    }
  };

  const formHandler = (e) => {
    e.preventDefault();
    addBookHandler();
  };
</script>

<main class="py-6 2xl:px-6">
  <div class="container">
    <div
      class="p-8 overflow-hidden bg-white shadow-cardShadow rounded-md max-w-xl mx-auto"
    >
      <h4 class="mb-8 text-xl font-bold text-center">Add New Book</h4>
      <form class="book-form" on:submit={formHandler}>
        <div class="space-y-2">
          <label for="lws-bookName">Book Name</label>
          <p />
          <input
            required
            class="text-input"
            type="text"
            id="lws-bookName"
            name="name"
            bind:value={title}
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
            bind:value={imgUrl}
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
            bind:checked={IsFeatured}
          />
          <label for="lws-featured" class="ml-2 text-sm">
            This is a featured book
          </label>
        </div>

        <button type="submit" class="submit" id="lws-submit">Add Book</button>
      </form>
    </div>
  </div>
</main>
