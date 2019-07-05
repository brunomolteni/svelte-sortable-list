# 🔃 SortableList

This component renders a list of items which can be reordered by draggin and dropping and implements FLIP animation for adding/removing/reordering items in the list.

To make the component work you need two thing at least: setting the `list` prop and responding to `on:reorder` event.

### Basic Example ( [Open in REPL](https://svelte.dev/repl/413e33b7f34049f08e443a31d51f5367?version=3.6.4) )

```jsx
<script>
import SortableList from 'svelte-sortable-list';

let list = ["First Item", "Second Item", "Third Item"];
const sortList = ev => {list = ev.detail};
</script>

<SortableList 
    {list} 
    on:sort={sortList}
/>
```

## ⤵️ Props and Slot

| name   | type      | required | default                           |
| ------ | --------- | -------- | --------------------------------- |
| `list` | Array     | ✔️       | ✖️                                |
| `key`  | String    | ❌       | ✖️                                |
| `slot` | Component | ❌       | `<p>{key ? item[key] : item}</p>` |

The way this works is that you are required to pass a `list` prop to the component, which could be an array with anything inside, but if the array contains objects or arrays you must pass the `key` prop to specify what property is going to be used as key (needs to be unique to each object in the array).

You can customize what element is used as the list item passing any element as the child. If you do this you can access the item data by setting `let:item` on `<SortableList>` and `{item}` on your element ( you can also access the index in `let:index`).

## ⤴️ Events

The component handles all the internal functionality but since you are passing the list as a prop, it can't actually change the data you pass to it, so you need to respond to an event that gets triggered any time you sort items.
This is done using the `on:sort` event handler, which gets passed an `event` object that contains the list inside the `details` property ( this is the default way of handling event data in svelte).


### Complete Example ( [Open in REPL](https://svelte.dev/repl/0b4fd50a87a94efd81b533229b43d941?version=3.6.4) )

```jsx
<script>
import SortableList from 'svelte-sortable-list';
import Component from './Component.svelte';

let list = [
	{id: 1, name: 'First Item'},
	{id: 2, name: 'Second Item'},
	{id: 3, name: 'Third Item'}
];
const sortList = ev => {list = ev.detail};
</script>

<SortableList 
    {list} 
    key="id" 
    on:sort={sortList}
    let:item 
>
    <Component {item} />
</SortableList>
```