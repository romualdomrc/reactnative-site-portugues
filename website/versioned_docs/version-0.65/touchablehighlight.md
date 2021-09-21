---
id: touchablehighlight
title: TouchableHighlight
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

> Se você está procurando uma maneira mais abrangente e preparada para o futuro de lidar com a entrada baseada em toque, confira a API [Pressable](pressable.md).

Um invólucro para fazer com que as visualizações respondam corretamente aos toques. Ao pressionar o componente, a opacidade do invólucro é diminuída, o que permite que a cor da base apareça, escureça ou provoque um efeito visual de tingimento.

O efeito visual vem da relação entre o invólucro e a View, que pode afetar o layout e, às vezes, causar efeitos visuais indesejados se não for usada corretamente, por exemplo, se a BackgroundColor da View envolvida não estiver explicitamente definida como uma cor opaca.

TouchableHighlight deve ter um filho (não zero ou mais de um). Se você deseja ter vários componentes filhos, envolva-os em uma View.

```jsx
function MyComponent(props) {
  return (
    <View {...props} style={{ flex: 1, backgroundColor: '#fff' }}>
      <Text>My Component</Text>
    </View>
  );
}

<TouchableHighlight
  activeOpacity={0.6}
  underlayColor="#DDDDDD"
  onPress={() => alert('Pressed!')}>
  <MyComponent />
</TouchableHighlight>;
```

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=TouchableHighlight%20Function%20Component%20Example
import React, { useState } from "react";
import { StyleSheet, Text, TouchableHighlight, View } from "react-native";

const TouchableHighlightExample = () => {
  const [count, setCount] = useState(0);
  const onPress = () => setCount(count + 1);

  return (
    <View style={styles.container}>
      <TouchableHighlight onPress={onPress}>
        <View style={styles.button}>
          <Text>Touch Here</Text>
        </View>
      </TouchableHighlight>
      <View style={styles.countContainer}>
        <Text style={styles.countText}>
          {count ? count : null}
        </Text>
      </View>
    </View>
  );
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
  },
  countText: {
    color: "#FF00FF"
  }
});

export default TouchableHighlightExample;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=TouchableHighlight%20Class%20Component%20Example
import React, { Component } from "react";
import { StyleSheet, Text, TouchableHighlight, View } from "react-native";

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
    return (
      <View style={styles.container}>
        <TouchableHighlight onPress={this.onPress}>
          <View style={styles.button}>
            <Text>Touch Here</Text>
          </View>
        </TouchableHighlight>
        <View style={[styles.countContainer]}>
          <Text style={[styles.countText]}>
            {this.state.count ? this.state.count : null}
          </Text>
        </View>
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
  },
  countText: {
    color: "#FF00FF"
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

### `activeOpacity`

Determina qual deve ser a opacidade da exibição envolvida quando o toque está ativo. O valor deve estar entre 0 e 1. O padrão é 0,85. Requer que `UnderlayColor` seja definido.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `onHideUnderlay`

Chamado imediatamente após o underlay (efeito visual) estar oculto.

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onShowUnderlay`

Chamado imediatamente após a exibição do underlay (efeito visual).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `style`

| Type       | Required |
| ---------- | -------- |
| View.style | No       |

---

### `underlayColor`

A cor do underlay que aparecerá quando o toque estiver ativo.

| Type               | Required |
| ------------------ | -------- |
| [color](colors.md) | No       |

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

Próximo foco da TV quando acionado o botão próximo (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusLeft`

Próximo foco da TV quando acionado o botão para a esquerda (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusRight`

Próximo foco da TV quando acionado o botão para a direita (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusUp`

Próximo foco da TV (consulte a documentação do componente `View`).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `testOnly_pressed`

É útil para testes instantâneos.

| Type | Required |
| ---- | -------- |
| bool | No       |
