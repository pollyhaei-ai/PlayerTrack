# PlayerTrack（台服 / Dalamud API 13）

台灣版《最終幻想XIV》用的 [Infiziert90/PlayerTrack](https://github.com/Infiziert90/PlayerTrack)（作者 Infi、kalilistic）。這個分支給 [cycleapple/XIVTCLauncher](https://github.com/cycleapple/XIVTCLauncher) 搭配 [yanmucorp/Dalamud](https://github.com/yanmucorp/Dalamud) **API 13 / .NET 9**。

它記錄遇見的玩家和一起打過的內容，可以分類、寫筆記，並在改名或換伺服器之後繼續追蹤。

**不要裝到官方 Dalamud API 14／15**（國際服 XIVLauncher）。這個組建只給台服。

## 下載

請用 **3.6.1.2**，不要用 3.6.1.1。

- 發行頁：https://github.com/pollyhaei-ai/PlayerTrack/releases/tag/api13-tw-3.6.1.2
- 壓縮檔：[PlayerTrack-api13-tw-3.6.1.2.zip](https://github.com/pollyhaei-ai/PlayerTrack/releases/download/api13-tw-3.6.1.2/PlayerTrack-api13-tw-3.6.1.2.zip)

3.6.1.1 在台服載入時會失敗：Dalamud 的文字清理器不接受 `TraditionalChinese`，插件在讀世界名稱時就中斷。3.6.1.2 改回傳原本的世界與資料中心名稱，並已在台服進遊戲載入。

## 安裝

1. 在 XIVTCLauncher 啟用 Dalamud，進過一次遊戲讓資料夾出現，然後**關閉遊戲**。
2. 下載上面的 zip。裡面是一個 `PlayerTrack` 資料夾，含 `PlayerTrack.dll`、`PlayerTrack.json`，以及一起載入的 NuGet 組件。
3. 把這個資料夾放到下面的路徑，`dll` 和 `json` 要在同一層，不要再多包一層 `PlayerTrack`：

```text
%AppData%\FFXIVSimpleLauncher\Dalamud\Config\devPlugins\PlayerTrack\
```

帳號如果用自己的插件設定檔，改放：

```text
%AppData%\FFXIVSimpleLauncher\Profiles\<設定檔 ID>\Dalamud\devPlugins\PlayerTrack\
```

4. 進遊戲後用 `/xldev` 啟用 PlayerTrack。同一個視窗可以重新載入。

`/ptrack` 開啟主視窗。`/ptrackconfig` 開啟設定。

## 使用前請先看

- 名牌，以及 Lodestone／NetStone 查詢，還沒在台服逐項核對。載入成功不代表這兩項已經在台服確認過。
- 上游是 [Infiziert90/PlayerTrack](https://github.com/Infiziert90/PlayerTrack)，作者 Infi、kalilistic。授權是本倉庫的 [MIT](LICENSE)。Copyright (c) 2025 Infi, kalilistic。

## 自行編譯

`Dalamud.NET.Sdk` 13.1.0 對本機的 `Dalamud.dll` 編譯。把 `DALAMUD_HOME` 指到 yanmucorp Dalamud `13.0.0.16` 裡含有 `Dalamud.dll` 的目錄（[發行檔](https://github.com/yanmucorp/Dalamud/releases) 的 `latest.7z`，或 XIVTCLauncher 的 `Injector`）。沒有設定時，SDK 會去官方啟動器的 `%AppData%\XIVLauncher\addon\Hooks\dev\`。

1. 安裝 .NET 9 SDK。`global.json` 指定 `9.0.100`，並在 9.0 功能帶內向前相容。
2. 在這個目錄執行 `dotnet build -c Release`。Linux 或 macOS 加上 `-p:EnableWindowsTargeting=true`。

專案目標是 `net9.0-windows7.0`。

## English

Fork of [Infiziert90/PlayerTrack](https://github.com/Infiziert90/PlayerTrack) by Infi and kalilistic, for the Traditional Chinese client: yanmucorp Dalamud API 13 / .NET 9 and XIVTCLauncher. Do not install this on official Dalamud API 14 or 15.

Download [PlayerTrack-api13-tw-3.6.1.2.zip](https://github.com/pollyhaei-ai/PlayerTrack/releases/download/api13-tw-3.6.1.2/PlayerTrack-api13-tw-3.6.1.2.zip). Do not use 3.6.1.1; it crashes on load because the sanitizer rejects `TraditionalChinese`. 3.6.1.2 returns the original world and datacenter names and has loaded in-game.

Put `PlayerTrack.dll` and `PlayerTrack.json` in `%AppData%\FFXIVSimpleLauncher\Dalamud\Config\devPlugins\PlayerTrack\` (or `Profiles\<profile ID>\Dalamud\devPlugins\PlayerTrack\` for a per-account plugin profile). Enable it in `/xldev`. `/ptrack` opens the main window and `/ptrackconfig` opens settings.

Nameplates and Lodestone/NetStone still need in-game checks on the Taiwan client. Upstream is MIT.
