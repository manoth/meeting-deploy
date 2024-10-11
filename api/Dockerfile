FROM node:18-alpine

# ตั้งค่าไดเรกทอรีทำงานใน container
WORKDIR /home/api

# อัพเดตและติดตั้ง dependencies ที่จำเป็นในหนึ่งคำสั่งเดียว
RUN apk update && apk upgrade && apk add --no-cache \
    alpine-sdk \
    git \
    openssh \
    python3 \
    tzdata \
    build-base \
    libtool \
    autoconf \
    automake \
    gzip \
    g++ \
    make \
    screen && \
    cp /usr/share/zoneinfo/Asia/Bangkok /etc/localtime && \
    echo "Asia/Bangkok" > /etc/timezone

# ตั้งค่า environment variables
ENV PORT=3000
ENV MYSQL_TYPE=mysql
ENV MYSQL_HOST=localhost
ENV MYSQL_PORT=3306
ENV MYSQL_USER=meeting
ENV MYSQL_PASSWORD='123456'
ENV MYSQL_DATABASE=db_meeting_room
ENV MYSQL_CHARSET=utf8
ENV MYSQL_TIMEZONE=UTC
ENV SECRET_KEY=e210245736292ce42f625bc28376e44cc73e582802d85e9cbc2da55e983f

# คัดลอกโค้ดทั้งหมดไปยัง container
COPY . .

# ติดตั้ง dependencies
RUN npm i && npm install pm2 typescript -g && tsc

# เปิดพอร์ตที่ต้องการใช้งาน
EXPOSE 3000

# รันคำสั่งเพื่อเริ่มโปรเจ็กต์
CMD ["pm2-runtime", "pm2.json"]