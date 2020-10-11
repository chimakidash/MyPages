# Systemd Error Messages

DNSサーバを構築している際に発生するエラーメッセージとその対応

## DNSサーバ起動時に発生するエラー

### journalctl -u named

```
dns_rdata_fromtext: hoge.zone:x: near eol: unexpected end of input
```

想定される問題: ゾーンファイル「hoge.zone」のx行目に不正な改行や空白が存在する際に発生する。

> SOAレコードに改行が存在している(SOAレコードは改行不可)
> hoge.zone の先頭行がTTLではない
> 先頭行が空白で始まる


```
hoge.zone:x: SOA record not at top of zone (hogehoge.zone.hogehoge.zone)
```

想定される問題: ゾーンファイル「hoge.zone」のSOAレコードのroot domain指定が漏れている

> hoge.zone のSOAレコードにおいて、「hogehoge.zone.」 の最終.(ドット)が抜けている

```
dns_rdata_fromtext: hoge.zone:x: near 'hogehoge.zone.': not a valid number
```

想定される問題: ゾーンファイル「hoge.zone」のx行目に存在するレコードの書式が正しくない

> MXレコードの優先度を書き忘れた

