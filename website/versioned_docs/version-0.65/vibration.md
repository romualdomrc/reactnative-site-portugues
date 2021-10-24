---
id: vibration
title: Vibration
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Vibra o dispositivo.

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Vibration&supportedPlatforms=ios,android
import React from "react";
import { Button, Platform, Text, Vibration, View, SafeAreaView, StyleSheet } from "react-native";

const Separator = () => {
  return <View style={Platform.OS === "android" ? styles.separator : null} />;
}

const App = () => {

  const ONE_SECOND_IN_MS = 1000;

  const PATTERN = [
    1 * ONE_SECOND_IN_MS,
    2 * ONE_SECOND_IN_MS,
    3 * ONE_SECOND_IN_MS
  ];

  const PATTERN_DESC =
    Platform.OS === "android"
      ? "wait 1s, vibrate 2s, wait 3s"
      : "wait 1s, vibrate, wait 2s, vibrate, wait 3s";

  return (
    <SafeAreaView style={styles.container}>
      <Text style={[styles.header, styles.paragraph]}>Vibration API</Text>
      <View>
        <Button title="Vibrate once" onPress={() => Vibration.vibrate()} />
      </View>
      <Separator />
      {Platform.OS == "android"
        ? [
            <View>
              <Button
                title="Vibrate for 10 seconds"
                onPress={() => Vibration.vibrate(10 * ONE_SECOND_IN_MS)}
              />
            </View>,
            <Separator />
          ]
        : null}
      <Text style={styles.paragraph}>Pattern: {PATTERN_DESC}</Text>
      <Button
        title="Vibrate with pattern"
        onPress={() => Vibration.vibrate(PATTERN)}
      />
      <Separator />
      <Button
        title="Vibrate with pattern until cancelled"
        onPress={() => Vibration.vibrate(PATTERN, true)}
      />
      <Separator />
      <Button
        title="Stop vibration pattern"
        onPress={() => Vibration.cancel()}
        color="#FF0000"
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
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
    textAlign: "center"
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Vibration&supportedPlatforms=ios,android
import React, { Component } from "react";
import { Button, Platform, Text, Vibration, View, SafeAreaView, StyleSheet } from "react-native";

const Separator = () => {
  return <View style={Platform.OS === "android" ? styles.separator : null} />;
}

class App extends Component {
  render() {
    const ONE_SECOND_IN_MS = 1000;

    const PATTERN = [
      1 * ONE_SECOND_IN_MS,
      2 * ONE_SECOND_IN_MS,
      3 * ONE_SECOND_IN_MS
    ];

    const PATTERN_DESC =
      Platform.OS === "android"
        ? "wait 1s, vibrate 2s, wait 3s"
        : "wait 1s, vibrate, wait 2s, vibrate, wait 3s";

    return (
      <SafeAreaView style={styles.container}>
        <Text style={[styles.header, styles.paragraph]}>Vibration API</Text>
        <View>
          <Button title="Vibrate once" onPress={() => Vibration.vibrate()} />
        </View>
        <Separator />
        {Platform.OS == "android"
          ? [
              <View>
                <Button
                  title="Vibrate for 10 seconds"
                  onPress={() => Vibration.vibrate(10 * ONE_SECOND_IN_MS)}
                />
              </View>,
              <Separator />
            ]
          : null}
        <Text style={styles.paragraph}>Pattern: {PATTERN_DESC}</Text>
        <Button
          title="Vibrate with pattern"
          onPress={() => Vibration.vibrate(PATTERN)}
        />
        <Separator />
        <Button
          title="Vibrate with pattern until cancelled"
          onPress={() => Vibration.vibrate(PATTERN, true)}
        />
        <Separator />
        <Button
          title="Stop vibration pattern"
          onPress={() => Vibration.cancel()}
          color="#FF0000"
        />
      </SafeAreaView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
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
    textAlign: "center"
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth
  }
});

export default App;
```

</TabItem>
</Tabs>

> Os aplicativos Android devem solicitar a permissão `android.permission.vibrate` adicionando `<uses-permission android:name="android.permission.VIBRATE"/>` a `AndroidManifest.xml`.

> A API Vibration é implementada como uma chamada `AudioServicesPlaySystemSound (KSystemSoundid_Vibrate) `no iOS.

---

# Referência

## Métodos

### `cancel()`

```jsx
Vibration.cancel();
```

Chame isso para parar de vibrar depois de ter invocado `vibrate () `com a repetição ativada.

---

### `vibrate()`

```jsx
Vibration.vibrate(pattern, repeat);
```

Aciona uma vibração com duração fixa.

**No Android, ** a duração da vibração é padrão de 400 milissegundos, e uma duração de vibração arbitrária pode ser especificada passando um número como o valor para o argumento `padrão`. **No iOS, ** a duração da vibração é fixada em cerca de 400 milissegundos.

O método `vibrate () `pode receber um argumento `padrão` com uma matriz de números que representam o tempo em milissegundos. Você pode definir `repeit` como true para percorrer o padrão de vibração em um loop até que `cancel () `seja chamado.

**No Android, ** os índices ímpares da matriz `padrão` representam a duração da vibração, enquanto os pares representam o tempo de separação. **No iOS, ** os números na matriz `padrão` representam o tempo de separação, pois a duração da vibração é fixa.

**Parâmetros: **

| Nome    | Tipo                                                                     | Padrão | Descrição                                                                                       |
| ------- | ------------------------------------------------------------------------ | ------- | ------------------------------------------------------------------------------------------------- |
| pattern | number <div className="label android">Android</div><hr/>array of numbers | `400`   | Duração da vibração em milissegundos. <hr/> Padrão de vibração como uma matriz de números em milissegundos. |
| repeat  | boolean                                                                  | `false` | Repita o padrão de vibração até `cancel () `.                                                        |
