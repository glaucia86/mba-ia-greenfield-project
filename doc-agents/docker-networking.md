# Redes Docker (Docker Networking)

Consulte ao configurar conexões, diagnosticar comunicação ou alterar portas dos containers.

## Rede e endereços

O [compose.yaml](../nestjs-project/compose.yaml) não declara redes personalizadas; os serviços compartilham a rede padrão criada pelo Compose. Entre containers desse projeto, use o nome do serviço e a porta interna. `localhost` dentro de um container aponta para ele próprio.

| Destino | A partir de outro container do Compose | A partir da máquina local |
| --- | --- | --- |
| API | `nestjs-api:3000` | `localhost:3000` |
| PostgreSQL | `db:5432` | `localhost:5432` |
| SMTP MailHog | `mailhog:1025` | `localhost:1025` |
| Interface web MailHog | `http://mailhog:8025` | `http://localhost:8025` |

Estes endereços refletem os mapeamentos atuais. A disponibilidade depende de cada processo estar iniciado. A API precisa ser iniciada manualmente conforme [Desenvolvimento](development.md).

## Regras de configuração

- Uma API executada no container deve usar `db` como host do PostgreSQL e `mailhog` como host SMTP quando essas integrações forem implementadas.
- Se uma tarefa justificar executar a API diretamente na máquina, ela usa as portas publicadas no host; o padrão de desenvolvimento é o container.
- Em um mapeamento `5433:5432`, clientes locais usam 5433; containers continuam usando `db:5432`.
- Não fixe IPs de containers. Use resolução por nome de serviço.
- Para acessar um serviço da máquina a partir do Docker Desktop, use `host.docker.internal`; verifique suporte/configuração em outros ambientes.
- Publicar portas permite acesso pelo host. Avalie ligação a `127.0.0.1` quando o acesso deva ser exclusivamente local; o arquivo atual não restringe o endereço de publicação.

## Verificação após inicialização

Confira em `docker compose ps` os serviços solicitados; o container da API não precisa estar ativo quando apenas a infraestrutura foi solicitada. Para PostgreSQL, `docker compose exec db pg_isready -U streamtube` deve informar `accepting connections`.

Para MailHog, verifique a interface HTTP e a saudação SMTP. No Windows, execute no host:

```powershell
curl.exe --fail --max-time 5 http://localhost:8025/ -o NUL
$smtpClient = [System.Net.Sockets.TcpClient]::new()
try {
  $connection = $smtpClient.ConnectAsync('localhost', 1025)
  if (-not $connection.Wait(5000)) { throw 'Timeout na conexão SMTP' }
  $smtpClient.ReceiveTimeout = 5000
  $smtpReader = [System.IO.StreamReader]::new($smtpClient.GetStream())
  $greeting = $smtpReader.ReadLine()
  if ($greeting -notmatch '^220[ -]') { throw "Saudação SMTP inesperada: $greeting" }
  $greeting
} finally {
  $smtpClient.Dispose()
}
```

Espere sucesso HTTP e saudação SMTP 220. Em outros ambientes, use verificações equivalentes. Se um serviço ainda estiver inicializando, repita a verificação com limite de tempo e examine logs; informe falhas em vez de prosseguir como se estivesse pronto. Prontidão não comprova integração da aplicação nem autenticação no banco.

## Diagnóstico

Execute em `nestjs-project/`:

```bash
docker compose config --quiet
docker compose ps
docker compose logs --tail 100 nestjs-api db mailhog
docker compose exec db pg_isready -U streamtube
docker compose exec nestjs-api node -e "require('dns').lookup('db', console.log)"
```

A validação de configuração não comprova conectividade. Resolução DNS também não comprova autenticação ou disponibilidade da aplicação. Confira processo, host, porta e credenciais separadamente. Evite divulgar segredos presentes em logs.

`depends_on` aguarda a saúde inicial do banco; não substitui tratamento de reconexões. Não remova volumes nem recrie dados como primeira tentativa de resolver problemas de rede.
