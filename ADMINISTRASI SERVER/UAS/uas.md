# **Ujian Akhir Semester : Deploy 2 System Apps Static Web dan Dynamic Web**
### 1. Membuat Insteance baru pada AWS Region ap-southeast-1 Singapore
![alt text](image.png)
### 2. Membuat Folder Project UAS
![alt text](image-1.png)
### 3. Membuat Static Web menggunakan php
![alt text](image-2.png)
### 4. Membuat dynamic-app menggunakan PHP 
![alt text](image-3.png)
### 5. Install Docker dari repository resmi Docker (jalankan dipowershell)
    "sudo apt update"
    "sudo apt install -y ca-certificates curl gnupg"
    "sudo install -m 0755 -d /etc/apt/keyrings"
    "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg"
    "sudo chmod a+r /etc/apt/keyrings/docker.gpg"
    ". /etc/os-release"
    "echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download docker.com/linux/ubuntu ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/ null"
    "sudo apt update"
    "sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin"

    LALU AKTIFKAN DOCKER
    "sudo systemctl enable docker"
    "sudo systemctl start docker"
    "sudo usermod -aG docker ubuntu"

    LALU CEK APAKAH DOCKER BERHASIL DIINSTALL
    "docker --version"
    "docker compose version"
![alt text](image-4.png)
### 6. Upload Folder Project ke EC2 melalui PowerShell
    JALANKAN
    "scp -i "D:\Study Recap\uas-2388010008-key.pem" -r "D:\Study Recap\uas-cloud" ubuntu@IP PUBLIC TERBARU:~/"

    LALU JALANKAN DOCKER COMPOSE
    "cd ~/uas-cloud"
    "cp .env.example .env"
    "docker compose config"
    "docker compose up -d --build"

    LALU CEK CONTAINER
    "docker compose ps"
![alt text](image-5.png)
### 7. Set Up Docker Hub
    BUAT REPOSITORY BARU PADA DOCKER HUB
    "sahrieellnr/uas-static"
    "sahrieellnr/uas-dinamic"
![alt text](image-5.png)

    BUAT ACCESS TOKEN DOCKER HUB
    "Account Settings -> Personal access tokens -> Generate new token"
    "Permission : Read & Write"

![alt text](image-6.png)
### 8. Login Docker ke EC2 Melalui PowerShell
    "docker login -u sahrieellnr"
    (Saat diminta password, paste Docker Hub access token, bukan password akun biasa.)

    BUILD IMAGE DARI PROJECT
    Pastikan Posisi Folder di (cd ~/uas-cloud)
    lalu build "docker compose build static-cv dynamic-app"
    lalu push image ke docker hub "docker compose push static-cv dynamic-app"
![alt text](image-7.png)
### 9. Set Up Github Repository
    BUAT REPOSITORY BARU
    https://github.com/sahrieellnadzif-wq/uas-adm.git

    LALU CONNECT FOLDER PROJECT KE REPOSITORY BARU
    "git remote add origin https://github.com/sahrieellnadzif-wq/uas-adm.git

    LALU PUSH FOLDER PROJECT KE REPOSITORY
    "git add ."
    "git commit -m "Initial UAS cloud deployment project""
    "git push -u origin main"
![alt text](image-8.png)
### 10. Set Up Github Secret
    DOCKERHUB_USERNAME = sahrieellnr
    DOCKERHUB_TOKEN    = token Docker Hub kamu
    EC2_HOST           = IP public EC2 terbaru
    EC2_USER           = ubuntu
    EC2_SSH_KEY        = isi private key .pem
    STATIC_IMAGE       = sahrieell/uas-static:latest
    DYNAMIC_IMAGE      = sahrieell/uas-dinamic:latest
    MYSQL_DATABASE     = uas_db
    MYSQL_USER         = uas_user
    MYSQL_ROOT_PASSWORD = isi MYSQL_ROOT_PASSWORD dari .env
    MYSQL_PASSWORD      = isi MYSQL_PASSWORD dari .env
![alt text](image-9.png)
### 11. Set Up Github Action
    ".github/workflows/deploy-static.yml"
    ".github/workflows/deploy-dynamic.yml"

    CLONE REPOSITORY GITHUB KE EC2
    "rm -rf uas-cloud"
    "git clone https://github.com/sahrieellnadzif-wq/uas-adm.git
    "cd uas-cloud"
    "cp .env.example .env"

    COMMIT & PUSH WORKFLOW
    "git status"
    "git add .github/workflows/deploy-static.yml .github/workflows/deploy-dynamic.yml"
    "git commit -m "Add GitHub Actions deployment workflows""
    "git push origin main"
![alt text](image-10.png))
### 12. Tes Menjalankan Web Static & Dynamic
    Static
![alt text](image-11.png)

    Dynamic
![alt text](image-12.png)
