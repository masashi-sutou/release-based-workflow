## release-drafterとは

- https://github.com/release-drafter/release-drafter のREADME.mdを参照
- OSSのように、どのバージョンでどのPRがどのような修正で行われたのか履歴を追いやすくわかりやすい

## リリースドラフトの作成フロー

```mermaid
sequenceDiagram
actor 開発者
開発者 -->> 開発者: ブランチ作成（例： feat/new_feature や fix/bug）
開発者 -->> GitHub: PRをmainに向けて作成
GitHub -->>+ release-drafter: PRをmainに向けたら、GitHub Actionsが起動
release-drafter -->>- GitHub: ブランチ名で判定して「feature」や「bug」のラベルがPRに付く
GitHub -->> GitHub: レビューしてmainにマージ
GitHub -->> release-drafter: PRをmainにマージしたら、GitHub Actionsが起動

alt リリースドラフトがある
	release-drafter -->> GitHub: ラベルをもとにリリースドラフトへ追記
else ない
	release-drafter -->> GitHub: 最新タグのバージョンをパッチ更新してリリースドラフト作成してドラフトへ追記
end

開発者 -->> GitHub: 手動でGitHub Actionsを起動してデプロイ
開発者 -->> GitHub: リリースドラフトを公開してタグを作成
```

## 参考

- https://github.com/masashi-sutou/release-based-workflow/releases