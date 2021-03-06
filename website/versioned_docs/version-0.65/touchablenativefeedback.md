---
id: touchablenativefeedback
title: TouchableNativeFeedback
---

> Se você está procurando uma maneira mais abrangente e preparada para o futuro de lidar com a entrada baseada em toque, confira a API [Pressable] (pressable.md).

Um invólucro para fazer com que as visualizações respondam corretamente aos toques (somente Android). No Android, esse componente usa o drawable de estado nativo para exibir feedback de toque.

No momento, ele só suporta ter uma única instância View como um nó filho, pois é implementado substituindo essa View por outra instância do nó RctView com algumas propriedades adicionais definidas.

O drawable de fundo do feedback nativo tocável pode ser personalizado com a propriedade `background`.

## Exemplo

```SnackPlayer name=TouchableNativeFeedback%20Android%20Component%20Example&supportedPlatforms=android
import React, { useState } from "react";
import { Text, View, StyleSheet, TouchableNativeFeedback, StatusBar } from "react-native";

const App = () => {
  const [rippleColor, setRippleColor] = useState(randomHexColor());
  const [rippleOverflow, setRippleOverflow] = useState(false);
  return (
    <View style={styles.container}>
      <TouchableNativeFeedback
        onPress={() => {
          setRippleColor(randomHexColor());
          setRippleOverflow(!rippleOverflow);
        }}
        background={TouchableNativeFeedback.Ripple(rippleColor, rippleOverflow)}
      >
        <View style={styles.touchable}>
          <Text style={styles.text}>TouchableNativeFeedback</Text>
        </View>
      </TouchableNativeFeedback>
    </View>
  );
};

const randomHexColor = () => {
  return "#000000".replace(/0/g, function() {
    return (~~(Math.random() * 16)).toString(16);
  });
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: StatusBar.currentHeight,
    backgroundColor: "#ecf0f1",
    padding: 8
  },
  touchable: { flex: 0.5, borderColor: "black", borderWidth: 1 },
  text: { alignSelf: "center" }
});

export default App;
```

---

# Reference

## Props

### [TouchableWithoutFeedback Props](touchablewithoutfeedback.md#props)

Inherits [TouchableWithoutFeedback Props](touchablewithoutfeedback.md#props).

---

### `background`

Determines the type of background drawable that's going to be used to display feedback. It takes an object with `type` property and extra data depending on the `type`. It's recommended to use one of the static methods to generate that dictionary.

| Type               | Required |
| ------------------ | -------- |
| backgroundPropType | No       |

---

### `useForeground`

Set to true to add the ripple effect to the foreground of the view, instead of the background. This is useful if one of your child views has a background of its own, or you're e.g. displaying images, and you don't want the ripple to be covered by them.

Check TouchableNativeFeedback.canUseNativeForeground() first, as this is only available on Android 6.0 and above. If you try to use this on older versions you will get a warning and fallback to background.

| Type | Required |
| ---- | -------- |
| bool | No       |

---

### `hasTVPreferredFocus`

TV preferred focus (see documentation for the View component).

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | Android  |

---

### `nextFocusDown`

TV next focus down (see documentation for the View component).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusForward`

TV next focus forward (see documentation for the View component).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusLeft`

TV next focus left (see documentation for the View component).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusRight`

TV next focus right (see documentation for the View component).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusUp`

TV next focus up (see documentation for the View component).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

## Methods

### `SelectableBackground()`

```jsx
static SelectableBackground(rippleRadius: ?number)
```

Cria um objeto que representa o plano de fundo padrão do tema android para elementos selecionáveis (? Android: ATTR/Fundo de Ítem selecionável). O parâmetro `RippleRadius` controla o raio do efeito cascata.

---

### `SelectableBackgroundBorderless()`

```jsx
static SelectableBackgroundBorderless(rippleRadius: ?number)
```

Cria um objeto que representa o plano de fundo padrão do tema android para elementos selecionáveis sem bordas (? Android: ATTR/selecionável em segundo plano (sem borda). Disponível na API android nível 21+. O parâmetro `RippleRadius` controla o raio do efeito cascata.

---

### `Ripple()`

```jsx
static Ripple(color: string, borderless: boolean, rippleRadius: ?number)
```

Cria um objeto que representa desenhável ondulado com cor especificada (como uma string). Se a propriedade `borderless` for avaliada como verdadeira, a ondulação será renderizada fora dos limites da visualização (veja os botões nativos da barra de ação como um exemplo desse comportamento). Esse tipo de plano de fundo está disponível na API do Android nível 21+.

**Parâmetros: **

| Nome         | Tipo    | Required | Descrição                                 |
| ------------ | ------- | -------- | ------------------------------------------- |
| color        | string  | Yes      | A cor ondulada                            |
| borderless   | boolean | Yes      | Se a ondulação puder renderizar fora de seus limites |
| rippleRadius | ?number | No       | controla o raio do efeito cascata    |

---

### `canUseNativeForeground()`

```jsx
static canUseNativeForeground()
```
