# Primeiros passos na pratica

### Gerar imagem `docker`

- `docker build -t williamkoller/hello-golang .`

### Rodar container `docker`

- `docker run --rm -p 8080:8080 williamkoller/hello-golang`

### Subir a imagem no hub.docker

- `docker push williamkoller/hello-golang`

```bash
Using default tag: latest
The push refers to repository [docker.io/williamkoller/hello-golang]
8b683326cf31: Pushed 
1f3c2906a4cc: Pushed 
5f70bf18a086: Mounted from library/golang 
888d9d1b4435: Mounted from library/golang 
21abefad2f2c: Mounted from library/golang 
6dd5a23a5acc: Mounted from library/golang 
d4fc045c9e3a: Mounted from library/golang 
latest: digest: sha256:712d204ad12bc394812051ba9885bc74efb0b588f2a5b0bf0f8174c05b2cf5e9 size: 1782
```