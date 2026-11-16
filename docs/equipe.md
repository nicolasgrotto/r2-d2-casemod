# Equipe e matriz de responsabilidades

← [Voltar ao índice](README.md)

## 1. Integrantes

O projeto tem quatro integrantes. A tabela mostra as **responsabilidades principais** de cada um. Isso não significa que alguém tenha trabalhado isoladamente: **todos tiveram participação no projeto**.

| Integrante | Responsabilidades principais | Documentos em que é responsável principal |
| --- | --- | --- |
| **Heitor Resende** | Arquitetura do casemod; planejamento estrutural; construção física da estrutura; configuração das máquinas virtuais e do Windows Server 2022 | [arquitetura.md](arquitetura.md); [software-e-infraestrutura.md](software-e-infraestrutura.md) (VMs e Windows Server 2022) |
| **Gabriel Cardoso** | Montagem dos componentes do computador; integração do hardware ao casemod; configuração dos sistemas operacionais; particionamento e ambiente Linux (o dual boot planejado foi substituído por uma VM); configurações de cibersegurança | [hardware.md](hardware.md); [software-e-infraestrutura.md](software-e-infraestrutura.md) (Parte I); [seguranca.md](seguranca.md) |
| **Nicolas Egea** | Mesmas responsabilidades de Gabriel Cardoso | [hardware.md](hardware.md); [software-e-infraestrutura.md](software-e-infraestrutura.md) (Parte I); [seguranca.md](seguranca.md) |
| **Nicolas Oliveira** | Desenvolvimento do R2 Desktop Companion e do Duel of Fates; hospedagem do Duel of Fates com IIS; acesso externo via ngrok. Colaborou (C) na parte de cibersegurança | [software-e-infraestrutura.md](software-e-infraestrutura.md) (hospedagem e ngrok); [desenvolvimento.md](desenvolvimento.md) (editorial) |

**Projetos de software de Nicolas Oliveira:** [R2 Desktop Companion](https://github.com/nicolasgrotto/r2-desktop-companion) e [Duel of Fates](https://github.com/nicolasgrotto/duel-of-fates).

## 2. Matriz RACI

Legenda: **R** (*Responsible*) = executa a atividade; **A** (*Accountable*) = responde pela entrega; **C** (*Consulted*) = participa das discussões, decisões e validações. Quem executa ou responde por uma atividade também a discute e valida, por isso o **C** aparece em todas as células.

| # | Atividade | Heitor Resende | Gabriel Cardoso | Nicolas Egea | Nicolas Oliveira |
| :---: | --- | :---: | :---: | :---: | :---: |
| 1 | Planejamento e arquitetura do casemod | **R, A, C** | C | C | C |
| 2 | Construção física da estrutura | **R, A, C** | C | C | C |
| 3 | Montagem e integração do hardware ao casemod, e testes de validação | **R, A, C** | **R, A, C** | **R, A, C** | **R, A, C** |
| 4 | Instalação e configuração dos sistemas operacionais | C | **R, A, C** | **R, A, C** | C |
| 5 | Particionamento do SSD e ambiente Linux (†) | C | **R, A, C** | **R, A, C** | C |
| 6 | Configurações de cibersegurança | C | **R, A, C** | **R, A, C** | C |
| 7 | Desenvolvimento do R2 Desktop Companion | C | C | C | **R, A, C** |
| 8 | Desenvolvimento do Duel of Fates | C | C | C | **R, A, C** |
| 9 | Configuração das máquinas virtuais (VirtualBox) e do Windows Server 2022 | **R, A, C** | C | C | C |
| 10 | Hospedagem do Duel of Fates (IIS) e acesso externo (ngrok) | C | C | C | **R, A, C** |
| 11 | Documentação por área (veja abaixo) | **R, A, C** (arquitetura; VMs e Windows Server) | **R, A, C** (hardware, sistemas e segurança) | **R, A, C** (hardware, sistemas e segurança) | **R, A, C** (hospedagem e desenvolvimento) |

(†) O dual boot não foi implementado: por uma mudança de última hora, o Linux (Parrot) roda em VM ([software-e-infraestrutura.md](software-e-infraestrutura.md#4-dual-boot)).

**Atividade 3:** todos ajudaram na montagem e integração do hardware, no dia, e nos testes para validar o conjunto.

**Atividade 6:** Gabriel Cardoso e Nicolas Egea executam (R) e respondem (A). Nicolas Oliveira colaborou (C).

**Atividade 11 (documentação por área):** cada integrante é responsável pela redação do documento da sua área e consulta os demais.
