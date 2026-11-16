# Documentação do R2-D2 Casemod

Esta pasta reúne a documentação oficial do projeto acadêmico **R2-D2: Droid Interativo**, apresentado na EXPOTEC 2026 (UniFECAF, Campus Sede, Taboão da Serra/SP). Os documentos Markdown organizam e consolidam as informações; os **PDFs originais da equipe** são a fonte primária e estão preservados sem alteração.

← [Voltar ao README principal](../README.md)

**Estado da documentação:** concluída. Última atualização: 15/11/2026.

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

## PDFs originais da equipe

Os PDFs ficam em [`pdfs/`](pdfs/). Foram copiados byte a byte (os hashes abaixo são idênticos aos dos arquivos entregues pela equipe). Apenas os nomes dos arquivos foram simplificados, sem acentos e sem a extensão dupla `.docx.pdf`, para funcionarem bem como links.

| Arquivo | Título original | Páginas | Descrição | Documento Markdown relacionado |
| --- | --- | :---: | --- | --- |
| [Ficha_Tecnica_R2-D2.pdf](pdfs/Ficha_Tecnica_R2-D2.pdf) | *R2-D2: Droid Interativo - Ficha Técnica* | 4 | Tabela com especificações do hardware, particionamento do SSD, hipervisor e máquinas virtuais | [hardware.md](hardware.md), [software-e-infraestrutura.md](software-e-infraestrutura.md) |
| [Cyber_R2-D2.pdf](pdfs/Cyber_R2-D2.pdf) | *R2-D2: Droid Interativo - Cyber* | 4 | Segurança cibernética e hardening: medidas preventivas, auditoria Nmap e regras de firewall | [seguranca.md](seguranca.md) |
| [Arquitetura_R2-D2.pdf](pdfs/Arquitetura_R2-D2.pdf) | *R2-D2: Droid Interativo - Arquitetura* | 12 | Confecção do casemod, 16 figuras, medidas, materiais e ferramentas | [arquitetura.md](arquitetura.md), [hardware.md](hardware.md) |

**Integridade (SHA-256):**

| Arquivo | SHA-256 |
| --- | --- |
| Ficha_Tecnica_R2-D2.pdf | `1fa457ebe4429da4e17c9404b7d97295e645352df1229e8be663d97e5a811ae6` |
| Cyber_R2-D2.pdf | `25ad727e25e148d6fe1de94dec1c6d8309fae84f2dfc0882471a78a7822407c8` |
| Arquitetura_R2-D2.pdf | `6372dc68a547a83eb4e790ff66793e9ba01c9124e76aa378ef588164e48ee7c7` |

Os três PDFs foram exportados do Google Docs e têm a mesma capa: Centro Universitário UniFECAF, Campus Sede, EXPOTEC, Taboão da Serra - SP, 2026. As versões editáveis (DOCX/Google Docs) ficam fora do repositório.

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
│   └── pdfs/                      PDFs originais da equipe (inalterados)
└── assets/
    └── images/
        ├── casemod/               Fotografias do casemod pronto (8 arquivos)
        └── construcao/            Figuras 1 a 16 do PDF de Arquitetura (fig-01.jpg a fig-16.jpg)
```

- **`assets/images/casemod/`** contém as fotografias do casemod concluído, usadas na galeria do README.
- **`assets/images/construcao/`** contém as figuras do PDF de Arquitetura, extraídas e salvas em JPEG, com numeração igual à do PDF.
- Os diagramas são escritos em **Mermaid** dentro dos próprios documentos, e por isso não há pasta separada de diagramas.

## Convenções

- **Dados sensíveis:** senhas, tokens, chaves, endereços IP reais e o endereço público do ngrok não são registrados nestes documentos.
- Os projetos de software têm documentação própria em seus repositórios: [R2 Desktop Companion](https://github.com/nicolasgrotto/r2-desktop-companion) e [Duel of Fates](https://github.com/nicolasgrotto/duel-of-fates). Aqui documentamos apenas sua relação com o casemod.
