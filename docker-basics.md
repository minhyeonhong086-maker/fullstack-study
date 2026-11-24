# Docker 기초

## 1. Docker란?
- 애플리케이션과 실행 환경(런타임, 라이브러리)을 **컨테이너** 로 묶어 어디서든 똑같이 실행하게 해주는 도구
- "내 컴퓨터에서는 되는데요" 문제를 줄임

## 2. 핵심 용어
| 용어 | 설명 |
|---|---|
| 이미지(Image) | 실행 환경의 설계도 (읽기 전용) |
| 컨테이너(Container) | 이미지를 실행한 인스턴스 |
| Dockerfile | 이미지를 만드는 명령서 |
| Docker Hub | 이미지 저장소 |

## 3. VM과 차이
- VM: OS 전체를 가상화 → 무겁다
- 컨테이너: 호스트 OS 커널을 공유 → 가볍고 빠르다

## 4. 기본 명령어
```bash
docker pull nginx                 # 이미지 내려받기
docker run -d -p 8080:80 nginx    # 실행 (내 8080 → 컨테이너 80)
docker ps                         # 실행 중인 컨테이너
docker stop <컨테이너ID>           # 정지
docker images                     # 이미지 목록
```

## 5. Node.js 앱 Dockerfile 예시
```dockerfile
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```
```bash
docker build -t my-app .
docker run -p 3000:3000 my-app
```
- `package.json`을 먼저 복사하면 코드만 바뀌었을 때 `npm install` 단계를 캐시로 재사용

## 6. .dockerignore
```
node_modules
.env
```

## 정리
- 이미지 = 설계도, 컨테이너 = 실행 중인 상태
- 배포·협업 환경을 통일하는 데 많이 사용된다.
