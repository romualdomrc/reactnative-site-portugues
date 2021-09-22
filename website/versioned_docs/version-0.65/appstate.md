---
id: appstate
title: AppState
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

`AppState` pode dizer se o aplicativo está em primeiro plano ou em segundo plano e notificá-lo quando o estado mudar.

O AppState é frequentemente usado para determinar a intenção e o comportamento adequado ao lidar com notificações push.

### App States

- `ativo` - O aplicativo está sendo executado em primeiro plano
- `background` - O aplicativo está sendo executado em segundo plano. O usuário é:
  - em outro aplicativo
  - na tela inicial
  - [Android] em outra `Atividade` (mesmo que tenha sido iniciada pelo seu aplicativo)
- [iOS] `inativo` - Este é um estado que ocorre ao fazer a transição entre o primeiro plano e o segundo plano e durante períodos de inatividade, como entrar na visualização Multitarefa ou no caso de uma chamada recebida

For more information, see [Apple's documentation](https://developer.apple.com/documentation/uikit/app_and_scenes/managing_your_app_s_life_cycle)

## Uso básico

Para ver o estado atual, você pode verificar `AppState.currentState`, que será mantido atualizado. No entanto, `currentState` será nulo no lançamento enquanto `AppState` o recupera pela ponte.

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=AppState%20Function%20Component%20Example
import React, { useRef, useState, useEffect } from "react";
import { AppState, StyleSheet, Text, View } from "react-native";

const AppStateExample = () => {
  const appState = useRef(AppState.currentState);
  const [appStateVisible, setAppStateVisible] = useState(appState.current);

  useEffect(() => {
    const subscription = AppState.addEventListener("change", nextAppState => {
      if (
        appState.current.match(/inactive|background/) &&
        nextAppState === "active"
      ) {
        console.log("App has come to the foreground!");
      }

      appState.current = nextAppState;
      setAppStateVisible(appState.current);
      console.log("AppState", appState.current);
    });

    return () => {
      subscription.remove();
    };
  }, []);

  return (
    <View style={styles.container}>
      <Text>Current state is: {appStateVisible}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});

export default AppStateExample;
```

Se você não quiser ver a atualização do AppState de `ativo` para `inativo` no iOS, você pode remover a variável de estado e usar o valor `AppState.current`.

 </TabItem> 
 <TabItem value="classical"> 

```SnackPlayer Name=AppState%20Class%20Component%20EXample
importar React, {Component} de “react”;
import {appState, StyleSheet, Text, View} de “react-native”;

classe AppStateExample estende o componente {
 estado = {
 AppState: appState.currentState
 };

 componentDidMount () {
 this.appStateSubscription = AppState.addEventListener (
 “mudança”,
 NextAppState => {
 se (
 this.state.appstate.match (/inativo|background/) &&
 NextAppState === “ativo”
 ) {
 console.log (“O aplicativo chegou ao primeiro plano!”) ;
 }
 this.setState ({appState: nextAppState});
 }
 );
 }

 Componente desmontará () {
 this.appstatesubscription.remove ();
 }

 render () {
 retorno (
 <View style={styles.container}> 
 <Text> O estado atual é: {this.state.AppState} </Text> 
 </View> 
 );
 }
}

const styles = StyleSheet.create ({
 recipiente: {
 flex: 1,
 Justificar conteúdo: “centro”,
 AlignItens: “centro”
 }
});

exportar AppStateExample padrão;
```

</TabItem>
</Tabs>

Este exemplo só parecerá dizer “O estado atual é: ativo” porque o aplicativo só é visível para o usuário quando está no estado `ativo`, e o estado nulo acontecerá apenas momentaneamente. Se você quiser experimentar o código, recomendamos usar seu próprio dispositivo em vez da visualização incorporada.

---

# Referência

## Eventos

### `change`

Esse evento é recebido quando o estado do aplicativo é alterado. O ouvinte é chamado com um dos [valores atuais do estado do aplicativo] (appstate #app -states).

### `memoryWarning`

Este evento é usado na necessidade de lançar um aviso de memória ou liberá-lo.

### `focus` <div class="label android">Android</div>

Recebido quando o aplicativo ganha foco (o usuário está interagindo com o aplicativo).

### `blur` <div class="label android">Android</div>

Recebido quando o usuário não está interagindo ativamente com o aplicativo. Útil em situações em que o usuário puxa para baixo a [gaveta de notificações] (https://developer.android.com/guide/topics/ui/notifiers/notifications#bar-and-drawer). `AppState` não mudará, mas o evento `blur` será disparado.

## Métodos

### `addEventListener()`

```jsx
addEventListener(type, handler);
```

Adicione um manipulador às alterações do AppState ouvindo o tipo de evento `change` e fornecendo o manipulador

---

### `removeEventListener()`

```jsx
removeEventListener(type, handler);
```

> **Descontinuado.** Use o método `remove () `na assinatura de evento retornada por [`addEventListener ()`](#addeventlistener).

## Properties

### `currentState`

```jsx
AppState.currentState;
```
