# Variable Map 設定和呼叫

<hr>

### 設定Variable Map的子Map

#### Damage Map
1. 工具列點擊Class Defaults  
![](https://i.imgur.com/Tsljy16.png)
2. 找到MOBA下的Variable Map
3. 按下Variable Map右邊的+ , 新增一個名稱可自定義的Map
4. 此Map填上Damage
5. 展開Damage Map底下的Values找到右邊的+ ,新增技能等級數個Value
6. 填上各等級的傷害  
![](https://i.imgur.com/Q45r3AQ.png)

#### Other Map
- 其他特殊效果只要在(4.)填上不同名稱;以及在(6.)填上不同效果值即成為其他效果Map
- 例如Duration Map(效果持續時間):  
![](https://i.imgur.com/wgmPtC5.png)
- 例如Critical Map(爆擊率):  
![](https://i.imgur.com/2FG8r0a.png)

### 在主圖 (EventGraph) 視窗中呼叫 Variable Map 的子 Map
##### 以 Damage Map 為例
1. 右鍵新增**Variable Map**節點, 右拉出**Find**節點, **Find**節點輸入Damage即取得Damage Map  
![](https://i.imgur.com/aanRbah.png)
2. 右鍵Get **Current Level**
3. **Current Level**節點右拉輸入-(減號)得到interger - interger運算元節點, 下面輸入1表示減1  
![](https://i.imgur.com/cAgqVDc.png)
4. **Find**節點右拉輸入Break新增**Break LevelVariable**把Damage Map的參數分開成float array, 此array右拉輸入Get新增**Get**節點, 此**Get**節點依照Index = **Current Level**-1取出Array裡的值  
![](https://i.imgur.com/vyIszxG.png)