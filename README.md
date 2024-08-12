# Configuração e Inicialização do Projeto

## Configuração do Domínio Local no Windows

Para acessar o seu projeto usando um domínio personalizado em um ambiente local no Windows, siga os passos abaixo:

1. **Editar o arquivo `hosts`**:
   - Abra o **Bloco de Notas** como Administrador.
   - Navegue até o arquivo `hosts` localizado em `C:\Windows\System32\drivers\etc\hosts`.
   - Adicione a seguinte linha ao final do arquivo:

     ```
     127.0.0.1       fundamentos.exemplo.com.br
     ```

   - Salve o arquivo e feche o editor.

2. **Verificar a configuração**:
   - Abra o **Prompt de Comando** ou **PowerShell** e execute o seguinte comando para garantir que o domínio resolve para o IP local:

     ```bash
     ping fundamentos.exemplo.com.br
     ```

   - Você deve ver uma resposta do `127.0.0.1`.

## Estrutura do Código

A configuração do `nginx` e do Docker para este projeto é estruturada da seguinte forma:

1. **Configuração do Nginx** (`nginx/conf.d/default.conf`):
   - **Escuta nas portas 80 e 443** para HTTP e HTTPS.
   - Configura certificados SSL autoassinados.
   - Serve o conteúdo normal e exibe páginas de erro 404 e 503.
   - Permite a exibição da página de manutenção quando acessada diretamente ou em caso de manutenção programada.

2. **Dockerfile e docker-compose.yml**:
   - **Dockerfile**: Define o ambiente para o `nginx`.
   - **docker-compose.yml**: Define os serviços do `nginx`, incluindo volumes.

## Inicialização do Docker

Para inicializar o projeto utilizando Docker, siga os passos abaixo:

1. **Instalar o Docker**:
   - Certifique-se de ter o Docker e o Docker Compose instalados. Você pode baixar e instalar a partir do [site oficial do Docker](https://www.docker.com/products/docker-desktop).

2. **Construir e iniciar os containers**:
   - Navegue até o diretório onde seu arquivo `docker-compose.yml` está localizado.
   - Execute o comando para construir e iniciar os containers:

     ```bash
     docker-compose up --build
     ```

   - Este comando irá construir as imagens do Docker e iniciar os containers definidos no arquivo `docker-compose.yml`.

3. **Verificar o status dos containers**:
   - Para garantir que os containers estão em execução, execute:

     ```bash
     docker ps
     ```

   - Você deve ver os containers `nginx` e `php` em execução.

4. **Acessar o site**:
   - Abra um navegador da web e vá para `HTTPS://fundamentos.exemplo.com.br` para ver o site em execução.
   - Se a página de manutenção estiver ativa, você poderá acessá-la diretamente em `HTTPS://fundamentos.exemplo.com.br/maintenance`.

## Considerações Finais

- Certifique-se de que todos os arquivos necessários (`404.html`, `maintenance.html`, etc.) estão no diretório correto e acessíveis pelo `nginx`.
- Para alterar a configuração do `nginx`, edite o arquivo `default.conf` e reinicie os containers com `docker-compose restart nginx`.

Se você encontrar algum problema ou tiver dúvidas, verifique os logs dos containers para obter mais informações:

```bash
docker-compose logs
