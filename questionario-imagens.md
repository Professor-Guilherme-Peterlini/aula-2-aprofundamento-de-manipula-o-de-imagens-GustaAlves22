# Questionário Teórico: Processamento de Imagens com Python

## Instruções
* Responda todas as questões de forma clara e concisa
* Justifique suas respostas quando solicitado
* Tempo estimado: 45 minutos

## Questões

### Parte 1: Conceitos Básicos

1. (2,0 pontos) Explique a diferença entre os métodos de redimensionamento de imagem:
   * Nearest Neighbor
      R: É uma técnica simples e rápida para redimensionar imagens porém resulta em imagens pixealizadas e com bordas com pouca suavidade, esse método é usado quando a velocidade é mais importante que a qualidade visual.
      
   * Bilinear
      R: Esse método faz a imagem ficar mais suave, pegando os quatro pixels mais próximos e misturando seus valores para calcular o novo pixel, esse método é mais rápido que métodos mais avançados e é bom para imagens com mudanças suaves.
   
   * Bicubic
      R: Esse método oferece a melhor qualidade de imagem, criando imagens mais suaves e detalhadas. Porém, ele é mais lento e exige mais processamento, sendo ideal quando a qualidade visual é a prioridade.

2. (1,5 pontos) Por que é importante fazer backup das imagens originais antes de aplicar transformações? Cite dois cenários onde isso é crítico.
      R: Fazer backup das imagens originais é importante porque as transformações podem ser irreversíveis e afetar a qualidade da imagem. 
      Dois cenários são:
      Projetos profissionais: A imagem original é a base para edições futuras e pode ser necessária para ajustes ou recomeçar a edição.
      Fotos importantes: Para preservar imagens valiosas, como registros históricos ou fotos pessoais, evitando perda de qualidade irreparável.
### Parte 2: Escala de Cinza

3. (2,0 pontos) Compare os dois métodos de conversão para escala de cinza vistos em aula:
   * Média simples dos canais RGB
   * Método por luminosidade (Y = 0.299R + 0.587G + 0.114B)
   Por que o segundo método é considerado mais preciso para a percepção humana?
      
      R: O olho humano é mais sensível ao verde, seguido pelo vermelho, e menos sensível ao azul. E nesse método o verde tem mais "peso"

4. (1,5 pontos) Em processamento de imagens, por que frequentemente convertemos uma imagem para escala de cinza antes de aplicar outros algoritmos?
      R: A conversão para escala de cinza reduz a complexidade computacional, elimina informações de cor desnecessárias e facilita a aplicação de algoritmos de processamento de imagem.

### Parte 3: Detecção de Bordas

5. (2,0 pontos) Explique o funcionamento dos seguintes operadores de detecção de bordas:
   * Sobel
      R: O operador Sobel utiliza dois filtros 3x3 para calcular os gradientes horizontal e vertical de uma imagem, permitindo detectar bordas. Ele calcula a magnitude do gradiente em cada pixel, destacando mudanças significativas de intensidade, o que é útil para localizar bordas em imagens.
   
   * Prewitt
      R: O operador Prewitt detecta bordas em imagens aplicando dois filtros 3x3 para calcular os gradientes nas direções horizontal e vertical. Ele é simples, eficiente e eficaz para detectar bordas em imagens com transições suaves.
   
   * Laplaciano
      R: O operador Laplaciano utiliza a segunda derivada da intensidade da imagem para identificar bordas, detectando mudanças bruscas de intensidade.

6. (1,5 pontos) Na função `pipeline_processamento()` implementada, por que aplicamos equalização de histograma antes da detecção de bordas?
      R: Para aumentar o contraste da imagem e destacar transições de intensidade. Isso melhora a precisão e a robustez do processo de detecção de bordas, especialmente em imagens com baixo contraste ou iluminação desigual.

### Parte 4: Aplicação Prática

7. (2,0 pontos) Considere o seguinte trecho de código:
```python
img_bordas = img_equalizada.filter(ImageFilter.FIND_EDGES)
img_final = img_bordas.point(lambda x: 255 if x > limiar else 0)
```
   * Qual o propósito da segunda linha?
      R: Para deixar preto e branco.

   * Como a escolha do valor de limiar afeta o resultado final?
      R: Limiar baixo: Detecta muitas bordas, mas inclui ruído.
         Limiar ideal: Equilibra bordas reais e ruído, gerando um resultado limpo.
         Limiar alto: Preserva apenas bordas fortes, descartando detalhes menores.

8. (2,5 pontos) Descreva um pipeline completo para:
   * Detectar bordas em uma imagem com ruído
R: Carregar a imagem:
      from PIL import Image, ImageFilter, ImageOps
      img = Image.open("imagem.jpg").convert("L")

Reduzir ruído:
img_suavizada = img.filter(ImageFilter.GaussianBlur(radius=2))

Equalizar o histograma:
img_equalizada = ImageOps.equalize(img_suavizada)

Detectar bordas:
img_bordas = img_equalizada.filter(ImageFilter.FIND_EDGES)

Binarizar a imagem:
limiar = 50
img_binarizada = img_bordas.point(lambda x: 255 if x > limiar else 0)

Salvar o resultado:
img_binarizada.save("bordas_detectadas.jpg")

   * Justifique cada etapa do processo
   * Explique como você escolheria os parâmetros


## Bônus (1,0 ponto extra)
Proponha uma modificação no pipeline de processamento que poderia melhorar os resultados em imagens com baixo contraste.
---
**Autor**: [Guilherme Tavares]  
**Data**: [24/01/2025]  
**Versão**: 1.1
