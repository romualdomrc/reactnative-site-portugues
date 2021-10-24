---
id: usewindowdimensions
title: useWindowDimensions
---

```jsx
import { useWindowDimensions } from 'react-native';
```

`UseWindowDimensions` atualiza automaticamente os valores de `largura` e `altura` quando o tamanho da tela muda. Você pode obter a largura e a altura da janela do aplicativo da seguinte forma:

```jsx
const { height, width } = useWindowDimensions();
```

## Exemplo

```SnackPlayer name=useWindowDimensions&supportedPlatforms=ios,android
import React from "react";
import { View, StyleSheet, Text, useWindowDimensions } from "react-native";

const App = () => {
  const window = useWindowDimensions();
  return (
    <View style={styles.container}>
      <Text>{`Window Dimensions: height - ${window.height}, width - ${window.width}`}</Text>
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  }
});

export default App;
```

- The [useDimensions](https://github.com/react-native-community/react-native-hooks#usedimensions) hook from the community [React native hooks](https://github.com/react-native-community/react-native-hooks) library aims to make handling screen/window size changes easier to work with.
- [React Native Responsive Dimensions](https://github.com/DaniAkash/react-native-responsive-dimensions) also comes with responsive hooks.

## Properties

### `fontScale`

```jsx
useWindowDimensions().fontScale;
```

A escala da fonte usada atualmente. Alguns sistemas operacionais permitem que os usuários dimensionem seus tamanhos de fonte maiores ou menores para maior conforto de leitura. Esta propriedade permitirá que você saiba o que está em vigor.

---

### `height`

```jsx
useWindowDimensions().height;
```

A altura em pixels da janela ou da tela que seu aplicativo ocupa.

---

### `scale`

```jsx
useWindowDimensions().scale;
```

A proporção de pixels do dispositivo em que seu aplicativo está sendo executado.

> Um valor de `1` indica PPI/DPI de 96 (76 em algumas plataformas). `2` indica uma tela Retina ou DPI alto.

---

### `width`

```jsx
useWindowDimensions().width;
```

A largura, em pixels, da janela ou da tela que o aplicativo ocupa.
