---
id: systrace
title: Systrace
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

`Systrace` é uma ferramenta padrão de criação de perfil baseada em marcadores do Android (e é instalada quando você instala o pacote de ferramentas da plataforma Android). Os blocos de código perfilados são cercados por marcadores de início/fim que são visualizados em um formato de gráfico colorido. Tanto o SDK do Android quanto o framework React Native fornecem marcadores padrão que você pode visualizar.

## Exemplo

`Systrace` permite que você marque eventos JavaScript (JS) com uma tag e um valor inteiro. Capture os eventos JS não cronometrados no EasyProfiler.

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Systrace%20Function%20Component%20Example
import React from "react";
import { Button, Text, View, SafeAreaView, StyleSheet, Systrace } from "react-native";

const App = () =>  {

  const enableProfiling = () => {
    Systrace.setEnabled(true); // Call setEnabled to turn on the profiling.
    Systrace.beginEvent('event_label')
    Systrace.counterEvent('event_label', 10);
  }

  const stopProfiling = () => {
    Systrace.endEvent()
  }

  return (
    <SafeAreaView style={styles.container}>
      <Text style={[styles.header, styles.paragraph]}>React Native Systrace API</Text>
    <View style={styles.buttonRow}>
      <Button title="Capture the non-Timed JS events in EasyProfiler" onPress={()=> enableProfiling()}/>
      <Button title="Stop capturing" onPress={()=> stopProfiling()} color="#FF0000"/>
    </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
    paddingTop: 44,
    padding: 8
  },
   header: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  },
  paragraph: {
    margin: 24,
    fontSize: 25,
    textAlign: "center"
  },
  buttonRow: {
    flexBasis: 150,
    marginVertical: 16,
    justifyContent: 'space-evenly'
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Systrace%20Class%20Component%20Example
import React, { Component } from "react";
import { Button, Text, View, SafeAreaView, StyleSheet, Systrace } from "react-native";

class App extends Component {

  enableProfiling = () => {
    Systrace.setEnabled(true); // Call setEnabled to turn on the profiling.
    Systrace.beginEvent('event_label')
    Systrace.counterEvent('event_label', 10);
  }

  stopProfiling = () => {
    Systrace.endEvent()
  }

  render() {
    return (
      <SafeAreaView style={styles.container}>
        <Text style={[styles.header, styles.paragraph]}>React Native Systrace API</Text>
      <View style={styles.buttonRow}>
        <Button title="Capture the non-Timed JS events in EasyProfiler" onPress={()=> this.enableProfiling()}/>
        <Button title="Stop capturing" onPress={()=> this.stopProfiling()} color="#FF0000"/>
      </View>
      </SafeAreaView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
    paddingTop: 44,
    padding: 8
  },
   header: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  },
  paragraph: {
    margin: 24,
    fontSize: 25,
    textAlign: "center"
  },
  buttonRow: {
    flexBasis: 150,
    marginVertical: 16,
    justifyContent: 'space-evenly'
  }
});

export default App;
```

</TabItem>
</Tabs>

---

# Referência

## Métodos

### `installReactHook()`

```jsx
static installReactHook(useFiber)
```

---

### `setEnabled()`

```jsx
static setEnabled(enabled)
```

---

### `isEnabled()`

```jsx
static isEnabled()
```

---

### `beginEvent()`

```jsx
static beginEvent(profileName?, args?)
```

BeginEvent/endEvent para iniciar e depois terminar um perfil dentro do mesmo quadro de pilha de chamadas.

---

### `endEvent()`

```jsx
static endEvent()
```

---

### `beginAsyncEvent()`

```jsx
static beginAsyncEvent(profileName?)
```

BeginAsyncEvent/endAsyncEvent para iniciar e terminar um perfil onde o fim pode ocorrer em outro thread ou fora do quadro de pilha atual, por exemplo, aguardar a variável de cookie retornada deve ser usada como entrada na chamada endAsyncEvent para encerrar o perfil.

---

### `endAsyncEvent()`

```jsx
static endAsyncEvent(profileName?, cookie?)
```

---

### `counterEvent()`

```jsx
static counterEvent(profileName?, value?)
```

Registre o valor no ProfileName na linha do tempo do systrace.
