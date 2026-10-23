# Gobuster

> Ferramenta de enumeração web para descobrir diretórios e arquivos em servidores web.

## 1. Comando básico

```bash
gobuster dir -u http://alvo-autorizado/ -w wordlist.txt
```

- `dir`: modo de enumeração de diretórios e arquivos.
- `-u`: URL do alvo.
- `-w`: caminho da wordlist.

## 2. Parâmetros úteis

| Parâmetro | Função |
|---|---|
| `-u` | Define a URL do alvo. |
| `-w` | Define a wordlist. |
| `-t` | Define o número de threads. |
| `-x` | Define extensões de arquivos para testar, como `php,txt`. |
| `-o` | Salva os resultados em um arquivo. |
| `-h` | Exibe a ajuda da ferramenta. |

Consulte `gobuster dir --help` para conferir as opções disponíveis na versão instalada.

## 3. Como interpretar os resultados

- `200`: resposta bem-sucedida; verificar o conteúdo.
- `301/302`: redirecionamento; conferir o destino.
- `403`: acesso proibido; investigar se o recurso deveria estar restrito.
- `404`: recurso não encontrado, conforme a resposta do servidor.

Os códigos não comprovam, isoladamente, a existência de uma vulnerabilidade.

## 4. Como continuar

1. Acesse os caminhos encontrados no ambiente autorizado.
2. Verifique o conteúdo e o comportamento das páginas.
3. Investigue possíveis exposições indevidas ou falhas de controle de acesso.
4. Se encontrar uma página de login, avalie seus controles de autenticação de forma autorizada.
5. Registre os achados relevantes e descarte resultados que não se confirmarem.

## 5. Referência

Documentação oficial: https://github.com/OJ/gobuster
