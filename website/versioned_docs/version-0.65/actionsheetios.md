---
id: actionsheetios
title: ActionSheetIOS
---

Exibe o componente nativo do iOS [Folha de ações] (https://developer.apple.com/design/human-interface-guidelines/ios/views/action-sheets/).

## Exemplo

```SnackPlayer name=ActionSheetIOS&supportedPlatforms=ios
import React, { useState } from "react";
import { ActionSheetIOS, Button, StyleSheet, Text, View } from "react-native";

const App = () => {
  const [result, setResult] = useState("🔮");

  const onPress = () =>
    ActionSheetIOS.showActionSheetWithOptions(
      {
        options: ["Cancel", "Generate number", "Reset"],
        destructiveButtonIndex: 2,
        cancelButtonIndex: 0,
        userInterfaceStyle: 'dark'
      },
      buttonIndex => {
        if (buttonIndex === 0) {
          // cancel action
        } else if (buttonIndex === 1) {
          setResult(Math.floor(Math.random() * 100) + 1);
        } else if (buttonIndex === 2) {
          setResult("🔮");
        }
      }
    );

  return (
    <View style={styles.container}>
      <Text style={styles.result}>{result}</Text>
      <Button onPress={onPress} title="Show Action Sheet" />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center"
  },
  result: {
    fontSize: 64,
    textAlign: "center"
  }
});

export default App;
```

# Reference

## Methods

### `showActionSheetWithOptions()`

```jsx
static showActionSheetWithOptions(options, callback)
```

Exibir uma folha de ações do iOS. O objeto `options` deve conter um ou mais dos:

- `options` (array de strings) - uma lista de títulos de botões (obrigatório)
- `cancelButtonIndex` (int) - índice do botão cancelar em `opções`
- `DestructiveButtonIndex` (int ou array de ints) - índices de botões destrutivos em `opções`
- `title` (string) - um título para mostrar acima da folha de ação
- `message` (string) - uma mensagem para mostrar abaixo do título
- `âncora` (número) - o nó ao qual a folha de ação deve ser ancorada (usado para iPad)
- `TintColor` (string) - a [cor] (cores) usada para títulos de botões não destrutivos
- `DisabledButtonIndices` (matriz de números) - uma lista de índices de botões que devem ser desativados
- `UserInterfaceStyle` (string) - o estilo de interface usado para a folha de ação, pode ser definido como `light` ou` dark`, caso contrário, o estilo padrão do sistema será usado

A função 'callback' usa um parâmetro, o índice baseado em zero do item selecionado.

Exemplo mínimo:

```jsx
ActionSheetIOS.showActionSheetWithOptions(
  {
    options: ['Cancel', 'Remove'],
    destructiveButtonIndex: 1,
    cancelButtonIndex: 0
  },
  (buttonIndex) => {
    if (buttonIndex === 1) {
      /* destructive action */
    }
  }
);
```

---

### `showShareActionSheetWithOptions()`

```jsx
static showShareActionSheetWithOptions(options, failureCallback, successCallback)
```

Exiba a planilha de compartilhamento do iOS. O objeto `options` deve conter um ou ambos `message` e `url` e também pode ter um `sujeito` ou` excludedActivityTypes`:

- `url` (string) - um URL para compartilhar
- `message` (string) - uma mensagem para compartilhar
- `subject` (string) - um assunto para a mensagem
- `ExcludedActivityTypes` (array) - as atividades a serem excluídas da ActionSheet

> **Nota: ** Se `url` apontar para um arquivo local, ou for um uri codificado em base64, o arquivo para o qual ele aponta será carregado e compartilhado diretamente. Desta forma, você pode compartilhar imagens, vídeos, arquivos PDF, etc. Se `url` apontar para um arquivo ou endereço remoto, ele deve estar em conformidade com o formato de URL, conforme descrito em [RFC 2396] (https://www.ietf.org/rfc/rfc2396.txt). Por exemplo, um URL da Web sem um protocolo adequado (HTTP/HTTPS) não será compartilhado.

A função 'FailureCallback' usa um parâmetro, um objeto de erro. A única propriedade definida neste objeto é uma propriedade `stack` opcional do tipo `string`.

A função 'SuccessCallback' usa dois parâmetros:

- um valor booleano que significa sucesso ou fracasso
- uma string que, em caso de sucesso, indica o método de compartilhamento
