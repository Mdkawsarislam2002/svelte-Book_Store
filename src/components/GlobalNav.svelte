<script>
  import logo from "../assets/logo.svg";
  import { searchValue } from "./../store.js";
</script>

<nav class="py-4 2xl:px-6">
  <div class="container flex items-center justify-between">
    <a href="/">
      <img src={logo} alt="logo" width="150px" class="object-contain" />
    </a>

    <ul class="hidden md:flex items-center space-x-6">
      <a class="font-semibold cursor-pointer" href="/" id="lws-bookStore">
        <li>Book Store</li>
      </a>
      <a class="cursor-pointer" href="/add" id="lws-addBook">
        <li>Add Book</li>
      </a>
    </ul>

    <form class="flex items-center">
      <div class="group relative rounded-md bg-white">
        <svg
          width="20"
          height="20"
          fill="currentColor"
          class="absolute left-3 top-1/2 -mt-2.5 text-slate-400 pointer-events-none group-focus-within:text-primary"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
          />
        </svg>
        <input
          type="text"
          placeholder="Filter books..."
          class="search"
          id="lws-search"
          on:input={(e) => searchValue.set(e.target.value)}
        />
      </div>
    </form>
  </div>
</nav>
