---
id: panresponder
title: PanResponder
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

`PanResponder` reconcilia vários toques em um único gesto. Ele torna os gestos de toque único resilientes a toques extras e pode ser usado para reconhecer gestos multitoque básicos.

Por padrão, `PanResponder` mantém um identificador `InteractionManager` para bloquear eventos JS de longa duração de interromper gestos ativos.

Ele fornece um invólucro previsível dos manipuladores de resposta fornecidos pelo [sistema de resposta a gestos] (gesture-responder-system.md). Para cada manipulador, ele fornece um novo objeto `GestureState` ao lado do objeto de evento nativo:

```
onPanResponderMove: (event, gestureState) => {}
```

Um evento nativo é um evento de toque sintético com a forma de [PressEvent] (pressevent).

Um objeto `GestureState` tem o seguinte:

- `StateId` - ID do GestureState - persistiu enquanto houver pelo menos um toque na tela
- `MOVEX` - as últimas coordenadas de tela do toque movido recentemente
- `Movey` - as últimas coordenadas de tela do toque movido recentemente
- `x0` - as coordenadas da tela da concessão do respondente
- `y0` - as coordenadas da tela da concessão do respondente
- `dx` - distância acumulada do gesto desde o início do toque
- `dy` - distância acumulada do gesto desde o início do toque
- `vx` - velocidade atual do gesto
- `vy` - velocidade atual do gesto
- `NumberActiveTouches` - Número de toques atualmente na tela

## Padrão de uso

```jsx
const ExampleComponent = () => {
  const panResponder = React.useRef(
    PanResponder.create({
      // Ask to be the responder:
      onStartShouldSetPanResponder: (evt, gestureState) => true,
      onStartShouldSetPanResponderCapture: (evt, gestureState) =>
        true,
      onMoveShouldSetPanResponder: (evt, gestureState) => true,
      onMoveShouldSetPanResponderCapture: (evt, gestureState) =>
        true,

      onPanResponderGrant: (evt, gestureState) => {
        // The gesture has started. Show visual feedback so the user knows
        // what is happening!
        // gestureState.d{x,y} will be set to zero now
      },
      onPanResponderMove: (evt, gestureState) => {
        // The most recent move distance is gestureState.move{X,Y}
        // The accumulated gesture distance since becoming responder is
        // gestureState.d{x,y}
      },
      onPanResponderTerminationRequest: (evt, gestureState) =>
        true,
      onPanResponderRelease: (evt, gestureState) => {
        // The user has released all touches while this view is the
        // responder. This typically means a gesture has succeeded
      },
      onPanResponderTerminate: (evt, gestureState) => {
        // Another component has become the responder, so this gesture
        // should be cancelled
      },
      onShouldBlockNativeResponder: (evt, gestureState) => {
        // Returns whether this component should block native components from becoming the JS
        // responder. Returns true by default. Is currently only supported on android.
        return true;
      }
    })
  ).current;

  return <View {...panResponder.panHandlers} />;
};
```

## Exemplo

`PanResponder` funciona com a API `Animated` para ajudar a criar gestos complexos na interface do usuário. O exemplo a seguir contém um componente animado `View` que pode ser arrastado livremente pela tela

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=PanResponder
import React, { useRef } from "react";
import { Animated, View, StyleSheet, PanResponder, Text } from "react-native";

const App = () => {
  const pan = useRef(new Animated.ValueXY()).current;

  const panResponder = useRef(
    PanResponder.create({
      onMoveShouldSetPanResponder: () => true,
      onPanResponderGrant: () => {
        pan.setOffset({
          x: pan.x._value,
          y: pan.y._value
        });
      },
      onPanResponderMove: Animated.event(
        [
          null,
          { dx: pan.x, dy: pan.y }
        ]
      ),
      onPanResponderRelease: () => {
        pan.flattenOffset();
      }
    })
  ).current;

  return (
    <View style={styles.container}>
      <Text style={styles.titleText}>Drag this box!</Text>
      <Animated.View
        style={{
          transform: [{ translateX: pan.x }, { translateY: pan.y }]
        }}
        {...panResponder.panHandlers}
      >
        <View style={styles.box} />
      </Animated.View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  titleText: {
    fontSize: 14,
    lineHeight: 24,
    fontWeight: "bold"
  },
  box: {
    height: 150,
    width: 150,
    backgroundColor: "blue",
    borderRadius: 5
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=PanResponder
import React, { Component } from "react";
import { Animated, View, StyleSheet, PanResponder, Text } from "react-native";

class App extends Component {
  pan = new Animated.ValueXY();
  panResponder = PanResponder.create({
    onMoveShouldSetPanResponder: () => true,
    onPanResponderGrant: () => {
      this.pan.setOffset({
        x: this.pan.x._value,
        y: this.pan.y._value
      });
    },
    onPanResponderMove: Animated.event([
      null,
      { dx: this.pan.x, dy: this.pan.y }
    ]),
    onPanResponderRelease: () => {
      this.pan.flattenOffset();
    }
  });

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.titleText}>Drag this box!</Text>
        <Animated.View
          style={{
            transform: [{ translateX: this.pan.x }, { translateY: this.pan.y }]
          }}
          {...this.panResponder.panHandlers}
        >
          <View style={styles.box} />
        </Animated.View>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  titleText: {
    fontSize: 14,
    lineHeight: 24,
    fontWeight: "bold"
  },
  box: {
    height: 150,
    width: 150,
    backgroundColor: "blue",
    borderRadius: 5
  }
});

export default App;
```

</TabItem>
</Tabs>

Try the [PanResponder example in RNTester](https://github.com/facebook/react-native/blob/master/packages/rn-tester/js/examples/PanResponder/PanResponderExample.js).

---

# Referência

## Métodos

### `create()`

```jsx
static create(config)
```

**Parâmetros: **

| Nome                                                        | Tipo   | Descrição |
| ----------------------------------------------------------- | ------ | ----------- |
| config <div className="label basic required">Required</div> | object | Consulte abaixo |

O objeto `config` fornece versões aprimoradas de todos os retornos de chamada do respondente que fornecem não apenas o [`PressEvent`] (pressevent), mas também o estado do gesto `PanResponder`, substituindo a palavra `Responder` por `PanResponder` em cada um dos retornos de chamada `OnResponder*` típicos. Por exemplo, o objeto `config` seria semelhante a:

- `onMoveShouldSetPanResponder: (e, gestureState) => {...}`
- `onMoveShouldSetPanResponderCapture: (e, gestureState) => {...}`
- `onStartShouldSetPanResponder: (e, gestureState) => {...}`
- `onStartShouldSetPanResponderCapture: (e, gestureState) => {...}`
- `onPanResponderReject: (e, gestureState) => {...}`
- `onPanResponderGrant: (e, gestureState) => {...}`
- `onPanResponderStart: (e, gestureState) => {...}`
- `onPanResponderEnd: (e, gestureState) => {...}`
- `onPanResponderRelease: (e, gestureState) => {...}`
- `onPanResponderMove: (e, gestureState) => {...}`
- `onPanResponderTerminate: (e, gestureState) => {...}`
- `onPanResponderTerminationRequest: (e, gestureState) => {...}`
- `onShouldBlockNativeResponder: (e, gestureState) => {...}`

Em geral, para eventos que têm equivalentes de captura, atualizamos o GestureState uma vez na fase de captura e também podemos usá-lo na fase de bolha.

Tenha cuidado com retornos de chamada `OnStartShould*`. Eles refletem apenas `GestureState` atualizado para eventos de início/fim que fazem bolhas/capturam para o nó. Uma vez que o nó é o respondente, você pode confiar em cada evento inicial/final sendo processado pelo gesto e `GestureState` sendo atualizado de acordo. (NumberActiveTouches) pode não ser totalmente preciso, a menos que você seja o respondente.
