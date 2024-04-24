# Containerize Laravel Dengan Docker Dan CI/CD Menggunakan GCP Serverless

Halo teman teman kali ini saya akan membahas topik yang cukup menarik buat saya dan baru saja saya pelajari dan mungkin teman teman butuhkan juga, tulisan ini saya buat agar bisa berkontribusi untuk programmer indonesia dan sebagai review jika suatu saat saya lupa materinya. tanpa berlama lama mari kita mulai dari pondasi di awal.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#id-4596" id="id-4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

**1.Theory**

\
**Docker** : layanan yang menyediakan kemampuan untuk mengemas dan menjalankan sebuah aplikasi dalam sebuah lingkungan terisolasi yang disebut dengan container. Dengan adanya isolasi dan keamanan yang memadai memungkinkan kamu untuk menjalankan banyak container di waktu yang bersamaan pada host tertentu.

**CI :** pengintegrasian kode ke dalam repositori kode kemudian menjalankan pengujian secara otomatis, cepat, dan sering.

**CD:** praktik yang dilakukan setelah proses CI selesai dan seluruh kode berhasil terintegrasi, sehingga aplikasi bisa dibangun lalu dirilis secara otomatis.

**GCP:** produk layanan komputasi _cloud_ yang dimiliki oleh Google. GCP mencakup infrastruktur _cloud_ publik dan G-Suite versi _enterprise_ dari Android, Chrome, dan antarmuka pemrograman aplikasi untuk pembelajaran mesin dan layanan pemetaan perusahaan.

**2.Alasan**

**Kenapa Menggunakan Docker?**

* Lingkungan Terisolasi
* Bisa Membuat Banyak Versi Aplikasi
* Bisa Mencoba Di Beberapa Envirotmen Berbeda
* dll.

**Kenapa Menggunakan CI/CD ?**

* Hype Di jaman sekarang
* Dapat menguji kode secara otomatis sebelum production
* Mempercepat deployment
* Mempermudah mendapatkan feedback dari user karena deployment juga cepa
* dll

**Kenapa Menggunakan GCP ?**

* Hype Di jaman sekarang
* Dunia Serba cloud sekarang
* Punya Akun Percobaan(alasan pribadi)
* Maintenance Mudah
* Di support lansung oleh google
* Tool yand disediakan banyak
* dll.

Praktik kali ini kita akan menggunakan laravel sebagai wadahnya untuk belajar dan kita tidak akan belajar mengenai bagaimana menginstall docker dan bagaimana menggunakan dan mendaftar gcp. jadi mungkin teman2 yang belum pernah belajar itu semua sebaikya di pelajari terlebih dahulu karena materi kali ini akan lansung pada intinya saja.

**3.Praktik Dockerize Laravel**

* Silahkan Install Laravel di situs resminya
* silahkan install docker di komputer anda
* masuk ke project laravel kamu dan buat sebuah file dengan nama `Dockerfile` di folder root
* Isikan File Seperti Di Bawah

![](<../../.gitbook/assets/image (58).png>)

Saya akan menjelaskan beberapa di bawah untuk yg tidak ada penjelasan silahkan lihat komentar di file

```docker
FROM php:7.3-cli-alpine

# envirotmen variable
ENV \
  APP_DIR="/app" \
  APP_PORT="8001"

# memindahkan file atau folder ke direktori yang di inginkan di docker
COPY . $APP_DIR
COPY .env.example $APP_DIR/.env

# menginstall kebutuhan yang ingin kita gunakan
RUN apk add --update \
    curl \
    php \
    php-opcache \
    php-openssl \
    php-pdo \
    php-json \
    php-phar \
    php-dom \
    && rm -rf /var/cache/apk/*

# menginstall composer
RUN curl -sS https://getcomposer.org/installer | php -- \
  --install-dir=/usr/bin --filename=composer

# menjalankan perintah composer
RUN cd $APP_DIR && composer update
RUN cd $APP_DIR && php artisan key:generate

# entrypoint
WORKDIR $APP_DIR
#
CMD php artisan serve --host=0.0.0.0 --port=$APP_PORT

# akses port yang dibuka
EXPOSE $APP_PORTyam
```

`From php:7.3-cli-alpine` — artinya project ini di bangun pada php 7.3.alpine

`WOKDIR` — Artinya entry point tempat kita bekerja nanti/folder tempat file dibangun

Mencoba Di Lokal Dengan Perintah

* `docker build -t laravel-docker:latest` -t=tag/nama ->perintah ini untuk membangun image di docker
* `docker run -p 8000:8001 laravel-docker:latest` -> untuk menjalankan container di docker agar bisa di coba di local
* Jika file suda running dan tidak ada masalah silahkan buka browser dan kunjungi `localhost:8000` maka project laravel akan diakses.

**4. Praktik Continius Integration dengan github**

* masih melanjutkan project yang sama
* buat sebuah folder di root dengan nama `.github/workflows`
* buat sebuah file dengan nama `laravel-github-actions.yml` di dalam folder yang telah di buat diatas _note:(nama file bisa di isi dengan sesuka hati)_
* Isi file dengan

```yaml
name: Laravel-github-action #nama pipeline bisa sesuai keinginan

on:
  push:
    branches: [ master ] # maksud dari ketiga kode diatas adalah dijalankan ketika ada push ke branch master

jobs: # pekerjaan yang akan dijalankan
  laravel-tests: # nama pekerjaan
    runs-on: ubuntu-latest # berjalan di os ubuntu
    steps: # langkah-langkah yg dijalankan
    - uses: actions/checkout@v3 # mengecekout dari github actions
    - name: Copy .env
      run: php -r "file_exists('.env') || copy('.env.example', '.env');" # mengecek apakah file .env sudah ada atau belum, jika belum maka akan menyalin file .env.example ke .env
    - name: Install Dependencies
      run: composer install -q --no-ansi --no-interaction --no-scripts --no-progress --prefer-dist # install dependensi di laravel yg diperlukan
    - name: Generate key
      run: php artisan key:generate # generate key laravel
    - name: Directory Permissions
      run: chmod -R 777 storage bootstrap/cache # mengubah permission untuk storage, bootstrap/cache
    - name: Create Database # membuat database untuk keperluan testing
      run: |
        mkdir -p database
        touch database/database.sqlite
    - name: Execute tests (Unit and Feature tests) via PHPUnit
      env:
        DB_CONNECTION: sqlite
        DB_DATABASE: database/database.sqlite
      run: vendor/bin/phpunit --testdox # menjalankan phpunit dengan testdox
   # materi ci sampai disini
   # materi cd dibawah
  deploy: # nama pekerjaan
    name: Setup Gcloud Account
    runs-on: ubuntu-latest # berjalan di os ubuntu
    env:
      IMAGE_NAME: gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} # nama image yg akan di deploy
    steps:

    - name: Login
      uses: google-github-actions/setup-gcloud@v0 # login ke gcloud
      with:
        project_id: ${{ secrets.GCP_PROJECT_ID }} # project id
        service_account_email: ${{ secrets.GCP_EMAIL }} # email service account
        service_account_key: ${{ secrets.GCP_CREDENTIALS }} # key service account

    - name: Configure Docker
      run: gcloud auth configure-docker --quiet # mengkonfigurasi docker

    - name: Checkout repository
      uses: actions/checkout@v2 # mengecekout dari github actions

    - name: Build Docker image
      run: docker build . -t gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} # membuat image dari laravel yg di deploy

    - name: Push Docker image
      run: docker push gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} # mengirim image ke gcloud

    - name: Deploy Docker image
      run: gcloud run deploy ${{ secrets.GCP_PROJECT_ID }} --image gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} --region us-central1 --platform managed --allow-unauthenticated --port 8001 # deploy image ke gcloud
ya
```

Untuk penjelasan silahkan lihat di komentar

* Buat sebuah repository dan hubungkan dengan project laravel yang sekarang
* commit dan push project kalian ke github
* kunjungi `Actions` di repo kalian

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Jika Pipeline kalian berhasil di bangun akan seperti diatas.

**5.Continius Development Dengan GCP Cloud Run Serverless**

* Mempunyai akun gcp silahkan mendaftar ke GCP nya lansung
* Menginstall Gcloud Cli [https://cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install)
* Melanjutkan File Yang Sama

Login Ke GCP Dengan Cli

`gcloud auth login` silahkan masuk dengan akun yang telah di buat sebelumnya

Membuat Project Id Dengan Cli

```
gcloud projects create nama_project_idgcloud config set project nama_project_id
```

Atau ke google console untuk buat project

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

* Enable Cloud Build Dan Container Registry

`gcloud services enable cloudbuild.googleapis.com run.googleapis.com containerregistry.googleapis.com`

Atau console

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

* Create Service Account

```
gcloud iam service-accounts create nama_akun_anda --description="Cloud Run deploy account" --display-name="Cloud-Run-Deploy"
```

Atau console

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

* Memberikan Permission Service Account

```
gcloud projects add-iam-policy-binding project_id_anda --member=serviceAccount:nama_akun_anda@project_id_anda.iam.gserviceaccount.com --role=roles/run.admingcloud projects add-iam-policy-binding project_id_anda --member=serviceAccount:nama_akun_anda@project_id_anda.iam.gserviceaccount.com --role=roles/storage.admingcloud projects add-iam-policy-binding project_id_anda --member=serviceAccount:nama_akun_anda@project_id_anda.iam.gserviceaccount.com --role=roles/iam.serviceAccountUser
```

* Membuat key di service Account

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

Klik add key. pilih json dan simpan json yang terdownload nanti

* Setelah Semua Selesai. kita repo github pilih setting dan pilih **secrets**
* pilih actions

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Buat Gcp Secret Kalian

![](<../../.gitbook/assets/image (51).png>)

`GCP_APP_NAME=nama_akun_kamu(sembarang)`

`GCP_CREDENTIALS=paste_isi_json_key_disini_yg_sudah_didownload`

`GCP_EMAIL=nama_akun@project_id.iam.gserviceaccount.com`

`GCP_PROJECT_ID=project_id_kalian`

```yaml
name: Laravel-github-action #nama pipeline bisa sesuai keinginan

on:
  push:
    branches: [ master ] # maksud dari ketiga kode diatas adalah dijalankan ketika ada push ke branch master

jobs: # pekerjaan yang akan dijalankan
  laravel-tests: # nama pekerjaan
    runs-on: ubuntu-latest # berjalan di os ubuntu
    steps: # langkah-langkah yg dijalankan
    - uses: actions/checkout@v3 # mengecekout dari github actions
    - name: Copy .env
      run: php -r "file_exists('.env') || copy('.env.example', '.env');" # mengecek apakah file .env sudah ada atau belum, jika belum maka akan menyalin file .env.example ke .env
    - name: Install Dependencies
      run: composer install -q --no-ansi --no-interaction --no-scripts --no-progress --prefer-dist # install dependensi di laravel yg diperlukan
    - name: Generate key
      run: php artisan key:generate # generate key laravel
    - name: Directory Permissions
      run: chmod -R 777 storage bootstrap/cache # mengubah permission untuk storage, bootstrap/cache
    - name: Create Database # membuat database untuk keperluan testing
      run: |
        mkdir -p database
        touch database/database.sqlite
    - name: Execute tests (Unit and Feature tests) via PHPUnit
      env:
        DB_CONNECTION: sqlite
        DB_DATABASE: database/database.sqlite
      run: vendor/bin/phpunit --testdox # menjalankan phpunit dengan testdox
   # materi ci sampai disini
   # materi cd dibawah
  deploy: # nama pekerjaan
    name: Setup Gcloud Account
    runs-on: ubuntu-latest # berjalan di os ubuntu
    env:
      IMAGE_NAME: gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} # nama image yg akan di deploy
    steps:

    - name: Login
      uses: google-github-actions/setup-gcloud@v0 # login ke gcloud
      with:
        project_id: ${{ secrets.GCP_PROJECT_ID }} # project id
        service_account_email: ${{ secrets.GCP_EMAIL }} # email service account
        service_account_key: ${{ secrets.GCP_CREDENTIALS }} # key service account

    - name: Configure Docker
      run: gcloud auth configure-docker --quiet # mengkonfigurasi docker

    - name: Checkout repository
      uses: actions/checkout@v2 # mengecekout dari github actions

    - name: Build Docker image
      run: docker build . -t gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} # membuat image dari laravel yg di deploy

    - name: Push Docker image
      run: docker push gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} # mengirim image ke gcloud

    - name: Deploy Docker image
      run: gcloud run deploy ${{ secrets.GCP_PROJECT_ID }} --image gcr.io/${{ secrets.GCP_PROJECT_ID }}/${{ secrets.GCP_APP_NAME }} --region us-central1 --platform managed --allow-unauthenticated --port 8001 # deploy image ke gcloudYa
```

* Setelah Mengatur kita kembali ke kodingan dengan menambahkan isi dari file sebelumnya `laravel-github-actions.yml` dengan

Penjelasan Ada di File

* Setelah itu commit dan push ke repository
* Lihat Ke github actions workflownya

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

* Setelah itu kunjungi google console kalian dan masuk ke **cloud run untuk melihat alamat website kalian**

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#id-4596" id="id-4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Selesai

Sekian Pembahasan Mengenai Dockerize And Ci Cd Serverles Di GCP. jika ada pertanyaan silahkan. **Salam Programmer Makassar**
