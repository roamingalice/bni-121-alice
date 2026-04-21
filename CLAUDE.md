# bni-121-alice — Claude Code 指令

Alice 的 BNI 華榮 121 個人頁。定位：**AI 商業流程架構師**。

## 月度 PR 更新系統（Phase 2 簡化版）

每月 1 號 9:00 會自動建 PR。整個系統分工：
- **run.sh**（Alice Mac 的 launchd）→ 掃 + 建 PR + 丟 JSON 到 Mac Mini
- **MiniMe**（Mac Mini）→ heartbeat 通知 Alice + 收到「OK」時 merge
- **你我（Claude Code）** → Alice 要改 PR 內容時由我處理

## 當 Alice 說「改那個 121 PR」「改月度 PR」「121 PR 幫我改 XX」時

**步驟：**

1. **ssh 讀 Mac Mini 的 pending JSON，或看是否已 archive：**
   ```bash
   ssh s@100.100.44.43 'cat ~/.openclaw/workspace-alice/memory/bni-121-pending.json 2>/dev/null || cat ~/.openclaw/workspace-alice/memory/archive/bni-121-$(date +%Y%m).json 2>/dev/null'
   ```
2. 拿到 JSON 後讀 `prs[].url`（通常 1-2 個 PR）
3. 問 Alice 具體要改什麼（如果她還沒說清楚）
4. 對每個相關 PR：
   ```bash
   gh pr checkout <url>
   # 改 HTML（用 Edit 工具，最小必要改動）
   git add -A && git commit -m "按 Alice 指示修改：{summary}"
   git push
   ```
5. 回報：「已改完並 push，PR 更新了。你 review 後可以 merge（或叫 MiniMe 幫你 merge）」

## 核心定位（不要改，除非 Alice 說）

- 專業別：AI 商業流程架構師
- 強烈願望、GAINS、三層引薦、九宮格等結構是 Alice 本人定版，**月度更新不要動這些**
- 月度更新只能加新成就到 GAINS 的 Accomplishments 列表最上面，或加新案例到 AI landing 的 project grid

## 部署資訊

- GitHub: `roamingalice/bni-121-alice`
- Live: https://roamingalice.github.io/bni-121-alice/
- 月度更新腳本：`~/scripts/bni-121-monthly/run.sh`（launchd 每月 1 號 9:00）
- MiniMe workspace on Mac Mini: `/Users/s/.openclaw/workspace-alice/`
