# C# 10+ Study Lab 🚀

Repositório dedicado ao estudo das funcionalidades do C# e ecossistema .NET, focado em File-Based Execution (execução baseada em arquivos). O objetivo aqui é eliminar o overhead de criação de projetos (.csproj) e focar estritamente na sintaxe e lógica da linguagem.

## 🛠 Requisitos de Ambiente

- **Runtime/SDK**: .NET 10 SDK (ou superior).
- **Editor Sugerido**: VS Code ou qualquer editor de texto leve.
- **SO**: Cross-platform (Windows, Linux, macOS).

## 🚀 Como Executar

Diferente das versões legadas do .NET, a partir da versão 10 você pode tratar arquivos .cs como scripts independentes, similar ao Node.js ou Python.

Para rodar qualquer arquivo deste repositório, utilize o terminal na raiz da pasta:

```bash
dotnet <nome-do-arquivo>.cs
```

### Exemplo Prático

Se você tem um arquivo `InterpolacaoStrings.cs`, basta executar:

```bash
dotnet InterpolacaoStrings.cs
```

## 🏗 Estrutura do Código (Top-Level Statements)

Os arquivos neste repositório utilizam Top-Level Statements. Isso significa que você não encontrará a cerimônia clássica de namespace, class Program e static void Main.

Anatomia de um arquivo de estudo:

```csharp
// 1. Imports (se necessário)
using System.Linq;

// 2. Lógica direta (O compilador gera o entry point automaticamente)
var stack = new[] { "C#", ".NET", "Cloud" };
Console.WriteLine($"Estudando: {string.Join(" -> ", stack)}");

// 3. Definições de tipos (opcional, sempre ao final do arquivo)
public record Dev(string Nome, string Nivel);
```

## 📊 Análise Técnica: Por que estudar assim?

| Funcionalidade          | Implementação Legada (< .NET 10) | Implementação Atual (.NET 10+) |
|-------------------------|----------------------------------|-------------------------------|
| Setup                  | `dotnet new console -n Nome`     | `touch arquivo.cs`            |
| Metadados              | Exige arquivo .csproj (XML)      | Apenas código C# puro         |
| Dependências           | `dotnet add package <nome>`      | Diretiva `#r "nuget: <nome>"` inline |
| Fricção                | Alta (gera pastas bin/obj/ etc)  | Baixa (foco no algoritmo)     |

## 📝 Notas de Arquitetura

- **Implicit Usings**: O runtime já injeta namespaces fundamentais como `System` e `System.Collections.Generic`. Você só precisa declarar `using` para bibliotecas específicas.
- **Scoping**: Variáveis declaradas no escopo global do arquivo são tratadas como variáveis locais do método Main gerado implicitamente.
- **NuGet Inline**: Para testar libs externas sem criar projetos, utilize a sintaxe de referência no topo do arquivo:

```csharp
#r "nuget: Newtonsoft.Json, 13.0.3"
```

## 🛠 Guia de Setup: C# como Script Engine

Este guia detalha como configurar seu ambiente para executar arquivos `.cs` de forma isolada, eliminando a necessidade de criar projetos (`.csproj`) para cada teste, simulando a experiência do Node.js ou Python.

1. Requisito de Runtime
- Certifique-se de ter o SDK do .NET 10 (ou superior) instalado.
- Verifique no terminal:

```bash
dotnet --version
```

- Se a versão for inferior a 10, o suporte nativo a execução de arquivo único pode exigir o uso de `dotnet-script`.

2. Configurando o VS Code (Code Runner)

Para rodar o código com um único atalho (Ctrl + Alt + N), siga este passo a passo:

Passo A: Instalação da Extensão
- Abra o VS Code.
- Vá até a aba de Extensions (Ctrl + Shift + X).
- Procure por "Code Runner" (de Jun Han).
- Clique em Install.

Passo B: Acesso às Configurações JSON
- Pressione Ctrl + Shift + P para abrir a paleta de comandos.
- Digite: `Preferences: Open User Settings (JSON)` e pressione Enter.

Passo C: Configuração do Executor Map
- Dentro do seu `settings.json`, localize o objeto `code-runner.executorMap`. Se não existir, crie-o.
- Adicione ou substitua a linha do `csharp` pela configuração abaixo:

```json
"code-runner.executorMap": {
  "csharp": "cd $dir && dotnet $fileName"
}
```

Passo D: Melhorando a Experiência de Terminal (Recomendado)
- Para permitir interação com o teclado (`Console.ReadLine()`) e garantir que o código mais recente seja executado, adicione estas flags fora do `executorMap`:

```json
"code-runner.runInTerminal": true,
"code-runner.saveFileBeforeRun": true,
"code-runner.clearPreviousOutput": true
```

3. Segunda Opção: Execução Manual via Terminal

Caso você prefira não usar extensões ou precise rodar o script em um ambiente de servidor/CI, a execução manual segue o fluxo de "Zero Fricção":

- Navegue até a pasta onde o arquivo está:

```bash
cd "e:/Meu arquivos/Developer/workspace-estudos/..."
```

- Execute o arquivo diretamente:

```bash
dotnet EstudoStrings.cs
```

## 📋 Comparativo de Opções de Execução

| Característica | Code Runner (Atalho) | Terminal Manual |
|---------------|----------------------|----------------|
| Velocidade de Teste | ⚡ Alta (Um clique/atalho) | 🐢 Média (Exige digitar o comando) |
| Contexto de Erro | Excelente para depuração rápida | Melhor para visualizar logs extensos |
| Interatividade | Requer `runInTerminal: true` | Nativa |

## 🏗 Estrutura Sugerida de Estudo

Para manter seu repositório organizado enquanto aprende as novas funcionalidades do C# 14, utilize a estrutura de Top-Level Statements:

```csharp
// Nome: EstudoInterpolacao.cs
using System;

var tech = "C# 10+";
Console.WriteLine($"Explorando {tech} sem projetos complexos!");

// Tipos podem ser declarados ao final do arquivo
public record Dev(string Nome, string Especialidade);
```

> Nota de Arquitetura: Ao usar `cd $dir && dotnet $fileName`, estamos garantindo que o compilador JIT do .NET trate o escopo do arquivo atual como o EntryPoint da aplicação, ignorando qualquer outro arquivo `.cs` presente na mesma pasta que não seja referenciado.

Happy Coding! — Edson Lopes