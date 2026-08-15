# PackMaker
<div align="center">

<!-- Logo Placeholder: Substitua o link abaixo pela URL do logo oficial do PackMaker -->
<img src="https://via.placeholder.com/200/24292E/FFFFFF?text=PackMaker+Logo" alt="PackMaker Logo" width="180"/>

# PackMaker

**Do código ao instalador com o mínimo de intervenção manual.**  
*Transforme projetos Python e executáveis portáteis em aplicativos e instaladores nativos para Windows de forma automatizada e direta.*

[![Status](https://img.shields.io/badge/Status-Beta-blue.svg?style=flat-square)](https://github.com/seu-usuario/PackMaker)
[![Plataforma](https://img.shields.io/badge/OS-Windows_10_|_11-lightgrey.svg?style=flat-square&logo=windows)](https://github.com/seu-usuario/PackMaker)
[![Licença](https://img.shields.io/badge/Licença-Consulte-green.svg?style=flat-square)](#licença)

<br>

[Visão Geral](#visão-geral) • 
[Fluxos de Trabalho](#fluxos-de-trabalho) • 
[Arquitetura](#arquitetura-e-funcionamento) • 
[Instalação](#requisitos-e-instalação) • 
[Roadmap](#estado-do-projeto-e-edição-pro)

</div>

---

## Visão Geral

O **PackMaker** é uma ferramenta de automação para o ecossistema Windows focada em simplificar a geração e distribuição de software. O projeto elimina a necessidade de manutenção de scripts complexos ou configuração manual de cadeias de empacotamento.

A edição gratuita oferece um fluxo focado na produtividade: ao selecionar um projeto e definir as configurações primárias, a ferramenta gerencia automaticamente as etapas de compilação e criação do instalador.

### Principais Funcionalidades

*   **Conversão Direta:** Transforma scripts e projetos Python em executáveis (`.exe`) autônomos.
*   **Geração de Instaladores:** Cria instaladores `Setup.exe` ou pacotes `.MSI` diretamente a partir de código-fonte ou executáveis pré-compilados.
*   **Resolução Automática de Dependências:** Na ausência de um arquivo `requirements.txt`, o sistema analisa estaticamente os imports do projeto para inferir e preparar os pacotes necessários.
*   **Configuração Centralizada:** Permite a definição de metadados do aplicativo (Nome, Versão, Fabricante, Ícones) e parametrização de atalhos.
*   **Otimização de Build:** Utiliza sistema de cache e armazenamento local de componentes para acelerar compilações subsequentes.
*   **Diagnóstico Sob Demanda:** Mantém o isolamento da complexidade técnica do usuário final, disponibilizando logs técnicos detalhados apenas quando necessário para auditoria ou debugging.

---

## Fluxos de Trabalho

O sistema adapta-se dinamicamente ao tipo de artefato de entrada fornecido:

| Artefato de Entrada | Saída Gerada | Descrição do Processo |
| :--- | :--- | :--- |
| **Projeto Python** | **EXE Portátil** | Conversão do código-fonte e dependências em um binário autônomo. |
| **Projeto Python** | **MSI** | Empacotamento completo em formato Windows Installer (foco corporativo). |
| **Projeto Python** | **Setup EXE** | Geração de instalador interativo padrão para o usuário final. |
| **EXE Pré-compilado** | **MSI** | Encapsulamento de um binário existente em um instalador MSI. |
| **EXE Pré-compilado** | **Setup EXE** | Encapsulamento de um binário existente em um instalador executável. |

---

## Arquitetura e Funcionamento

O design do PackMaker visa abstrair a complexidade subjacente entre o desenvolvimento do código e a distribuição final.

<div align="center">

```mermaid
graph LR
    A[Projeto/Executável] -->|Análise| B(PackMaker)
    B -->|Preparação de Ambiente| C{Auto-Build}
    C -->|Compilação| D[Binário Windows]
    D -->|Empacotamento| E((Instalador Final))
    
    style B fill:#24292E,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#0366D6,stroke:#333,stroke-width:2px,color:#fff
