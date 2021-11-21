[useMemo helps to cache our data in memory](https://www.youtube.com/watch?v=THL1OPn72vo)

```
import { useMemo, useState } from 'react';
import cx from 'classnames';

import './App.css';

const App = () => {
  const [num, setNum] = useState(0);
  const [isDarkMode, setDarkMode] = useState(false);

  const slowFunc = () => {
    for(let i=0; i<1000000000; i++) {}
    return 2*num;
  }

  const doubleNum = useMemo(() => {
    return slowFunc()
  }, [num]);


  return (
    <div>
        <input type="number" 
          value={num}
          onChange={(e) => setNum(e.target.value)}
        />

        <div className={
          cx({
            themeBox: true,
            dark: isDarkMode
          })
        }>
          {doubleNum}
        </div>
          <button onClick={() => setDarkMode(!isDarkMode)}>Change Theme</button>
    </div>
  );
}

export default App;
```

as we can see when user changes value in input it take more time to show the `doubleNum` as it is taking more time in `slowFunc`, but it is taking more time in changing the theme because in every render App function calls hence `slowFunc` will also be called

To avoid this slow rendering thing we can useMemo