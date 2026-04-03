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

## 📚 Glossário: C# – Fundamentos da Linguagem

## **1. C# – Fundamentos da Linguagem**

### **1. Variáveis e Tipos de Dados**

#### 1.1. Tipos de Dados Primitivos
- Integrais (`int`, `long`, `short`, `byte`)
- Ponto flutuante (`float`, `double`, `decimal`)
- Caractere (`char`)
- Booleano (`bool`)

#### 1.2. Tipos de Dados por Referência e Personalizados
##### 1.2.1. Classes
##### 1.2.2. Structs
##### 1.2.3. Interfaces
##### 1.2.4. Enums
##### 1.2.5. Records
##### 1.2.6. required

#### 1.3. Tipos Anuláveis (Nullable)
##### 1.3.1. Tipos de valor anuláveis (`int?`)
##### 1.3.2. Nullable Reference Types (`string` vs `string?`)
##### 1.3.3. Análises e avisos do compilador

#### 1.4. Operadores
##### 1.4.1. Aritméticos
##### 1.4.2. Lógicos
##### 1.4.3. Relacionais
##### 1.4.4. Operadores nulos (`??`, `?.`, `!`)

#### 1.5. Conversão de Tipos
##### 1.5.1. Conversão implícita e explícita (cast)
##### 1.5.2. Classe `Convert`
##### 1.5.3. `Parse` e `TryParse`

---

## **2. Estruturas de Controle de Fluxo**

### 2.1. Condicionais
#### 2.1.1. `if`
#### 2.1.2. `if / else`
#### 2.1.3. `switch`
#### 2.1.4. `switch expression`

### 2.2. Laços de Repetição
#### 2.2.1. `for`
#### 2.2.2. `while`
#### 2.2.3. `do…while`
#### 2.2.4. `foreach`
#### 2.2.5. `List Patterns`
#### 2.2.6. `pan Pattern Matching`

### 2.3. Controle de Fluxo
#### 2.3.1. `break`
#### 2.3.2. `continue`
#### 2.3.3. `return`

---

## **3. Métodos e Funções**

### 3.1. Declaração de Métodos
### 3.2. Métodos com Retorno
### 3.3. Métodos `void`

### 3.4. Parâmetros
#### 3.4.1. Parâmetros por valor
#### 3.4.2. `ref`, `out`, `in`
#### 3.4.3. Parâmetros opcionais
#### 3.4.4. Named Parameters

### 3.5. Métodos Recursivos
### 3.6. Métodos Estáticos x Métodos de Instância

---

## **4. Arrays e Estruturas Sequenciais**

### 4.1. Declaração e Inicialização
### 4.2. Arrays Multidimensionais
### 4.3. Arrays Irregulares (Jagged Arrays)

### 4.4. Operações com Arrays
#### 4.4.1. Iteração
#### 4.4.2. Ordenação
#### 4.4.3. Busca

---

## **5. Classes e Objetos**

### 5.1. Declaração de Classes

### 5.2. Propriedades
#### 5.2.1. Auto-properties
#### 5.2.2. Propriedades somente leitura
#### 5.2.3. Propriedades imutáveis

### 5.3. Métodos
#### 5.3.1. Sobrecarga de Métodos
#### 5.3.2. Retorno de Objetos

### 5.4. Construtores
#### 5.4.1. Construtor padrão
#### 5.4.2. Sobrecarga de Construtores

### 5.5. Palavra-chave `this`
### 5.6. Sobrecarga de Operadores

---

## **6. Herança**

### 6.1. Classes Base e Derivadas
### 6.2. Palavra-chave `base`
### 6.3. Ordem de Execução de Construtores
### 6.4. Métodos `virtual`, `override`
### 6.5. Uso de `sealed`

---

## **7. Polimorfismo**

### 7.1. Polimorfismo de Sobrecarga
### 7.2. Polimorfismo de Substituição

---

## **8. Encapsulamento**

### 8.1. Modificadores de Acesso
- `public`
- `private`
- `protected`
- `internal`
- `protected internal`
- `private protected`

### 8.2. Propriedades (`get` / `set`)
### 8.3. Indexadores

---

## **9. Delegates e Eventos**

### 9.1. Delegates
#### 9.1.1. Delegate customizado
#### 9.1.2. Multicast Delegate
#### 9.1.3. `Func`, `Action`, `Predicate`

### 9.2. Eventos
#### 9.2.1. Declaração de Eventos
#### 9.2.2. Assinatura e Disparo
#### 9.2.3. Padrão Observer

---

## **10. Interfaces**

### 10.1. Declaração
### 10.2. Implementação
### 10.3. Múltiplas Interfaces
### 10.4. Métodos Default

---

## **11. Tratamento de Exceções**

### 11.1. `try / catch / finally`
### 11.2. Lançamento de Exceções
#### 11.2.1. `throw`
### 11.3. Hierarquia de Exceções
### 11.4. Exceções Personalizadas
### 11.5. Inner Exception
### 11.6. Filtros de Exceção (`when`)

---

## **12. Coleções**

### 12.1. `List<T>`
### 12.2. `Dictionary<TKey, TValue>`
### 12.3. `LinkedList<T>`
### 12.4. `Queue<T>`
### 12.5. `Stack<T>`
### 12.6. `HashSet<T>`
### 12.6. `Collection Expressions`

### 12.7. Coleções Concorrentes
- `ConcurrentDictionary`
- `ConcurrentQueue`
- `ConcurrentBag`

---

## **13. LINQ**

### 13.1. Conceitos
#### 13.1.1. Execução tardia (Deferred execution)
#### 13.1.2. Execução imediata

### 13.2. Operadores
#### 13.2.1. `Where`
#### 13.2.2. `Select`
#### 13.2.3. `GroupBy`
#### 13.2.4. `OrderBy`

### 13.3. Operadores de Conjunto
#### 13.3.1. `Union`
#### 13.3.2. `Intersect`
#### 13.3.3. `Except`

---

## **14. Expressões Lambda**

### 14.1. Sintaxe
### 14.2. Uso com Delegates
### 14.3. Uso com LINQ

---

## **15. Programação Assíncrona**

### 15.1. `async / await`
### 15.2. `Task` e `ValueTask`
### 15.3. Cancelamento (`CancellationToken`)
### 15.4. Async Enumerable & IAsyncDisposable
### 15.5. Task.WaitAsync

---

## **16. Concorrência e Paralelismo**

### 16.1. Concorrência x Paralelismo
### 16.2. `lock`
### 16.3. `Monitor`
### 16.4. `Semaphore`
### 16.5. `SemaphoreSlim`

---

## **17. Gerenciamento de Memória**

### 17.1. Stack x Heap
### 17.2. Value Types x Reference Types
### 17.3. Garbage Collector (.NET)
### 17.4. Imutabilidade
### 17.5. Pooling de Objetos
### 17.6. Tipos Avançados de Memória
#### 17.6.1. `Span<T>`
#### 17.6.2. `ReadOnlySpan<T>`
#### 17.6.3. `Memory<T>`
#### 17.6.4. `Inline Arrays`
#### 17.6.5. `Ref Fields e Scoped Ref`

---

## **18. Datas, Horários e Tempo**

### 18.1. `DateTime`
### 18.2. `DateTimeOffset`
### 18.3. UTC x Local
### 18.4. TimeZone

---

## **19. Serialização**

### 19.1. Serialização JSON
### 19.2. Custom Converters
### 19.3. Versionamento de Contratos

---

## **20. Logging e Diagnóstico**

### 20.1. Conceitos de Logging
### 20.2. Níveis de Log
### 20.3. Correlação de Eventos

---

## **21. C# – Manipulação de Arquivos**

## 2122.1. Leitura e Escrita**

### 21.1.1. Arquivos de Texto
### 21.1.2. Arquivos Binários

## **21.2. Diretórios**
### 21.2.1. Criação e Remoção
### 21.2.2. Navegação
### 21.2.3. Verificação
### 21.2.4. Listagem

## **21.3. XML**
### 21.3.1. Leitura
### 21.3.2. Escrita
### 21.3.3. Modificação
### 21.3.4. Validação
### 21.3.5. Transformações

## **21.4. JSON**
### 21.4.1. Leitura
### 21.4.2. Escrita
### 21.4.3. Modificação
### 21.4.4. Validação
### 21.4.5. Serialização de Objetos

---

## **22. C# – Manipulação de Dados**

## **22.1. Conceitos de Banco de Dados**
### 22.1.1. Relacional
### 22.1.2. Transações
### 22.1.3. Normalização




Happy Coding! — Edson Lopes