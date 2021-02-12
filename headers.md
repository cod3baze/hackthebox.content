# Headers

Os cabeçalhos HTTP fornecem uma maneira adicional de passar informações entre o cliente e o servidor. Existem cabeçalhos específicos para solicitações e respostas, bem como cabeçalhos gerais comuns a ambos. Os cabeçalhos podem ter um ou vários valores anexados após o nome do cabeçalho e separados por dois pontos. Existem muitos cabeçalhos usados para diferentes fins, que são divididos em diferentes categorias:

- [x] General Headers
- [x] Entity Headers
- [x] Request Headers
- [x] Response Headers
- [x] Security Headers

1. General Headers

Esses cabeçalhos não pertencem especificamente a uma solicitação ou resposta. Eles são contextuais e são usados para descrever a mensagem em vez de seu conteúdo.

| Header       | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Date`       | O cabeçalho **Date** contém a data e a hora em que a mensagem foi originada. É preferível converter a hora para o fuso horário UTC padrão.                                                                                                                                                                                                                                                     |
| `Connection` | O cabeçalho **Connection** determina se a conexão de rede atual deve permanecer ativa após a conclusão da solicitação. Dois valores comumente usados para este cabeçalho são **close** e **keep-alive**. O valor de **fechamento** do cliente ou servidor significa que eles gostariam de encerrar a conexão, enquanto o cabeçalho **keep-aliv**e indica que a conexão deve permanecer aberta. |

General Headers - Example

```xml
lavisa@htb[/htb]$ curl -I -X GET https://www.inlanefreight.com

<SNIP>
Date: Sun, 06 Aug 2020 08:49:37 GMT
Connection: keep-alive
```

---

2 - Entity Headers

Semelhante aos cabeçalhos gerais, os cabeçalhos de entidade podem ser comuns à solicitação e à resposta. Esses cabeçalhos são usados para descrever o conteúdo (entidade) sendo transferido por uma mensagem. Eles geralmente são encontrados em respostas e solicitações POST ou PUT (por exemplo, um upload de arquivo).

| Header             | Description                                                                                                                                                                                                                                                                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Content-Type`     | Este cabeçalho é usado para descrever o **tipo de recurso** que está sendo transferido. O valor é adicionado automaticamente pelos navegadores no lado do cliente e retornado na resposta do servidor.                                                                                                                                                     |
| `Media-Type`       | O **tipo de mídia** descreve os dados que estão sendo transmitidos. Por exemplo, o tipo de mídia para um PDF é **application/pdf**, enquanto o tipo para uma imagem PNG é **image/png**. Este cabeçalho pode desempenhar um papel crucial em fazer o servidor interpretar nossa entrada. O campo **charset** denota o padrão de codificação, como _UTF-8_. |
| `Boundary`         | A diretiva de limite atua como um criador para separar o conteúdo quando há mais de um na mesma mensagem.                                                                                                                                                                                                                                                  |
| `Content-Length`   | O cabeçalho Content-Length contém o tamanho da entidade que está sendo passada. Esse cabeçalho é necessário porque o servidor o usa para ler dados do corpo da mensagem.                                                                                                                                                                                   |
| `Content-Encoding` | Os dados podem passar por várias transformações antes de serem transmitidos. Por exemplo, grandes quantidades de dados podem ser compactados para reduzir o tamanho da mensagem. O tipo de codificação usado deve ser especificado usando o cabeçalho Content-Encoding.                                                                                    |

Entity Headers - Example

```xml
lavisa@htb[/htb]$ curl -I -X GET https://www.inlanefreight.com

<SNIP>
Content-Length: 26012
Content-Type: text/html; charset=ISO-8859-4
Content-Encoding: gzip
```

---

3 - Request Headers

O _cliente_ envia cabeçalhos de solicitação em uma transação HTTP.
Eles são definidos no _RFC 2616_. Esses cabeçalhos são usados em uma
solicitação HTTP e _não estão relacionados ao conteúdo da mensagem_.
Cabeçalhos como **Accept**, **Accept-**, e **IF-** permitem solicitações condicionais.
Cabeçalhos como **Cookie** ou **User-Agent** são enviados para que o servidor possa
personalizar a resposta. Os cabeçalhos a seguir são comumente vistos em
solicitações HTTP.

| Header          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Host`          | O cabeçalho **Host** é usado para especificar o host que está sendo consultado para o recurso. Pode ser um nome de domínio ou um endereço IP. Os servidores HTTP podem ser configurados para hospedar sites diferentes, que são revelados com base no nome do host. Isso torna o cabeçalho do host um importante destino de enumeração.                                                                                                                                                                                                                                                                                                                      |
| `User-agent`    | O cabeçalho **User-Agent** é usado para descrever os recursos de solicitação do cliente. Por exemplo, um navegador ou uma biblioteca. Esse cabeçalho pode revelar muito sobre o cliente, como o navegador, sua versão e o sistema operacional.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `Accept`        | O cabeçalho _Accept_ descreve quais tipos de mídia o cliente pode entender. Ele pode conter vários tipos de mídia separados por vírgulas. O valor **`*/*`** significa todos os tipos de mídia.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `Cookie`        | O cabeçalho Cookie deve conter pares de valor de cookie no formato nome = valor. HTTP é um protocolo sem estado, o que significa que o servidor não tem como identificar os clientes que se conectam a ele. Este é um problema ao hospedar recursos e conteúdo protegidos. Um cookie é um dado armazenado no cliente e no servidor, que atua como um identificador. Estes são repassados ao servidor por solicitação, mantendo assim o acesso do cliente. Os cookies também podem servir a outros propósitos, como salvar preferências do usuário ou rastreamento de sessão. Pode haver vários cookies em um único cabeçalho, separados por ponto-e-vírgula. |
| `Referer`       | O cabeçalho _Referer_ denota de onde a solicitação atual está vindo. Por exemplo, clicar em um link dos resultados de pesquisa do Google tornaria *https://google.com* o referenciador. Confiar neste cabeçalho pode ser perigoso, pois pode ser facilmente manipulado, levando a consequências indesejadas.                                                                                                                                                                                                                                                                                                                                                 |
| `Authorization` | O cabeçalho HTTP de autorização _é outra maneira do servidor identificar os clientes_. Após a autenticação bem-sucedida, o servidor retorna um token exclusivo para o cliente. Ao contrário dos cookies, os tokens são armazenados apenas no lado do cliente e recuperados pelo servidor por solicitação. Existem vários tipos de tipos de autenticação com base no servidor da Web e no tipo de aplicativo usado.                                                                                                                                                                                                                                           |

Request Headers - Example

```xml
lavisa@htb[/htb]$ curl -I -X GET https://www.inlanefreight.com

Host: www.inlanefreight.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/605.1.15 (KHTML, like Gecko)
Cookie: cookie1=298zf09hf012fh2; cookie2=u32t4o3tb3gg4
Accept: text/plain
Referer: https://www.hackthebox.eu/
Authorization: BASIC cGFzc3dvcmQK
<SNIP>
```
