# REST API using ASP.NET Core Web API
## Table of Contents
- [Create a new project](#create-a-new-project)
- [Add a Controller](#add-a-controller)
- [Add a Model](#add-a-model)
- [Add a Repository](#add-a-repository)
- [Code](#code)
  - [BooksController](#bookscontroller)
  - [Book](#book)
  - [BookRepo](#bookrepo)
  - [CreateUpdateBookSchema](#createupdatebookschema)


## Create a new project

1. File -> New Project
2. Choose the ASP .NET Core Web API project template
3. Name the project RestApiLab5
4. Name the solution RestApiLab5App
4. Leave the default settings, except for HTTPS - deselect Configure for HTTPS
5. Create and run the project to see what has been created

## Add a Controller

1. Right-click on the Controllers folder
2. Add -> Controller -> API -> API Controller with read/write actions
3. Name the controller BooksController

## Add a Model
1. Create a folder named Models in the Solution Explorer
2. Within the Models folder, create a class named Book
3. This class will serve as the basic schema for the book data

## Add a Repository
1. Create a folder named Repo in the Solution Explorer
2. Within the Repo folder, create an interface named IBook
3. The IBook interface will contain the functions to interact with the database
4. Within the Repo folder, create a class named BookRepo that implements the IBook interface
5. The BookRepo class will use an in-memory database to store the book data

## Code
### `BooksController`
```cpp
using Microsoft.AspNetCore.Mvc;
using MyAPI.Models;
using MyAPI.Repositories;

// For more information on enabling Web API for empty projects, visit https://go.microsoft.com/fwlink/?LinkID=397860

namespace MyAPI.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class BooksController : ControllerBase
    {
        private IBook BookRepository;

        // Constructor
        public BooksController(IBook bookRepo)
        {
            BookRepository = bookRepo;
        }

        // GET: Get all books
        [HttpGet]
        public ActionResult<IEnumerable<Book>> GetBooks()
        {
            return BookRepository.GetBooks().ToList();
        }

        // GET: Get book by Id
        [HttpGet("{id}")]
        public ActionResult<Book> GetBook(Guid id)
        {
            Book foundBook = BookRepository.GetBook(id);

            if(foundBook == null)
                return NotFound();

            return foundBook;
        }

        // POST: Add a book
        [HttpPost]
        public ActionResult CreateBook(CreateUpdateBookSchema book)
        {
            // Create a new book
            var newBook = new Book();

            // Set the data for the book
            newBook.Id = Guid.NewGuid();
            newBook.Title = book.Title;
            newBook.Author = book.Author;
            newBook.Price= book.Price;

            // Add the book using the repo
            BookRepository.CreateBook(newBook);

            return Ok();
        }

        // PUT: Update a book entry
        [HttpPut("{id}")]
        public ActionResult UpdateBook(Guid id, CreateUpdateBookSchema book)
        {
            // Find the book the user wants to update
            var bookToUpdate = BookRepository.GetBook(id);

            // Make sure its not null
            if(bookToUpdate == null) return NotFound();

            // Change the book's data
            bookToUpdate.Author = book.Author;
            bookToUpdate.Price = book.Price;
            bookToUpdate.Author = book.Author;

            // Update the book entry using the repository
            BookRepository.UpdateBook(bookToUpdate);

            return Ok();
        }

        // DELETE: Delete a book
        [HttpDelete("{id}")]
        public ActionResult DeleteBook(Guid id)
        {
            // First of all check if we have the book we try to delete
            var foundBook = BookRepository.GetBook(id);
            if(foundBook == null) return NotFound();

            // Ok, delete it
            BookRepository.DeleteBook(id);
            return Ok();
        }
    }
}
```
### `Book`
```cpp
using System.ComponentModel.DataAnnotations;

namespace MyAPI.Models
{
    public class Book
    {
        [Required]
        public Guid Id { get; set; }

        [Required]
        public string Title { get; set; }

        [Required] public string Author { get;set; }

        [Required]
        [Range(0, 100)]
        public int Price { get; set; }

    }
}
```

### `BookRepo`
```cpp
using MyAPI.Repositories;

namespace MyAPI.Models
{
    public class BookRepo : IBook
    {
        // Create a repo (its a list here)
        private List<Book> books;

        // Constructor
        public BookRepo()
        {
            // Add a book
            books = new()
            {
                // Here we create a new book
                new Book
                {
                    Id = Guid.NewGuid(),
                    Title = "Crime and Punishment",
                    Author = "Dostoyefski",
                    Price = 10
                }
            };

        }

        // Create a new Book
        public void CreateBook(Book book)
        {
            books.Add(book);
        }

        // Delete a Book
        public void DeleteBook(int id)
        {
            throw new NotImplementedException();
        }

        // Get a book by id
        public Book GetBook(Guid id)
        {
            // Find Book
            var book = books.Where(
                    x => x.Id == id
                )
                .SingleOrDefault();

            return book;
        }

        // Get all the books
        public IEnumerable<Book> GetBooks()
        {
            return books;
        }

        // Update a book
        public void UpdateBook(Guid id, Book book)
        {
            var foundBookIndex = books.FindIndex(x => x.Id == id);
            if(foundBookIndex > -1)
                books[foundBookIndex] = book;
        }

        // Delete a book
        void IBook.DeleteBook(Guid id)
        {
            var foundBookIndex = books.FindIndex(x => x.Id == id);
            if (foundBookIndex > -1)
                books.RemoveAt(foundBookIndex);
        }
    }
}
```

### `CreateUpdateBookSchema`
```cpp
using System.ComponentModel.DataAnnotations;

namespace MyAPI.Models
{
    public record CreateUpdateBookSchema
    {
        [Required]
        public string Title { get; set; }

        [Required] public string Author { get; set; }

        [Required]
        [Range(0, 100)]
        public int Price { get; set; }
    }
}
```
### `IBook`
```cpp
using MyAPI.Models;
using System.Collections;

namespace MyAPI.Repositories
{
    public interface IBook
    {
        public IEnumerable<Book> GetBooks();
        public Book GetBook(Guid id);
        public void CreateBook(Book book);
        public void UpdateBook(Book book);
        public void DeleteBook(Guid id);
    }
}
```

