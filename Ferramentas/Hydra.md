# Hydra

> Ferramenta de auditoria de credenciais que automatiza testes de autenticação em diversos serviços e protocolos.

## 1. Sintaxe básica

```bash
hydra [opções] IP_OU_HOST serviço
```

Exemplo genérico:

```bash
hydra -l usuario -P senhas.txt IP_OU_HOST ssh
```

**Elementos do comando:**
- `-l`: usuário único.
- `-L`: arquivo com lista de usuários.
- `-p`: senha única.
- `-P`: arquivo com lista de senhas.
- `IP_OU_HOST`: endereço do alvo autorizado.
- `serviço`: protocolo ou serviço a testar, como `ssh`, `ftp` ou `http-post-form`.

## 2. Parâmetros úteis

| Parâmetro | Função |
|---|---|
| `-t 4` | Define 4 tarefas paralelas |
| `-s 2222` | Define uma porta específica |
| `-o resultado.txt` | Salva os resultados em arquivo |
| `-V` | Exibe cada tentativa |
| `-v` | Ativa mensagens detalhadas |
| `-f` | Para após encontrar uma combinação válida para o alvo |
| `-h` | Exibe a ajuda |

## 3. Exemplos por serviço

### SSH

```bash
hydra -l usuario -P senhas.txt IP_OU_HOST ssh
```

Testa combinações de senha para um usuário em um serviço SSH acessível.

### FTP

```bash
hydra -l usuario -P senhas.txt IP_OU_HOST ftp
```

Testa combinações de senha para autenticação FTP.

### Formulário web — HTTP POST

```bash
hydra -l usuario -P senhas.txt IP_OU_HOST http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
```

- `/login`: caminho que recebe os dados do formulário.
- `username=^USER^`: campo de usuário.
- `password=^PASS^`: campo de senha.
- `F=incorrect`: texto que indica falha de autenticação.

**Atenção:** o caminho, os nomes dos campos e o critério de falha precisam corresponder ao funcionamento real da aplicação.

## 4. Como interpretar os resultados

- **Credencial encontrada:** valide o resultado no contexto autorizado e registre a evidência.
- **Nenhuma credencial encontrada:** não significa que a senha correta esteja ausente de todas as listas.
- **Erro de conexão:** confira IP, porta, serviço ativo e conectividade.
- **Resultado inconsistente:** revise a resposta do serviço e os critérios de sucesso ou falha configurados.

## 5. Como continuar

1. Identifique o serviço e a porta em uso.
2. Consulte a sintaxe específica desse serviço.
3. Verifique se o serviço está acessível e permite autenticação.
4. Registre o resultado e as evidências.
5. Em uma análise defensiva, avalie logs de autenticação, tentativas repetidas, bloqueios e mecanismos de limitação de tentativas.

## 6. Referências

- [Repositório oficial do Hydra](https://github.com/vanhauser-thc/thc-hydra)
- [TryHackMe — Hydra](https://tryhackme.com/room/hydra)

> Utilize a ferramenta somente em laboratórios ou sistemas para os quais você tenha autorização explícita.
