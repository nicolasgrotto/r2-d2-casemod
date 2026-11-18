# Documentação do R2-D2 Casemod

Esta pasta reúne a documentação do projeto acadêmico **R2-D2: Droid Interativo**, apresentado na EXPOTEC 2026 (UniFECAF, Campus Sede, Taboão da Serra/SP): um documento por área e os PDFs elaborados pela equipe.

← [Voltar ao README principal](../README.md)

**Última atualização:** 18/11/2026.

## Documentos

| Documento | Conteúdo | Responsável principal |
| --- | --- | --- |
| [arquitetura.md](arquitetura.md) | Conceito, estrutura externa e interna, dimensões, materiais, etapas de construção, desafios e soluções | Heitor Resende |
| [hardware.md](hardware.md) | Componentes do computador, especificações, montagem e integração ao casemod | Gabriel Cardoso e Nicolas Egea |
| [software-e-infraestrutura.md](software-e-infraestrutura.md) | Sistemas operacionais, particionamento, dual boot (substituído por VM), virtualização, Windows Server 2022, IIS, publicação do Duel of Fates e ngrok | Gabriel Cardoso e Nicolas Egea (Parte I); Heitor Resende (VMs e Windows Server 2022) e Nicolas Oliveira (IIS e ngrok) (Parte II) |
| [seguranca.md](seguranca.md) | Medidas de cibersegurança, auditoria com Nmap, hardening, riscos e recomendações | Gabriel Cardoso e Nicolas Egea |
| [desenvolvimento.md](desenvolvimento.md) | Evolução cronológica do projeto, desenvolvimento dos softwares, integração e resultado | Nicolas Oliveira (editorial), com os demais integrantes |
| [equipe.md](equipe.md) | Integrantes, responsabilidades e matriz RACI | Todos |

Todos os integrantes participaram do projeto; "responsável principal" indica a área em que cada um liderou.

## Documentos em PDF

Os PDFs elaborados pela equipe ficam em [`pdfs/`](pdfs/).

| Arquivo | Páginas | Conteúdo | Documento relacionado |
| --- | :---: | --- | --- |
| [Ficha_Tecnica_R2-D2.pdf](pdfs/Ficha_Tecnica_R2-D2.pdf) | 4 | Especificações do hardware, particionamento do SSD, hipervisor e máquinas virtuais | [hardware.md](hardware.md), [software-e-infraestrutura.md](software-e-infraestrutura.md) |
| [Cyber_R2-D2.pdf](pdfs/Cyber_R2-D2.pdf) | 8 | Segurança cibernética e hardening: medidas preventivas, regra do ngrok, varreduras Nmap, RDP com NLA, regra de firewall e tríade CIA | [seguranca.md](seguranca.md) |
| [Arquitetura_R2-D2.pdf](pdfs/Arquitetura_R2-D2.pdf) | 12 | Construção do casemod, 16 figuras, medidas, materiais e ferramentas | [arquitetura.md](arquitetura.md), [hardware.md](hardware.md) |

## Organização dos materiais

```text
R2-D2-Casemod/
├── README.md                      Apresentação do projeto
├── docs/
│   ├── README.md                  Este índice
│   ├── arquitetura.md
│   ├── hardware.md
│   ├── software-e-infraestrutura.md
│   ├── seguranca.md
│   ├── desenvolvimento.md
│   ├── equipe.md
│   └── pdfs/                      PDFs da equipe
└── assets/
    └── images/
        ├── casemod/               Fotografias do casemod pronto (8 arquivos)
        └── construcao/            Figuras 1 a 16 da construção (fig-01.jpg a fig-16.jpg)
```

- **`assets/images/casemod/`** contém as fotografias do casemod concluído, usadas na galeria do README.
- **`assets/images/construcao/`** contém as figuras da construção, numeradas de 1 a 16.
- Os diagramas são escritos em **Mermaid** dentro dos próprios documentos, e por isso não há pasta separada de diagramas.

## Convenções

- Os projetos de software têm documentação própria em seus repositórios: [R2 Desktop Companion](https://github.com/nicolasgrotto/r2-desktop-companion) e [Duel of Fates](https://github.com/nicolasgrotto/duel-of-fates). Aqui documentamos apenas sua relação com o casemod.
