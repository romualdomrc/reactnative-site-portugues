---
id: devsettings
title: DevSettings
---

O módulo `DevSettings` expõe métodos para personalizar configurações para desenvolvedores em desenvolvimento.

---

# Referência

## Métodos

### `addMenuItem()`

```jsx
static addMenuItem(title, handler)
```

Adicione um item de menu personalizado ao menu do desenvolvedor.

**Parâmetros: **

| Nome                                                         | Tipo     |
| ------------------------------------------------------------ | -------- |
| title <div className="label basic required">Required</div>   | string   |
| handler <div className="label basic required">Required</div> | function |

**Exemplo: **

```jsx
DevSettings.addMenuItem('Show Secret Dev Screen', () => {
  Alert.alert('Showing secret dev screen!');
});
```

---

### `reload()`

```jsx
static reload()
```

Recarregue o aplicativo. Pode ser invocado diretamente ou na interação do usuário.

**Exemplo: **

```jsx
<Button title="Reload" onPress={() => DevSettings.reload()} />
```
