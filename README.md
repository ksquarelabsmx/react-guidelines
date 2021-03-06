# KSquare React Guidelines

> NOTE: This guide takes for granted that you are using typescript + react

If you wan't to contribute to the guideline follow the [contribution guide](https://github.com/ksquarelabsmx/react-guidelines/blob/master/CONTRIBUTING.md)

## Objects

1. Favor object shorthand syntax

```js
// bad
const name = "Juan Perez";
const user = {
  name: name
};

// good
const name = "Juan Perez";
const user = {
  name
};
```

2. Prefer object destructuring access to functions prop and properties in objects

For props with "one nested level":

```js
const user = {
  name: "John Doe",
  age: 50
};

// Good
const useUserInfo = user => {
  const { name, age } = user;
  //...
};

// Better
const useUserInfo = ({ name, age }) => {
  //...
};

useUserInfo(user);
```

For props with "many nested levels"

```js
const user = {
  name: {
    first: "John",
    last: "Doe"
  },
  age: 50
};

// Good
const useUserInfo = user => {
  const {
    name: { first, last },
    age
  } = user;
  //...
};

// This is the best for small objects
const useUserInfo = ({ name: { first, last }, age }) => {
  //...
};

// This is the best for any size I think
const useUserInfo = ({ name, age }) => {
  const { first, last } = name;
  //...
};

useUserInfo(user);
```

Working with arrays

```js
const carsList = [
  {
    brand: "ferrari",
    type: "sportscar",
    engine: {
      horsepower: 600,
      liters: 4,
      fuel: "gas"
    },
    wheels: 4
  },
  {
    brand: "porshe",
    type: "sportscar",
    engine: {
      horsepower: 455,
      liters: 6,
      fuel: "gas"
    },
    wheels: 4
  }
];

const [ferrari, porsche] = carsList;
```

## Functions

1. Favor `arrow functions` expressions over function declarations or named expressions

```js
// good
const isEven = (n: number): number => n % 2 === 0;

// bad
function isEven(n: number): number {
  return n % 2 === 0;
}

const isEven = function(n: number): number {
  return n % 2 === 0;
};
```

## React

1. Favor `FunctionalComponents` (`React.FC`) over `classes` (`React.Component`)

```js
// good
const Card: React.FC = () => {
  // ...
};

// bad
class Card extends React.Component {
  // ...
}
```

2. Interfaces should have the prefix `I`

```js
// good
interface IUser {
  // ...
}

// bad
interface User {
  // ...
}
```

3. Prop-related interfaces should have the following structure `I[Component]Props`

```js
// good
interface ICardProps {
  // ...
}

// bad
interface AnythingElse {
  // ...
}
```

4. State-related interfaces should have the following structure `I[Component]State`

```js
// good
interface ICardState {
  // ...
}

// bad
interface AnythingElse {
  // ...
}
```

## Modules

1. Favor `named exports` over `export default`

```js
// good
export const Card: React.FC = () => {
  // ..
};

// bad
const Card: React.FC = () => {
  // ..
};

export default Card;
```

2. Always export your interfaces

```js
// good
export interface ICardProps {
  // ...
}

// bad
interface ICardProps {
  // ...
}
```

3. Every Module should have its own directory and and `index.ts` file

```js
// Card/index.ts
export { Card, ICardProps } from "./Card";
```

4. Every Component should have its own file

```js
// Card/Card.ts
export const Card: React.FC = () => {
  // ...
};
```
