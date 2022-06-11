## <b>Submission Bookshelf - API</b>

## <b>Dicoding Indonesia</b>

### <b>📖 Kelas Belajar Membuat Aplikasi Back-End untuk Pemula.</b>

<br>

---

<br>

## <b>Kriteria</b>

### Terdapat 5 kriteria utama yang terpenuhi dalam membuat proyek Bookshelf API.

<br>

## Kriteria 1 : API dapat menyimpan buku

### API yang Anda buat harus dapat menyimpan buku melalui route:

- ### Method : **POST**
- ### URL : **/books**
- ### Body Request :

```
{
  "name": string,
  "year": number,
  "author": string,
  "summary": string,
  "publisher": string,
  "pageCount": number,
  "readPage": number,
  "reading": boolean
}
```

### Objek buku yang disimpan pada server harus memiliki struktur seperti contoh di bawah ini:

```
{
  "id": "Qbax5Oy7L8WKf74l",
  "name": "Buku A",
  "year": 2010,
  "author": "John Doe",
  "summary": "Lorem ipsum dolor sit amet",
  "publisher": "Dicoding Indonesia",
  "pageCount": 100,
  "readPage": 25,
  "finished": false,
  "reading": false,
  "insertedAt": "2021-03-04T09:11:44.598Z",
  "updatedAt": "2021-03-04T09:11:44.598Z"
}
```

### Properti yang ditebalkan diolah dan didapatkan di sisi server. Berikut penjelasannya:

- ### `id` : nilai `id` haruslah unik. Untuk membuat nilai unik, Anda bisa memanfaatkan _nanoid_.
- ### `finished` : merupakan properti boolean yang menjelaskan apakah buku telah selesai dibaca atau belum. Nilai finished didapatkan dari observasi `pageCount === readPage`.
- ### `insertedAt` : merupakan properti yang menampung tanggal dimasukkannya buku. Anda bisa gunakan `new Date().toISOString()` untuk menghasilkan nilainya.
- ### `updatedAt` : merupakan properti yang menampung tanggal diperbarui buku. Ketika buku baru dimasukkan, berikan nilai properti ini sama dengan `insertedAt`.

### Server harus merespons **gagal** bila:

- ### Client tidak melampirkan properti `name` pada request body. Bila hal ini terjadi, maka _server_ akan merespons dengan:

  - ### Status Code : **400**
  - ### Response Body:

```
{
  "status": "fail",
  "message": "Gagal menambahkan buku. Mohon isi nama buku"
}
```

- ### Client melampirkan nilai properti `readPage` yang lebih besar dari nilai properti `pageCount`. Bila hal ini terjadi, maka _server_ akan merespons dengan:
  - ### Status Code : **400**
  - ### Response Body:

```
{
  "status": "fail",
  "message": "Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"
}
```

- ### Server **gagal** memasukkan buku karena alasan umum _(generic error)_. Bila hal ini terjadi, maka _server_ akan merespons dengan:
  - ### Status Code : **500**
  - ### Response Body :

```
{
  "status": "error",
  "message": "Buku gagal ditambahkan"
}
```

### Bila buku **berhasil** dimasukkan, _server_ harus mengembalikan respons dengan:

- ### Status Code : **201**
- ### Response Body:

```
{
  "status": "success",
  "message": "Buku berhasil ditambahkan",
  "data": {
      "bookId": "1L7ZtDUFeGs7VlEt"
  }
}
```

## Kriteria 2 : API dapat menampilkan seluruh buku

### API yang Anda buat harus dapat menampilkan seluruh buku yang disimpan melalui route:

- ### Method : **GET**
- ### URL : **/books**

### _Server_ harus mengembalikan respons dengan:

- ### Status Code : **200**
- ### Response Body:

```
{
    "status": "success",
    "data": {
        "books": [
            {
                "id": "Qbax5Oy7L8WKf74l",
                "name": "Buku A",
                "publisher": "Dicoding Indonesia"
            },
            {
                "id": "1L7ZtDUFeGs7VlEt",
                "name": "Buku B",
                "publisher": "Dicoding Indonesia"
            },
            {
                "id": "K8DZbfI-t3LrY7lD",
                "name": "Buku C",
                "publisher": "Dicoding Indonesia"
            }
        ]
    }
}
```

Jika **belum** terdapat buku yang dimasukkan, _server_ bisa merespons dengan array `books` kosong.

```
{
    "status": "success",
    "data": {
        "books": []
    }
}
```

## Kriteria 3 : API dapat menampilkan detail buku

### API yang Anda buat harus dapat menampilkan seluruh buku yang disimpan melalui route:

- ### Method : **GET**
- ### URL: **/books/{bookId}**

### Bila buku dengan `id` yang dilampirkan oleh _client_ tidak ditemukan, maka _server_ harus mengembalikan respons dengan:

- ### Status Code : **404**
- ### Response Body:

```
{
    "status": "fail",
    "message": "Buku tidak ditemukan"
}
```

### Bila buku dengan `id` yang dilampirkan **ditemukan**, maka _server_ harus mengembalikan respons dengan:

- ### Status Code : **200**
- ### Response Body:

```
{
    "status": "success",
    "data": {
        "book": {
            "id": "aWZBUW3JN_VBE-9I",
            "name": "Buku A Revisi",
            "year": 2011,
            "author": "Jane Doe",
            "summary": "Lorem Dolor sit Amet",
            "publisher": "Dicoding",
            "pageCount": 200,
            "readPage": 26,
            "finished": false,
            "reading": false,
            "insertedAt": "2021-03-05T06:14:28.930Z",
            "updatedAt": "2021-03-05T06:14:30.718Z"
        }
    }
}
```

## Kriteria 4 : API dapat mengubah data buku

### API yang Anda buat harus dapat mengubah data buku berdasarkan `id` melalui route:

- ### Method : **PUT**
- ### URL : **/books/{bookId}**
- ### Body Request:

```
{
    "name": string,
    "year": number,
    "author": string,
    "summary": string,
    "publisher": string,
    "pageCount": number,
    "readPage": number,
    "reading": boolean
}
```

### _Server_ harus merespons **gagal** bila:

### _Client_ tidak melampirkan properti `name` pada request body. Bila hal ini terjadi, maka _server_ akan merespons dengan:

- ### Status Code : **400**
- ### Response Body:

```
{
    "status": "fail",
    "message": "Gagal memperbarui buku. Mohon isi nama buku"
}
```

### _Client_ melampirkan nilai properti `readPage` yang lebih besar dari nilai properti `pageCount`. Bila hal ini terjadi, maka _server_ akan merespons dengan:

- ### Status Code : **400**
- ### Response Body:

{
"status": "fail",
"message": "Gagal memperbarui buku. readPage tidak boleh lebih besar dari pageCount"
}

### `Id` yang dilampirkan oleh _client_ tidak ditemukkan oleh _server_. Bila hal ini terjadi, maka _server_ akan merespons dengan:

- ### Status Code : **404**
- ### Response Body:

```
{
    "status": "fail",
    "message": "Gagal memperbarui buku. Id tidak ditemukan"
}
```

### Bila buku **berhasil diperbarui**, _server_ harus mengembalikan respons dengan:

- ### Status Code : **200**
- ### Response Body:

```
{
    "status": "success",
    "message": "Buku berhasil diperbarui"
}
```

## Kriteria 5 : API dapat menghapus buku

### API yang Anda buat harus dapat menghapus buku berdasarkan `id` melalui route berikut:

- ### Method : **DELETE**
- ### URL: **/books/{bookId}**

### Bila id yang dilampirkan tidak dimiliki oleh buku manapun, maka server harus mengembalikan respons berikut:

- ### Status Code : **404**
- ### Response Body:

```
{
    "status": "fail",
    "message": "Buku gagal dihapus. Id tidak ditemukan"
}
```

### Bila `id` dimiliki oleh salah satu buku, maka buku tersebut harus dihapus dan _server_ mengembalikan respons berikut:

- ### Status Code : **200**
- ### Response Body:

```
{
    "status": "success",
    "message": "Buku berhasil dihapus"
}
```

<br>

## **Pengujian**

### Ketika membangun Bookshelf API, tentu Anda perlu menguji untuk memastikan API berjalan sesuai dengan kriteria yang ada. Kami sudah menyediakan berkas Postman Collection dan Environment yang dapat Anda gunakan untuk pengujian. Silakan unduh berkasnya pada tautan berikut:

- ### [Postman Bookshelf API Test Collection dan Environment](https://github.com/dicodingacademy/a261-backend-pemula-labs/raw/099-shared-files/BookshelfAPITestCollectionAndEnvironment.zip)

### Anda perlu meng-import kedua berkas tersebut pada **Postman** untuk menggunakannya.

1. ### Caranya, ekstrak berkas yang sudah diunduh hingga menghasilkan dua berkas file JSON.

2. ### Kemudian pada aplikasi Postman, klik tombol **import** yang berada di atas panel kiri aplikasi Postman.

3. ### Kemudian klik tombol **Upload Files** untuk meng-import kedua berkas JSON hasil ekstraksi.

4. ### Setelah itu, Bookshelf API Test Collection dan Environment akan tersedia pada Postman Anda.

<br>

## **Tambahan Fitur :**

- ### Fitur query parameters pada route **GET /books** (Mendapatkan seluruh buku).
- ### `?name` : Tampilkan seluruh buku yang mengandung nama berdasarkan nilai yang diberikan pada query ini. Contoh **/books?name=”dicoding”**, maka akan menampilkan daftar buku yang mengandung nama “dicoding” secara non-case sensitive _(tidak peduli besar dan kecil huruf)_.
- ### `?reading` : Bernilai 0 atau 1. Bila 0, maka tampilkan buku yang sedang tidak dibaca (reading: _false_). Bila 1, maka tampilkan buku yang sedang dibaca (reading: _true_). Selain itu, tampilkan buku baik sedang dibaca atau tidak.
- ### `?finished` : Bernilai 0 atau 1. Bila 0, maka tampilkan buku yang sudah belum selesai dibaca (finished: _false_). Bila 1, maka tampilkan buku yang sudah selesai dibaca (finished: _true_). Selain itu, tampilkan buku baik yang sudah selesai atau belum dibaca.
- ### Menerapkan **CORS** pada seluruh resource yang ada.
- ### Menggunakan **ESLint** dan salah satu style guide agar gaya penulisan kode JavaScript lebih konsisten.
