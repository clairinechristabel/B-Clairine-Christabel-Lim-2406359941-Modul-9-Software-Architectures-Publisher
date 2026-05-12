# Jawaban Pertanyaan

**a. How much data your publisher program will send to the message broker in one run?**

Program publisher akan mengirimkan **5 buah pesan (data event)** ke message broker dalam satu kali eksekusi (run). Data yang dikirimkan berupa 5 objek `UserCreatedEventMessage` yang masing-masing berisi field `user_id` dan `user_name` (untuk Amir, Budi, Cica, Dira, dan Emir).

**b. The url of: "amqp://guest:guest@localhost:5672" is the same as in the subscriber program, what does it mean?**

Kesamaan URL tersebut mengartikan bahwa program *publisher* dan program *subscriber* terhubung ke **instans message broker (RabbitMQ) yang sama**. 

Message broker tersebut berjalan di komputer lokal (`localhost`) pada port `5672`, dan menggunakan kredensial default yaitu username `guest` dan password `guest`. Karena keduanya terhubung ke broker yang sama, maka pesan-pesan yang dikirimkan (publish) oleh publisher dapat diterima dan diproses secara langsung oleh subscriber.
