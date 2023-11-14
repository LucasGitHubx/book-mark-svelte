<script>
	// A book is conformed by: a title, an author, a class, and two buttons, one for delete 
	// and the other one for put the book as read.
	let books = [];
	let author = "";
	let title = "";
	let id = 0;

	const handleButtonForm = (e) => {
		e.preventDefault();

		if(author.trim() == "" || title.trim() == "" ){
			alert("You cannot insert empty inputs!");
		} else {
			books = [...books,{title, author, classBook:"non-read", id}];
			author = "";
			title = "";
			id++;	
		}
	}

	const handleButtonDelete = (id) => {
		books = books.filter((book) => book.id != id);
	}

	const handleButtonRead = (e, book) => {
		const libro = e.target.parentElement.parentElement.parentElement;
		
		if(libro.classList.contains("non-read")){
			// Removing and adding class for styling
			libro.classList.remove("non-read")
			libro.classList.add("read");
			
			// Changing class in the array
			book.classBook = "read";

			libro.querySelector(".book-text").style.textDecoration = "line-through";
		} else {
			// Removing and adding class for styling
			libro.classList.remove("read")
			libro.classList.add("non-read");
			
			// Changing class in the array
			book.classBook = "non-read";
		
			libro.querySelector(".book-text").style.textDecoration = "none";
		}
	}
</script>

<main>
	<h1>BookMark</h1>
	<form>
		<div>
			<input type="text" placeholder="Introduce a book..." id="input-bookname" bind:value={title}>
			<input type="text" placeholder="Introduce book's author..." id="input bookauthor" bind:value={author}>
		</div>
		<button on:click={handleButtonForm}>Insert</button>
	</form>
	{#each books as book}
		<div class="book non-read">
			<div class="book-text">
				<h4>{book.title}</h4>
				<p>{book.author}</p>
			</div>
			<div class="book-buttons">
				<button id="read" on:click={() => handleButtonRead(event, book)}><i class="bi bi-bookmark" style="color:green;"></i></button>
				<button id="delete" on:click={() => handleButtonDelete(book.id)}><i class="bi bi-trash" style="color: red;"></i></button>
			</div>
		</div>
	{/each}
</main>

<style>
	@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css");

	main {
		width: 90%;
		max-width: 400px;
		min-width: 300px;
		text-align: center;
		/* padding: 1em; */
		margin: 0 auto;
	}
	form{
		display: flex;
		align-items: center;
		flex-direction: column;
		gap: 1.5rem;
	}
	form div{
		max-width: 325px;
	}
	form div input{
		margin-top: 10px;
	}
	form input{
		border: 1px solid black;
	}
	form button{
		width: 75px;
		background-color: rgb(177, 91, 177);
		color: white;
		font-weight: bold;
		padding: 10px;
	}
	form button:hover{
		background-color:rgb(218, 139, 218) ;
	}
	form button:active{
		background-color: rgb(129, 59, 129);
	}

	/* Styling books */
	.book{
		margin: 1.5rem auto;

		width: 90%;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.book .book-text{
		text-align: justify;

		display: flex;
		flex-direction: column;
	}
	.book-text h4, .book-text p{
		margin: 0px;
	}
	.book-buttons{
		display: flex;
		gap: 1.2rem;
	}
	.book-buttons button{
		border: none;
	}
	.book-buttons i{
		font-size: 1.5rem;
		cursor: pointer;
	}

</style>