# 新增技能 Create Skill

<hr>

### 建立

1. 在Content Browser底下的 **Content**  \> **MOBA** > **Hero** > **_英雄代號_** \> **Skill** 資料夾下滑鼠右鍵新增一個Blueprint Class  
![](https://i.imgur.com/uKQ3uaA.png)

2. 此Blueprint Class繼承**HeroSkill** class  
![](https://i.imgur.com/4PzdRLR.png)

3. 技能檔案命名規則為 : **_武將代號_**(E/R/T/W)_Skill  
![](https://i.imgur.com/Sb5gHep.png)![](https://i.imgur.com/5h96mIe.png)

4. 打開剛剛新增的BP技能進入BP編輯頁面， 找到工具列的**Class Defauls**底下的**MOBA**， 編輯**Name**(技能名字)、**Texture**(技能圖示) 
![](https://i.imgur.com/Tsljy16.png)
![](https://i.imgur.com/o5igKUS.png)

5. 打開英雄的BP(**_武將代號_**_hero)， 找到MOBA底下的**Skill Classes**右邊的+新增一個**array element**， 設定新技能如此便能在角色面板上看見此技能新增出來  
![](https://i.imgur.com/e5dhCjC.png)
![](https://i.imgur.com/nfbyOIa.png)
![](https://i.imgur.com/FjaYmxZ.png)

    <div class="note note-teal">最多只能有 4 個技能</div>

6. 回到BP技能編輯頁面， 工具列Class Details > MOBA底下的**Level CD**，此技能每個等級的CD時間， 技能等級最大有多少就新增幾個**array element**  
![](https://i.imgur.com/DOCwY8t.png)

    <div class="note note-teal">等級越高，CD時間應越短</div>

7. **Level Mana Cost**為此技能每個等級的耗魔， 同上新增**array element**

8. **MOBA**底下的**Variable Map**為此技能的"依技能等級有所不同"的變數， 點右邊+新增一個**Map**，此**Map**名稱**自定義**. 
    - 攻擊技能應有**Damage** : **Map**取名為**Damage**， 點**Values**右側的+為此**Map**新增每個等級的傷害量  
    ![](https://i.imgur.com/zFh9kb8.png)
    - Buff技能同樣， 例如Buff了爆擊率 : 命名為**Critical**並新增每個等級的爆擊率
    ![](https://i.imgur.com/2FG8r0a.png)