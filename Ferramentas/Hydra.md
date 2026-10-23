# Hydra

## 1. Visão geral

**Categoria:** Auditoria de credenciais e autenticação  
**Interface:** Linha de comando (CLI)  
**Principal utilização:** Testar a resistência de mecanismos de autenticação a tentativas de senhas comuns ou previsíveis.

### Para que serve?

O Hydra é uma ferramenta que automatiza tentativas de autenticação em serviços e protocolos compatíveis. Ele permite testar combinações de usuários e senhas a partir de listas de credenciais.

Entre suas aplicações estão:

- Auditoria de senhas fracas.
- Avaliação de mecanismos de autenticação.
- Testes autorizados de resistência a ataques de dicionário.
- Validação de controles como bloqueio de conta e limitação de tentativas.

**Importante:** o Hydra não descobre necessariamente uma senha por conta própria. Ele testa as credenciais fornecidas e identifica respostas que correspondam aos critérios de sucesso ou falha configurados.

## 2. Como funciona?

O Hydra recebe os dados do alvo, o método de autenticação e uma lista de credenciais. Em seguida, realiza tentativas e analisa as respostas do serviço.

Fluxo simplificado:

```text
Usuário + Lista de senhas
           |
           v
         Hydra
           |
           v
 Tentativas de autenticação
           |
           v
 Serviço de autenticação
           |
           v
 Análise das respostas
           |
           v
 Credenciais válidas ou
 resultado inconclusivo
```

### Ataque de dicionário

Um ataque de dicionário utiliza uma lista predefinida de senhas prováveis, em vez de testar todas as combinações possíveis.

Exemplo de uma lista de laboratório:

```text
abc123
123456
password
qwerty
654321
```

A ferramenta testa as entradas conforme os parâmetros definidos.

A eficácia depende da qualidade da lista, das características do serviço e dos controles de segurança existentes.

## 3. Comando utilizado no laboratório

O TryHackMe apresenta o seguinte comando para testar o formulário de login da aplicação de laboratório:

```bash
hydra -l admin -P passlist.txt www.onlineshop.thm http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V
```

Utilize esse comando somente no laboratório autorizado para o qual foi fornecido.

### Entendendo os parâmetros

| Parâmetro | Função |
|---|---|
| `hydra` | Executa a ferramenta. |
| `-l admin` | Define um único nome de usuário para as tentativas. |
| `-P passlist.txt` | Informa o arquivo que contém a lista de senhas. |
| `www.onlineshop.thm` | Define o host de destino. |
| `http-post-form` | Seleciona o módulo para testar um formulário de autenticação HTTP enviado por POST. |
| `/login` | Indica o caminho do formulário de login. |
| `username=^USER^` | Marca o campo em que a ferramenta insere o nome de usuário. |
| `password=^PASS^` | Marca o campo em que a ferramenta insere a senha testada. |
| `F=incorrect` | Define o texto que indica uma falha de autenticação na resposta. |
| `-V` | Exibe informações detalhadas sobre as tentativas. |

### Entendendo a estrutura do formulário

A parte do comando referente ao formulário segue, de forma simplificada, esta estrutura:

```text
/caminho:campos_enviados:indicador_de_falha
```

No exemplo:

- `/login` representa o caminho acessado.
- `username` e `password` são os nomes dos campos enviados ao servidor.
- `^USER^` e `^PASS^` são marcadores substituídos pelos valores testados.
- `F=incorrect` indica que a resposta contendo `incorrect` é interpretada como falha.

Esse último ponto é fundamental: o critério precisa corresponder ao comportamento real da aplicação. Se o servidor utilizar outra mensagem de erro, redirecionamentos ou respostas inconsistentes, o resultado poderá ser interpretado incorretamente.

## 4. Interpretando os resultados

Ao executar o comando, a Hydra apresenta informações sobre as tentativas realizadas e pode indicar credenciais que correspondem aos critérios configurados.

Na análise, observe:

- Se o usuário testado corresponde ao esperado.
- Se o resultado foi identificado como uma tentativa bem-sucedida.
- Se a aplicação realmente permite autenticação com a credencial identificada.
- Se existem bloqueios, limitação de tentativas ou respostas inconsistentes.

**Uma resposta identificada pela ferramenta não deve ser considerada prova definitiva sem validação.** O critério configurado pode gerar falsos positivos caso a aplicação responda de maneira inesperada.

## 5. Diferença entre Hydra e Gobuster

| Característica | Hydra | Gobuster |
|---|---|---|
| Objetivo principal | Auditar autenticação e credenciais | Enumerar caminhos e arquivos web |
| Entrada típica | Usuários e listas de senhas | Wordlist de caminhos |
| O que testa | Tentativas de autenticação | Requisições para caminhos possíveis |
| Resultado esperado | Indícios de credenciais válidas | Caminhos e recursos que merecem análise |

As ferramentas podem contribuir para etapas diferentes de uma avaliação de segurança. A descoberta de um caminho de login com o Gobuster, por exemplo, pode motivar uma avaliação autorizada dos controles de autenticação com o Hydra.

## 6. Controles defensivos relacionados

Para reduzir o risco de tentativas automatizadas de senha, considere avaliar:

- Limitação da frequência de tentativas.
- Bloqueio temporário ou controles adaptativos após falhas repetidas.
- MFA (autenticação multifator).
- Monitoramento de falhas de autenticação.
- Alertas para padrões anormais de login.
- Políticas de senhas e proteção contra senhas comuns.
- Proteção contra automação abusiva, quando aplicável.

Esses controles devem ser avaliados em conjunto. Bloquear contas indiscriminadamente, por exemplo, pode permitir ataques de negação de serviço contra usuários legítimos.

## 7. Cuidados e limitações

- Execute testes apenas em sistemas próprios, laboratórios ou ambientes com autorização explícita.
- Tentativas automatizadas podem gerar alertas, bloqueios e impacto operacional.
- O sucesso depende da configuração correta do módulo e dos critérios de resposta.
- A ausência de credenciais identificadas não comprova que o mecanismo de autenticação seja seguro.
- A ferramenta não substitui a avaliação dos controles de autenticação nem a análise de logs.

## 8. Referências

- Código-fonte e documentação: https://github.com/vanhauser-thc/thc-hydra
- Laboratório: TryHackMe — registrar o nome da sala e da tarefa estudada.
