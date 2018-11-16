title: Selektivní rozmazání
Description: Jak rozmazat pouze pozadí obrázku
---
>Tento dokument pracuje s [obrázkem kytky](/zodoc/assets/img/kytka256.jpg) v proměnné `A`
  
Rozostřit pouze tu část, která není samotnou kytkou. Ve skutečnosti se rozostří celý obrázek a nerozmazaná místa se nahradí původním obrázkem.

![](../media/2018-11-03-09-44-29.png)

``` matlab
Abin = uint8(rgb2gray(A)>128);% prahování obrazu

f_gaussian = fspecial('gaussian',20,4); % konstrukce gaussovského filtru
A_gaussian = imfilter(A,f_gaussian,'same');% uplatnění filtru. 'same' -> stejná velikost i po filtraci
Abin_rgb = repmat(Abin,[1 1 3]);%nareplikování binárního obrazu do 3 rozměrů (aby se tím dal násobit RGB obraz)
A_selective_blur = Abin_rgb.*A + (1-Abin_rgb).*A_gaussian; %nerozmazaná část + rozmazaná část

imshow(A_selective_blur)
```