# Guia-api
Estudos sobre o funcionamento de APIs, métodos HTTP e arquiteturas.
# Guia Completo sobre APIs: Métodos, Clientes e Arquiteturas (Cloud vs. LAN)

Este repositório é um estudo sobre os conceitos fundamentais de APIs, desde as ações que elas executam até onde elas operam e como interagimos com elas.

## 1. O que é uma API? A Analogia do Garçom

A forma mais fácil de entender os conceitos é com uma analogia:

Pense em uma API (Interface de Programação de Aplicações) como um **garçom digital** em um restaurante.

* **Você (ou seu software):** O cliente no restaurante.
* **O Servidor (Banco de Dados):** A cozinha que prepara os dados.
* **A API (o Garçom):** O intermediário que anota seu pedido, leva para a cozinha e traz os dados (ou "pratos") para você.
* **O JSON:** O "idioma" da comanda, que tanto você quanto a cozinha entendem.

## 2. Métodos HTTP: As Ações do Pedido

Quando você chama o garçom, você não diz apenas "comida". Você dá uma **ação** específica. Esses são os **Métodos (ou "Verbos") HTTP**.

Eles definem *o que* você quer que a API faça com os dados.

| Método | Ação (O que você diz ao garçom) | Operação (CRUD) |
| :--- | :--- | :--- |
| 🟢 **GET** | "Me **traga** o cardápio." (Apenas ler dados) | **R**ead (Ler) |
| 🟡 **POST** | "Por favor, **adicione** este novo pedido à comanda." (Criar dados) | **C**reate (Criar) |
| 🔵 **PUT** | "**Substitua** meu pedido antigo *inteiro* por este novo." (Substituir dados) | **U**pdate (Atualizar) |
| 🟣 **PATCH** | "**Mude apenas** a bebida do meu pedido." (Modificar parte dos dados) | **U**pdate (Atualizar) |
| 🔴 **DELETE** | "**Cancele** este item da minha comanda." (Apagar dados) | **D**elete (Apagar) |

---

#### Métodos Secundários (Mais Técnicos)

| Método | Ação (O que você diz ao garçom) |
| :--- | :--- |
| 🟢 **HEAD** | "O prato X está disponível?" (Pede os cabeçalhos, mas não o prato/dados. É um `GET` sem resposta.) |
| 🌸 **OPTIONS** | "O que eu posso pedir para esta mesa? (Posso adicionar, cancelar, etc.?)" (Pergunta ao servidor quais métodos são permitidos) |

## 3. Softwares que se Comunicam com APIs (Clientes de API)

Para fazer um pedido ao "garçom" (API), você precisa de um "meio de comunicação". Esse meio é um **Cliente de API**.

Existem dois tipos principais de clientes:

### A. Ferramentas de Teste e Desenvolvimento (Para Humanos)

São aplicativos gráficos que programadores usam para construir, testar e depurar APIs manualmente, antes de escrever qualquer código.

* **Postman:** O mais popular e completo. É uma plataforma inteira para todo o ciclo de vida da API.
* **Insomnia:** Um concorrente muito popular, conhecido por sua interface limpa e foco em velocidade.
* **cURL:** Uma ferramenta de linha de comando. Não é gráfica, mas é extremamente poderosa e está presente na maioria dos sistemas (Linux, macOS, Windows).
    * *Exemplo de `GET` com cURL:* `curl -X GET "https://api.exemplo.com/tarefas"`

### B. Código e Bibliotecas (Para Aplicações)

Quando seu *aplicativo* (um site, um script, um app de celular) precisa falar com uma API, ele não usa o Postman. Ele usa **bibliotecas de código** feitas para isso.

* **Em R (RStudio):** Você provavelmente usaria pacotes como `httr` ou `jsonlite`.
    * *Exemplo:* `resposta <- httr::GET("https://api.exemplo.com/dados")`
* **Em Python:** As bibliotecas `Requests` ou `HTTPX` são o padrão.
* **Em JavaScript (Web):** A função nativa `fetch()` ou a biblioteca `axios`.
* **Em IoT (Arduino/ESP):** Bibliotecas como `HTTPClient.h` para se conectar a APIs.

## 4. Onde a API "Mora"? Arquitetura Cloud vs. LAN

Agora que sabemos *o que* pedir (Métodos) e *como* pedir (Clientes), a última pergunta é: **onde o garçom trabalha?**

### ☁️ API Cloud (Web API)

O "garçom" trabalha em um restaurante na internet (na "nuvem"). Qualquer pessoa no mundo com o endereço certo e permissão pode fazer um pedido.

* **Acesso:** Global, via internet.
* **Exemplos:** API do Google Maps, API do Spotify, API do seu banco.

### 🏠 API LAN (On-Premises API)

O "garçom" trabalha na cozinha da *sua* casa (na sua rede local, ou "LAN"). Apenas pessoas que estão *dentro* da sua casa (conectadas no mesmo Wi-Fi/rede) podem fazer um pedido.

* **Acesso:** Local, apenas dentro da rede privada.
* **Exemplos:** Controlar sua Smart TV pelo celular (ambos no mesmo Wi-Fi), sensores de uma fábrica falando com um servidor central na mesma fábrica.

### Tabela Comparativa

| Característica | ☁️ API Cloud (Web API) | 🏠 API LAN (On-Premises) |
| :--- | :--- | :--- |
| **Acessibilidade** | **Global.** Acessível de qualquer lugar do mundo via internet. | **Local.** Acessível apenas por dispositivos na mesma rede privada. |
| **Performance (Latência)** | **Variável.** Depende da internet e da distância. Latência maior. | **Muito Alta.** Comunicação quase instantânea. Latência baixíssima. |
| **Segurança** | **Exposta.** Requer segurança robusta na aplicação (Tokens, Chaves de API). | **Isolada.** Protegida da internet por firewalls. O risco é interno. |
| **Dependência** | **Alta dependência da internet.** Se a internet cair, a API para. | **Independente da internet.** Funciona perfeitamente sem conexão externa. |

## 5. Juntando Tudo: O Fluxo Completo

1.  **Onde?** Você decide se sua API será **Cloud** (ex: `https://api.meusite.com`) ou **LAN** (ex: `http://192.168.1.100/api`).
2.  **O Quê?** Você define as "ações" que ela pode fazer (os Métodos HTTP: `GET /dados`, `POST /dados`, etc.).
3.  **Como?** Um **Cliente de API** (como o **Postman** para testar, ou a biblioteca `httr` no **RStudio**) é usado para enviar a requisição.
4.  **Pedido:** O cliente envia uma requisição, por exemplo: `POST` para `http://192.168.1.100/api/sensores` com um `JSON` no corpo.
5.  **Resposta:** A API (o garçom) processa o pedido e retorna uma **Resposta HTTP**.

## 6. Códigos de Resposta HTTP: A Resposta do Garçom

Quando a API responde, ela envia um **Código de Status** que resume o que aconteceu com seu pedido. Eles são agrupados em categorias:

* **`1xx` (Informativo):** "Recebi seu pedido e estou pensando..." (Raro de ver)
* **`2xx` (Sucesso):** "Tudo certo! Aqui está o que você pediu."
* **`3xx` (Redirecionamento):** "O que você quer está em outro lugar, vá para lá."
* **`4ax` (Erro do Cliente):** "Você fez o pedido errado."
* **`5xx` (Erro do Servidor):** "Eu (a API/cozinha) cometi um erro."

### Códigos Mais Importantes para Saber

| Código | Nome | O que o Garçom diz... |
| :--- | :--- | :--- |
| **`200 OK`** | **OK** | "Aqui está o cardápio que você pediu." (Resposta padrão para `GET`) |
| **`201 Created`** | **Criado** | "Seu novo pedido foi anotado com sucesso." (Resposta padrão para `POST`) |
| **`204 No Content`**| **Sem Conteúdo** | "Entendido, cancelei o item." (Resposta comum para `DELETE` bem-sucedido) |
| | | |
| **`400 Bad Request`**| **Requisição Ruim**| "Não entendi o que você escreveu na comanda." (O JSON enviado está quebrado ou faltando) |
| **`401 Unauthorized`**| **Não Autorizado** | "Quem é você? Você precisa fazer login para pedir." (Falta um Token ou Chave de API) |
| **`403 Forbidden`** | **Proibido** | "Eu sei quem você é, mas você *não tem permissão* para pedir este prato." (O usuário não tem privilégios) |
| **`404 Not Found`** | **Não Encontrado** | "Procurei em todo lugar, mas não temos o prato (endpoint) que você pediu." (A URL está errada) |
| | | |
| **`500 Internal Server Error`** | **Erro Interno do Servidor** | "Eu fui levar o pedido para a cozinha e ela explodiu! Não é sua culpa, é nossa." (Erro genérico no código da API) |
