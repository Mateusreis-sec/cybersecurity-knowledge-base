# Nmap

> Ferramenta de descoberta de hosts, varredura de portas e identificação de serviços em redes.

## 1. Sintaxe básica

```bash
nmap [opções] IP_OU_HOST
```

Exemplo básico:

```bash
nmap 192.168.1.10
```

Verifica as portas mais comuns do alvo e apresenta os resultados encontrados.

## 2. Parâmetros úteis

| Parâmetro | Função |
|---|---|
| `-sn` | Descobre hosts ativos sem realizar varredura de portas |
| `-Pn` | Trata o alvo como ativo, ignorando a descoberta inicial de hosts |
| `-p 80,443` | Analisa somente as portas 80 e 443 |
| `-p-` | Analisa as portas TCP de 1 a 65535 |
| `-sV` | Tenta identificar serviços e versões |
| `-O` | Tenta identificar o sistema operacional |
| `-sC` | Executa os scripts padrão do Nmap |
| `-T4` | Usa um perfil de temporização mais rápido |
| `-oN resultado.txt` | Salva a saída em formato de texto |
| `-oA resultado` | Salva a saída nos formatos normal, XML e grepável |
| `-v` | Aumenta o nível de detalhes exibidos |

**Observação:** `-Pn` não significa que o host está realmente ativo. Apenas faz o Nmap pular a etapa inicial de descoberta.

## 3. Exemplos por objetivo

### Descobrir hosts ativos na rede

```bash
nmap -sn 192.168.1.0/24
```

Verifica quais hosts respondem à descoberta na sub-rede indicada.

### Verificar portas específicas

```bash
nmap -p 22,80,443 192.168.1.10
```

Verifica as portas SSH, HTTP e HTTPS.

### Identificar serviços e versões

```bash
nmap -sV 192.168.1.10
```

Tenta identificar quais serviços estão disponíveis nas portas encontradas e suas versões.

### Varredura completa de portas TCP

```bash
nmap -p- 192.168.1.10
```

Verifica as portas TCP de 1 a 65535. Pode levar mais tempo do que uma varredura padrão.

### Verificação mais detalhada

```bash
nmap -sV -sC -O 192.168.1.10
```

Combina identificação de serviços e versões, scripts padrão e tentativa de identificação do sistema operacional. Pode gerar mais tráfego e levar mais tempo.

### Salvar os resultados

```bash
nmap -sV -oN resultado.txt 192.168.1.10
```

Salva os resultados em `resultado.txt` para consulta posterior.

## 4. Como interpretar os resultados

| Estado | Significado |
|---|---|
| `open` | Existe um serviço aceitando conexões naquela porta |
| `closed` | A porta respondeu, mas não há serviço escutando nela naquele momento |
| `filtered` | Um filtro ou firewall impede determinar se a porta está aberta ou fechada |
| `open\|filtered` | O Nmap não conseguiu distinguir entre aberta e filtrada |

**Exemplo:** se a porta `22/tcp` aparecer como `open` e o serviço for identificado como SSH, você terá um ponto de partida para investigar a configuração e a exposição desse serviço.

Uma porta aberta, por si só, não comprova vulnerabilidade.

## 5. Como continuar a investigação

1. Identifique as portas abertas.
2. Use `-sV` para descobrir os serviços e suas versões.
3. Pesquise vulnerabilidades relevantes para as versões identificadas, validando se as condições se aplicam ao alvo.
4. Verifique se os serviços precisam estar expostos e se estão configurados adequadamente.
5. Registre o comando, o horário, o alvo autorizado e os resultados.

### Relação com redes

- **Camada 3 — Rede:** endereços IP e alcance do host.
- **Camada 4 — Transporte:** portas TCP/UDP e estado das conexões.
- **Camada 7 — Aplicação:** identificação de serviços como HTTP, SSH e FTP.

## 6. Referências

- [Documentação oficial do Nmap](https://nmap.org/docs.html)
- [Guia de referência em português](https://nmap.org/man/pt_BR/)
- [Resumo oficial de opções](https://nmap.org/book/man-briefoptions.html)

> Utilize o Nmap somente em redes próprias, laboratórios ou sistemas para os quais você tenha autorização.
