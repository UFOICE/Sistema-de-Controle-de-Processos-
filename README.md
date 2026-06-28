# Sistema de Controle de Processos Físicos - SFPC (Controle de Fluxo)
**Disciplina:** Programação Aplicada  
**Curso:** Engenharia de Computação - Centro Universitário SATC  
**Objetivo:** Automatizar e rastrear a tramitação de processos físicos no setor do SFPC utilizando o paradigma de Programação Orientada a Objetos (POO) em C++.

---

## 1. Justificativa: POO vs. Programação Estruturada

O objetivo central deste projeto é demonstrar as vantagens da POO sobre a programação estruturada tradicional no gerenciamento de fluxos complexos:

* **Na Programação Estruturada:** Para gerenciar os processos, precisaríamos de múltiplas matrizes ou vetores globais separados (um para protocolos, um para responsáveis, um para status). As funções modificariam esses dados diretamente de qualquer lugar do código, gerando alto risco de corrupção de dados (por exemplo, alterar o status de um processo para uma fase inexistente por acidente).
* **Na Programação Orientada a Objetos (POO):** Cada processo é tratado como uma entidade autônoma e blindada (Objeto). O estado do processo (número de protocolo, responsável, etapa atual) é **encapsulado**. Nenhuma função externa pode modificar o status de um processo de forma arbitrária; toda transição de fase deve passar obrigatoriamente pelos métodos validadores da classe, garantindo a integridade da fila do SFPC.

---

## 2. Diagrama de Classes (UML)

O sistema foi modelado utilizando duas classes principais com responsabilidades bem definidas, reduzindo o acoplamento do código.

```mermaid
classDiagram
    class Processo {
        - string numeroProtocolo
        - string registradoPor
        - string status
        + Processo(string protocolo, string militarResponsavel)
        + getProtocolo() string
        + getRegistradoPor() string
        + getStatus() string
        + setStatus(string novoStatus) void
        + exibirDados() void
    }

    class GerenciadorProcessos {
        - vector~Processo~ listaProcessos
        + registrarProcesso() void
        + listarPorStatus(string statusAlvo) void
        + atualizarStatusProcesso() void
        + exibirTodos() void
    }

    GerenciadorProcessos "1" --> "*" Processo : Gerencia e armazena
