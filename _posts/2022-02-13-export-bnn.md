---
title: "Export a binary neural network to C"
date: 2022-02-13T09:47:00.000Z
categories:
  - blog
tags:
  - geisten  - tinyML
  - c
published: false
---

After successfully training a binary neural network, we will install the generated model on the actual target platform. To run the code on as many different systems as possible, we need to convert the model into a format that is as platform-independent as possible but still efficient. The best solution for this for more than 50 years is the programming language C. It combines the desired properties such as portability and efficiency with the ability to address hardware directly while having low requirements for a runtime environment. This makes C practically unique and is also referred to as the lingua franca of programming languages. Code generation from a trained binary neural network is trivial:

```python
import codegeist as cg

# define module
class MnistModel(nn.Module):
      ...
model = MnistModel()

# build and train the model
train_model(model, ...)

#print the generated C code
print(cg.transform(model))

```

The result is a single C file containing both the trained weights, required functions, and conversion factors.
 

```c
#include <stdlib.h>
#include <stdio.h>
#include "geisten.h"

...


uint8_t input[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
unsigned int layer_0[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
int layer_1_bias[] = {...};
unsigned int layer_1[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
const unsigned int layer_2_weights[][25] = {{...}}
int layer_2[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
int layer_3_bias[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
int layer_4_bias[] = {-51028, -177514, -10425, 6707, -22223, -41041, -137751, -42726, 7424, -83931, -14338, -44805, -344, -65079, -26877, -61337, -103129, 21014, -6831, -99731, -36819, -69708, -139073, -52130, 1137, -86182, -8399, -32446, -80859, -110330, -91849, -30346, -169595, -79392, -47715, -187554, 144, -89737, 2541, -60858, -72935, -85458, -105005, -2720, -20956, -41462, -32535, -79150, -124511, -5307, -73426, -75315, -67713, -62697, -6364, -27507, -14118, -126685, -98312, -40468, -11523, -166940, -119908, -12682, -103693, -84629, -59240, -156695, -32011, -84625, -57023, -113155, -68135, 12033, -58450, -38763, -93903, -69663, -114359, -154117, -92771, -116732, -5278, -63334, -1935, -51701, -99577, -8243, -65781, -11279, -46434, -38463, -77059, -1551, -91616, -19041, -62651, -109725, -104325, -4481, -56223, 804, -106304, -54765, -76797, -131053, -127090, -163639, -110418, -23991, 5962, -125626, -21356, 6016, -125078, 10298, -16452, -75272, -51389, -43853};
...
int layer_5[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
unsigned int layer_6[] = {0};

int main(void) {

    // attempt to read the array of type int and store
    // the value in the "input" array
    while (fread(input, sizeof(uint8_t), 784, stdin) == 784) {
        binarize_scaled_activation(784, input, 100000, layer_1_bias, layer_1);
        linear2d(784, 120, layer_2_weights, layer_1, layer_2);
        prelu2d(120, layer_2, 1, layer_3_bias, layer_2);
        binarize_scaled_activation(120, layer_2, 100000, layer_4_bias, layer_4);
        linear2d(120, 10, layer_5_weights, layer_4, layer_5);
        layer_6[0] = argmax(10, layer_5);
        printf("%d\n", layer_6[0]);
    }
    return EXIT_SUCCESS;
}
```

The above example represents implementing a simple neural network to process the MNIST database. The data is imported via the C stdin stream, processed, and the identified number is written to the stdout stream. 


Nachdem wir erfolgreich ein binäres neuronales Netz erstellt haben werden wir es in ein C - Programm umwandeln damit wir es nativ auf beliebigen Systemen ausführen können.

Wir werden keine Decimalzahlen verwenden, da wir davon ausgehen, dass nicht jedes System ein floatingppoint unit besitzt. Daraus folgt, dass wir die floating point Werte zunächst in Integerwerte umwandeln müssen.  

```c
float f = 0.4;
int resolution = 1000;
int n = f * resolution; //integer value
```

Nun ist es jedoch so, dass in pytorch und in den meisten anderen Frameworks die Eingabewerte in float Werte umgewandelt werden, damit das training vereinfacht wird. 

Die meisten gemessenen Eingabedaten liegen jedoch als integer Werte vor. Da die Werte binarieisert werden muss der Schwellwert angepasst werden.

$$
y = \begin{cases} +1 & x \ge \alpha \\ -1 & x < \alpha \end{cases}
$$

$$
\alpha_n = \alpha * r
$$

Damit haben wir elegant die transformation von decimalwerten nach integerwerten umgesetzt und abgeschlossen. Die restlichen Layer können ganz normal mit den bestehenden umrechnungswerten berechnet werden.
