# Arquitectura de Redes Neuronales Convolucionales

## Martín Cogo Belver

## indice

- AlexNet
- VGG
- ResNet
- DenseNet

<style>
img {
  margin: auto;
  max-width: 100%;
  height: auto;
}
table, th, td {
  border: 1px solid black;
}
</style>

## AlexNet(2012)

- Fue Creada por Alex Krizhevsky.
- Ganadora del ImageNet challenge.
- Represento una mejora significativa respecto a LeNet.
- Primera implementación utilizando GPU's.
- Esta red demostró que las Features adquiridas mediante el aprendizaje de las red son mucho mejores que las manualmente diseñadas.  
!["LeNet vs AlexNet"](./Img/AlexNet.png)  

### Cambios que trajo AlexNet

- Utiliza la función de activación **ReLU**, a diferencia de LeNet que utiliza la función de activación **Sigmoid**.
- Para controlar la complejidad de las capas totalmente conectadas utiliza la técnica de **dropout**, a diferencia de LeNet que utiliza *weight decay*.
- Utilizo técnicas para aumentar imágenes como flipping, clipping y cambios de color.
- Una desventaja del la arquitectura es que requiere mucha memoria y poder de computo comparada con redes más modernas.  

## VGG (2014)

- VGG *Visual Geometry Group* era un grupo de la universidad de Oxford que propuso crear un esquema de bloques para construir CNN's.

- El bloque básico esta compuesto por:

1. Una *secuencia* de capas convolucionales de 3x3 con **padding** de 1 para mantener su resolución y con función de activación **ReLU**
2. Una capa de *Pooling* de tipo **max-pooling** 2x2 con **stride** de 2.

- La construcción de redes mediante estos bloques hace que la resolución decrezca rápidamente imponiendo un limite a la cantidad de capas que se pueden utilizar.  
!["AlexNet vs VGG"](./Img/VGG-Block.png)  

- La Red VGG original tienen 5 bloques convolucionales, donde los primero 2 tienen 1 capa convolucional y los otros 3 tienen 2 capas convolucionales.  
!["VGG's"](./Img/VGG.png)  

## ResNet (2015)

- Propuesta en un paper por He et al. Con la idea de que en cada capa adicional de la arquitectura debe contener más fácilmente la función que se busca.  
!["Function classes"](./Img/FunctionClasses.png)  

- Define entonces los "Residual Blocks" que se utilizan para construir la CNN.  
!["Residual Block"](./Img/ResNet-Blocks.png)  
*La idea intuitiva es que la red ya no busca aprender $f(x)$ sino que tan diferente es $f(x)$ respecto a la funcion $y = x$.*

- ResNet-18  
!["ResNet-18"](./Img/ResNet-18.png)  

## DenseNet (2017)

- Es la extension de la ResNet. ResNet descompone la función en:$$f(x)= x + g(x)$$
entonces, lo que busca DenseNet es encontrar información entre los términos sin necesariamente sumarlos, sino que concatenando.  
!["DenseNet operation"](./Img/DenseNetOperation.png)  

- Se le llama DenseNet ya que el grafo de dependencias se vuelve denso. $$x → [x, f1 (x), f2 ( [x, f1 (x)]) , f3 ([x, f1 (x) , f2 ([x, f1 (x)])]) , . . .]$$   
!["DenseNet Graph"](./Img/DenseNet-Graph.png)  

- Como cada capa que se agrega al modelo incrementa el numero de canales, añadir varias capas lleva a un modelo altamente complejo.

- Para evitar el problema de que al conectar todos los feature maps del modelo entre si sea necesario que tengan el mismo tamaño y mucha memoria.  
![""](./Img/DenseNet.png)  
Para solucionar esto se propone utilizar la conectividad solo en los "Dense Blocks" y unir los bloques con *average-pooling*.

## Comparativa sobre el dataset Fashion-MNIST

<table>
    <tr>
        <th>AlexNet</th>
        <th>VGG</th>
        <th>ResNet</th>
        <th>DenseNet</th>
    </tr>
    <tr>
        <td><img width="700" src="./Img/AlexNetPerformance.png"></td>
        <td><img width="800" src="./Img/VGGPerformance.png"></td>
        <td><img width="700" src="./Img/ResNetPerformance.png"></td>
        <td><img width="700" src="./Img/DenseNetPerformance.png"></td>
    </tr>
</table>

## Referencias

- Dive into deep learning. https://www.amazon.com/Dive-into-Learning-Aston-Zhang/dp/1009389432
- Best deep CNN architectures and their principles: from AlexNet to EfficientNet. https://theaisummer.com/cnn-architectures/#terminology
