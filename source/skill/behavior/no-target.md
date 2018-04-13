# 無目標技能 No Target

<hr>

### 藍圖設計思維
以施法者為中心立即放技能, 以半徑找到所有影響目標或者只對自己有影響
- 可以是Buff技、攻擊技AOE或英雄面對方向的指向技
- 計算傷害或者給予Buff給自己
- 攻擊技也可以加上異常狀態Buff給敵人

### 技能設定階段
- Class Defaults>MOBA需設定**Name(技能名)**、**Skill Behavior(技能行為)**、**Texture(技能圖示)**、**Level CD(技能CD)**、**Level Mana Cast(技能耗魔)**  
![](https://i.imgur.com/MhId39x.png)

### 找尋技能目標階段
- 目標有可能是以自身為中心的AOE，或是指向技時英雄面對方向上的目標
- 指向技由Bullet處理目標，所以這邊只處理AOE的場合
- 如果是上Buff給自己也沒有此階段
- 如果有同時有**找尋技能目標階段**和**生成技能特效階段**，會使用seqence節點來區分執行順序

##### 1. 新增事件
- 在技能藍圖的主圖(EventGraph)上右鍵新增Event BP Spell Now, 點擊技能會立即呼叫此Event  
![](https://i.imgur.com/fXiqvEj.png)

##### 2. 事件順序
- 右鍵新增**Seqence**節點,藍圖會依順序跑, then0拉給找尋技能目標階段和給予傷害或上Buff階段 , then1拉給生成技能特效

##### 3.找尋自身為半徑的所有目標
-  右鍵新增**Caster** 節點,並左鍵拉此節點的線放開可搜尋到Caster(HeroCharacter)底下的Function : **Find Radius Actor by Location**新增之  
![](https://i.imgur.com/k9DZ3yR.png)
![](https://i.imgur.com/rC7sG4F.png)
- **Caster**拉出**GetActorLocation**節點給**Find Radius Actor by Location**當Center參數, 手動輸入半徑, 並勾選Check Alive檢查目標是否是活的  
![](https://i.imgur.com/8AMKNGi.png)

### 給予傷害/上Buff階段
- **Find Radius Actor by Location**節點輸出是一個HeroCharacter的Array, 使用**ForEachLoop**找到每個目標(HeroCharacter)給予傷害或Buff
- 或只對自己上Buff
- 傷害和Buff依技能等級有所不同, 使用Variable Map來儲存不同等級的傷害/效果

##### 0. 使用ForEachLoop找Array中的每個HeroCharacter
- 右鍵新增**ForEachLoop**節點, 此節點的左方輸入Array為**Find Radius Actor by Location**的Return Value  
![](https://i.imgur.com/DkvZavj.png)
- **ForEachLoop**節點的輸出就是一個目標HeroCharacter


##### 對目標攻擊時

###### 需先設定 Variable Map 中的 Damage Map

- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md#)

###### 呼叫攻擊計算函式
1. 右鍵新增**Get Player Controller** 節點, 拉此節點轉換成**MOBAPlayerController**  
![](https://i.imgur.com/8Xustbx.png)
![](https://i.imgur.com/ZVBYKSg.png)
2. **Find Radius Actor by Location**右方的執行線(白線)拉給**Cast to MOBAPlayerController**
3. 新增計算傷害函式 : 
- **Cast to MOBAPlayerController**節點的As MOBAPlayer Controller右拉可找到MOBAPlayer Controller底下的Function : **Server Attack Compute**
4. **Server Attack Compute**的Attacker為**Caster**(可右鍵再新增一次節點),Victim為目標HeroCharacter(**ForEachLoop**節點的Array Element)
![](https://i.imgur.com/yYphs7x.png)
- 傷害類型有物傷、法傷和純傷
![](https://i.imgur.com/vf24U23.png)
5. 取得**Variable Map**中Damage Map : 
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md#)
6. AOE的攻擊階段Overview:  
![](https://i.imgur.com/PbqUpsX.png)

##### 對目標Buff時

###### 需先設定Variable Map中的 Map
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md#),設定Duration Map,如有其他效果Map也一併新增

###### 生成Buff
和Passive的永久Buff不同, 需要設定Duration(效果期間)
1. 主圖右鍵新增**Spawn Actor from Class**  
![](https://i.imgur.com/wb4vp49.png)
- Class選擇一個Buff, 繼承HeroBuff的BP類別
- Spawn Transform 為目標HeroCharacter(**ForEachLoop**的Array Element或者**Caster**), 右拉出的**GetActorTransform**  
![](https://i.imgur.com/Jj4JAJV.png)
--
![](https://i.imgur.com/jOUQlj6.png)
2. 設定Buff變數Duration : 
- **Spawn Actor from Class**節點的Return Value為一個HeroBuff的實體Actor, 右拉出**Set Duration**節點設定HeroBuff底下的一個變數Duration的值  
![](https://i.imgur.com/1ZxHQBE.png)
3. 呼叫VariableMap的子Map給**Set Duration**節點 : 
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md#)

###### 加Buff到英雄上
1. 目標HeroCharacter(**ForEachLoop**的Array Element或者**Caster**), 右拉出的函式**Add Buff**, 不可重複的Buff則是**Add Unique Buff**  
![](https://i.imgur.com/HK0o4Rt.png)
--
![](https://i.imgur.com/b6SLhPQ.png)
- **Spawn Actor from Class**節點的Buff丟給**Add Buff**
![](https://i.imgur.com/5csGQKf.png)

##### 攻擊+異常狀態
- 實作上其實就是
1. 生成Buff給目標Character
2. 給予目標傷害
- 目標Character必定是敵人

###### 需先設定Variable Map中的 Map
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md#),新增此異常狀態的持續時間  
![](https://i.imgur.com/zTXP4t7.png)

###### 生成Buff
- 參照前面的[生成Buff](##生成Buff)
- Spawn Transform的目標HeroCharacter一定是敵人:**ForEachLoop**的Array Element
- Map為上面設定的StunDuration Map, 此異常的持續時間

###### 加Buff到英雄上
- 參照前面的[加Buff到英雄上](##加Buff到英雄上-)
- Add Buff的目標HeroCharacter一定是敵人:**ForEachLoop**的Array Element

###### 呼叫攻擊計算函式
- 參照前面的[呼叫攻擊計算函式](##呼叫攻擊計算函式)

### 生成技能特效階段:
- 如果對自己放Buff且已在HeroBuff設定其特效, 此階段可不用
1. 右鍵新增**Spawn Actor from Class**節點,**Seqence**的then1拉給此節點
2. Class選取要新增的特效類別, Spawn Transform為**Caster**節點拉出的**GetActorTransform**  
![](https://i.imgur.com/cTtpSXm.png)

### 整個主圖:
- 攻擊周遭敵軍技能
![](https://i.imgur.com/yovzvJi.png)

- 放Buff給自己
![](https://i.imgur.com/pkHm6zl.png)

- 放Buff給自己(加上技能特效和Buff唯一)
![](https://i.imgur.com/hKsqjUy.png)

- 施放技能給周遭友軍
![](https://i.imgur.com/t3Mi9fj.png)
![](https://i.imgur.com/fZ7mySk.png)

- 攻擊周遭敵軍並暈他們
![](https://i.imgur.com/po08wGJ.png)
![](https://i.imgur.com/8nxZJN4.png)
![](https://i.imgur.com/jVFBx3n.png)

***

## 往英雄面對方向的指向技
- 指向技的找尋目標、給予傷害和生成特效三個階段都是在Bullet(繼承SkillDirectionActor或SkillSplineActor)完成的
- 我們只需要生成Bullet並設定它的傷害和方向即可 

### 1. 新增指向技 : 
- 新增**Spawn Actor from Class**節點, Class選擇Bullet(子彈)繼承SkillDirectionActor, Spawn Transform為**Caster**的**GetActorTransform**  
![](https://i.imgur.com/OxTTCqT.png)

### 2. 設定方向 : 
- **Spawn Actor from Class**節點的Return Value右拉**Set Direction** , Attacker是**Caster**
- Dir是**Event BP Spell Now**的VFace To ,也許會需要**Normalize**和去掉Z值(不往上下偏移)
- VFace To右拉**Normalize**
- **Normalize**節點的Return Value上按右鍵選Split Struct Pin分為Return Value X Y Z  
![](https://i.imgur.com/NpNKuyB.png)
![](https://i.imgur.com/QaJEQGj.png)
- **Normalize**節點的任一Return Value右拉找到**Make Vector**,**Make Vector**節點的X Y分別是 **Normalize**節點Return ValueX Y, Z則設為0(防止上下飄移)  
![](https://i.imgur.com/bxIkK7d.png)

### 3. 設定傷害 : 
- **Spawn Actor from Class**節點的Return Value右拉**Set Damage**
- 參考[信長Variable Map設定和呼叫]  (/source/unreal-teach/common.md),呼叫Damage Map
![](https://i.imgur.com/XhmKwjU.png)

### 4. 整個主圖 : 
![](https://i.imgur.com/hLKborw.png)