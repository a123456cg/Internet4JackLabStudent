# Breadcrumbs

<hr>

#### 說明

該組件名稱主要用途為表示進度、步驟等指標。

#### 使用

- Demo
<div class="breadcrumbs">
  <div class="inner">
    <ul class="cf">
      <li>
        <a class="active" href="/source/repo/clone.md">
          <span>1</span>
          <span>專案下載</span>
        </a>
      </li>
      <li>
        <a href="/source/repo/thirdparty.md">
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


- Markdown
```html
<div class="breadcrumbs">
    <div class="inner">
        <ul class="cf">
            <li>
            <a class="active" href="/source/repo/clone.md">
                <span>1</span>
                <span>專案下載</span>
            </a>
            </li>
            <li>
            <a href="/source/repo/thirdparty.md">
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
```