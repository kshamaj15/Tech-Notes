useRef returns a mutable ref object whose .current property is initialized to the passed argument (initialValue). The returned object will persist for the full lifetime of the component.

```
import { useEffect, useRef, useState } from 'react';

const App = () => {
  const [inputVal, setInputVal] = useState('');
  const countRef = useRef(0);
  const inputRef = useRef();

  const focus = () => {
    inputRef.current.focus();
  }

  useEffect(() => {
    countRef.current++;
  })

  return (
    <div>
      <input 
        ref={inputRef}
        type="text" 
        value={inputVal} 
        onChange={(e) => setInputVal(e.target.value)}
      />
      <p>Input is rendered {countRef.current} times</p>
      <button onClick={focus}>focus</button>
    </div>
  );
}

export default App;
```

`countRef` is persisting value of count even after every render, its not reseting
`inputRef.current` is the reference for input element