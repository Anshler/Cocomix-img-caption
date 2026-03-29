# Evaluating Methods For Applying Large Concept Model To Image Captioning 👁️📜🖋️

[![Paper](https://img.shields.io/badge/paper-PDF-red?style=flat-square&logo=adobeacrobatreader)](paper.pdf)
[![Zenodo](https://img.shields.io/badge/zenodo-10.5281%2Fzenodo.19276839-blue?style=flat-square&logo=zenodo)](https://doi.org/10.5281/zenodo.19276839)
[![HuggingFace](https://img.shields.io/badge/🤗%20model-Anshler%2Fclip--cocomix-yellow?style=flat-square)](https://huggingface.co/Anshler/clip-cocomix)
[![Dataset](https://img.shields.io/badge/dataset-Flickr30k-orange?style=flat-square&logo=kaggle)](https://www.kaggle.com/datasets/eeshawn/flickr30k)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1kEDfGMac2pzbC3ciEM4v3Yso9IQoirIt?usp=sharing)

> **TL;DR** — We apply Large Concept Models to image captioning via a prefix-based framework, outperforming GPT-2 baselines on all major metrics (BLEU, METEOR, ROUGE, CIDEr, BERTScore) under frozen language model training.

## Abstract

This thesis investigates the application of [Large Concept Models](https://arxiv.org/abs/2502.08524) (LCMs) to image captioning, a task requiring both visual recognition and linguistic reasoning.

Unlike Transformer-based captioners that optimize token likelihood, LCMs internalize high-dimensional concept representations, enabling richer semantic abstraction. We integrate LCMs into a prefix-based captioning framework and introduce Prefix Concept Extraction (PCE), which converts image embeddings into pseudo-tokens for explicit cross-modal alignment.

Experiments on Flickr30k demonstrate that LCM-based captioners consistently outperform GPT-2 baselines under frozen language model training, achieving higher BLEU, METEOR, ROUGE, CIDEr, and BERTScore metrics. While GPT-2 remains competitive when fine-tuned, LCM variants show stronger semantic fidelity and generalization. Finally, we implement the proposed models as an extension for Stable Diffusion WebUI, enabling practical deployment for dataset creation and real-world usage. These findings highlight concept-based modeling as a promising alternative to sequence likelihood optimization in multimodal learning.

## Architecture

<img src="img/Cocomix.png" alt="Cocomix architecture" style="width: 100%;">

<img src="img/captionArchitecture.png" alt="Our image caption architecture" style="width: 100%;">

## Dataset

This model was trained on the [Flickr30k](https://www.kaggle.com/datasets/eeshawn/flickr30k) dataset

## Evaluation

* Frozen LM setting

| Model         | BLEU-1 | BLEU-2 | BLEU-3 | BLEU-4 | METEOR | ROUGE | CIDEr | BERTScore |
|--------------|--------|--------|--------|--------|--------|-------|-------|-----------|
| GPT-2        | 0.5245 | 0.3516 | 0.2285 | 0.1460 | 0.1961 | 0.4844 | 0.4384 | 0.8922 |
| Cocomix      | 0.5847 | 0.4016 | 0.2647 | 0.1737 | 0.2033 | 0.4982 | **0.4660** | 0.8953 |
| Cocomix+PCE  | **0.6221** | **0.4267** | **0.2822** | **0.1841** | **0.2052** | **0.5060** | 0.4587 | **0.8967** |

> **Cocomix+PCE achieves the best results** in the frozen language model setting, demonstrating the benefit of Prefix Concept Extraction for semantic alignment under constrained training.

<img src="img/eval.png" alt="Evaluation results" style="width: 100%;">

## Inference

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1kEDfGMac2pzbC3ciEM4v3Yso9IQoirIt?usp=sharing)

We also create a _[Stable diffusion WebUI](https://github.com/AUTOMATIC1111/stable-diffusion-webui) extension_ to interact with the model locally. Load the extension from this repo [Anshler/Cocomix_sd_extension](https://github.com/Anshler/Cocomix_sd_extension)

## Training

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1N62KynuP-gaE32EVxXn2LwJweqm6OgKL?usp=sharing)

Run [FSB_Capstone_ClipCap.ipynb](FSB_Capstone_ClipCap.ipynb) or open the above Colab Notebook. Replace all the folder names with your valid sources, else it won't work.

__Important notes__:
* The code is for training the image captioner from scratch, if you want to finetune the current model, try modify the code yourself to load weight from HuggingFace (using the Inference code as reference).

* We trained both our Cocomix and GPT-2 language model from scratch using the openwebtext dataset in this [Colab Notebook](https://colab.research.google.com/drive/1AnYL6hxHiXxc13AcbXh50PbdFkMJrc00?usp=sharing). The pipeline was based on the original [CoComix repo](https://github.com/facebookresearch/RAM/tree/main/projects/cocomix).

* For your image caption training you can use the normal gpt-2 or anything else.

## Models
The weights of our caption models, as well as the corresponding Cocomix and GPT-2 language model are published on HuggingFace (frozen LM version)

[![HuggingFace](https://img.shields.io/badge/🤗%20model-Anshler%2Fclip--cocomix-yellow?style=flat-square)](https://huggingface.co/Anshler/clip-cocomix)

CLIP model used is ViT-L-14

## Citation

```bibtex
@misc{huynh2026evaluating,
  author       = {Huynh, M. T.},
  title        = {Evaluating Methods For Applying Large Concept Model To Image Captioning},
  year         = {2026},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.19276839},
  url          = {https://doi.org/10.5281/zenodo.19276839}
}
```
