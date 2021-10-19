---
id: imagebackground
title: ImageBackground
---

Um pedido comum entre desenvolvedores da web é o `background-image`. Pra dar uma moral pra eles, tem o componente `<ImageBackground>`, que tem as mesmas propriedades do `<Image>` e adiciona quaisquer filhos que você deseja em cima dele.

As vezes não é legal usar `<ImageBackground>` porque a implementação dele é básica. Da uma olhada no [código fonte](https://github.com/facebook/react-native/blob/master/Libraries/Image/ImageBackground.js) pra ter uma ideia e crie seu próprio componente quando precisar.

Note que você precisa especificar width e height nos atributos de estilo.

## Exemplo

```SnackPlayer name=ImageBackground
import React from "react";
import { ImageBackground, StyleSheet, Text, View } from "react-native";

const image = { uri: "https://reactjs.org/logo-og.png" };

const App = () => (
  <View style={styles.container}>
    <ImageBackground source={image} resizeMode="cover" style={styles.image}>
      <Text style={styles.text}>Inside</Text>
    </ImageBackground>
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  image: {
    flex: 1,
    justifyContent: "center"
  },
  text: {
    color: "white",
    fontSize: 42,
    lineHeight: 84,
    fontWeight: "bold",
    textAlign: "center",
    backgroundColor: "#000000c0"
  }
});

export default App;
```

---

# Referência

## Props

### [Image Props](image.md#props)

Herda [Image Props](image.md#props).

---

### `imageStyle`

| Type                                |
| ----------------------------------- |
| [Image Style](image-style-props.md) |

---

### `imageRef`

Permite setar uma referencia pro componente `Image` que está do lado de dentro.

| Type                                                  |
| ----------------------------------------------------- |
| [Ref](https://reactjs.org/docs/refs-and-the-dom.html) |

---

### `style`

| Type                              |
| --------------------------------- |
| [View Style](view-style-props.md) |
