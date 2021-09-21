---
id: touchableopacity
title: TouchableOpacity
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

> Se você está procurando uma maneira mais abrangente e preparada para o futuro de lidar com a entrada baseada em toque, confira a API [Pressable](pressable.md).

Um invólucro para fazer com que as visualizações respondam corretamente aos toques. Ao pressionar o componente, a opacidade da View encapsulada é diminuída, diminuindo a intensidade da visualização.

A opacidade é controlada envolvendo os componentes filhos em uma `Animated.View`, que é adicionada à hierarquia de visualizações. Esteja ciente de que isso pode afetar o layout.

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=TouchableOpacity%20Function%20Component%20Example
import React, { useState } from "react";
import { StyleSheet, Text, TouchableOpacity, View } from "react-native";

const App = () => {
  const [count, setCount] = useState(0);
  const onPress = () => setCount(prevCount => prevCount + 1);

  return (
    <View style={styles.container}>
      <View style={styles.countContainer}>
        <Text>Count: {count}</Text>
      </View>
      <TouchableOpacity
        style={styles.button}
        onPress={onPress}
      >
        <Text>Press Here</Text>
      </TouchableOpacity>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingHorizontal: 10
  },
  button: {
    alignItems: "center",
    backgroundColor: "#DDDDDD",
    padding: 10
  },
  countContainer: {
    alignItems: "center",
    padding: 10
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=TouchableOpacity%20Class%20Component%20Example
import React, { Component } from "react";
import { StyleSheet, Text, TouchableOpacity, View } from "react-native";

class App extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  onPress = () => {
    this.setState({
      count: this.state.count + 1
    });
  };

  render() {
    const { count } = this.state;
    return (
      <View style={styles.container}>
        <View style={styles.countContainer}>
          <Text>Count: {count}</Text>
        </View>
        <TouchableOpacity
          style={styles.button}
          onPress={this.onPress}
        >
          <Text>Press Here</Text>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingHorizontal: 10
  },
  button: {
    alignItems: "center",
    backgroundColor: "#DDDDDD",
    padding: 10
  },
  countContainer: {
    alignItems: "center",
    padding: 10
  }
});

export default App;
```

</TabItem>
</Tabs>

---

# Reference

## Props

### [TouchableWithoutFeedback Props](touchablewithoutfeedback.md#props)

Herda [TouchableWithoutFeedback Props](touchablewithoutfeedback.md#props).

---

### `style`

| Type       | Required |
| ---------- | -------- |
| View.style | No       |

---

### `activeOpacity`

Determina qual deve ser a opacidade da exibição envolvida quando o toque está ativo. O padrão é `0,2`.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `tvParallaxProperties`

_ (Somente Apple TV) _ Objeto com propriedades para controlar efeitos de rolagem (parallax) da Apple TV.

- `Enabled`: Se `true`, os efeitos de rolagem são ativados. O padrão é `true`.
- `ShiftDistanceX`: O padrão é `2.0`.
- `ShiftDistancey`: O padrão é `2.0`.
- `tiltAngle`: O padrão é `0,05`.
- `magnification`: O padrão é `1,0`.
- `PressMagnification`: O padrão é `1.0`.
- `PressDuration`: O padrão é `0.3`.
- `PressDelay`: O padrão é `0,0`.

| Type   | Required | Platform |
| ------ | -------- | -------- |
| object | No       | iOS      |

---

### `hasTVPreferredFocus`

_ (somente Apple TV) _ Foco preferencial da TV (consulte a documentação do componente `View`).

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | iOS      |

---

### `nextFocusDown`

Próximo foco da TV quando acionado o botão para baixo (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusForward`

Próximo foco da TV quando acionado o botão para o próximo (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusLeft`

Próximo foco da TV quando acionado o botão para esquerda (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusRight`

Próximo foco da TV quando acionado o botão para direita (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusUp`

Próximo foco da TV (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |
