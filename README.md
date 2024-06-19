# SBSeg'24 Modelo de Detecção de Malware para Android com Multi-view e Otimização Multiobjetivo

## Apresentação

Este repositório está atrelado ao artigo "Modelo de Detecção de Malware para Android com Multi-view e Otimização Multiobjetivo", de Fransozi, P., Geremias, J. e Viegas, E. O artigo foi publicado no XVIII Workshop de Trabalhos de Iniciação Científica e de Graduação (WTICG) do 24º Simpósio Brasileiro em Segurança da Informação e de Sistemas Computacionais.

Título: Modelo de Detecção de Malware para Android com Multi-view e Otimização Multiobjetivo
Resumo: Nos últimos anos, diversas técnicas de aprendizado de máquina com alta acurácia foram propostas para detecção de _malware_ em aplicativos _Android_. Infelizmente, essas propostas são raramente utilizadas em ambiente de produção devido a uma limitada capacidade de generalização, o que resulta em uma baixa acurácia. Este artigo propõe um modelo de detecção _multi-view_ composto de duas etapas. Na primeira etapa, um conjunto de múltiplas características é extraído de análises de pacotes de aplicativos _Android_, fornecendo um vetor comportamental complementar do aplicativo para a tarefa de classificação, aumentando a generalização. A segunda etapa consiste em realizar uma otimização multiobjetivo para selecionar um subconjunto ideal de características baseado em cada _view_ para classificação com método _ensemble_. Nossa proposta visa um algoritmo que ativamente selecione um subconjunto de características que ao mesmo tempo melhore a acurácia e reduza o custo computacional em um contexto _multi-view_. Os experimentos em nosso novo _dataset_, composto por aproximadamente 40 mil amostras de aplicativos, demonstraram a viabilidade de nossa proposta. O nosso método consegue melhorar as taxas de verdadeiro positivo em uma média de 4,4, exigindo até 65\% dos custos com processamento de inferência.

## Tutorial para reprodução do experimento

Esta seção apresenta um passo-a-passo para reprodução do experimento.

### Requisitos
