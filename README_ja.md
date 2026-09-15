# Relaypublisher の Homebrew tap

この tap は、winget 風の YAML manifest を Microsoft Intune の LOB アプリとして公開する CLI `relaypublisher` を、
Apple silicon の macOS 向けに配布します。

formula は `kkamegawa/Relaypublisher` の各 GitHub release に添付された self-contained な `osx-arm64` single-file app を
インストールします。このリポジトリでは何もビルドしません。formula は release の `SHA256SUMS.txt` に記録された
sha256 でその archive を固定しており、.NET SDK は不要です。

正式なドキュメントは英語版の [README.md](README.md) です。

## Install

Homebrew 6.0 以降は、明示的に trust していない第三者 tap を読み込みません。最初に一度この tap を追加して trust します:

```bash
brew tap kkamegawa/tap
brew trust --tap kkamegawa/tap
brew install relaypublisher
```

## 更新・pin・削除

```bash
brew upgrade relaypublisher
brew pin relaypublisher
brew uninstall relaypublisher
```

## 対応プラットフォーム

- Apple silicon の macOS のみです。Intel Mac では formula のインストールが拒否されます。Intel Mac と Linux では
  `dotnet tool install --global relaypublisher` で NuGet global tool を入れてください。
- stable release のみです。prerelease は NuGet package としてのみ公開します。
- tap は最新 version だけを持ちます。rollback は NuGet global tool の `--version` で行ってください。
- formula と NuGet global tool を両方入れないでください。`PATH` で先に見つかった方が使われます。

## formula の更新方法

Relaypublisher の stable release が公開されると、その release workflow がこのリポジトリに version と sha256 を
更新する pull request を作ります。`brew test-bot` workflow が Apple silicon の runner で formula をインストールし、
`codesign --verify --strict` で ad-hoc 署名を検証し、`relaypublisher --version` を実行します。この check が通った後に
pull request を手動でマージします。

`Formula/relaypublisher.rb` は Relaypublisher リポジトリの `tools/New-HomebrewFormula.ps1` が生成します。手で編集しないでください。

## License

MIT License。詳細は [LICENSE](LICENSE) を参照してください。
