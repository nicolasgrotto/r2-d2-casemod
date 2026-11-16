# Segurança cibernética e hardening

> **Responsáveis principais:** Gabriel Cardoso e Nicolas Egea. Todos os integrantes participaram do projeto; veja [equipe.md](equipe.md).
>
> **Fonte primária:** [Cyber_R2-D2.pdf](pdfs/Cyber_R2-D2.pdf) (documento original da equipe). Complementos da [Ficha Técnica](pdfs/Ficha_Tecnica_R2-D2.pdf) quando indicados.

← [Voltar ao índice](README.md)

## Sumário

1. [Escopo e tratamento de dados sensíveis](#1-escopo-e-tratamento-de-dados-sensíveis)
2. [Medidas implementadas](#2-medidas-implementadas)
3. [Auditoria de portas com Nmap](#3-auditoria-de-portas-com-nmap)
4. [Hardening do Windows Server 2022](#4-hardening-do-windows-server-2022)
5. [Riscos identificados e mitigação](#5-riscos-identificados-e-mitigação)
6. [Recomendações não aplicadas](#6-recomendações-não-aplicadas)

---

## 1. Escopo e tratamento de dados sensíveis

A segurança cobre os três ambientes do projeto: **Windows 10 Pro** (host), **Windows Server 2022** (VM `wswerv`) e **Parrot Security OS 7.4** (VM `Parrot_Cyber`), detalhados em [software-e-infraestrutura.md](software-e-infraestrutura.md).

Esta documentação **não registra** senhas, tokens, chaves, endereços IP reais, o endereço público do túnel ngrok nem o *hostname* do computador. O endereço interno aparece mascarado (`192.168.1.XXX`), como no PDF original.

**Como ler este documento:** as seções 2 a 5 reproduzem o que a equipe registrou no PDF Cyber como **implementado**. A seção 6 reúne **recomendações desta documentação que não constam como aplicadas**. Todas as medidas da seção 2 são declaradas pela equipe; o PDF não anexa capturas de tela nem saídas de comando, exceto o comando de firewall (seção 4) e o resumo da varredura (seção 3).

## 2. Medidas implementadas

| # | Medida | Onde | Descrição | Registro no PDF |
| --- | --- | --- | --- | --- |
| 1 | **Filtragem de DNS anti-malware** | Os três sistemas | DNS de segurança da Cloudflare (`1.1.1.2` primário e `1.0.0.2` secundário), que bloqueia a resolução de domínios maliciosos e tentativas de *phishing* na camada de rede | Valores informados |
| 2 | **Traffic Policy do ngrok** | Túnel de acesso externo | Políticas aplicadas no túnel reverso, com gateway seguro em HTTPS (TLS) que filtra e controla requisições antes de chegarem a `localhost:5000` | Descrição geral; regras não detalhadas |
| 3 | **Proteção de endpoint** | Windows 10 e Windows Server 2022 | Windows Defender com monitoramento em tempo real | Declarado |
| 4 | **Isolamento por *sandbox*** | Parrot Security OS | Mecanismos nativos de confinamento de aplicações via **Firejail** e recursos de proteção de rede | Declarado; sem detalhes |
| 5 | **VPN** | Windows 10 (host) | ProtonVPN em interface de túnel virtual dedicada, para confidencialidade e integridade do tráfego externo | Declarado (a interface consta na Ficha Técnica) |
| 6 | **Gerenciamento de atualizações** | Os três sistemas | Atualização integral de pacotes e correções, para mitigar vulnerabilidades conhecidas (CVEs) | Declarado |
| 7 | **Política de credenciais fortes** | Contas administrativas dos três sistemas | Senhas robustas com maiúsculas, minúsculas, números e símbolos, contra ataques de força bruta e de dicionário | Declarado |
| 8 | **Auditoria de portas com Nmap** | VM `Parrot_Cyber` contra a VM `wswerv` | Varredura de reconhecimento e detecção de versões (seção 3) | Comando e resultados resumidos |
| 9 | **Regra de firewall de bloqueio** | VM `wswerv` | Bloqueio de entrada das portas 5357 e 5985 (seção 4) | Comando completo |
| 10 | **RDP habilitado de forma controlada** | VM `wswerv` | Acesso remoto administrativo ativado, com regra de entrada específica no Windows Defender Firewall (seção 4) | Declarado |
| 11 | **Isolamento da aplicação em *loopback*** | VM `wswerv` | A aplicação em `localhost:5000` não é acessível diretamente pela rede local | Confirmado pela varredura |

Complemento: segundo a Ficha Técnica, o host usa **UEFI com Secure Boot desativado**.

## 3. Auditoria de portas com Nmap

A partir da VM `Parrot_Cyber` foi executada uma varredura de reconhecimento e detecção de versões contra o endereço interno do Windows Server 2022, na rede em modo Bridge:

```bash
sudo nmap -sV -Pn 192.168.1.XXX
```

**Resultados da 1.ª varredura (diagnóstico inicial):**

| Porta | Estado | Serviço informado | Observação do PDF |
| --- | --- | --- | --- |
| 80/tcp | aberta | Microsoft IIS httpd 10.0 | Servidor web ativo, operando em conjunto com a aplicação local em `localhost:5000` |
| 5357/tcp | aberta | Microsoft HTTPAPI httpd 2.0 | Rotulada no PDF como serviço de descoberta de dispositivos (SSDP/UPnP) |
| 5985/tcp | aberta | Microsoft HTTPAPI httpd 2.0 | WinRM, gerenciamento remoto do Windows via HTTP sem criptografia |
| 3389/tcp | **ausente** | — | Permitiu concluir que o RDP, requisito do projeto, estava desativado |

Conclusões registradas: a porta interna da aplicação (`localhost:5000`) permaneceu isolada (protegida em *loopback*) e o RDP precisava ser habilitado. Segundo a equipe, a porta 5000 é a do site do Duel of Fates no IIS, exposta externamente pelo ngrok.

> **Nota técnica:** a porta 5357/tcp costuma ser associada ao WSDAPI (descoberta de dispositivos na rede), enquanto o SSDP/UPnP usa UDP. O PDF rotula o serviço como SSDP/UPnP. A conclusão do hardening (bloquear a porta) não muda.

## 4. Hardening do Windows Server 2022

Com base no diagnóstico do Nmap, foram executadas duas ações corretivas:

1. **Ativação controlada do RDP (porta 3389/tcp):** habilitação do acesso remoto administrativo exigido pelos requisitos do projeto e liberação da regra de entrada correspondente no Windows Defender Firewall.
2. **Redução da superfície de ataque:** regra restritiva de entrada `Hardening_R2D2_Bloqueio_WinRM`, que bloqueia o tráfego TCP nas portas desnecessárias 5357 e 5985:

```cmd
netsh advfirewall firewall add rule name="Hardening_R2D2_Bloqueio_WinRM" dir=in action=block protocol=TCP localport=5985,5357
```

**Resultado registrado:** a aplicação principal opera isolada em `localhost:5000`, e o servidor expõe na rede local apenas os serviços estritamente necessários: **80/tcp** (IIS) e **3389/tcp** (RDP). O PDF afirma que as demais portas ficam filtradas contra acessos externos não autorizados.

## 5. Riscos identificados e mitigação

Riscos identificados pela equipe no diagnóstico e nas medidas descritas:

| Risco | Origem | Mitigação aplicada | Situação |
| --- | --- | --- | --- |
| WinRM (5985) exposto, via HTTP sem criptografia | Varredura Nmap | Regra de firewall de bloqueio | Mitigado (conforme o PDF) |
| Serviço de descoberta de dispositivos (5357) exposto | Varredura Nmap | Regra de firewall de bloqueio | Mitigado (conforme o PDF) |
| Aplicação web acessível diretamente na rede local | Arquitetura (`localhost:5000`) | Aplicação mantida em *loopback* | Mitigado; confirmado pela varredura |
| Exposição externa da aplicação | Uso do ngrok | Túnel HTTPS/TLS com Traffic Policy | Mitigado; regras não detalhadas |
| Resolução de domínios maliciosos e *phishing* | Navegação e atualizações | DNS Cloudflare `1.1.1.2` / `1.0.0.2` | Mitigado |
| Vulnerabilidades conhecidas (CVEs) | Pacotes desatualizados | Atualização integral dos três sistemas | Mitigado no momento da atualização |
| Ataques de força bruta e de dicionário | Contas administrativas | Senhas fortes e padronizadas | Mitigado (declarado) |
| Tráfego externo do host exposto | Rede do host | ProtonVPN em interface dedicada | Mitigado |

## 6. Recomendações não aplicadas

Estas são recomendações **desta documentação**, opcionais: a equipe avaliará quais fazem sentido para o escopo do projeto acadêmico. Elas **não constam** como implementadas no PDF original e não devem ser lidas como medidas existentes:

1. **Nova varredura após o hardening.** O PDF descreve apenas a "1.ª varredura". Uma 2.ª varredura, também de portas UDP e de todas as portas TCP, comprovaria o estado final afirmado na seção 4.
2. **Restringir o RDP.** Limitar a regra da porta 3389 a origens confiáveis e exigir autenticação em nível de rede (NLA), pois o RDP foi aberto na rede local.
3. **Documentar a Traffic Policy do ngrok.** Registrar as regras efetivamente aplicadas, para que a medida seja verificável.
4. **Registrar evidências.** Anexar saídas de comando e capturas (Nmap, regras de firewall, estado do Defender), sem dados sensíveis.
5. **Justificar o Secure Boot desativado.** Registrar o motivo da configuração do host ou reativá-lo, se possível.
