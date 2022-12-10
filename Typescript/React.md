# React types

Немного о типизации в React. 

### Events
```ts
interface Props {
    onChange: (event: React.ChangeEvent<HTMLInputElement>)
     => void;
    onClick?(event: React.MouseEvent<HTMLDivElement>): void;

}
```

### Component

 [Как типизировать компоненты?](Component.md)

### Component as props
```ts
    interface Props {
        children: ReactNode
    }
```

### useState
```ts
  const [isOpen, setIsOpen] = useState<boolean>(false)
  const [filter, setFilter] = useState<string | null>(null)
  const [user, setUser] = useState<User>(props.user)
  const [items, setItems] = useState<Item[]>([])

```

### refs
```ts
    // useRef
    const headerRef = useRef<HTMLDivElement | null>(null);

    // in props
    interface Props { 
        inputRef: RefObject<HTMLInputElement>;
    };
```

