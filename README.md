# Library App Back-End with Hapi.js

This project is a Bookshelf API built using the Hapi.js framework. It provides a simple CRUD API for managing books. The project is designed to meet the requirements of the Dicoding Submission for the "Belajar Membuat Aplikasi Back-End untuk Pemula" class.

## Features
- **Add Books**: Add new books with attributes like title, author, publisher, page count, and reading status.
- **View Books**: Retrieve all books or filter them by:
  - name (case-insensitive partial match)
  - reading status (0 or 1)
  - finished status (0 or 1)
- **View Book Details**: Retrieve detailed information about a single book by its ID.
- **Edit Book**: Update an existing book’s details.
- **Delete Book**: Remove a book by its ID.

## Tech Stack
- **Runtime**: [Node.js](https://nodejs.org/)
- **Framework**: [Hapi.js](https://hapi.dev/)
- **Database**: In-memory array (no external databases required)

The application is designed to be easily tested and run locally without additional database setup.

---

## Getting Started

### Prerequisites
  - Node.js (version 18 or above recommended)
  - npm (comes with Node.js)

---

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/library-app-back-end.git
   cd library-app-back-end
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the server:
   ```bash
   npm run start
   ```

4. Test the API using tools like Postman or curl.

---

## API Documentation

### Add Book
```http
/POST /books
```
**Request Body**:
```json
{
  "name": "Buku A",
  "year": 2021,
  "author": "Jane Doe",
  "summary": "Buku A summary",
  "publisher": "Publisher A",
  "pageCount": 250,
  "readPage": 100,
  "reading": true
}
```
**Response (Success)**:
```json
{
  "status": "success",
  "message": "Buku berhasil ditambahkan",
  "data": {
    "bookId": "abc123xyz"
  }
}
```
**Failure Cases:**
- Missing name:
```json
{
  "status": "fail",
  "message": "Gagal menambahkan buku. Mohon isi nama buku"
}

```
- readPage > pageCount:
```json
{
  "status": "fail",
  "message": "Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"
}
```

---

### Get All Notes
```http
/GET /books
```
Query Parameters:
- ?name=<string> : Filter books that contain <string> in their name (case-insensitive).
- ?reading=0 or ?reading=1 : Filter by reading status.
- ?finished=0 or ?finished=1 : Filter by finished status.

**Response (Success)**:
```json
{
  "status": "success",
  "data": {
    "books": [
      {
        "id": "abc123xyz",
        "name": "Buku A",
        "publisher": "Publisher A"
      }
    ]
  }
}
```

---

### Get Note by ID
```http
/GET /books/{bookId}
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `bookId`  | `string` | **Required**. ID of the book      |

**Response (Success)**:
```json
{
  "status": "success",
  "data": {
    "book": {
      "id": "abc123xyz",
      "name": "Buku A",
      "year": 2021,
      "author": "Jane Doe",
      "summary": "Buku A summary",
      "publisher": "Publisher A",
      "pageCount": 250,
      "readPage": 100,
      "finished": false,
      "reading": true,
      "insertedAt": "2024-12-01T10:00:00.000Z",
      "updatedAt": "2024-12-01T10:00:00.000Z"
    }
  }
}
```

**Response (Not Found)**:
```json
{
  "status": "fail",
  "message": "Buku tidak ditemukan"
}
```

---

### Edit Note
```http
/PUT /books/{bookId}
```
**Request Body (example)**:
```json
{
  "name": "Buku A Revisi",
  "year": 2021,
  "author": "Jane Doe Updated",
  "summary": "Updated summary",
  "publisher": "Publisher A Updated",
  "pageCount": 250,
  "readPage": 150,
  "reading": false
}
```

**Response (Success)**:
```json
{
  "status": "success",
  "message": "Buku berhasil diperbarui"
}
```

**Failure Cases:**
- Missing name:
```json
{
  "status": "fail",
  "message": "Gagal memperbarui buku. Mohon isi nama buku"
}
```
- readPage > pageCount:
```json
{
  "status": "fail",
  "message": "Gagal memperbarui buku. readPage tidak boleh lebih besar dari pageCount"
}
```
- Book ID not found
```json
{
  "status": "fail",
  "message": "Gagal memperbarui buku. Id tidak ditemukan"
}
```

---

### Delete Note
```http
/DELETE /books/{bookId}
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `BookId`  | `string` | **Required**. ID of the book      |

**Response (Success)**:
```json
{
  "status": "success",
  "message": "Buku berhasil dihapus"
}
```

**Response (Not Found)**:
```json
{
  "status": "fail",
  "message": "Buku gagal dihapus. Id tidak ditemukan"
}
```

---
