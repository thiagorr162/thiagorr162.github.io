---
title: "AmnioML: amniotic fluid segmentation and volume prediction with uncertainty quantification"
collection: publications
permalink: /publication/amnioml
excerpt: "We present AmnioML, a machine learning solution that leverages deep learning and conformal prediction to output fast and accurate volume estimates and segmentation masks from fetal MRIs."
date: 2023-06-26
venue: 'AAAI'
paperurl: 'https://ojs.aaai.org/index.php/AAAI/article/view/26837'
author_profile: false
---

Accurately predicting the volume of amniotic fluid is fundamental to assessing pregnancy risks, though the task usually requires many hours of laborious work by medical experts. In this paper, we present AmnioML, a machine learning solution that leverages deep learning and conformal prediction to output fast and accurate volume estimates and segmentation masks from fetal MRIs with Dice coefficient over 0.9. Also, we make available a novel, curated dataset for fetal MRIs with 853 exams and benchmark the performance of many recent deep learning architectures. In addition, we introduce a conformal prediction tool that yields narrow predictive intervals with theoretically guaranteed coverage, thus aiding doctors in detecting pregnancy risks and saving lives. A successful case study of AmnioML deployed in a medical setting is also reported. Real-world clinical benefits include up to 20x segmentation time reduction, with most segmentations deemed by doctors as not needing any further manual refinement. Furthermore, AmnioML's volume predictions were found to be highly accurate in practice, with mean absolute error below 56mL and tight predictive intervals, showcasing its impact in reducing pregnancy complications. 


### References:
- [Article from Folha de São Paulo](https://www1.folha.uol.com.br/ciencia/2021/09/inteligencia-artificial-criada-por-matematicos-brasileiros-previne-doencas-na-gravidez.shtml?origin=folha)
- [Deployed Award](https://impa.br/noticias/artigo-do-impa-e-premiado-em-conferencia-internacional-sobre-ia/)
- [Github Repo](https://github.com/dccsillag/amnioml)
- [Main Paper](https://ojs.aaai.org/index.php/AAAI/article/view/26837)
- [Presentation](/files/presentations/amnioML-alek-2024.pdf)


<figure>
  <video style="width: 100%; height: auto;" controls>
    <source src="/files/videos/amnioml/reconstruction.mp4" type="video/mp4">
    Seu navegador não suporta o elemento de vídeo.
  </video>
  <figcaption>AmnioML Reconstruction.</figcaption>
</figure>
