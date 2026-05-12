# Jawaban Pertanyaan

**a. How much data your publisher program will send to the message broker in one run?**

Program publisher akan mengirimkan tepat **5 buah pesan (data event)** ke message broker dalam satu kali eksekusi (run). Pesan-pesan ini dikirimkan secara berurutan menggunakan metode `publish_event` yang disediakan oleh library `CrosstownBus`. Setiap pesan yang dikirimkan merupakan instansiasi dari struct `UserCreatedEventMessage`. Di dalam struct tersebut, terdapat dua atribut atau data utama yang dibungkus dan dikirimkan, yaitu `user_id` dan `user_name`. Kelima data pesan tersebut memiliki nilai `user_id` yang bersifat unik, berurutan mulai dari "1" hingga "5". Selain itu, nilai `user_name` pada masing-masing data juga dibuat berbeda sesuai dengan identitas pengguna, yaitu "Amir", "Budi", "Cica", "Dira", dan "Emir" yang masing-masing didahului oleh nomor NPM. Oleh karena itu, total beban data per satu kali pengeksekusian program adalah 5 event pendaftaran user.

**b. The url of: "amqp://guest:guest@localhost:5672" is the same as in the subscriber program, what does it mean?**

Kesamaan URL "amqp://guest:guest@localhost:5672" tersebut merupakan hal yang sangat krusial dalam arsitektur berbasis *message broker*. Hal ini mengartikan bahwa program *publisher* dan program *subscriber* secara fisik maupun logis terhubung ke **instans message broker (RabbitMQ) yang sama**. Komponen `amqp` pada URL tersebut menunjukkan protokol komunikasi (*Advanced Message Queuing Protocol*) yang digunakan untuk pertukaran pesan antar layanan. Bagian `guest:guest` merepresentasikan kredensial berupa *username* dan *password* default yang digunakan untuk melakukan proses autentikasi ke dalam layanan broker. Selanjutnya, bagian `localhost:5672` menandakan bahwa server message broker tersebut sedang beroperasi secara lokal di komputer yang sama melalui port 5672. Karena *publisher* dan *subscriber* menunjuk pada alamat (URL) identik ini, saluran komunikasi data yang terintegrasi dapat terbentuk dengan baik. Dengan demikian, setiap pesan event (seperti *user_created*) yang dilepaskan (*publish*) oleh publisher akan dipastikan masuk ke antrean (queue) yang tepat dan siap diambil (*consume*) oleh subscriber.

![Running RabbitMQ as message broker.](image.png)

![Sending and processing event.](image-2.png)

![Monitoring chart based on publisher.](image-3.png)