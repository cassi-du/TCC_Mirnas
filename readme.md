# Predição de Câncer de Pâncreas via Expressão de miRNAs

Este projeto faz parte do **Trabalho de Conclusão de Curso (TCC)** e tem como objetivo o **treinamento e predição de câncer de pâncreas** a partir da análise de **valores de expressão de microRNAs (miRNAs) do sangue**.

O projeto utiliza técnicas de **Machine Learning supervisionado**, com foco atual no algoritmo **Random Forest**, visando maior robustez e melhor desempenho em comparação a abordagens anteriores baseadas em redes neurais, com treinamento via CPU e GPU.

---

# Objetivo do Projeto

- Analisar datasets de expressão de miRNAs
- Tratar desbalanceamento de classes
- Selecionar características relevantes
- Treinar modelos de Machine Learning
- Realizar predições para auxílio no diagnóstico de câncer de pâncreas

---

# Tecnologias Utilizadas

- **Python 3.10+**
- **Scikit-learn**
- **Random Forest**
- **SMOTE (balanceamento de classes)**
- **Pandas / NumPy**
- **Matplotlib**
- **Joblib / Pickle**

---

# Estrutura de Branches

O projeto está atualmente organizado da seguinte forma:

| Branch | Descrição |
|------|----------|
| `master` | Primeira abordagem utilizando Keras (descontinuada) |
| `main` | Versão estável utilizando Random Forest, treinamento via CPU
| `develop` | Branch de testes e experimentos, várias arvores e modelos de treino, treinamento via GPU |

---

# Estrutura Geral do Projeto

```Project
Projeto-TCC/
├── Databases/                  # Dados brutos e processados
│   ├── database.csv            # Dataset original
│   └── database_processed.csv  # Dados tratados para análise
│
├── models/                     # Modelos treinados e normalizadores
│   ├── model.joblib            # Modelo treinado
│   └── normalizadores.model    # Normalizador utilizado no treino
│
├── plots/                      # Imagens e gráficos gerados durante o treino
│   ├── treino_rf.png
│   └── distribuicao_mirnas.png
│
├── src/                        # Notebooks ou scripts
│   └── analysis.ipynb          # Notebook principal com treinamento e predição
│
├── requirements.txt            # Bibliotecas necessárias
├── README.md                   # Documentação do projeto
└── .gitignore                  # Arquivos e pastas ignoradas pelo Git
```

# Futuro tópico: como rodar ambiente virttual, não realizado ainda pois iremos implementar ambiente Conda e Cuml