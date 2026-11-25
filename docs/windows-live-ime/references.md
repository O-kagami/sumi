# 調査資料

参照日：2026-11-24。一次資料を優先する。上流コードの確認済みコミットは`0eaeef17e37a576301cba759e7a1c5419f77c42d`（2026-11-23）。

文書内の設計案と、現在のコードに存在する機能を区別する。Macの細かな動作は資料だけで確定せず、参照実機の記録を追加する。

## Upstream

| ID | 資料 | 主な確認対象 |
| --- | --- | --- |
| U1 | [Mozkey](https://github.com/koyasi777/mozkey) | 全体の構成と機能 |
| U2 | [config.proto](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/protocol/config.proto) | ライブ変換・予測・外観の設定 |
| U3 | [config_handler.cc](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/config/config_handler.cc) | 初期値・移行・保存 |
| U4 | [session.cc](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/session/session.cc) | ライブ変換・候補・キー処理 |
| U5 | [text_renderer.cc](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/renderer/win32/text_renderer.cc) | DirectWrite/Direct2DとGDI |
| U6 | [tip_ui_handler_conventional.cc](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/win32/tip/tip_ui_handler_conventional.cc) | 外部／アプリ内レンダラー分岐 |
| U7 | [config_dialog.cc](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/gui/config_dialog/config_dialog.cc) | Qt設定UIと移植元 |
| U8 | [zenz_scorer/main.cc](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/zenz_scorer/main.cc) | AI起動・キャッシュ・待機 |
| U9 | [installer_oss_64bit.wxs](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/win32/installer/installer_oss_64bit.wxs) | サービス、配布構成 |
| U10 | [client_interface.h](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/client/client_interface.h) | GetConfig/SetConfig/Reload/SyncData |
| U11 | [client.cc](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/client/client.cc) | IPC接続 |
| U12 | [user_dictionary_storage.h](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/dictionary/user_dictionary_storage.h) | 辞書ロック・保存 |
| U13 | [TIP BUILD](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/src/win32/tip/BUILD.bazel) | 複数アーキテクチャ |
| U14 | [LICENSE](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/LICENSE) | 本体と辞書の条件 |
| U15 | [THIRD_PARTY_NOTICES](https://github.com/koyasi777/mozkey/blob/0eaeef17e37a576301cba759e7a1c5419f77c42d/THIRD_PARTY_NOTICES.md) | 第三者部品 |
| U16 | [辞書通知](https://github.com/koyasi777/mozkey/blob/main/src/data/installer/DICTIONARY_NOTICES.md) | 出典別の条件・配布前の確認 |
| U17 | [署名方針](https://github.com/koyasi777/mozkey/blob/main/CODE_SIGNING_POLICY.md) | 未署名の現状と計画 |

mainリンクの通知類は、出荷する版に固定して再確認する。

## Apple

| ID | 公式資料 |
| --- | --- |
| A1 | [日本語入力とライブ変換](https://support.apple.com/ja-jp/guide/japanese-input-method/jpim10265/6.3/mac/26) |
| A2 | [日本語入力ソースの設定](https://support.apple.com/en-ke/guide/japanese-input-method/jpim662a12b9/mac) |
| A3 | [候補ウィンドウ](https://support.apple.com/en-gb/guide/japanese-input-method/jpim10262/6.3/mac/27) |
| A4 | [日本語変換ショートカット](https://support.apple.com/ja-jp/guide/japanese-input-method/jpim10263/6.3/mac/26) |
| A5 | [再変換](https://support.apple.com/en-ae/guide/japanese-input-method/jpim10309/mac) |
| A6 | [日本語入力モード](https://support.apple.com/en-ca/guide/japanese-input-method/jpimf6ffb247/6.3/mac/27) |
| A7 | [文字・文節の変更](https://support.apple.com/en-md/guide/japanese-input-method/jpim10231/mac) |

地域・OS版の異なる公式ページが含まれる。細かな差を推測で埋めず、基準Macの版を決めてから対応するガイドと実測を照合する。調査時、一部の直接取得は429となり、検索サービスが返したApple公式本文も参照した。

## Microsoft

| ID | 公式資料 |
| --- | --- |
| M1 | [C++/WinRT](https://learn.microsoft.com/en-us/windows/apps/develop/cpp-winrt/intro-to-using-cpp-with-winrt) |
| M2 | [Unpackaged WinUI 3](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/unpackage-winui-app) |
| M3 | [Windows App SDK self-contained](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/self-contained-deploy/deploy-self-contained-apps) |
| M4 | [IME要件](https://learn.microsoft.com/en-us/windows/apps/develop/input/input-method-editor-requirements) |
| M5 | [MSI/EXE提出要件](https://learn.microsoft.com/en-us/windows/apps/publish/publish-your-app/msi/app-package-requirements) |
| M6 | [Storeポリシー](https://learn.microsoft.com/en-us/windows/apps/publish/store-policies) |
| M7 | [MSIX準備時の制約](https://learn.microsoft.com/en-us/windows/msix/desktop/desktop-to-uwp-prepare) |

Store関連では特にサービス依存、全PE署名、オフライン・サイレント導入を確認する。Store公開の可否は未確定で、通常のWinUIアプリの配布条件だけからIMEの認証を保証しない。

## Performance

| ID | 一次資料 |
| --- | --- |
| R1 | [Rustの所有権](https://doc.rust-lang.org/stable/book/ch04-01-what-is-ownership.html) |
| R2 | [VMMap](https://learn.microsoft.com/en-us/sysinternals/downloads/vmmap) |
| R3 | [Working Set](https://learn.microsoft.com/en-us/windows/win32/memory/working-set) |
| R4 | [Windows Performance Recorder](https://learn.microsoft.com/en-us/windows-hardware/test/wpt/windows-performance-recorder) |

## 調査の限界

Windows実行・ビルド、ARM64 Windows実機のメモリ測定、Macのキー操作記録、Storeへの問い合わせはまだ行っていない。実装済み・検証済みという意味の資料ではない。

## Licensing / repository visibility

| ID | 一次資料 | 確認対象 |
| --- | --- | --- |
| L1 | [Sumiの上流LICENSE](../../LICENSE) | BSD系条件と辞書固有条件（保持） |
| L2 | [第三者通知](../../THIRD_PARTY_NOTICES.md) | 辞書・モデル・ランタイムの個別条件 |
| L3 | [GitHub Forks](https://docs.github.com/en/pull-requests/reference/forks) | Public Forkの公開範囲、ネットワーク間のGitデータ共有 |
| L4 | [GitHub Terms of Service §D](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service#d-user-generated-content) | 公開コンテンツの閲覧・Fork等の許諾、リポジトリライセンスによる投稿の扱い |
| L5 | [BSD 3-Clause](https://opensource.org/license/bsd-3-clause) | ソース／バイナリ再配布、通知の維持、推奨・承認の表示 |
| L6 | [Qt GPL/LGPL obligations](https://www.qt.io/development/open-source-lgpl-obligations) | クローズド配布におけるQtの条件 |
| L7 | [Windows Zenzランタイム通知](../../src/win32/installer/zenz_runtime/licenses/THIRD_PARTY_NOTICES.md) | モデルApache-2.0、llama.cpp MIT（同梱版の記録） |
| L8 | [辞書の配布通知](../../src/data/installer/DICTIONARY_NOTICES.md) | 混在する出典・データの配布可否の確認 |

L1〜L8の確認日：2026-11-25。リリース時は実際に出荷するバージョンの原文と依存一覧を確認する。非公開開発先の作成、最終的な配布ライセンス監査は未実施。
