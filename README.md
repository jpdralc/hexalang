# HEXALANG

O **HexaLang** é uma linguagem inspirada no futebol que transpila arquivos `.hexa` para Python.

A saída do código .hexa, ao ser transpilado, contém:
* Narração de voz (TTS)
* Sons de torcida (Vinhetas clássicas das rádios brasileiras que tem 10% de chance de tocarem a cada saída no terminal)
* Efeito máquina de escrever

---

# Estrutura do Projeto

```txt
HEXALANG/
│
├── audios/                 # Sons usados pelo sistema
│
├── hexa_scripts/           # Scripts .hexa
│   ├── hello.hexa
│   ├── jogo.hexa
│   ├── cervejas.hexa
│   └── ...
│
├── hexa_to_python/         # Python gerado automaticamente
│
├── utils/
│   ├── view_windows_language.py
│
├── hexalang.py             # Transpilador
├── hexa.bat                # Executor automático
│
└── README.md
```

---

# Requisitos

## Python
```txt
3.10.x < Python < 3.14.x
```

Baixe em:

https://www.python.org/downloads/

---

# Instalação das Dependências

O HexaLang usa:

* **[pywin32](https://pypi.org/project/pywin32/):** Necessária para fazer a ponte entre o Python e o sistema de voz nativo do Windows (SAPI5). É essa biblioteca que permite que a linguagem `.hexa` "ganhe voz" e narre a execução do código como um verdadeiro locutor esportivo, tudo localmente e sem precisar de internet.

Rode esse comando: 
```bash
 pip install pywin32
```

# Rode os códigos existentes:

```bash
 ./hexa.bat ./hexa_scripts/cerveja.hexa
```

```bash
 ./hexa.bat ./hexa_scripts/hello.hexa
```

```bash
 ./hexa.bat ./hexa_scripts/jogo.hexa
```

```bash
 ./hexa.bat ./hexa_scripts/inputs.hexa
```

## Dicionário da Linguagem

Abaixo estão as palavras reservadas da linguagem e como elas são traduzidas "por debaixo dos panos" para o Python.
### 📢 Saídas de Texto e Áudio (Outputs)

| Sintaxe .hexa | O que faz | Equivalente em Python |
| :--- | :--- | :--- |
| `apita o árbitro` | Inicia o código, tipo um begin | `print("apita o árbitro")` |
| `fim de papo` | Encerra o código | `print("fim de papo")` |
| `a torcida canta "texto"` | Imprime o texto especificado | `print("texto")` |
| `a torcida conta [var]` | Lê o valor da variável em velocidade acelerada | `narrate_fast([var])` |
| `torcida grita [var]` | Imprime o valor de uma variável | `print([var])` |
| `o estadio grita [var]` | Imprime o valor de uma variável em destaque | `print([var])` |

### 📥 Variáveis e Entrada de Dados (Inputs)

| Sintaxe .hexa | O que faz | Equivalente em Python |
| :--- | :--- | :--- |
| `camisa [valor] [var]` | Declara uma variável numérica inteira | `var = valor` |
| `odd [valor] [var]` | Declara uma variável numérica decimal | `var = valor` |
| `[var] é "texto"` | Declara uma variável de texto (String) | `var = "texto"` |
| `[var] responde a pergunta "texto"` | Pede uma entrada de dados ao usuário | `var = input("texto")` |

### ➕ Operadores Matemáticos

| Sintaxe .hexa | O que faz | Equivalente em Python |
| :--- | :--- | :--- |
| `[var] vai mais [valor]` | Soma um valor à variável existente | `var += valor` |
| `[var] vai menos [valor]` | Subtrai um valor da variável existente | `var -= valor` |

### ⚖️ Estruturas de Condição e Repetição

| Sintaxe .hexa | O que faz | Equivalente em Python |
| :--- | :--- | :--- |
| `chama o var pra ver se [condição]` | Cria um bloco condicional | `if condicao:` |
| `vamos as opcoes do banco [var]` | Cria um bloco de múltipla escolha | `match var:` |
| `se entrar o [valor]:` | Define uma das opções da múltipla escolha | `case valor:` |
| `enquanto [condição]` | Cria um laço de repetição | `while condicao:` |
| `...` *(no fim da linha)* | Pula para a próxima iteração do laço | `continue` |
| `.` *(no fim da linha)* | Interrompe o laço imediatamente | `break` |

### 🆚 Operadores de Comparação

| Sintaxe .hexa | O que faz | Equivalente em Python |
| :--- | :--- | :--- |
| `é igual a` | Verifica se dois valores são iguais | `==` |
| `é maior que` | Verifica se o valor da esquerda é maior | `>` |
| `é menor que` | Verifica se o valor da esquerda é menor | `<` |

Crie um código em Hexa

```txt
apita o árbitro

camisa 0 gols

a torcida canta "O jogo começou!"

enquanto gols é menor que 5
    a torcida conta gols
    gols vai mais 1
...

fim de papo
```

Salve como:

```txt
meu_codigo.hexa
```

---

## 2. Execute usando o `hexa.bat`

Dentro da pasta do projeto:

```bash
 ./hexa.bat ./hexa_scripts/meu_codigo.hexa
```

O sistema irá:

1. Transpilar `.hexa` → `.py`
2. Executar o Python automaticamente
3. Narrar o código com voz e sons

---

# Importante

O `hexa.bat` funciona apenas dentro da pasta do projeto.

Se quiser executar manualmente fora dela:

## 1. Transpile

```bash
python hexalang.py arquivo.hexa
```

## 2. Execute o Python gerado

```bash
python arquivo.py
```
---

# Sistema de Áudio

A cada saída do código existe uma chance de 10% de tocar uma vinheta aleatória.

Os sons ficam em:

```txt
audios/
```

Você pode adicionar novos arquivos `.wav`.

Exemplo:

```txt
audios/meu_audio.wav
```

---

# Como Funciona

```txt
Arquivo .hexa
      ↓
Transpilador Python
      ↓
Arquivo .py gerado
      ↓
Execução
      ↓
Narração + Sons + Texto
```

---


## OPCIONAL: Caso seu código esteja sendo narrado em inglês, siga esse passo a passo pra instalar a voz em PT-BR:

Pré-requisitos

* Windows 10 ou 11
* PowerShell como Administrador
* Internet

---

## Instalar Voz PT-BR

Abra o **PowerShell como Administrador** e execute:

```powershell
Add-WindowsCapability -Online -Name Language.TextToSpeech~~~pt-BR~0.0.1.0
```

---

## Habilitar a voz no SAPI5

Execute os comandos abaixo linha por linha:

```powershell
$source = "HKLM:\SOFTWARE\Microsoft\Speech_OneCore\Voices\Tokens\MSTTS_V110_ptBR_MariaM"

$dest = "HKLM:\SOFTWARE\Microsoft\Speech\Voices\Tokens\MSTTS_V110_ptBR_MariaM"

Copy-Item -Path $source -Destination $dest -Recurse -Force
```

---

## Verificar instalação

Na pasta do projeto execute:

```bash
python .\utils\view_windows_language.py
```

Resultado esperado:

```txt
Microsoft Maria - Portuguese (Brazil)
```

---

