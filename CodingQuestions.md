### Q. We have 2 dropdowns, One has the country and the other has cities. if we select the country, only  the country cities  should  be displayed.
```js
import "./styles.css";
import { useState } from "react";
export default function App() {
  const [country, setCountry] = useState(0);
  const countries = [
    { name: "India", value: "IN", cities: ["Delhi", "Mumbai"] },
    { name: "Pak", value: "PK", cities: ["Lahore", "Karachi"] },
    { name: "Bangladesh", value: "BG", cities: ["Dhaka", "Chittagong"] },
  ];

  function handleDropdown(e) {
    setCountry(e.target.value);
  }

  return (
    <div className="App">
      <select value={country} onChange={handleDropdown}>
        {countries.map((item, index) => (
          <option value={index}>{item.name}</option>
        ))}
      </select>

      <select>
        {countries[country].cities.map((item, index)=> {
          return <option>{item}</option>;
        })}
      </select>
    </div>
  );
}
```

- ### Q. Create an Array which has few elements, It has both checkbox and the delete button. But Default, the delete button should be disabled. As soon as click on checkbox, the delete button should be enabled.
```js
import "./styles.css";
import { useState } from "react";
export default function App() {
  const countries = ["India", "pakistan", "china"];

  const [data, setData] = useState(countries);
  const [checkInput, setCheckInput] = useState(Array(data.length).fill(false));

  //
  function handleDelete(indexEl) {
    const filteredArray = data.filter((el, i) => i !== indexEl);
    setData(filteredArray);
    setCheckInput(checkInput.filter((el, i) => i !== indexEl));
  }

  function handleInput(index) {
    const newCheckInput = [...checkInput];
    newCheckInput[index] = !newCheckInput[index];
    setCheckInput(newCheckInput);
  }

  return (
    <div>
      <ul>
        {data.map((item, index) => {
          return (
            <li key={item}>
              <input
                type="checkbox"
                checked={checkInput[index]}
                onChange={() => handleInput(index)}
              />
              <label>{item}</label>
              <button
                onClick={() => handleDelete(index)}
                disabled={!checkInput[index]}
              >
                Delete
              </button>
            </li>
          );
        })}
      </ul>
    </div>
  );
}
```
- ### Q. 
