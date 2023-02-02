# React-Typescript-tutorials

## What is this page about

My main goal is to summarize the coding techniques we used to learn in React with Typescript, and provide simple example to each one. This is not about theory. I hope that this cheat sheet will help students not to drown at the start in interfaces, models, classes, react hooks itc... This specific material are based on React course in John Bryce, 2023.  

## Installations

> React install, project install (ts template), run.
```
1. NodeJs install.
2. npm i -g create-react-app  => React global install on PC.
3. create-react-app my-project-name --template typescript  => Create React project.
4. npm start  => run React project.
5. npm i  =>  auto-download all packages in "dependencies" (while you run project on new workspace).
```
> Tools.
```
1. npm i -g react-cli-snippets  => tool to create react components, by Assaf Finkelshtein.
```

## Interpolation

> Wrapping the variables inline.
```
const percent = 10;
<span>Only today - {percent}% off on all store shoes!</span>
```

## Conditional rendering

> Show the content on condition. There is 3 main techniques: 

1. Interpolation with ternary operator: 
```
{ isWeekend() ? <span>Pizza 🍕 </span> : <span>Cake🎂</span> }
```
2. Short cuit - condition, then logic && or ||, then HTML to render:

```
{ isWeekend() && <span>Pizza 🍕 </span> }
```
3. Condition with other 'return' that return HTML.


```
if isWeekend() return <span>Today is weekend</span>;

return (
    <span>Today is regular day</span>
);
```

## Displaying lists

> Popular method to renders lists is map method: 
```
import "./Desserts.css";

function Desserts(): JSX.Element {

    const items = [ // Demo for getting the desserts from backend.
        { id: 1, name: "Apple Pie"},
        { id: 2, name: "Ice Cream"},
        { id: 3, name: "Pavlova"},
        { id: 4, name: "Eclair"}
    ];

    return (
        <div className="Desserts">
		    {items.map(item => <span key={item.id}>{item.name} 🍧 </span>)}
        </div>
    );
}

export default Desserts;
```

## Events

We can trigger functions from page events. Triggered function can be without args, with SyntheticEvent, or with customs args:

```
function Recommendations(): JSX.Element {

    // No arguments:
    function first(): void {
        console.log('click on btn');
    }

    // SyntheticEvent argument (or derivation):
    function second(args: SyntheticEvent): void {
        console.log(args);
    }

    // Getting my own arguments:
    function third(item: string, price: number): void {
        console.log(item, price);
    }

    return (
        <div className="Recommendations Box">

			<button onClick={first}>First</button>

			<button onClick={second}>Second</button>

			<button onClick={() => third("Apple Pie", 12)}>Third</button>

        </div>
    );
}
```
## Media

> Create Assets/Images folder, place the file there. Import it and use it as an "src" in img tag:

```
import imageSource from "../../../Assets/Images/dish.jpg";

function Dish(): JSX.Element {
    return (
        <div className="Dish">
            <img src={imageSource} />
        </div>
    );
}
```
## Props

> Props can be passed from parent to child element. Child should configure expected props type with 'interface':
```
interface SaleProps {
    discount: number;
    category: string;
}

function Sale(props: SaleProps): JSX.Element {
    return (
        <div className="Sale Box">
			<span>{props.discount}% discount on all {props.category}</span>
        </div>
    );
}
```
> And the parent pass props to child:
```
<Sale discount={10} category="Candies" />
```

## State and side effect
- **Hooks** - react system functions - we can't change their names. 

- **Lifecycle Hooks** - those special functions will work only in class component.

- **React Hooks** - those special functions will work only in functional component. 

### useState

State is an special variable. React monitors them, and if their values change, react will re-render the component.
> When we call to useState react hook - we also have to specify the type of data we want to manage, and the initial value to the state. The function returns array with 2 items:
1. The first item is actually a state variable.
2. The second item is an state setter, with that setter we set new values to state (this func is also an trigger to render page)

```
    const sellerNameArr = useState<string>("");
    const sellerName = sellerNameArr[0]; // First item in the array is the state variable we need.
    const setSellerName = sellerNameArr[1]; // Second item in the array is a function for changing the variable.
```
3. There is also short syntax to assign the state and setter func to variables - using Array Destructuring Assignment:
```
const [num, setNum] = useState<number>(0);
```
4. We also can use our custom created type:
```
const [product, setProduct] = useState<ProductModel>();
```

### useEffect