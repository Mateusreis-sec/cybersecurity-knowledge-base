# Gobuster

## 1. Visão geral

**Categoria:** Reconhecimento e enumeração web  
**Interface:** Linha de comando (CLI)  
**Linguagem:** Go  
**Principal utilização:** Descoberta de diretórios e arquivos em aplicações web.

### Para que serve?

O Gobuster é uma ferramenta de enumeração que automatiza a descoberta de caminhos em um servidor web.

Ele utiliza uma lista de palavras (*wordlist*) para testar diferentes caminhos e identificar quais retornam respostas interessantes do servidor.

Por exemplo, uma aplicação pode possuir caminhos como:

- `/admin`
- `/login`
- `/register`
- `/backup`
- `/api`

Esses caminhos podem não estar visíveis nos menus ou links públicos do site. O Gobuster permite testar automaticamente diversas possibilidades, facilitando a identificação de conteúdo que merece investigação.

**Importante:** encontrar um caminho não significa necessariamente encontrar uma vulnerabilidade. É preciso avaliar o conteúdo, as permissões de acesso e o comportamento da aplicação.

## 2. Como funciona?

O funcionamento básico pode ser resumido em quatro etapas:

1. Recebe a URL do alvo.
2. Lê as palavras de uma wordlist.
3. Envia requisições HTTP para testar os caminhos.
4. Exibe os resultados encontrados, incluindo códigos de status HTTP e outros dados disponíveis.

Exemplo conceitual:

```text
Wordlist
   |
   v
Gobuster
   |
   v
Requisições HTTP
   |
   v
Servidor Web
   |
   v
Respostas HTTP
   |
   v
Resultados para análise
```

## 3. Comando básico

```bash
gobuster dir --url http://www.onlineshop.thm/ -w /usr/share/wordlists/dirbuster/directory-list.txt
```

Esse comando utiliza o modo `dir` para testar possíveis diretórios e arquivos no endereço informado.

### Parâmetros

| Parâmetro | Função |
|---|---|
| `gobuster` | Executa a ferramenta. |
| `dir` | Seleciona o modo de enumeração de diretórios e arquivos. |
| `--url` | Define a URL do alvo. |
| `-w` | Informa o caminho da wordlist utilizada nos testes. |

### Entendendo a wordlist

Uma wordlist é um arquivo de texto contendo palavras que serão utilizadas nos testes.

Exemplo:

```text
admin
login
register
backup
uploads
```

A ferramenta combina cada palavra com a URL base para testar os caminhos correspondentes.

No comando do laboratório, a wordlist utilizada é:

```text
/usr/share/wordlists/dirbuster/directory-list.txt
```

Esse caminho depende do ambiente em que a ferramenta está sendo executada. Se o arquivo não existir, será necessário localizar outra wordlist disponível.

## 4. Interpretando os resultados

Durante a enumeração, o Gobuster pode apresentar diferentes códigos de status HTTP.

| Código | Significado | Interpretação inicial |
|---|---|---|
| `200` | OK | O servidor retornou uma resposta bem-sucedida. |
| `301` | Moved Permanently | O recurso foi redirecionado permanentemente. |
| `302` | Found | O recurso foi redirecionado temporariamente. |
| `401` | Unauthorized | É necessária autenticação ou ela não foi aceita. |
| `403` | Forbidden | O acesso foi proibido pelo servidor. |
| `404` | Not Found | O servidor informou que o recurso não foi encontrado. |
| `500` | Internal Server Error | O servidor encontrou um erro interno. |

Os códigos devem ser interpretados no contexto da aplicação. Por exemplo, um `403` pode indicar um caminho existente sem permissão de acesso, mas isso não é uma garantia universal.

Algumas aplicações também retornam páginas personalizadas ou o mesmo código HTTP para caminhos inexistentes. Por isso, os resultados precisam ser validados manualmente.

## 5. Fluxo de utilização

1. Identificar a URL autorizada para teste.
2. Selecionar uma wordlist apropriada.
3. Executar o Gobuster com os parâmetros necessários.
4. Analisar os caminhos e códigos HTTP retornados.
5. Acessar os resultados relevantes manualmente.
6. Verificar se existe exposição indevida, falha de controle de acesso ou outra condição de segurança.

## 6. Limitações e cuidados

- O resultado depende da qualidade e abrangência da wordlist.
- Respostas HTTP não comprovam, isoladamente, a existência de vulnerabilidades.
- Aplicações podem limitar requisições ou bloquear a enumeração.
- Redirecionamentos, páginas personalizadas e respostas genéricas podem gerar resultados que exigem validação.
- A enumeração pode gerar volume elevado de requisições e registros nos sistemas monitorados.

Utilizar somente em aplicações próprias, laboratórios ou ambientes para os quais exista autorização explícita.

## 7. Referências

- Documentação e código-fonte: https://github.com/OJ/gobuster
- Laboratório: TryHackMe
