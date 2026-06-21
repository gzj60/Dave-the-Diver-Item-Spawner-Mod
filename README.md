# Dave the Diver Item Spawner Mod

English | [中文](#中文)

A BepInEx IL2CPP plugin for **Dave the Diver** that adds an in-game item spawner panel. Press `F8` in game, search for an item, choose an amount, and add it through the game's save/storage APIs.

一个用于 **潜水员戴夫 / Dave the Diver** 的 BepInEx IL2CPP 插件。它会在游戏内添加物品生成面板：按 `F8` 打开，搜索物品，输入数量，然后通过游戏自己的存档/库存 API 添加物品。

> This is an unofficial mod. Back up your save before using it.
>
> 这是非官方 Mod。使用前建议先备份存档。

## Features

- Toggle the item spawner panel with `F8`.
- Search by localized item name, internal text id, or numeric `TID`.
- Add selected search results.
- Add a direct numeric `TID` even when search results are incomplete.
- Route normal items to inventory and ingredients to ingredient storage.
- Clamp item amounts to a safe positive range.
- Show status messages in the panel and write details to the BepInEx log.

## Requirements

- **Dave the Diver** on Windows.
- **BepInEx IL2CPP** installed in the game folder.
- BepInEx interop assemblies generated under `BepInEx\interop`.
- .NET SDK installed for building from source.

The project defaults to this game path:

```powershell
E:\SteamLibrary\steamapps\common\Dave the Diver
```

If your game is installed somewhere else, pass `DaveTheDiverRoot` or `GameRoot` when building.

## Build

From the repository root:

```powershell
dotnet build .\DaveItemSpawner\DaveItemSpawner.sln -c Release
```

If your game path is different:

```powershell
dotnet build .\DaveItemSpawner\DaveItemSpawner.sln -c Release -p:DaveTheDiverRoot="D:\SteamLibrary\steamapps\common\Dave the Diver"
```

The plugin DLL will be created at:

```text
DaveItemSpawner\src\DaveItemSpawner\bin\Release\net6.0\DaveItemSpawner.dll
```

## Install

Create a plugin folder under the game install and copy the DLL:

```powershell
$gameRoot = "E:\SteamLibrary\steamapps\common\Dave the Diver"
New-Item -ItemType Directory -Force -Path "$gameRoot\BepInEx\plugins\DaveItemSpawner"
Copy-Item -Force ".\DaveItemSpawner\src\DaveItemSpawner\bin\Release\net6.0\DaveItemSpawner.dll" "$gameRoot\BepInEx\plugins\DaveItemSpawner\DaveItemSpawner.dll"
```

To uninstall, remove:

```text
BepInEx\plugins\DaveItemSpawner
```

## Usage

1. Start the game with BepInEx installed.
2. Load a save.
3. Press `F8` to show or hide the item spawner panel.
4. Search by item name, text id, or numeric `TID`.
5. Select an item and enter an amount.
6. Click `Add Selected`, or enter a numeric `TID` and click `Add TID`.

Some special or progression-related items may fail or behave differently. The plugin reports failures in the panel and logs exception details through BepInEx.

## Development

Project layout:

```text
DaveItemSpawner/
  DaveItemSpawner.sln
  src/DaveItemSpawner/          Plugin source
  tests/DaveItemSpawner.Tests/  No-package console test harness
docs/
  superpowers/specs/            Design notes
  superpowers/plans/            Implementation plan
```

Run helper tests:

```powershell
dotnet run --project .\DaveItemSpawner\tests\DaveItemSpawner.Tests\DaveItemSpawner.Tests.csproj
```

## Notes

- This mod does not overwrite base game files.
- Removing the plugin folder disables the mod.
- Always keep a save backup before adding items.
- BepInEx logs are usually written to `BepInEx\LogOutput.log`.

---

# 中文

[English](#dave-the-diver-item-spawner-mod) | 中文

## 功能

- 按 `F8` 打开或关闭物品生成面板。
- 支持按本地化物品名称、内部文本 ID 或数字 `TID` 搜索。
- 可以添加搜索结果中选中的物品。
- 搜索结果不完整时，也可以直接输入数字 `TID` 添加。
- 普通物品会进入库存，食材会进入食材仓库。
- 物品数量会限制在安全的正整数范围内。
- 面板会显示操作状态，详细信息会写入 BepInEx 日志。

## 环境要求

- Windows 版 **Dave the Diver / 潜水员戴夫**。
- 游戏目录中已安装 **BepInEx IL2CPP**。
- 已生成 `BepInEx\interop` 下的 interop 程序集。
- 已安装 .NET SDK，用于从源码构建。

项目默认游戏路径是：

```powershell
E:\SteamLibrary\steamapps\common\Dave the Diver
```

如果你的游戏安装在其他位置，构建时传入 `DaveTheDiverRoot` 或 `GameRoot`。

## 构建

在仓库根目录运行：

```powershell
dotnet build .\DaveItemSpawner\DaveItemSpawner.sln -c Release
```

如果游戏路径不同：

```powershell
dotnet build .\DaveItemSpawner\DaveItemSpawner.sln -c Release -p:DaveTheDiverRoot="D:\SteamLibrary\steamapps\common\Dave the Diver"
```

构建后的插件 DLL 位于：

```text
DaveItemSpawner\src\DaveItemSpawner\bin\Release\net6.0\DaveItemSpawner.dll
```

## 安装

在游戏目录下创建插件文件夹并复制 DLL：

```powershell
$gameRoot = "E:\SteamLibrary\steamapps\common\Dave the Diver"
New-Item -ItemType Directory -Force -Path "$gameRoot\BepInEx\plugins\DaveItemSpawner"
Copy-Item -Force ".\DaveItemSpawner\src\DaveItemSpawner\bin\Release\net6.0\DaveItemSpawner.dll" "$gameRoot\BepInEx\plugins\DaveItemSpawner\DaveItemSpawner.dll"
```

卸载时删除这个目录即可：

```text
BepInEx\plugins\DaveItemSpawner
```

## 使用方法

1. 确认游戏已安装 BepInEx，然后启动游戏。
2. 进入一个存档。
3. 按 `F8` 显示或隐藏物品生成面板。
4. 输入物品名称、文本 ID 或数字 `TID` 搜索。
5. 选择物品并输入数量。
6. 点击 `Add Selected`，或输入数字 `TID` 后点击 `Add TID`。

部分特殊物品或剧情相关物品可能添加失败，或者表现与普通物品不同。插件会在面板中显示失败信息，并通过 BepInEx 记录详细异常。

## 开发

项目结构：

```text
DaveItemSpawner/
  DaveItemSpawner.sln
  src/DaveItemSpawner/          插件源码
  tests/DaveItemSpawner.Tests/  无额外测试包的控制台测试
docs/
  superpowers/specs/            设计说明
  superpowers/plans/            实现计划
```

运行辅助测试：

```powershell
dotnet run --project .\DaveItemSpawner\tests\DaveItemSpawner.Tests\DaveItemSpawner.Tests.csproj
```

## 注意事项

- 本 Mod 不会覆盖游戏本体文件。
- 删除插件文件夹即可禁用 Mod。
- 添加物品前建议备份存档。
- BepInEx 日志通常位于 `BepInEx\LogOutput.log`。
