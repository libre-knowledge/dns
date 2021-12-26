# 《自由知識協作平台》主題範本

快速創建風格一致的《自由知識協作平台》主題

![「檢查專案中的潛在問題」GitHub Actions 作業流程狀態標章](https://github.com/libre-knowledge/subject-template/actions/workflows/check-potential-problems.yml/badge.svg "本專案使用 GitHub Actions 自動化檢查專案中的潛在問題") [![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white "本專案使用 pre-commit 檢查專案中的潛在問題")](https://github.com/pre-commit/pre-commit) [![REUSE 規範遵從狀態標章](https://api.reuse.software/badge/github.com/libre-knowledge/subject-template "本專案遵從 REUSE 規範降低軟體授權合規成本")](https://api.reuse.software/info/github.com/libre-knowledge/subject-template)

## 使用說明

1. 點擊 [GitHub 專案頁面](https://github.com/libre-knowledge/subject-template)右上角的[「使用這個範本(Use this template)」綠色按鈕](https://github.com/libre-knowledge/subject-template/generate)
1. 遵循網頁提示建立新的專案
1. 編輯 [real.README.md 主題說明文件模板](real.README.md)，將 `_佔位字_` 替換為適當之內容（別忘了替換 `libre-knowledge/_專案ID_`），並移除未使用之（待補）章節
1. 用 [real.markdownlint.yml Markdownlint 配置文件](real.markdownlint.yml) 替換掉 [.markdownlint.yml 本專案專屬的 Markdownlint 配置文件](.markdownlint.yml)
1. 替換 [.reuse/dep5 REUSE DEP5 機器可讀著作權宣告文件](.reuse/dep5) 文件中的 `Upstream-Name`（替換為 _主題名稱_）欄位、 `Upstream-Contact`（替換為該主題專案議題追蹤系統的網頁標題與網址）欄位跟 `Source`（替換為專案網址）欄位
1. 將 [real.README.md 主題說明文件模板](real.README.md) 替換掉 [README.md 本專案說明文件](README.md)
1. 將變更提交為新修訂版（參考提交標題： `docs: 撰寫主題說明文件雛型`）
1. （如果是將專案版控庫復刻(clone)到本地）將本地變更推送到遠端版控庫）

## 參考資料

* [Machine-readable debian/copyright file](https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/)
* [Tutorial: How to become REUSE-compliant \| REUSE](https://reuse.software/tutorial/)
