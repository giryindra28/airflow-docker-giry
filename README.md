# airflow-docker-giry
b. Buatlah Kubernetes YAML File untuk Deploy App disertai penjelasannya!

*sebelum menjalankan instalasi ini, pastikan udah memiliki docker dan dokcer compose di os anda, untuk windows bisa memakai docker dekstop

### Setup:
Untuk instalasi ariflow ini, versi ariflow yang diinstall adalah versi 2.2.0 dan beberapa layanan untuk mendukung airflow, yaitu:
  1. Database  (postgresql) ada dua postgresql:
      - image postgresql pertama untuk datalake
      - image postgresql kedua untuk data warehouse
  2. Setup Airflow:
      - Postgresql sebagai reponya airflow
      - Redis sebagai backend airflow untuk menyimpan konfigurasi dan status tugas, jadi antrian tugas yang nantinya dilakukan
      - Airflow webserver, scheduler, worker
      - flower untuk menyediakan tampilan web yang memudahkjan dalam memantau setiap worker yang dijalankan, progress setiap task  
      
### Running setup:
1. Jadi unntuk penginstalan, sebelumnya haruus konfigurasi kredensial di file.env, contohnya:
    AIRFLOW_UID=50000
    DB_NAME=test
    USER_NAME=giry
    USER_PASSWORD=passgiry
    AIRFLOW_CONN_POSTGRES_DATALAKE=postgresql://giry:passgiry@172.17.0.1:5433/test
    AIRFLOW_CONN_POSTGRES_DATAWAREHOUSE=postgresql://giry:passgiry@172.17.0.1:5434/test
 *harap install postgresql di lokal dulu, bisa pake dbeaver 
 
2. ubah kredensial di dalam credentials.json :
    {
        "postgres_lake": {
            "host":"172.17.0.1",
            "port":"5433",
            "database":"test",
            "username":"giry",
            "password":"passgiry"
        },
        "postgres_warehouse": {
            "host":"172.17.0.1",
            "port":"5434",
            "database":"test",
            "username":"giry",
            "password":"passgiry"
        }
    }
*sesuaikan dengan database kita di lokal 

3. buka terminal

4. jalankan perintah "dokcer-compose up" agak lama ini bisa 10 - 20 menit tergantung internet

5. kalo sudah, buka browser dan masukan localhost:8080
  *catatan kalo port 8080 sudah dipakai oleh app lain, bisa di ganti di dalam file yml

6. masukan username dan password untuk ariflow
*tertera id pass nya di docker-compose kita tadi

7. airflow telah terinstall dan siap digunakan

8. Tinggal buat ETL dan proses dag untuk airflow 

#### selesai
