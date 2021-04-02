<p align="center"><img src="https://github.com/fgsoruco/opencv_4/blob/main/display/cover_1.gif?raw=true"/></p>

<h1 align="center">OpenCV_4</h1>

<p align="center">Este paquete contiene la implementación de módulos OpenCV, la versión utilizada es 4.3.0 tanto para plataformas Android como iOS.</p><br>

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

- [Acerca de esta versión](#acerca-de-esta-versión)
- [Instalando](#instalando)
- [Cómo utilizar](#cómo-utilizar)
- [Ejemplos](#módulo-image-filtering)
  - [Image Filtering](#módulo-image-filtering)
  - [Color Space Conversions](#módulo-color-space-conversions)
  - [Color Maps](#módulo-color-maps)
  - [Miscellaneous Image Transformations](#módulo-miscellaneous-image-transformations)
- [Errores o solicitudes](#errores-o-solicitudes)
- [Donar](#Donar)


# Acerca de esta versión

## Compatibilidad
* Esta desarrollada para la integración la librería de visión artificial OpenCV en su versión 4.3.0
* Es compatible con Android e iOS.
* Se tuvo en cuenta la integración sencilla con paquetes populares de flutter como [image_picker](https://pub.dev/packages/image_picker) para procesar imágenes de la galería o la camara, puedes ver el ejemplo de implementación [aquí](https://pub.dev/packages/opencv_4/example), en este caso necesitas configurar tu proyecto con [Nullsafety](#cómo-utilizar)..

* Los módulos de OpenCV empleados son los siguientes:
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
   



## Procesamiento
* Todos los procesamientos son a través del path de la imagen.
* Imágenes en flutter a travez de la carpeta asset configurada. __Default__
* Imágenes en la web.
* Imágenes de la galería o camara usando [image_picker](https://pub.dev/packages/image_picker)

## Sintaxis
* Parecida a Phyton para llamada a métodos y constantes de procesamiento de imagen por ejemplo 
  * `Cv2.ctvColor` 
  * `Cv2.COLOR_BGR2GRAY`

<!-- ## Proximanente
* Implementación de más módulos de OpenCV, sé está trabajando en ello.
* Procesamiento de videos y gif animados, sé está trabajando en ello. -->

# Instalando

### 1. Dependencias

Agregue esto al archivo `pubspec.yaml` de su paquete:

```yaml
dependencies:
  opencv_4: ^1.0.0
```

### 2. Instalar

Puede instalar paquetes desde la línea de comandos:


```
$ flutter pub get
```

### 3. Importar el paquete

Ahora en su código `Dart`, puede usar:

```dart
import 'package:opencv_4/opencv_4.dart';
```

# Cómo utilizar

## Pre requisitos
1. Android: requiere la mínima versión 21 en el proyecto `android (folder) -> app (folder) -> build.gradle`

```gradle
defaultConfig {
    ...
    minSdkVersion 21
    ...
}
```
2. Si se va a trabajar con el path de assets flutter no requiere permisos ni en Android e iOS.
3. Si se desea trabajar con imágenes de la web no requiere configuración.
4. Si se va a utilizar el paquete [image_picker](https://pub.dev/packages/image_picker) para trabajar con imágenes de la camara y galería, seguir su configuración de permisos para [Android e iOS](https://pub.dev/packages/image_picker#installation).
4. `Nullsafety` si vas a utilizar el [ejemplo](https://pub.dev/packages/opencv_4/example) debes configurar el archivo `pubspect.yaml`

```yaml
environment:
  sdk: ">=2.12.0 <3.0.0"
```


## Classes
`Cv2`: Clase que contiene la implementación de módulos y constantes de OpenCV

`CVPathFrom`: Permite configurar la ruta para procesar las imágenes.
* `URL` (___static constant___) configurar opencv para imágenes web
* `GALLERY_CAMERA` (___static constant___) configurar opencv para las imágenes obtenidas de la galeria o camara
* `ASSETS` (___static constant___) configurar opencv para imágenes de flutter en `pubspect.yaml` -> `assets/test.jpg`

## Módulo: Image Filtering


<h2 align="center">Imagen original</h2>

<p align="center"><img src="https://github.com/fgsoruco/opencv_4/blob/main/display/Test.JPG?raw=true" height = "300px"></p>


<h5 align="center"><i>from my <a href="https://www.behance.net/gallery/114930481/Jujuy">
    behance
  </a> acount</h5></i>

Algunos ejemplos

## Bilateral Filter

Debe ser llamado dentro de una función __async__

<img src="https://github.com/fgsoruco/opencv_4/blob/main/display/bilateralFilter.JPG?raw=true" align = "right" height = "300px">


```dart

Uint8List _byte = await Cv2.bilateralFilter(
        pathFrom: CVPathFrom.ASSETS,
        pathString: 'assets/Test.JPG',
        diameter: 20,
        sigmaColor: 75,
        sigmaSpace: 75,
        borderType: Cv2.BORDER_DEFAULT,
      );

      setState(() {
        _byte;
      });

```
Mostrar resultado en un widget `Image`
```dart
Image.memory(
      _byte,
      width: 300,
      height: 300,
      fit: BoxFit.fill,
    )
```


**Nota:** Si quieres procesar una imagen de la web debes configurar `pathFrom: CVPathFrom.URL` remplazar en `pathString` por una URL por ejemplo. `pathString: 'https://mir-s3-cdn-cf.behance.net/project_modules/fs/313f8e114930481.6044f05fcd866.jpeg'`


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
Puedes escribir solicitudes de módulos y errores en [issue tracker](https://github.com/fgsoruco/opencv_4/issues).


## Donar
Para darte una mejor solución...

[![ko-fi](https://github.com/fgsoruco/opencv_4/blob/main/display/donate-coffee.png?raw=true)](https://paypal.me/fgsoruco)

* `BTC`: bc1qhy5uer94d4xvp2wgtfg5l6s6jk8gwj6d0ufqvh
* `BNB`: bnb17z7dqeeyrkhq2l9mx6p3hg6ewvshrpkqqzcpr9
* `ETH`: 0xb76D1F1f97eBf5B2096D5449cB3DDD2096CCB4b3