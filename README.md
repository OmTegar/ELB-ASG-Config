# How to use the apps

Silahkan install node dan beberapa package yang di perlukan untuk melakukan konfigurasi.

silahkan running script berikut untuk melakukan installasi node dan bebepada package yang di perlukan lainya :
```bash
sudo apt update
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install nodejs -y
sudo apt-get install rsync build-essential git mysql-client -y
```

Run the following command as a user installation script:
```bash
cd /home/ubuntu
sudo apt install binutils -y
git clone https://github.com/aws/efs-utils
cd efs-utils
./build-deb.sh
sudo apt-get -y install ./build/amazon-efs-utils*deb
cd /home/ubuntu
mkdir efs
sudo mount -t efs -o tls fs-0ef13ba7dec46de8b:/ /home/ubuntu/efs
df -h
```
Ubah EFS ID <script> sudo mount -t efs -o tls [efs id]> efs </script> atau bisa copy paste dari EFS console. Agar EFS dapat Terkoneksi secara otomatis bisa membuka fstab di etc dengan perintah: 
```bash
sudo nano /etc/fstab
```
lalu tambahkan script berikut :
```bash
fs-0ef13ba7dec46de8b:/ /home/ubuntu/efs efs _netdev,noresvport,tls 0 0
```

kita installasi aplikasi menggunakan perintah git sebagai berikut :
```bash
cd /home/ubuntu/efs && git clone https://github.com/adinur21/ukk.git
cd ukk/ && npm install
```

Install `node_modules` on this project

```bash
  npm install --save express
  npm install -g nodemon
  npm install -g cors
  npm install -g body-parser
```

[Install node and npm](https://linuxize.com/post/how-to-install-node-js-on-ubuntu-22-04/)

[Install express](https://expressjs.com/en/starter/installing.html)

[Install nodemon](https://www.npmjs.com/package/nodemon)

[Install cors](https://www.thelinuxfaq.com/npm/npm-packages/cors#:~:text=%24%20sudo%20npm%20install%20cors%20%24%20sudo%20npm,command%20as%20below%2C%20%24%20sudo%20npm%20update%20cors)


After that, you can setup the database. go to directory model and edit `dbConnection.js`.

```bash
const db = mySql.createPool({
  host: "localhost",
  user: "root",
  password: "",
  database: "cloud_api"
})
```

Use these command to connect, create database and create table
Make sure your SQL engine is 8.0.XX
```bash
  #Install MySQL connector
  apt install mysql-client -y
  
  # connect database
  mysql -h <RDS endpoin> -u <username> -p
  
 #show database
 show databases;

 # Create the cloud_api database
 create database cloud_api;
 
  # create table
  CREATE TABLE guru (
  id_guru int(11) AUTO_INCREMENT PRIMARY KEY,
  nama_guru varchar(255),
  mapel_guru varchar(255),
  sekolah_guru varchar(255)
  );
  
  #Select table
  use cloud_api;
  
  # insert guru

  INSERT INTO guru (nama_guru, mapel_guru, sekolah_guru) VALUES ('Adi','cloud','SMK Telkom Malang');
  INSERT INTO guru (nama_guru, mapel_guru, sekolah_guru) VALUES ('OmTegar','Kuli Jawa','STM Kuli Jawa');
  
  # update guru
  UPDATE guru SET nama_guru = ?, mapel_guru = ?, sekolah_guru = ? WHERE id_guru = ?;
  
  # delete guru
  DELETE FROM guru WHERE id_guru = ?;
  
```
Run the project

```bash
  npm run start

  # use yarn
  yarn start
```

Finally test the apps with Elastic Load Balancer dns
```bash
<dns endpoint ELB>/api/guru/v1
```

# API Spec

## Get all guru

Request :

- Method : GET
- Endpoint : `/api/guru/v1`
- Header :
  - Content-Type: application/json
  - Accept: application/json

Response :

```json
{
  "guru": [
    {
      "id_guru": "number",
      "nama_guru": "string",
      "mapel_guru": "string",
      "sekolah_guru": "string"
    }
  ],
  "message": "string"
}
```

## Get guru by id

Request :

- Method : GET
- Endpoint : `/api/guru/v1/{id_guru}`
- Header :
  - Content-Type: application/json
  - Accept: application/json

Response :

```json
{
  "guru": {
    "id_guru": "number",
    "nama_guru": "string",
    "mapel_guru": "string",
    "sekolah_guru": "string"
  },
  "message": "string"
}
```

## Create guru

Request :

- Method : POST
- Endpoint : `/api/guru/v1/create`
- Header :
  - Content-Type: application/json
  - Accept: application/json
- Body :

```json
{
  "nama_guru": "string",
  "mapel_guru": "string",
  "sekolah_guru": "string"
}
```

Response :

```json
{
  "data": {
    "id_guru": "number",
    "nama_guru": "string",
    "mapel_guru": "string",
    "sekolah_guru": "string"
  },
  "message": "string"
}
```

## Update guru

Request :

- Method : PUT
- Endpoint : `/api/guru/v1/{id_guru}/update`
- Header :
  - Content-Type: application/json
  - Accept: application/json
- Body :

```json
{
  "nama_guru": "string",
  "mapel_guru": "string",
  "sekolah_guru": "string"
}
```

Response :

```json
{
  "data": {
    "id_guru": "number",
    "nama_guru": "string",
    "mapel_guru": "string",
    "sekolah_guru": "string"
  },
  "message": "string"
}
```

## Delete guru

Request :

- Method : DELETE
- Endpoint : `/api/guru/v1/{id_guru}`
- Header :
  - Content-Type: application/json
  - Accept: application/json

Response :

```json
{
  "message": "string"
}
```

## Thanks to Authors

- [@setyawannn](https://www.github.com/setyawannn)
- [@kkafi09](https://www.github.com/kkafi09)
