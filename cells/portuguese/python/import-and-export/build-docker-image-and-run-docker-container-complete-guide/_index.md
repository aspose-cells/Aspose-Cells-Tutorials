---
category: general
date: 2026-06-21
description: Aprenda como criar uma imagem Docker e executar um contêiner Docker com
  o mapeamento de portas adequado. Inclui mapeamento de portas com docker run e exposição
  de porta no Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: pt
og_description: Crie a imagem Docker e execute o contêiner Docker com o mapeamento
  de porta correto. Domine o mapeamento de portas do docker run e exponha a porta
  no Docker em minutos.
og_title: Criar Imagem Docker e Executar Contêiner Docker – Guia Completo
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
title: Construir Imagem Docker e Executar Contêiner Docker – Guia Completo
url: /pt/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Construir Imagem Docker e Executar Contêiner Docker – Guia Completo

Já se perguntou como **build docker image** para um aplicativo web simples e depois colocá‑lo em funcionamento sem problemas? Você não está sozinho — muitos desenvolvedores enfrentam a mesma dificuldade quando começam a brincar com containerização. Neste tutorial vamos percorrer todo o processo, desde escrever um Dockerfile até expor a porta correta e, finalmente, usar `docker run` para mapear essa porta para o seu host. Ao final, você saberá exatamente como **run docker container** com mapeamento de porta adequado e entenderá por que expor uma porta no Docker é importante.

Vamos cobrir tudo o que você precisa: o comando exato `docker build`, como **docker build from Dockerfile**, as nuances de `docker run port mapping` e até um rápido teste de sanidade para garantir que o contêiner está realmente escutando onde você espera. Sem enrolação, apenas um guia prático, passo a passo, que você pode copiar‑colar no seu terminal.

## O Que Você Vai Conquistar

- Escrever um Dockerfile mínimo para um app Node.js (ou qualquer outro).  
- **Build docker image** usando a sintaxe oficial da CLI.  
- Entender a diferença entre `EXPOSE` no Dockerfile e a flag `-p` no `docker run`.  
- **Run docker container** com `docker run port mapping` para que você possa acessar o serviço em `http://localhost:5000`.  
- Diagnosticar armadilhas comuns como portas esquecidas ou portas host‑container incompatíveis.

### Pré‑requisitos

- Docker Engine instalado (Desktop ou Engine 20.10+).  
- Familiaridade básica com a linha de comando.  
- Um aplicativo web pequeno (usaremos um servidor Python Flask de uma linha, mas você pode trocar por qualquer outro).  

Se você tem isso, vamos começar.

---

## Etapa 1: Criar um Aplicativo Simples

Primeiro, precisamos de algo para containerizar. Crie uma pasta chamada `myapp` e coloque um único arquivo `app.py` dentro:

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

> **Dica:** A linha `host="0.0.0.0"` indica ao Flask para escutar em todas as interfaces, o que é necessário para que o Docker encaminhe o tráfego do host.

Agora você tem um serviço web diminuto que escuta na porta 5000 dentro do contêiner.

## Etapa 2: Escrever o Dockerfile (Docker Build from Dockerfile)

Em seguida, precisamos de um **Dockerfile** que diga ao Docker como montar a imagem. Coloque este arquivo ao lado de `app.py`:

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

Alguns pontos a observar:

- `FROM python:3.11-slim` nos fornece uma imagem base leve.  
- `EXPOSE 5000` **expose port in docker** — é uma dica para quem lê o Dockerfile, mas não abre a porta no host.  
- A linha `CMD` executa nosso servidor Flask quando o contêiner inicia.

## Etapa 3: **Build Docker Image** a partir do Dockerfile

Abra um terminal, `cd` para a pasta que contém o Dockerfile e execute:

```bash
docker build -t myflaskapp .
```

Vamos destrinchar esse comando:

- `docker build` é o verbo que **builds docker image** camadas com base nas instruções do Dockerfile.  
- `-t myflaskapp` marca a imagem resultante com um nome amigável que você pode referenciar depois.  
- O `.` final indica ao Docker que use o diretório atual como contexto de build (o local onde ele procura o Dockerfile e quaisquer arquivos que você `COPY`).

Você deverá ver uma saída semelhante a:

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

Se aparecer algum erro, verifique a sintaxe do Dockerfile e confirme que o arquivo `app.py` está na mesma pasta.

### Verificar se a Imagem Existe

Execute `docker images` e procure por `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Você verá algo como:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Parabéns — você acabou de **build docker image** com sucesso!

## Etapa 4: **Run Docker Container** com Mapeamento de Porta

Agora que a imagem está pronta, é hora de **run docker container** e tornar o app Flask acessível a partir da sua máquina host. Use a flag `-p` para fazer **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Explicação:

- O primeiro `5000` (lado esquerdo) é a **porta host**.  
- O segundo `5000` (lado direito) é a **porta do contêiner** que expusemos anteriormente.  
- O Docker encaminhará o tráfego de `localhost:5000` na sua máquina para a porta 5000 dentro do contêiner.

Você deverá ver os logs de inicialização do Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Abra um navegador e acesse `http://localhost:5000`. Você verá “Hello from Docker!” — o contêiner está servindo tráfego exatamente como esperado.

### Desacoplar o Contêiner (Opcional)

Se não quiser que o terminal fique bloqueado, adicione `-d` para rodar em segundo plano:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Você pode parar mais tarde com `docker stop <container-id>`.

## Etapa 5: Mergulho Profundo – **Expose Port in Docker** vs. **Docker Run Port Mapping**

É fácil confundir a instrução `EXPOSE` com a flag `-p`, mas elas têm propósitos diferentes:

| Conceito | O que faz | Abre a porta no host? |
|----------|-----------|-----------------------|
| `EXPOSE` (no Dockerfile) | Documenta quais portas o contêiner *pretende* escutar. | **Não** – apenas metadados. |
| `-p host:container` (docker run) | Cria uma regra NAT que encaminha o tráfego da porta host para a porta do contêiner. | **Sim** – encaminhamento real de porta. |

Se você esquecer de incluir `EXPOSE`, o comando `docker run -p` ainda funciona, mas perde a documentação útil para usuários posteriores. Por outro lado, se você apenas `EXPOSE` e nunca usar `-p`, o serviço permanece inacessível a partir do host.

### Usando `docker run` com Portas Host Diferentes

Às vezes você já tem algo escutando na porta 5000 do host. Sem problemas — basta mapear para outra porta host:

```bash
docker run -p 8080:5000 myflaskapp
```

Agora o app está acessível em `http://localhost:8080`, enquanto continua escutando na 5000 dentro do contêiner. Essa flexibilidade é um dos pontos fortes do **docker run port mapping**.

## Etapa 6: Armadilhas Comuns & Casos de Borda

| Problema | Sintoma | Solução |
|----------|----------|----------|
| Esquecer `EXPOSE` | Novos desenvolvedores não sabem qual porta mapear. | Adicione `EXPOSE 5000` (ou a porta que seu app usa). |
| Usar porta host errada | O navegador retorna “connection refused”. | Verifique se o lado esquerdo de `-p` corresponde à porta que você está tentando acessar. |
| Contêiner falha ao iniciar | Sem logs, o contêiner sai instantaneamente. | Rode `docker logs <container-id>` para ver mensagens de erro; costuma ser dependência faltante ou `CMD` incorreto. |
| Porta já em uso no host | Docker exibe “bind: address already in use”. | Escolha outra porta host (`-p 8080:5000`). |
| Não bindar em `0.0.0.0` | Serviço só acessível de dentro do contêiner. | No Flask, defina `host="0.0.0.0"`; outros frameworks têm configurações semelhantes. |

### Construindo Imagens Multi‑Stage (Avançado)

Se precisar de uma imagem final ainda menor, você pode **build docker image** com um Dockerfile multi‑stage:

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

Essa técnica remove camadas de tempo de build, resultando em uma imagem mais enxuta — ótima para produção.

## Etapa 7: Limpeza

Quando terminar de experimentar, faça a limpeza:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Limpar evita inchaço de disco e mantém seu ambiente Docker organizado.

---

## Conclusão

Agora você tem um fluxo de trabalho sólido, de ponta a ponta, para **build docker image** e **run docker container** com mapeamento de porta adequado usando **docker run port mapping**. Ao entender como **expose port in docker** funciona e como a flag `-p` realmente encaminha o tráfego, você pode containerizar qualquer serviço e torná‑lo acessível a partir do seu host ou da rede mais ampla.

Qual o próximo passo? Experimente trocar o app Flask por um binário Go, adicione variáveis de ambiente com `-e` ou envie sua imagem recém‑construída para o Docker Hub usando `docker push`. O céu é o limite, e você acabou de ganhar um novo superpoder no mundo DevOps.

Happy container


## O Que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais de API e explorar abordagens alternativas em seus próprios projetos.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}