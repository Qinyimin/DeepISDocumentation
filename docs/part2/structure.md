# 项目组织结构

项目文件层次结构如下：

```
.
├── public              	#
│   ├── index.html          # The origin html
│   └── manifest.json       # 
│
├── src		                # main source file holder
│   ├── component           # React component library
│   ├── image               # Image file holder
│   ├── redux               # useInfo
│   ├── App.js				
│   ├── index.js
│   └── DashBoard.js        # Connects platform and extension projects
│
├── ...                     
├── package.json            # Shared devDependencies and commands
└── README.md               # This file
```

React组件放于src/component中，每个组件形成文件夹，由index.js文件导出，引用时引用至文件夹即可，如：

```
import {CaseManager} from './component/CaseManagement';
```

