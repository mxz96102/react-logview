
## LogView

### Basic Usage

You can use log view easily by import LogView component

```tsx
import React from 'react';
import { LogView } from 'react-logview';

const generateRandomLogs = (sum) => {
  let i = sum;
  let str = ''
  while (sum--) {
    str += `${Math.random() > 0.5 ? '[WARN]' : '[ERROR]'}: ${Math.random().toString(16).slice(-5).repeat(10)}\n`
  }
  return str
}

export default () => <LogView content={generateRandomLogs(100)} height={120} />;
```

### Massive Mount of Logs

Event with million lines of logs, still not block browser

```tsx
import React, {useState} from 'react';
import { LogView } from 'react-logview';

const generateRandomLogs = (sum) => {
  let i = sum;
  let str = ''
  while (sum--) {
    str += `${Math.random() > 0.5 ? '[WARN]' : '[ERROR]'}: ${Math.random().toString(16).slice(-5).repeat(10)}\n`
  }
  return str
}

export default () => { 
  const [content, setContent] = useState('Press Load to load');
  
  return <><button onClick={() => setContent(generateRandomLogs(1200000))}>Load</button><LogView revert language="prolog" content={content} height={200}  /></>};
```

### Themes

We support light(github style) and dark(darcula style) by using theme;

```tsx
import React from 'react';
import { LogView } from 'react-logview';

const generateRandomLogs = (sum) => {
  let i = sum;
  let str = ''
  while (sum--) {
    str += `${Math.random() > 0.5 ? '[WARN]' : '[ERROR]'}: ${Math.random().toString(16).slice(-5).repeat(10)}\n`
  }
  return str
}

export default () => <>
  Light Theme
  <LogView content={generateRandomLogs(100)} height={120} />
  Dark Theme
  <LogView content={generateRandomLogs(100)} height={120} theme="dark" />
</>;
```

### Keyword Search

By using keyword props, you can find the lines contains your words.


```tsx
import React, { useState } from 'react';
import { LogView } from 'react-logview';

const generateRandomLogs = (sum) => {
  let i = sum;
  let str = ''
  while (sum--) {
    str += `${Math.random() > 0.5 ? '[WARN]' : '[ERROR]'}: ${Math.random().toString(16).slice(-5).repeat(10)}\n`
  }
  return str
}

export default () => {
  const [keyword, setKeyword] = useState('ERROR')
  console.log(keyword)

  return <>
  <input value={keyword} onChange={({target: {value}}) => setKeyword(value)} />
  <LogView content={generateRandomLogs(100)} height={120} keywords={keyword} />
</>};
```

### Props

| Props          | Type              | Description                                             |
|----------------|-------------------|---------------------------------------------------------|
| content        | string            | (required) content of logs                              |
| width          | number            | width                                                   |
| height         | number            | height                                                  |
| fontSize       | number            | font size of log                                        |
| theme          | "light" \| "dark" | theme now only support light and dark                   |
| language       | string            | language of logs default set to prolog                  |
| focusLine      | number            | on change of focus line, view will scroll to lineNumber |
| keywords       | string            | filter the line that contains keywords                  |
| style          | Style             | styles of view                                          |
| listRef        | MutableRef        | ref of container dom                                    |
| onScrollBottom | () => void        | call back on scroll to bottom                           |
| revert         | boolean           | revert logs rank                                        |



