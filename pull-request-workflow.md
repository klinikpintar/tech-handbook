# Kolaborasi dan Review menggunakan *Pull Request*

Bagian ini berisi tentang proses _Pull Request_ yang berjalan di Medigo, tata cara dan kesepakatan yang berlaku. 

---
### *Main Cast*

Dalam proses _Pull Request_ ini terdapat tiga peran utama, yakni:
- **Captain**: *Code reviewer & decision maker* (pengembang utama).
- **QA**: *Feature/function reviewer*.
- **Member**: *Developer* (pengembang).

![](https://i.imgur.com/qNyLVwx.png)

### *Pull Request Manifesto @ Medigo*

1. Tidak boleh ada proses development di dalam *branch* `develop` atau `master` - kedua *branch* tersebut hanya berfungsi untuk `merge, test & release` fitur yang sudah stabil
2. Segera buat *Pull Request* setelah *branch* dibuat dan *remote push* sudah dilakukan.
3. *Pull Request* akan ditolak apabila ditemukan konflik dalam kode. Pengembang harus menyelesaikan konflik tersebut dan memastikan tidak ada konflik dalam *Pull Request*
4. Lakukan penamaan *branch* sesuai kesepakatan bersama ( lihat Ketentuan *Branching* )
5. *Branch* `hotfix` akan menghasilkan *Pull Request* ke *branch* `master` dan *branch* `develop`
7. Pengembang utama sebaiknya melakukan proses `merge` di repositori lokal. Khusus untuk branch `story` sebaiknya dilakukan *preserve commit history* dengan melakukan proses `git merge --no-ff`. Untuk branch lain silahkan `merge & squash` menggunakan `git merge --squash`
8. Pengembang utama yang memiliki akses *push* ke `master` dan `develop` harus mengatur proses `release` aplikasi dan memungkinkan untuk membuat *branch* `release` dengan beberapa permintaan pekerjaan tambahan sebelum akhirnya akan dilakukan `merge` ke `develop` dan `master`


### Ketentuan *Branching*

Pilihan nama *branch* yang dapat digunakan adalah

- **story**/[nomor trello]-[deskripsi]

>  Untuk *Story* yang dirasa terlalu besar, pecah ke dalam *Task* yang lebih kecil untuk kemudian di merge ke *branch* `story` sebelum melakukan *Pull Request* ke *branch* `develop`

- **task**/[nomor trello]-[deskripsi]
- **improvement**/[nomor trello]-[deskripsi]
- **bugfix**/[nomor trello]-[deskripsi]
- **hotfix**/[nomor trello]-[deskripsi]

Contoh:

- task/TQ-091-post-schedule-to-medigo-webhook
- improvement/w-165-use-promise-all-to-get-schedules-api
- bugfix/w-150-slot-number-is-undefined
- hotfix/w-199-health-center-config-not-loaded

**Notes**

Untuk repository yang tidak akan mengalami banyak pengembangan ( one and done ), harap menggunakan branching berikut

- **master**  : cukup jelas
- **develop** : hasil pengembangan dari branch `latest` akan di-merge kesini
- **latest** : seluruh pengembangan akan dilakukan di branch ini dan PR akan dibuat ke `develop`
 
### Konsep Git

- Gunakan pesan *commit* yang relevan dan masukkan *tag* yang sesuai.
	- [DOCS] deskripsi perubahan pada dokumentasi
	- [ADD] deskripsi penambahan fitur yang dilakukan
	- [UPDATE] deskripsi *update* yang dilakukan pada fitur yang ada
	- [FIX] deskripsi perbaikan yang dilakukan
	- [PERF] deskripsi perubahan yang meningkatkan *performance*
	- [STYLE] deskripsi perapian code sesuai *standard* yang dilakukan
	- [REFACTOR] deskripsi code yang diubah tetapi bukan perbaikan atau penambahan fitur
- [Git Cheatsheet](https://www.git-tower.com/blog/git-cheat-sheet/)
- [Rewrite Commit History](https://git-scm.com/book/id/v2/Git-Tools-Rewriting-History)
- [Squash Published Commits](https://stackoverflow.com/questions/5667884/how-to-squash-commits-in-git-after-they-have-been-pushed)

### Ketentuan *Pull Request*

*Template* yang digunakan untuk membuat *pull request* (dalam format markdown) adalah

#### ISSUE LINK

Berisi tautan *Trello card* yang berkaitan dengan perubahan yang dilakukan.

#### WHAT TO TEST

Apa saja yang perlu dites untuk memastikan fitur baru atau perbaikan fitur berjalan dengan baik.

#### EXPECTATION

Daftar apa saja yang perlu diperiksa yang dijadikan patokan bahwa fitur berjalan sebagaimana mestinya.

#### HOW

Berisi langkah-langkah mengenai bagaimana cara QA mereproduksi *state* fitur agar bisa melakukan *review* *pull request* tanpa kendala seperti setup, inisialisasi database, software yang perlu di-*install*, dll.

#### ADDITIONAL NOTES

Berisi catatan tambahan atau hal-hal pendukung yang perlu diketahui oleh QA dalam melakukan *review*. Biasanya aset atau *file* yang harus di-*download*, ketergantungan *pull request* di repositori ini dengan *pull request* di repositori lain, dll.

---

Contoh:

#### ISSUE LINK

https://trello.com/c/uPka4Ic7

#### WHAT TO TEST

##### GET POSTS API

Send request to endpoint `GET /api/posts` and give query params as following:

| Key             | Value           |
|-----------------|-----------------|
| `category_slug` | `dinosaur`      |
| `page`          | `1`             |

#### EXPECTATION

- [ ] Returns status code 200 OK
- [ ] Returns object like this

```json
{
  "data": [
    {
      "id": 1,
      "title": "What's my favorite dinosaur? I like any dinosaur that wants to worship my problems",
      "excerpt": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam ac lectus dolor. Donec enim tortor, cursus interdum facilisis quis, aliquam ac ipsum. Sed malesuada lacinia molestie. In non diam massa. Duis viverra dictum risus, at pretium erat. Morbi a diam faucibus, placerat lectus nec, dapibus lectus. Donec id massa urna.",
      "image": "http://localhost:8002/storage/posts/2020-01/iPZcSQJfvroaMobBoYcX.png",
      "link": "http://localhost:8002/blog/whats-my-favorite-dinosaur-i-like-any-dinosaur-that-wants-to-worship-my-problems",
      "meta_description": "Amtocephale Pamparaptor Daxiatitan Kundurosaurus Carcharodontosaurus Shuosaurus Unaysaurus Shenzhouraptor Lexovisaurus Bradycneme.",
      "meta_keywords": "cephale, raptor, saurus, bradycneme, titan",
      "created_at": {
        "date": "2020-01-20 08:00:10.000000",
        "timezone_type": 3,
        "timezone": "UTC"
      }
    }
  ],
  "links": {
    "first": "http://localhost:8002/api/posts?page=1",
    "last": "http://localhost:8002/api/posts?page=1",
    "prev": null,
    "next": null
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "path": "http://localhost:8002/api/posts",
    "per_page": 5,
    "to": 1,
    "total": 1
  }
}
```

#### HOW

1. Install and use PHP 7.1,
2. Install and use MySQL 5.6 or MariaDB,
3. Create a database for this app (name is up to you),
4. Restore the database with attached SQL script,
5. Clone this repo to your local machine,
6. Change directory to the cloned repo,
7. Run `composer install`,
8. Run `php artisan key:generate`,
9. Change `APP_URL` to `http://localhost:8002` in `.env` file,
10. Change DB related variables according to your own database in `.env` file,
11. Run `php artisan serve --port:8002`,
12. Login to http://localhost:8002/admin using `dino@example.com` and `secret` as credentials,
13. Go to Categories menu from sidebar,
14. Add new category with Name Dinosaur (don’t change the slug),
15. Edit any post and change the Post Category to Dinosaur,
16. Send request the API endpoint mentioned above using Postman or any other REST client.
17. See if the returned posts are only of Dinosaur category.

#### ADDITIONAL NOTES

SQL script: [download link](https://google.co.id)
