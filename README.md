# PlayerTrack（台服 / Dalamud API 13）

這是 [Infiziert90/PlayerTrack](https://github.com/Infiziert90/PlayerTrack) 的分支（作者 Infi、kalilistic），把組建目標改成台灣版用戶端用的 [yanmucorp/Dalamud](https://github.com/yanmucorp/Dalamud) **API 13 / .NET 9**，給 [cycleapple/XIVTCLauncher](https://github.com/cycleapple/XIVTCLauncher) 手動安裝。

PlayerTrack 用來記錄遇見的玩家和一起打過的內容，可以分類、寫筆記，並在改名或換伺服器之後繼續追蹤。顏色、圖示、名牌與提醒仍是上游的功能。

## 安裝（XIVTCLauncher）

1. 在 XIVTCLauncher 啟用 Dalamud，進過一次遊戲，讓設定資料夾建立起來，然後**關閉遊戲**。
2. 從 [api13-tw-3.6.1.1 發行頁](https://github.com/pollyhaei-ai/PlayerTrack/releases/tag/api13-tw-3.6.1.1) 下載 `PlayerTrack-api13-tw-3.6.1.1.zip`，解壓到登入時使用的 dev plugins 資料夾。解壓後會得到 `PlayerTrack\`（內含 `PlayerTrack.dll`、`PlayerTrack.json`，以及 NuGet 相依組件）：
   - 共用設定：`%AppData%\FFXIVSimpleLauncher\Dalamud\Config\devPlugins\`
   - 帳號自己的插件設定檔：`%AppData%\FFXIVSimpleLauncher\Profiles\<設定檔 ID>\Dalamud\devPlugins\`
3. 確認檔案在 `devPlugins\PlayerTrack\`，`PlayerTrack.dll` 和 `PlayerTrack.json` 同一層。
4. 進遊戲後用 `/xldev` 啟用 PlayerTrack，也可以在那裡重新載入。
5. `/ptrack` 開啟主視窗。`/ptrackconfig` 開啟設定。

## 使用前請先看

- **不要裝到官方 Dalamud API 14／15**（國際服 XIVLauncher）。這個組建只給台服 yanmucorp API 13。
- 名牌、世界名稱是否認得台服，以及 Lodestone／NetStone 查詢，都還沒在台服用戶端核對過。程式沒有寫死排除世界 ID 4028–4035；世界表會不會收下台服世界，取決於台服 `World` 表裡的名稱、資料中心與區域，需要進遊戲確認。
- 授權是上游的 MIT。Copyright (c) 2025 Infi, kalilistic。

## 自行編譯

`Dalamud.NET.Sdk` 13.1.0 不會附帶 Dalamud，而是對本機的 `Dalamud.dll` 編譯。沒有設定 `DALAMUD_HOME` 時，SDK 會去 `%AppData%\XIVLauncher\addon\Hooks\dev\`（Linux 則是 `~/.xlcore/dalamud/Hooks/dev/`）。XIVTCLauncher 的檔案在 `%AppData%\FFXIVSimpleLauncher\Dalamud\`，含有 `Dalamud.dll` 的是 `Injector`。

1. 安裝 .NET 9 SDK。`global.json` 指定 `9.0.100`，並在 9.0 功能帶內向前相容（對應 Dalamud .NET 9）。
2. 把 `DALAMUD_HOME` 指到 yanmucorp Dalamud `13.0.0.16` 裡含有 `Dalamud.dll` 的目錄（[發行檔](https://github.com/yanmucorp/Dalamud/releases) 的 `latest.7z`，或啟動器已下載的 `Injector`）。
3. 在這個目錄執行 `dotnet build -c Release`。

在 Linux 或 macOS 上另外加上 `-p:EnableWindowsTargeting=true`。專案目標是 `net9.0-windows7.0`。Release 組建會由 DalamudPackager 在輸出目錄產生 `PlayerTrack/latest.zip`。

## 使用的程式庫

- [AutoMapper](https://github.com/AutoMapper/AutoMapper)
- [Dapper](https://github.com/DapperLib/Dapper)
- [FlexConfig](https://github.com/kalilistic/FlexConfig)
- [FluentDapperLite](https://github.com/kalilistic/FluentDapperLite)
- [FluentMigrator](https://github.com/fluentmigrator/fluentmigrator)
- [NetStone](https://github.com/karashiiro/NetStone)
- [SQLite](https://github.com/sqlite/sqlite)

## English

Fork of [Infiziert90/PlayerTrack](https://github.com/Infiziert90/PlayerTrack) by Infi and kalilistic, retargeted to yanmucorp Dalamud API 13 / .NET 9 for the Traditional Chinese client and XIVTCLauncher. Do not install this on official Dalamud API 14 or 15.

Download [PlayerTrack-api13-tw-3.6.1.1.zip](https://github.com/pollyhaei-ai/PlayerTrack/releases/download/api13-tw-3.6.1.1/PlayerTrack-api13-tw-3.6.1.1.zip) and extract it so `PlayerTrack.dll` and `PlayerTrack.json` sit in `%AppData%\FFXIVSimpleLauncher\Dalamud\Config\devPlugins\PlayerTrack\` (or `Profiles\<profile ID>\Dalamud\devPlugins\PlayerTrack\` when the account uses its own profile). Enable it in `/xldev`. `/ptrack` opens the main window and `/ptrackconfig` opens settings.

Nameplates, whether Taiwan worlds are recognized, and Lodestone/NetStone lookups still need in-game checks on the Taiwan client. The world filter does not hard-code an exclusion of IDs 4028–4035. Upstream is MIT.
