---
id: share
title: Share
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Function%20Component%20Example&supportedPlatforms=ios,android
import React from 'react';
import { Share, View, Button } from 'react-native';

const ShareExample = () => {
  const onShare = async () => {
    try {
      const result = await Share.share({
        message:
          'React Native | A framework for building native apps using React',
      });
      if (result.action === Share.sharedAction) {
        if (result.activityType) {
          // shared with activity type of result.activityType
        } else {
          // shared
        }
      } else if (result.action === Share.dismissedAction) {
        // dismissed
      }
    } catch (error) {
      alert(error.message);
    }
  };
  return (
    <View style={{ marginTop: 50 }}>
      <Button onPress={onShare} title="Share" />
    </View>
  );
};

export default ShareExample;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Class%20Component%20Example&supportedPlatforms=ios,android
import React, { Component } from 'react';
import { Share, View, Button } from 'react-native';

class ShareExample extends Component {
  onShare = async () => {
    try {
      const result = await Share.share({
        message:
          'React Native | A framework for building native apps using React',
      });

      if (result.action === Share.sharedAction) {
        if (result.activityType) {
          // shared with activity type of result.activityType
        } else {
          // shared
        }
      } else if (result.action === Share.dismissedAction) {
        // dismissed
      }
    } catch (error) {
      alert(error.message);
    }
  };

  render() {
    return (
      <View style={{ marginTop: 50 }}>
        <Button onPress={this.onShare} title="Share" />
      </View>
    );
  }
}

export default ShareExample;
```

</TabItem>
</Tabs>

# Referência

## Métodos

### `share()`

```jsx
static share(content, options)
```

Abra uma caixa de diálogo para compartilhar conteúdo de texto.

No iOS, retorna uma Promise que será invocada com um objeto contendo `action` e `ActivityType`. Se o usuário ignorar a caixa de diálogo, a Promise ainda será resolvida com a ação `share.dismissedAction` e todas as outras chaves sendo indefinidas. Observe que algumas opções de compartilhamento não aparecerão ou funcionarão no simulador do iOS.

No Android, retorna uma Promise que sempre será resolvida com a ação sendo `sharedAction`.

**Propriedades: **

| Nome                                                         | Tipo   | Descrição                                                                                                                                                                                                                                        |
| ------------------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| content <div className="label basic required">Required</div> | object | `message` - uma mensagem para compartilhar <br/> `url` - um URL para compartilhar <div class="label ios"> iOS </div> <br/> `title` - título da mensagem <div class="label android"> Android </div> <hr/> Pelo menos um dos `url` e `message` é necessário.                        |
| options                                                      | object | `dialogTitle` <div class="label android">Android</div><br/>`excludedActivityTypes` <div class="label ios">iOS</div><br/>`subject` - a subject to share via email <div class="label ios">iOS</div><br/>`tintColor` <div class="label ios">iOS</div> |

---

## Propriedades

### `sharedAction`

```jsx
static sharedAction
```

O conteúdo foi compartilhado com sucesso.

---

### `dismissedAction` <div class="label ios">iOS</div>

```jsx
static dismissedAction
```

A caixa de diálogo foi descartada.
