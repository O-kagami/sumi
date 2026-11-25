# Sumi

**macOS標準の日本語入力に近い操作感を目指す、Windows向け日本語IME。**

Sumiは [Mozkey](https://github.com/koyasi777/mozkey) を基盤とする独立開発プロジェクトです。Mozkeyの上流は [Mozc](https://github.com/google/mozc) です。Apple・Google・Mozkeyの公式製品ではありません。

**現在は設計段階です。** Sumiとしての実装・ビルド・配布はまだ行っていません。

## 開発方針

- macOS標準日本語入力を参照し、ライブ変換・キー操作・候補表示・文節編集・確定／取消を実機比較で再現。
- 通常入力中は余計な候補や補助UIを出さない基準プロファイル。候補表示はMacの挙動に合わせる。
- 初版からWinUI 3の設定アプリ（C++/WinRTを第一候補）を採用し、辞書・キー設定まで完結。
- MozkeyのC++変換エンジンとTSF接続を活用。Windows 11 ARM64/x64、軽量動作を重視し、Rustは同条件で計測して効果がある部品に採用。
- Microsoft Store掲載を目標に署名・インストール・ライセンスを検証。

## 開発資料

[設計資料の目次](docs/windows-live-ime/README.md) · [実装方針](docs/windows-live-ime/implementation-plan.md) · [Mac入力互換仕様](docs/windows-live-ime/macos-input-compatibility.md) · [WinUI 3](docs/windows-live-ime/winui3-settings.md) · [省メモリ・Rust](docs/windows-live-ime/performance-and-rust.md) · [ロードマップ](docs/windows-live-ime/roadmap.md) · [ライセンス方針](docs/windows-live-ime/licensing.md)

## ライセンス・公開範囲

このリポジトリはMozkeyの正式なPublic Forkです。上流由来コード・データは元の[LICENSE](LICENSE)および[第三者通知](THIRD_PARTY_NOTICES.md)に従います。これらの権利は変更しません。

Sumiの独自実装は原則として独立したPrivateリポジトリで管理し、可能な範囲で独自ライセンスとします（Private開発先は未作成）。[Sumi独自部分の権利表示](LICENSE-SUMI.md)は既存のOSSライセンスやGitHub利用規約を上書きしません。このPublic Forkに秘密のコードをコミットしないでください。

## 上流資料

移行前のMozkeyのREADMEは [README-MOZKEY.md](README-MOZKEY.md) に内容を変更せず保存しています。そこに記載される機能・インストーラー・リリースは上流Mozkeyのものであり、Sumiのリリースではありません。
