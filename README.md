# 🛡️ Roadmap de Cibersegurança (Blue Team) - Guia de Estudos

![Nível](https://img.shields.io/badge/n%C3%ADvel-iniciante%20%2F%20est%C3%A1gio-brightgreen)
![Foco](https://img.shields.io/badge/foco-Blue%20Team-blue)
![Base](https://img.shields.io/badge/base-roadmap.sh-6366f1)
![Idioma](https://img.shields.io/badge/idioma-PT--BR-yellow)
![Status](https://img.shields.io/badge/status-em%20estudo-orange)

> Guia de estudos baseado no [roadmap de cibersegurança do roadmap.sh](https://roadmap.sh/cyber-security).
> A ideia aqui é simples: pegar **todos** os conceitos do roadmap e explicar de um jeito fácil, do zero, com exemplos reais de comando e configuração. Feito pra quem está começando (estágio / júnior) e quer entender o "porquê" de cada coisa, não só decorar.

---

## 📌 Como usar este guia

- Leia de cima pra baixo na primeira vez. A ordem segue uma linha lógica de aprendizado: fundamentos de TI, sistemas, redes, depois segurança de verdade.
- Cada conceito tem três partes: **o que é**, **por que importa pro Blue Team** e um **exemplo real** (comando, config ou cenário).
- Os exemplos de comando foram pensados pra você rodar numa máquina virtual de laboratório, nunca em produção ou em rede que não seja sua.
- Marque o que você já domina e volte nos tópicos que ainda são novidade.

> ⚠️ **Aviso de laboratório:** varredura de rede, captura de pacote e teste de exploração só em ambiente autorizado (sua própria VM, laboratórios do TryHackMe/HackTheBox, etc). Fazer isso em rede de terceiros sem permissão é crime.

---

## 📚 Índice

1. [Fundamentos de TI](#1-fundamentos-de-ti)
2. [Sistemas Operacionais](#2-sistemas-operacionais)
3. [Virtualização](#3-virtualização)
4. [Conhecimento de Redes](#4-conhecimento-de-redes)
5. [Protocolos de Rede](#5-protocolos-de-rede)
6. [Ferramentas de Troubleshooting](#6-ferramentas-de-troubleshooting)
7. [Métodos de Autenticação](#7-métodos-de-autenticação)
8. [Conhecimento de Segurança (o coração do roadmap)](#8-conhecimento-de-segurança)
9. [Criptografia](#9-criptografia)
10. [Frameworks de Segurança](#10-frameworks-de-segurança)
11. [Tipos de Ataque](#11-tipos-de-ataque)
12. [Ataques Comuns](#12-ataques-comuns)
13. [Malware](#13-malware)
14. [Ferramentas de Resposta a Incidentes e Forense](#14-ferramentas-de-resposta-a-incidentes-e-forense)
15. [Logs](#15-logs)
16. [Conceitos de Hardening](#16-conceitos-de-hardening)
17. [Protocolos Seguros vs Inseguros](#17-protocolos-seguros-vs-inseguros)
18. [Termos de Defesa (AV, EDR, IDS, DLP...)](#18-termos-de-defesa)
19. [Processo de Resposta a Incidentes](#19-processo-de-resposta-a-incidentes)
20. [SIEM e SOAR](#20-siem-e-soar)
21. [Padrões e Compliance](#21-padrões-e-compliance)
22. [Cloud](#22-cloud)
23. [Programação](#23-programação)
24. [Certificações](#24-certificações)
25. [CTFs e Prática](#25-ctfs-e-prática)
26. [Próximos Passos](#26-próximos-passos)

---

## 1. Fundamentos de TI

Antes de "hackear" ou "defender" qualquer coisa, você precisa entender como um computador e uma rede funcionam. Essa é a base.

### Componentes de Hardware
As peças físicas do computador. Saber o básico ajuda a entender ataques de baixo nível e forense.
- **CPU:** o cérebro, executa as instruções.
- **RAM:** memória temporária. Importante pra forense, porque malware muitas vezes vive só na RAM (fileless malware). Por isso a gente coleta "dump de memória".
- **Disco (HD/SSD):** onde os dados ficam guardados. É de onde se tira imagem forense.
- **Placa de rede (NIC):** conecta na rede, tem o endereço MAC.

### Tipos de Conexão
Formas de dois aparelhos trocarem dados sem cabo. Cada uma tem seu alcance e seus riscos.
- **WiFi:** rede sem fio local. Risco: redes abertas, Evil Twin (ponto de acesso falso).
- **Bluetooth:** curta distância. Risco: pareamento com aparelho malicioso.
- **NFC:** pertinho (poucos centímetros). Usado em pagamento por aproximação.
- **Infravermelho (Infrared):** antigo, linha de visão direta.

### Troubleshooting Independente de SO
Resolver problema olhando a lógica, não decorando tela. "Está sem internet" pode ser cabo, placa de rede, DNS, firewall. Você testa camada por camada: o cabo está conectado? A placa tem IP? Consigo pingar o gateway? Consigo resolver um nome? Esse raciocínio vale em Windows, Linux ou Mac.

### Suítes Populares
Ferramentas de produtividade que toda empresa usa. Como Blue Team, você vai investigar logs de uso delas.
- **MS Office / Microsoft 365:** o mais comum em empresa. Fonte enorme de phishing (anexos .docx com macro).
- **Google Workspace (Suite):** e-mail, drive, docs na nuvem do Google.
- **iCloud:** nuvem da Apple.

### Noções de Rede
Como as máquinas conversam. É tão importante que tem uma seção inteira só pra isso mais abaixo.

---

## 2. Sistemas Operacionais

O roadmap pede pra você aprender **Windows, Linux e MacOS**. Pro Blue Team, Windows e Linux são os mais importantes (servidores e estações rodam eles).

Pra cada SO, estude estes pontos:

| Tópico | O que entender |
|---|---|
| Instalação e Configuração | Como subir o SO do zero |
| Versões e Diferenças | Windows 10 vs 11, Server; Ubuntu vs CentOS vs Kali |
| Navegar por GUI e CLI | Fazer as coisas pela interface **e** pela linha de comando |
| Permissões | Quem pode ler, escrever e executar o quê |
| Instalar Software | `apt`, `yum`, winget, loja |
| CRUD em Arquivos | Criar, Ler, Atualizar e Deletar arquivos |
| Troubleshooting | Resolver problemas do sistema |
| Comandos Comuns | O dia a dia no terminal |

### Exemplo real - Permissões no Linux
No Linux, cada arquivo tem dono, grupo e "outros", com permissões de leitura (r), escrita (w) e execução (x).

```bash
# Ver as permissões de um arquivo
ls -l relatorio.txt
# -rw-r--r-- 1 cesar analistas 1024 nov 11 23:00 relatorio.txt
#  │└┬┘└┬┘└┬┘
#  │ │  │  └── outros: só leitura (r--)
#  │ │  └───── grupo "analistas": só leitura (r--)
#  │ └──────── dono "cesar": leitura e escrita (rw-)
#  └────────── tipo de arquivo (- = arquivo comum)

# Dar permissão de execução só pro dono
chmod u+x script.sh

# Deixar um arquivo com rwx pro dono, rx pro grupo, nada pros outros
chmod 750 script.sh
```

Por que isso importa: ataque muito comum é um arquivo com permissão aberta demais (ex: `777`, todo mundo pode mexer). Hardening = fechar essas permissões.

### Exemplo real - Permissões no Windows
No Windows a gente usa `icacls` pra ver e ajustar permissões (ACLs).

```powershell
# Ver permissões de uma pasta
icacls "C:\dados\financeiro"

# Remover acesso do grupo "Todos"
icacls "C:\dados\financeiro" /remove:g "Todos"
```

---

## 3. Virtualização

Virtualização é rodar vários "computadores" (máquinas virtuais) dentro de um só computador físico. É a base de laboratório de segurança e de toda a nuvem.

### Conceitos chave
- **Host OS:** o sistema do computador físico (sua máquina real).
- **Guest OS:** o sistema que roda dentro da máquina virtual (ex: um Kali Linux virtual).
- **Hypervisor:** o programa que cria e gerencia as VMs. Dois tipos:
  - **Tipo 1 (bare metal):** roda direto no hardware. Ex: VMware ESXi, Proxmox. Usado em servidor.
  - **Tipo 2 (hosted):** roda em cima do seu SO normal. Ex: VirtualBox, VMware Workstation. Usado no notebook.
- **VM (Máquina Virtual):** o computador virtual em si.

### Tecnologias comuns
- **VirtualBox:** grátis, ótimo pra começar laboratório em casa.
- **VMware (Workstation/ESXi):** muito usado em empresa.
- **Proxmox:** plataforma open source de virtualização de servidor.

### Exemplo real - montando um lab
A forma mais comum de estudar segurança: no seu notebook (Host = Windows), instale o VirtualBox (Hypervisor tipo 2) e crie duas VMs:
1. Um **Kali Linux** (máquina de ataque / análise).
2. Um **Windows ou Metasploitable** (máquina alvo vulnerável).

Coloque as duas na mesma rede interna isolada ("Host-only" ou "Internal Network") pra elas se enxergarem sem tocar na internet. Pronto, laboratório seguro pra praticar.

---

## 4. Conhecimento de Redes

Essa é a parte mais pesada do roadmap e a mais importante pra Blue Team. Quase toda investigação de incidente passa por entender rede.

### Modelo OSI
É um "mapa" de 7 camadas que explica como um dado sai de um app e chega em outro computador. Decorar ajuda a investigar: você sempre pergunta "em qual camada está o problema?".

| Camada | Nome | Exemplo | Ataque típico |
|---|---|---|---|
| 7 | Aplicação | HTTP, DNS, SMTP | SQL Injection, XSS |
| 6 | Apresentação | SSL/TLS, criptografia | Downgrade de TLS |
| 5 | Sessão | Controle de conexão | Sequestro de sessão |
| 4 | Transporte | TCP, UDP (portas) | SYN flood |
| 3 | Rede | IP, roteamento | IP spoofing |
| 2 | Enlace | MAC, switch, ARP | ARP spoofing, VLAN hopping |
| 1 | Física | Cabo, WiFi | Grampear cabo |

Macete pra decorar (de 1 a 7): "**P**ode **E**nviar **R**ede **T**ranquila **S**em **A**traso **A**lgum" (Física, Enlace, Rede, Transporte, Sessão, Apresentação, Aplicação).

### Protocolos comuns e portas
Porta é como um "apartamento" dentro do endereço IP (o prédio). Cada serviço escuta numa porta. Blue Team precisa saber as portas na ponta da língua pra ler log de firewall.

| Serviço | Porta | Pra que serve |
|---|---|---|
| FTP | 21 | Transferir arquivo (inseguro) |
| SSH / SFTP | 22 | Acesso remoto seguro (Linux) |
| Telnet | 23 | Acesso remoto (inseguro, evite) |
| SMTP | 25 | Enviar e-mail |
| DNS | 53 | Resolver nome em IP |
| HTTP | 80 | Site sem criptografia |
| HTTPS | 443 | Site com criptografia |
| RDP | 3389 | Acesso remoto (Windows) |
| SMB | 445 | Compartilhamento de arquivo Windows |
| LDAP | 389 | Consulta ao Active Directory |
| Kerberos | 88 | Autenticação no AD |

> 💡 Portas 3389 (RDP) e 445 (SMB) abertas pra internet são clássicas de ransomware. Fique de olho nisso em log.

### Subnetting (sub-redes) e CIDR
Subnetting é dividir uma rede grande em pedaços menores. CIDR é a notação com a "/" que diz quantos bits são da rede.

- `192.168.1.0/24` significa: os 24 primeiros bits são a rede. Sobram 8 bits pra hosts, ou seja, 256 endereços (de `192.168.1.0` a `192.168.1.255`).
- `/24` = máscara `255.255.255.0`.
- `/16` = rede bem maior (`172.16.0.0/16`, 65 mil endereços).

Por que importa: quando você vê um alerta de um IP, saber a sub-rede diz se ele é da rede interna de servidores, da rede de usuários, da DMZ, etc.

### IP Público vs Privado
- **Privado:** usado só dentro da rede da empresa/casa. Não navega direto na internet. Faixas: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.
- **Público:** único no mundo, visível na internet.
- O **NAT** (veja abaixo) é o que traduz um pro outro.

### Terminologia de IP
- **localhost / loopback (`127.0.0.1`):** o próprio computador falando com ele mesmo. Útil pra testar serviço local.
- **subnet mask (máscara):** define onde termina a rede e começa o host (ex: `255.255.255.0`).
- **default gateway:** o "portão de saída" da rede, normalmente o roteador. É pra onde o tráfego vai quando o destino está fora da sua rede.

### Terminologia de Rede (a decorar)
- **VLAN:** rede virtual que separa tráfego dentro do mesmo switch (ex: VLAN de visitantes separada da VLAN financeiro).
- **DMZ:** "zona desmilitarizada", uma rede no meio do caminho onde ficam servidores expostos pra internet (ex: site), separados da rede interna. Se o servidor for invadido, o atacante não cai direto na rede interna.
- **ARP:** protocolo que descobre o MAC a partir do IP dentro da rede local.
- **DHCP:** entrega IP automático pros aparelhos.
- **DNS:** traduz nome (`google.com`) em IP (`142.250.x.x`).
- **NAT:** traduz os IPs privados da rede num IP público só pra sair na internet.
- **Router (roteador):** liga redes diferentes e escolhe o caminho dos pacotes.
- **Switch:** liga aparelhos da mesma rede local.
- **VPN:** cria um "túnel" criptografado por cima da internet, como se você estivesse na rede da empresa de casa.

### Tamanhos de rede
- **LAN:** rede local (seu escritório).
- **WLAN:** LAN sem fio (WiFi).
- **MAN:** rede metropolitana (uma cidade).
- **WAN:** rede ampla (liga cidades/países; a internet é a maior WAN).

### Funções de serviços de infra
- **DHCP:** distribui IPs.
- **DNS:** resolve nomes.
- **NTP:** sincroniza o relógio de todas as máquinas. **Crítico pra segurança:** se os relógios estão errados, a correlação de logs no SIEM fica toda bagunçada e o certificado TLS pode quebrar.
- **IPAM:** ferramenta pra gerenciar e documentar quais IPs estão em uso.

### Topologias de rede
Como os aparelhos estão fisicamente/logicamente ligados.
- **Estrela (Star):** todos ligados num ponto central (switch). A mais comum hoje.
- **Anel (Ring):** cada um ligado ao próximo em círculo.
- **Malha (Mesh):** todos ligados em todos. Redundante, caro.
- **Barramento (Bus):** todos num cabo só. Antigo.

### NAS e SAN
Formas de armazenamento em rede.
- **NAS:** um "HD de rede" que vários computadores acessam por arquivos. Simples.
- **SAN:** rede dedicada de armazenamento de alta performance, usada em datacenter.

---

## 5. Protocolos de Rede

Protocolo é a "língua" que dois sistemas combinam pra conversar. Saber qual é seguro e qual não é faz parte do trabalho de Blue Team.

- **SSH (22):** acesso remoto a servidor Linux com criptografia. Substitui o Telnet.
- **RDP (3389):** área de trabalho remota do Windows.
- **FTP (21):** transfere arquivo, mas **sem criptografia** (senha vai em texto puro). Evite.
- **SFTP (22):** FTP por cima do SSH, criptografado. Use este.
- **HTTP (80):** web sem criptografia.
- **HTTPS (443):** web com criptografia (SSL/TLS).
- **SSL/TLS:** a camada de criptografia que protege HTTPS, e-mail, VPN. SSL é o nome antigo; hoje o certo é **TLS** (1.2 e 1.3).

### Exemplo real - SSH
```bash
# Conectar num servidor Linux por SSH
ssh cesar@192.168.1.50

# Conectar numa porta diferente da padrão
ssh cesar@192.168.1.50 -p 2222
```
Por que o Blue Team se importa: várias tentativas de SSH falhando no log (`Failed password`) é sinal clássico de ataque de força bruta.

---

## 6. Ferramentas de Troubleshooting

Essas são as ferramentas de linha de comando que você mais vai usar pra diagnosticar rede. São as mesmas que atacantes usam pra "mapear" e que você usa pra investigar.

### Categorias
- **Packet Sniffers (farejadores de pacote):** capturam o tráfego cru da rede. Ex: Wireshark, tcpdump.
- **Port Scanners (escaneadores de porta):** descobrem quais portas/serviços estão abertos. Ex: nmap.
- **Protocol Analyzers (analisadores de protocolo):** interpretam o que os pacotes significam. Ex: Wireshark.

### As ferramentas uma por uma

**`ping`** - testa se um host está vivo e qual a latência.
```bash
ping 8.8.8.8
```

**`ipconfig` (Windows) / `ip` ou `ifconfig` (Linux)** - mostra a configuração de rede da sua máquina.
```bash
ipconfig /all          # Windows: mostra IP, MAC, DNS, gateway
ip addr                # Linux moderno
```

**`nslookup` / `dig`** - consultam o DNS (nome para IP).
```bash
nslookup google.com
dig google.com +short   # dig é mais detalhado, padrão em Linux
```

**`tracert` (Windows) / `traceroute` (Linux)** - mostra o caminho (saltos) até um destino.
```bash
tracert google.com
```

**`netstat`** - mostra conexões de rede ativas e portas em escuta. Ótimo pra achar malware "chamando pra casa".
```bash
netstat -ano             # Windows: conexões + PID do processo
netstat -tulpn           # Linux: portas em escuta
```

**`arp`** - mostra a tabela que liga IP a MAC na rede local. Útil pra detectar ARP spoofing.
```bash
arp -a
```

**`route`** - mostra/edita a tabela de rotas (pra onde o tráfego vai).
```bash
route print              # Windows
ip route                 # Linux
```

**`nmap`** - o escaneador de rede mais famoso. Descobre hosts, portas e serviços.
```bash
# Varredura rápida das portas mais comuns de um host (só no SEU lab)
nmap 192.168.1.50

# Descobrir versão dos serviços
nmap -sV 192.168.1.50

# Descobrir hosts vivos numa sub-rede
nmap -sn 192.168.1.0/24
```

**`tcpdump`** - captura pacotes pela linha de comando (quando não dá pra abrir o Wireshark).
```bash
# Capturar tráfego da porta 80 e salvar num arquivo pra analisar depois
tcpdump -i eth0 port 80 -w captura.pcap
```

**`iptables`** - firewall do Linux por linha de comando.
```bash
# Bloquear todo tráfego vindo de um IP malicioso
iptables -A INPUT -s 203.0.113.10 -j DROP
```

---

## 7. Métodos de Autenticação

Autenticação é **provar que você é quem diz ser**. Aqui entram os protocolos que você citou que quer entender melhor (LDAP e amigos). Vou dar atenção especial pra eles.

### CIA, só pra situar: Autenticação vs Autorização
- **Autenticação:** "quem é você?" (login e senha, token).
- **Autorização:** "o que você pode fazer?" (permissões depois de logado).

### LDAP
**O que é:** LDAP (Lightweight Directory Access Protocol) é o protocolo usado pra **consultar e autenticar** num serviço de diretório. O exemplo mais famoso de diretório é o **Active Directory (AD)** da Microsoft. Pense no AD como uma "agenda telefônica gigante" da empresa: usuários, grupos, computadores, impressoras. O LDAP é a língua que você usa pra perguntar coisas pra essa agenda.

- Roda na **porta 389** (texto puro) ou **636** (LDAPS, criptografado com TLS, que é o certo).
- A estrutura é hierárquica, em árvore, com nomes tipo `cn=Cesar Neto,ou=SOC,dc=empresa,dc=com,dc=br`:
  - `cn` = common name (nome do objeto)
  - `ou` = organizational unit (departamento/setor)
  - `dc` = domain component (partes do domínio)

**Como o AD usa o LDAP na prática:** quando você loga no computador da empresa, a máquina pergunta ao Domain Controller (servidor do AD) "esse usuário e senha estão certos?" usando LDAP (e Kerberos). Quando um app precisa saber "o Cesar está no grupo de administradores?", ele faz uma consulta LDAP.

**Exemplo real - consulta LDAP por linha de comando:**
```bash
# A partir de um Linux, consultando um AD
# Busca o usuário "cesar" dentro do domínio empresa.com.br
ldapsearch -x -H ldap://10.0.0.10 \
  -D "cesar@empresa.com.br" -W \
  -b "dc=empresa,dc=com,dc=br" \
  "(sAMAccountName=cesar)"

# -x  = autenticação simples
# -H  = endereço do servidor LDAP (o Domain Controller)
# -D  = o usuário que vai se autenticar (bind)
# -W  = vai pedir a senha
# -b  = base da busca (onde começar a procurar na árvore)
# o último argumento é o filtro: "ache quem tem o login cesar"
```

No Windows/PowerShell, a mesma ideia com o módulo de AD:
```powershell
# Buscar um usuário no AD
Get-ADUser -Filter "SamAccountName -eq 'cesar'" -Properties MemberOf

# Ver quem está no grupo de administradores do domínio
Get-ADGroupMember "Domain Admins"
```

**Por que o Blue Team se importa com LDAP:** ataques como *LDAP enumeration* (atacante mapeando todos os usuários e grupos), *Kerberoasting* e abuso de contas privilegiadas passam por aqui. Monitorar consultas LDAP estranhas e logins no AD é pão com manteiga de SOC. E sempre prefira **LDAPS (636)** em vez de LDAP (389) pra senha não trafegar em texto puro.

### Kerberos
**O que é:** o protocolo de autenticação padrão do Active Directory (porta 88). Funciona com "tickets". Em vez de mandar a senha toda hora, você pega um ticket (TGT) de um servidor central (KDC) e usa esse ticket pra acessar os serviços. É mais seguro porque a senha não fica indo e voltando.

- Ataques famosos: **Kerberoasting** (roubar ticket de serviço pra quebrar a senha offline) e **Pass-the-Ticket**.

### RADIUS
**O que é:** protocolo que centraliza autenticação de acesso à rede. Muito usado em WiFi corporativo e VPN. Quando você conecta no WiFi da empresa com seu usuário, quem valida você é um servidor RADIUS por trás.

### SSO (Single Sign-On)
**O que é:** logar uma vez e acessar vários sistemas sem digitar senha de novo. Ex: você loga no Google e já entra no Gmail, Drive, YouTube. Em empresa, usa protocolos como SAML e OAuth. Bom pra usabilidade, mas se a conta de SSO cai, o atacante acessa tudo de uma vez (por isso MFA é obrigatório aqui).

### Certificados
**O que é:** arquivos digitais que provam identidade usando criptografia (parte da PKI, veja a seção de criptografia). O cadeado do HTTPS é um certificado dizendo "este site é mesmo o banco X".

### Autenticação Local
**O que é:** usuário e senha guardados na própria máquina, não num servidor central. Ex: a conta de administrador local do Windows. Risco: se a mesma senha de admin local está em todas as máquinas, o atacante compromete uma e passa pra todas (por isso existe o LAPS, que gera senha diferente em cada máquina).

---

## 8. Conhecimento de Segurança

Aqui começa o "miolo" do roadmap. São os conceitos que todo analista de segurança precisa ter na cabeça.

### Tríade CIA
A base de tudo em segurança. Três objetivos:
- **Confidencialidade (Confidentiality):** só quem pode ver, vê. (criptografia, permissões)
- **Integridade (Integrity):** o dado não foi alterado sem autorização. (hash, assinatura)
- **Disponibilidade (Availability):** o sistema está no ar quando precisa. (backup, redundância, anti-DDoS)
Todo ataque fere pelo menos um desses. Ransomware, por exemplo, fere confidencialidade (vazam os dados) e disponibilidade (criptografam tudo).

### Defesa em Profundidade (Defense in Depth)
Não confiar numa só camada de proteção. Você empilha várias: firewall + antivírus + EDR + MFA + treino de usuário + backup. Se uma falha, a próxima segura. Como as muralhas e o fosso de um castelo.

### Zero Trust
Filosofia moderna: **"nunca confie, sempre verifique"**. Antigamente, quem estava dentro da rede era considerado confiável. No Zero Trust, cada acesso é verificado, mesmo de quem já está dentro. Nada é confiável por padrão.

### Times Blue / Red / Purple
- 🔵 **Blue Team:** defesa. Monitora, detecta, responde a incidentes. **É o seu time.**
- 🔴 **Red Team:** ataque simulado. Testa as defesas agindo como um inimigo real.
- 🟣 **Purple Team:** junta os dois. O Red ataca, o Blue defende, e eles trocam informação pra melhorar juntos.

### Falso/Verdadeiro Positivo e Negativo
Conceito que você vive no dia a dia de SOC analisando alerta:
- **Verdadeiro Positivo (True Positive):** o alerta disparou e **era** ameaça de verdade. (acertou)
- **Falso Positivo (False Positive):** o alerta disparou mas **não** era nada. (alarme falso, o que mais incomoda)
- **Verdadeiro Negativo (True Negative):** não disparou e realmente não tinha ameaça. (tudo certo)
- **Falso Negativo (False Negative):** **não** disparou mas **tinha** ameaça. (o pior de todos, passou batido)
O trabalho de afinar o SIEM é reduzir falso positivo (ruído) sem aumentar falso negativo (cegueira).

### Cyber Kill Chain
Modelo da Lockheed Martin que descreve as 7 fases de um ataque. Entender ajuda a saber "em que ponto o atacante está" e onde cortar.
1. **Reconhecimento:** atacante pesquisa o alvo.
2. **Armamento (Weaponization):** monta a arma (ex: PDF com exploit).
3. **Entrega (Delivery):** manda (ex: e-mail de phishing).
4. **Exploração (Exploitation):** a vulnerabilidade é explorada.
5. **Instalação:** instala o malware/backdoor.
6. **Comando e Controle (C2):** o malware conversa com o atacante.
7. **Ações no Objetivo:** rouba dados, criptografa, etc.
Quanto mais cedo você corta a corrente, menor o estrago.

### Threat Hunting
Caça proativa a ameaças. Em vez de esperar o alerta tocar, você parte da hipótese "e se tiver um atacante escondido?" e vai procurar nos logs sinais que passaram despercebidos. É um nível acima da triagem reativa.

### Threat Intel e OSINT
- **Threat Intelligence:** informação sobre ameaças (IPs maliciosos, hashes de malware, grupos de ataque). Alimenta suas defesas com "o que está rolando lá fora".
- **OSINT (Open Source Intelligence):** coletar informação de fontes públicas (redes sociais, sites, vazamentos). Atacante usa pra te mapear; defensor usa pra investigar e pra monitorar a marca da empresa.

### Gestão de Vulnerabilidades
Processo contínuo de **achar, priorizar e corrigir** falhas. Ferramentas (Nessus, Qualys, OpenVAS) escaneiam e geram uma nota (CVSS, de 0 a 10). Você prioriza as críticas e as que já estão sendo exploradas no mundo real (lista KEV da CISA).

### Honeypots
Uma "isca": um sistema falso de propósito, feito pra atrair atacante. Como ninguém legítimo deveria tocar nele, qualquer acesso é suspeito e gera alerta valioso.

### IDS e IPS
- **IDS (Intrusion Detection System):** **detecta** e alerta sobre atividade maliciosa. Só avisa.
- **IPS (Intrusion Prevention System):** detecta **e bloqueia** na hora.
Pense: IDS é câmera de segurança (grava e avisa), IPS é a porta que tranca sozinha.

### Hardening de SO
Deixar o sistema mais "duro" de invadir: desligar serviços que não usa, fechar portas, remover software desnecessário, aplicar senha forte, atualizar. Menos coisa ligada = menos porta de entrada (menor superfície de ataque).

### Isolamento
Separar sistemas pra que um problema num não contamine os outros. Ex: isolar na rede uma máquina infectada pra o malware não se espalhar (a famosa "contenção").

### Escalonamento de Privilégio (Privilege Escalation)
Quando o atacante entra como usuário comum e consegue virar administrador/root. É um dos passos mais importantes de um ataque. Dois tipos:
- **Vertical:** usuário comum vira admin.
- **Horizontal:** acessa a conta de outro usuário do mesmo nível.

### Runbooks (e Playbooks)
Receita de bolo escrita do que fazer numa situação específica. Ex: "Runbook de phishing: passo 1, isolar; passo 2, bloquear remetente; passo 3, procurar quem clicou...". Garante que todo mundo responde do mesmo jeito, mesmo sob pressão.

### Backups e Resiliência
Cópia dos dados pra recuperar depois de desastre ou ransomware. Regra de ouro **3-2-1:** 3 cópias, em 2 mídias diferentes, 1 fora do local (offsite). E teste o restore. Backup que nunca foi testado não é backup, é esperança.

### Definição de Risco
**Risco = Ameaça x Vulnerabilidade x Impacto.** É a chance de algo ruim acontecer vezes o estrago que causaria. Segurança não é "proteger tudo igual", é priorizar onde o risco é maior.

### Compliance e Auditores
- **Compliance:** cumprir regras e normas (PCI-DSS pra cartão, LGPD pra dados pessoais, ISO 27001).
- **Auditor:** quem verifica se a empresa está mesmo cumprindo. Você vai preparar evidências pra eles.

### Perímetro vs DMZ vs Segmentação
- **Perímetro:** a "borda" da rede, onde fica o firewall de entrada.
- **DMZ:** zona intermediária pros servidores expostos à internet (já explicado em redes).
- **Segmentação:** dividir a rede interna em pedaços isolados pra um invasor não andar livre. (ex: rede de servidores separada da rede de usuários).

### Pentest - Regras de Engajamento
Antes de um teste de invasão, se define por escrito: o que pode ser testado, quando, até onde ir, e o que **não** pode. Protege as duas partes legalmente. Sem autorização por escrito, pentest é crime.

### Forense (básico)
Investigar o que aconteceu depois de um incidente, preservando as evidências de forma que valham juridicamente. Conceito central: **cadeia de custódia** (registro de quem tocou na evidência, quando e como), e trabalhar sempre numa **cópia** da evidência, nunca no original.

### Engenharia Reversa (básico)
Pegar um programa (ex: um malware) e desmontar pra entender o que ele faz, sem ter o código-fonte. Usa ferramentas como Ghidra e IDA. Serve pra criar detecção contra aquele malware.

### Ferramentas de Hacking e Exploit Frameworks
Pra se defender, entenda o que o atacante usa:
- **Metasploit:** o framework de exploração mais famoso. Tem módulos prontos pra explorar falhas conhecidas.
- **Burp Suite:** teste de aplicação web.
- **Cobalt Strike:** ferramenta de "red team" muito abusada por criminosos reais em ataques de ransomware (saber a assinatura dele é ouro pro Blue Team).

### Handshakes
É o "aperto de mão" inicial de uma conexão, onde os dois lados combinam as regras.
- **TCP 3-way handshake:** SYN, SYN-ACK, ACK. Antes de qualquer dado, o cliente e o servidor fazem esses 3 passos. Entender isso explica ataques como SYN flood.
- **TLS handshake:** onde cliente e servidor combinam a criptografia e trocam certificados antes de proteger a conexão.

### Ataques Web e OWASP Top 10
O **OWASP Top 10** é a lista das 10 falhas web mais críticas, atualizada de tempos em tempos. Vale conhecer pelo nome: Broken Access Control, Injection (SQLi), Cryptographic Failures, Insecure Design, Security Misconfiguration, etc. É a referência mundial de segurança de aplicação web.

---

## 9. Criptografia

Criptografia é a matemática que protege os dados. Você não precisa ser matemático, mas precisa entender os conceitos.

### Hashing (Hash)
Transforma qualquer dado numa "impressão digital" de tamanho fixo. É **mão única**: dá pra gerar o hash, mas não dá pra voltar ao original. Serve pra verificar integridade e guardar senha.
- Mesma entrada = sempre o mesmo hash. Mudou 1 letra = hash totalmente diferente.
- Algoritmos: MD5 e SHA-1 (quebrados, evite), **SHA-256** (atual).

```bash
# Gerar o hash SHA-256 de um arquivo pra conferir se ele foi alterado
sha256sum instalador.exe
# e51a... (se bater com o hash oficial, o arquivo é íntegro)
```
Uso em Blue Team: você pega o hash de um arquivo suspeito e joga no VirusTotal pra ver se é malware conhecido.

### Salting (Sal)
Um valor aleatório adicionado à senha antes de gerar o hash. Assim, duas pessoas com a mesma senha têm hashes diferentes, e o atacante não consegue usar tabelas prontas (rainbow tables) pra quebrar.

### Chave Pública vs Privada (criptografia assimétrica)
Cada pessoa tem um par de chaves:
- **Chave pública:** pode compartilhar com todo mundo.
- **Chave privada:** só sua, secreta.
O que uma chave fecha, só a outra abre. Dois usos:
- **Sigilo:** alguém criptografa com sua chave **pública**, só você abre com a **privada**.
- **Assinatura:** você assina com sua chave **privada**, todos verificam com a **pública** (prova que foi você).
É assim que HTTPS, SSH e e-mail assinado funcionam.

### Troca de Chaves (Key Exchange)
O problema: como dois lados combinam uma chave secreta por um canal que pode estar sendo espionado? A solução (ex: algoritmo Diffie-Hellman) permite combinar um segredo em comum sem nunca mandar o segredo pela rede. É o que acontece no handshake do TLS.

### PKI (Public Key Infrastructure)
Toda a estrutura que gerencia certificados digitais: quem emite, quem valida, quem revoga. No centro está a **CA (Autoridade Certificadora)**, uma entidade confiável que assina os certificados. Quando seu navegador confia no cadeado de um site, é porque confia na CA que assinou aquele certificado.

### Ofuscação (Obfuscation)
Embaralhar/esconder dados ou código pra dificultar a leitura. Importante: ofuscação **não é** criptografia (não é seguro de verdade, só dificulta). Atacantes ofuscam malware pra escapar do antivírus; você precisa saber "desofuscar" scripts suspeitos.

---

## 10. Frameworks de Segurança

Frameworks são "modelos mentais" pra organizar e entender ataques. Três que o roadmap pede:

### MITRE ATT&CK
O mais importante hoje. É uma enciclopédia gigante de **táticas e técnicas** reais de atacantes, organizadas por fase. Cada técnica tem um código (ex: `T1566` = Phishing). No SOC você mapeia seus alertas pra ATT&CK pra saber "o que o atacante estava tentando fazer" e onde estão seus pontos cegos de detecção.
- Site: [attack.mitre.org](https://attack.mitre.org)

### Cyber Kill Chain
Já explicada acima. É mais linear (7 fases do começo ao fim de um ataque).

### Diamond Model
Modelo que analisa um ataque por 4 vértices de um diamante: **Adversário** (quem), **Capacidade** (com que ferramenta/malware), **Infraestrutura** (de onde, qual servidor C2) e **Vítima** (quem foi atingido). Ajuda a conectar ataques do mesmo grupo.

> 💡 Resumo prático: **Kill Chain** = as fases do ataque. **ATT&CK** = o catálogo de como cada passo é feito. **Diamond** = como relacionar os atores de um ataque.

---

## 11. Tipos de Ataque

Aqui estão os ataques, principalmente os de **engenharia social** (enganar pessoas). A maioria dos incidentes começa com um humano clicando em algo.

### Engenharia Social
O "hack da mente": manipular pessoas pra elas entregarem acesso ou informação. É a origem da maioria dos ataques porque é mais fácil enganar gente do que quebrar criptografia.

### Família do Phishing
- **Phishing:** e-mail falso em massa pra roubar senha/dado ("seu banco pede pra atualizar a conta").
- **Spear Phishing:** phishing direcionado a uma pessoa específica, com detalhes dela.
- **Whaling:** phishing mirando "peixe grande" (CEO, diretor).
- **Vishing (Whishing):** golpe por **voz** (ligação telefônica).
- **Smishing:** golpe por **SMS**.

### Spam vs Spim
- **Spam:** mensagem em massa indesejada por e-mail.
- **Spim:** o mesmo, mas por mensageiro instantâneo (Teams, WhatsApp, etc).

### Ataques físicos / presenciais
- **Shoulder Surfing:** espiar sua tela/senha por cima do ombro.
- **Dumpster Diving:** vasculhar o lixo da empresa atrás de documento sensível.
- **Tailgating:** entrar na área restrita "colado" numa pessoa autorizada (sem crachá).
- **Impersonation (Impersonação):** se passar por outra pessoa (ex: fingir ser o suporte de TI).

### Ataques baseados em engano técnico
- **Watering Hole:** infectar um site que a vítima costuma visitar, esperando ela cair.
- **Drive-by:** o site infecta seu computador só por você visitar, sem clicar em nada.
- **Typo Squatting:** registrar domínios parecidos com erros de digitação (`gooogle.com`) pra pegar quem digita errado.

### Ataques de senha
- **Brute Force (força bruta):** testar milhares de senhas numa conta até acertar.
- **Password Spray:** o contrário esperto: testar **uma** senha comum (ex: `Senha@2026`) em **muitas** contas. Evita travar as contas e passa despercebido. Muito comum, fique de olho.

### Zero Day
Falha que ninguém conhece ainda (nem o fabricante), então **não tem correção**. Ataque de zero day é perigoso porque não existe patch pra se proteger na hora.

---

## 12. Ataques Comuns

Ataques mais "técnicos", contra sistemas e redes.

| Ataque | O que é (simples) |
|---|---|
| **DoS** | Sobrecarregar um serviço pra derrubá-lo, a partir de uma fonte |
| **DDoS** | O mesmo, mas de **milhares** de fontes ao mesmo tempo (botnet) |
| **MITM (Man-in-the-Middle)** | Atacante se põe no meio da conversa e lê/altera tudo |
| **Spoofing** | Falsificar identidade (IP, MAC, e-mail, DNS) pra se passar por outro |
| **ARP Spoofing** | Envenenar a tabela ARP da rede local pra fazer MITM |
| **DNS Poisoning** | Corromper respostas de DNS pra te mandar pro site falso |
| **SQL Injection (SQLi)** | Injetar comando SQL num campo de site pra roubar/alterar o banco |
| **XSS (Cross-Site Scripting)** | Injetar script malicioso numa página pra rodar no navegador da vítima |
| **CSRF** | Fazer o navegador logado da vítima executar uma ação sem ela querer |
| **Directory Traversal** | Usar `../../` pra sair da pasta do site e ler arquivos do servidor |
| **Buffer Overflow** | Estourar a memória de um programa pra executar código do atacante |
| **Memory Leak** | Programa que não libera memória; pode causar queda (disponibilidade) |
| **Replay Attack** | Capturar um dado válido (ex: token) e reenviar depois pra se autenticar |
| **Pass the Hash** | Usar o **hash** da senha roubado (sem saber a senha) pra logar como a vítima |

### Ataques de WiFi
- **Evil Twin:** ponto de acesso WiFi falso com o mesmo nome do real, pra você conectar nele.
- **Rogue Access Point:** um AP não autorizado plugado na rede da empresa (porta dos fundos).
- **Deauth Attack:** forçar a desconexão de um aparelho do WiFi (pra fazer ele reconectar no Evil Twin).
- **VLAN Hopping:** "pular" de uma VLAN pra outra que deveria estar isolada.

### Exemplo real - SQL Injection (pra reconhecer, não pra atacar)
Um campo de login inseguro monta a consulta assim:
```sql
SELECT * FROM usuarios WHERE login = 'cesar' AND senha = '12345';
```
Se o atacante digita no campo senha: `' OR '1'='1`, a consulta vira:
```sql
SELECT * FROM usuarios WHERE login = 'cesar' AND senha = '' OR '1'='1';
```
Como `'1'='1'` é sempre verdadeiro, ele loga sem saber a senha. A defesa é usar *prepared statements* (consultas parametrizadas). Em log de WAF, você reconhece tentativa de SQLi por padrões como `' OR 1=1`, `UNION SELECT`, `--`.

---

## 13. Malware

Malware é qualquer software malicioso. Conhecer os tipos ajuda a classificar um incidente.

- **Vírus:** se anexa a um arquivo e se espalha quando o arquivo roda.
- **Worm:** se espalha sozinho pela rede, sem precisar de interação humana (ex: WannaCry).
- **Trojan (Cavalo de Troia):** se disfarça de programa legítimo pra você instalar.
- **Ransomware:** criptografa seus arquivos e pede resgate. O terror das empresas hoje.
- **Spyware:** espiona o que você faz.
- **Keylogger:** grava tudo que você digita (senhas inclusive).
- **Rootkit:** se esconde fundo no sistema pra não ser detectado e manter acesso.
- **Botnet:** rede de máquinas infectadas controladas pelo atacante (usada em DDoS).
- **Fileless Malware:** vive só na memória (RAM), sem gravar arquivo no disco, pra escapar do antivírus.
- **Adware:** empurra propaganda; chato, às vezes perigoso.

### Como o malware age (ciclo geral)
Entrega (phishing) → Execução → Persistência (garante que volta ao reiniciar) → Escalonamento de privilégio → Comunicação com C2 → Objetivo (roubar/criptografar). Esse ciclo é o que você reconstrói numa investigação.

### Exemplo real - checando um arquivo suspeito
```bash
# 1. Gerar o hash do arquivo
sha256sum arquivo_suspeito.exe

# 2. Pegar esse hash e pesquisar no VirusTotal (site), SEM subir o arquivo
#    se for confidencial. Se muitos antivírus apontam malware, confirmado.
```

---

## 14. Ferramentas de Resposta a Incidentes e Forense

Quando um incidente acontece, essas ferramentas ajudam a investigar e coletar evidência. Várias já apareceram em troubleshooting; aqui o foco é investigação.

### Comandos de descoberta rápida
```bash
# Ver conexões ativas pra achar comunicação com C2
netstat -ano          # Windows
netstat -tulpn        # Linux

# Procurar uma palavra dentro de logs (ex: um IP malicioso)
grep "203.0.113.10" /var/log/auth.log

# Ver as últimas linhas de um log em tempo real
tail -f /var/log/syslog

# Baixar e inspecionar o conteúdo de uma URL suspeita (com cuidado)
curl -I https://site-suspeito.com    # -I só os cabeçalhos
```

### Ferramentas de captura e cópia
- **`dd`:** copia dados bit a bit. Usado pra criar imagem forense de um disco inteiro.
```bash
# Criar imagem forense de um disco (exemplo de laboratório)
dd if=/dev/sdb of=imagem_forense.dd bs=4M status=progress
```
- **`memdump`:** captura o conteúdo da memória RAM (pra pegar malware fileless e senhas na memória).

### Ferramentas gráficas de forense
- **Wireshark:** analisa capturas de rede (.pcap) pacote por pacote. A ferramenta nº 1 de análise de tráfego.
- **FTK Imager:** cria e abre imagens forenses de disco.
- **Autopsy:** plataforma de análise forense de disco (arquivos deletados, timeline, etc).
- **WinHex:** editor hexadecimal pra olhar dados crus do disco/memória.

### Ferramentas online de análise (reputação)
Antes de abrir qualquer coisa suspeita, consulte:
- **VirusTotal:** verifica arquivo/URL/hash contra dezenas de antivírus.
- **urlscan.io:** "fotografa" e analisa um site sem você visitá-lo.
- **any.run / Joe Sandbox:** executam o malware numa sandbox isolada e mostram o que ele faz.
- **urlvoid:** checa reputação de domínio.
- **WHOIS:** mostra quem registrou um domínio e quando (domínio criado ontem = suspeito).

```bash
# Consultar WHOIS de um domínio pela linha de comando
whois dominio-suspeito.com
```

### LOLBAS / GTFOBins / WADComs (usando ferramentas pra fins não planejados)
Técnica de "viver da terra" (*living off the land*): o atacante usa ferramentas **legítimas** que já vêm no sistema pra agir, evitando trazer malware que o antivírus pegaria. Ex: usar o `certutil.exe` do Windows pra baixar arquivo, ou o `powershell` pra rodar código.
- **LOLBAS:** catálogo dessas técnicas no **Windows**.
- **GTFOBins:** o mesmo pro **Linux**.
- **WADComs:** foco em ambiente **Windows/Active Directory**.
Pro Blue Team, isso é crucial: você precisa detectar uso **anormal** de ferramenta normal (ex: por que o `certutil` baixou um .exe da internet?).

---

## 15. Logs

Log é o registro do que aconteceu. **Sem log, não tem investigação.** O trabalho do SOC vive de ler e correlacionar logs.

- **Event Logs (Windows):** eventos do sistema, segurança e aplicação. IDs importantes:
  - `4624` = login com sucesso
  - `4625` = login falhou (vários seguidos = força bruta)
  - `4688` = novo processo criado
  - `4720` = nova conta criada
- **Syslog (Linux/rede):** formato padrão de log de sistemas Linux, roteadores, firewalls. Fica em `/var/log/`.
- **Netflow:** metadados de tráfego (quem falou com quem, quando, quanto), sem o conteúdo. Ótimo pra ver comunicação com C2.
- **Packet Captures (.pcap):** o tráfego cru e completo, capturado pelo Wireshark/tcpdump.
- **Firewall Logs:** o que o firewall permitiu e bloqueou. Fonte rica de tentativa de ataque.

### Exemplo real - caçando força bruta no log do Linux
```bash
# Contar tentativas de login SSH que falharam, por IP de origem
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr
#  142 203.0.113.10   <- esse IP tentou 142 vezes, provável ataque
#    3 192.168.1.20
```
Esse tipo de consulta é a essência do que um SIEM automatiza em escala.

---

## 16. Conceitos de Hardening

Hardening é "endurecer" o sistema pra reduzir pontos de entrada. Técnicas que o roadmap cita:

- **Controle MAC-based:** liberar/bloquear acesso à rede pelo endereço MAC do aparelho.
- **Controle NAC-based (Network Access Control):** só deixa entrar na rede o aparelho que cumpre as regras (antivírus atualizado, patch em dia).
- **Port Blocking:** fechar portas de rede que não são usadas.
- **Group Policy (GPO):** no Windows/AD, aplica regras de segurança em massa a todas as máquinas (senha forte, bloqueio de USB, etc).
- **Sinkholes:** redirecionar tráfego malicioso (ex: domínio de C2) pra um "buraco" controlado, cortando a comunicação do malware.
- **ACLs (Access Control Lists):** listas que dizem quem/qual tráfego pode passar (em firewall, roteador ou arquivo).
- **Patching:** aplicar atualizações que corrigem falhas. A medida mais básica e mais ignorada. Muito ataque explora falha que já tinha correção.
- **Jump Server (bastion):** um servidor intermediário e monitorado por onde **todo** acesso administrativo precisa passar. Concentra e vigia o acesso privilegiado.
- **Endpoint Security:** proteção na "ponta" (notebooks, estações): antivírus, EDR, disco criptografado.

### Exemplo real - GPO de senha forte
No AD, uma Group Policy pode forçar: senha mínima de 14 caracteres, troca a cada 90 dias, bloqueio após 5 tentativas erradas. Aplicada uma vez no domínio, vale pra todas as máquinas automaticamente.

---

## 17. Protocolos Seguros vs Inseguros

Regra geral: a versão "segura" quase sempre adiciona criptografia (TLS/SSL) por cima da insegura. Como Blue Team, você sinaliza o uso dos inseguros.

| Inseguro | Seguro | O que muda |
|---|---|---|
| FTP (21) | **SFTP (22)** / FTPS | Criptografa a transferência de arquivo |
| HTTP (80) | **HTTPS (443)** | Criptografa a navegação web |
| Telnet (23) | **SSH (22)** | Criptografa o acesso remoto |
| LDAP (389) | **LDAPS (636)** | Criptografa consulta ao diretório |
| DNS (53) | **DNSSEC** | Garante que a resposta DNS é autêntica |
| SSL (antigo) | **TLS 1.2 / 1.3** | Versão atual e segura da criptografia |

Outros que o roadmap cita:
- **IPSEC:** criptografa o tráfego na camada de rede (base de muitas VPNs).
- **SRTP:** versão segura do RTP (criptografa chamadas de voz/vídeo).
- **S/MIME:** criptografa e assina e-mails.

---

## 18. Termos de Defesa

A "sopa de letrinhas" das ferramentas de defesa. Saber a diferença evita confusão no dia a dia.

- **Antivírus (AV):** detecta malware conhecido por assinatura. Defesa básica.
- **Antimalware:** termo mais amplo, pega também spyware, adware, etc.
- **EDR (Endpoint Detection and Response):** o "antivírus turbinado". Além de detectar, grava o comportamento do endpoint e permite responder (isolar a máquina, matar processo). É o que roda num SOC moderno.
- **XDR:** o EDR expandido, correlacionando endpoint + rede + e-mail + nuvem num lugar só. (é bem o universo do Cortex, por exemplo).
- **DLP (Data Loss Prevention):** impede vazamento de dado sensível (ex: bloqueia alguém de mandar planilha de cartão por e-mail).
- **Firewall:** controla tráfego de rede por regras (IP, porta).
- **Next-Gen Firewall (NGFW):** firewall moderno que também enxerga aplicação, usuário e faz inspeção profunda.
- **Host-Based Firewall:** firewall na própria máquina (ex: Firewall do Windows), não na borda da rede.
- **HIPS (Host Intrusion Prevention System):** IPS rodando no próprio host.
- **NIDS / NIPS:** IDS/IPS de **rede** (Network), olhando o tráfego que passa.
- **Sandboxing:** executar arquivo suspeito num ambiente isolado e descartável pra ver o que faz sem risco.
- **ACL:** lista de controle de acesso (já citada).

### WiFi - EAP vs PEAP, WPS e o padrão de criptografia
- **WEP:** criptografia WiFi **antiga e quebrada**. Nunca use.
- **WPA / WPA2 / WPA3:** evolução da segurança WiFi. **WPA3** é o mais atual e seguro; WPA2 ainda é muito comum; WPA e WEP estão obsoletos.
- **WPS:** aquele botão/PIN de pareamento fácil do roteador. Cômodo, mas **inseguro** (PIN pode ser quebrado). Desligue.
- **EAP vs PEAP:** métodos de autenticação em WiFi corporativo. **PEAP** coloca o EAP dentro de um túnel TLS, protegendo as credenciais. Usado com RADIUS no WiFi da empresa.

---

## 19. Processo de Resposta a Incidentes

Quando algo ruim acontece, se segue um processo. O modelo mais usado (NIST / SANS) tem 6 fases. Decore essa ordem, é pergunta clássica de entrevista e do dia a dia.

1. **Preparação (Preparation):** antes do incidente. Ter ferramentas, runbooks, contatos e treino prontos.
2. **Identificação (Identification):** detectar e confirmar que é um incidente de verdade (sai do alerta pra "sim, é real").
3. **Contenção (Containment):** impedir que se espalhe. Ex: isolar a máquina da rede. Pode ser de curto e longo prazo.
4. **Erradicação (Eradication):** remover a ameaça (apagar o malware, fechar a brecha usada).
5. **Recuperação (Recovery):** voltar tudo ao normal com segurança (restaurar backup, monitorar se volta).
6. **Lições Aprendidas (Lessons Learned):** reunião pós-incidente. O que deu errado, o que melhorar, atualizar o runbook. **Não pule essa.**

### Classificação de ameaças
- **Zero Day:** falha sem correção conhecida (já explicada).
- **Known vs Unknown:** ameaça conhecida (tem assinatura, dá pra detectar fácil) vs desconhecida (precisa de análise de comportamento).
- **APT (Advanced Persistent Threat):** grupo sofisticado, geralmente patrocinado por governo, que entra e fica **meses** escondido roubando dado aos poucos. Alvo: grandes empresas e governos.

### Público / Audiência
Num incidente, você comunica pra gente diferente de jeito diferente:
- **Management / Gestão:** quer impacto no negócio, sem jargão.
- **Stakeholders:** os interessados no sistema afetado.
- **Legal (Jurídico):** riscos legais, LGPD, notificação.
- **HR (RH):** quando envolve funcionário.
- **Compliance:** quando envolve norma/regulação.
Saber adaptar a linguagem é uma habilidade que te destaca cedo na carreira.

---

## 20. SIEM e SOAR

As duas plataformas que são o "quartel-general" do SOC. Entender a diferença é essencial.

### SIEM (Security Information and Event Management)
Centraliza **todos os logs** da empresa (servidores, firewall, AD, nuvem, endpoints) num lugar só, correlaciona e gera **alertas**. É onde o analista de SOC vive, caçando e investigando.
- Exemplos de mercado: Splunk, Microsoft Sentinel, Elastic/ELK, Palo Alto Cortex XSIAM.
- O valor está na **correlação:** sozinho, "um login fora do horário" não é nada; junto com "de um país estranho" + "seguido de acesso a dado sensível", vira um alerta forte.

### SOAR (Security Orchestration, Automation and Response)
Automatiza a resposta. Pega os alertas do SIEM e roda **playbooks automáticos**: bloquear um IP, isolar uma máquina, abrir um ticket, enriquecer o alerta com threat intel, tudo sem mão humana. Serve pra dar conta do volume e responder em segundos.

> 💡 Analogia: o **SIEM** é o detetive que junta as pistas e aponta o suspeito. O **SOAR** é o esquadrão que já sai agindo seguindo o manual.

### Distros de hacking (bom conhecer)
- **Kali Linux:** a distro mais famosa pra pentest, cheia de ferramentas prontas.
- **ParrotOS:** alternativa ao Kali, também focada em segurança e privacidade.
Pro Blue Team, vale ter um Kali no lab pra entender as ferramentas que o outro lado usa.

---

## 21. Padrões e Compliance

Normas e frameworks que dizem **como** fazer segurança direito. Você não decora tudo, mas precisa saber o que cada sigla é.

- **ISO 27001 / 27002:** padrão internacional de gestão de segurança da informação. 27001 é a norma certificável; 27002 traz os controles práticos (Anexo A). Empresa séria busca essa certificação.
- **NIST:** instituto americano com frameworks muito usados no mundo todo.
- **NIST CSF (Cybersecurity Framework):** organiza segurança em 5 (hoje 6) funções: **Identificar, Proteger, Detectar, Responder, Recuperar** (e Governar). Ótimo mapa mental da área toda.
- **RMF (Risk Management Framework):** processo do NIST pra gerir risco em sistemas.
- **CIS Controls / CIS Benchmarks:** lista prática e priorizada de controles de segurança, e guias de hardening passo a passo por tecnologia (ótimos e gratuitos).

E os que valem pra quem trabalha com dado no Brasil:
- **LGPD:** lei brasileira de proteção de dados pessoais.
- **PCI-DSS:** norma obrigatória pra quem lida com dado de cartão de crédito.

---

## 22. Cloud

Hoje tudo vai pra nuvem, e a segurança vai junto. O roadmap pede a base de cloud.

### Conceitos
- **Cloud vs On-Premises:** on-premises é infra na casa da empresa (servidor físico próprio); cloud é alugar infra de um provedor pela internet. Muda quem é responsável pelo quê.
- **Modelo de Responsabilidade Compartilhada:** regra de ouro da segurança em nuvem. O provedor cuida da segurança **da** nuvem (hardware, datacenter); **você** cuida da segurança **na** nuvem (suas configs, acessos, dados). A maioria dos vazamentos em nuvem é config errada do cliente, não falha do provedor.
- **Infrastructure as Code (IaC):** criar a infra escrevendo código (Terraform, CloudFormation) em vez de clicar no painel. Permite versionar e auditar. Risco: um erro no código se multiplica em tudo.
- **Serverless:** rodar código sem gerenciar servidor (ex: AWS Lambda). Você só cuida da função; o provedor cuida do resto.

### Modelos de Serviço
- **IaaS (Infra como Serviço):** você aluga a máquina virtual e cuida do SO pra cima. Ex: EC2.
- **PaaS (Plataforma como Serviço):** você só sobe sua aplicação, a plataforma cuida do resto. Ex: App Service.
- **SaaS (Software como Serviço):** software pronto pra usar. Ex: Gmail, Microsoft 365.
> Quanto mais "aaS", menos você gerencia e menos você é responsável pela infra.

### Modelos de Implantação
- **Privada:** nuvem só sua.
- **Pública:** compartilhada (AWS, Azure, GCP).
- **Híbrida:** mistura das duas.

### Provedores e Armazenamento
- **Provedores:** AWS, Azure (Microsoft), GCP (Google).
- **Armazenamento:** S3 (AWS), OneDrive (Microsoft), Google Drive, Box, Dropbox, iCloud.
> ⚠️ Bucket S3 configurado como público é uma das causas de vazamento mais comuns do mundo. Sempre cheque.

---

## 23. Programação

Você não precisa virar desenvolvedor, mas saber ler e escrever script muda seu patamar. Prioridades pro Blue Team:

- **Python:** 🥇 a mais importante. Automatiza tarefa, processa log, consulta API, faz parsing. Comece por ela.
- **Bash:** essencial pra qualquer coisa em Linux (já usou vários exemplos aqui).
- **PowerShell:** essencial pra Windows e AD. Atacantes abusam muito dela, então você precisa ler PowerShell malicioso.
- **JavaScript:** ajuda a entender ataques web (XSS).
- **Go e C++:** mais pra frente, pra entender malware e ferramentas de performance.

### Exemplo real - Python pra Blue Team
```python
# Script simples que lê um log e lista os IPs que mais falharam login
from collections import Counter
import re

ips = []
with open("auth.log") as f:
    for linha in f:
        if "Failed password" in linha:
            achado = re.search(r"from (\d+\.\d+\.\d+\.\d+)", linha)
            if achado:
                ips.append(achado.group(1))

for ip, qtd in Counter(ips).most_common(5):
    print(f"{qtd} tentativas de: {ip}")
```
Esse tipo de scriptzinho resolve muito problema real de SOC e é ótimo pra começar.

---

## 24. Certificações

Certificação ajuda a conseguir o primeiro emprego e a estruturar o estudo. Ordem sugerida pra quem está começando no Blue Team:

### Iniciante (comece aqui)
- **CompTIA Security+:** 🎯 a certificação de entrada mais recomendada do mundo. Cobre quase tudo deste roadmap em nível introdutório. Se for tirar uma, é essa.
- **CompTIA Network+:** fundamentos de rede. Boa antes da Security+ se rede é seu ponto fraco.
- **CompTIA A+:** fundamentos de TI/suporte. Bem básica.
- **CompTIA Linux+:** fundamentos de Linux.
- **CCNA (Cisco):** rede num nível mais profundo e prático.

### Foco Blue Team / SOC (próximo passo)
- **Blue Team Level 1 (BTL1):** muito prática, focada em SOC, forense e resposta a incidente. Excelente pro seu perfil.
- **GSEC, GCIH, GCIA (GIAC/SANS):** respeitadíssimas, porém caras.

### Avançadas (futuro)
- **CISSP:** gestão de segurança (mais sênior, pede experiência).
- **CISM / CISA:** gestão e auditoria.
- **OSCP / GPEN / CEH / CREST / GWAPT:** mais voltadas pra **ataque** (Red Team/pentest), bom conhecer o lado ofensivo.

> 💡 Dica: não colecione certificação. Uma boa (Security+ ou BTL1) + projetos práticos + um home lab valem mais que cinco provas decoradas.

---

## 25. CTFs e Prática

Teoria sem prática não fixa. **CTF (Capture The Flag)** são desafios onde você "hackeia" ou defende pra achar uma "flag" (código secreto). É a melhor forma de treinar de graça e legalmente.

- **TryHackMe:** 🥇 melhor pra começar. Guia você passo a passo, tem trilha de Blue Team/SOC inteira. Comece por aqui.
- **HackTheBox:** mais difícil e realista. Ótimo pro próximo nível (tem a trilha HTB Academy mais guiada).
- **picoCTF:** CTF educativo e gratuito, bom pra fundamentos.
- **VulnHub:** máquinas virtuais vulneráveis pra baixar e praticar no seu lab offline.
- **SANS Holiday Hack Challenge:** desafio anual, divertido e gratuito.

### Sugestão de rotina de estudo
1. Leia o conceito aqui neste guia.
2. Faça uma sala relacionada no TryHackMe.
3. Reproduza no seu home lab (Kali + alvo no VirtualBox).
4. Anote o que aprendeu (um repositório de notas como este já é meio caminho).

---

## 26. Próximos Passos

Você não precisa aprender tudo de uma vez. Um caminho realista pra quem está em estágio/início de Blue Team:

**Fase 1 - Fundamentos (1 a 3 meses)**
- [ ] Redes (OSI, TCP/IP, portas, subnetting)
- [ ] Linha de comando Linux e Windows
- [ ] Montar um home lab no VirtualBox
- [ ] Trilha de pré-segurança do TryHackMe

**Fase 2 - Base de Segurança (3 a 6 meses)**
- [ ] Tríade CIA, Defesa em Profundidade, Kill Chain
- [ ] Tipos de ataque e de malware
- [ ] Ler e correlacionar logs (Event Log, syslog)
- [ ] Estudar pra CompTIA Security+

**Fase 3 - Blue Team na prática (6+ meses)**
- [ ] SIEM (fazer consultas, criar alerta): pratique num Splunk/Sentinel/ELK gratuito
- [ ] Processo de Resposta a Incidentes de ponta a ponta
- [ ] MITRE ATT&CK aplicado aos seus alertas
- [ ] Trilha de SOC Analyst do TryHackMe + BTL1

**Sempre**
- [ ] Automatizar algo com Python toda semana
- [ ] Acompanhar notícia de segurança (threat intel)
- [ ] Manter este repositório de notas atualizado

---

## 📎 Recursos

- 🗺️ [Roadmap original (roadmap.sh)](https://roadmap.sh/cyber-security)
- 📚 [MITRE ATT&CK](https://attack.mitre.org)
- 🎯 [TryHackMe](https://tryhackme.com) · [HackTheBox](https://www.hackthebox.com)
- 🔎 [VirusTotal](https://www.virustotal.com) · [urlscan.io](https://urlscan.io)
- 🛡️ [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- 📏 [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)

---

> Feito como guia de estudos pessoal, com base no roadmap de cibersegurança do roadmap.sh.
> A segurança é uma maratona, não uma corrida de 100 metros. Estude um pouco todo dia e revise sempre. 🛡️
