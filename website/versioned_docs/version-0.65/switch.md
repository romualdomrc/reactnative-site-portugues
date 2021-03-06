---
id: switch
title: Switch
---

Renderiza uma entrada booleana.

Este é um componente controlado que requer um onValueChangeretorno de chamada que atualiza o value prop para que o componente reflita as ações do usuário. Se o valueprop não for atualizado, o componente continuará a renderizar o value prop fornecido em vez do resultado esperado de quaisquer ações do usuário.

## Example

```SnackPlayer name=Switch&supportedPlatforms=android,ios
import React, { useState } from "react";
import { View, Switch, StyleSheet } from "react-native";

const App = () => {
  const [isEnabled, setIsEnabled] = useState(false);
  const toggleSwitch = () => setIsEnabled(previousState => !previousState);

  return (
    <View style={styles.container}>
      <Switch
        trackColor={{ false: "#767577", true: "#81b0ff" }}
        thumbColor={isEnabled ? "#f5dd4b" : "#f4f3f4"}
        ios_backgroundColor="#3e3e3e"
        onValueChange={toggleSwitch}
        value={isEnabled}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  }
});

export default App;
```

---

# Reference

## Props

### [View Props](view.md#props)

Inherits [View Props](view.md#props).

---

### `disabled`

Se verdadeiro, o usuário não será capaz de alternar a chave.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `ios_backgroundColor` <div class="label ios">iOS</div>

No iOS, cor personalizada para o plano de fundo. Essa cor de fundo pode ser vista quando o valor da chave é falseou quando a chave está desabilitada (e a chave é translúcida).

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `onChange`

Chamado quando o usuário tenta alterar o valor da chave. Recebe o evento de mudança como um argumento. Se você deseja receber apenas o novo valor, use onValueChange.

| Type     |
| -------- |
| function |

---

### `onValueChange`

Chamado quando o usuário tenta alterar o valor da chave. Recebe o novo valor como argumento. Se, em vez disso, quiser receber um evento, use onChange.

| Type     |
| -------- |
| function |

---

### `thumbColor`

Cor do punho do interruptor de primeiro plano. Se estiver definido no iOS, o controle do interruptor perderá sua sombra projetada.

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `trackColor`

Cores personalizadas para a trilha do switch.

_iOS_: quando o valor de troca é`false`, a trilha encolhe até a borda. Se você quiser alterar a cor do fundo exposto pela trilha reduzida, use [`ios_backgroundColor`](switch.md#ios_backgroundColor).

| Type                                                            |
| --------------------------------------------------------------- |
| object: { false: [color](colors.md), true: [color](colors.md) } |

---

### `value`

O valor do switch. Se verdadeiro, a chave será ligada. O valor padrão é falso.

| Type |
| ---- |
| bool |
