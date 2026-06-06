# Predição de Câncer de Pâncreas via Expressão de miRNAs

Este projeto faz parte de um **Trabalho de Conclusão de Curso (TCC)** e tem como objetivo o **treinamento e predição de câncer de pâncreas** a partir da análise de **valores de expressão de microRNAs (miRNAs)** obtidos através de amostras de sangue.

O projeto utiliza uma arquitetura multimodelo e multiplataforma de **Machine Learning supervisionado**, aplicando paralelismo em GPU para modelos de larga escala e execuções tradicionais via CPU.

---

## 🎯 Objetivo do Projeto

- Analisar conjuntos de dados complexos de expressão de miRNAs.
- Mitigar o desbalanceamento severo de classes utilizando técnicas de oversampling.
- Selecionar características biológicas relevantes através de SHAP e importância por permutação.
- Treinar, avaliar e comparar múltiplos modelos de Machine Learning (CPU e GPU).
- Fornecer métricas consolidadas para auxílio no diagnóstico precoce do câncer de pâncreas.

---

## 🗂️ Estrutura Geral do Projeto

Abaixo está representada a árvore de diretórios do projeto organizada por modelo e hardware de execução:

```text
TCC/
├── Databases/                      # Conjuntos de dados brutos e processados
├── RandonForest - CPU/             # Pipeline Random Forest para execução em CPU
│   ├── models/                    # Modelos treinados salvos (.joblib)
│   ├── models_Tree/               # Exportação individual de árvores de decisão
│   ├── plots/                     # Gráficos gerados (Matplotlib)
│   └── RandonForest_CPU.ipynb     # Notebook principal CPU
│
│
│
├── RandonForest - GPU/             # Pipeline Random Forest acelerado por GPU (cuML)
│   ├── models/                    # Modelos GPU salvos
│   ├── models_Tree_GPU/           # Árvores estruturadas para GPU
│   ├── plots/                     # Gráficos de desempenho GPU
│   └── RandonForest_GPU.ipynb     # Notebook principal GPU
│
│
│
├── SVM/                            # Pipeline Support Vector Machine
│   ├── models/
│   ├── models_Tree_GPU/
│   ├── plots/
│   └── SVM.ipynb                  # Notebook principal SVM
│
│
├── XGBoost/                        # Pipeline Xtreme Gradient Boosting
│   ├── models/
│   ├── models_Tree_GPU/
│   ├── plots/
│   ├── Top20_miRNAs_XGBoost.csv   # Seleção de features gerada pelo modelo
│   └── XGBoost.ipynb              # Notebook principal XGBoost
│
│
├── .gitignore                      # Filtros de arquivos para o Git
├── environment.yml                # Configuração do ambiente Conda para GPU (WSL)
├── readme.md                      # Documentação do projeto
└── requirements.txt               # Dependências Python para pipelines CPU/Padrão



## 🛠️ Tecnologias Utilizadas

- **Linguagem:** Python 3.10
- **Modelagem Padrão (CPU):** Scikit-learn (Random Forest, SVM), XGBoost
- **Aceleração por Hardware (GPU):** RAPIDS cuML (Random Forest GPU via CUDA 12.0)
- **Processamento de Dados & Balanceamento:** Pandas, NumPy, Scipy, Imbalanced-learn (SMOTE)
- **Explicabilidade & Visualização:** SHAP, Matplotlib
- **Persistência de Modelos:** Joblib

---

## 🚀 Como Configurar e Rodar o Projeto

O projeto é dividido em dois ecossistemas de execução. Siga o guia abaixo dependendo do modelo que deseja rodar:

### 🔹 Cenário A: Executando os Modelos Padrão (CPU / Instalação Direta)
*Modelos suportados: `RandonForest - CPU`, `SVM` e `XGBoost`.*

Esta configuração utiliza o ambiente virtual padrão do Python (`venv`) e instala as dependências via `requirements.txt`. Pode ser executada nativamente no seu sistema operacional (Windows ou Linux).

```bash
# 1. Certifique-se de estar na pasta raiz do projeto (TCC) após o clone
cd TCC

# 2. Crie o ambiente virtual com Python 3.10+
python -m venv venv

# 3. Ative o ambiente virtual
# No Windows (Prompt de Comando):
venv\Scripts\activate
# No Windows (PowerShell):
.\venv\Scripts\activate
# No Linux/macOS:
source venv/bin/activate

# 4. Atualize o gerenciador de pacotes pip e instale as dependências
pip install --upgrade pip
pip install -r requirements.txt


### 🔹 Cenário B: Executando o Modelo Acelerado por GPU (WSL + Conda)
*Se aplica exclusivamente ao modelo: `RandonForest - GPU` (utilizando RAPIDS cuML).*

Este passo-a-passo pressupõe que você já abriu o terminal do Ubuntu dentro do WSL, realizou o `git clone` e **já está posicionado dentro da pasta do projeto**.

#### Passo 1: Instalar o Miniconda (Caso ainda não tenha no Ubuntu do WSL)
Se você já possui o comando `conda` funcionando no terminal do WSL, pule para o **Passo 2**. Caso contrário, execute os comandos abaixo:

```bash
# Baixa o instalador do Miniconda para Linux
wget [https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh](https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh)

# Executa a instalação (pressione Enter e digite 'yes' quando solicitado)
bash Miniconda3-latest-Linux-x86_64.sh

# Reinicialize o shell para ativar o comando conda
exec bash

# 2. Cria o ambiente virtual completo com cuML, CUDA 12.0 e Python 3.10 a partir do arquivo
conda env create -f environment.yml

# 3. Ative o ambiente virtual criado
conda activate gpu_env