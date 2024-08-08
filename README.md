---
jupyter:
  kernelspec:
    display_name: Octave
    language: octave
    name: octave
  language_info:
    file_extension: .m
    help_links:
    - text: GNU Octave
      url: "https://www.gnu.org/software/octave/support.html"
    - text: Octave Kernel
      url: "https://github.com/Calysto/octave_kernel"
    - text: MetaKernel Magics
      url: "https://metakernel.readthedocs.io/en/latest/source/README.html"
    mimetype: text/x-octave
    name: octave
    version: 6.4.0
  nbformat: 4
  nbformat_minor: 5
---

::: {#1aa7f75d-6cc0-4ad3-b8e9-980e2f11f0f4 .cell .markdown}
## Representação de imagens matriciais
:::

::: {#bed412ab-b71e-422a-9355-5d4d4b1b3dc9 .cell .markdown}
### Definição
:::

::: {#cda56730-d145-4354-a0b0-66a1a02ccf36 .cell .markdown}
Uma imagem digital é constituída por um conjunto de pixels, representado
por uma matriz bidimensional ou tridimensional, de acordo com os tipos
definidos a seguir.
:::

::: {#efebdeb6-8787-4c92-9263-e498ac18d2a6 .cell .markdown}
### Tipos
:::

::: {#5d86d676-0941-406e-818e-4c741a5b3051 .cell .markdown}
Octave suporta quatro tipos de imagens:

-   imagens em tons de cinza;
-   imagens binárias;
-   imagens RGB;
-   imagens indexadas.
:::

::: {#00913bbe-434b-4138-97bc-a093af36d1a1 .cell .markdown}
### Imagem grayscale
:::

::: {#e5e8fb5e-671a-4892-99b7-50681a423450 .cell .markdown}
Uma imagem em tons de cinza (**grayscale**) é representada por uma
matriz bidimensional **M x N**, em que cada elemento expressa a
intensidade do pixel.
:::

::: {#82dd4a6c-0bb9-4394-9b84-fb79ecb7067a .cell .code execution_count="25"}
``` octave
A = [0 2 4 6 8; 10 12 14 16 18; 20 22 24 26 28];
imagesc(A)
colormap(gray)
axis image % preserva a proporção da imagem
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/2749d400523079d734f53f2c944c157fa45829ba.png)
:::
:::

::: {#6840884f-a6e8-472b-8269-b75b0130a49f .cell .markdown}
### Intermezzo
:::

::: {#11cf5d53-2542-46a1-b5e1-b4577481b4cf .cell .markdown}
A transição de tons de cinza é baseada nos valores discretos na matriz
**A**.
:::

::: {#85ecb211-c67a-45a0-ab5d-aa0a6b0f659d .cell .code execution_count="26"}
``` octave
num_elementos = numel(A)
```

::: {.output .stream .stdout}
    num_elementos = 15
:::
:::

::: {#2a364c6a-2e7a-47ad-9c61-e74e994f37ec .cell .markdown}
A matriz **A** possui apenas 15 valores distintos (em uma matriz de
3x5), o que resulta em uma imagem com transições abruptas entre os
níveis de cinza.
:::

::: {#1258adf0-7c87-4258-a933-37fee2de19dd .cell .markdown}
Se aumentarmos a resolução da imagem, podemos obter uma transição mais
suave entre os tons de cinza.
:::

::: {#55a30e7e-0be5-4fc2-b059-a4b198dd2304 .cell .code execution_count="27"}
``` octave
outsize = [256 512]; % [y x]
% criamos alguns vetores
x = linspace(0,1,outsize(2)); % linhas
y = linspace(0,1,outsize(1)).'; % colunas
% criamos a matriz no intervalo [0.2 0.8]
Z = 0.2 + 0.3*(x+y);
```
:::

::: {#ed065be4-dc66-4d8b-9c3f-8c58f7e6cf98 .cell .code execution_count="28"}
``` octave
num_elementos = numel(Z)
```

::: {.output .stream .stdout}
    num_elementos = 131072
:::
:::

::: {#8707f309-ba09-4419-9790-a86a021c77a3 .cell .markdown}
A matriz **Z** tem 131,072 valores (em uma matriz de 256x512)
distribuídos suavemente, resultando em uma imagem com transições muito
mais suaves entre os níveis de cinza.
:::

::: {#df9958c5-ee4e-4a84-992b-a9d34834e73b .cell .code execution_count="29"}
``` octave
imagesc(Z) 
caxis([0 1]) % define a escala
colormap(gray(256)) % define o mapa de cores
axis image % preserva a proporção da imagem
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/89ae91727bac3813de3c297c555cee52cd6267a1.png)
:::
:::

::: {#be0c45b3-88f6-4d2b-8802-b6c0cdc3ff26 .cell .markdown}
### Imagem binária
:::

::: {#edffffaf-83c5-4e15-8d73-933ec5de861d .cell .markdown}
A imagem **binária** é uma matriz bidimensional **M x N** da classe
*logical*. Pode ser considerada um caso especial de imagens em tons de
cinza, considerando apenas os dois valores extremos da escala: 0 ou
preto, se falso; 1 ou branco, se verdadeiro.
:::

::: {#985c8e94-794a-44e5-b86b-d6775bfecbe3 .cell .code execution_count="30"}
``` octave
B = eye(5);
B = logical(B);
imagesc(B);
colormap gray
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/49de8ef3dd84afe1483a2b22c80f43bde88f5d8d.png)
:::
:::

::: {#4a2449fb-3519-401c-9fb6-e9065d9007c7 .cell .markdown}
### Imagem truecolor
:::

::: {#00535041-2b27-4bd2-a749-ac66611b991e .cell .markdown}
Uma imagem **RGB** (**truecolor**) é representada por uma matriz
tridimensional **M x N x 3**. Cada pixel da imagem possui uma cor,
resultante da combinação da intensidade de cada um dos canais: **red**
(vermelho), **green** (verde) e **blue** (azul).
:::

::: {#d78fb533-d045-4e95-b881-b14160840899 .cell .code execution_count="31"}
``` octave
% Criação da matriz C
C = zeros(3,3,3);
C(:,:,1) = [.1 .2 .3 ; .4 .5 .6; .7 .8 .9]; % vermelho
C(:,:,2) = [.21 .22 .23; .24 .25 .26; .27 .28 .29]; % verde
C(:,:,3) = [.31 .32 .33; .34 .35 .36; .37 .38 .39]; % azul

% Exibir a imagem com imshow para imagens coloridas
imagesc(C);
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/67980885067f7a72952a494fbf6c4c6f0eb384d8.png)
:::
:::

::: {#c331a04f-b805-4616-bcf0-867a71c3f27f .cell .markdown}
### Imagem indexada
:::

::: {#08341d4b-7bb0-4822-820a-cc96505bd0e8 .cell .markdown}
Uma imagem indexada consiste em uma matriz de inteiros **M x N** e um
mapa de cores **C x 3**. Cada número inteiro corresponde a um índice no
mapa de cores e cada linha no mapa de cores corresponde a uma cor
**RGB**. O mapa de cores deve ser da classe *double* com valores entre 0
e 1.
:::

::: {#2e8634f3-fa31-404c-b848-6aad22b9515b .cell .code execution_count="32"}
``` octave
graphics_toolkit ("gnuplot");
[D, map] = rgb2ind (C); % Convertemos de RGB para índice de cores
imagesc(D);
colormap (map)
D
map
```

::: {.output .stream .stdout}
    D =

      0  1  2
      3  4  5
      6  7  8

    map =

       0.1000   0.2100   0.3100
       0.2000   0.2200   0.3200
       0.3000   0.2300   0.3300
       0.4000   0.2400   0.3400
       0.5000   0.2500   0.3500
       0.6000   0.2600   0.3600
       0.7000   0.2700   0.3700
       0.8000   0.2800   0.3800
       0.9000   0.2900   0.3900
:::

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/35ad90689274fa75e7fa141db230efb369cf42e1.png)
:::
:::

::: {#4c5b7498-b226-4e34-9d93-0cd39b92f1a5 .cell .markdown}
Por economia de espaço, omitimos a expressão numérica da matriz **Z** e
do mapa de cores, no exemplo abaixo.
:::

::: {#370db113-04c9-4524-88f1-828ada7be0a3 .cell .code execution_count="33"}
``` octave
W = double(Z); % Garantimos que A esteja em formato de ponto flutuante
W = W / max(W(:)); % Normalizamos a imagem para o intervalo [0, 1]
%Z = A(1:3,2:4); % Fatiamos a matriz original para o formato 3x3
[D, map] = gray2ind(W);
imagesc(D);
colormap gray
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/d3f7ca41223de7b49a019ebf8885f5002d0bd6cd.png)
:::
:::

::: {#baae5015-abb1-411e-9aa7-05d02fa3f3cd .cell .markdown}
### Classes
:::

::: {#8d563de3-709a-4e61-8e49-85ca916b3a12 .cell .markdown}
A intensidade do pixel, para imagens em tons de cinza e RGB, depende da
classe da matriz. Isto é, a escala esperada dos dados da imagem é
determinada pela sua classe numérica, definida de acordo com os
intervalos nominais descritos na tabela abaixo:
:::

::: {#cdf71a1b-2842-40d8-a0f8-7176eca63a30 .cell .markdown}
  Tipo      Descrição                        Intervalo
  --------- -------------------------------- -----------
  logical   Binário                          0 ou 1
  uint8     Inteiro sem sinal de 8 bits      0-255
  uint16    Inteiro sem sinal de 16 bits     0-65535
  double    Real de dupla precisão 64 bits   0 e 1
:::

::: {#9f62fbc6-a484-4105-90f3-7a5a9fa3de64 .cell .markdown}
Para obtermos as classes das matrizes **A**, **B**, **C**, **D** e
**Z**, definimos a seguinte função:
:::

::: {#3e0ec380-556f-4e11-bffe-6ad9f544a0a7 .cell .code execution_count="34"}
``` octave
function tipos = obterTipos(varargin)
    tipos = cell(size(varargin));
    for i = 1:nargin
        tipos{i} = class(varargin{i});
    end
end

obterTipos(A, B, C, D, Z)
```

::: {.output .stream .stdout}
    ans =
    {
      [1,1] = double
      [1,2] = logical
      [1,3] = double
      [1,4] = uint8
      [1,5] = double
    }
:::
:::

::: {#48335bb2-33b9-4b42-801d-95a213e40f9c .cell .markdown}
### Mapas de cores
:::

::: {#29389859-d5c9-421d-ab02-08a179bdb2bd .cell .markdown}
Um mapa de cores é uma matriz de valores que define as cores de objetos
gráficos.`<br>`{=html} Pode ter qualquer comprimento, mas deve
apresentar três colunas de largura. Na definição de *Peter Kovisi*, pode
ser entendido como uma linha ou curva desenhada através de um espaço de
cores tridimensional.
:::

::: {#6fd490a7-96af-4990-b7b6-851196001da5 .cell .markdown}
### Default
:::

::: {#19d08bb1-11b8-46ab-aa2a-bacf8d5906ea .cell .markdown}
**Viridis**, mapa de cores perceptualmente uniforme com luminância
crescente monotonicamente e um arco suave e agradável em tons de azul,
verde e amarelo, de acordo com a descrição de *Kenneth Moreland*, é o
valor padrão adotado pelo Octave, caso não seja fornecido argumento para
a função *colormap()*.
:::

::: {#a8d5fc40-9ae9-44e4-9b8d-50e90d7a9301 .cell .code execution_count="35"}
``` octave
F = [0 2 4 6; 8 10 12 14; 16 18 20 22];
imagesc(F)
colorbar
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/910cee7ca73c8f60a44dd544811e333dc3f440b2.png)
:::
:::

::: {#8617e338-2442-4cc1-af66-f37b37c0b28c .cell .markdown}
### Exemplos de opções integradas
:::

::: {#3da48d59-d35c-437c-a8f4-16604cf2eb42 .cell .markdown}
Octave disponibiliza diversos mapas de cores para escolha do usuário.
Lembramos, no entanto, das advertências para que seja evitado o modelo
*rainbow*, considerado perceptualmente não-uniforme, com transições
enganosas, contra-indicado para pessoas com deficiência visual para
cores, condição conhecida como *daltonismo*.
:::

::: {#bea02588-3fed-4f1c-aabb-1b6972279b1a .cell .markdown}
Exibimos a seguir alguns mapas de cores disponíveis no Octave.
:::

::: {#2442e7d5-e3cf-4504-a33e-e4229c9151a6 .cell .code execution_count="43"}
``` octave
% Definimos a imagem
img = [0 2 4 6; 8 10 12 14; 16 18 20 22];


% Definimos os mapas de cores
colormaps = {'viridis', 'prism', 'jet', 'hot', 'cool', 'spring', 
                'summer', 'autumn', 'winter', 'gray', 'bone', 'hsv'};

% Criamos as imagens com a mesma escala, mas diferentes mapas de cores
figure;

for i = 1:12
    ax = subplot(2, 6, i);
    colormap(ax, colormaps{i});
    imagesc(img);
    axis off;
    title(colormaps{i});
end

% Ajustamos o tamanho da figura para caber todos os subplots
set(gcf, 'Position', [100, 100, 1200, 600]);
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/4cb2e3dd6f39aa1998d7ebc7d7b4c2ff173aef7a.png)
:::
:::

::: {#fa2bfe14-ef26-446c-97d8-5c37d388321b .cell .markdown}
### ColorCET
:::

::: {#54d6afc6-7f13-4fe8-bdd3-b6cfa66d3f15 .cell .markdown}
*ColorCET* é um conjunto de mapas de cores perceptualmente uniformes,
distribuído sob a licença *Creative Commons*, criado por *Peter Kovisi*,
cuja versão para Octave pode ser baixada no endereço
<https://colorcet.com/download/index.html>.
:::

::: {#97c001c6-fd0c-4929-b438-5ec42b61f0a6 .cell .code execution_count="37"}
``` octave
cm = colorcet('C2');
imagesc(F)
colorbar
colormap(cm)
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/d1ca4bed561301d01a12501e068aade84a722662.png)
:::
:::

::: {#fdeab4dc-f8d7-4a43-afd3-4aca4916bac5 .cell .markdown}
### Transformações
:::

::: {#7c6a102d-0102-452a-ad9e-1b955fc0f3f0 .cell .markdown}
Podemos realizar operações com as matrizes numéricas para produzir
alterações nas imagens.
:::

::: {#a24bbba7-f485-4a04-9d95-7c3de9778425 .cell .markdown}
Temos a matriz original:
:::

::: {#5706bca4-51e5-4009-ac15-ea51159c8421 .cell .code execution_count="38"}
``` octave
G = [1 2 3; 4 5 6; 7 3 1; 4 4 4];
imagesc(G)
colorbar
colormap jet
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/bfae8534849827742e9b0028afebd8bd2bedf9f5.png)
:::
:::

::: {#c862f981-bd44-451f-afd8-58c99d797cb2 .cell .markdown}
Realizamos uma transformação trigonométrica:
:::

::: {#4fa39078-4b97-439a-a4bd-13144996c80e .cell .code execution_count="39"}
``` octave
G = [1 2 3; 4 5 6; 7 3 1; 4 4 4];
G2 = G .^ cos(pi);
imagesc(G2)
colorbar
colormap jet
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/89a309d4156cf34b6e9dbc8e74f74e84043beacf.png)
:::
:::

::: {#23182cec-6cf9-4850-8246-53b5c804746e .cell .markdown}
Em seguida efetuamos uma transformação geométrica:
:::

::: {#8fa78745-92b5-4f51-9bc9-fa82df67955d .cell .code execution_count="40"}
``` octave
G3 = G .^ 2;
imagesc(G3)
colorbar
colormap jet
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/80b87a11feb76706dfc1629739f76c36fbba3231.png)
:::
:::

::: {#603d9f83-52d4-42c7-8e76-71982ea5e57c .cell .markdown}
Finalizamos com uma transformação espacial:
:::

::: {#39e299e7-8db1-4859-89df-f1072d4d0717 .cell .code execution_count="41"}
``` octave
G4 = fliplr(G);
imagesc(G4)
colorbar
colormap jet
```

::: {.output .display_data}
![](vertopal_9d304073527a4842a29a77e877bc782f/4075aed3240aaf01f5452b5f840ad2d4daba660e.png)
:::
:::

::: {#dec17b24-ebf3-4077-88e7-ce39a99bea59 .cell .markdown}
**Referências**:

Eaton, John W., Bateman, David , Hauberg, Søren, Wehbring, Rik (2024).
GNU Octave version 9.2.0 manual: a high-level interactive language for
numerical computations.

Kovesi, Peter (2015). Good Colour Maps: How to Design Them.
arXiv:1509.03700 \[cs.GR\].

Kovesi, Peter (2024). *ColorCET - Perceptually Uniform Colour Maps*.
Acessado em 06/08/2024: <https://colorcet.com/>.

Moreland, Kenneth (2016). *Why We Use Bad Color Maps and What You Can Do
About It.* In Proceedings of Human Vision and Electronic Imaging (HVEI),
February 2016. DOI 10.2352/ISSN.2470-1173.2016.16.HVEI-133.`<br>`{=html}

Moreland, Kenneth (2016). *Color Map Advice for Scientific
Visualization*. Acessado em 06/08/2024:
<https://www.kennethmoreland.com/color-advice/>.
:::
