---
id: dimensions
title: Dimensions
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

> [`UseWindowDimensions`] (usewindowdimensions) é a API preferida para componentes React. Ao contrário de `Dimensões`, ele é atualizado à medida que as dimensões da janela são atualizadas. Isso funciona bem com o paradigma React.

```jsx
import { Dimensions } from 'react-native';
```

Você pode obter a largura e a altura da janela do aplicativo usando o seguinte código:

```jsx
const windowWidth = Dimensions.get('window').width;
const windowHeight = Dimensions.get('window').height;
```

> Embora as dimensões estejam disponíveis imediatamente, elas podem mudar (por exemplo, devido à rotação do dispositivo, dispositivos dobráveis, etc.), portanto, qualquer lógica de renderização ou estilos que dependam dessas constantes deve tentar chamar essa função em cada renderização, em vez de armazenar em cache o valor (por exemplo, usando estilos embutidos em vez de definir um valor em uma `StyleSheet`).

Se você estiver direcionando dispositivos dobráveis ou dispositivos que podem alterar o tamanho da tela ou o tamanho da janela do aplicativo, você pode usar o ouvinte de eventos disponível no módulo Dimensões, conforme mostrado no exemplo abaixo.

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Dimensions
import React, { useState, useEffect } from "react";
import { View, StyleSheet, Text, Dimensions } from "react-native";

const window = Dimensions.get("window");
const screen = Dimensions.get("screen");

const App = () => {
  const [dimensions, setDimensions] = useState({ window, screen });

  useEffect(() => {
    const subscription = Dimensions.addEventListener(
      "change",
      ({ window, screen }) => {
        setDimensions({ window, screen });
      }
    );
    return () => subscription?.remove();
  });

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Window Dimensions</Text>
      {Object.entries(dimensions.window).map(([key, value]) => (
        <Text>{key} - {value}</Text>
      ))}
      <Text style={styles.header}>Screen Dimensions</Text>
      {Object.entries(dimensions.screen).map(([key, value]) => (
        <Text>{key} - {value}</Text>
      ))}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  },
  header: {
    fontSize: 16,
    marginVertical: 10
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Dimensions
import React, { Component } from "react";
import { View, StyleSheet, Text, Dimensions } from "react-native";

const window = Dimensions.get("window");
const screen = Dimensions.get("screen");

class App extends Component {
  state = {
    dimensions: {
      window,
      screen
    }
  };

  onChange = ({ window, screen }) => {
    this.setState({ dimensions: { window, screen } });
  };

  componentDidMount() {
    this.dimensionsSubscription = Dimensions.addEventListener("change", this.onChange);
  }

  componentWillUnmount() {
    this.dimensionsSubscription?.remove();
  }

  render() {
    const { dimensions: { window, screen } } = this.state;

    return (
      <View style={styles.container}>
        <Text style={styles.header}>Window Dimensions</Text>
        {Object.entries(window).map(([key, value]) => (
          <Text>{key} - {value}</Text>
        ))}
        <Text style={styles.header}>Screen Dimensions</Text>
        {Object.entries(screen).map(([key, value]) => (
          <Text>{key} - {value}</Text>
        ))}
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  },
  header: {
    fontSize: 16,
    marginVertical: 10
  }
});

export default App;
```

</TabItem>
</Tabs>

# Referência

## Métodos

### `addEventListener()`

```jsx
static addEventListener(type, handler)
```

Adicione um manipulador de eventos. Eventos com suporte:

- `change`: É acionado quando uma propriedade dentro do objeto `Dimensões` muda. O argumento para o manipulador de eventos é um objeto do tipo [`DimensionsValue`] (#dimensionsvalue).

---

### `get()`

```jsx
static get(dim)
```

As dimensões iniciais são definidas antes de `RunApplication` ser chamado, portanto, elas devem estar disponíveis antes de qualquer outro requisito ser executado, mas podem ser atualizadas posteriormente.

Exemplo: `const {height, width} = dimensions.get ('janela'); `

**Parâmetros: **

| Nome                                                               | Tipo   | Descrição                                                                       |
| ------------------------------------------------------------------ | ------ | --------------------------------------------------------------------------------- |
| dim <div className="label basic required two-lines">Required</div> | string | Nome da dimensão conforme definido ao chamar `set`. Retorna o valor da dimensão. |

> Para Android, a dimensão `janela` excluirá o tamanho usado pela `barra de status` (se não translúcida) e `barra de navegação inferior`

---

### `removeEventListener()`

```jsx
static removeEventListener(type, handler)
```

> **Descontinuado.** Use o método `remove () `na assinatura de evento retornada por [`addEventListener ()`] (#addeventlistener).

---

### `set()`

```jsx
static set(dims)
```

Isso só deve ser chamado a partir do código nativo enviando o evento `DidUpdateDimensions`.

**Parâmetros: **

| Nome                                                      | Tipo   | Descrição                               |
| --------------------------------------------------------- | ------ | ----------------------------------------- |
| dims <div className="label basic required">Required</div> | object | Objeto de dimensões com chave de string a ser definido. |

---

## Definições de tipo

### DimensionsValue

**Propriedades: **

| Nome   | Tipo                                        | Descrição                             |
| ------ | ------------------------------------------- | --------------------------------------- |
| window | [DisplayMetrics](dimensions#displaymetrics) | Tamanho da janela do aplicativo visível. |
| screen | [DisplayMetrics](dimensions#displaymetrics) | Tamanho da tela do dispositivo.            |

### DisplayMetrics

| Tipo   |
| ------ |
| object |

**Propriedades: **

| Nome      | Tipo   |
| --------- | ------ |
| width     | number |
| height    | number |
| scale     | number |
| fontScale | number |
