---
id: toastandroid
title: ToastAndroid
---

A API ToastAndroid do React Native expõe o módulo ToastAndroid da plataforma Android como um módulo JS. Ele fornece o método `show (mensagem, duração) `que usa os seguintes parâmetros:

- _message_ Uma string com o texto a brindar
- _duration_ A duração do brinde - `ToastAndroid.short` ou `ToastAndroid.long`

Como alternativa, você pode usar `ShowWithGravity (mensagem, duração, gravidade) `para especificar onde o brinde aparece no layout da tela. Pode ser `ToastAndroid.top`, `ToastAndroid.bottom` ou `ToastAndroid.center`.

O método 'ShowWithGravityAndOffset (mensagem, duração, gravidade, xOffset, yOffset) 'adiciona a capacidade de especificar um deslocamento em pixels.

```SnackPlayer name=Toast%20Android%20API%20Example&supportedPlatforms=android
import React from "react";
import { View, StyleSheet, ToastAndroid, Button, StatusBar } from "react-native";

const App = () => {
  const showToast = () => {
    ToastAndroid.show("A pikachu appeared nearby !", ToastAndroid.SHORT);
  };

  const showToastWithGravity = () => {
    ToastAndroid.showWithGravity(
      "All Your Base Are Belong To Us",
      ToastAndroid.SHORT,
      ToastAndroid.CENTER
    );
  };

  const showToastWithGravityAndOffset = () => {
    ToastAndroid.showWithGravityAndOffset(
      "A wild toast appeared!",
      ToastAndroid.LONG,
      ToastAndroid.BOTTOM,
      25,
      50
    );
  };

  return (
    <View style={styles.container}>
      <Button title="Toggle Toast" onPress={() => showToast()} />
      <Button
        title="Toggle Toast With Gravity"
        onPress={() => showToastWithGravity()}
      />
      <Button
        title="Toggle Toast With Gravity & Offset"
        onPress={() => showToastWithGravityAndOffset()}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: StatusBar.currentHeight,
    backgroundColor: "#888888",
    padding: 8
  }
});

export default App;
```

### Hack imperativo

A API ToastAndroid é imperativa, mas há uma maneira de expor um componente declarativo dela, como neste exemplo:

```Snack Player Name=Advanced%20Toasta076FCA089DBD5Z0NDROID%20API%20EX Amostra e Plataformas Suportadas=Android
importar React, {useState, useEffect} de “react”;
import {View, StyleSheet, ToastAndroid, Button, StatusBar} de “react-native”;

const Toast = ({visível, mensagem}) => {
 if (visível) {
 brinde android. mostrar com gravidade e offset (
 mensagem,
 Brinde para Android. longo,
 Brinde para Android. inferior,
 25,
 50
 );
 retorno nulo;
 }
 retorno nulo;
};

const App = () => {
 const [VisIBLEToast, setVisIBLEToast] = UseState (false);

 useEffect (() => setVisibleToast (false), [VisibleToast]);

 const handleButtonPress = () => {
 setVisíbleToast (verdadeiro);
 };

 retorno (
 <View style={styles.container}> 
 <Toast visible={visibleToast} message="Example" /> 
 <Button title="Toggle Toast" onPress={() => Pressione o botão da alça ()} />
 </View> 
 );
};

const styles = StyleSheet.create ({
 recipiente: {
 flex: 1,
 Justificar conteúdo: “centro”,
 PaddingTop: barra de status. Altura atual,
 Cor de Fundo: "#888888 “,
 estofamento: 8
 }
});

exportar aplicativo padrão;
```

---

# Referência

## Métodos

### `show()`

```jsx
static show(message, duration)
```

---

### `showWithGravity()`

```jsx
static showWithGravity(message, duration, gravity)
```

---

### `showWithGravityAndOffset()`

```jsx
static showWithGravityAndOffset(message, duration, gravity, xOffset, yOffset)
```

## Propriedades

### `SHORT`

Indica a duração na tela.

```jsx
ToastAndroid.SHORT;
```

---

### `LONG`

Indica a duração na tela.

```jsx
ToastAndroid.LONG;
```

---

### `TOP`

Indica a posição na tela.

```jsx
ToastAndroid.TOP;
```

---

### `BOTTOM`

Indica a posição na tela.

```jsx
ToastAndroid.BOTTOM;
```

---

### `CENTER`

Indica a posição na tela.

```jsx
ToastAndroid.CENTER;
```
