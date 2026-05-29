# 🌱 Edge AI para Detecção de Estresse Hídrico e Pragas com Redução de Overhead de Rede

> Projeto da disciplina de Inteligência Artificial — Universidade Presbiteriana Mackenzie  
> Faculdade de Computação e Informática — 7º Período CC Noite  
> Prof. Dr. Ivan Carlos Alcântara de Oliveira

---

## 👥 Integrantes

| Nome | RA | E-mail |
|------|----|--------|
| Gabriel Vieira de Sousa | 10410264 | 10410264@mackenzista.com.br |
| Guilherme Rainho Geraldo | 10418251 | 10418251@mackenzista.com.br |
| Guilherme Gomes Arantes Teles | 10364065 | 10364065@mackenzista.com.br |

---

## 📋 Descrição do Projeto

Sistema de **visão computacional embarcado em dispositivos de borda** (Raspberry Pi 4) para identificar, em tempo real, sintomas de **estresse hídrico**, **doenças foliares** e **presença de pragas** em plantações.

O sistema utiliza o modelo **MobileNetV2** com quantização **INT8** via **TensorFlow Lite**, treinado sobre o dataset **PlantVillage** (54.306 imagens, 38 classes). Ao transmitir apenas alertas estruturados via **LoRaWAN/MQTT** em vez de imagens brutas, o sistema reduz o overhead de rede em **99,5%** em comparação com abordagens tradicionais baseadas em nuvem.

**Área:** Sustentabilidade / Agricultura de Precisão  
**Opção:** ML/DL/VC/PLN (Visão Computacional + Deep Learning)

---

## 🏆 Resultados Obtidos (N2)

| Métrica | FP32 | INT8 PTQ | INT8 QAT | Meta |
|---------|------|----------|----------|------|
| Acurácia | 96,4% | 95,8% | 96,1% | ≥ 95% ✅ |
| F1-Score (macro) | 0,962 | 0,957 | 0,960 | — |
| Tamanho do modelo | 13,4 MB | 3,6 MB | 3,6 MB | < 4 MB ✅ |
| Latência (Raspberry Pi 4) | ~287 ms | **74 ms** | **72 ms** | 30–100 ms ✅ |
| Redução de tráfego de rede | — | **99,5%** | **99,5%** | ≥ 90% ✅ |

> **Todas as metas foram atingidas ou superadas.**

---

## 🎬 Vídeo de Apresentação (YouTube)

📺 **[https://www.youtube.com/watch?v=<ID_DO_VIDEO>](https://www.youtube.com/watch?v=<ID_DO_VIDEO>)**

O vídeo (máx. 5 minutos) contém:
- Apresentação dos integrantes, disciplina e instituição
- Definição do problema e motivação
- Explicação da arquitetura Edge AI (CNN + TFLite + LoRaWAN)
- Demonstração de inferência local no Raspberry Pi 4
- Navegação pelo repositório GitHub

---

## 🗂️ Estrutura do Repositório

```
edge-ai-plant-disease/
│
├── README.md                          # Este arquivo
│
├── docs/
│   ├── Artigo_N1_EdgeAI.docx          # Relatório parcial N1 (template SBC)
│   ├── Artigo_N2_EdgeAI.docx          # Relatório completo N2 (template SBC)
│   ├── fig1_distribuicao_classes.png
│   ├── fig2_amostras_visuais.png
│   ├── fig3_analise_rgb.png
│   ├── fig4_qualidade_imagens.png
│   ├── fig5_correlacao_especie_doenca.png
│   ├── fig6_curvas_aprendizado.png
│   ├── fig7_matriz_confusao.png
│   ├── fig8_metricas_sistema.png
│   └── resultados_finais.csv
│
├── dataset/
│   └── README.md                      # Descrição e instruções do dataset
│
├── notebooks/
│   ├── 01_analise_exploratoria.ipynb  # Análise exploratória do PlantVillage (N1)
│   └── 02_treinamento_quantizacao.ipynb  # Treinamento, quantização e benchmark (N2)
│
└── models/                            # Modelos exportados (gerados ao rodar o notebook)
    ├── mobilenetv2_fp32_best.h5
    ├── mobilenetv2_fp32.tflite
    ├── mobilenetv2_int8_ptq.tflite
    └── mobilenetv2_int8_qat.tflite
```

---

## 🛠️ Tecnologias Utilizadas

- Python 3.10+
- TensorFlow 2.15 / TensorFlow Lite
- TensorFlow Model Optimization (QAT)
- MobileNetV2 (pré-treinada em ImageNet)
- OpenCV, Pandas, NumPy, Matplotlib, Seaborn
- Scikit-learn (métricas de avaliação)
- Jupyter Notebook

---

## 📊 Dataset

**PlantVillage** — 54.306 imagens de folhas de plantas, organizadas em 38 classes (14 espécies × 26 doenças + folhas saudáveis). Detalhes em [`dataset/README.md`](dataset/README.md).

---

## 🚀 Como Reproduzir

```bash
# 1. Clone o repositório
git clone https://github.com/GuilhermeTeles/edge-ai-plant-disease.git
cd edge-ai-plant-disease

# 2. Instale as dependências
pip install tensorflow==2.15.0 tensorflow-model-optimization scikit-learn \
            matplotlib seaborn pandas numpy Pillow tqdm opencv-python

# 3. Baixe o dataset PlantVillage (Kaggle CLI)
pip install kaggle
kaggle datasets download -d abdallahalidev/plantvillage-dataset
unzip plantvillage-dataset.zip -d dataset/plantvillage/

# 4. Execute os notebooks em ordem
jupyter notebook notebooks/01_analise_exploratoria.ipynb
jupyter notebook notebooks/02_treinamento_quantizacao.ipynb
```

### Implantar no Raspberry Pi 4

```bash
# No RPi4 — instalar TFLite runtime
pip install tflite-runtime

# Executar inferência com o modelo quantizado
python src/inference_rpi.py --model models/mobilenetv2_int8_ptq.tflite --camera 0
```

---

## 📄 Relatórios

| Bimestre | Arquivo | Descrição |
|----------|---------|-----------|
| N1 | [`docs/Artigo_N1_EdgeAI.docx`](docs/Artigo_N1_EdgeAI.docx) | Proposta, análise exploratória e resultados parciais |
| N2 | [`docs/Artigo_N2_EdgeAI.docx`](docs/Artigo_N2_EdgeAI.docx) | Relatório completo com treinamento, quantização e benchmark |

---

## 📅 Histórico de Atualizações

| Data | Autor | Descrição |
|------|-------|-----------|
| 22/05/2026 | Guilherme Teles | Criação do repositório e estrutura inicial |
| 22/05/2026 | Guilherme Teles | Adição do notebook de análise exploratória (N1) |
| 22/05/2026 | Guilherme Teles | Adição do relatório N1 e descrição do dataset |
| 28/05/2026 | Guilherme Rainho | Adição do notebook de treinamento e quantização (N2) |
| 28/05/2026 | Gabriel Vieira | Implementação de QAT e benchmark de latência |
| 28/05/2026 | Guilherme Teles | Relatório N2 completo e atualização do README |
