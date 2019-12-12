Reduzir peso do site
====================

É sempre interessante deixar o site o mais leve o possível, ainda mais com os
efeitos e extras que utilizamos.
Neste documento, seguem algumas dicas para deixar o site em uma velocidade
amigável.

_Lossless Compression_ (Sem perda de qualidade)
-----------------------------------------------

Vamos considerar a redução de uma foto tirada a partir de uma câmera
semi-profissional, e a imagem foi chamada de `sample.jpg`. O arquivo possui os
seguintes atributos:

- **Tamanho**: 4.2MB
- **Tipo**: JPEG
- **DPI**: 72x72
- **Dimensões**: 3888x2592
- **Padrão**: Exif
- **Informações extras**:
    - Informações Exif: TIFF image data, little-endian, direntries=12,
        manufacturer=Canon, model=Canon EOS DIGITAL REBEL XS,
        orientation=upper-left, xresolution=196, yresolution=204,
        resolutionunit=2, datetime=2017:10:02 16:49:05
    - Outras: baseline, precision 8, frames 3

O programa `convert` (do pacote `imagemagick`) possui várias tarefas
interessantes que podemos utilizar. Ele possui a seguinte estrutura:

```bash
convert imagem-de-origem [-flags] imagem-de-destino
```

### _Sampling Factor_

Primeiramente, alterando o "sampling factor", podemos eliminar várias
informações desnecessárias mantendo a qualidade da imagem.

```bash
convert sample.jpg -strip -alpha Remove -sampling-factor 4:2:0 sample.jpg
```

- **Tamanho**: **3.7MB**
- **Tipo**: JPEG
- **DPI**: 72x72
- **Dimensões**: 3888x2592
- **Padrão**: JFIF
- **Informações extras**: **baseline, precision 8, frames 3**

### _Interlace_

Alterando o Interlace para JPEG e o espaço de cores para RGB, mudaremos o
formato "baseline" para "progressive", o que é recomendado apenas para imagens
acima de 10KB:

```bash
convert sample.jpg -strip -alpha Remove -sampling-factor 4:2:0 -interlace JPEG -colorspace RGB sample.jpg
```

Obtemos:

- **Tamanho**: **3.6MB**
- **Tipo**: JPEG
- **DPI**: 72x72
- **Dimensões**: 3888x2592
- **Padrão**: JFIF
- **Informações extras**: **segment length 16, progressive**, precision 8, frames 3

### Qualidade

Podemos reduzir a qualidade da imagem...e mesmo assim será bastante
imperceptível. Basicamente, reduzir com um 85:

```bash
convert sample.jpg -strip -alpha Remove -sampling-factor 4:2:0 -interlace JPEG -colorspace RGB -quality 85 sample.jpg
```

Obtemos:

- **Tamanho**: **1.1MB**
- **Tipo**: JPEG
- **DPI**: 72x72
- **Dimensões**: 3888x2592
- **Padrão**: JFIF
- **Informações extras**: segment length 16, progressive, precision 8, frames 3

Dica: Thumbnails
----------------

Para a sessão de fotos, faça thumbnails das fotos e transforme-as em links. No
caso, você pode aproveitar a flag `-resize` do `convert` para isso:

```bash
convert sample.jpg -resize 800x sample-thumb.jpg
```

Perceba que apenas a lagura foi dada (800). Isso serve para manter o
aspect-ratio (proporção). Para redimensionar a altura e manter a proporção para
a largura:

```bash
convert sample.jpg -resize x800 sample-thumb.jpg
```
