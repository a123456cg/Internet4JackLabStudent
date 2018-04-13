# 被動技能 Passive

<hr>

### 藍圖設計思維
***技能習得後自動施放技能***, 給予自身效果期間長且有唯一性的BUFF
- 不需設Duration(效果期間), 在Buff BP內設定Duration
- 有唯一性, 相同名稱的BUFF新的會蓋過舊的無法疊加
- 對象是自己
- 只有**技能設定階段**和**上Buff階段**。**找尋技能目標階段**->目標是自己 ; **生成技能特效階段**->僅有Buff特效在上Buff時已有

### 技能設定階段
- Class Defaults>MOBA需設定**Name(技能名)**、**Skill Behavior(技能行為)**、**Texture(技能圖示)**、**Level CD(技能CD)**、**Level Mana Cast(技能耗魔)**  
![](https://i.imgur.com/BIffKaA.png)
- **Level CD(技能CD)**和**Level Mana Cast(技能耗魔)** 的值是右邊+號新增出來的, 代表每個技能等級各自的CD和耗魔

### 上Buff階段

#### 1.新增事件
- 在技能藍圖的主圖(EventGraph)上右鍵新增Event BP Spell Passive, 技能習得後立即呼叫此Event 
![](https://i.imgur.com/wraRsc5.png)

#### 2.生成BUFF
- 右鍵新增**Spawn Actor from Class**節點, Class選擇繼承HeroBuff的BP類別(此時節點名稱會變成:SpawnActor XXXX)  
![](https://i.imgur.com/m9ErR9Y.png)

#### 3.生成位置
- 右鍵新增**Caster**節點(一個HeroSkill下的HeroCharacter類別變數), 右拉**Caster**上的藍點放開找到**GetActorTransform**此為**Caster**底下的函式 ,拉給**Spawn Actor from Class**節點的Spawn Transform  
![](https://i.imgur.com/c0eU75r.png)
![](https://i.imgur.com/0lgof1J.png)
![](https://i.imgur.com/Wgnv6rU.png)
- 如此一來就生成一個BP類別的實體Actor了

#### 4.Buff Unique Map 
- **Spawn Actor from Class**節點的Return Value右拉找到**Buff Unique Map**此為HeroBuff底下的一個Map變數  
![](https://i.imgur.com/qPg9Uq3.png)

#### 5.加入新的element到Buff Unique Map裡
- **Buff Unique Map**節點右拉輸入**Add**為此Map加入Buff增強角色的效果, 此例是增加物理爆擊率
![](https://i.imgur.com/fiCiEcn.png)  
- 新增的element還需要加入一個浮點小數代表Buff的量

#### 6.新增VariableMap的子Map
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md)

#### 7. Buff Unique Map新增的Buff效果數值
- **Buff Unique Map**的**Add**節點下面的數值由Critical Map提供  
![](https://i.imgur.com/7elMd6G.png)

#### 8. 加入Buff到英雄上
- 右鍵新增**Caster**節點, 右拉**Caster**節點找到**Caster**底下的**Add Unique Buff**函數  
![](https://i.imgur.com/ReRXslp.png)
- **Add Unique Buff**節點的Buff為**Spawn Actor from Class**節點的Return Value  
![](https://i.imgur.com/vYA1jaS.png)
- **注意白線(執行線)的順序, 一定要先設Buff Unique Map才能Add Unique Buff**

### 整個主圖
![](https://i.imgur.com/mzd1Frx.png)