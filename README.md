# JAVASCRIPT INTERMEDIATE
## *Asynchronous*
### *Callback*
*Callback* adalah sebuah *function*, namun bedanya dengan *function* pada umumnya adalah pada cara eksekusinya. Jika *function* pada umumnya dieksekusi secara langsung, sedangkan *callback* dieksekusi di dalam *function* lain melalui parameter. Kita akan menemukan proses *callback asynchronous* pada proses ajax, komunikasi HTTP, Operasi file, *timer* dan sebagainya.

***Synchronous* dan *Asynchronous* pada JavaScript**

Pada *synchronous output* di proses berdasarkan urutan kode.

Contoh proses synchronous:

    function proses1() {
        console.log("proses 1 selesai dijalankan");
    }

    function proses2() {
        console.log("proses 2 selesai dijalankan");
    }

    function proses3() {
        console.log("proses 3 selesai dijalankan");
    }

    proses1();
    proses2();
    proses3();



Pada kode di atas, kita bisa melihat bahwa proses1(), proses2(), dan proses3() berjalan berurutan seperti yang seharusnya. Sedangkan pada *asynchronous* yang biasa dikenal juga dengan sebutan *non*-*blocking* mengizinkan komputer kita untuk memproses perintah lain sambil menunggu suatu proses lain yang sedang berlangsung. Ini artinya kita bisa melakukan lebih dari 1 proses sekaligus (*multi*-*thread*).

Contoh proses asynchronous:

    function proses1() {
        console.log("proses 1 selesai dijalankan");
    }

    function proses2() {
        // setTimeout or delay for *asynchronous* simulation
        setTimeout(function () {
            console.log("proses 2 selesai dijalankan");
        }, 100);
    }

    function proses3() {
        console.log("proses 3 selesai dijalankan");
    }

    proses1();
    proses2();
    proses3();



Pada hasil output di atas kita bisa lihat bahwa proses3() selesai terlebih dahulu dibanding proses2(). Hal ini terjadi dikarenakan proses2() melakukan **setTimeout()** yang merupakan proses *asynchronous* sehingga proses3() selesai terlebih dibanding proses2().

**Menggunakan *Callback***

Kita akan coba memperbaiki *asynchronous* di atas dengan memastikan *output* proses1, proses2, dan proses3 sesuai urutan dengan menggunakan *callback*.

    function proses1() {
        console.log("proses 1 selesai dijalankan");
    }

    function proses2(callback) {
        setTimeout(function () {
            console.log("proses 2 selesai dijalankan");
            callback();
        }, 100);
    }

    function proses3() {
        console.log("proses 3 selesai dijalankan");
    }
    proses1();
    proses2(proses3);



Analogi kasus di atas adalah bayangkan kamu memiliki *method* yang melakukan proses menampilkan *image* lalu kita memerlukan *callback* untuk memastikan proses menampilkan *image* terpanggil terlebih dahulu sebelum menampilkan ke *user* yang ingin mengaksesnya. Jadi *callback* dapat digunakan untuk mengatur order function yang harus berjalan terlebih dahulu.

**Membuat *callback function***

Kita dapat memanggil callback pada sebuah function dengan cara memanggilnya ke dalam parameter dan digunakan di dalam function. Langkah-langkahnya sebagai berikut:

1. Deklarasikan dahulu **function greeting(name)** yang ingin kita panggil dalam *callback function* lain. **Function greeting(name)** berisi **console.log()** yang menerima sebuah parameter **name**.

        function greeting(name) {
            console.log("Halo " + (name) + ", selamat datang di Skilvul!");
        }

2. buat sebuah **function introduction(firstName, lastName, callback)** dengan menerima parameter **firstName**, **lastName** dan **callback** lalu di dalam **function** tersebut kita menggabungkan parameter **firstName** dan **lastName** ke dalam variabel **fullName** untuk mengirimkannya ke dalam *callback*.

        function introduction(firstName, lastName, callback) {
            const fullName = (firstName) + (lastName);

            callback(fullName);
        }

        introduction("Ahmad", "Fauzul", greeting); 

    
3. Dalam pemanggilan **function introduction**, kita mengisi argumen dari parameter yang dibutuhkan yaitu Ahmad, Fauzul, dan **function greeting** yang sudah kita buat sebelumnya lalu kita panggil **callback(fullName)** di dalam **function introduction** sehingga kita bisa mendapatkan hasil dari **function greeting**.

### *Promise*
*Promise* adalah salah satu fitur dari ES6 (ES2015) JavaScript. Konsep *promise* hadir untuk memecahkan masalah yang bertele-tele dengan *callback*, semakin banyak kita menggunakan *callback* untuk proses *asynchronous* semakin kompleks dan sulit kode kita untuk dibaca dan dipelihara.

**Konsep *Promise***

*Promise* sesuai dengan artinya adalah janji. Seperti ketika kita berjanji, jika apa yang kita janjikan bisa kita lakukan maka kita harus melakukannya, jika janjinya ada halangan maka kita tidak bisa melakukannya atau jika janji tersebut belum pada waktunya kita juga harus menunggunya.

**3 Status *Promise* di JavaScript**

Analogi dari sebuah *promise* di JavaScript itu sama seperti kita saat mengambil suatu data baik itu dari database maupun *Request* API. Akan ada 3 kondisi yaitu data sedang diproses, data berhasil didapatkan, atau data gagal didapatkan.

- **pending**, jika data sedang diproses.
- **fulfilled**, jika data telah berhasil didapatkan.
- **rejected**, jika data gagal didapatkan.

**Contoh menggunakan *promise***

    let newPromise = new Promise((resolve, reject) => {
        if (true) {
            // apa yang dilakukan jika promise fulfilled
            resolve("Berhasil");
        } else {
            // apa yang dilakukan jika promise rejected
            reject("Gagal");
        }
    });

Kita bisa membuat sendiri apa yang akan dilakukan pada sebuah *promise*. Di dalam *promise* ada 2 *keyword* yaitu **resolve()** (jika proses berhasil atau *fullfilled*) dan **reject()** (jika proses gagal atau *rejected*).

**Contoh penggunaan *promise fullfilled***

Untuk *fulfilled* hanya bisa tereksekusi jika kita kondisi berhasil pada saat kita melakukan *async*. Kita *set condition* menjadi *true* untuk simulasi *fulfilled*.

    const condition = true;

    let newPromise = new Promise((resolve, reject) => {
        if (condition) {
            // apa yang dilakukan jika promise 'fulfilled'
            resolve("Berhasil");
        } else {
            // apa yang dilakukan jika promise 'rejected'
            reject(new Error("Error Gagal"));
        }
    });

Untuk bisa mengeksekusi promise yang sudah dibuat kita bisa memanggil promise tersebut menggunakan **.then()**:

    const condition = true;

    let newPromise = new Promise((resolve, reject) => {
        if (condition) {
            // apa yang dilakukan jika promise 'fulfilled'
            resolve("Berhasil");
        } else {
            // apa yang dilakukan jika promise 'rejected'
            reject(new Error("Error Gagal"));
        }
    });

    newPromise.then((result) => {
        console.log(result);
    });



Selain itu kita juga bisa memanggil **.then()** lebih dari satu kali ketika dibutuhkan.

Contoh:

    const condition = true;

    let newPromise = new Promise((resolve, reject) => {
        if (condition) {
            // apa yang dilakukan jika promise 'fulfilled'
            resolve("Berhasil");
        } else {
            // apa yang dilakukan jika promise 'rejected'
            reject(new Error("Error Gagal"));
        }
    });

    newPromise.then((result) => {
        return result;
    })

    .then((result2) => {
        console.log(result2 + "!!");
    });



**Contoh penggunaan *promise rejected***

Untuk *rejected* hanya bisa tereksekusi jika kita mengalami *error* pada saat kita melakukan proses *asynchronous*. Kita *set condition* menjadi *false* untuk simulasi *rejected*.

    const condition = false;

    let newPromise = new Promise((resolve, reject) => {
        if (condition) {
            // apa yang dilakukan jika promise 'fulfilled'
            resolve("Berhasil");
        } else {
            // apa yang dilakukan jika promise 'rejected'
            reject(new Error("Error Gagal"));
        }
    });


Untuk bisa mengantisipasi jika terjadi *error* kita bisa menambahkan **.catch()** pada *promise*. Sehingga, kita bisa memberi tahu pengguna jika terjadi suatu *error*.

    const condition = false;

    let newPromise = new Promise((resolve, reject) => {
        if (condition) {
            // apa yang dilakukan jika promise 'fulfilled'
            resolve("Berhasil");
        } else {
            // apa yang dilakukan jika promise 'rejected'
            reject(new Error("Error Gagal"));
        }
    });

    newPromise.then((result) => {
        console.log(result);
    })

    .catch((error) => {
        console.log(error.message); //
    });


Selain **.then()** dan **.catch()**, dalam *promise* kita juga memiliki **.finally()** dalam *promise* JavaScript. **.finally()** adalah fungsi *callback* yang pasti tereksekusi dalam kondisi apapun (**fullfield** ataupun **rejected**).

    const condition = true;

    let newPromise = new Promise((resolve, reject) => {
        if (condition) {
            // apa yang dilakukan jika promise 'fulfilled'
            resolve("Berhasil");
        } else {
            // apa yang dilakukan jika promise 'rejected'
            reject(new Error("Error Gagal"));
        }
    });

    newPromise
    .then((result) => {
        console.log(result); // Output: Berhasil
    })
    .catch((error) => {
        console.log(error);
    })
    .finally(() => {
        console.log("Finally tetap terpanggil dalam kondisi fulfilled ataupun rejected");
    });



### *Promise Instance*
Pada banyak kasus biasanya kita dapat menggunakan *promise instance* seperti **.then()**, **.catch()**, dan **.finally()** untuk mengantisipasi *response* saat kita melakukan *request* ke *server*.

Berikut contoh  penggunaan *promise instance* untuk proses mengambil data API dari https://jsonplaceholder.typicode.com/ :

    fetch("https://jsonplaceholder.typicode.com/users")
    .then((response) => response.json()) // Jika data berhasil didapatkan

    .then((json) => console.log(json))
    .catch((error) => console.log(error)) // Jika data tidak berhasil didapatkan
  
    .finally(() => {
        console.log("Finally tetap terpanggil dalam kondisi fulfilled ataupun rejected"); // Finally tetap terpanggil dalam kondisi fulfilled ataupun rejected
    });



Dari kode di atas, kita dapat mengetahui bahwa:
1. **.then()** digunakan untuk mengantisipasi keadaan *fulfilled*, setelah *response* didapatkan dan menampilkan data *array of object* dari *server*.
2. **.catch()** digunakan untuk mengantisipasi keadaan *rejected*, jika *response* gagal didapatkan atau terdapat *error* lain dari *server*, lantas apa yang ingin kita lakukan pada aplikasi? Menampilkan page error? Atau menampilkan alert?
3. **.finally()** digunakan untuk mengantisipasi apa yang akan aplikasi lakukan saat *response* berhasil ataupun gagal didapatkan. Namun, penggunaan **.finally()** biasanya jarang dilakukan.

### *Async*/*await*
*Async*/*await* baru ada ketika update ES8 JavaScript dan dibangun menggunakan *promise*. Jadi sebenarnya *async*/*await* dan *promise* itu sama saja, namun hanya berbeda dari *syntax* dan cara penggunaannya. Sebuah *async function* bisa tidak berisi *await* sama sekali atau lebih dari satu *await*. *Keyword await* hanya bisa digunakan didalam *async function*, jika digunakan di luar *async function* maka akan terjadi error.

***Async***

*Async*, mengubah *function synchronous* menjadi *asynchronous*.

Berikut ini contoh penggunaan dari async :

    // async menggunakan keyword function 
    async function tesAsyncAwait() {
        return "Fulfilled";
    }

    console.log(tesAsyncAwait());

    // async menggunakan arrow function
    const tesAsyncAwait = async () => {
        return "Fulfilled";
    };

    console.log(tesAsyncAwait());

Jika salah satu kode di atas dijalankan, maka akan terlihat hasil *output* di console 

***Await***

*Await* hanya bisa digunakan dalam *async function* dan *await* adalah *keyword* dalam *async* yang digunakan untuk menunda hingga proses *asynchronous* selesai.

Berikut contoh penggunaan dari *async*/*await*:

    async function tesAsyncAwait() {
        await 'Fulfilled';
    }

Kita juga bisa memberikan *error handling* pada *async*/*await*. Berikut contoh lengkap penggunaan *async*/*await*:

    // Definisikan dahulu promise yang ingin digunakan
    let condition = true;
    let tesAsyncAwait = async (condition) => {
        if (condition) {
            return "Condition is fulfilled!";
        } else {
            throw "Condition is rejected!";
        }
    };

    // Membuat fungsi run menjadi asynchronous menggunakan async/await
    const run = async (condition) => {
        try {
            const message = await tesAsyncAwait(condition);
            console.log(message);  // Output: Condition is fulfilled!
            console.log("After condition is fulfilled"); // Output: After condition is fulfilled
        } catch (error) {
            console.log(error);
        }
    };

    run(true);

Dari kode di atas, kita dapat melihat bahwa *run* adalah sebuah fungsi *async* dan *await* dipanggil bersamaan dengan fungsi **tesAsyncAwait(condition)**. **Await** pada fungsi ini artinya, **console.log** pada *message* dan **After condition is fulfilled** tidak akan dijalankan (ditunda) hingga proses **tesAsyncAwait(condition)** selesai dijalankan.



Berikut merupakan contoh perbandingan jika program sebelumnya dibuat menggunakan *promise*:

    let condition = true;
    let tesPromise = new Promise((resolve, reject) => {
         if (condition) {
            resolve("Condition is fulfilled!");
        } else {
            reject(new Error("Condition is rejected!"));
        }
    });

    tesPromise
    .then(result =>{
        console.log(result); // Condition is fulfilled!
        console.log("After condition is fulfilled"); // After condition is fulfilled
    })
    .catch(error =>{
        console.log(error);
    })


### *Fetch*
Dalam JavaScript kita bisa mengirimkan *network request* dan juga bisa mengambil informasi data terbaru dari *server* jika dibutuhkan. Contoh *network request* yang biasa kita lakukan adalah sebagai berikut:

- Mengirimkan data dari sebuah form.
- Mengambil data untuk ditampilkan dalam list/table.
- Mendapatkan notifikasi.

Dalam melakukan *network request*, JavaScript memiliki metode bernama **fetch()**. Proses melakukan **fetch()** adalah salah satu proses *asynchronous* di JavaScript sehingga kita perlu menggunakan salah satu di antara *promise* atau *async*/*await*.

***Fetch* dengan *Promise***

Berikut ini contoh *request* data dengan **fetch()** menggunakan *promise*:

    fetch("https://jsonplaceholder.typicode.com/posts")
    .then(function (response) {
        return response.json();
    })
    .then(function (post) {
        console.log(post);
    });

Kode di atas mengambil data end-point dari API JSONPlaceholder.


***Fetch* dengan *async*/*await***

Berikut contoh *request* data dengan **fetch()** menggunakan *async*/*await*:

    const tesFetchAsync = async () => {
        let response = await fetch("https://jsonplaceholder.typicode.com/posts");
        response = await response.json();
        console.log(response);
    };
    tesFetchAsync();

Kita masih mengambil data dari sumber end-point yang sama dengan fetch() sebelumnya yang menggunakan promise sehingga hasilnya pun masih sama persis seperti sebelumnya.



# RESPONSIVE WEB DESIGN
Dalam membuat aplikasi kita harus memikirkan *user* yang akan menggunakannya. *Device* yang umumnya digunakan adalah laptop/PC, smartphone, dan tablet. *Responsive Web Design* bertujun untuk membuat *desain website* kita dapat diakses dalam *device* apapun.

## *Add Viewport in* HTML
Salah satu cara untuk membuat website kita menjadi responsive adalah dengan menambahkan baris perintah
    
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

di tag `<head>` pada HTML.

Perintah lengkapnya:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
    </body>
    </html>

## Media *Query*
*Media query* digunakan untuk membuat beberapa *styles* tergantung pada jenis *device*. *Media query* untuk *responsive web design* umumnya hanya menggunakan 2 jenis media query, yaitu:

1. min-width

        @media screen and (min-width: your pixel) {
            /* tag elemen HTML dan CSS */
        }
2. max-width

        @media screen and (max-width: your pixel) {
            /* tag elemen HTML dan CSS */
        }

Ada 2 cara dalam menggunakan media query

1. Membuat file css berbeda untuk masing-masing *device*.
2. Menggabungkan 1 file css untuk *setting styling* berbagai *device*.

## *Breakpoint*
*Breakpoint* adalah perubahan yg terjadi pada tampilan saat berganti *device* atau ukuran *width*. Misalnya ada 2 tampilan berbeda untuk 2 *device*, artinya ada 2 buah *breakpoint*. 

*Responsive web design* dilakukan sesuai kebutuhan konten kita. Jika konten yang ditampilkan sudah tidak bisa diakses atau sulit dilihat pada *width* tertentu, sudah saatnya kamu menggunakan *media query*. Tidak ada aturan baku besaran *width* dan berapa banyak *breakpoint* yang harus dilakukan. 

# *BOOTSTRAP*
*Bootstrap* adalah *framework* HTML, CSS, dan JavaScript yang berfungsi untuk mendesain *website responsive* dengan cepat dan mudah. *Bootstrap* bersifat *responsive* berkat *grid system* yang digunakan. Sistem *grid* pada *bootstrap* menggunakan rangkaian *containers*, baris, dan kolom untuk menyesuaikan bentuk *layout* dan konten *website* kita. *Bootstrap* menjamin tampilan *website* kita akan tetap rapi dan konsisten di berbagai perangkat pengunjung, baik melalui smartphone, tablet, ataupun laptop.

## Memanggil *Bootstrap*
Ada 2 cara dalam memanggil *bootstrap*, yaitu:

1. *Bootstrap online*

    Pada file HTML, tuliskan perintah berikut: (menggunakan *bootstrap 5)

        <!-- memanggil css bootstrap online -->
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/css/bootstrap.min.css">

        <!-- memanggil js bootstrap online -->
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/js/bootstrap.bundle.min.js"></script>

2. *Bootstrap* yang sudah didownload

    Langkah pertama adalah mendownload file *bootsrap* 5 pada *browser*, kemudian simpan di folder "vendor" kita. Setelah itu baru bisa dipanggil pada file HTML dengan perintah:

        <!-- memanggil css bootstrap yang sudah didownload -->
        <link rel="stylesheet" href="css/bootstrap.min.css">

        <!-- memanggil js bootstrap yang sudah didownload -->
        <script src="js/bootstrap.bundle.js"></script>

## *Grid System*
Penggunaan *Grid System*, layar pada laptop kita akan terbagi menjadi 12 bagian (kolom). Untuk lebih jelasnya, tuiskan code berikut pada file HTML.

        <div class="container" style="background-color: red;">
        <div class="row">
            <div class="col-12" style="background-color: green;">
            &nbsp;
            </div>
        </div>

        <div class="row">
            <div class="col-4" style="background-color: yellow;">
            &nbsp;
            </div>

            <div class="col-8" style="background-color: violet;">
                &nbsp;
                </div>
        </div>

        <div class="row">
            <div class="col-7" style="background-color: blue;">
            &nbsp;
            </div>
        </div>

        <div class="row">
            <div class="col-10" style="background-color: violet;">
            &nbsp;
            </div>
        </div>

        <div class="row">
            <div class="col-10" style="background-color: greenyellow;">
            &nbsp;
            </div>
        </div>
    </div>


Pada code di atas, 

- class col-12 menandakan full-width
- &nbsp; untuk blankspace
- class : container dan container-fluid untuk container full-width

*Bootstrap* menyediakan *component-component* yang siap pakai, seperti *accordion*, *alert*, *badge*, *card*, *button*, *navbar*, dan lain-lain.