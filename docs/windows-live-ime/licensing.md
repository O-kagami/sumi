# ライセンス・非公開開発方針

更新：2026-11-25  
状態：開発・配布方針を定義。法的な最終審査、依存関係の全件監査、Private開発先の作成は未実施。

## 1. 方針

SumiはMozkey（さらに上流はMozc）の派生製品として、**既存の権利を侵害せず、Sumi独自実装を可能な限りクローズドソースにする**。

- 上流のLICENSE、各ファイルの著作権・免責、AUTHORS、CONTRIBUTORS、辞書・モデル等の通知をそのまま保持する。
- BSD 3-Clauseは、条件を満たすソース／バイナリ再配布と商用利用を許容し、通常は独自改変のソース公開を要求しない。ただし第三者部品の個別条件は別である。
- 独自部分には[LICENSE-SUMI.md](../../LICENSE-SUMI.md)の権利表示を適用する。保護対象は実際に権利を持つ新規の表現・実装のみ。上流由来の部分まで独占しない。AI生成物等に権利が成立するかは別途確認する。
- 既存の許諾は遡及的に取り消さない。第三者の権利、法定の利用、GitHub利用規約に反する制限を加えない。

## 2. 公開Forkと非公開コードの分離

| 管理先 | 公開範囲 | 内容 |
| --- | --- | --- |
| O-kagami/sumi | Public（現在の正式Fork） | Mozkey由来の基盤、設計文書、公開承認済み変更 |
| 独立Privateリポジトリ（仮称 sumi-private、未作成） | Private | 独自のWinUI 3・操作互換・描画・性能改善・非公開テストと配布準備 |
| リリース配布先 | バイナリを配布する場合のみ公開 | 監査済みMSI/EXE、必要なOSSライセンス・通知・ソース提供等 |

Public Forkの公開範囲は上流ネットワークに連動するため、単独でPrivateへ変更できない。GitHubの規約により公開内容には閲覧・サービス内Forkなどの権利があり、ライセンス付きリポジトリへの投稿にも既定のライセンス条件が関係する。公開済みの内容を「All rights reserved」と記すだけで完全に制限できると扱わない。

Private側はGitHubの正式Forkではなく独立したリポジトリとして作り、公開側のコードと履歴を取り込む。公開側へのpush先を確認し、秘密のコミット・ブランチ・PR・CIログ・成果物を公開側に送らない。上流同期は原則fetch/mergeでPrivate側へ取り込み、Privateの履歴を公開Forkへmergeしない。公開する変更だけを選別・ライセンス確認する。秘密鍵・トークン・実際の入力履歴はどちらにもコミットしない。

## 3. 部品別の管理

| 部品 | 現時点の根拠 | 方針 |
| --- | --- | --- |
| Mozc/Mozkeyのコード | 上流LICENSE、各ファイルの通知 | BSD系の適用範囲を保持。改変バイナリにも必要な通知を添付 |
| Mozc基本辞書 | 上流LICENSEと辞書通知に記載されるNAIST/ICOT等の混在条件 | 出典・条件・免責を確認して保持 |
| 追加辞書 daily | merge-utの混在条件、Wikipedia由来コスト、Sudachi由来、Nico/pixiv由来等 | 各出典を個別監査。CC BY-SA等が適用される成果物はその条件に従う。権利不明・互換性未確認の材料は出荷前に除外または許諾取得 |
| Zenz v3.2 small GGUF | 現行Windows同梱通知ではApache-2.0 | 正確な出荷モデル・出典・NOTICE・変更表示等を確認 |
| llama.cpp / ggml | 現行同梱通知ではMIT | ライセンス・著作権表示を同梱、実際のビルド依存も確認 |
| Qt | モジュールによりLGPL/GPL/商用等 | WinUI 3移行で出荷物から除去を目標。残す場合は該当条件を満たすか商用許諾を取得 |
| Windows App SDK / WinUI 3 / VC++ runtime | 実際の利用バージョンのライセンス・再配布条件 | 許可された同梱方法と通知を確認 |
| 新規Rust依存 | crateごとのライセンス | BSD/MIT/Apache-2.0等の許容的な依存を優先。コピーレフトや不明な条件は導入前にレビュー |
| Sumi独自のコード・デザイン・アイコン | 実際の権利保有・新規作成を確認 | Private管理・独自ライセンス。AppleやMozkeyの商標・素材を無断で自社のものとして扱わない |

ライセンス名は現行の通知で確認した範囲であり、依存の全件監査が済んだ意味ではない。GPL等の義務が生じる構成を無条件で禁止するのではなく、クローズド配布と両立する代替品を優先し、必要な権利と義務を満たせない場合は配布しない。

辞書については、Wikipedia由来データの使用が生成辞書全体に継承義務を生じさせるかは未確定。Nico/pixiv由来データは生成者が著作権を主張しないことだけでは第三者の許諾にならない。上流の注意を引き継ぐ。辞書を除外する場合は変換品質を比較し、精度低下を隠さない。

## 4. 実装・リリース時の必須事項

1. 実装前に独立Privateリポジトリのアクセス・remote・上流同期方針を確認する。
2. 新規依存、モデル、フォント、画像、辞書データの導入時に出典、固定版、ライセンス、再配布条件、変更の有無を記録する。
3. 出荷バイナリ・DLL・モデル・辞書・配布データのSBOM／ライセンス一覧を生成し、実際のMSI内容と照合する。
4. 上流LICENSE、必要な個別LICENSE/NOTICE、帰属、免責、該当するソース提供や再リンク手段を配布物に同梱または条件どおり提供する。Web上へのリンクだけで足りるとは仮定しない。
5. Sumiの利用条件は独自部分とOSS部分の範囲を明示し、OSSが認める権利を制限しない。EULAは配布前にレビューする。
6. WinUI 3化によるQt依存の除去、サービス依存、署名、Store要件、配布用名称を確認する。
7. 出荷可否が不明な部品・データを残した状態で一般配布しない。

## 5. 参照と現状

- [上流LICENSE](../../LICENSE)
- [THIRD_PARTY_NOTICES](../../THIRD_PARTY_NOTICES.md)
- [辞書の配布通知](../../src/data/installer/DICTIONARY_NOTICES.md)
- [Windows Zenz通知](../../src/win32/installer/zenz_runtime/licenses/THIRD_PARTY_NOTICES.md)
- [GitHub Forks](https://docs.github.com/en/pull-requests/reference/forks)
- [GitHub Terms of Service §D](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service#d-user-generated-content)
- [BSD 3-Clause](https://opensource.org/license/bsd-3-clause)
- [Qt GPL/LGPL obligations](https://www.qt.io/development/open-source-lgpl-obligations)

最終配布ライセンスや商用利用可否は、実際に含まれるコード・データ・モデルについて確認してから決める。本資料は開発方針であって、最終的な法律意見・配布許諾ではない。
