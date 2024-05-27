# HungerGames

## 1.游戏介绍

游戏简介：我饿，我馋，我想吃零食。  
游戏玩法：每个关卡玩家都需要想方设法靠近“黄油零食”来吃掉零食，其中玩家通过键盘的“A”，“W”，“S”，“D”键或者“←”，“↑”，“↓”，“→”键进行移动，鼠标左键进行射击。

## 2.任务分工

游戏开发&策划：杨钰铃  
游戏美术：胡楠  
游戏音效：王雨欣  
游戏 UI：赵慧君

## 3.制作说明

### 3.1 游戏开发

该游戏由 Unity3D 引擎作为游戏开发，C#和 Python 作为编程语言。  
整个游戏场景由关于运行的脚本有两个，一个 C#脚本（调用 Python），一个 Python 脚本（被调用用于 Unity3D）。

https://github.com/25244/HungerGames/assets/90137164/e0ee2803-0056-4c1c-abc7-cc63ea04b5e4

需要说明的是，该游戏所使用的 python 环境是由 unity3D 提供的 Python For Unity，由于 unity3D 尚未稳定 python 功能，仅提供在编辑环境中`using UnityEditor.Scripting.Python;`能够使用，无法发布。

```C#
using System.Diagnostics;
using System.IO;
using UnityEditor.Scripting.Python;
using UnityEngine;
public class PythonManager : MonoBehaviour
{
    [System.Obsolete]
    void Update()
    {
        string path = Application.dataPath + "/Python/pythonTest.py";
        PythonRunner.RunFile(path);
    }

}
```

所以我们提供了一个\*.zip 文件，该文件环境已经配置好，可直接使用 Unity3D 打开运行。

(不推荐)同时我们还提供一个*.unitypackage 文件，该为场景的导出包，并无环境配置，如果需要运行该文件需要进行以下操作：  
1.自行安装 Python 和 Unity3D；  
2.新键 Unity 项目；  
3.项目中的 Packages/manifest.json 新增一行：  
`com.unity.scripting.python": "5.0.0-pre.5`  
这里的版本是基于 Unity 的版本 2020.3.30f1c1，需要等待一段时间安装。  
如果是更高的版本可以到 Package Manager 找到 Python Scripting 进行升级。  
4.在 Unity3D 项目环境中安装 pygame；  
游戏中的开始界面由 pygame 构成，所以需要导入 pygame 模块。  
具体操作是：点击 项目 → 菜单 →Edit→Project Setting→Python Scripting→Spawn shell in environment，并添加以下代码  
`pip install pygame`  
5.导入包前的项目装备；  
由于，导入包中不能自动添加层级，所以在正式导入包之前得添加层级  
User Layer6：Bullet  
User Layer7：NowLevels  
User Layer8：Player  
User Layer9：Ground  
6.导入*.unitypackage 文件。  
一般情况下，这个流程就能正常运行包，而在实际操作过程中，导入包的碰撞器大小发生了变化，无法运行获取参数导致报错等的问题 ，在调整的时候发现出现的意外问题还挺多，也就是导入包的方式得进行多次重新的调整，修改和处理，所以不推荐该运行文件的方法。  
当然除了导入\*.unitypackage 文件意外，其他的方法已经能够让 Unity3D 和 python 进行结合，并且能够安装 python 所需的模块，并且正常运行，所以仍写下配置过程于方法。

### 3.2 游戏美术
