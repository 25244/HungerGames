# HungerGames

## 1.游戏介绍

游戏简介：我饿，我馋，我想吃零食。  
游戏玩法：每个关卡玩家都需要想方设法靠近“黄油零食”来吃掉零食，其中玩家通过键盘的“A”，“W”，“S”，“D”键或者“←”，“↑”，“↓”，“→”键进行移动，鼠标左键进行射击。
<img width="556" alt="1" src="https://github.com/25244/HungerGames/assets/90137164/7f04003d-1c64-49fd-ac34-d181ef69c112">  
<img width="556" alt="7" src="https://github.com/25244/HungerGames/assets/90137164/eeeccc56-f8eb-484b-b054-e8b4ec66df90">

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

(不推荐)同时我们还提供一个\*.unitypackage 文件，该为场景的导出包，并无环境配置，如果需要运行该文件需要进行以下操作：  
1.自行安装 Python 和 Unity3D；  
2.新键 Unity 项目；  
<img width="963" alt="10" src="https://github.com/25244/HungerGames/assets/90137164/e73cdfcb-757f-451c-986b-5373f56f5082">

3.项目中的 Packages/manifest.json 新增一行：  
`com.unity.scripting.python": "5.0.0-pre.5`  
<img width="641" alt="11" src="https://github.com/25244/HungerGames/assets/90137164/14a77df4-5a8e-4e26-8e7b-3a72594b60b6">

这里的版本是基于 Unity 的版本 2020.3.30f1c1，需要等待一段时间安装。
<img width="734" alt="12" src="https://github.com/25244/HungerGames/assets/90137164/07d41e9d-4a89-43f4-bd14-57c5e118cd4e">

如果是更高的版本可以到 Package Manager 找到 Python Scripting 进行升级。  
<img width="601" alt="13" src="https://github.com/25244/HungerGames/assets/90137164/90f0b705-5e66-45e3-9563-e2da28a2b654">

4.在 Unity3D 项目环境中安装 pygame；  
游戏中的开始界面由 pygame 构成，所以需要导入 pygame 模块。  
具体操作是：点击 项目 → 菜单 →Edit→Project Setting→Python Scripting→Spawn shell in environment，并添加以下代码  
`pip install pygame`

<img width="675" alt="14" src="https://github.com/25244/HungerGames/assets/90137164/3ef3a58d-7513-4e78-8def-6ef941d82783">

5.导入包前的项目装备；  
由于，导入包中不能自动添加层级，所以在正式导入包之前得添加层级  
User Layer6：Bullet  
User Layer7：NowLevels  
User Layer8：Player  
User Layer9：Ground  
6.导入\*.unitypackage 文件。  
一般情况下，这个流程就能正常运行包，而在实际操作过程中，导入包的碰撞器大小发生了变化，无法运行获取参数导致报错等的问题 ，在调整的时候发现出现的意外问题还挺多，也就是导入包的方式得进行多次重新的调整，修改和处理，所以不推荐该运行文件的方法。  
当然除了导入\*.unitypackage 文件意外，其他的方法已经能够让 Unity3D 和 python 进行结合，并且能够安装 python 所需的模块，并且正常运行，所以仍写下配置过程于方法。

### 3.2 游戏美术

建模三个场景，这个游戏风格为 lowpoly。为了省空间几乎没用贴图。  
第一关使用了粒子系统。  
![15](https://github.com/25244/HungerGames/assets/90137164/5ccdf519-6a21-447a-9615-ff55c3fe6a38)

第二关使用灯光系统。  
![16](https://github.com/25244/HungerGames/assets/90137164/ce15a3f8-b396-4b7e-85fe-1b25afa08096)

第三关附加了一个针对草丛裁剪透明的，以及一个深度水体动画的。  
![17](https://github.com/25244/HungerGames/assets/90137164/1b058b83-3a36-460c-9a30-1526e886c8ab)

### 3.3 游戏音乐

基于游戏风格，在制作背景音乐时增加简单、明快的特点，对游戏不会产生过多的干扰，使玩家更加专注于游戏本身。音乐使用三条音轨，在音色选择上都着重于音色本身的清新感，通过轻快的节奏，偏迷幻电子的风格使音乐更加符合游戏特点。  
乐曲速度为 94，在活跃的同时不会使玩家产生急迫感。

低音选择“琶音动画”音色，经过“水下”效果处理，增加音乐的汪洋感，更符合游戏美术以蓝色为主题的视觉效果。  
第二条音轨选择“迷幻铃铛”音色，低音部分用四分音符拉长，作为环境音，高音选择十六分之一音符，用短暂的铃铛声作为次主音，增加灵动的氛围感。

第三条音轨使用“声音盒子主音”来制作，也是音乐的主旋律。音色本身具有电子感，简单的旋律增加音乐活泼可爱的特点，每拍之间首位音调相同，达到延续不断的音乐效果。在旋律编写完成后整体八度降调，削弱音色本身的科技感，增加生命感，达到轻松的氛围效果。

在与游戏匹配时在起始页面只使用第一轨与第二轨，在进入游戏后加入第三轨，增加游戏的层次感，能给玩家带来层层带入的感觉，此时第二轨作为次主音，铃铛音色的旋律编写会被凸显。

## 4.游戏演示

https://github.com/25244/HungerGames/assets/90137164/3e14a359-189f-4780-ab1a-e50f6b7623d9
