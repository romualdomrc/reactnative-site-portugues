---
id: layoutanimation
title: LayoutAnimation
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Anima automaticamente as visualizações para as novas posições quando o próximo layout acontecer.

Uma maneira comum de usar essa API é chamá-la antes de atualizar o gancho de estado em componentes funcionais e chamar `setState` em componentes de classe.

Observe que, para que isso funcione em**Android**, você precisa definir os seguintes sinalizadores via `UIManager`:

```js
if (Platform.OS === 'android') {
  if (UIManager.setLayoutAnimationEnabledExperimental) {
    UIManager.setLayoutAnimationEnabledExperimental(true);
  }
}
```

## Exemplo

```SnackPlayer name=LayoutAnimation&supportedPlatforms=android,ios
import React, { useState } from "react";
import { LayoutAnimation, Platform, StyleSheet, Text, TouchableOpacity, UIManager, View } from "react-native";

if (
  Platform.OS === "android" &&
  UIManager.setLayoutAnimationEnabledExperimental
) {
  UIManager.setLayoutAnimationEnabledExperimental(true);
}
const App = () => {
  const [expanded, setExpanded] = useState(false);

  return (
    <View style={style.container}>
      <TouchableOpacity
        onPress={() => {
          LayoutAnimation.configureNext(LayoutAnimation.Presets.spring);
          setExpanded(!expanded);
        }}
      >
        <Text>Press me to {expanded ? "collapse" : "expand"}!</Text>
      </TouchableOpacity>
      {expanded && (
        <View style={style.tile}>
          <Text>I disappear sometimes!</Text>
        </View>
      )}
    </View>
  );
};

const style = StyleSheet.create({
  tile: {
    backgroundColor: "lightgrey",
    borderWidth: 0.5,
    borderColor: "#d6d7da"
  },
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    overflow: "hidden"
  }
});

export default App;
```

---

# Reference

## Methods

### `configureNext()`

```jsx
static configureNext(config, onAnimationDidEnd?, onAnimationDidFail?)
```

Agenda uma animação para acontecer no próximo layout.

#### Parâmetros:

| Nome               | Tipo     | Obrigatório | Descrição                         |
| ------------------ | -------- | -------- | ----------------------------------- |
| config             | object   | sim      | Veja a descrição da configuração abaixo.       |
| onAnimationDidEnd  | function | Não       | Chamado quando a animação terminou. |
| onAnimationDidFail | function | Não       | Chamado quando a animação falhou.   |

O parâmetro `config` é um objeto com as chaves abaixo. [`create`] (layoutanimation.md #create) retorna um objeto válido para `config`, e os objetos [`Presets`] (layoutanimation.md #presets) também podem ser passados como `config`.

- `duração` em milissegundos
- `create`, configuração opcional para animação em novas visualizações
- `update`, configuração opcional para animar exibições que foram atualizadas
- `delete`, configuração opcional para animar visualizações à medida que elas são removidas

A configuração que é passada para `create`, `update` ou `delete` tem as seguintes chaves:

- `type`, o [tipo de animação] (layoutanimation.md #types) para usar
- `propriedade`, a [propriedade de layout] (layoutanimation.md #properties) para animar (opcional, mas recomendado para `create` e `delete`)
- `SpringDamping` (número, opcional e apenas para uso com `type: Type.spring`)
- `initialVelocity` (number, optional)
- `delay` (number, optional)
- `duration` (number, optional)

---

### `create()`

```jsx
static create(duration, type, creationProp)
```

Auxiliar que cria um objeto (com os campos `create`, `update` e `delete`) para passar para [`ConfigureNext`] (layoutanimation.md #configurenext). O parâmetro `type` é um [tipo de animação] (layoutanimation.md #types), e o parâmetro `CreationProp` é uma [propriedade de layout] (layoutanimation.md #properties).

**Exemplo: **

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=LayoutAnimation&supportedPlatforms=android,ios
import React, { useState } from "react";
import {
  View,
  Platform,
  UIManager,
  LayoutAnimation,
  StyleSheet,
  Button
} from "react-native";

if (
  Platform.OS === "android" &&
  UIManager.setLayoutAnimationEnabledExperimental
) {
  UIManager.setLayoutAnimationEnabledExperimental(true);
}

const App = () => {
  const [boxPosition, setBoxPosition] = useState("left");

  const toggleBox = () => {
    LayoutAnimation.configureNext(
      LayoutAnimation.create(
        500,
        LayoutAnimation.Types.spring,
        LayoutAnimation.Properties.scaleXY
      )
    );
    setBoxPosition(boxPosition === "left" ? "right" : "left");
  };

  return (
    <View style={styles.container}>
      <View style={styles.buttonContainer}>
        <Button title="Toggle Layout" onPress={toggleBox} />
      </View>
      <View
        style={[styles.box, boxPosition === "left" ? null : styles.moveRight]}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "flex-start",
    justifyContent: "center"
  },
  box: {
    height: 100,
    width: 100,
    borderRadius: 5,
    margin: 8,
    backgroundColor: "blue"
  },
  moveRight: {
    alignSelf: "flex-end",
    height: 200,
    width: 200
  },
  buttonContainer: {
    alignSelf: "center"
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=LayoutAnimation&supportedPlatforms=android,ios
import React, { Component } from "react";
import {
  View,
  Platform,
  UIManager,
  LayoutAnimation,
  StyleSheet,
  Button
} from "react-native";

if (
  Platform.OS === "android" &&
  UIManager.setLayoutAnimationEnabledExperimental
) {
  UIManager.setLayoutAnimationEnabledExperimental(true);
}

class App extends Component {
  state = {
    boxPosition: "left"
  };

  toggleBox = () => {
    LayoutAnimation.configureNext(
      LayoutAnimation.create(
        500,
        LayoutAnimation.Types.spring,
        LayoutAnimation.Properties.scaleXY
      )
    );
    this.setState({
      boxPosition: this.state.boxPosition === "left" ? "right" : "left"
    });
  };

  render() {
    return (
      <View style={styles.container}>
        <View style={styles.buttonContainer}>
          <Button title="Toggle Layout" onPress={this.toggleBox} />
        </View>
        <View
          style={[
            styles.box,
            this.state.boxPosition === "left" ? null : styles.moveRight
          ]}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "flex-start",
    justifyContent: "center"
  },
  box: {
    height: 100,
    width: 100,
    borderRadius: 5,
    margin: 8,
    backgroundColor: "blue"
  },
  moveRight: {
    alignSelf: "flex-end",
    height: 200,
    width: 200
  },
  buttonContainer: {
    alignSelf: "center"
  }
});

export default App;
```

</TabItem>
</Tabs>

## Properties

### Types

Uma enumeração de tipos de animação a serem usados no método [`create`] (layoutanimation.md #create), ou nas configurações `create`/`update`/`delete` para [`configureNext`] (layoutanimation.md #configurenext). (exemplo de uso: `LayoutAnimation.types.easein`)

| Tipos         |
| ------------- |
| spring        |
| linear        |
| easeInEaseOut |
| easeIn        |
| easeOut       |
| keyboard      |

---

### Propriedades

Uma enumeração de propriedades de layout a serem animadas para serem usadas no método [`create`] (layoutanimation.md #create), ou nas configurações `create`/`update`/`delete` para [`configureNext`] (layoutanimation.md #configurenext). (exemplo de uso: `LayoutAnimation.properties.opacity`)

| Propriedades |
| ---------- |
| opacity    |
| scaleX     |
| scaleY     |
| scaleXY    |

---

### Presets

Um conjunto de configurações de animação predefinidas para passar para [`ConfigureNext`] (layoutanimation.md #configurenext).

| Presets       | Value                                                                                                                                                                 |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| easeInEaseOut | `create(300, 'easeInEaseOut', 'opacity')`                                                                                                                             |
| linear        | `create(500, 'linear', 'opacity')`                                                                                                                                    |
| spring        | `{ duration: 700, create: { type: 'linear', property: 'opacity' }, update: { type: 'spring', springDamping: 0.4 }, delete: { type: 'linear', property: 'opacity' } }` |

---

### `easeInEaseOut`

Calls `configureNext()` with `Presets.easeInEaseOut`.

---

### `linear`

Calls `configureNext()` with `Presets.linear`.

---

### `spring`

Chama `configureNext () `com `Presets.spring`.

**Exemplo: **

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=LayoutAnimation&supportedPlatforms=android,ios
import React, { useState } from "react";
import {
  View,
  Platform,
  UIManager,
  LayoutAnimation,
  StyleSheet,
  Button
} from "react-native";

if (
  Platform.OS === "android" &&
  UIManager.setLayoutAnimationEnabledExperimental
) {
  UIManager.setLayoutAnimationEnabledExperimental(true);
}

const App = () => {
  const [firstBoxPosition, setFirstBoxPosition] = useState("left");
  const [secondBoxPosition, setSecondBoxPosition] = useState("left");
  const [thirdBoxPosition, setThirdBoxPosition] = useState("left");

  const toggleFirstBox = () => {
    LayoutAnimation.configureNext(LayoutAnimation.Presets.easeInEaseOut);
    setFirstBoxPosition(firstBoxPosition === "left" ? "right" : "left");
  };

  const toggleSecondBox = () => {
    LayoutAnimation.configureNext(LayoutAnimation.Presets.linear);
    setSecondBoxPosition(secondBoxPosition === "left" ? "right" : "left");
  };

  const toggleThirdBox = () => {
    LayoutAnimation.configureNext(LayoutAnimation.Presets.spring);
    setThirdBoxPosition(thirdBoxPosition === "left" ? "right" : "left");
  };

  return (
    <View style={styles.container}>
      <View style={styles.buttonContainer}>
        <Button title="EaseInEaseOut" onPress={toggleFirstBox} />
      </View>
      <View
        style={[
          styles.box,
          firstBoxPosition === "left" ? null : styles.moveRight
        ]}
      />
      <View style={styles.buttonContainer}>
        <Button title="Linear" onPress={toggleSecondBox} />
      </View>
      <View
        style={[
          styles.box,
          secondBoxPosition === "left" ? null : styles.moveRight
        ]}
      />
      <View style={styles.buttonContainer}>
        <Button title="Spring" onPress={toggleThirdBox} />
      </View>
      <View
        style={[
          styles.box,
          thirdBoxPosition === "left" ? null : styles.moveRight
        ]}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "flex-start",
    justifyContent: "center"
  },
  box: {
    height: 100,
    width: 100,
    borderRadius: 5,
    margin: 8,
    backgroundColor: "blue"
  },
  moveRight: {
    alignSelf: "flex-end"
  },
  buttonContainer: {
    alignSelf: "center"
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=LayoutAnimation&supportedPlatforms=android,ios
import React, { Component } from "react";
import {
  View,
  Platform,
  UIManager,
  LayoutAnimation,
  StyleSheet,
  Button
} from "react-native";

if (
  Platform.OS === "android" &&
  UIManager.setLayoutAnimationEnabledExperimental
) {
  UIManager.setLayoutAnimationEnabledExperimental(true);
}

class App extends Component {
  state = {
    firstBoxPosition: "left",
    secondBoxPosition: "left",
    thirdBoxPosition: "left"
  };

  toggleFirstBox = () => {
    LayoutAnimation.configureNext(LayoutAnimation.Presets.easeInEaseOut);
    this.setState({
      firstBoxPosition:
        this.state.firstBoxPosition === "left" ? "right" : "left"
    });
  };

  toggleSecondBox = () => {
    LayoutAnimation.configureNext(LayoutAnimation.Presets.linear);
    this.setState({
      secondBoxPosition:
        this.state.secondBoxPosition === "left" ? "right" : "left"
    });
  };

  toggleThirdBox = () => {
    LayoutAnimation.configureNext(LayoutAnimation.Presets.spring);
    this.setState({
      thirdBoxPosition:
        this.state.thirdBoxPosition === "left" ? "right" : "left"
    });
  };

  render() {
    return (
      <View style={styles.container}>
        <View style={styles.buttonContainer}>
          <Button title="EaseInEaseOut" onPress={this.toggleFirstBox} />
        </View>
        <View
          style={[
            styles.box,
            this.state.firstBoxPosition === "left" ? null : styles.moveRight
          ]}
        />
        <View style={styles.buttonContainer}>
          <Button title="Linear" onPress={this.toggleSecondBox} />
        </View>
        <View
          style={[
            styles.box,
            this.state.secondBoxPosition === "left" ? null : styles.moveRight
          ]}
        />
        <View style={styles.buttonContainer}>
          <Button title="Spring" onPress={this.toggleThirdBox} />
        </View>
        <View
          style={[
            styles.box,
            this.state.thirdBoxPosition === "left" ? null : styles.moveRight
          ]}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "flex-start",
    justifyContent: "center"
  },
  box: {
    height: 100,
    width: 100,
    borderRadius: 5,
    margin: 8,
    backgroundColor: "blue"
  },
  moveRight: {
    alignSelf: "flex-end"
  },
  buttonContainer: {
    alignSelf: "center"
  }
});

export default App;
```

</TabItem>
</Tabs>
