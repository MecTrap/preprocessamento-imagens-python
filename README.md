# Pipeline — Pré-processamento de Imagens

## 1. Visão geral

Este documento apresenta a pipeline didática utilizada no projeto de **pré-processamento de imagens do dataset Fruits-262**.

A pipeline representa as principais etapas executadas pelo projeto, desde a obtenção do dataset até a geração das imagens processadas.

O fluxo principal é:

```text
┌─────────────────────────┐
│  1. Obter o Dataset     │
│       Fruits-262        │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  2. Configurar o        │
│       caminho           │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  3. Localizar categorias│
│       e imagens         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  4. Redimensionar       │
│       mantendo          │
│       proporção         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  5. Criar imagem        │
│       300 × 300         │
│       transparente      │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  6. Centralizar imagem  │
│       processada        │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  7. Salvar como PNG     │
└─────────────────────────┘
```

---

## 2. Objetivo

O objetivo do projeto é realizar o pré-processamento das imagens do dataset Fruits-262   , deixando todas as imagens em um padrão de tamanho de **300 × 300 pixels**, sem distorcer ou cortar o conteúdo original.

Para isso, a imagem é redimensionada proporcionalmente e depois posicionada no centro de uma nova imagem de 300 × 300 pixels com fundo transparente.

---

## 3. Tecnologias utilizadas

| Tecnologia    | Função                                              |
| ------------- | --------------------------------------------------- |
| Python        | Desenvolvimento do projeto                          |
| Pillow        | Leitura, redimensionamento e salvamento das imagens |
| pathlib       | Navegação e manipulação de arquivos e diretórios    |
| python-dotenv | Leitura das configurações do arquivo `.env`         |
| os            | Acesso às variáveis de ambiente                     |
| KaggleHub     | Download do dataset                                 |

> `os` faz parte da biblioteca padrão do Python e, portanto, não precisa ser instalado separadamente.

---

# 4. Etapas da Pipeline

## 4.1 Obtenção do Dataset

O primeiro passo consiste em obter o dataset **Fruits-262**, que contém imagens organizadas em diferentes categorias de frutas.

O projeto possui o arquivo:

```text
baixar_dataset.py
```

Esse script utiliza o KaggleHub para realizar o download do dataset.

```text
Kaggle
   │
   ▼
Fruits-262
   │
   ▼
Download
   │
   ▼
Dataset disponível localmente
```

---

## 4.2 Configuração do caminho

Após obter o dataset, é necessário informar ao programa onde as imagens estão armazenadas.

Essa configuração é realizada por meio do arquivo:

```text
.env
```

A variável utilizada pelo projeto é:

```text
path_pictures
```

Exemplo:

```env
path_pictures=C:/caminho/para/Fruits-262
```

O uso de uma variável de ambiente evita que o caminho absoluto do dataset precise ficar diretamente escrito no código.

---

## 4.3 Localização das imagens

Com o caminho configurado, o programa percorre os diretórios do dataset.

O processo pode ser representado assim:

```text
Dataset
   │
   ├── Categoria 1
   │      ├── imagem 1
   │      ├── imagem 2
   │      └── ...
   │
   ├── Categoria 2
   │      ├── imagem 1
   │      ├── imagem 2
   │      └── ...
   │
   └── ...
```

O programa identifica as categorias existentes e posteriormente localiza as imagens dentro delas.

---

## 4.4 Redimensionamento

Cada imagem encontrada passa pelo processo de redimensionamento.

O limite utilizado é:

```text
300 × 300 pixels
```

O redimensionamento mantém a proporção original da imagem.

### Exemplo

Uma imagem de:

```text
1200 × 800
```

pode ser redimensionada para:

```text
300 × 200
```

A imagem não é esticada nem comprimida de maneira diferente em cada eixo.

Outro exemplo:

```text
600 × 1200
```

pode se tornar:

```text
150 × 300
```

Assim, a proporção original é preservada.

---

## 4.5 Criação da área de 300 × 300

Depois do redimensionamento, o programa cria uma nova imagem com tamanho fixo:

```text
300 × 300 pixels
```

Essa nova imagem possui fundo transparente.

A finalidade dessa etapa é permitir que todas as imagens tenham exatamente o mesmo tamanho final.

```text
┌──────────────────────────┐
│                          │
│                          │
│       IMAGEM             │
│      PROCESSADA          │
│                          │
│                          │
└──────────────────────────┘

       300 × 300
```

---

## 4.6 Centralização

A imagem redimensionada é posicionada no centro da área de 300 × 300 pixels.

Por exemplo:

```text
Imagem redimensionada
300 × 200
```

será posicionada dentro de:

```text
Canvas
300 × 300
```

O resultado será aproximadamente:

```text
┌─────────────────────────┐
│                         │
├─────────────────────────┤
│      IMAGEM 300 × 200   │
├─────────────────────────┤
│                         │
└─────────────────────────┘
```

As áreas que não são ocupadas pela imagem permanecem transparentes.

---

## 4.7 Salvamento

Após o processamento, a imagem final é salva no formato:

```text
PNG
```

O arquivo processado é armazenado no local definido pelo projeto.

O resultado pode ser representado por:

```text
Imagem original
       │
       ▼
Redimensionamento
       │
       ▼
Canvas 300 × 300
       │
       ▼
Centralização
       │
       ▼
Arquivo PNG
```

---

# 5. Fluxo completo

A pipeline completa do projeto pode ser resumida em:

```text
                 INÍCIO
                    │
                    ▼
          ┌──────────────────┐
          │ Obter Fruits-262 │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Configurar .env  │
          │ path_pictures    │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Localizar        │
          │ categorias       │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Localizar        │
          │ imagens          │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Redimensionar    │
          │ mantendo         │
          │ proporção        │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Criar canvas     │
          │ 300 × 300        │
          │ transparente     │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Centralizar      │
          │ imagem           │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │ Salvar como PNG  │
          └────────┬─────────┘
                   │
                   ▼
                  FIM
```

---

# 6. Entrada e saída

## Entrada

A pipeline recebe:

* Dataset Fruits-262;
* Caminho do dataset configurado no `.env`;
* Imagens organizadas em suas respectivas categorias.

## Processamento

As imagens passam por:

1. Localização;
2. Leitura;
3. Redimensionamento proporcional;
4. Criação de uma área de 300 × 300 pixels;
5. Centralização;
6. Preparação para salvamento.

## Saída

O resultado é uma imagem:

```text
300 × 300 pixels
```

em formato:

```text
PNG
```

com a imagem original preservada proporcionalmente e as áreas restantes transparentes.

---

# 7. Exemplo visual

### Antes

```text
Imagem original

┌──────────────────────────────┐
│                              │
│          FRUTA               │
│                              │
└──────────────────────────────┘

1200 × 800 pixels
```

### Durante o processamento

```text
        Redimensionamento
               │
               ▼
       Mantém proporção
               │
               ▼
       Cria área 300 × 300
               │
               ▼
       Centraliza a imagem
```

### Depois

```text
┌───────────────────────────┐
│                           │
│        FRUTA              │
│                           │
│                           │
└───────────────────────────┘

300 × 300 pixels
PNG
```

---

# 8. Por que utilizar uma pipeline?

A divisão do processo em etapas facilita a compreensão e a organização do sistema.

Neste projeto, a pipeline permite visualizar claramente:

* De onde vêm os dados;
* Como as imagens são localizadas;
* Quais transformações são realizadas;
* Qual padrão é aplicado;
* Qual é o resultado final.

Além disso, uma estrutura de pipeline facilita futuras alterações no projeto, como adicionar novas etapas de processamento ou modificar o padrão das imagens.

---

# 9. Possíveis melhorias futuras

A pipeline pode ser expandida futuramente com novas etapas, como:

```text
Dataset
   ↓
Validação
   ↓
Redimensionamento
   ↓
Remoção de ruído
   ↓
Normalização
   ↓
Padronização
   ↓
Armazenamento
```

Também seria possível integrar o projeto posteriormente a uma pipeline de CI/CD utilizando ferramentas de automação.

Essas melhorias não fazem parte da pipeline atual e são apresentadas apenas como possibilidades de evolução.

---

# 10. Conclusão

A pipeline organiza o fluxo de pré-processamento das imagens do Fruits-262 em etapas simples e sequenciais.

O processo começa com a obtenção e configuração do dataset, passa pela localização e processamento das imagens e termina com a geração de arquivos PNG padronizados em uma área de 300 × 300 pixels.

A utilização dessa estrutura facilita a compreensão do funcionamento do projeto e demonstra como um problema de processamento de imagens pode ser dividido em etapas bem definidas.

---

## Resumo da Pipeline

```text
Fruits-262
    ↓
Configuração do caminho
    ↓
Localização das imagens
    ↓
Redimensionamento proporcional
    ↓
Canvas transparente 300 × 300
    ↓
Centralização
    ↓
Salvamento em PNG
    ↓
Imagem processada
```

**Fim da pipeline.**
