---
id: alert
title: Alert
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Inicia uma caixa de diálogo de alerta com o título e a mensagem especificados.

Opcionalmente, forneça uma lista de botões. Tocar em qualquer botão acionará o respectivo retorno de chamada onPress e descartará o alerta. Por padrão, o único botão será um botão “OK”.

Essa é uma API que funciona tanto no Android quanto no iOS e pode mostrar alertas estáticos. O alerta que solicita que o usuário insira algumas informações está disponível apenas no iOS.

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Alert%20Function%20Component%20Example&supportedPlatforms=ios,android
import React, { useState } from "react";
import { View, StyleSheet, Button, Alert } from "react-native";

const App = () => {
  const createTwoButtonAlert = () =>
    Alert.alert(
      "Alert Title",
      "My Alert Msg",
      [
        {
          text: "Cancel",
          onPress: () => console.log("Cancel Pressed"),
          style: "cancel"
        },
        { text: "OK", onPress: () => console.log("OK Pressed") }
      ]
    );

  const createThreeButtonAlert = () =>
    Alert.alert(
      "Alert Title",
      "My Alert Msg",
      [
        {
          text: "Ask me later",
          onPress: () => console.log("Ask me later pressed")
        },
        {
          text: "Cancel",
          onPress: () => console.log("Cancel Pressed"),
          style: "cancel"
        },
        { text: "OK", onPress: () => console.log("OK Pressed") }
      ]
    );

  return (
    <View style={styles.container}>
      <Button title={"2-Button Alert"} onPress={createTwoButtonAlert} />
      <Button title={"3-Button Alert"} onPress={createThreeButtonAlert} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "space-around",
    alignItems: "center"
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Alert%20Class%20Component%20Example&supportedPlatforms=ios,android
import React, { Component } from "react";
import { View, StyleSheet, Button, Alert } from "react-native";

class App extends Component {
  createTwoButtonAlert = () =>
    Alert.alert(
      "Alert Title",
      "My Alert Msg",
      [
        {
          text: "Cancel",
          onPress: () => console.log("Cancel Pressed"),
          style: "cancel"
        },
        { text: "OK", onPress: () => console.log("OK Pressed") }
      ]
    );

  createThreeButtonAlert = () =>
    Alert.alert(
      "Alert Title",
      "My Alert Msg",
      [
        {
          text: "Ask me later",
          onPress: () => console.log("Ask me later pressed")
        },
        {
          text: "Cancel",
          onPress: () => console.log("Cancel Pressed"),
          style: "cancel"
        },
        { text: "OK", onPress: () => console.log("OK Pressed") }
      ]
    );

  render() {
    return (
      <View style={styles.container}>
        <Button title={"2-Button Alert"} onPress={this.createTwoButtonAlert} />

        <Button
          title={"3-Button Alert"}
          onPress={this.createThreeButtonAlert}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "space-around",
    alignItems: "center"
  }
});

export default App;
```

</TabItem>
</Tabs>

## iOS

No iOS, você pode especificar qualquer número de botões. Cada botão pode, opcionalmente, especificar um estilo, as opções disponíveis são representadas pelo enum [alertButtonStyle] (#alertbuttonstyle -ios).

## Android

No Android, no máximo três botões podem ser especificados. O Android tem um conceito de botão neutro, negativo e positivo:

- Se você especificar um botão, ele será o 'positivo' (como 'OK')
- Dois botões significam 'negativo', 'positivo' (como 'Cancelar', 'OK')
- Três botões significam 'neutro', 'negativo', 'positivo' (como 'Mais tarde', 'Cancelar', 'OK')

Os alertas no Android podem ser descartados tocando fora da caixa de alerta. Ele é desativado por padrão e pode ser ativado fornecendo um parâmetro opcional [Options] (alert #options -android) com a propriedade cancelável definida como `true`, ou seja, <br/> `{cancelable: true}`.

O evento cancel pode ser tratado fornecendo uma propriedade de retorno de chamada `onDismiss` dentro do parâmetro `options`.

### Exemplo <div class="label android"> Android </div>

```SnackPlayer name=Alert%20Android%20Dissmissable%20Example&supportedPlatforms=android
import React from "react";
import { View, StyleSheet, Button, Alert } from "react-native";

const showAlert = () =>
  Alert.alert(
    "Alert Title",
    "My Alert Msg",
    [
      {
        text: "Cancel",
        onPress: () => Alert.alert("Cancel Pressed"),
        style: "cancel",
      },
    ],
    {
      cancelable: true,
      onDismiss: () =>
        Alert.alert(
          "This alert was dismissed by tapping outside of the alert dialog."
        ),
    }
  );

const App = () => (
  <View style={styles.container}>
    <Button title="Show alert" onPress={showAlert} />
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  }
});

export default App;
```

---

# Reference

## Methods

### `alert()`

```jsx
static alert(title, message?, buttons?, options?)
```

**Parâmetros: **

| Name                                                   | Type                             | Description                                                             |
| ------------------------------------------------------ | -------------------------------- | ----------------------------------------------------------------------- |
| title <div class="label basic required">Required</div> | string                           | O título do diálogo. Passar `null` ou string vazia ocultará o título.   |
| message                                                | string                           | Uma mensagem opcional que aparece abaixo do título da caixa de diálogo. |
| buttons                                                | [Buttons](alert#buttons)         | Um array opcional contendo configuração de botões.                      |
| options <div class="label android">Android</div>       | [Options](alert#options-android) | Uma configuração de alerta opcional para o Android.                     |

---

### `prompt()` <div class="label ios">iOS</div>

```jsx
static prompt(title, message?, callbackOrButtons?, type?, defaultValue?, keyboardType?)
```

Crie e exiba um prompt para inserir algum texto na forma de Alerta.

**Parâmetros: **

| Name                                                   | Type                                  | Description                                                                                                                                                                                                                |
| ------------------------------------------------------ | ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| title <div class="label basic required">Required</div> | string                                | O título do diálogo.                                                                                                                                                                                                       |
| message                                                | string                                | Uma mensagem opcional que aparece acima da entrada de texto.                                                                                                                                                               |
| callbackOrButtons                                      | function<hr/>[Buttons](alert#buttons) | Se for passada uma função, ela será chamada com o valor do prompt <br/> `(text: string) => void`, quando o usuário tocar em 'OK'. <hr/> Se passar uma matriz, os botões serão configurados com base no conteúdo da matriz. |
| type                                                   | [AlertType](alert#alerttype-ios)      | Isso configura a entrada de texto.                                                                                                                                                                                         |
| defaultValue                                           | string                                | O texto padrão na entrada de texto.                                                                                                                                                                                        |
| keyboardType                                           | string                                | O tipo de teclado do primeiro campo de texto (se existir). Um dos TextInput [KeyboardTypes] (textInput #keyboardtype).                                                                                                     |

---

## Type Definitions

### AlertButtonStyle <div class="label ios">iOS</div>

Um estilo de botão Alerta do iOS.

| Type |
| ---- |
| enum |

**Constants:**

| Value           | Description                 |
| --------------- | --------------------------- |
| `'default'`     | Estilo de botão padrão.     |
| `'cancel'`      | Estilo de botão Cancelar.   |
| `'destructive'` | Estilo de botão destrutivo. |

---

### AlertType <div class="label ios">iOS</div>

Um tipo de alerta do iOS.

| Type |
| ---- |
| enum |

**Constants:**

| Value              | Description                        |
| ------------------ | ---------------------------------- |
| `'default'`        | Alerta padrão sem entradas         |
| `'plain-text'`     | Alerta de entrada de texto simples |
| `'secure-text'`    | Alerta de entrada de texto seguro  |
| `'login-password'` | Alerta de login e senha            |

---

### Buttons

Matriz de objetos que contém a configuração dos botões de alerta.

| Type              |
| ----------------- |
| matriz de objetos |

**Propriedades dos objetos: **

| Name                                   | Type                                           | Description                                                  |
| -------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| text                                   | string                                         | Button label.                                                |
| onPress                                | function                                       | Função de retorno de chamada quando o botão é pressionado.   |
| style <div class="label ios">iOS</div> | [AlertButtonStyle](alert#alertbuttonstyle-ios) | Estilo de botão, no Android, essa propriedade será ignorada. |

---

### Options <div class="label android">Android</div>

| Type   |
| ------ |
| object |

**Properties:**

| Name       | Type     | Description                                                             |
| ---------- | -------- | ----------------------------------------------------------------------- |
| cancelable | boolean  | Define se o alerta pode ser descartado tocando fora da caixa de alerta. |
| onDismiss  | function | Função de retorno de chamada acionada quando o alerta foi descartado.   |
