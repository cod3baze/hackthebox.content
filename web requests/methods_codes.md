# Methods and Codes

HTTP Methods

- Multiple HTTP methods can be used while accessing resources. Let's look at some of the commonly used methods.

| Method    | Description                                                                                                                                                                                                                                                                                                                                                                          |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `GET`     | Este é o método HTTP mais comum, que solicita um recurso específico. Dados adicionais podem ser passados para o servidor por meio de strings de consulta.                                                                                                                                                                                                                            |
| `POST`    | Este é outro método comum usado para enviar dados ao servidor. Ele pode lidar com vários tipos de entrada, como texto, PDFs e outras formas de dados binários. Esses dados são anexados ao corpo da solicitação presente após os cabeçalhos. O método POST é comumente usado ao enviar informações (formulários, logins) ou carregar dados para um site, como imagens ou documentos. |
| `HEAD`    | Este método solicita os cabeçalhos que seriam retornados se uma solicitação GET fosse feita ao servidor. Ele não retorna o corpo da solicitação e geralmente é feito para verificar o comprimento da resposta antes de baixar os recursos.                                                                                                                                           |
| `PUT`     | Este método é semelhante ao POST, pois é usado para criar novos recursos no servidor. Permitir esse método sem os controles adequados pode levar à adição de recursos maliciosos (ou seja, enviar um arquivo malicioso para o servidor da web).                                                                                                                                      |
| `DELETE`  | Este método permite que os usuários excluam um recurso existente no servidor da web. Isso pode levar à negação de serviço **(DoS)** sem os controles adequados no local.                                                                                                                                                                                                             |
| `OPTIONS` | Este método retorna informações sobre o servidor, como os métodos aceitos por ele.                                                                                                                                                                                                                                                                                                   |

## Response codes

- Um servidor HTTP pode retornar cinco tipos de códigos de resposta:

| CODE  | Description                                                                                                                                              |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `1xx` | Normalmente fornece informações e continua processando a solicitação.                                                                                    |
| `2xx` | Códigos de resposta positiva retornados quando uma solicitação é bem-sucedida.                                                                           |
| `3xx` | Retornado quando o servidor redireciona o cliente.                                                                                                       |
| `4xx` | Esta classe de códigos significa solicitações impróprias do cliente. Por exemplo, solicitar um recurso que não existe ou solicitar um formato incorreto. |
| `5xx` | Retornado quando há algum problema com o próprio servidor HTTP.                                                                                          |

- Let's look at some common HTTP response codes and their meaning.

| Type                        | Description                                                                                                                                                     |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `200 OK`                    | Retornado em uma solicitação bem-sucedida e a resposta geralmente contém o recurso solicitado.                                                                  |
| `302 Found`                 | Este código redireciona o cliente para outro URL. Por exemplo, redirecionar o usuário para seu painel após um login bem-sucedido.                               |
| `400 Bad Request`           | Normalmente retornado ao encontrar solicitações malformadas, como solicitações com terminadores de linha ausentes.                                              |
| `403 Forbidden`             | Este código significa que o cliente não tem acesso apropriado ao recurso. Ele também pode ser retornado quando o servidor detecta entrada maliciosa do usuário. |
| `404 Not Found`             | Retornado quando o cliente solicita um recurso que não existe no servidor.                                                                                      |
| `500 Internal Server Error` | Conforme o nome descreve, esse código é retornado quando o servidor não consegue processar a solicitação.                                                       |
