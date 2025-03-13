# Nginx - Proxy Reverso

Fala pessoal, resolvi fazer uma configuração de um Nginx para entender como funciona na prática o proxy reverso. 

Eu me fiz o seguinte desafio: Configure um servidor Nginx para que quando for digitado o nome do site o Nginx redirecione para o servidor correto.

## 1.0 Ambiente

Para a configuração do ambiente resolvi criar dois containers com `Node.js` que apontam para uma página simples em HTML.

Os domínios são:

- vendas.paulo.com
- juridico.paulo.com

A ideia é que os mesmo domínios apontam para o mesmo endereço IP, que é meu endereço de `loopback`, o famoso 127.0.0.1.

## 2.0 Configuração do Nginx

Optei por utilizar o Nginx em um container. Mas por qual motivo? Simplismente pela facilidade de configuração e também para que caso você que esteja lendo essa documentação agora queira pegar esse projeto e executá-lo possa simular o ambiente em sua máquina local.

Você verá que o dentro do diretório `nginx` há o arquivo de configuração geral do Nginx, que é o `nginx.conf`.

### nginx.conf

No arquivo, adicionei a instrução `include /etc/nginx/conf.d/*.conf;`, que vai incluir todos os arquivos dentro do diretório `conf.d`. Dentro do diretório há os arquivos de configuração dos respestivos servidores que utlizei no projeto.

## 3.0 Subindo os Containers 

Para o projeto optei por criar um arquivo que suba os dois servidores e depois suba o Nginx.

O `compose.yaml` já faz o build das imagens de cada projeto e cria uma rede personalizada que é usada para que os containers se comuniquem.

Dentro dos diretórios `vendas, juridico` há `Dockerfiles` para que o compose chame o arquivo e os build.

## 4.0 Configurando o DNS Local

Uma coisa que eu não tinha mexido ainda era na configuração do DNS local da minha máquina, achei muito interessante.

Basicamente é bem simples. Siga o passo a passo para configurar no Linux.

1. Acesse o diretório:

```bash
cd /etc
```

2. Edite o arquivo `hosts` com o vim ou outro editor:

```bash
vim hosts
```

3. Caso esteja utilizando o vim, clique na letra `i` do seu teclado.

4. Adicione a seguinte anotação no arquivo:

```bash
127.0.0.1 vendas.paulo.com
127.0.0.1 juridico.paulo.com
```

5. Agora, clique no botão `ESC`.

6. Insira a anotação 

```bash
:wq
```

Para salvar o arquivo.

### Importante

Lembre-se de utilizar o `sudo` para fazer essa operação.

## 5.0 Executando o Projeto

Após fazer a configuração do seu DNS local, e hora de colocar a mão na massa. Siga as instruções passo a passo:

1. Faça um clone do repositório:

```bash

```

2. Acesse o repositório:

```bash

```

3. Use o comando:

```bash
docker compose up -d
```

Para subir os containers.

6. Utilize o comando:

```bash
docker ps
```

e verifique se todos os containers estão funcionando.

## 6.0 Acessando 

Com os containers todos UPs, é hora de fazer o teste. 

### vendas.paulo.com

Coloque a URL `vendas.paulo.com` no navegador e você verá que a página retornada contém o título: *Bem-vindo ao setor de Vendas*

![alt text](/images/image-1.png)

### juridico.paulo.com

Coloque agora a URL `juridico.paulo.com` no navegador e você verá que a página retornada contém o título: *Bem-vindo ao setor Jurídico*

![alt text](/images/image-2.png)

## 7.0 Conclusão

Como você pode observar não é uma coisa de outro mundo lidar com o Nginx. Ainda há muitas coisas que podem ser feitas, como por exemplo:

- Criar um load balancer e distribuir a carga atráves de diferentes containers.
- Ativar a compressão de arquivo para reduzir o número o tamanho das respostas HTTP.
- Configurar certificados SSL.

Em breve irei lançar atualizações configurando certificados SSL auto-assinados.

## Dúvidas e Sugestões?

Entre em contato comigo via:

- [Linkedin](https://www.linkedin.com/in/paulo-fabiano)
- [Email](mailto:pfabianof@gmail.com)