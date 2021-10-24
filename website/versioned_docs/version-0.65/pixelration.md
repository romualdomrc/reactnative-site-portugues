---
id: pixelratio
title: PixelRatio
---

`PixelRatio` dá acesso à densidade de pixels e à escala de fonte do dispositivo.

## Obtendo uma imagem com o tamanho correto

Você deve obter uma imagem de resolução mais alta se estiver em um dispositivo de alta densidade de pixels. Uma boa regra é multiplicar o tamanho da imagem exibida pela proporção de pixels.

```jsx
var image = getImage({
  width: PixelRatio.getPixelSizeForLayoutSize(200),
  height: PixelRatio.getPixelSizeForLayoutSize(100)
});
<Image source={image} style={{ width: 200, height: 100 }} />;
```

## Ajuste de grade de pixels

No iOS, você pode especificar posições e dimensões para elementos com precisão arbitrária, por exemplo, 29.674825. Mas, em última análise, a tela física tem apenas um número fixo de pixels, por exemplo 640 × 1136 para iPhone SE (1ª geração) ou 828 × 1792 para iPhone 11. O iOS tenta ser o mais fiel possível ao valor do usuário espalhando um pixel original em vários para enganar o olho. A desvantagem dessa técnica é que ela faz com que o elemento resultante pareça desfocado.

Na prática, descobrimos que os desenvolvedores não querem esse recurso e precisam contornar isso fazendo o arredondamento manual para evitar elementos borrados. No React Native, estamos arredondando todos os pixels automaticamente.

Temos que ter cuidado quando fazer esse arredondamento. Você nunca quer trabalhar com valores arredondados e não arredondados ao mesmo tempo em que acumulará erros de arredondamento. Ter um erro de arredondamento é mortal porque uma borda de um pixel pode desaparecer ou ser duas vezes maior.

No React Native, tudo em JavaScript e dentro do mecanismo de layout funciona com números de precisão arbitrários. É somente quando definimos a posição e as dimensões do elemento nativo no segmento principal que arredondamos. Além disso, o arredondamento é feito em relação à raiz e não ao pai, novamente para evitar o acúmulo de erros de arredondamento.

## Exemplo

```SnackPlayer name=PixelRatio%20Example
import React from "react";
import { Image, PixelRatio, ScrollView, StyleSheet, Text, TextInput, View } from "react-native";

const size = 50;
const cat = {
  uri: "https://reactnative.dev/docs/assets/p_cat1.png",
  width: size,
  height: size
};

const App = () => (
  <ScrollView style={styles.scrollContainer}>
    <View style={styles.container}>
      <Text>Current Pixel Ratio is:</Text>
      <Text style={styles.value}>{PixelRatio.get()}</Text>
    </View>
    <View style={styles.container}>
      <Text>Current Font Scale is:</Text>
      <Text style={styles.value}>{PixelRatio.getFontScale()}</Text>
    </View>
    <View style={styles.container}>
      <Text>On this device images with a layout width of</Text>
      <Text style={styles.value}>{size} px</Text>
      <Image source={cat} />
    </View>
    <View style={styles.container}>
      <Text>require images with a pixel width of</Text>
      <Text style={styles.value}>
        {PixelRatio.getPixelSizeForLayoutSize(size)} px
      </Text>
      <Image
        source={cat}
        style={{
          width: PixelRatio.getPixelSizeForLayoutSize(size),
          height: PixelRatio.getPixelSizeForLayoutSize(size)
        }}
      />
    </View>
  </ScrollView>
);

const styles = StyleSheet.create({
  scrollContainer: {
    flext: 1,
    marginTop: "2em",
    justifyContent: "center",
  },
  container: {
    justifyContent: "center",
    alignItems: "center"
  },
  value: {
    fontSize: 24,
    marginBottom: 12,
    marginTop: 4
  }
});

export default App;
```

---

# Reference

## Methods

### `get()`

```jsx
static get()
```

Retorna a densidade de pixels do dispositivo. Alguns exemplos:

- `PixelRatio.get() === 1`
  - [mdpi Android devices](https://material.io/tools/devices/)
- `PixelRatio.get() === 1.5`
  - [hdpi Android devices](https://material.io/tools/devices/)
- `PixelRatio.get() === 2`
  - iPhone SE, 6S, 7, 8
  - iPhone XR
  - iPhone 11
  - [xhdpi Android devices](https://material.io/tools/devices/)
- `PixelRatio.get() === 3`
  - iPhone 6S Plus, 7 Plus, 8 Plus
  - iPhone X, XS, XS Max
  - iPhone 11 Pro, 11 Pro Max
  - Pixel, Pixel 2
  - [xxhdpi Android devices](https://material.io/tools/devices/)
- `PixelRatio.get() === 3.5`
  - Nexus 6
  - Pixel XL, Pixel 2 XL
  - [xxxhdpi Android devices](https://material.io/tools/devices/)

---

### `getFontScale()`

```jsx
static getFontScale(): number
```

Retorna o fator de escala para tamanhos de fonte. Essa é a proporção usada para calcular o tamanho absoluto da fonte, portanto, qualquer elemento que dependa muito disso deve usar isso para fazer cálculos.

- no valor do Android reflete a preferência do usuário definida em**Configurações > Exibição > Tamanho da font**
- no iOS, o valor reflete a preferência do usuário definida em**Configurações > Tela e brilho > Tamanho do texto**, o valor também pode ser atualizado em**Configurações > Acessibilidade > Tamanho da tela e do texto > Texto maior**

Se uma escala de fonte não estiver definida, isso retornará a proporção de pixels do dispositivo.

---

### `getPixelSizeForLayoutSize()`

```jsx
static getPixelSizeForLayoutSize(layoutSize: number): number
```

Converte um tamanho de layout (dp) em tamanho de pixel (px).

Garantido para retornar um número inteiro.

---

### `roundToNearestPixel()`

```jsx
static roundToNearestPixel(layoutSize: number): number
```

Arredonda um tamanho de layout (dp) para o tamanho de layout mais próximo que corresponde a um número inteiro de pixels. Por exemplo, em um dispositivo com um PixelRatio de 3, `PixelRatio.RoundTonearestPixel (8,4) = 8,33`, o que corresponde exatamente a (8,33\ * 3) = 25 pixels.
