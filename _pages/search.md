---
layout: page
---

<style>
	#search-container {
	    max-width: 100%;
	}

	input[type=text] {
	  font-size: normal;
	  outline: none;
	  padding: 1rem;
          background: #ddd;
	  width: 80%;
		-webkit-appearance: none;
		font-family: inherit;
		font-size: 100%;
		border: none;
	}
	#results-container {
		margin: .5rem 0;
	}
</style>

<!-- Html Elements for Search -->
<div id="search-container">
<input type="text" id="search-input" placeholder="Gõ từ cần tìm ...">
<ol id="results-container"></ol>
</div>

<!-- Script pointing to search-script.js -->
<script src="/search.js" type="text/javascript"></script>

<!-- Configuration -->
<script type="text/javascript">
SimpleJekyllSearch({
  searchInput: document.getElementById('search-input'),
  resultsContainer: document.getElementById('results-container'),
  json: '/search.json',
  searchResultTemplate: '<li><a href="{url}">{title}</a></li>',
  noResultsText: 'Không tìm thấy bài viết!',
  limit: 10,
  fuzzy: false,
  exclude: ['Welcome']
})
</script>
