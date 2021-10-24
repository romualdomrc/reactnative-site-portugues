---
id: backhandler
title: BackHandler
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

A API Backhandler detecta pressionamentos de botão de hardware para navegação reversa, permite registrar ouvintes de eventos para a ação de retorno do sistema e permite controlar como o aplicativo responde. É apenas para Android.

As assinaturas de eventos são chamadas na ordem inversa (ou seja, a última assinatura registrada é chamada primeiro).

- **Se uma assinatura retornar verdadeira, ** as assinaturas registradas anteriormente não serão chamadas.
- **Se nenhuma assinatura retornar verdadeira ou nenhuma estiver registrada, ** ela invoca programaticamente a funcionalidade padrão do botão Voltar para sair do aplicativo.

> **Aviso para usuários modais: ** Se seu aplicativo mostrar um `Modal` aberto, `BackHandler` não publicará nenhum evento ([veja `Modal` docs] (modal #onrequestclose)).

## Padrão

```jsx
BackHandler.addEventListener('hardwareBackPress', function () {
  /**
   * this.onMainScreen and this.goBack are just examples,
   * you need to use your own implementation here.
   *
   * Typically you would use the navigator here to go to the last state.
   */

  if (!this.onMainScreen()) {
    this.goBack();
    /**
     * When true is returned the event will not be bubbled up
     * & no other back action will execute
     */
    return true;
  }
  /**
   * Returning false will let the event to bubble up & let other event listeners
   * or the system's default back action to be executed.
   */
  return false;
});
```

## Exemplo

O exemplo a seguir implementa um cenário em que você confirma se o usuário deseja sair do aplicativo:

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=BackHandler&supportedPlatforms=android
import React, { useEffect } from "react";
import { Text, View, StyleSheet, BackHandler, Alert } from "react-native";

const App = () => {
  useEffect(() => {
    const backAction = () => {
      Alert.alert("Hold on!", "Are you sure you want to go back?", [
        {
          text: "Cancel",
          onPress: () => null,
          style: "cancel"
        },
        { text: "YES", onPress: () => BackHandler.exitApp() }
      ]);
      return true;
    };

    const backHandler = BackHandler.addEventListener(
      "hardwareBackPress",
      backAction
    );

    return () => backHandler.remove();
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Click Back button!</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  text: {
    fontSize: 18,
    fontWeight: "bold"
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=BackHandler&supportedPlatforms=android
import React, { Component } from "react";
import { Text, View, StyleSheet, BackHandler, Alert } from "react-native";

class App extends Component {
  backAction = () => {
    Alert.alert("Hold on!", "Are you sure you want to go back?", [
      {
        text: "Cancel",
        onPress: () => null,
        style: "cancel"
      },
      { text: "YES", onPress: () => BackHandler.exitApp() }
    ]);
    return true;
  };

  componentDidMount() {
    this.backHandler = BackHandler.addEventListener(
      "hardwareBackPress",
      this.backAction
    );
  }

  componentWillUnmount() {
    this.backHandler.remove();
  }

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>Click Back button!</Text>
      </View>
    );
  }
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  text: {
    fontSize: 18,
    fontWeight: "bold"
  }
});

export default App;
```

</TabItem>
</Tabs>

`BackHandler.addEventListener` cria um ouvinte de eventos e retorna um objeto `NativeEventSubscription` que deve ser limpo usando o método `NativeEventSubscription.remove`.

Além disso, `BackHandler.removeEventListener` também pode ser usado para limpar o ouvinte de eventos. Certifique-se de que o retorno de chamada tenha a referência à mesma função usada na chamada `AddEventListener`, conforme mostrado no exemplo a seguir

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=BackHandler&supportedPlatforms=android
import React, { useEffect } from "react";
import { Text, View, StyleSheet, BackHandler, Alert } from "react-native";

const App = () => {
  const backAction = () => {
    Alert.alert("Hold on!", "Are you sure you want to go back?", [
      {
        text: "Cancel",
        onPress: () => null,
        style: "cancel"
      },
      { text: "YES", onPress: () => BackHandler.exitApp() }
    ]);
    return true;
  };

  useEffect(() => {
    BackHandler.addEventListener("hardwareBackPress", backAction);

    return () =>
      BackHandler.removeEventListener("hardwareBackPress", backAction);
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Click Back button!</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  text: {
    fontSize: 18,
    fontWeight: "bold"
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=BackHandler&supportedPlatforms=android
import React, { Component } from "react";
import { Text, View, StyleSheet, BackHandler, Alert } from "react-native";

class App extends Component {
  backAction = () => {
    Alert.alert("Hold on!", "Are you sure you want to go back?", [
      {
        text: "Cancel",
        onPress: () => null,
        style: "cancel"
      },
      { text: "YES", onPress: () => BackHandler.exitApp() }
    ]);
    return true;
  };

  componentDidMount() {
    BackHandler.addEventListener("hardwareBackPress", this.backAction);
  }

  componentWillUnmount() {
    BackHandler.removeEventListener("hardwareBackPress", this.backAction);
  }

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>Click Back button!</Text>
      </View>
    );
  }
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  text: {
    fontSize: 18,
    fontWeight: "bold"
  }
});

export default App;
```

</TabItem>
</Tabs>

## Uso com o React Navigation

Se você estiver usando o React Navigation para navegar por telas diferentes, siga o guia deles em [Comportamento personalizado do botão Voltar do Android] (https://reactnavigation.org/docs/custom-android-back-button-handling/)

## Backhandler hook

[React Native Hooks](https://github.com/react-native-community/hooks#usebackhandler) has a nice `useBackHandler` hook which will simplify the process of setting up event listeners.

---

# Referência

## Métodos

### `addEventListener()`

```jsx
static addEventListener(eventName, handler)
```

---

### `exitApp()`

```jsx
static exitApp()
```

---

### `removeEventListener()`

```jsx
static removeEventListener(eventName, handler)
```
