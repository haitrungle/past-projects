---
background: /unsplash-background.jpg
# https://sli.dev/custom/highlighters.html
highlighter: shiki
canvasWidth: 1000
aspectRatio: 16/10
# show line numbers in code blocks
lineNumbers: false
css: unocss
fonts:
  sans: "Inter"
  weights: '200,400,700'
  mono: "Iosevka"
---

# My past projects

Le Trung Hai

City University of Hong Kong

---
layout: center
---

# StayFocused: Mobile Focusing App (WIP)

A controlled experiment exploring how to reduce _compulsive_ smartphone usage

---

# StayFocused: Mobile Focusing App (WIP)

### Features
- A pomodoro-like timer
- __Reflective prompts__ when people touch their phones
- __Chatbot agent__ to increase interactivity

<img src="/Interfaces.png" class="mx-auto w-2/3" />

---

# StayFocused: Mobile Focusing App (WIP)

### Features
- A pomodoro-like timer
- __Reflective prompts__ when people touch their phones
- __Chatbot agent__ to increase interactivity

<img src="/teaser.png" class="mx-auto w-7/10"/>

---

# StayFocused: Mobile Focusing App (WIP)

### Tech stack
- __TypeScript__ with __React Native__ as the mobile framework
- __Zustand__ for state management, custom hook for styling
- __Firebase__ for user authentication and data collection

<div class="grid gap-4" style="grid-template-columns: 48ch 1fr;">
<div>
<small>The Zustand store for user settings and session information</small>
```ts
export const useAppStore = create<AppStore>()(
  persist(
    set => ({
      ...defaultApp,
      saveSettings: settings => set(settings),
      saveSession: session =>
        set(state => ({focusSessions: [...state.focusSessions, session]})),
    }),
    {
      name: 'app-data',
      getStorage: () => AsyncStorage,
    },
  ),
);
```
</div>
<div>
<small>Usage</small>
```ts
export function App() {
  const user = useAppStore(state => state.uid);
}
```
</div>
</div>

---

# StayFocused: Mobile Focusing App (WIP)

### Tech stack
- __TypeScript__ with __React Native__ as the mobile framework
- __Zustand__ for state management, custom hook for styling
- __Firebase__ for user authentication and data collection

<div class="grid gap-4" style="grid-template-columns: 48ch 1fr;">
<div>
<small>Custom hook to manage styling, inspired by the Mantine component library</small>
```ts
export function createStyles<Key extends string = string, Params = void>(
  input:
    | ((theme: Theme, params: Params) => Record<Key, CSSStyles>)
    | Record<Key, CSSStyles>,
) {
  const getCssObject = typeof input === 'function' ? input : () => input;

  function useStyles(params: Params) {
    const theme = useContext(ThemeContext);
    const cssObject = getCssObject(theme, params);
    return StyleSheet.create(cssObject);
  }

  return useStyles;
}
```
</div>
<div>
<small>Usage</small>
```ts
const useStyles = createStyles(theme => ({
  container: {
    flex: 1,
    backgroundColor: theme.backgroundColor,
  },
}));
```
</div>
</div>

---
layout: center
---

# Primox: A Lox Interpreter in Rust (WIP)

Implmenting the Lox language from [Crafting Interpreters](https://craftinginterpreters.com/) in Rust

---

# Primox: A Lox Interpreter in Rust (WIP)

- Numbers and strings
- Print and expression statements
- Arithmetic and logical expressions

<div class="w-[48ch]">
```sh
> print 3 * (1 + 2) - 5 / 4
7.75
> print 5 + 7 > 12
false
> print 34 - 34 != false
true
> print (10 > 5) ? "10 is larger than 5" : "10 is smaller than 5"
10 is larger than 5
```
</div>

---

# Primox: A Lox Interpreter in Rust (WIP)

- Scanning and lexing
- Abstract syntax tree printer
- Recursive descent parser

<div class="w-[48ch]">
```rust {all|1,4|9,11,13}
pub(crate) fn parse(&mut self) -> Result<Vec<Stmt>, ParseError> {
  let mut statements = vec![];
  while !self.is_at_end() {
    statements.push(self.statement()?);
  }
  Ok(statements)
}

fn statement(&mut self) -> Result<Stmt, ParseError> {
  if self.current_is(&[PRINT]) {
    self.print_statement()
  } else {
    self.expression_statement()
  }
}
```
</div>

---
layout: center
---

# HashTable: Implementing Hash Table in C++

Comparative analysis of various hash table implementations in C++

---

# HashTable: Implementing Hash Table in C++

- Two hashing methods (on `unsigned`)
  - Modular (division) hashing
  - Multiplicative hashing
- Three collision resolution stretegies
  - Separate chaining
  - Linear probing
  - Quadratic probing

<div class="w-[48ch]">
```cpp
struct Hasher {
  virtual unsigned hash(unsigned x) = 0;
  virtual void set_size(unsigned size) = 0;

private:
  unsigned table_size;
};

struct HashTable {
  virtual void Insert(unsigned x) = 0;
  virtual void Delete(unsigned x) = 0;
  virtual unsigned* Search(unsigned x) = 0;
};
```
</div>

---

# HashTable: Implementing Hash Table in C++

Comparison of benchmark results

|                                           | `input-0.txt` | `input-1.txt` | `input-2.txt` | `input-3.txt` |
|-------------------------------------------|:-------------:|:-------------:|:-------------:|:-------------:|
| `std::unordered_set`, default hashing     |     2.542     |      2.078    |      2.323    |      2.392    |
| separate chaining, division hashing       |     2.335     |      2.870    |      2.190    |      2.169    |
| separate chaining, multiplicative hashing |     2.345     |      2.134    |      2.268    |      2.156    |
| linear probing, division hashing          |     2.416     |      2.574    |      2.449    |      2.168    |
| linear probing, multiplicative hashing    |     2.313     |      2.220    |      2.259    |      2.071    |
| quadratic probing, division hashing       |     2.358     |      2.591    |      2.216    |      2.133    |
| quadratic probing, multiplicative hashing |     2.291     |      2.244    |      2.297    |      2.102    |
