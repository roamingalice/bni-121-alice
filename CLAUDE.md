# bni-121-alice — Claude Code 指令

Alice 的 BNI 華榮 121 個人頁。定位：**AI 商業流程架構師**。

## Session Startup Check（重要）

每次 session 開始（Alice 在此 repo 工作時），**先跑一次 pending check**：

```bash
ssh s@100.100.44.43 'cat ~/.openclaw/workspace-alice/memory/bni-121-pending.json 2>/dev/null'
```

解析 JSON：

- 空的 / 檔案不存在 → 正常開始，什麼都不說
- `status == "merged"` → 應該已 archive，正常開始
- `status == "waiting_review"` → 還在等 Alice 回 MiniMe，不用我們處理，正常開始
- `status == "pending_cc_changes"` → **有待處理的月度修改**，主動告訴 Alice：
  - 「MiniMe 轉來一筆月度更新修改：『{change_request}』，要現在處理嗎？」
  - Alice 說要 → 讀 PR URL（`prs[]`），checkout 分支，執行修改，push，更新 JSON 為 `cc_done`
  - Alice 說等等 → 不動 JSON，下次開啟再問

## 處理 pending_cc_changes 的完整流程

1. ssh 讀完整 JSON，拿到 PR URLs 和 change_request
2. 對每個 PR：`gh pr checkout <url>`
3. 按 change_request 的指示改 HTML（保持現有結構，最小必要修改）
4. `git add` + `git commit -m "按 Alice 指示修改：{summary}"`
5. `git push`
6. `ssh s@100.100.44.43 'python3 - <<"EOF" ... EOF'` 更新 JSON：
   - status 改為 `cc_done`
   - 加 `cc_done_at` 時間戳
   - 加 `cc_commit_sha`（方便回溯）
7. 最後 move JSON 到 archive：`ssh s@100.100.44.43 'mv ~/.openclaw/workspace-alice/memory/bni-121-pending.json ~/.openclaw/workspace-alice/memory/archive/bni-121-{month}.json'`
8. 跟 Alice 說：「已改完並 push，PR 更新了。你 review 後可以 merge」

## 部署資訊

- GitHub: `roamingalice/bni-121-alice`
- Live: https://roamingalice.github.io/bni-121-alice/
- 月度更新腳本：`~/scripts/bni-121-monthly/run.sh`（launchd 每月 1 號 9:00 自動跑）
- Phase 2 整合：MiniMe 在 Mac Mini 負責 Telegram 通知 + merge，Claude Code 處理修改

## 核心定位（不要改，除非 Alice 說）

- 專業別：AI 商業流程架構師（不是 AI 落地師、不是顧問）
- 強烈願望、GAINS、三層引薦、九宮格等結構是 Alice 本人定版的，**月度更新不要動這些**
- 月度更新只能加新成就到 GAINS 的 Accomplishments 列表最上面，或加新案例到 AI landing 的 project grid
