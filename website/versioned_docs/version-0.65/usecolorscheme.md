---
id: usecolorscheme
title: useColorScheme
---

```jsx
import { useColorScheme } from 'react-native';
```

O gancho React `UseColorScheme` fornece e assina atualizações de esquema de cores do módulo [`Appearance`] (aparência). O valor de retorno indica o esquema de cores preferido pelo usuário atual. O valor pode ser atualizado posteriormente, seja por meio de ação direta do usuário (por exemplo, seleção de temas nas configurações do dispositivo) ou em uma programação (por exemplo, temas claros e escuros que seguem o ciclo dia/noite).

### Esquemas de cores compatíveis

- `"light"`: O usuário prefere um tema de cores claras.
- `"dark"`: O usuário prefere um tema de cores escuras.
- `null`: O usuário não indicou um tema de cores preferido.

> **Nota: ** Atualmente devido a restrições técnicas, quando o depurador do Chrome estiver ativado, esse gancho _sempre_ retornará `"light"`.

---

## Exemplo

```SnackPlayer
import React from 'react';
import { Text, StyleSheet, useColorScheme, View } from 'react-native';

const App = () => {
  const colorScheme = useColorScheme();
  return (
    <View style={styles.container}>
      <Text>useColorScheme(): {colorScheme}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
});

export default App;
```

Você pode encontrar um exemplo completo que demonstra o uso desse gancho junto com um contexto React para adicionar suporte para temas claros e escuros ao seu aplicativo em [`AppearanceExample.js`] (https://github.com/facebook/react-native/blob/master/packages/rn-tester/js/examples/Appearance/AppearanceExample.js).
