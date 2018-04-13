# 範圍技能 AOE

<hr>

### 藍圖設計思維:
藍圖設計和No Target的攻擊技能一樣, 唯一差別是找尋技能目標階段的技能中心位置由滑鼠點擊決定  
![](https://i.imgur.com/BMWL8ts.png)
- 給予傷害或上Buff階段和生成技能特效階段都和No Target一樣

### 技能設定階段:
- Class Defaults>MOBA需設定**Name(技能名)**、**Skill Behavior(技能行為)**、**Texture(技能圖示)**、**Hint Actor(目標游標)**、**Level CD(技能CD)**、**Level Mana Cast(技能耗魔)**  
![](https://i.imgur.com/HWAiPLp.png)

#### Hint Actor(目標游標):

##### 目標游標圖示:
1. 在Skill檔案位置右鍵新增一個Blueprint Class繼承SkillHintActor  
![](https://i.imgur.com/ID5ZZ5S.png)
2. 名稱為技能名+Hint  
![](https://i.imgur.com/4eUnMfF.png)
3. 打開此HintActor藍圖編輯, 工具列Class Defaults的Skill Hint下的Skill Type修改成Range Skill  
![](https://i.imgur.com/Tsljy16.png)
![](https://i.imgur.com/nGaDZaI.png)
4. Fly Skill下設定你的Skill Diameter、Skill Cast Radius、Minimal Cast Radius  
![](https://i.imgur.com/hKmtpSh.png)
5. Components 視窗找到BodySprite修改底下Sprite > Source Sprite  
![](https://i.imgur.com/bfOCRZX.png)
6. Sprite放在Content Browser：Content > MOBA > Skill資料夾下 ,右鍵新增Sprite  
![](https://i.imgur.com/2V9rkNq.png)
7. 打開Sprite在Source Texture選貼圖, Source Dimension改成跟圖片解析度等比例即可  
![](https://i.imgur.com/DeVwAEE.png)

##### 點擊技能後，滑鼠位置會顯示剛剛的Sprite
- 再點左鍵呼藍圖事件**Event BP Spell to Position**．
- 再點右鍵則取消技能施放

### 找尋技能目標階段:

#### 0.新增事件：
- 主圖下,新增**Event BP Spell to Position**

#### 1.事件順序：
- 新增**seqence**, Then0放事件主體, Then1放技能特效

#### 2.找到所有目標:
- 新增**Caster**, 右拉新增**Caster**函式:**Find Radius Actor by Location**
- Center是**Event BP Spell to Position**的Pos
- Radius手動輸入
- Check Alive要勾選  
![](https://i.imgur.com/9Dj2gky.png)

#### 3. 拜訪每個目標:
- ForEachLoop  
![](https://i.imgur.com/f2m4H2C.png)

### 給予傷害或上Buff階段:

#### 傷害:
- 和No Target的攻擊技能一樣
1. 找到MOBAPlayerController  
![](https://i.imgur.com/3ozRO1Q.png)
- 插入到ForEachLoop前,可以不用每個Loop都執行一次
2. Variable Map的Damage Map  
![](https://i.imgur.com/XeOeZKq.png)
![](https://i.imgur.com/jDqHPop.png)
3. MOBAPlayerController的Server Attack Compute   
![](https://i.imgur.com/NGAoHpN.png)

#### Buff:
1. 新增**Spawn Actor from Class**
- Class 選繼承HeroBuff的BP Class
- Spawn Transform是**Event BP Spell to Position**的Pos右拉出的**Make Transform(建立一個transform格式)**   
![](https://i.imgur.com/z9XnJEa.png)
2. **Spawn Actor from Class**的Buff右拉**SetDuration**
- Variable Map的Duration Map設給**SetDuration**  
![](https://i.imgur.com/NOncNkA.png)
3. 目標的Add Buff/Add Unique Buff  
![](https://i.imgur.com/5qgFDU5.png)

#### 傷害+Buff:
給予傷害和給予Buff的BP合起來即可, 見[整個主圖](#整個主圖2)

### 生成技能特效階段:
- Spawn Transform在**Event BP Spell to Position**的Pos右拉**Make Transform**  
![](https://i.imgur.com/Xey2ZZU.png)

### 整個主圖:
- 攻擊  
![](https://i.imgur.com/zkDRp8N.png)
- Buff  
![](https://i.imgur.com/TYyOsNi.png)
![](https://i.imgur.com/oKZHmWb.png)

- 攻擊+Buff  
![](https://i.imgur.com/Jg15TaM.png)
![](https://i.imgur.com/HEhR1oj.png)
![](https://i.imgur.com/U8r7ULH.png)
