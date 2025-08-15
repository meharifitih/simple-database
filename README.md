# golang-database

A simple file-based JSON database in Go, supporting basic CRUD operations with concurrency safety.

## Features

- Store, read, and delete JSON records in collections (folders)
- Thread-safe operations using mutexes
- Customizable logging (uses [lumber](https://github.com/jcelliott/lumber))
- Example usage with a `users` collection

## Project Structure

```
go.mod
go.sum
main.go
users/
    Alice.json
    Bob.json
    Charlie.json
    David.json
    Jane.json
    John.json
```

## Usage

### Running the Example

1. Clone the repository.
2. Run:

   ```sh
   go run main.go
   ```

   This will:
   - Initialize the database in the current directory
   - Write several user records to the `users` collection
   - Read and print all user records

### Database API

The main database logic is implemented in [`main.go`](main.go):

- `New(dir string, options *Options) (*Driver, error)`: Create a new database driver.
- `Write(collection, resource string, v interface{}) error`: Write a record.
- `Read(collection, resource string, v interface{}) error`: Read a record.
- `ReadAll(collection string) ([]string, error)`: Read all records in a collection.
- `Delete(collection, resource string) error`: Delete a record or collection.

### Example User Structure

```go
type Address struct {
    City    string
    State   string
    Country string
    PinCode json.Number
}

type User struct {
    Name    string
    Age     json.Number
    Contact string
    Company string
    Address Address
}
```

## Dependencies

- [github.com/jcelliott/lumber](https://github.com/jcelliott/lumber) for logging

Install dependencies with:

```sh
go mod tidy
```

## License

MIT