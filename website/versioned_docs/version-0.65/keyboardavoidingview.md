---
id: keyboardavoidingview
title: KeyboardAvoidingView
---

Esse é um componente que resolve um problema já conhecido em que as views precisam sair da frente do teclado virtual. Isso ajusta automaticamente sua altura, posição ou padding baseado na altura do teclado.

## Exemplo

```SnackPlayer name=KeyboardAvoidingView&supportedPlatforms=android,ios
import React from 'react';
import { View, KeyboardAvoidingView, TextInput, StyleSheet, Text, Platform, TouchableWithoutFeedback, Button, Keyboard  } from 'react-native';

const KeyboardAvoidingComponent = () => {
  return (
    <KeyboardAvoidingView
      behavior={Platform.OS === "ios" ? "padding" : "height"}
      style={styles.container}
    >
      <TouchableWithoutFeedback onPress={Keyboard.dismiss}>
        <View style={styles.inner}>
          <Text style={styles.header}>Header</Text>
          <TextInput placeholder="Username" style={styles.textInput} />
          <View style={styles.btnContainer}>
            <Button title="Submit" onPress={() => null} />
          </View>
        </View>
      </TouchableWithoutFeedback>
    </KeyboardAvoidingView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  inner: {
    padding: 24,
    flex: 1,
    justifyContent: "space-around"
  },
  header: {
    fontSize: 36,
    marginBottom: 48
  },
  textInput: {
    height: 40,
    borderColor: "#000000",
    borderBottomWidth: 1,
    marginBottom: 36
  },
  btnContainer: {
    backgroundColor: "white",
    marginTop: 12
  }
});

export default KeyboardAvoidingComponent;
```

---

# Referência

## Props

### [View Props](view.md#props)

Herda [View Props](view.md#props).

---

### `behavior`

Especifica como reagir com a presença do teclado.

> Android e iOS interagem diferentemente com essa propriedade. É recomendado aplicar `behavior` em ambos os sistemas.

| Type                                        |
| ------------------------------------------- |
| enum(`'height'`, `'position'`, `'padding'`) |

---

### `contentContainerStyle`

O estilo do conteúdo do container (View) quando o behavior é `'position'`.

| Type                              |
| --------------------------------- |
| [View Style](view-style-props.md) |

---

### `enabled`

Ativa ou desativa o KeyboardAvoidingView.

| Type    | Default |
| ------- | ------- |
| boolean | `true`  |

---

### `keyboardVerticalOffset`

Essa é a distancia entre o topo da tela do usuário e a view do react native, pode ser diferente de zero dependendo da necessidade.

| Type   | Default |
| ------ | ------- |
| number | `0`     |
