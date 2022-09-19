# React types

Немного о типизации в React:

### Events
```ts
interface Props {
    onChange: (event: React.ChangeEvent<HTMLInputElement>)
     => void;
    onClick?(event: React.MouseEvent<HTMLDivElement>): void;

}
```

### component

 [Как типизировать компоненты?](Component.md)

В пропсах:
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

