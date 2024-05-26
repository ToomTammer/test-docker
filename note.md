## Foundation ลองรัน Docker และพื้นฐาน Image / Container
# command
# ใช้สำหรับเช็ค container ที่กำลัง run อยู่ตอนนี้ได้
docker ps

## pull image มาลงเครื่อง
# command
docker pull <url docker หรือชื่อ ถ้าอยู่ใน docker hub>
# example (สำหรับ hello world)
docker pull hello-world

## run image นั้นออกมาเป็น 1 container
# command
docker run <ชื่อ image ที่จะ run>

# example (run image hello-world)
docker run hello-world

docker pull คือคำสั่งสำหรับการนำ image จาก Server ดึงมา load ไว้ใน local
หลังจาก pull แล้ว สามารถใช้คำสั่ง docker images เพื่อทำการเช็คได้ว่า ตอนนี้ image อยู่ที่เครื่องเราแล้วหรือไม่ ? (เช็คได้จากชื่อ hello-world ** ภาพของเครื่องผม คือมีหลาย images อยู่ในเครื่อง ให้สังเกตแค่ image ที่เรา pull มาก็พอ)

docker run คือคำสั่งสำหรับการ run image (ที่อยู่ในเครื่อง) ออกมาเป็น Container 1 เครื่อง

##### ลองเขียน Dockerfile เพื่อ custom module ขึ้นมา 
1. สร้าง package.json (จาก npm init) และลง package express เอาไว้ (npm install express)
2. สร้าง index.js ที่ทำการ run http server เอาไว้ และมี API 1 อันที่แสดงคำว่า hello world ออกมา
3. และที่ไฟล์นั้นจะทำการเปิด http server เอาไว้ที่ port 8000 เพื่อให้สามารถยิง localhost:8000/hello-world แล้วได้ข้อความ "hello world" ออกมาได้
4. ลองทดสอบโดยการ run node index.js

5. เมื่อเราเรียบเรียงเรียบร้อย เราจะลองมาสร้าง Dockerfile กัน

## build image
# command
docker build -t <ชื่อ image ที่ต้องการตั้ง> -f <ตำแหน่ง dockerfile> <path เริ่มต้นที่จะใช้ run docker file>

# example ที่เราจะ run
docker build -t node-server -f ./Dockerfile .
# ถ้าเกิดเป็น Dockerfile อยู่แล้ว (ไม่ใช่ชื่ออื่น) สามารถย่อเหลือเพียงแค่
docker build -t node-server .

## quit process
ทีนี้เราลอง ctrl+c ออกมาก่อน (ทำการ quit process) หากใคร quit ไม่ได้ ให้เปิด terminal (หรือ cmd ใหม่) แล้วใช้คำสั่งนี้

docker rm -f $(docker ps -a -q)

## docker run

# command
docker run -p <port ภายนอก>:<port ภายใน> <ชื่อ image>

# example สำหรับ run เคสนี้
docker run -p 8000:8000 node-server

# เพิ่ม -d เพื่อให้สามารถ run background ได้
# -d คือ การรันแบบ backgroud
docker run -d -p 8000:8000 node-server

# สำหรับ log ของ node (ที่พิมพ์คำว่า localhost)
# command
docker logs <ชื่อ container>

# example (ดูตามชื่อข้างหลังใน docker ps)
docker logs charming_ishizaka

# สามารถตั้งชื่อ Container name ได้เช่นกัน ด้วยการใส่ --name ได้
# เพิ่ม name มา
docker run -d -p 8000:8000 --name my-container node-server

# ตอน log (ดูเพิ่มเติมจากตอน docker ps ได้) ดู port ที่ รัน
docker log my-container


# docker-compose (ต่อ) docker_compose.md