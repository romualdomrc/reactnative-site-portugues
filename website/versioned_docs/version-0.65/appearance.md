---
id: appearance
title: Appearance
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

```jsx
import { Appearance } from 'react-native';
```

O módulo `Aparência` expõe informações sobre as preferências de aparência do usuário, como seu esquema de cores preferido (claro ou escuro).

#### Notas do desenvolvedor

<Tabs groupId="guide" defaultValue="web" values={constants.getDevNotesTabs(["android", "ios", "web"])}>

<TabItem value="web">

> A API `Appearance` é inspirada no [Rascunho das Consultas de Mídia] (https://drafts.csswg.org/mediaqueries-5/) do W3C. A preferência do esquema de cores é modelada após o recurso de mídia CSS [`prefers-color-scheme`] (https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme).

</TabItem>
<TabItem value="android">

> A preferência do esquema de cores será mapeada para a preferência do usuário Light ou [Dark theme] (https://developer.android.com/guide/topics/ui/look-and-feel/darktheme) em dispositivos Android 10 (API de nível 29) e superior.

</TabItem>
<TabItem value="ios">

> A preferência do esquema de cores será mapeada para a preferência do usuário Light ou [Dark Mode] (https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/dark-mode/) em dispositivos iOS 13 e superior.

</TabItem>
</Tabs>

## Exemplo

Você pode usar o módulo `Aparência` para determinar se o usuário prefere um esquema de cores escuras:

```jsx
const colorScheme = Appearance.getColorScheme();
if (colorScheme === 'dark') {
  // Use dark color scheme
}
```

Embora o esquema de cores esteja disponível imediatamente, isso pode mudar (por exemplo, mudança programada do esquema de cores ao nascer ou ao pôr do sol). Qualquer lógica de renderização ou estilos que dependam do esquema de cores preferido pelo usuário deve tentar chamar essa função em cada renderização, em vez de armazenar em cache o valor. Por exemplo, você pode usar o gancho React [`UseColorScheme`] (usecolorscheme), pois ele fornece e assina atualizações de esquema de cores, ou você pode usar estilos embutidos em vez de definir um valor em uma `StyleSheet`.

---

# Referência

## Métodos

### `getColorScheme()`

```jsx
static getColorScheme()
```

Indica o esquema de cores preferido do usuário atual. O valor pode ser atualizado posteriormente, seja por meio de ação direta do usuário (por exemplo, seleção de temas nas configurações do dispositivo) ou em uma programação (por exemplo, temas claros e escuros que seguem o ciclo dia/noite).

Esquemas de cores suportados:

- `light`: O usuário prefere um tema de cores claras.
- `dark`: O usuário prefere um tema de cores escuras.
- null: O usuário não indicou um tema de cores preferido.

Veja também: gancho `UseColorScheme`.

> Nota: `getColorScheme () `sempre retornará `light` ao depurar com o Chrome.

---

### `addChangeListener()`

```jsx
static addChangeListener(listener)
```

Adicione um manipulador de eventos que é acionado quando as preferências de aparência mudam.

---

### `removeChangeListener()`

```jsx
static removeChangeListener(listener)
```

> **Descontinuado.** Use o método `remove () `na assinatura de evento retornada por [`addChangeListener ()`] (#addchangelistener).
