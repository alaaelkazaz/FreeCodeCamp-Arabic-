


  
Search 8,000+ tutorials

[![freeCodeCamp.org](https://www.freecodecamp.org/news/content/images/2019/11/fcc_primary_large_24X210.svg)](https://www.freecodecamp.org/news)

[Forum](https://forum.freecodecamp.org/)  [Donate](https://www.freecodecamp.org/donate/)

[](https://www.freecodecamp.org/)

Learn to code —  free 3,000-hour curriculum

JUNE 8, 2021/[#REACT](https://www.freecodecamp.org/news/tag/react/)

# How to Pass Data and Events Between Components in React

![Nishant Kumar](https://www.freecodecamp.org/news/content/images/size/w100/2021/08/InShot_20210711_214335593.jpg)

[Nishant Kumar](https://www.freecodecamp.org/news/author/nishant-kumar/)

![How to Pass Data and Events Between Components in React](https://www.freecodecamp.org/news/content/images/size/w2000/2021/05/Colorful-Animal-Crossing-Icons-Icon-Set-2.png)

إذا كنت تحاول تنفيذ عمليات CRUD باستخدام نقاط نهاية API ، فقد تجد أنه من الصعب إدارة البيانات عبر عناصر متعددة
أو ربما لديك نموذج ، لكنك تريد تشغيله من عنصر مختلف.

قد يكون التفاف رأسك حول كيفية معالجة هذه السيناريوهات أمرًا صعبًا.

في هذا الدرس التوضيحي ، سأوضح لك كيف يمكنك القيام بذلك.

## How to Pass Data Between a Parent Component and a Child Component
أولا، دعونا نمرر البيانات بين مكون الأب ومكون للطفل.

أولا، ستحتاج إلى إنشاء مكونين، أب وطفل واحد.
```
import React from 'react'

export default function Parent() {
  return (
    <div>
      
    </div>
  )
}

```

Parent.js

```
import React from 'react'

export default function Child() {
    return (
        <div>
            
        </div>
    )
}

```

Child.js

بعد ذلك، ستقوم بإضافة مكون الطفل في المكون الرئيسي وإعادته.


```
import React from 'react'
import Child from './Child';

export default function Parent() {
  return (
    <div>
      <Child/>
    </div>
  )
}
```
ثم نقوم بمناداة مكون الطفل في المكون الرئيسي

ثم عليك إنشاء function و زر لتشغيل هذه ال function. أيضا، ستقوم بإنشاء state باستخدام hook _usestate_ لإدارة البيانات.

```
import React from 'react'
import Child from './Child';
import { Button } from 'semantic-ui-react';
import { useState } from 'react';
import './App.css';

export default function Parent() {
  const [data, setData] = useState('');
  
  const parentToChild = () => {
    setData("This is data from Parent Component to the Child Component.");
  }
  return (
    <div className="App">
      <Child/>
      
      <div>
        <Button primary onClick={() => parentToChild()}>Click Parent</Button>
      </div>
    </div>
  )
}

```

كما ترون هنا، ندعو وظيفة _parenttochild_ على زر _Click Parent_ انقر فوق الزر. عند النقر فوق زر الأب ، سيقوم بتخزين "هذه البيانات من المكون الرئيسي إلى مكون الطفل" في متغير _Data_.

الآن، دعنا نمرر تلك البيانات إلى مكونات الأطفال لدينا. يمكنك القيام بذلك باستخدام الprops.

تمرير البيانات كprops  عند مناداة مكون الطفل مثل هذا:

```
<Child parentToChild={data}/>
```

Parent.js

هنا، نحن نمرر البيانات في مكون الطفل باسم _Data_

`data" هي البيانات التي يجب أن نمرها، و "parenttochild` هو اسم الخاصية "property".

بعد ذلك، حان الوقت لالتقاط البيانات في مكون الطفل. وهو بسيط جدا.

هنا، يمكن أن يكون هناك حالتين.

الحالة 1: إذا كنت تستخدم مكون وظيفي، فما عليك سوى التقاط parentToChild من المعاملات paramters.

```
import React from 'react'

export default function Child({parentToChild}) {
    return (
        <div>
            {parentToChild}
        </div>
    )
}
```

React Functional Component

الحالة 2: إذا كان لديك مكون صنفي "class component"، فعليك استخدام  `this.props.parentToChild`.

```
import React, { Component } from 'react'

export default class Child extends Component {
    render() {
        return (
            <div>
                {this.props.parentToChild}
            </div>
        )
    }
}
```

React Class Component

في كلتا الحالتين، سوف تحصل على نفس النتائج:
![](https://www.freecodecamp.org/news/content/images/2021/06/Screenshot-2021-06-06-132836.png)

عند النقر فوق الزر  `Click Parent` ، سنرى البيانات كمخرجات على الشاشة.
```
import React from 'react'
import Child from './Child';
import { Button } from 'semantic-ui-react';
import { useState } from 'react';
import './App.css';

export default function Parent() {
  const [data, setData] = useState('');
  
  const parentToChild = () => {
    setData("This is data from Parent Component to the Child Component.");
  }
  return (
    <div className="App">
      <Child parentToChild={data}/>
      
      <div className="child">
        <Button primary onClick={() => parentToChild()}>Click Parent</Button>
      </div>
    </div>
  )
}
```

أعلاه سترى الكود الكامل ل  `Parent Component`.

## How to Pass Data Between a Child Component and a Parent Component
تنفيذ هذا مخادع إلى حد ما.

أولا، تحتاج إلى إنشاء function في المكون الرئيسي يسمى `childtoparent` وحالة فارغة تسمى" data ".
```
const [data, setData] = useState('');

const childToParent = () => {
   
}
```

Parent Component

ثم، قم بتمرير وظيفة `childToParent` "كخاصية لمكون الطفل.
```
<Child childToParent={childToParent}/>
```
تمرير childToParent إلى مكون الطفل.

الآن، في مكون الطفل لدينا، اقبل نداء هذه الوظيفة كخاصية وتعيينها لحدث OnClick.

أيضا، أعلن حالة تحتوي على بعض البيانات في شكل سلسلة أو رقم.

ثم مرر البيانات في وظيفة `perttochild` كخواص.

```
import React from 'react'
import { Button } from 'semantic-ui-react';

export default function Child({childToParent}) {
    const data = "This is data from Child Component to the Parent Component."
    return (
        <div>
            <Button primary onClick={() => childToParent(data)}>Click Child</Button>
        </div>
    )
}
```

Child Component

بعد ذلك، في المكون الرئيسي، اقبل هذه البيانات في وظيفة `childtoparent` كخاصية. ثم قم بتعيين البيانات باستخدام رابط Usestate.
```
import './App.css';
import { useState } from 'react';
import Child from './Child';

function Parent() {
  const [data, setData] = useState('');
  
  const childToParent = (childdata) => {
    setData(childdata);
  }

  return (
    <div className="App">
      <div>
        <Child/>
      </div>
    </div>
  );
}

export default Parent;

```

Parent Component

بعد ذلك، اعرض متغير البيانات في وظيفة العودة.
```
import './App.css';
import { useState } from 'react';
import Child from './Child';

function Parent() {
  const [data, setData] = useState('');
  
  const childToParent = (childdata) => {
    setData(childdata);
  }

  return (
    <div className="App">
     {data}
      <div>
        <Child childToParent={childToParent}/>
      </div>
    </div>
  );
}

export default Parent;
```

Parent Component

سيتم استبدال بيانات الأب ببيانات المكون الطفل عند النقر فوق الزر  `Click Child` .

![](https://www.freecodecamp.org/news/content/images/2021/06/Screenshot-2021-06-06-134803.png)

الآن يمكنك تمرير البيانات من  **Child to Parent**  و  **Parent to Child** كمحترف .

### You can also pass events like onClick or OnChange
ما عليك سوى استدعاء alert method في وظيفة  `childToParent`  وتمرير هذه الوظيفة كخاصية للمكون الطفل _.

```
import './App.css';
import Child from './Child';

function Parent() {
  const childToParent = () => {
    alert("This is an alert from the Child Component")
  }

  return (
    <div className="App">
      <div className="child">
        <Child childToParent={childToParent}/>
      </div>
    </div>
  );
}

export default Parent;
```

Parent Component

وفي الطفل _c_omponent، اقبل "وظيفة`childToParent` كخاصية . ثم قم بتعيينه إلى حدث OnClick على زر.
```
import React from 'react'
import { Button } from 'semantic-ui-react';

export default function Child({childToParent}) {
    return (
        <div>
            <Button primary onClick={() => childToParent()}>Click Child</Button>
        </div>
    )
}
```

Child Component

سيتم استدعاء وظيفتك في المكون الرئيسي عند النقر فوق الزر في مكون الطفل وسترى هذا التنبيه:

![](https://www.freecodecamp.org/news/content/images/2021/06/Screenshot-2021-06-06-140405.png)

هذا كل ما في الأمر!

يمكنك [  إيجاد الكود علي github ](https://github.com/nishant-666/Passing-data-in-React).
إذا كنت ترغب في تجربة المزيد.
> حسنا، هذا هو كل ما لدينا في هذا الدرس يا رفاق . تعلمٌ سعيد.

يمكنك [ابحث عن الرمز الموجود على GitHub] (https://github.com/nishant-666/passing-data-in-React) إذا كنت ترغب في تجربة المزيد.
----------
