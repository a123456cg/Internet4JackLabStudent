# 安裝套件 Package

<div class="breadcrumbs">
  <div class="inner">
    <ul class="cf">
      <li>
        <a href="/source/repo/clone.md">
          <span>1</span>
          <span>專案下載</span>
        </a>
      </li>
      <li>
        <a class="active" href="/source/repo/thirdparty.md">
          <span>2</span>
          <span>安裝套件</span>
        </a>
      </li>
      <li>
        <a href="/source/repo/compiled.md">
          <span>3</span>
          <span>專案編譯</span>
        </a>
      </li>
      <li>
        <a href="/source/repo/update.md">
          <span>4</span>
          <span>更新專案</span>
        </a>
      </li>
    </ul>
  </div>
</div>

<hr>

### 關於套件

本遊戲有安裝一些第三方套件進行開發，因此需要先將**全部**進行安裝，未來若有引入新的，皆可以在 [Releases](https://github.com/RemakeAONTeam/AON/releases) 中找到。

目前引入的套件列表：

- [flann](https://github.com/RemakeAONTeam/AON/releases/tag/flann)
- [mqtt](https://github.com/RemakeAONTeam/AON/releases/tag/mqtt)
- [lz4](https://github.com/RemakeAONTeam/AON/releases/tag/lz4)

### 如何安裝

1. 從 [Releases](https://github.com/RemakeAONTeam/AON/releases) 下載指定的套件。
    <div class="note note-teal">通常檔案格式為：zip、rar、7z</div>

2. 將檔案解壓縮後放置於以下指定路徑，`\Epic Games\` 為你的 Unreal 安裝路徑：
    ```bash
    "C:\Program Files\Epic Games\UE_4.19\Engine\Source\ThirdParty"
    ```
    <div class="note note-teal">UE_4.19：請根據你的 UE 引擎，選擇資料夾。</div>