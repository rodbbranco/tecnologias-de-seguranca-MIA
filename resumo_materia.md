# Tecnologias de Segurança 2026/2027 – Resumo para o teste de dezembro

Fontes: "Apresentação 1.pdf" (48 slides, CP1 – Fundamentos de Cibersegurança) e "Apresentação 2.pdf" (17 slides, Segurança em Redes e ACLs, secção 5b). Quando houver mais apresentações (firewalls em detalhe, IDS/IPS, SIEM, VPN, hardening...) este resumo deve ser alargado. Nota: o PDF são capturas de ecrã, por isso li-o slide a slide; alguns números (ex. do gráfico de setores) não são legíveis.

**Legenda:** ⭐ = muito provável no teste.

---

## 0. Objetivos e plano da disciplina
- Reconhecer os componentes-chave de uma plataforma operacional de segurança que assegure **confidencialidade, integridade e disponibilidade (CIA)**.
- Administrar/configurar tecnologias de segurança de rede; identificar requisitos de segurança (serviço, tecnologias, **computação em nuvem**); identificar e explorar vulnerabilidades e padrões de ataque; desenhar medidas que mantenham a rede robusta; conhecer ferramentas de teste de vulnerabilidade.
- Tópicos futuros:
  - **Operações de Segurança:** exploração de vulnerabilidades, ferramentas **SIEM**, infraestrutura de operações, **orquestração, automação e resposta (SOAR)**.
  - **Segurança em Redes:** firewalls; deteção de padrões de ataque e anomalias (**IDS/IPS**); filtros de conteúdos web; **VPN**; desenho de serviços seguros; **hardening**; isolamento e virtualização; **NFV**; prevenção de perda de dados (DLP); gestão unificada de ameaças (UTM). Modelo **PDCA (Plan-Do-Check-Act)** do Sistema de Gestão de Segurança da Informação (SGSI).
- CP1: Fundamentos → CP1.1 Tendências de computação → CP1.2 Ciberameaças → CP1.3 Ciberataques.

## 1. Motivação: o que é "segurança"?
- Analogia do cadeado: "é adequado?" depende do **bem a proteger** (valor subjetivo; "segurança é um sentimento"), de **quanto tempo e como fica exposto**.
- ⭐ **A segurança não é absoluta nem definitiva.** O contexto (tempo, espaço, envolvente social) influencia-a.
- Fragilidades por camada TCP/IP (slide "Motivação"):

| Camada | Fragilidades |
|---|---|
| Aplicação | Denial of Service |
| Transporte (TCP/UDP) | Port scanning, sequence attacks |
| Rede (IPv4, ICMP, IGMP) | IP spoofing, routing poisoning, wrong diagnostics |
| Ligação (Ethernet, ARP) | Sniffing, MAC spoofing |
| Física | Acesso / diafonia / partilha |
- Transversal: erros de especificação e bugs de código (*Spec & Code Bugs*).

## 2. Fundamentos: modelos de segurança da informação ⭐
### Tríade CIA
- ⭐ **Confidencialidade (confidentiality/privacy/secrecy):** o conteúdo só é acessível a entidades **autorizadas**. Garante-se por **proteção física** (cofre, rack trancada, carrinha blindada) e por **algoritmos matemáticos** (cifragem/decifragem com chave; o atacante vê apenas texto cifrado – exemplo Gail → Jeremy).
- ⭐ **Integridade:** o conteúdo só é alterado por entidades autorizadas. São necessários mecanismos que **detetem** manipulação (adição, alteração, remoção), intencional (fraude) ou acidental (negligência). Violações: alterar a aparência de um website, intercetar e modificar uma transação de e-commerce, alterar uma ficha de informação num servidor.
- ⭐ **Disponibilidade:** os sistemas e infraestruturas permitem aceder à informação com a qualidade esperada quando solicitada. É uma medida da acessibilidade. **99,999 % ("cinco noves") ≈ 5 minutos offline por ano.** Violações: suporte digital danificado (*head crash*), ligação de acesso ao servidor saturada, bug no servidor (natural ou malicioso) que o torna inacessível.

### Cubo da segurança da informação (Cisco Learning Institute) ⭐
Três dimensões:
1. **Atributos:** Confidentiality, Integrity, Availability.
2. **Estado da informação:** Processing, Storage, Transmission.
3. **Medidas de segurança:** Policy and Procedures, Technology (e educação/awareness).
- 👉 É no estado de **processamento** que é **mais difícil** garantir os atributos.

### Para além da tríade (não há consenso)
- **Donn Parker (2002) – 6 princípios (Hexad):** Confidencialidade, Integridade, Disponibilidade, **Autenticidade (authenticity)**, **Titularidade (possession)**, **Utilidade (utility, valor relativo da informação)**. ⭐
- **2013 – conjunto alargado de 8 atributos:** Confidentiality, Integrity, Availability, **Accountability, Auditability, Authenticity/Trustworthiness, Non-repudiation, Privacy**.
- Objetivos típicos (Handbook of Applied Cryptography): privacidade/confidencialidade, integridade de dados, autenticação de entidade, autenticação de mensagem (origem dos dados), assinatura, autorização, validação, controlo de acesso, certificação, *timestamping*, *witnessing*, receção/confirmação, propriedade, anonimato, **não-repúdio** (impedir negar compromissos/ações anteriores), revogação.

## 3. Tendências de computação e efeito na cibersegurança (CP1.1)
- **Computação em nuvem:** flexibilidade e escalabilidade, mas **aumenta a superfície de ataque** (dados fora do controlo direto da organização). Garantir a segurança dos dados na nuvem é preocupação crítica. A **localização da informação** (data centers em vários países) levanta questões legais/jurisdicionais.
- **Super-computadores:** a capacidade de processamento atual afeta a cibersegurança (ex.: quebra de cifras/ataques de força bruta).
- **IA:** ajuda a identificar/responder a ameaças em tempo real, mas **também é usada por cibercriminosos para automatizar ataques**. ⭐ (dupla face)
- **IoT:** câmaras, termóstatos, frigoríficos ligados à Internet **aumentam os pontos de acesso**, muitos vulneráveis.
- **Blockchain:** além de criptomoedas, usada em **autenticação** e **garantia de integridade de dados**; também pode ser alvo de ataques.
- **5G:** mais velocidade e capacidade, mas mais dispositivos ligados → maior exposição; exige mecanismos de segurança nas redes e nos dispositivos.
- **Mobilidade:** dependência de dispositivos/apps móveis; roubo ou perda expõe dados privados.
- **Ataques avançados:** ransomware, **APT (Advanced Persistent Threats)** e engenharia social exigem defesas igualmente avançadas. **Educação/consciencialização** são fundamentais.
- **Responsabilidade partilhada (cloud):** o provider e o cliente partilham a responsabilidade pela segurança dos dados e sistemas. ⭐
- **Conformidade regulatória:** **RGPD** (Europa) molda as práticas; incumprimento → multas elevadas.

## 4. Ciberameaças (CP1.2)
### 4.1 Taxonomia de ciberataques (diagrama)
Classificação por 5 dimensões ⭐:
1. **Attack Vector:** misconfiguration, kernel flaws, design flaws, **buffer overflow** (stack, heap), insufficient input validation, symbolic link, file descriptor attack, race condition, incorrect permission, **social engineering**.
2. **Operational Impact:** installed malware (virus, spyware, trojan, worm), misuse of resources, user compromise, root compromise, web compromise, arbitrary code execution, **denial of service** (host-based, network-based, distributed).
3. **Defense:** **Mitigation** (remover da rede, whitelisting, reference advisory) e **Remediation** (patch system, correct code).
4. **Informational Impact:** distort, disrupt, destruct, disclose, discovery.
5. **Target:** OS (kernel/driver), network, local, user, application, server (DB, email, web), client.
- Exemplos de aplicação (tabela): **MS RPC Stack Overflow** (buffer overflow stack → malware ACE → distort → patch), **Gimmiv.A** (stack overflow → trojan → disclosure), **Conficker** (stack overflow → worm → disrupt; Windows Server/2000/XP).

### 4.2 Vulnerabilidade típica: Buffer overflow ⭐
- Segundo o **CERT**, cerca de **1/3 das vulnerabilidades de software** são buffer overflows.
- **Buffer** = zona de memória reservada por uma aplicação para dados temporários. Aplicações deficientes aceitam mais dados do que o buffer suporta → corrompem zonas de memória contíguas (outros dados ou código).
- **Vírus e trojans** tendem a explorar *root buffers* **locais**; **worms** como **SQL Slammer** e **Code Red** exploraram *root buffers* **remotos** (não precisam de utilizadores locais nem dos seus privilégios).

### 4.3 Tipos de malware
- ⭐ **Vírus:** termo proposto em **1983 por Frederick Cohen** (estudante da USC). Analogia com o vírus biológico (precisa de célula hospedeira). Código malicioso **integrado numa aplicação legítima**; propaga-se quando ativado; pode ser inofensivo ou destrutivo; meio preferencial de disseminação: **email**.
- ⭐ **Cavalos de Troia:** nome da mitologia grega; aplicação com propósito aparentemente inofensivo que esconde código malicioso (danos locais, aceitar comandos remotos – *back doors*, divulgar informação confidencial). **Não criam réplicas de si próprios**, são fáceis de elaborar (*script kids*), operam em cliente/servidor, são difíceis de detetar e por vezes autodestroem-se. Exemplos: keylogger, backdoor, spammers. Tipos: remote-access, data-sending, destructive, proxy, FTP, security-software-disabler, denial-of-service.
- ⭐ **Worms (vermes):** executam-se e **replicam-se de forma autónoma**, explorando vulnerabilidades de protocolos e aplicações; ameaça temível pelo impacto global. Caracterizam-se por explorar uma vulnerabilidade, ter um mecanismo de propagação em rede e uma **payload** com o código ofensivo (ex.: backdoor). Fases: Probe → Penetrate → Persist → Propagate → Paralyze. 
  - **Sapphire/SQL Slammer (jan. 2003, 10 min):** worm de propagação mais rápida da história; 90 % dos servidores SQL na Internet infetados em 10 min; afetou redes móveis na Coreia do Sul, terminais ATM do Bank of America, 5 root servers DNS, reservas da Continental Airlines; em Portugal, 300 000 clientes sem Internet durante 12 h.
  - Comparação (≈20 anos): Morris 1988, Love Bug 2000, Code Red 2001, Slammer 2003, MyDoom 2004, Zotob 2005, MS RPC DNS 0day 2007.
- ⭐ **Ransomware:** família do malware; forma emergente que **bloqueia o acesso** do utilizador aos ficheiros/dispositivo, normalmente **cifrando** toda a informação; objetivo: **pedir resgate financeiro** para decifrar (por vezes ameaça de expor os dados). Exemplo: **CryptoLocker 2.0** (chave privada RSA, prazo de 72 h, pagamento em bitcoins). Slide marcado como **leitura obrigatória**.
- Outros: spyware, rootkit, adware, keylogger, remote access, worm.

### 4.4 Cronologia dos vírus históricos (ver screenshot do slide) ⭐ datas
| Ano | Marco |
|---|---|
| início anos 1970 | **Creeper** (ARPANET) |
| 1974 | Rabbit |
| 1975 | ANIMAL |
| 1982 | Elk Cloner |
| **1983** | **Termo "computer virus" cunhado** (Cohen) |
| 1986 | **Brain** (boot sector) |
| 1989 | Ghostball |
| 1991 | Michelangelo |
| 1995 | **Concept** (macro virus) |
| 1999 | **Melissa** |
| 2001 | **Simile** (multi-OS) |
- Dica mnemónica: Creeper (ARPANET, 70s) → Elk Cloner (82) → termo (83) → Brain (86, boot sector) → Concept (95, macro) → Melissa (99, email) → Simile (01, multi-OS).

### 4.5 Dados da UE (relatório ENISA, ano 2022)
- **Top 8 ameaças:** 1) Ransomware, 2) Malware, 3) Social engineering, 4) Threats against data, 5) Threats against availability: DoS, 6) Threats against availability: Internet threats, 7) Disinformation/misinformation, 8) Supply-chain attacks. ⭐ (ordem)
- Ransomware: >10 TB de dados roubados por mês; **phishing é o vetor inicial mais comum**; DDoS também entre as maiores ameaças.
- Custo anual da cibercriminalidade para a economia mundial: **5,5 biliões de euros no final de 2020**, o dobro de 2015.
- Setor mais atingido por nº de incidentes: **administração pública/governo (~24 %)**, seguido de serviços digitais (~13 %), público geral (~12 %), serviços (~12 %), finanças/banca (~9 %), saúde (~7 %).
- **Instituições relevantes:** FIRST, MITRE, CERT, SANS, INFOSYSSEC, Center for Internet Security, (ISC)², **CNCS** (Centro Nacional de Cibersegurança, Portugal) e **CERT.PT**.

## 4b. Leitura obrigatória: Ransomware (artigo MDPI) ⭐
**Kapoor, Gupta, Gupta, Tanwar, Sharma, Davidson (2022). "Ransomware Detection, Avoidance, and Mitigation Scheme: A Review and Future Directions". *Sustainability* 14(1), 8.** (https://www.mdpi.com/2071-1050/14/1/8)
Nota: resumo feito a partir de uma síntese automática do texto, não de leitura integral. Confirma pormenores no artigo.

- **Framework DAM = Detection, Avoidance, Mitigation:** organiza técnicas, ferramentas e estratégias de defesa contra ransomware.
- **Tipos:** **Crypto ransomware** (cifra ficheiros com chave simétrica ou assimétrica; mais comum e eficaz) vs **Locker ransomware** (bloqueia o acesso ao dispositivo sem cifrar; menos eficaz porque os dados continuam acessíveis).
- **Fases do ataque:** 1) Infeção (email, média amovível, malvertising, engenharia social) → 2) Cifragem/bloqueio (muitas vezes contacta servidores C&C) → 3) Pedido de resgate → 4) Resultado (pagamento, tentativa de engenharia inversa ou perda permanente).
- **Deteção:** análise **estática** (código sem executar; ex. IDA Pro) vs **dinâmica** (comportamento em execução, tráfego de rede). Maioria híbrida e baseada em IA; é **reativa**. A deteção pode demorar 50-60 s, mas estirpes avançadas cifram em ~15 s.
- **Evitar (avoidance):** a estratégia **mais desejável**: patches e atualizações, boas práticas de email e consciencialização do utilizador (*cyber-hygiene*), desativar JavaScript/Java no browser, Controlled Folder Access. Níveis de implementação de 1 (pequenas entidades) a 4 (infraestruturas críticas).
- **Mitigação:** SDN para pôr servidores C&C em lista negra, engenharia inversa para recuperar dados, ferramentas de endpoint (Defender, Sophos), **backups e snapshots**, análise de entropia de ficheiros. Na prática, a maioria das vítimas paga ou perde os dados; não há solução universal.
- **Caso Djvu (desde T4 2018):** ~250 variantes, distribuído por cracks/torrents e anexos de email; passou de AES (simétrico) para RSA (assimétrico); cifra só os primeiros 2-5 MB dos ficheiros; ~45-60 s para cifrar; desconto de 50 % se pagar em 72 h.
- **Conclusões:** não existe proteção ponta-a-ponta; **prevenção > deteção > mitigação**; defesas reativas; são necessários testes de intrusão, políticas atualizadas e ciber-seguro. Trabalho futuro: deteção/sandboxing no browser, assistentes de ciber-higiene com IA, repositórios de software confiáveis, backup/restore, monitorização de CVEs em tempo real.
- **Perguntas:** (a) O que significa DAM? (b) Crypto vs locker? (c) Quatro fases de um ataque? (d) Análise estática vs dinâmica? (e) Porque é que a prevenção é preferível? (f) Que medidas de mitigação existem? (g) O que distingue o Djvu?

## 5. Ciberataques (CP1.3)
- **Definição:** tentativas orquestradas contra sistemas, redes ou dispositivos para explorar, comprometer, manipular ou danificar informação/dados. Incluem violação (com ou sem sucesso) das defesas para expor informação sensível, interromper serviços, disseminar malware.
- **Nota do professor (via Rodrigo, 13/10/2026): para já, nos ciberataques só são exigidas as definições**, não as defesas. Foca-te em saber definir cada um com uma frase e um exemplo.
- **Quem os orquestra:** indivíduos (com ou sem formação), grupos organizados (motivações ideológicas, políticas, religiosas, financeiras), **hackers éticos** (procuram vulnerabilidades para tornar o sistema mais seguro), **governos** (políticos, económicos, informação classificada).

| Ataque | Ideia-chave |
|---|---|
| ⭐ **Malware** | Envio/propagação de software malicioso (vírus, trojans, spyware, ransomware...). |
| ⭐ **Phishing** | Mensagens fraudulentas (muitas vezes por email) fingindo fontes fidedignas para obter senhas, códigos, cartões de crédito. |
| ⭐ **Social engineering** | Manipular o ser humano para revelar informação sensível ou praticar atos que comprometem a segurança; atinge vulneráveis, crianças e jovens; também para fraudes. |
| ⭐ **Man-in-the-Middle (MitM)** | Atacante interceta a mensagem entre duas partes e potencialmente altera-a sem que saibam; nem sempre altera o conteúdo (muitas vezes só espia). Tipos: Wi-Fi eavesdropping, DNS spoofing, session hijacking, ARP cache poisoning, man-in-the-browser, IP spoofing, SSL hijacking, email hijacking. Grande parte dos ataques deriva deste. |
| ⭐ **SQL Injection** | Inserção de comandos SQL maliciosos em caixas de entrada de dados para manipular/obter dados da BD (muito usado anos 90 e início de 2000). Ex.: `' OR 1=1 --`. Defesa: validação de input. |
| ⭐ **Brute force** | Tentar muitas combinações utilizador/senha (dicionários com milhões de linhas) até acertar. Exemplo da ferramenta **Hydra** (THC). |
| ⭐ **DoS / DDoS** | Sobrecarregar sistemas, serviços ou redes tornando-os inacessíveis a utilizadores legítimos. **DDoS** = vários dispositivos (**botnet**, controlados por um *command and control server*/bot master) espalhados geograficamente atacam em simultâneo. Afeta a **disponibilidade**. |

## 5b. Segurança em Redes e ACLs (Apresentação 2) ⭐
### Segurança em redes
- Definição (segundo a Cisco) ⭐: **qualquer atividade projetada para proteger o acesso, o uso e a integridade da rede corporativa e dos dados.** Inclui tecnologias de hardware e software; visa uma variedade de ameaças; impede que as ameaças entrem ou se espalhem na rede; a segurança eficaz **controla e gere o acesso** à rede.
- **Tipos de segurança em rede (lista dos slides):** firewalls; segurança no email; software dedicado (antivírus, antimalware); correta **segmentação** da rede; controlo de acessos; segurança nas aplicações; análise de comportamentos; prevenção contra perda de dados (DLP); sistemas de prevenção de intrusão (IPS); segurança em dispositivos móveis e IoT; SIEM; VPN; segurança na web; segurança nas redes sem fios.
- **Tópicos a abordar (resto da disciplina):** firewalls; deteção de padrões de ataque e anomalias (IDS/IPS); filtros de conteúdos web; VPN; desenho de serviços seguros (hardening, isolamento e virtualização, NFV); prevenção de perdas de dados; gestão unificada de ameaças (UTM).
- Trabalho para a aula seguinte: instalar o **Cisco Packet Tracer**. Segundo o Rodrigo (indicação do professor), na aula vai fazer-se um exercício prático: **montar uma rede em que toda a gente tem acesso a tudo e depois ir "fechando os caminhos" com ACLs**.

### ACL – Listas de Controlo de Acesso ⭐⭐
- **O que são:** filtros que permitem identificar PDUs (quadros Ethernet, pacotes IPv4/IPv6...) com base num conjunto de características (**SA, DA, flags**, etc.). Funcionam como uma **forma simplificada de firewall**: bloqueiam ou permitem a passagem de pacotes, filtram tráfego **in e out**, e aplicam-se desde um simples host até uma rede.
- **Para que servem:** condicionar fluxos de pacotes em trânsito (firewalling); selecionar fluxos para tratamento prioritário (**QoS**); selecionar fluxos para encriptação e translação (**NAT/PAT**); selecionar fluxos que desencadeiam ligações dial-up (WAN); controlar a troca de rotas entre protocolos de encaminhamento.

### Regras de aplicação ⭐
- **Tráfego IN:** o que vem da rede e entra no router por uma interface. **Tráfego OUT:** o que sai de uma interface do router e vai para a rede.
- **Só é permitida uma ACL por protocolo, por direção e por interface** (não podem existir duas ACLs TCP no sentido IN na F0/0).
- Uma ACL é uma **sequência** de testes, avaliados por ordem. **Um pacote só é sujeito a um teste se não verificou nenhum anterior** (a primeira correspondência decide: permit ou deny).
- **Deny any implícito no final:** o IOS considera um teste implícito final que descarta tudo o que não foi permitido. Por isso a ACL deve absorver qualquer pacote.
- Se não há ACL na interface, o pacote segue normalmente; se esgota a lista sem correspondência, é descartado (e envia-se "destination not found/unreachable").

### Standard vs Extended ⭐⭐
| | **Standard** | **Extended** |
|---|---|---|
| Numeração | **1–99 e 1300–1999** | **100–199 e 2000–2699** |
| Filtra | Apenas endereço de **origem** (SA) | Origem **e destino**, protocolo, portas, flags TCP, tipo ICMP... |
| Posição | **Mais próximo do destino** | **Mais próximo da origem** |
| Sintaxe | `access-list <n> {deny\|permit} <source> [wildcard] [log]` | `access-list <n> {deny\|permit} <protocolo> <origem> [wildcard] [operador porta] <destino> [wildcard] [operador porta] [established] [log]` |
- **Named ACL:** mesmas características das extended, mas identificadas por **nome** em vez de número.
- **Outros tipos (slide "Tipos de ACL"):** identificação (numerada/nomeada) e característica: **standard** (SA), **extended** (SA, DA, protocolo, portas, flags TCP, tipo ICMP), **dinâmica** (*lock-and-key*, acesso autenticado), **reflexiva** (com extended + established identifica sessões), **temporal** (*time-based*, acesso diferenciado no tempo), **contextual** (*context-based*, **CBAC**, programação de firewalls).

### ACL stateful: `established` ⭐
- Com a opção `established`, o tráfego de retorno de uma ligação previamente estabelecida é **automaticamente autorizado**, sem criar outra ACL para o sentido inverso. **Só em ACLs extended** (TCP).
- Exemplo: `access-list 103 permit tcp host 192.168.0.2 host 200.200.200.1 established` – o tráfego que volta para o host é permitido porque a ligação partiu do host interno (de confiança).

### Wildcard mask ⭐⭐ (muito provável em exercício)
- Define quais os hosts/redes/sub-redes afetados pela ACL. **Bit 0 = o bit tem de ser igual (match exato); bit 1 = pode ser qualquer valor ("don't care").** É o inverso de uma máscara de rede.
- Representação de gamas: o endereço do pacote é comparado com o "padrão desejado" bit a bit; só os bits com wildcard 0 são verificados. Pertence à gama se **todos** os bits verificarem a condição.
- Exemplo 1: **192.168.1.0/24** (máscara 255.255.255.0) → wildcard **0.0.0.255** (255 = 11111111, os 8 bits livres).
- Exemplo 2: **192.168.16.0/24 a 192.168.31.0/24** → wildcard **0.0.15.255**: os 2 primeiros octetos têm de ser 192.168; **15** é a soma dos bits para que as sub-redes (16 a 31) casem com a regra; **255** no último octeto = indiferente.
- Truque: wildcard = 255.255.255.255 − máscara de rede. Para um host usa-se `host x.x.x.x` (wildcard 0.0.0.0) e para tudo `any`.

### Como criar e aplicar uma ACL na Cisco ⭐
1. **Definir:** (a) identificação do objetivo; (b) seleção da posição; (c) sequência de testes.
2. **Criar** em modo de configuração global:
```
R1> enable
R1# configure terminal
R1(config)# access-list n {permit | deny} <Teste1>
R1(config)# access-list n {permit | deny} <Teste2>
```
3. **Aplicar** a uma interface, indicando a direção:
```
R1(config)# interface <IF>
R1(config-if)# ip access-group <nº/nome> {in | out}
```

### Exercício prático para treinar (Packet Tracer): abrir tudo e fechar com ACLs
Sugestão minha, não vem dos slides:
1. Montar uma rede simples: 1 router, 2 ou 3 redes/LANs (ex.: Alunos, Docentes, Servidores) com PCs e um servidor; configurar IPs e testar `ping` entre todos (tudo acessível).
2. Definir o objetivo de cada regra (ex.: "Alunos não acedem aos Servidores", "só HTTP para o servidor web").
3. Escolher o tipo e a posição: **standard** perto do destino (só filtra origem); **extended** perto da origem (filtra origem, destino, protocolo, porta).
4. Escrever as regras por ordem (o mais específico primeiro) e lembrar o **deny any implícito**: se só pões `deny`, acrescenta `permit any` no fim.
5. Aplicar com `ip access-group <n> in|out` na interface certa e **testar de novo** (ping, acesso web) para ver o que foi bloqueado.
6. Verificar com `show access-lists` e `show ip interface <IF>`.

## 6. Mapa rápido: ataque → atributo CIA violado
- DoS/DDoS, falha de hardware → **Disponibilidade**.
- Alteração de website/transação (MitM com modificação) → **Integridade**.
- Sniffing, phishing, espionagem, ransomware com exposição de dados → **Confidencialidade**.
- Ransomware também afeta a disponibilidade (bloqueio dos ficheiros).

## 7. Perguntas de autoavaliação (flashcards)
1. Quais são os três atributos fundamentais da segurança da informação? Define cada um.
2. O que significa "99,999 % de disponibilidade" em tempo offline por ano?
3. Dá dois exemplos de violações de integridade e dois de disponibilidade.
4. Como se garante a confidencialidade? (duas abordagens com exemplo)
5. Quais as 3 dimensões do cubo da segurança da informação e os seus valores? Em que estado é mais difícil garantir os atributos?
6. Que seis princípios propôs Donn Parker em 2002? Quais são os 3 que acrescenta à tríade?
7. Que atributos adicionais surgem na proposta de 2013?
8. O que é não-repúdio? E accountability/auditability?
9. Porque é que "a segurança não é absoluta nem definitiva"?
10. Indica uma fragilidade típica em cada camada TCP/IP (aplicação, transporte, rede, ligação).
11. Como é que a computação em nuvem aumenta a superfície de ataque? O que é o modelo de responsabilidade partilhada?
12. Porque é que a IA é uma "faca de dois gumes" na cibersegurança?
13. Qual o impacto do IoT e do 5G na segurança?
14. Quais as cinco dimensões da taxonomia de ciberataques? Exemplifica cada uma.
15. Distingue **mitigation** de **remediation**.
16. O que é um buffer overflow? Que fração das vulnerabilidades representa segundo o CERT?
17. Diferença entre vírus, worm e trojan (replicação, forma de propagação, dependência de hospedeiro).
18. Quem propôs o termo "vírus de computador" e quando? Qual foi o primeiro vírus (anos 70)?
19. Que vírus foi o primeiro de boot sector (1986)? E o primeiro macro virus famoso (1995)? E o de 1999?
20. Que worm infetou 90 % dos servidores SQL em 10 minutos? Em que ano?
21. Descreve as fases de um worm (Probe → Paralyze).
22. O que é ransomware, como funciona e qual o objetivo? Porque é que o phishing é relevante aqui?
23. Enumera as 8 principais ameaças do relatório ENISA 2022.
24. Qual o custo estimado da cibercriminalidade em 2020? E a relação com 2015?
25. Distingue DoS de DDoS. O que é uma botnet?
26. Explica um ataque MitM e cita 4 variantes.
27. Como funciona uma SQL injection? Como se previne?
28. O que é brute force/ataque de dicionário? Que ferramenta aparece no slide?
29. Quem são os atores que orquestram ciberataques (inclui hackers éticos)?
30. Que entidades portuguesas são referência em cibersegurança? (CNCS, CERT.PT)
31. Que é segurança em redes segundo a Cisco?
32. O que é uma ACL e para que serve (cita 4 utilizações)?
33. Diferença entre ACL standard e extended: numeração, o que filtram e onde se posicionam.
34. Quantas ACLs podem existir por protocolo, direção e interface? Porquê?
35. O que é o "deny any" implícito? Que consequência tem para a escrita de uma ACL?
36. Em que ordem são avaliadas as regras de uma ACL? O que acontece quando há correspondência?
37. Para que serve a opção `established`? Em que tipo de ACL se usa?
38. Escreve a wildcard mask para 192.168.1.0/24 e para 192.168.16.0 a 192.168.31.255.
39. Em wildcard, o que significa bit 0 e bit 1?
40. Enumera 4 tipos de ACL (dinâmica, reflexiva, temporal, contextual) e para que servem.
41. Quais os comandos Cisco para criar e depois aplicar uma ACL a uma interface?
42. O que é uma named ACL?

## 8. Conselhos de estudo
- Dominar bem **CIA + hexad de Parker + cubo** (definições e exemplos de violação): é a parte mais "teórica" e mais cobrável.
- Saber **comparar malware** (vírus/worm/trojan/ransomware) numa tabela e **associar cada ciberataque ao atributo CIA** afetado.
- Memorizar a **cronologia** (1983 termo, 1986 Brain, 1995 Concept, 1999 Melissa, 2003 Slammer) e a **lista ENISA**.
- ACLs: treinar à mão **wildcard masks** e escrever ACLs standard/extended (e saber onde as posicionar); decorar as **numerações** e o **deny any implícito**. Instala o Packet Tracer para praticar.
- Rever as futuras matérias (firewalls, IDS/IPS, VPN, SIEM, hardening) assim que as apresentações seguintes estiverem na Library.
