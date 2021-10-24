---
id: safeareaview
title: SafeAreaView
---

O objetivo do `SafeAreaView` é renderizar conteúdo dentro dos limites da área segura de um dispositivo. Atualmente, ele é aplicável apenas a dispositivos iOS com iOS versão 11 ou posterior.

`SafeAreaView` renderiza conteúdo aninhado e aplica automaticamente o preenchimento para refletir a parte da exibição que não é coberta por barras de navegação, barras de guias, barras de ferramentas e outras visualizações ancestrais. Além disso, e o mais importante, os acolchoamentos da Área Segura refletem a limitação física da tela, como cantos arredondados ou entalhes da câmera (ou seja, a área da caixa do sensor no iPhone X).

## Exemplo

Para usar, envolva sua visualização de nível superior com um `SafeAreaView` com um estilo `flex: 1` aplicado a ela. Você também pode usar uma cor de fundo que corresponda ao design do aplicativo.

```SnackPlayer name=SafeAreaView&supportedPlatforms=ios
import React from 'react';
import { StyleSheet, Text, SafeAreaView } from 'react-native';

const App = () => {
  return (
    <SafeAreaView style={styles.container}>
      <Text>Page content</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
});

export default App;
```

---

# Referência

## adereços

### [View Props](view.md#props)

Herda [Exibir adereços] (view.md #props).

> Como o preenchimento é usado para implementar o comportamento do componente, as regras de preenchimento em estilos aplicados a um `SafeAreaView` serão ignoradas e podem causar resultados diferentes dependendo da plataforma. Consulte [#22211] (https://github.com/facebook/react-native/issues/22211) para obter detalhes.

---

### `emulateUnlessSupported`

| Tipo | Obrigatório | Default |
| ---- | -------- | ------- |
| bool | No       | true    |
