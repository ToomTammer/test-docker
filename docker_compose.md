# docker-compose
1. docker-compose.yml
# command
docker-compose up -d --build

# ใช้เมื่อไม่มีการเปลี่ยนแปลงที่ docker file
docker-compose up -d

2. Next step เราจะเพิ่ม mysql และ phpmyadmin เข้ามา

# stop all service
# command
docker-compose down

# docker volume, volume ทั้งหมดและเจอชื่อ volume ที่สร้างออกมา
# command
docker volume ls

# ลบ docker volume
docker volume rm <ชื่อ volume>

# วิธีการเข้าไปสำรวจใน container (ใน container จะเป็น Linux)
# command
docker exec -it <container name> sh

# example
docker exec -it mysql sh

# ถ้าอันไหน support bash ก็ใช้ bash แทนได้
docker exec -it mysql bash

# example command line
docker exec -it db sh
sh-5.1# mysql -u root -p
Enter password:
mysql> show databases;
mysql> use <Databases name>
mysql> SELCET * from <Table name>;
