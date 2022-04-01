# Criando imagem docker

Nesse exemplo criaremos uma imagem usando como base a imagem do `nginx`, sobrescrevendo o conteúdo padrão do arquivo `index.html`.

### Preparação
1. Crie um arquivo com nome `Dockerfile`
2. Use o comando `FROM` para indicar a imagem base
3. Use o comando COPY para sobrescrever o conteúdo do arquivo `index.html` no caminho padrão que se encontra no nginx `/usr/share/nginx/html/index.html`

### Criando imagem

Execute o comando `build` do docker para criarmos a nova imagem

```
docker build -t USERNAME/nginx-test:latest .
```
O `.` no final, indica que o arquivo `Dockerfile` está na própria pasta onde o comando está sendo executado. 

`nginx-test` é o nome que foi dado para essa nova imagem

`USERNAME` deve ser o usuário do Dockerhub, para fazermos a publicação da imagem

Output:

```
Sending build context to Docker daemon  4.608kB
Step 1/2 : FROM nginx:latest
 ---> 12766a6745ee
Step 2/2 : COPY ./index.html /usr/share/nginx/html/index.html
 ---> b69a76394920
Successfully built b69a76394920
Successfully tagged USERNAME/nginx-test:latest
```

### Publicando imagem no dockerhub

```
docker push USERNAME/nginx-test:latest
```

Output:
```
The push refers to repository [docker.io/USERNAME/nginx-test]
959362e15eb1: Pushed 
ea4bc0cd4a93: Mounted from library/nginx 
fac199a5a1a5: Mounted from library/nginx 
5c77d760e1f4: Mounted from library/nginx 
33cf1b723f65: Mounted from library/nginx 
ea207a4854e7: Mounted from library/nginx 
608f3a074261: Mounted from library/php 
latest: digest: sha256:4a72c155396c82c4795355a85288a3412f5cc507b28ca2dc3b1e0cf918764634 size: 1777
```

**Testando imagem**
```
docker run -p 8080:80 USERNAME/nginx-test
```
Esse comando vai baixar a imagem (caso ainda não exista) no dockerhub e executar o container.

Basta acessar o endereço `http://localhost:8080` e visualizar a página que foi customizada.