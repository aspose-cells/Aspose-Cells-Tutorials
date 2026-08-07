---
category: general
date: 2026-06-21
description: Docker 이미지 빌드와 적절한 포트 매핑으로 Docker 컨테이너를 실행하는 방법을 배웁니다. Docker run 포트
  매핑 및 Docker에서 포트 노출을 포함합니다.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: ko
og_description: 올바른 포트 매핑으로 Docker 이미지를 빌드하고 Docker 컨테이너를 실행합니다. 몇 분 만에 Docker 실행
  포트 매핑을 마스터하고 Docker에서 포트를 노출하세요.
og_title: Docker 이미지 빌드 및 Docker 컨테이너 실행 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  headline: Build Docker Image and Run Docker Container – Complete Guide
  type: TechArticle
- description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  name: Build Docker Image and Run Docker Container – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Docker Engine installed (Desktop or Engine 20.10+). - Basic familiarity
      with the command line. - A tiny web app (we’ll use a one‑line Python Flask server,
      but you can swap it for anything).'
  - name: Verify the Image Exists
    text: 'Run `docker images` and look for `myflaskapp`:'
  - name: Detaching the Container (Optional)
    text: 'If you don’t want the terminal to be blocked, add `-d` to run in the background:'
  - name: Using `docker run` with Different Host Ports
    text: 'Sometimes you might already have something listening on host port 5000.
      No problem—just map to a different host port:'
  - name: Building Multi‑Stage Images (Advanced)
    text: 'If you ever need a smaller final image, you can **build docker image**
      with a multi‑stage Dockerfile:'
  type: HowTo
tags:
- docker
- containers
- devops
title: Docker 이미지 빌드 및 Docker 컨테이너 실행 – 완전 가이드
url: /ko/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker 이미지 빌드 및 Docker 컨테이너 실행 – 완전 가이드

간단한 웹 앱을 위한 **build docker image**를 어떻게 만들고, 문제 없이 실행할 수 있는지 궁금하셨나요? 처음 컨테이너화를 시도하는 많은 개발자들이 같은 벽에 부딪히곤 합니다. 이 튜토리얼에서는 Dockerfile 작성부터 올바른 포트 노출, `docker run`을 사용해 포트를 호스트에 매핑하는 전체 과정을 단계별로 안내합니다. 마지막까지 따라오시면 **run docker container**를 올바른 포트 매핑과 함께 실행하는 방법을 정확히 알게 되고, Docker에서 포트를 노출하는 것이 왜 중요한지도 이해하게 됩니다.

필요한 모든 내용을 다룹니다: 정확한 `docker build` 명령, **docker build from Dockerfile** 방법, `docker run port mapping`의 미묘한 차이점, 그리고 컨테이너가 기대한 대로 포트를 리스닝하고 있는지 확인하는 간단한 검증까지. 불필요한 내용 없이 바로 터미널에 복사‑붙여넣기 할 수 있는 실전 가이드입니다.

## 달성 목표

- Node.js(또는 기타) 앱을 위한 최소 Dockerfile 작성하기.  
- 공식 CLI 구문을 사용해 **build docker image**하기.  
- Dockerfile의 `EXPOSE`와 `docker run`의 `-p` 플래그 차이점 이해하기.  
- `docker run port mapping`을 사용해 **run docker container**하고 `http://localhost:5000`에서 서비스에 접근하기.  
- 포트를 잊어버리거나 호스트‑컨테이너 포트가 맞지 않을 때 발생하는 일반적인 함정 진단하기.

### 사전 요구 사항

- Docker Engine 설치됨(Desktop 또는 Engine 20.10 이상).  
- 기본적인 커맨드 라인 사용 경험.  
- 작은 웹 앱(예시로 한 줄 Python Flask 서버 사용, 다른 언어로 교체 가능).  

위 조건을 만족한다면 바로 시작해봅시다.

---

## 1단계: 간단한 애플리케이션 만들기

먼저 컨테이너화할 무언가가 필요합니다. `myapp` 폴더를 만들고 그 안에 `app.py` 파일을 하나 넣으세요:

```python
# app.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

> **Pro tip:** `host="0.0.0.0"` 라인은 Flask가 모든 인터페이스에서 리스닝하도록 지정하는데, 이는 Docker가 호스트에서 트래픽을 전달하기 위해 필수입니다.

이제 컨테이너 내부에서 포트 5000을 리스닝하는 작은 웹 서비스가 준비되었습니다.

## 2단계: Dockerfile 작성 (Docker Build from Dockerfile)

다음으로 Docker가 이미지를 조립하는 방법을 알려주는 **Dockerfile**이 필요합니다. `app.py`와 같은 디렉터리에 이 파일을 두세요:

```dockerfile
# Dockerfile
FROM python:3.11-slim

# Install Flask
RUN pip install flask

# Copy our app into the image
COPY app.py /app/app.py

WORKDIR /app

# Expose the internal port (does NOT publish it yet)
EXPOSE 5000

# Default command to run the app
CMD ["python", "app.py"]
```

주의할 점 몇 가지:

- `FROM python:3.11-slim`은 가벼운 베이스 이미지를 제공합니다.  
- `EXPOSE 5000` **expose port in docker** – Dockerfile을 보는 사람에게 포트를 알려주는 힌트일 뿐, 실제로 호스트에서 포트를 열지는 않습니다.  
- `CMD` 라인은 컨테이너가 시작될 때 Flask 서버를 실행합니다.

## 3단계: Dockerfile로 **Docker 이미지 빌드**하기

터미널을 열고 Dockerfile이 있는 폴더로 `cd` 이동한 뒤 다음 명령을 실행하세요:

```bash
docker build -t myflaskapp .
```

명령을 풀어보면:

- `docker build`는 Dockerfile 지시에 따라 **build docker image** 레이어를 생성하는 동사입니다.  
- `-t myflaskapp`은 결과 이미지에 나중에 참조할 수 있는 친숙한 이름을 태그합니다.  
- 마지막 `.`은 현재 디렉터리를 빌드 컨텍스트(즉, Dockerfile과 `COPY`할 파일들을 찾는 위치)로 사용하라는 의미입니다.

다음과 비슷한 출력이 보일 것입니다:

```
Sending build context to Docker daemon  3.072kB
Step 1/6 : FROM python:3.11-slim
 ---> 3b6c0f...
Step 2/6 : RUN pip install flask
 ---> Using cache
 ---> 9e2b7a...
...
Successfully built 1c2d3e4f5g6h
Successfully tagged myflaskapp:latest
```

오류가 발생하면 Dockerfile 구문을 다시 확인하고 `app.py` 파일이 같은 폴더에 있는지 점검하세요.

### 이미지 존재 확인

`docker images`를 실행하고 `myflaskapp`을 찾아보세요:

```bash
docker images | grep myflaskapp
```

다음과 같은 결과가 나타납니다:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

축하합니다—**built docker image**를 성공적으로 완료했습니다!

## 4단계: 포트 매핑으로 **Docker 컨테이너 실행**하기

이미지가 준비되었으니 이제 **run docker container**하고 Flask 앱을 호스트 머신에서 접근 가능하도록 만들 차례입니다. `-p` 플래그를 사용해 **docker run port mapping**을 수행합니다:

```bash
docker run -p 5000:5000 myflaskapp
```

설명:

- 왼쪽 `5000`은 **호스트 포트**입니다.  
- 오른쪽 `5000`은 앞서 `EXPOSE`한 **컨테이너 포트**입니다.  
- Docker는 머신의 `localhost:5000` 트래픽을 컨테이너 내부의 포트 5000으로 전달합니다.

다음과 같은 Flask 시작 로그가 보일 것입니다:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

브라우저에서 `http://localhost:5000`에 접속하면 “Hello from Docker!”가 표시됩니다—컨테이너가 예상대로 트래픽을 제공하고 있습니다.

### 컨테이너 백그라운드 실행 (선택)

터미널이 차단되는 것을 원치 않으면 `-d` 옵션을 추가해 백그라운드에서 실행하세요:

```bash
docker run -d -p 5000:5000 myflaskapp
```

나중에 `docker stop <container-id>`로 중지할 수 있습니다.

## 5단계: **Docker에서 포트 노출** vs. **Docker Run 포트 매핑** 깊이 파헤치기

`EXPOSE` 명령과 `-p` 플래그를 혼동하기 쉽지만, 목적이 다릅니다:

| 개념 | 무엇을 수행하는가 | 호스트에서 포트를 열나요? |
|------|------------------|--------------------------|
| `EXPOSE` (Dockerfile) | 컨테이너가 **리슨**하려는 포트를 문서화합니다. | **아니오** – 메타데이터일 뿐입니다. |
| `-p host:container` (docker run) | 호스트 포트에서 컨테이너 포트로 트래픽을 전달하는 NAT 규칙을 생성합니다. | **예** – 실제 포트 포워딩이 이루어집니다. |

`EXPOSE`를 빼도 `docker run -p`는 동작하지만, 후속 사용자를 위한 문서가 사라집니다. 반대로 `EXPOSE`만 하고 `-p`를 쓰지 않으면 호스트에서 서비스에 접근할 수 없습니다.

### 다른 호스트 포트로 `docker run` 사용하기

이미 호스트 포트 5000을 사용 중일 수도 있습니다. 문제없습니다—다른 호스트 포트로 매핑하면 됩니다:

```bash
docker run -p 8080:5000 myflaskapp
```

이제 앱은 `http://localhost:8080`에서 접근 가능하고, 컨테이너 내부에서는 여전히 5000 포트를 사용합니다. 이러한 유연성이 **docker run port mapping**의 핵심 장점 중 하나입니다.

## 6단계: 흔히 마주치는 함정 및 예외 상황

| 문제 | 증상 | 해결 방법 |
|------|------|-----------|
| `EXPOSE` 누락 | 새 개발자가 어떤 포트를 매핑해야 할지 모름 | `EXPOSE 5000`(또는 앱이 사용하는 포트) 추가 |
| 잘못된 호스트 포트 사용 | 브라우저에서 “connection refused” 표시 | `-p` 왼쪽 값이 접근하려는 포트와 일치하는지 확인 |
| 컨테이너 시작 시 크래시 | 로그가 없고 컨테이너가 즉시 종료 | `docker logs <container-id>`로 오류 확인; 종종 의존성 누락이나 `CMD` 오류 |
| 호스트 포트 충돌 | Docker가 “bind: address already in use” 출력 | 다른 호스트 포트 사용 (`-p 8080:5000`) |
| `0.0.0.0` 바인딩 안 함 | 서비스가 컨테이너 내부에서만 접근 가능 | Flask에서는 `host="0.0.0.0"` 설정; 다른 프레임워크도 유사한 옵션 필요 |

### 멀티‑스테이지 이미지 빌드 (고급)

더 작은 최종 이미지를 원한다면 멀티‑스테이지 Dockerfile로 **build docker image**할 수 있습니다:

```dockerfile
# Stage 1: Build
FROM python:3.11-slim AS builder
RUN pip install --target=/app flask
COPY app.py /app/

# Stage 2: Runtime
FROM python:3.11-slim
COPY --from=builder /app /app
WORKDIR /app
EXPOSE 5000
CMD ["python", "app.py"]
```

이 기법은 빌드‑타임 레이어를 제거해 보다 가벼운 이미지를 만들며, 프로덕션에 적합합니다.

## 7단계: 정리하기

실험이 끝났다면 다음 명령으로 정리하세요:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

정리를 하면 디스크 용량이 불필요하게 차는 것을 방지하고 Docker 환경을 깔끔하게 유지할 수 있습니다.

---

## 결론

이제 **build docker image**와 **run docker container**를 올바른 **docker run port mapping**과 함께 수행하는 완전한 워크플로우를 익혔습니다. **expose port in docker**와 `-p` 플래그가 실제 트래픽을 어떻게 포워딩하는지 이해함으로써, 어떤 서비스든 컨테이너화하고 호스트 또는 외부 네트워크에서 접근 가능하게 만들 자신감을 얻었습니다.

다음 단계는? Flask 앱을 Go 바이너리로 교체하거나 `-e` 옵션으로 환경 변수를 추가하고, `docker push`로 이미지를 Docker Hub에 올려보세요. 가능성은 무한하고, 이제 DevOps 세계에서 새로운 슈퍼파워를 손에 넣었습니다.

컨테이너와 함께 즐거운 시간 보내세요


## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 배운 기술을 확장하고, 추가 API 기능을 마스터하거나 프로젝트에 적용할 수 있는 다양한 구현 방식을 탐구하도록 설계되었습니다.

- [Aspose.Cells for .NET을 사용한 Excel 이미지 렌더링 마스터: 종합 가이드](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [Aspose.Cells for .NET으로 차트에 이미지 추가하기: 단계별 가이드](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [Aspose.Cells를 사용한 .NET 워크북에 이미지 하이퍼링크 추가하기: 향상된 인터랙티브 기능](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}