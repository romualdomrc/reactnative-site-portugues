---
id: settings
title: Settings
---

`Settings` serve como um wrapper para [`NSUserDefaults`] (https://developer.apple.com/documentation/foundation/nsuserdefaults), um armazenamento persistente de chave-valor disponível apenas no iOS.

## Exemplo

```SnackPlayer name=Settings%20Example&supportedPlatforms=ios
import React, { useState } from "react";
import { Button, Settings, StyleSheet, Text, View } from "react-native";

const App = () => {
  const [data, setData] = useState(Settings.get("data"));

  const storeData = data => {
    Settings.set(data);
    setData(Settings.get("data"));
  };

  return (
    <View style={styles.container}>
      <Text>Stored value:</Text>
      <Text style={styles.value}>{data}</Text>
      <Button
        onPress={() => storeData({ data: "React" })}
        title="Store 'React'"
      />
      <Button
        onPress={() => storeData({ data: "Native" })}
        title="Store 'Native'"
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  },
  value: {
    fontSize: 24,
    marginVertical: 12
  }
});

export default App;
```

---

# Reference

## Methods

### `clearWatch()`

```jsx
static clearWatch(watchId: number)
```

`watchID` é o número retornado por `watchKeys () `quando a assinatura foi configurada originalmente.

---

### `get()`

```jsx
static get(key: string): mixed
```

Obtenha o valor atual para uma determinada `chave` em `NSUserDefaults`.

---

### `set()`

```jsx
static set(settings: object)
```

Defina um ou mais valores em `NSUserDefaults`.

---

### `watchKeys()`

```jsx
static watchKeys(keys: string | array<string>, callback: function): number
```

Inscreva-se para ser notificado quando o valor de qualquer uma das chaves especificadas pelo parâmetro `keys` tiver sido alterado em `NSUserDefaults`. Retorna um número `watchId` que pode ser usado com `ClearWatch () `para cancelar a assinatura.

> **Nota: ** `watchKeys () `por design ignora chamadas internas `set ()` e dispara callback somente em alterações pré-formadas fora do código React Native.
