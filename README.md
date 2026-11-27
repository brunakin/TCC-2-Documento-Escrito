# Classificação Automática de Chamados de TI Utilizando Processamento de Linguagem Natural com Explicabilidade Baseada em Grafos

Trabalho de Conclusão de Curso (TCC 2) do Bacharelado em Ciência da Computação do Centro Universitário Senac – Santo Amaro, 2026.

**Autores:** Agatha Barbosa Marinho dos Santos, Bruna Kinjo Luiz Pinto e Kayke Ahrens Biscegli
**Orientador:** Prof. Douglas José Baquião Ribeiro

## Contexto

Equipes de suporte de TI recebem grandes volumes de chamados em texto livre, e classificá-los à mão é lento e sujeito a erros. Modelos baseados em *transformers*, como o BERT, classificam bem, mas não revelam por que atribuíram uma categoria a um chamado, o que dificulta a auditoria das suas decisões.

## Objetivo

Investigar como a inclusão de uma camada de explicabilidade baseada em SHAP, LIME e grafos de co-ocorrência (redes em que as palavras são ligadas quando aparecem próximas no texto) a um *pipeline* de classificação com BERTimbau contribui para a auditabilidade do processo decisório, comparando a qualidade das explicações dos dois métodos.

## Dados

Chamados de suporte técnico em português brasileiro, anonimizados e cedidos por duas empresas do setor farmacêutico (Empresa A e Empresa B): 53.279 chamados em 11 categorias. Os dados foram divididos em treino, validação e teste de modo que textos repetidos fiquem no mesmo conjunto.

## Método

Foram comparados quatro cenários, que acrescentam um componente por vez:

1. *Baseline* com SVM e TF-IDF
2. *Fine-tuning* do BERTimbau
3. Explicações SHAP e LIME
4. Grafo de co-ocorrência ponderado pelas explicações

Em uma amostra de 98 chamados do conjunto de teste, o SHAP e o LIME foram avaliados quanto à fidelidade, à estabilidade e à concordância entre si. A rastreabilidade do grafo, tomada como critério de auditabilidade, foi examinada em três casos aplicados.

## Principais resultados

- **Classificação:** o BERTimbau obteve F1-macro de 0,628 e acurácia de 0,724 no conjunto de teste. O *baseline* SVM com TF-IDF obteve F1-macro de 0,591. A diferença foi de 3,7 pontos percentuais (intervalo de confiança de 95%: 1,0 a 6,7), abaixo da meta de 5 pontos estabelecida inicialmente.
- **Explicações:** SHAP e LIME tiveram fidelidade bem acima do acaso e apontaram a mesma palavra no topo em 69% dos chamados. Só o Tau-LOO distinguiu os métodos, a favor do LIME.
- **Estabilidade:** nos chamados em que o SHAP precisou ser estimado por amostragem, ele foi mais estável que o LIME no Jaccard e no Spearman, mas menos estável na mesma palavra no topo (83% dos pares de repetições, contra 93% do LIME).
- **Grafo:** nos três casos aplicados, cada nó e cada aresta pôde ser levado ao chamado e aos pesos do SHAP e do LIME. O grafo expôs, por exemplo, que um erro do modelo se apoiou em muito pouca evidência.

## Interface

Os resultados foram integrados a uma interface *web* que classifica um chamado digitado, exibe o grafo de co-ocorrência e permite alternar entre os pesos do SHAP e do LIME. A interface é uma prova de conceito e não foi avaliada junto a analistas de TI.

## Documento

O texto completo está em [`tcc2/tcc2.pdf`](tcc2/tcc2.pdf).

## Palavras-chave

Processamento de Linguagem Natural. BERT. Inteligência Artificial Explicável. Grafos de Co-ocorrência. Classificação de Chamados de TI.
