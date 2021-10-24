---
id: inputaccessoryview
title: InputAccessoryView
---

Um componente que permite a personalização da visualização do acessório de entrada do teclado no iOS. A visualização do acessório de entrada é exibida acima do teclado sempre que um `TextInput` tem foco. Esse componente pode ser usado para criar barras de ferramentas personalizadas.

Para usar esse componente, envolva sua barra de ferramentas personalizada com o componente InputAccessoryView e defina um `NativeId`. Em seguida, passe esse `NativeId` como o `InputAccessoryViewID` de qualquer `TextInput` que você desejar. Um exemplo básico:

```SnackPlayer name=InputAccessoryView&supportedPlatforms=ios
import React, { useState } from 'react';
import { Button, InputAccessoryView, ScrollView, TextInput } from 'react-native';

export default App = () => {
  const inputAccessoryViewID = 'uniqueID';
  const initialText = '';
  const [text, setText] = useState(initialText);

  return (
    <>
      <ScrollView keyboardDismissMode="interactive">
        <TextInput
          style={{
            padding: 16,
            marginTop: 50,
          }}
          inputAccessoryViewID={inputAccessoryViewID}
          onChangeText={setText}
          value={text}
          placeholder={'Please type here…'}
        />
      </ScrollView>
      <InputAccessoryView nativeID={inputAccessoryViewID}>
        <Button
          onPress={() => setText(initialText)}
          title="Clear text"
        />
      </InputAccessoryView>
    </>
  );
}
```

Este componente também pode ser usado para criar entradas de texto fixo (entradas de texto ancoradas na parte superior do teclado). Para fazer isso, envolva um `TextInput` com o componente `InputAccessoryView` e não defina um `nativeId`. Para um exemplo, veja [InputAccessoryViewExample.js] (https://github.com/facebook/react-native/blob/master/packages/rn-tester/js/examples/InputAccessoryView/InputAccessoryViewExample.js).

---

# Referência

## Props

### `backgroundColor`

| Tipo               |
| ------------------ |
| [color](colors.md) |

---

### `nativeID`

Um ID que é usado para associar este `InputAccessoryView` a TextInput (s) especificado (s).

| Tipo   |
| ------ |
| string |

---

### `style`

| Tipo                              |
| --------------------------------- |
| [View Style](view-style-props.md) |

# Problemas conhecidos

- [react-native #18997] (https://github.com/facebook/react-native/issues/18997): Não suporta várias linhas `TextInput`
- [react-native #20157] (https://github.com/facebook/react-native/issues/20157): Não é possível usar com uma barra de guias inferior
