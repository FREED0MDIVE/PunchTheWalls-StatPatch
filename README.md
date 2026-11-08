# Punch The Walls - Stat Patch

A small mod that boosts the player's upgrade stats in **Punch The Walls** (Steam, PC).

| Stat | Multiplier vs stock |
|---|---|
| Punch damage | x5 |
| Punch speed | x5 |
| Vacuum range | x15 |
| Trash bin capacity | x15 |
| Suction flow cap | x15 |
| Punch area (blocks) | x2 (kept low on purpose - high area values cause physics lag) |

Tested on Steam game version **1.0.1** (works on both rule editions the game
now ships with - the patch boosts both branches). Single-player and hosting
co-op (the stats are computed on the host).

v1.1 note: update 1.0.1 reworked the stat formulas and nerfed stock values
(about 1/5 of the old edition). The multipliers above are unchanged, so patched
numbers are lower in absolute terms than in v1.0 - that simply matches the new stock.

## Install

1. Close the game.
2. Unzip anywhere (e.g. your Desktop - not inside the game folder).
3. Double-click **install.bat**. It finds your Steam library automatically,
   backs up the original DLL to `Assembly-CSharp.dll.orig`, and patches it.
   Safe to run more than once (e.g. after a game update, just run it again).

If your game is not in a standard Steam library, run this instead:

```
powershell -ExecutionPolicy Bypass -File install.ps1 -GamePath "D:\SteamLibrary\steamapps\common\Punch The Walls"
```

## Uninstall

Double-click **restore.bat**. A Steam "verify integrity of game files" also restores the stock DLL.

## How it works

`PtwStatPatcher.exe` edits the game's IL code in memory and rewrites
`Assembly-CSharp.dll` in place (via dnlib, MIT licensed). It changes only the
stat formulas in `PunchForEscape.Progress` and the suction flow clamp in
`PunchForEscape.Vacuum` - no game assets, no other DLLs.
Source of the patcher: ask the author / see the repository where you got this.

If the patcher prints unexpected values after a game update, the stock
constants may have changed - wait for an update or report it to the author.

## Requirements

Windows x64 with .NET Framework 4.x (preinstalled on Windows 10/11) and
PowerShell (preinstalled). No admin rights needed if your game library is on a
drive you can write to (standard case).

---

# 한국어 안내

**펀치 더 월즈(Punch The Walls)** 플레이어 능력치 modifications:
펀치 피해 ×5, 펀치 속도 ×5, 흡입 범위 ×15, 쓰레기통 용량 ×15, 흡입 속도 상한 ×15,
펀치 범위 ×2 (래그 방지를 위해 의도적으로 낮춤).
**1.0.1 테스트 완료** — 게임이 새로 도입한 두 룰 에디션(V1/V2) 모두에 동일 배율 적용.
1.0.1에서 스톡 수치가 이전 에디션 대비 약 1/5로 너프되어, 패치 후 절대 수치가
v1.0 때보다 낮아 보입니다(배율은 동일).

**설치**: 게임을 종료하고 `install.bat`을 더블클릭하면 끝.
원본 DLL은 `Assembly-CSharp.dll.orig`로 자동 백업됩니다.
게임이 업데이트되면 `install.bat`을 다시 실행하세요 (중복 실행 안전).

**삭제(원복)**: `restore.bat`을 더블클릭. 스팀의 "게임 파일 무결성 검증"으로도 복원됩니다.

주의: 이 도구는 게임 파일을 배포하지 않으며, 설치된 게임의 코드 상수만 수정합니다.
코옵 호스트의 능력치가 참여자에게도 적용됩니다.
