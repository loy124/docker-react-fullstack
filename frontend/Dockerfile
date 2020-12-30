FROM node:alpine as builder

WORKDIR /app

COPY package.json ./

RUN npm install

COPY ./ ./

RUN npm run build

FROM nginx
EXPOSE 3000
#default.conf에서 해준 설정을 nginx컨테이너 안에 있는 설정이 되게 복사를해준다.
#현재 frontend/nginx에 있는 default.conf를 복사해준다.
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
#builder로 부터 /app/에 build파일이 생기면 /usr/share/nginx/html 파일에 복사하는 설정 
COPY --from=builder /app/build  /usr/share/nginx/html