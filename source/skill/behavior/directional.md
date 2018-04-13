# 指向技能 Directional

<hr>

### 藍圖設計思維:
指向技的找尋技能目標階段、給予傷害、生成技能特效階段皆由繼承 SkillDirectionActor或 SkillSplineActor的BP class完成,BP Class 稱之我們命名為Bullet
- 指向技點擊之後, 滑鼠游標決定攻擊方向,左鍵確定右鍵取消 
- 在BP上我們只要生成Bullet,設定此Bullet的方向跟傷害即可

### 技能設定階段:
- Class Defaults>MOBA需設定**Name(技能名)**、**Skill Behavior(技能行為)**、**Texture(技能圖示)**、**Hint Actor(目標游標)**、**Level CD(技能CD)**、**Level Mana Cast(技能耗魔)**  
![](https://i.imgur.com/uplcoeM.png)

#### Hint Actor(目標游標):

##### 目標游標圖示:
1. 在Skill檔案位置右鍵新增一個Blueprint Class繼承SkillHintActor  
![](https://i.imgur.com/ID5ZZ5S.png)
2. 名稱為技能名+Hint  
![](https://i.imgur.com/4eUnMfF.png)
3. 打開此HintActor藍圖編輯, 工具列Class Defaults的Skill Hint下的Skill Type修改成Direction Skill  
![](https://i.imgur.com/Tsljy16.png)
![](https://i.imgur.com/8ia7tdK.png)
4. Components 視窗找到BodySprite修改底下Sprite > Source Sprite  
![](https://i.imgur.com/nqbN4xX.png)
5. Components 視窗找到HeadSprite修改底下Sprite > Source Sprite  
![](https://i.imgur.com/RqizLS0.png)
6. Components 視窗找到FootSprite修改底下Sprite > Source Sprite  
![](https://i.imgur.com/HBW9rtf.png)
- BodySprite會伸縮,而另外兩個不會變動 
- Sprite放在Content Browser：Content > MOBA > Skill資料夾下 

### 找尋技能目標&給予傷害&生成技能特效階段 :
- 在主圖(EventGraph)新增**Event BP Spell to Direction**  
![](https://i.imgur.com/I5cA5pu.png)

#### 生成Bullet:
1. 新增**Spawn Actor from Class**
- Class選繼承SkillDirectionActor或 SkillSplineActor的BP class
- Spawn Transform是**Caster**右拉出來的**GetActorTransform**  
![](https://i.imgur.com/IavXMbG.png)

#### 設定Bullet方向:
如果此Bullet是繼承自SkillDirectionActor會需要**Set Direction**
如果此Bullet是繼承自SkillSplineActor,則只需**Set Attacker**  
![](https://i.imgur.com/18bIINZ.png)

1. 設定方向, **Spawn Actor from Class**節點的Return Value是Bullet物件
2. 右拉**Spawn Actor from Class**節點的Return Value出**Set Direction**
- Attacker是**Caster**
- Dir是**Event BP Spell to Direction**減去**Caster**的GetActorLocation  
![](https://i.imgur.com/6fCGIF5.png)

#### 設定Bullet傷害:
1. **Spawn Actor from Class**節點的Return Value右拉**Set Damage**
2. Damage Map
- 參考[信長Variable Map設定和呼叫](/source/unreal-teach/common.md),得到此技能的傷害給**Set Damage**  
![](https://i.imgur.com/A8bcnul.png)

### 整個主圖:
![](https://i.imgur.com/6AjKa3T.png)
