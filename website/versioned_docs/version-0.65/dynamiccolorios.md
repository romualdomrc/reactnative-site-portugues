---
id: dynamiccolorios
title: DynamicColorIOS
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

A função `DynamicColorios` é um tipo de cor de plataforma específico para iOS.

```jsx
DynamicColorIOS({
  light: color,
  dark: color,
  highContrastLight: color, // (optional) will fallback to "light" if not provided
  highContrastDark: color // (optional) will fallback to "dark" if not provided
});
```

`DynamicColorios` recebe um único argumento como um objeto com duas chaves obrigatórias: `dark` e `light`, e duas teclas opcionais `HighContrastLight` e `HighContrastDark`. Eles correspondem às cores que você deseja usar para “modo claro” e “modo escuro” no iOS, e quando o modo de acessibilidade de alto contraste está ativado, a versão de alto contraste delas.

Em tempo de execução, o sistema escolherá qual das cores exibir, dependendo da aparência atual do sistema e das configurações de acessibilidade. As cores dinâmicas são úteis para cores de marca ou outras cores específicas do aplicativo que ainda respondem automaticamente às alterações nas configurações do sistema.

#### Notas do desenvolvedor

<Tabs groupId="guide" defaultValue="web" values={constants.getDevNotesTabs(["ios", "web"])}>

<TabItem value="web">

> Se você estiver familiarizado com `@media (prefere-color-scheme: dark)` em CSS, isso é semelhante! Somente em vez de definir todas as cores em uma consulta de mídia, você define qual cor usar em que circunstâncias exatamente onde você está usando. arrumado!

</TabItem>
<TabItem value="ios">

> A função `DynamicColorios` é semelhante aos métodos nativos do iOS [`UIColor ColorWithDynamicProvider: `] (https://developer.apple.com/documentation/uikit/uicolor/3238040-colorwithdynamicprovider)

</TabItem>
</Tabs>

## Exemplo

```jsx
import { DynamicColorIOS } from 'react-native';

const customDynamicTextColor = DynamicColorIOS({
  dark: 'lightskyblue',
  light: 'midnightblue'
});

const customContrastDynamicTextColor = DynamicColorIOS({
  dark: 'darkgray',
  light: 'lightgray',
  highContrastDark: 'black',
  highContrastLight: 'white'
});
```
