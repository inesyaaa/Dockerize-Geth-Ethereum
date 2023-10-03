# Dockerize Geth-Ethereum Documentation

## Instaling Node

1. Pastikan server sudah terinstall docker
    Sesuaikan dengan OS yang digunakan pada server.
    - `https://docs.docker.com/engine/install/ubuntu/`

2. Buat folder "node"
    ```sh
      mkdir <nama folder yang diinginkan>
    ```
3. Buat akun baru di node Ethereum yang dijalankan dengan perangkat lunak Geth.
    ```sh
      geth --datadir <nama folder node> account new
    ```
    simpan kredential yang didapat.

4. Buatlah file bernama "password.txt" dan isi file tersebut dengan kata sandi dari akun tersebut.

5. Buat file genesis.json untuk membuat konfigurasi awal (genesis) dari blockchain Ethereum privat. 

6. Konfigurasi bootnode
    - Generate bootkey pada folder node yang telah dibuat.
    ```sh
        bootnode -genkey boot.key
    ```

    - boot.key ini kemudian dapat digunakan untuk menghasilkan bootnode sebagai berikut:
    ```sh
        bootnode -nodekey boot.key -addr :30305
    ```  
    - Simpan kredential alamat dari bootnode.
    ```sh
        enode://....................................
    ```

## Dockerize 
1. Buat Dockerfile dengan menggunakan file dan kredensial yang sudah dihasilkan sebelumnya.
2. Build images docker
    ```sh
    docker build -t <nama_image>:<tag> -f <nama file dockerfiel> .
    ```
    untuk melihat images berhasil di build
        - `docker images`

3. Buat file docker-compose.yaml untuk memudahkan dalam mengatur kontainer Docker dan layanan yang akan dijalankan.

4. Jalankan file docker-compose.yaml dengan cara:
    ```sh
    'docker compose up -d' atau 'docker-compose up -d'
    ```

5. Setelah itu lihat daftar kontainer yang berjalan
    ```sh
    docker ps
    ```

6. Lihat Log dari Kontainer yang dibuat
    ```sh
    docker logs <nama_kontainer_atau_id>
    ```

7. Menjalankan Shell di dalam Kontainer
    ```sh
    docker exec -it <id> geth attach
    ```


