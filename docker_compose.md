# docker-compose
1. docker-compose.yml
   
#docker-compose (ตัว management ของ Docker)
ราสามารถใช้ Docker รันทุกอย่างได้เลยนะ ตั้งแต่ Http server, database เช่น สมมุติเราจะสร้าง Container 3 ตัวคือ
1. node - http server (แบบเมื่อกี้)
2. mysql - database
3. phpmyadmin - หน้าจัดการ database

เราก็สามารถไล่สร้าง Dockerfile ทีละอัน และ run ทั้ง 3 ตัวมาก็ได้ ปัญหามันจะเกิดขึ้นคือ
1. ถ้า Container เยอะ เราจะเริ่มจัดการยากขึ้น
2. ยิ่งถ้ามีการ update application จะต้องคอยมา update แต่ละ image จะยิ่งจัดการยาก

มันก็เลยมี tool ตัวหนึ่ง คือตัว Composer สำหรับการควบคุม Docker container แบบทีละหลายตัวได้ คือ docker-compose ขึ้นมา

docker-compose คือเครื่องมือสำหรับจัดการ docker แบบทีละหลาย container ได้ ข้อดีของ docker-compose คือ ถ้าเกิด application เรามีการใช้ image file ร่วมกันหลายตัว มันจะเป็นตัวควบคุมทำให้ image แต่ละตัวสื่อสารกันได้ง่ายขึ้น (รวมถึงสามารถจำลองการ communication ใน production จริงได้เช่นกัน)

ซึ่งข้อดีของปัจจุบันคือ docker-compose เป็นตัว default ที่ลงมาให้กับ Docker desktop แล้วเรียบร้อย ! (ใช่ครับ เมื่อก่อนมันต้องไปหาลงเอง) ดังนั้นจึงไม่ต้องลงอะไรเพิ่มแล้ว สามารถใช้งานได้เลย

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
