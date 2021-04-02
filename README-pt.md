<p align="center"><img src="https://github.com/fgsoruco/opencv_4/blob/main/display/cover_1.gif?raw=true"/></p>

<h1 align="center">opencv_4</h1>

<p align="center">Esta biblioteca contém a implementação de módulos OpenCV, a versão utilizada é 4.3.0 para plataformas Android e iOS.</p><br>

<p align="center">
  <a href="https://flutter.dev">
    <img src="https://github.com/fgsoruco/opencv_4/blob/main/display/Platform-Flutter.png?raw=true"
      alt="Platform" />
  </a>
  <a href="https://pub.dartlang.org/packages/opencv_4">
    <img src="https://github.com/fgsoruco/opencv_4/blob/main/display/nullsafety.png?raw=true"
      alt="Nullsafety" />
  </a>
  <a href="https://pub.dartlang.org/packages/opencv_4">
    <img src="https://github.com/fgsoruco/opencv_4/blob/main/display/pub-version.png?raw=true"
      alt="Pub Package" />
  </a>
  <br>
  <a href="https://opensource.org/licenses/BSD-3-Clause">
    <img src="https://github.com/fgsoruco/opencv_4/blob/main/display/animated-bsd.png?raw=true"
      alt="License: BSD-3-Clause" />
  </a>
  <a href="https://paypal.me/fgsoruco">
    <img src="https://github.com/fgsoruco/opencv_4/blob/main/display/donate.png?raw=true"
      alt="Donate" />
  </a>
</p><br>


# Tabla de contenido

- [Sobre este lançamento](#sobre-este-lançamento)
- [Instalando](#instalando)
- [Como usar](#como-usar)
- [Exemplos](#módulo-image-filtering)
  - [Image Filtering](#módulo-image-filtering)
  - [Color Space Conversions](#módulo-color-space-conversions)
  - [Color Maps](#módulo-color-maps)
  - [Miscellaneous Image Transformations](#módulo-miscellaneous-image-transformations)
- [Errores o solicitudes](#errores-o-solicitudes)
- [Donar](#Donar)


# Sobre este lançamento

## Compatibilidade
* Foi desenvolvido para a integração da biblioteca de visão artificial OpenCV em sua versão 4.3.50
* É compatível com Android e iOS.
* A integração simples com bibliotecas de flutter populares como [image_picker](https://pub.dev/packages/image_picker) foi levada em consideração para processar imagens da galeria ou câmera, você pode ver o exemplo de implementação [aqui](https://pub.dev/packages/opencv_4/example), neste caso você precisa configurar seu projeto com [Nullsafety](#como-usar).

* Os módulos OpenCV usados ​​são os seguintes:
  * __Image Processing__
    * Image Filtering
      * _bilateralFilter_
      * _blur_
      * _boxFilter_
      * _dilate_
      * _erode_
      * _filter2D_
      * _gaussianBlur_
      * _laplacian_
      * _medianBlur_
      * _morphologyEx_
      * _pyrDown_
      * _pyrMeanShiftFiltering_
      * _pyrUp_
      * _scharr_
      * _sobel_
      * _sqrBoxFilter_
    * Miscellaneous Image Transformations
      * _adaptiveThreshold_
      * _distanceTransform_
      * _threshold_
    * Color Space Conversions
      * _cvtColor_
    * ColorMaps in OpenCV
      * _applyColorMap_
   



## Processamento de imagem
* Todo o processamento é feito através do path da imagem
* Imagens no flutter por meio do diretório de assets configurado. __Default__
* Imagens na web.
* Imagens da galeria ou câmera usando [image_picker](https://pub.dev/packages/image_picker)

## Sintaxe
* Semelhante ao Python para chamar métodos e constantes de processamento de imagem, por exemplo 
  * `Cv2.ctvColor` 
  * `Cv2.COLOR_BGR2GRAY`

<!-- ## Em breve
* Implementação de mais módulos OpenCV, estou trabalhando nisso.
* Processamento de vídeos e gifs animados, estou trabalhando nisso. -->

# Instalando

### 1. Dependências

Adicione isso ao arquivo `pubspec.yaml` do seu projeto:

```yaml
dependencies:
  opencv_4: ^1.0.0
```

### 2. Instalar

Você pode instalar bibliotecas a partir da linha de comando:


```
$ flutter pub get
```

### 3. Importe o bibliotecas

Agora em seu código `Dart`, você pode usar:

```dart
import 'package:opencv_4/opencv_4.dart';
```

# Como usar

## Pré requisitos
1. Android: requer a versão mínima 21 no projeto `android (folder) -> app (folder) -> build.gradle`

```gradle
defaultConfig {
    ...
    minSdkVersion 21
    ...
}
```
2. Se você vai trabalhar com o path de assets flutter, não requer permissões no Android e iOS.
3. Se você deseja trabalhar com imagens da web, nenhuma configuração é necessária.
4. Se a biblioteca [image_picker](https://pub.dev/packages/image_picker) for usada para trabalhar com imagens da câmera e da galeria, siga as configurações de permissão para [Android e iOS](https://pub.dev/packages/image_picker#installation).
5. `Nullsafety` se você vai usar o [exemplo](https://pub.dev/packages/opencv_4/example) você deve configurar `pubspect.yaml`

```yaml
environment:
  sdk: ">=2.12.0 <3.0.0"
```


## Classes
`Cv2`: Classe que contém a implementação de módulos e constantes OpenCV

`CVPathFrom`: Permite que você configure o path para processar as imagens.

* `URL` (___static constant___) configurar opencv para imagens da web
* `GALLERY_CAMERA` (___static constant___) configurar o opencv para as imagens obtidas na galeria ou câmera
* `ASSETS` (___static constant___) configurar opencv para imagens flutter em `pubspect.yaml` -> `assets/test.jpg`

## Módulo: Image Filtering


<h2 align="center">Imagem original</h2>


<p align="center"><img src="https://github.com/fgsoruco/opencv_4/blob/main/display/Test.JPG?raw=true" height = "300px"></p>

<h5 align="center"><i>from my <a href="https://www.behance.net/gallery/114930481/Jujuy">
    behance
  </a> acount</h5></i>

Alguns exemplos

## Bilateral Filter

Deve ser chamado em uma função __async__

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/bilateralFilter.JPG?raw=true" align = "right" height = "300px">


```dart

Uint8List _byte = await Cv2.bilateralFilter(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG?raw=true',
        diameter: 20,
        sigmaColor: 75,
        sigmaSpace: 75,
        borderType: Cv2.BORDER_DEFAULT,
      );

      setState(() {
        _byte;
      });

```
Mostrar resultado no widget `Image`
```dart
Image.memory(
      _byte,
      width: 300,
      height: 300,
      fit: BoxFit.fill,
    )
```


**Nota:** Se você deseja processar uma imagem da web, você deve configurar `pathFrom: CVPathFrom.URL` substituir em `pathString` 
por um url. `pathString: 'https://mir-s3-cdn-cf.behance.net/project_modules/fs/313f8e114930481.6044f05fcd866.jpeg'`


## Dilate

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/dilate.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.dilate(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG',
        kernelSize: [3, 3],
      );

      setState(() {
        _byte;
      });




```

## Filter2D

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/filter2D.JPG?raw=true" align = "right" height = "300px">

```dart

Uint8List _byte = await Cv2.filter2D(
        pathFrom: CVPathFrom.URL,
        pathString:
          'https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/634dba114930481.6044f05fcb2dd.jpeg',
        outputDepth: -1,
        kernelSize: [2, 2],
      );

      setState(() {
        _byte;
      });

```


## Median Blur

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/medianBlur.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.medianBlur(
        pathFrom: CVPathFrom.URL,
        pathString:
          'https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/16fe9f114930481.6044f05fca574.jpeg',
        kernelSize: 19,
      );

      setState(() {
        _byte;
      });

```

## MorphologyEx

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/morphologyEx.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.morphologyEx(
        pathFrom: CVPathFrom.URL,
        pathString:
          'https://mir-s3-cdn-cf.behance.net/project_modules/fs/c7da51114930481.6044f05fcc76a.jpeg',
        operation: Cv2.MORPH_TOPHAT,
        kernelSize: [5, 5],
      );

      setState(() {
        _byte;
      });
```

## PyrMeanShiftFiltering

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/pyrMeanShiftFiltering.JPG?raw=true" align = "right" height = "300px">

```dart



Uint8List _byte = await Cv2.pyrMeanShiftFiltering(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG',
        spatialWindowRadius: 20,
        colorWindowRadius: 20,
      );

      setState(() {
        _byte;
      });


```

## Scharr

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/scharr.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.scharr(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG',
        depth: Cv2.CV_SCHARR,
        dx: 0,
        dy: 1,
      );

      setState(() {
        _byte;
      });


```

## Módulo: Color Space Conversions

## CvtColor

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/cvtColor.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.cvtColor(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG',
        outputType: Cv2.COLOR_BGR2GRAY,
      );

      setState(() {
        _byte;
      });


```

## Módulo: Color Maps

## ApplyColorMap

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/applyColorMap.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.applyColorMap(
        pathFrom: CVPathFrom.URL,
        pathString:
          'https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/16fe9f114930481.6044f05fca574.jpeg',
        colorMap: Cv2.COLORMAP_JET,
      );

      setState(() {
        _byte;
      });


```
## Módulo: Miscellaneous Image Transformations

## Threshold

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/threshold.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.threshold(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG',
        thresholdValue: 150,
        maxThresholdValue: 200,
        thresholdType: Cv2.THRESH_BINARY,
      );

      setState(() {
        _byte;
      });


```

## AdaptiveThreshold

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/adaptiveThreshold.JPG?raw=true" align = "right" height = "300px">

```dart


Uint8List _byte = await Cv2.adaptiveThreshold(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG',
        maxValue: 125,
        adaptiveMethod: Cv2.ADAPTIVE_THRESH_MEAN_C,
        thresholdType: Cv2.THRESH_BINARY,
        blockSize: 11,
        constantValue: 12,
      );

      setState(() {
        _byte;
      });


```

## Errores o solicitudes
Você pode escrever solicitações de módulo e erros em [issue tracker](https://github.com/fgsoruco/opencv_4/issues).


## Donar
Para te dar uma solução melhor...

[![ko-fi](https://github.com/fgsoruco/opencv_4/blob/main/display/donate-coffee.png?raw=true)](https://paypal.me/fgsoruco)

* `BTC`: bc1qhy5uer94d4xvp2wgtfg5l6s6jk8gwj6d0ufqvh
* `BNB`: bnb17z7dqeeyrkhq2l9mx6p3hg6ewvshrpkqqzcpr9
* `ETH`: 0xb76D1F1f97eBf5B2096D5449cB3DDD2096CCB4b3