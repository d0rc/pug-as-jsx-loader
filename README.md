# pug-as-jsx loader for webpack

## Installation

```
npm install pug-as-jsx-loader --save-dev
```

## Usage

[Documentation: Using loaders](http://webpack.github.io/docs/using-loaders.html)

``` javascript
var jsx = require("pug-as-jsx-loader!./file.pug");
// => returns file.pug content as jsx
```

- import pug template
```
import React from 'react';

import template from './file.pug';      // ← import pug template
import ItemDetail from './ItemDetail';

class Report extends React.Component {
  render() {
    const {
      items,
      period,
    } = this.props;

    return template.call(this, {        // ← use transpiled function
      // variables
      items,
      period,
      // components
      ItemDetail,
    });
  }
};
```

- pug template (./file.pug)
```
div
  h1 {period.start} ~ {period.end}
  ul
    li(@repeat='items as item')
      i.ico(@if='item.icon', className='{"ico-" + item.icon}')
      ItemDetail(item='{item}')
```

- transpiled function
```
import React from 'react';

export default function (params = {}) {
  const { items, period, ItemDetail } = params;
  return (
    <div>
      <h1>
        {period.start} ~ {period.end}
      </h1>
      <ul>
        {items.map((item, i) =>
          <li key={i}>
            {(item.icon) && (
            <i className={`ico ico-${item.icon}`} />
            )}
            <ItemDetail item={item} />
          </li>
        )}
      </ul>
    </div>
  );
};
```

## License

MIT (http://www.opensource.org/licenses/mit-license.php)
