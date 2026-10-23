# Hydra

> Ferramenta de auditoria de credenciais que automatiza testes de autenticação em serviços compatíveis.

## 1. Comando do laboratório

Exemplo utilizado no TryHackMe para testar um formulário de login HTTP em um ambiente autorizado:

```bash
hydra -l admin -P passlist.txt www.onlineshop.thm http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V
```

**Parâmetros do comando:**

| Parâmetro | Função |
|---|---|
| `-l admin` | Define um único usuário. |
| `-L users.txt` | Define uma lista de usuários. |
| `-p senha` | Define uma única senha. |
| `-P passlist.txt` | Define uma lista de senhas. |
| `-t 4` | Define quatro tarefas paralelas. |
| `-s 8080` | Define a porta do serviço. |
| `-o resultado.txt` | Salva os resultados em um arquivo. |
| `-V` | Exibe cada tentativa realizada. |
| `-v` | Ativa a saída detalhada. |
| `-f` | Interrompe após encontrar a primeira combinação válida no alvo. |
| `-h` | Exibe a ajuda da ferramenta. |

## 2. Formulários web

O módulo `http-post-form` permite testar formulários de autenticação que enviam dados por HTTP POST.

Estrutura simplificada:

```text
"/caminho:campos_do_formulario:critério_de_falha"
```

No exemplo do laboratório:

- `/login`: caminho da página de autenticação.
- `username=^USER^`: campo destinado ao usuário.
- `password=^PASS^`: campo destinado à senha.
- `F=incorrect`: identifica a mensagem que indica falha de autenticação.

O caminho, os nomes dos campos e o critério de falha precisam corresponder ao comportamento real da aplicação.

## 3. Como interpretar os resultados

- **Credencial identificada:** a ferramenta encontrou uma combinação que corresponde aos critérios configurados.
- **Nenhuma credencial encontrada:** nenhuma combinação foi identificada como válida durante o teste.
- **Erro de conexão:** verifique conectividade, resolução DNS, porta e disponibilidade do serviço.
- **Resultados inconsistentes:** confira o critério de falha, os campos do formulário e as respostas HTTP.

Uma credencial indicada pela ferramenta deve ser validada no ambiente autorizado. Uma mensagem de resposta mal interpretada pode gerar falsos positivos.

## 4. Como continuar

1. Valide o resultado de autenticação no laboratório.
2. Verifique quais recursos ficam acessíveis após o login.
3. Avalie os controles de segurança, como MFA, limitação de tentativas e bloqueio temporário.
4. Em uma análise defensiva, procure falhas de autenticação repetidas nos logs e investigue padrões suspeitos.
5. Registre o resultado, o impacto e as medidas corretivas pertinentes.

## 5. Referências

- [Documentação oficial do Hydra](https://github.com/vanhauser-thc/thc-hydra)
- [Sala Hydra — TryHackMe](https://tryhackme.com/room/hydra)

**Uso autorizado:** execute testes somente em laboratórios, sistemas próprios ou ambientes com permissão explícita.
