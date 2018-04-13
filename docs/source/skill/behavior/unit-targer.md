# 單一目標技能 Unit Target

<hr>

### 藍圖設計思維:
點擊目標後給予攻擊或者Buff
- 可以給同時給目標攻擊和異常Buff
- 因為技能事件Event BP Spell to Actor是在選定目標後才呼叫, 角色需先移動到目標才會呼叫此事件

### 技能設定階段:
- Class Defaults>MOBA需設定**Name(技能名)**、**Skill Behavior(技能行為)**、**Face Skill(是否面對技能)**、**Cast Range(施法距離)**、**Texture(技能圖示)**、**Level CD(技能CD)**、**Level Mana Cast(技能耗魔)**  
![](https://i.imgur.com/dksWKt5.png)
- 不設定**Cast Range(施法距離)** 技能可能無法發動

### 找尋技能目標階段:

#### 1. 新增事件 : 
- 在主圖(EventGraph)視窗, 右鍵新增**Event BP Spwll to Actor**
- **Event BP Spwll to Actor**的Victim即為目標HeroCharacter  
![](https://i.imgur.com/fIm5NGw.png)

#### 2. 新增事件順序 : 
- 新增**Seqence**節點, Then0拉給傷害計算/上Buff, Then1拉給技能特效, BP會依照Then0 Then1 ...的順序執行

### 給予傷害或上Buff階段:

#### 傷害:

##### 0.設定Damage Map
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md),新增Variable Map的子Map:Damage Map

##### 1. 計算傷害:
- 新增**Get Player Controller**節點, 右拉此節點**Cast To MOBAPlayerController**, As MOMAPlayerController右拉出**Server Attack Compute**  
![](https://i.imgur.com/itjfckk.png)
- Attacker為**Caster**
- Victim為**Event BP Spell to Actor**
- Dtype為傷害類型:物傷、法傷和純傷
- Damage由Damage Map取得(依技能等級有所不同)

##### 2. 設定傷害:
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md),呼叫Damage Map  
![](https://i.imgur.com/92zSxNF.png)
- 傷害值丟給**Server Attack Compute**  
![](https://i.imgur.com/USscGut.png)

#### Buff:

##### 0.設定Duration Map
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md),新增Variable Map的子Map:Duration Map
- 可新增其他Map儲存Buff所需要用到跟技能等級掛勾的數值

##### 1.生成Buff
1. 主圖右鍵新增**Spawn Actor from Class**  
![](https://i.imgur.com/wb4vp49.png)
- Class選擇一個Buff, 繼承HeroBuff的BP類別
- Spawn Transform 為目標HeroCharacter(**Event BP Spwll to Actor**的Victim), 右拉出的**GetActorTransform**  
![](https://i.imgur.com/BSdwWsG.png)
2. 設定Buff變數Duration : 
- **Spawn Actor from Class**節點的Return Value為一個HeroBuff的實體Actor, 右拉出**Set Duration**節點設定HeroBuff底下的一個變數Duration的值  
![](https://i.imgur.com/1ZxHQBE.png)

##### 2.加Buff到英雄上 : 
- 目標HeroCharacter(**Event BP Spell to Actor**的Victim)右拉出的函式**Add Buff**, 不可重複的Buff則是**Add Unique Buff**
- **Spawn Actor from Class**節點的Buff丟給**Add Buff**  
![](https://i.imgur.com/ZkRS9Fl.png)

#### 攻擊+異常Buff:
- 參照上方給予敵方負面異常Buff+給予傷害合併即可

##### 需先設定Variable Map中的 Map
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md),新增此異常狀態的持續時間  
![](https://i.imgur.com/zTXP4t7.png)

##### 1.[生成Buff](#1生成Buff)
##### 2.[加Buff到英雄上](#2加Buff到英雄上-)
##### 3.[計算傷害](#1-計算傷害)
##### 4.[設定傷害](#2-設定傷害)

### 生成技能特效階段:
- 上Buff也許不需要此階段, 因為在HeroBuff BP裡設定了其特效
1. 新增**Spawn Actor from Class**節點, **Seqence**節點的Then1拉給此節點
- Class為特效類別
- Spawn Transform為**Event BP Spell to Actor**的Victim拉出的**GetActorTransform**  
![](https://i.imgur.com/1S6U6u4.png)

### 整個主圖:
- 一般攻擊技能  
![](https://i.imgur.com/6hfTDHR.png)
- Buff技能  
![](https://i.imgur.com/kcujb06.png)
- 攻擊+異常技能  
![](https://i.imgur.com/eF8p76F.png)
![](https://i.imgur.com/LhNhf2f.png)
