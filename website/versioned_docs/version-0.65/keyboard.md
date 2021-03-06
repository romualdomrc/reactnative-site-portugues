---
id: keyboard
title: Keyboard
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Módulo `Keyboard` para controlar eventos do teclado.

### Uso

O módulo Teclado permite que você ouça eventos nativos e reaja a eles, além de fazer alterações no teclado, como dispensá-lo.

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Keyboard%20Function%20Component%20Example&supportedPlatforms=ios,android
import React, { useState, useEffect } from "react";
import { Keyboard, Text, TextInput, StyleSheet, View } from "react-native";

const Example = () => {
  const [keyboardStatus, setKeyboardStatus] = useState(undefined);

  useEffect(() => {
    const showSubscription = Keyboard.addListener("keyboardDidShow", () => {
      setKeyboardStatus("Keyboard Shown");
    });
    const hideSubscription = Keyboard.addListener("keyboardDidHide", () => {
      setKeyboardStatus("Keyboard Hidden");
    });

    return () => {
      showSubscription.remove();
      hideSubscription.remove();
    };
  }, []);

  return (
    <View style={style.container}>
      <TextInput
        style={style.input}
        placeholder='Click here…'
        onSubmitEditing={Keyboard.dismiss}
      />
      <Text style={style.status}>{keyboardStatus}</Text>
    </View>
  );
}

const style = StyleSheet.create({
  container: {
    flex: 1,
    padding: 36
  },
  input: {
    padding: 10,
    borderWidth: 0.5,
    borderRadius: 4
  },
  status: {
    padding: 10,
    textAlign: "center"
  }
});

export default Example;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Keyboard%20Class%20Component%20Example&supportedPlatforms=ios,android
import React, { Component } from 'react';
import { Keyboard, Text, TextInput, StyleSheet, View } from 'react-native';

class Example extends Component {
  state = {
    keyboardStatus: undefined
  };

  componentDidMount() {
    this.keyboardDidShowSubscription = Keyboard.addListener(
      'keyboardDidShow',
      () => {
        this.setState({ keyboardStatus: 'Keyboard Shown' });
      },
    );
    this.keyboardDidHideSubscription = Keyboard.addListener(
      'keyboardDidHide',
      () => {
        this.setState({ keyboardStatus: 'Keyboard Hidden' });
      },
    );
  }

  componentWillUnmount() {
    this.keyboardDidShowSubscription.remove();
    this.keyboardDidHideSubscription.remove();
  }

  render() {
    return (
      <View style={style.container}>
        <TextInput
          style={style.input}
          placeholder='Click here…'
          onSubmitEditing={Keyboard.dismiss}
        />
        <Text style={style.status}>
          {this.state.keyboardStatus}
        </Text>
      </View>
    )
  }
}

const style = StyleSheet.create({
  container: {
    flex: 1,
    padding: 36
  },
  input: {
    padding: 10,
    borderWidth: 0.5,
    borderRadius: 4
  },
  status: {
    padding: 10,
    textAlign: "center"
  }
});

export default Example;
```

</TabItem>
</Tabs>

---

# Referência

## Métodos

### `addListener()`

```jsx
static addListener(eventName, callback)
```

The `addListener` function connects a JavaScript function to an identified native keyboard notification event.

This function then returns the reference to the listener.

**Parâmetros: **

| Nome                                                                     | Tipo     | Descrição                                                                    |
| ------------------------------------------------------------------------ | -------- | ------------------------------------------------------------------------------ |
| eventName <div className="label basic two-lines required">Required</div> | string   | A string que identifica o evento que você está ouvindo. Veja a lista abaixo. |
| callback <div className="label basic two-lines required">Required</div>  | function | A função a ser chamada quando o evento for acionado                                 |

**`eventName`**

Isso pode ser qualquer um dos seguintes:

- `keyboardWillShow`
- `keyboardDidShow`
- `keyboardWillHide`
- `keyboardDidHide`
- `keyboardWillChangeFrame`
- `keyboardDidChangeFrame`

> Observe que se você definir `Android:WindowSoftInputMode` para `AdjustSize` ou `AdjustPan`, apenas os eventos `KeyboardDidShow` e `KeyboardDidHide` estarão disponíveis no Android. Se você definir `Android:WindowSoftInputMode` como `AdjustNothing`, nenhum evento estará disponível no Android. `KeyboardWillShow` assim como `KeyboardWillHide` geralmente não estão disponíveis no Android, pois não há nenhum evento nativo correspondente.

---

### `removeListener()`

```jsx
static removeListener(eventName, callback)
```

> **Descontinuado.** Use o método `remove () `na assinatura de evento retornada por [`addListener ()`] (#addlistener).

**Parâmetros: **

| Nome      | Tipo     | Obrigatório | Descrição                                                                    |
| --------- | -------- | -------- | ------------------------------------------------------------------------------ |
| eventName | string   | sim      | O `NativeEvent` é a string que identifica o evento que você está ouvindo |
| callback  | function | sim      | A função a ser chamada quando o evento for acionado                                 |

---

### `removeAllListeners()`

```jsx
static removeAllListeners(eventName)
```

Remove todos os ouvintes de um tipo de evento específico.

**Parâmetros: **

| Nome      | Tipo   | Obrigatório | Descrição                                                          |
| --------- | ------ | -------- | -------------------------------------------------------------------- |
| eventType | string | sim      | Os ouvintes de string de eventos nativos estão observando, o que será removido. |

---

### `dismiss()`

```jsx
static dismiss()
```

Descarta o teclado ativo e remove o foco.

---

### `scheduleLayoutAnimation`

```jsx
static scheduleLayoutAnimation(event)
```

Útil para sincronizar o TextInput (ou outro acessório de teclado), o tamanho das mudanças de posição com os movimentos do teclado.
