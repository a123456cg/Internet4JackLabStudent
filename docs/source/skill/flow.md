# 技能流程 Skill Flow

<hr>

### 開發階段

#### 1.技能設定階段
- 在BP事件發生前, 設定這個技能的Class Defaults下的MOBA屬性。  
![](https://i.imgur.com/QRUM7ry.png)

    - Name(技能名)
    - Skill Behavior(技能行為)
    - Texture(技能圖示)
    - HintActor(技能游標)
    - Level CD(技能CD)
    - Level Mana Cast(技能耗魔)


#### 2.找尋技能目標階段
- AOE需要在BP判斷技能命中對象

#### 3.攻擊或上Buff階段
- 傷害和Buff效果是依技能等級而有所不同，此時需要使用Class Defaults下MOBA屬性的Variable Map自定義技能的傷害(Damage Map)或效果(Something Map)
- Buff為繼承HeroBuff的BP Class ,此BP Class有自己的特效

#### 4.生成技能特效階段
- 技能最後要生成特效

<div class="note note-yellow">
指向技的 2、3、4 階段由繼承 SkillDirectionActor 或 SkillSplineActor 的BP class : Bullet完成</div>